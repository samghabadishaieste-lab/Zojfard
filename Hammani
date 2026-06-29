<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بازی کلمات هم‌معنی - کلاس دوم</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Vazirmatn:wght@400;700&display=swap');

        body {
            font-family: 'Vazirmatn', sans-serif;
            background-color: #f0f8ff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        #game-container {
            background-color: white;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            width: 90%;
            max-width: 500px;
            text-align: center;
            border: 5px solid #ffeb3b;
        }

        h1 { color: #ff5722; margin-bottom: 10px; }
        h2 { color: #4caf50; font-size: 1.2rem; }
        .teacher-name { color: #2196f3; font-weight: bold; }

        input[type="text"] {
            padding: 12px;
            width: 80%;
            border-radius: 10px;
            border: 2px solid #ddd;
            margin: 20px 0;
            font-family: 'Vazirmatn';
            text-align: center;
            font-size: 1rem;
        }

        button {
            background-color: #4caf50;
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 50px;
            font-size: 1.1rem;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.2s;
            font-family: 'Vazirmatn';
        }

        button:hover { transform: scale(1.05); background-color: #45a049; }

        .option-btn {
            display: block;
            width: 100%;
            margin: 10px 0;
            background-color: #2196f3;
        }

        .hidden { display: none; }

        #question-text { font-size: 1.5rem; margin-bottom: 20px; color: #333; }
        #progress { font-size: 0.9rem; color: #888; margin-bottom: 10px; }
        
        .result-card { font-size: 1.2rem; line-height: 2; }
        .score-big { font-size: 3rem; color: #ff5722; display: block; }
        .congrats { color: #4caf50; font-weight: bold; font-size: 1.4rem; }
    </style>
</head>
<body>

<div id="game-container">
    <!-- صفحه شروع -->
    <div id="start-screen">
        <h1>بازی کلمات 🎈</h1>
        <h2>آموزگار: <span class="teacher-name">شاییده صفی</span></h2>
        <p>سلام قهرمان! نام خود را بنویس:</p>
        <input type="text" id="student-name" placeholder="نام و نام خانوادگی">
        <br>
        <button onclick="startGame()">شروع بازی 🚀</button>
    </div>

    <!-- صفحه سوالات -->
    <div id="quiz-screen" class="hidden">
        <div id="progress">سوال ۱ از ۲۰</div>
        <div id="question-text">کلمه اینجا قرار می‌گیرد</div>
        <div id="options-container">
            <!-- دکمه‌های گزینه‌ها توسط جاوااسکریپت ساخته می‌شوند -->
        </div>
    </div>

    <!-- صفحه نتیجه نهایی -->
    <div id="result-screen" class="hidden">
        <h1>کارنامه شما 🏆</h1>
        <div class="result-card" id="result-content">
            <!-- نتایج اینجا نمایش داده می‌شود -->
        </div>
        <br>
        <button onclick="location.reload()">دوباره بازی کن 🔄</button>
    </div>
</div>

<script>
    // لیست سوالات (هم‌معنی کلمات پایه دوم)
    const questions = [
        { q: "خوشحال", a: "شاد", b: "غمگین", correct: "a" },
        { q: "زیبا", a: "زشت", b: "قشنگ", correct: "b" },
        { q: "بزرگ", a: "عظیم", b: "کوچک", correct: "a" },
        { q: "تند", a: "سریع", b: "آرام", correct: "a" },
        { q: "دوست", a: "دشمن", b: "رفیق", correct: "b" },
        { q: "نور", a: "روشنایی", b: "تاریکی", correct: "a" },
        { q: "آفتاب", a: "خورشید", b: "ماه", correct: "a" },
        { q: "سخت", a: "آسان", b: "سخت", correct: "b" }, // کلمه سخت خودش هم‌معنی است، اما برای تست: دشوار
        { q: "دشوار", a: "سخت", b: "آسان", correct: "a" },
        { q: "بوی خوش", a: "عطر", b: "بوی بد", correct: "a" },
        { q: "بزرگسال", a: "پیر", b: "بزرگ", correct: "b" },
        { q: "بخشیدن", a: "گذشت کردن", b: "تنبیه کردن", correct: "a" },
        { q: "کمک", a: "یاری", b: "مانع", correct: "a" },
        { q: "دانشمند", a: "آدم عاقل", b: "آدم نادان", correct: "a" },
        { q: "فراوان", a: "زیاد", b: "کم", correct: "a" },
        { q: "آرام", a: "آسوده", b: "پرجنب‌وجوش", correct: "a" },
        { q: "هوشمند", a: "زرنگ", b: "کند", correct: "a" },
        { q: "خوابیدن", a: "استراحت کردن", b: "دویدن", correct: "a" },
        { q: "خنده", a: "شادی", b: "گریه", correct: "a" },
        { q: "فردا", a: "روز آینده", b: "روز گذشته", correct: "a" }
    ];

    // اصلاح برخی سوالات برای دقت بیشتر در سطح دوم
    questions[2] = { q: "بسیار بزرگ", a: "عظیم", b: "کوچک", correct: "a" };
    questions[7] = { q: "سخت", a: "دشوار", b: "آسان", correct: "a" };

    let currentQuestionIndex = 0;
    let score = 0;
    let studentName = "";

    function startGame() {
        studentName = document.getElementById('student-name').value;
        if (studentName.trim() === "") {
            alert("لطفاً ابتدا نام خود را وارد کنید 😊");
            return;
        }
        document.getElementById('start-screen').classList.add('hidden');
        document.getElementById('quiz-screen').classList.remove('hidden');
        showQuestion();
    }

    function showQuestion() {
        const qData = questions[currentQuestionIndex];
        document.getElementById('progress').innerText = `سوال ${currentQuestionIndex + 1} از ${questions.length}`;
        document.getElementById('question-text').innerText = `هم‌معنی کلمه "${qData.q}" چیست؟`;
        
        const optionsContainer = document.getElementById('options-container');
        optionsContainer.innerHTML = '';

        // ایجاد دکمه گزینه A
        const btnA = document.createElement('button');
        btnA.innerText = qData.a;
        btnA.className = 'option-btn';
        btnA.onclick = () => checkAnswer('a');
        optionsContainer.appendChild(btnA);

        // ایجاد دکمه گزینه B
        const btnB = document.createElement('button');
        btnB.innerText = qData.b;
        btnB.className = 'option-btn';
        btnB.onclick = () => checkAnswer('b');
        optionsContainer.appendChild(btnB);
    }

    function checkAnswer(answer) {
        if (answer === questions[currentQuestionIndex].correct) {
            score++;
        }

        currentQuestionIndex++;

        if (currentQuestionIndex < questions.length) {
            showQuestion();
        } else {
            showResults();
        }
    }

    function showResults() {
        document.getElementById('quiz-screen').classList.add('hidden');
        document.getElementById('result-screen').classList.remove('hidden');

        const resultContent = document.getElementById('result-content');
        let message = "";
        let colorClass = "";

        if (score >= 17) {
            message = "آفرین قهرمان! تو فوق‌العاده‌ای! 🌟";
            colorClass = "congrats";
        } else if (score >= 13) {
            message = "خیلی خوب بود! عالی پیش می‌روی! 👍";
        } else {
            message = "امیدوارم دفعه بعد بهتر شوی، دوباره تلاش کن! 💪";
        }

        resultContent.innerHTML = `
            <p>دانش‌آموز عزیز: <strong>${studentName}</strong></p>
            <p>امتیاز شما:</p>
            <span class="score-big">${score} از ${questions.length}</span>
            <p class="${colorClass}">${message}</p>
        `;
    }
</script>

</body>
</html>
