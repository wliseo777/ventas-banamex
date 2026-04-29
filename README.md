<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>WLISEOS — Sistema de Ventas</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --pri:#7C3AED;--pri-d:#5B21B6;--pri-l:#9D5BF5;--pri-f:rgba(124,58,237,.14);
  --gold:#F0C060;--gold-d:#C8A84B;--gold-f:rgba(240,192,96,.13);
  --green:#10D980;--green-f:rgba(16,217,128,.12);
  --red:#EF4444;--red-f:rgba(239,68,68,.12);
  --cyan:#06B6D4;--cyan-f:rgba(6,182,212,.12);
  --orange:#F97316;--orange-f:rgba(249,115,22,.12);
  --bg:#07090F;--s1:#0F1219;--s2:#161B26;--s3:#1D2535;--s4:#232B3E;
  --br:rgba(255,255,255,.06);--br2:rgba(255,255,255,.11);--br3:rgba(255,255,255,.2);
  --tx:#EBF1FF;--mu:#637A9F;--mu2:#8BA3C0;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'Outfit',sans-serif;background:var(--bg);color:var(--tx);min-height:100vh;}
body::before{content:'';position:fixed;inset:0;background:radial-gradient(ellipse 90% 50% at 50% -5%,rgba(124,58,237,.12),transparent);pointer-events:none;z-index:0;}

/* ─ LOGIN ─ */
#login-screen{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:1.5rem;position:relative;z-index:1;}
.login-box{width:100%;max-width:400px;background:var(--s1);border:1px solid rgba(124,58,237,.4);border-radius:22px;padding:2.8rem 2.2rem;box-shadow:0 0 80px rgba(124,58,237,.12),0 40px 80px rgba(0,0,0,.55);}
.l-logo{font-family:'Bebas Neue',sans-serif;font-size:2.6rem;letter-spacing:.07em;text-align:center;margin-bottom:.15rem;background:linear-gradient(135deg,#fff 20%,var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
.l-sub{text-align:center;color:var(--mu);font-size:11px;margin-bottom:2.2rem;letter-spacing:.06em;text-transform:uppercase;}
.lf{display:flex;flex-direction:column;gap:5px;margin-bottom:.9rem;}
.lf label{font-size:10px;font-weight:600;color:var(--mu);text-transform:uppercase;letter-spacing:.09em;}
.lf input{background:var(--s2);border:1px solid var(--br2);border-radius:10px;padding:12px 15px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:14px;outline:none;transition:border-color .2s,box-shadow .2s;width:100%;}
.lf input:focus{border-color:var(--pri);box-shadow:0 0 0 3px var(--pri-f);}
.lf input::placeholder{color:#2e3a52;}
.l-btn{width:100%;padding:13px;background:linear-gradient(135deg,var(--pri),var(--pri-d));border:none;border-radius:10px;color:#fff;font-family:'Outfit',sans-serif;font-size:15px;font-weight:600;cursor:pointer;transition:all .2s;margin-top:.5rem;box-shadow:0 4px 22px rgba(124,58,237,.4);}
.l-btn:hover{transform:translateY(-1px);box-shadow:0 8px 30px rgba(124,58,237,.6);}
.l-btn:active{transform:scale(.98);}
.l-err{display:none;margin-top:1rem;padding:10px 14px;background:var(--red-f);border:1px solid rgba(239,68,68,.3);border-radius:9px;color:#fca5a5;font-size:13px;text-align:center;}
.l-err.show{display:block;}

/* ─ NAV ─ */
#app{display:none;position:relative;z-index:1;}
nav{display:flex;align-items:center;padding:0 1.4rem;height:56px;background:rgba(15,18,25,.95);backdrop-filter:blur(18px);border-bottom:1px solid var(--br2);position:sticky;top:0;z-index:100;gap:6px;}
nav::after{content:'';position:absolute;bottom:-1px;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,rgba(124,58,237,.5),rgba(240,192,96,.4),transparent);}
.n-logo{font-family:'Bebas Neue',sans-serif;font-size:1.45rem;letter-spacing:.07em;background:linear-gradient(120deg,#fff 30%,var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;white-space:nowrap;margin-right:4px;}
.n-tabs{display:flex;gap:2px;flex:1;flex-wrap:wrap;}
.tab{padding:6px 13px;border-radius:7px;border:1px solid transparent;font-family:'Outfit',sans-serif;font-size:12px;font-weight:500;cursor:pointer;transition:all .15s;background:transparent;color:var(--mu);}
.tab:hover{color:var(--tx);background:var(--s2);}
.tab.on{background:var(--pri-f);color:#c4b5fd;border-color:rgba(124,58,237,.28);}
.tab.gold.on{background:var(--gold-f);color:var(--gold);border-color:rgba(240,192,96,.3);}
.tab.tchat{position:relative;}
.chat-unread-dot{display:none;position:absolute;top:4px;right:4px;width:7px;height:7px;border-radius:50%;background:var(--red);border:1.5px solid var(--bg);}
.chat-unread-dot.show{display:block;}
.n-right{display:flex;align-items:center;gap:6px;margin-left:auto;}
.n-user{font-size:11px;color:var(--mu);background:var(--s2);border:1px solid var(--br2);border-radius:7px;padding:5px 10px;white-space:nowrap;}
.n-user strong{color:var(--tx);}
.out-btn{padding:5px 11px;border-radius:7px;border:1px solid var(--br2);background:transparent;color:var(--mu);font-family:'Outfit',sans-serif;font-size:11px;cursor:pointer;transition:all .15s;}
.out-btn:hover{color:var(--tx);border-color:var(--br3);}

/* ─ PAGES ─ */
.pg{display:none;}.pg.on{display:block;}
.wrap{max-width:600px;margin:0 auto;padding:2rem 1.4rem;}
.wide{max-width:1180px;margin:0 auto;padding:2rem 1.4rem;}
.pgtitle{font-family:'Bebas Neue',sans-serif;font-size:2.4rem;letter-spacing:.03em;line-height:1;margin-bottom:.3rem;}
.pgtitle span{color:var(--pri-l);}
.pgtitle.gt span{color:var(--gold);}
.pgtitle.gc span{color:var(--cyan);}
.pgtitle.gb span{color:var(--green);}
.pgsub{color:var(--mu2);font-size:13px;margin-bottom:1.8rem;}

/* ─ SPINNER ─ */
.spinner-overlay{position:fixed;inset:0;background:rgba(0,0,0,.7);display:none;align-items:center;justify-content:center;z-index:9999;}
.spinner-overlay.show{display:flex;}
.spinner{width:40px;height:40px;border:3px solid var(--br2);border-top-color:var(--pri);border-radius:50%;animation:spin .6s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}

/* ─ CARD / FIELD / BUTTON ─ */
.card{background:var(--s1);border:1px solid var(--br2);border-radius:16px;padding:1.75rem;}
.card.glow{box-shadow:0 0 50px rgba(124,58,237,.07),0 8px 32px rgba(0,0,0,.35);}
.field{display:flex;flex-direction:column;gap:5px;margin-bottom:.9rem;}
.field label{font-size:10px;font-weight:600;color:var(--mu);text-transform:uppercase;letter-spacing:.09em;}
.field input,.field select,.field textarea{background:var(--s2);border:1px solid var(--br2);border-radius:9px;padding:11px 13px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:14px;outline:none;transition:border-color .18s,box-shadow .18s;width:100%;}
.field input:focus,.field select:focus,.field textarea:focus{border-color:var(--pri);box-shadow:0 0 0 3px var(--pri-f);}
.field select option{background:#1D2535;}
.field input::placeholder,.field textarea::placeholder{color:#2a364e;}
.field textarea{resize:vertical;min-height:70px;line-height:1.5;}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.frow{display:flex;gap:10px;align-items:flex-end;margin-bottom:.9rem;}
.frow .field{flex:1;margin-bottom:0;}
.folio-pill{background:var(--s2);border:1px solid var(--br2);border-radius:9px;padding:11px 13px;font-size:11px;color:var(--gold);white-space:nowrap;font-weight:700;font-family:monospace;}
.sbtn{width:100%;padding:13px;background:linear-gradient(135deg,var(--pri),var(--pri-d));border:none;border-radius:10px;color:#fff;font-family:'Outfit',sans-serif;font-size:14px;font-weight:600;cursor:pointer;transition:all .2s;margin-top:.4rem;box-shadow:0 4px 18px rgba(124,58,237,.35);}
.sbtn:hover{transform:translateY(-1px);box-shadow:0 8px 26px rgba(124,58,237,.5);}
.sbtn:disabled{background:#1a2030;color:#445;cursor:not-allowed;box-shadow:none;transform:none;}
.toast{display:none;margin-top:.9rem;padding:11px 15px;border-radius:9px;font-size:13px;font-weight:500;text-align:center;}
.toast.ok{background:var(--green-f);border:1px solid rgba(16,217,128,.3);color:var(--green);}
.toast.err{background:var(--red-f);border:1px solid rgba(239,68,68,.3);color:#fca5a5;}
.toast.show{display:block;}
.slbl{font-size:10px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.1em;margin:1.4rem 0 8px;}

/* ─ RECENT ITEMS ─ */
.ri{display:flex;justify-content:space-between;align-items:center;padding:11px 14px;background:var(--s1);border:1px solid var(--br);border-radius:10px;margin-bottom:6px;font-size:13px;gap:10px;transition:border-color .15s;}
.ri:hover{border-color:var(--br2);}
.ri-n{font-weight:600;font-size:13px;}
.ri-m{color:var(--mu2);font-size:11px;margin-top:2px;}
.ri-f{font-family:monospace;font-size:10px;color:var(--gold);white-space:nowrap;}
.ri-actions{display:flex;flex-direction:column;align-items:flex-end;gap:5px;flex-shrink:0;}

/* ─ STATS ─ */
.sgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px;margin-bottom:1.5rem;}
.sc{background:var(--s1);border:1px solid var(--br2);border-radius:12px;padding:1.1rem 1.2rem;position:relative;overflow:hidden;}
.sc::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(255,255,255,.025),transparent 60%);pointer-events:none;}
.sc-l{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:.09em;font-weight:600;}
.sc-v{font-family:'Bebas Neue',sans-serif;font-size:2.4rem;letter-spacing:.02em;margin-top:4px;line-height:1;}
.cv-g{color:var(--gold);}
.cv-r{color:var(--red);}
.cv-gr{color:var(--green);}
.cv-p{color:var(--pri-l);}
.sync-bar{display:flex;align-items:center;gap:8px;padding:8px 13px;background:var(--s2);border:1px solid var(--br);border-radius:9px;font-size:12px;color:var(--mu2);margin-bottom:1rem;flex-wrap:wrap;}
.sync-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0;}
.sync-dot.ok{background:var(--green);}
.sync-dot.err{background:var(--red);}
.sync-dot.loading{background:var(--gold);animation:pulse 1s infinite;}
@keyframes pulse{0%,100%{opacity:1;}50%{opacity:.3;}}
.srv-status{display:inline-flex;align-items:center;gap:4px;padding:2px 9px;border-radius:20px;font-size:10px;font-weight:700;margin-left:auto;letter-spacing:.04em;}
.srv-ok{background:var(--green-f);border:1px solid rgba(16,217,128,.3);color:var(--green);}
.srv-err{background:var(--red-f);border:1px solid rgba(239,68,68,.3);color:#fca5a5;}
.srv-loading{background:var(--gold-f);border:1px solid rgba(240,192,96,.3);color:var(--gold);}

/* ─ TABLE ─ */
.tctrl{display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-bottom:1rem;}
.tctrl input,.tctrl select{background:var(--s1);border:1px solid var(--br2);border-radius:8px;padding:8px 12px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:12px;outline:none;}
.tctrl input{flex:1;min-width:180px;}
.ibtn{padding:7px 13px;border-radius:7px;border:1px solid var(--br2);background:transparent;color:var(--mu2);font-family:'Outfit',sans-serif;font-size:12px;font-weight:500;cursor:pointer;transition:all .15s;}
.ibtn.gold{border-color:rgba(240,192,96,.35);color:var(--gold);}
.ibtn.gold:hover{background:var(--gold-f);}
.ibtn.danger{border-color:rgba(239,68,68,.3);color:var(--red);}
.ibtn.danger:hover{background:var(--red-f);}
.twrap{background:#0F1219;border:1px solid rgba(255,255,255,.11);border-radius:14px;overflow:auto;}
table{width:100%;border-collapse:collapse;min-width:750px;background:#0F1219;color:#EBF1FF;}
table th{padding:10px 13px;text-align:left;font-size:10px;font-weight:700;color:#8BA3C0;text-transform:uppercase;letter-spacing:.08em;border-bottom:1px solid rgba(255,255,255,.07);white-space:nowrap;background:#1D2535;}
table tr{background:#0F1219;}
table tr:nth-child(even){background:#161B26;}
table tr:hover{background:#232B3E;}
table tr:last-child td{border-bottom:none;}
table td{padding:9px 14px;font-size:13px;font-weight:500;border-bottom:1px solid rgba(255,255,255,.06);vertical-align:middle;color:#EBF1FF;}
.tdf{font-family:monospace;font-size:11px;color:#F0C060;font-weight:700;}
.tdb{font-weight:700;color:#EBF1FF;}
.tdm{color:#8BA3C0;font-size:12px;}
.badge{display:inline-block;padding:2px 8px;border-radius:4px;font-size:10px;font-weight:600;letter-spacing:.02em;}
.b-r{background:var(--red-f);color:#fca5a5;}
.b-b{background:rgba(59,130,246,.12);color:#93c5fd;}
.b-g{background:var(--gold-f);color:var(--gold);}
.b-p{background:var(--pri-f);color:#c4b5fd;}
.b-c{background:var(--cyan-f);color:var(--cyan);}
.b-gr{background:var(--green-f);color:var(--green);}
.delbtn{background:transparent;border:none;color:#2a364e;cursor:pointer;font-size:14px;padding:2px 6px;border-radius:4px;transition:color .15s;}
.delbtn:hover{color:var(--red);}
.share-btn-tbl{background:var(--cyan-f);border:1px solid rgba(6,182,212,.3);color:var(--cyan);cursor:pointer;font-size:11px;padding:4px 10px;border-radius:6px;transition:all .15s;font-family:'Outfit',sans-serif;font-weight:600;}
.share-btn-tbl:hover{background:var(--cyan);color:#fff;border-color:var(--cyan);}
.share-btn-tbl.shared{background:var(--pri-f);border-color:rgba(124,58,237,.3);color:#c4b5fd;}
.share-btn-tbl.shared:hover{background:var(--red-f);border-color:var(--red);color:#fca5a5;}
.empty{padding:3rem;text-align:center;color:var(--mu);font-size:13px;}

/* ─ RANKING ─ */
.rgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:8px;margin-top:8px;}
.rcard{background:var(--s1);border:1px solid var(--br);border-radius:10px;padding:12px 14px;display:flex;align-items:center;gap:12px;}
.rpos{font-family:'Bebas Neue',sans-serif;font-size:1.7rem;color:var(--mu);min-width:28px;}
.rp1{color:var(--gold);}
.rp2{color:#bbb;}
.rp3{color:#cd7f32;}
.rkn{font-size:13px;font-weight:600;}
.rkc{font-size:11px;color:var(--mu2);}

/* ─ USERS ─ */
.twocol{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem;align-items:start;}
.ugrid{display:grid;gap:7px;margin-top:8px;}
.ucard{background:var(--s1);border:1px solid var(--br2);border-radius:11px;padding:11px 14px;display:flex;align-items:center;gap:11px;}
.uav{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:12px;flex-shrink:0;}
.av-e{background:var(--red-f);color:#fca5a5;}
.av-a{background:var(--gold-f);color:var(--gold);}
.av-s{background:var(--pri-f);color:#c4b5fd;}
.ui{flex:1;min-width:0;}
.un{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.ur{font-size:10px;color:var(--mu2);margin-top:2px;}
.del-u{border:none;border-radius:5px;padding:5px 9px;font-family:'Outfit',sans-serif;font-size:11px;font-weight:600;cursor:pointer;transition:all .15s;background:var(--red-f);color:#fca5a5;}
.del-u:hover{background:var(--red);color:#fff;}

/* ─ FORM ESTADO ─ */
.estado-selector{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:.9rem;}
.estado-opt{display:flex;align-items:center;gap:8px;background:var(--s2);border:2px solid var(--br2);border-radius:10px;padding:10px 12px;cursor:pointer;transition:all .18s;}
.estado-opt input[type=radio]{accent-color:var(--gold);width:15px;height:15px;flex-shrink:0;}
.estado-opt.sel-pend{border-color:#fbbf24!important;background:rgba(251,191,36,.07);}
.estado-opt.sel-pre{border-color:#a78bfa!important;background:rgba(167,139,250,.07);}
.estado-opt.sel-decl{border-color:var(--red)!important;background:rgba(239,68,68,.07);}
.estado-opt.sel-ok{border-color:var(--green)!important;background:rgba(16,217,128,.07);}
.estado-lbl{font-size:13px;font-weight:600;}
.estado-sub{font-size:10px;color:var(--mu2);}
.req-alert{background:var(--red-f);border:1px solid rgba(239,68,68,.3);border-radius:8px;padding:10px 14px;font-size:12px;color:#fca5a5;margin-bottom:.9rem;display:none;}
.req-alert.show{display:block;}

/* ─ STATS SECTION ─ */
.stats-section{background:var(--s2);border:1px solid var(--br2);border-radius:14px;padding:1.3rem;margin-bottom:1.2rem;}
.stats-section-title{font-size:11px;font-weight:700;color:var(--mu2);text-transform:uppercase;letter-spacing:.1em;margin-bottom:1rem;}
.mini-table{width:100%;border-collapse:collapse;font-size:12px;}
.mini-table{width:100%;border-collapse:collapse;font-size:13px;background:#0F1219;color:#EBF1FF;}
.mini-table thead tr{background:#1D2535;}
.mini-table tbody tr{background:#0F1219;}
.mini-table tbody tr:nth-child(even){background:#161B26;}
.mini-table th{padding:8px 10px;text-align:left;color:#8BA3C0;font-size:10px;text-transform:uppercase;letter-spacing:.06em;border-bottom:1px solid rgba(255,255,255,.07);font-weight:700;}
.mini-table td{padding:8px 10px;border-bottom:1px solid rgba(255,255,255,.06);color:#EBF1FF;font-size:13px;}
.mini-table tr:last-child td{border-bottom:none;}
.mini-table tr:hover td{background:#232B3E;}
.exec-accordion{margin-bottom:7px;border:1px solid var(--br2);border-radius:10px;overflow:hidden;}
.exec-acc-head{display:flex;align-items:center;justify-content:space-between;padding:10px 14px;cursor:pointer;background:var(--s3);font-size:13px;font-weight:500;color:var(--tx);}
.exec-acc-head:hover{background:rgba(255,255,255,.03);}
.exec-acc-body{display:none;padding:10px 14px;background:var(--s2);}
.exec-acc-body.open{display:block;}

/* ─ BADGES ─ */
.st-badge{display:inline-flex;align-items:center;gap:4px;padding:3px 9px;border-radius:20px;font-size:11px;font-weight:600;cursor:pointer;transition:opacity .15s;white-space:nowrap;}
.st-badge:hover{opacity:.75;}
.st-pend{background:rgba(251,191,36,.13);border:1px solid rgba(251,191,36,.35);color:#fbbf24;}
.st-decl{background:var(--red-f);border:1px solid rgba(239,68,68,.35);color:#fca5a5;}
.st-pre{background:var(--pri-f);border:1px solid rgba(124,58,237,.35);color:#c4b5fd;}
.st-ok{background:var(--green-f);border:1px solid rgba(16,217,128,.3);color:var(--green);}
.st-none{background:rgba(120,120,120,.12);border:1px solid rgba(120,120,120,.28);color:#666;}
.shared-badge{display:inline-flex;align-items:center;gap:4px;padding:2px 7px;border-radius:4px;font-size:10px;font-weight:600;background:var(--cyan-f);border:1px solid rgba(6,182,212,.3);color:var(--cyan);margin-top:2px;}
.shared-out{background:var(--pri-f);border:1px solid rgba(124,58,237,.3);color:#c4b5fd;}

/* ── BENEFITS — REDESIGN ── */
.ben-layout{display:grid;grid-template-columns:260px 1fr;gap:1.5rem;align-items:start;}
.ben-sidebar{display:flex;flex-direction:column;gap:6px;position:sticky;top:72px;}
.ben-pill{display:flex;align-items:center;gap:10px;padding:10px 13px;border-radius:12px;cursor:pointer;border:2px solid transparent;transition:all .18s;background:var(--s2);}
.ben-pill:hover{background:var(--s3);}
.ben-pill.active{border-color:rgba(255,255,255,.22);background:var(--s3);}
.ben-pill-stripe{width:5px;height:40px;border-radius:3px;flex-shrink:0;}
.ben-pill-info{flex:1;min-width:0;}
.ben-pill-name{font-size:12px;font-weight:700;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.ben-pill-seg{font-size:10px;color:var(--mu2);margin-top:1px;text-transform:uppercase;letter-spacing:.05em;}
.ben-detail{animation:fadeIn .18s ease;}
@keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
.ben-card-visual{border-radius:18px;padding:1.4rem 1.5rem;position:relative;overflow:hidden;min-height:180px;display:flex;flex-direction:column;justify-content:space-between;box-shadow:0 10px 40px rgba(0,0,0,.55);margin-bottom:1.2rem;}
.ben-card-visual::before{content:'';position:absolute;top:-30%;right:-10%;width:200px;height:200px;border-radius:50%;background:rgba(255,255,255,.07);pointer-events:none;}
.bcv-badge{display:inline-block;background:rgba(0,0,0,.3);backdrop-filter:blur(8px);border:1px solid rgba(255,255,255,.18);border-radius:20px;padding:3px 11px;font-size:10px;font-weight:700;color:#fff;letter-spacing:.04em;margin-bottom:.8rem;}
.bcv-chip{width:34px;height:24px;border-radius:4px;background:linear-gradient(135deg,#c8a84b,#f0c060,#c8a84b);margin-bottom:.7rem;box-shadow:0 2px 8px rgba(0,0,0,.4);}
.bcv-num{font-family:monospace;font-size:13px;letter-spacing:.18em;color:rgba(255,255,255,.75);margin-bottom:.4rem;}
.bcv-name{font-size:13px;color:#fff;font-weight:700;letter-spacing:.03em;}
.bcv-logo{position:absolute;top:1.1rem;right:1.2rem;font-family:'Bebas Neue',sans-serif;font-size:.9rem;color:rgba(255,255,255,.85);letter-spacing:.06em;}
.bcv-mc{position:absolute;bottom:1.1rem;right:1.2rem;display:flex;}
.bcv-mc span{width:20px;height:20px;border-radius:50%;opacity:.9;}
.bcv-mc .r{background:#eb001b;}.bcv-mc .y{background:#f79e1b;margin-left:-8px;}
.ben-nums-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(130px,1fr));gap:8px;margin-bottom:1.2rem;}
.ben-num-box{background:var(--s2);border:1px solid var(--br2);border-radius:10px;padding:10px 12px;}
.bnn{font-size:10px;color:var(--mu2);text-transform:uppercase;letter-spacing:.07em;font-weight:600;}
.bnv{font-size:14px;font-weight:700;margin-top:3px;}
.bnv.gold{color:var(--gold);}
.bnv.green{color:var(--green);}
.bnv.red{color:#fca5a5;}
.bnv.pri{color:#c4b5fd;}
.ben-section-hd{font-size:10px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.09em;margin:1.1rem 0 .6rem;display:flex;align-items:center;gap:6px;}
.ben-section-hd::after{content:'';flex:1;height:1px;background:var(--br2);}
.ben-benefits-list{display:flex;flex-direction:column;gap:6px;margin-bottom:1rem;}
.ben-benefit-item{display:flex;align-items:flex-start;gap:10px;padding:10px 13px;background:var(--s2);border:1px solid var(--br);border-radius:10px;transition:border-color .15s;}
.ben-benefit-item:hover{border-color:var(--br2);}
.bbi-ico{font-size:18px;flex-shrink:0;margin-top:1px;}
.bbi-body{flex:1;min-width:0;}
.bbi-title{font-size:13px;font-weight:700;margin-bottom:2px;}
.bbi-desc{font-size:12px;color:var(--mu2);line-height:1.5;}
.ben-reqs-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(190px,1fr));gap:6px;margin-bottom:.8rem;}
.ben-req{background:var(--s2);border:1px solid var(--br);border-radius:8px;padding:8px 11px;font-size:12px;color:var(--mu2);display:flex;gap:7px;align-items:flex-start;}
.ben-req span:first-child{color:var(--green);font-weight:700;}
.ben-nota{background:var(--gold-f);border:1px solid rgba(240,192,96,.2);border-radius:9px;padding:10px 14px;font-size:11px;color:#bbb;line-height:1.6;}
/* Card colors */
.c-joy{background:linear-gradient(135deg,#C8102E,#8B0B1F);}
.c-clasica{background:linear-gradient(135deg,#1a2744,#2e4a8a);}
.c-teleton{background:linear-gradient(135deg,#4a0080,#9333ea);}
.c-oro{background:linear-gradient(135deg,#7c4f00,#C8A84B);}
.c-descubre{background:linear-gradient(135deg,#064e3b,#10b981);}
.c-platinum{background:linear-gradient(135deg,#1f2937,#6b7280);}
.c-explora{background:linear-gradient(135deg,#1e3a8a,#3b82f6);}

/* ─ STATUS MODAL ─ */
.st-modal{position:fixed;inset:0;background:rgba(0,0,0,.82);display:none;align-items:center;justify-content:center;z-index:999;padding:1rem;}
.st-modal.show{display:flex;}
.st-box{background:var(--s1);border:1px solid var(--br2);border-radius:20px;padding:2rem;max-width:470px;width:100%;max-height:90vh;overflow-y:auto;box-shadow:0 40px 80px rgba(0,0,0,.6);}
.st-box h3{font-family:'Bebas Neue',sans-serif;font-size:1.5rem;letter-spacing:.03em;margin-bottom:.3rem;}
.st-box p{font-size:13px;color:var(--mu2);margin-bottom:1.2rem;}
.st-opts{display:flex;flex-direction:column;gap:7px;margin-bottom:1.2rem;}
.st-opt{display:flex;align-items:center;gap:10px;background:var(--s2);border:2px solid var(--br2);border-radius:10px;padding:11px 14px;cursor:pointer;transition:border-color .15s;}
.st-opt input[type=radio]{accent-color:var(--gold);width:16px;height:16px;flex-shrink:0;}
.st-opt-label{font-size:13px;font-weight:600;}
.st-opt-sub{font-size:11px;color:var(--mu2);margin-top:2px;}
.st-comments-section{margin-bottom:1rem;}
.st-comments-header{font-size:10px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.07em;margin-bottom:8px;}
.st-req-badge{display:inline-block;padding:1px 5px;background:var(--red-f);border-radius:4px;color:#fca5a5;font-size:9px;font-weight:700;margin-left:4px;}
.st-comment-block{background:var(--s2);border:1px solid var(--br);border-radius:9px;padding:11px 13px;margin-bottom:7px;}
.st-comment-block.highlighted{border-color:rgba(240,192,96,.4);background:rgba(240,192,96,.05);}
.st-comment-label{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.07em;margin-bottom:6px;}
.st-comment-label.pend{color:#fbbf24;}.st-comment-label.pre{color:#a78bfa;}.st-comment-label.decl{color:var(--red);}.st-comment-label.ok{color:var(--green);}
.st-comment-block textarea{width:100%;background:rgba(0,0,0,.2);border:1px solid var(--br2);border-radius:7px;padding:9px 11px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:13px;resize:vertical;min-height:60px;outline:none;line-height:1.5;}
.st-comment-block textarea:focus{border-color:var(--gold);}
.st-btns{display:flex;gap:8px;justify-content:flex-end;margin-top:1.2rem;}
.st-save{padding:10px 22px;background:linear-gradient(135deg,var(--pri),var(--pri-d));border:none;border-radius:8px;color:#fff;font-family:'Outfit',sans-serif;font-size:13px;font-weight:600;cursor:pointer;box-shadow:0 4px 14px rgba(124,58,237,.35);}
.st-save:hover{box-shadow:0 6px 22px rgba(124,58,237,.55);}
.st-cancel{padding:10px 18px;background:transparent;border:1px solid var(--br2);border-radius:8px;color:var(--mu2);font-family:'Outfit',sans-serif;font-size:13px;cursor:pointer;}
.st-cancel:hover{color:var(--tx);}
.st-detail-pop{position:fixed;inset:0;background:rgba(0,0,0,.82);display:none;align-items:center;justify-content:center;z-index:999;padding:1rem;}
.st-detail-pop.show{display:flex;}
.st-detail-box{background:var(--s1);border:1px solid var(--br2);border-radius:20px;padding:2rem;max-width:420px;width:100%;}
.st-detail-box h3{font-family:'Bebas Neue',sans-serif;font-size:1.3rem;margin-bottom:1rem;}
.st-detail-txt{font-size:14px;line-height:1.7;color:#ccc;background:var(--s2);border-radius:10px;padding:14px;}
.nota-preview{font-size:10px;color:var(--mu2);margin-top:2px;max-width:220px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}

/* ─ SHARE MODAL ─ */
.share-modal{position:fixed;inset:0;background:rgba(0,0,0,.82);display:none;align-items:center;justify-content:center;z-index:999;padding:1rem;}
.share-modal.show{display:flex;}
.share-box{background:var(--s1);border:1px solid var(--br2);border-radius:20px;padding:2rem;max-width:400px;width:100%;box-shadow:0 40px 80px rgba(0,0,0,.6);}
.share-box h3{font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:.03em;margin-bottom:.3rem;}
.share-box p{font-size:12px;color:var(--mu2);margin-bottom:1.2rem;}
.unshare-btn{width:100%;padding:10px;background:var(--red-f);border:1px solid rgba(239,68,68,.3);border-radius:9px;color:#fca5a5;font-family:'Outfit',sans-serif;font-size:13px;font-weight:600;cursor:pointer;margin-bottom:1rem;transition:all .15s;}
.unshare-btn:hover{background:var(--red);color:#fff;}
.share-user-list{display:flex;flex-direction:column;gap:6px;max-height:260px;overflow-y:auto;}
.user-pick-item{display:flex;align-items:center;gap:10px;padding:10px 12px;background:var(--s2);border:2px solid var(--br2);border-radius:10px;cursor:pointer;transition:all .18s;}
.user-pick-item:hover,.user-pick-item.picked{border-color:var(--cyan);background:var(--cyan-f);}
.upi-av{width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:12px;flex-shrink:0;background:var(--red-f);color:#fca5a5;}
.upi-name{font-size:13px;font-weight:700;}
.upi-user{font-size:11px;color:var(--mu2);}
.share-actions{display:flex;gap:8px;justify-content:flex-end;margin-top:1.2rem;}
.share-save{padding:10px 22px;background:linear-gradient(135deg,var(--cyan),#0891b2);border:none;border-radius:8px;color:#fff;font-family:'Outfit',sans-serif;font-size:13px;font-weight:600;cursor:pointer;box-shadow:0 4px 14px rgba(6,182,212,.3);}
.share-save:hover{box-shadow:0 6px 22px rgba(6,182,212,.5);}

/* ─ CHAT ─ */
.chat-layout{display:grid;grid-template-columns:280px 1fr;height:calc(100vh - 138px);min-height:520px;background:var(--s1);border:1px solid var(--br2);border-radius:16px;overflow:hidden;box-shadow:0 20px 60px rgba(0,0,0,.4);}
.chat-sidebar{border-right:1px solid var(--br);display:flex;flex-direction:column;overflow:hidden;background:var(--s2);}
.chat-sidebar-head{padding:.85rem 1rem;border-bottom:1px solid var(--br);display:flex;align-items:center;justify-content:space-between;flex-shrink:0;}
.chat-sidebar-title{font-family:'Bebas Neue',sans-serif;font-size:1.1rem;letter-spacing:.05em;}
.chat-top-btns{display:flex;gap:4px;}
.chat-new-btn,.chat-grp-btn{padding:4px 10px;border-radius:6px;border:1px solid var(--br2);background:transparent;color:var(--mu2);font-family:'Outfit',sans-serif;font-size:11px;font-weight:600;cursor:pointer;transition:all .15s;}
.chat-new-btn:hover{color:var(--cyan);border-color:var(--cyan);}
.chat-grp-btn{display:none;}
.chat-grp-btn:hover{color:var(--green);border-color:var(--green);}
.chat-grp-btn.show{display:block;}
.chat-contacts{flex:1;overflow-y:auto;}
.chat-contact{padding:.65rem 1rem;cursor:pointer;border-bottom:1px solid rgba(255,255,255,.03);display:flex;align-items:center;gap:9px;transition:background .12s;}
.chat-contact:hover{background:rgba(255,255,255,.04);}
.chat-contact.active{background:var(--pri-f);border-left:3px solid var(--pri);}
.chat-av{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:12px;flex-shrink:0;}
.cav-e{background:var(--red-f);color:#fca5a5;}
.cav-a{background:var(--gold-f);color:var(--gold);}
.cav-s{background:var(--pri-f);color:#c4b5fd;}
.cav-all{background:var(--cyan-f);color:var(--cyan);font-size:15px;}
.cav-grp{background:var(--green-f);color:var(--green);font-size:14px;}
.chat-ci{flex:1;min-width:0;}
.chat-cn{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.chat-cl{font-size:11px;color:var(--mu2);margin-top:1px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.chat-unread{background:var(--red);color:#fff;border-radius:10px;font-size:10px;font-weight:700;padding:1px 6px;min-width:18px;text-align:center;flex-shrink:0;}
.chat-main{display:flex;flex-direction:column;overflow:hidden;}
.chat-main-head{padding:.8rem 1.2rem;border-bottom:1px solid var(--br);display:flex;align-items:center;gap:10px;flex-shrink:0;background:rgba(255,255,255,.012);}
.chat-main-title{font-size:14px;font-weight:700;}
.chat-main-sub{font-size:11px;color:var(--mu2);margin-top:1px;}
.chat-msgs{flex:1;overflow-y:auto;padding:1rem;display:flex;flex-direction:column;gap:5px;}
.chat-day-sep{text-align:center;font-size:10px;color:var(--mu);padding:6px 0;position:relative;font-weight:600;letter-spacing:.06em;text-transform:uppercase;}
.chat-day-sep::before{content:'';position:absolute;top:50%;left:0;right:0;height:1px;background:var(--br);}
.chat-day-sep span{background:var(--s1);padding:0 10px;position:relative;}
.chat-msg-wrap{display:flex;flex-direction:column;}
.chat-msg-wrap.mine{align-items:flex-end;}
.chat-msg-wrap.theirs{align-items:flex-start;}
.chat-bname{font-size:10px;color:var(--mu2);margin-bottom:3px;padding:0 4px;font-weight:600;}
.chat-bubble{max-width:72%;padding:9px 13px;border-radius:14px;font-size:13px;line-height:1.55;word-break:break-word;}
.chat-bubble.mine{background:linear-gradient(135deg,var(--pri),var(--pri-d));color:#fff;border-bottom-right-radius:4px;box-shadow:0 4px 14px rgba(124,58,237,.3);}
.chat-bubble.theirs{background:var(--s3);color:var(--tx);border-bottom-left-radius:4px;border:1px solid var(--br);}
.chat-bubble img{max-width:100%;border-radius:8px;display:block;margin-top:4px;cursor:pointer;}
.chat-btime{font-size:10px;opacity:.45;margin-top:3px;padding:0 4px;}
.chat-empty-state{flex:1;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:8px;color:var(--mu);}
.chat-empty-state .ce-icon{font-size:2.5rem;margin-bottom:6px;}
.chat-empty-state p{font-size:13px;}
.chat-empty-state small{font-size:11px;color:var(--mu);}
.chat-input-area{padding:.75rem 1rem;border-top:1px solid var(--br);display:flex;gap:6px;align-items:flex-end;flex-shrink:0;}
.chat-input-area textarea{flex:1;background:var(--s2);border:1px solid var(--br2);border-radius:10px;padding:9px 12px;color:var(--tx);font-family:'Outfit',sans-serif;font-size:13px;resize:none;outline:none;max-height:90px;min-height:40px;line-height:1.5;transition:border-color .18s;}
.chat-input-area textarea:focus{border-color:var(--pri);}
.chat-img-btn{padding:9px 10px;background:var(--s2);border:1px solid var(--br2);border-radius:10px;color:var(--mu2);cursor:pointer;font-size:16px;transition:all .15s;flex-shrink:0;}
.chat-img-btn:hover{border-color:var(--pri);color:#c4b5fd;}
.chat-send{padding:9px 17px;background:linear-gradient(135deg,var(--pri),var(--pri-d));border:none;border-radius:10px;color:#fff;font-family:'Outfit',sans-serif;font-size:13px;font-weight:600;cursor:pointer;white-space:nowrap;transition:all .18s;box-shadow:0 4px 14px rgba(124,58,237,.3);}
.chat-send:hover{box-shadow:0 6px 22px rgba(124,58,237,.5);}
.chat-send:disabled{background:#1a2030;color:#445;cursor:not-allowed;box-shadow:none;}
/* img preview in input */
.chat-img-preview{display:none;align-items:center;gap:8px;padding:.5rem 1rem;border-top:1px solid var(--br);background:var(--s2);flex-shrink:0;}
.chat-img-preview.show{display:flex;}
.chat-img-preview img{height:50px;border-radius:6px;object-fit:cover;}
.chat-img-preview span{font-size:12px;color:var(--mu2);flex:1;}
.chat-img-preview button{background:var(--red-f);border:none;color:#fca5a5;border-radius:5px;padding:3px 8px;cursor:pointer;font-size:12px;}
/* All-messages admin */
.chat-all-msg{display:flex;flex-direction:column;gap:3px;padding:9px 12px;border-radius:10px;background:var(--s2);border:1px solid var(--br);margin-bottom:4px;}
.chat-all-meta{font-size:10px;color:var(--mu2);display:flex;gap:6px;align-items:center;flex-wrap:wrap;}
.chat-all-from{font-weight:700;color:var(--pri-l);}
.chat-all-to{font-weight:700;color:var(--cyan);}
.chat-all-text{font-size:13px;margin-top:3px;}
.chat-all-text img{max-width:200px;border-radius:6px;display:block;margin-top:4px;}
/* Generic modal */
.generic-modal{position:fixed;inset:0;background:rgba(0,0,0,.82);display:none;align-items:center;justify-content:center;z-index:1000;padding:1rem;}
.generic-modal.show{display:flex;}
.generic-box{background:var(--s1);border:1px solid var(--br2);border-radius:20px;padding:2rem;max-width:400px;width:100%;box-shadow:0 40px 80px rgba(0,0,0,.6);}
.generic-box h3{font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:.04em;margin-bottom:1.2rem;}
.gmod-btns{display:flex;gap:8px;justify-content:flex-end;margin-top:1.3rem;}
/* Group members selector */
.grp-member-list{display:flex;flex-direction:column;gap:5px;max-height:220px;overflow-y:auto;margin-top:.6rem;}
.grp-member-item{display:flex;align-items:center;gap:9px;padding:8px 11px;background:var(--s2);border:2px solid var(--br2);border-radius:9px;cursor:pointer;transition:all .15s;}
.grp-member-item.picked{border-color:var(--green);background:var(--green-f);}
.grp-member-item .gmi-av{width:28px;height:28px;border-radius:50%;background:var(--red-f);color:#fca5a5;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;flex-shrink:0;}
.grp-member-item .gmi-name{font-size:13px;font-weight:600;}

/* ─ DELETE CHAT/GROUP ─ */
.conv-del-btn{background:transparent;border:none;color:#2a364e;cursor:pointer;font-size:13px;padding:2px 5px;border-radius:4px;transition:color .15s;flex-shrink:0;opacity:0;}
.chat-contact:hover .conv-del-btn{opacity:1;}
.conv-del-btn:hover{color:var(--red);}

/* ─ NOTIFICATION TOAST ─ */
.notif-toast{position:fixed;bottom:1.5rem;right:1.5rem;background:var(--s1);border:1px solid var(--pri);border-radius:14px;padding:1rem 1.2rem;max-width:320px;z-index:9999;display:none;box-shadow:0 10px 40px rgba(0,0,0,.6);animation:slideIn .3s ease;}
.notif-toast.show{display:flex;gap:10px;align-items:flex-start;}
@keyframes slideIn{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:none}}
.notif-icon{font-size:22px;flex-shrink:0;}
.notif-from{font-size:12px;font-weight:700;color:#c4b5fd;margin-bottom:3px;}
.notif-text{font-size:13px;color:var(--tx);line-height:1.4;}
.notif-close{background:transparent;border:none;color:var(--mu2);cursor:pointer;font-size:16px;padding:0;margin-left:auto;flex-shrink:0;}

/* ─ GROUP BADGE ─ */
.grp-badge{font-size:9px;background:var(--green-f);color:var(--green);border-radius:3px;padding:1px 5px;margin-left:5px;font-weight:700;}

/* ─ RESPONSIVE ─ */
@media(max-width:768px){
  nav{padding:0 .8rem;}
  .twocol{grid-template-columns:1fr;}
  .row2{grid-template-columns:1fr;}
  .estado-selector{grid-template-columns:1fr;}
  .chat-layout{grid-template-columns:1fr;}
  .chat-sidebar{max-height:200px;border-right:none;border-bottom:1px solid var(--br);}
  .ben-layout{grid-template-columns:1fr;}
  .ben-sidebar{position:static;}
}
</style>
</head>
<body>
<div class="spinner-overlay" id="spinner"><div class="spinner"></div></div>

<!-- ── LOGIN ── -->
<div id="login-screen">
  <div class="login-box">
    <div class="l-logo">WLISEOS</div>
    <div class="l-sub">Sistema de Ventas · Banamex</div>
    <div class="lf"><label>Usuario</label><input type="text" id="l-user" placeholder="tu.usuario" autocomplete="username"></div>
    <div class="lf"><label>Contraseña</label><input type="password" id="l-pass" placeholder="••••••••" autocomplete="current-password"></div>
    <button class="l-btn" id="login-btn">Entrar al sistema</button>
    <div class="l-err" id="login-err"></div>
  </div>
</div>

<!-- ── APP ── -->
<div id="app">
  <nav>
    <div class="n-logo">WLISEOS</div>
    <div class="n-tabs" id="n-tabs"></div>
    <div class="n-right">
      <div class="n-user">Hola, <strong id="nav-name"></strong></div>
      <button class="out-btn" id="logout-btn">Salir</button>
    </div>
  </nav>

  <!-- EXEC -->
  <div id="pg-exec" class="pg">
    <div class="wrap">
      <div class="pgtitle">Nueva <span>venta</span></div>
      <p class="pgsub">* campos obligatorios</p>
      <div class="card glow">
        <div class="row2">
          <div class="field"><label>Nombre del cliente *</label><input type="text" id="f-cliente" placeholder="Ej. María González"></div>
          <div class="field"><label>Teléfono</label><input type="tel" id="f-tel" placeholder="Ej. 5512345678" maxlength="15"></div>
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
          <div class="field"><label>RFC (opcional)</label><input type="text" id="f-rfc" placeholder="Ej. GOMJ850101MDF"></div>
          <div class="field"><label>Ingresos mensuales (opcional)</label><input type="number" id="f-ingresos" placeholder="25000" min="0"></div>
        </div>
        <div class="row2">
          <div class="field"><label>Tarjeta referencia (opcional)</label><input type="text" id="f-tarjetaRef" placeholder="Ej. Clásica Banamex"></div>
          <div class="field"><label>LDC referencia (opcional)</label><input type="number" id="f-ldcRef" placeholder="30000" min="0"></div>
        </div>
        <div class="field"><label>Estado de la venta *</label></div>
        <div class="estado-selector">
          <label class="estado-opt" id="eopt-pend"><input type="radio" name="f-estado" value="pendiente"><div><div class="estado-lbl">📞 Pendiente</div><div class="estado-sub">Sin contactar</div></div></label>
          <label class="estado-opt" id="eopt-pre"><input type="radio" name="f-estado" value="preasignado"><div><div class="estado-lbl">⭐ Preasignado</div><div class="estado-sub">Oferta asignada</div></div></label>
          <label class="estado-opt" id="eopt-decl"><input type="radio" name="f-estado" value="declino"><div><div class="estado-lbl">❌ Declinó</div><div class="estado-sub">No quiso</div></div></label>
          <label class="estado-opt" id="eopt-ok"><input type="radio" name="f-estado" value="vendida"><div><div class="estado-lbl">✅ Vendida</div><div class="estado-sub">Contratada</div></div></label>
        </div>
        <div class="field">
          <label>Comentario de la gestión *</label>
          <textarea id="f-comentario" placeholder="Describe el resultado de la gestión…" rows="3"></textarea>
        </div>
        <div class="req-alert" id="req-alert"></div>
        <div class="frow">
          <div class="field"><label>Folio (auto si vacío)</label><input type="text" id="f-folio" placeholder="WLS-000001" maxlength="20"></div>
          <div class="folio-pill" id="folio-pill">—</div>
        </div>
        <button class="sbtn" id="reg-btn">✦ Registrar venta</button>
        <div class="toast ok" id="t-ok"></div>
        <div class="toast err" id="t-err"></div>
      </div>
      <div class="slbl">Mis últimas ventas</div>
      <div id="exec-recent"></div>
    </div>
  </div>

  <!-- STATS -->
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
      <div class="pgtitle gb">Beneficios <span>tarjetas</span></div>
      <p class="pgsub">Manual actualizado · Selecciona una tarjeta para ver detalles</p>
      <div class="ben-layout">
        <div class="ben-sidebar" id="ben-sidebar"></div>
        <div id="ben-detail-wrap"></div>
      </div>
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
        <span class="srv-status srv-loading" id="srv-status">⏳ Conectando…</span>
      </div>
      <div class="sgrid">
        <div class="sc"><div class="sc-l">Total ventas</div><div class="sc-v cv-g" id="s-tot">—</div></div>
        <div class="sc"><div class="sc-l">Ejecutivos</div><div class="sc-v cv-r" id="s-exe">—</div></div>
        <div class="sc"><div class="sc-l">Hoy</div><div class="sc-v cv-gr" id="s-hoy">—</div></div>
        <div class="sc"><div class="sc-l">Esta semana</div><div class="sc-v cv-p" id="s-sem">—</div></div>
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
        <button class="ibtn gold" id="export-btn">📊 Exportar</button>
        <button class="ibtn danger" id="clear-btn">Borrar todo</button>
      </div>
      <div class="twrap">
        <table>
          <thead><tr><th>Folio</th><th>Ejecutivo</th><th>Cliente</th><th>Tel.</th><th>Tarjeta</th><th>Estado</th><th>Comentario</th><th>Compartida</th><th>Fecha</th><th>Reg.</th><th></th></tr></thead>
          <tbody id="t-body"></tbody>
        </table>
        <div class="empty" id="t-empty" style="display:none">No hay ventas registradas todavía.</div>
      </div>
      <div class="slbl" style="margin-top:1.75rem">🏆 Ranking</div>
      <div class="rgrid" id="rank-grid"></div>
    </div>
  </div>

  <!-- USUARIOS -->
  <div id="pg-users" class="pg">
    <div class="wide">
      <div class="pgtitle gt">Gestión de <span>usuarios</span></div>
      <p class="pgsub">Agrega o elimina miembros del equipo.</p>
      <div class="twocol">
        <div class="card">
          <div style="font-size:14px;font-weight:700;margin-bottom:1.2rem;">Agregar usuario</div>
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
    <div class="wide" style="padding-bottom:0">
      <div class="pgtitle gc">Chat del <span>equipo</span></div>
      <p class="pgsub" id="chat-sub">Mensajes privados y grupos</p>
      <div class="chat-layout">
        <div class="chat-sidebar">
          <div class="chat-sidebar-head">
            <span class="chat-sidebar-title">💬 Mensajes</span>
            <div class="chat-top-btns">
              <button class="chat-grp-btn" id="chat-grp-btn" title="Crear grupo">👥 Grupo</button>
              <button class="chat-new-btn" id="chat-new-btn">+ Nuevo</button>
            </div>
          </div>
          <div class="chat-contacts" id="chat-contacts"><div style="padding:2rem;text-align:center;color:var(--mu);font-size:13px">Cargando…</div></div>
        </div>
        <div class="chat-main">
          <div class="chat-main-head" id="chat-main-head" style="display:none">
            <div class="chat-av cav-e" id="chat-head-av">?</div>
            <div><div class="chat-main-title" id="chat-head-name">—</div><div class="chat-main-sub" id="chat-head-sub">—</div></div>
          </div>
          <div class="chat-msgs" id="chat-msgs">
            <div class="chat-empty-state">
              <div class="ce-icon">💬</div>
              <p>Selecciona una conversación</p>
              <small>o inicia una nueva con el botón "+ Nuevo"</small>
            </div>
          </div>
          <div class="chat-img-preview" id="chat-img-preview">
            <img id="chat-img-prev-thumb" src="" alt="">
            <span>Imagen lista para enviar</span>
            <button id="chat-img-clear">✕ Quitar</button>
          </div>
          <div class="chat-input-area" id="chat-input-area" style="display:none">
            <label class="chat-img-btn" title="Adjuntar imagen">📎<input type="file" id="chat-img-input" accept="image/*" style="display:none"></label>
            <textarea id="chat-input" placeholder="Escribe… (Enter envía, Shift+Enter salto de línea)"></textarea>
            <button class="chat-send" id="chat-send-btn">Enviar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ── STATUS MODAL ── -->
<div class="st-modal" id="st-modal">
  <div class="st-box">
    <h3>Actualizar estado</h3>
    <p id="st-modal-client"></p>
    <div class="st-opts">
      <label class="st-opt"><input type="radio" name="st-radio" value="pendiente"><div><div class="st-opt-label">📞 Pendiente</div><div class="st-opt-sub">Sin contactar</div></div></label>
      <label class="st-opt"><input type="radio" name="st-radio" value="declino"><div><div class="st-opt-label">❌ Declinó</div><div class="st-opt-sub">No quiso</div></div></label>
      <label class="st-opt"><input type="radio" name="st-radio" value="preasignado"><div><div class="st-opt-label">⭐ Preasignado</div><div class="st-opt-sub">Oferta asignada</div></div></label>
      <label class="st-opt"><input type="radio" name="st-radio" value="vendida"><div><div class="st-opt-label">✅ Vendida</div><div class="st-opt-sub">Contratada</div></div></label>
    </div>
    <div class="st-comments-section">
      <div class="st-comments-header">💬 Comentario <span class="st-req-badge">REQUERIDO</span></div>
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
    <div style="margin-top:1.2rem;text-align:right;"><button class="st-cancel" id="st-detail-close">Cerrar</button></div>
  </div>
</div>

<!-- ── SHARE MODAL ── -->
<div class="share-modal" id="share-modal">
  <div class="share-box">
    <h3>Compartir venta</h3>
    <p id="share-modal-info">Folio: —</p>
    <div id="share-unshare-area" style="display:none">
      <button class="unshare-btn" id="unshare-btn">🚫 Quitar compartido (actualmente con @<span id="share-current-user">—</span>)</button>
    </div>
    <div class="slbl" style="margin-top:.5rem">Compartir con:</div>
    <div class="share-user-list" id="share-user-list"></div>
    <div class="share-actions">
      <button class="st-cancel" id="share-cancel">Cancelar</button>
      <button class="share-save" id="share-save">📤 Compartir</button>
    </div>
  </div>
</div>

<!-- ── CHAT: NUEVO CONTACTO ── -->
<div class="generic-modal" id="chat-modal">
  <div class="generic-box">
    <h3>Nueva conversación</h3>
    <div class="field"><label>Selecciona a quién escribirle</label>
      <select id="chat-select-user" style="font-family:'Outfit',sans-serif;font-size:13px;"></select>
    </div>
    <div class="gmod-btns">
      <button class="st-cancel" id="chat-modal-cancel">Cancelar</button>
      <button class="chat-send" id="chat-modal-ok" style="padding:10px 22px;">Abrir chat</button>
    </div>
  </div>
</div>

<!-- ── CHAT: NUEVO GRUPO ── -->
<div class="generic-modal" id="grp-modal">
  <div class="generic-box">
    <h3>Crear grupo</h3>
    <div class="field"><label>Nombre del grupo</label><input type="text" id="grp-name-input" placeholder="Ej. Equipo Norte"></div>
    <div class="slbl" style="margin-top:.5rem">Selecciona miembros:</div>
    <div class="grp-member-list" id="grp-member-list"></div>
    <div class="gmod-btns">
      <button class="st-cancel" id="grp-modal-cancel">Cancelar</button>
      <button class="chat-send" id="grp-modal-ok" style="padding:10px 22px;background:linear-gradient(135deg,var(--green),#059669);">Crear grupo</button>
    </div>
  </div>
</div>

<!-- ── NOTIFICATION TOAST ── -->
<div class="notif-toast" id="notif-toast">
  <div class="notif-icon">💬</div>
  <div style="flex:1;min-width:0">
    <div class="notif-from" id="notif-from"></div>
    <div class="notif-text" id="notif-text"></div>
  </div>
  <button class="notif-close" onclick="document.getElementById('notif-toast').classList.remove('show')">✕</button>
</div>

<!-- ── IMAGE LIGHTBOX ── -->
<div id="img-lightbox" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,.9);z-index:9999;align-items:center;justify-content:center;cursor:zoom-out;" onclick="this.style.display='none'">
  <img id="img-lightbox-src" src="" style="max-width:90vw;max-height:90vh;border-radius:10px;box-shadow:0 20px 60px rgba(0,0,0,.8);">
</div>

<script>
const API_URL='https://domelike-rubdown-hatching.ngrok-free.dev';
const FIXED_ACCOUNTS=[{username:'wliseo',password:'wliseo777',name:'Wliseo',role:'superadmin'}];

/* ── API ── */
async function api(action,body={}){
  try{
    const h={'Content-Type':'application/json','ngrok-skip-browser-warning':'true'};
    if(action==='getSales'){const r=await fetch(`${API_URL}/api/ventas`,{headers:h});setDbS(true);return{ok:true,data:await r.json()};}
    if(action==='addSale'){const r=await fetch(`${API_URL}/api/ventas`,{method:'POST',headers:h,body:JSON.stringify(body)});setDbS(true);return await r.json();}
    if(action==='deleteSale'){await fetch(`${API_URL}/api/ventas/${body.folio}`,{method:'DELETE',headers:h});setDbS(true);return{ok:true};}
    if(action==='clearSales'){await fetch(`${API_URL}/api/ventas`,{method:'DELETE',headers:h});setDbS(true);return{ok:true};}
    if(action==='updateSale'){const r=await fetch(`${API_URL}/api/ventas/${body.folio}`,{method:'PUT',headers:h,body:JSON.stringify(body)});setDbS(true);return await r.json();}
    if(action==='getUsers'){const r=await fetch(`${API_URL}/api/usuarios`,{headers:h});setDbS(true);return{ok:true,data:await r.json()};}
    if(action==='addUser'){const r=await fetch(`${API_URL}/api/usuarios`,{method:'POST',headers:h,body:JSON.stringify(body)});setDbS(true);return await r.json();}
    if(action==='deleteUser'){await fetch(`${API_URL}/api/usuarios/${body.username}`,{method:'DELETE',headers:h});setDbS(true);return{ok:true};}
    return{ok:false,error:'Acción desconocida'};
  }catch(e){setDbS(false);return{ok:false,error:''+e.message};}
}
function setDbS(ok){const el=document.getElementById('srv-status');if(!el)return;el.className=ok?'srv-status srv-ok':'srv-status srv-err';el.textContent=ok?'✓ Conectado':'✕ Sin conexión';}


/* ── STATE ── */
let CU=null,SALES_CACHE=[],USERS_CACHE=[],currentSaleForStatus=null;
let CHAT_ACTIVE=null,CHAT_POLL=null,SHARE_FOLIO=null,SHARE_PICKED=null,CHAT_IMG_DATA=null;

/* ── UTILS ── */
function esc(s){return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}
function fmt(ts){if(!ts)return'—';const d=new Date(ts);return d.toLocaleDateString('es-MX',{day:'2-digit',month:'short',year:'numeric'})+' '+d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});}
function fmtDate(s){if(!s)return'—';const[y,m,d]=s.split('-');return`${parseInt(d)} ${['Ene','Feb','Mar','Abr','May','Jun','Jul','Ago','Sep','Oct','Nov','Dic'][parseInt(m)-1]} ${y}`;}
function fmtTime(ts){if(!ts)return'';const d=new Date(ts),now=new Date();if(d.toDateString()===now.toDateString())return d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});return d.toLocaleDateString('es-MX',{day:'2-digit',month:'short'})+' '+d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});}
function ini(n){return(n||'?').trim().split(/\s+/).slice(0,2).map(w=>w[0]||'').join('').toUpperCase()||'?';}
function genFolio(){return'WLS-'+String(Date.now()).slice(-6);}
function spin(on){document.getElementById('spinner').classList.toggle('show',on);}
function showToast(id,msg,type){const el=document.getElementById(id);if(!el)return;el.textContent=msg;el.className='toast '+type+' show';clearTimeout(el._t);el._t=setTimeout(()=>el.classList.remove('show'),4000);}
function getComment(s){if(!s.comentarios)return s.notaEstado||'';return s.comentarios[s.estado||'pendiente']||'';}
function eCls(e){return{pendiente:'pend',declino:'decl',preasignado:'pre',vendida:'ok'}[e]||'none';}
function eTxt(e){return{pendiente:'📞 Pendiente',declino:'❌ Declinó',preasignado:'⭐ Preasignado',vendida:'✅ Vendida'}[e]||'⬜ Sin estado';}
function isAdmin(){return CU&&(CU.role==='admin'||CU.role==='superadmin');}
function getAllUsers(){
  const a=[];
  FIXED_ACCOUNTS.forEach(u=>{if(u.username!==CU.username)a.push({username:u.username,name:u.name,role:u.role});});
  USERS_CACHE.forEach(u=>{if(u.username!==CU.username&&!a.find(x=>x.username===u.username))a.push({username:u.username,name:u.name,role:u.role});});
  return a;
}

/* ── LOGIN / BOOT ── */
async function doLogin(){
  const u=(document.getElementById('l-user').value||'').trim().toLowerCase();
  const p=document.getElementById('l-pass').value;
  const errEl=document.getElementById('login-err');
  errEl.classList.remove('show');
  if(!u||!p){errEl.textContent='Escribe usuario y contraseña';errEl.classList.add('show');return;}
  const fixed=FIXED_ACCOUNTS.find(x=>x.username===u&&x.password===p);
  if(fixed){CU={...fixed};await bootApp();return;}
  spin(true);const r=await api('getUsers');spin(false);
  if(!r.ok){errEl.textContent='Error: '+r.error;errEl.classList.add('show');return;}
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
  buildNav();buildBen();
  reqNotifPerm();
  if(isAdmin())await goPage('dash');else await goPage('exec');
}

/* ── NAV ── */
function buildNav(){
  const tabs=document.getElementById('n-tabs');
  if(isAdmin()){
    tabs.innerHTML='<button class="tab gold" data-pg="dash">Dashboard</button><button class="tab gold" data-pg="stats">Estadísticas</button><button class="tab gold" data-pg="ben">Beneficios</button><button class="tab gold" data-pg="users">Usuarios</button><button class="tab gold tchat" data-pg="chat">💬 Chat<span class="chat-unread-dot" id="nav-chat-dot"></span></button>';
  }else{
    tabs.innerHTML='<button class="tab" data-pg="exec">Registrar</button><button class="tab" data-pg="stats">Estadísticas</button><button class="tab" data-pg="ben">Beneficios</button><button class="tab tchat" data-pg="chat">💬 Chat<span class="chat-unread-dot" id="nav-chat-dot"></span></button>';
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
  document.querySelector(`.tab[data-pg="${p}"]`)?.classList.add('on');
  if(p==='exec'){setTodayDate();refreshFolio();await renderRecent();}
  if(p==='stats')await renderStats();
  if(p==='dash')await loadDash();
  if(p==='users')await loadUsers();
  if(p==='chat')await initChat();
}
function setTodayDate(){const el=document.getElementById('f-fecha');if(el&&!el.value)el.value=new Date().toISOString().slice(0,10);}
function refreshFolio(){const el=document.getElementById('folio-pill');if(el)el.textContent=genFolio();}

/* ── FORM CHANGES ── */
document.addEventListener('change',function(e){
  if(e.target.name==='f-estado'){
    const map={pendiente:'eopt-pend',preasignado:'eopt-pre',declino:'eopt-decl',vendida:'eopt-ok'};
    const sel={pendiente:'sel-pend',preasignado:'sel-pre',declino:'sel-decl',vendida:'sel-ok'};
    Object.values(map).forEach(id=>{const el=document.getElementById(id);if(el)el.className='estado-opt';});
    const s=map[e.target.value];if(s){const el=document.getElementById(s);if(el)el.className='estado-opt '+sel[e.target.value];}
  }
  if(e.target.name==='st-radio')
    document.querySelectorAll('.st-comment-block').forEach(b=>b.classList.toggle('highlighted',b.dataset.estado===e.target.value));
});

/* ── REGISTRAR VENTA ── */
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
  const alertEl=document.getElementById('req-alert');
  alertEl.classList.remove('show');
  if(!cliente){alertEl.textContent='⚠ Escribe el nombre del cliente';alertEl.classList.add('show');return;}
  if(!tarjeta){alertEl.textContent='⚠ Selecciona el tipo de tarjeta';alertEl.classList.add('show');return;}
  if(!fecha){alertEl.textContent='⚠ Selecciona la fecha de venta';alertEl.classList.add('show');return;}
  if(!estado){alertEl.textContent='⚠ Selecciona el estado de la venta';alertEl.classList.add('show');return;}
  if(!comentario){alertEl.textContent='⚠ Escribe un comentario';alertEl.classList.add('show');return;}
  if(!folio)folio=genFolio();
  document.getElementById('reg-btn').disabled=true;spin(true);
  const comentarios={pendiente:'',preasignado:'',declino:'',vendida:''};
  comentarios[estado]=comentario;
  const r=await api('addSale',{folio,exec:CU.name,username:CU.username,cliente,tel,tarjeta,fecha,registrado:new Date().toISOString(),rfc:rfc||null,ingresos:ingresos||null,tarjetaRef:tarjetaRef||null,ldcRef:ldcRef||null,estado,comentarios,notaEstado:comentario});
  spin(false);document.getElementById('reg-btn').disabled=false;
  if(!r.ok){alertEl.textContent='Error: '+r.error;alertEl.classList.add('show');return;}
  ['f-cliente','f-tel','f-folio','f-rfc','f-ingresos','f-tarjetaRef','f-ldcRef','f-comentario'].forEach(id=>{const el=document.getElementById(id);if(el)el.value='';});
  document.getElementById('f-tarjeta').value='';
  document.getElementById('f-fecha').value=new Date().toISOString().slice(0,10);
  document.querySelectorAll('input[name="f-estado"]').forEach(r=>r.checked=false);
  ['eopt-pend','eopt-pre','eopt-decl','eopt-ok'].forEach(id=>{const el=document.getElementById(id);if(el)el.className='estado-opt';});
  refreshFolio();showToast('t-ok','✓ Venta registrada — Folio '+folio,'ok');
  await renderRecent();
}

/* ── RENDER RECENT ── */
async function renderRecent(){
  const list=document.getElementById('exec-recent');
  const r=await api('getSales');
  if(!r.ok){list.innerHTML='<p style="color:#fca5a5;font-size:13px">Error al cargar.</p>';return;}
  const data=r.data.filter(v=>v.username===CU.username||(v.sharedWith&&v.sharedWith===CU.username)).slice(0,12);
  if(!data.length){list.innerHTML='<p style="color:var(--mu);font-size:13px">Aún no tienes ventas registradas.</p>';return;}
  list.innerHTML=data.map(v=>{
    const com=getComment(v);const isMine=v.username===CU.username;
    const shBadge=!isMine?`<span class="shared-badge">📥 De @${esc(v.username)}</span>`:v.sharedWith?`<span class="shared-badge shared-out">📤 @${esc(v.sharedWith)}</span>`:'';
    const shareBtn=isMine?`<button class="share-btn-tbl${v.sharedWith?' shared':''}" onclick="openShareModal('${esc(v.folio)}')" title="${v.sharedWith?'Cambiar/quitar compartido':'Compartir con otro ejecutivo'}">${v.sharedWith?'🔄 @'+esc(v.sharedWith):'📤 Compartir'}</button>`:'';
    return`<div class="ri">
      <div style="flex:1;min-width:0">
        <div class="ri-n">${esc(v.cliente)}${v.rfc?' 📄':''}${v.ingresos?' 💰':''}</div>
        <div class="ri-m">${esc(v.tarjeta)}${v.tel?' · '+esc(v.tel):''} · ${fmtDate(v.fecha)}</div>
        ${shBadge}
        ${com?`<div class="nota-preview" title="${esc(com)}">💬 ${esc(com)}</div>`:''}
      </div>
      <div class="ri-actions">
        <span class="ri-f">${esc(v.folio)}</span>
        <span class="st-badge st-${eCls(v.estado)}" onclick="openStatusModalFromFolio('${esc(v.folio)}')">${eTxt(v.estado)}</span>
        ${shareBtn}
      </div>
    </div>`;
  }).join('');
}

/* ── SHARE ── */
async function openShareModal(folio){
  SHARE_FOLIO=folio;SHARE_PICKED=null;
  // Try to find in cache, otherwise fetch
  let sale=SALES_CACHE.find(v=>v.folio===folio);
  if(!sale){
    spin(true);
    const r=await api('getSales');spin(false);
    if(r.ok){SALES_CACHE=r.data||[];sale=SALES_CACHE.find(v=>v.folio===folio)||{folio};}
    else sale={folio};
  }
  // Ensure users are loaded
  if(USERS_CACHE.length===0){spin(true);const r=await api('getUsers');spin(false);if(r.ok)USERS_CACHE=r.data||[];}
  document.getElementById('share-modal-info').textContent='Folio: '+folio+(sale.cliente?' · '+sale.cliente:'');
  const uArea=document.getElementById('share-unshare-area');
  if(sale.sharedWith){
    uArea.style.display='block';
    document.getElementById('share-current-user').textContent=sale.sharedWith;
  }else{uArea.style.display='none';}
  const users=getAllUsers();
  if(!users.length){document.getElementById('share-user-list').innerHTML='<p style="color:var(--mu);font-size:13px">No hay otros ejecutivos registrados.</p>';}
  else{
    document.getElementById('share-user-list').innerHTML=users.map(u=>`
      <div class="user-pick-item" data-u="${esc(u.username)}" onclick="pickShareUser('${esc(u.username)}')">
        <div class="upi-av">${ini(u.name)}</div>
        <div><div class="upi-name">${esc(u.name)}</div><div class="upi-user">@${esc(u.username)}</div></div>
      </div>`).join('');
  }
  document.getElementById('share-modal').classList.add('show');
}
window.pickShareUser=function(username){
  document.querySelectorAll('.user-pick-item').forEach(x=>x.classList.remove('picked'));
  const el=document.querySelector(`.user-pick-item[data-u="${username}"]`);
  if(el)el.classList.add('picked');
  SHARE_PICKED=username;
};
async function doShareSale(remove=false){
  if(!SHARE_FOLIO)return;
  if(!remove&&!SHARE_PICKED){alert('Selecciona un ejecutivo de la lista.');return;}
  spin(true);
  const payload={folio:SHARE_FOLIO,sharedWith:remove?null:SHARE_PICKED};
  const r=await api('updateSale',payload);
  spin(false);
  if(!r.ok){alert('Error al guardar: '+(r.error||'inténtalo de nuevo'));return;}
  document.getElementById('share-modal').classList.remove('show');
  // Update local cache
  const idx=SALES_CACHE.findIndex(v=>v.folio===SHARE_FOLIO);
  if(idx>-1)SALES_CACHE[idx].sharedWith=remove?null:SHARE_PICKED;
  // Show toast + refresh
  const toastId=document.getElementById('t-ok')?'t-ok':'u-ok';
  if(remove){
    showToast(toastId,'✓ Compartido eliminado correctamente','ok');
  }else{
    const u=getAllUsers().find(x=>x.username===SHARE_PICKED);
    showToast(toastId,'✓ Venta compartida con '+(u?u.name:'@'+SHARE_PICKED),'ok');
  }
  if(document.getElementById('pg-exec').classList.contains('on'))await renderRecent();
  if(document.getElementById('pg-dash').classList.contains('on'))renderDashTable();
}

/* ── STATS ── */
const eLabels={pendiente:'📞 Pendiente',preasignado:'⭐ Preasignado',declino:'❌ Declinó',vendida:'✅ Vendida'};
async function renderStats(){
  const r=await api('getSales');if(!r.ok)return;
  const all=r.data,today=new Date().toDateString();
  const mine=all.filter(v=>v.username===CU.username||(v.sharedWith&&v.sharedWith===CU.username));
  document.getElementById('stats-sub').textContent=isAdmin()?'Vista completa del equipo':'Tu rendimiento y estadísticas globales';
  const vend=all.filter(v=>v.estado==='vendida').length;
  const pct=all.length?Math.round(vend/all.length*100):0;
  document.getElementById('stats-global-cards').innerHTML=`
    <div class="sc"><div class="sc-l">Total equipo</div><div class="sc-v cv-g">${all.length}</div></div>
    <div class="sc"><div class="sc-l">Hoy</div><div class="sc-v cv-gr">${all.filter(v=>v.registrado&&new Date(v.registrado).toDateString()===today).length}</div></div>
    <div class="sc"><div class="sc-l">Esta semana</div><div class="sc-v cv-p">${all.filter(v=>v.registrado&&new Date(v.registrado).getTime()>Date.now()-7*86400000).length}</div></div>
    <div class="sc"><div class="sc-l">Vendidas ✅</div><div class="sc-v cv-gr">${vend}<span style="font-size:1rem;color:var(--mu)"> (${pct}%)</span></div></div>`;
  const byT={};all.forEach(v=>{if(!byT[v.tarjeta])byT[v.tarjeta]={t:0,v:0};byT[v.tarjeta].t++;if(v.estado==='vendida')byT[v.tarjeta].v++;});
  document.getElementById('stats-global-tarjeta').innerHTML=Object.entries(byT).sort((a,b)=>b[1].t-a[1].t).map(([t,c])=>`<tr><td>${esc(t)}</td><td><strong>${c.t}</strong></td><td style="color:var(--green)">${c.v}</td></tr>`).join('')||'<tr><td colspan="3" style="color:var(--mu);text-align:center">Sin datos</td></tr>';
  const byE={pendiente:0,preasignado:0,declino:0,vendida:0};all.forEach(v=>{const e=v.estado||'pendiente';byE[e]=(byE[e]||0)+1;});
  document.getElementById('stats-global-estado').innerHTML=Object.entries(byE).map(([e,c])=>`<tr><td>${eLabels[e]}</td><td><strong>${c}</strong></td><td style="color:var(--mu2)">${all.length?Math.round(c/all.length*100):0}%</td></tr>`).join('');
  const misSec=document.getElementById('stats-mis-section');
  if(isAdmin()){misSec.style.display='none';}else{
    misSec.style.display='block';
    const mv=mine;
    document.getElementById('stats-mis-cards').innerHTML=`
      <div class="sc"><div class="sc-l">Mis ventas</div><div class="sc-v cv-g">${mv.length}</div></div>
      <div class="sc"><div class="sc-l">Hoy</div><div class="sc-v cv-gr">${mv.filter(v=>v.registrado&&new Date(v.registrado).toDateString()===today).length}</div></div>
      <div class="sc"><div class="sc-l">Semana</div><div class="sc-v cv-p">${mv.filter(v=>v.registrado&&new Date(v.registrado).getTime()>Date.now()-7*86400000).length}</div></div>
      <div class="sc"><div class="sc-l">Vendidas ✅</div><div class="sc-v cv-gr">${mv.filter(v=>v.estado==='vendida').length}</div></div>`;
    const mbt={};mv.forEach(v=>{mbt[v.tarjeta]=(mbt[v.tarjeta]||0)+1;});
    document.getElementById('stats-mis-tarjeta').innerHTML=Object.entries(mbt).sort((a,b)=>b[1]-a[1]).map(([t,c])=>`<tr><td>${esc(t)}</td><td><strong>${c}</strong></td></tr>`).join('')||'<tr><td colspan="2" style="color:var(--mu);text-align:center">Sin datos</td></tr>';
    const mbe={pendiente:0,preasignado:0,declino:0,vendida:0};mv.forEach(v=>{const e=v.estado||'pendiente';mbe[e]=(mbe[e]||0)+1;});
    document.getElementById('stats-mis-estado').innerHTML=Object.entries(mbe).map(([e,c])=>`<tr><td>${eLabels[e]}</td><td><strong>${c}</strong></td></tr>`).join('');
  }
  const execSec=document.getElementById('stats-exec-section');
  if(isAdmin()){
    execSec.style.display='block';
    const bxe={};all.forEach(v=>{if(!bxe[v.exec])bxe[v.exec]=[];bxe[v.exec].push(v);});
    const list=document.getElementById('stats-exec-list');
    if(!Object.keys(bxe).length){list.innerHTML='<p style="color:var(--mu);font-size:13px">Sin ventas aún.</p>';return;}
    list.innerHTML=Object.entries(bxe).sort((a,b)=>b[1].length-a[1].length).map(([name,vs])=>{
      const vd=vs.filter(v=>v.estado==='vendida').length;
      const hy=vs.filter(v=>v.registrado&&new Date(v.registrado).toDateString()===today).length;
      const sm=vs.filter(v=>v.registrado&&new Date(v.registrado).getTime()>Date.now()-7*86400000).length;
      const bte={};vs.forEach(v=>{bte[v.tarjeta]=(bte[v.tarjeta]||0)+1;});
      const bee={pendiente:0,preasignado:0,declino:0,vendida:0};vs.forEach(v=>{const e=v.estado||'pendiente';bee[e]=(bee[e]||0)+1;});
      return`<div class="exec-accordion"><div class="exec-acc-head" onclick="this.nextElementSibling.classList.toggle('open');this.querySelector('.arr').textContent=this.nextElementSibling.classList.contains('open')?'▲':'▼'">
        <span style="font-weight:700">${esc(name)}</span>
        <span style="display:flex;gap:8px;align-items:center"><span class="badge b-b">${vs.length} ventas</span><span class="badge b-gr">${vd} vendidas</span><span class="arr" style="color:var(--mu);font-size:12px">▼</span></span>
      </div>
      <div class="exec-acc-body">
        <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(100px,1fr));gap:8px;margin-bottom:10px">
          <div class="sc" style="padding:.6rem .9rem"><div class="sc-l">Total</div><div class="sc-v cv-g" style="font-size:1.5rem">${vs.length}</div></div>
          <div class="sc" style="padding:.6rem .9rem"><div class="sc-l">Hoy</div><div class="sc-v cv-gr" style="font-size:1.5rem">${hy}</div></div>
          <div class="sc" style="padding:.6rem .9rem"><div class="sc-l">Semana</div><div class="sc-v cv-p" style="font-size:1.5rem">${sm}</div></div>
          <div class="sc" style="padding:.6rem .9rem"><div class="sc-l">Vendidas</div><div class="sc-v cv-gr" style="font-size:1.5rem">${vd}</div></div>
        </div>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
          <div><div class="slbl" style="margin-top:0">Por tarjeta</div><table class="mini-table"><thead><tr><th>Tarjeta</th><th>Cant.</th></tr></thead><tbody>${Object.entries(bte).sort((a,b)=>b[1]-a[1]).map(([t,c])=>`<tr><td>${esc(t)}</td><td><strong>${c}</strong></td></tr>`).join('')}</tbody></table></div>
          <div><div class="slbl" style="margin-top:0">Por estado</div><table class="mini-table"><thead><tr><th>Estado</th><th>Cant.</th></tr></thead><tbody>${Object.entries(bee).map(([e,c])=>`<tr><td style="font-size:11px">${eLabels[e]}</td><td><strong>${c}</strong></td></tr>`).join('')}</tbody></table></div>
        </div>
      </div></div>`;
    }).join('');
  }else{execSec.style.display='none';}
}

/* ── DASHBOARD ── */
function setSyncS(s,m){const dot=document.getElementById('sync-dot'),txt=document.getElementById('sync-txt');if(!dot)return;dot.className='sync-dot '+s;txt.textContent=m;}
async function loadDash(){
  setSyncS('loading','Cargando datos…');
  const r=await api('getSales');if(!r.ok){setSyncS('err','Error: '+r.error);return;}
  SALES_CACHE=r.data||[];setSyncS('ok','Sincronizado · '+SALES_CACHE.length+' ventas');renderDashTable();
}
window.openStatusModalFromFolio=function(folio){
  let s=SALES_CACHE.find(v=>v.folio===folio);
  if(s){openStatusModal(s);return;}
  api('getSales').then(r=>{if(r.ok){const x=r.data.find(v=>v.folio===folio);if(x)openStatusModal(x);}});
};
function openStatusModal(sale){
  currentSaleForStatus=sale;
  document.getElementById('st-modal-client').textContent=`Cliente: ${sale.cliente} — Folio: ${sale.folio}`;
  const estado=sale.estado||'pendiente';
  const radio=document.querySelector(`input[name="st-radio"][value="${estado}"]`);if(radio)radio.checked=true;
  const c=sale.comentarios||{},l=sale.notaEstado||'';
  document.getElementById('st-nota-pend').value=c.pendiente||(estado==='pendiente'?l:'');
  document.getElementById('st-nota-pre').value=c.preasignado||(estado==='preasignado'?l:'');
  document.getElementById('st-nota-decl').value=c.declino||(estado==='declino'?l:'');
  document.getElementById('st-nota-ok').value=c.vendida||(estado==='vendida'?l:'');
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
  const tbody=document.getElementById('t-body'),empty=document.getElementById('t-empty');
  if(!data.length){tbody.innerHTML='';empty.style.display='block';}
  else{
    empty.style.display='none';
    const _TD='padding:9px 13px;color:#EBF1FF;font-size:13px;font-weight:500;vertical-align:middle;border-bottom:1px solid rgba(255,255,255,.06);';
    const _TDM='padding:9px 13px;color:#8BA3C0;font-size:12px;vertical-align:middle;border-bottom:1px solid rgba(255,255,255,.06);';
    tbody.innerHTML=data.map((v,i)=>{
      const com=getComment(v);
      const bg=i%2===0?'#0F1219':'#161B26';
      const shared=v.sharedWith?`<span class="badge b-c">📤 @${esc(v.sharedWith)}</span>`:'<span style="color:#445">—</span>';
      return`<tr style="background:${bg}" onmouseover="this.style.background='#232B3E'" onmouseout="this.style.background='${bg}'">
        <td style="${_TD}font-family:monospace;color:#F0C060;font-weight:700;">${esc(v.folio)}</td>
        <td style="${_TD}font-weight:700;">${esc(v.exec)}</td>
        <td style="${_TD}">${esc(v.cliente)}</td>
        <td style="${_TDM}">${esc(v.tel||'—')}</td>
        <td style="${_TD}"><span class="badge b-r">${esc(v.tarjeta)}</span></td>
        <td style="${_TD}"><span class="st-badge st-${eCls(v.estado)}" onclick="openStatusModalFromFolio('${esc(v.folio)}')">${eTxt(v.estado)}</span></td>
        <td style="${_TDM}max-width:170px;">${com?`<span style="cursor:pointer;color:#c4b5fd" onclick="showStatusNote('${com.replace(/'/g,"\\'")}')">💬 ${esc(com.slice(0,35))}${com.length>35?'…':''}</span>`:'<span style="color:#445">—</span>'}</td>
        <td style="${_TD}">${shared}</td>
        <td style="${_TDM}">${fmtDate(v.fecha)}</td>
        <td style="${_TDM}">${fmt(v.registrado)}</td>
        <td style="${_TD}display:flex;gap:4px;align-items:center;">
          <button class="share-btn-tbl" onclick="openShareModal('${esc(v.folio)}')" title="${v.sharedWith?'Reasignar/Quitar':'Compartir'}">📤</button>
          <button class="delbtn" data-folio="${esc(v.folio)}">✕</button>
        </td>
      </tr>`;
    }).join('');
  }
  const counts={};all.forEach(v=>{counts[v.exec]=(counts[v.exec]||0)+1;});
  const sorted=Object.entries(counts).sort((a,b)=>b[1]-a[1]).slice(0,12);
  document.getElementById('rank-grid').innerHTML=sorted.length?sorted.map(([name,cnt],i)=>`<div class="rcard"><div class="rpos ${['rp1','rp2','rp3'][i]||''}">${i+1}</div><div><div class="rkn">${esc(name)}</div><div class="rkc">${cnt} venta${cnt!==1?'s':''}</div></div></div>`).join(''):'<p style="color:var(--mu);font-size:13px">Sin datos aún.</p>';
}
window.showStatusNote=function(n){document.getElementById('st-detail-txt').textContent=n;document.getElementById('st-detail-pop').classList.add('show');};
async function delSale(folio){
  if(!confirm('¿Eliminar la venta '+folio+'?'))return;
  spin(true);const r=await api('deleteSale',{folio});spin(false);
  if(!r.ok){alert('Error: '+r.error);return;}
  SALES_CACHE=SALES_CACHE.filter(v=>v.folio!==folio);renderDashTable();setSyncS('ok','Sincronizado · '+SALES_CACHE.length+' ventas');
}
function exportarExcel(){
  if(!SALES_CACHE.length){alert('No hay ventas para exportar.');return;}
  const cols=['Folio','Ejecutivo','Cliente','Teléfono','Tarjeta','Estado','Comentario','Compartida','Fecha','Registrado','RFC','Ingresos','Ref Tarjeta','Ref LDC'];
  const rows=SALES_CACHE.map(v=>[v.folio,v.exec,v.cliente,v.tel||'',v.tarjeta,v.estado||'',getComment(v).replace(/"/g,"'"),v.sharedWith||'',fmtDate(v.fecha),fmt(v.registrado),v.rfc||'',v.ingresos||'',v.tarjetaRef||'',v.ldcRef||''].map(c=>`"${c}"`).join(','));
  const csv=[cols.map(c=>`"${c}"`).join(','),...rows].join('\n');
  const blob=new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'});
  const url=URL.createObjectURL(blob);const a=document.createElement('a');a.href=url;a.download='wliseos_'+new Date().toISOString().slice(0,10)+'.csv';a.click();URL.revokeObjectURL(url);
}

/* ── USERS ── */
async function loadUsers(){
  spin(true);const r=await api('getUsers');spin(false);
  if(!r.ok){showToast('u-err','Error al cargar usuarios','err');return;}
  USERS_CACHE=r.data||[];renderUsersUI();
}
function renderUsersUI(){
  const isSup=CU.role==='superadmin';
  const fx=FIXED_ACCOUNTS.map(u=>`<div class="ucard"><div class="uav av-s">${ini(u.name)}</div><div class="ui"><div class="un">${esc(u.name)}</div><div class="ur"><span class="badge b-p">@${esc(u.username)} · superadmin</span></div></div></div>`).join('');
  const uc=USERS_CACHE.length?USERS_CACHE.map(u=>{const rl=u.role==='admin'?'admin':'ejecutivo';const bc=u.role==='admin'?'b-g':'b-b';return`<div class="ucard"><div class="uav av-e">${ini(u.name)}</div><div class="ui"><div class="un">${esc(u.name)}</div><div class="ur"><span class="badge ${bc}">@${esc(u.username)} · ${rl}</span></div></div>${isSup?`<button class="del-u" data-uname="${esc(u.username)}">Eliminar</button>`:''}</div>`;}).join(''):'<p style="color:var(--mu);font-size:13px;margin-top:4px">No hay usuarios aún.</p>';
  document.getElementById('ugrid').innerHTML=fx+uc;
}
async function addUser(){
  const name=(document.getElementById('nu-name').value||'').trim();
  const username=(document.getElementById('nu-user').value||'').trim().toLowerCase().replace(/\s+/g,'');
  const password=document.getElementById('nu-pass').value;
  const role=CU.role==='superadmin'?(document.getElementById('nu-role').value||'exec'):'exec';
  if(!name||!username||!password){showToast('u-err','Completa todos los campos','err');return;}
  if(password.length<4){showToast('u-err','Contraseña mínimo 4 caracteres','err');return;}
  if(FIXED_ACCOUNTS.find(x=>x.username===username)){showToast('u-err','Usuario reservado','err');return;}
  document.getElementById('add-user-btn').disabled=true;
  spin(true);const r=await api('addUser',{name,username,password,role});spin(false);
  document.getElementById('add-user-btn').disabled=false;
  if(!r.ok){showToast('u-err',r.error||'Error','err');return;}
  document.getElementById('nu-name').value='';document.getElementById('nu-user').value='';document.getElementById('nu-pass').value='';
  showToast('u-ok','Usuario "'+name+'" agregado ✓','ok');await loadUsers();
}


/* ── API chat endpoints ── */
async function api_getMessages(){
  try{
    const h={'Content-Type':'application/json','ngrok-skip-browser-warning':'true'};
    const r=await fetch(`${API_URL}/api/mensajes`,{headers:h});
    setDbS(true);return{ok:true,data:await r.json()};
  }catch(e){setDbS(false);return{ok:false,data:[]};}
}
async function api_sendMessage(msg){
  try{
    const h={'Content-Type':'application/json','ngrok-skip-browser-warning':'true'};
    const r=await fetch(`${API_URL}/api/mensajes`,{method:'POST',headers:h,body:JSON.stringify(msg)});
    setDbS(true);return await r.json();
  }catch(e){setDbS(false);return{ok:false};}
}

/* ── CHAT (API-based — idéntico al original que funciona) ── */
let CHAT_MESSAGES=[];
let _chatImgData=null,_chatPasteReady=false;
/* ── HIDDEN CONVS (localStorage) ── */
const LS_HIDDEN='wliseos_hidden_v1';
function hiddenLoad(){try{return JSON.parse(localStorage.getItem(LS_HIDDEN)||'{}');}catch{return{};}}
function hideConv(key){const h=hiddenLoad();h[CU.username+'_'+key]=Date.now();localStorage.setItem(LS_HIDDEN,JSON.stringify(h));}
function isHidden(key){const h=hiddenLoad();return !!(h[CU.username+'_'+key]);}
function unhide(key){const h=hiddenLoad();delete h[CU.username+'_'+key];localStorage.setItem(LS_HIDDEN,JSON.stringify(h));}

/* ── GROUPS (via API — syncs across devices) ── */
function myGroups(){
  // Groups are stored as special messages type='group_create' in the API
  const created={};
  CHAT_MESSAGES.forEach(m=>{
    if(!m||!m.type)return;
    if(m.type==='group_create'&&m.members&&m.members.includes(CU.username)){
      if(!created[m.groupId])created[m.groupId]={id:m.groupId,name:m.groupName,members:m.members,createdBy:m.from};
    }
    if(m.type==='group_delete'&&created[m.groupId])delete created[m.groupId];
  });
  return Object.values(created);
}

/* ── BROWSER NOTIFICATIONS ── */
async function reqNotifPerm(){if('Notification' in window&&Notification.permission==='default')await Notification.requestPermission();}
function showNotifToast(fromName,text){
  const t=document.getElementById('notif-toast');
  const f=document.getElementById('notif-from');
  const tx=document.getElementById('notif-text');
  if(!t)return;
  f.textContent=fromName;
  tx.textContent=text.length>80?text.slice(0,80)+'…':text;
  t.classList.add('show');
  clearTimeout(t._t);t._t=setTimeout(()=>t.classList.remove('show'),5000);
}
function fireNotification(fromName,text,groupName){
  const title=groupName?`👥 ${groupName}: ${fromName}`:`💬 ${fromName}`;
  const body=(text||'📎 Imagen').slice(0,120);
  // In-app toast ALWAYS (no permission needed)
  showNotifToast(title,body);
  // Browser notification - only if page is not focused
  if(document.hidden||!document.hasFocus()){
    if('Notification' in window&&Notification.permission==='granted'){
      try{
        const n=new Notification(title,{body,icon:'/favicon.ico',badge:'/favicon.ico',tag:'wliseos-msg-'+Date.now()});
        n.onclick=()=>{window.focus();goPage('chat');n.close();};
        setTimeout(()=>{try{n.close();}catch(e){}},7000);
      }catch(e){}
    }else if('Notification' in window&&Notification.permission!=='denied'){
      Notification.requestPermission().then(p=>{if(p==='granted')fireNotification(fromName,text,groupName);});
    }
  }
}

function getAllChatUsers(){
  const all=[];
  FIXED_ACCOUNTS.forEach(u=>{if(u.username!==CU.username)all.push({username:u.username,name:u.name,role:u.role});});
  USERS_CACHE.forEach(u=>{if(u.username!==CU.username&&!all.find(x=>x.username===u.username))all.push({username:u.username,name:u.name,role:u.role});});
  return all;
}
function chatLastRead(contact){try{return parseInt(localStorage.getItem('cr_'+CU.username+'_'+contact)||'0');}catch{return 0;}}
function chatMarkRead(contact){try{localStorage.setItem('cr_'+CU.username+'_'+contact,Date.now());}catch(e){}}
function fmtChatTime(ts){
  if(!ts)return'';
  const d=new Date(ts),now=new Date();
  if(d.toDateString()===now.toDateString())return d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});
  return d.toLocaleDateString('es-MX',{day:'2-digit',month:'short'})+' '+d.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'});
}
function chatAvCls(role){return role==='superadmin'?'cav-s':role==='admin'?'cav-a':'cav-e';}

async function initChat(){
  reqNotifPerm();
  document.getElementById('chat-sub').textContent=isAdmin()?'Vista completa · todos los mensajes del equipo':'Mensajes privados y grupos';
  if(USERS_CACHE.length===0){const r=await api('getUsers');if(r.ok)USERS_CACHE=r.data||[];}
  const r=await api_getMessages();
  CHAT_MESSAGES=r.ok?(r.data||[]):[];
  // Show group button for admins
  const grpBtn=document.getElementById('chat-grp-btn');
  if(grpBtn){grpBtn.classList.toggle('show',isAdmin());grpBtn.onclick=openGrpModal;}
  renderChatContacts();
  if(CHAT_ACTIVE)renderChatMessages();
  startChatPoll();
  document.getElementById('chat-new-btn').onclick=openChatModal;
  document.getElementById('chat-send-btn').onclick=sendChatMsg;
  document.getElementById('chat-input').onkeydown=function(e){if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();sendChatMsg();}};
  // Image input
  const imgInp=document.getElementById('chat-img-input');
  if(imgInp)imgInp.onchange=function(){
    const f=this.files[0];if(!f)return;
    const rd=new FileReader();
    rd.onload=ev=>{_chatImgData=ev.target.result;const t=document.getElementById('chat-img-prev-thumb');if(t)t.src=_chatImgData;const p=document.getElementById('chat-img-preview');if(p)p.classList.add('show');};
    rd.readAsDataURL(f);this.value='';
  };
  const imgClr=document.getElementById('chat-img-clear');
  if(imgClr)imgClr.onclick=()=>{_chatImgData=null;const p=document.getElementById('chat-img-preview');if(p)p.classList.remove('show');};
  if(!_chatPasteReady){
    _chatPasteReady=true;
    document.addEventListener('paste',function(e){
      if(!CHAT_ACTIVE||CHAT_ACTIVE.username==='__all__')return;
      if(!document.getElementById('pg-chat')?.classList.contains('on'))return;
      const items=e.clipboardData?.items;if(!items)return;
      for(const item of items){
        if(item.type.startsWith('image/')){
          const f=item.getAsFile();if(!f)continue;
          const rd=new FileReader();
          rd.onload=ev=>{_chatImgData=ev.target.result;const t=document.getElementById('chat-img-prev-thumb');if(t)t.src=_chatImgData;const p=document.getElementById('chat-img-preview');if(p)p.classList.add('show');};
          rd.readAsDataURL(f);e.preventDefault();break;
        }
      }
    });
  }
}

function startChatPoll(){
  stopChatPoll();
  CHAT_POLL=setInterval(async()=>{
    const prevIds=new Set(CHAT_MESSAGES.map(m=>m.timestamp+'__'+m.from+'__'+(m.to||'')));
    const r=await api_getMessages();
    if(r.ok){
      const newMsgs=r.data||[];
      // Detect new real chat messages (not group_create/delete meta)
      const incoming=newMsgs.filter(m=>{
        if(!m||!m.from||!m.to)return false;
        if(m.from===CU.username)return false;
        if(m.type==='group_create'||m.type==='group_delete')return false;
        const uid=m.timestamp+'__'+m.from+'__'+(m.to||'');
        if(prevIds.has(uid))return false;
        if(m.to===CU.username)return true;
        const myGrpIds=myGroups().map(g=>g.id);
        return myGrpIds.includes(m.to);
      });
      incoming.forEach(m=>{
        const grps=myGroups();
        const grp=grps.find(g=>g.id===m.to);
        const chatOpen=document.getElementById('pg-chat')?.classList.contains('on');
        const activeConv=CHAT_ACTIVE&&(CHAT_ACTIVE.username===m.from||(CHAT_ACTIVE.groupId&&CHAT_ACTIVE.groupId===m.to));
        if(!activeConv||!chatOpen){
          fireNotification(m.fromName||m.from,m.text||'📎 Imagen',grp?grp.name:null);
        }
      });
      CHAT_MESSAGES=newMsgs;
      renderChatContacts();
      if(CHAT_ACTIVE&&document.getElementById('pg-chat')?.classList.contains('on'))renderChatMessages(false);
    }
    updateChatDot();
  },5000);
}
function stopChatPoll(){if(CHAT_POLL){clearInterval(CHAT_POLL);CHAT_POLL=null;}}

function updateChatDot(){
  const dot=document.getElementById('nav-chat-dot');if(!dot||!CU)return;
  try{
    const lr_cache={};
    const chatLR=k=>{if(!(k in lr_cache))lr_cache[k]=chatLastRead(k);return lr_cache[k];};
    const myGrpIds=myGroups().map(g=>g.id);
    const hasUnread=CHAT_MESSAGES.some(m=>{
      if(!m||m.from===CU.username)return false;
      if(m.to===CU.username)return new Date(m.timestamp).getTime()>chatLR(m.from);
      if(myGrpIds.includes(m.to))return new Date(m.timestamp).getTime()>chatLR(m.to);
      return false;
    });
    dot.classList.toggle('show',hasUnread);
  }catch(e){}
}

function getConversations(){
  const convMap={};
  const users=getAllChatUsers();
  const groups=myGroups(); // from API messages type=group_create
  const grpIds=new Set(groups.map(g=>g.id));
  const grpMap={};
  groups.forEach(g=>{grpMap[g.id]={...g,messages:[]};});

  CHAT_MESSAGES.forEach(m=>{
    if(!m||!m.from||!m.to)return;
    if(m.type==='group_create'||m.type==='group_delete')return; // skip meta
    // Group chat message
    if(grpIds.has(m.to)){if(grpMap[m.to])grpMap[m.to].messages.push(m);return;}
    if((m.to||'').startsWith('grp_'))return; // unknown group, skip
    if(m.to==='__groups__')return; // meta messages
    // DM
    const myMsg=m.from===CU.username||m.to===CU.username;
    if(!isAdmin()&&!myMsg)return;
    const other=m.from===CU.username?m.to:m.from;
    const otherName=m.from===CU.username?(m.toName||m.to):(m.fromName||m.from);
    if(!convMap[other])convMap[other]={username:other,name:otherName,role:'exec',messages:[]};
    convMap[other].messages.push(m);
  });
  users.forEach(u=>{if(!convMap[u.username])convMap[u.username]={...u,messages:[]};});

  const sort=(a,b)=>{
    const ta=a.messages.length?new Date(a.messages[a.messages.length-1].timestamp).getTime():0;
    const tb=b.messages.length?new Date(b.messages[b.messages.length-1].timestamp).getTime():0;
    return tb-ta;
  };
  return{groups:Object.values(grpMap).sort(sort),dms:Object.values(convMap).sort(sort)};
}

function renderChatContacts(){
  const cont=document.getElementById('chat-contacts');if(!cont)return;
  const {groups,dms}=getConversations();
  let html='';
  if(isAdmin()){
    const allActive=CHAT_ACTIVE&&CHAT_ACTIVE.username==='__all__';
    html+=`<div class="chat-contact${allActive?' active':''}" onclick="selectChatContact('__all__','Todos los mensajes','admin')">
      <div class="chat-av cav-all">📋</div>
      <div class="chat-ci"><div class="chat-cn">Todos los mensajes</div><div class="chat-cl">${CHAT_MESSAGES.length} mensajes en total</div></div>
    </div>`;
  }
  // Groups first
  groups.filter(g=>!isHidden('grp_'+g.id)).forEach(g=>{
    const lm=g.messages[g.messages.length-1];
    const prev=lm?(lm.text?(lm.text.length>30?lm.text.slice(0,30)+'…':lm.text):'🖼 Imagen'):'Sin mensajes';
    const lr=chatLastRead(g.id);
    const unread=g.messages.filter(m=>m.from!==CU.username&&new Date(m.timestamp).getTime()>lr).length;
    const isAct=CHAT_ACTIVE&&CHAT_ACTIVE.groupId===g.id;
    const canDel=isAdmin()||g.createdBy===CU.username;
    html+=`<div class="chat-contact${isAct?' active':''}" onclick="selectChatGroup('${esc(g.id)}','${esc(g.name)}')">
      <div class="chat-av cav-grp">👥</div>
      <div class="chat-ci">
        <div class="chat-cn">${esc(g.name)}<span class="grp-badge">${g.members.length}</span></div>
        <div class="chat-cl">${lm?`${esc(lm.fromName||lm.from)}: ${esc(prev)}`:prev}</div>
      </div>
      ${unread>0?`<div class="chat-unread">${unread}</div>`:''}
      ${canDel?`<button class="conv-del-btn" onclick="event.stopPropagation();deleteGroup('${esc(g.id)}','${esc(g.name)}')" title="Eliminar grupo">🗑</button>`:''}
    </div>`;
  });
  if(!dms.length&&!groups.length){
    cont.innerHTML=html+'<div style="padding:1.5rem 1rem;text-align:center;color:var(--mu);font-size:13px">Sin conversaciones.<br><span style="font-size:11px">Presiona "+ Nuevo".</span></div>';
    return;
  }
  // DMs
  dms.filter(c=>c.username&&!isHidden('dm_'+c.username)).forEach(c=>{
    const lm=c.messages[c.messages.length-1];
    const lastText=lm?(lm.text?(lm.text.length>30?lm.text.slice(0,30)+'…':lm.text):'🖼 Imagen'):'Escribe el primer mensaje';
    const lr=chatLastRead(c.username);
    const unread=c.messages.filter(m=>m.from===c.username&&m.to===CU.username&&new Date(m.timestamp).getTime()>lr).length;
    const isActive=CHAT_ACTIVE&&CHAT_ACTIVE.username===c.username;
    html+=`<div class="chat-contact${isActive?' active':''}" onclick="selectChatContact('${esc(c.username)}','${esc(c.name||c.username)}','${c.role||'exec'}')">
      <div class="chat-av ${chatAvCls(c.role||'exec')}">${ini(c.name||c.username)}</div>
      <div class="chat-ci">
        <div class="chat-cn">${esc(c.name||c.username)}${(c.role==='admin'||c.role==='superadmin')?'<span style="font-size:9px;background:var(--gold-f);color:var(--gold);border-radius:3px;padding:1px 5px;margin-left:5px;font-weight:700;">ADMIN</span>':''}</div>
        <div class="chat-cl">${esc(lastText)}</div>
      </div>
      ${unread>0?`<div class="chat-unread">${unread}</div>`:''}
      <button class="conv-del-btn" onclick="event.stopPropagation();deleteConv('${esc(c.username)}')" title="Ocultar conversación">🗑</button>
    </div>`;
  });
  cont.innerHTML=html;
}

window.selectChatGroup=function(gid,gname){
  CHAT_ACTIVE={groupId:gid,name:gname};chatMarkRead(gid);
  document.getElementById('chat-main-head').style.display='flex';
  document.getElementById('chat-head-name').textContent=gname;
  const g=myGroups().find(x=>x.id===gid);
  document.getElementById('chat-head-sub').textContent=g?`${g.members.length} miembros · Grupo`:'Grupo';
  document.getElementById('chat-head-av').className='chat-av cav-grp';
  document.getElementById('chat-head-av').textContent='👥';
  document.getElementById('chat-input-area').style.display='flex';
  renderChatContacts();renderChatMessages();
  setTimeout(()=>document.getElementById('chat-input')?.focus(),80);
  updateChatDot();
};

window.selectChatContact=function(username,name,role){
  CHAT_ACTIVE={username,name,role};
  if(username!=='__all__')chatMarkRead(username);
  renderChatContacts();renderChatMessages();
  document.getElementById('chat-main-head').style.display='flex';
  document.getElementById('chat-head-name').textContent=username==='__all__'?'Todos los mensajes':name;
  document.getElementById('chat-head-sub').textContent=username==='__all__'?'Vista solo lectura · administradores':'@'+username;
  document.getElementById('chat-head-av').className='chat-av '+(username==='__all__'?'cav-all':chatAvCls(role));
  document.getElementById('chat-head-av').textContent=username==='__all__'?'📋':ini(name);
  document.getElementById('chat-input-area').style.display=username==='__all__'?'none':'flex';
  setTimeout(()=>document.getElementById('chat-input')?.focus(),80);
  updateChatDot();
};

function renderChatMessages(scroll=true){
  const msgEl=document.getElementById('chat-msgs');if(!msgEl||!CHAT_ACTIVE)return;
  if(CHAT_ACTIVE.username==='__all__'){
    const msgs=[...CHAT_MESSAGES].filter(m=>m&&m.from&&m.to&&m.type!=='group_create'&&m.type!=='group_delete'&&m.to!=='__groups__').sort((a,b)=>new Date(a.timestamp)-new Date(b.timestamp));
    if(!msgs.length){msgEl.innerHTML='<div class="chat-empty-state"><div class="ce-icon">📭</div><p>Sin mensajes todavía</p></div>';return;}
    msgEl.innerHTML=msgs.map(m=>`<div class="chat-all-msg">
      <div class="chat-all-meta">
        <span class="chat-all-from">${esc(m.fromName||m.from)}</span><span style="margin:0 3px;color:var(--mu)">→</span>
        <span class="chat-all-to">${esc(m.toName||m.to)}</span>
        <span style="margin-left:auto;color:var(--mu);font-size:10px">${fmtChatTime(m.timestamp)}</span>
      </div>
      <div class="chat-all-text">${m.text?esc(m.text):''}${m.img?`<img src="${m.img}" style="max-width:200px;border-radius:6px;display:block;margin-top:4px" alt="">`:''}</div>
    </div>`).join('');
  }else if(CHAT_ACTIVE.groupId){
    const msgs=CHAT_MESSAGES.filter(m=>m&&m.to===CHAT_ACTIVE.groupId).sort((a,b)=>new Date(a.timestamp)-new Date(b.timestamp));
    if(!msgs.length){msgEl.innerHTML=`<div class="chat-empty-state"><div class="ce-icon">👥</div><p>Sé el primero en escribir en <strong>${esc(CHAT_ACTIVE.name)}</strong></p><small>Todos los miembros del grupo verán este mensaje</small></div>`;return;}
    let html='',lastDay='';
    msgs.forEach(m=>{
      if(!m||!m.ts&&!m.timestamp)return;
      const ts=m.timestamp||m.ts;
      let day='';try{day=new Date(ts).toLocaleDateString('es-MX',{weekday:'long',day:'numeric',month:'long'});}catch(e){}
      if(day&&day!==lastDay){html+=`<div class="chat-day-sep"><span>${day}</span></div>`;lastDay=day;}
      const isMine=m.from===CU.username;
      const tp=m.text?`<span style="white-space:pre-wrap">${esc(m.text)}</span>`:'';
      const ip=m.img?`<img src="${m.img}" alt="" style="max-width:100%;border-radius:8px;display:block;margin-top:${m.text?'6':'0'}px;cursor:zoom-in" onclick="openChatLightbox(this.src)">`:'';
      html+=`<div class="chat-msg-wrap ${isMine?'mine':'theirs'}">
        ${!isMine?`<div class="chat-bname">${esc(m.fromName||m.from)}</div>`:''}
        <div class="chat-bubble ${isMine?'mine':'theirs'}">${tp}${ip}</div>
        <div class="chat-btime">${fmtChatTime(ts)}</div>
      </div>`;
    });
    msgEl.innerHTML=html;
  }else{
    const msgs=CHAT_MESSAGES.filter(m=>m&&m.from&&m.to&&((m.from===CU.username&&m.to===CHAT_ACTIVE.username)||(m.from===CHAT_ACTIVE.username&&m.to===CU.username))).sort((a,b)=>new Date(a.timestamp)-new Date(b.timestamp));
    if(!msgs.length){msgEl.innerHTML=`<div class="chat-empty-state"><div class="ce-icon">✉️</div><p>Escríbele a <strong>${esc(CHAT_ACTIVE.name)}</strong></p><small>Sé el primero en enviar un mensaje</small></div>`;return;}
    let html='',lastDay='';
    msgs.forEach(m=>{
      let day='';try{day=new Date(m.timestamp).toLocaleDateString('es-MX',{weekday:'long',day:'numeric',month:'long'});}catch(e){}
      if(day&&day!==lastDay){html+=`<div class="chat-day-sep"><span>${day}</span></div>`;lastDay=day;}
      const isMine=m.from===CU.username;
      const tp=m.text?`<span style="white-space:pre-wrap">${esc(m.text)}</span>`:'';
      const ip=m.img?`<img src="${m.img}" alt="" style="max-width:100%;border-radius:8px;display:block;margin-top:${m.text?'6':'0'}px;cursor:zoom-in" onclick="openChatLightbox(this.src)">`:'';
      html+=`<div class="chat-msg-wrap ${isMine?'mine':'theirs'}">
        ${!isMine?`<div class="chat-bname">${esc(m.fromName||m.from)}</div>`:''}
        <div class="chat-bubble ${isMine?'mine':'theirs'}">${tp}${ip}</div>
        <div class="chat-btime">${fmtChatTime(m.timestamp)}</div>
      </div>`;
    });
    msgEl.innerHTML=html;
  }
  if(scroll)setTimeout(()=>{if(msgEl)msgEl.scrollTop=msgEl.scrollHeight;},50);
}

window.openChatLightbox=function(src){const lb=document.getElementById('img-lightbox');if(lb){document.getElementById('img-lightbox-src').src=src;lb.style.display='flex';}};

async function sendChatMsg(){
  if(!CHAT_ACTIVE||(CHAT_ACTIVE.username==='__all__'))return;
  const input=document.getElementById('chat-input');
  const text=(input.value||'').trim();
  if(!text&&!_chatImgData)return;
  const btn=document.getElementById('chat-send-btn');btn.disabled=true;
  const isGroup=!!CHAT_ACTIVE.groupId;
  const toId=isGroup?CHAT_ACTIVE.groupId:CHAT_ACTIVE.username;
  const toName=CHAT_ACTIVE.name||CHAT_ACTIVE.username||'';
  const msg={from:CU.username,fromName:CU.name,to:toId,toName,text:text||'',timestamp:new Date().toISOString()};
  if(_chatImgData)msg.img=_chatImgData;
  input.value='';_chatImgData=null;
  const p=document.getElementById('chat-img-preview');if(p)p.classList.remove('show');
  const r=await api_sendMessage(msg);
  btn.disabled=false;
  if(r&&r.ok!==false){
    CHAT_MESSAGES.push(msg);
    chatMarkRead(toId);
    renderChatContacts();renderChatMessages(true);
  }else{input.value=text;alert('Error al enviar. Intenta de nuevo.');}
}

function openChatModal(){
  const users=getAllChatUsers();
  if(!users.length){alert('No hay otros usuarios registrados aún.');return;}
  let ex=document.getElementById('_cmod');if(ex)ex.remove();
  const m=document.createElement('div');m.id='_cmod';
  m.style.cssText='position:fixed;inset:0;background:rgba(0,0,0,.82);display:flex;align-items:center;justify-content:center;z-index:1000;padding:1rem;';
  m.innerHTML=`<div style="background:var(--s1);border:1px solid var(--br2);border-radius:20px;padding:2rem;max-width:380px;width:100%;box-shadow:0 40px 80px rgba(0,0,0,.6);">
    <h3 style="font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:.04em;margin-bottom:1.2rem;">Nueva conversación</h3>
    <div class="field"><label>Selecciona a quién escribirle</label>
      <select id="_csel">${users.map(u=>`<option value="${esc(u.username)}" data-name="${esc(u.name)}" data-role="${u.role||'exec'}">${esc(u.name)} (@${esc(u.username)})</option>`).join('')}</select>
    </div>
    <div style="display:flex;gap:8px;justify-content:flex-end;margin-top:1.3rem;">
      <button class="st-cancel" onclick="document.getElementById('_cmod').remove()">Cancelar</button>
      <button class="chat-send" style="padding:10px 22px;" onclick="(()=>{const s=document.getElementById('_csel');const o=s.options[s.selectedIndex];document.getElementById('_cmod').remove();selectChatContact(o.value,o.dataset.name,o.dataset.role)})()">Abrir chat</button>
    </div>
  </div>`;
  document.body.appendChild(m);
}

/* ── GROUP CHAT ── */
async function openGrpModal(){
  if(!isAdmin())return;
  if(USERS_CACHE.length===0){spin(true);const r=await api('getUsers');spin(false);if(r.ok)USERS_CACHE=r.data||[];}
  document.getElementById('grp-name-input').value='';
  const users=getAllChatUsers();
  document.getElementById('grp-member-list').innerHTML=users.length
    ?users.map(u=>`<div class="grp-member-item" data-u="${esc(u.username)}" onclick="this.classList.toggle('picked')"><div class="gmi-av">${ini(u.name)}</div><div class="gmi-name">${esc(u.name)} <span style="font-size:10px;color:var(--mu2)">@${esc(u.username)}</span></div></div>`).join('')
    :'<p style="color:var(--mu);font-size:13px">No hay usuarios para agregar.</p>';
  document.getElementById('grp-modal').classList.add('show');
  document.getElementById('grp-modal-cancel').onclick=()=>document.getElementById('grp-modal').classList.remove('show');
  document.getElementById('grp-modal-ok').onclick=createGroup;
}
async function createGroup(){
  const name=(document.getElementById('grp-name-input').value||'').trim();
  if(!name){alert('Escribe un nombre para el grupo.');return;}
  const picked=[...document.querySelectorAll('.grp-member-item.picked')].map(el=>el.dataset.u);
  if(!picked.length){alert('Selecciona al menos un miembro.');return;}
  const gid='grp_'+Date.now();
  const members=[CU.username,...picked];
  // Store group via API as a special message
  const groupMsg={
    type:'group_create',
    groupId:gid,
    groupName:name,
    members:members,
    from:CU.username,
    fromName:CU.name,
    to:'__groups__',
    toName:'grupos',
    text:'Grupo creado: '+name,
    timestamp:new Date().toISOString()
  };
  spin(true);
  const r=await api_sendMessage(groupMsg);
  spin(false);
  if(!r||r.ok===false){alert('Error al crear el grupo. Intenta de nuevo.');return;}
  CHAT_MESSAGES.push(groupMsg);
  document.getElementById('grp-modal').classList.remove('show');
  renderChatContacts();
  selectChatGroup(gid,name);
}

window.deleteGroup=async function(gid,gname){
  if(!confirm('¿Eliminar el grupo "'+gname+'"? Esto lo quitará para todos los miembros.'))return;
  const delMsg={
    type:'group_delete',
    groupId:gid,
    from:CU.username,
    fromName:CU.name,
    to:'__groups__',
    toName:'grupos',
    text:'Grupo eliminado',
    timestamp:new Date().toISOString()
  };
  spin(true);await api_sendMessage(delMsg);spin(false);
  CHAT_MESSAGES.push(delMsg);
  if(CHAT_ACTIVE&&CHAT_ACTIVE.groupId===gid)CHAT_ACTIVE=null;
  renderChatContacts();
  if(!CHAT_ACTIVE)document.getElementById('chat-msgs').innerHTML='<div class="chat-empty-state"><div class="ce-icon">💬</div><p>Selecciona una conversación</p></div>';
};

window.deleteConv=function(username){
  if(!confirm('¿Ocultar la conversación con este usuario? Los mensajes no se borran del servidor.'))return;
  hideConv('dm_'+username);
  if(CHAT_ACTIVE&&CHAT_ACTIVE.username===username){
    CHAT_ACTIVE=null;
    document.getElementById('chat-main-head').style.display='none';
    document.getElementById('chat-input-area').style.display='none';
    document.getElementById('chat-msgs').innerHTML='<div class="chat-empty-state"><div class="ce-icon">💬</div><p>Selecciona una conversación</p></div>';
  }
  renderChatContacts();
};

/* ── BENEFITS (PRO REDESIGN + MANUAL DATA) ── */
const CARDS=[
  {id:'joy',css:'c-joy',stripe:'#C8102E',seg:'Clásico',badge:'Sin anualidad · Sin CVV impreso',num:'•••• •••• •••• 1234',
   cat:'83.5% sin IVA',tasa:'62.75% anual',comision:'Sin comisión de por vida*',ingreso:'$15,000',ldc:'Desde $15,000',adicional:'—',pts:'No genera puntos Premia',
   benefits:[
     {i:'🚫',t:'Sin CVV impreso',d:'CVV digital que cambia en cada compra desde la App Banamex, para mayor seguridad en compras en línea.'},
     {i:'🛍️',t:'Descuentos todo el año',d:'Descuentos y promociones en negocios con participación Banamex.'},
     {i:'📅',t:'Elige tu fecha de corte',d:'Puedes cambiar tu fecha de corte una vez al año.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra tus boletos antes que nadie para eventos culturales, deportivos y espectáculos en México.'},
     {i:'🆘',t:'Mastercard Global Service',d:'Respaldo en caso de pérdida o robo de TDC: reposición en 48 hrs.'},
     {i:'⚠️',t:'Penalización por inactividad',d:'Realiza al menos $300 en compras al mes para no generar comisión de penalización por inactividad ($149 + IVA).'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio (máx. 3 meses)','18 años mínimo','Ingresos desde $15,000 MXN'],
   nota:'*Sin comisión de por vida con compra mínima de $300/mes para evitar penalización por inactividad.'},
  {id:'clasica',css:'c-clasica',stripe:'#2e4a8a',seg:'Clásico',badge:'5% Puntos Premia',num:'•••• •••• •••• 2345',
   cat:'88.7% sin IVA',tasa:'62.63% anual',comision:'$815 sin IVA',ingreso:'$15,000',ldc:'Desde $15,000',adicional:'$405 sin IVA',pts:'5% Puntos Premia en todas tus compras',
   benefits:[
     {i:'🎁',t:'1er año sin anualidad',d:'Realiza una compra sin monto mínimo antes de tu primer corte y la primera comisión por administración va por cuenta de Banamex. (Se bonifica posterior a 90 días)'},
     {i:'⭐',t:'5% Puntos Premia',d:'En todas tus compras. Úsalos para comprar lo que quieras o como efectivo en cajeros Citibanamex.'},
     {i:'⛽',t:'Puntos Dobles en gasolina',d:'El doble de puntos al cargar gasolina todos los días de la semana, topado a 1,000 puntos por semana.'},
     {i:'🏥',t:'3, 6 o 12 pagos fijos en Salud y Belleza',d:'En hospitales, laboratorios médicos, farmacias y clínicas de salud y belleza. Monto mínimo $3,000. Tel: 55 2226 3639.'},
     {i:'📅',t:'Elige tu fecha de corte',d:'Cambia tu fecha de pago una vez al año.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra tus boletos antes que nadie para los mejores eventos.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio (máx. 3 meses)','18 años mínimo','Ingresos desde $15,000 MXN'],
   nota:'Primer año sin anualidad con una compra antes del primer corte.'},
  {id:'teleton',css:'c-teleton',stripe:'#9333ea',seg:'Clásico',badge:'Causa social · 6 adicionales',num:'•••• •••• •••• 3456',
   cat:'87.0% sin IVA',tasa:'62.47% anual',comision:'$540 sin IVA',ingreso:'$15,000',ldc:'Desde $15,000',adicional:'Sin costo (6 adicionales)',pts:'No genera puntos Premia',
   benefits:[
     {i:'🎁',t:'1er año sin anualidad',d:'Realiza una compra sin monto mínimo antes de tu primer corte y la primera comisión va por cuenta Banamex. (Se bonifica posterior a 90 días)'},
     {i:'💰',t:'Anualidad más baja del mercado',d:'Solo $540 sin IVA a partir del segundo año.'},
     {i:'👨‍👩‍👧‍👦',t:'6 tarjetas adicionales sin costo',d:'Suma a toda tu familia sin costo adicional.'},
     {i:'❤️',t:'Apoya al Teletón',d:'Cada uso de tu tarjeta apoya los Centros de Rehabilitación Teletón.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra tus boletos antes que nadie para eventos culturales, deportivos y espectáculos en México.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio (máx. 3 meses)','18 años mínimo','Ingresos desde $15,000 MXN'],
   nota:'Primer año sin anualidad con una compra sin monto mínimo antes del primer corte.'},
  {id:'oro',css:'c-oro',stripe:'#C8A84B',seg:'Oro',badge:'7% Puntos Premia',num:'•••• •••• •••• 4567',
   cat:'85.7% sin IVA',tasa:'60.58% anual',comision:'$1,230 sin IVA',ingreso:'$25,000',ldc:'Desde $25,000',adicional:'$620 sin IVA',pts:'7% Puntos Premia en todas tus compras',
   benefits:[
     {i:'🎁',t:'1er año sin anualidad',d:'Realiza una compra sin monto mínimo antes de tu primer corte. (Comisión se bonifica posterior a 90 días)'},
     {i:'⭐',t:'7% Puntos Premia',d:'El mayor % en tarjetas básicas. Puntos dobles al consumir gasolina todos los días, topado a 1,000 puntos por semana.'},
     {i:'✈️',t:'3 MSI en viajes, salud y belleza',d:'3 meses sin intereses en viajes, hospitales, laboratorios, farmacias y clínicas.'},
     {i:'🛡️',t:'Seguro de Accidente en Viajes',d:'Hasta $400 USD de cobertura por incidente en caso de robo o daño accidental.'},
     {i:'🌍',t:'Master Seguro de Viajes',d:'Hasta $250,000 USD para cuidar tu integridad y la de tu familia en viajes.'},
     {i:'🔒',t:'Seguro por fraude',d:'Cubre hasta el saldo de la cuenta en caso de robo, extravío o facturación fraudulenta del plástico.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra tus boletos antes que nadie para los mejores eventos en México.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio (máx. 3 meses)','18 años mínimo','Ingresos desde $25,000 MXN'],
   nota:'Primer año sin anualidad con una compra antes del primer corte. Consulta términos y condiciones de Puntos Premia.'},
  {id:'descubre',css:'c-descubre',stripe:'#10b981',seg:'Oro',badge:'Puntos Momentos · 2x1 Vuelos',num:'•••• •••• •••• 5678',
   cat:'86.0% sin IVA',tasa:'60.65% anual',comision:'$1,230 sin IVA',ingreso:'$25,000',ldc:'Desde $25,000',adicional:'$620 sin IVA',pts:'1 Punto Momento por cada dólar gastado',
   benefits:[
     {i:'🎁',t:'1er año sin anualidad',d:'Realiza una compra sin monto mínimo antes de tu primer corte. (Se bonifica posterior a 90 días)'},
     {i:'🌟',t:'Puntos Momentos en todas tus compras',d:'1 Punto Momento Banamex por cada dólar gastado (o su equivalente en pesos).'},
     {i:'✈️',t:'2x1 en boletos de avión',d:'Viaja a playas nacionales: Acapulco, La Paz, Puerto Vallarta, Huatulco, Cozumel, Cancún, Los Cabos, Veracruz, Mazatlán, Zihuatanejo. Bienvenida: 600 pts en 3 meses. Aniversario: 4,500 pts.'},
     {i:'🎩',t:'Mastercard Concierge 24/7',d:'Atención personalizada en todo el mundo: reservas de restaurantes, coordinación de eventos especiales y más.'},
     {i:'🚗',t:'Elite Valet AICM',d:'50% de descuento en el Aeropuerto Internacional de la Ciudad de México. Hasta 5 días naturales, 2 entradas por mes.'},
     {i:'🍽️',t:'Dining Program',d:'20% de descuento en restaurantes seleccionados al reservar vía Mastercard Concierge. ¡Bebida de cortesía de bienvenida!'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Compra tus boletos antes que nadie para los mejores eventos.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio (máx. 3 meses)','18 años mínimo','Ingresos desde $25,000 MXN'],
   nota:'Primer año sin anualidad. El certificado 2x1 de bienvenida se obtiene acumulando 600 puntos en los primeros 3 meses.'},
  {id:'platinum',css:'c-platinum',stripe:'#6b7280',seg:'Platinum',badge:'Premium · 10% Puntos Premia',num:'•••• •••• •••• 6789',
   cat:'40.7% sin IVA',tasa:'32.02% anual',comision:'$2,725 sin IVA',ingreso:'$75,000',ldc:'Desde $50,000',adicional:'$1,360 sin IVA',pts:'10% Puntos Premia — el mayor % de la línea',
   benefits:[
     {i:'🎁',t:'1er año sin anualidad',d:'Realiza una compra sin monto mínimo antes de tu primer corte. (Se bonifica posterior a 90 días)'},
     {i:'💎',t:'10% Puntos Premia',d:'El mayor porcentaje de la línea Banamex en cada compra.'},
     {i:'🛡️',t:'LIBRA Premium Citibanamex',d:'Asistencia Vial, Legal y Gestoría, en el Hogar y Médica — incluida de por vida.'},
     {i:'🛫',t:'10 accesos salas BEYOND + 4 VIP mundiales',d:'10 accesos anuales a Salas Beyond para ti y 1 acompañante, más 4 accesos a Salas Mastercard Airport Experiences en más de 800 salas VIP alrededor del mundo.'},
     {i:'🎩',t:'Mastercard Concierge 24/7',d:'Atención personalizada en todo el mundo: restaurantes, eventos especiales y más.'},
     {i:'🍽️',t:'Dining Program',d:'20% de descuento en restaurantes seleccionados + bebida de cortesía por persona.'},
     {i:'🚗',t:'Elite Valet AICM',d:'50% de descuento en estacionamiento AICM. Hasta 5 días, 2 entradas por mes.'},
     {i:'📉',t:'CAT más bajo del segmento',d:'40.7% sin IVA — tasa preferencial para el segmento Platinum.'},
     {i:'🎟️',t:'Preventas exclusivas',d:'Para los mejores eventos culturales, deportivos y espectáculos.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio (máx. 3 meses)','18 años mínimo','Ingresos desde $75,000 MXN','Buen historial crediticio'],
   nota:'Primer año sin anualidad. Consulta términos y condiciones de Puntos Premia.'},
  {id:'explora',css:'c-explora',stripe:'#3b82f6',seg:'Platinum',badge:'Viajero Frecuente · 1.15 Puntos',num:'•••• •••• •••• 7890',
   cat:'81.2% sin IVA',tasa:'58.19% anual',comision:'$2,725 sin IVA',ingreso:'$75,000',ldc:'Desde $50,000',adicional:'$1,360 sin IVA',pts:'1.15 Puntos Momentos por cada dólar',
   benefits:[
     {i:'🎁',t:'1er año sin anualidad',d:'Realiza una compra sin monto mínimo antes de tu primer corte. (Se bonifica posterior a 90 días)'},
     {i:'🌟',t:'1.15 Puntos Momentos',d:'Por cada dólar gastado (o equivalente en pesos). ¡Tus tarjetas adicionales también generan puntos!'},
     {i:'✈️',t:'2x1 en boletos de avión',d:'Playas nacionales. Bienvenida: acumula 1,300 puntos en primeros 3 meses. Aniversario: 10,000 Puntos Explora acumulados.'},
     {i:'🛫',t:'10 accesos salas BEYOND + 4 VIP mundiales',d:'10 accesos anuales a Salas Beyond para ti y 1 acompañante, más 4 accesos a Salas Mastercard Airport Experiences (800+ salas VIP mundiales).'},
     {i:'🎩',t:'Mastercard Concierge 24/7',d:'Atención personalizada en todo el mundo: restaurantes, coordinación de viajes y eventos.'},
     {i:'🚗',t:'Elite Valet AICM',d:'50% de descuento en estacionamiento AICM. Hasta 5 días, 2 entradas por mes.'},
     {i:'🔒',t:'Seguros Mastercard',d:'Asistencias de viaje, equipaje, autos y toda la protección que necesitas.'},
   ],
   reqs:['INE/IFE o pasaporte vigente','Comprobante de domicilio (máx. 3 meses)','18 años mínimo','Ingresos desde $75,000 MXN','Buen historial crediticio'],
   nota:'Primer año sin anualidad. El certificado 2x1 de bienvenida requiere 1,300 pts en primeros 3 meses; el de aniversario, 10,000 Puntos Explora.'},
];
let _activeBen=CARDS[0].id;
function buildBen(){
  const sid=document.getElementById('ben-sidebar');
  if(!sid)return;
  sid.innerHTML=CARDS.map(c=>`
    <div class="ben-pill${_activeBen===c.id?' active':''}" onclick="selectBen('${c.id}')">
      <div class="ben-pill-stripe" style="background:${c.stripe}"></div>
      <div class="ben-pill-info">
        <div class="ben-pill-name">${c.id==='joy'?'Joy Banamex':c.id==='clasica'?'Clásica Banamex':c.id==='teleton'?'Teletón Banamex':c.id==='oro'?'Oro Banamex':c.id==='descubre'?'Descubre Banamex':c.id==='platinum'?'Platinum Banamex':'Explora Banamex'}</div>
        <div class="ben-pill-seg">${c.seg} · ${c.pts.split(' ')[0]} ${c.pts.split(' ')[1]||''}</div>
      </div>
    </div>`).join('');
  renderBenDetail(_activeBen);
}
window.selectBen=function(id){_activeBen=id;document.querySelectorAll('.ben-pill').forEach(p=>p.classList.toggle('active',p.onclick.toString().includes("'"+id+"'")));renderBenDetail(id);};
function renderBenDetail(id){
  const c=CARDS.find(x=>x.id===id);if(!c)return;
  const wrap=document.getElementById('ben-detail-wrap');
  const cardName=id==='joy'?'Joy Banamex':id==='clasica'?'Clásica Banamex':id==='teleton'?'Teletón Banamex':id==='oro'?'Oro Banamex':id==='descubre'?'Descubre Banamex':id==='platinum'?'Platinum Banamex':'Explora Banamex';
  wrap.innerHTML=`<div class="ben-detail">
    <div class="ben-card-visual ${c.css}">
      <div><div class="bcv-badge">${c.badge}</div></div>
      <div>
        <div class="bcv-chip"></div>
        <div class="bcv-num">${c.num}</div>
        <div class="bcv-name">${cardName}</div>
      </div>
      <div class="bcv-logo">BANAMEX</div>
      <div class="bcv-mc"><span class="r"></span><span class="y"></span></div>
    </div>
    <div class="ben-nums-grid">
      <div class="ben-num-box"><div class="bnn">CAT</div><div class="bnv red">${c.cat}</div></div>
      <div class="ben-num-box"><div class="bnn">Tasa anual</div><div class="bnv red">${c.tasa}</div></div>
      <div class="ben-num-box"><div class="bnn">Anualidad</div><div class="bnv gold">${c.comision}</div></div>
      <div class="ben-num-box"><div class="bnn">Ingreso mín.</div><div class="bnv green">${c.ingreso}</div></div>
      <div class="ben-num-box"><div class="bnn">LDC mín.</div><div class="bnv green">${c.ldc}</div></div>
      <div class="ben-num-box"><div class="bnn">Adicional</div><div class="bnv pri">${c.adicional}</div></div>
    </div>
    <div class="ben-section-hd">✨ Beneficios</div>
    <div class="ben-benefits-list">${c.benefits.map(b=>`
      <div class="ben-benefit-item">
        <div class="bbi-ico">${b.i}</div>
        <div class="bbi-body"><div class="bbi-title">${b.t}</div><div class="bbi-desc">${b.d}</div></div>
      </div>`).join('')}
    </div>
    <div class="ben-section-hd">📋 Requisitos</div>
    <div class="ben-reqs-grid">${c.reqs.map(r=>`<div class="ben-req"><span>✔</span><span>${r}</span></div>`).join('')}</div>
    <div class="ben-nota">ℹ️ ${c.nota}</div>
  </div>`;
}

/* ── CLICK EVENTS ── */
document.addEventListener('click',async function(e){
  if(e.target.id==='login-btn'){doLogin();return;}
  if(e.target.id==='logout-btn'){doLogout();return;}
  if(e.target.id==='reg-btn'){registrarVenta();return;}
  if(e.target.id==='refresh-btn'){await loadDash();return;}
  if(e.target.id==='add-user-btn'){addUser();return;}
  if(e.target.classList.contains('delbtn')&&e.target.dataset.folio){delSale(e.target.dataset.folio);return;}
  if(e.target.classList.contains('del-u')&&e.target.dataset.uname){
    if(!confirm('¿Eliminar al usuario @'+e.target.dataset.uname+'?'))return;
    spin(true);const r=await api('deleteUser',{username:e.target.dataset.uname});spin(false);
    if(!r.ok){alert('Error: '+r.error);return;}await loadUsers();return;
  }
  if(e.target.id==='export-btn'){exportarExcel();return;}
  if(e.target.id==='clear-btn'){
    if(!confirm('¿Borrar TODAS las ventas? Esta acción no se puede deshacer.'))return;
    spin(true);const r=await api('clearSales');spin(false);
    if(!r.ok){alert('Error: '+r.error);return;}
    SALES_CACHE=[];renderDashTable();setSyncS('ok','Sincronizado · 0 ventas');return;
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
    if(document.getElementById('pg-dash').classList.contains('on'))await loadDash();
    else await renderRecent();return;
  }
  if(e.target.id==='st-detail-close'){document.getElementById('st-detail-pop').classList.remove('show');return;}
  if(e.target.id==='share-cancel'){document.getElementById('share-modal').classList.remove('show');return;}
  if(e.target.id==='unshare-btn'){await doShareSale(true);return;}
  if(e.target.id==='share-save'){await doShareSale(false);return;}
});
document.addEventListener('keydown',function(e){
  if(e.key==='Enter'&&document.getElementById('login-screen').style.display!=='none')doLogin();
  if(e.key==='Escape'){
    ['st-modal','st-detail-pop','share-modal','chat-modal','grp-modal'].forEach(id=>document.getElementById(id)?.classList.remove('show'));
    document.getElementById('img-lightbox').style.display='none';
  }
});
document.addEventListener('input',function(e){if(e.target.id==='d-search'||e.target.id==='d-filt')renderDashTable();});
document.getElementById('login-screen').style.display='flex';
</script>
</body>
</html>
