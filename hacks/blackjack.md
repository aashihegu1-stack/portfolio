---
layout: default
title: Blackjack Card Game
permalink: /blackjack/
---

<style>
#game-container {
    width: 800px;
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
.points-list {
    list-style: none;
    padding: 0;
    font-size: 18px;
    font-weight: bold;
    color: #333;
    text-align: center;
}
#message {
    font-weight: bold;
    color: black !important;
}
.player-area {
    margin-bottom: 20px;
}
.cards-container {
    display: flex;
    justify-content: center;
    min-height: 120px;
}
.card {
    width: 80px;
    height: 110px;
    border: 1px solid #333;
    border-radius: 5px;
    margin: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    font-weight: bold;
    background-color: #fff;
    box-shadow: 2px 2px 5px rgba(0,0,0,0.2);
}
button {
    padding: 10px 20px;
    margin: 10px;
    font-size: 16px;
    cursor: pointer;
}
.hand-container {
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>

<div id="menu">
    <h1>Blackjack</h1>
    <button onclick="startGame()">Play Game</button>
    <button onclick="showHowTo()">How to Play</button>
</div>

<div id="how-to" style="display:none;">
    <h2>How to Play</h2>
    <p>
        Get as close to 21 as possible without going over.<br>
        Face cards = 10, Aces = 1 or 11.<br>
        Dealer hits on 16.
    </p>
    <button onclick="goBack()">Back</button>
</div>

<div id="game-container">
    <h2>Blackjack</h2>
    <p>Dealer hits on 16</p>

    <div id="dealer-area" class="player-area">
        <h2>Dealer's Hand: <span id="dealer-score">0</span></h2>
        <div class="hand-container">
            <div id="dealer-cards" class="cards-container"></div>
            <div id="dealer-points" class="points-list"></div>
        </div>
    </div>

    <div id="player-area" class="player-area">
        <h2>Your Hand: <span id="player-score">0</span></h2>
        <div class="hand-container">
            <div id="player-cards" class="cards-container"></div>
            <div id="player-points" class="points-list"></div>
        </div>
    </div>

    <div id="game-controls">
        <button id="new-game-btn">New Game</button>
        <button id="hit-btn">Hit</button>
        <button id="stand-btn">Stand</button>
    </div>

    <p id="message"></p>
</div>

<script>
let dealerCardsEl = document.getElementById("dealer-cards");
let playerCardsEl = document.getElementById("player-cards");
let dealerScoreEl = document.getElementById("dealer-score");
let playerScoreEl = document.getElementById("player-score");
let messageEl = document.getElementById("message");

let newGameBtn = document.getElementById("new-game-btn");
let hitBtn = document.getElementById("hit-btn");
let standBtn = document.getElementById("stand-btn");

let deck = [];
let playerHand = [];
let dealerHand = [];
let gameOver = false;

// Betting system
let playerMoney = 100;
let betIncrement = 10;
let currentBet = 0;

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

// Deck & card functions
function createDeck() {
    const suits = ["♠","♥","♦","♣"];
    const values = ["A","2","3","4","5","6","7","8","9","10","J","Q","K"];
    let newDeck = [];
    for (let suit of suits)
        for (let value of values) newDeck.push({value,suit});
    return shuffle(newDeck);
}

function shuffle(deck) {
    for (let i=deck.length-1;i>0;i--){
        let j = Math.floor(Math.random()*(i+1));
        [deck[i],deck[j]]=[deck[j],deck[i]];
    }
    return deck;
}

function getCardValue(card){
    if (["J","Q","K"].includes(card.value)) return 10;
    if (card.value==="A") return 11;
    return parseInt(card.value);
}

function calculateHand(hand){
    let value=0, aces=0;
    for (let c of hand){
        value += getCardValue(c);
        if (c.value==="A") aces++;
    }
    while(value>21 && aces>0){value-=10; aces--;}
    return value;
}

function renderHand(hand, container, pointsContainer){
    container.innerHTML="";
    for (let c of hand){
        let cardEl = document.createElement("div");
        cardEl.className="card";
        cardEl.textContent=c.value+c.suit;
        cardEl.style.color=(c.suit==="♥"||c.suit==="♦")?"red":"black";
        container.appendChild(cardEl);
    }
    pointsContainer.textContent=calculateHand(hand);
}

function renderDealerInitial(){
    dealerCardsEl.innerHTML="";
    let firstCard=dealerHand[0];
    let cardEl1=document.createElement("div");
    cardEl1.className="card";
    cardEl1.textContent=firstCard.value+firstCard.suit;
    cardEl1.style.color=(firstCard.suit==="♥"||firstCard.suit==="♦")?"red":"black";
    dealerCardsEl.appendChild(cardEl1);

    let hiddenCard=document.createElement("div");
    hiddenCard.className="card";
    hiddenCard.textContent="🂠";
    dealerCardsEl.appendChild(hiddenCard);

    document.getElementById("dealer-points").textContent=getCardValue(firstCard);
}

function updateScores(){
    dealerScoreEl.textContent=calculateHand(dealerHand);
    playerScoreEl.textContent=calculateHand(playerHand);
}

// New betting system
function newGame(){
    if(playerMoney<=0){
        alert("You lost everything! Game over. Refresh to restart.");
        return;
    }

    currentBet = parseInt(prompt("You can bet up to $" + playerMoney + ". Enter your bet:"));
    while(isNaN(currentBet) || currentBet<=0 || currentBet>playerMoney){
        currentBet=parseInt(prompt("Invalid bet. Enter a bet up to $" + playerMoney + ":"));
    }

    deck=createDeck();
    playerHand=[deck.pop(),deck.pop()];
    dealerHand=[deck.pop(),deck.pop()];
    gameOver=false;

    renderHand(playerHand,playerCardsEl,document.getElementById("player-points"));
    renderDealerInitial();
    messageEl.textContent="Bet: $"+currentBet+". Your move.";
}

function hit(){
    if(gameOver) return;
    playerHand.push(deck.pop());
    renderHand(playerHand,playerCardsEl,document.getElementById("player-points"));
    if(calculateHand(playerHand)>21) endRound("lose");
}

function stand(){
    if(gameOver) return;

    dealerCardsEl.children[1].textContent=dealerHand[1].value+dealerHand[1].suit;
    dealerCardsEl.children[1].style.color=(dealerHand[1].suit==="♥"||dealerHand[1].suit==="♦")?"red":"black";
    document.getElementById("dealer-points").textContent=calculateHand(dealerHand);

    while(calculateHand(dealerHand)<17){
        dealerHand.push(deck.pop());
        renderHand(dealerHand,dealerCardsEl,document.getElementById("dealer-points"));
    }

    updateScores();
    let playerValue=calculateHand(playerHand);
    let dealerValue=calculateHand(dealerHand);

    if(playerValue>dealerValue && playerValue<=21 || dealerValue>21){
        endRound("win");
    } else if(dealerValue>playerValue && dealerValue<=21){
        endRound("lose");
    } else{
        endRound("tie");
    }
}

function endRound(result){
    gameOver=true;
    if(result==="win"){
        messageEl.textContent="You win! You earned $10.";
        playerMoney+=10;
    } else if(result==="lose"){
        messageEl.textContent="You lost everything! Refresh to restart.";
        playerMoney=0;
    } else{
        messageEl.textContent="It's a tie! Your money remains the same.";
    }
}

newGameBtn.addEventListener("click",newGame);
hitBtn.addEventListener("click",hit);
standBtn.addEventListener("click",stand);
</script>