<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>حيوان / جماد / ∞</title>
<style>
  body {
    font-family: "Arial", sans-serif;
    background: linear-gradient(to right, #fceabb, #f8b500);
    color: #333;
    margin: 0;
    padding: 0;
    text-align: center;
  }
  h1 { margin-top: 30px; font-size: 2.5em; color:#3a3a3a; }
  button {
    margin: 10px;
    padding: 15px 30px;
    font-size: 1.1em;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    background-color: #ffcc00;
    transition: 0.3s;
  }
  button:hover { background-color: #ffaa00; }
  #gameContainer { display: none; padding: 20px; }
  table { margin: 0 auto; border-collapse: collapse; width: 90%; }
  th, td {
    border: 2px solid #333;
    padding: 10px;
    min-width: 120px;
    height: 60px;
    position: relative;
  }
  td input {
    width: 100%;
    height: 100%;
    box-sizing: border-box;
    font-size: 1em;
    padding: 5px;
    border: 1px solid #aaa;
    border-radius: 5px;
    text-align: center;
  }
  td button {
    width: 100%;
    height: 100%;
    background-color: #ff7777;
    color: white;
    font-weight: bold;
    font-size: 1em;
  }
  .green { background-color: #4CAF50; color:white; font-weight:bold; }
  .red { background-color: #f44336; color:white; font-weight:bold; }
  #timer { font-size: 1.5em; margin: 15px; }
</style>
</head>
<body>

<!-- الصفحة الرئيسية -->
<div id="landingPage">
  <h1>حيوان / جماد / ∞</h1>
  <p>حياكم في لعبة حيوان / جماد / ∞</p>
  <button onclick="showRules()">قوانين اللعبة</button>
  <button onclick="startGame()">بدء اللعبة</button>
</div>

<!-- صفحة القوانين -->
<div id="rulesPage" style="display:none; padding:20px;">
  <h2>قوانين لعبة جماد حيوان (النظام المطوّر)</h2>
  <p><b>أولًا: اختيار الحرف</b><br>يتم اختيار الحرف إما عن طريق البرنامج أو بالاتفاق بين اللاعبين وبالدور.</p>
  <p><b>ثانيًا: بدء الجولة</b><br>بعد اختيار الحرف، يبدأ جميع اللاعبين بكتابة الإجابات في جميع الفئات المختارة من المصاطر المتوفرة لديهم. تستمر الكتابة طوال الوقت المحدد فقط.</p>
  <p><b>ثالثًا: انتهاء الوقت</b><br>عند انتهاء الوقت، يُمنع الجميع من إضافة أو تعديل أي إجابة.</p>
  <p><b>رابعًا: مراجعة الإجابات</b><br>بعد الانتهاء، يبدأ النقاش بين اللاعبين للتأكد من صحة الإجابات وتوافقها مع الحرف المطلوب. يتم شطب جميع الإجابات المتكررة بين اللاعبين حسب نظام النقاط الموضح أدناه.</p>
  <h3>نظام احتساب النقاط (النظام الجديد)</h3>
  <ul style="text-align:right; display:inline-block; text-align: right;">
    <li>إجابة فردية × فردية: تُشطب الإجابتان وتُلغى النقطة من الطرفين.</li>
    <li>إجابة ثنائية × فردي: تُشطب الإجابة الثنائية فقط، الفردي يحتفظ بنقطته.</li>
    <li>إجابة ثنائية × ثنائية: تُشطب الإجابتان ولا تُحتسب أي نقطة.</li>
    <li>إجابة ثنائية غير مكررة: يحصل اللاعب على نقطتين كاملتين.</li>
  </ul>
  <p><b>خامسًا: جمع النقاط</b><br>يتم جمع النقاط من الإجابات الصحيحة وغير المكررة فقط. اللاعب صاحب أعلى مجموع نقاط هو الفائز.</p>
  <button onclick="startGame()">بدء اللعبة</button>
</div>

<!-- صفحة اللعبة -->
<div id="gameContainer">
  <div id="timer">الوقت: 00:00</div>
  <div>
    <label>اختر المدة: </label>
    <select id="timeSelect">
      <option value="60">دقيقة واحدة</option>
      <option value="120">دقيقتان</option>
      <option value="180">ثلاث دقائق</option>
    </select>
    <button onclick="startTimer()">بدء الجولة</button>
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
      <tr id="row1">
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>
        <td><input readonly></td>
      </tr>
    </tbody>
  </table>
  <div style="margin-top:10px;">
    <button onclick="calculatePoints()">حساب النقاط</button>
    <button onclick="nextRound()">الجولة التالية</button>
    <button onclick="endGame()">إنهاء اللعبة</button>
  </div>
</div>

<script>
let timer;
let timeLeft;
let gameStarted = false;

// التنقل بين الصفحات
function showRules() {
  document.getElementById('landingPage').style.display='none';
  document.getElementById('rulesPage').style.display='block';
}
function startGame() {
  document.getElementById('landingPage').style.display='none';
  document.getElementById('rulesPage').style.display='none';
  document.getElementById('gameContainer').style.display='block';
}

// المؤقت
function startTimer() {
  const select = document.getElementById('timeSelect');
  timeLeft = parseInt(select.value);
  if(timer) clearInterval(timer);
  gameStarted = true;
  enableInputs(true);
  timer = setInterval(() => {
    let minutes = Math.floor(timeLeft/60);
    let seconds = timeLeft % 60;
    document.getElementById('timer').innerText = `الوقت: ${minutes.toString().padStart(2,'0')}:${seconds.toString().padStart(2,'0')}`;
    timeLeft--;
    if(timeLeft<0){
      clearInterval(timer);
      document.getElementById('timer').innerText = "انتهى الوقت!";
      gameStarted = false;
      enableInputs(false);
      convertToButtons();
    }
  },1000);
}

// تمكين أو تعطيل الكتابة
function enableInputs(enable){
  const inputs = document.querySelectorAll('td input');
  inputs.forEach(inp => {
    inp.disabled = !enable;
  });
}

// التعامل مع Enter
function checkEnter(e,input){
  if(e.key==='Enter'){
    e.preventDefault();
    if(input.value.indexOf("\n")===-1){
      input.value += "\n"; // السطر الثاني → ثنائي
      input.style.backgroundColor="#c8f5c8"; // أخضر
    }
  }
}

// تحويل الخانات إلى أزرار بعد انتهاء الوقت
function convertToButtons(){
  const inputs = document.querySelectorAll('td input');
  inputs.forEach(inp=>{
    if(!inp.readOnly && inp.value!==''){
      const btn = document.createElement('button');
      btn.innerText = inp.value;
      btn.onclick = () => btn.style.textDecoration = "line-through";
      inp.parentNode.replaceChild(btn, inp);
    }
  });
}

// حساب النقاط
function calculatePoints(){
  const rows = document.querySelectorAll('#gameTable tbody tr');
  rows.forEach(row=>{
    let sum = 0;
    row.querySelectorAll('td').forEach((td,i)=>{
      if(i<10){
        let val=0;
        const child = td.firstChild;
        if(child){
          if(child.tagName==='INPUT'){
            val = child.value.includes("\n") ? 2 : (child.value?1:0);
          } else if(child.tagName==='BUTTON' && child.style.textDecoration!=='line-through'){
            val = child.innerText.includes("\n") ? 2 : (child.innerText?1:0);
          }
        }
        sum += val;
      } else { td.firstChild.value = sum; }
    });
  });
}

// الجولة التالية
function nextRound(){
  const tbody = document.querySelector('#gameTable tbody');
  const row = document.createElement('tr');
  row.innerHTML = `<td><input maxlength="15" onkeydown="checkEnter(event,this)"></td>`.repeat(10)+`<td><input readonly></td>`;
  tbody.appendChild(row);
}

// إنهاء اللعبة
function endGame(){
  calculatePoints();
  alert("تم إنهاء اللعبة! تحقق من عمود المجموع لكل الجولات.");
}
</script>

</body>
</html>
