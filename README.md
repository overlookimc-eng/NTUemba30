
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>台大EMBA 30週年場佈｜專案進度儀表板</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700&family=DM+Mono:wght@400;500&display=swap');
:root{
  --cr:#8B1A2F; --cr-dk:#6B1217; --cr-lt:#F8ECEA; --cr-md:#C4637A;
  --go:#B5A130; --go-dk:#8C7A1A; --go-lt:#F6F1D6; --go-md:#D4C040;
  --or:#E05A1E; --or-lt:#FDF0E8;
  --ok:#2D5A1A; --ok-lt:#EBF4E3;
  --wt:#5A3A1A; --wt-lt:#FDF5E6;
  --iv:#FAF8F3; --iv-dk:#EDE8DF;
  --bd:#E0D5C5; --bd-s:#C4B49A;
  --tx:#241810; --mu:#7A6858; --hn:#B0A090;
  --r:6px;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Noto Sans TC',sans-serif;background:var(--iv);color:var(--tx);font-size:13.5px;line-height:1.55}

/* ─── BRAND TOP BAR ─── */
.topbar{height:4px;background:linear-gradient(90deg,var(--or) 0% 33%,var(--cr-dk) 33% 66%,var(--go) 66% 100%)}

/* ─── HEADER ─── */
header{background:var(--cr);color:#fff;padding:1.6rem 2.5rem 1.4rem;position:relative;overflow:hidden}
header::before{content:'30';position:absolute;right:1.75rem;top:50%;transform:translateY(-50%);font-size:7.5rem;font-weight:700;opacity:.09;color:var(--go);font-family:'DM Mono',monospace;line-height:1;pointer-events:none}
header h1{font-size:1.2rem;font-weight:500;letter-spacing:.04em;margin-bottom:.18rem}
header p{font-size:.74rem;opacity:.65;font-weight:300;letter-spacing:.02em}
.hm{display:flex;gap:2rem;margin-top:1rem;flex-wrap:wrap}
.hmi{display:flex;flex-direction:column;gap:2px}
.hmi .l{font-size:.6rem;opacity:.5;text-transform:uppercase;letter-spacing:.1em}
.hmi .v{font-size:.88rem;font-weight:500;font-family:'DM Mono',monospace;color:var(--go-md)}

/* ─── REFRESH BAR ─── */
.rbar{background:#fff;border-bottom:1px solid var(--bd);padding:.48rem 2.5rem;display:flex;align-items:center;justify-content:space-between;font-size:.7rem;color:var(--mu)}
.dot{width:6px;height:6px;border-radius:50%;background:#4caf50;display:inline-block;margin-right:5px;animation:pulse 2s infinite}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.3}}
.rbtn{background:none;border:1px solid var(--bd-s);border-radius:var(--r);padding:3px 10px;font-size:.68rem;cursor:pointer;color:var(--mu);font-family:inherit;transition:all .12s}
.rbtn:hover{background:var(--iv-dk);color:var(--tx)}

/* ─── MAIN ─── */
.main{padding:1.2rem 2.5rem 3rem;max-width:1500px}
.err{background:var(--or-lt);border:1px solid #e8a020;border-radius:var(--r);padding:.8rem 1rem;margin-bottom:1.1rem;font-size:.78rem;color:var(--or);display:none}

/* ─── STAT CARDS ─── */
.sg{display:grid;grid-template-columns:repeat(auto-fit,minmax(125px,1fr));gap:8px;margin-bottom:1.1rem}
.sc{background:#fff;border:1px solid var(--bd);border-top:3px solid var(--bd-s);border-radius:var(--r);padding:.8rem .95rem}
.sc .l{font-size:.6rem;color:var(--mu);text-transform:uppercase;letter-spacing:.07em;margin-bottom:4px}
.sc .n{font-size:1.6rem;font-weight:700;font-family:'DM Mono',monospace;line-height:1;color:var(--tx)}
.sc .s{font-size:.64rem;color:var(--hn);margin-top:3px}
.sc.hi{background:var(--cr-lt);border-top-color:var(--cr)}.sc.hi .n{color:var(--cr)}
.sc.go{background:var(--go-lt);border-top-color:var(--go)}.sc.go .n{color:var(--go-dk)}
.sc.ok{background:var(--ok-lt);border-top-color:var(--ok)}.sc.ok .n{color:var(--ok)}
.sc.or{background:var(--or-lt);border-top-color:var(--or)}.sc.or .n{color:var(--or)}

/* ─── SECTION HEADER ─── */
.sh{display:flex;align-items:center;gap:9px;margin:1.15rem 0 .55rem}
.sh-dot{width:7px;height:7px;border-radius:50%;background:var(--cr);flex-shrink:0}
.sh h2{font-size:.7rem;font-weight:500;text-transform:uppercase;letter-spacing:.12em;color:var(--mu);white-space:nowrap}
.sh .line{flex:1;height:1px;background:var(--bd)}

/* ─── MILESTONES ─── */
.mg{display:grid;grid-template-columns:repeat(auto-fill,minmax(205px,1fr));gap:8px;margin-bottom:1.1rem}
.mc{background:#fff;border:1px solid var(--bd);border-left:3px solid var(--bd-s);border-radius:var(--r);padding:.75rem .85rem}
.mc.urg{border-left-color:var(--or);background:var(--or-lt)}
.mc.pnd{border-left-color:var(--go)}
.mc.ok{border-left-color:var(--ok);background:var(--ok-lt)}
.mc.hot{border-left-color:var(--cr);background:var(--cr-lt)}
.me{font-weight:500;font-size:.76rem;margin-bottom:2px;color:var(--tx)}
.md{font-family:'DM Mono',monospace;font-size:.68rem;color:var(--cr);font-weight:500;margin-bottom:2px}
.md-c{font-size:.61rem;color:var(--mu);margin-bottom:4px}
.mn{font-size:.65rem;color:var(--mu);line-height:1.5}

/* ─── TABLE ─── */
.tw{overflow-x:auto;margin-bottom:1.1rem}
table{width:100%;border-collapse:collapse;font-size:.75rem;background:#fff;border:1px solid var(--bd);border-radius:var(--r);overflow:hidden;min-width:960px}
thead th{background:var(--cr);color:#fff;border-bottom:2px solid var(--cr-dk);padding:7px 9px;text-align:left;font-weight:500;font-size:.63rem;text-transform:uppercase;letter-spacing:.06em;white-space:nowrap}
thead th:first-child{width:34px;text-align:center}
tbody tr{border-bottom:1px solid var(--bd)}
tbody tr:last-child{border-bottom:none}

/* 群組標題 */
tbody tr.gr td{background:var(--go-lt);color:var(--go-dk);font-weight:600;font-size:.72rem;padding:5px 10px;letter-spacing:.03em;border-bottom:1px solid var(--bd-s)}

/* 主品項 */
tbody tr.mr{background:var(--cr-lt)}
tbody tr.mr:hover{background:#f0dada}
tbody tr.mr td.nm{color:var(--cr-dk);font-weight:500}

/* 子項目 */
tbody tr.sr:hover{background:var(--iv-dk)}
tbody tr.sr td.nm{color:var(--mu);font-size:.72rem}

/* 警示行 */
tbody tr.wr{background:var(--or-lt)}
tbody tr.wr:hover{background:#fce0ce}

tbody td{padding:5px 9px;vertical-align:middle}
td.nm{min-width:195px}
td.mo{font-family:'DM Mono',monospace;font-size:.68rem;text-align:center}
td.ct{text-align:center}

/* ─── BADGES ─── */
.badge{display:inline-block;padding:2px 7px;border-radius:100px;font-size:.61rem;font-weight:500;white-space:nowrap;line-height:1.4}
.b-ok{background:var(--ok-lt);color:var(--ok)}
.b-wip{background:var(--cr-lt);color:var(--cr)}
.b-td{background:var(--iv-dk);color:var(--mu)}
.b-wt{background:var(--go-lt);color:var(--go-dk)}
.b-wn{background:var(--or-lt);color:var(--or)}

/* ─── PROGRESS BAR ─── */
.pbw{display:flex;align-items:center;gap:5px;min-width:88px}
.pb{flex:1;height:5px;background:var(--iv-dk);border-radius:3px;overflow:hidden}
.pbf{height:100%;border-radius:3px;background:var(--cr);transition:width .45s}
.pbf.mid{background:var(--go)}
.pbf.done{background:var(--ok)}
.pp{font-family:'DM Mono',monospace;font-size:.64rem;color:var(--mu);min-width:26px;text-align:right}

/* ─── LOADING ─── */
.loading{text-align:center;padding:3rem 2rem;color:var(--mu);font-size:.8rem}
.spinner{width:24px;height:24px;border:2px solid var(--bd);border-top-color:var(--cr);border-radius:50%;animation:spin .8s linear infinite;margin:0 auto .85rem}
@keyframes spin{to{transform:rotate(360deg)}}

/* ─── FOOTER ─── */
footer{text-align:center;padding:1.2rem;font-size:.64rem;color:var(--hn);border-top:1px solid var(--bd);margin-top:1.5rem}
.ftl{font-size:.7rem;font-weight:500;color:var(--cr);letter-spacing:.04em;margin-bottom:3px}

@media(max-width:660px){
  header,.main,.rbar{padding-left:1rem;padding-right:1rem}
  .sg{grid-template-columns:repeat(2,1fr)}
  header::before{font-size:4.5rem}
}
</style>
</head>
<body>

<div class="topbar"></div>

<header>
  <h1>台大 EMBA 30 週年　場佈專案進度儀表板</h1>
  <p>活動日期：2026/10/17–18　｜　施工進場截止：2026/10/16　｜　EiMBA × GMBA × EMBA 三專班聯合週年慶</p>
  <div class="hm">
    <div class="hmi"><span class="l">專案期間</span><span class="v">5/5 – 10/18</span></div>
    <div class="hmi"><span class="l">主要廠商</span><span class="v">4 家</span></div>
    <div class="hmi"><span class="l">總金額（含稅）</span><span class="v" id="total-amt">讀取中…</span></div>
    <div class="hmi"><span class="l">最後更新</span><span class="v" id="lu">—</span></div>
  </div>
</header>

<div class="rbar">
  <span><span class="dot"></span>資料來源：Google Sheets（每次開啟即時讀取）</span>
  <button class="rbtn" onclick="init()">重新整理</button>
</div>

<div class="main">
  <div class="err" id="err"></div>
  <div id="loading" class="loading"><div class="spinner"></div>正在從 Google Sheets 載入資料⋯</div>
  <div id="dash" style="display:none">

    <!-- 統計卡 -->
    <div class="sg" id="sg"></div>

    <!-- 里程碑 -->
    <div class="sh"><div class="sh-dot"></div><h2>重要里程碑</h2><div class="line"></div></div>
    <div class="mg" id="mg"></div>

    <!-- 作品進度 -->
    <div class="sh"><div class="sh-dot"></div><h2>作品進度追蹤</h2><div class="line"></div></div>
    <div class="tw">
      <table>
        <thead><tr>
          <th>序</th>
          <th>品項名稱</th>
          <th>進場月份</th>
          <th>整體進度</th>
          <th>預計完成日</th>
          <th>企劃/初稿</th>
          <th>二修</th>
          <th>定稿</th>
          <th>施工進場</th>
          <th>費用到帳</th>
          <th>卡關點</th>
          <th>下一步行動</th>
        </tr></thead>
        <tbody id="tb"></tbody>
      </table>
    </div>

  </div>
</div>

<footer>
  <div class="ftl">台大 EiMBA ｜ GMBA ｜ EMBA　三專班聯合 30 週年慶</div>
  資料每次開啟自動從 Google Sheets 讀取最新狀態　｜　請款明細金額連動品項明細即時計算
</footer>

<script>
/* ─── 設定 ─── */
const SID = '1zuwiuVKlD1ZWzXUKhbCL68wuyNwHdVv5JOM8O5dlPTs';
const SHEETS = {
  dash:  '🏠 總覽儀表板',
  prog:  '📋 作品進度追蹤',
  pay:   '💰 請款明細',
};

/* ─── CSV 工具 ─── */
function csvUrl(sheet){
  return 'https://docs.google.com/spreadsheets/d/'+SID+'/gviz/tq?tqx=out:csv&sheet='+encodeURIComponent(sheet);
}
async function fetchCSV(sheet){
  const res = await fetch(csvUrl(sheet),{cache:'no-store'});
  if(!res.ok) throw new Error('無法讀取工作表「'+sheet+'」（HTTP '+res.status+'）');
  return parseCSV(await res.text());
}
function parseCSV(text){
  const rows=[];
  for(const line of text.split('\n')){
    if(!line.trim()) continue;
    const cols=[]; let cur='',inQ=false;
    for(const c of line){
      if(c==='"'){inQ=!inQ;}
      else if(c===','&&!inQ){cols.push(cur.trim());cur='';}
      else cur+=c;
    }
    cols.push(cur.trim()); rows.push(cols);
  }
  return rows;
}

/* ─── 日期工具 ─── */
function parseDate(s){
  if(!s) return null;
  const m=s.match(/(\d{4})[\/\-](\d{1,2})[\/\-](\d{1,2})/);
  return m ? new Date(+m[1],+m[2]-1,+m[3]) : null;
}
function daysLeft(s){
  const d=parseDate(s); if(!d) return null;
  return Math.ceil((d-new Date())/864e5);
}
function fmtDate(s){
  const d=parseDate(s); if(!d) return s||'—';
  return (d.getMonth()+1)+'/'+(d.getDate());
}
function daysTag(n){
  if(n===null) return '';
  if(n<0)  return '<span style="color:var(--ok);font-weight:500">已過期</span>';
  if(n===0) return '<span style="color:var(--or);font-weight:600">今天</span>';
  if(n<=7) return '<span style="color:var(--or);font-weight:500">還有 '+n+' 天</span>';
  if(n<=30) return '<span style="color:var(--go-dk);font-weight:500">還有 '+n+' 天</span>';
  return '<span style="color:var(--mu)">還有 '+n+' 天</span>';
}

/* ─── Badge ─── */
function badge(v){
  if(!v||v==='—'||v===' —') return '<span style="color:var(--hn)">—</span>';
  if(v.includes('✅')||v.includes('完成'))    return '<span class="badge b-ok">完成</span>';
  if(v.includes('🔵')||v.includes('🔄')||v.includes('進行中')) return '<span class="badge b-wip">進行中</span>';
  if(v.includes('⬜')||v.includes('待施工')||v.includes('未開始')) return '<span class="badge b-td">'+v.replace(/[⬜]/g,'').trim()+'</span>';
  if(v.includes('⏳')||v.includes('待請款')) return '<span class="badge b-wt">待請款</span>';
  return '<span class="badge b-td">'+v.replace(/[⬜⏳✅🔄🔵‼️]/g,'').trim()+'</span>';
}

/* ─── Progress bar ─── */
function pbar(pct){
  const n=Math.round(parseFloat(pct)*100)||0;
  const c=n>=100?'done':n>=50?'mid':'';
  return '<div class="pbw"><div class="pb"><div class="pbf '+c+'" style="width:'+n+'%"></div></div><span class="pp">'+n+'%</span></div>';
}

/* ─── 判斷列類型 ─── */
// 群組標題：B欄以 ── 開頭
function isGroupRow(r){ return (r[1]||'').trim().startsWith('──'); }
// 主品項：I欄（施工進場）有實際狀態值（非空、非 —）
function isMainRow(r){
  const i=(r[8]||'').trim();
  return i!==''&&i!=='—'&&i!==' —';
}
// 子項目：B欄含 └
function isSubRow(r){ return (r[1]||'').includes('└'); }

/* ─── 渲染統計卡 ─── */
function renderStats(rows, payRows){
  // 只統計主品項（非群組、非子項）
  const data = rows.slice(2).filter(r=>
    !isGroupRow(r) && isMainRow(r) && (r[1]||'').trim()
  );
  const total = data.length;
  const done  = data.filter(r=>parseFloat(r[3]||0)>=1).length;
  const wip   = data.filter(r=>{const p=parseFloat(r[3]||0);return p>0&&p<1;}).length;
  const avg   = total>0 ? Math.round(data.reduce((s,r)=>s+parseFloat(r[3]||0)*100,0)/total) : 0;
  const days  = Math.ceil((new Date('2026-10-17')-new Date())/864e5);

  // 總金額：從請款明細 G欄（含稅）加總
  let total_amt = 0;
  for(const r of payRows.slice(2)){
    if(!r[0]||r[0].trim()==='合計') continue;
    const g = parseFloat((r[6]||'').replace(/[^0-9.]/g,''));
    if(!isNaN(g)&&g>0) total_amt+=g;
  }
  const amtStr = total_amt>0 ? 'NT$'+Math.round(total_amt).toLocaleString('zh-TW') : '—';
  document.getElementById('total-amt').textContent = amtStr;

  document.getElementById('sg').innerHTML =
    '<div class="sc hi"><div class="l">整體進度</div><div class="n">'+avg+'<span style="font-size:.85rem;font-weight:400">%</span></div><div class="s">所有主品項平均</div></div>'+
    '<div class="sc go"><div class="l">主品項數</div><div class="n">'+total+'</div><div class="s">項</div></div>'+
    '<div class="sc or"><div class="l">進行中</div><div class="n">'+wip+'</div><div class="s">項</div></div>'+
    '<div class="sc ok"><div class="l">已完成</div><div class="n">'+done+'</div><div class="s">項</div></div>'+
    '<div class="sc '+(days<=30?'or':'hi')+'"><div class="l">活動倒數</div><div class="n">'+days+'</div><div class="s">天（10/17 活動）</div></div>';
}

/* ─── 渲染里程碑 ─── */
function renderMilestones(rows){
  const g=document.getElementById('mg'); g.innerHTML='';
  let on=false;
  for(const r of rows){
    const b=(r[1]||'').trim(), c=(r[2]||'').trim(), d=(r[3]||'').trim(), e=(r[4]||'').trim();
    if(b==='里程碑事項'){on=true;continue;}
    if(!on||!b) continue;
    if(b==='請款月份') break;
    const n  = daysLeft(c);
    const passed  = n!==null&&n<0;
    const urgent  = d.includes('緊急')||(n!==null&&n>=0&&n<=7);
    const hotzone = n!==null&&n>7&&n<=30;
    const cls = passed?'ok': urgent?'urg': hotzone?'hot': 'pnd';
    const bc  = passed?'b-ok': urgent?'b-wn': 'b-td';
    const el  = document.createElement('div');
    el.className='mc '+cls;
    el.innerHTML=
      '<div class="me">'+b+'</div>'+
      '<div class="md">'+c+'</div>'+
      '<div class="md-c">'+daysTag(n)+'</div>'+
      (d?'<div style="margin-bottom:4px"><span class="badge '+bc+'">'+d.replace(/[✅⏳‼️]/g,'').trim()+'</span></div>':'')+
      '<div class="mn">'+e+'</div>';
    g.appendChild(el);
  }
}

/* ─── 渲染作品進度表 ─── */
function renderItems(rows){
  const tb=document.getElementById('tb'); tb.innerHTML='';

  for(const r of rows.slice(2)){
    const name=(r[1]||'').trim();
    if(!name) continue;

    // ── 群組標題行 ──────────────────────────────
    if(isGroupRow(r)){
      const tr=document.createElement('tr'); tr.className='gr';
      tr.innerHTML='<td colspan="12" style="padding-left:12px">'+name+'</td>';
      tb.appendChild(tr); continue;
    }

    const main    = isMainRow(r);
    const sub     = isSubRow(r);
    const hasWarn = (r[10]||'').includes('⚠️');

    // 列的 class
    const rowCls = hasWarn?'wr': main?'mr': 'sr';

    // 序號：A欄可能是日期格式，過濾掉非整數
    const seqRaw = (r[0]||'').trim();
    const seq = /^\d+$/.test(seqRaw) ? seqRaw : '';

    // 進度條：主品項 & 子項目都顯示（公式欄位 D）
    const pctCell = (r[3]||'').trim();
    const pctDisplay = pbar(pctCell);

    // 日期格式化
    const dateStr = fmtDate(r[4]);

    // 卡關點：截短並加顏色
    const warn = (r[10]||'').replace('⚠️','').trim();
    const warnHtml = warn
      ? '<span style="color:var(--or);font-size:.65rem">⚠ '+warn+'</span>'
      : '';

    // 下一步行動
    const action = (r[11]||'').trim();

    const tr=document.createElement('tr'); tr.className=rowCls;
    tr.innerHTML=
      '<td class="mo ct" style="color:var(--hn)">'+seq+'</td>'+
      '<td class="nm">'+name+'</td>'+
      '<td class="mo ct">'+((r[2]||'')).replace('月','<span style="font-size:.6rem;color:var(--hn)">月</span>')+'</td>'+
      '<td>'+pctDisplay+'</td>'+
      '<td class="mo ct" style="font-size:.66rem;color:var(--mu)">'+dateStr+'</td>'+
      '<td class="ct">'+badge(r[5])+'</td>'+
      '<td class="ct">'+badge(r[6])+'</td>'+
      '<td class="ct">'+badge(r[7])+'</td>'+
      '<td class="ct">'+(main?badge(r[8]):'<span style="color:var(--hn)">—</span>')+'</td>'+
      '<td class="ct">'+(main?badge(r[9]):'<span style="color:var(--hn)">—</span>')+'</td>'+
      '<td style="max-width:150px">'+warnHtml+'</td>'+
      '<td style="font-size:.65rem;color:var(--mu);max-width:220px;line-height:1.4">'+action+'</td>';
    tb.appendChild(tr);
  }
}

/* ─── 主程式 ─── */
async function init(){
  document.getElementById('loading').style.display='block';
  document.getElementById('dash').style.display='none';
  document.getElementById('err').style.display='none';

  try{
    const [dashRows, progRows, payRows] = await Promise.all([
      fetchCSV(SHEETS.dash),
      fetchCSV(SHEETS.prog),
      fetchCSV(SHEETS.pay),
    ]);

    document.getElementById('lu').textContent =
      new Date().toLocaleString('zh-TW',{month:'2-digit',day:'2-digit',hour:'2-digit',minute:'2-digit'});

    document.getElementById('loading').style.display='none';
    document.getElementById('dash').style.display='block';

    renderStats(progRows, payRows);
    renderMilestones(dashRows);
    renderItems(progRows);

  }catch(e){
    document.getElementById('loading').style.display='none';
    document.getElementById('dash').style.display='block';
    const eb=document.getElementById('err');
    eb.style.display='block';
    eb.textContent='讀取失敗：'+e.message+'。請確認試算表已設為「知道連結的人可以檢視」。';
    console.error(e);
  }
}

init();
</script>
</body>
</html>
