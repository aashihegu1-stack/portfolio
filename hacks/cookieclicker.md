---
layout: default
title: Cookie Clicker Game
permalink: /cookieclicker/
---

<style>
#game-container {
    width: 600px;
    margin: 0 auto;
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
    display: none;
}
#menu, #how-to {
    text-align: center;
    margin-top: 100px;
}
button {
    padding: 10px 20px;
    margin: 10px;
    font-size: 16px;
    cursor: pointer;
}
#cookie-btn {
    font-size: 100px;
    background: none;
    border: none;
    cursor: pointer;
}
#upgrades button {
    display: block;
    width: 100%;
    margin: 5px 0;
}
</style>

<div id="menu">
    <h1>Cookie Clicker</h1>
    <button onclick="startGame()">Play Game</button>
    <button onclick="showHowTo()">How to Play</button>
</div>

<div id="how-to" style="display:none;">
    <h2>How to Play</h2>
    <p>
        Click the cookie 🍪 to earn cookies.<br>
        Use your cookies to buy upgrades that increase how many cookies you get per click or per second.<br>
        Return to the menu at any time with the "New Game" button.
    </p>
    <button onclick="goBack()">Back</button>
</div>

<div id="game-container">
    <h2>Cookie Clicker</h2>
    <p id="cookies-count">Cookies: 0</p>
    <p id="cps-count">Cookies per second: 0</p>

    <button id="cookie-btn" onclick="clickCookie()">🍪</button>

    <div id="upgrades">
        <button id="cursor-btn" onclick="buyCursor()">Buy Cursor (15 cookies)</button>
        <button id="grandma-btn" onclick="buyGrandma()">Buy Grandma (100 cookies)</button>
    </div>

    <div id="game-controls">
        <button id="new-game-btn" onclick="newGame()">New Game</button>
    </div>

    <p id="message"></p>
</div>

<script>
let cookies = 0;
let clickPower = 1;
let cps = 0;
let autoInterval = null;

function startGame() {
    document.getElementById("menu").style.display = "none";
    document.getElementById("how-to").style.display = "none";
    document.getElementById("game-container").style.display = "block";
    newGame();
}

function showHowTo() {
    document.getElementById("menu").style.display = "none";
    document.getElementById("how-to").style.display = "block";
}

function goBack() {
    document.getElementById("how-to").style.display = "none";
    document.getElementById("menu").style.display = "block";
}

function updateDisplay() {
    document.getElementById("cookies-count").textContent = `Cookies: ${Math.floor(cookies)}`;
    document.getElementById("cps-count").textContent = `Cookies per second: ${cps}`;
}

function clickCookie() {
    cookies += clickPower;
    updateDisplay();
}

function buyCursor() {
    if (cookies >= 15) {
        cookies -= 15;
        clickPower += 1;
        document.getElementById("message").textContent = "Bought cursor! +1 click power.";
        updateDisplay();
    } else {
        document.getElementById("message").textContent = "Not enough cookies for a cursor.";
    }
}

function buyGrandma() {
    if (cookies >= 100) {
        cookies -= 100;
        cps += 1;
        document.getElementById("message").textContent = "Bought grandma! +1 cps.";
        updateDisplay();
        startAuto();
    } else {
        document.getElementById("message").textContent = "Not enough cookies for a grandma.";
    }
}

function startAuto() {
    if (autoInterval === null) {
        autoInterval = setInterval(() => {
            cookies += cps;
            updateDisplay();
        }, 1000);
    }
}

function newGame() {
    cookies = 0;
    clickPower = 1;
    cps = 0;
    document.getElementById("message").textContent = "";
    updateDisplay();
    if (autoInterval !== null) {
        clearInterval(autoInterval);
        autoInterval = null;
    }
}
</script>
