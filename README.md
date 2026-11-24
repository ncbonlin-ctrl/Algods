<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>صندوق التكافل الاجتماعي</title>
  <style>
    :root {
      --bg: #f4f7f5;
      --surface: #ffffff;
      --primary: #1b5e20;
      --primary-hover: #144718;
      --accent: #2e7d32;
      --text: #1f2933;
      --muted: #52606d;
      --border: #d9e2ec;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: system-ui, -apple-system, "Segoe UI", Tahoma, Arial, sans-serif;
      background-color: var(--bg);
      color: var(--text);
      line-height: 1.7;
    }

    header {
      background: linear-gradient(135deg, var(--primary), var(--accent));
      color: #fff;
      padding: 2.2rem 1.2rem;
      text-align: center;
    }

    header h1 {
      font-size: 2rem;
      margin-bottom: 0.5rem;
    }

    header p {
      font-size: 1.05rem;
      opacity: 0.95;
      max-width: 680px;
      margin: 0 auto;
    }

    .container {
      max-width: 980px;
      margin: 2rem auto;
      padding: 0 1rem;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1.25rem;
      margin-bottom: 2rem;
    }

    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 1.4rem;
      box-shadow: 0 4px 14px rgba(0, 0, 0, 0.04);
    }

    .card h2 {
      font-size: 1.2rem;
      color: var(--primary);
      margin-bottom: 0.5rem;
    }

    .card p {
      color: var(--muted);
      font-size: 0.96rem;
    }

    .support-box {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 1.75rem;
      text-align: center;
      box-shadow: 0 6px 18px rgba(0, 0, 0, 0.05);
    }

    .support-box h2 {
      color: var(--primary);
      margin-bottom: 0.6rem;
      font-size: 1.35rem;
    }

    .support-box p {
      color: var(--muted);
      margin-bottom: 1.2rem;
    }

    .amounts {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 0.65rem;
      margin-bottom: 1.25rem;
    }

    .amount-btn {
      border: 1px solid var(--primary);
      background: #fff;
      color: var(--primary);
      padding: 0.55rem 1.1rem;
      border-radius: 8px;
      font-size: 0.95rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .amount-btn.active,
    .amount-btn:hover {
      background: var(--primary);
      color: #fff;
    }

    .cta-btn {
      background-color: var(--primary);
      color: #fff;
      border: none;
      padding: 0.8rem 1.8rem;
      border-radius: 10px;
      font-size: 1rem;
      font-weight: 700;
      cursor: pointer;
      transition: background-color 0.2s ease;
    }

    .cta-btn:hover {
      background-color: var(--primary-hover);
    }

    .status-msg {
      margin-top: 1rem;
      font-size: 0.95rem;
      color: var(--primary);
      font-weight: 600;
      min-height: 1.5rem;
    }

    footer {
      text-align: center;
      color: var(--muted);
      font-size: 0.9rem;
      padding: 2rem 1rem 2.5rem;
    }
  </style>
</head>
<body>
  <header>
    <h1>صندوق التكافل الاجتماعي</h1>
    <p>مبادرة مجتمعية تهدف إلى دعم الأسر المحتاجة، وتعزيز روح التعاون والتضامن بين أبناء المجتمع.</p>
  </header>

  <main class="container">
    <section class="grid" aria-label="أهداف الصندوق">
      <article class="card">
        <h2>إعانة الأسر</h2>
        <p>تقديم دعم مادي وعيني منظم للأسر الأكثر احتياجاً في الظروف المعيشية الطارئة.</p>
      </article>
      <article class="card">
        <h2>الدعم الصحي والتعليمي</h2>
        <p>المساهمة في تغطية الاحتياجات الأساسية للعلاج والدراسة للفئات المستحقة.</p>
      </article>
      <article class="card">
        <h2>الشفافية والمتابعة</h2>
        <p>توجيه المساهمات بوضوح ومسؤولية لضمان وصول الدعم إلى مستحقيه بأمانة.</p>
      </article>
    </section>

    <section class="support-box" aria-label="المساهمة في الصندوق">
      <h2>ساهم في دعم الصندوق</h2>
      <p>اختر قيمة المساهمة التقريبية ثم اضغط على زر التأكيد لتجربة واجهة الصفحة.</p>

      <div class="amounts" id="amountGroup">
        <button type="button" class="amount-btn active" data-value="50">50</button>
        <button type="button" class="amount-btn" data-value="100">100</button>
        <button type="button" class="amount-btn" data-value="250">250</button>
        <button type="button" class="amount-btn" data-value="500">500</button>
      </div>

      <button type="button" class="cta-btn" id="confirmBtn">تأكيد المساهمة</button>
      <div class="status-msg" id="statusMsg"></div>
    </section>
  </main>

  <footer>
    صندوق التكافل الاجتماعي — جميع الحقوق محفوظة
  </footer>

  <script>
    const buttons = document.querySelectorAll('.amount-btn');
    const confirmBtn = document.getElementById('confirmBtn');
    const statusMsg = document.getElementById('statusMsg');
    let selectedAmount = '50';

    buttons.forEach((btn) => {
      btn.addEventListener('click', () => {
        buttons.forEach((b) => b.classList.remove('active'));
        btn.classList.add('active');
        selectedAmount = btn.dataset.value;
        statusMsg.textContent = '';
      });
    });

    confirmBtn.addEventListener('click', () => {
      statusMsg.textContent = `تم اختيار مساهمة بقيمة (${selectedAmount}) ضمن معاينة الصفحة.`;
    });
  </script>
</body>
</html>
