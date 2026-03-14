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

/* ─── TARJETAS VISUALES ─── */
.cards-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(285px,1fr));gap:1.1rem;margin-bottom:1.5rem;}
.tc{border-radius:20px;padding:1.5rem 1.6rem;position:relative;overflow:hidden;cursor:pointer;
  transition:transform .22s,box-shadow .22s;min-height:185px;
  display:flex;flex-direction:column;justify-content:space-between;
  box-shadow:0 6px 28px rgba(0,0,0,.55);}
.tc::before{content:'';position:absolute;inset:0;
  background:radial-gradient(circle at 80% -10%,rgba(255,255,255,.09) 0%,transparent 55%),
             radial-gradient(circle at 10% 110%,rgba(255,255,255,.06) 0%,transparent 50%);
  pointer-events:none;}
.tc:hover{transform:translateY(-6px);box-shadow:0 22px 56px rgba(0,0,0,.7);}
.tc.sel{outline:3px solid rgba(255,255,255,.85);outline-offset:3px;}
.tc-joy    {background:linear-gradient(135deg,#C8102E 0%,#6d0518 100%);}
.tc-clasica{background:linear-gradient(135deg,#0f2550 0%,#1a3f8a 100%);}
.tc-teleton{background:linear-gradient(135deg,#5b0f9c 0%,#8b2edb 100%);}
.tc-oro    {background:linear-gradient(135deg,#5c3500 0%,#a0720a 60%,#c9a227 100%);}
.tc-descubre{background:linear-gradient(135deg,#014421 0%,#147a3c 100%);}
.tc-platinum{background:linear-gradient(135deg,#1a1a1a 0%,#4a4a4a 100%);}
.tc-explora{background:linear-gradient(135deg,#0a1f6e 0%,#1c4fd8 100%);}
.tc-chip{width:38px;height:27px;border-radius:5px;
  background:linear-gradient(135deg,#a87010,#e8c542,#a87010);
  box-shadow:0 1px 5px rgba(0,0,0,.45);margin-bottom:.9rem;position:relative;}
.tc-chip::after{content:'';position:absolute;top:50%;left:0;right:0;height:1px;background:rgba(0,0,0,.2);}
.tc-num{font-family:'Courier New',monospace;font-size:13.5px;letter-spacing:.22em;
  color:rgba(255,255,255,.82);margin-bottom:.4rem;}
.tc-cname{font-size:9.5px;color:rgba(255,255,255,.5);text-transform:uppercase;letter-spacing:.12em;margin-bottom:2px;}
.tc-tit{font-size:13.5px;color:#fff;font-weight:600;}
.tc-logo{position:absolute;top:1.1rem;right:1.2rem;font-family:'Bebas Neue',sans-serif;
  font-size:.95rem;color:rgba(255,255,255,.9);letter-spacing:.07em;}
.tc-badge{position:absolute;top:1.1rem;left:1.2rem;background:rgba(0,0,0,.38);
  backdrop-filter:blur(8px);border:1px solid rgba(255,255,255,.22);
  border-radius:20px;padding:3px 10px;font-size:10px;font-weight:600;color:#fff;white-space:nowrap;}
.tc-mc{position:absolute;bottom:1.1rem;right:1.2rem;display:flex;}
.tc-mc .r{width:22px;height:22px;border-radius:50%;background:#eb001b;opacity:.9;}
.tc-mc .y{width:22px;height:22px;border-radius:50%;background:#f79e1b;opacity:.9;margin-left:-9px;}
/* detail */
.card-detail{background:var(--s1);border:1px solid var(--br2);border-radius:18px;
  padding:1.75rem;margin-top:1.2rem;animation:slideUp .2s ease;}
@keyframes slideUp{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:none}}
.cd-top{display:flex;gap:1rem;align-items:flex-start;flex-wrap:wrap;margin-bottom:1.4rem;}
.cd-mini{border-radius:14px;padding:1rem 1.1rem;width:175px;min-height:105px;flex-shrink:0;
  display:flex;flex-direction:column;justify-content:space-between;}
.cd-tb{flex:1;min-width:0;}
.cd-title{font-family:'Bebas Neue',sans-serif;font-size:1.65rem;letter-spacing:.03em;line-height:1;}
.cd-pts{font-size:12px;color:var(--mu);margin-top:.3rem;}
.cd-close{background:var(--s2);border:1px solid var(--br2);border-radius:8px;
  padding:6px 14px;font-family:'Outfit',sans-serif;font-size:12px;color:var(--mu);cursor:pointer;}
.cd-close:hover{color:var(--tx);}
.cd-nums{display:grid;grid-template-columns:repeat(auto-fill,minmax(128px,1fr));gap:7px;margin-bottom:1.2rem;}
.cd-n{background:var(--s2);border-radius:10px;padding:10px 12px;}
.cd-nl{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;font-weight:500;}
.cd-nv{font-size:14px;font-weight:600;margin-top:3px;}
.nv-r{color:#f77;}.nv-g{color:var(--green);}.nv-o{color:var(--gold-l);}
.cd-sec{font-size:10.5px;font-weight:600;color:var(--mu);text-transform:uppercase;
  letter-spacing:.09em;margin:1.1rem 0 .55rem;}
.cd-bens{list-style:none;display:flex;flex-direction:column;gap:6px;}
.cd-bens li{display:flex;gap:10px;align-items:flex-start;font-size:13px;line-height:1.55;
  color:#ccc;background:var(--s2);border-radius:8px;padding:9px 12px;}
.cd-ico{font-size:15px;flex-shrink:0;margin-top:1px;}
.cd-bt{font-weight:600;color:var(--tx);display:block;margin-bottom:2px;}
.cd-reqs{display:grid;grid-template-columns:repeat(auto-fill,minmax(205px,1fr));gap:6px;}
.cd-req{background:var(--s2);border-radius:8px;padding:8px 12px;font-size:12px;color:#ccc;
  display:flex;gap:8px;align-items:flex-start;}
.cd-nota{margin-top:1rem;background:rgba(200,168,75,.1);border:1px solid rgba(200,168,75,.22);
  border-radius:8px;padding:10px 14px;font-size:11px;color:#bbb;line-height:1.65;}

/* ─── ESTADOS DE VENTA ─── */
.st{display:inline-flex;align-items:center;gap:4px;padding:4px 10px;border-radius:20px;
  font-size:11px;font-weight:600;cursor:pointer;border:1px solid transparent;
  transition:opacity .15s;white-space:nowrap;user-select:none;}
.st:hover{opacity:.75;}
.st-nueva {background:rgba(100,116,139,.15);border-color:rgba(100,116,139,.4);color:#94a3b8;}
.st-pend  {background:rgba(251,191,36,.13);border-color:rgba(251,191,36,.45);color:#fbbf24;}
.st-decl  {background:rgba(239,68,68,.13);border-color:rgba(239,68,68,.45);color:#f87171;}
.st-pre   {background:rgba(168,85,247,.13);border-color:rgba(168,85,247,.45);color:#c084fc;}
.st-ok    {background:rgba(34,197,94,.11);border-color:rgba(34,197,94,.35);color:var(--green);}

/* ─── OVERLAY + MODALES ─── */
.ov{position:fixed;inset:0;background:rgba(0,0,0,.8);display:none;
  align-items:center;justify-content:center;z-index:9000;padding:1rem;}
.ov.show{display:flex;}
/* modal de estado */
.stmod{background:var(--s1);border:1px solid var(--br2);border-radius:20px;
  padding:1.75rem;max-width:430px;width:100%;box-shadow:0 24px 80px rgba(0,0,0,.7);}
.stmod h3{font-family:'Bebas Neue',sans-serif;font-size:1.5rem;letter-spacing:.03em;margin-bottom:.25rem;}
.stmod-cl{font-size:13px;color:var(--mu);margin-bottom:1.25rem;line-height:1.5;}
.sm-opts{display:flex;flex-direction:column;gap:7px;margin-bottom:1.2rem;}
.sm-opt{display:flex;align-items:center;gap:11px;background:var(--s2);
  border:2px solid var(--br2);border-radius:11px;padding:11px 14px;cursor:pointer;
  transition:border-color .15s;}
.sm-opt.chosen{border-color:var(--gold);}
.sm-opt input[type=radio]{accent-color:var(--gold);width:16px;height:16px;flex-shrink:0;}
.sm-ol{font-size:13px;font-weight:500;}
.sm-os{font-size:11px;color:var(--mu);margin-top:2px;}
.sm-nota{margin-bottom:1.1rem;}
.sm-nota label{font-size:11px;font-weight:500;color:var(--mu);text-transform:uppercase;
  letter-spacing:.06em;display:block;margin-bottom:6px;}
.sm-nota textarea{width:100%;background:var(--s2);border:1px solid var(--br2);
  border-radius:9px;padding:10px 13px;color:var(--tx);font-family:'Outfit',sans-serif;
  font-size:13px;resize:vertical;min-height:78px;outline:none;}
.sm-nota textarea:focus{border-color:var(--gold);}
.sm-btns{display:flex;gap:8px;justify-content:flex-end;}
.sm-save{padding:10px 22px;background:var(--red);border:none;border-radius:9px;color:#fff;
  font-family:'Outfit',sans-serif;font-size:14px;font-weight:600;cursor:pointer;}
.sm-save:hover{background:var(--red-d);}
.sm-cancel{padding:10px 18px;background:transparent;border:1px solid var(--br2);
  border-radius:9px;color:var(--mu);font-family:'Outfit',sans-serif;font-size:13px;cursor:pointer;}
.sm-cancel:hover{color:var(--tx);}
/* popup de razón */
.rpop{background:var(--s1);border:1px solid var(--br2);border-radius:18px;
  padding:1.6rem;max-width:390px;width:100%;box-shadow:0 20px 70px rgba(0,0,0,.7);}
.rpop h4{font-family:'Bebas Neue',sans-serif;font-size:1.3rem;letter-spacing:.03em;margin-bottom:.9rem;}
.rpop-body{background:var(--s2);border-radius:10px;padding:14px 16px;font-size:13.5px;
  line-height:1.7;color:#d0d0d0;white-space:pre-wrap;word-break:break-word;}
.rpop-btns{margin-top:1.1rem;display:flex;gap:8px;justify-content:flex-end;}

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
            <th>Tarjeta</th><th>Fecha venta</th><th>Estado</th><th></th>
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
/* ── ALMACENAMIENTO LOCAL ── */
const SK_S = 'bnx_sales_v6';
const SK_U = 'bnx_users_v6';

function loadS(k){ try{ return JSON.parse(localStorage.getItem(k))||[]; }catch{ return []; } }
function saveS(k,d){ localStorage.setItem(k, JSON.stringify(d)); }

/* ── API (solo localStorage, sin APIs externas) ── */
async function api(action, body={}){
  try{
    if(action==='getSales'){
      return {ok:true, data: loadS(SK_S)};
    }
    if(action==='addSale'){
      const arr = loadS(SK_S);
      arr.unshift(body);
      saveS(SK_S, arr);
      return {ok:true};
    }
    if(action==='deleteSale'){
      const arr = loadS(SK_S).filter(v=>v.folio!==body.folio);
      saveS(SK_S, arr);
      return {ok:true};
    }
    if(action==='clearSales'){
      saveS(SK_S, []);
      return {ok:true};
    }
    if(action==='getUsers'){
      return {ok:true, data: loadS(SK_U)};
    }
    if(action==='addUser'){
      const arr = loadS(SK_U);
      if(arr.find(u=>u.username===body.username)) return {ok:false, error:'El usuario ya existe'};
      arr.push(body);
      saveS(SK_U, arr);
      return {ok:true};
    }
    if(action==='deleteUser'){
      const arr = loadS(SK_U).filter(u=>u.username!==body.username);
      saveS(SK_U, arr);
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
  const ST_MAP2={nueva:'st-nueva',pendiente:'st-pend',declino:'st-decl',preasignado:'st-pre',vendida:'st-ok'};
  const ST_LBL2={nueva:'🆕 Nueva',pendiente:'📞 Pendiente',declino:'❌ Declinó',preasignado:'⭐ Preasignado',vendida:'✅ Vendida'};
  list.innerHTML=data.map(v=>{
    const sc=ST_MAP2[v.status||'nueva']||'st-nueva';
    const sl=ST_LBL2[v.status||'nueva']||'🆕 Nueva';
    const nt=esc(v.statusNota||'');
    return `<div class="ri">
      <div style="flex:1;min-width:0">
        <div class="ri-n">${esc(v.cliente)}</div>
        <div class="ri-m">${esc(v.tarjeta)}${v.tel?' · '+esc(v.tel):''} · ${fmtDate(v.fecha)}</div>
      </div>
      <span class="st ${sc}" data-folio="${esc(v.folio)}" data-nota="${nt}" style="margin-left:8px">${sl}</span>
    </div>`;
  }).join('');
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
    tbody.innerHTML=data.map(v=>{
    const ST_MAP={nueva:['st-nueva','🆕 Nueva'],pendiente:['st-pend','📞 Pendiente'],declino:['st-decl','❌ Declinó'],preasignado:['st-pre','⭐ Preasignado'],vendida:['st-ok','✅ Vendida']};
    const [sc,sl]=ST_MAP[v.status||'nueva']||ST_MAP.nueva;
    const nt=esc(v.statusNota||'');
    return `<tr>
      <td class="tdf">${esc(v.folio)}</td>
      <td class="tdb">${esc(v.exec)}</td>
      <td>${esc(v.cliente)}</td>
      <td class="tdm">${esc(v.tel||'—')}</td>
      <td><span class="badge b-r">${esc(v.tarjeta)}</span></td>
      <td class="tdm">${fmtDate(v.fecha)}</td>
      <td><span class="st ${sc}" data-folio="${esc(v.folio)}" data-nota="${nt}">${sl}</span></td>
      <td><button class="delbtn" data-folio="${esc(v.folio)}">✕</button></td>
    </tr>`;
  }).join('');
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

/* ═══ BENEFICIOS ═══ */
const CARDS=[
  {id:'joy',color:'tc-joy',name:'Joy Banamex',badge:'Sin anualidad',num:'•••• •••• •••• 1234',
   cat:'~84%',tasa:'~63.69% anual',anual:'Sin comisión*',ing:'$7,000',ldc:'Desde $15,000',adic:'—',
   pts:'No genera Puntos Premia',
   bens:[
     {i:'🚫',t:'Sin anualidad de por vida',d:'Sin comisión siempre que realices al menos $300 en compras al mes. Si no compras, penalización de $149 sin IVA.'},
     {i:'🔐',t:'CVV Digital dinámico',d:'Sin CVV impreso en el plástico. Tu número de seguridad cambia en cada compra desde la App Banamex.'},
     {i:'🎬',t:'2x1 en Cinépolis',d:'En salas tradicionales comprando en cinepolis.com o la app. Vigente hasta 31 ago 2026.'},
     {i:'☕',t:'Bonificación Starbucks',d:'$45 de ahorro en tu próximo consumo al recargar $150 en la app Starbucks Rewards los domingos.'},
     {i:'📅',t:'Elige tu fecha de corte',d:'Cambia tu fecha de corte una vez al año llamando al 55 1226 2639 (24 hrs, 365 días).'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Boletos antes que nadie para los mejores eventos culturales, deportivos y espectáculos.'},
     {i:'🆘',t:'Mastercard Global Service',d:'Reposición de tarjeta en 48 hrs por robo o extravío en cualquier parte del mundo.'},
   ],
   reqs:['IFE/INE vigente o tarjeta de residente + pasaporte','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $7,000 MXN'],
   nota:'*Realiza al menos $300 en compras al mes para evitar penalización de $149 sin IVA por inactividad.'
  },
  {id:'clasica',color:'tc-clasica',name:'Clásica Banamex',badge:'5% Puntos Premia',num:'•••• •••• •••• 2345',
   cat:'~88.7%',tasa:'~62.63% anual',anual:'$815 sin IVA',ing:'$7,000',ldc:'Desde $15,000',adic:'$405 sin IVA',
   pts:'5% Puntos Premia en todas tus compras',
   bens:[
     {i:'🎁',t:'1er año sin anualidad',d:'Realiza una compra antes del primer corte. Bonificación a los 90 días. Vigente hasta 21 may 2026.'},
     {i:'🏆',t:'Bono bienvenida 2,000 pts',d:'Al gastar $5,000 en los primeros 3 meses. Vigente hasta 21 may 2026.'},
     {i:'⭐',t:'5% Puntos Premia',d:'En todas tus compras. Úsalos como efectivo en cajeros Citibanamex o establecimientos participantes.'},
     {i:'⛽',t:'Puntos Dobles en gasolina',d:'Doble de puntos al cargar gasolina lun-dom. Tope 1,000 Puntos/semana. Hasta 21 may 2026.'},
     {i:'🏥',t:'3/6/12 Pagos fijos Salud y Belleza',d:'Hospitales, laboratorios, farmacias. Mínimo $3,000. Llamar 48 hrs después al 55 2226 3639.'},
     {i:'🎬',t:'2x1 en Cinépolis',d:'En salas tradicionales. Vigente hasta 31 ago 2026.'},
     {i:'🏥',t:'Libra One gratis 1 año',d:'Asistencias médicas, nutricionales y más sin costo el primer año.'},
   ],
   reqs:['IFE/INE vigente o tarjeta de residente + pasaporte','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $7,000 MXN'],
   nota:'Primer año sin anualidad vigente del 25 ago 2025 al 21 may 2026. Solo titulares.'
  },
  {id:'teleton',color:'tc-teleton',name:'Teletón Banamex',badge:'Causa social',num:'•••• •••• •••• 3456',
   cat:'~87.0%',tasa:'~62.47% anual',anual:'$540 sin IVA',ing:'$7,000',ldc:'Desde $15,000',adic:'Sin costo',
   pts:'No genera Puntos Premia',
   bens:[
     {i:'❤️',t:'Apoya al Teletón con cada compra',d:'Cada uso de tu tarjeta apoya a los Centros de Rehabilitación Infantil Teletón de México.'},
     {i:'💰',t:'Anualidad más baja del segmento',d:'Solo $540 sin IVA al año. Primer año bonificado con una compra. Vigente hasta 21 may 2026.'},
     {i:'👨‍👩‍👧',t:'6 tarjetas adicionales sin costo',d:'Agrega hasta 6 adicionales para tu familia sin ningún costo extra.'},
     {i:'🎬',t:'2x1 en Cinépolis',d:'En salas tradicionales de todo el país. Hasta 31 ago 2026.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra boletos antes que nadie en los mejores eventos de México.'},
     {i:'🏥',t:'Libra One gratis 1 año',d:'Asistencias médicas y más sin costo el primer año.'},
   ],
   reqs:['IFE/INE vigente o tarjeta de residente + pasaporte','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $7,000 MXN'],
   nota:'Primer año sin anualidad con una compra antes del primer corte. Vigente hasta 21 may 2026.'
  },
  {id:'oro',color:'tc-oro',name:'Oro Banamex',badge:'7% Puntos Premia',num:'•••• •••• •••• 4567',
   cat:'~85.7%',tasa:'~60.58% anual',anual:'$1,230 sin IVA',ing:'$7,000',ldc:'Desde $25,000',adic:'$620 sin IVA',
   pts:'7% Puntos Premia en todas tus compras',
   bens:[
     {i:'🎁',t:'1er año sin anualidad + bono',d:'Anualidad bonificada + 2,000 Puntos al gastar $5,000 en 3 meses. Hasta 21 may 2026.'},
     {i:'⭐',t:'7% Puntos Premia',d:'El mayor % en tarjetas básicas Banamex. Canjea como efectivo en cajeros o negocios.'},
     {i:'⛽',t:'Puntos Dobles en gasolina',d:'Doble de puntos lun-dom. Tope 1,000 pts/semana. Hasta 21 may 2026.'},
     {i:'✈️',t:'MSI en viajes, salud y mascotas',d:'3 meses sin intereses. Mínimo $3,000. Llamar al 55 2226 3639.'},
     {i:'🛡️',t:'Seguro de viajes',d:'Hasta $400 USD por robo/daño en viajes. Master Seguro hasta $250,000 USD.'},
     {i:'🔒',t:'Seguro por fraude',d:'Cobertura hasta el saldo total de la cuenta por cargos no reconocidos.'},
     {i:'🏥',t:'Libra One gratis 1 año',d:'Asistencias médicas, viales y más sin costo el primer año.'},
   ],
   reqs:['IFE/INE vigente o tarjeta de residente + pasaporte','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $7,000 MXN'],
   nota:'Bono bienvenida hasta 21 may 2026. Reflejado hasta 60 días después de cumplir los 3 meses.'
  },
  {id:'descubre',color:'tc-descubre',name:'Descubre Banamex',badge:'Puntos Momentos',num:'•••• •••• •••• 5678',
   cat:'~86.0%',tasa:'~62.31% anual',anual:'$1,230 sin IVA',ing:'$7,000',ldc:'Desde $25,000',adic:'$620 sin IVA',
   pts:'1 Punto Momento por cada $1 USD gastado',
   bens:[
     {i:'🎁',t:'1er año sin anualidad + bono',d:'Bono 2,000 Puntos al gastar $5,000 en 3 meses. Hasta 21 may 2026.'},
     {i:'🌟',t:'Puntos Momentos en todo',d:'1 Punto por cada dólar gastado. Las tarjetas adicionales también acumulan.'},
     {i:'✈️',t:'2x1 en vuelos nacionales',d:'Bienvenida: 600 pts en 3 meses. Aniversario: 4,500 pts. Cancún, Los Cabos, PVR, Acapulco, Cozumel, Huatulco, La Paz, Veracruz, Mazatlán, Zihuatanejo.'},
     {i:'🎩',t:'Mastercard Concierge 24/7',d:'Asistente personal global: restaurantes, hoteles, eventos en todo el mundo.'},
     {i:'🚗',t:'Elite Valet AICM',d:'50% de descuento en estacionamiento AICM. Hasta 5 días, 2 entradas/mes.'},
     {i:'🍽️',t:'Dining Program',d:'20% descuento en restaurantes seleccionados + bebida de cortesía.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra antes que nadie para los mejores eventos.'},
   ],
   reqs:['IFE/INE vigente o tarjeta de residente + pasaporte','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $7,000 MXN'],
   nota:'CAT calculado al 31 mar 2025, vigente al 30 sep 2025. Comisión por administración $1,230 sin IVA.'
  },
  {id:'platinum',color:'tc-platinum',name:'Platinum Banamex',badge:'Premium · VIP Lounges',num:'•••• •••• •••• 6789',
   cat:'~40.7%',tasa:'~32.02% anual',anual:'$2,725 sin IVA',ing:'$50,000',ldc:'Desde $50,000',adic:'$1,360 sin IVA',
   pts:'10% Puntos Premia — el más alto de Banamex',
   bens:[
     {i:'🎁',t:'1er año sin anualidad + bono',d:'Bono 4,000 Puntos al gastar $15,000 en 3 meses. Hasta 21 may 2026.'},
     {i:'💎',t:'10% Puntos Premia',d:'El mayor % de puntos de toda la línea. Canjea como efectivo en cajeros.'},
     {i:'📉',t:'Tasa preferencial',d:'CAT ~40.7% — la más baja de las tarjetas estándar Banamex.'},
     {i:'🛡️',t:'LIBRA Premium gratis de por vida',d:'Asistencias Vial, Legal, Gestoría, Hogar y Médica sin costo mientras tengas la tarjeta activa.'},
     {i:'✈️',t:'14 accesos VIP al año',d:'10 accesos Salones Beyond (CDMX/GDL/MTY, tú+acompañante) + 4 salas Mastercard Airport Experiences.'},
     {i:'🎩',t:'Mastercard Concierge 24/7',d:'Asistente personal en todo el mundo para reservas y coordinación especial.'},
     {i:'🍽️',t:'Dining Program',d:'20% descuento en restaurantes seleccionados + bebida de cortesía.'},
   ],
   reqs:['IFE/INE vigente o tarjeta de residente + pasaporte','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $50,000 MXN','Buen historial crediticio'],
   nota:'Bono vigente hasta 21 may 2026. Solo titulares. Tasa preferencial mejora con buen historial de pagos.'
  },
  {id:'explora',color:'tc-explora',name:'Explora Banamex',badge:'Viajero frecuente',num:'•••• •••• •••• 7890',
   cat:'~81.2%',tasa:'~60.27% anual',anual:'$2,725 sin IVA',ing:'$50,000',ldc:'Desde $50,000',adic:'$1,360 sin IVA',
   pts:'1.15 Puntos Momentos por cada $1 USD gastado',
   bens:[
     {i:'🎁',t:'1er año sin anualidad + bono',d:'Bono 4,000 Puntos al gastar $15,000 en 3 meses. Hasta 21 may 2026.'},
     {i:'🌟',t:'1.15 Puntos Momentos',d:'Por cada dólar gastado. Las adicionales también acumulan en la cuenta titular.'},
     {i:'✈️',t:'2x1 en vuelos + bono aniversario',d:'Bienvenida: 1,300 pts en 3 meses. Aniversario: 10,000 Puntos Explora para vuelos nacionales e internacionales.'},
     {i:'🛫',t:'14 accesos VIP al año',d:'10 Salones Beyond + 4 accesos 800+ salas Mastercard Airport Experiences (LoungeKey).'},
     {i:'🎩',t:'Mastercard Concierge 24/7',d:'Asistente personal global los 365 días para reservas y eventos especiales.'},
     {i:'🚗',t:'Elite Valet AICM',d:'50% descuento estacionamiento AICM. Hasta 5 días, 2 entradas/mes.'},
     {i:'🔒',t:'Master Seguro hasta $1M USD',d:'Cobertura de viaje, equipaje, autos y más. Hasta $1,000,000 USD para ti y familia.'},
   ],
   reqs:['IFE/INE vigente o tarjeta de residente + pasaporte','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $50,000 MXN','Buen historial crediticio'],
   nota:'CAT calculado al 31 mar 2025. Bono vigente hasta 21 may 2026. Solo titulares.'
  }
];

let _selCard=null;

function buildBenPanels(){
  document.getElementById('ben-tabs').style.display='none';
  document.getElementById('ben-panels').innerHTML=
    '<div class="cards-grid" id="cg"></div><div id="cd-wrap"></div>';
  _renderGrid();
}
function _renderGrid(){
  const g=document.getElementById('cg'); if(!g)return;
  g.innerHTML=CARDS.map(c=>`
    <div class="tc ${c.color}${_selCard===c.id?' sel':''}" data-cid="${c.id}">
      <div class="tc-badge">${c.badge}</div>
      <div class="tc-logo">BANAMEX</div>
      <div><div class="tc-chip"></div><div class="tc-num">${c.num}</div></div>
      <div style="display:flex;align-items:flex-end;justify-content:space-between;">
        <div><div class="tc-cname">Tarjeta de Crédito</div><div class="tc-tit">${c.name}</div></div>
        <div class="tc-mc"><span class="r"></span><span class="y"></span></div>
      </div>
    </div>`).join('');
  g.querySelectorAll('.tc').forEach(el=>el.addEventListener('click',()=>_showDetail(el.dataset.cid)));
}
function _showDetail(id){
  _selCard=id; _renderGrid();
  const c=CARDS.find(x=>x.id===id);
  const w=document.getElementById('cd-wrap');
  w.innerHTML=`
    <div class="card-detail">
      <div class="cd-top">
        <div class="tc ${c.color} cd-mini">
          <div><div class="tc-chip" style="width:28px;height:20px;margin-bottom:.5rem"></div>
          <div style="font-family:'Courier New',monospace;font-size:10px;color:rgba(255,255,255,.6);letter-spacing:.1em">${c.num}</div></div>
          <div style="font-size:11.5px;color:#fff;font-weight:600">${c.name}</div>
        </div>
        <div class="cd-tb">
          <div class="cd-title">${c.name}</div>
          <div class="cd-pts">${c.pts}</div>
        </div>
        <button class="cd-close" id="cd-close">✕ Cerrar</button>
      </div>
      <div class="cd-nums">
        <div class="cd-n"><div class="cd-nl">CAT Prom.</div><div class="cd-nv nv-r">${c.cat} sin IVA</div></div>
        <div class="cd-n"><div class="cd-nl">Tasa anual</div><div class="cd-nv nv-r">${c.tasa}</div></div>
        <div class="cd-n"><div class="cd-nl">Anualidad</div><div class="cd-nv nv-o">${c.anual}</div></div>
        <div class="cd-n"><div class="cd-nl">Ingreso mín.</div><div class="cd-nv nv-g">${c.ing}</div></div>
        <div class="cd-n"><div class="cd-nl">Línea de crédito</div><div class="cd-nv nv-g">${c.ldc}</div></div>
        <div class="cd-n"><div class="cd-nl">Adicional</div><div class="cd-nv">${c.adic}</div></div>
      </div>
      <div class="cd-sec">✨ Beneficios principales</div>
      <ul class="cd-bens">${c.bens.map(b=>`<li><span class="cd-ico">${b.i}</span><div><span class="cd-bt">${b.t}</span>${b.d}</div></li>`).join('')}</ul>
      <div class="cd-sec">📋 Requisitos</div>
      <div class="cd-reqs">${c.reqs.map(r=>`<div class="cd-req"><span style="color:var(--green);flex-shrink:0">✔</span><span>${r}</span></div>`).join('')}</div>
      <div class="cd-nota">ℹ️ ${c.nota}</div>
    </div>`;
  document.getElementById('cd-close').onclick=()=>{
    _selCard=null;_renderGrid();document.getElementById('cd-wrap').innerHTML='';
  };
  w.scrollIntoView({behavior:'smooth',block:'nearest'});
}



/* ═══ LÓGICA DE ESTADOS ═══ */
let _stFolio = null;

function openStatusModal(folio){
  const v = loadS(SK_S).find(x=>x.folio===folio);
  if(!v) return;
  _stFolio = folio;
  document.getElementById('sm-info').textContent = '👤 '+v.cliente+' · '+v.tarjeta+' · '+v.folio;
  const cur = v.status||'nueva';
  document.querySelectorAll('.sm-opt').forEach(opt=>{
    const r=opt.querySelector('input[type=radio]');
    r.checked = r.value===cur;
    opt.classList.toggle('chosen', r.value===cur);
  });
  document.getElementById('sm-nota-txt').value = v.statusNota||'';
  document.getElementById('sm-req').style.display='none';
  document.getElementById('ov-st').classList.add('show');
}

function closeStatusModal(){
  document.getElementById('ov-st').classList.remove('show');
  _stFolio=null;
}

function saveStatus(){
  const chosen = [...document.querySelectorAll('input[name="smr"]')].find(r=>r.checked)?.value||'nueva';
  const nota = (document.getElementById('sm-nota-txt').value||'').trim();
  if((chosen==='pendiente'||chosen==='declino')&&!nota){
    document.getElementById('sm-req').style.display='inline';
    document.getElementById('sm-nota-txt').focus();
    return;
  }
  const all = loadS(SK_S);
  const idx = all.findIndex(x=>x.folio===_stFolio);
  if(idx===-1){closeStatusModal();return;}
  all[idx].status = chosen;
  all[idx].statusNota = nota;
  saveS(SK_S, all);
  closeStatusModal();
  if(CU.role==='admin'){SALES_CACHE=all;renderDashTable();}
  else renderRecent();
}

function openReasonPopup(folio){
  const v = loadS(SK_S).find(x=>x.folio===folio);
  if(!v) return;
  const titles={nueva:'Estado: Nueva',pendiente:'📞 Pendiente de llamar',declino:'❌ Motivo de declinación',preasignado:'⭐ Nota preasignado',vendida:'✅ Nota de venta'};
  document.getElementById('rp-title').textContent = titles[v.status||'nueva']||'Nota';
  document.getElementById('rp-body').textContent = v.statusNota||'Sin nota registrada.';
  document.getElementById('rp-edit-btn').onclick=()=>{
    document.getElementById('ov-rp').classList.remove('show');
    openStatusModal(folio);
  };
  document.getElementById('ov-rp').classList.add('show');
}

/* ── EVENT DELEGATION ── */
document.addEventListener('click',async function(e){
  if(e.target.id==='login-btn'){doLogin();return;}
  if(e.target.id==='logout-btn'){doLogout();return;}
  if(e.target.id==='reg-btn'){registrarVenta();return;}
  if(e.target.id==='refresh-btn'){await loadAndRenderDash();return;}
  if(e.target.id==='add-user-btn'){addUser();return;}
  if(e.target.classList.contains('delbtn')&&e.target.dataset.folio){delSale(e.target.dataset.folio);return;}
  // Badge de estado → abrir popup de razón o modal de edición
  if(e.target.classList.contains('st')&&e.target.dataset.folio){
    const folio=e.target.dataset.folio;
    const nota=(e.target.dataset.nota||'').trim();
    const v=loadS(SK_S).find(x=>x.folio===folio);
    if(v&&nota&&(v.status==='pendiente'||v.status==='declino'||v.status==='preasignado')){
      openReasonPopup(folio);
    } else {
      openStatusModal(folio);
    }
    return;
  }
  if(e.target.id==='sm-cancel-btn'||e.target.id==='ov-st'){closeStatusModal();return;}
  if(e.target.id==='sm-save-btn'){saveStatus();return;}
  if(e.target.id==='rp-close-btn'||e.target.id==='ov-rp'){document.getElementById('ov-rp').classList.remove('show');return;}
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


document.addEventListener('change',function(e){
  if(e.target.name==='smr'){
    document.querySelectorAll('.sm-opt').forEach(o=>o.classList.toggle('chosen',o.querySelector('input').value===e.target.value));
    document.getElementById('sm-req').style.display='none';
  }
});
/* ── ARRANQUE ── */
document.getElementById('login-screen').style.display='flex';
</script>

<!-- MODAL ESTADO -->
<div class="ov" id="ov-st">
  <div class="stmod">
    <h3>Estado de la venta</h3>
    <p class="stmod-cl" id="sm-info"></p>
    <div class="sm-opts">
      <label class="sm-opt" data-v="nueva">
        <input type="radio" name="smr" value="nueva">
        <div><div class="sm-ol">🆕 Nueva</div><div class="sm-os">Sin gestión aún</div></div>
      </label>
      <label class="sm-opt" data-v="pendiente">
        <input type="radio" name="smr" value="pendiente">
        <div><div class="sm-ol">📞 Pendiente de llamar</div><div class="sm-os">Cliente aún no contactado — agrega nota</div></div>
      </label>
      <label class="sm-opt" data-v="declino">
        <input type="radio" name="smr" value="declino">
        <div><div class="sm-ol">❌ Declinó</div><div class="sm-os">Cliente no quiso la tarjeta — agrega motivo</div></div>
      </label>
      <label class="sm-opt" data-v="preasignado">
        <input type="radio" name="smr" value="preasignado">
        <div><div class="sm-ol">⭐ Preasignado</div><div class="sm-os">Cliente con oferta ya asignada</div></div>
      </label>
      <label class="sm-opt" data-v="vendida">
        <input type="radio" name="smr" value="vendida">
        <div><div class="sm-ol">✅ Vendida</div><div class="sm-os">Tarjeta contratada exitosamente</div></div>
      </label>
    </div>
    <div class="sm-nota">
      <label>Nota / Razón <span id="sm-req" style="color:#f87171;display:none">* obligatoria para este estado</span></label>
      <textarea id="sm-nota-txt" placeholder="Ej: No contestó, llamar martes por la tarde…"></textarea>
    </div>
    <div class="sm-btns">
      <button class="sm-cancel" id="sm-cancel-btn">Cancelar</button>
      <button class="sm-save" id="sm-save-btn">💾 Guardar estado</button>
    </div>
  </div>
</div>

<!-- POPUP RAZÓN -->
<div class="ov" id="ov-rp">
  <div class="rpop">
    <h4 id="rp-title">Nota</h4>
    <div class="rpop-body" id="rp-body"></div>
    <div class="rpop-btns">
      <button class="sm-cancel" id="rp-edit-btn">✏️ Editar estado</button>
      <button class="sm-save" id="rp-close-btn">Cerrar</button>
    </div>
  </div>
</div>

</body>
</html>
