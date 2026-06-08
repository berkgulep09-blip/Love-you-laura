<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>I Love You Laura ❤️</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    overflow:hidden;
    background:black;
    font-family:Arial,sans-serif;
}

canvas{
    position:fixed;
    inset:0;
}

.centerText{
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
    text-align:center;
    color:#ffb6d9;
    text-shadow:
        0 0 10px #fff,
        0 0 20px #ff7eb8,
        0 0 40px #ff7eb8,
        0 0 60px #ff7eb8;
    z-index:10;
    animation:pulse 2s infinite alternate;
}

.centerText h1{
    font-size:70px;
    letter-spacing:5px;
}

.centerText h2{
    font-size:50px;
    margin-top:10px;
}

@keyframes pulse{
    from{
        transform:translate(-50%,-50%) scale(1);
    }
    to{
        transform:translate(-50%,-50%) scale(1.08);
    }
}
</style>
</head>
<body>

<div class="centerText">
    <h1>I LOVE YOU</h1>
    <h2>LAURA ❤️</h2>
</div>

<canvas id="canvas"></canvas>

<script>

const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

function resize(){
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
resize();
window.addEventListener("resize",resize);

let time = 0;

function heart(t){
    return{
        x:16*Math.pow(Math.sin(t),3),
        y:13*Math.cos(t)
        -5*Math.cos(2*t)
        -2*Math.cos(3*t)
        -Math.cos(4*t)
    };
}

function animate(){

    time += 0.02;

    ctx.fillStyle = "rgba(0,0,0,0.08)";
    ctx.fillRect(0,0,canvas.width,canvas.height);

    const scale = 22 + Math.sin(time*2)*2;

    for(let i=0;i<90;i++){

        const t = (Math.PI*2*i/90)+time;

        const p = heart(t);

        let x = p.x*scale;
        let y = p.y*scale;

        const rot = time*0.4;

        const rx =
            x*Math.cos(rot) -
            y*Math.sin(rot);

        const ry =
            x*Math.sin(rot) +
            y*Math.cos(rot);

        const px = canvas.width/2 + rx;
        const py = canvas.height/2 - ry;

        ctx.save();

        ctx.translate(px,py);

        ctx.rotate(t);

        ctx.font = "14px Arial";

        ctx.shadowBlur = 20;
        ctx.shadowColor = "#ff7eb8";

        ctx.fillStyle = "#ff9ecf";

        ctx.fillText("Laura ❤️",0,0);

        ctx.restore();
    }

    requestAnimationFrame(animate);
}

animate();

</script>

</body>
</html>
