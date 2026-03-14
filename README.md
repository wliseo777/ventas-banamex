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
.field input,.field select,.field textarea{background:var(--s2);border:1px solid var(--br2);border-radius:8px;padding:11px 14px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:14px;outline:none;transition:border-color .15s;width:100%;}
.field input:focus,.field select:focus,.field textarea:focus{border-color:var(--red);}
.field select option{background:#1e1e1e;}
.field input::placeholder,.field textarea::placeholder{color:#444;}
.field textarea{resize:vertical;min-height:70px;line-height:1.5;}
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
.sync-bar{display:flex;align-items:center;gap:8px;padding:8px 14px;background:var(--s2);border-radius:8px;font-size:12px;color:var(--mu);margin-bottom:1rem;flex-wrap:wrap;}
.sync-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.sync-dot.ok{background:var(--green);}
.sync-dot.err{background:var(--red);}
.sync-dot.loading{background:var(--gold-l);animation:pulse 1s infinite;}
@keyframes pulse{0%,100%{opacity:1;}50%{opacity:.3;}}
/* Telegram status indicator */
.tg-status{display:inline-flex;align-items:center;gap:5px;padding:3px 9px;border-radius:20px;font-size:10px;font-weight:600;margin-left:auto;}
.tg-ok{background:rgba(34,197,94,.15);border:1px solid rgba(34,197,94,.3);color:var(--green);}
.tg-err{background:var(--red-f);border:1px solid rgba(200,16,46,.3);color:#f88;}
.tg-loading{background:rgba(200,168,75,.13);border:1px solid rgba(200,168,75,.3);color:var(--gold-l);}

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

/* ── TARJETAS VISUALES ── */
.cards-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:1.25rem;margin-bottom:2rem;}
.tc{border-radius:18px;padding:1.5rem 1.6rem;position:relative;overflow:hidden;cursor:pointer;transition:transform .2s,box-shadow .2s;min-height:190px;display:flex;flex-direction:column;justify-content:space-between;box-shadow:0 8px 32px rgba(0,0,0,.5);}
.tc:hover{transform:translateY(-5px);box-shadow:0 20px 50px rgba(0,0,0,.7);}
.tc.sel{outline:3px solid rgba(255,255,255,.8);outline-offset:3px;}
.tc-joy{background:linear-gradient(135deg,#C8102E 0%,#8B0B1F 100%);}
.tc-clasica{background:linear-gradient(135deg,#1a2744 0%,#2e4a8a 100%);}
.tc-teleton{background:linear-gradient(135deg,#4a0080 0%,#9333ea 100%);}
.tc-oro{background:linear-gradient(135deg,#7c4f00 0%,#C8A84B 100%);}
.tc-descubre{background:linear-gradient(135deg,#064e3b 0%,#10b981 100%);}
.tc-platinum{background:linear-gradient(135deg,#1f2937 0%,#6b7280 100%);}
.tc-explora{background:linear-gradient(135deg,#1e3a8a 0%,#3b82f6 100%);}
.tc-chip{width:36px;height:26px;border-radius:5px;background:linear-gradient(135deg,#c8a84b,#f0c060,#c8a84b);margin-bottom:1rem;box-shadow:0 2px 8px rgba(0,0,0,.4);}
.tc-num{font-family:monospace;font-size:14px;letter-spacing:.2em;color:rgba(255,255,255,.8);margin-bottom:.5rem;}
.tc-cardname{font-size:10px;color:rgba(255,255,255,.5);text-transform:uppercase;letter-spacing:.1em;}
.tc-titular{font-size:13px;color:#fff;font-weight:600;letter-spacing:.04em;}
.tc-logo{position:absolute;top:1.2rem;right:1.2rem;font-family:'Bebas Neue',sans-serif;font-size:.95rem;color:rgba(255,255,255,.9);letter-spacing:.06em;}
.tc-badge{position:absolute;top:1.2rem;left:50%;transform:translateX(-50%);background:rgba(0,0,0,.35);backdrop-filter:blur(6px);border:1px solid rgba(255,255,255,.2);border-radius:20px;padding:3px 11px;font-size:10px;font-weight:600;color:#fff;white-space:nowrap;}
.tc-mc{position:absolute;bottom:1.2rem;right:1.2rem;display:flex;}
.tc-mc span{width:22px;height:22px;border-radius:50%;opacity:.9;}
.tc-mc .r{background:#eb001b;}
.tc-mc .y{background:#f79e1b;margin-left:-9px;}
/* Detail panel */
.card-detail{background:var(--s1);border:1px solid var(--br2);border-radius:16px;padding:1.75rem;margin-top:1.5rem;animation:fadeIn .2s ease;}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
.cd-top{display:flex;gap:1.25rem;align-items:flex-start;flex-wrap:wrap;margin-bottom:1.5rem;}
.cd-mini{border-radius:12px;padding:1rem 1.1rem;width:180px;min-height:110px;flex-shrink:0;display:flex;flex-direction:column;justify-content:space-between;}
.cd-title{font-family:'Bebas Neue',sans-serif;font-size:1.7rem;letter-spacing:.03em;flex:1;}
.cd-pts{font-size:12px;color:var(--mu);margin-top:.2rem;}
.cd-close{background:var(--s2);border:1px solid var(--br2);border-radius:8px;padding:6px 14px;font-family:'Outfit',sans-serif;font-size:12px;color:var(--mu);cursor:pointer;flex-shrink:0;align-self:flex-start;}
.cd-close:hover{color:var(--tx);}
.cd-nums{display:grid;grid-template-columns:repeat(auto-fill,minmax(135px,1fr));gap:8px;margin-bottom:1.25rem;}
.cd-n{background:var(--s2);border-radius:10px;padding:10px 12px;}
.cd-nl{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;font-weight:500;}
.cd-nv{font-size:14px;font-weight:600;margin-top:3px;}
.red{color:#f88;}.green{color:var(--green);}.gold{color:var(--gold-l);}
.cd-sec{font-size:11px;font-weight:600;color:var(--mu);text-transform:uppercase;letter-spacing:.08em;margin:1.2rem 0 .6rem;}
.cd-bens{list-style:none;display:flex;flex-direction:column;gap:7px;}
.cd-bens li{display:flex;gap:10px;align-items:flex-start;font-size:13px;line-height:1.55;color:#ccc;background:var(--s2);border-radius:8px;padding:9px 12px;}
.cd-ico{font-size:15px;flex-shrink:0;margin-top:1px;}
.cd-bt{font-weight:600;color:var(--tx);display:block;margin-bottom:2px;}
.cd-reqs{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:7px;}
.cd-req{background:var(--s2);border-radius:8px;padding:8px 12px;font-size:12px;color:#ccc;display:flex;gap:8px;align-items:flex-start;}
.cd-nota{background:var(--gold-f);border:1px solid rgba(200,168,75,.25);border-radius:8px;padding:10px 14px;font-size:11px;color:#bbb;line-height:1.6;margin-top:1rem;}

/* ── STATUS BADGES en ventas ── */
.st-badge{display:inline-flex;align-items:center;gap:5px;padding:3px 9px;border-radius:20px;font-size:11px;font-weight:600;cursor:pointer;transition:opacity .15s;white-space:nowrap;}
.st-badge:hover{opacity:.8;}
.st-pend{background:rgba(251,191,36,.15);border:1px solid rgba(251,191,36,.4);color:#fbbf24;}
.st-decl{background:rgba(239,68,68,.15);border:1px solid rgba(239,68,68,.4);color:#ef4444;}
.st-pre{background:rgba(168,85,247,.15);border:1px solid rgba(168,85,247,.4);color:#a855f7;}
.st-ok{background:var(--green-f);border:1px solid rgba(34,197,94,.3);color:var(--green);}

/* ── STATUS MODAL mejorado ── */
.st-modal{position:fixed;inset:0;background:rgba(0,0,0,.75);display:none;align-items:center;justify-content:center;z-index:999;padding:1rem;}
.st-modal.show{display:flex;}
.st-box{background:var(--s1);border:1px solid var(--br2);border-radius:18px;padding:2rem;max-width:460px;width:100%;max-height:90vh;overflow-y:auto;}
.st-box h3{font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:.03em;margin-bottom:.3rem;}
.st-box p{font-size:13px;color:var(--mu);margin-bottom:1.25rem;line-height:1.6;}
.st-opts{display:flex;flex-direction:column;gap:8px;margin-bottom:1.25rem;}
.st-opt{display:flex;align-items:center;gap:10px;background:var(--s2);border:2px solid var(--br2);border-radius:10px;padding:11px 14px;cursor:pointer;transition:border-color .15s;}
.st-opt:hover{border-color:var(--br2);}
.st-opt.chosen{border-color:var(--gold);}
.st-opt input[type=radio]{accent-color:var(--gold);width:16px;height:16px;flex-shrink:0;}
.st-opt-label{font-size:13px;font-weight:500;}
.st-opt-sub{font-size:11px;color:var(--mu);margin-top:2px;}

/* ── COMENTARIOS POR ESTADO ── */
.st-comments-section{margin-bottom:1rem;}
.st-comments-header{font-size:11px;font-weight:600;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;margin-bottom:10px;display:flex;align-items:center;gap:6px;}
.st-comment-block{background:var(--s2);border:1px solid var(--br);border-radius:10px;padding:12px 14px;margin-bottom:8px;}
.st-comment-block.highlighted{border-color:rgba(200,168,75,.4);background:rgba(200,168,75,.05);}
.st-comment-label{font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:.07em;margin-bottom:6px;display:flex;align-items:center;gap:5px;}
.st-comment-label.pend{color:#fbbf24;}
.st-comment-label.pre{color:#a855f7;}
.st-comment-label.decl{color:#ef4444;}
.st-comment-label.ok{color:var(--green);}
.st-comment-block textarea{width:100%;background:rgba(0,0,0,.2);border:1px solid var(--br2);border-radius:7px;padding:9px 12px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:13px;resize:vertical;min-height:65px;outline:none;line-height:1.5;}
.st-comment-block textarea:focus{border-color:var(--gold);}
.st-comment-block textarea::placeholder{color:#444;}
.st-comment-hint{font-size:10px;color:var(--mu);margin-top:4px;line-height:1.4;}
.st-req-badge{display:inline-block;padding:1px 6px;background:var(--red-f);border-radius:4px;color:#f88;font-size:9px;font-weight:600;margin-left:4px;}

.st-btns{display:flex;gap:8px;justify-content:flex-end;margin-top:1.25rem;}
.st-save{padding:10px 22px;background:var(--red);border:none;border-radius:8px;color:#fff;font-family:'Outfit',sans-serif;font-size:14px;font-weight:600;cursor:pointer;}
.st-save:hover{background:var(--red-d);}
.st-cancel{padding:10px 18px;background:transparent;border:1px solid var(--br2);border-radius:8px;color:var(--mu);font-family:'Outfit',sans-serif;font-size:13px;cursor:pointer;}
.st-cancel:hover{color:var(--tx);}

/* ── STATUS DETAIL POPUP ── */
.st-detail-pop{position:fixed;inset:0;background:rgba(0,0,0,.75);display:none;align-items:center;justify-content:center;z-index:999;padding:1rem;}
.st-detail-pop.show{display:flex;}
.st-detail-box{background:var(--s1);border:1px solid var(--br2);border-radius:18px;padding:2rem;max-width:420px;width:100%;}
.st-detail-box h3{font-family:'Bebas Neue',sans-serif;font-size:1.3rem;margin-bottom:1rem;}
.st-detail-txt{font-size:14px;line-height:1.7;color:#ccc;background:var(--s2);border-radius:10px;padding:14px;}

/* Nota inline en tabla */
.nota-preview{font-size:10px;color:var(--mu);margin-top:2px;max-width:200px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
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
        <div class="row2">
          <div class="field"><label>RFC del cliente (opcional)</label><input type="text" id="f-rfc" placeholder="Ej. GOMJ850101MDF"></div>
          <div class="field"><label>Ingresos mensuales (opcional)</label><input type="number" id="f-ingresos" placeholder="Ej. 25000" min="0"></div>
        </div>
        <div class="row2">
          <div class="field"><label>Tarjeta de referencia (opcional)</label><input type="text" id="f-tarjetaRef" placeholder="Ej. Clásica Banamex"></div>
          <div class="field"><label>Línea de crédito ref. (opcional)</label><input type="number" id="f-ldcRef" placeholder="Ej. 30000" min="0"></div>
        </div>
        <!-- COMENTARIO INICIAL -->
        <div class="field">
          <label>Comentario inicial (opcional)</label>
          <textarea id="f-comentario" placeholder="Ej. Cliente con tarjeta Oro vigente, le falta documentación, llamar jueves…" rows="2"></textarea>
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
      <div class="sync-bar">
        <div class="sync-dot loading" id="sync-dot"></div>
        <span id="sync-txt">Cargando…</span>
        <span class="tg-status tg-loading" id="tg-status">⏳ Telegram…</span>
      </div>
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
            <th>Tarjeta</th><th>Estado</th><th>Comentario</th><th>Fecha venta</th><th>Registrado</th><th></th>
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
      <div style="display:flex;align-items:flex-start;gap:10px;padding:11px 14px;background:rgba(200,168,75,.07);border:1px solid rgba(200,168,75,.2);border-radius:8px;font-size:12px;color:#bbb;margin-bottom:1.5rem;line-height:1.6;">
        <span style="font-size:16px;flex-shrink:0;margin-top:1px;">💾</span>
        <span>Los ejecutivos se guardan <strong style="color:var(--gold-l)">en este navegador/dispositivo</strong>. Si abres la app en otra computadora o celular, tendrás que volver a agregarlos ahí. Las <strong style="color:var(--gold-l)">ventas</strong> sí se sincronizan automáticamente entre todos vía Telegram.</span>
      </div>
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
/* ════════════════════════════════════════════════════
   TELEGRAM CONFIG
   ════════════════════════════════════════════════════ */
const TG_TOKEN = '8674156237:AAH_TxLj17k8U08zwTuz1XxrvNLgaqsPNcE';
const TG_CHAT  = '-1003454541647';
const TG_URL   = 'https://api.telegram.org/bot' + TG_TOKEN;

/* ════════════════════════════════════════════════════
   CLAVES DE ALMACENAMIENTO

   DISEÑO CORRECTO:
   ─ VENTAS   → Telegram (sincronización entre dispositivos)
               usa un mensaje "ancla" que SE EDITA siempre.
               La ID del mensaje ancla se guarda en localStorage.
   ─ USUARIOS → SOLO localStorage. Nunca van a Telegram.
               El problema anterior era que getUpdates avanza
               el offset y nunca vuelve a ver mensajes viejos,
               borrando así los usuarios al leer desde otro
               dispositivo. Solución definitiva: usuarios son
               locales al admin, no necesitan sincronizarse.
   ════════════════════════════════════════════════════ */
const SK_S        = 'bnx_sales_v7';      // ventas en localStorage (caché)
const SK_U        = 'bnx_users_v7';      // usuarios en localStorage (fuente de verdad)
const SK_SALES_MSG= 'bnx_tg_sales_msgid';// ID del mensaje ancla de ventas en Telegram
const TG_PREFIX   = 'BNX_SALES_V7:';    // prefijo del mensaje de ventas

let TG_CONNECTED = null;

function loadLS(k){ try{ return JSON.parse(localStorage.getItem(k))||[]; }catch{ return []; } }
function saveLS(k,d){ localStorage.setItem(k, JSON.stringify(d)); }

/* ════════════════════════════════════════════════════
   TELEGRAM — VENTAS CON MENSAJE ANCLA
   En lugar de enviar un nuevo mensaje cada vez, se
   edita siempre el mismo mensaje. Así getUpdates no
   importa nada: la verdad está en ese único mensaje.
   ════════════════════════════════════════════════════ */
async function tgPost(method, params={}){
  try{
    const r = await fetch(`${TG_URL}/${method}`,{
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body:JSON.stringify(params)
    });
    return await r.json();
  }catch(e){ return {ok:false, description:e.message}; }
}

/* Guarda ventas: edita el mensaje ancla si existe, si no crea uno nuevo */
async function tgSaveVentas(arr){
  const text = TG_PREFIX + JSON.stringify(arr);
  const existingId = localStorage.getItem(SK_SALES_MSG);
  let r;
  if(existingId){
    r = await tgPost('editMessageText',{
      chat_id: TG_CHAT,
      message_id: parseInt(existingId),
      text
    });
    // Si el edit falla (mensaje borrado, etc.), crear nuevo
    if(!r.ok){
      r = await tgPost('sendMessage',{ chat_id: TG_CHAT, text });
      if(r.ok && r.result?.message_id){
        localStorage.setItem(SK_SALES_MSG, r.result.message_id);
      }
    }
  } else {
    r = await tgPost('sendMessage',{ chat_id: TG_CHAT, text });
    if(r.ok && r.result?.message_id){
      localStorage.setItem(SK_SALES_MSG, r.result.message_id);
    }
  }
  setTgStatus(r.ok);
  return r.ok;
}

/* Lee ventas: intenta leer el mensaje ancla directamente por ID.
   Si no tiene ID guardada, hace un scan de los últimos 100 mensajes. */
async function tgLoadVentas(){
  const existingId = localStorage.getItem(SK_SALES_MSG);
  if(existingId){
    // Telegram no tiene "getMessage" directo, usamos forwardMessage como truco
    // En cambio, confiamos en el caché local y solo sincronizamos en refresh
    // Hacemos getUpdates sin offset para ver si hay algo más nuevo
  }
  // Scan sin offset — lee TODOS los updates disponibles (últimos ~100)
  // NO guardamos offset para que siempre pueda encontrar el mensaje ancla
  const r = await tgPost('getUpdates',{ limit:100 });
  if(!r.ok){ setTgStatus(false); return null; }
  setTgStatus(true);
  let latest = null;
  let latestMsgId = 0;
  for(const u of (r.result||[])){
    const txt = u.message?.text || u.edited_message?.text || '';
    const msgId = u.message?.message_id || u.edited_message?.message_id || 0;
    const chatId = (u.message?.chat?.id || u.edited_message?.chat?.id || '').toString();
    if(chatId === TG_CHAT && txt.startsWith(TG_PREFIX) && msgId >= latestMsgId){
      try{
        latest = JSON.parse(txt.slice(TG_PREFIX.length));
        latestMsgId = msgId;
        // Guardar el ID del mensaje más reciente como ancla
        localStorage.setItem(SK_SALES_MSG, msgId);
      }catch{}
    }
  }
  return latest;
}

function setTgStatus(ok){
  TG_CONNECTED = ok;
  const el = document.getElementById('tg-status');
  if(!el) return;
  if(ok){
    el.className = 'tg-status tg-ok';
    el.textContent = '✓ Telegram conectado';
  } else {
    el.className = 'tg-status tg-err';
    el.textContent = '✕ Sin conexión Telegram';
  }
}

/* ════════════════════════════════════════════════════
   API WRAPPER
   VENTAS  → Telegram (sincronizado)
   USUARIOS → localStorage puro (sin Telegram)
   ════════════════════════════════════════════════════ */
async function api(action, body={}){
  try{
    /* ── VENTAS ── */
    if(action==='getSales'){
      const remote = await tgLoadVentas();
      if(remote !== null){ saveLS(SK_S, remote); return {ok:true, data:remote}; }
      return {ok:true, data: loadLS(SK_S)};
    }
    if(action==='addSale'){
      const arr = loadLS(SK_S);
      arr.unshift(body);
      saveLS(SK_S, arr);
      await tgSaveVentas(arr);
      return {ok:true};
    }
    if(action==='deleteSale'){
      const arr = loadLS(SK_S).filter(v=>v.folio!==body.folio);
      saveLS(SK_S, arr);
      await tgSaveVentas(arr);
      return {ok:true};
    }
    if(action==='clearSales'){
      saveLS(SK_S, []);
      await tgSaveVentas([]);
      return {ok:true};
    }
    if(action==='updateSale'){
      const arr = loadLS(SK_S);
      const idx = arr.findIndex(v=>v.folio===body.folio);
      if(idx!==-1) arr[idx] = {...arr[idx], ...body};
      saveLS(SK_S, arr);
      await tgSaveVentas(arr);
      SALES_CACHE = arr;
      return {ok:true};
    }

    /* ── USUARIOS: SOLO localStorage, nunca Telegram ── */
    if(action==='getUsers'){
      return {ok:true, data: loadLS(SK_U)};
    }
    if(action==='addUser'){
      const arr = loadLS(SK_U);
      if(arr.find(u=>u.username===body.username)) return {ok:false, error:'El usuario ya existe'};
      arr.push(body);
      saveLS(SK_U, arr);
      return {ok:true};
    }
    if(action==='deleteUser'){
      const arr = loadLS(SK_U).filter(u=>u.username!==body.username);
      saveLS(SK_U, arr);
      return {ok:true};
    }

    return {ok:false, error:'Acción desconocida'};
  }catch(e){
    setTgStatus(false);
    return {ok:false, error:e.message};
  }
}

/* ════════════════════════════════════════════════════
   UTILS
   ════════════════════════════════════════════════════ */
const ADM_U='admin', ADM_P='admin123';
let CU=null, SALES_CACHE=[], USERS_CACHE=[];
let currentSaleForStatus = null;

function esc(s){return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}
function fmt(ts){if(!ts)return '—';const d=new Date(ts);return d.toLocaleDateString('es-MX',{day:'2-digit',month:'short',year:'numeric'})+' '+d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});}
function fmtDate(s){if(!s)return '—';const[y,m,d]=s.split('-');const M=['Ene','Feb','Mar','Abr','May','Jun','Jul','Ago','Sep','Oct','Nov','Dic'];return `${parseInt(d)} ${M[parseInt(m)-1]} ${y}`;}
function ini(n){return n.trim().split(/\s+/).slice(0,2).map(w=>w[0]||'').join('').toUpperCase()||'?';}
function genFolio(){return 'BNX-'+String(Date.now()).slice(-6);}
function spin(on){document.getElementById('spinner').classList.toggle('show',on);}
function showToast(id,msg,type){const el=document.getElementById(id);if(!el)return;el.textContent=msg;el.className='toast '+type+' show';clearTimeout(el._t);el._t=setTimeout(()=>el.classList.remove('show'),4000);}

/* ════════════════════════════════════════════════════
   AUTH
   ════════════════════════════════════════════════════ */
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

/* ════════════════════════════════════════════════════
   EJECUTIVO
   ════════════════════════════════════════════════════ */
function setTodayDate(){const el=document.getElementById('f-fecha');if(el&&!el.value)el.value=new Date().toISOString().slice(0,10);}
function refreshFolio(){const el=document.getElementById('folio-pill');if(el)el.textContent=genFolio();}

async function registrarVenta(){
  const cliente=(document.getElementById('f-cliente').value||'').trim();
  const tel=(document.getElementById('f-tel').value||'').trim();
  const tarjeta=document.getElementById('f-tarjeta').value;
  const fecha=document.getElementById('f-fecha').value;
  const comentario=(document.getElementById('f-comentario').value||'').trim();
  let folio=(document.getElementById('f-folio').value||'').trim();
  const rfc = (document.getElementById('f-rfc').value||'').trim();
  const ingresos = (document.getElementById('f-ingresos').value||'').trim();
  const tarjetaRef = (document.getElementById('f-tarjetaRef').value||'').trim();
  const ldcRef = (document.getElementById('f-ldcRef').value||'').trim();

  if(!cliente){showToast('t-err','Escribe el nombre del cliente','err');return;}
  if(!tarjeta){showToast('t-err','Selecciona el tipo de tarjeta','err');return;}
  if(!fecha){showToast('t-err','Selecciona la fecha de venta','err');return;}
  if(!folio)folio=genFolio();

  document.getElementById('reg-btn').disabled=true;
  spin(true);
  const r = await api('addSale',{
    folio,
    exec:CU.name,
    username:CU.username,
    cliente,
    tel,
    tarjeta,
    fecha,
    registrado: new Date().toISOString(),
    rfc: rfc || null,
    ingresos: ingresos || null,
    tarjetaRef: tarjetaRef || null,
    ldcRef: ldcRef || null,
    estado: 'pendiente',
    // comentarios por estado: objeto separado para cada estado
    comentarios: {
      pendiente: comentario || '',
      preasignado: '',
      declino: '',
      vendida: ''
    }
  });
  spin(false);
  document.getElementById('reg-btn').disabled=false;
  if(!r.ok){showToast('t-err','Error al guardar: '+r.error,'err');return;}
  document.getElementById('f-cliente').value='';
  document.getElementById('f-tel').value='';
  document.getElementById('f-tarjeta').value='';
  document.getElementById('f-folio').value='';
  document.getElementById('f-fecha').value=new Date().toISOString().slice(0,10);
  document.getElementById('f-rfc').value='';
  document.getElementById('f-ingresos').value='';
  document.getElementById('f-tarjetaRef').value='';
  document.getElementById('f-ldcRef').value='';
  document.getElementById('f-comentario').value='';
  refreshFolio();
  showToast('t-ok','✓ Venta guardada — Folio '+folio,'ok');
  renderRecent();
}

function estadoClase(estado) {
  return { 'pendiente': 'pend', 'declino': 'decl', 'preasignado': 'pre', 'vendida': 'ok' }[estado] || 'pend';
}

function estadoTexto(estado) {
  const textos = { 'pendiente': '📞 Pendiente', 'declino': '❌ Declinó', 'preasignado': '⭐ Preasignado', 'vendida': '✅ Vendida' };
  return textos[estado] || '📞 Pendiente';
}

// Obtener el comentario activo del estado actual
function getComentarioActivo(sale) {
  if(!sale.comentarios) {
    // Compatibilidad con registros viejos que usaban notaEstado
    return sale.notaEstado || '';
  }
  return sale.comentarios[sale.estado || 'pendiente'] || '';
}

function renderRecent(){
  const list=document.getElementById('exec-recent');
  // Recargar desde localStorage para ver cambios recientes
  const localSales = loadLS(SK_S);
  const data = localSales.filter(v=>v.username===CU.username).slice(0,6);
  if(!data.length){list.innerHTML='<p style="color:var(--mu);font-size:13px">Aún no tienes ventas registradas.</p>';return;}
  list.innerHTML=data.map(v=>{
    const comentario = getComentarioActivo(v);
    return `<div class="ri">
      <div style="flex:1;min-width:0">
        <div class="ri-n">${esc(v.cliente)}${v.rfc?' 📄':''}${v.ingresos?' 💰':''}</div>
        <div class="ri-m">${esc(v.tarjeta)}${v.tel?' · '+esc(v.tel):''} · ${fmtDate(v.fecha)}</div>
        ${comentario?`<div class="nota-preview" title="${esc(comentario)}">💬 ${esc(comentario)}</div>`:''}
      </div>
      <div style="display:flex;flex-direction:column;align-items:flex-end;gap:4px;flex-shrink:0;">
        <span class="ri-f">${esc(v.folio)}</span>
        <span class="st-badge st-${estadoClase(v.estado)}" onclick="openStatusModalFromFolio('${esc(v.folio)}')">${estadoTexto(v.estado)}</span>
      </div>
    </div>`;
  }).join('');
}

/* ════════════════════════════════════════════════════
   DASHBOARD
   ════════════════════════════════════════════════════ */
function setSyncStatus(s,msg){
  const dot=document.getElementById('sync-dot');
  const txt=document.getElementById('sync-txt');
  if(!dot)return;
  dot.className='sync-dot '+s;
  txt.textContent=msg;
}

async function loadAndRenderDash(){
  setSyncStatus('loading','Cargando datos…');
  const tgEl = document.getElementById('tg-status');
  if(tgEl){ tgEl.className='tg-status tg-loading'; tgEl.textContent='⏳ Telegram…'; }
  const r=await api('getSales');
  if(!r.ok){setSyncStatus('err','Error: '+r.error);return;}
  SALES_CACHE=r.data||[];
  setSyncStatus('ok','Sincronizado · '+SALES_CACHE.length+' ventas');
  renderDashTable();
}

window.openStatusModalFromFolio = function(folio) {
  // Buscar primero en SALES_CACHE, si no en localStorage
  let sale = SALES_CACHE.find(v => v.folio === folio);
  if(!sale) sale = loadLS(SK_S).find(v => v.folio === folio);
  if (sale) openStatusModal(sale);
};

function openStatusModal(sale) {
  currentSaleForStatus = sale;
  document.getElementById('st-modal-client').textContent = `Cliente: ${sale.cliente} — Folio: ${sale.folio}`;

  // Precargar el estado actual
  const estado = sale.estado || 'pendiente';
  const radio = document.querySelector(`input[name="st-radio"][value="${estado}"]`);
  if (radio) radio.checked = true;

  // Rellenar comentarios por estado
  const comentarios = sale.comentarios || {};
  // Compatibilidad con registros viejos
  const legacyNota = sale.notaEstado || '';

  document.getElementById('st-nota-pend').value  = comentarios.pendiente   || (estado==='pendiente'   ? legacyNota : '');
  document.getElementById('st-nota-pre').value   = comentarios.preasignado || (estado==='preasignado' ? legacyNota : '');
  document.getElementById('st-nota-decl').value  = comentarios.declino     || (estado==='declino'     ? legacyNota : '');
  document.getElementById('st-nota-ok').value    = comentarios.vendida     || (estado==='vendida'     ? legacyNota : '');

  document.getElementById('st-modal').classList.add('show');
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
  if(!data.length){
    tbody.innerHTML='';
    empty.style.display='block';
  } else {
    empty.style.display='none';
    tbody.innerHTML=data.map(v=>{
      const comentario = getComentarioActivo(v);
      return `<tr>
        <td class="tdf">${esc(v.folio)}</td>
        <td class="tdb">${esc(v.exec)}</td>
        <td>${esc(v.cliente)}</td>
        <td class="tdm">${esc(v.tel||'—')}</td>
        <td><span class="badge b-r">${esc(v.tarjeta)}</span></td>
        <td>
          <span class="st-badge st-${estadoClase(v.estado)}" onclick="openStatusModalFromFolio('${esc(v.folio)}')">
            ${estadoTexto(v.estado)}
          </span>
        </td>
        <td class="tdm" style="max-width:180px;">
          ${comentario
            ? `<span style="cursor:pointer;color:#ccc;" onclick="showStatusNote('${comentario.replace(/'/g,"\\'")}')" title="${esc(comentario)}">💬 ${esc(comentario.slice(0,40))}${comentario.length>40?'…':''}</span>`
            : '<span style="color:#444">—</span>'}
        </td>
        <td class="tdm">${fmtDate(v.fecha)}</td>
        <td class="tdm">${fmt(v.registrado)}</td>
        <td><button class="delbtn" data-folio="${esc(v.folio)}">✕</button></td>
      </tr>`;
    }).join('');
  }

  // Ranking
  const counts={};
  all.forEach(v=>{counts[v.exec]=(counts[v.exec]||0)+1;});
  const sorted=Object.entries(counts).sort((a,b)=>b[1]-a[1]).slice(0,12);
  const pc=['rp1','rp2','rp3'];
  document.getElementById('rank-grid').innerHTML=sorted.length
    ?sorted.map(([name,cnt],i)=>`<div class="rcard"><div class="rpos ${pc[i]||''}">${i+1}</div><div><div class="rkn">${esc(name)}</div><div class="rkc">${cnt} venta${cnt!==1?'s':''}</div></div></div>`).join('')
    :'<p style="color:var(--mu);font-size:13px">Sin datos aún.</p>';
}

window.showStatusNote = function(nota) {
  document.getElementById('st-detail-txt').textContent = nota;
  document.getElementById('st-detail-pop').classList.add('show');
};

async function delSale(folio){
  if(!confirm('¿Eliminar la venta con folio '+folio+'?'))return;
  spin(true);const r=await api('deleteSale',{folio});spin(false);
  if(!r.ok){alert('Error: '+r.error);return;}
  SALES_CACHE=SALES_CACHE.filter(v=>v.folio!==folio);
  renderDashTable();
  setSyncStatus('ok','Sincronizado · '+SALES_CACHE.length+' ventas');
}

/* ════════════════════════════════════════════════════
   USUARIOS
   ════════════════════════════════════════════════════ */
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

/* ════════════════════════════════════════════════════
   BENEFICIOS
   ════════════════════════════════════════════════════ */
const CARDS=[
  {id:'joy',color:'tc-joy',name:'Joy Banamex',badge:'Sin anualidad',
   num:'•••• •••• •••• 1234',
   cat:'84% sin IVA',tasa:'63.69% anual',anualidad:'Sin comisión*',ingreso:'$15,000',ldc:'Desde $15,000',adicional:'—',
   pts:'No genera puntos Premia',
   bens:[
     {i:'🎬',t:'2x1 en Cinépolis',d:'Boletos en salas tradicionales comprando en cinepolis.com o la app. Código: W4BE26UE25WD44Z6 (vigente al 31 ago 2026).'},
     {i:'☕',t:'Bonificación Starbucks',d:'Ahorra $45 en tu próximo consumo al recargar $150 en la app Starbucks Rewards los domingos.'},
     {i:'🚫',t:'Sin CVV impreso',d:'Más segura para compras en línea. Tu CVV digital cambia en cada compra desde la App Banamex.'},
     {i:'📅',t:'Elige tu fecha de corte',d:'Cambia tu fecha de corte una vez al año llamando al 55 1226 2639.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra tus boletos antes que nadie para los mejores eventos culturales, deportivos y espectáculos de México.'},
     {i:'🆘',t:'Mastercard Global Service',d:'Reposición de tarjeta en 48 hrs en caso de robo o extravío en cualquier parte del mundo.'},
     {i:'🏥',t:'Libra One gratis 1 año',d:'Consulta médica, nutricional y más asistencias sin costo durante el primer año. Solicítalo al 55 5809 4904.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses (luz, agua, predial, TV de paga)','18 años de edad mínimo','Ingresos desde $15,000 MXN'],
   nota:'*Realiza al menos $300 en compras al mes para evitar comisión por inactividad de $149 sin IVA. Aplican cargos recurrentes.'
  },
  {id:'clasica',color:'tc-clasica',name:'Clásica Banamex',badge:'Puntos Premia 5%',
   num:'•••• •••• •••• 2345',
   cat:'88.7% sin IVA',tasa:'62.63% anual',anualidad:'$815 sin IVA',ingreso:'$15,000',ldc:'Desde $15,000',adicional:'$405 sin IVA',
   pts:'5% Puntos Premia en todas tus compras',
   bens:[
     {i:'🎁',t:'1er año sin anualidad',d:'Realiza una compra antes del primer corte. Bonificación a los 90 días. Vigente hasta 21 mayo 2026. Solo titulares.'},
     {i:'⭐',t:'5% Puntos Premia',d:'Acumula en todas tus compras y úsalos como efectivo en cajeros Citibanamex o en establecimientos participantes.'},
     {i:'⛽',t:'Puntos Dobles en gasolina',d:'Gana el doble de puntos al cargar gasolina todos los días de la semana. Tope de 1,000 puntos por semana.'},
     {i:'🏥',t:'3, 6 o 12 Pagos Fijos en Salud',d:'En hospitales, laboratorios, farmacias y clínicas de salud y belleza. Mínimo $3,000. Llama 48 hrs después al 55 2226 3639.'},
     {i:'🎬',t:'2x1 en Cinépolis',d:'Beneficio Mastercard en salas tradicionales comprando desde cinepolis.com o la app.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Acceso anticipado a boletos de los mejores eventos antes que el público en general.'},
     {i:'🏥',t:'Libra One gratis 1 año',d:'Asistencias médicas, nutricionales y más sin costo el primer año de la tarjeta.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $15,000 MXN'],
   nota:'Bono bienvenida: 2,000 Puntos Premia al gastar $5,000 en primeros 3 meses. Vigente hasta 21 may 2026.'
  },
  {id:'teleton',color:'tc-teleton',name:'Teletón Banamex',badge:'Causa social',
   num:'•••• •••• •••• 3456',
   cat:'87.0% sin IVA',tasa:'62.47% anual',anualidad:'$540 sin IVA',ingreso:'$15,000',ldc:'Desde $15,000',adicional:'Sin costo',
   pts:'No genera puntos Premia',
   bens:[
     {i:'❤️',t:'Apoya al Teletón',d:'Cada uso de tu tarjeta apoya a los Centros de Rehabilitación Infantil Teletón en México.'},
     {i:'💰',t:'Anualidad más baja del segmento',d:'Solo $540 sin IVA. Primer año sin anualidad con una compra antes del primer corte. Vigente hasta 21 may 2026.'},
     {i:'👨‍👩‍👧‍👦',t:'6 tarjetas adicionales sin costo',d:'Agrega hasta 6 tarjetas adicionales para tu familia sin ningún costo extra.'},
     {i:'🎬',t:'2x1 en Cinépolis',d:'Beneficio Mastercard en salas tradicionales de todo el país.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra tus boletos antes que nadie en los mejores eventos de México.'},
     {i:'🏥',t:'Libra One gratis 1 año',d:'Asistencias médicas y más sin costo el primer año.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $15,000 MXN'],
   nota:'Primer año sin anualidad con una compra antes del primer corte. Vigente hasta 21 may 2026. Solo titulares.'
  },
  {id:'oro',color:'tc-oro',name:'Oro Banamex',badge:'Puntos Premia 7%',
   num:'•••• •••• •••• 4567',
   cat:'85.7% sin IVA',tasa:'60.58% anual',anualidad:'$1,230 sin IVA',ingreso:'$25,000',ldc:'Desde $25,000',adicional:'$620 sin IVA',
   pts:'7% Puntos Premia en todas tus compras',
   bens:[
     {i:'🎁',t:'1er año sin anualidad + bono',d:'Anualidad bonificada con una compra. Bono de 2,000 Puntos al gastar $5,000 en primeros 3 meses. Vigente hasta 21 may 2026.'},
     {i:'⭐',t:'7% Puntos Premia',d:'El mayor % de puntos en tarjetas básicas Banamex. Acumula y canjea como efectivo en cajeros.'},
     {i:'⛽',t:'Puntos Dobles en gasolina',d:'El doble de puntos al cargar gasolina todos los días. Tope de 1,000 pts/semana.'},
     {i:'✈️',t:'3 MSI en viajes y salud',d:'3 meses sin intereses en viajes, salud y belleza. Mínimo $3,000. Llama al 55 2226 3639.'},
     {i:'🛡️',t:'Seguro de viajes',d:'Hasta $400 USD por robo o daño accidental en viajes. Master Seguro de Viajes hasta $250,000 USD.'},
     {i:'🔒',t:'Seguro por fraude',d:'Cobertura hasta el saldo total de la cuenta en caso de facturación fraudulenta.'},
     {i:'🏥',t:'Libra One gratis 1 año',d:'Asistencias médicas, viales y más sin costo el primer año de la tarjeta.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $25,000 MXN'],
   nota:'Bono bienvenida: 2,000 Puntos Premia al gastar $5,000 en primeros 3 meses. Vigente hasta 21 may 2026.'
  },
  {id:'descubre',color:'tc-descubre',name:'Descubre Banamex',badge:'Puntos Momentos',
   num:'•••• •••• •••• 5678',
   cat:'86.0% sin IVA',tasa:'62.31% anual',anualidad:'$1,230 sin IVA',ingreso:'$25,000',ldc:'Desde $25,000',adicional:'$620 sin IVA',
   pts:'1 Punto Momento por cada $1 USD gastado',
   bens:[
     {i:'🎁',t:'1er año sin anualidad + bono',d:'Anualidad bonificada. Bono de 2,000 Puntos al gastar $5,000 en primeros 3 meses. Vigente hasta 21 may 2026.'},
     {i:'🌟',t:'Puntos Momentos',d:'1 Punto Momento por cada dólar gastado (o equivalente en pesos) en todas tus compras.'},
     {i:'✈️',t:'2x1 en vuelos nacionales',d:'Bienvenida: 600 pts en 3 meses. Aniversario: 4,500 pts. Destinos: Cancún, Los Cabos, PVR, Acapulco, Cozumel, Huatulco, La Paz, Veracruz, Mazatlán, Zihuatanejo.'},
     {i:'🎩',t:'Mastercard Concierge 24/7',d:'Asistente personal para reservas de restaurantes, hoteles y coordinación de eventos en todo el mundo.'},
     {i:'🚗',t:'Elite Valet AICM',d:'50% de descuento en estacionamiento cercano al AICM. Hasta 5 días naturales, 2 entradas por mes.'},
     {i:'🍽️',t:'Dining Program',d:'20% de descuento en restaurantes seleccionados más bebida de cortesía en tu visita.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra antes que nadie para los mejores eventos culturales, deportivos y espectáculos.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años de edad mínimo','Ingresos desde $25,000 MXN'],
   nota:'Bono bienvenida: 2,000 Puntos Momentos al gastar $5,000 en primeros 3 meses. Calculado al 31 mar 2025, vigente al 30 sep 2025.'
  },
  {id:'platinum',color:'tc-platinum',name:'Platinum Banamex',badge:'Premium · Salas VIP',
   num:'•••• •••• •••• 6789',
   cat:'40.7% sin IVA',tasa:'32.02% anual',anualidad:'$2,725 sin IVA',ingreso:'$75,000',ldc:'Desde $50,000',adicional:'$1,360 sin IVA',
   pts:'10% Puntos Premia en todas tus compras',
   bens:[
     {i:'🎁',t:'1er año sin anualidad + bono',d:'Anualidad bonificada. Bono de 4,000 Puntos al gastar $15,000 en primeros 3 meses. Vigente hasta 21 may 2026.'},
     {i:'💎',t:'10% Puntos Premia',d:'El mayor % de puntos de toda la línea Banamex. Acumula y úsalos como efectivo en cajeros.'},
     {i:'🛡️',t:'LIBRA Premium gratis de por vida',d:'Asistencias Vial, Legal, Gestoría, en el Hogar y Médica sin costo mientras mantengas la tarjeta activa.'},
     {i:'✈️',t:'14 accesos anuales a salas VIP',d:'10 accesos a Salones Beyond (tú + 1 acompañante) en CDMX, GDL y MTY + 4 accesos a 800+ salas Mastercard Airport Experiences en el mundo.'},
     {i:'🎩',t:'Mastercard Concierge 24/7',d:'Asistente personal en todo el mundo para reservas, eventos especiales y coordinación.'},
     {i:'🍽️',t:'Dining Program',d:'20% de descuento en restaurantes seleccionados + bebida de cortesía.'},
     {i:'📉',t:'CAT preferencial',d:'Solo 40.7% sin IVA — la tasa más baja de las tarjetas estándar Banamex.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años mínimo','Ingresos desde $75,000 MXN','Buen historial crediticio'],
   nota:'Bono bienvenida: 4,000 Puntos Premia al gastar $15,000 en primeros 3 meses. Vigente hasta 21 may 2026. Solo titulares.'
  },
  {id:'explora',color:'tc-explora',name:'Explora Banamex',badge:'Viajero frecuente',
   num:'•••• •••• •••• 7890',
   cat:'81.2% sin IVA',tasa:'60.27% anual',anualidad:'$2,725 sin IVA',ingreso:'$75,000',ldc:'Desde $50,000',adicional:'$1,360 sin IVA',
   pts:'1.15 Puntos Momentos por cada $1 USD gastado',
   bens:[
     {i:'🎁',t:'1er año sin anualidad + bono',d:'Anualidad bonificada. Bono de 4,000 Puntos al gastar $15,000 en primeros 3 meses. Vigente hasta 21 may 2026.'},
     {i:'🌟',t:'1.15 Puntos Momentos',d:'Por cada dólar gastado (o equivalente en pesos). Las tarjetas adicionales también acumulan puntos en la cuenta titular.'},
     {i:'✈️',t:'2x1 en vuelos + bono aniversario',d:'Bienvenida: 1,300 pts en 3 meses. Aniversario: 10,000 Puntos Explora para vuelos nacionales e internacionales.'},
     {i:'🛫',t:'14 accesos anuales a salas VIP',d:'10 accesos a Salones Beyond + 4 accesos a 800+ salas Mastercard Airport Experiences en todo el mundo.'},
     {i:'🎩',t:'Mastercard Concierge 24/7',d:'Asistente personal global los 365 días para reservas, eventos y coordinación especial.'},
     {i:'🚗',t:'Elite Valet AICM',d:'50% de descuento en estacionamiento AICM. Hasta 5 días naturales, 2 entradas por mes.'},
     {i:'🔒',t:'Master Seguro de Viajes hasta $1M USD',d:'Cobertura de hasta $1,000,000 USD para ti y tu familia más seguro de equipaje, autos y más.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años mínimo','Ingresos desde $75,000 MXN','Buen historial crediticio'],
   nota:'Bono bienvenida: 4,000 Puntos al gastar $15,000 en primeros 3 meses. Calculado al 31 mar 2025, vigente al 30 sep 2025.'
  }
];

let _activeCard = null;

function buildBenPanels(){
  document.getElementById('ben-tabs').style.display='none';
  document.getElementById('ben-panels').innerHTML=
    '<div class="cards-grid" id="cards-grid"></div><div id="card-detail-wrap"></div>';
  renderCardsGrid();
}

function renderCardsGrid(){
  const grid = document.getElementById('cards-grid');
  if(!grid) return;
  grid.innerHTML = CARDS.map(c=>`
    <div class="tc ${c.color}${_activeCard===c.id?' sel':''}" data-cid="${c.id}">
      <div class="tc-badge">${c.badge}</div>
      <div class="tc-logo">BANAMEX</div>
      <div>
        <div class="tc-chip"></div>
        <div class="tc-num">${c.num}</div>
      </div>
      <div style="display:flex;align-items:flex-end;justify-content:space-between;">
        <div>
          <div class="tc-cardname">Tarjeta de Crédito</div>
          <div class="tc-titular">${c.name}</div>
        </div>
        <div class="tc-mc"><span class="r"></span><span class="y"></span></div>
      </div>
    </div>`).join('');
  grid.querySelectorAll('.tc').forEach(el=>el.addEventListener('click',()=>showCardDetail(el.dataset.cid)));
}

function showCardDetail(id){
  _activeCard = id;
  renderCardsGrid();
  const c = CARDS.find(x=>x.id===id);
  const wrap = document.getElementById('card-detail-wrap');
  wrap.innerHTML=`
    <div class="card-detail">
      <div class="cd-top">
        <div class="tc ${c.color} cd-mini">
          <div>
            <div class="tc-chip" style="width:28px;height:20px;margin-bottom:.5rem;"></div>
            <div style="font-family:monospace;font-size:10px;color:rgba(255,255,255,.6);letter-spacing:.1em;">${c.num}</div>
          </div>
          <div style="font-size:11px;color:#fff;font-weight:600;">${c.name}</div>
        </div>
        <div style="flex:1;min-width:0;">
          <div class="cd-title">${c.name}</div>
          <div class="cd-pts">${c.pts}</div>
        </div>
        <button class="cd-close" id="cd-close">✕ Cerrar</button>
      </div>
      <div class="cd-nums">
        <div class="cd-n"><div class="cd-nl">CAT Promedio</div><div class="cd-nv red">${c.cat}</div></div>
        <div class="cd-n"><div class="cd-nl">Tasa anual</div><div class="cd-nv red">${c.tasa}</div></div>
        <div class="cd-n"><div class="cd-nl">Anualidad</div><div class="cd-nv gold">${c.anualidad}</div></div>
        <div class="cd-n"><div class="cd-nl">Ingreso mínimo</div><div class="cd-nv green">${c.ingreso}</div></div>
        <div class="cd-n"><div class="cd-nl">Línea de Crédito</div><div class="cd-nv green">${c.ldc}</div></div>
        <div class="cd-n"><div class="cd-nl">Tarjeta adicional</div><div class="cd-nv">${c.adicional}</div></div>
      </div>
      <div class="cd-sec">✨ Beneficios principales</div>
      <ul class="cd-bens">
        ${c.bens.map(b=>`<li><span class="cd-ico">${b.i}</span><div><span class="cd-bt">${b.t}</span>${b.d}</div></li>`).join('')}
      </ul>
      <div class="cd-sec">📋 Requisitos de contratación</div>
      <div class="cd-reqs">
        ${c.reqs.map(r=>`<div class="cd-req"><span>✔</span><span>${r}</span></div>`).join('')}
      </div>
      <div class="cd-nota">ℹ️ ${c.nota}</div>
    </div>`;
  document.getElementById('cd-close').addEventListener('click',()=>{
    _activeCard=null; renderCardsGrid();
    document.getElementById('card-detail-wrap').innerHTML='';
    document.getElementById('card-detail-wrap').scrollIntoView({behavior:'smooth',block:'nearest'});
  });
  wrap.scrollIntoView({behavior:'smooth',block:'nearest'});
}

/* ════════════════════════════════════════════════════
   EVENT DELEGATION
   ════════════════════════════════════════════════════ */
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
    const csv=['Folio,Ejecutivo,Cliente,Teléfono,Tarjeta,Estado,Comentario,Fecha Venta,Registrado,RFC,Ingresos,TarjetaRef,LDCRef',
      ...SALES_CACHE.map(v=>{
        const com = getComentarioActivo(v);
        return `"${v.folio}","${v.exec}","${v.cliente}","${v.tel||''}","${v.tarjeta}","${v.estado||'pendiente'}","${com.replace(/"/g,"'")}","${fmtDate(v.fecha)}","${fmt(v.registrado)}","${v.rfc||''}","${v.ingresos||''}","${v.tarjetaRef||''}","${v.ldcRef||''}"`;
      })
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
  if(e.target.id==='st-cancel'){
    document.getElementById('st-modal').classList.remove('show');
    currentSaleForStatus = null;
    return;
  }
  if(e.target.id==='st-save'){
    if (!currentSaleForStatus) return;
    const estadoSeleccionado = document.querySelector('input[name="st-radio"]:checked')?.value;
    if (!estadoSeleccionado) { alert('Selecciona un estado.'); return; }

    // Validar que pendiente y declino tengan comentario
    const comentPend = document.getElementById('st-nota-pend').value.trim();
    const comentDecl = document.getElementById('st-nota-decl').value.trim();
    if (estadoSeleccionado === 'pendiente' && !comentPend) {
      alert('Escribe un comentario para el estado "Pendiente" (ej: no contestó, llamar el martes).');
      document.getElementById('st-nota-pend').focus();
      return;
    }
    if (estadoSeleccionado === 'declino' && !comentDecl) {
      alert('Escribe el motivo de la declinación.');
      document.getElementById('st-nota-decl').focus();
      return;
    }

    const nuevosComentarios = {
      pendiente:   document.getElementById('st-nota-pend').value.trim(),
      preasignado: document.getElementById('st-nota-pre').value.trim(),
      declino:     document.getElementById('st-nota-decl').value.trim(),
      vendida:     document.getElementById('st-nota-ok').value.trim()
    };

    spin(true);
    const r = await api('updateSale', {
      folio: currentSaleForStatus.folio,
      estado: estadoSeleccionado,
      comentarios: nuevosComentarios,
      // Compatibilidad: también guardamos notaEstado con el comentario activo
      notaEstado: nuevosComentarios[estadoSeleccionado] || ''
    });
    spin(false);

    if(!r.ok){ alert('Error al guardar: '+r.error); return; }

    document.getElementById('st-modal').classList.remove('show');
    currentSaleForStatus = null;

    // Refrescar la vista actual
    if (document.getElementById('pg-dash').classList.contains('on')) {
      renderDashTable();
    } else {
      renderRecent();
    }
    return;
  }
  if(e.target.id==='st-detail-close'){
    document.getElementById('st-detail-pop').classList.remove('show');
    return;
  }
});

document.addEventListener('keydown',function(e){
  if(e.key==='Enter'&&document.getElementById('login-screen').style.display!=='none')doLogin();
  if(e.key==='Escape'){
    document.getElementById('st-modal').classList.remove('show');
    document.getElementById('st-detail-pop').classList.remove('show');
  }
});
document.addEventListener('input',function(e){
  if(e.target.id==='d-search'||e.target.id==='d-filt')renderDashTable();
  // Resaltar el bloque de comentario del estado seleccionado
  if(e.target.name==='st-radio'){
    // handled via change below
  }
});
document.addEventListener('change',function(e){
  if(e.target.name==='st-radio') highlightActiveComment(e.target.value);
});
function highlightActiveComment(estado){
  const map = {pendiente:'pend',preasignado:'pre',declino:'decl',vendida:'ok'};
  document.querySelectorAll('.st-comment-block').forEach(b=>{
    b.classList.toggle('highlighted', b.dataset.estado === estado);
  });
}

/* ── ARRANQUE ── */
document.getElementById('login-screen').style.display='flex';
</script>

<!-- ════════ STATUS MODAL ════════ -->
<div class="st-modal" id="st-modal">
  <div class="st-box">
    <h3>Estado de la venta</h3>
    <p id="st-modal-client">Cliente: —</p>

    <div class="st-opts">
      <label class="st-opt">
        <input type="radio" name="st-radio" value="pendiente">
        <div><div class="st-opt-label">📞 Pendiente de llamar</div><div class="st-opt-sub">El cliente aún no ha sido contactado</div></div>
      </label>
      <label class="st-opt">
        <input type="radio" name="st-radio" value="declino">
        <div><div class="st-opt-label">❌ Declinó</div><div class="st-opt-sub">El cliente no quiso la tarjeta</div></div>
      </label>
      <label class="st-opt">
        <input type="radio" name="st-radio" value="preasignado">
        <div><div class="st-opt-label">⭐ Preasignado</div><div class="st-opt-sub">Cliente con oferta de tarjeta ya asignada</div></div>
      </label>
      <label class="st-opt">
        <input type="radio" name="st-radio" value="vendida">
        <div><div class="st-opt-label">✅ Vendida</div><div class="st-opt-sub">Tarjeta contratada exitosamente</div></div>
      </label>
    </div>

    <!-- COMENTARIOS POR ESTADO (uno por cada estado) -->
    <div class="st-comments-section">
      <div class="st-comments-header">💬 Comentarios por estado</div>

      <div class="st-comment-block" data-estado="pendiente">
        <div class="st-comment-label pend">📞 Pendiente <span class="st-req-badge">REQUERIDO</span></div>
        <textarea id="st-nota-pend" placeholder="Ej: No contestó, llamar el martes por la tarde. Le falta comprobante de domicilio…"></textarea>
        <div class="st-comment-hint">¿Qué pasó? ¿Cuándo volver a llamar? ¿Qué necesita el cliente?</div>
      </div>

      <div class="st-comment-block" data-estado="preasignado">
        <div class="st-comment-label pre">⭐ Preasignado</div>
        <textarea id="st-nota-pre" placeholder="Ej: Cliente tiene oferta Oro asignada. Línea $45,000. Confirmar entrega viernes…"></textarea>
        <div class="st-comment-hint">Detalles de la oferta asignada, línea de crédito, condiciones especiales.</div>
      </div>

      <div class="st-comment-block" data-estado="declino">
        <div class="st-comment-label decl">❌ Declinó <span class="st-req-badge">REQUERIDO</span></div>
        <textarea id="st-nota-decl" placeholder="Ej: Ya tiene muchas tarjetas. Prefirió esperar. No calificó por historial…"></textarea>
        <div class="st-comment-hint">¿Por qué declinó? Esto ayuda a mejorar el proceso.</div>
      </div>

      <div class="st-comment-block" data-estado="vendida">
        <div class="st-comment-label ok">✅ Vendida</div>
        <textarea id="st-nota-ok" placeholder="Ej: Contratada Oro $40,000. Activación en 5 días. Cliente muy satisfecho…"></textarea>
        <div class="st-comment-hint">Detalles del cierre: tipo, línea, condiciones, observaciones finales.</div>
      </div>
    </div>

    <div class="st-btns">
      <button class="st-cancel" id="st-cancel">Cancelar</button>
      <button class="st-save" id="st-save">Guardar estado</button>
    </div>
  </div>
</div>

<!-- ════════ STATUS DETAIL POPUP ════════ -->
<div class="st-detail-pop" id="st-detail-pop">
  <div class="st-detail-box">
    <h3>Comentario</h3>
    <div class="st-detail-txt" id="st-detail-txt"></div>
    <div style="margin-top:1.25rem;text-align:right;">
      <button class="st-cancel" id="st-detail-close">Cerrar</button>
    </div>
  </div>
</div>

</body>
</html>
</html>
