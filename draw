<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Online Drawing Board</title>

<style>
    body {
        margin: 0;
        overflow: hidden;
        background: #f0f0f0;
    }
    #toolbar {
        position: fixed;
        top: 10px;
        left: 10px;
        background: white;
        padding: 10px;
        border-radius: 8px;
        box-shadow: 0 2px 10px rgba(0,0,0,0.2);
        display: flex;
        gap: 10px;
        z-index: 10;
    }
    canvas { display: block; }
</style>
</head>
<body>

<div id="toolbar">
    <input type="color" id="colorPicker" value="#000000">
    <input type="range" id="brushSize" min="2" max="40" value="5">
    <button id="clearBtn">Clear</button>
</div>

<canvas id="canvas"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
resizeCanvas();
window.addEventListener("resize", resizeCanvas);

let drawing = false;
let color = document.getElementById("colorPicker").value;
let brush = document.getElementById("brushSize").value;

document.getElementById("colorPicker").addEventListener("change", e => color = e.target.value);
document.getElementById("brushSize").addEventListener("change", e => brush = e.target.value);
document.getElementById("clearBtn").addEventListener("click", () => ctx.clearRect(0, 0, canvas.width, canvas.height));

function start(e) { drawing = true; draw(e); }
function stop() { drawing = false; ctx.beginPath(); }
function draw(e) {
    if (!drawing) return;
    let x = e.clientX || e.touches[0].clientX;
    let y = e.clientY || e.touches[0].clientY;
    ctx.lineWidth = brush;
    ctx.lineCap = "round";
    ctx.strokeStyle = color;
    ctx.lineTo(x, y);
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(x, y);
}

canvas.addEventListener("mousedown", start);
canvas.addEventListener("mouseup", stop);
canvas.addEventListener("mousemove", draw);

canvas.addEventListener("touchstart", start);
canvas.addEventListener("touchend", stop);
canvas.addEventListener("touchmove", draw);
</script>

</body>
</html>
