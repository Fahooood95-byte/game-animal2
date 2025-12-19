<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حيوان / جماد / ∞</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Readex+Pro:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Readex Pro', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #333;
            direction: rtl;
        }

        .container {
            width: 95%;
            max-width: 1200px;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.15);
            padding: 40px;
            margin: 20px;
        }

        /* ===== الصفحة الرئيسية ===== */
        .landing-page {
            text-align: center;
        }

        .logo {
            font-size: 3.5em;
            font-weight: 700;
            background: linear-gradient(45deg, #f093fb 0%, #f5576c 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 30px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .welcome-text {
            font-size: 1.8em;
            color: #555;
            margin-bottom: 50px;
            font-weight: 600;
        }

        .btn {
            display: inline-block;
            padding: 15px 40px;
            margin: 15px;
            font-size: 1.3em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
            text-decoration: none;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        .btn-primary {
            background: linear-gradient(45deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .btn-secondary {
            background: linear-gradient(45deg, #f093fb 0%, #f5576c 100%);
            color: white;
        }

        .btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }

        /* ===== صفحة القوانين ===== */
        .rules-page {
            display: none;
        }

        .rules-title {
            font-size: 2.5em;
            color: #667eea;
            margin-bottom: 30px;
            text-align: center;
            font-weight: 700;
        }

        .rules-content {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            padding: 30px;
            border-radius: 15px;
            line-height: 2;
            font-size: 1.1em;
            border-right: 5px solid #667eea;
        }

        .rules-content h3 {
            color: #764ba2;
            margin: 20px 0 10px 0;
            font-size: 1.3em;
        }

        .rules-content ul {
            margin-right: 30px;
            margin-bottom: 15px;
        }

        .rules-content li {
            margin-bottom: 8px;
        }

        .rules-content strong {
            color: #f5576c;
        }

        /* ===== صفحة اللعبة ===== */
        .game-page {
            display: none;
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            flex-wrap: wrap;
            gap: 20px;
        }

        .timer-section {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .timer-select {
            padding: 10px 15px;
            border: 2px solid #667eea;
            border-radius: 10px;
            font-size: 1em;
            background: white;
            cursor: pointer;
        }

        .timer-display {
            font-size: 2em;
            font-weight: 700;
            color: #f5576c;
            min-width: 100px;
            text-align: center;
        }

        .btn-small {
            padding: 10px 25px;
            font-size: 1em;
        }

        .timer-controls {
            display: flex;
            gap: 10px;
        }

        .game-table {
            overflow-x: auto;
            margin-bottom: 30px;
        }

        table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        th {
            background: linear-gradient(45deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px 10px;
            font-weight: 600;
            font-size: 1.1em;
        }

        td {
            padding: 0;
            background: #f8f9fa;
            position: relative;
        }

        .cell-input {
            width: 100%;
            height: 60px;
            border: none;
            text-align: center;
            font-size: 1em;
            background: transparent;
            font-family: inherit;
        }

        .cell-input:focus {
            outline: 2px solid #f093fb;
            background: #fff;
        }

        .cell-button {
            width: 100%;
            height: 60px;
            border: none;
            background: #e9ecef;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 1em;
            font-family: inherit;
        }

        .cell-button:hover {
            background: #dee2e6;
        }

        .cell-button.crossed {
            background: #f5576c;
            color: white;
            text-decoration: line-through;
        }

        .answer-type {
            position: absolute;
            top: 5px;
            left: 5px;
            padding: 3px 8px;
            border-radius: 5px;
            font-size: 0.7em;
            font-weight: 600;
        }

        .single {
            background: #f5576c;
            color: white;
        }

        .double {
            background: #28a745;
            color: white;
        }

        .total-cell {
            background: linear-gradient(45deg, #f093fb 0%, #f5576c 100%);
            color: white;
            font-weight: 700;
            font-size: 1.2em;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .game-actions {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }

        /* ===== صفحة النتائج النهائية ===== */
        .results-page {
            display: none;
            text-align: center;
        }

        .results-title {
            font-size: 2.5em;
            color: #667eea;
            margin-bottom: 30px;
            font-weight: 700;
        }

        .final-score {
            font-size: 4em;
            color: #f5576c;
            margin: 40px 0;
            font-weight: 700;
            background: linear-gradient(45deg, #f093fb 0%, #f5576c 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* ===== تصميم متجاوب ===== */
        @media (max-width: 768px) {
            .logo {
                font-size: 2.5em;
            }
            
            .welcome-text {
                font-size: 1.4em;
            }
            
            .btn {
                padding: 12px 30px;
                font-size: 1.1em;
                width: 90%;
                margin: 10px auto;
                display: block;
            }
            
            .container {
                padding: 20px;
            }
            
            .game-header {
                flex-direction: column;
                text-align: center;
            }
            
            th, .cell-input, .cell-button {
                font-size: 0.9em;
            }
        }
    </style>
</head>
<body>
    <!-- ===== الصفحة الرئيسية ===== -->
    <div class="container landing-page" id="landingPage">
        <h1 class="logo">حيوان / جماد / ∞</h1>
        <p class="welcome-text">حياكم في لعبة حيوان / جماد / ∞</p>
        <button class="btn btn-primary" onclick="showRules()">قوانين اللعبة</button>
        <button class="btn btn-secondary" onclick="startGame()">بدء اللعبة</button>
    </div>

    <!-- ===== صفحة القوانين ===== -->
    <div class="container rules-page" id="rulesPage">
        <h2 class="rules-title">📜 قوانين لعبة حيوان / جماد (النظام المطوّر)</h2>
        <div class="rules-content">
            <h3>أولًا: اختيار الحرف</h3>
            <ul>
                <li>يتم اختيار الحرف إما عن طريق البرنامج أو بالاتفاق بين اللاعبين وبالدور.</li>
            </ul>

            <h3>ثانيًا: بدء الجولة</h3>
            <ul>
                <li>بعد اختيار الحرف، يبدأ جميع اللاعبين بكتابة الإجابات في جميع الفئات المختارة من المصاطر المتوفرة لديهم.</li>
                <li>تستمر الكتابة طوال الوقت المحدد فقط.</li>
            </ul>

            <h3>ثالثًا: انتهاء الوقت</h3>
            <ul>
                <li>عند انتهاء الوقت، يُمنع الجميع من إضافة أو تعديل أي إجابة.</li>
            </ul>

            <h3>رابعًا: مراجعة الإجابات</h3>
            <ul>
                <li>بعد الانتهاء، يبدأ النقاش بين اللاعبين للتأكد من صحة الإجابات وتوافقها مع الحرف المطلوب.</li>
                <li>يتم شطب جميع الإجابات المتكررة بين اللاعبين حسب نظام النقاط الموضح أدناه.</li>
            </ul>

            <h3>نظام احتساب النقاط (النظام الجديد)</h3>
            <p><strong>أنواع الإجابة:</strong></p>
            <ul>
                <li>إجابة فردية (إجابة واحدة)</li>
                <li>إجابة ثنائية (إجابتان في نفس الفئة – مخاطرة)</li>
            </ul>

            <p><strong>قواعد احتساب النقاط:</strong></p>
            <ol>
                <li><strong>فردي × فردي:</strong> تُشطب الإجابتان وتُلغى النقطة من الطرفين</li>
                <li><strong>ثنائي × فردي:</strong> تُشطب الإجابة الثنائية فقط، لا تُشطب الإجابة الفردية، اللاعب الفردي يحصل على نقطته</li>
                <li><strong>ثنائي × ثنائي:</strong> تُشطب الإجابتان ولا تُحتسب أي نقطة</li>
                <li><strong>إجابة ثنائية غير مكررة:</strong> يحصل اللاعب على نقطتين كاملتين</li>
            </ol>

            <h3>خامسًا: جمع النقاط</h3>
            <ul>
                <li>يتم جمع النقاط من الإجابات الصحيحة وغير المكررة فقط.</li>
                <li>اللاعب صاحب أعلى مجموع نقاط هو الفائز.</li>
            </ul>
        </div>
        <button class="btn btn-secondary" onclick="startGame()">بدء اللعبة</button>
    </div>

    <!-- ===== صفحة اللعبة ===== -->
    <div class="container game-page" id="gamePage">
        <div class="game-header">
            <div class="timer-section">
                <label>⏱️ المؤقت:</label>
                <select class="timer-select" id="timerSelect">
                    <option value="60">دقيقة واحدة</option>
                    <option value="120">دقيقتان</option>
                    <option value="180">ثلاث دقائق</option>
                </select>
                <div class="timer-display" id="timerDisplay">00:00</div>
            </div>
            <div class="timer-controls">
                <button class="btn btn-primary btn-small" id="startTimer" onclick="startTimer()">ابدأ</button>
                <button class="btn btn-secondary btn-small" id="resetTimer" onclick="resetTimer()">إعادة</button>
            </div>
            <button class="btn btn-secondary btn-small" onclick="endGame()">إنهاء اللعبة</button>
        </div>

        <div class="game-table">
            <table id="gameTable">
                <thead>
                    <tr>
                        <th>1</th>
                        <th>2</th>
                        <th>3</th>
                        <th>4</th>
                        <th>5</th>
                        <th>6</th>
                        <th>7</th>
                        <th>8</th>
                        <th>9</th>
                        <th>10</th>
                        <th>المجموع</th>
                    </tr>
                </thead>
                <tbody id="tableBody">
                    <tr data-row="0">
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="0"></td>
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="1"></td>
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="2"></td>
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="3"></td>
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="4"></td>
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="5"></td>
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="6"></td>
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="7"></td>
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="8"></td>
                        <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="9"></td>
                        <td class="total-cell" id="total-0"></td>
                    </tr>
                </tbody>
            </table>
        </div>

        <div class="game-actions">
            <button class="btn btn-primary" onclick="calculateScore()">حساب النقاط</button>
            <button class="btn btn-secondary" onclick="nextRound()">الجولة التالية</button>
        </div>
    </div>

    <!-- ===== صفحة النتائج النهائية ===== -->
    <div class="container results-page" id="resultsPage">
        <h2 class="results-title">🏆 النتيجة النهائية</h2>
        <p style="font-size: 1.5em; margin-bottom: 30px;">المجموع الكلي للنقاط</p>
        <div class="final-score" id="finalScore">0</div>
        <button class="btn btn-primary" onclick="resetGame()">العودة للصفحة الرئيسية</button>
    </div>

    <script>
        let timerInterval;
        let timeLeft = 0;
        let timerRunning = false;
        let isTimeUp = false;
        let currentRow = 0;
        let totalScore = 0;

        function showPage(pageId) {
            document.querySelectorAll('.container').forEach(page => {
                page.style.display = 'none';
            });
            document.getElementById(pageId).style.display = 'block';
        }

        function showRules() {
            showPage('rulesPage');
        }

        function startGame() {
            showPage('gamePage');
            resetTimer();
            addAnswerTypeLabels();
        }

        function startTimer() {
            if (timerRunning) return;
            
            const select = document.getElementById('timerSelect');
            const selectedTime = parseInt(select.value);
            
            if (timeLeft === 0) {
                timeLeft = selectedTime;
            }
            
            timerRunning = true;
            isTimeUp = false;
            
            document.getElementById('startTimer').disabled = true;
            document.getElementById('timerSelect').disabled = true;
            
            timerInterval = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();
                
                if (timeLeft <= 0) {
                    timeUp();
                }
            }, 1000);
        }

        function resetTimer() {
            clearInterval(timerInterval);
            timerRunning = false;
            isTimeUp = false;
            timeLeft = 0;
            
            document.getElementById('startTimer').disabled = false;
            document.getElementById('timerSelect').disabled = false;
            
            updateTimerDisplay();
            
            // إعادة تمكين الكتابة في جميع الخلايا
            document.querySelectorAll('.cell-input').forEach(input => {
                input.disabled = false;
            });
        }

        function updateTimerDisplay() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            document.getElementById('timerDisplay').textContent = 
                `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }

        function timeUp() {
            clearInterval(timerInterval);
            timerRunning = false;
            isTimeUp = true;
            
            document.getElementById('timerDisplay').textContent = 'انتهى الوقت!';
            document.getElementById('startTimer').disabled = false;
            document.getElementById('timerSelect').disabled = false;
            
            // تحويل الخلايا إلى أزرار
            convertInputsToButtons();
        }

        function convertInputsToButtons() {
            document.querySelectorAll('.cell-input').forEach(input => {
                const value = input.value;
                const cell = input.parentElement;
                const row = input.getAttribute('data-row');
                const col = input.getAttribute('data-col');
                
                input.remove();
                
                const button = document.createElement('button');
                button.className = 'cell-button';
                button.textContent = value || '';
                button.setAttribute('data-row', row);
                button.setAttribute('data-col', col);
                button.onclick = () => toggleCross(button);
                
                cell.appendChild(button);
            });
        }

        function toggleCross(button) {
            if (!isTimeUp) return;
            button.classList.toggle('crossed');
        }

        function handleInput(input, event) {
            if (isTimeUp) {
                input.disabled = true;
                return;
            }
            
            const cell = input.parentElement;
            const answerType = cell.querySelector('.answer-type');
            
            if (event.key === 'Enter') {
                event.preventDefault();
                const lines = input.value.split('\n');
                
                if (lines.length > 1) {
                    answerType.textContent = 'ثنائي';
                    answerType.className = 'answer-type double';
                } else {
                    answerType.textContent = 'فردي';
                    answerType.className = 'answer-type single';
                }
            } else {
                if (input.value.includes('\n')) {
                    answerType.textContent = 'ثنائي';
                    answerType.className = 'answer-type double';
                } else {
                    answerType.textContent = 'فردي';
                    answerType.className = 'answer-type single';
                }
            }
        }

        function addAnswerTypeLabels() {
            document.querySelectorAll('td[data-col]').forEach(cell => {
                if (!cell.querySelector('.answer-type')) {
                    const label = document.createElement('div');
                    label.className = 'answer-type single';
                    label.textContent = 'فردي';
                    cell.appendChild(label);
                }
            });
        }

        function calculateScore() {
            if (!isTimeUp) {
                alert('يجب انتهاء الوقت أولاً!');
                return;
            }
            
            let roundScore = 0;
            const currentRowElement = document.querySelector(`tr[data-row="${currentRow}"]`);
            
            currentRowElement.querySelectorAll('.cell-button').forEach(button => {
                if (!button.classList.contains('crossed')) {
                    const answerType = button.parentElement.querySelector('.answer-type');
                    if (answerType.textContent === 'ثنائي') {
                        roundScore += 2;
                    } else {
                        roundScore += 1;
                    }
                }
            });
            
            totalScore += roundScore;
            document.getElementById(`total-${currentRow}`).textContent = roundScore;
            
            alert(`نقاط هذه الجولة: ${roundScore}`);
        }

        function nextRound() {
            const tbody = document.getElementById('tableBody');
            currentRow++;
            
            const newRow = document.createElement('tr');
            newRow.setAttribute('data-row', currentRow);
            
            for (let i = 0; i < 10; i++) {
                const cell = document.createElement('td');
                const input = document.createElement('input');
                input.type = 'text';
                input.className = 'cell-input';
                input.setAttribute('data-col', i);
                input.setAttribute('data-row', currentRow);
                input.onkeyup = (e) => handleInput(input, e);
                
                const label = document.createElement('div');
                label.className = 'answer-type single';
                label.textContent = 'فردي';
                
                cell.appendChild(input);
                cell.appendChild(label);
                newRow.appendChild(cell);
            }
            
            const totalCell = document.createElement('td');
            totalCell.className = 'total-cell';
            totalCell.id = `total-${currentRow}`;
            newRow.appendChild(totalCell);
            
            tbody.appendChild(newRow);
            
            // إعادة ضبط المؤقت
            resetTimer();
            isTimeUp = false;
        }

        function endGame() {
            showPage('resultsPage');
            document.getElementById('finalScore').textContent = totalScore;
        }

        function resetGame() {
            showPage('landingPage');
            currentRow = 0;
            totalScore = 0;
            
            // إعادة تعيين الجدول
            const tbody = document.getElementById('tableBody');
            tbody.innerHTML = `
                <tr data-row="0">
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="0"></td>
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="1"></td>
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="2"></td>
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="3"></td>
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="4"></td>
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="5"></td>
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="6"></td>
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="7"></td>
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="8"></td>
                    <td><input type="text" class="cell-input" onkeyup="handleInput(this, event)" data-col="9"></td>
                    <td class="total-cell" id="total-0"></td>
                </tr>
            `;
            
            resetTimer();
        }

        // تهيئة الصفحة
        window.onload = () => {
            addAnswerTypeLabels();
        };
    </script>
</body>
</html>
