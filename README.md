<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>حيوان / جماد / ∞</title>

<style>
body{
  font-family: Arial, sans-serif;
  background: linear-gradient(to right,#fceabb,#f8b500);
  text-align:center;
  margin:0;
}

button{
  padding:12px 25px;
  font-size:16px;
  border:none;
  border-radius:10px;
  cursor:pointer;
  background:#ffcc00;
}
button:hover{background:#ffaa00}

table{
  width:98%;
  margin:auto;
  border-collapse:collapse;
}
th,td{
  border:2px solid #333;
}
th{
  background:#333;
  color:white;
  padding:8px;
}
td{
  height:70px;
}

textarea{
  width:100%;
  height:100%;
  resize:none;
  text-align:center;
  font-size:15px;
}

.sum-col{
  width:70px;
  background:#eee;
}

#timer{
  font-size:22px;
  margin:15px;
}

button.cell-btn{
  width:100%;
  height:100%;
  background:#ff7777;
  color:white;
  font-size:15px;
  font-weight:bold;
}
button.cell-btn.strike{
  text-decoration:line-through;
  background:#999;
}
</style>
</head>

<body>

<!-- الصفحة الرئيسية -->
<div id="landing">
  <h1>حيوان / جماد / ∞</h1>
  <p>حياكم في لعبة حيوان / جماد / ∞</p>
  <button onclick="showRules()">قوانين اللعبة</button>
  <button onclick="startGame()">بدء اللعبة</button>
</div>

<!-- صفحة القوانين -->
<div id="rules" style="display:none;padding:20px">
  <h2>قوانين لعبة جماد حيوان (النظام المطوّر)</h2>
  <p>بعد اختيار الحرف يبدأ اللاعبون بالكتابة حتى انتهاء الوقت فقط.</p>
  <p>بعدها يتم شطب الإجابات المكررة يدويًا.</p>
  <button onclick="startGame()">بدء اللعبة</button>
</div>

<!-- صفحة اللعبة -->
<div id="game" style="display:none">

<div id="timer">00:00</div>

<select id="timeSelect">
  <option value="60">دقيقة</option>
  <option value="120">دقيقتان</option>
  <option value="180">3 دقائق</option>
</select>

<button onclick="startTimer()">بدء الجولة</button>

<table id="table">
<thead>
<tr>
  <th class="sum-col">المجموع</th>
  <th>10</th><th>9</th><th>8</th><th>7</th><th>6</th>
  <th>5</th><th>4</th><th>3</th><th>2</th><th>1</th>
</tr>
</thead>

<tbody id="body"></tbody>
</table>

<br>
<button onclick="calculate()">حساب النقاط</button>
<button onclick="nextRound()">الجولة التالية</button>
<button onclick="finish()">إنهاء اللعبة</button>

</div>

<script>
let timer,active=false;

function showRules(){
  landing.style.display="none";
  rules.style.display="block";
}

function startGame(){
  landing.style.display="none";
  rules.style.display="none";
  game.style.display="block";
  nextRound();
}

function startTimer(){
  let time=+timeSelect.value;
  active=true;
  enable(true);

  timer=setInterval(()=>{
    timerDiv(time--);
    if(time<0){
      clearInterval(timer);
      active=false;
      enable(false);
      convert();
    }
  },1000);
}

function timerDiv(t){
  let m=Math.floor(t/60),s=t%60;
  timer.textContent=`${m}:${s.toString().padStart(2,"0")}`;
}

function enable(v){
  document.querySelectorAll("textarea").forEach(t=>t.disabled=!v);
}

function convert(){
  document.querySelectorAll("textarea").forEach(t=>{
    if(t.value.trim()){
      let b=document.createElement("button");
      b.className="cell-btn";
      b.textContent=t.value;
      b.onclick=()=>b.classList.toggle("strike");
      t.parentNode.replaceChild(b,t);
    }
  });
}

function calculate(){
  document.querySelectorAll("#body tr").forEach(row=>{
    let sum=0;
    row.querySelectorAll("td").forEach((td,i)=>{
      if(i>0){
        let el=td.firstChild;
        if(el && el.tagName==="BUTTON" && !el.classList.contains("strike")){
          sum+= el.textContent.includes("\n") ? 2 : 1;
        }
      }
    });
    row.querySelector(".sum-col input").value=sum;
  });
}

function nextRound(){
  let tr=document.createElement("tr");

  let sumTd=document.createElement("td");
  sumTd.className="sum-col";
  let inp=document.createElement("input");
  inp.readOnly=true;
  sumTd.appendChild(inp);
  tr.appendChild(sumTd);

  for(let i=0;i<10;i++){
    let td=document.createElement("td");
    let ta=document.createElement("textarea");
    ta.disabled=true;
    ta.onkeydown=e=>{
      if(!active){e.preventDefault();return;}
      if(e.key==="Enter" && !ta.value.includes("\n")){
        e.preventDefault();
        ta.value+="\n";
      }
    }
    td.appendChild(ta);
    tr.appendChild(td);
  }
  body.appendChild(tr);
}

function finish(){
  calculate();
  let total=0;
  document.querySelectorAll(".sum-col input").forEach(i=>{
    total+= +i.value;
  });
  alert("النتيجة النهائية: "+total+" نقطة");
}
</script>

</body>
</html>
