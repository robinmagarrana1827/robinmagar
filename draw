<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Doodle & Note Board</title>
<style>
    body, html {
        margin: 0;
        padding: 0;
        height: 100%;
        overflow: hidden;
        background: #f0f0f0;
        font-family: Arial, sans-serif;
        user-select: none;
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
    .note {
        position: absolute;
        background: yellow;
        padding: 5px 10px;
        border-radius: 5px;
        cursor: move;
        font-size: 16px;
        box-shadow: 0 1px 5px rgba(0,0,0,0.3);
        user-select: text;
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
    <button id="addNoteBtn">Add Note</button>
</div>

<canvas id="canvas"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

// Resize canvas
function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
resizeCanvas();
window.addEventListener("resize", resizeCanvas);

// Drawing state
let drawing = false;
let color = document.getElementById("colorPicker").value;
let brush = document.getElementById("brushSize").value;
let erasing = false;

// Toolbar events
document.getElementById("colorPicker").addEventListener("change", e => {
    color = e.target.value;
    erasing = false;
});
document.getElementById("brushSize").addEventListener("change", e => brush = e.target.value);
document.getElementById("eraserBtn").addEventListener("click", () => erasing = true);
document.getElementById("clearBtn").addEventListener("click", () => {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    document.querySelectorAll('.note').forEach(n => n.remove());
});
document.getElementById("saveBtn").addEventListener("click", () => {
    // Hide notes temporarily
    const notes = document.querySelectorAll('.note');
    notes.forEach(n => n.style.display = 'none');

    // Save canvas
    const link = document.createElement('a');
    link.download = 'doodle_note.png';
    link.href = canvas.toDataURL();
    link.click();

    // Show notes again
    notes.forEach(n => n.style.display = 'block');
});

// Drawing functions
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
    const rect = canvas.getBoundingClientRect();
    let x, y;
    if (e.touches) {
        x = e.touches[0].clientX - rect.left;
        y = e.touches[0].clientY - rect.top;
    } else {
        x = e.clientX - rect.left;
        y = e.clientY - rect.top;
    }

    ctx.lineWidth = brush;
    ctx.lineCap = 'round';
    ctx.strokeStyle = erasing ? '#f0f0f0' : color;

    ctx.lineTo(x, y);
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(x, y);
}

// Mouse events
canvas.addEventListener("mousedown", startDrawing);
canvas.addEventListener("mouseup", stopDrawing);
canvas.addEventListener("mousemove", draw);

// Touch events
canvas.addEventListener("touchstart", startDrawing);
canvas.addEventListener("touchend", stopDrawing);
canvas.addEventListener("touchmove", draw);

// Add Note feature
document.getElementById("addNoteBtn").addEventListener("click", () => {
    const text = prompt("Enter your note:");
    if (!text) return;

    const note = document.createElement('div');
    note.className = 'note';
    note.textContent = text;
    note.style.left = '50px';
    note.style.top = '50px';
    document.body.appendChild(note);

    // Dragging
    let offsetX, offsetY, isDragging = false;
    note.addEventListener('mousedown', e => {
        isDragging = true;
        offsetX = e.offsetX;
        offsetY = e.offsetY;
        note.style.zIndex = 1001;
    });
    document.addEventListener('mousemove', e => {
        if (!isDragging) return;
        note.style.left = (e.clientX - offsetX) + 'px';
        note.style.top = (e.clientY - offsetY) + 'px';
    });
    document.addEventListener('mouseup', e => {
        isDragging = false;
        note.style.zIndex = 1000;
    });

    // Touch dragging
    note.addEventListener('touchstart', e => {
        isDragging = true;
        const touch = e.touches[0];
        const rect = note.getBoundingClientRect();
        offsetX = touch.clientX - rect.left;
        offsetY = touch.clientY - rect.top;
        note.style.zIndex = 1001;
        e.preventDefault();
    });
    document.addEventListener('touchmove', e => {
        if (!isDragging) return;
        const touch = e.touches[0];
        note.style.left = (touch.clientX - offsetX) + 'px';
        note.style.top = (touch.clientY - offsetY) + 'px';
    });
    document.addEventListener('touchend', e => {
        isDragging = false;
        note.style.zIndex = 1000;
    });
});
</script>

</body>
</html>
