
<!DOCTYPE html>
<html>
<head>
  <title>Valentine?</title>

  <!-- Confetti -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

  <style>
    body {
      background: #ffe6ea;
      font-family: Arial, sans-serif;
      text-align: center;
      padding-top: 40px;
      overflow: hidden;
      margin: 0;
    }

    h1 {
      color: black;
      margin-bottom: 30px;
    }

    .options {
      display: flex;
      justify-content: center;
      gap: 40px;
      flex-wrap: wrap;
      margin-top: 20px;
    }

    .cat, .btn {
      width: 160px;
      cursor: pointer;
      transition: transform 0.3s;
      background: white;
      border: none;
      padding: 12px;
      border-radius: 20px;
      font-size: 16px;
    }

    .cat:hover, .btn:hover {
      transform: scale(1.1);
    }

    #message {
      margin-top: 30px;
      font-size: 20px;
      color: black;
      font-weight: bold;
      padding: 0 25px;
      line-height: 1.6;
    }

    /* Floating hearts */
    .heart {
      position: fixed;
      bottom: -20px;
      font-size: 24px;
      animation: floatUp 6s linear infinite;
      opacity: 0.8;
      pointer-events: none;
    }

    @keyframes floatUp {
      0% { transform: translateY(0) scale(1); opacity: 0.8; }
      100% { transform: translateY(-100vh) scale(1.5); opacity: 0; }
    }

    /* Gallery */
    .gallery {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: #ffe6ea;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 10;
    }

    .slide {
      width: 230px;
      border-radius: 15px;
      opacity: 0;
      transform: scale(0.8);
      transition: all 1.5s ease;
      position: absolute;
    }

    .slide.show {
      opacity: 1;
      transform: scale(1);
    }
  </style>
</head>

<body>

<h1 id="question">Will you be my Valentine?</h1>

<div class="options" id="options">
  <img src="yes-cat.png" class="cat" onclick="yesClick()">
  <img src="no-cat.png" class="cat" onclick="noFirstClick()">
</div>

<div id="message"></div>

<!-- Gallery -->
<div id="gallery" class="gallery" style="display:none;">
  <img src="pic1.jpg" class="slide" id="slide1">
  <img src="pic2.jpg" class="slide" id="slide2">
  <img src="pic3.jpg" class="slide" id="slide3">
  <img src="pic4.jpg" class="slide" id="slide4">
  <img src="pic5.jpg" class="slide" id="slide5">
</div>

<!-- Audio -->
<audio id="loveSong" src="song.mp3"></audio>
<audio id="happyCat" src="happy-cat.mp3"></audio>

<script>
function yesClick() {
  document.getElementById("question").innerText = "First riddle 😼";
  document.getElementById("options").innerHTML = `
    <input type="text" id="riddleInput" placeholder="Type your answer"
      style="padding:12px;border-radius:12px;border:none;font-size:16px;width:200px;text-align:center;">
    <br><br>
    <button class="btn" onclick="checkRiddle()">Submit</button>
  `;
  document.getElementById("message").innerText =
    "Ke kherhaaa laadle _____ hum bhi rakhe hh!!";
}

function checkRiddle() {
  const answer = document.getElementById("riddleInput").value
    .trim()
    .toLowerCase();

  if (answer === "asla") {
    document.getElementById("happyCat").play();
    secondStep();
  } else {
    document.getElementById("message").innerText =
      "Galat 😼 soch ache se… laadle!";
  }
}

function secondStep() {
  document.getElementById("question").innerText = "Second riddle 😼";
  document.getElementById("options").innerHTML = `
    <input type="text" id="riddle2Input" placeholder="Type your answer"
      style="padding:12px;border-radius:12px;border:none;font-size:16px;width:200px;text-align:center;">
    <br><br>
    <button class="btn" onclick="checkSecondRiddle()">Submit</button>
  `;
  document.getElementById("message").innerText =
    "Fill ups!! ____ daal";
}

function checkSecondRiddle() {
  const answer = document.getElementById("riddle2Input").value
    .trim()
    .toLowerCase();

  if (answer === "chana") {
    document.getElementById("happyCat").play();
    finalSurprise();
  } else {
    document.getElementById("message").innerText =
      "Hehe galat 😏 soch phir se!";
  }
}

function finalSurprise() {
  document.getElementById("loveSong").play();

  confetti({
    particleCount: 180,
    spread: 90,
    origin: { y: 0.6 }
  });

  startHearts();

  document.getElementById("question").innerText = "YAY! 💖";
  document.getElementById("options").innerHTML = `
    <button class="btn" onclick="beMine()">Be mine 💌</button>
  `;

  document.getElementById("message").innerText =
    "Hie so this might a little yk whatever!! Thank u so muvhhhhh bbu for always being there legit I don't have words to explain what I feel for u!! Man u came in my life so unexpectedly and then just ended up becoming my favrt PART! lobhhhhh youu Mwah 💋";

  document.getElementById("gallery").style.display = "flex";
  startSlideshow();
}

function beMine() {
  confetti({
    particleCount: 250,
    spread: 120,
    origin: { y: 0.5 }
  });

  document.getElementById("question").innerText = "Forever mine 💖";
  document.getElementById("options").innerHTML = "";
  document.getElementById("message").innerText =
    "No riddles left now… just us 💞";
}

function noFirstClick() {
  document.getElementById("question").innerText = "Are you sure? 🥺";
  document.getElementById("options").innerHTML = `
    <button class="btn" onclick="yesClick()">YES</button>
    <button class="btn" onclick="noSecondClick()">Accept please</button>
  `;
}

function noSecondClick() {
  document.getElementById("question").innerText = "Only one option left 😼";
  document.getElementById("options").innerHTML = `
    <button class="btn" onclick="yesClick()">YES</button>
  `;
}

/* Floating hearts */
function startHearts() {
  setInterval(() => {
    const heart = document.createElement("div");
    heart.classList.add("heart");
    heart.innerHTML = "💖";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.fontSize = (20 + Math.random() * 30) + "px";
    document.body.appendChild(heart);

    setTimeout(() => heart.remove(), 6000);
  }, 300);
}

/* Slideshow */
function startSlideshow() {
  const slides = [
    slide1, slide2, slide3, slide4, slide5
  ];

  let i = 0;

  function showNext() {
    if (i > 0) slides[i - 1].classList.remove("show");

    if (i < slides.length) {
      slides[i].classList.add("show");
      i++;
      setTimeout(showNext, 2500);
    }
  }

  showNext();
}
</script>

</body>
</html>
