<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Coin Collector</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;700&display=swap" rel="stylesheet">
<style>
  body { margin: 0; background: #f4f0df; color: #234735; font-family: "Space Grotesk", sans-serif; }
  main { max-width: 600px; margin: auto; padding: 25px 16px; animation: appear .4s; }
  h1 { font-size: clamp(32px, 7vw, 48px); margin: 0; }
  p { line-height: 1.6; }
  canvas { width: 100%; display: block; border: 4px solid #234735; box-sizing: border-box; }
  button { background: #234735; color: white; border: 0; padding: 12px 18px; margin: 12px 3px 0 0; font: inherit; cursor: pointer; }
  button:hover { background: #527448; }
  button:active { transform: scale(.95); }
  button:focus-visible { outline: 3px solid #bd7525; outline-offset: 3px; }
  #stats { font-weight: bold; }
  @keyframes appear { from { opacity: 0; } }
  @media (prefers-reduced-motion: reduce) { main { animation: none; } }
</style>
</head>
<body>
<main>
  <h1>Coin Collector</h1>
  <p>Move with arrow keys or the buttons. Collect gold coins.<br>Grey blocks stop you. Red blocks cost one life!</p>
  <p id="stats"></p>
  <canvas id="game" width="600" height="360" aria-label="Coin collecting game board"></canvas>
  <nav aria-label="Game controls">
    <button onclick="move(-1,0)" aria-label="Left">←</button>
    <button onclick="move(0,-1)" aria-label="Up">↑</button>
    <button onclick="move(0,1)" aria-label="Down">↓</button>
    <button onclick="move(1,0)" aria-label="Right">→</button>
    <button onclick="restart()">Restart</button>
  </nav>
  <p id="message" role="status">Collect all five coins to finish each level.</p>
</main>

<script>
const canvas = document.getElementById("game");
const pen = canvas.getContext("2d");
let level = 1, score = 0, lives = 3;
let x = 0, y = 0, coins = [], won = false, audio;

// Each pair is a column and row on the board.
const walls = [[3,1], [3,2], [6,3], [6,4]];
const hazards = [[5,1], [4,4], [8,2], [1,3]];

function loadLevel() {
  x = 0;
  y = 0;
  lives = 3;
  coins = [[2,0], [8,0], [1,5], [5,5], [9,5]];
  draw();
}

function draw() {
  pen.fillStyle = ["#d4e3b6", "#efd3a3", "#c0cee4"][level - 1];
  pen.fillRect(0, 0, 600, 360);

  // Draw the board grid.
  pen.strokeStyle = "#23473520";
  for (let row = 0; row < 6; row++)
    for (let col = 0; col < 10; col++)
      pen.strokeRect(col * 60, row * 60, 60, 60);

  pen.fillStyle = "#667268";
  for (const [col, row] of walls)
    pen.fillRect(col * 60 + 5, row * 60 + 5, 50, 50);

  pen.fillStyle = "#bd5143";
  for (const [col, row] of hazards.slice(0, level + 1))
    pen.fillRect(col * 60 + 10, row * 60 + 10, 40, 40);

  pen.fillStyle = "#e9ac24";
  for (const [col, row] of coins) {
    pen.beginPath();
    pen.arc(col * 60 + 30, row * 60 + 30, 13, 0, Math.PI * 2);
    pen.fill();
  }

  // Simple player sprite: green body and two eyes.
  pen.fillStyle = "#234735";
  pen.fillRect(x * 60 + 14, y * 60 + 12, 32, 36);
  pen.fillStyle = "white";
  pen.fillRect(x * 60 + 20, y * 60 + 20, 5, 5);
  pen.fillRect(x * 60 + 35, y * 60 + 20, 5, 5);

  document.getElementById("stats").textContent =
    `Level ${level}/3 • Score ${score} • Lives ${lives}`;
}

function sound(frequency) {
  const Audio = window.AudioContext || window.webkitAudioContext;
  if (!Audio) return;
  audio = audio || new Audio();
  audio.resume();
  const note = audio.createOscillator();
  const volume = audio.createGain();
  note.frequency.value = frequency;
  volume.gain.setValueAtTime(0.05, audio.currentTime);
  volume.gain.exponentialRampToValueAtTime(0.001, audio.currentTime + 0.12);
  note.connect(volume);
  volume.connect(audio.destination);
  note.start();
  note.stop(audio.currentTime + 0.12);
}

function move(dx, dy) {
  if (won) return;
  const nx = x + dx, ny = y + dy;

  if (nx < 0 || nx > 9 || ny < 0 || ny > 5) return;
  if (walls.some(([col, row]) => col === nx && row === ny)) return;

  if (hazards.slice(0, level + 1).some(([col, row]) => col === nx && row === ny)) {
    lives--;
    sound(150);
    document.getElementById("message").textContent = "Ouch! Avoid the red blocks.";
    if (lives <= 0) {
      score = (level - 1) * 50;
      loadLevel();
      document.getElementById("message").textContent = "No lives left. This level restarted!";
    }
    draw();
    return;
  }

  x = nx;
  y = ny;
  const coin = coins.findIndex(([col, row]) => col === x && row === y);
  if (coin !== -1) {
    coins.splice(coin, 1);
    score += 10;
    sound(800);
  }

  if (coins.length === 0) {
    if (level < 3) {
      level++;
      loadLevel();
      document.getElementById("message").textContent = "Next level! Watch for more red blocks.";
    } else {
      won = true;
      document.getElementById("message").textContent = "You won! All 15 coins collected!";
    }
  }
  draw();
}

function restart() {
  level = 1;
  score = 0;
  won = false;
  loadLevel();
  document.getElementById("message").textContent = "Collect all five coins to finish each level.";
}

document.addEventListener("keydown", function(event) {
  const directions = { ArrowLeft: [-1,0], ArrowRight: [1,0], ArrowUp: [0,-1], ArrowDown: [0,1] };
  if (directions[event.key]) {
    event.preventDefault();
    move(...directions[event.key]);
  }
});

loadLevel();
</script>
</body>
</html>
