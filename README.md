<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mahshid Ceram · Loyalty Card</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;700&display=swap');

        :root {
            --bg-color: #f4f7f6;
            --card-bg: #ffffff;
            --primary: #2c7a7b;
            --primary-light: #319795;
            --accent: #dd6b20;
            --text-main: #2d3748;
            --text-muted: #718096;
            --border-radius: 16px;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Vazirmatn', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        .app-container {
            width: 100%;
            max-width: 500px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        /* --- کارت مشتری --- */
        .loyalty-card {
            background: linear-gradient(135deg, var(--primary), var(--primary-light));
            color: white;
            padding: 30px 20px;
            border-radius: var(--border-radius);
            box-shadow: 0 10px 25px rgba(44, 122, 123, 0.3);
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .loyalty-card::before {
            content: '';
            position: absolute;
            top: -50px;
            right: -50px;
            width: 150px;
            height: 150px;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
        }

        .loyalty-card h2 {
            font-size: 1.4rem;
            margin-bottom: 5px;
            font-weight: 700;
        }

        .loyalty-card .code {
            font-size: 1rem;
            opacity: 0.8;
            letter-spacing: 2px;
            margin-bottom: 20px;
        }

        .stamps-container {
            display: flex;
            justify-content: center;
            gap: 12px;
            margin-bottom: 20px;
            direction: ltr; /* مهرها از چپ به راست */
        }

        .stamp {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            border: 2px dashed rgba(255,255,255,0.5);
            background: transparent;
            color: white;
            font-size: 1.2rem;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: all 0.3s ease;
        }

        .stamp.full {
            background: white;
            color: var(--primary);
            border: 2px solid white;
            transform: scale(1.1);
        }

        .stamp:not(.full):hover {
            background: rgba(255,255,255,0.2);
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: rgba(0,0,0,0.2);
            border-radius: 4px;
            margin-bottom: 15px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: #fff;
            width: 0%;
            transition: width 0.4s ease;
        }

        .reward-text {
            font-size: 0.9rem;
            line-height: 1.6;
            background: rgba(0,0,0,0.15);
            padding: 10px;
            border-radius: 8px;
        }

        /* --- پنل ادمین --- */
        .panel {
            background: var(--card-bg);
            padding: 25px;
            border-radius: var(--border-radius);
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
        }

        .panel h2 {
            font-size: 1.1rem;
            margin-bottom: 15px;
            color: var(--primary);
            border-bottom: 2px solid #eee;
            padding-bottom: 8px;
        }

        .field {
            display: block;
            margin-bottom: 15px;
        }

        .field span {
            display: block;
            font-size: 0.85rem;
            margin-bottom: 6px;
            color: var(--text-muted);
        }

        input, select {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid #cbd5e0;
            border-radius: 8px;
            font-family: inherit;
            font-size: 0.95rem;
            transition: border-color 0.2s;
        }

        input:focus, select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(44, 122, 123, 0.1);
        }

        .btn {
            padding: 10px 15px;
            border: none;
            border-radius: 8px;
            font-family: inherit;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 700;
        }

        .btn.primary {
            background: var(--primary);
            color: white;
        }

        .btn.primary:hover {
            background: var(--primary-light);
        }

        .btn.wide {
            width: 100%;
            font-size: 1rem;
            padding: 12px;
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .divider {
            height: 1px;
            background: #eee;
            margin: 25px 0;
        }

        .customer-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px;
            background: #f8fafc;
            border-radius: 8px;
            margin-bottom: 10px;
            border: 1px solid #e2e8f0;
            cursor: pointer;
            transition: all 0.2s;
        }

        .customer-row:hover {
            border-color: var(--primary);
            background: #f0fdf4;
        }

        .customer-info strong {
            display: block;
            font-size: 0.95rem;
        }

        .customer-info span {
            font-size: 0.8rem;
            color: var(--text-muted);
        }

        .footer {
            text-align: center;
            font-size: 0.8rem;
            color: var(--text-muted);
            margin-top: 20px;
        }
        
        .hidden {
            display: none;
        }
    </style>
</head>
<body>

<div class="app-container">
    
    <!-- نمایش کارت مشتری -->
    <div class="loyalty-card">
        <h2 id="customerName">کارت مشتری</h2>
        <div class="code" id="cardCode">کد وفاداری</div>
        
        <div class="stamps-container" id="stamps"></div>
        
        <div class="progress-bar">
            <div class="progress-fill" id="progress"></div>
        </div>
        
        <div class="reward-text" id="reward"></div>
        <div style="margin-top: 15px; font-size: 0.8rem; opacity: 0.8;" id="shareInfo"></div>
    </div>

    <!-- پنل ادمین -->
    <div class="panel" id="adminTools">
        <h2>ساخت کارت مشتری جدید</h2>

        <label class="field">
            <span>نام مشتری</span>
            <input id="newName" placeholder="مثلاً مهشید">
        </label>

        <label class="field">
            <span>کد اختصاصی</span>
            <input id="newCode" placeholder="مثلاً MS-1001">
        </label>

        <label class="field">
            <span>تعداد مهرهای مجاز برای این کارت</span>
            <select id="newLimit">
                <option value="1">۱ مهر</option>
                <option value="2" selected>۲ مهر</option>
                <option value="3">۳ مهر</option>
                <option value="4">۴ مهر</option>
                <option value="5">۵ مهر</option>
            </select>
        </label>

        <button class="btn primary wide" id="create">ساخت کارت</button>

        <div class="divider"></div>

        <h2>کارت‌های مشتریان</h2>
        <p class="muted" style="font-size: 0.8rem; margin-bottom: 15px; color: #718096;">
            برای دیدن کارت هر مشتری، روی اسمش کلیک کنید.
        </p>

        <div id="customers"></div>
    </div>

    <div class="footer">
        Mahshid Ceram · Handmade Pottery
    </div>
</div>

<script>
const STORAGE_KEY = 'mahshidCeramDemo_v3';

let db = {
    customers: {},
    active: null
};

// تبدیل اعداد به فارسی
const fa = n => String(n).replace(/\d/g, d => '۰۱۲۳۴۵۶۷۸۹'[d]);
const el = id => document.getElementById(id);

// جلوگیری از تزریق کد (امنیت)
function safe(s) {
    return String(s).replace(/[&<>"']/g, c => ({
        '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;'
    }[c]));
}

function save() {
    try {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(db));
    } catch (e) {
        alert('ذخیره اطلاعات انجام نشد.');
    }
}

function load() {
    try {
        let x = JSON.parse(localStorage.getItem(STORAGE_KEY));
        if (x && x.customers) db = x;
    } catch (e) {}
}

function renderCard() {
    let c = db.active && db.customers[db.active];
    let limit = c ? Math.max(1, Math.min(5, Number(c.limit) || 5)) : 5;

    el('stamps').innerHTML = '';

    for (let i = 0; i < 5; i++) {
        let d = document.createElement('button');
        d.type = 'button';
        d.className = 'stamp' + (c && i < c.stamps ? ' full' : '');
        d.textContent = c && i < c.stamps ? '❀' : '○';
        d.setAttribute('aria-label', 'جای مهر ' + (i + 1));
        
        if (c && i < limit && i >= c.stamps) {
            d.style.cursor = 'pointer';
        } else {
            d.style.cursor = 'default';
        }

        d.style.opacity = c && i >= limit ? '.35' : '1';
        
        d.title = i >= limit ? 'این جای مهر مجاز نیست' : (c && i < c.stamps ? 'این مهر قبلاً ثبت شده' : 'ثبت مهر');

        d.onclick = () => {
            if (!c) return;

            if (i >= limit) {
                alert('تعداد مهرهای مجاز این کارت ' + fa(limit) + ' تاست.');
                return;
            }
            if (i < c.stamps) {
                alert('این مهر قبلاً ثبت شده است.');
                return;
            }
            if (c.stamps >= limit) {
                alert('تعداد مهرهای مجاز این کارت تکمیل شده است.');
                return;
            }

            c.stamps++;
            save();
            renderCard();
        };

        el('stamps').appendChild(d);
    }

    el('customerName').textContent = c ? 'سلام، ' + c.name + '!' : 'کارت مشتری';
    el('cardCode').textContent = c ? c.code : 'کارت وفاداری';
    
    el('progress').style.width = ((c ? c.stamps : 0) / limit * 100) + '%';

    el('reward').innerHTML = c && c.stamps >= limit
        ? '<strong>تعداد مهرهای مجاز تکمیل شد 🎁</strong><br>برای جایزه با مهشید سرام هماهنگ کن.'
        : '<strong>جایزه‌ات نزدیکه!</strong><br>روی جای مهر بزن؛ بعد از ثبت ' + fa(limit) + ' مهر، مهرهای بیشتر ثبت نمی‌شوند.';

    el('shareInfo').textContent = c 
        ? 'کد کارت تو: ' + c.code + ' · نسخهٔ آزمایشی؛ مهرها فقط در همین مرورگر ذخیره می‌شوند.'
        : 'برای دیدن کارتت، کد مشتری را از پنل بگیر.';
}

function renderCustomers() {
    let root = el('customers');
    root.innerHTML = '';

    let entries = Object.values(db.customers);

    if (!entries.length) {
        root.innerHTML = '<p style="color:#718096; font-size:0.9rem;">هنوز مشتری‌ای ساخته نشده.</p>';
        return;
    }

    entries.forEach(c => {
        let r = document.createElement('div');
        r.className = 'customer-row';
        
        r.onclick = () => {
            db.active = c.id;
            save();
            renderCard();
        };

        r.innerHTML = `
            <div class="customer-info">
                <strong>${safe(c.name)}</strong>
                <span>کد: ${safe(c.code)}</span>
            </div>
            <div style="font-size: 0.9rem; color: #2c7a7b; font-weight: bold;">
                ${fa(c.stamps)} از ${fa(c.limit)} مهر
            </div>
        `;
        root.appendChild(r);
    });
}

// ساخت کارت جدید
el('create').onclick = () => {
    let name = el('newName').value.trim();
    let code = el('newCode').value.trim();
    let limit = Number(el('newLimit').value);

    if (!name || !code) {
        alert('لطفاً نام مشتری و کد اختصاصی را وارد کنید.');
        return;
    }

    // بررسی تکراری نبودن کد
    let isDuplicate = Object.values(db.customers).some(c => c.code === code);
    if (isDuplicate) {
        alert('این کد اختصاصی قبلاً استفاده شده است. لطفاً کد دیگری وارد کنید.');
        return;
    }

    let id = 'cust_' + Date.now();
    db.customers[id] = {
        id: id,
        name: name,
        code: code,
        limit: limit,
        stamps: 0
    };

    db.active = id;
    el('newName').value = '';
    el('newCode').value = '';

    save();
    renderCustomers();
    renderCard();
};

// شروع برنامه
load();
renderCustomers();
renderCard();

</script>
</body>
</html>
