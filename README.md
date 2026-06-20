# nursing-journey-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Nursing Clinical Journey</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: linear-gradient(to right, #eef2f3, #d9e4f5);
    margin: 0;
    padding: 0;
}

/* container animation */
.container {
    max-width: 850px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.15);
    animation: fadeIn 0.5s ease;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(15px); }
    to { opacity: 1; transform: translateY(0); }
}

h1 { text-align: center; color: #2c3e50; }

#progress {
    width: 100%;
    background: #ecf0f1;
    border-radius: 20px;
    margin-bottom: 20px;
}

#bar {
    height: 12px;
    width: 0%;
    background: #27ae60;
    transition: 0.4s;
}

/* IMAGE STYLE */
#sceneImg {
    width: 100%;
    border-radius: 12px;
    margin-bottom: 15px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.2);
    animation: fadeIn 0.6s ease;
}

#story {
    font-size: 18px;
    line-height: 1.7;
    color: #2c3e50;
    min-height: 120px;
    animation: fadeIn 0.5s ease;
}

/* BUTTONS + ANIMATION */
.btn {
    display: block;
    width: 100%;
    margin: 10px 0;
    padding: 14px;
    font-size: 16px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    background: #3498db;
    color: white;
    transition: 0.2s;
}

.btn:hover {
    background: #1f78c1;
    transform: scale(1.02);
}

/* shake effect for bad choices */
.shake {
    animation: shake 0.4s;
}

@keyframes shake {
    0% { transform: translateX(0); }
    25% { transform: translateX(-6px); }
    50% { transform: translateX(6px); }
    75% { transform: translateX(-6px); }
    100% { transform: translateX(0); }
}

.end {
    text-align: center;
    font-weight: bold;
    font-size: 20px;
}
</style>
</head>

<body>

<div class="container">
    <h1>🩺 Nursing Clinical Journey</h1>

    <div id="progress"><div id="bar"></div></div>

    <!-- IMAGE -->
    <img id="sceneImg" src="" alt="scene">

    <div id="story"></div>
    <div id="choices"></div>
</div>

<script>

const story = document.getElementById("story");
const choices = document.getElementById("choices");
const bar = document.getElementById("bar");
const img = document.getElementById("sceneImg");

/* UPDATE SCREEN WITH IMAGE + TEXT */
function show(text, image, options, progress){
    story.innerHTML = text;
    img.src = image;
    bar.style.width = progress + "%";

    choices.innerHTML = "";

    options.forEach(opt => {
        const btn = document.createElement("button");
        btn.className = "btn";
        btn.innerText = opt.text;
        btn.onclick = opt.action;
        choices.appendChild(btn);
    });
}

/* SCENES IMAGES (free links) */
const images = {
    start: "https://images.unsplash.com/photo-1580281657527-47f249e8f5b1",
    study: "https://images.unsplash.com/photo-1454165804606-c3d57bc86b40",
    party: "https://images.unsplash.com/photo-1521337706264-a414f153a5bd",
    hospital: "https://images.unsplash.com/photo-1586773860418-d37222d8fce3",
    emergency: "https://images.unsplash.com/photo-1584515933487-779824d29309",
    success: "https://images.unsplash.com/photo-1584516150909-c43483ee7932",
    fail: "https://images.unsplash.com/photo-1582719478250-c89cae4dc85b"
};

/* START */
function start(){
    show(
        "I begin my nursing clinical journey feeling nervous but excited. Everything feels real now.",
        images.start,
        [
            {text: "Begin", action: page2}
        ],
        5
    );
}

/* PAGE 2 */
function page2(){
    show(
        "A major exam is announced. I must choose between studying or going to a party.",
        images.study,
        [
            {text: "Study", action: study},
            {text: "Party", action: party}
        ],
        15
    );
}

/* PARTY ENDING */
function party(){
    document.querySelector(".container").classList.add("shake");

    show(
        "<div class='end'>❌ I chose the party and struggled later with exams.</div>",
        images.party,
        [
            {text: "Restart", action: start}
        ],
        25
    );

    setTimeout(() => {
        document.querySelector(".container").classList.remove("shake");
    }, 500);
}

/* STUDY */
function study(){
    show(
        "I focus on studying hard and preparing for my exam.",
        images.study,
        [
            {text: "Continue", action: rest}
        ],
        35
    );
}

/* REST GOOD */
function rest(){
    show(
        "I choose rest and wake up refreshed for the exam.",
        images.study,
        [
            {text: "Go to Clinical", action: clinical}
        ],
        45
    );
}

/* CLINICAL */
function clinical(){
    show(
        "I enter the hospital for my first clinical experience.",
        images.hospital,
        [
            {text: "Comfort Patient", action: goodCare},
            {text: "Focus Tasks", action: neutralCare}
        ],
        55
    );
}

/* GOOD CARE */
function goodCare(){
    show(
        "I comfort the patient and build trust through communication.",
        images.hospital,
        [
            {text: "Emergency", action: emergency}
        ],
        65
    );
}

/* NEUTRAL */
function neutralCare(){
    show(
        "I focus on tasks and learn communication is also important.",
        images.hospital,
        [
            {text: "Emergency", action: emergency}
        ],
        65
    );
}

/* EMERGENCY */
function emergency(){
    show(
        "🚨 A sudden emergency happens in the hospital.",
        images.emergency,
        [
            {text: "Stay Calm", action: success},
            {text: "Panic", action: fail}
        ],
        80
    );
}

/* SUCCESS */
function success(){
    show(
        "<div class='end'>🏆 SUCCESS</div><br>I stay calm and assist the team effectively.",
        images.success,
        [
            {text: "Restart", action: start}
        ],
        100
    );
}

/* FAIL */
function fail(){
    document.querySelector(".container").classList.add("shake");

    show(
        "<div class='end'>⚠️ I panicked but learned from experience.</div>",
        images.fail,
        [
            {text: "Restart", action: start}
        ],
        100
    );

    setTimeout(() => {
        document.querySelector(".container").classList.remove("shake");
    }, 500);
}

start();

</script>

</body>
</html>