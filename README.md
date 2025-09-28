<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>だ液とデンプン — 実験計画（ヨウ素／ベネジクト・二択・スクショ対応）</title>
<style>
  :root{
    --bg:#f6f8fb; --card:#fff; --ink:#111827; --muted:#6b7280;
    --border:#e5e7eb; --accent:#2563eb;
  }
  *{box-sizing:border-box}
  body{margin:0; font-family:system-ui,-apple-system,Segoe UI,Roboto,"Noto Sans JP",Meiryo,sans-serif; background:var(--bg); color:var(--ink);}
  header{position:sticky; top:0; z-index:5; background:#ffffffd9; backdrop-filter:blur(6px); border-bottom:1px solid var(--border)}
  .wrap{max-width:1024px; margin:0 auto; padding:12px 16px}
  h1{font-size:18px; margin:0}
  .sub{font-size:12px; color:var(--muted)}
  .toolbar{display:flex; gap:8px; flex-wrap:wrap; margin-top:8px}
  .btn{appearance:none; border:1px solid var(--border); background:var(--card); padding:8px 12px; border-radius:10px; cursor:pointer; font-weight:700}
  .btn.primary{background:var(--accent); color:#fff; border-color:var(--accent)}
  .btn.warn{background:#fff7ed; color:#9a3412; border-color:#fed7aa}
  .btn.ghost{background:#fff}
  main .wrap{padding:16px}
  .tabs{display:flex; gap:8px; flex-wrap:wrap; margin:6px 0 14px}
  .tab{padding:8px 12px; border:1px solid var(--border); border-radius:999px; cursor:pointer; background:#fff; font-weight:800}
  .tab.active{background:var(--accent); color:#fff; border-color:var(--accent)}
  .grid{display:grid; gap:14px}
  @media(min-width:980px){ .grid{grid-template-columns: repeat(2,1fr);} }
  .card{background:var(--card); border:1px solid var(--border); border-radius:16px; padding:14px}
  .tube-head{display:flex; align-items:center; gap:10px; margin-bottom:8px}
  .tube-title{font-weight:800}
  .row{display:grid; grid-template-columns: 130px 1fr; gap:10px; align-items:center; margin:6px 0}
  label{font-weight:700}
  select, textarea, input[type="text"]{width:100%; padding:8px; border:1px solid var(--border); border-radius:10px; background:#fff; font:inherit}
  .muted{color:var(--muted)}
  table{width:100%; border-collapse:collapse; border:1px solid var(--border); border-radius:12px; overflow:hidden}
  th,td{padding:8px; border-bottom:1px solid var(--border); text-align:left; font-size:14px}
  th{background:#f9fafb}
  details{border:1px dashed var(--border); border-radius:12px; padding:10px; background:#fcfcfd}
  summary{cursor:pointer; font-weight:800}
  .foot{font-size:12px; color:var(--muted)}
  @media print{ header,.toolbar,.tabs{display:none!important}; body{background:#fff}; .grid{grid-template-columns:1fr 1fr} .card{break-inside:avoid} }
  .tube-svg{width:60px; height:60px}

  /* Snapshot */
  .snapshot-wrap{margin-top:18px}
  .shot-toolbar{display:flex; gap:10px; align-items:center; flex-wrap:wrap; margin:10px 0}
  .snapshot{
    background:#fff; border:1px solid var(--border); border-radius:16px; padding:16px;
    box-shadow:0 1px 2px rgba(0,0,0,.04);
  }
  .snapshot .title{font-weight:900; font-size:20px; margin:0 0 6px}
  .snapshot .meta{color:var(--muted); font-size:13px; margin-bottom:10px}
  .shot-grid{display:grid; gap:12px}
  @media(min-width:980px){ .shot-grid{grid-template-columns: repeat(2,1fr);} }
  .shot-card{border:1px solid var(--border); border-radius:12px; padding:12px}
  .shot-head{display:flex; align-items:center; gap:12px; margin-bottom:6px}
  .shot-tube{width:90px; height:90px}
  .shot-name{font-weight:800}
  .shot-row{display:grid; grid-template-columns: 120px 1fr; gap:8px; font-size:14px; margin:4px 0}
  @media print{ .snapshot{box-shadow:none} }
</style>
</head>
<body>
<header>
  <div class="wrap">
    <h1>だ液 × デンプン — 実験計画</h1>
    <div class="sub">前提：すべての試験管には<strong>デンプン水</strong>が入っている。だ液を入れるか決め、観察試薬の結果を<strong>予想</strong>する。</div>
    <div class="toolbar">
      <button class="btn primary" id="add">試験管を追加</button>
      <button class="btn" id="save">保存</button>
      <button class="btn ghost" id="print">印刷</button>
      <button class="btn warn" id="reset">保存を消す（初期化）</button>
    </div>
  </div>
</header>

<main>
  <div class="wrap">
    <div class="tabs">
      <button class="tab active" id="tab-iodine">実験① ヨウ素液</button>
      <button class="tab" id="tab-bene">実験② ベネジクト液</button>
    </div>

    <details>
      <summary>観点ヒントを表示</summary>
      <ul>
        <li><strong>変える条件</strong>：だ液（入れる／入れない）</li>
        <li><strong>実験① ヨウ素液</strong>：デンプンが残れば青紫（予想として選ぶ）。</li>
        <li><strong>実験② ベネジクト液</strong>：還元糖があれば赤褐色に変化（予想として選ぶ）。</li>
      </ul>
    </details>

    <h2 style="margin:10px 0">試験管（イラストの液色＝現在の予想）</h2>
    <div id="list" class="grid"></div>

    <div class="card">
      <h3>まとめ（メモ）</h3>
      <div class="row">
        <label for="sum">実験のねらい・根拠</label>
        <textarea id="sum" rows="3" placeholder="もしも実験結果にちがいがあったら、○○の条件によるものだと確かめることができる"></textarea>
      </div>
      <div class="row">
        <label>予想一覧</label>
        <div id="tbl"></div>
      </div>
    </div>

    <section class="snapshot-wrap">
      <div class="card">
        <h3>スクリーンショット用エリア（発表用）</h3>
        <div class="shot-toolbar">
          <label style="min-width:240px">発表者名：<input id="shotName" type="text" placeholder="氏名や班名"></label>
          <label>表示する実験：
            <select id="shotMode">
              <option value="current">現在のタブ（実験①/②）</option>
              <option value="iodine">実験① ヨウ素液</option>
              <option value="bene">実験② ベネジクト液</option>
              <option value="both">両方（①と②）</option>
            </select>
          </label>
          <button class="btn" id="shotRefresh">スクショ用表示を更新</button>
          <span class="muted">※この下の白い枠を画面キャプチャしてください。</span>
        </div>
        <div id="snapshot" class="snapshot"></div>
      </div>
    </section>
  </div>
</main>

<footer>
  <div class="wrap foot">© 授業用ツール。ローカル保存対応。</div>
</footer>

<script>
(function(){
  const qs = s=>document.querySelector(s);
  const qsa = s=>Array.from(document.querySelectorAll(s));
  const h=(t,p={},...c)=>{const e=document.createElement(t); for(const[k,v] of Object.entries(p)){ if(k==='class')e.className=v; else if(k==='html')e.innerHTML=v; else e.setAttribute(k,v);} for(const x of c){ if(x==null)continue; if(typeof x==='string') e.appendChild(document.createTextNode(x)); else e.appendChild(x);} return e;};
  const uid=()=> 't_'+Math.random().toString(36).slice(2,9);

  const STORE_KEY = 'saliva_plan_tabs_v6_bene_simple';

  // Colors
  const BLUEPURPLE = '#3b4cca'; // iodine positive
  const BROWN = '#8b5e34';      // iodine negative (iodine color)
  const BASE = '#93c5fd';       // default
  const BENEMAP = { none:'#2563eb', 'red-brown':'#b45309' }; // 二択だけ

  // State
  let state = load() || { exp:'iodine', tubes:[], memo:'', snapshot:{name:'', mode:'current'} };
  if(state.tubes.length===0){
    state.tubes.push(makeTube('試験管 A', true));
    state.tubes.push(makeTube('試験管 B', false));
  }

  function makeTube(title, saliva){
    return {
      id:uid(), title, saliva:!!saliva,
      iodine:'unknown',        // 'blue' | 'no-blue' | 'unknown'
      benedict:'unknown',      // 'none' | 'red-brown' | 'unknown'
    };
  }

  function colorForTube(t){
    if(state.exp==='iodine'){
      if(t.iodine==='blue') return BLUEPURPLE;
      if(t.iodine==='no-blue') return BROWN;
      return BASE;
    }else{
      if(t.benedict in BENEMAP) return BENEMAP[t.benedict];
      return BASE;
    }
  }

  function tubeSVG(color){
    const svg = document.createElementNS('http://www.w3.org/2000/svg','svg');
    svg.setAttribute('viewBox','0 0 64 64'); svg.setAttribute('class','tube-svg');
    const glass = document.createElementNS(svg.namespaceURI,'rect'); glass.setAttribute('x','20'); glass.setAttribute('y','6'); glass.setAttribute('width','24'); glass.setAttribute('height','52'); glass.setAttribute('rx','8'); glass.setAttribute('fill','#e5e7eb'); glass.setAttribute('stroke','#94a3b8');
    const liq = document.createElementNS(svg.namespaceURI,'rect'); liq.setAttribute('x','22'); liq.setAttribute('y','38'); liq.setAttribute('width','20'); liq.setAttribute('height','18'); liq.setAttribute('rx','6'); liq.setAttribute('fill', color);
    svg.appendChild(glass); svg.appendChild(liq);
    return svg;
  }
  function tubeSVGShot(color){
    const svg = document.createElementNS('http://www.w3.org/2000/svg','svg');
    svg.setAttribute('viewBox','0 0 100 100'); svg.setAttribute('class','shot-tube');
    const g = document.createElementNS(svg.namespaceURI,'g');
    const glass = document.createElementNS(svg.namespaceURI,'rect'); glass.setAttribute('x','30'); glass.setAttribute('y','10'); glass.setAttribute('width','40'); glass.setAttribute('height','80'); glass.setAttribute('rx','10'); glass.setAttribute('fill','#e5e7eb'); glass.setAttribute('stroke','#94a3b8');
    const liq = document.createElementNS(svg.namespaceURI,'rect'); liq.setAttribute('x','32'); liq.setAttribute('y','56'); liq.setAttribute('width','36'); liq.setAttribute('height','32'); liq.setAttribute('rx','8'); liq.setAttribute('fill', color);
    g.appendChild(glass); g.appendChild(liq); svg.appendChild(g); return svg;
  }

  function renderUI(){
    // tabs
    qsa('.tab').forEach(b=>b.classList.remove('active'));
    qs('#tab-'+state.exp).classList.add('active');

    // list
    const list = qs('#list'); list.innerHTML='';
    for(const t of state.tubes){
      list.appendChild(renderTubeCard(t));
    }

    // table
    renderTable();

    // memo
    const sum = qs('#sum'); if(sum && sum!==document.activeElement) sum.value = state.memo || '';
  }

  function renderTubeCard(t){
    const color = colorForTube(t);
    const card = h('div',{class:'card'});
    card.appendChild(h('div',{class:'tube-head'},
      tubeSVG(color),
      h('div',{}, h('div',{class:'tube-title'}, t.title),
        h('div',{class:'muted'}, state.exp==='iodine'?'実験①：ヨウ素液の予想色を表示':'実験②：ベネジクト液の予想色を表示')
      ),
      h('div',{style:'margin-left:auto; display:flex; gap:8px; align-items:center'}, h('button',{class:'btn warn', onclick:()=>{ delTube(t.id); }},'削除'))
    ));

    // saliva
    const salivaRow = h('div',{class:'row'});
    salivaRow.appendChild(h('label',{},'だ液'));
    const salSel = h('select',{});
    salSel.appendChild(h('option',{value:'yes'},'入れる'));
    salSel.appendChild(h('option',{value:'no'},'入れない'));
    salSel.value = t.saliva ? 'yes':'no';
    salSel.addEventListener('change', e=>{ t.saliva=(e.target.value==='yes'); saveSilent(); renderAll(); });
    salivaRow.appendChild(salSel);
    card.appendChild(salivaRow);

    if(state.exp==='iodine'){
      const row = h('div',{class:'row'});
      row.appendChild(h('label',{},'ヨウ素液の予想'));
      const sel = h('select',{});
      [['unknown','選択してください'],['blue','青紫になる'],['no-blue','青紫にならない']].forEach(([v,txt])=> sel.appendChild(h('option',{value:v}, txt)));
      sel.value = t.iodine;
      sel.addEventListener('change', e=>{ t.iodine=e.target.value; saveSilent(); renderAll(); });
      row.appendChild(sel);
      card.appendChild(row);
    }else{
      const row = h('div',{class:'row'});
      row.appendChild(h('label',{},'ベネジクト液の予想'));
      const sel = h('select',{});
      [['unknown','選択してください'],['none','変化なし'],['red-brown','赤褐色']].forEach(([v,txt])=> sel.appendChild(h('option',{value:v}, txt)));
      sel.value = t.benedict;
      sel.addEventListener('change', e=>{ t.benedict=e.target.value; saveSilent(); renderAll(); });
      row.appendChild(sel);
      card.appendChild(row);
    }
    return card;
  }

  function renderTable(){
    const div = qs('#tbl'); div.innerHTML='';
    const table = h('table',{});
    if(state.exp==='iodine'){
      table.appendChild(h('thead',{}, h('tr',{},
        h('th',{},'試験管'), h('th',{},'だ液'), h('th',{},'ヨウ素液（予想）')
      )));
    } else {
      table.appendChild(h('thead',{}, h('tr',{},
        h('th',{},'試験管'), h('th',{},'だ液'), h('th',{},'ベネジクト（予想）')
      )));
    }
    const tbody = h('tbody',{});
    for(const t of state.tubes){
      if(state.exp==='iodine'){
        tbody.appendChild(h('tr',{},
          h('td',{}, t.title),
          h('td',{}, t.saliva?'入れる':'入れない'),
          h('td',{}, dispIodine(t.iodine))
        ));
      }else{
        tbody.appendChild(h('tr',{},
          h('td',{}, t.title),
          h('td',{}, t.saliva?'入れる':'入れない'),
          h('td',{}, dispBene(t.benedict))
        ));
      }
    }
    table.appendChild(tbody); div.appendChild(table);
  }

  function dispIodine(v){ return v==='blue'?'青紫になる': v==='no-blue'?'青紫にならない':'—'; }
  function dispBene(v){ const map={none:'変化なし','red-brown':'赤褐色'}; return map[v] || '—'; }

  // Snapshot
  function renderSnapshot(){
    const wrap = qs('#snapshot'); wrap.innerHTML='';
    const mode = state.snapshot.mode || 'current';
    const name = state.snapshot.name || '';
    const title = h('div',{class:'title'}, mode==='bene'?'実験② ベネジクト液': mode==='iodine'?'実験① ヨウ素液': mode==='both'?'実験①＋②（予想）':'現在のタブ（予想）');
    const meta = h('div',{class:'meta'}, (name? ('発表者：'+name+'　'): '') + '前提：各試験管にデンプン水。だ液は各試験管で設定。');
    wrap.appendChild(title); wrap.appendChild(meta);

    const grid = h('div',{class:'shot-grid'});

    function cardFor(t, which){
      const card = h('div',{class:'shot-card'});
      const head = h('div',{class:'shot-head'});
      const color = (which==='bene')
        ? ((t.benedict in BENEMAP)? BENEMAP[t.benedict]: BASE)
        : (t.iodine==='blue'? '#3b4cca' : (t.iodine==='no-blue'?'#8b5e34': BASE));
      head.appendChild(tubeSVGShot(color));
      head.appendChild(h('div',{class:'shot-name'}, t.title));
      card.appendChild(head);

      const r1 = h('div',{class:'shot-row'}); r1.appendChild(h('div',{},'だ液')); r1.appendChild(h('div',{}, t.saliva?'入れる':'入れない')); card.appendChild(r1);
      if(which==='iodine'){
        const r2 = h('div',{class:'shot-row'}); r2.appendChild(h('div',{},'ヨウ素液の予想')); r2.appendChild(h('div',{}, dispIodine(t.iodine))); card.appendChild(r2);
      }else if(which==='bene'){
        const r3 = h('div',{class:'shot-row'}); r3.appendChild(h('div',{},'ベネジクト液の予想')); r3.appendChild(h('div',{}, dispBene(t.benedict))); card.appendChild(r3);
      }
      return card;
    }

    if(mode==='both'){
      for(const t of state.tubes){
        const both = h('div',{class:'shot-card'});
        const head = h('div',{class:'shot-head'});
        head.appendChild(tubeSVGShot(colorForTube(t)));
        head.appendChild(h('div',{class:'shot-name'}, t.title + '（①/②）'));
        both.appendChild(head);
        const r0 = h('div',{class:'shot-row'}); r0.appendChild(h('div',{},'だ液')); r0.appendChild(h('div',{}, t.saliva?'入れる':'入れない')); both.appendChild(r0);
        const r1 = h('div',{class:'shot-row'}); r1.appendChild(h('div',{},'① ヨウ素液')); r1.appendChild(h('div',{}, dispIodine(t.iodine))); both.appendChild(r1);
        const r2 = h('div',{class:'shot-row'}); r2.appendChild(h('div',{},'② ベネジクト液')); r2.appendChild(h('div',{}, dispBene(t.benedict))); both.appendChild(r2);
        grid.appendChild(both);
      }
    }else if(mode==='iodine' || (mode==='current' && state.exp==='iodine')){
      for(const t of state.tubes){ grid.appendChild(cardFor(t, 'iodine')); }
    }else{
      for(const t of state.tubes){ grid.appendChild(cardFor(t, 'bene')); }
    }

    wrap.appendChild(grid);
  }

  // Combined re-render
  function renderAll(){ renderUI(); renderSnapshot(); }

  // Storage
  function save(){ state.memo = qs('#sum').value; localStorage.setItem(STORE_KEY, JSON.stringify(state)); alert('保存しました'); }
  function saveSilent(){ try{ localStorage.setItem(STORE_KEY, JSON.stringify(state)); }catch(e){} }
  function load(){ try{ const raw=localStorage.getItem(STORE_KEY); return raw?JSON.parse(raw):null; }catch(e){ return null; } }

  // Actions
  function addTube(){
    const title = nextTitle(state.tubes[state.tubes.length-1]?.title || '試験管 A');
    state.tubes.push(makeTube(title, false)); saveSilent(); renderAll();
  }
  function delTube(id){
    if(!confirm('この試験管を削除します。')) return;
    state.tubes = state.tubes.filter(t=>t.id!==id); saveSilent(); renderAll();
  }
  function nextTitle(title){
    const m=title.match(/(.*?)([A-ZＡ-Ｚ])$/); if(m){ const n=String.fromCharCode(m[2].charCodeAt(0)+1); return m[1]+n; }
    return title+'（2）';
  }

  // Events
  qs('#add').addEventListener('click', addTube);
  qs('#save').addEventListener('click', save);
  qs('#print').addEventListener('click', ()=>{ state.memo = qs('#sum').value; saveSilent(); window.print(); });
  qs('#reset').addEventListener('click', ()=>{
    if(!confirm('保存を消して初期化します。')) return;
    localStorage.removeItem(STORE_KEY);
    state = { exp:'iodine', tubes:[ makeTube('試験管 A', true), makeTube('試験管 B', false) ], memo:'', snapshot:{name:'', mode:'current'} };
    renderAll();
  });
  qs('#tab-iodine').addEventListener('click', ()=>{ state.exp='iodine'; saveSilent(); renderAll(); });
  qs('#tab-bene').addEventListener('click', ()=>{ state.exp='bene'; saveSilent(); renderAll(); });

  // Snapshot controls
  const shotName = qs('#shotName');
  const shotMode = qs('#shotMode');
  const shotRefresh = qs('#shotRefresh');
  if(shotName){ shotName.value = state.snapshot.name || ''; shotName.addEventListener('input', e=>{ state.snapshot.name = e.target.value; saveSilent(); renderSnapshot(); }); }
  if(shotMode){ shotMode.value = state.snapshot.mode || 'current'; shotMode.addEventListener('change', e=>{ state.snapshot.mode = e.target.value; saveSilent(); renderSnapshot(); }); }
  if(shotRefresh){ shotRefresh.addEventListener('click', ()=> renderSnapshot()); }

  // Init
  renderAll();
})();
</script>
</body>
</html>
