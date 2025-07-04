<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Will You Be Mine AFRUU?</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://fonts.googleapis.com/css2?family=Pacifico&display=swap"
      rel="stylesheet"
    />
    <style>
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }
      body {
        font-family: "Pacifico", cursive;
        background: #0d0d0d;
        overflow-x: hidden;
        color: white;
      }

      .step {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        padding: 60px 20px 40px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: flex-start;
        text-align: center;
        opacity: 0;
        transition: opacity 1s ease-in-out;
        z-index: 1;
      }

      .step.active {
        opacity: 1;
        z-index: 2;
      }

      h1 {
        color: #ff0033;
        font-size: 2.4em;
        margin-bottom: 15px;
      }

      p {
        color: #e0e0e0;
        font-size: 1.1em;
        margin-bottom: 25px;
        max-width: 90%;
      }

      .sticker {
        width: 150px;
        height: 150px; /* 💡 force square */
        max-width: 80%;
        margin-bottom: 20px;
        animation: bounce 2s infinite;
        border-radius: 50%;
        border: 4px solid #ff004f;
        box-shadow: 0 0 12px #ff004f;
        object-fit: cover;
      }

      @keyframes bounce {
        0%,
        100% {
          transform: translateY(0);
        }
        50% {
          transform: translateY(-10px);
        }
      }

      .glow-btn {
        padding: 12px 30px;
        border: none;
        border-radius: 30px;
        background: #ff004f;
        color: #fff;
        font-size: 1.1em;
        font-family: "Pacifico", cursive;
        cursor: pointer;
        position: relative;
        overflow: hidden;
        transition: transform 0.3s ease;
      }

      .glow-btn::before {
        content: "";
        position: absolute;
        top: -50%;
        left: -50%;
        width: 200%;
        height: 200%;
        background: radial-gradient(
          circle,
          rgba(255, 0, 76, 0.7) 10%,
          transparent 70%
        );
        animation: pulse 2s infinite;
        z-index: 0;
      }

      .glow-btn span {
        position: relative;
        z-index: 1;
      }

      .glow-btn:hover {
        transform: scale(1.05);
      }

      @keyframes pulse {
        0% {
          transform: scale(1);
          opacity: 1;
        }
        100% {
          transform: scale(1.4);
          opacity: 0;
        }
      }

      .game-boxes {
        display: flex;
        gap: 15px;
        flex-wrap: wrap;
        justify-content: center;
        margin-top: 20px;
      }

      .gift {
        width: 100px;
        height: 100px;
        background: url("https://cdn-icons-png.flaticon.com/512/7641/7641727.png")
          center/cover no-repeat;
        background-color: #1a1a1a;
        border: 3px solid #ff0033;
        border-radius: 15px;
        cursor: pointer;
        transition: transform 0.3s;
      }

      .gift:hover {
        transform: scale(1.1);
      }

      .hearts {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: 0;
      }

      .heart {
        width: 20px;
        height: 20px;
        background: red;
        position: absolute;
        transform: rotate(45deg);
        animation: float 6s linear infinite;
      }

      .heart::before,
      .heart::after {
        content: "";
        width: 20px;
        height: 20px;
        background: red;
        border-radius: 50%;
        position: absolute;
      }

      .heart::before {
        top: -10px;
        left: 0;
      }
      .heart::after {
        left: -10px;
        top: 0;
      }

      @keyframes float {
        0% {
          transform: translateY(100vh) rotate(45deg);
          opacity: 1;
        }
        100% {
          transform: translateY(-10vh) rotate(45deg);
          opacity: 0;
        }
      }

      #popup {
        display: none;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.85);
        backdrop-filter: blur(6px);
        z-index: 9999;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        text-align: center;
        animation: scaleUp 0.6s ease forwards;
      }

      #popup.show {
        display: flex;
      }

      #popup h1 {
        font-size: 2.5em;
        color: #ff0033;
        margin-bottom: 10px;
      }

      @keyframes scaleUp {
        from {
          transform: scale(0.6);
          opacity: 0;
        }
        to {
          transform: scale(1);
          opacity: 1;
        }
      }

      @media screen and (max-width: 600px) {
        .sticker {
          width: 120px;
          height: 120px;
        }
        h1 {
          font-size: 1.8em;
        }
        p {
          font-size: 1em;
        }
        .glow-btn {
          font-size: 1em;
          padding: 10px 20px;
        }
      }
    </style>
  </head>
  <body>
    <div class="hearts" id="hearts"></div>
    <audio id="bgMusic" autoplay loop>
      <source
        src="https://cdn.pixabay.com/audio/2023/04/11/audio_6c9cc12c61.mp3"
        type="audio/mpeg"
      />
    </audio>

    <!-- Step 1 -->
    <div class="step active" id="step1">
      <img
        class="sticker"
        src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExYzZha2NrejRoZGpyN21pdms1OWZlbHpkYmNmbmVzdjgwbDRuaTBzcSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/l0MYsxZiDtc1wPHmU/giphy.gif"
        alt="bear blowing kiss"
      />
      <h1>I have a little secret…</h1>
      <p>It’s been on my heart for a while now 💌</p>
      <button class="glow-btn" onclick="nextStep(2)">
        <span>Tell Me</span>
      </button>
    </div>

    <!-- Step 2 -->
    <div class="step" id="step2">
      <img
        class="sticker"
        src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExbG5ka3IxNHV6NzQ3bTkyZ3hnbHgwM3J3bmVieDhiNTdoYm8wZHIwMSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ewzF6uunnPn6L5amuW/giphy.gif"
        alt="hearts bear"
      />
      <h1>You light up my life AFRUU 🌟</h1>
      <p>Your smile, your soul, the way you laugh — it’s all magic to me.</p>
      <button class="glow-btn" onclick="nextStep(3)">
        <span>Okay… ☺️</span>
      </button>
    </div>

    <!-- Step 3 -->
    <div class="step" id="step3">
      <img
        class="sticker"
        src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExdDMyN25wcDlyajI0NjRkNmZicThxZXNlY3RjczE3b21vaDF5cDB2NCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/l0HlO3BJ8LALPW4sE/giphy.gif"
        alt="gift bear"
      />
      <h1>Let’s play a game 🎁</h1>
      <p>One of these boxes holds the real surprise. Choose wisely 😜</p>
      <div class="game-boxes">
        <div class="gift" onclick="checkGift(1)"></div>
        <div class="gift" onclick="checkGift(2)"></div>
        <div class="gift" onclick="checkGift(3)"></div>
      </div>
    </div>

    <!-- Step 4 -->
    <div class="step" id="step4">
      <img
        class="sticker"
        src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExYWxkNzNpcDRhNjR1aDhoNTlxZmJ3OTRhbXBuN3Zxa3R0ZjJ0ZW5saSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/XODYgwdnFvgqxOsNW1/giphy.gif"
        alt="hugging bears"
      />
      <h1>Before You Say YES… 🥹</h1>
      <p>
         I promise to laugh with you, protect you, and cherish every second with
        you and i will make you mine bby💖
      </p>
      <button class="glow-btn" onclick="nextStep(5)">
        <span>That’s Sweet…</span>
      </button>
    </div>

    <!-- Step 5 -->
    <div class="step" id="step5">
      <img
        class="sticker"
        src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExdzlhNzRtaXJ4OHhhYWlxZGwwcXRyNzlsYW5zamt5aW0zajMwbHZpNiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/KyCS9bVWntiutYBlh5/giphy.gif"
        alt="hugging bears"
      />
      <h1>Will You Be Mine afruu? 💍</h1>
      <p>Say YES, and let’s grow together and make our each other life beautiful and shunshine 🌹</p>
      <button class="glow-btn" onclick="showLovePopup()">
        <span>YES 💕</span>
      </button>
    </div>

    <!-- Final Popup -->
    <div id="popup">
      <img
        class="sticker"
        src="https://media4.giphy.com/media/Vz58J8shFW6BvqnYTm/giphy.gif"
        alt="hugging bears"
      />
      <h1>Yaaay! 💖</h1>
      <p>You made my world complete AFIM meri jaan 🌍💘</p>
    </div>

    <script>
      function nextStep(n) {
        document
          .querySelectorAll(".step")
          .forEach((s) => s.classList.remove("active"));
        document.getElementById("step" + n).classList.add("active");
      }

      function checkGift(num) {
        if (num === 2) {
          nextStep(4);
        } else {
          alert("Oops! Try again, love 💌");
        }
      }

      function showLovePopup() {
        document.getElementById("popup").classList.add("show");
      }

      const heartsContainer = document.getElementById("hearts");
      setInterval(() => {
        const heart = document.createElement("div");
        heart.className = "heart";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.animationDuration = 3 + Math.random() * 2 + "s";
        heartsContainer.appendChild(heart);
        setTimeout(() => heart.remove(), 6000);
      }, 150);
    </script>
    <!-- Confetti Script -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <script>
      function showLovePopup() {
        document.getElementById("popup").classList.add("show");

        // 🎉 Fire confetti
        confetti({
          particleCount: 250,
          spread: 80,
          origin: { y: 0.7 },
        });
      }
    </script>
  </body>
</html>
