const canvas = document.getElementById('pixelCanvas');
const ctx = canvas.getContext('2d');
const colorPicker = document.getElementById('colorPicker');
const clearButton = document.getElementById('clearButton');
const gridSizeInput = document.getElementById('gridSize');
const gridSizeButton = document.getElementById('gridSizeButton');

// Initial grid size
let gridSize = 16; 
let pixelSize = 20; // Adjust pixel size as needed

// Set default drawing color
let currentColor = '#000000';
colorPicker.addEventListener('change', (event) => {
  currentColor = event.target.value;
});

// Clear canvas function
clearButton.addEventListener('click', () => {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
});

// Change grid size function
gridSizeButton.addEventListener('click', () => {
  gridSize = parseInt(gridSizeInput.value, 10);
  if (gridSize > 0) {
    createGrid(gridSize);
  } else {
    alert('Please enter a valid grid size.');
  }
});

// Create the initial grid
createGrid(gridSize);

// Draw pixel function
function drawPixel(x, y) {
  ctx.fillStyle = currentColor;
  ctx.fillRect(x * pixelSize, y * pixelSize, pixelSize, pixelSize);
}

// Handle mouse clicks to draw pixels
canvas.addEventListener('click', (event) => {
  // Get mouse coordinates relative to canvas
  const x = Math.floor(event.offsetX / pixelSize);
  const y = Math.floor(event.offsetY / pixelSize);

  // Draw a pixel
  drawPixel(x, y);
});

// Function to create the grid
function createGrid(size) {
  canvas.width = size * pixelSize;
  canvas.height = size * pixelSize;
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Draw grid lines (optional)
  ctx.strokeStyle = '#ccc'; 
  for (let i = 0; i <= size; i++) {
    ctx.beginPath();
    ctx.moveTo(i * pixelSize, 0);
    ctx.lineTo(i * pixelSize, canvas.height);
    ctx.stroke();

    ctx.beginPath();
    ctx.moveTo(0, i * pixelSize);
    ctx.lineTo(canvas.width, i * pixelSize);
    ctx.stroke();
  }
}

<!DOCTYPE html>
<html>
<head>
  <title>Pixel Art Editor</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Pixel Art Editor</h1>

  <div id="controls">
    <label for="colorPicker">Color:</label>
    <input type="color" id="colorPicker" value="#000000">
    <button id="clearButton">Clear</button>
    <label for="gridSize">Grid Size:</label>
    <input type="number" id="gridSize" min="1" value="16">
    <button id="gridSizeButton">Set Grid</button>
  </div>

  <canvas id="pixelCanvas" width="500" height="500"></canvas>

  <script src="script.js"></script>
</body>
</html>

body {
  font-family: sans-serif;
  margin: 0;
  padding: 0;
}

#controls {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

#pixelCanvas {
  border: 1px solid black;
}

