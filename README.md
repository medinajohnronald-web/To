
<html>
<head>
  <title>Birthday Greeting</title>
  <style>
    body {
      font-family: "Poppins", sans-serif;
      text-align: center;
      margin: 0;
      padding: 0;
      height: 100vh;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4, #fbc2eb);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      overflow: hidden;
    }

    h2 {
      color: #333;
      margin-bottom: 20px;
    }

    input {
      padding: 10px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      width: 200px;
      outline: none;
    }

    button {
      padding: 10px 20px;
      margin-left: 10px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      background: #ff6f61;
      color: white;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: #e55b50;
    }

    #birthdayMessage {
      font-size: 3em;
      font-weight: bold;
      color: #fff;
      text-shadow: 2px 2px 5px #000;
      display: none;
      animation: pop 0.6s ease;
    }

    @keyframes pop {
      0% { transform: scale(0.5); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
    }
  </style>
</head>
<body>
  <h2 id="title">Enter Your Name</h2>

  <form id="form">
    <input type="text" id="nameInput" placeholder="Your name" required>
    <button type="submit">Submit</button>
  </form>

  <h1 id="birthdayMessage"></h1>
  <canvas id="confetti"></canvas>

  <script>
    const form = document.getElementById("form");
    const message = document.getElementById("birthdayMessage");
    const title = document.getElementById("title");

    form.addEventListener("submit", function(event) {
      event.preventDefault();
      const name = document.getElementById("nameInput").value;

      form.style.display = "none";
      title.style.display = "none";

      message.textContent = "🎉 HAPPY BIRTHDAY " + name + "! 🎂";
      message.style.display = "block";

      startConfetti();
    });

    // Confetti effect
    const canvas = document.getElementById("confetti");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const confettiParticles = [];
    const colors = ["#f94144","#f3722c","#f8961e","#f9c74f","#90be6d","#43aa8b","#577590"];

    function ConfettiParticle() {
      this.x = Math.random() * canvas.width;
      this.y = Math.random() * canvas.height - canvas.height;
      this.size = Math.random() * 8 + 5;
      this.color = colors[Math.floor(Math.random() * colors.length)];
      this.speed = Math.random() * 3 + 2;
      this.tilt = Math.random() * 10 - 5;

      this.update = function() {
        this.y += this.speed;
        this.x += this.tilt * 0.1;
        if (this.y > canvas.height) {
          this.y = -10;
          this.x = Math.random() * canvas.width;
        }
      };

      this.draw = function() {
        ctx.beginPath();
        ctx.fillStyle = this.color;
        ctx.fillRect(this.x, this.y, this.size, this.size);
        ctx.fill();
      };
    }

    function startConfetti() {
      for (let i = 0; i < 150; i++) {
        confettiParticles.push(new ConfettiParticle());
      }
      animateConfetti();
    }

    function animateConfetti() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (let i = 0; i < confettiParticles.length; i++) {
        confettiParticles[i].update();
        confettiParticles[i].draw();
      }
      requestAnimationFrame(animateConfetti);
    }
  </script>
</body>
</html>
