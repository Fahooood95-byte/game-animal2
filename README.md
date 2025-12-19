<!-- index.html -->
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>حيوان / جماد / ∞ - اللعبة</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <main id="app">
    <!-- Landing Page -->
    <section id="landing" class="page active">
      <header class="brand">
        <h1 class="logo">حيوان / جماد / ∞</h1>
      </header>
      <p class="welcome">حياكم في لعبة حيوان / جماد / ∞</p>
      <div class="cta">
        <button id="btnRules" class="btn btn-outline">قوانين اللعبة</button>
        <button id="btnStart" class="btn btn-primary">بدء اللعبة</button>
      </div>
    </section>

    <!-- Rules Page -->
    <section id="rules" class="page">
      <article class="card">
        <h2>قوانين لعبة جماد حيوان (النظام المطوّر)</h2>
        <p>أولًا: اختيار الحرف</p>
        <p>يتم اختيار الحرف إما عن طريق البرنامج أو بالاتفاق بين اللاعبين وبالدور.</p>
        <p>ثانيًا: بدء الجولة</p>
        <p>بعد اختيار الحرف، يبدأ جميع اللاعبين بكتابة الإجابات في جميع الفئات المختارة من المصاطر المتوفرة لديهم. تستمر الكتابة طوال الوقت المحدد فقط.</p>
        <p>ثالثًا: انتهاء الوقت</p>
        <p>عند انتهاء الوقت، يُمنع الجميع من إضافة أو تعديل أي إجابة.</p>
        <p>رابعًا: مراجعة الإجابات</p>
        <p>بعد الانتهاء، يبدأ النقاش بين اللاعبين لتأكيد صحة الإجابات وتوافقها مع الحرف المطلوب. يتم شطب جميع الإجابات المتكررة حسب النظام أدناه.</p>
        <!-- أكمل بقية النص كما هو -->
        <button id="startFromRules" class="btn btn-primary">بدء اللعبة</button>
      </article>
    </section>

    <!-- Game Page -->
    <section id="game" class="page">
      <div class="toolbar">
        <select id="timeLimit" aria-label="وقت">
          <option value="60">دقيقة واحدة</option>
          <option value="120">دقيقتان</option>
          <option value="180">ثلاث دقائق</option>
        </select>
        <button id="btnPlay" class="btn btn-success">ابدأ</button>
      </div>

      <table id="scoreTable" class="score-table" aria-label="جدول النقاط">
        <thead>
          <tr>
            <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
            <th>6</th><th>7</th><th>8</th><th>9</th><th>10</th><th>المجموع</th>
          </tr>
        </thead>
        <tbody id="row1">
          <tr>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td><input type="text" maxlength="1" class="cell" /></td>
            <td class="sumCell" aria-label="المجموع"></td>
          </tr>
        </tbody>
      </table>

      <div class="controls">
        <button id="btnScore" class="btn btn-primary">حساب النقاط</button>
        <button id="btnNextRound" class="btn btn-secondary" disabled>الجولة التالية</button>
        <button id="btnEndGame" class="btn btn-danger">إنهاء اللعبة</button>
      </div>
    </section>
  </main>

  <script src="app.js"></script>
  <style>
    /* تضمين مبسط للأنماط هنا، يمكنك وضعها في styles.css لاحقًا */
  </style>
</body>
</html>
// app.js (مخطط بسيط لتجربة المبدأ)
document.addEventListener('DOMContentLoaded', () => {
  const landing = document.getElementById('landing');
  const rules = document.getElementById('rules');
  const game = document.getElementById('game');
  const btnStart = document.getElementById('btnStart');
  const btnRules = document.getElementById('btnRules');
  const startFromRules = document.getElementById('startFromRules');
  const btnPlay = document.getElementById('btnPlay');
  const timeLimit = document.getElementById('timeLimit');
  const btnScore = document.getElementById('btnScore');
  const btnNextRound = document.getElementById('btnNextRound');
  const btnEndGame = document.getElementById('btnEndGame');
  const sumCell = document.querySelector('.sumCell');
  const cells = document.querySelectorAll('.cell');

  function show(page) {
    [landing, rules, game].forEach(p => p.classList.remove('active'));
    page.classList.add('active');
  }

  btnRules.addEventListener('click', () => show(rules));
  btnStart.addEventListener('click', () => show(game));
  startFromRules.addEventListener('click', () => show(game));

  // Prototyping: simple timer
  let timer = null;
  btnPlay.addEventListener('click', () => {
    // iniciar timer... para el prototipo
    alert('المؤقت سيبدأ الآن (تمثيل بسيط).');
  });

  btnScore.addEventListener('click', () => {
    // حساب بسيط: مجموع الخانات كإطار عام
    let sum = 0;
    cells.forEach((c) => {
      const v = c.value.trim();
      if (v) sum += 1; // ترجيح مرحلي: عد الخانات غير الفارغة
    });
    sumCell.textContent = sum;
    btnNextRound.disabled = false;
  });

  btnNextRound.addEventListener('click', () => {
    // إضافة صف جديد بسيط
    const table = document.getElementById('scoreTable');
    const tbody = table.querySelector('tbody');
    const newRow = document.createElement('tr');
    for (let i = 0; i < 11; i++) {
      const td = document.createElement(i === 10 ? 'td' : 'td');
      if (i < 10) {
        const input = document.createElement('input');
        input.type = 'text';
        input.maxLength = 1;
        input.className = 'cell';
        td.appendChild(input);
      } else {
        td.className = 'sumCell';
      }
      newRow.appendChild(td);
    }
    tbody.appendChild(newRow);
  });

  btnEndGame.addEventListener('click', () => {
    // صفحة نتيجة نهائية بسيطة
    alert('نهاية اللعبة. ستعرض النتيجة النهائية في صفحة النتائج الحقيقية لاحقًا.');
  });
});
