---
layout: page
title: Clicker Game
permalink: /clicker/
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Click to Score</title>
    <style>
        .container {
            text-align: center;
        }
        .score-board {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: #2ecc71;
        }
        .icon-container {
            margin-top: 20px;
            position: relative;
            display: inline-block;
        }
        .icon {
            font-size: 5rem;
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        .icon:hover {
            transform: scale(1.2);
        }
        .minion-button {
            background-color: #00b400; /* Button background color */
            color: black;              /* Text color */
            border: none;              /* Remove default border */
            padding: 10px 20px;        /* Padding inside the button */
            border-radius: 5px;        /* Rounded corners */
            font-size: 16px;           /* Font size */
            cursor: pointer;           /* Change cursor on hover */
            transition: background-color 0.3s, transform 0.2s; /* Smooth transitions */
            margin: 10px;
        }
        .minion-button:hover {
            background-color: #018c10; /* Change background color on hover */
            transform: scale(1.05);    /* Slightly enlarge button on hover */
        }
        .minion-button:active {
            background-color: #006400; /* Change background color when button is pressed */
            transform: scale(0.95);    /* Slightly shrink button when pressed */
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Click the Cookie to Gain Points!</h1>
        <div class="score-board">Score: <span id="score">0</span></div>
        <div class="icon-container">
            <i id="clickable-icon" class="icon">🍪</i>
        </div>
        <!-- Preloading and using a fast, small click sound -->
        <audio id="click-sound" src="https://freesound.org/data/previews/66/66717_931655-lq.mp3" preload="auto"></audio>
        <div class="menu">
            <h2>Buy Minions</h2>
            <div>
                <button class="minion-button" id="minion1" onclick="buyMinion(1)" disabled>Buy Worker (Cost: 50)</button>
                <span id="minion1-status">Not Owned</span>
            </div>
            <div>
                <button class="minion-button" id="minion2" onclick="buyMinion(2)" disabled>Buy Farmer (Cost: 200)</button>
                <span id="minion2-status">Not Owned</span>
            </div>
            <div>
                <button class="minion-button" id="minion3" onclick="buyMinion(3)" disabled>Buy Engineer (Cost: 500)</button>
                <span id="minion3-status">Not Owned</span>
            </div>
            <div>
                <button class="minion-button" id="minion4" onclick="buyMinion(4)" disabled>Buy Scientist (Cost: 1000)</button>
                <span id="minion4-status">Not Owned</span>
            </div>
        </div>
    </div>
    <script>
        let score = 0;
        let minionsOwned = {1: 0, 2: 0, 3: 0, 4: 0};
        const clickSound = document.getElementById("click-sound");
        const scoreDisplay = document.getElementById("score");
        document.getElementById("clickable-icon").addEventListener("click", function() {
            score++;
            updateScore();
            clickSound.currentTime = 0;  // Reset sound
            clickSound.play();  // Only play sound on manual click
        });
        function updateScore() {
            scoreDisplay.textContent = score;
            // Enable buttons if player has enough score
            if (score >= 50) {
                document.getElementById("minion1").disabled = false;
            }
            if (score >= 200) {
                document.getElementById("minion2").disabled = false;
            }
            if (score >= 500) {
                document.getElementById("minion3").disabled = false;
            }
            if (score >= 1000) {
                document.getElementById("minion4").disabled = false;
            }
        }
        function buyMinion(minion) {
            if (minion === 1 && score >= 50) {
                score -= 50;
                minionsOwned[1]++;
                document.getElementById("minion1-status").textContent = `Owned (${minionsOwned[1]})`;
                startMinion(1);
            } else if (minion === 2 && score >= 200) {
                score -= 200;
                minionsOwned[2]++;
                document.getElementById("minion2-status").textContent = `Owned (${minionsOwned[2]})`;
                startMinion(2);
            } else if (minion === 3 && score >= 500) {
                score -= 500;
                minionsOwned[3]++;
                document.getElementById("minion3-status").textContent = `Owned (${minionsOwned[3]})`;
                startMinion(3);
            } else if (minion === 4 && score >= 1000) {
                score -= 1000;
                minionsOwned[4]++;
                document.getElementById("minion4-status").textContent = `Owned (${minionsOwned[4]})`;
                startMinion(4);
            }
            updateScore();
        }
        function startMinion(minion) {
            if (minion === 1) {
                setInterval(function() {
                    score += minionsOwned[1];  // Each Worker gives 1 point every 2 seconds
                    updateScore();
                }, 2000);  // Worker clicks every 2 seconds
            }
            if (minion === 2) {
                setInterval(function() {
                    score += minionsOwned[2] * 2;  // Each Farmer gives 2 points every 5 seconds
                    updateScore();
                }, 5000);  // Farmer clicks every 5 seconds
            }
            if (minion === 3) {
                setInterval(function() {
                    score += minionsOwned[3] * 5;  // Each Engineer gives 5 points every 10 seconds
                    updateScore();
                }, 10000);  // Engineer clicks every 10 seconds
            }
            if (minion === 4) {
                setInterval(function() {
                    score += minionsOwned[4] * 10;  // Each Scientist gives 10 points every 15 seconds
                    updateScore();
                }, 15000);  // Scientist clicks every 15 seconds
            }
        }
    </script>
</body>
</html>
