<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>台大EMBA 30週年場佈｜專案進度儀表板</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700&family=DM+Mono:wght@400;500&display=swap');
  :root {
    --bg:#f7f6f2; --surface:#fff; --border:#e8e5de; --border-strong:#d0ccc2;
    --text:#1a1916; --text-muted:#7a766e; --accent:#1a4a3a; --accent-light:#e6f0ec;
    --amber:#b8680a; --amber-light:#fef3e2; --red:#8b2020; --red-light:#fdeaea;
    --green:#1a5c3a; --green-light:#e6f4ec; --blue:#1a3a6a; --blue-light:#e6eef8;
    --gray:#5a5650; --gray-light:#f0ede8; --r:6px;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  body{font-family:'Noto Sans TC',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;font-size:14px;line-height:1.6}
  header{background:var(--accent);color:white;padding:2rem 2.5rem 1.5rem;position:relative;overflow:hidden}
  header::before{content:'30';position:absolute;right:2rem;top:50%;transform:translateY(-50%);font-size:9rem;font-weight:700;opacity:.08;font-family:'DM Mono',monospace;line-height:1}
  header h1{font-size:1.35rem;font-weight:500;letter-spacing:.02em;margin-bottom:.25rem}
  header p{font-size:.8rem;opacity:.65;font-weight:300}
  .header-meta{display:flex;gap:2rem;margin-top:1.25rem;flex-wrap:wrap}
  .hm{display:flex;flex-direction:column;gap:2px}
  .hm .lbl{font-size:.68rem;opacity:.5;text-transform:uppercase;letter-spacing:.08em}
  .hm .val{font-size:1rem;font-weight:500;font-family:'DM Mono',monospace}
  .refresh-bar{background:var(--surface);border-bottom:1px solid var(--border);padding:.6rem 2.5rem;display:flex;align-items:center;justify-content:space-between;font-size:.75rem;color:var(--text-muted)}
  .dot{width:7px;height:7px;border-radius:50%;background:#4caf50;display:inline-block;margin-right:6px;animation:pulse 2s infinite}
  @keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}
  .rbtn{background:none;border:1px solid var(--border-strong);border-radius:var(--r);padding:4px 12px;font-size:.72rem;cursor:pointer;color:var(--text-muted);font-family:inherit;transition:all .15s}
  .rbtn:hover{background:var(--gray-light);color:var(--text)}
  .main{padding:1.5rem 2.5rem 3rem;max-width:1400px}
  .err{background:var(--amber-light);border:1px solid #e6a020;border-radius:var(--r);padding:1rem 1.25rem;margin-bottom:1.5rem;font-size:.82rem;color:var(--amber);display:none}
  .stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:10px;margin-bottom:1.5rem}
  .sc{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:1rem 1.1rem}
  .sc .lbl{font-size:.68rem;color:var(--text-muted);text-transform:uppercase;letter-spacing:.06em;margin-bottom:6px}
  .sc .num{font-size:1.8rem;font-weight:700;font-family:'DM Mono',monospace;line-height:1}
  .sc .sub{font-size:.7rem;color:var(--text-muted);margin-top:4px}
  .sc.hi{background:var(--accent-light);border-color:#9fc8b4}
  .sc.hi .num{color:var(--accent)}
  .sh{display:flex;align-items:center;gap:10px;margin-bottom:.75rem;margin-top:1.5rem}
  .sh h2{font-size:.82rem;font-weight:500;text-transform:uppercase;letter-spacing:.1em;color:var(--text-muted);white-space:nowrap}
  .sh .line{flex:1;height:1px;background:var(--border)}
  .tw{overflow-x:auto;margin-bottom:1.5rem}
  table{width:100%;border-collapse:collapse;font-size:.8rem;background:var(--surface);border:1px solid var(--border);border-radius:var(--r);overflow:hidden}
  thead th{background:var(--gray-light);border-bottom:1px solid var(--border-strong);padding:8px 12px;text-align:left;font-weight:500;font-size:.72rem;text-transform:uppercase;letter-spacing:.06em;color:var(--text-muted);white-space:nowrap}
  tbody tr{border-bottom:1px solid var(--border);transition:background .1s}
  tbody tr:last-child{border-bottom:none}
  tbody tr:hover{background:var(--bg)}
  tbody td{padding:8px 12px;vertical-align:middle}
  td.nm{font-weight:500;min-width:200px}
  td.mo{font-family:'DM Mono',monospace;font-size:.75rem}
  .badge{display:inline-block;padding:2px 8px;border-radius:100px;font-size:.68rem;font-weight:500;white-space:nowrap}
  .b-ok{background:var(--green-light);color:var(--green)}
  .b-wip{background:var(--amber-light);color:var(--amber)}
  .b-td{background:var(--gray-light);color:var(--gray)}
  .b-wt{background:var(--blue-light);color:var(--blue)}
  .b-wn{background:var(--red-light);color:var(--red)}
  .pbw{display:flex;align-items:center;gap:8px;min-width:120px}
  .pb{flex:1;height:6px;background:var(--gray-light);border-radius:3px;overflow:hidden}
  .pbf{height:100%;border-radius:3px;background:var(--accent);transition:width .6s ease}
  .pbf.mid{background:var(--amber)}
  .pbf.done{background:var(--green)}
  .pp{font-family:'DM Mono',monospace;font-size:.72rem;color:var(--text-muted);min-width:32px;text-align:right}
  .mg{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:10px;margin-bottom:1.5rem}
  .mc{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:.9rem 1rem;border-left:3px solid var(--border-strong)}
  .mc.urg{border-left-color:#c0392b}
  .mc.pnd{border-left-color:var(--amber)}
  .mc.ok{border-left-color:var(--green)}
  .mc .me{font-weight:500;font-size:.82rem;margin-bottom:4px}
  .mc .md{font-family:'DM Mono',monospace;font-size:.72rem;color:var(--text-muted);margin-bottom:4px}
  .mc .mn{font-size:.72rem;color:var(--text-muted)}
  .loading{text-align:center;padding:3rem 2rem;color:var(--text-muted);font-size:.85rem}
  .spinner{width:28px;height:28px;border:2px solid var(--border);border-top-color:var(--accent);border-radius:50%;animation:spin .8s linear infinite;margin:0 auto 1rem}
  @keyframes spin{to{transform:rotate(360deg)}}
  footer{text-align:center;padding:1.5rem;font-size:.7rem;color:var(--text-muted);border-top:1px solid var(--border);margin-top:2rem}
  @media(max-width:640px){header,.main,.refresh-bar{padding-left:1rem;padding-right:1rem}.stats{grid-template-columns:repeat(2,1fr)}}
</style>
</head>
<body>
<header>
  <h1>台大 EMBA 30週年｜場佈專案進度儀表板</h1>
  <p>活動日期：2026/10/17–18　｜　施工進場截止：2026/10/16</p>
  <div class="header-meta">
    <div class="hm"><span class="lbl">專案期間</span><span class="val">5/5 – 10/18</span></div>
    <div class="hm"><span class="lbl">主要廠商</span><span class="val">4 家</span></div>
    <div class="hm"><span class="lbl">總金額（含稅）</span><span class="val">NT$1,095,171</span></div>
    <div class="hm"><span class="lbl">最後更新</span><span class="val" id="lu">—</span></div>
  </div>
</header>
<div class="refresh-bar">
  <span><span class="dot"></span>資料來源：Google Sheets（即時讀取）</span>
  <button class="rbtn" onclick="loadData()">重新整理</button>
</div>
<div class="main">
  <div class="err" id="err"></div>
  <div id="loading" class="loading"><div class="spinner"></div>正在從 Google Sheets 載入資料⋯</div>
  <div id="dash" style="display:none">
    <div class="stats" id="stats"></div>
    <div class="sh"><h2>重要里程碑</h2><div class="line"></div></div>
    <div class="mg" id="mg"></div>
    <div class="sh"><h2>作品進度追蹤</h2><div class="line"></div></div>
    <div class="tw">
      <table>
        <thead><tr>
          <th>品項名稱</th><th>進場月份</th><th>整體進度</th><th>預計完成日期</th>
          <th>企劃/初稿</th><th>二修</th><th>定稿</th><th>施工進場</th><th>費用到帳</th><th>下一步行動</th>
        </tr></thead>
        <tbody id="tb"></tbody>
      </table>
    </div>
  </div>
</div>
<footer>台大 EMBA 30週年場佈專案｜資料每次開啟時自動從 Google Sheets 讀取最新狀態</footer>

<script>
const SID = '15193fhzEGNrBDRk-ZwGgrY9r4CMhAAWBkrvkaX5OJ3Y';

function csvUrl(sheet) {
  return 'https://docs.google.com/spreadsheets/d/' + SID + '/gviz/tq?tqx=out:csv&sheet=' + encodeURIComponent(sheet);
}

async function fetchCSV(sheet) {
  const r = await fetch(csvUrl(sheet), {cache:'no-store'});
  if (!r.ok) throw new Error('HTTP ' + r.status);
  return parseCSV(await r.text());
}

function parseCSV(text) {
  const rows = [];
  for (const line of text.split('\n')) {
    if (!line.trim()) continue;
    const cols = []; let cur = '', inQ = false;
    for (const c of line) {
      if (c === '"') { inQ = !inQ; }
      else if (c === ',' && !inQ) { cols.push(cur.trim()); cur = ''; }
      else cur += c;
    }
    cols.push(cur.trim());
    rows.push(cols);
  }
  return rows;
}

function badge(v) {
  if (!v || v === '—' || v === ' —') return '<span style="color:#ccc">—</span>';
  if (v.includes('完成') || v.includes('✅')) return '<span class="badge b-ok">完成</span>';
  if (v.includes('進行中') || v.includes('🔄')) return '<span class="badge b-wip">進行中</span>';
  if (v.includes('待施工') || v.includes('⬜')) return '<span class="badge b-td">待施工</span>';
  if (v.includes('待請款') || v.includes('⏳')) return '<span class="badge b-wt">待請款</span>';
  if (v.includes('未開始')) return '<span class="badge b-td">未開始</span>';
  return '<span class="badge b-td">' + v.replace(/[⬜⏳✅🔄‼️]/g,'').trim() + '</span>';
}

function pbar(pct) {
  const n = Math.round(parseFloat(pct) * 100) || 0;
  const c = n >= 100 ? 'done' : n >= 50 ? 'mid' : '';
  return '<div class="pbw"><div class="pb"><div class="pbf ' + c + '" style="width:' + n + '%"></div></div><span class="pp">' + n + '%</span></div>';
}

async function loadData() {
  document.getElementById('loading').style.display = 'block';
  document.getElementById('dash').style.display = 'none';
  document.getElementById('err').style.display = 'none';
  try {
    const [items, ms] = await Promise.all([
      fetchCSV('📋 作品進度追蹤'),
      fetchCSV('🏠 總覽儀表板')
    ]);
    document.getElementById('lu').textContent = new Date().toLocaleString('zh-TW',{month:'2-digit',day:'2-digit',hour:'2-digit',minute:'2-digit'});
    document.getElementById('loading').style.display = 'none';
    document.getElementById('dash').style.display = 'block';
    renderStats(items);
    renderMilestones(ms);
    renderItems(items);
  } catch(e) {
    document.getElementById('loading').style.display = 'none';
    document.getElementById('dash').style.display = 'block';
    const eb = document.getElementById('err');
    eb.style.display = 'block';
    eb.textContent = '無法讀取資料：' + e.message + '。請確認試算表已設為「知道連結的人可以檢視」。';
  }
}

function renderStats(rows) {
  const data = rows.slice(2).filter(r => r[1]&&r[1].trim()&&r[8]&&r[8].trim()!=='—'&&r[8].trim()!==' —');
  const total = data.length;
  const done  = data.filter(r => parseFloat(r[3]||0) >= 1).length;
  const wip   = data.filter(r => { const p=parseFloat(r[3]||0); return p>0&&p<1; }).length;
  const avg   = total > 0 ? Math.round(data.reduce((s,r) => s + parseFloat(r[3]||0)*100, 0)/total) : 0;
  const days  = Math.ceil((new Date('2026-10-17') - new Date()) / 864e5);
  document.getElementById('stats').innerHTML =
    '<div class="sc hi"><div class="lbl">整體進度</div><div class="num">' + avg + '<span style="font-size:1rem;font-weight:400">%</span></div><div class="sub">所有主品項平均</div></div>' +
    '<div class="sc"><div class="lbl">品項總數</div><div class="num">' + total + '</div><div class="sub">主品項</div></div>' +
    '<div class="sc"><div class="lbl">進行中</div><div class="num" style="color:var(--amber)">' + wip + '</div><div class="sub">品項</div></div>' +
    '<div class="sc"><div class="lbl">已完成</div><div class="num" style="color:var(--green)">' + done + '</div><div class="sub">品項</div></div>' +
    '<div class="sc"><div class="lbl">活動倒數</div><div class="num" style="color:' + (days<=30?'var(--red)':'var(--text)') + '">' + days + '</div><div class="sub">天（10/17活動日）</div></div>';
}

function renderMilestones(rows) {
  const g = document.getElementById('mg');
  g.innerHTML = '';
  let on = false;
  for (const r of rows) {
    const b=r[1]||'', c=r[2]||'', d=r[3]||'', e=r[4]||'';
    if (b==='里程碑事項') { on=true; continue; }
    if (!on || !b || b.trim()==='') continue;
    if (b==='請款月份') break;
    const cls = d.includes('✅')?'ok': d.includes('緊急')?'urg':'pnd';
    const bc  = d.includes('✅')?'b-ok': d.includes('緊急')?'b-wn':'b-td';
    const el = document.createElement('div');
    el.className = 'mc ' + cls;
    el.innerHTML = '<div class="me">' + b + '</div><div class="md">' + c + '</div>' +
      (d ? '<div><span class="badge ' + bc + '">' + d.replace(/[✅⏳‼️]/g,'').trim() + '</span></div>' : '') +
      '<div class="mn" style="margin-top:6px">' + e + '</div>';
    g.appendChild(el);
  }
}

function renderItems(rows) {
  const tb = document.getElementById('tb');
  tb.innerHTML = '';
  for (const r of rows.slice(2)) {
    if (!r[1] || r[1].trim() === '') continue;
    const isMain = r[8] && r[8].trim() !== '' && r[8].trim() !== '—' && r[8].trim() !== ' —';
    const tr = document.createElement('tr');
    if (!isMain) tr.style.background = 'rgba(0,0,0,0.012)';
    const nameStyle = isMain ? '' : 'font-weight:400;color:var(--text-muted);padding-left:24px';
    tr.innerHTML =
      '<td class="nm" style="' + nameStyle + '">' + (r[1]||'') + '</td>' +
      '<td class="mo">' + (r[2]||'') + '</td>' +
      '<td>' + (isMain ? pbar(r[3]||'0') : '') + '</td>' +
      '<td class="mo" style="font-size:.72rem">' + (r[4]||'') + '</td>' +
      '<td>' + badge(r[5]) + '</td>' +
      '<td>' + badge(r[6]) + '</td>' +
      '<td>' + badge(r[7]) + '</td>' +
      '<td>' + (isMain ? badge(r[8]) : '<span style="color:#ccc">—</span>') + '</td>' +
      '<td>' + (isMain ? badge(r[9]) : '<span style="color:#ccc">—</span>') + '</td>' +
      '<td style="font-size:.72rem;color:var(--text-muted);max-width:200px">' + (r[11]||'') + '</td>';
    tb.appendChild(tr);
  }
}

loadData();
</script>
</body>
</html>
