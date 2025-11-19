<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Clean Drawing Board</title>
<style>
    body, html {
        margin: 0;
        padding: 0;
        height: 100%;
        overflow: hidden;
        background: #f0f0f0;
        font-family: Arial, sans-serif;
    }
    #toolbar {
        position: fixed;
        top: 10px;
        left: 50%;
        transform: translateX(-50%);
        background: white;
        padding: 10px 15px;
        border-radius: 8px;
        box-shadow: 0 2px 10px rgba(0,0,0,0.2);
        display: flex;
        gap: 10px;
        z-index: 1000;
        align-items: center;
    }
    #toolbar button, #toolbar input[type="color"], #toolbar input[type="range"] {
        cursor: pointer;
    }
    canvas {
        display: block;
    }
</style>
</head>
<body>

<div id="toolbar">
    <input type="color" id="colorPicker" value="#000000" title="Choose Color">
    <input type="range" id="brushSize" min="2" max="40" value="5" title="Brush Size">
    <button id="eraserBtn">Eraser</button>
    <button id="clearBtn">Clear</button>
    <button id="saveBtn">Save</button>
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
let erasing = false;

document.getElementById("colorPicker").addEventListener("change", e => {
    color = e.target.value;
    erasing = false;
});
document.getElementById("brushSize").addEventListener("change", e => brush = e.target.value);
document.getElementById("eraserBtn").addEventListener("click", () => erasing = true);
document.getElementById("clearBtn").addEventListener("click", () => ctx.clearRect(0, 0, canvas.width, canvas.height));
document.getElementById("saveBtn").addEventListener("click", () => {
    const link = document.createElement('a');
    link.download = 'drawing.png';
    link.href = canvas.toDataURL();
    link.click();
});

function startDrawing(e) {
    drawing = true;
    draw(e);
}

function stopDrawing() {
    drawing = false;
    ctx.beginPath();
}

function draw(e) {
    if (!drawing) return;

    let x = e.clientX || e.touches[0].clientX;
    let y = e.clientY || e.touches[0].clientY;

    ctx.lineWidth = brush;
    ctx.lineCap = 'round';
    ctx.strokeStyle = erasing ? '#f0f0f0' : color;

    ctx.lineTo(x, y);
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(x, y);
}

canvas.addEventListener("mousedown", startDrawing);
canvas.addEventListener("mouseup", stopDrawing);
canvas.addEventListener("mousemove", draw);

canvas.addEventListener("touchstart", startDrawing);
canvas.addEventListener("touchend", stopDrawing);
canvas.addEventListener("touchmove", draw);
</script>

</body>
</html>
