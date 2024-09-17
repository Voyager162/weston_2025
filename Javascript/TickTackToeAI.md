---
layout: post
title: Tick Tack Toe
permalink: /TickTackToe
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe AI</title>
    <style>
        .game-container {
            display: flex;
            justify-content: center;
            flex-direction: column;
            align-items: center;
            margin-top: 50px;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
            margin-bottom: 20px;
        }
        .cell {
            width: 100px;
            height: 100px;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #ffffff;
            font-size: 2rem;
            cursor: pointer;
            border-radius: 10px;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            color: white;
        }
        .status {
            color: white;
            font-size: 1.5rem;
        }
        .reset-btn {
            padding: 10px 20px;
            background-color: #4a90e2;
            border: none;
            color: white;
            font-size: 1rem;
            cursor: pointer;
            border-radius: 5px;
        }
        .reset-btn:hover {
            background-color: #3a78c2;
        }
        .reset-btn:active {
            background-color: #2a68b2;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>Tic-Tac-Toe: Play Against AI</h1>
        <div class="board" id="board">
            <div class="cell" id="0"></div>
            <div class="cell" id="1"></div>
            <div class="cell" id="2"></div>
            <div class="cell" id="3"></div>
            <div class="cell" id="4"></div>
            <div class="cell" id="5"></div>
            <div class="cell" id="6"></div>
            <div class="cell" id="7"></div>
            <div class="cell" id="8"></div>
        </div>
        <div class="status" id="status">Your turn!</div>
        <button class="reset-btn" onclick="resetGame()">Reset Game</button>
    </div>
    <script>
        const board = ['', '', '', '', '', '', '', '', ''];
        const player = 'X';
        const ai = 'O';
        let currentPlayer = player;
        let gameActive = true;
        const winCombinations = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],
            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],
            [0, 4, 8],
            [2, 4, 6]
        ];
        document.querySelectorAll('.cell').forEach(cell => {
            cell.addEventListener('click', handleCellClick);
        });
        function handleCellClick(e) {
            const cellIndex = e.target.id;
            if (board[cellIndex] === '' && currentPlayer === player && gameActive) {
                makeMove(cellIndex, player);
                if (!checkWin(player) && !isBoardFull()) {
                    currentPlayer = ai;
                    bestMove();
                }
            }
        }
        function makeMove(index, symbol) {
            board[index] = symbol;
            document.getElementById(index).innerText = symbol;
            if (checkWin(symbol)) {
                document.getElementById('status').innerText = symbol === player ? 'You win!' : 'AI wins!';
                gameActive = false;
            } else if (isBoardFull()) {
                document.getElementById('status').innerText = 'It\'s a draw!';
                gameActive = false;
            }
        }
        function checkWin(symbol) {
            return winCombinations.some(combination => {
                return combination.every(index => board[index] === symbol);
            });
        }
        function isBoardFull() {
            return board.every(cell => cell !== '');
        }
        function bestMove() {
            let bestScore = -Infinity;
            let move;
            for (let i = 0; i < board.length; i++) {
                if (board[i] === '') {
                    board[i] = ai;
                    let score = minimax(board, 0, false);
                    board[i] = '';
                    if (score > bestScore) {
                        bestScore = score;
                        move = i;
                    }
                }
            }
            makeMove(move, ai);
            currentPlayer = player;
            document.getElementById('status').innerText = 'Your turn!';
        }
        function minimax(board, depth, isMaximizing) {
            if (checkWin(ai)) {
                return 10 - depth;
            } else if (checkWin(player)) {
                return depth - 10;
            } else if (isBoardFull()) {
                return 0;
            }
            if (isMaximizing) {
                let bestScore = -Infinity;
                for (let i = 0; i < board.length; i++) {
                    if (board[i] === '') {
                        board[i] = ai;
                        let score = minimax(board, depth + 1, false);
                        board[i] = '';
                        bestScore = Math.max(score, bestScore);
                    }
                }
                return bestScore;
            } else {
                let bestScore = Infinity;
                for (let i = 0; i < board.length; i++) {
                    if (board[i] === '') {
                        board[i] = player;
                        let score = minimax(board, depth + 1, true);
                        board[i] = '';
                        bestScore = Math.min(score, bestScore);
                    }
                }
                return bestScore;
            }
        }
        function resetGame() {
            for (let i = 0; i < board.length; i++) {
                board[i] = '';
                document.getElementById(i).innerText = '';
            }
            currentPlayer = player;
            gameActive = true;
            document.getElementById('status').innerText = 'Your turn!';
        }
    </script>
</body>
</html>

