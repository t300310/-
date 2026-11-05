[生命保険料控除　計算ツール.html](https://github.com/user-attachments/files/34402748/default.html)
<!doctype html>
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>令和8年分 生命保険料控除 計算ツール</title>
<style>
:root{font-family:"Yu Gothic UI",Meiryo,sans-serif;color:#243044;background:#f4f6f9}
*{box-sizing:border-box}body{margin:0;padding:22px}.wrap{max-width:1100px;margin:auto}
h1{font-size:1.55rem;margin:0 0 8px}.lead,.hint{color:#64748b;font-size:.88rem}
.card{background:#fff;border:1px solid #dce2ea;border-radius:12px;padding:18px;margin:14px 0}
h2{font-size:1.12rem;margin:0 0 12px}.group{border:1px solid #e0e6ee;border-radius:9px;padding:13px;margin:12px 0}
.group-head{display:flex;justify-content:space-between;align-items:center;gap:10px;flex-wrap:wrap}
.group h3{font-size:1rem;margin:0}.entry{display:grid;grid-template-columns:minmax(160px,1fr) minmax(150px,220px) auto;gap:9px;align-items:center;margin-top:10px}
input[type=text],input[type=number]{width:100%;padding:9px;border:1px solid #c8d1dc;border-radius:7px;font:inherit}
button{border:0;border-radius:7px;padding:9px 13px;font:inherit;cursor:pointer;background:#2459a6;color:white}
button.secondary{background:#e8edf4;color:#243044}button.remove{background:#fbeaea;color:#9d2929;padding:8px 11px}
.add{font-size:.88rem;padding:8px 12px}.row{display:flex;align-items:center;gap:10px;flex-wrap:wrap}
table{width:100%;border-collapse:collapse;margin-top:8px}th,td{padding:9px;border-bottom:1px solid #e5eaf0;text-align:right}th:first-child,td:first-child{text-align:left}
.total{background:#eef4ff;font-weight:700}.result{font-size:1.2rem}.amount{font-variant-numeric:tabular-nums}
.warning{background:#fff8e8;border-left:4px solid #d69b22;padding:12px;border-radius:6px;font-size:.88rem}

/* 申告書転記案内のスタイル */
.transcribe-table th,.transcribe-table td{text-align:left;vertical-align:middle}
.transcribe-table td.val-col{text-align:right;font-weight:700;font-variant-numeric:tabular-nums}
.transcribe-table td.chk-col{text-align:center;width:90px}
.badge-code{display:inline-block;background:#2459a6;color:#fff;border-radius:4px;padding:2px 6px;font-size:.82rem;font-weight:700;margin-right:6px}
.notice-box{background:#eef6ff;border:1px solid #bce0fd;border-radius:8px;padding:12px;margin-bottom:14px;font-size:.9rem}
.checked-row{background-color:#f8fafc;color:#94a3b8}
.sub-desc{font-size:.8rem;color:#64748b;font-weight:normal;display:block;margin-top:2px}
</style></head>
<body><div class="wrap">
<h1>令和8年分 生命保険料控除 計算ツール</h1>
<p class="lead">保険の名称と年間払込保険料を契約ごとに入力できます。同じ区分の保険は「保険を追加」から行を増やしてください。</p>

<div class="card">
<h2>1．保険契約の入力</h2>
<p class="hint">年間払込保険料は、令和8年中に支払った（または支払う予定の）保険料から配当金等を差し引いた金額を入力してください。複数契約がある場合は、契約ごとに入力してください。</p>
<div class="row" style="margin:10px 0 14px"><label style="display:flex;align-items:center;gap:8px;margin:0"><input id="under23" type="checkbox"> 23歳未満の扶養親族がいる（一般生命保険料の令和8年特例を適用）</label></div>
<div class="group" data-kind="lifeNew"><div class="group-head"><h3>一般生命保険料（新制度）</h3><button class="add" type="button">＋ 保険を追加</button></div><div class="entries"></div></div>
<div class="group" data-kind="lifeOld"><div class="group-head"><h3>一般生命保険料（旧制度）</h3><button class="add" type="button">＋ 保険を追加</button></div><div class="entries"></div></div>
<div class="group" data-kind="careNew"><div class="group-head"><h3>介護医療保険料</h3><button class="add" type="button">＋ 保険を追加</button></div><div class="entries"></div></div>
<div class="group" data-kind="pensionNew"><div class="group-head"><h3>個人年金保険料（新制度）</h3><button class="add" type="button">＋ 保険を追加</button></div><div class="entries"></div></div>
<div class="group" data-kind="pensionOld"><div class="group-head"><h3>個人年金保険料（旧制度）</h3><button class="add" type="button">＋ 保険を追加</button></div><div class="entries"></div></div>
<div class="row" style="margin-top:14px"><button id="reset" class="secondary" type="button">すべてリセット</button></div>
</div>

<div class="card"><h2>2．控除額の計算結果</h2>
<table><thead><tr><th>区分</th><th>年間払込保険料の合計</th><th>控除額</th></tr></thead><tbody>
<tr><td>一般生命保険料（新制度）</td><td id="vLifeNew">0円</td><td id="dLifeNew">0円</td></tr>
<tr><td>一般生命保険料（旧制度）</td><td id="vLifeOld">0円</td><td id="dLifeOld">0円</td></tr>
<tr><td>介護医療保険料</td><td id="vCareNew">0円</td><td id="dCareNew">0円</td></tr>
<tr><td>個人年金保険料（新制度）</td><td id="vPensionNew">0円</td><td id="dPensionNew">0円</td></tr>
<tr><td>個人年金保険料（旧制度）</td><td id="vPensionOld">0円</td><td id="dPensionOld">0円</td></tr>
<tr class="total"><td>一般生命保険料控除（合算後）</td><td>—</td><td id="dLifeTotal">0円</td></tr>
<tr class="total"><td>介護医療保険料控除</td><td>—</td><td id="dCareTotal">0円</td></tr>
<tr class="total"><td>個人年金保険料控除（合算後）</td><td>—</td><td id="dPensionTotal">0円</td></tr>
<tr class="total"><td>生命保険料控除額 合計</td><td>—</td><td class="result" id="grandTotal">0円</td></tr>
</tbody></table><p class="hint" id="detail"></p></div>

<!-- 申告書への転記案内 -->
<div class="card">
<h2>3．給与所得者の保険料控除申告書への転記案内</h2>
<p class="hint">年末調整の申告書（保険料控除申告書）の各記入欄へ、以下の通り転記してください。</p>

<div class="notice-box" id="transcribeNotice">
  <!-- JavaScriptで案内メッセージを切り替え -->
</div>

<table class="transcribe-table">
  <thead>
    <tr>
      <th>申告書の記入欄</th>
      <th style="text-align:right">転記する金額</th>
      <th style="text-align:center">転記済み</th>
    </tr>
  </thead>
  <tbody>
    <!-- 一般生命保険料 合計額 -->
    <tr>
      <td>
        <span class="badge-code">A</span>一般生命保険料（新制度）の合計額
      </td>
      <td class="val-col" id="tr_A">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <tr>
      <td>
        <span class="badge-code">B</span>一般生命保険料（旧制度）の合計額
      </td>
      <td class="val-col" id="tr_B">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <!-- 一般生命保険料 計算欄 -->
    <tr id="row_calc_12">
      <td>
        <span class="badge-code" id="code_12">①</span>Aの金額を計算式Ⅰ（新保険料等用）に当てはめて計算した金額
      </td>
      <td class="val-col" id="tr_calc_12">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <tr>
      <td>
        <span class="badge-code">③</span>Bの金額を計算式Ⅲ（旧保険料等用）に当てはめて計算した金額
      </td>
      <td class="val-col" id="tr_calc_3">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <tr id="row_calc_45">
      <td>
        <span class="badge-code" id="code_45">④</span><span id="label_45">① ＋ ③（最高40,000円）</span>
      </td>
      <td class="val-col" id="tr_calc_45">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <!-- 一般生命保険料 控除額 イ -->
    <tr style="background:#f0f7ff">
      <td>
        <span class="badge-code">イ</span>一般生命保険料 控除額
        <span class="sub-desc" id="desc_I">③と④のいずれか大きい金額（最高5万円）</span>
      </td>
      <td class="val-col" id="tr_I">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>

    <!-- 介護医療保険料 -->
    <tr>
      <td>
        <span class="badge-code">C</span>介護医療保険料の合計額
      </td>
      <td class="val-col" id="tr_C">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <tr style="background:#f0f7ff">
      <td>
        <span class="badge-code">ロ</span>介護医療保険料 控除額
        <span class="sub-desc">Cの金額を計算式Ⅰ（新保険料等用）に当てはめて計算した金額（最高4万円）</span>
      </td>
      <td class="val-col" id="tr_RO">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>

    <!-- 個人年金保険料 合計額 -->
    <tr>
      <td>
        <span class="badge-code">D</span>個人年金保険料（新制度）の合計額
      </td>
      <td class="val-col" id="tr_D">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <tr>
      <td>
        <span class="badge-code">E</span>個人年金保険料（旧制度）の合計額
      </td>
      <td class="val-col" id="tr_E">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <!-- 個人年金保険料 計算欄 -->
    <tr>
      <td>
        <span class="badge-code">⑥</span>Dの金額を計算式Ⅰ（新保険料等用）に当てはめて計算した金額
      </td>
      <td class="val-col" id="tr_calc_6">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <tr>
      <td>
        <span class="badge-code">⑦</span>Eの金額を計算式Ⅲ（旧保険料等用）に当てはめて計算した金額
      </td>
      <td class="val-col" id="tr_calc_7">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <tr>
      <td>
        <span class="badge-code">⑧</span>⑥ ＋ ⑦（最高40,000円）
      </td>
      <td class="val-col" id="tr_calc_8">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
    <!-- 個人年金保険料 控除額 ハ -->
    <tr style="background:#f0f7ff">
      <td>
        <span class="badge-code">ハ</span>個人年金保険料 控除額
        <span class="sub-desc">⑦と⑧のいずれか大きい金額（最高5万円）</span>
      </td>
      <td class="val-col" id="tr_HA">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>

    <!-- 合計 -->
    <tr class="total">
      <td>
        <span class="badge-code" style="background:#1e40af">合計</span>生命保険料控除額（イ ＋ ロ ＋ ハ、最高12万円）
      </td>
      <td class="val-col result" id="tr_TOTAL">0円</td>
      <td class="chk-col"><input type="checkbox" class="tr-chk"></td>
    </tr>
  </tbody>
</table>
</div>

<div class="card"><h2>計算方法（所得税）</h2>
<ul>
<li>計算式Ⅰ（新保険料等用）：20,000円以下は全額、20,000円超40,000円以下は「保険料×1/2＋10,000円」、40,000円超80,000円以下は「保険料×1/4＋20,000円」、80,000円超は一律40,000円。</li>
<li>計算式Ⅲ（旧保険料等用）：25,000円以下は全額、25,000円超50,000円以下は「保険料×1/2＋12,500円」、50,000円超100,000円以下は「保険料×1/4＋25,000円」、100,000円超は一律50,000円。</li>
<li>計算式Ⅱ（年齢23歳未満の扶養親族を有する場合の新保険料等用・令和8年特例）：30,000円以下は全額、30,000円超60,000円以下は「保険料×1/2＋15,000円」、60,000円超120,000円以下は「保険料×1/4＋30,000円」、120,000円超は一律60,000円。</li>
<li>一般生命保険料・個人年金保険料で新旧両方がある場合、旧契約の年間保険料が60,000円を超えると旧制度のみで計算し、60,000円以下なら新旧の計算額を合算します（上限は通常40,000円）。一般生命保険料は上記特例の対象となる場合、上限60,000円です。</li>
<li>一般・介護医療・個人年金の各控除の合計上限は120,000円です。</li>
</ul><div class="warning">このツールは所得税の控除額を試算するものです。実際の申告では保険会社から届く控除証明書および国税庁の記載要領を優先してください。契約ごとの適用区分・新旧判定も控除証明書で確認してください。</div></div>
</div>

<script>
const kinds=['lifeNew','lifeOld','careNew','pensionNew','pensionOld'];
const labels={lifeNew:'一般生命保険料（新制度）',lifeOld:'一般生命保険料（旧制度）',careNew:'介護医療保険料',pensionNew:'個人年金保険料（新制度）',pensionOld:'個人年金保険料（旧制度）'};
const yen=n=>Math.floor(n).toLocaleString('ja-JP')+'円';

function addEntry(kind,name='',amount=''){
 const group=document.querySelector('[data-kind="'+kind+'"] .entries');
 const row=document.createElement('div');row.className='entry';
 const nm=document.createElement('input');nm.type='text';nm.className='name';nm.placeholder='保険の名称（任意）';nm.value=name;nm.setAttribute('aria-label',labels[kind]+'の保険名称');
 const val=document.createElement('input');val.type='number';val.min='0';val.step='1';val.placeholder='年間払込保険料（円）';val.value=amount;val.setAttribute('aria-label',labels[kind]+'の年間払込保険料');
 const del=document.createElement('button');del.type='button';del.className='remove';del.textContent='削除';del.addEventListener('click',()=>{row.remove();calculate()});
 nm.addEventListener('input',calculate);val.addEventListener('input',calculate);
 row.append(nm,val,del);group.append(row);calculate();
}

function sumKind(kind){return [...document.querySelectorAll('[data-kind="'+kind+'"] input[type=number]')].reduce((s,e)=>s+Math.max(0,Number(e.value)||0),0)}

// 計算式Ⅰ（新保険料等用）
function calcFormula1(p){if(p<=20000)return p;if(p<=40000)return p/2+10000;if(p<=80000)return p/4+20000;return 40000}
// 計算式Ⅱ（年齢23歳未満の扶養親族を有する場合の新保険料等用）
function calcFormula2(p){if(p<=30000)return p;if(p<=60000)return p/2+15000;if(p<=120000)return p/4+30000;return 60000}
// 計算式Ⅲ（旧保険料等用）
function calcFormula3(p){if(p<=25000)return p;if(p<=50000)return p/2+12500;if(p<=100000)return p/4+25000;return 50000}

function calcPair(n,o,special=false){
 if(!n&&!o)return {value:0,detail:'入力なし'};
 if(!n)return {value:Math.min(calcFormula3(o),50000),detail:'旧制度のみ'};
 const nd=special?calcFormula2(n):calcFormula1(n);
 if(!o)return {value:Math.min(nd,special?60000:40000),detail:special?'新制度・特例':'新制度のみ'};
 if(o>60000)return {value:Math.min(calcFormula3(o),special?60000:50000),detail:'旧契約が6万円超のため旧制度で計算'};
 const cap=special?60000:40000;
 return {value:Math.min(nd+calcFormula3(o),cap),detail:'新旧合算'};
}

function calculate(){
 const v=Object.fromEntries(kinds.map(k=>[k,sumKind(k)]));
 const special=document.getElementById('under23').checked;
 
 const life=calcPair(v.lifeNew,v.lifeOld,special);
 const pension=calcPair(v.pensionNew,v.pensionOld,false);
 const careTotal=Math.min(calcFormula1(v.careNew),40000);

 // 個別計算欄（①〜⑧）の計算（④・⑧は最高40,000円、⑤は最高60,000円の上限を適用）
 const c1 = calcFormula1(v.lifeNew);             // ① Aを計算式Ⅰへ
 const c2 = calcFormula2(v.lifeNew);             // ② Aを計算式Ⅱへ
 const c3 = calcFormula3(v.lifeOld);             // ③ Bを計算式Ⅲへ
 const c4 = Math.min(c1 + c3, 40000);            // ④ ①+③（最高40,000円）
 const c5 = Math.min(c2 + c3, 60000);            // ⑤ ②+③（最高60,000円）
 
 const c6 = calcFormula1(v.pensionNew);          // ⑥ Dを計算式Ⅰへ
 const c7 = calcFormula3(v.pensionOld);          // ⑦ Eを計算式Ⅲへ
 const c8 = Math.min(c6 + c7, 40000);            // ⑧ ⑥+⑦（最高40,000円）

 // 表（2．控除額の計算結果）の更新
 const rows=[
  ['LifeNew',v.lifeNew,special?c2:c1],
  ['LifeOld',v.lifeOld,c3],
  ['CareNew',v.careNew,calcFormula1(v.careNew)],
  ['PensionNew',v.pensionNew,c6],
  ['PensionOld',v.pensionOld,c7]
 ];
 rows.forEach(([id,a,d])=>{document.getElementById('v'+id).textContent=yen(a);document.getElementById('d'+id).textContent=yen(d)});
 document.getElementById('dLifeTotal').textContent=yen(life.value);
 document.getElementById('dCareTotal').textContent=yen(careTotal);
 document.getElementById('dPensionTotal').textContent=yen(pension.value);
 const grandTotalVal=Math.min(life.value+careTotal+pension.value,120000);
 document.getElementById('grandTotal').textContent=yen(grandTotalVal);
 document.getElementById('detail').textContent='一般生命保険料：'+life.detail+' ／ 個人年金保険料：'+pension.detail+'。名称欄は管理用で、控除額には影響しません。';

 // --- 3. 申告書への転記案内の更新処理 ---
 document.getElementById('tr_A').textContent = yen(v.lifeNew);
 document.getElementById('tr_B').textContent = yen(v.lifeOld);
 document.getElementById('tr_C').textContent = yen(v.careNew);
 document.getElementById('tr_D').textContent = yen(v.pensionNew);
 document.getElementById('tr_E').textContent = yen(v.pensionOld);

 const notice = document.getElementById('transcribeNotice');
 const code12 = document.getElementById('code_12');
 const trCalc12 = document.getElementById('tr_calc_12');
 const code45 = document.getElementById('code_45');
 const label45 = document.getElementById('label_45');
 const trCalc45 = document.getElementById('tr_calc_45');
 const descI = document.getElementById('desc_I');

 if (special) {
  notice.innerHTML = '💡 <strong>23歳未満の扶養親族がいる（特例適用）場合：</strong><br>一般生命保険料の計算欄は <strong>①・④ ではなく ②・⑤</strong> を使用します。';
  code12.textContent = '②';
  trCalc12.textContent = yen(c2);
  code45.textContent = '⑤';
  label45.textContent = '② ＋ ③（最高60,000円）';
  trCalc45.textContent = yen(c5);
  descI.textContent = '⑤の金額（最高6万円）';
 } else {
  notice.innerHTML = '💡 申告書の記号欄（A〜E、①〜⑧、イ・ロ・ハ）にそのまま対応しています。';
  code12.textContent = '①';
  trCalc12.textContent = yen(c1);
  code45.textContent = '④';
  label45.textContent = '① ＋ ③（最高40,000円）';
  trCalc45.textContent = yen(c4);
  descI.textContent = '③と④のいずれか大きい金額（最高5万円 / 新旧合算は最高4万円）';
 }

 document.getElementById('tr_calc_3').textContent = yen(c3);
 document.getElementById('tr_I').textContent = yen(life.value);

 document.getElementById('tr_RO').textContent = yen(careTotal);

 document.getElementById('tr_calc_6').textContent = yen(c6);
 document.getElementById('tr_calc_7').textContent = yen(c7);
 document.getElementById('tr_calc_8').textContent = yen(c8);
 document.getElementById('tr_HA').textContent = yen(pension.value);

 document.getElementById('tr_TOTAL').textContent = yen(grandTotalVal);
}

// チェックボックス選択時のスタイル変化
document.querySelectorAll('.tr-chk').forEach(chk => {
 chk.addEventListener('change', (e) => {
  const tr = e.target.closest('tr');
  if (e.target.checked) {
   tr.classList.add('checked-row');
  } else {
   tr.classList.remove('checked-row');
  }
 });
});

document.querySelectorAll('.group').forEach(g=>{const kind=g.dataset.kind;g.querySelector('.add').addEventListener('click',()=>addEntry(kind))});
document.getElementById('under23').addEventListener('change',calculate);
document.getElementById('reset').addEventListener('click',()=>{
 document.querySelectorAll('.entries').forEach(e=>e.innerHTML='');
 kinds.forEach(k=>addEntry(k));
 document.getElementById('under23').checked=false;
 document.querySelectorAll('.tr-chk').forEach(chk => { chk.checked = false; chk.closest('tr').classList.remove('checked-row'); });
 calculate();
});

kinds.forEach(k=>addEntry(k));
</script></body></html>
