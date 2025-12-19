<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>حيوان / جماد / ∞</title>
<style>
body {
  font-family: Arial;
  direction: rtl;
  text-align: center;
  background: #f5f5f5;
}

button {
  padding: 10px 15px;
  margin: 5px;
  font-size: 16px;
}

.table-container {
  max-height: 70vh;
  overflow-y: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #999;
  padding: 5px;
}

th {
  background: #ddd;
  position: sticky;
  top: 0;
}

.cell-box {
  position: relative;
}

.cell-number {
  position: absolute;
  top: 2px;
  left: 2px;
  font-size: 10px;
  color: #666;
}

textarea {
  width: 100%;
  height: 60px;
  resize: none;
}

button.answer-btn {
  width: 100%;
  height: 60px;
}

.strike {
  text-decoration: line-through;
  background: #fbb;
}
</style>
</head>

<body>

<h1>حيوان / جماد / ∞</h1>

<button onclick="startTimer()">ابدأ الجولة</button>
<button onclick="endGame()">إنهاء اللعبة</button>
<p id="timer">الوقت: 0</p>

<div class="table-container">
<table id="gameTable">
<thead>
<tr>
<th>المجموع</th>
<script>
for (let i = 10; i >= 1; i--) {
  document.write(`<th>${i}</th>`);
}
</script>
</tr>
</thead>
<tbody id="tableBody"></tbody>
</table>
</div>

<script>
let time = 60;
let timerInterval;
let writingEnabled = false;
let cellCounter = 1;

function createRow() {
  const tr = document.createElement("tr");

  const totalTd = document.createElement("td");
  totalTd.className = "total";
  totalTd.textContent = "0";
  tr.appendChild(totalTd);

  for (let i = 0; i < 10; i++) {
    const td = document.createElement("td");
    const box = document.createElement("div");
    box.className = "cell-box";

    const num = document.createElement("div");
    num.className = "cell-number";
    num.textContent = cellCounter++;
    box.appendChild(num);

    const textarea = document.createElement("textarea");
    textarea.disabled = true;
    box.appendChild(textarea);

    td.appendChild(box);
    tr.appendChild(td);
  }

  document.getElementById("tableBody").appendChild(tr);
}

for (let i = 0; i < 10; i++) createRow();

function startTimer() {
  clearInterval(timerInterval);
  time = 60;
  writingEnabled = true;
  document.querySelectorAll("textarea").forEach(t => t.disabled = false);

  timerInterval = setInterval(() => {
    time--;
    document.getElementById("timer").textContent = "الوقت: " + time;
    if (time <= 0) endRound();
  }, 1000);
}

function endRound() {
  clearInterval(timerInterval);
  writingEnabled = false;

  document.querySelectorAll("textarea").forEach(t => {
    const btn = document.createElement("button");
    btn.className = "answer-btn";
    btn.textContent = t.value || "—";
    btn.onclick = () => toggleStrike(btn);
    t.replaceWith(btn);
  });

  calculateTotals();
}

function toggleStrike(btn) {
  btn.classList.toggle("strike");
  calculateTotals();
}

function calculateTotals() {
  document.querySelectorAll("#tableBody tr").forEach(row => {
    let score = 0;
    row.querySelectorAll(".answer-btn").forEach(btn => {
      if (!btn.classList.contains("strike") && btn.textContent !== "—") {
        score++;
      }
    });
    row.querySelector(".total").textContent = score;
  });
}

function endGame() {
  let total = 0;
  document.querySelectorAll(".total").forEach(t => {
    total += parseInt(t.textContent);
  });
  alert("النتيجة النهائية: " + total);
}
</script>

</body>
</html>
