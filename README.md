<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="stopwatch">
        <div id="display">00:00:00</div>
        <button id="startStop">Start</button>
        <button id="reset">Reset</button>
    </div>
    <script src="script.js"></script>
</body>
</html>
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
    margin: 0;
    font-family: Arial, sans-serif;
}

.stopwatch {
    text-align: center;
    background: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

#display {
    font-size: 3em;
    margin-bottom: 20px;
}

button {
    font-size: 1em;
    padding: 10px 20px;
    margin: 5px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button#startStop {
    background-color: #28a745;
    color: white;
}

button#reset {
    background-color: #dc3545;
    color: white;
}
let startStopButton = document.getElementById('startStop');
let resetButton = document.getElementById('reset');
let display = document.getElementById('display');

let timer;
let isRunning = false;
let elapsedTime = 0;

function updateDisplay() {
    let hours = Math.floor(elapsedTime / 3600);
    let minutes = Math.floor((elapsedTime % 3600) / 60);
    let seconds = elapsedTime % 60;

    display.textContent = 
        String(hours).padStart(2, '0') + ':' + 
        String(minutes).padStart(2, '0') + ':' + 
        String(seconds).padStart(2, '0');
}

function startStop() {
    if (isRunning) {
        clearInterval(timer);
        startStopButton.textContent = 'Start';
    } else {
        timer = setInterval(() => {
            elapsedTime++;
            updateDisplay();
        }, 1000);
        startStopButton.textContent = 'Stop';
    }
    isRunning = !isRunning;
}

function reset() {
    clearInterval(timer);
    isRunning = false;
    elapsedTime = 0;
    updateDisplay();
    startStopButton.textContent = 'Start';
}

startStopButton.addEventListener('click', startStop);
resetButton.addEventListener('click', reset);

updateDisplay();
