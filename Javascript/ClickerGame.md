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
        }
        .icon {
            font-size: 5rem;
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        .icon:hover {
            transform: scale(1.2);
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
                <button id="minion1" onclick="buyMinion(1)" disabled>Buy Minion 1 (Cost: 50)</button>
                <span id="minion1-status">Not Owned</span>
            </div>
            <div>
                <button id="minion2" onclick="buyMinion(2)" disabled>Buy Minion 2 (Cost: 200)</button>
                <span id="minion2-status">Not Owned</span>
            </div>
        </div>
    </div>
    <script>
        let score = 0;
        let minion1Owned = false;
        let minion2Owned = false;
        const clickSound = document.getElementById("click-sound");
        const scoreDisplay = document.getElementById("score");
        document.getElementById("clickable-icon").addEventListener("click", function() {
            score++;
            updateScore();
            clickSound.currentTime = 0;  // Reset sound
            clickSound.play();
        });
        function updateScore() {
            scoreDisplay.textContent = score;
            // Enable buttons if player has enough score
            if (score >= 50 && !minion1Owned) {
                document.getElementById("minion1").disabled = false;
            }
            if (score >= 200 && !minion2Owned) {
                document.getElementById("minion2").disabled = false;
            }
        }
        function buyMinion(minion) {
            if (minion === 1 && score >= 50) {
                score -= 50;
                minion1Owned = true;
                document.getElementById("minion1").disabled = true;
                document.getElementById("minion1-status").textContent = "Owned";
                startMinion(1);
            } else if (minion === 2 && score >= 200) {
                score -= 200;
                minion2Owned = true;
                document.getElementById("minion2").disabled = true;
                document.getElementById("minion2-status").textContent = "Owned";
                startMinion(2);
            }
            updateScore();
        }
        function startMinion(minion) {
            if (minion === 1) {
                setInterval(function() {
                    score++;
                    updateScore();
                    clickSound.currentTime = 0;  // Reset sound
                    clickSound.play();
                }, 200);  // Minion 1 clicks every 2 seconds
            }
            if (minion === 2) {
                setInterval(function() {
                    score ++;
                    updateScore();
                    clickSound.currentTime = 0;  // Reset sound
                    clickSound.play();
                }, 1);  // Minion 2 clicks every 5 seconds, but gives 3 points
            }
        }
    </script>
</body>
</html>