# Tiltable-3D-element-using-JS

#index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Tiltable 3D element</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h1>Hello there!</h1>
        <div class="circle">
            <span></span>
            <span></span>
            <span></span>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>

#style.css
.container{
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 32rem;
    height: 20rem;
    background: linear-gradient(60deg,#8e36d6,#d61f76);
    transform: perspective(1000px);
    transform-style: preserve-3d;
    border-radius: 20px;
    box-shadow: 0 15px 40px rgba(0, 0, 0, 0,0.20),
                0 15px 12px rgba(0, 0, 0, 0.15);
    transition: all 180ms ease-out;
}

.container h1{
    color: #fff;
    font-size: 2.2rem;
    font-weight: 600;
    font-family: poppins;
    text-shadow: 0 0 22px rgba(0, 0, 0, 0.6);
    transform: translateZ(40px);
}

.circle{
    position: absolute;
    top: 1rem;
    right: 2rem;
}

.circle span{
    display: inline-flex;
    width: 0.5rem;
    height: 0.5rem;
    margin: 0 0.1rem;
    border-radius: 25px;
    background: #ffffff;
    box-shadow: 0 0 22px rgba(0, 0, 0, 0.7);
    transform: translateZ(40px);
}

#script.js
const box = document.querySelector('.container')
const boxRect = box.getBoundingClientRect()

box.addEventListener('mousemove', e => {
    const xPosition = (e.clientX - boxRect.left) / boxRect.width
    const yPosition = (e.clientY - boxRect.top) / boxRect.height - 0.6
    const xOffset = -(xPosition - 0.6)
    const dxNorm = Math.min(Math.max(xOffset, -0.6), 0.6)
    box.style.transform = `perspective(1000px)
                            rotateY(${dxNorm*45}deg)
                            rotateX(${yPosition*45}deg)`
})

box.addEventListener('mouseleave', () => {
    box.style.transform = 'none'
})
