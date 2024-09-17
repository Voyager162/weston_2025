---
layout: post
title: Javascript Calculator
permalink: /javascriptCalculator
---

<!-- HTML structure with embedded CSS and JavaScript for an enhanced calculator -->
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        .calculator {
            background: #f4f4f4;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
            width: 320px;
        }
        .display {
            background-color: #222;
            color: white;
            font-size: 2.5rem;
            text-align: right;
            padding: 10px;
            border-radius: 10px;
            box-shadow: inset 0px 4px 8px rgba(0, 0, 0, 0.2);
            margin-bottom: 20px;
            height: 60px;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        button {
            padding: 20px;
            font-size: 1.5rem;
            border-radius: 10px;
            border: none;
            background: #3498db;
            color: white;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
            cursor: pointer;
            transition: transform 0.2s ease-in-out;
        }
        button:hover {
            transform: scale(1.05);
        }
        button:active {
            transform: scale(0.95);
        }
        .history {
            margin-top: 20px;
            background: #fff;
            padding: 10px;
            border-radius: 10px;
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        }
        .history p {
            font-size: 1rem;
            margin: 5px 0;
            color: #333;
        }
        .history-title {
            font-weight: bold;
            text-align: center;
            margin-bottom: 10px;
            color: #2a5298;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div id="display" class="display">0</div>
        <div class="buttons">
            <button onclick="clearDisplay()">C</button>
            <button onclick="backspace()">←</button>
            <button onclick="appendOperator('/')">÷</button>
            <button onclick="appendOperator('*')">×</button>
            <button onclick="appendNumber('7')">7</button>
            <button onclick="appendNumber('8')">8</button>
            <button onclick="appendNumber('9')">9</button>
            <button onclick="appendOperator('-')">-</button>
            <button onclick="appendNumber('4')">4</button>
            <button onclick="appendNumber('5')">5</button>
            <button onclick="appendNumber('6')">6</button>
            <button onclick="appendOperator('+')">+</button>
            <button onclick="appendNumber('1')">1</button>
            <button onclick="appendNumber('2')">2</button>
            <button onclick="appendNumber('3')">3</button>
            <button onclick="calculate()">=</button>
            <button onclick="appendNumber('0')" style="grid-column: span 2;">0</button>
            <button onclick="appendDot()">.</button>
            <button onclick="appendOperator('%')">%</button>
            <!-- New Operations -->
            <button onclick="calculateSquareRoot()">√</button>
            <button onclick="appendOperator('^')">^</button>
        </div>
        <!-- History Section -->
        <div class="history">
            <div class="history-title">Calculation History</div>
            <div id="history-list">
                <!-- History items will be added here dynamically -->
            </div>
        </div>
    </div>
    <script>
        let currentInput = '';
        let history = [];
        function updateDisplay(value) {
            document.getElementById('display').textContent = value;
        }
        function appendNumber(number) {
            currentInput += number;
            updateDisplay(currentInput);
        }
        function appendOperator(operator) {
            currentInput += ` ${operator} `;
            updateDisplay(currentInput);
        }
        function appendDot() {
            if (!currentInput.includes('.')) {
                currentInput += '.';
                updateDisplay(currentInput);
            }
        }
        function clearDisplay() {
            currentInput = '';
            updateDisplay('0');
        }
        function backspace() {
            currentInput = currentInput.trim().slice(0, -1);
            if (currentInput === '') {
                updateDisplay('0');
            } else {
                updateDisplay(currentInput);
            }
        }
        function calculate() {
            try {
                // Handle exponentiation (x^y)
                if (currentInput.includes('^')) {
                    const [base, exponent] = currentInput.split('^');
                    const result = Math.pow(parseFloat(base), parseFloat(exponent));
                    addHistory(`${currentInput} = ${result}`);
                    currentInput = result.toString();
                    updateDisplay(result);
                } else {
                    const result = eval(currentInput.replace('×', '*').replace('÷', '/').replace('%', '%'));
                    addHistory(`${currentInput} = ${result}`);
                    currentInput = result.toString();
                    updateDisplay(result);
                }
            } catch (error) {
                updateDisplay('Error');
                currentInput = '';
            }
        }
        function calculateSquareRoot() {
            try {
                const result = Math.sqrt(parseFloat(currentInput));
                addHistory(`√${currentInput} = ${result}`);
                currentInput = result.toString();
                updateDisplay(result);
            } catch (error) {
                updateDisplay('Error');
                currentInput = '';
            }
        }
        function addHistory(entry) {
            history.push(entry);
            const historyList = document.getElementById('history-list');
            const p = document.createElement('p');
            p.textContent = entry;
            historyList.appendChild(p);
        }
    </script>
</body>
</html>
