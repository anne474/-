<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <title>2주 매출 대시보드 (그래프 포함)</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root { color-scheme: dark; }
    body{font-family:system-ui,Arial,sans-serif;background:#0f1115;color:#e6e8ec;margin:24px}
    h1{font-size:20px;margin:0 0 16px}
    .controls{display:flex;gap:12px;flex-wrap:wrap;align-items:end;margin-bottom:16px}
    .field{display:flex;flex-direction:column;gap:6px}
    .field label{font-size:12px;color:#9aa4b2}
    input,button{background:#151923;border:1px solid #2a2f3a;border-radius:8px;color:#e6e8ec;padding:10px 12px}
    button{cursor:pointer}
    table{width:100%;border-collapse:collapse;margin-top:8px}
    th,td{border-bottom:1px solid #222839;padding:10px;text-align:center}
    th{color:#aab3c5;font-weight:600;background:#141926;position:sticky;top:0}
    td input[type="number"]{width:120px;text-align:right}
    .right{text-align:right}
    canvas{margin-top:24px;background:#141926;border-radius:12px;padding:12px}
  </style>
  <!-- Chart.js 불러오기 -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
  <h1>📊 2주 매출 대시보드</h1>

  <!-- 상단 설정 -->
  <div class="controls">
    <div class="field">
      <label for="goal">총 목표 금액</label>
      <input id="goal" type="number" min="0" step="1000" />
    </div>
    <div class="field">
      <label for="start">시작일</label>
      <input id="start" type="date" />
    </div>
    <div class="field">
      <label for="days">기간(일)</label>
      <input id="days" type="number" min="1" step="1" />
    </div>
    <button id="apply">설정 적용</button>
    <button id="reset">초기화</button>
  </div>

  <!-- 요약 -->
  <div class="controls" style="gap:24px">
    <div class="field"><label>누적 목표</label><div id="sumTarget" class="right">-</div></div>
    <div class="field"><label>누적 매출</label><div id="sumSales" class="right">-</div></div>
    <div class="field"><label>총 달성률</label><div id="achv" class="right">-</div></div>
  </div>

  <!-- 표 -->
  <table>
    <thead>
      <tr>
        <th>일차</th>
        <th>날짜(요일)</th>
        <th>일별 목표</th>
        <th>실제 매출</th>
        <th>누적 목표</th>
        <th>누적 매출</th>
        <th>달성률</th>
      </tr>
    </thead>
    <tbody id="tbody"></tbody>
  </table>

  <!-- 그래프 -->
  <canvas id="salesChart" height="100"></canvas>

  <script>
    // ---- 유틸
    const DAYS = ['일','월','화','수','목','금','토'];
    const weekday = (y,m,d) => DAYS[new Date(y, m-1, d).getDay()];
    const fmt = n => (Number(n)||0).toLocaleString();
    const pct = (a,b) => b>0 ? ((a/b)*100).toFixed(2)+'%' : '-';
    const pad2 = n => String(n).padStart(2,'0');

    // ---- 상태 (localStorage 저장)
    const KEY = 'sales-dashboard:v2';
    const todayISO = () => new Date().toISOString().slice(0,10);
    const initState = {
      goal: 1800000,
      start: '2025-09-16',
      days: 14,
      targets: [],
      sales: []
    };
    let state = load() || initState;

    function save(){ localStorage.setItem(KEY, JSON.stringify(state)); }
    function load(){ try{ return JSON.parse(localStorage.getItem(KEY)); }catch(e){ return null; } }

    // ---- DOM
    const $goal  = document.getElementById('goal');
    const $start = document.getElementById('start');
    const $days  = document.getElementById('days');
    const $apply = document.getElementById('apply');
    const $reset = document.getElementById('reset');
    const $tbody = document.getElementById('tbody');
    const $sumTarget = document.getElementById('sumTarget');
    const $sumSales  = document.getElementById('sumSales');
    const $achv      = document.getElementById('achv');

    // ---- 차트 세팅
    const ctx = document.getElementById('salesChart').getContext('2d');
    let chart = new Chart(ctx, {
      type: 'line',
      data: {
        labels: [],
        datasets: [
          { label:'누적 목표', data:[], borderColor:'#8884d8', fill:false },
          { label:'누적 매출', data:[], borderColor:'#82ca9d', fill:false }
        ]
      },
      options: {
        responsive:true,
        plugins:{ legend:{ labels:{ color:'#e6e8ec' } } },
        scales:{
          x:{ ticks:{ color:'#e6e8ec' } },
          y:{ ticks:{ color:'#e6e8ec' } }
        }
      }
    });

    // ---- 렌더
    function render(){
      $goal.value  = state.goal;
      $start.value = state.start;
      $days.value  = state.days;

      const base = Math.floor((state.goal||0)/ (state.days||1));
      for(let i=0;i<state.days;i++){
        if(state.targets[i] == null) state.targets[i] = base;
        if(state.sales[i]   == null) state.sales[i]   = 0;
      }

      $tbody.innerHTML = '';
      let cumT=0, cumS=0, sumT=0, sumS=0;

      const labels=[], dataTarget=[], dataSales=[];

      for(let i=0;i<state.days;i++){
        const d0 = new Date(state.start);
        d0.setDate(d0.getDate()+i);
        const y = d0.getFullYear(), m = d0.getMonth()+1, d = d0.getDate();

        const t = Number(state.targets[i])||0;
        const s = Number(state.sales[i])||0;
        cumT += t; cumS += s;

        const label = `${pad2(m)}/${pad2(d)}(${weekday(y,m,d)})`;
        labels.push(label);
        dataTarget.push(cumT);
        dataSales.push(cumS);

        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${i+1}</td>
          <td>${y}-${pad2(m)}-${pad2(d)} (${weekday(y,m,d)})</td>
          <td class="right"><input type="number" min="0" step="1000" value="${t}" data-idx="${i}" data-k="targets"></td>
          <td class="right"><input type="number" min="0" step="1000" value="${s}" data-idx="${i}" data-k="sales"></td>
          <td class="right">${fmt(cumT)}</td>
          <td class="right">${fmt(cumS)}</td>
          <td class="right">${pct(cumS, cumT)}</td>
        `;
        $tbody.appendChild(tr);

        sumT = cumT; sumS = cumS;
      }

      $sumTarget.textContent = fmt(sumT);
      $sumSales.textContent  = fmt(sumS);
      $achv.textContent      = pct(sumS, sumT);

      // 이벤트 바인딩
      $tbody.querySelectorAll('input[type="number"]').forEach(inp=>{
        inp.oninput = () => {
          const i = Number(inp.dataset.idx);
          const k = inp.dataset.k;
          state[k][i] = Number(inp.value)||0;
          save();
          render();
        };
      });

      // 차트 업데이트
      chart.data.labels = labels;
      chart.data.datasets[0].data = dataTarget;
      chart.data.datasets[1].data = dataSales;
      chart.update();
    }

    // ---- 버튼
    $apply.onclick = () => {
      state.goal  = Number($goal.value)||0;
      state.start = $start.value || todayISO();
      const newDays = Math.max(1, Number($days.value)||1);
      state.days = newDays;
      state.targets.length = newDays;
      state.sales.length   = newDays;
      save();
      render();
    };
    $reset.onclick = () => {
      if(confirm('모든 값을 초기화할까요?')) {
        state = JSON.parse(JSON.stringify(initState));
        save();
        render();
      }
    };

    render();
  </script>
</body>
</html>
