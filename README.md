<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>حيوان / جماد / ∞</title>

<style>
body{
    font-family: Arial;
    background: linear-gradient(135deg,#ffd89b,#19547b);
    margin:0;
    padding:20px;
    color:#222;
}

.hidden{display:none}

button{
    padding:12px 20px;
    font-size:16px;
    border:none;
    border-radius:8px;
    cursor:pointer;
    background:#ff9800;
    color:#fff;
}

button:hover{opacity:.9}

.center{text-align:center}

table{
    width:100%;
    border-collapse:collapse;
    margin-top:15px;
}

th,td{
    border:2px solid #333;
    text-align:center;
    padding:4px;
}

th{
    background:#333;
    color:#fff;
    font-size:14px;
}

textarea{
    width:100%;
    height:52px;
    resize:none;
    font-size:14px;
    text-align:center;
    border:none;
    outline:none;
}

textarea:disabled{
    background:#eee;
}

.small{
    width:60px;
    font-weight:bold;
    background:#fafafa;
}

.cell-btn{
    width:100%;
    height:52px;
    background:#fafafa;
    border:none;
    cursor:pointer;
}

.crossed{
    text-decoration: line-through;
    background:#ffdddd;
}

.tag{
    font-size:11px;
    padding:2px 6px;
    border-radius:5px;
    display:inline-block;
    margin-top:2px;
}

.single{background:#e53935;color:#fff}
.double{background:#43a047;color:#fff}

.controls{margin:10px 0}
</style>
</head>

<body>

<!-- الصفحة الرئيسية -->
<div id="home" class="center">
    <h1>حيوان / جماد / ∞</h1>
    <p>حياكم في لعبة حيوان / جماد / ∞</p>
    <button onclick="showRules()">قوانين اللعبة</button>
    <br><br>
    <button onclick="startGame()">بدء اللعبة</button>
</div>

<!-- القوانين -->
<div id="rules" class="hidden">
    <h2>قوانين لعبة جماد حيوان (النظام المطوّر)</h2>
    <p>
    اختيار الحرف – كتابة أثناء الوقت – شطب يدوي – نظام فردي / ثنائي – جمع النقاط
    </p>
    <button onclick="startGame()">بدء اللعبة</button>
</div>

<!-- صفحة اللعبة -->
<div id="game" class="hidden">

<div class="controls">
<select id="timeSelect">
<option value="60">دقيقة</option>
<option value="120">دقيقتان</option>
<option value="180">3 دقائق</option>
</select>

<button onclick="startTimer()">بدء</button>
<span id="timer">00:00</span>
</div>

<table id="gameTable">
<thead>
<tr>
<th class="small">المجموع</th>
<th>10</th><th>9</th><th>8</th><th>7</th><th>6</th>
<th>5</th><th>4</th><th>3</th><th>2</th><th>1</th>
</tr>
</thead>
<tbody></tbody>
</table>

<br>
<button onclick="calcPoints()">حساب النقاط</button>
<button onclick="nextRound()">الجولة التالية</button>
<button onclick="endGame()">إنهاء اللعبة</button>

</div>

<script>
let timerRunning=false;
let interval;
let tbody=document.querySelector("#gameTable tbody");

function showRules(){
    home.classList.add("hidden");
    rules.classList.remove("hidden");
}

function startGame(){
    home.classList.add("hidden");
    rules.classList.add("hidden");
    game.classList.remove("hidden");
    addRow();
}

function addRow(){
    let tr=document.createElement("tr");
    tr.innerHTML=`<td class="small">0</td>`;
    for(let i=10;i>=1;i--){
        tr.innerHTML+=`
        <td>
            <textarea disabled
            oninput="updateType(this)"
            ></textarea>
            <div class="tag single">فردي</div>
        </td>`;
    }
    tbody.appendChild(tr);
}

function updateType(el){
    let tag=el.nextElementSibling;
    if(el.value.includes("\n")){
        tag.textContent="ثنائي";
        tag.className="tag double";
    }else{
        tag.textContent="فردي";
        tag.className="tag single";
    }
}

function startTimer(){
    clearInterval(interval);
    let t=parseInt(timeSelect.value);
    timerRunning=true;
    document.querySelectorAll("textarea").forEach(t=>t.disabled=false);
    interval=setInterval(()=>{
        let m=Math.floor(t/60);
        let s=t%60;
        timer.textContent=`${m}:${s.toString().padStart(2,"0")}`;
        t--;
        if(t<0){
            clearInterval(interval);
            timerRunning=false;
            lockCells();
        }
    },1000);
}

function lockCells(){
    document.querySelectorAll("textarea").forEach(t=>{
        let btn=document.createElement("button");
        btn.className="cell-btn";
        btn.innerHTML=t.value.replace(/\n/g,"<br>");
        btn.onclick=()=>btn.classList.toggle("crossed");
        t.parentElement.replaceChild(btn,t);
    });
}

function calcPoints(){
    tbody.querySelectorAll("tr").forEach(tr=>{
        let sum=0;
        tr.querySelectorAll(".cell-btn").forEach(btn=>{
            if(!btn.classList.contains("crossed")){
                sum+=btn.innerHTML.includes("<br>")?2:1;
            }
        });
        tr.children[0].textContent=sum;
    });
}

function nextRound(){ addRow(); }

function endGame(){
    let total=0;
    tbody.querySelectorAll("tr").forEach(tr=>{
        total+=parseInt(tr.children[0].textContent||0);
    });
    alert("النتيجة النهائية: "+total);
}
</script>

</body>
</html>
