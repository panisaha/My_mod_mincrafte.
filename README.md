<div class="panel hidden" id="adminTools">

   <h2>ساخت کارت مشتری جدید</h2>

   <label class="field">
    <span>نام مشتری</span>
    <input id="newName" placeholder="نام مشتری">
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

   <button class="btn primary wide" id="create">
    ساخت کارت
   </button>

   <div class="divider"></div>

   <h2>کارت‌های مشتریان</h2>

   <p class="muted">
    مشتری فقط تا تعداد مهرهای مجاز می‌تواند روی جای مهر بزند.
   </p>

   <div id="customers"></div>

  </div>
 </section>

 <div class="footer">
  Mahshid Ceram · Handmade Pottery
 </div>

</main>
</div>

<script>
const STORAGE='mahshidCeramDemo_v2';

let db={
 customers:{},
 active:null
};

const fa=n=>
 String(n).replace(/\d/g,d=>'۰۱۲۳۴۵۶۷۸۹'[d]);

const el=id=>document.getElementById(id);

function safe(s){
 return String(s).replace(/[&<>"']/g,c=>({
  '&':'&amp;',
  '<':'&lt;',
  '>':'&gt;',
  '"':'&quot;',
  "'":'&#39;'
 }[c]));
}

function save(){
 try{
  localStorage.setItem(STORAGE,JSON.stringify(db));
 }catch(e){
  alert('ذخیره اطلاعات انجام نشد.');
 }
}

function load(){
 try{
  let x=JSON.parse(localStorage.getItem(STORAGE));
  if(x&&x.customers)db=x;
 }catch(e){}
}

function renderCard(){

 let c=db.active&&db.customers[db.active];

 let limit=c?
 Math.max(1,Math.min(5,Number(c.limit)||5)):5;

 el('stamps').innerHTML='';

 for(let i=0;i<5;i++){

  let d=document.createElement('button');

  d.type='button';

  d.className='stamp'+
  (c&&i<c.stamps?' full':'');

  d.textContent=c&&i<c.stamps?'❀':'○';

  d.setAttribute('aria-label','جای مهر '+(i+1));

  d.style.cursor=
  c&&i<limit&&i>=c.stamps?'pointer':'default';

  d.style.opacity=
  c&&i>=limit?'.35':'1';

  d.title=
  i>=limit?'این جای مهر مجاز نیست':
  (c&&i<c.stamps?'این مهر قبلاً ثبت شده':'ثبت مهر');

  d.onclick=()=>{

   if(!c)return;

   if(i>=limit){
    alert('تعداد مهرهای مجاز این کارت '+fa(limit)+' تاست.');
    return;
   }

   if(i<c.stamps){
    alert('این مهر قبلاً ثبت شده است.');
    return;
   }

   if(c.stamps>=limit){
    alert('تعداد مهرهای مجاز این کارت تکمیل شده است.');
    return;
   }

   c.stamps++;

   save();
   renderCard();
   renderCustomers();
  };

  el('stamps').appendChild(d);
 }

 el('customerName').textContent=
 c?'سلام، '+c.name+'!':'کارت مشتری';

 el('cardCode').textContent=
 c?c.code:'کارت وفاداری';

 el('count').textContent=
 fa(c?c.stamps:0)+' از '+fa(limit)+' مهر مجاز';

 el('limitLabel').textContent=
 fa(limit)+' مهر مجاز 🎁';

 el('progress').style.width=
 ((c?c.stamps:0)/limit*100)+'%';

 el('reward').innerHTML=
 c&&c.stamps>=limit
 ?
 '<strong>تعداد مهرهای مجاز تکمیل شد 🎁</strong><br>'+
 'برای جایزه با مهشید سرام هماهنگ کن. '+
 'تکمیل کارت به‌تنهایی به معنی ارسال خودکار جایزه نیست.'
 :
 '<strong>جایزه‌ات نزدیکه!</strong><br>'+
 'روی جای مهر بزن؛ بعد از ثبت '+
 fa(limit)+' مهر، مهرهای بیشتر ثبت نمی‌شوند.';

 el('shareInfo').textContent=
 c?'کد کارت تو: '+c.code+
 ' · نسخهٔ آزمایشی؛ مهرها فقط در همین مرورگر ذخیره می‌شوند.'
 :
 'برای دیدن کارتت، کد مشتری را از پنل بگیر.';

 el('copyLink').disabled=!c;

 el('copyNote').textContent=
 c?'لینک نمایشی کارت را می‌توانی کپی کنی؛ برای دسترسی از گوشی‌های دیگر باید سایت آنلاین شود.'
 :'برای ساخت لینک، اول کارت مشتری را انتخاب کن.';
}

function renderCustomers(){

 let root=el('customers');

 root.innerHTML='';

 let entries=Object.values(db.customers);

 if(!entries.length){
  root.innerHTML='<p class="muted">هنوز مشتری‌ای ساخته نشده.</p>';
  return;
 }

 entries.forEach(c=>{

  let r=document.createElement('div');

  r.className='customer-row';

  let info=document.createElement('div');

