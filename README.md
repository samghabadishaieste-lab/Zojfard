<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بازی جذاب زوج و فرد 🎨</title>
    <style>
        :root {
            --primary-color: #ff6b6b;
            --secondary-color: #4ecdc4;
            --bg-color: #f7f7f7;
            --text-color: #2d3436;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #fceabb, #f8b500);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        #game-container {
            background: white;
            padding: 2rem;
            border-radius: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
            text-align: center;
            width: 90%;
            max-width: 400px;
            border: 8px solid #fff;
        }

        h1 { color: #ff4757; font-size: 1.5rem; margin-bottom: 20px; }

        #number-display {
            font-size: 80px;
            font-weight: bold;
            color: #2f3542;
            margin: 20px 0;
            background: #f1f2f6;
            border-radius: 20px;
            padding: 20px;
            animation: pop 0.3s ease;
        }

        @keyframes pop {
            0% { transform: scale(0.5); }
            100% { transform: scale(1); }
        }

        .buttons {
            display: flex;
            gap: 15px;
            justify-content: center;
        }

        button {
            padding: 15px 30px;
            font-size: 1.2rem;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            transition: transform 0.2s, background 0.2s;
            font-weight: bold;
            color: white;
            flex: 1;
        }

        .btn-even { background-color: #4834d4; }
        .btn-odd { background-color: #eb4d4b; }

        button:active { transform: scale(0.9); }

        #score-board {
            margin-top: 20px;
            font-size: 1.2rem;
            color: #57606f;
        }

        #feedback {
            height: 30px;
            margin-top: 10px;
            font-weight: bold;
            font-size: 1.1rem;
        }

        .correct { color: #2ecc71; }
        .wrong { color: #e74c3c; }
    </style>
</head>
<body>

<div id="game-container">
    <h1>آیا این عدد زوج است یا فرد؟ 🤔</h1>
    <div id="number-display">?</div>
    
    <div class="buttons">
        <button class="btn-even" onclick="checkAnswer('even')">زوج</button>
        <button class="btn-odd" onclick="checkAnswer('odd')">فرد</button>
    </div>

    <div id="feedback"></div>
    
    <div id="score-board">
        امتیاز شما: <span id="score">0</span>
    </div>
</div>

<script>
    let currentNumber = 0;
    let score = 0;

    function generateNumber() {
        currentNumber = Math.floor(Math.random() * 100) + 1; // اعداد بین 1 تا 100
        const display = document.getElementById('number-display');
        display.innerText = currentNumber;
        display.style.animation = 'none';
        display.offsetHeight; // Trigger reflow
        display.style.animation = 'pop 0.3s ease';
    }

    function checkAnswer(choice) {
        const isEven = currentNumber % 2 === 0;
        const feedback = document.getElementById('feedback');
        const scoreDisplay = document.getElementById('score');

        if ((choice === 'even' && isEven) || (choice === 'odd' && !isEven)) {
            score += 10;
            feedback.innerText = "آفرین! درست بود 🎉";
            feedback.className = "correct";
            document.body.style.backgroundColor = "#b8e994"; // Green flash
        } else {
            score = Math.max(0, score - 5);
            feedback.innerText = "اشتباه بود، دوباره تلاش کن! ❌";
            feedback.className = "wrong";
            document.body.style.backgroundColor = "#ffaaa5"; // Red flash
        }

        scoreDisplay.innerText = score;
        
        // Reset background color after a short delay
        setTimeout(() => {
            document.body.style.backgroundColor = "";
        }, 300);

        generateNumber();
    }

    // Start the game
    generateNumber();
</script>

</body>
</html>
