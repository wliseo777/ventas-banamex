<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>WLISEOS — Sistema de Ventas</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --pri:#7C3AED;--pri-d:#5B21B6;--pri-l:#9D5BF5;--pri-f:rgba(124,58,237,.16);
  --gold:#F0C060;--gold-d:#C8A84B;--gold-f:rgba(240,192,96,.13);
  --green:#10D980;--green-f:rgba(16,217,128,.13);
  --red:#EF4444;--red-f:rgba(239,68,68,.14);
  --cyan:#06B6D4;--cyan-f:rgba(6,182,212,.13);
  --bg:#07090F;--s1:#0F1219;--s2:#161B26;--s3:#1D2535;
  --br:rgba(255,255,255,.06);--br2:rgba(255,255,255,.11);--br3:rgba(255,255,255,.18);
  --tx:#EBF1FF;--mu:#637A9F;--mu2:#8BA3C0;
  --blue-f:rgba(59,130,246,.13);
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'Outfit',sans-serif;background:var(--bg);color:var(--tx);min-height:100vh;}

/* ── LOGIN ── */
#login-screen{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:1.5rem;background:radial-gradient(ellipse 80% 60% at 50% -10%,rgba(124,58,237,.18),transparent);}
.login-box{width:100%;max-width:400px;background:var(--s1);border:1px solid rgba(124,58,237,.35);border-radius:22px;padding:2.6rem 2.2rem;box-shadow:0 0 60px rgba(124,58,237,.1),0 30px 60px rgba(0,0,0,.5);}
.l-logo{font-family:'Bebas Neue',sans-serif;font-size:2.4rem;letter-spacing:.06em;text-align:center;margin-bottom:.2rem;background:linear-gradient(135deg,#fff 30%,var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
.l-sub{text-align:center;color:var(--mu);font-size:12px;margin-bottom:2rem;letter-spacing:.04em;}
.lf{display:flex;flex-direction:column;gap:6px;margin-bottom:1rem;}
.lf label{font-size:10px;font-weight:600;color:var(--mu);text-transform:uppercase;letter-spacing:.08em;}
.lf input{background:var(--s2);border:1px solid var(--br2);border-radius:10px;padding:12px 15px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:14px;outline:none;transition:border-color .2s,box-shadow .2s;width:100%;}
.lf input:focus{border-color:var(--pri);box-shadow:0 0 0 3px var(--pri-f);}
.lf input::placeholder{color:#2e3a52;}
.l-btn{width:100%;padding:13px;background:linear-gradient(135deg,var(--pri),var(--pri-d));border:none;border-radius:11px;color:#fff;font-family:'Outfit',sans-serif;font-size:15px;font-weight:600;cursor:pointer;transition:all .2s;margin-top:.5rem;box-shadow:0 4px 20px rgba(124,58,237,.4);}
.l-btn:hover{transform:translateY(-1px);box-shadow:0 6px 28px rgba(124,58,237,.55);}
.l-btn:active{transform:scale(.98);}
.l-err{display:none;margin-top:1rem;padding:10px 14px;background:var(--red-f);border:1px solid rgba(239,68,68,.3);border-radius:9px;color:#fca5a5;font-size:13px;text-align:center;}
.l-err.show{display:block;}

/* ── NAV ── */
#app{display:none;}
nav{display:flex;align-items:center;justify-content:space-between;padding:0 1.5rem;height:56px;background:rgba(15,18,25,.9);backdrop-filter:blur(16px);border-bottom:1px solid var(--br);position:sticky;top:0;z-index:50;}
nav::after{content:'';position:absolute;bottom:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(--pri-f),var(--pri-f),transparent);}
.n-logo{font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:.07em;background:linear-gradient(135deg,#fff,var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
.n-right{display:flex;align-items:center;gap:8px;}
.n-user{font-size:12px;color:var(--mu);background:var(--s2);border:1px solid var(--br2);border-radius:8px;padding:5px 11px;}
.n-user strong{color:var(--tx);}
.n-tabs{display:flex;gap:3px;flex-wrap:wrap;}
.tab{padding:6px 14px;border-radius:8px;border:none;font-family:'Outfit',sans-serif;font-size:12px;font-weight:500;cursor:pointer;transition:all .18s;background:transparent;color:var(--mu);}
.tab:hover{color:var(--tx);background:var(--s2);}
.tab.on{background:var(--pri-f);color:#c4b5fd;border:1px solid rgba(124,58,237,.3);}
.tab.gold.on{background:var(--gold-f);color:var(--gold);border:1px solid rgba(240,192,96,.3);}
.out-btn{padding:6px 13px;border-radius:8px;border:1px solid var(--br2);background:transparent;color:var(--mu);font-family:'Outfit',sans-serif;font-size:12px;cursor:pointer;transition:all .15s;}
.out-btn:hover{color:var(--tx);border-color:var(--br3);}

/* ── PAGES ── */
.pg{display:none;}
.pg.on{display:block;}
.wrap{max-width:580px;margin:0 auto;padding:2rem 1.5rem;}
.wide{max-width:1160px;margin:0 auto;padding:2rem 1.5rem;}
.pgtitle{font-family:'Bebas Neue',sans-serif;font-size:2.3rem;letter-spacing:.03em;line-height:1;margin-bottom:.35rem;}
.pgtitle span{color:var(--pri-l);}
.pgtitle.gt span{color:var(--gold);}
.pgsub{color:var(--mu);font-size:13px;margin-bottom:1.75rem;}
.spinner-overlay{position:fixed;inset:0;background:rgba(0,0,0,.7);display:none;align-items:center;justify-content:center;z-index:999;}
.spinner-overlay.show{display:flex;}
.spinner{width:40px;height:40px;border:3px solid var(--br2);border-top-color:var(--pri);border-radius:50%;animation:spin .7s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}

/* ── CARDS / FORMS ── */
.card{background:var(--s1);border:1px solid var(--br2);border-radius:18px;padding:1.8rem;}
.field{display:flex;flex-direction:column;gap:6px;margin-bottom:1rem;}
.field label{font-size:10px;font-weight:600;color:var(--mu);text-transform:uppercase;letter-spacing:.08em;}
.field input,.field select,.field textarea{background:var(--s2);border:1px solid var(--br2);border-radius:10px;padding:11px 14px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:14px;outline:none;transition:border-color .18s,box-shadow .18s;width:100%;}
.field input:focus,.field select:focus,.field textarea:focus{border-color:var(--pri);box-shadow:0 0 0 3px var(--pri-f);}
.field select option{background:#161B26;}
.field input::placeholder,.field textarea::placeholder{color:#2e3a52;}
.field textarea{resize:vertical;min-height:70px;line-height:1.5;}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.frow{display:flex;gap:10px;align-items:flex-end;margin-bottom:1rem;}
.frow .field{flex:1;margin-bottom:0;}
.folio-pill{background:var(--s2);border:1px solid var(--br2);border-radius:10px;padding:11px 14px;font-size:11px;color:var(--gold);white-space:nowrap;font-weight:700;font-family:monospace;}
.sbtn{width:100%;padding:13px;background:linear-gradient(135deg,var(--pri),var(--pri-d));border:none;border-radius:11px;color:#fff;font-family:'Outfit',sans-serif;font-size:15px;font-weight:600;cursor:pointer;transition:all .2s;margin-top:.5rem;box-shadow:0 4px 20px rgba(124,58,237,.35);}
.sbtn:hover{transform:translateY(-1px);box-shadow:0 6px 28px rgba(124,58,237,.5);}
.sbtn:disabled{background:#1D2535;color:var(--mu);cursor:not-allowed;box-shadow:none;transform:none;}
.toast{display:none;margin-top:1rem;padding:12px 16px;border-radius:10px;font-size:13px;font-weight:500;text-align:center;}
.toast.ok{background:var(--green-f);border:1px solid rgba(16,217,128,.3);color:var(--green);}
.toast.err{background:var(--red-f);border:1px solid rgba(239,68,68,.3);color:#fca5a5;}
.toast.show{display:block;}
.slbl{font-size:10px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.08em;margin:1.5rem 0 8px;}

/* ── RECENT ITEMS ── */
.ri{display:flex;justify-content:space-between;align-items:flex-start;padding:12px 15px;background:var(--s1);border:1px solid var(--br);border-radius:12px;margin-bottom:6px;font-size:13px;gap:10px;transition:border-color .15s;}
.ri:hover{border-color:var(--br2);}
.ri-n{font-weight:600;color:var(--tx);}
.ri-m{color:var(--mu);font-size:12px;margin-top:2px;}
.ri-f{font-family:monospace;font-size:11px;color:var(--gold);white-space:nowrap;font-weight:700;}
.ri-actions{display:flex;flex-direction:column;align-items:flex-end;gap:5px;flex-shrink:0;}
.share-ri-btn{background:none;border:1px solid rgba(124,58,237,.35);border-radius:6px;color:#a78bfa;font-size:11px;padding:3px 8px;cursor:pointer;font-family:'Outfit',sans-serif;transition:all .15s;white-space:nowrap;}
.share-ri-btn:hover{background:var(--pri-f);border-color:rgba(124,58,237,.6);}

/* ── STATS GRID ── */
.sgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(145px,1fr));gap:10px;margin-bottom:1.5rem;}
.sc{background:var(--s1);border:1px solid var(--br);border-radius:14px;padding:1rem 1.1rem;position:relative;overflow:hidden;}
.sc::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(124,58,237,.04),transparent);pointer-events:none;}
.sc-l{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:.07em;font-weight:600;}
.sc-v{font-family:'Bebas Neue',sans-serif;font-size:2.3rem;letter-spacing:.03em;margin-top:2px;line-height:1;}
.cv-g{color:var(--gold);}
.cv-r{color:var(--red);}
.cv-gr{color:var(--green);}
.cv-p{color:var(--pri-l);}

/* ── SYNC BAR ── */
.sync-bar{display:flex;align-items:center;gap:8px;padding:8px 14px;background:var(--s2);border:1px solid var(--br);border-radius:10px;font-size:12px;color:var(--mu);margin-bottom:1rem;flex-wrap:wrap;}
.sync-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0;}
.sync-dot.ok{background:var(--green);box-shadow:0 0 6px var(--green);}
.sync-dot.err{background:var(--red);}
.sync-dot.loading{background:var(--gold);animation:pulse 1s infinite;}
@keyframes pulse{0%,100%{opacity:1;}50%{opacity:.3;}}
.srv-status{display:inline-flex;align-items:center;gap:5px;padding:3px 9px;border-radius:20px;font-size:10px;font-weight:600;margin-left:auto;}
.srv-ok{background:var(--green-f);border:1px solid rgba(16,217,128,.3);color:var(--green);}
.srv-err{background:var(--red-f);border:1px solid rgba(239,68,68,.3);color:#fca5a5;}
.srv-loading{background:var(--gold-f);border:1px solid rgba(240,192,96,.3);color:var(--gold);}

/* ── TABLE ── */
.tctrl{display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-bottom:1rem;}
.tctrl input,.tctrl select{background:var(--s1);border:1px solid var(--br2);border-radius:9px;padding:8px 12px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:13px;outline:none;transition:border-color .15s;}
.tctrl input:focus,.tctrl select:focus{border-color:var(--pri);}
.tctrl input{flex:1;min-width:180px;}
.ibtn{padding:8px 14px;border-radius:9px;border:1px solid var(--br2);background:transparent;color:var(--mu);font-family:'Outfit',sans-serif;font-size:12px;font-weight:500;cursor:pointer;transition:all .15s;}
.ibtn:hover{color:var(--tx);border-color:var(--br3);}
.ibtn.gold{border-color:rgba(240,192,96,.35);color:var(--gold);}
.ibtn.gold:hover{background:var(--gold-f);}
.ibtn.pri{border-color:rgba(124,58,237,.4);color:#c4b5fd;}
.ibtn.pri:hover{background:var(--pri-f);}
.ibtn.danger{border-color:rgba(239,68,68,.3);color:var(--red);}
.ibtn.danger:hover{background:var(--red-f);}
.twrap{background:var(--s1);border:1px solid var(--br2);border-radius:16px;overflow:auto;}
table{width:100%;border-collapse:collapse;min-width:720px;}
thead tr{background:var(--s2);}
th{padding:10px 14px;text-align:left;font-size:10px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.07em;border-bottom:1px solid var(--br);white-space:nowrap;}
td{padding:9px 14px;font-size:12px;border-bottom:1px solid var(--br);vertical-align:middle;}
tr:last-child td{border-bottom:none;}
tr:hover td{background:rgba(124,58,237,.03);}
.tdf{font-family:monospace;font-size:11px;color:var(--gold);font-weight:700;}
.tdb{font-weight:600;}
.tdm{color:var(--mu);font-size:11px;}
.badge{display:inline-block;padding:2px 9px;border-radius:5px;font-size:10px;font-weight:700;}
.b-r{background:var(--red-f);color:#fca5a5;}
.b-b{background:var(--blue-f);color:#93c5fd;}
.b-g{background:var(--gold-f);color:var(--gold);}
.b-p{background:var(--pri-f);color:#c4b5fd;}
.b-purple{background:rgba(168,85,247,.15);color:#a855f7;}
.b-green{background:var(--green-f);color:var(--green);}
.delbtn{background:transparent;border:none;color:#2e3a52;cursor:pointer;font-size:14px;padding:2px 6px;border-radius:4px;transition:color .15s;}
.delbtn:hover{color:var(--red);}
.share-td-btn{background:none;border:1px solid rgba(124,58,237,.3);border-radius:6px;color:#a78bfa;font-size:10px;padding:3px 7px;cursor:pointer;font-family:'Outfit',sans-serif;transition:all .15s;white-space:nowrap;}
.share-td-btn:hover{background:var(--pri-f);}
.empty{padding:3rem;text-align:center;color:var(--mu);font-size:14px;}

/* ── RANKING ── */
.rgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(195px,1fr));gap:8px;margin-top:8px;}
.rcard{background:var(--s1);border:1px solid var(--br);border-radius:12px;padding:12px 15px;display:flex;align-items:center;gap:12px;}
.rpos{font-family:'Bebas Neue',sans-serif;font-size:1.7rem;color:var(--mu);min-width:28px;}
.rp1{color:var(--gold);}
.rp2{color:#94a3b8;}
.rp3{color:#cd7f32;}
.rkn{font-size:13px;font-weight:600;}
.rkc{font-size:12px;color:var(--mu);}

/* ── USERS ── */
.twocol{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem;align-items:start;}
.ugrid{display:grid;gap:8px;margin-top:8px;}
.ucard{background:var(--s1);border:1px solid var(--br2);border-radius:13px;padding:12px 15px;display:flex;align-items:center;gap:12px;}
.uav{width:40px;height:40px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:13px;flex-shrink:0;}
.av-e{background:var(--pri-f);color:#c4b5fd;}
.av-a{background:var(--gold-f);color:var(--gold);}
.av-s{background:rgba(168,85,247,.2);color:#a855f7;}
.ui{flex:1;min-width:0;}
.un{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.ur{font-size:11px;color:var(--mu);margin-top:2px;}
.del-u{border:none;border-radius:7px;padding:5px 10px;font-family:'Outfit',sans-serif;font-size:11px;font-weight:600;cursor:pointer;transition:all .15s;background:var(--red-f);color:#fca5a5;white-space:nowrap;}
.del-u:hover{background:var(--red);color:#fff;}

/* ── ESTADO OPTS ── */
.estado-selector{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:1rem;}
.estado-opt{display:flex;align-items:center;gap:9px;background:var(--s2);border:2px solid var(--br2);border-radius:11px;padding:10px 12px;cursor:pointer;transition:border-color .15s,background .15s;}
.estado-opt input[type=radio]{accent-color:var(--gold);width:15px;height:15px;flex-shrink:0;}
.estado-opt.sel-pend{border-color:#fbbf24!important;background:rgba(251,191,36,.07);}
.estado-opt.sel-pre{border-color:#a855f7!important;background:rgba(168,85,247,.07);}
.estado-opt.sel-decl{border-color:var(--red)!important;background:rgba(239,68,68,.07);}
.estado-opt.sel-ok{border-color:var(--green)!important;background:rgba(16,217,128,.07);}
.estado-lbl{font-size:13px;font-weight:500;}
.estado-sub{font-size:10px;color:var(--mu);}
.req-alert{background:var(--red-f);border:1px solid rgba(239,68,68,.3);border-radius:9px;padding:10px 14px;font-size:12px;color:#fca5a5;margin-bottom:1rem;display:none;}
.req-alert.show{display:block;}

/* ── STATS SECTIONS ── */
.stats-section{background:var(--s1);border:1px solid var(--br2);border-radius:16px;padding:1.3rem;margin-bottom:1.3rem;}
.stats-section-title{font-size:11px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.08em;margin-bottom:1rem;}
.mini-table{width:100%;border-collapse:collapse;font-size:12px;}
.mini-table th{padding:7px 10px;text-align:left;color:var(--mu);font-size:10px;text-transform:uppercase;letter-spacing:.05em;border-bottom:1px solid var(--br);font-weight:700;}
.mini-table td{padding:7px 10px;border-bottom:1px solid var(--br);}
.mini-table tr:last-child td{border-bottom:none;}
.mini-table tr:hover td{background:rgba(124,58,237,.03);}
.exec-accordion{margin-bottom:8px;border:1px solid var(--br2);border-radius:12px;overflow:hidden;}
.exec-acc-head{display:flex;align-items:center;justify-content:space-between;padding:11px 15px;cursor:pointer;background:var(--s2);font-size:13px;font-weight:500;transition:background .15s;}
.exec-acc-head:hover{background:var(--s3);}
.exec-acc-body{display:none;padding:12px 15px;background:var(--s1);}
.exec-acc-body.open{display:block;}

/* ── TARJETAS ── */
.cards-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:1.25rem;margin-bottom:2rem;}
.tc{border-radius:20px;padding:1.5rem 1.6rem;position:relative;overflow:hidden;cursor:pointer;transition:transform .2s,box-shadow .2s;min-height:190px;display:flex;flex-direction:column;justify-content:space-between;box-shadow:0 10px 40px rgba(0,0,0,.6);}
.tc:hover{transform:translateY(-6px);box-shadow:0 24px 60px rgba(0,0,0,.7);}
.tc.sel{outline:3px solid rgba(255,255,255,.75);outline-offset:3px;}
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
.tc-titular{font-size:13px;color:#fff;font-weight:700;letter-spacing:.04em;}
.tc-logo{position:absolute;top:1.2rem;right:1.2rem;font-family:'Bebas Neue',sans-serif;font-size:.95rem;color:rgba(255,255,255,.9);letter-spacing:.06em;}
.tc-badge{position:absolute;top:1.2rem;left:50%;transform:translateX(-50%);background:rgba(0,0,0,.35);backdrop-filter:blur(6px);border:1px solid rgba(255,255,255,.2);border-radius:20px;padding:3px 11px;font-size:10px;font-weight:700;color:#fff;white-space:nowrap;}
.tc-mc{position:absolute;bottom:1.2rem;right:1.2rem;display:flex;}
.tc-mc span{width:22px;height:22px;border-radius:50%;opacity:.9;}
.tc-mc .r{background:#eb001b;}
.tc-mc .y{background:#f79e1b;margin-left:-9px;}
.card-detail{background:var(--s1);border:1px solid var(--br2);border-radius:18px;padding:1.8rem;margin-top:1.5rem;animation:fadeIn .2s ease;}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
.cd-top{display:flex;gap:1.25rem;align-items:flex-start;flex-wrap:wrap;margin-bottom:1.5rem;}
.cd-mini{border-radius:14px;padding:1rem 1.1rem;width:180px;min-height:110px;flex-shrink:0;display:flex;flex-direction:column;justify-content:space-between;}
.cd-title{font-family:'Bebas Neue',sans-serif;font-size:1.8rem;letter-spacing:.03em;flex:1;}
.cd-pts{font-size:12px;color:var(--mu);margin-top:.2rem;}
.cd-close{background:var(--s2);border:1px solid var(--br2);border-radius:9px;padding:6px 14px;font-family:'Outfit',sans-serif;font-size:12px;color:var(--mu);cursor:pointer;flex-shrink:0;align-self:flex-start;transition:all .15s;}
.cd-close:hover{border-color:var(--br3);color:var(--tx);}
.cd-nums{display:grid;grid-template-columns:repeat(auto-fill,minmax(135px,1fr));gap:8px;margin-bottom:1.25rem;}
.cd-n{background:var(--s2);border-radius:11px;padding:10px 12px;}
.cd-nl{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:.06em;font-weight:600;}
.cd-nv{font-size:14px;font-weight:700;margin-top:3px;}
.red{color:#fca5a5;}.green{color:var(--green);}.gold{color:var(--gold);}
.cd-sec{font-size:10px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.09em;margin:1.2rem 0 .6rem;}
.cd-bens{list-style:none;display:flex;flex-direction:column;gap:7px;}
.cd-bens li{display:flex;gap:10px;align-items:flex-start;font-size:13px;line-height:1.55;color:#ccc;background:var(--s2);border-radius:10px;padding:9px 12px;}
.cd-ico{font-size:15px;flex-shrink:0;margin-top:1px;}
.cd-bt{font-weight:700;color:var(--tx);display:block;margin-bottom:2px;}
.cd-reqs{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:7px;}
.cd-req{background:var(--s2);border-radius:9px;padding:8px 12px;font-size:12px;color:#ccc;display:flex;gap:8px;align-items:flex-start;}
.cd-nota{background:var(--gold-f);border:1px solid rgba(240,192,96,.2);border-radius:10px;padding:10px 14px;font-size:11px;color:#bbb;line-height:1.6;margin-top:1rem;}

/* ── STATUS BADGES ── */
.st-badge{display:inline-flex;align-items:center;gap:5px;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:700;cursor:pointer;transition:opacity .15s;white-space:nowrap;}
.st-badge:hover{opacity:.8;}
.st-pend{background:rgba(251,191,36,.15);border:1px solid rgba(251,191,36,.4);color:#fbbf24;}
.st-decl{background:var(--red-f);border:1px solid rgba(239,68,68,.4);color:#fca5a5;}
.st-pre{background:rgba(168,85,247,.15);border:1px solid rgba(168,85,247,.4);color:#a855f7;}
.st-ok{background:var(--green-f);border:1px solid rgba(16,217,128,.3);color:var(--green);}
.st-none{background:rgba(120,120,120,.1);border:1px solid rgba(120,120,120,.3);color:var(--mu);}

/* ── STATUS MODAL ── */
.st-modal{position:fixed;inset:0;background:rgba(0,0,0,.8);display:none;align-items:center;justify-content:center;z-index:999;padding:1rem;}
.st-modal.show{display:flex;}
.st-box{background:var(--s1);border:1px solid var(--br2);border-radius:20px;padding:2rem;max-width:480px;width:100%;max-height:92vh;overflow-y:auto;}
.st-box h3{font-family:'Bebas Neue',sans-serif;font-size:1.5rem;letter-spacing:.03em;margin-bottom:.3rem;}
.st-box p{font-size:13px;color:var(--mu);margin-bottom:1.25rem;line-height:1.6;}
.st-opts{display:flex;flex-direction:column;gap:8px;margin-bottom:1.25rem;}
.st-opt{display:flex;align-items:center;gap:10px;background:var(--s2);border:2px solid var(--br2);border-radius:11px;padding:11px 14px;cursor:pointer;transition:border-color .15s;}
.st-opt.chosen{border-color:var(--gold);}
.st-opt input[type=radio]{accent-color:var(--gold);width:16px;height:16px;flex-shrink:0;}
.st-opt-label{font-size:13px;font-weight:500;}
.st-opt-sub{font-size:11px;color:var(--mu);margin-top:2px;}
.st-comments-section{margin-bottom:1rem;}
.st-comments-header{font-size:10px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.07em;margin-bottom:10px;}
.st-comment-block{background:var(--s2);border:1px solid var(--br);border-radius:11px;padding:12px 14px;margin-bottom:8px;}
.st-comment-block.highlighted{border-color:rgba(240,192,96,.4);background:rgba(240,192,96,.04);}
.st-comment-label{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.07em;margin-bottom:6px;display:flex;align-items:center;gap:5px;}
.st-comment-label.pend{color:#fbbf24;}
.st-comment-label.pre{color:#a855f7;}
.st-comment-label.decl{color:#fca5a5;}
.st-comment-label.ok{color:var(--green);}
.st-comment-block textarea{width:100%;background:rgba(0,0,0,.2);border:1px solid var(--br2);border-radius:8px;padding:9px 12px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:13px;resize:vertical;min-height:65px;outline:none;line-height:1.5;}
.st-comment-block textarea:focus{border-color:var(--gold);}
.st-comment-block textarea::placeholder{color:#2e3a52;}
.st-req-badge{display:inline-block;padding:1px 7px;background:var(--red-f);border-radius:4px;color:#fca5a5;font-size:9px;font-weight:700;margin-left:4px;}
.st-btns{display:flex;gap:8px;justify-content:flex-end;margin-top:1.25rem;}
.st-save{padding:10px 22px;background:linear-gradient(135deg,var(--pri),var(--pri-d));border:none;border-radius:9px;color:#fff;font-family:'Outfit',sans-serif;font-size:14px;font-weight:700;cursor:pointer;transition:all .15s;}
.st-save:hover{box-shadow:0 4px 20px rgba(124,58,237,.5);}
.st-cancel{padding:10px 18px;background:transparent;border:1px solid var(--br2);border-radius:9px;color:var(--mu);font-family:'Outfit',sans-serif;font-size:13px;cursor:pointer;transition:all .15s;}
.st-cancel:hover{color:var(--tx);border-color:var(--br3);}
.st-detail-pop{position:fixed;inset:0;background:rgba(0,0,0,.8);display:none;align-items:center;justify-content:center;z-index:999;padding:1rem;}
.st-detail-pop.show{display:flex;}
.st-detail-box{background:var(--s1);border:1px solid var(--br2);border-radius:20px;padding:2rem;max-width:420px;width:100%;}
.st-detail-box h3{font-family:'Bebas Neue',sans-serif;font-size:1.4rem;margin-bottom:1rem;}
.st-detail-txt{font-size:14px;line-height:1.75;color:#ccc;background:var(--s2);border-radius:11px;padding:15px;}
.nota-preview{font-size:10px;color:var(--mu);margin-top:3px;max-width:220px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}

/* ── SHARE BADGES ── */
.shared-badge{display:inline-flex;align-items:center;gap:4px;padding:2px 8px;border-radius:5px;font-size:10px;font-weight:700;background:var(--cyan-f);border:1px solid rgba(6,182,212,.3);color:var(--cyan);margin-top:3px;}
.shared-out{background:rgba(168,85,247,.14);border:1px solid rgba(168,85,247,.3);color:#c084fc;}

/* ── SHARE MODAL ── */
.share-modal{position:fixed;inset:0;background:rgba(0,0,0,.8);display:none;align-items:center;justify-content:center;z-index:1000;padding:1rem;}
.share-modal.show{display:flex;}
.share-modal-box{background:var(--s1);border:1px solid rgba(124,58,237,.35);border-radius:20px;padding:2rem;max-width:380px;width:100%;box-shadow:0 0 60px rgba(124,58,237,.15);}
.share-modal-box h3{font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:.03em;margin-bottom:.3rem;}
.share-modal-box p{font-size:12px;color:var(--mu);margin-bottom:1.25rem;}

/* ── CHAT ── */
.chat-wrap{max-width:1100px;margin:0 auto;padding:1.5rem;}
.chat-layout{display:grid;grid-template-columns:280px 1fr;height:calc(100vh - 130px);min-height:500px;background:var(--s1);border:1px solid var(--br2);border-radius:18px;overflow:hidden;}
.chat-sidebar{border-right:1px solid var(--br);display:flex;flex-direction:column;overflow:hidden;background:var(--s2);}
.chat-sidebar-head{padding:.9rem 1rem;border-bottom:1px solid var(--br);display:flex;align-items:center;justify-content:space-between;flex-shrink:0;}
.chat-sidebar-title{font-family:'Bebas Neue',sans-serif;font-size:1.1rem;letter-spacing:.05em;color:var(--tx);}
.chat-new-btn{padding:5px 12px;border-radius:8px;border:1px solid rgba(124,58,237,.4);background:var(--pri-f);color:#c4b5fd;font-family:'Outfit',sans-serif;font-size:12px;font-weight:600;cursor:pointer;transition:all .15s;}
.chat-new-btn:hover{background:rgba(124,58,237,.25);}
.chat-contacts{flex:1;overflow-y:auto;}
.chat-contact{padding:.75rem 1rem;cursor:pointer;border-bottom:1px solid rgba(255,255,255,.03);display:flex;align-items:center;gap:10px;transition:background .12s;}
.chat-contact:hover{background:rgba(124,58,237,.07);}
.chat-contact.active{background:var(--pri-f);border-left:3px solid var(--pri);}
.chat-av{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:12px;flex-shrink:0;}
.cav-e{background:var(--pri-f);color:#c4b5fd;}
.cav-a{background:var(--gold-f);color:var(--gold);}
.cav-s{background:rgba(168,85,247,.2);color:#a855f7;}
.cav-all{background:var(--cyan-f);color:var(--cyan);font-size:16px;}
.chat-ci{flex:1;min-width:0;}
.chat-cn{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;color:var(--tx);}
.chat-cl{font-size:11px;color:var(--mu);margin-top:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.chat-unread{background:var(--pri);color:#fff;border-radius:10px;font-size:10px;font-weight:700;padding:1px 7px;min-width:18px;text-align:center;flex-shrink:0;}
.chat-main{display:flex;flex-direction:column;overflow:hidden;}
.chat-main-head{padding:.85rem 1.2rem;border-bottom:1px solid var(--br);display:flex;align-items:center;gap:12px;flex-shrink:0;background:var(--s1);}
.chat-main-title{font-size:14px;font-weight:700;color:var(--tx);}
.chat-main-sub{font-size:11px;color:var(--mu);}
.chat-msgs{flex:1;overflow-y:auto;padding:1.1rem 1.2rem;display:flex;flex-direction:column;gap:4px;background:var(--bg);}
.chat-day-sep{text-align:center;font-size:10px;color:var(--mu);padding:6px 0;position:relative;margin:6px 0;}
.chat-day-sep::before{content:'';position:absolute;top:50%;left:0;right:0;height:1px;background:var(--br);}
.chat-day-sep span{background:var(--bg);padding:0 10px;position:relative;}
.chat-msg-wrap{display:flex;flex-direction:column;}
.chat-msg-wrap.mine{align-items:flex-end;}
.chat-msg-wrap.theirs{align-items:flex-start;}
.chat-bname{font-size:10px;color:var(--mu);margin-bottom:3px;padding:0 4px;}
.chat-bubble{max-width:70%;padding:9px 14px;border-radius:16px;font-size:13px;line-height:1.6;word-break:break-word;}
.chat-bubble.mine{background:var(--pri);color:#fff;border-bottom-right-radius:5px;box-shadow:0 4px 16px rgba(124,58,237,.35);}
.chat-bubble.theirs{background:var(--s2);color:var(--tx);border-bottom-left-radius:5px;border:1px solid var(--br2);}
.chat-btime{font-size:10px;color:var(--mu);margin-top:3px;padding:0 4px;}
.chat-empty-state{flex:1;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:8px;color:var(--mu);}
.chat-empty-icon{font-size:2.5rem;margin-bottom:6px;}
.chat-input-area{padding:.85rem 1.2rem;border-top:1px solid var(--br);display:flex;gap:8px;align-items:flex-end;flex-shrink:0;background:var(--s1);}
.chat-input-area textarea{flex:1;background:var(--s2);border:1px solid var(--br2);border-radius:12px;padding:10px 14px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:13px;resize:none;outline:none;max-height:90px;min-height:40px;line-height:1.55;transition:border-color .15s;}
.chat-input-area textarea:focus{border-color:var(--pri);}
.chat-send{padding:10px 20px;background:linear-gradient(135deg,var(--pri),var(--pri-d));border:none;border-radius:12px;color:#fff;font-family:'Outfit',sans-serif;font-size:13px;font-weight:700;cursor:pointer;white-space:nowrap;transition:all .15s;box-shadow:0 4px 14px rgba(124,58,237,.4);}
.chat-send:hover{box-shadow:0 6px 20px rgba(124,58,237,.55);}
.chat-send:disabled{background:var(--s3);color:var(--mu);cursor:not-allowed;box-shadow:none;}
.chat-all-msg{background:var(--s2);border:1px solid var(--br);border-radius:11px;padding:10px 14px;margin-bottom:5px;}
.chat-all-meta{font-size:10px;color:var(--mu);display:flex;gap:6px;align-items:center;margin-bottom:4px;}
.chat-all-from{font-weight:700;color:var(--pri-l);}
.chat-all-to{color:var(--gold);}
.chat-all-text{font-size:13px;color:var(--tx);}
.chat-notice{background:var(--pri-f);border:1px solid rgba(124,58,237,.3);border-radius:10px;padding:12px 16px;font-size:13px;color:#c4b5fd;margin-bottom:1rem;text-align:center;}
@media(max-width:640px){
  nav{padding:0 .75rem;}
  .twocol{grid-template-columns:1fr;}
  .row2{grid-template-columns:1fr;}
  .estado-selector{grid-template-columns:1fr;}
  .chat-layout{grid-template-columns:1fr;height:auto;}
  .chat-sidebar{max-height:200px;border-right:none;border-bottom:1px solid var(--br);}
  .chat-msgs{min-height:300px;}
}
</style>
</head>
<body>
<div class="spinner-overlay" id="spinner"><div class="spinner"></div></div>

<div id="login-screen">
  <div class="login-box">
    <div class="l-logo">WLISEOS</div>
    <p class="l-sub">Sistema de Ventas · Inicia sesión</p>
    <div class="lf"><label>Usuario</label><input type="text" id="l-user" placeholder="tu usuario" autocomplete="username"></div>
    <div class="lf"><label>Contraseña</label><input type="password" id="l-pass" placeholder="••••••••" autocomplete="current-password"></div>
    <button class="l-btn" id="login-btn">Entrar al sistema</button>
    <div class="l-err" id="login-err"></div>
  </div>
</div>

<div id="app">
  <nav>
    <div class="n-logo">WLISEOS</div>
    <div class="n-tabs" id="n-tabs"></div>
    <div class="n-right">
      <div class="n-user">Hola, <strong id="nav-name"></strong></div>
      <button class="out-btn" id="logout-btn">Salir</button>
    </div>
  </nav>

  <!-- REGISTRAR VENTA -->
  <div id="pg-exec" class="pg">
    <div class="wrap">
      <div class="pgtitle">Nueva <span>venta</span></div>
      <p class="pgsub">Todos los campos marcados con * son obligatorios</p>
      <div class="card">
        <div class="row2">
          <div class="field"><label>Nombre del cliente *</label><input type="text" id="f-cliente" placeholder="Ej. María González"></div>
          <div class="field"><label>Teléfono del cliente</label><input type="tel" id="f-tel" placeholder="Ej. 5512345678" maxlength="15"></div>
        </div>
        <div class="row2">
          <div class="field">
            <label>Tipo de tarjeta *</label>
            <select id="f-tarjeta">
              <option value="">— Selecciona —</option>
              <option>Joy Banamex</option><option>Clásica Banamex</option><option>Teleton Banamex</option>
              <option>Oro Banamex</option><option>Descubre Banamex</option>
              <option>Platinum Banamex</option><option>Explora Banamex</option><option>Otra</option>
            </select>
          </div>
          <div class="field"><label>Fecha de venta *</label><input type="date" id="f-fecha"></div>
        </div>
        <div class="row2">
          <div class="field"><label>RFC del cliente (opcional)</label><input type="text" id="f-rfc" placeholder="Ej. GOMJ850101MDF"></div>
          <div class="field"><label>Ingresos mensuales (opcional)</label><input type="number" id="f-ingresos" placeholder="Ej. 25000" min="0"></div>
        </div>
        <div class="row2">
          <div class="field"><label>Tarjeta de referencia (opcional)</label><input type="text" id="f-tarjetaRef" placeholder="Ej. Clásica Banamex"></div>
          <div class="field"><label>Línea de crédito ref. (opcional)</label><input type="number" id="f-ldcRef" placeholder="Ej. 30000" min="0"></div>
        </div>
        <div class="field"><label>Estado de la venta *</label></div>
        <div class="estado-selector">
          <label class="estado-opt" id="eopt-pend"><input type="radio" name="f-estado" value="pendiente"><div><div class="estado-lbl">📞 Pendiente</div><div class="estado-sub">Sin contactar aún</div></div></label>
          <label class="estado-opt" id="eopt-pre"><input type="radio" name="f-estado" value="preasignado"><div><div class="estado-lbl">⭐ Preasignado</div><div class="estado-sub">Oferta ya asignada</div></div></label>
          <label class="estado-opt" id="eopt-decl"><input type="radio" name="f-estado" value="declino"><div><div class="estado-lbl">❌ Declinó</div><div class="estado-sub">No quiso la tarjeta</div></div></label>
          <label class="estado-opt" id="eopt-ok"><input type="radio" name="f-estado" value="vendida"><div><div class="estado-lbl">✅ Vendida</div><div class="estado-sub">Contratada exitosamente</div></div></label>
        </div>
        <div class="field"><label>Comentario de la gestión *</label><textarea id="f-comentario" placeholder="Describe el resultado de la gestión con este cliente…" rows="3"></textarea></div>
        <div class="req-alert" id="req-alert"></div>
        <div class="frow">
          <div class="field"><label>Folio (automático si lo dejas vacío)</label><input type="text" id="f-folio" placeholder="WLS-000001" maxlength="20"></div>
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

  <!-- ESTADÍSTICAS -->
  <div id="pg-stats" class="pg">
    <div class="wide">
      <div class="pgtitle">Estadísticas <span>equipo</span></div>
      <p class="pgsub" id="stats-sub">Cargando…</p>
      <div class="stats-section">
        <div class="stats-section-title">🌐 Globales del equipo</div>
        <div class="sgrid" id="stats-global-cards"></div>
        <div class="row2" style="gap:1rem">
          <div><div class="slbl" style="margin-top:0">Por tarjeta</div><div class="twrap"><table class="mini-table"><thead><tr><th>Tarjeta</th><th>Total</th><th>Vendidas</th></tr></thead><tbody id="stats-global-tarjeta"></tbody></table></div></div>
          <div><div class="slbl" style="margin-top:0">Por estado</div><div class="twrap"><table class="mini-table"><thead><tr><th>Estado</th><th>Cant.</th><th>%</th></tr></thead><tbody id="stats-global-estado"></tbody></table></div></div>
        </div>
      </div>
      <div class="stats-section" id="stats-mis-section">
        <div class="stats-section-title">👤 Mis ventas</div>
        <div class="sgrid" id="stats-mis-cards"></div>
        <div class="row2" style="gap:1rem">
          <div><div class="slbl" style="margin-top:0">Por tarjeta</div><div class="twrap"><table class="mini-table"><thead><tr><th>Tarjeta</th><th>Cant.</th></tr></thead><tbody id="stats-mis-tarjeta"></tbody></table></div></div>
          <div><div class="slbl" style="margin-top:0">Por estado</div><div class="twrap"><table class="mini-table"><thead><tr><th>Estado</th><th>Cant.</th></tr></thead><tbody id="stats-mis-estado"></tbody></table></div></div>
        </div>
      </div>
      <div class="stats-section" id="stats-exec-section" style="display:none">
        <div class="stats-section-title">👥 Por ejecutivo</div>
        <div id="stats-exec-list"></div>
      </div>
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
      <p class="pgsub">Todas las ventas del equipo en tiempo real</p>
      <div class="sync-bar">
        <div class="sync-dot loading" id="sync-dot"></div>
        <span id="sync-txt">Cargando…</span>
        <span class="srv-status srv-loading" id="srv-status">⏳ Servidor…</span>
      </div>
      <div class="sgrid">
        <div class="sc"><div class="sc-l">Total ventas</div><div class="sc-v cv-g" id="s-tot">—</div></div>
        <div class="sc"><div class="sc-l">Ejecutivos activos</div><div class="sc-v cv-p" id="s-exe">—</div></div>
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
        <button class="ibtn gold" id="export-btn">📊 Excel</button>
        <button class="ibtn danger" id="clear-btn">Borrar todo</button>
      </div>
      <div class="twrap">
        <table>
          <thead><tr><th>Folio</th><th>Ejecutivo</th><th>Cliente</th><th>Teléfono</th><th>Tarjeta</th><th>Estado</th><th>Comentario</th><th>Compartida</th><th>Fecha</th><th>Registrado</th><th></th></tr></thead>
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
      <p class="pgsub">Agrega o elimina usuarios del equipo.</p>
      <div class="twocol">
        <div class="card">
          <div style="font-size:14px;font-weight:600;margin-bottom:1.2rem;">Agregar usuario</div>
          <div class="field"><label>Nombre completo</label><input type="text" id="nu-name" placeholder="Ej. Juan Pérez"></div>
          <div class="field"><label>Usuario</label><input type="text" id="nu-user" placeholder="Ej. jperez" autocomplete="off"></div>
          <div class="field"><label>Contraseña</label><input type="password" id="nu-pass" placeholder="Mínimo 4 caracteres"></div>
          <div class="field" id="nu-role-wrap" style="display:none">
            <label>Rol</label>
            <select id="nu-role"><option value="exec">Ejecutivo</option><option value="admin">Admin</option></select>
          </div>
          <button class="sbtn" id="add-user-btn">Agregar usuario</button>
          <div class="toast ok" id="u-ok"></div>
          <div class="toast err" id="u-err"></div>
        </div>
        <div>
          <div class="slbl" style="margin-top:0">Usuarios registrados</div>
          <div class="ugrid" id="ugrid"></div>
        </div>
      </div>
    </div>
  </div>

  <!-- CHAT -->
  <div id="pg-chat" class="pg">
    <div class="chat-wrap">
      <div class="pgtitle">Chat del <span>equipo</span></div>
      <p class="pgsub" id="chat-sub">Mensajes en tiempo real</p>
      <div class="chat-layout">
        <div class="chat-sidebar">
          <div class="chat-sidebar-head">
            <span class="chat-sidebar-title">Conversaciones</span>
            <button class="chat-new-btn" id="chat-new-btn">+ Nuevo</button>
          </div>
          <div class="chat-contacts" id="chat-contacts"></div>
        </div>
        <div class="chat-main">
          <div class="chat-main-head" id="chat-main-head" style="display:none">
            <div class="chat-av cav-e" id="chat-head-av">?</div>
            <div><div class="chat-main-title" id="chat-head-name">—</div><div class="chat-main-sub" id="chat-head-sub">—</div></div>
          </div>
          <div class="chat-msgs" id="chat-msgs">
            <div class="chat-empty-state"><div class="chat-empty-icon">💬</div><span style="font-weight:600">Selecciona una conversación</span><span style="font-size:12px">o presiona "+ Nuevo" para comenzar</span></div>
          </div>
          <div class="chat-input-area" id="chat-input-area" style="display:none">
            <textarea id="chat-input" placeholder="Escribe un mensaje… (Enter para enviar)" rows="1"></textarea>
            <button class="chat-send" id="chat-send-btn">Enviar ↑</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- STATUS MODAL -->
<div class="st-modal" id="st-modal">
  <div class="st-box">
    <h3>Actualizar estado</h3>
    <p id="st-modal-client">Cliente: —</p>
    <div class="st-opts">
      <label class="st-opt"><input type="radio" name="st-radio" value="pendiente"><div><div class="st-opt-label">📞 Pendiente</div><div class="st-opt-sub">Sin contactar aún</div></div></label>
      <label class="st-opt"><input type="radio" name="st-radio" value="declino"><div><div class="st-opt-label">❌ Declinó</div><div class="st-opt-sub">No quiso la tarjeta</div></div></label>
      <label class="st-opt"><input type="radio" name="st-radio" value="preasignado"><div><div class="st-opt-label">⭐ Preasignado</div><div class="st-opt-sub">Oferta ya asignada</div></div></label>
      <label class="st-opt"><input type="radio" name="st-radio" value="vendida"><div><div class="st-opt-label">✅ Vendida</div><div class="st-opt-sub">Contratada exitosamente</div></div></label>
    </div>
    <div class="st-comments-section">
      <div class="st-comments-header">💬 Comentario del estado seleccionado <span class="st-req-badge">REQUERIDO</span></div>
      <div class="st-comment-block" data-estado="pendiente"><div class="st-comment-label pend">📞 Pendiente</div><textarea id="st-nota-pend" placeholder="Ej: No contestó, llamar el martes…"></textarea></div>
      <div class="st-comment-block" data-estado="preasignado"><div class="st-comment-label pre">⭐ Preasignado</div><textarea id="st-nota-pre" placeholder="Ej: Oferta Oro $45,000 asignada…"></textarea></div>
      <div class="st-comment-block" data-estado="declino"><div class="st-comment-label decl">❌ Declinó</div><textarea id="st-nota-decl" placeholder="Ej: Ya tiene muchas tarjetas…"></textarea></div>
      <div class="st-comment-block" data-estado="vendida"><div class="st-comment-label ok">✅ Vendida</div><textarea id="st-nota-ok" placeholder="Ej: Contratada Oro $40,000…"></textarea></div>
    </div>
    <div class="st-btns"><button class="st-cancel" id="st-cancel">Cancelar</button><button class="st-save" id="st-save">Guardar</button></div>
  </div>
</div>

<div class="st-detail-pop" id="st-detail-pop">
  <div class="st-detail-box">
    <h3>Comentario</h3>
    <div class="st-detail-txt" id="st-detail-txt"></div>
    <div style="margin-top:1.25rem;text-align:right;"><button class="st-cancel" id="st-detail-close">Cerrar</button></div>
  </div>
</div>

<!-- SHARE MODAL -->
<div class="share-modal" id="share-modal">
  <div class="share-modal-box">
    <h3>📤 Compartir venta</h3>
    <p id="share-modal-desc">Selecciona el ejecutivo con quien compartir esta venta.</p>
    <div class="field"><label>Ejecutivo</label><select id="share-user-select"></select></div>
    <div class="st-btns"><button class="st-cancel" id="share-cancel">Cancelar</button><button class="st-save" id="share-confirm">Compartir</button></div>
  </div>
</div>

<!-- CHAT NEW MODAL -->
<div class="share-modal" id="chat-modal">
  <div class="share-modal-box">
    <h3>💬 Nueva conversación</h3>
    <p>Selecciona con quién quieres chatear.</p>
    <div class="field"><label>Ejecutivo</label><select id="chat-user-select"></select></div>
    <div class="st-btns"><button class="st-cancel" id="chat-modal-cancel">Cancelar</button><button class="st-save" id="chat-modal-ok">Abrir chat</button></div>
  </div>
</div>

<script>
const API_URL='https://domelike-rubdown-hatching.ngrok-free.dev';
const FIXED_ACCOUNTS=[{username:'wliseo',password:'wliseo777',name:'Wliseo',role:'superadmin'}];

// ── API ──
async function api(action,body={}){
  try{
    const h={'Content-Type':'application/json','ngrok-skip-browser-warning':'true'};
    if(action==='getSales'){const r=await fetch(`${API_URL}/api/ventas`,{headers:h});setDbStatus(true);const d=await r.json();return{ok:true,data:d.filter(v=>!v._chat)};}
    if(action==='addSale'){const r=await fetch(`${API_URL}/api/ventas`,{method:'POST',headers:h,body:JSON.stringify(body)});setDbStatus(true);return await r.json();}
    if(action==='deleteSale'){await fetch(`${API_URL}/api/ventas/${body.folio}`,{method:'DELETE',headers:h});setDbStatus(true);return{ok:true};}
    if(action==='clearSales'){await fetch(`${API_URL}/api/ventas`,{method:'DELETE',headers:h});setDbStatus(true);return{ok:true};}
    if(action==='updateSale'){const r=await fetch(`${API_URL}/api/ventas/${body.folio}`,{method:'PUT',headers:h,body:JSON.stringify(body)});setDbStatus(true);return await r.json();}
    if(action==='getUsers'){const r=await fetch(`${API_URL}/api/usuarios`,{headers:h});setDbStatus(true);return{ok:true,data:await r.json()};}
    if(action==='addUser'){const r=await fetch(`${API_URL}/api/usuarios`,{method:'POST',headers:h,body:JSON.stringify(body)});setDbStatus(true);return await r.json();}
    if(action==='deleteUser'){await fetch(`${API_URL}/api/usuarios/${body.username}`,{method:'DELETE',headers:h});setDbStatus(true);return{ok:true};}
    // CHAT usa el mismo endpoint de ventas con _chat:true
    if(action==='getChats'){const r=await fetch(`${API_URL}/api/ventas`,{headers:h});setDbStatus(true);const d=await r.json();return{ok:true,data:d.filter(v=>v._chat===true)};}
    if(action==='sendChat'){const r=await fetch(`${API_URL}/api/ventas`,{method:'POST',headers:h,body:JSON.stringify(body)});setDbStatus(true);return await r.json();}
    return{ok:false,error:'Acción desconocida'};
  }catch(e){setDbStatus(false);return{ok:false,error:'Sin conexión: '+e.message};}
}
function setDbStatus(ok){const el=document.getElementById('srv-status');if(!el)return;el.className=ok?'srv-status srv-ok':'srv-status srv-err';el.textContent=ok?'✓ Servidor conectado':'✕ Sin conexión';}

// ── GLOBALS ──
let CU=null,SALES_CACHE=[],USERS_CACHE=[],currentSaleForStatus=null;
let CHAT_MSGS=[],CHAT_ACTIVE=null,CHAT_POLL=null;
let _shareFolio=null;

// ── UTILS ──
function esc(s){return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}
function fmt(ts){if(!ts)return'—';const d=new Date(ts);return d.toLocaleDateString('es-MX',{day:'2-digit',month:'short',year:'numeric'})+' '+d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});}
function fmtDate(s){if(!s)return'—';const[y,m,d]=s.split('-');const M=['Ene','Feb','Mar','Abr','May','Jun','Jul','Ago','Sep','Oct','Nov','Dic'];return`${parseInt(d)} ${M[parseInt(m)-1]} ${y}`;}
function ini(n){return(n||'?').trim().split(/\s+/).slice(0,2).map(w=>w[0]||'').join('').toUpperCase()||'?';}
function genFolio(){return'WLS-'+String(Date.now()).slice(-6);}
function spin(on){document.getElementById('spinner').classList.toggle('show',on);}
function showToast(id,msg,type){const el=document.getElementById(id);if(!el)return;el.textContent=msg;el.className='toast '+type+' show';clearTimeout(el._t);el._t=setTimeout(()=>el.classList.remove('show'),4500);}
function getComentarioActivo(sale){if(!sale.comentarios)return sale.notaEstado||'';return sale.comentarios[sale.estado||'pendiente']||'';}
function estadoClase(e){return{'pendiente':'pend','declino':'decl','preasignado':'pre','vendida':'ok'}[e]||'none';}
function estadoTexto(e){return{'pendiente':'📞 Pendiente','declino':'❌ Declinó','preasignado':'⭐ Preasignado','vendida':'✅ Vendida'}[e]||'⬜ Sin estado';}
function isAdmin(){return CU&&(CU.role==='admin'||CU.role==='superadmin');}
function fmtChatTime(ts){if(!ts)return'';const d=new Date(ts),now=new Date();if(d.toDateString()===now.toDateString())return d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});return d.toLocaleDateString('es-MX',{day:'2-digit',month:'short'})+' '+d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});}
function chatLastRead(c){try{return parseInt(localStorage.getItem('wls_cr_'+CU.username+'_'+c)||'0');}catch{return 0;}}
function chatMarkRead(c){try{localStorage.setItem('wls_cr_'+CU.username+'_'+c,Date.now());}catch{}}

// ── LOGIN ──
async function doLogin(){
  const u=(document.getElementById('l-user').value||'').trim().toLowerCase();
  const p=document.getElementById('l-pass').value;
  const errEl=document.getElementById('login-err');
  errEl.classList.remove('show');
  if(!u||!p){errEl.textContent='Escribe usuario y contraseña';errEl.classList.add('show');return;}
  const fixed=FIXED_ACCOUNTS.find(x=>x.username===u&&x.password===p);
  if(fixed){CU={...fixed};await bootApp();return;}
  spin(true);const r=await api('getUsers');spin(false);
  if(!r.ok){errEl.textContent='Error de conexión: '+r.error;errEl.classList.add('show');return;}
  USERS_CACHE=r.data||[];
  const found=USERS_CACHE.find(x=>x.username.toLowerCase()===u&&x.password===p);
  if(found){CU={...found};await bootApp();return;}
  errEl.textContent=USERS_CACHE.length===0?'Sin usuarios. Contacta al administrador.':'Usuario o contraseña incorrectos';
  errEl.classList.add('show');
}
function doLogout(){CU=null;SALES_CACHE=[];stopChatPoll();document.getElementById('app').style.display='none';document.getElementById('login-screen').style.display='flex';document.getElementById('l-user').value='';document.getElementById('l-pass').value='';}

async function bootApp(){
  document.getElementById('login-screen').style.display='none';
  document.getElementById('app').style.display='block';
  document.getElementById('nav-name').textContent=CU.name;
  buildNav();buildBenPanels();
  if(isAdmin())await goPage('dash');
  else await goPage('exec');
}

function buildNav(){
  const tabs=document.getElementById('n-tabs');
  if(isAdmin()){
    tabs.innerHTML='<button class="tab gold" data-pg="dash">Dashboard</button><button class="tab gold" data-pg="stats">Estadísticas</button><button class="tab gold" data-pg="ben">Beneficios</button><button class="tab gold" data-pg="users">Usuarios</button><button class="tab gold" data-pg="chat">💬 Chat</button>';
  }else{
    tabs.innerHTML='<button class="tab" data-pg="exec">Registrar</button><button class="tab" data-pg="stats">Estadísticas</button><button class="tab" data-pg="ben">Beneficios</button><button class="tab" data-pg="chat">💬 Chat</button>';
  }
  document.querySelectorAll('.tab').forEach(btn=>btn.addEventListener('click',()=>goPage(btn.dataset.pg)));
  const rw=document.getElementById('nu-role-wrap');
  if(rw)rw.style.display=CU.role==='superadmin'?'flex':'none';
}

async function goPage(p){
  stopChatPoll();
  document.querySelectorAll('.pg').forEach(el=>el.classList.remove('on'));
  document.querySelectorAll('.tab').forEach(el=>el.classList.remove('on'));
  document.getElementById('pg-'+p)?.classList.add('on');
  const tb=document.querySelector(`.tab[data-pg="${p}"]`);if(tb)tb.classList.add('on');
  if(p==='exec'){setTodayDate();refreshFolio();await renderRecent();}
  if(p==='stats')await renderStats();
  if(p==='dash')await loadAndRenderDash();
  if(p==='users')await loadAndRenderUsers();
  if(p==='chat')await initChat();
}
function setTodayDate(){const el=document.getElementById('f-fecha');if(el&&!el.value)el.value=new Date().toISOString().slice(0,10);}
function refreshFolio(){const el=document.getElementById('folio-pill');if(el)el.textContent=genFolio();}

document.addEventListener('change',function(e){
  if(e.target.name==='f-estado'){
    const map={pendiente:'eopt-pend',preasignado:'eopt-pre',declino:'eopt-decl',vendida:'eopt-ok'};
    const selMap={pendiente:'sel-pend',preasignado:'sel-pre',declino:'sel-decl',vendida:'sel-ok'};
    Object.values(map).forEach(id=>{const el=document.getElementById(id);if(el)el.className='estado-opt';});
    const sel=map[e.target.value];if(sel){const el=document.getElementById(sel);if(el)el.className='estado-opt '+selMap[e.target.value];}
  }
  if(e.target.name==='st-radio')
    document.querySelectorAll('.st-comment-block').forEach(b=>b.classList.toggle('highlighted',b.dataset.estado===e.target.value));
});

// ── REGISTRAR VENTA ──
async function registrarVenta(){
  const cliente=(document.getElementById('f-cliente').value||'').trim();
  const tel=(document.getElementById('f-tel').value||'').trim();
  const tarjeta=document.getElementById('f-tarjeta').value;
  const fecha=document.getElementById('f-fecha').value;
  const estadoEl=document.querySelector('input[name="f-estado"]:checked');
  const estado=estadoEl?estadoEl.value:'';
  const comentario=(document.getElementById('f-comentario').value||'').trim();
  let folio=(document.getElementById('f-folio').value||'').trim();
  const rfc=(document.getElementById('f-rfc').value||'').trim();
  const ingresos=(document.getElementById('f-ingresos').value||'').trim();
  const tarjetaRef=(document.getElementById('f-tarjetaRef').value||'').trim();
  const ldcRef=(document.getElementById('f-ldcRef').value||'').trim();
  const alertEl=document.getElementById('req-alert');alertEl.classList.remove('show');
  if(!cliente){alertEl.textContent='⚠ Escribe el nombre del cliente';alertEl.classList.add('show');return;}
  if(!tarjeta){alertEl.textContent='⚠ Selecciona el tipo de tarjeta';alertEl.classList.add('show');return;}
  if(!fecha){alertEl.textContent='⚠ Selecciona la fecha de venta';alertEl.classList.add('show');return;}
  if(!estado){alertEl.textContent='⚠ Selecciona el estado de la venta';alertEl.classList.add('show');return;}
  if(!comentario){alertEl.textContent='⚠ Escribe un comentario sobre esta gestión';alertEl.classList.add('show');return;}
  if(!folio)folio=genFolio();
  document.getElementById('reg-btn').disabled=true;spin(true);
  const comentarios={pendiente:'',preasignado:'',declino:'',vendida:''};comentarios[estado]=comentario;
  const payload={folio,exec:CU.name,username:CU.username,cliente,tel,tarjeta,fecha,registrado:new Date().toISOString(),rfc:rfc||null,ingresos:ingresos||null,tarjetaRef:tarjetaRef||null,ldcRef:ldcRef||null,estado,comentarios,notaEstado:comentario};
  const r=await api('addSale',payload);
  spin(false);document.getElementById('reg-btn').disabled=false;
  if(!r.ok){alertEl.textContent='Error: '+r.error;alertEl.classList.add('show');return;}
  ['f-cliente','f-tel','f-folio','f-rfc','f-ingresos','f-tarjetaRef','f-ldcRef','f-comentario'].forEach(id=>{const el=document.getElementById(id);if(el)el.value='';});
  document.getElementById('f-tarjeta').value='';
  document.getElementById('f-fecha').value=new Date().toISOString().slice(0,10);
  document.querySelectorAll('input[name="f-estado"]').forEach(r=>r.checked=false);
  ['eopt-pend','eopt-pre','eopt-decl','eopt-ok'].forEach(id=>{const el=document.getElementById(id);if(el)el.className='estado-opt';});
  refreshFolio();
  showToast('t-ok','✓ Venta registrada · Folio '+folio,'ok');
  await renderRecent();
}

// ── COMPARTIR VENTA EXISTENTE ──
window.openShareModal=function(folio){
  _shareFolio=folio;
  const sale=SALES_CACHE.find(v=>v.folio===folio);
  const desc=sale?`Cliente: ${sale.cliente} · Folio: ${folio}`:`Folio: ${folio}`;
  document.getElementById('share-modal-desc').textContent=desc;
  // Populate user select
  const sel=document.getElementById('share-user-select');
  const users=getAllUsers();
  sel.innerHTML=users.map(u=>`<option value="${esc(u.username)}">${esc(u.name)} (@${esc(u.username)})</option>`).join('');
  if(sale&&sale.sharedWith)sel.value=sale.sharedWith;
  document.getElementById('share-modal').classList.add('show');
};

async function doShareSale(){
  if(!_shareFolio)return;
  const sel=document.getElementById('share-user-select');
  const targetUsername=sel.value;
  if(!targetUsername){alert('Selecciona un ejecutivo.');return;}
  document.getElementById('share-confirm').disabled=true;
  spin(true);
  // Get current sale data and update with sharedWith
  const r2=await api('getSales');
  let sale=null;
  if(r2.ok)sale=r2.data.find(v=>v.folio===_shareFolio);
  // Also check SALES_CACHE if not found
  if(!sale)sale=SALES_CACHE.find(v=>v.folio===_shareFolio);
  if(!sale){spin(false);document.getElementById('share-confirm').disabled=false;alert('No se encontró la venta.');return;}
  const payload={...sale,sharedWith:targetUsername};
  const r=await api('updateSale',payload);
  spin(false);document.getElementById('share-confirm').disabled=false;
  document.getElementById('share-modal').classList.remove('show');
  _shareFolio=null;
  if(!r.ok){alert('Error al compartir: '+r.error);return;}
  const targetUser=getAllUsers().find(u=>u.username===targetUsername);
  const tname=targetUser?targetUser.name:targetUsername;
  // Refresh appropriate view
  if(document.getElementById('pg-exec').classList.contains('on'))await renderRecent();
  if(document.getElementById('pg-dash').classList.contains('on'))await loadAndRenderDash();
  alert(`✓ Venta compartida con ${tname} (@${targetUsername})`);
}

// ── RENDER RECENT ──
async function renderRecent(){
  const list=document.getElementById('exec-recent');
  list.innerHTML='<p style="color:var(--mu);font-size:13px">Cargando…</p>';
  const r=await api('getSales');
  if(!r.ok){list.innerHTML='<p style="color:#fca5a5;font-size:13px">Error al cargar.</p>';return;}
  const data=r.data.filter(v=>v.username===CU.username||(v.sharedWith&&v.sharedWith===CU.username)).slice(0,12);
  if(!data.length){list.innerHTML='<p style="color:var(--mu);font-size:13px">Aún no tienes ventas registradas.</p>';return;}
  list.innerHTML=data.map(v=>{
    const com=getComentarioActivo(v);
    const isMine=v.username===CU.username;
    const sharedBadge=!isMine?`<span class="shared-badge">📥 De @${esc(v.username)}</span>`:
      v.sharedWith?`<span class="shared-badge shared-out">📤 @${esc(v.sharedWith)}</span>`:'';
    return`<div class="ri">
      <div style="flex:1;min-width:0">
        <div class="ri-n">${esc(v.cliente)}${v.rfc?' 📄':''}${v.ingresos?' 💰':''}</div>
        <div class="ri-m">${esc(v.tarjeta)}${v.tel?' · '+esc(v.tel):''} · ${fmtDate(v.fecha)}</div>
        ${sharedBadge}
        ${com?`<div class="nota-preview" title="${esc(com)}">💬 ${esc(com)}</div>`:''}
      </div>
      <div class="ri-actions">
        <span class="ri-f">${esc(v.folio)}</span>
        <span class="st-badge st-${estadoClase(v.estado)}" onclick="openStatusModalFromFolio('${esc(v.folio)}')">${estadoTexto(v.estado)}</span>
        <button class="share-ri-btn" onclick="openShareModalWithUsers('${esc(v.folio)}')">📤 Compartir</button>
      </div>
    </div>`;
  }).join('');
}

// Open share modal loading users first
window.openShareModalWithUsers=async function(folio){
  if(USERS_CACHE.length===0){spin(true);const r=await api('getUsers');spin(false);if(r.ok)USERS_CACHE=r.data||[];}
  if(!SALES_CACHE.length){spin(true);const r=await api('getSales');spin(false);if(r.ok)SALES_CACHE=r.data||[];}
  openShareModal(folio);
};

function getAllUsers(){
  const all=[];
  FIXED_ACCOUNTS.forEach(u=>{if(u.username!==CU.username)all.push({username:u.username,name:u.name,role:u.role});});
  USERS_CACHE.forEach(u=>{if(u.username!==CU.username&&!all.find(x=>x.username===u.username))all.push({username:u.username,name:u.name,role:u.role});});
  return all;
}

const eLabels={'pendiente':'📞 Pendiente','preasignado':'⭐ Preasignado','declino':'❌ Declinó','vendida':'✅ Vendida'};

// ── STATS ──
async function renderStats(){
  const r=await api('getSales');if(!r.ok)return;
  const all=r.data;
  const misVentas=all.filter(v=>v.username===CU.username);
  const today=new Date().toDateString();
  document.getElementById('stats-sub').textContent=isAdmin()?'Vista completa del equipo':'Tu rendimiento y estadísticas globales';
  const vendidas=all.filter(v=>v.estado==='vendida').length;
  const pct=all.length?Math.round(vendidas/all.length*100):0;
  document.getElementById('stats-global-cards').innerHTML=`
    <div class="sc"><div class="sc-l">Total equipo</div><div class="sc-v cv-g">${all.length}</div></div>
    <div class="sc"><div class="sc-l">Hoy</div><div class="sc-v cv-gr">${all.filter(v=>v.registrado&&new Date(v.registrado).toDateString()===today).length}</div></div>
    <div class="sc"><div class="sc-l">Esta semana</div><div class="sc-v cv-p">${all.filter(v=>v.registrado&&new Date(v.registrado).getTime()>Date.now()-7*86400000).length}</div></div>
    <div class="sc"><div class="sc-l">Vendidas ✅</div><div class="sc-v cv-gr">${vendidas}<span style="font-size:1rem;color:var(--mu)"> (${pct}%)</span></div></div>
  `;
  const byT={};all.forEach(v=>{if(!byT[v.tarjeta])byT[v.tarjeta]={t:0,v:0};byT[v.tarjeta].t++;if(v.estado==='vendida')byT[v.tarjeta].v++;});
  document.getElementById('stats-global-tarjeta').innerHTML=Object.entries(byT).sort((a,b)=>b[1].t-a[1].t).map(([t,c])=>`<tr><td>${esc(t)}</td><td><strong>${c.t}</strong></td><td style="color:var(--green)">${c.v}</td></tr>`).join('')||'<tr><td colspan="3" style="color:var(--mu);text-align:center">Sin datos</td></tr>';
  const byE={pendiente:0,preasignado:0,declino:0,vendida:0};all.forEach(v=>{const e=v.estado||'pendiente';byE[e]=(byE[e]||0)+1;});
  document.getElementById('stats-global-estado').innerHTML=Object.entries(byE).map(([e,c])=>`<tr><td>${eLabels[e]}</td><td><strong>${c}</strong></td><td style="color:var(--mu)">${all.length?Math.round(c/all.length*100):0}%</td></tr>`).join('');
  const misSec=document.getElementById('stats-mis-section');
  if(isAdmin()){misSec.style.display='none';}else{
    misSec.style.display='block';
    const mv=misVentas;
    document.getElementById('stats-mis-cards').innerHTML=`
      <div class="sc"><div class="sc-l">Mis ventas</div><div class="sc-v cv-g">${mv.length}</div></div>
      <div class="sc"><div class="sc-l">Hoy</div><div class="sc-v cv-gr">${mv.filter(v=>v.registrado&&new Date(v.registrado).toDateString()===today).length}</div></div>
      <div class="sc"><div class="sc-l">Esta semana</div><div class="sc-v cv-p">${mv.filter(v=>v.registrado&&new Date(v.registrado).getTime()>Date.now()-7*86400000).length}</div></div>
      <div class="sc"><div class="sc-l">Vendidas ✅</div><div class="sc-v cv-gr">${mv.filter(v=>v.estado==='vendida').length}</div></div>
    `;
    const misByT={};mv.forEach(v=>{misByT[v.tarjeta]=(misByT[v.tarjeta]||0)+1;});
    document.getElementById('stats-mis-tarjeta').innerHTML=Object.entries(misByT).sort((a,b)=>b[1]-a[1]).map(([t,c])=>`<tr><td>${esc(t)}</td><td><strong>${c}</strong></td></tr>`).join('')||'<tr><td colspan="2" style="color:var(--mu);text-align:center">Sin datos</td></tr>';
    const misByE={pendiente:0,preasignado:0,declino:0,vendida:0};mv.forEach(v=>{const e=v.estado||'pendiente';misByE[e]=(misByE[e]||0)+1;});
    document.getElementById('stats-mis-estado').innerHTML=Object.entries(misByE).map(([e,c])=>`<tr><td>${eLabels[e]}</td><td><strong>${c}</strong></td></tr>`).join('');
  }
  const execSec=document.getElementById('stats-exec-section');
  if(isAdmin()){
    execSec.style.display='block';
    const byExec={};all.forEach(v=>{if(!byExec[v.exec])byExec[v.exec]=[];byExec[v.exec].push(v);});
    const list=document.getElementById('stats-exec-list');
    if(!Object.keys(byExec).length){list.innerHTML='<p style="color:var(--mu);font-size:13px">Sin ventas registradas aún.</p>';return;}
    list.innerHTML=Object.entries(byExec).sort((a,b)=>b[1].length-a[1].length).map(([name,vs])=>{
      const vend=vs.filter(v=>v.estado==='vendida').length;
      const hoyE=vs.filter(v=>v.registrado&&new Date(v.registrado).toDateString()===today).length;
      const semE=vs.filter(v=>v.registrado&&new Date(v.registrado).getTime()>Date.now()-7*86400000).length;
      const byTE={};vs.forEach(v=>{byTE[v.tarjeta]=(byTE[v.tarjeta]||0)+1;});
      const byEE={pendiente:0,preasignado:0,declino:0,vendida:0};vs.forEach(v=>{const e=v.estado||'pendiente';byEE[e]=(byEE[e]||0)+1;});
      return`<div class="exec-accordion">
        <div class="exec-acc-head" onclick="this.nextElementSibling.classList.toggle('open');this.querySelector('.arr').textContent=this.nextElementSibling.classList.contains('open')?'▲':'▼'">
          <span style="font-weight:600">${esc(name)}</span>
          <span style="display:flex;gap:8px;align-items:center">
            <span class="badge b-b">${vs.length} ventas</span><span class="badge b-green">${vend} vendidas</span>
            <span class="arr" style="color:var(--mu);font-size:12px">▼</span>
          </span>
        </div>
        <div class="exec-acc-body">
          <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(110px,1fr));gap:8px;margin-bottom:10px">
            <div class="sc" style="padding:.6rem .9rem"><div class="sc-l">Total</div><div class="sc-v cv-g" style="font-size:1.5rem">${vs.length}</div></div>
            <div class="sc" style="padding:.6rem .9rem"><div class="sc-l">Hoy</div><div class="sc-v cv-gr" style="font-size:1.5rem">${hoyE}</div></div>
            <div class="sc" style="padding:.6rem .9rem"><div class="sc-l">Semana</div><div class="sc-v cv-p" style="font-size:1.5rem">${semE}</div></div>
            <div class="sc" style="padding:.6rem .9rem"><div class="sc-l">Vendidas</div><div class="sc-v cv-gr" style="font-size:1.5rem">${vend}</div></div>
          </div>
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
            <div><div class="slbl" style="margin-top:0">Por tarjeta</div><table class="mini-table"><thead><tr><th>Tarjeta</th><th>Cant.</th></tr></thead><tbody>${Object.entries(byTE).sort((a,b)=>b[1]-a[1]).map(([t,c])=>`<tr><td>${esc(t)}</td><td><strong>${c}</strong></td></tr>`).join('')}</tbody></table></div>
            <div><div class="slbl" style="margin-top:0">Por estado</div><table class="mini-table"><thead><tr><th>Estado</th><th>Cant.</th></tr></thead><tbody>${Object.entries(byEE).map(([e,c])=>`<tr><td style="font-size:11px">${eLabels[e]}</td><td><strong>${c}</strong></td></tr>`).join('')}</tbody></table></div>
          </div>
        </div>
      </div>`;
    }).join('');
  }else{execSec.style.display='none';}
}

// ── DASHBOARD ──
function setSyncStatus(s,msg){const dot=document.getElementById('sync-dot');const txt=document.getElementById('sync-txt');if(!dot)return;dot.className='sync-dot '+s;txt.textContent=msg;}

async function loadAndRenderDash(){
  setSyncStatus('loading','Cargando datos…');
  const r=await api('getSales');
  if(!r.ok){setSyncStatus('err','Error: '+r.error);return;}
  SALES_CACHE=r.data||[];
  setSyncStatus('ok','Sincronizado · '+SALES_CACHE.length+' ventas');
  renderDashTable();
}

window.openStatusModalFromFolio=function(folio){
  let sale=SALES_CACHE.find(v=>v.folio===folio);
  if(sale){openStatusModal(sale);return;}
  api('getSales').then(r=>{if(r.ok){const s=r.data.find(v=>v.folio===folio);if(s)openStatusModal(s);}});
};

function openStatusModal(sale){
  currentSaleForStatus=sale;
  document.getElementById('st-modal-client').textContent=`Cliente: ${sale.cliente} — Folio: ${sale.folio}`;
  const estado=sale.estado||'pendiente';
  const radio=document.querySelector(`input[name="st-radio"][value="${estado}"]`);if(radio)radio.checked=true;
  const comentarios=sale.comentarios||{};const legacy=sale.notaEstado||'';
  document.getElementById('st-nota-pend').value=comentarios.pendiente||(estado==='pendiente'?legacy:'');
  document.getElementById('st-nota-pre').value=comentarios.preasignado||(estado==='preasignado'?legacy:'');
  document.getElementById('st-nota-decl').value=comentarios.declino||(estado==='declino'?legacy:'');
  document.getElementById('st-nota-ok').value=comentarios.vendida||(estado==='vendida'?legacy:'');
  document.querySelectorAll('.st-comment-block').forEach(b=>b.classList.toggle('highlighted',b.dataset.estado===estado));
  document.getElementById('st-modal').classList.add('show');
}

function renderDashTable(){
  const search=(document.getElementById('d-search').value||'').toLowerCase();
  const ft=document.getElementById('d-filt').value;
  const all=SALES_CACHE;let data=all.slice();
  if(search)data=data.filter(v=>(v.exec||'').toLowerCase().includes(search)||(v.cliente||'').toLowerCase().includes(search)||(v.folio||'').toLowerCase().includes(search));
  if(ft)data=data.filter(v=>v.tarjeta===ft);
  document.getElementById('s-tot').textContent=all.length;
  document.getElementById('s-exe').textContent=new Set(all.map(v=>v.username)).size;
  const today=new Date().toDateString();
  document.getElementById('s-hoy').textContent=all.filter(v=>v.registrado&&new Date(v.registrado).toDateString()===today).length;
  document.getElementById('s-sem').textContent=all.filter(v=>v.registrado&&new Date(v.registrado).getTime()>Date.now()-7*86400000).length;
  const tbody=document.getElementById('t-body');const empty=document.getElementById('t-empty');
  if(!data.length){tbody.innerHTML='';empty.style.display='block';}
  else{
    empty.style.display='none';
    tbody.innerHTML=data.map(v=>{
      const com=getComentarioActivo(v);
      const sharedCell=v.sharedWith?`<span class="badge b-p">@${esc(v.sharedWith)}</span>`:'<span style="color:#2e3a52">—</span>';
      return`<tr>
        <td class="tdf">${esc(v.folio)}</td>
        <td class="tdb">${esc(v.exec)}</td>
        <td>${esc(v.cliente)}</td>
        <td class="tdm">${esc(v.tel||'—')}</td>
        <td><span class="badge b-r">${esc(v.tarjeta)}</span></td>
        <td><span class="st-badge st-${estadoClase(v.estado)}" onclick="openStatusModalFromFolio('${esc(v.folio)}')">${estadoTexto(v.estado)}</span></td>
        <td class="tdm" style="max-width:160px;">${com?`<span style="cursor:pointer;color:#ccc;" onclick="showStatusNote('${com.replace(/'/g,"\\'")}')" title="${esc(com)}">💬 ${esc(com.slice(0,38))}${com.length>38?'…':''}</span>`:'<span style="color:#2e3a52">—</span>'}</td>
        <td>${sharedCell}</td>
        <td class="tdm">${fmtDate(v.fecha)}</td>
        <td class="tdm">${fmt(v.registrado)}</td>
        <td style="display:flex;gap:5px;align-items:center;"><button class="share-td-btn" onclick="openShareModalWithUsers('${esc(v.folio)}')">📤</button><button class="delbtn" data-folio="${esc(v.folio)}">✕</button></td>
      </tr>`;
    }).join('');
  }
  const counts={};all.forEach(v=>{counts[v.exec]=(counts[v.exec]||0)+1;});
  const sorted=Object.entries(counts).sort((a,b)=>b[1]-a[1]).slice(0,12);
  const pc=['rp1','rp2','rp3'];
  document.getElementById('rank-grid').innerHTML=sorted.length?sorted.map(([name,cnt],i)=>`<div class="rcard"><div class="rpos ${pc[i]||''}">${i+1}</div><div><div class="rkn">${esc(name)}</div><div class="rkc">${cnt} venta${cnt!==1?'s':''}</div></div></div>`).join(''):'<p style="color:var(--mu);font-size:13px">Sin datos aún.</p>';
}

window.showStatusNote=function(nota){document.getElementById('st-detail-txt').textContent=nota;document.getElementById('st-detail-pop').classList.add('show');};

async function delSale(folio){
  if(!confirm('¿Eliminar la venta con folio '+folio+'?'))return;
  spin(true);const r=await api('deleteSale',{folio});spin(false);
  if(!r.ok){alert('Error: '+r.error);return;}
  SALES_CACHE=SALES_CACHE.filter(v=>v.folio!==folio);renderDashTable();setSyncStatus('ok','Sincronizado · '+SALES_CACHE.length+' ventas');
}

function exportarExcel(){
  if(!SALES_CACHE.length){alert('No hay ventas para exportar.');return;}
  const cols=['Folio','Ejecutivo','Cliente','Teléfono','Tarjeta','Estado','Comentario','Compartida con','Fecha Venta','Registrado','RFC','Ingresos','Tarjeta Ref','LDC Ref'];
  const rows=SALES_CACHE.map(v=>[v.folio,v.exec,v.cliente,v.tel||'',v.tarjeta,v.estado||'',getComentarioActivo(v).replace(/"/g,"'"),v.sharedWith||'',fmtDate(v.fecha),fmt(v.registrado),v.rfc||'',v.ingresos||'',v.tarjetaRef||'',v.ldcRef||''].map(c=>`"${c}"`).join(','));
  const csv=[cols.map(c=>`"${c}"`).join(','),...rows].join('\n');
  const blob=new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'});
  const url=URL.createObjectURL(blob);const a=document.createElement('a');a.href=url;a.download='wliseos_ventas_'+new Date().toISOString().slice(0,10)+'.csv';a.click();URL.revokeObjectURL(url);
}

// ── USUARIOS ──
async function loadAndRenderUsers(){
  spin(true);const r=await api('getUsers');spin(false);
  if(!r.ok){showToast('u-err','Error al cargar usuarios','err');return;}
  USERS_CACHE=r.data||[];renderUsersUI();
}
function renderUsersUI(){
  const isSup=CU.role==='superadmin';
  const fixedCards=FIXED_ACCOUNTS.map(u=>`<div class="ucard"><div class="uav av-s">${ini(u.name)}</div><div class="ui"><div class="un">${esc(u.name)}</div><div class="ur"><span class="badge b-purple">@${esc(u.username)} · superadmin</span></div></div></div>`).join('');
  const userCards=USERS_CACHE.length?USERS_CACHE.map(u=>{const rl=u.role==='admin'?'admin':'ejecutivo';const bc=u.role==='admin'?'b-g':'b-p';return`<div class="ucard"><div class="uav av-e">${ini(u.name)}</div><div class="ui"><div class="un">${esc(u.name)}</div><div class="ur"><span class="badge ${bc}">@${esc(u.username)} · ${rl}</span></div></div>${isSup?`<button class="del-u" data-uname="${esc(u.username)}">Eliminar</button>`:''}</div>`;}).join(''):'<p style="color:var(--mu);font-size:13px;margin-top:4px">No hay usuarios agregados aún.</p>';
  document.getElementById('ugrid').innerHTML=fixedCards+userCards;
}
async function addUser(){
  const name=(document.getElementById('nu-name').value||'').trim();
  const username=(document.getElementById('nu-user').value||'').trim().toLowerCase().replace(/\s+/g,'');
  const password=document.getElementById('nu-pass').value;
  const role=CU.role==='superadmin'?(document.getElementById('nu-role').value||'exec'):'exec';
  if(!name||!username||!password){showToast('u-err','Completa todos los campos','err');return;}
  if(password.length<4){showToast('u-err','Contraseña mínimo 4 caracteres','err');return;}
  if(FIXED_ACCOUNTS.find(x=>x.username===username)){showToast('u-err','Ese usuario está reservado','err');return;}
  document.getElementById('add-user-btn').disabled=true;
  spin(true);const r=await api('addUser',{name,username,password,role});spin(false);
  document.getElementById('add-user-btn').disabled=false;
  if(!r.ok){showToast('u-err',r.error||'Error','err');return;}
  document.getElementById('nu-name').value='';document.getElementById('nu-user').value='';document.getElementById('nu-pass').value='';
  showToast('u-ok','Usuario "'+name+'" agregado','ok');await loadAndRenderUsers();
}

// ── CHAT (almacena mensajes en /api/ventas con _chat:true) ──
async function initChat(){
  if(USERS_CACHE.length===0){const r=await api('getUsers');if(r.ok)USERS_CACHE=r.data||[];}
  document.getElementById('chat-sub').textContent=isAdmin()?'Vista de admin · todos los mensajes del equipo':'Mensajes privados en tiempo real';
  const r=await api('getChats');
  CHAT_MSGS=r.ok?(r.data||[]):[];
  renderChatSidebar();
  if(CHAT_ACTIVE)renderChatMessages();
  startChatPoll();
  document.getElementById('chat-new-btn').onclick=openChatNewModal;
  document.getElementById('chat-send-btn').onclick=sendChatMsg;
  document.getElementById('chat-input').onkeydown=function(e){if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();sendChatMsg();}};
}
function stopChatPoll(){if(CHAT_POLL){clearInterval(CHAT_POLL);CHAT_POLL=null;}}
function startChatPoll(){
  stopChatPoll();
  CHAT_POLL=setInterval(async()=>{
    if(!document.getElementById('pg-chat').classList.contains('on'))return;
    const r=await api('getChats');
    if(r.ok){const old=CHAT_MSGS.length;CHAT_MSGS=r.data||[];renderChatSidebar();if(CHAT_ACTIVE)renderChatMessages(CHAT_MSGS.length!==old);}
  },4000);
}

function getMyChatConversations(){
  const convMap={};
  if(isAdmin()){
    // Admin sees all conversations
    CHAT_MSGS.forEach(m=>{
      const key=[m.from,m.to].sort().join('__');
      if(!convMap[key]){
        convMap[key]={key,from:m.from,fromName:m.fromName,to:m.to,toName:m.toName,messages:[]};
      }
      convMap[key].messages.push(m);
    });
    return Object.values(convMap).sort((a,b)=>{
      const ta=a.messages[a.messages.length-1]?.timestamp||'';
      const tb=b.messages[b.messages.length-1]?.timestamp||'';
      return tb.localeCompare(ta);
    });
  }else{
    // Exec sees only their conversations
    CHAT_MSGS.forEach(m=>{
      if(m.from!==CU.username&&m.to!==CU.username)return;
      const other=m.from===CU.username?m.to:m.from;
      const otherName=m.from===CU.username?m.toName:m.fromName;
      if(!convMap[other])convMap[other]={other,otherName,messages:[]};
      convMap[other].messages.push(m);
    });
    return Object.values(convMap).sort((a,b)=>{
      const ta=a.messages[a.messages.length-1]?.timestamp||'';
      const tb=b.messages[b.messages.length-1]?.timestamp||'';
      return tb.localeCompare(ta);
    });
  }
}

function renderChatSidebar(){
  const cont=document.getElementById('chat-contacts');
  const convs=getMyChatConversations();
  let html='';
  if(isAdmin()){
    const allActive=CHAT_ACTIVE&&CHAT_ACTIVE._type==='all';
    html+=`<div class="chat-contact${allActive?' active':''}" onclick="selectChatView('__all__')">
      <div class="chat-av cav-all">📋</div>
      <div class="chat-ci"><div class="chat-cn">Todos los mensajes</div><div class="chat-cl">${CHAT_MSGS.length} mensajes · solo lectura</div></div>
    </div>`;
    // Show all known users too
    getAllUsers().forEach(u=>{
      const myConv=convs.find(c=>c.key&&(c.from===u.username||c.to===u.username));
      const lastMsg=myConv?myConv.messages[myConv.messages.length-1]:null;
      const lr=chatLastRead(u.username);
      const unread=myConv?myConv.messages.filter(m=>m.from!==CU.username&&new Date(m.timestamp).getTime()>lr).length:0;
      const isAct=CHAT_ACTIVE&&CHAT_ACTIVE.username===u.username;
      html+=chatContactHTML(u.username,u.name,u.role,lastMsg?.text||'Sin mensajes',unread,isAct);
    });
  }else{
    if(!convs.length){html='<div style="padding:1.2rem;text-align:center;color:var(--mu);font-size:12px">Sin conversaciones aún.<br>Presiona "+ Nuevo"</div>';}
    else{
      convs.forEach(c=>{
        const lr=chatLastRead(c.other);
        const unread=c.messages.filter(m=>m.from!==CU.username&&new Date(m.timestamp).getTime()>lr).length;
        const isAct=CHAT_ACTIVE&&CHAT_ACTIVE.username===c.other;
        const lastText=c.messages[c.messages.length-1]?.text||'';
        html+=chatContactHTML(c.other,c.otherName,'exec',lastText,unread,isAct);
      });
    }
  }
  cont.innerHTML=html;
}

function chatContactHTML(username,name,role,lastText,unread,isActive){
  const avClass=role==='superadmin'?'cav-s':role==='admin'?'cav-a':'cav-e';
  const av=ini(name||username);
  const roleTag=role==='admin'||role==='superadmin'?`<span style="font-size:9px;background:var(--gold-f);color:var(--gold);border-radius:3px;padding:1px 4px;margin-left:4px;font-weight:700;">${role==='superadmin'?'SUPER':'ADMIN'}</span>`:'';
  return`<div class="chat-contact${isActive?' active':''}" onclick="selectChatWithUser('${esc(username)}','${esc(name||username)}','${role}')">
    <div class="chat-av ${avClass}">${av}</div>
    <div class="chat-ci">
      <div class="chat-cn">${esc(name||username)}${roleTag}</div>
      <div class="chat-cl">${esc((lastText||'').slice(0,40))}</div>
    </div>
    ${unread>0?`<div class="chat-unread">${unread}</div>`:''}
  </div>`;
}

window.selectChatView=function(type){
  CHAT_ACTIVE={_type:'all'};
  renderChatSidebar();
  const head=document.getElementById('chat-main-head');head.style.display='flex';
  document.getElementById('chat-head-av').className='chat-av cav-all';
  document.getElementById('chat-head-av').textContent='📋';
  document.getElementById('chat-head-name').textContent='Todos los mensajes';
  document.getElementById('chat-head-sub').textContent='Vista de administrador · solo lectura';
  document.getElementById('chat-input-area').style.display='none';
  renderChatMessages();
};

window.selectChatWithUser=function(username,name,role){
  CHAT_ACTIVE={username,name,role};
  chatMarkRead(username);
  renderChatSidebar();
  const head=document.getElementById('chat-main-head');head.style.display='flex';
  const avClass=role==='superadmin'?'cav-s':role==='admin'?'cav-a':'cav-e';
  document.getElementById('chat-head-av').className='chat-av '+avClass;
  document.getElementById('chat-head-av').textContent=ini(name||username);
  document.getElementById('chat-head-name').textContent=name||username;
  document.getElementById('chat-head-sub').textContent='@'+username;
  document.getElementById('chat-input-area').style.display='flex';
  renderChatMessages();
  document.getElementById('chat-input').focus();
};

function renderChatMessages(scroll=true){
  const el=document.getElementById('chat-msgs');
  if(!CHAT_ACTIVE){return;}
  if(CHAT_ACTIVE._type==='all'){
    // Admin: show all messages
    const msgs=[...CHAT_MSGS].sort((a,b)=>a.timestamp.localeCompare(b.timestamp));
    if(!msgs.length){el.innerHTML='<div class="chat-empty-state"><div class="chat-empty-icon">📭</div><span>Sin mensajes aún en el equipo</span></div>';return;}
    el.innerHTML=msgs.map(m=>`<div class="chat-all-msg">
      <div class="chat-all-meta"><span class="chat-all-from">${esc(m.fromName||m.from)}</span><span>→</span><span class="chat-all-to">${esc(m.toName||m.to)}</span><span style="margin-left:auto;font-size:10px">${fmtChatTime(m.timestamp)}</span></div>
      <div class="chat-all-text">${esc(m.text)}</div>
    </div>`).join('');
  }else{
    const msgs=CHAT_MSGS.filter(m=>(m.from===CU.username&&m.to===CHAT_ACTIVE.username)||(m.from===CHAT_ACTIVE.username&&m.to===CU.username)).sort((a,b)=>a.timestamp.localeCompare(b.timestamp));
    if(!msgs.length){el.innerHTML=`<div class="chat-empty-state"><div class="chat-empty-icon">💬</div><span style="font-weight:600">Chat con ${esc(CHAT_ACTIVE.name)}</span><span style="font-size:12px">Escribe tu primer mensaje</span></div>`;return;}
    let html='';let lastDay='';
    msgs.forEach(m=>{
      const d=new Date(m.timestamp);
      const day=d.toLocaleDateString('es-MX',{weekday:'long',day:'numeric',month:'long'});
      if(day!==lastDay){html+=`<div class="chat-day-sep"><span>${day}</span></div>`;lastDay=day;}
      const isMine=m.from===CU.username;
      html+=`<div class="chat-msg-wrap ${isMine?'mine':'theirs'}">
        ${!isMine?`<div class="chat-bname">${esc(m.fromName||m.from)}</div>`:''}
        <div class="chat-bubble ${isMine?'mine':'theirs'}">${esc(m.text)}</div>
        <div class="chat-btime">${fmtChatTime(m.timestamp)}</div>
      </div>`;
    });
    el.innerHTML=html;
  }
  if(scroll)setTimeout(()=>{el.scrollTop=el.scrollHeight;},50);
}

async function sendChatMsg(){
  if(!CHAT_ACTIVE||CHAT_ACTIVE._type==='all')return;
  const input=document.getElementById('chat-input');
  const text=(input.value||'').trim();if(!text)return;
  const btn=document.getElementById('chat-send-btn');btn.disabled=true;
  input.value='';
  const toUser=getAllUsers().find(u=>u.username===CHAT_ACTIVE.username)||{username:CHAT_ACTIVE.username,name:CHAT_ACTIVE.name};
  const msgFolio='MSG-'+Date.now()+'-'+Math.random().toString(36).slice(2,6);
  const msg={
    _chat:true,folio:msgFolio,
    from:CU.username,fromName:CU.name,
    to:CHAT_ACTIVE.username,toName:CHAT_ACTIVE.name||toUser.name,
    text,timestamp:new Date().toISOString(),
    registrado:new Date().toISOString(),
    // Fields to satisfy backend schema
    exec:CU.name,username:CU.username,cliente:'-',tarjeta:'-',fecha:new Date().toISOString().slice(0,10),estado:'pendiente'
  };
  CHAT_MSGS.push(msg); // optimistic update
  renderChatMessages();
  chatMarkRead(CHAT_ACTIVE.username);
  const r=await api('sendChat',msg);
  btn.disabled=false;
  if(r&&r.ok===false){
    CHAT_MSGS=CHAT_MSGS.filter(m=>m.folio!==msgFolio);
    input.value=text;
    renderChatMessages();
    alert('Error al enviar. Intenta de nuevo.');
  }
}

function openChatNewModal(){
  const users=getAllUsers();
  if(!users.length){alert('No hay otros usuarios en el sistema.');return;}
  const sel=document.getElementById('chat-user-select');
  sel.innerHTML=users.map(u=>`<option value="${esc(u.username)}" data-name="${esc(u.name)}" data-role="${u.role}">${esc(u.name)} (@${esc(u.username)})</option>`).join('');
  document.getElementById('chat-modal').classList.add('show');
}

// ── TARJETAS (beneficios) ──
const CARDS=[
  {id:'joy',color:'tc-joy',name:'Joy Banamex',badge:'Sin anualidad',num:'•••• •••• •••• 1234',cat:'84% sin IVA',tasa:'63.69% anual',anualidad:'Sin comisión*',ingreso:'$15,000',ldc:'Desde $15,000',adicional:'—',pts:'No genera puntos Premia',bens:[{i:'🎬',t:'2x1 en Cinépolis',d:'En salas tradicionales comprando en cinepolis.com o la app.'},{i:'☕',t:'Bonificación Starbucks',d:'Ahorra $45 al recargar $150 en la app Starbucks Rewards los domingos.'},{i:'🚫',t:'Sin CVV impreso',d:'CVV digital cambia en cada compra desde la App Banamex.'},{i:'📅',t:'Elige tu fecha de corte',d:'Una vez al año.'},{i:'🎟️',t:'Preventas exclusivas',d:'Compra antes que nadie.'},{i:'🆘',t:'Mastercard Global Service',d:'Reposición en 48 hrs por robo o extravío.'},{i:'🏥',t:'Libra One gratis 1 año',d:'Consulta médica y más sin costo el primer año.'}],reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años mínimo','Ingresos desde $15,000 MXN'],nota:'*Realiza al menos $300 en compras al mes para evitar comisión por inactividad.'},
  {id:'clasica',color:'tc-clasica',name:'Clásica Banamex',badge:'Puntos Premia 5%',num:'•••• •••• •••• 2345',cat:'88.7% sin IVA',tasa:'62.63% anual',anualidad:'$815 sin IVA',ingreso:'$15,000',ldc:'Desde $15,000',adicional:'$405 sin IVA',pts:'5% Puntos Premia',bens:[{i:'🎁',t:'1er año sin anualidad',d:'Con una compra antes del primer corte.'},{i:'⭐',t:'5% Puntos Premia',d:'Acumula y úsalos como efectivo en cajeros.'},{i:'⛽',t:'Puntos Dobles en gasolina',d:'El doble al cargar gasolina todos los días.'},{i:'🏥',t:'Pagos Fijos en Salud',d:'3, 6 o 12 MSI en hospitales y farmacias.'},{i:'🎬',t:'2x1 en Cinépolis',d:'En salas tradicionales.'},{i:'🎟️',t:'Preventas exclusivas',d:'Para los mejores eventos.'},{i:'🏥',t:'Libra One gratis 1 año',d:'Sin costo el primer año.'}],reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años mínimo','Ingresos desde $15,000 MXN'],nota:'Bono: 2,000 Puntos Premia al gastar $5,000 en primeros 3 meses.'},
  {id:'teleton',color:'tc-teleton',name:'Teletón Banamex',badge:'Causa social',num:'•••• •••• •••• 3456',cat:'87.0% sin IVA',tasa:'62.47% anual',anualidad:'$540 sin IVA',ingreso:'$15,000',ldc:'Desde $15,000',adicional:'Sin costo',pts:'No genera puntos Premia',bens:[{i:'❤️',t:'Apoya al Teletón',d:'Cada uso apoya los Centros de Rehabilitación.'},{i:'💰',t:'Anualidad más baja',d:'$540 sin IVA. Primer año gratis.'},{i:'👨‍👩‍👧‍👦',t:'6 adicionales sin costo',d:'Para toda tu familia.'},{i:'🎬',t:'2x1 en Cinépolis',d:'En salas tradicionales.'},{i:'🎟️',t:'Preventas exclusivas',d:'Para los mejores eventos.'},{i:'🏥',t:'Libra One gratis 1 año',d:'Sin costo el primer año.'}],reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años mínimo','Ingresos desde $15,000 MXN'],nota:'Primer año sin anualidad con una compra antes del primer corte.'},
  {id:'oro',color:'tc-oro',name:'Oro Banamex',badge:'Puntos Premia 7%',num:'•••• •••• •••• 4567',cat:'85.7% sin IVA',tasa:'60.58% anual',anualidad:'$1,230 sin IVA',ingreso:'$25,000',ldc:'Desde $25,000',adicional:'$620 sin IVA',pts:'7% Puntos Premia',bens:[{i:'🎁',t:'1er año sin anualidad + bono',d:'Bono de 2,000 Puntos al gastar $5,000 en primeros 3 meses.'},{i:'⭐',t:'7% Puntos Premia',d:'El mayor % en tarjetas básicas.'},{i:'⛽',t:'Puntos Dobles en gasolina',d:'El doble todos los días.'},{i:'✈️',t:'3 MSI en viajes y salud',d:'3 meses sin intereses.'},{i:'🛡️',t:'Seguro de viajes',d:'Hasta $400 USD.'},{i:'🔒',t:'Seguro por fraude',d:'Hasta el saldo total.'},{i:'🏥',t:'Libra One gratis 1 año',d:'Sin costo el primer año.'}],reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años mínimo','Ingresos desde $25,000 MXN'],nota:'Bono: 2,000 Puntos Premia al gastar $5,000 en primeros 3 meses.'},
  {id:'descubre',color:'tc-descubre',name:'Descubre Banamex',badge:'Puntos Momentos',num:'•••• •••• •••• 5678',cat:'86.0% sin IVA',tasa:'62.31% anual',anualidad:'$1,230 sin IVA',ingreso:'$25,000',ldc:'Desde $25,000',adicional:'$620 sin IVA',pts:'1 Punto Momento por $1 USD',bens:[{i:'🎁',t:'1er año sin anualidad + bono',d:'Bono de 2,000 Puntos al gastar $5,000 en primeros 3 meses.'},{i:'🌟',t:'Puntos Momentos',d:'1 punto por dólar gastado.'},{i:'✈️',t:'2x1 en vuelos nacionales',d:'Cancún, Los Cabos, PVR y más.'},{i:'🎩',t:'Mastercard Concierge 24/7',d:'Asistente personal.'},{i:'🚗',t:'Elite Valet AICM',d:'50% de descuento en estacionamiento.'},{i:'🍽️',t:'Dining Program',d:'20% en restaurantes seleccionados.'},{i:'🎟️',t:'Preventas exclusivas',d:'Para los mejores eventos.'}],reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años mínimo','Ingresos desde $25,000 MXN'],nota:'Bono: 2,000 Puntos Momentos al gastar $5,000 en primeros 3 meses.'},
  {id:'platinum',color:'tc-platinum',name:'Platinum Banamex',badge:'Premium · Salas VIP',num:'•••• •••• •••• 6789',cat:'40.7% sin IVA',tasa:'32.02% anual',anualidad:'$2,725 sin IVA',ingreso:'$75,000',ldc:'Desde $50,000',adicional:'$1,360 sin IVA',pts:'10% Puntos Premia',bens:[{i:'🎁',t:'1er año sin anualidad + bono',d:'Bono 4,000 Puntos al gastar $15,000 en primeros 3 meses.'},{i:'💎',t:'10% Puntos Premia',d:'El mayor % de la línea.'},{i:'🛡️',t:'LIBRA Premium de por vida',d:'Vial, Legal, Gestoría, Hogar y Médica.'},{i:'✈️',t:'14 accesos VIP anuales',d:'10 Salones Beyond + 4 mundiales.'},{i:'🎩',t:'Mastercard Concierge 24/7',d:'Asistente personal global.'},{i:'🍽️',t:'Dining Program',d:'20% + bebida de cortesía.'},{i:'📉',t:'CAT preferencial',d:'40.7% sin IVA.'}],reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años mínimo','Ingresos desde $75,000 MXN','Buen historial'],nota:'Bono: 4,000 Puntos al gastar $15,000 en primeros 3 meses.'},
  {id:'explora',color:'tc-explora',name:'Explora Banamex',badge:'Viajero frecuente',num:'•••• •••• •••• 7890',cat:'81.2% sin IVA',tasa:'60.27% anual',anualidad:'$2,725 sin IVA',ingreso:'$75,000',ldc:'Desde $50,000',adicional:'$1,360 sin IVA',pts:'1.15 Puntos Momentos por $1 USD',bens:[{i:'🎁',t:'1er año sin anualidad + bono',d:'Bono 4,000 Puntos al gastar $15,000 en primeros 3 meses.'},{i:'🌟',t:'1.15 Puntos Momentos',d:'Por cada dólar gastado.'},{i:'✈️',t:'2x1 en vuelos + bono aniversario',d:'10,000 Puntos en aniversario.'},{i:'🛫',t:'14 accesos VIP anuales',d:'10 Salones Beyond + 4 mundiales.'},{i:'🎩',t:'Mastercard Concierge 24/7',d:'Asistente los 365 días.'},{i:'🚗',t:'Elite Valet AICM',d:'50% de descuento.'},{i:'🔒',t:'Seguro Viajes hasta $1M USD',d:'Para ti y tu familia.'}],reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio no mayor a 3 meses','18 años mínimo','Ingresos desde $75,000 MXN','Buen historial'],nota:'Bono: 4,000 Puntos al gastar $15,000 en primeros 3 meses.'}
];
let _activeCard=null;
function buildBenPanels(){document.getElementById('ben-tabs').style.display='none';document.getElementById('ben-panels').innerHTML='<div class="cards-grid" id="cards-grid"></div><div id="card-detail-wrap"></div>';renderCardsGrid();}
function renderCardsGrid(){const grid=document.getElementById('cards-grid');if(!grid)return;grid.innerHTML=CARDS.map(c=>`<div class="tc ${c.color}${_activeCard===c.id?' sel':''}" data-cid="${c.id}"><div class="tc-badge">${c.badge}</div><div class="tc-logo">BANAMEX</div><div><div class="tc-chip"></div><div class="tc-num">${c.num}</div></div><div style="display:flex;align-items:flex-end;justify-content:space-between;"><div><div class="tc-cardname">Tarjeta de Crédito</div><div class="tc-titular">${c.name}</div></div><div class="tc-mc"><span class="r"></span><span class="y"></span></div></div></div>`).join('');grid.querySelectorAll('.tc').forEach(el=>el.addEventListener('click',()=>showCardDetail(el.dataset.cid)));}
function showCardDetail(id){_activeCard=id;renderCardsGrid();const c=CARDS.find(x=>x.id===id);const wrap=document.getElementById('card-detail-wrap');wrap.innerHTML=`<div class="card-detail"><div class="cd-top"><div class="tc ${c.color} cd-mini"><div><div class="tc-chip" style="width:28px;height:20px;margin-bottom:.5rem;"></div><div style="font-family:monospace;font-size:10px;color:rgba(255,255,255,.6);">${c.num}</div></div><div style="font-size:11px;color:#fff;font-weight:700;">${c.name}</div></div><div style="flex:1;min-width:0;"><div class="cd-title">${c.name}</div><div class="cd-pts">${c.pts}</div></div><button class="cd-close" id="cd-close">✕ Cerrar</button></div><div class="cd-nums"><div class="cd-n"><div class="cd-nl">CAT</div><div class="cd-nv red">${c.cat}</div></div><div class="cd-n"><div class="cd-nl">Tasa anual</div><div class="cd-nv red">${c.tasa}</div></div><div class="cd-n"><div class="cd-nl">Anualidad</div><div class="cd-nv gold">${c.anualidad}</div></div><div class="cd-n"><div class="cd-nl">Ingreso mín.</div><div class="cd-nv green">${c.ingreso}</div></div><div class="cd-n"><div class="cd-nl">Línea</div><div class="cd-nv green">${c.ldc}</div></div><div class="cd-n"><div class="cd-nl">Adicional</div><div class="cd-nv">${c.adicional}</div></div></div><div class="cd-sec">✨ Beneficios</div><ul class="cd-bens">${c.bens.map(b=>`<li><span class="cd-ico">${b.i}</span><div><span class="cd-bt">${b.t}</span>${b.d}</div></li>`).join('')}</ul><div class="cd-sec">📋 Requisitos</div><div class="cd-reqs">${c.reqs.map(r=>`<div class="cd-req"><span>✔</span><span>${r}</span></div>`).join('')}</div><div class="cd-nota">ℹ️ ${c.nota}</div></div>`;document.getElementById('cd-close').addEventListener('click',()=>{_activeCard=null;renderCardsGrid();document.getElementById('card-detail-wrap').innerHTML='';});wrap.scrollIntoView({behavior:'smooth',block:'nearest'});}

// ── EVENT LISTENERS ──
document.addEventListener('click',async function(e){
  if(e.target.id==='login-btn'){doLogin();return;}
  if(e.target.id==='logout-btn'){doLogout();return;}
  if(e.target.id==='reg-btn'){registrarVenta();return;}
  if(e.target.id==='refresh-btn'){await loadAndRenderDash();return;}
  if(e.target.id==='add-user-btn'){addUser();return;}
  if(e.target.classList.contains('delbtn')&&e.target.dataset.folio){delSale(e.target.dataset.folio);return;}
  if(e.target.classList.contains('del-u')&&e.target.dataset.uname){
    if(!confirm('¿Eliminar al usuario @'+e.target.dataset.uname+'?'))return;
    spin(true);const r=await api('deleteUser',{username:e.target.dataset.uname});spin(false);
    if(!r.ok){alert('Error: '+r.error);return;}await loadAndRenderUsers();return;
  }
  if(e.target.id==='export-btn'){exportarExcel();return;}
  if(e.target.id==='clear-btn'){
    if(!confirm('¿Borrar TODAS las ventas? No se puede deshacer.'))return;
    spin(true);const r=await api('clearSales');spin(false);
    if(!r.ok){alert('Error: '+r.error);return;}
    SALES_CACHE=[];renderDashTable();setSyncStatus('ok','Sincronizado · 0 ventas');return;
  }
  if(e.target.id==='st-cancel'){document.getElementById('st-modal').classList.remove('show');currentSaleForStatus=null;return;}
  if(e.target.id==='st-save'){
    if(!currentSaleForStatus)return;
    const estadoSel=document.querySelector('input[name="st-radio"]:checked')?.value;
    if(!estadoSel){alert('Selecciona un estado.');return;}
    const taMap={pendiente:'pend',preasignado:'pre',declino:'decl',vendida:'ok'};
    const comentActivo=document.getElementById('st-nota-'+taMap[estadoSel]).value.trim();
    if(!comentActivo){alert('Escribe un comentario para el estado seleccionado.');return;}
    const nuevos={pendiente:document.getElementById('st-nota-pend').value.trim(),preasignado:document.getElementById('st-nota-pre').value.trim(),declino:document.getElementById('st-nota-decl').value.trim(),vendida:document.getElementById('st-nota-ok').value.trim()};
    spin(true);const r=await api('updateSale',{folio:currentSaleForStatus.folio,estado:estadoSel,comentarios:nuevos,notaEstado:nuevos[estadoSel]||''});spin(false);
    if(!r.ok){alert('Error: '+r.error);return;}
    document.getElementById('st-modal').classList.remove('show');currentSaleForStatus=null;
    if(document.getElementById('pg-dash').classList.contains('on'))await loadAndRenderDash();
    else await renderRecent();return;
  }
  if(e.target.id==='st-detail-close'){document.getElementById('st-detail-pop').classList.remove('show');return;}
  if(e.target.id==='share-cancel'){document.getElementById('share-modal').classList.remove('show');_shareFolio=null;return;}
  if(e.target.id==='share-confirm'){doShareSale();return;}
  if(e.target.id==='chat-modal-cancel'){document.getElementById('chat-modal').classList.remove('show');return;}
  if(e.target.id==='chat-modal-ok'){
    const sel=document.getElementById('chat-user-select');
    const opt=sel.options[sel.selectedIndex];
    if(!opt)return;
    document.getElementById('chat-modal').classList.remove('show');
    selectChatWithUser(opt.value,opt.dataset.name||opt.text,opt.dataset.role||'exec');return;
  }
});
document.addEventListener('keydown',function(e){
  if(e.key==='Enter'&&document.getElementById('login-screen').style.display!=='none')doLogin();
  if(e.key==='Escape'){
    document.getElementById('st-modal')?.classList.remove('show');
    document.getElementById('st-detail-pop')?.classList.remove('show');
    document.getElementById('share-modal')?.classList.remove('show');
    document.getElementById('chat-modal')?.classList.remove('show');
  }
});
document.addEventListener('input',function(e){if(e.target.id==='d-search'||e.target.id==='d-filt')renderDashTable();});

// Load user select with data attributes for chat modal
document.getElementById('chat-user-select').addEventListener('change',function(){
  const opt=this.options[this.selectedIndex];
  if(opt){this.dataset.role=opt.dataset.role||'exec';}
});

document.getElementById('login-screen').style.display='flex';
</script>
</body>
</html>
