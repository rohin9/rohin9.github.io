<html lang="en">
<head>
  <meta charset="UTF-8">
  <style>
    * {
      box-sizing: border-box;
      font-family: 'Comic Sans MS', 'Segoe UI', cursive;
    }

    body {
      margin: 0;
      height: 100vh;
      background: #ffd6e8;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
    }

    .container {
      text-align: center;
      z-index: 2;
    }

    h1 {
      font-size: 3rem;
      color: #b30059;
      margin-bottom: 40px;
      margin-top: -120px; /* moves text higher */
    }

    .buttons {
      position: relative;
      width: 320px;
      height: 220px;
      margin: 0 auto;
    }

    button {
      font-size: 1.5rem;
      padding: 15px 35px;
      border-radius: 50px;
      border: none;
      cursor: pointer;
      position: absolute;
      transition:
        transform 0.35s cubic-bezier(.34,1.56,.64,1),
        left 0.25s ease,
        top 0.25s ease;
      white-space: nowrap;
    }

    #yesBtn {
      background-color: #ff4d6d;
      color: white;
      left: 50%;
      transform: translateX(-50%) scale(1);
    }

    #noBtn {
      background-color: white;
      color: #b30059;
      border: 2px solid #ff4d6d;
      left: 50%;
      top: 90px;
      transform: translateX(-50%);
    }

    /* Floating hearts */
    .heart {
      position: absolute;
      bottom: -20px;
      color: #ff4d6d;
      animation: floatUp linear infinite;
      opacity: 0.8;
      pointer-events: none;
    }

    @keyframes floatUp {
      from {
        transform: translateY(0) rotate(0deg);
        opacity: 1;
      }
      to {
        transform: translateY(-110vh) rotate(360deg);
        opacity: 0;
      }
    }
  </style>
</head>
<body>

<div class="container">
  <h1>Madi, will you be my Valentine? 💘</h1>
  <div class="buttons">
<br>
    <button id="yesBtn">Yes 💕</button>
<br>
    <button id="noBtn">No 😔</button>
  </div>
</div>

<script>
  const noBtn = document.getElementById("noBtn");
  const yesBtn = document.getElementById("yesBtn");
  const container = document.querySelector(".buttons");

  let hoverCount = 0;
  let currentScale = 1;

  const scales = [1, 1.5, 2, 3];
  const texts = ["Yes 💕", "Yes! 💖", "YES! 💖", "YES!! 💖💘"];

  // Move NO button on hover
  noBtn.addEventListener("mouseover", (e) => {
    const containerRect = container.getBoundingClientRect();
    const mouseX = e.clientX;
    const mouseY = e.clientY;

    const moveDistance = 200;
    const angle = Math.random() * 2 * Math.PI;
    const dx = moveDistance * Math.cos(angle);
    const dy = moveDistance * Math.sin(angle);

    let newX = mouseX - containerRect.left - noBtn.offsetWidth / 2 + dx;
    let newY = mouseY - containerRect.top - noBtn.offsetHeight / 2 + dy;

    // Keep inside container
    newX = Math.max(0, Math.min(container.offsetWidth - noBtn.offsetWidth, newX));
    newY = Math.max(0, Math.min(container.offsetHeight - noBtn.offsetHeight, newY));

    noBtn.style.left = `${newX}px`;
    noBtn.style.top = `${newY}px`;

    // Grow YES button safely
    if (hoverCount < scales.length) {
      yesBtn.style.transform = `translateX(-50%) scale(${scales[hoverCount]})`;
      yesBtn.textContent = texts[hoverCount];
      hoverCount++;
    }
  });

  // Alert if NO is clicked
  noBtn.addEventListener("click", () => {
    alert("I think you meant to click the other button 😭💔");
  });

  // YES click: GIF + celebration
  yesBtn.addEventListener("click", () => {
    document.body.innerHTML = `
      <div style="
        height:100vh;
        display:flex;
        flex-direction:column;
        justify-content:center;
        align-items:center;
        background:#ffd6e8;
        color:#b30059;
        text-align:center;
        gap:20px;
      ">
        <img 
          src="https://media1.tenor.com/m/_NMzaxfKAJYAAAAC/excited-dog.gif"
          alt="Happy Valentine GIF"
          style="max-width:300px; width:80%; border-radius:20px;"
        />
        <div style="font-size:3rem;">
          I knew you'd say yes!<br>💖💖💖
        </div>
        (I love you and can't wait to see you soon 😍🤤🥰)
      </div>
    `;
    startCelebrationHearts();
  });

  // Floating hearts for main page
  function createHeart() {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "❤️";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.fontSize = Math.random() * 20 + 20 + "px";
    heart.style.animationDuration = Math.random() * 3 + 4 + "s";
    document.body.appendChild(heart);
    setTimeout(() => heart.remove(), 7000);
  }
  setInterval(createHeart, 300);

  // Celebration hearts on YES page
  function startCelebrationHearts() {
    setInterval(() => {
      const heart = document.createElement("div");
      heart.innerHTML = Math.random() > 0.5 ? "❤️" : "💖";
      heart.style.position = "absolute";
      heart.style.left = Math.random() * 100 + "vw";
      heart.style.bottom = "-20px";
      heart.style.fontSize = Math.random() * 30 + 30 + "px";
      heart.style.animation = "floatUp 3s linear forwards";
      heart.style.opacity = "0.9";
      heart.style.pointerEvents = "none";
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 3000);
    }, 120);
  }
</script>

</body>
</html>
