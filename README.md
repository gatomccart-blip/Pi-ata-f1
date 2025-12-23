# Pi-ñata-f1
Piñata the Racing crew
<!DOCTYPE html><html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Piñata F1 Interactiva</title>
  <style>
    body {
      margin: 0;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      background: radial-gradient(circle at top, #ffcc00, #e10600);
      font-family: system-ui, sans-serif;
      overflow: hidden;
    }h1 { margin: 10px 0; color: #111; }

#counter { font-size: 18px; margin-bottom: 10px; }

#scene {
  position: relative;
  width: 320px;
  height: 220px;
}

.pinata {
  position: absolute;
  top: 60px;
  left: 10px;
  width: 300px;
  height: 80px;
  background: linear-gradient(90deg, #e10600, #ff3b3b);
  border-radius: 20px 80px 80px 20px;
  box-shadow: inset -10px 0 0 rgba(0,0,0,.25);
  transition: transform .15s;
}

.nose {
  position: absolute;
  right: -45px;
  top: 25px;
  width: 70px;
  height: 30px;
  background: #222;
  border-radius: 10px;
}

.wing {
  position: absolute;
  left: -20px;
  top: 10px;
  width: 20px;
  height: 60px;
  background: #111;
  border-radius: 6px;
}

.wheel {
  position: absolute;
  bottom: -22px;
  width: 42px;
  height: 42px;
  background: #000;
  border-radius: 50%;
}

.wheel.left { left: 50px; }
.wheel.right { right: 50px; }

.shake { transform: rotate(-6deg); }

.candy {
  position: absolute;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  animation: fall 1.3s forwards;
}

@keyframes fall {
  from { transform: translateY(0) scale(1); opacity: 1; }
  to { transform: translateY(160px) scale(.3); opacity: 0; }
}

button {
  margin-top: 16px;
  padding: 14px 28px;
  font-size: 18px;
  border: none;
  border-radius: 16px;
  background: #111;
  color: #fff;
  cursor: pointer;
}

button:active { transform: scale(.95); }

#message {
  margin-top: 8px;
  font-weight: bold;
  color: #111;
}

  </style>
</head>
<body>
  <h1>Piñata F1 🏎️</h1>
  <div id="counter">Golpes: 0 / 3</div>  <div id="scene">
    <div id="pinata" class="pinata">
      <div class="wing"></div>
      <div class="nose"></div>
      <div class="wheel left"></div>
      <div class="wheel right"></div>
    </div>
  </div><button id="hitBtn">Golpear piñata</button>

  <div id="message"></div>  <!-- Sonidos --><audio id="hitSound" src="https://assets.mixkit.co/active_storage/sfx/2568/2568-preview.mp3"></audio> <audio id="breakSound" src="https://assets.mixkit.co/active_storage/sfx/2707/2707-preview.mp3"></audio>

  <script>
    const pinata = document.getElementById('pinata');
    const scene = document.getElementById('scene');
    const btn = document.getElementById('hitBtn');
    const counter = document.getElementById('counter');
    const message = document.getElementById('message');

    const hitSound = document.getElementById('hitSound');
    const breakSound = document.getElementById('breakSound');

    let hits = 0;
    const maxHits = 3;

    btn.addEventListener('click', hit);
    pinata.addEventListener('click', hit);

    function hit() {
      hits++;
      hitSound.currentTime = 0;
      hitSound.play();

      pinata.classList.add('shake');
      setTimeout(() => pinata.classList.remove('shake'), 150);

      counter.textContent = `Golpes: ${hits} / ${maxHits}`;

      if (hits >= maxHits) {
        breakPinata();
        hits = 0;
      }
    }

    function breakPinata() {
      breakSound.play();
      pinata.style.display = 'none';
      message.textContent = '¡Piñata rota! 🎉🍬';

      for (let i = 0; i < 20; i++) {
        const candy = document.createElement('div');
        candy.className = 'candy';
        candy.style.left = Math.random() * 300 + 'px';
        candy.style.top = '90px';
        candy.style.background = `hsl(${Math.random()*360}, 85%, 60%)`;
        scene.appendChild(candy);
        setTimeout(() => candy.remove(), 1300);
      }

      setTimeout(() => {
        pinata.style.display = 'block';
        message.textContent = '¡Lista otra vez!';
        counter.textContent = `Golpes: 0 / ${maxHits}`;
      }, 1700);
    }
  </script></body>
</html>
