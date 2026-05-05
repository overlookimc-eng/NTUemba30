<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>台大EMBA 30週年場佈｜專案進度儀表板</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700&family=DM+Mono:wght@400;500&display=swap');

  :root {
    --bg: #f7f6f2;
    --surface: #ffffff;
    --border: #e8e5de;
    --border-strong: #d0ccc2;
    --text: #1a1916;
    --text-muted: #7a766e;
    --text-hint: #b0ac a4;
    --accent: #1a4a3a;
    --accent-light: #e6f0ec;
    --amber: #b8680a;
    --amber-light: #fef3e2;
    --red: #8b2020;
    --red-light: #fdeaea;
    --green: #1a5c3a;
    --green-light: #e6f4ec;
    --blue: #1a3a6a;
    --blue-light: #e6eef8;
    --gray: #5a5650;
    --gray-light: #f0ede8;
    --r: 6px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Noto Sans TC', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    font-size: 14px;
    line-height: 1.6;
  }

  header {
    background: var(--accent);
    color: white;
    padding: 2rem 2.5rem 1.5rem;
    position: relative;
    overflow: hidden;
  }
  header::before {
    content: '30';
    position: absolute;
    right: 2rem;
    top: 50%;
    transform: translateY(-50%);
    font-size: 9rem;
    font-weight: 700;
    opacity: 0.08;
    font-family: 'DM Mono', monospace;
    line-height: 1;
  }
  header h1 {
    font-size: 1.35rem;
    font-weight: 500;
    letter-spacing: 0.02em;
    margin-bottom: 0.25rem;
  }
  header p {
    font-size: 0.8rem;
    opacity: 0.65;
    font-weight: 300;
  }
  .header-meta {
    display: flex;
    gap: 2rem;
    margin-top: 1.25rem;
    flex-wrap: wrap;
  }
  .header-meta-item {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }
  .header-meta-item .label {
    font-size: 0.68rem;
    opacity: 0.5;
    text-transform: uppercase;
    letter-spacing: 0.08em;
  }
  .header-meta-item .value {
    font-size: 1rem;
    font-weight: 500;
    font-family: 'DM Mono', monospace;
  }

  .refresh-bar {
    background: var(--surface);
    border-bottom: 1px solid var(--border);
    padding: 0.6rem 2.5rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 0.75rem;
    color: var(--text-muted);
  }
  .refresh-bar .status-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: #4caf50;
    display: inline-block;
    margin-right: 6px;
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%,100% { opacity: 1; }
    50% { opacity: 0.4; }
  }
  .refresh-btn {
    background: none;
    border: 1px solid var(--border-strong);
    border-radius: var(--r);
    padding: 4px 12px;
    font-size: 0.72rem;
    cursor: pointer;
    color: var(--text-muted);
    font-family: inherit;
    transition: all 0.15s;
  }
  .refresh-btn:hover { background: var(--gray-light); color: var(--text); }

  .main { padding: 1.5rem 2.5rem 3rem; max-width: 1400px; }

  .error-banner {
    background: var(--amber-light);
    border: 1px solid #e6a020;
    border-radius: var(--r);
    padding: 1rem 1.25rem;
    margin-bottom: 1.5rem;
    font-size: 0.82rem;
    color: var(--amber);
    display: none;
  }

  .config-box {
    background: var(--blue-light);
    border: 1px solid #b0c8e8;
    border-radius: var(--r);
    padding: 1rem 1.25rem;
    margin-bottom: 1.5rem;
    font-size: 0.82rem;
    color: var(--blue);
    display: none;
  }
  .config-box code {
    background: white;
    border: 1px solid #c0d4ec;
    border-radius: 4px;
    padding: 2px 6px;
    font-family: 'DM Mono', monospace;
    font-size: 0.78rem;
    word-break: break-all;
  }

  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 10px;
    margin-bottom: 1.5rem;
  }
  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--r);
    padding: 1rem 1.1rem;
  }
  .stat-card .label {
    font-size: 0.68rem;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.06em;
    margin-bottom: 6px;
  }
  .stat-card .number {
    font-size: 1.8rem;
    font-weight: 700;
    font-family: 'DM Mono', monospace;
    line-height: 1;
    color: var(--text);
  }
  .stat-card .sub {
    font-size: 0.7rem;
    color: var(--text-muted);
    margin-top: 4px;
  }
  .stat-card.highlight { background: var(--accent-light); border-color: #9fc8b4; }
  .stat-card.highlight .number { color: var(--accent); }

  .section-header {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 0.75rem;
    margin-top: 1.5rem;
  }
  .section-header h2 {
    font-size: 0.82rem;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--text-muted);
  }
  .section-header .line {
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .table-wrap { overflow-x: auto; margin-bottom: 1.5rem; }
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.8rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--r);
    overflow: hidden;
  }
  thead th {
    background: var(--gray-light);
    border-bottom: 1px solid var(--border-strong);
    padding: 8px 12px;
    text-align: left;
    font-weight: 500;
    font-size: 0.72rem;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--text-muted);
    white-space: nowrap;
  }
  tbody tr {
    border-bottom: 1px solid var(--border);
    transition: background 0.1s;
  }
  tbody tr:last-child { border-bottom: none; }
  tbody tr:hover { background: var(--bg); }
  tbody td {
    padding: 8px 12px;
    vertical-align: middle;
    color: var(--text);
  }
  td.item-name { font-weight: 500; min-width: 200px; }
  td.mono { font-family: 'DM Mono', monospace; font-size: 0.75rem; }

  .badge {
    display: inline-block;
    padding: 2px 8px;
    border-radius: 100px;
    font-size: 0.68rem;
    font-weight: 500;
    white-space: nowrap;
  }
  .badge-done { background: var(--green-light); color: var(--green); }
  .badge-wip  { background: var(--amber-light); color: var(--amber); }
  .badge-todo { background: var(--gray-light);  color: var(--gray); }
  .badge-wait { background: var(--blue-light);  color: var(--blue); }
  .badge-warn { background: var(--red-light);   color: var(--red); }

  .progress-bar-wrap {
    display: flex;
    align-items: center;
    gap: 8px;
    min-width: 120px;
  }
  .progress-bar {
    flex: 1;
    height: 6px;
    background: var(--gray-light);
    border-radius: 3px;
    overflow: hidden;
  }
  .progress-bar-fill {
    height: 100%;
    border-radius: 3px;
    background: var(--accent);
    transition: width 0.6s ease;
  }
  .progress-bar-fill.mid  { background: var(--amber); }
  .progress-bar-fill.done { background: var(--green); }
  .progress-pct {
    font-family: 'DM Mono', monospace;
    font-size: 0.72rem;
    color: var(--text-muted);
    min-width: 32px;
    text-align: right;
  }

  .milestone-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 10px;
    margin-bottom: 1.5rem;
  }
  .milestone-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--r);
    padding: 0.9rem 1rem;
    border-left: 3px solid var(--border-strong);
  }
  .milestone-card.urgent { border-left-color: #c0392b; }
  .milestone-card.pending { border-left-color: var(--amber); }
  .milestone-card.ok { border-left-color: var(--green); }
  .milestone-card .m-event { font-weight: 500; font-size: 0.82rem; margin-bottom: 4px; }
  .milestone-card .m-date {
    font-family: 'DM Mono', monospace;
    font-size: 0.72rem;
    color: var(--text-muted);
    margin-bottom: 4px;
  }
  .milestone-card .m-note { font-size: 0.72rem; color: var(--text-muted); }

  .loading {
    text-align: center;
    padding: 3rem 2rem;
    color: var(--text-muted);
    font-size: 0.85rem;
  }
  .loading .spinner {
    width: 28px; height: 28px;
    border: 2px solid var(--border);
    border-top-color: var(--accent);
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
    margin: 0 auto 1rem;
  }
  @keyframes spin { to { transform: rotate(360deg); } }

  footer {
    text-align: center;
    padding: 1.5rem;
    font-size: 0.7rem;
    color: var(--text-muted);
    border-top: 1px solid var(--border);
    margin-top: 2rem;
  }

  @media (max-width: 640px) {
    header, .main, .refresh-bar { padding-left: 1rem; padding-right: 1rem; }
    .stats-grid { grid-template-columns: repeat(2, 1fr); }
  }
</style>
</head>
<body>

<header>
  <h1>台大 EMBA 30週年｜場佈專案進度儀表板</h1>
  <p>活動日期：2026/10/17–18　｜　施工進場截止：2026/10/16</p>
  <div class="header-meta">
    <div class="header-meta-item">
      <span class="label">專案期間</span>
      <span class="value">5/5 – 10/18</span>
    </div>
    <div class="header-meta-item">
      <span class="label">主要廠商</span>
      <span class="value">4 家</span>
    </div>
    <div class="header-meta-item">
      <span class="label">總金額（含稅）</span>
      <span class="value">NT$1,095,171</span>
    </div>
    <div class="header-meta-item">
      <span class="label">最後更新</span>
      <span class="value" id="last-update">—</span>
    </div>
  </div>
</header>

<div class="refresh-bar">
  <span><span class="status-dot"></span>資料來源：Google Sheets（即時讀取）</span>
  <button class="refresh-btn" onclick="loadData()">重新整理</button>
</div>

<div class="main">

  <div class="config-box" id="config-hint">
    <strong>設定說明：</strong>請將下方程式碼中的 <code>15193fhzEGNrBDRk-ZwGgrY9r4CMhAAWBkrvkaX5OJ3Y</code> 替換為你的 Google 試算表 ID。<br>
    試算表 ID 是網址中 <code>/d/</code> 和 <code>/edit</code> 之間的那段文字。<br>
    同時確保試算表已設定為「知道連結的人可以檢視」。
  </div>

  <div class="error-banner" id="error-banner"></div>

  <div id="loading-state" class="loading">
    <div class="spinner"></div>
    正在從 Google Sheets 載入資料⋯
  </div>

  <div id="dashboard" style="display:none">

    <div class="stats-grid" id="stats-grid"></div>

    <div class="section-header">
      <h2>重要里程碑</h2>
      <div class="line"></div>
    </div>
    <div class="milestone-grid" id="milestone-grid"></div>

    <div class="section-header">
      <h2>作品進度追蹤</h2>
      <div class="line"></div>
    </div>
    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>品項名稱</th>
            <th>進場月份</th>
            <th>整體進度</th>
            <th>預計完成日期</th>
            <th>企劃/初稿</th>
            <th>二修</th>
            <th>定稿</th>
            <th>施工進場</th>
            <th>費用到帳</th>
            <th>下一步行動</th>
          </tr>
        </thead>
        <tbody id="items-tbody"></tbody>
      </table>
    </div>

  </div>
</div>

<footer>
  台大 EMBA 30週年場佈專案｜資料每次開啟時自動從 Google Sheets 讀取最新狀態
</footer>

<script>
const SHEET_ID = '15193fhzEGNrBDRk-ZwGgrY9r4CMhAAWBkrvkaX5OJ3Y';
const SHEET_NAME = '📋 作品進度追蹤';
const MILESTONE_SHEET = '🏠 總覽儀表板';

function csvUrl(sheet) {
  return `https://docs.google.com/spreadsheets/d/${SHEET_ID}/gviz/tq?tqx=out:csv&sheet=${encodeURIComponent(sheet)}`;
}

async function fetchCSV(sheet) {
  const res = await fetch(csvUrl(sheet));
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  const text = await res.text();
  return parseCSV(text);
}

function parseCSV(text) {
  const rows = [];
  const lines = text.split('\n');
  for (const line of lines) {
    if (!line.trim()) continue;
    const cols = [];
    let cur = '', inQ = false;
    for (let i = 0; i < line.length; i++) {
      const c = line[i];
      if (c === '"') { inQ = !inQ; }
      else if (c === ',' && !inQ) { cols.push(cur.trim()); cur = ''; }
      else cur += c;
    }
    cols.push(cur.trim());
    rows.push(cols);
  }
  return rows;
}

function statusBadge(val) {
  if (!val || val === ' —' || val === '—') return '<span style="color:#b0ac a4;font-size:0.7rem;">—</span>';
  if (val.includes('完成') || val.includes('✅')) return `<span class="badge badge-done">完成</span>`;
  if (val.includes('進行中') || val.includes('🔄')) return `<span class="badge badge-wip">進行中</span>`;
  if (val.includes('待施工') || val.includes('⬜')) return `<span class="badge badge-todo">待施工</span>`;
  if (val.includes('待請款') || val.includes('⏳')) return `<span class="badge badge-wait">待請款</span>`;
  if (val.includes('未開始')) return `<span class="badge badge-todo">未開始</span>`;
  return `<span class="badge badge-todo">${val.replace(/[⬜⏳✅🔄]/g,'').trim()}</span>`;
}

function progressBar(pct) {
  const n = Math.round(parseFloat(pct) * 100) || 0;
  const cls = n >= 100 ? 'done' : n >= 50 ? 'mid' : '';
  return `<div class="progress-bar-wrap">
    <div class="progress-bar"><div class="progress-bar-fill ${cls}" style="width:${n}%"></div></div>
    <span class="progress-pct">${n}%</span>
  </div>`;
}

function milestoneClass(dateStr, status) {
  if (status && status.includes('✅')) return 'ok';
  if (status && status.includes('緊急')) return 'urgent';
  return 'pending';
}

async function loadData() {
  if (SHEET_ID === 'YOUR_SHEET_ID') {
    document.getElementById('config-hint').style.display = 'block';
    document.getElementById('loading-state').style.display = 'none';
    document.getElementById('dashboard').style.display = 'block';
    renderFallback();
    return;
  }

  document.getElementById('loading-state').style.display = 'block';
  document.getElementById('dashboard').style.display = 'none';
  document.getElementById('error-banner').style.display = 'none';

  try {
    const [itemRows, msRows] = await Promise.all([
      fetchCSV(SHEET_NAME),
      fetchCSV(MILESTONE_SHEET)
    ]);

    document.getElementById('last-update').textContent = new Date().toLocaleString('zh-TW', {month:'2-digit',day:'2-digit',hour:'2-digit',minute:'2-digit'});
    document.getElementById('loading-state').style.display = 'none';
    document.getElementById('dashboard').style.display = 'block';

    renderItems(itemRows);
    renderMilestones(msRows);
    renderStats(itemRows);

  } catch (e) {
    document.getElementById('loading-state').style.display = 'none';
    document.getElementById('dashboard').style.display = 'block';
    const eb = document.getElementById('error-banner');
    eb.style.display = 'block';
    eb.textContent = `無法讀取 Google Sheets 資料：${e.message}。請確認試算表 ID 正確且已設定公開檢視權限。`;
    renderFallback();
  }
}

function renderItems(rows) {
  const tbody = document.getElementById('items-tbody');
  tbody.innerHTML = '';
  const dataRows = rows.slice(2);
  for (const r of dataRows) {
    if (!r[1] || r[1].trim() === '') continue;
    const name = r[1] || '';
    const month = r[2] || '';
    const pct = r[3] || '0';
    const date = r[4] || '';
    const f = r[5] || '';
    const g = r[6] || '';
    const h = r[7] || '';
    const i = r[8] || '';
    const j = r[9] || '';
    const action = r[11] || '';

    const isMain = i && i.trim() !== '' && i.trim() !== '—' && i.trim() !== ' —';
    const tr = document.createElement('tr');
    if (!isMain) tr.style.background = 'rgba(0,0,0,0.012)';
    tr.innerHTML = `
      <td class="item-name" style="${!isMain?'font-weight:400;color:var(--text-muted);padding-left:24px':''}">${name}</td>
      <td class="mono">${month}</td>
      <td>${isMain ? progressBar(pct) : ''}</td>
      <td class="mono" style="font-size:0.72rem">${date}</td>
      <td>${statusBadge(f)}</td>
      <td>${statusBadge(g)}</td>
      <td>${statusBadge(h)}</td>
      <td>${i && i !== ' —' ? statusBadge(i) : '<span style="color:#ccc">—</span>'}</td>
      <td>${j && j !== ' —' ? statusBadge(j) : '<span style="color:#ccc">—</span>'}</td>
      <td style="font-size:0.72rem;color:var(--text-muted);max-width:200px">${action}</td>
    `;
    tbody.appendChild(tr);
  }
}

function renderMilestones(rows) {
  const grid = document.getElementById('milestone-grid');
  grid.innerHTML = '';
  let inMilestone = false;
  for (const r of rows) {
    if (!r || r.length < 3) continue;
    const b = r[1] || '';
    const c = r[2] || '';
    const d = r[3] || '';
    const e = r[4] || '';
    if (b === '里程碑事項') { inMilestone = true; continue; }
    if (!inMilestone || !b || b.trim() === '') continue;
    if (b === '請款月份') break;
    const cls = milestoneClass(c, d);
    const card = document.createElement('div');
    card.className = `milestone-card ${cls}`;
    card.innerHTML = `
      <div class="m-event">${b}</div>
      <div class="m-date">${c}</div>
      <div>${d ? `<span class="badge ${d.includes('✅')?'badge-done':d.includes('緊急')?'badge-warn':'badge-todo'}">${d.replace(/[✅⏳‼️]/g,'').trim()}</span>` : ''}</div>
      <div class="m-note" style="margin-top:6px">${e}</div>
    `;
    grid.appendChild(card);
  }
}

function renderStats(rows) {
  const dataRows = rows.slice(2).filter(r => r[1] && r[1].trim() && r[8] && r[8].trim() !== '' && r[8].trim() !== '—' && r[8].trim() !== ' —');
  const total = dataRows.length;
  const done = dataRows.filter(r => (r[3]||'').includes('1') || parseFloat(r[3]||0) >= 1).length;
  const inProgress = dataRows.filter(r => { const p = parseFloat(r[3]||0); return p > 0 && p < 1; }).length;
  const avgPct = total > 0 ? Math.round(dataRows.reduce((s,r) => s + parseFloat(r[3]||0)*100, 0) / total) : 0;

  const today = new Date();
  const eventDate = new Date('2026-10-17');
  const daysLeft = Math.ceil((eventDate - today) / (1000*60*60*24));

  document.getElementById('stats-grid').innerHTML = `
    <div class="stat-card highlight">
      <div class="label">整體進度</div>
      <div class="number">${avgPct}<span style="font-size:1rem;font-weight:400">%</span></div>
      <div class="sub">所有主品項平均</div>
    </div>
    <div class="stat-card">
      <div class="label">品項總數</div>
      <div class="number">${total}</div>
      <div class="sub">主品項</div>
    </div>
    <div class="stat-card">
      <div class="label">進行中</div>
      <div class="number" style="color:var(--amber)">${inProgress}</div>
      <div class="sub">品項</div>
    </div>
    <div class="stat-card">
      <div class="label">已完成</div>
      <div class="number" style="color:var(--green)">${done}</div>
      <div class="sub">品項</div>
    </div>
    <div class="stat-card">
      <div class="label">活動倒數</div>
      <div class="number" style="color:${daysLeft<=30?'var(--red)':'var(--text)'}">${daysLeft}</div>
      <div class="sub">天（10/17活動日）</div>
    </div>
  `;
}

function renderFallback() {
  const milestones = [
    {event:'大事記背板文案定稿', date:'2026/5/18', status:'⏳ 待啟動', note:'5/5啟動，文案2週完成', cls:'pending'},
    {event:'木作立體字確認下單', date:'2026/5/18', status:'‼️ 緊急', note:'5/5即刻確認廠商，45天製作期', cls:'urgent'},
    {event:'大事記背板施工進場', date:'2026/6/1', status:'⏳ 待啟動', note:'視覺定稿後6月進場', cls:'pending'},
    {event:'三專班帆布定稿施工', date:'2026/8/10', status:'⏳ 待啟動', note:'視覺6/1定稿，帆布製作後8月進場', cls:'pending'},
    {event:'展區文案全數定稿', date:'2026/8/31', status:'⏳ 待啟動', note:'7/1啟動，9月視覺設計', cls:'pending'},
    {event:'所有品項施工完成', date:'2026/10/15', status:'⏳ 待啟動', note:'截止10/16施工進場', cls:'pending'},
  ];
  const grid = document.getElementById('milestone-grid');
  grid.innerHTML = milestones.map(m => `
    <div class="milestone-card ${m.cls}">
      <div class="m-event">${m.event}</div>
      <div class="m-date">${m.date}</div>
      <div><span class="badge ${m.cls==='urgent'?'badge-warn':'badge-todo'}">${m.status.replace(/[⏳‼️]/g,'').trim()}</span></div>
      <div class="m-note" style="margin-top:6px">${m.note}</div>
    </div>
  `).join('');

  const items = [
    ['30週年大事記背板(6F)','6月','0','2026/6/1','⬜ 未開始','⬜ 未開始','⬜ 未開始','⬜ 待施工','⏳ 待請款','文案5/5啟動，視覺5/19，定稿6/1後進場'],
    ['三專班主題帆布(2F)','8月','0','2026/8/10','⬜ 未開始','⬜ 未開始','⬜ 未開始','⬜ 待施工','⏳ 待請款','視覺5/19~6/1，帆布輸出，8月施工'],
    ['台大木作立體字(草皮)','8月','0','2026/8/20','⬜ 未開始','⬜ 未開始','⬜ 未開始','⬜ 待施工','⏳ 待請款','5/5即刻確認廠商下單，45天製作期'],
    ['影像留聲機互動區(1F)','10月','0','2026/10/5','⬜ 未開始','⬜ 未開始','⬜ 未開始','⬜ 待施工','⏳ 待請款','視覺7/1~7/14，硬體備料至9/30'],
    ['跨越三十展區(B1)','10月','0','2026/10/5','⬜ 未開始','⬜ 未開始','⬜ 未開始','⬜ 待施工','⏳ 待請款','文案7/1~8/31，視覺9/1~9/21'],
  ];
  const tbody = document.getElementById('items-tbody');
  tbody.innerHTML = items.map(r => `
    <tr>
      <td class="item-name">${r[0]}</td>
      <td class="mono">${r[1]}</td>
      <td>${progressBar(r[2])}</td>
      <td class="mono" style="font-size:0.72rem">${r[3]}</td>
      <td>${statusBadge(r[4])}</td>
      <td>${statusBadge(r[5])}</td>
      <td>${statusBadge(r[6])}</td>
      <td>${statusBadge(r[7])}</td>
      <td>${statusBadge(r[8])}</td>
      <td style="font-size:0.72rem;color:var(--text-muted)">${r[9]}</td>
    </tr>
  `).join('');

  document.getElementById('stats-grid').innerHTML = `
    <div class="stat-card highlight">
      <div class="label">整體進度</div>
      <div class="number">0<span style="font-size:1rem;font-weight:400">%</span></div>
      <div class="sub">（連結 Sheets 後自動計算）</div>
    </div>
    <div class="stat-card">
      <div class="label">品項總數</div>
      <div class="number">12</div>
      <div class="sub">主品項</div>
    </div>
    <div class="stat-card">
      <div class="label">活動倒數</div>
      <div class="number" style="color:var(--text)">${Math.ceil((new Date('2026-10-17')-new Date())/(1000*60*60*24))}</div>
      <div class="sub">天（10/17活動日）</div>
    </div>
  `;
  document.getElementById('last-update').textContent = '（示範模式）';
}

loadData();
</script>
</body>
</html>
