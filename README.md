<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        .calculator {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            padding: 20px;
            width: 320px;
        }

        .display {
            background: #2d3436;
            color: #00ff00;
            font-size: 2.5em;
            padding: 20px;
            border-radius: 10px;
            text-align: right;
            margin-bottom: 20px;
            word-wrap: break-word;
            word-break: break-all;
            min-height: 60px;
            font-weight: bold;
            font-family: 'Courier New', monospace;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        button {
            padding: 20px;
            font-size: 1.5em;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: bold;
        }

        button:hover {
            transform: scale(1.05);
        }

        button:active {
            transform: scale(0.95);
        }

        .number, .decimal {
            background: #ecf0f1;
            color: #2d3436;
        }

        .number:hover, .decimal:hover {
            background: #bdc3c7;
        }

        .operator {
            background: #667eea;
            color: white;
        }

        .operator:hover {
            background: #5568d3;
        }

        .equals {
            background: #00b894;
            color: white;
            grid-column: span 2;
        }

        .equals:hover {
            background: #009876;
        }

        .clear {
            background: #d63031;
            color: white;
            grid-column: span 2;
        }

        .clear:hover {
            background: #b71c1c;
        }

        .delete {
            background: #fdcb6e;
            color: #2d3436;
        }

        .delete:hover {
            background: #f9b233;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="clear" onclick="clearDisplay()">C</button>
            <button class="delete" onclick="deleteLast()">DEL</button>
            <button class="operator" onclick="appendOperator('/')">/</button>
            <button class="operator" onclick="appendOperator('*')">×</button>
            
            <button class="number" onclick="appendNumber('7')">7</button>
            <button class="number" onclick="appendNumber('8')">8</button>
            <button class="number" onclick="appendNumber('9')">9</button>
            <button class="operator" onclick="appendOperator('-')">−</button>
            
            <button class="number" onclick="appendNumber('4')">4</button>
            <button class="number" onclick="appendNumber('5')">5</button>
            <button class="number" onclick="appendNumber('6')">6</button>
            <button class="operator" onclick="appendOperator('+')">+</button>
            
            <button class="number" onclick="appendNumber('1')">1</button>
            <button class="number" onclick="appendNumber('2')">2</button>
            <button class="number" onclick="appendNumber('3')">3</button>
            <button class="decimal" onclick="appendNumber('.')">.</button>
            
            <button class="number" onclick="appendNumber('0')">0</button>
            <button class="equals" onclick="calculate()">=</button>
        </div>
    </div>

    <script>
        let display = document.getElementById('display');
        let expression = '';

        function appendNumber(num) {
            if (num === '.' && expression.includes('.')) {
                return;
            }
            expression += num;
            updateDisplay();
        }

        function appendOperator(op) {
            if (expression === '') return;
            if (['+', '-', '×', '/'].includes(expression[expression.length - 1])) {
                expression = expression.slice(0, -1);
            }
            expression += op;
            updateDisplay();
        }

        function clearDisplay() {
            expression = '';
            updateDisplay();
        }

        function deleteLast() {
            expression = expression.slice(0, -1);
            updateDisplay();
        }

        function calculate() {
            try {
                let result = expression.replace(/×/g, '*').replace(/−/g, '-');
                result = eval(result);
                expression = result.toString();
                updateDisplay();
            } catch (error) {
                display.textContent = 'Error';
                expression = '';
            }
        }

        function updateDisplay() {
            display.textContent = expression || '0';
        }
    </script>
</body>
</html>
