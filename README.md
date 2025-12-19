<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>حيوان / جماد / ∞</title>
<style>
  body {
    font-family: 'Arial', sans-serif;
    background: linear-gradient(to bottom, #fceabb, #f8b500);
    margin: 0;
    padding: 0;
    text-align: center;
    direction: rtl;
  }
  h1 { font-size: 2em; margin-top: 20px; }
  p { font-size: 1.2em; }
  button {
    padding: 10px 20px;
    margin: 10px;
    font-size: 1em;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    background-color: #4CAF50;
    color: white;
    transition: 0.3s;
  }
  button:hover { background-color: #45a049; }
  .container { max-width: 900px; margin: auto; }
  table { margin: 20px auto; border-collapse: collapse; width: 95%; }
  td, th {
    border: 1px solid #999;
    padding: 8px;
    min-width: 60px;
    text-align: center;
    font-size: 1em;
  }
  input {
    width: 90%;
    padding: 5px;
    font-size: 1em;
    text-align: center;
  }
  .red { background-color: #ff6b6b; color: white; font-weight: bold; padding: 2px 6px; border-radius: 4px; }
  .green { background-color: #4caf50; color: white; font-weight: bold; padding: 2px 6px; border-radius: 4px; }
  .timer { font-size: 1.5em; margin: 10px; }
  .hidden { display: none; }
</style>
</head>
<body>

<div id="landing-page" class="container">
  <h1>حيوان / جماد / ∞</h1>
  <p>حياكم في لعبة حيوان / جماد / ∞</p>
  <button onclick="showPage('rules-page')">قوانين اللعبة</button>
  <button onclick="showPage('game-page')">بدء اللعبة</button>
</div>

<div id="rules-page" class="container hidden">
  <h1>قوانين لعبة جماد حيوان (النظام المطوّر)</h1>
  <p>
  <b>أولًا: اختيار الحرف</b><br>
  يتم اختيار الحرف إما عن طريق البرنامج أو بالاتفاق بين اللاعبين وبالدور.<br><br>
  <b>ثانيًا: بدء الجولة</b><br>
  بعد اختيار الحرف، يبدأ جميع اللاعبين بكتابة الإجابات في جميع الفئات المختارة من المصاطر المتوفرة لديهم. تستمر الكتابة طوال الوقت المحدد فقط.<br><br>
  <b>ثالثًا: انتهاء الوقت</b><br>
  عند انتهاء الوقت، يُمنع الجميع من إضافة أو تعديل أي إجابة.<br><br>
  <b>رابعًا: مراجعة الإجابات</b><br>
  بعد الانتهاء، يبدأ النقاش بين اللاعبين للتأكد من صحة الإجابات وتوافقها مع الحرف المطلوب. يتم شطب الإجابات المكررة حسب نظام النقاط أدناه.<br><br>
  <b>نظام احتساب النقاط (النظام الجديد)</b><br>
  فردي × فردي = تُشطب الإجابتان<br>
  ثنائي × فردي = تُشطب الإجابة الثنائية فقط، الفردي يحتسب<br>
  ثنائي × ثنائي = تُشطب الإجابتان، لا تُحتسب نقاط<br>
  ثنائي غير مكرر = نقطتان كاملتان<br><br>
  <b>خامسًا: جمع النقاط</b><br>
  يتم جمع النقاط من الإجابات الصحيحة وغير المكررة فقط. اللاعب صاحب أعلى مجموع نقاط هو الفائز.
  </p>
  <button onclick="showPage('game-page')">بدء اللعبة</button>
  <button onclick="showPage('landing-page')">العودة للصفحة الرئيسية</button>
</div>

<div id="game-page" class="container hidden">
  <h1>اللعبة</h1>
  <div class="timer">
    <label>اختر الوقت: </label>
    <select id="time-select">
      <option value="60">دقيقة واحدة</option>
      <option value="120">دقيقتان</option>
      <option value="180">ثلاث دقائق</option>
    </select>
    <button onclick="startTimer()">بدء المؤقت</button>
    <span id="countdown">00:00</span>
  </div>
  
  <table id="game-table">
    <thead>
      <tr>
        <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
        <th>6</th><th>7</th><th>8</th><th>9</th><th>10</th><th>المجموع</th>
      </tr>
    </thead>
    <tbody id="game-body">
      <tr>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td><input onkeydown="markAnswer(event, this)"></td>
        <td id="sum-0"></td>
      </tr>
    </tbody>
  </table>

  <button onclick="calculatePoints()">حساب النقاط</button>
  <button onclick="nextRound()">الجولة التالية</button>
  <button onclick="endGame()">إنهاء اللعبة</button>

  <div id="final-score" class="hidden">
    <h2>النتيجة النهائية</h2>
    <div id="scoreboard"></div>
    <button onclick="location.reload()">إعادة اللعبة</button>
  </div>
</div>

<script>
function showPage(pageId) {
  document.getElementById('landing-page').classList.add('hidden');
  document.getElementById('rules-page').classList.add('hidden');
  document.getElementById('game-page').classList.add('hidden');
  document.getElementById(pageId).classList.remove('hidden');
}

// Timer
let timerInterval;
function startTimer() {
  clearInterval(timerInterval);
  let select = document.getElementById('time-select');
  let time = parseInt(select.value);
  let display = document.getElementById('countdown');
  let inputs = document.querySelectorAll('#game-table input');
  inputs.forEach(i => i.disabled = false);

  timerInterval = setInterval(() => {
    let minutes = Math.floor(time / 60);
    let seconds = time % 60;
    display.textContent = `${minutes.toString().padStart(2,'0')}:${seconds.toString().padStart(2,'0')}`;
    if(time <= 0) {
      clearInterval(timerInterval);
      inputs.forEach(i => i.disabled = true);
      alert('انتهى الوقت!');
    }
    time--;
  }, 1000);
}

// Mark answer as فردي or ثنائي
function markAnswer(event, input) {
  if(event.key === 'Enter') {
    event.preventDefault();
    if(input.nextElementSibling && input.value !== '') {
      input.classList.remove('red');
      input.classList.add('green');
    }
  } else {
    input.classList.add('red');
    input.classList.remove('green');
  }
}

// Calculate Points
function calculatePoints() {
  let tbody = document.getElementById('game-body');
  tbody.querySelectorAll('tr').forEach((row, index) => {
    let sum = 0;
    row.querySelectorAll('input').forEach(inp => {
      if(inp.classList.contains('red')) sum += 1;
      if(inp.classList.contains('green')) sum += 2;
    });
    row.querySelector(`#sum-${index}`).textContent = sum;
  });
}

// Next Round
function nextRound() {
  let tbody = document.getElementById('game-body');
  let newRow = document.createElement('tr');
  for(let i=0;i<10;i++) {
    let td = document.createElement('td');
    let input = document.createElement('input');
    input.onkeydown = (e) => markAnswer(e, input);
    td.appendChild(input);
    newRow.appendChild(td);
  }
  let sumTd = document.createElement('td');
  sumTd.id = `sum-${tbody.rows.length}`;
  newRow.appendChild(sumTd);
  tbody.appendChild(newRow);
}

// End Game
function endGame() {
  let tbody = document.getElementById('game-body');
  let scores = [];
  tbody.querySelectorAll('tr').forEach((row,index)=>{
    let sum = parseInt(row.querySelector(`#sum-${index}`).textContent)||0;
    scores.push(`الجولة ${index+1}: ${sum} نقطة`);
  });
  document.getElementById('scoreboard').innerHTML = scores.join('<br>');
  document.getElementById('final-score').classList.remove('hidden');
  document.getElementById('game-table').classList.add('hidden');
}
</script>

</body>
</html>
