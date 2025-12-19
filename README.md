<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>حيوان / جماد / ∞</title>
<style>
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(120deg, #f6d365, #fda085);
    margin: 0;
    padding: 0;
    direction: rtl;
  }
  h1, h2, h3 {
    text-align: center;
    margin: 10px 0;
  }
  button {
    padding: 10px 20px;
    margin: 5px;
    font-size: 16px;
    cursor: pointer;
    border: none;
    border-radius: 8px;
    background-color: #ff6b6b;
    color: white;
    transition: 0.3s;
  }
  button:hover {
    background-color: #ff8787;
  }
  .container {
    width: 90%;
    max-width: 800px;
    margin: auto;
    padding: 20px;
    text-align: center;
  }
  .hidden {
    display: none;
  }
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
  }
  td, th {
    border: 1px solid #fff;
    padding: 10px;
    text-align: center;
    font-size: 16px;
  }
  input {
    width: 90%;
    padding: 5px;
    font-size: 16px;
  }
  .single {
    background-color: #ff4d4d;
    color: white;
    padding: 2px 6px;
    border-radius: 4px;
    margin-left: 5px;
  }
  .double {
    background-color: #2ed573;
    color: white;
    padding: 2px 6px;
    border-radius: 4px;
    margin-left: 5px;
  }
  .timer {
    font-size: 24px;
    margin-top: 10px;
    font-weight: bold;
  }
  .button-row {
    margin-top: 20px;
  }
  .btn-end {
    background-color: #3742fa;
  }
</style>
</head>
<body>

<!-- الصفحة الرئيسية -->
<div id="homePage" class="container">
  <h1>حيوان / جماد / ∞</h1>
  <h2>حياكم في لعبة حيوان / جماد / ∞</h2>
  <div class="button-row">
    <button onclick="showPage('rulesPage')">قوانين اللعبة</button>
    <button onclick="showPage('gamePage')">بدء اللعبة</button>
  </div>
</div>

<!-- صفحة القوانين -->
<div id="rulesPage" class="container hidden">
  <h2>قوانين لعبة جماد حيوان (النظام المطوّر)</h2>
  <p><strong>أولًا: اختيار الحرف</strong><br>يتم اختيار الحرف إما عن طريق البرنامج أو بالاتفاق بين اللاعبين وبالدور.</p>
  <p><strong>ثانيًا: بدء الجولة</strong><br>بعد اختيار الحرف، يبدأ جميع اللاعبين بكتابة الإجابات في جميع الفئات المختارة من المصاطر المتوفرة لديهم. تستمر الكتابة طوال الوقت المحدد فقط.</p>
  <p><strong>ثالثًا: انتهاء الوقت</strong><br>عند انتهاء الوقت، يُمنع الجميع من إضافة أو تعديل أي إجابة.</p>
  <p><strong>رابعًا: مراجعة الإجابات</strong><br>بعد الانتهاء، يبدأ النقاش بين اللاعبين للتأكد من صحة الإجابات وتوافقها مع الحرف المطلوب. يتم شطب جميع الإجابات المتكررة بين اللاعبين حسب نظام النقاط الموضح أدناه.</p>
  
  <h3>نظام احتساب النقاط</h3>
  <p>أنواع الإجابة: فردي أو ثنائي.</p>
  <ol>
    <li>فردي × فردي: تُشطب الإجابتان وتُلغى النقطة من الطرفين</li>
    <li>ثنائي × فردي: تُشطب الإجابة الثنائية فقط، الفردي يحصل على نقطته</li>
    <li>ثنائي × ثنائي: تُشطب الإجابتان، لا تُحتسب أي نقطة</li>
    <li>إجابة ثنائية غير مكررة: يحصل اللاعب على نقطتين كاملتين</li>
  </ol>
  <p>جمع النقاط: يُحسب مجموع النقاط من الإجابات الصحيحة وغير المكررة. الأعلى مجموعًا هو الفائز.</p>

  <div class="button-row">
    <button onclick="showPage('gamePage')">بدء اللعبة</button>
  </div>
</div>

<!-- صفحة اللعبة -->
<div id="gamePage" class="container hidden">
  <h2>صفحة اللعبة</h2>
  <div class="timer" id="timerDisplay">00:00</div>
  <div class="button-row">
    <button onclick="setTimer(1)">1 دقيقة</button>
    <button onclick="setTimer(2)">2 دقيقة</button>
    <button onclick="setTimer(3)">3 دقائق</button>
    <button onclick="startTimer()">بدء</button>
  </div>

  <table id="gameTable">
    <thead>
      <tr>
        <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
        <th>6</th><th>7</th><th>8</th><th>9</th><th>10</th>
        <th>المجموع</th>
      </tr>
    </thead>
    <tbody>
      <tr id="currentRow">
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" oninput="markSingleOrDouble(this)"></td>
        <td><input type="text" disabled></td>
      </tr>
    </tbody>
  </table>

  <div class="button-row">
    <button onclick="calculatePoints()">حساب النقاط</button>
    <button onclick="nextRound()">الجولة التالية</button>
    <button class="btn-end" onclick="endGame()">إنهاء اللعبة</button>
  </div>
</div>

<!-- صفحة النتائج -->
<div id="resultPage" class="container hidden">
  <h2>النتيجة النهائية</h2>
  <div id="finalResults"></div>
  <div class="button-row">
    <button onclick="location.reload()">العودة للصفحة الرئيسية</button>
  </div>
</div>

<script>
  let currentTimer = 0;
  let timerInterval;
  
  function showPage(pageId) {
    document.querySelectorAll('.container').forEach(div => div.classList.add('hidden'));
    document.getElementById(pageId).classList.remove('hidden');
  }

  function setTimer(minutes) {
    currentTimer = minutes * 60;
    updateTimerDisplay();
  }

  function startTimer() {
    if(currentTimer <= 0) return alert("اختر مدة زمنية أولاً!");
    clearInterval(timerInterval);
    timerInterval = setInterval(() => {
      if(currentTimer <= 0) {
        clearInterval(timerInterval);
        disableInputs();
        return;
      }
      currentTimer--;
      updateTimerDisplay();
    }, 1000);
  }

  function updateTimerDisplay() {
    const mins = Math.floor(currentTimer / 60).toString().padStart(2,'0');
    const secs = (currentTimer % 60).toString().padStart(2,'0');
    document.getElementById('timerDisplay').innerText = `${mins}:${secs}`;
  }

  function markSingleOrDouble(input) {
    const value = input.value.trim();
    if(!value) return;
    if(value.includes('\n')) {
      input.nextSibling?.remove();
      const span = document.createElement('span');
      span.className = 'double';
      span.innerText = 'ثنائي';
      input.parentNode.appendChild(span);
    } else {
      input.nextSibling?.remove();
      const span = document.createElement('span');
      span.className = 'single';
      span.innerText = 'فردي';
      input.parentNode.appendChild(span);
    }
  }

  function disableInputs() {
    document.querySelectorAll('#currentRow input').forEach(input => input.disabled = true);
  }

  function calculatePoints() {
    const row = document.getElementById('currentRow');
    let total = 0;
    row.querySelectorAll('td').forEach((td, index) => {
      if(index === 10) return;
      const span = td.querySelector('span');
      if(span) total += (span.className === 'single') ? 1 : 2;
    });
    row.cells[10].innerText = total;
  }

  function nextRound() {
    const table = document.getElementById('gameTable').getElementsByTagName('tbody')[0];
    const newRow = table.rows[0].cloneNode(true);
    newRow.id = 'currentRow';
    newRow.querySelectorAll('input').forEach((input, index) => {
      if(index === 10) input.value = '';
      else { input.value=''; input.disabled=false; input.nextSibling?.remove(); }
    });
    table.appendChild(newRow);
  }

  function endGame() {
    showPage('resultPage');
    const results = Array.from(document.querySelectorAll('#gameTable tbody tr'))
      .map(r => parseInt(r.cells[10].innerText)||0);
    const sum = results.reduce((a,b)=>a+b,0);
    document.getElementById('finalResults').innerText = `مجموع النقاط النهائي: ${sum}`;
  }
</script>

</body>
</html>
