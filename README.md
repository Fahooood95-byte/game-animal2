<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حيوان / جماد / ∞</title>
    <style>
        body {
            margin: 0;
            font-family: "Tahoma", sans-serif;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: #222;
            text-align: center;
        }
        .container {
            padding: 20px;
        }
        h1 {
            font-size: 36px;
            margin-bottom: 10px;
        }
        button {
            padding: 12px 20px;
            margin: 8px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            cursor: pointer;
        }
        .primary {
            background: #4CAF50;
            color: white;
        }
        .secondary {
            background: #2196F3;
            color: white;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
            background: white;
            border-radius: 12px;
            overflow: hidden;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 6px;
            min-width: 80px;
        }
        .timer {
            font-size: 22px;
            margin: 10px;
        }
    </style>
</head>
<body>
    <!-- الصفحة الرئيسية -->
    <div id="home" class="container">
        <h1>حيوان / جماد / ∞</h1>
        <h2>حياكم في لعبة حيوان / جماد / ∞</h2>
        <button class="secondary" onclick="showRules()">قوانين اللعبة</button>
        <button class="primary" onclick="startGame()">بدء اللعبة</button>
    </div>

    <!-- صفحة القوانين -->
    <div id="rules" class="container" style="display: none;">
        <h2>قوانين لعبة جماد حيوان (النظام المطوّر)</h2>
        <p style="text-align:right; line-height:1.8">
            أولًا: اختيار الحرف<br>
            يتم اختيار الحرف إما عن طريق البرنامج أو بالاتفاق بين اللاعبين وبالدور.<br><br>
            ثانيًا: بدء الجولة<br>
            بعد اختيار الحرف، يبدأ جميع اللاعبين بكتابة الإجابات.<br><br>
            ثالثًا: انتهاء الوقت<br>
            عند انتهاء الوقت، يُمنع الجميع من إضافة أو تعديل أي إجابة.<br><br>
            رابعًا: مراجعة الإجابات<br>
            يتم شطب الإجابات المتكررة يدويًا حسب نظام النقاط.<br><br>
            نظام النقاط:<br>
            الفردي = 1 نقطة<br>
            الثنائي = 2 نقاط
        </p>
        <button class="primary" onclick="startGame()">بدء اللعبة</button>
    </div>

    <!-- صفحة اللعبة -->
    <div id="game" class="container" style="display: none;">
        <div class="timer" id="timer">00:00</div>
        <select id="timeSelect">
            <option value="60">دقيقة</option>
            <option value="120">دقيقتان</option>
            <option value="180">ثلاث دقائق</option>
        </select>
        <br>
        <button class="primary" onclick="startTimer()">بدء</button>
        <table id="gameTable"></table>
        <button class="secondary" onclick="calculate()">حساب النقاط</button>
        <button class="primary" onclick="nextRound()">الجولة التالية</button>
        <button class="danger" onclick="endGame()">إنهاء اللعبة</button>
    </div>

    <!-- صفحة النتيجة -->
    <div id="result" class="container" style="display: none;">
        <h2>النتيجة النهائية</h2>
        <h1 id="finalScore">0</h1>
        <button class="primary" onclick="location.reload()">إعادة اللعب</button>
    </div>

    <script>
        let timerInterval;
        let timeLeft;
        let totalScore = 0;

        function showRules() {
            document.getElementById('home').style.display = 'none';
            document.getElementById('rules').style.display = 'block';
        }

        function startGame() {
            document.getElementById('home').style.display = 'none';
            document.getElementById('rules').style.display = 'none';
            document.getElementById('game').style.display = 'block';
            nextRound();
        }

        function startTimer() {
            clearInterval(timerInterval);
            timeLeft = parseInt(document.getElementById('timeSelect').value);
            updateTimer();
            timerInterval = setInterval(() => {
                timeLeft--;
                updateTimer();
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                }
            }, 1000);
        }

        function updateTimer() {
            let m = Math.floor(timeLeft / 60);
            let s = timeLeft % 60;
            document.getElementById('timer').innerText = `${m}:${s.toString().padStart(2, '0')}`;
        }

        function nextRound() {
            // إضافة صف جديد للجدول
        }

        function calculate() {
            // حساب النقاط
        }

        function endGame() {
            document.getElementById('game').style.display = 'none';
            document.getElementById('result').style.display = 'block';
            document.getElementById('finalScore').innerText = totalScore;
        }
    </script>
</body>
</html>
