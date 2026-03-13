<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ventas Banamex</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root{
  --red:#C8102E;--red-d:#8B0B1F;--red-f:rgba(200,16,46,0.13);
  --gold:#C8A84B;--gold-l:#f0c060;--gold-f:rgba(200,168,75,0.13);
  --bg:#0d0d0d;--s1:#161616;--s2:#1e1e1e;
  --br:rgba(255,255,255,0.08);--br2:rgba(255,255,255,0.15);
  --tx:#f0ede8;--mu:#777;
  --green:#22c55e;--green-f:rgba(34,197,94,0.11);
  --blue-f:rgba(59,130,246,0.13);
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'Outfit',sans-serif;background:var(--bg);color:var(--tx);min-height:100vh;}

/* LOGIN */
#login-screen{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:1.5rem;}
.login-box{width:100%;max-width:400px;background:var(--s1);border:1px solid var(--br2);border-radius:20px;padding:2.5rem 2rem;}
.l-logo{font-family:'Bebas Neue',sans-serif;font-size:2rem;letter-spacing:.05em;text-align:center;margin-bottom:.3rem;}
.l-logo span{color:var(--red);}
.l-sub{text-align:center;color:var(--mu);font-size:13px;margin-bottom:2rem;}
.lf{display:flex;flex-direction:column;gap:6px;margin-bottom:1rem;}
.lf label{font-size:11px;font-weight:500;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;}
.lf input{background:var(--s2);border:1px solid var(--br2);border-radius:8px;padding:11px 14px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:14px;outline:none;transition:border-color .15s;width:100%;}
.lf input:focus{border-color:var(--red);}
.lf input::placeholder{color:#444;}
.l-btn{width:100%;padding:13px;background:var(--red);border:none;border-radius:10px;color:#fff;font-family:'Outfit',sans-serif;font-size:15px;font-weight:600;cursor:pointer;transition:background .15s,transform .1s;margin-top:.5rem;}
.l-btn:hover{background:var(--red-d);}
.l-btn:active{transform:scale(.98);}
.l-err{display:none;margin-top:1rem;padding:10px 14px;background:var(--red-f);border:1px solid rgba(200,16,46,.3);border-radius:8px;color:#f88;font-size:13px;text-align:center;}
.l-err.show{display:block;}

/* NAV */
#app{display:none;}
nav{display:flex;align-items:center;justify-content:space-between;padding:0 1.5rem;height:54px;background:var(--s1);border-bottom:1px solid var(--br);position:sticky;top:0;z-index:50;}
.n-logo{font-family:'Bebas Neue',sans-serif;font-size:1.3rem;letter-spacing:.05em;}
.n-logo span{color:var(--red);}
.n-right{display:flex;align-items:center;gap:8px;}
.n-user{font-size:12px;color:var(--mu);background:var(--s2);border:1px solid var(--br);border-radius:6px;padding:5px 10px;}
.n-user strong{color:var(--tx);}
.n-tabs{display:flex;gap:4px;}
.tab{padding:5px 14px;border-radius:6px;border:none;font-family:'Outfit',sans-serif;font-size:13px;font-weight:500;cursor:pointer;transition:all .15s;background:transparent;color:var(--mu);}
.tab:hover{color:var(--tx);background:var(--s2);}
.tab.on{background:var(--red);color:#fff;}
.tab.gold.on{background:var(--gold);color:#000;}
.out-btn{padding:5px 12px;border-radius:6px;border:1px solid var(--br2);background:transparent;color:var(--mu);font-family:'Outfit',sans-serif;font-size:12px;cursor:pointer;}
.out-btn:hover{color:var(--tx);}

/* PAGES */
.pg{display:none;}
.pg.on{display:block;}
.wrap{max-width:560px;margin:0 auto;padding:2rem 1.5rem;}
.wide{max-width:1150px;margin:0 auto;padding:2rem 1.5rem;}
.pgtitle{font-family:'Bebas Neue',sans-serif;font-size:2.2rem;letter-spacing:.03em;line-height:1;margin-bottom:.35rem;}
.pgtitle span{color:var(--red);}
.pgtitle.gt span{color:var(--gold);}
.pgsub{color:var(--mu);font-size:13px;margin-bottom:1.75rem;}

/* SPINNER */
.spinner-overlay{position:fixed;inset:0;background:rgba(0,0,0,.6);display:none;align-items:center;justify-content:center;z-index:999;}
.spinner-overlay.show{display:flex;}
.spinner{width:40px;height:40px;border:3px solid var(--br2);border-top-color:var(--red);border-radius:50%;animation:spin .7s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}

/* FORM */
.card{background:var(--s1);border:1px solid var(--br2);border-radius:16px;padding:1.75rem;}
.field{display:flex;flex-direction:column;gap:6px;margin-bottom:1rem;}
.field label{font-size:11px;font-weight:500;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;}
.field input,.field select{background:var(--s2);border:1px solid var(--br2);border-radius:8px;padding:11px 14px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:14px;outline:none;transition:border-color .15s;width:100%;}
.field input:focus,.field select:focus{border-color:var(--red);}
.field select option{background:#1e1e1e;}
.field input::placeholder{color:#444;}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.frow{display:flex;gap:10px;align-items:flex-end;margin-bottom:1rem;}
.frow .field{flex:1;margin-bottom:0;}
.folio-pill{background:var(--s2);border:1px solid var(--br2);border-radius:8px;padding:11px 14px;font-size:11px;color:var(--gold-l);white-space:nowrap;font-weight:600;font-family:monospace;}
.sbtn{width:100%;padding:13px;background:var(--red);border:none;border-radius:10px;color:#fff;font-family:'Outfit',sans-serif;font-size:15px;font-weight:600;cursor:pointer;transition:background .15s;margin-top:.5rem;}
.sbtn:hover{background:var(--red-d);}
.sbtn:disabled{background:#333;color:#666;cursor:not-allowed;}
.toast{display:none;margin-top:1rem;padding:12px 16px;border-radius:10px;font-size:13px;font-weight:500;text-align:center;}
.toast.ok{background:var(--green-f);border:1px solid rgba(34,197,94,.3);color:var(--green);}
.toast.err{background:var(--red-f);border:1px solid rgba(200,16,46,.3);color:#f88;}
.toast.show{display:block;}

/* RECENT */
.slbl{font-size:11px;font-weight:500;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;margin:1.5rem 0 8px;}
.ri{display:flex;justify-content:space-between;align-items:center;padding:10px 14px;background:var(--s1);border:1px solid var(--br);border-radius:8px;margin-bottom:6px;font-size:13px;gap:10px;}
.ri-n{font-weight:500;}
.ri-m{color:var(--mu);font-size:12px;}
.ri-f{font-family:monospace;font-size:11px;color:var(--gold-l);white-space:nowrap;}

/* STATS */
.sgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px;margin-bottom:1.5rem;}
.sc{background:var(--s1);border:1px solid var(--br);border-radius:12px;padding:1rem 1.1rem;}
.sc-l{font-size:11px;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;font-weight:500;}
.sc-v{font-family:'Bebas Neue',sans-serif;font-size:2.2rem;letter-spacing:.03em;margin-top:2px;}
.cv-g{color:var(--gold-l);}
.cv-r{color:var(--red);}
.cv-gr{color:var(--green);}

/* SYNC BAR */
.sync-bar{display:flex;align-items:center;gap:8px;padding:8px 14px;background:var(--s2);border-radius:8px;font-size:12px;color:var(--mu);margin-bottom:1rem;}
.sync-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.sync-dot.ok{background:var(--green);}
.sync-dot.err{background:var(--red);}
.sync-dot.loading{background:var(--gold-l);animation:pulse 1s infinite;}
@keyframes pulse{0%,100%{opacity:1;}50%{opacity:.3;}}

/* TABLE */
.tctrl{display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-bottom:1rem;}
.tctrl input,.tctrl select{background:var(--s1);border:1px solid var(--br2);border-radius:8px;padding:8px 12px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:13px;outline:none;}
.tctrl input{flex:1;min-width:180px;}
.ibtn{padding:8px 14px;border-radius:8px;border:1px solid var(--br2);background:transparent;color:var(--mu);font-family:'Outfit',sans-serif;font-size:12px;font-weight:500;cursor:pointer;transition:all .15s;}
.ibtn.gold{border-color:rgba(200,168,75,.4);color:var(--gold-l);}
.ibtn.gold:hover{background:var(--gold);color:#000;}
.ibtn.danger{border-color:rgba(200,16,46,.3);color:var(--red);}
.ibtn.danger:hover{background:var(--red);color:#fff;}
.twrap{background:var(--s1);border:1px solid var(--br2);border-radius:14px;overflow:auto;}
table{width:100%;border-collapse:collapse;min-width:700px;}
thead tr{background:var(--s2);}
th{padding:10px 14px;text-align:left;font-size:11px;font-weight:600;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;border-bottom:1px solid var(--br);white-space:nowrap;}
td{padding:9px 14px;font-size:12px;border-bottom:1px solid var(--br);vertical-align:middle;}
tr:last-child td{border-bottom:none;}
tr:hover td{background:rgba(255,255,255,.015);}
.tdf{font-family:monospace;font-size:11px;color:var(--gold-l);}
.tdb{font-weight:500;}
.tdm{color:var(--mu);font-size:11px;}
.badge{display:inline-block;padding:2px 8px;border-radius:4px;font-size:11px;font-weight:500;}
.b-r{background:var(--red-f);color:#f88;}
.b-b{background:var(--blue-f);color:#93c5fd;}
.b-g{background:var(--gold-f);color:var(--gold-l);}
.delbtn{background:transparent;border:none;color:#444;cursor:pointer;font-size:14px;padding:2px 6px;border-radius:4px;transition:color .15s;}
.delbtn:hover{color:var(--red);}
.empty{padding:3rem;text-align:center;color:var(--mu);font-size:14px;}

/* RANKING */
.rgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(190px,1fr));gap:8px;margin-top:8px;}
.rcard{background:var(--s1);border:1px solid var(--br);border-radius:10px;padding:12px 14px;display:flex;align-items:center;gap:12px;}
.rpos{font-family:'Bebas Neue',sans-serif;font-size:1.6rem;color:var(--mu);min-width:28px;}
.rp1{color:var(--gold-l);}
.rp2{color:#bbb;}
.rp3{color:#cd7f32;}
.rkn{font-size:13px;font-weight:500;}
.rkc{font-size:12px;color:var(--mu);}

/* USERS */
.twocol{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem;align-items:start;}
.ugrid{display:grid;gap:8px;margin-top:8px;}
.ucard{background:var(--s1);border:1px solid var(--br2);border-radius:12px;padding:12px 14px;display:flex;align-items:center;gap:12px;}
.uav{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:600;font-size:13px;flex-shrink:0;}
.av-e{background:var(--red-f);color:#f88;}
.av-a{background:var(--gold-f);color:var(--gold-l);}
.ui{flex:1;min-width:0;}
.un{font-size:13px;font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.ur{font-size:11px;color:var(--mu);margin-top:2px;}
.del-u{border:none;border-radius:6px;padding:5px 10px;font-family:'Outfit',sans-serif;font-size:11px;font-weight:500;cursor:pointer;transition:all .15s;background:var(--red-f);color:#f88;white-space:nowrap;}
.del-u:hover{background:var(--red);color:#fff;}

/* BENEFICIOS */
.ben-tabs{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:1.5rem;}
.btab{padding:6px 14px;border-radius:20px;border:1px solid var(--br2);background:transparent;color:var(--mu);font-family:'Outfit',sans-serif;font-size:13px;cursor:pointer;transition:all .15s;white-space:nowrap;}
.btab.on{border-color:var(--gold);color:var(--gold-l);background:var(--gold-f);}
.ben-panel{display:none;}
.ben-panel.on{display:block;}
.ben-hero{background:var(--s1);border:1px solid var(--br2);border-radius:16px;padding:1.5rem;}
.ben-name{font-family:'Bebas Neue',sans-serif;font-size:1.8rem;letter-spacing:.03em;color:var(--gold-l);margin-bottom:.75rem;}
.ben-meta{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:8px;margin-bottom:1.25rem;}
.bm{background:var(--s2);border-radius:10px;padding:10px 12px;}
.bm-l{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;font-weight:500;}
.bm-v{font-size:14px;font-weight:500;margin-top:3px;}
.bm-v.red{color:#f88;}
.bm-v.green{color:var(--green);}
.ben-list{list-style:none;display:flex;flex-direction:column;gap:8px;}
.ben-list li{display:flex;gap:10px;align-items:flex-start;font-size:13px;line-height:1.6;color:#ccc;background:var(--s2);border-radius:8px;padding:10px 12px;}
.ben-bullet{min-width:20px;height:20px;border-radius:50%;background:var(--gold-f);color:var(--gold-l);font-size:11px;font-weight:600;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px;}

@media(max-width:640px){
  nav{padding:0 1rem;}
  .twocol{grid-template-columns:1fr;}
  .row2{grid-template-columns:1fr;}
}
</style>
</head>
<body>

<div class="spinner-overlay" id="spinner"><div class="spinner"></div></div>

<!-- LOGIN -->
<div id="login-screen">
  <div class="login-box">
    <div class="l-logo">BANAMEX <span>VENTAS</span></div>
    <p class="l-sub">Inicia sesión con tu cuenta</p>
    <div class="lf"><label>Usuario</label><input type="text" id="l-user" placeholder="tu usuario" autocomplete="username"></div>
    <div class="lf"><label>Contraseña</label><input type="password" id="l-pass" placeholder="••••••••" autocomplete="current-password"></div>
    <button class="l-btn" id="login-btn">Entrar</button>
    <div class="l-err" id="login-err"></div>
  </div>
</div>

<!-- APP -->
<div id="app">
  <nav>
    <div class="n-logo">BANAMEX <span>VENTAS</span></div>
    <div class="n-tabs" id="n-tabs"></div>
    <div class="n-right">
      <div class="n-user">Hola, <strong id="nav-name"></strong></div>
      <button class="out-btn" id="logout-btn">Salir</button>
    </div>
  </nav>

  <!-- EJECUTIVO -->
  <div id="pg-exec" class="pg">
    <div class="wrap">
      <div class="pgtitle">Nueva <span>venta</span></div>
      <p class="pgsub">Registra los datos de tu tarjeta vendida</p>
      <div class="card">
        <div class="row2">
          <div class="field"><label>Nombre del cliente</label><input type="text" id="f-cliente" placeholder="Ej. María González"></div>
          <div class="field"><label>Teléfono del cliente</label><input type="tel" id="f-tel" placeholder="Ej. 5512345678" maxlength="15"></div>
        </div>
        <div class="row2">
          <div class="field">
            <label>Tipo de tarjeta vendida</label>
            <select id="f-tarjeta">
              <option value="">— Selecciona —</option>
              <option>Joy Banamex</option><option>Clásica Banamex</option><option>Teleton Banamex</option>
              <option>Oro Banamex</option><option>Descubre Banamex</option>
              <option>Platinum Banamex</option><option>Explora Banamex</option><option>Otra</option>
            </select>
          </div>
          <div class="field"><label>Fecha de venta</label><input type="date" id="f-fecha"></div>
        </div>
        <div class="frow">
          <div class="field"><label>Folio (automático si lo dejas vacío)</label><input type="text" id="f-folio" placeholder="BNX-000001" maxlength="20"></div>
          <div class="folio-pill" id="folio-pill">—</div>
        </div>
        <button class="sbtn" id="reg-btn">Registrar venta</button>
        <div class="toast ok" id="t-ok"></div>
        <div class="toast err" id="t-err"></div>
      </div>
      <div class="slbl">Mis últimas ventas</div>
      <div id="exec-recent"></div>
    </div>
  </div>

  <!-- BENEFICIOS -->
  <div id="pg-ben" class="pg">
    <div class="wide">
      <div class="pgtitle">Beneficios de <span>tarjetas</span></div>
      <p class="pgsub">Consulta rápida de beneficios, tasas y requisitos</p>
      <div class="ben-tabs" id="ben-tabs"></div>
      <div id="ben-panels"></div>
    </div>
  </div>

  <!-- DASHBOARD -->
  <div id="pg-dash" class="pg">
    <div class="wide">
      <div class="pgtitle gt">Dashboard <span>ventas</span></div>
      <p class="pgsub">Todas las ventas de tu equipo en tiempo real</p>
      <div class="sync-bar"><div class="sync-dot loading" id="sync-dot"></div><span id="sync-txt">Cargando…</span></div>
      <div class="sgrid">
        <div class="sc"><div class="sc-l">Total ventas</div><div class="sc-v cv-g" id="s-tot">—</div></div>
        <div class="sc"><div class="sc-l">Ejecutivos activos</div><div class="sc-v cv-r" id="s-exe">—</div></div>
        <div class="sc"><div class="sc-l">Hoy</div><div class="sc-v cv-gr" id="s-hoy">—</div></div>
        <div class="sc"><div class="sc-l">Esta semana</div><div class="sc-v" id="s-sem">—</div></div>
      </div>
      <div class="tctrl">
        <input type="text" id="d-search" placeholder="Buscar ejecutivo, cliente o folio…">
        <select id="d-filt">
          <option value="">Todas las tarjetas</option>
          <option>Joy Banamex</option><option>Clásica Banamex</option><option>Teleton Banamex</option>
          <option>Oro Banamex</option><option>Descubre Banamex</option><option>Platinum Banamex</option>
          <option>Explora Banamex</option><option>Otra</option>
        </select>
        <button class="ibtn gold" id="refresh-btn">↻ Actualizar</button>
        <button class="ibtn gold" id="export-btn">Exportar CSV</button>
        <button class="ibtn danger" id="clear-btn">Borrar todo</button>
      </div>
      <div class="twrap">
        <table>
          <thead><tr>
            <th>Folio</th><th>Ejecutivo</th><th>Cliente</th><th>Teléfono</th>
            <th>Tarjeta</th><th>Fecha venta</th><th>Registrado</th><th></th>
          </tr></thead>
          <tbody id="t-body"></tbody>
        </table>
        <div class="empty" id="t-empty" style="display:none">No hay ventas registradas todavía.</div>
      </div>
      <div class="slbl" style="margin-top:1.75rem">Ranking de ejecutivos</div>
      <div class="rgrid" id="rank-grid"></div>
    </div>
  </div>

  <!-- USUARIOS -->
  <div id="pg-users" class="pg">
    <div class="wide">
      <div class="pgtitle gt">Gestión de <span>usuarios</span></div>
      <p class="pgsub">Agrega o elimina ejecutivos. La cuenta admin no se puede borrar.</p>
      <div class="twocol">
        <div class="card">
          <div style="font-size:14px;font-weight:500;margin-bottom:1.2rem;">Agregar ejecutivo</div>
          <div class="field"><label>Nombre completo</label><input type="text" id="nu-name" placeholder="Ej. Juan Pérez"></div>
          <div class="field"><label>Usuario</label><input type="text" id="nu-user" placeholder="Ej. jperez" autocomplete="off"></div>
          <div class="field"><label>Contraseña</label><input type="password" id="nu-pass" placeholder="Mínimo 4 caracteres"></div>
          <button class="sbtn" id="add-user-btn">Agregar ejecutivo</button>
          <div class="toast ok" id="u-ok"></div>
          <div class="toast err" id="u-err"></div>
        </div>
        <div>
          <div class="slbl" style="margin-top:0">Ejecutivos registrados</div>
          <div class="ugrid" id="ugrid"></div>
        </div>
      </div>
    </div>
  </div>
</div>

<script>
/* ── TELEGRAM CONFIG ── */
const TG_TOKEN = '8674156237:AAH_TxLj17k8U08zwTuz1XxrvNLgaqsPNcE';
const TG_CHAT  = '-1003454541647';
const TG_URL   = 'https://api.telegram.org/bot' + TG_TOKEN;

/* ── LOCAL CACHE ── */
const SK_S = 'bnx_sales_v5';
const SK_U = 'bnx_users_v5';
const SK_OFFSET = 'bnx_tg_offset';

function loadS(k){ try{ return JSON.parse(localStorage.getItem(k))||[]; }catch{ return []; } }
function saveS(k,d){ localStorage.setItem(k, JSON.stringify(d)); }

/* ── TELEGRAM API ── */
async function tgPost(method, params={}){
  const r = await fetch(`${TG_URL}/${method}`, {
    method: 'POST',
    headers: {'Content-Type':'application/json'},
    body: JSON.stringify(params)
  });
  return await r.json();
}

// Guarda datos en Telegram como mensaje en el grupo
async function tgSave(type, data){
  const text = `BNX_${type}:${JSON.stringify(data)}`;
  await tgPost('sendMessage', { chat_id: TG_CHAT, text });
}

// Lee el estado más reciente desde Telegram
async function tgLoad(type){
  const offset = parseInt(localStorage.getItem(SK_OFFSET)||'0');
  const r = await tgPost('getUpdates', { offset: offset > 0 ? offset : undefined, limit: 100 });
  if(!r.ok) return null;
  const prefix = `BNX_${type}:`;
  let latest = null;
  let maxId = offset;
  for(const u of (r.result||[])){
    if(u.update_id >= maxId) maxId = u.update_id + 1;
    const txt = u.message?.text || '';
    if(u.message?.chat?.id?.toString() === TG_CHAT && txt.startsWith(prefix)){
      try{ latest = JSON.parse(txt.slice(prefix.length)); }catch{}
    }
  }
  if(maxId > offset) localStorage.setItem(SK_OFFSET, maxId);
  return latest;
}

/* ── API wrapper ── */
async function api(action, body={}){
  try{
    if(action==='getSales'){
      const remote = await tgLoad('SALES');
      if(remote !== null){ saveS(SK_S, remote); return {ok:true, data:remote}; }
      return {ok:true, data: loadS(SK_S)};
    }
    if(action==='addSale'){
      const arr = loadS(SK_S);
      arr.unshift(body);
      saveS(SK_S, arr);
      await tgSave('SALES', arr);
      return {ok:true};
    }
    if(action==='deleteSale'){
      const arr = loadS(SK_S).filter(v=>v.folio!==body.folio);
      saveS(SK_S, arr);
      await tgSave('SALES', arr);
      return {ok:true};
    }
    if(action==='clearSales'){
      saveS(SK_S, []);
      await tgSave('SALES', []);
      return {ok:true};
    }
    if(action==='getUsers'){
      const remote = await tgLoad('USERS');
      if(remote !== null){ saveS(SK_U, remote); return {ok:true, data:remote}; }
      return {ok:true, data: loadS(SK_U)};
    }
    if(action==='addUser'){
      const arr = loadS(SK_U);
      if(arr.find(u=>u.username===body.username)) return {ok:false, error:'El usuario ya existe'};
      arr.push(body);
      saveS(SK_U, arr);
      await tgSave('USERS', arr);
      return {ok:true};
    }
    if(action==='deleteUser'){
      const arr = loadS(SK_U).filter(u=>u.username!==body.username);
      saveS(SK_U, arr);
      await tgSave('USERS', arr);
      return {ok:true};
    }
    return {ok:false, error:'Acción desconocida'};
  }catch(e){
    return {ok:false, error:e.message};
  }
}

/* ── UTILS ── */
const ADM_U='admin', ADM_P='admin123';
let CU=null, SALES_CACHE=[], USERS_CACHE=[];
function esc(s){return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}
function fmt(ts){if(!ts)return '—';const d=new Date(ts);return d.toLocaleDateString('es-MX',{day:'2-digit',month:'short',year:'numeric'})+' '+d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});}
function fmtDate(s){if(!s)return '—';const[y,m,d]=s.split('-');const M=['Ene','Feb','Mar','Abr','May','Jun','Jul','Ago','Sep','Oct','Nov','Dic'];return `${parseInt(d)} ${M[parseInt(m)-1]} ${y}`;}
function ini(n){return n.trim().split(/\s+/).slice(0,2).map(w=>w[0]||'').join('').toUpperCase()||'?';}
function genFolio(){return 'BNX-'+String(Date.now()).slice(-6);}
function spin(on){document.getElementById('spinner').classList.toggle('show',on);}
function showToast(id,msg,type){const el=document.getElementById(id);if(!el)return;el.textContent=msg;el.className='toast '+type+' show';clearTimeout(el._t);el._t=setTimeout(()=>el.classList.remove('show'),4000);}

/* ── AUTH ── */
async function doLogin(){
  const u=(document.getElementById('l-user').value||'').trim().toLowerCase();
  const p=document.getElementById('l-pass').value;
  const errEl=document.getElementById('login-err');
  errEl.classList.remove('show');
  if(!u||!p){errEl.textContent='Escribe usuario y contraseña';errEl.classList.add('show');return;}
  if(u===ADM_U&&p===ADM_P){CU={username:ADM_U,name:'Administrador',role:'admin'};await bootApp();return;}
  spin(true);
  const r=await api('getUsers');
  spin(false);
  if(!r.ok){errEl.textContent='Error de conexión: '+r.error;errEl.classList.add('show');return;}
  USERS_CACHE=r.data||[];
  const found=USERS_CACHE.find(x=>x.username.toLowerCase()===u&&x.password===p);
  if(found){CU={username:found.username,name:found.name,role:'exec'};await bootApp();return;}
  errEl.textContent='Usuario o contraseña incorrectos';
  errEl.classList.add('show');
}

function doLogout(){
  CU=null;SALES_CACHE=[];
  document.getElementById('app').style.display='none';
  document.getElementById('login-screen').style.display='flex';
  document.getElementById('l-user').value='';
  document.getElementById('l-pass').value='';
}

async function bootApp(){
  document.getElementById('login-screen').style.display='none';
  document.getElementById('app').style.display='block';
  document.getElementById('nav-name').textContent=CU.name;
  buildNav();
  buildBenPanels();
  if(CU.role==='admin') await goPage('dash');
  else goPage('exec');
}

function buildNav(){
  const tabs=document.getElementById('n-tabs');
  if(CU.role==='admin'){
    tabs.innerHTML='<button class="tab gold" data-pg="dash">Dashboard</button><button class="tab gold" data-pg="ben">Beneficios</button><button class="tab gold" data-pg="users">Usuarios</button>';
  } else {
    tabs.innerHTML='<button class="tab" data-pg="exec">Registrar venta</button><button class="tab" data-pg="ben">Beneficios</button>';
  }
  document.querySelectorAll('.tab').forEach(btn=>btn.addEventListener('click',()=>goPage(btn.dataset.pg)));
}

async function goPage(p){
  document.querySelectorAll('.pg').forEach(el=>el.classList.remove('on'));
  document.querySelectorAll('.tab').forEach(el=>el.classList.remove('on'));
  document.getElementById('pg-'+p).classList.add('on');
  const tb=document.querySelector(`.tab[data-pg="${p}"]`);
  if(tb)tb.classList.add('on');
  if(p==='exec'){setTodayDate();refreshFolio();renderRecent();}
  if(p==='dash')await loadAndRenderDash();
  if(p==='users')await loadAndRenderUsers();
}

/* ── EJECUTIVO ── */
function setTodayDate(){const el=document.getElementById('f-fecha');if(el&&!el.value)el.value=new Date().toISOString().slice(0,10);}
function refreshFolio(){const el=document.getElementById('folio-pill');if(el)el.textContent=genFolio();}

async function registrarVenta(){
  const cliente=(document.getElementById('f-cliente').value||'').trim();
  const tel=(document.getElementById('f-tel').value||'').trim();
  const tarjeta=document.getElementById('f-tarjeta').value;
  const fecha=document.getElementById('f-fecha').value;
  let folio=(document.getElementById('f-folio').value||'').trim();
  if(!cliente){showToast('t-err','Escribe el nombre del cliente','err');return;}
  if(!tarjeta){showToast('t-err','Selecciona el tipo de tarjeta','err');return;}
  if(!fecha){showToast('t-err','Selecciona la fecha de venta','err');return;}
  if(!folio)folio=genFolio();
  document.getElementById('reg-btn').disabled=true;
  spin(true);
  const r=await api('addSale',{folio,exec:CU.name,username:CU.username,cliente,tel,tarjeta,fecha,registrado:new Date().toISOString()});
  spin(false);
  document.getElementById('reg-btn').disabled=false;
  if(!r.ok){showToast('t-err','Error al guardar: '+r.error,'err');return;}
  document.getElementById('f-cliente').value='';
  document.getElementById('f-tel').value='';
  document.getElementById('f-tarjeta').value='';
  document.getElementById('f-folio').value='';
  document.getElementById('f-fecha').value=new Date().toISOString().slice(0,10);
  refreshFolio();
  showToast('t-ok','✓ Venta guardada — Folio '+folio,'ok');
  renderRecent();
}

function renderRecent(){
  const list=document.getElementById('exec-recent');
  const data=loadS(SK_S).filter(v=>v.username===CU.username).slice(0,6);
  if(!data.length){list.innerHTML='<p style="color:var(--mu);font-size:13px">Aún no tienes ventas registradas.</p>';return;}
  list.innerHTML=data.map(v=>`<div class="ri"><div style="flex:1;min-width:0"><div class="ri-n">${esc(v.cliente)}</div><div class="ri-m">${esc(v.tarjeta)}${v.tel?' · '+esc(v.tel):''} · ${fmtDate(v.fecha)}</div></div><span class="ri-f">${esc(v.folio)}</span></div>`).join('');
}

/* ── DASHBOARD ── */
function setSyncStatus(s,msg){
  const dot=document.getElementById('sync-dot');
  const txt=document.getElementById('sync-txt');
  if(!dot)return;
  dot.className='sync-dot '+s;
  txt.textContent=msg;
}

async function loadAndRenderDash(){
  setSyncStatus('loading','Cargando datos…');
  const r=await api('getSales');
  if(!r.ok){setSyncStatus('err','Error: '+r.error);return;}
  SALES_CACHE=r.data||[];
  setSyncStatus('ok','Sincronizado · '+SALES_CACHE.length+' ventas');
  renderDashTable();
}

function renderDashTable(){
  const search=(document.getElementById('d-search').value||'').toLowerCase();
  const ft=document.getElementById('d-filt').value;
  const all=SALES_CACHE;
  let data=all.slice();
  if(search)data=data.filter(v=>(v.exec||'').toLowerCase().includes(search)||(v.cliente||'').toLowerCase().includes(search)||(v.folio||'').toLowerCase().includes(search)||(v.tel||'').includes(search));
  if(ft)data=data.filter(v=>v.tarjeta===ft);
  document.getElementById('s-tot').textContent=all.length;
  document.getElementById('s-exe').textContent=new Set(all.map(v=>v.username)).size;
  const today=new Date().toDateString();
  document.getElementById('s-hoy').textContent=all.filter(v=>v.registrado&&new Date(v.registrado).toDateString()===today).length;
  const weekAgo=Date.now()-7*86400000;
  document.getElementById('s-sem').textContent=all.filter(v=>v.registrado&&new Date(v.registrado).getTime()>weekAgo).length;
  const tbody=document.getElementById('t-body');
  const empty=document.getElementById('t-empty');
  if(!data.length){tbody.innerHTML='';empty.style.display='block';}
  else{
    empty.style.display='none';
    tbody.innerHTML=data.map(v=>`<tr><td class="tdf">${esc(v.folio)}</td><td class="tdb">${esc(v.exec)}</td><td>${esc(v.cliente)}</td><td class="tdm">${esc(v.tel||'—')}</td><td><span class="badge b-r">${esc(v.tarjeta)}</span></td><td class="tdm">${fmtDate(v.fecha)}</td><td class="tdm">${fmt(v.registrado)}</td><td><button class="delbtn" data-folio="${esc(v.folio)}">✕</button></td></tr>`).join('');
  }
  const counts={};
  all.forEach(v=>{counts[v.exec]=(counts[v.exec]||0)+1;});
  const sorted=Object.entries(counts).sort((a,b)=>b[1]-a[1]).slice(0,12);
  const pc=['rp1','rp2','rp3'];
  document.getElementById('rank-grid').innerHTML=sorted.length
    ?sorted.map(([name,cnt],i)=>`<div class="rcard"><div class="rpos ${pc[i]||''}">${i+1}</div><div><div class="rkn">${esc(name)}</div><div class="rkc">${cnt} venta${cnt!==1?'s':''}</div></div></div>`).join('')
    :'<p style="color:var(--mu);font-size:13px">Sin datos aún.</p>';
}

async function delSale(folio){
  if(!confirm('¿Eliminar la venta con folio '+folio+'?'))return;
  spin(true);const r=await api('deleteSale',{folio});spin(false);
  if(!r.ok){alert('Error: '+r.error);return;}
  SALES_CACHE=SALES_CACHE.filter(v=>v.folio!==folio);
  renderDashTable();
  setSyncStatus('ok','Sincronizado · '+SALES_CACHE.length+' ventas');
}

/* ── USUARIOS ── */
async function loadAndRenderUsers(){
  spin(true);const r=await api('getUsers');spin(false);
  if(!r.ok){showToast('u-err','Error al cargar usuarios','err');return;}
  USERS_CACHE=r.data||[];
  renderUsersUI();
}

function renderUsersUI(){
  const adminCard=`<div class="ucard"><div class="uav av-a">AD</div><div class="ui"><div class="un">Administrador</div><div class="ur"><span class="badge b-g">admin</span></div></div></div>`;
  document.getElementById('ugrid').innerHTML=adminCard+(USERS_CACHE.length
    ?USERS_CACHE.map(u=>`<div class="ucard"><div class="uav av-e">${ini(u.name)}</div><div class="ui"><div class="un">${esc(u.name)}</div><div class="ur"><span class="badge b-b">@${esc(u.username)}</span></div></div><button class="del-u" data-uname="${esc(u.username)}">Eliminar</button></div>`).join('')
    :'<p style="color:var(--mu);font-size:13px;margin-top:4px">No hay ejecutivos agregados aún.</p>');
}

async function addUser(){
  const name=(document.getElementById('nu-name').value||'').trim();
  const username=(document.getElementById('nu-user').value||'').trim().toLowerCase().replace(/\s+/g,'');
  const password=document.getElementById('nu-pass').value;
  if(!name||!username||!password){showToast('u-err','Completa todos los campos','err');return;}
  if(password.length<4){showToast('u-err','Contraseña mínimo 4 caracteres','err');return;}
  if(username===ADM_U){showToast('u-err','Ese usuario está reservado','err');return;}
  document.getElementById('add-user-btn').disabled=true;
  spin(true);const r=await api('addUser',{name,username,password});spin(false);
  document.getElementById('add-user-btn').disabled=false;
  if(!r.ok){showToast('u-err',r.error||'Error al agregar','err');return;}
  document.getElementById('nu-name').value='';
  document.getElementById('nu-user').value='';
  document.getElementById('nu-pass').value='';
  showToast('u-ok','Ejecutivo "'+name+'" agregado','ok');
  await loadAndRenderUsers();
}

/* ── BENEFICIOS ── */
const CARDS=[
  {id:'joy',name:'Joy Banamex',meta:{Ingresos:'$15,000',LDC:'$15,000',CAT:'83.5% sin IVA',Tasa:'62.75% anual',Anualidad:'Sin comisión de por vida'},beneficios:['Sin comisión de administración de por vida con compra mínima de $300 al mes.','Descuentos y promociones todo el año en negocios participantes.','Puedes elegir tu fecha de corte una vez al año.','Sin CVV impreso para mayor seguridad en compras en línea.','Preventas exclusivas para eventos culturales, deportivos y espectáculos.','Mastercard Global Service: reposición en 48 hrs en caso de pérdida.']},
  {id:'clasica',name:'Clásica Banamex',meta:{Ingresos:'$15,000',LDC:'$15,000',CAT:'88.7% sin IVA',Tasa:'62.63% anual',Anualidad:'$815 sin IVA',Adicional:'$405 sin IVA'},beneficios:['Primera anualidad bonificada con una compra antes del primer corte (bonificación a 90 días).','5% en Puntos Premia por todas tus compras. Úsalos como efectivo en cajeros Citibanamex.','Puntos Dobles al cargar gasolina todos los días (topado a 1,000 puntos/semana).','3, 6 o 12 Pagos Fijos en Salud y Belleza. Monto mínimo $3,000 al 55 2226 3639.','Preventas exclusivas para eventos culturales, deportivos y espectáculos.','Cambia tu fecha de corte una vez al año.']},
  {id:'teleton',name:'Teleton Banamex',meta:{Ingresos:'$15,000',LDC:'$15,000',CAT:'87.0% sin IVA',Tasa:'62.47% anual',Anualidad:'$540 sin IVA',Adicional:'Sin costo'},beneficios:['Primera anualidad bonificada con una compra antes del primer corte.','Anualidad más baja del mercado en su segmento.','6 tarjetas adicionales sin costo.','Preventas exclusivas para los mejores eventos de México.','Cada uso apoya al Teletón y causa social.']},
  {id:'oro',name:'Oro Banamex',meta:{Ingresos:'$25,000',LDC:'$25,000',CAT:'85.7% sin IVA',Tasa:'60.58% anual',Anualidad:'$1,230 sin IVA',Adicional:'$620 sin IVA'},beneficios:['Primera anualidad bonificada con una compra antes del primer corte.','7% en Puntos Premia por todas tus compras.','Puntos Premia al doble al consumir gasolina (topado a 1,000 pts/semana).','3 MSI en viajes, salud y belleza. Monto mínimo $3,000.','MSI en negocios participantes: viajes, tecnología, ropa y más.','Seguro de Accidente en Viajes: hasta $400 USD por robo o daño accidental.','Master Seguro de Viajes: hasta $250,000 USD para ti y tu familia.','Seguro por facturación fraudulenta: cubre hasta el saldo de la cuenta.','Preventas exclusivas para eventos culturales, deportivos y espectáculos.']},
  {id:'descubre',name:'Descubre Banamex',meta:{Ingresos:'$25,000',LDC:'$25,000',CAT:'86.0% sin IVA',Tasa:'60.65% anual',Anualidad:'$1,230 sin IVA',Adicional:'$620 sin IVA'},beneficios:['Primera anualidad bonificada con una compra antes del primer corte.','1 Punto Momento Banamex por cada dólar gastado en todas tus compras.','2x1 en boletos de avión a playas nacionales: bienvenida (600 pts en 3 meses) o aniversario (4,500 pts). Destinos: Acapulco, La Paz, Puerto Vallarta, Huatulco, Cozumel, Cancún, Los Cabos, Veracruz, Mazatlán, Zihuatanejo.','Mastercard Concierge 24/7: asistente personal en todo el mundo.','Elite Valet AICM: 50% descuento, hasta 5 días, 2 entradas por mes.','Dining Program: 20% descuento en restaurantes seleccionados + bebida de cortesía.','Preventas exclusivas para los mejores eventos de México.']},
  {id:'platinum',name:'Platinum Banamex',meta:{Ingresos:'$75,000',LDC:'$50,000',CAT:'40.7% sin IVA',Tasa:'32.02% anual',Anualidad:'$2,725 sin IVA',Adicional:'$1,360 sin IVA'},beneficios:['Primera anualidad bonificada con una compra antes del primer corte.','10% en Puntos Premia por todas tus compras.','LIBRA Premium gratis: Asistencia Vial, Legal, Gestoría, en el Hogar y Médica.','10 accesos GRATIS a Salas Beyond (tú + 1 acompañante) + 4 accesos a 800+ salas VIP Mastercard al año.','Mastercard Concierge 24/7 en todo el mundo.','Dining Program: 20% descuento en restaurantes seleccionados + bebida de cortesía.','Elite Valet AICM: 50% descuento, hasta 5 días, 2 entradas por mes.','MSI en negocios participantes.','Preventas exclusivas para eventos culturales, deportivos y espectáculos.']},
  {id:'explora',name:'Explora Banamex',meta:{Ingresos:'$75,000',LDC:'$50,000',CAT:'81.2% sin IVA',Tasa:'58.19% anual',Anualidad:'$2,725 sin IVA',Adicional:'$1,360 sin IVA'},beneficios:['Primera anualidad bonificada con una compra antes del primer corte.','1.15 Puntos Momentos Banamex por cada dólar gastado. Tarjetas adicionales también generan puntos.','2x1 en boletos de avión: bienvenida (1,300 pts en 3 meses) o aniversario (10,000 Puntos Explora).','10 accesos GRATIS a Salas Beyond (tú + 1 acompañante) + 4 accesos a 800+ salas VIP Mastercard al año.','Mastercard Concierge 24/7 en todo el mundo.','Elite Valet AICM: 50% descuento, hasta 5 días, 2 entradas por mes.','Seguros Mastercard completos: viaje, equipaje, autos y más.']}
];

function buildBenPanels(){
  const tabsEl=document.getElementById('ben-tabs');
  const panelsEl=document.getElementById('ben-panels');
  tabsEl.innerHTML=CARDS.map((c,i)=>`<button class="btab${i===0?' on':''}" data-bid="${c.id}">${c.name}</button>`).join('');
  panelsEl.innerHTML=CARDS.map((c,i)=>`<div class="ben-panel${i===0?' on':''}" id="ben-${c.id}"><div class="ben-hero"><div class="ben-name">${c.name}</div><div class="ben-meta">${Object.entries(c.meta).map(([k,v])=>`<div class="bm"><div class="bm-l">${k}</div><div class="bm-v ${k==='Tasa'||k==='CAT'?'red':'green'}">${v}</div></div>`).join('')}</div><ul class="ben-list">${c.beneficios.map((b,i)=>`<li><span class="ben-bullet">${i+1}</span><span>${b}</span></li>`).join('')}</ul></div></div>`).join('');
  tabsEl.querySelectorAll('.btab').forEach(btn=>{
    btn.addEventListener('click',()=>{
      tabsEl.querySelectorAll('.btab').forEach(b=>b.classList.remove('on'));
      panelsEl.querySelectorAll('.ben-panel').forEach(p=>p.classList.remove('on'));
      btn.classList.add('on');
      document.getElementById('ben-'+btn.dataset.bid).classList.add('on');
    });
  });
}

/* ── EVENT DELEGATION ── */
document.addEventListener('click',async function(e){
  if(e.target.id==='login-btn'){doLogin();return;}
  if(e.target.id==='logout-btn'){doLogout();return;}
  if(e.target.id==='reg-btn'){registrarVenta();return;}
  if(e.target.id==='refresh-btn'){await loadAndRenderDash();return;}
  if(e.target.id==='add-user-btn'){addUser();return;}
  if(e.target.classList.contains('delbtn')&&e.target.dataset.folio){delSale(e.target.dataset.folio);return;}
  if(e.target.classList.contains('del-u')&&e.target.dataset.uname){
    if(!confirm('¿Eliminar al ejecutivo @'+e.target.dataset.uname+'?'))return;
    spin(true);const r=await api('deleteUser',{username:e.target.dataset.uname});spin(false);
    if(!r.ok){alert('Error: '+r.error);return;}
    await loadAndRenderUsers();return;
  }
  if(e.target.id==='export-btn'){
    if(!SALES_CACHE.length){alert('No hay ventas para exportar.');return;}
    const csv=['Folio,Ejecutivo,Cliente,Teléfono,Tarjeta,Fecha Venta,Registrado',
      ...SALES_CACHE.map(v=>`"${v.folio}","${v.exec}","${v.cliente}","${v.tel||''}","${v.tarjeta}","${fmtDate(v.fecha)}","${fmt(v.registrado)}"`)
    ].join('\n');
    const blob=new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'});
    const url=URL.createObjectURL(blob);
    const a=document.createElement('a');a.href=url;
    a.download='ventas_banamex_'+new Date().toISOString().slice(0,10)+'.csv';
    a.click();URL.revokeObjectURL(url);return;
  }
  if(e.target.id==='clear-btn'){
    if(!confirm('¿Borrar TODAS las ventas? No se puede deshacer.'))return;
    spin(true);const r=await api('clearSales');spin(false);
    if(!r.ok){alert('Error: '+r.error);return;}
    SALES_CACHE=[];renderDashTable();
    setSyncStatus('ok','Sincronizado · 0 ventas');return;
  }
});
document.addEventListener('keydown',function(e){
  if(e.key==='Enter'&&document.getElementById('login-screen').style.display!=='none')doLogin();
});
document.addEventListener('input',function(e){
  if(e.target.id==='d-search'||e.target.id==='d-filt')renderDashTable();
});

/* ── ARRANQUE ── */
document.getElementById('login-screen').style.display='flex';
</script>
</body>
</html>
