[TitleOrderDashboard_FINAL (20).html](https://github.com/user-attachments/files/27288887/TitleOrderDashboard_FINAL.20.html)
# title-dashboard<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="Title Orders">
<meta name="mobile-web-app-capable" content="yes">
<meta name="theme-color" content="#1B4F8A">
<link rel="manifest" id="pwa-manifest">
<title>Title Search Order Management</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<style>
:root{
  --bg:#F5F4F0;--surface:#fff;--surface2:#EFEDE8;--border:rgba(0,0,0,.08);--border2:rgba(0,0,0,.14);
  --text:#1A1917;--text2:#6B6860;--text3:#9E9C96;
  --blue:#1B4F8A;--blue-l:#E8EFF8;--blue-t:#0C3464;
  --green:#2D6A35;--green-l:#E8F3EA;
  --amber:#7A4F0D;--amber-l:#FDF3E3;
  --red:#8B2020;--red-l:#FDEAEA;
  --purple:#5B21B6;--purple-l:#EDE9FE;
  --teal:#0E6655;--teal-l:#D1F0EA;
  --r:10px;--rl:14px;
}
/* ── AUTH ── */
#login-screen{display:flex;min-height:100vh;background:var(--bg);align-items:center;justify-content:center}
.login-box{background:var(--surface);border:1px solid var(--border2);border-radius:var(--rl);padding:36px 40px;width:400px;max-width:95vw;box-shadow:0 8px 40px rgba(0,0,0,.10)}
.login-logo{text-align:center;margin-bottom:28px}
.login-logo .b1{font-size:22px;font-weight:700;color:var(--blue);letter-spacing:-.5px}
.login-logo .b2{font-size:12px;color:var(--text3);margin-top:4px}
.login-logo .login-icon{width:56px;height:56px;background:var(--blue-l);border-radius:50%;display:flex;align-items:center;justify-content:center;margin:0 auto 12px}
.login-logo .login-icon svg{width:28px;height:28px;color:var(--blue)}
.login-field{margin-bottom:14px}
.login-field label{font-size:12px;font-weight:500;color:var(--text2);display:block;margin-bottom:5px}
.login-field input{width:100%;padding:10px 12px;border:1px solid var(--border2);border-radius:var(--r);font-size:13px;font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);outline:none;transition:border-color .15s,box-shadow .15s}
.login-field input:focus{border-color:var(--blue);box-shadow:0 0 0 3px rgba(27,79,138,.1);background:var(--surface)}
.login-btn{width:100%;padding:11px;background:var(--blue);color:#fff;border:none;border-radius:var(--r);font-size:14px;font-weight:600;font-family:'DM Sans',sans-serif;cursor:pointer;transition:background .15s;margin-top:6px}
.login-btn:hover{background:var(--blue-t)}
.login-btn:active{transform:scale(.98)}
.login-error{background:var(--red-l);color:var(--red);border-radius:var(--r);padding:9px 12px;font-size:12px;margin-bottom:12px;display:none}
.login-error.show{display:block}
.login-cred-row{display:flex;align-items:center;gap:8px;padding:7px 10px;border-radius:8px;cursor:pointer;border:1px solid var(--border);background:var(--bg);transition:all .12s}
.login-cred-row:hover{background:var(--blue-l);border-color:var(--blue)}
.login-cred-av{width:26px;height:26px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;flex-shrink:0}
.login-cred-email{flex:1;font-size:11px;color:var(--text2);font-family:'DM Mono',monospace;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.login-cred-role{font-size:9px;font-weight:600;padding:2px 7px;border-radius:999px;flex-shrink:0}
.login-cred-role.admin{background:#E8F3EA;color:#1A4021}
.login-cred-role.team{background:var(--blue-l);color:var(--blue-t)}
/* ── USER TOPBAR ── */
.user-topbar-info{display:flex;align-items:center;gap:8px;flex-shrink:0}
.user-avatar{width:30px;height:30px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:600;flex-shrink:0}
.user-name{font-size:12px;font-weight:500;color:var(--text2)}
.user-role{font-size:10px;padding:2px 7px;border-radius:999px;font-weight:600}
.role-admin{background:#E8F3EA;color:#1A4021}
.role-team{background:var(--blue-l);color:var(--blue-t)}
/* ── COMMUNICATION PANEL ── */
#comm-fab{position:fixed;bottom:24px;right:24px;z-index:900;display:flex;flex-direction:column;align-items:flex-end;gap:8px}
#comm-toggle{width:54px;height:54px;border-radius:50%;background:var(--blue);border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;box-shadow:0 4px 20px rgba(27,79,138,.4);transition:all .2s;position:relative}
#comm-toggle:hover{background:var(--blue-t);transform:scale(1.06)}
#comm-toggle svg{width:24px;height:24px;color:#fff}
#comm-badge{position:absolute;top:-2px;right:-2px;width:16px;height:16px;border-radius:50%;background:#DC2626;color:#fff;font-size:9px;font-weight:700;display:none;align-items:center;justify-content:center;border:2px solid var(--bg)}
#comm-badge.show{display:flex}
#comm-panel{background:var(--surface);border:1px solid var(--border2);border-radius:var(--rl);width:420px;height:580px;display:none;flex-direction:column;overflow:hidden;box-shadow:0 12px 48px rgba(0,0,0,.18)}
#comm-panel.open{display:flex}
/* Panel header */
.cp-head{background:var(--blue);color:#fff;padding:0;display:flex;flex-direction:column;flex-shrink:0}
.cp-head-top{padding:12px 16px;display:flex;align-items:center;justify-content:space-between}
.cp-head-top h4{font-size:13px;font-weight:600;display:flex;align-items:center;gap:7px}
.cp-head-btns{display:flex;gap:4px;align-items:center}
.cp-head-btn{background:rgba(255,255,255,.15);border:none;color:#fff;cursor:pointer;border-radius:7px;padding:5px 7px;transition:background .15s;display:flex;align-items:center;gap:4px;font-size:11px;font-weight:500}
.cp-head-btn:hover{background:rgba(255,255,255,.28)}
.cp-head-btn svg{width:13px;height:13px}
/* Contact tabs */
.cp-contacts{display:flex;overflow-x:auto;padding:0 12px 10px;gap:6px;scrollbar-width:none}
.cp-contacts::-webkit-scrollbar{display:none}
.cp-contact{display:flex;flex-direction:column;align-items:center;gap:4px;cursor:pointer;flex-shrink:0;padding:4px 6px;border-radius:8px;transition:background .15s;min-width:48px}
.cp-contact:hover{background:rgba(255,255,255,.15)}
.cp-contact.active{background:rgba(255,255,255,.22)}
.cp-contact-av{width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;border:2px solid transparent;position:relative;flex-shrink:0}
.cp-contact.active .cp-contact-av{border-color:#fff}
.cp-contact-av .online{position:absolute;bottom:0;right:0;width:9px;height:9px;border-radius:50%;background:#22C55E;border:2px solid var(--blue)}
.cp-contact-name{font-size:9px;color:rgba(255,255,255,.85);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:48px;text-align:center}
.cp-contact-unread{position:absolute;top:-3px;right:-3px;width:14px;height:14px;border-radius:50%;background:#EF4444;color:#fff;font-size:8px;font-weight:700;display:none;align-items:center;justify-content:center;border:1.5px solid var(--blue)}
.cp-contact-unread.show{display:flex}
/* Messages area */
.cp-msgs{flex:1;overflow-y:auto;padding:14px 14px 8px;display:flex;flex-direction:column;gap:10px;background:var(--bg)}
.cp-msgs::-webkit-scrollbar{width:4px}
.cp-msgs::-webkit-scrollbar-track{background:transparent}
.cp-msgs::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}
/* Message bubbles */
.cp-msg{display:flex;flex-direction:column;max-width:82%}
.cp-msg.me{align-self:flex-end;align-items:flex-end}
.cp-msg.them{align-self:flex-start;align-items:flex-start}
.cp-msg-meta{font-size:10px;color:var(--text3);margin-bottom:3px;display:flex;align-items:center;gap:5px}
.cp-bubble{padding:9px 12px;border-radius:14px;font-size:12px;line-height:1.5;word-break:break-word}
.cp-msg.me .cp-bubble{background:var(--blue);color:#fff;border-bottom-right-radius:4px}
.cp-msg.them .cp-bubble{background:var(--surface);color:var(--text);border-bottom-left-radius:4px;border:1px solid var(--border)}
.cp-msg-time{font-size:10px;color:var(--text3);margin-top:3px}
/* File attachment bubble */
.cp-file-bubble{display:flex;align-items:center;gap:9px;padding:10px 13px;border-radius:12px;cursor:pointer;max-width:240px;border:1px solid transparent;transition:opacity .15s}
.cp-file-bubble:hover{opacity:.85}
.cp-msg.me .cp-file-bubble{background:rgba(255,255,255,.15);border-color:rgba(255,255,255,.25)}
.cp-msg.them .cp-file-bubble{background:var(--surface2);border-color:var(--border)}
.cp-file-icon{width:34px;height:34px;border-radius:8px;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.cp-file-info{flex:1;min-width:0}
.cp-file-name{font-size:11px;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.cp-file-size{font-size:10px;opacity:.7;margin-top:1px}
/* File preview strip */
.cp-file-preview-strip{padding:8px 12px;background:var(--blue-l);border-top:1px solid var(--border);display:none;gap:8px;align-items:center;flex-wrap:wrap}
.cp-file-preview-strip.show{display:flex}
.cp-file-chip{display:flex;align-items:center;gap:5px;padding:4px 9px;background:var(--surface);border:1px solid var(--border2);border-radius:6px;font-size:11px;max-width:160px}
.cp-file-chip span{overflow:hidden;text-overflow:ellipsis;white-space:nowrap;flex:1}
.cp-file-chip button{background:none;border:none;cursor:pointer;color:var(--text3);font-size:13px;line-height:1;padding:0;flex-shrink:0}
/* Input row */
.cp-input-row{padding:10px 12px;border-top:1px solid var(--border);display:flex;gap:7px;align-items:flex-end;background:var(--surface);flex-shrink:0}
.cp-input-row textarea{flex:1;border:1px solid var(--border2);border-radius:10px;padding:8px 11px;font-size:12px;font-family:'DM Sans',sans-serif;resize:none;min-height:38px;max-height:90px;outline:none;background:var(--bg);line-height:1.4}
.cp-input-row textarea:focus{border-color:var(--blue);box-shadow:0 0 0 3px rgba(27,79,138,.08);background:var(--surface)}
.cp-icon-btn{background:none;border:1px solid var(--border2);border-radius:9px;padding:8px;cursor:pointer;color:var(--text2);display:flex;align-items:center;justify-content:center;transition:all .15s;flex-shrink:0}
.cp-icon-btn:hover{background:var(--surface2);border-color:var(--blue);color:var(--blue)}
.cp-icon-btn svg{width:15px;height:15px}
.cp-send-btn{background:var(--blue);color:#fff;border:none;border-radius:9px;padding:9px 14px;cursor:pointer;font-size:12px;font-weight:600;white-space:nowrap;transition:background .15s;flex-shrink:0}
.cp-send-btn:hover{background:var(--blue-t)}
/* Call overlay */
#call-overlay{position:fixed;top:0;left:0;width:100vw;height:100vh;background:rgba(10,20,40,.88);z-index:980;display:none;align-items:center;justify-content:center}
#call-overlay.show{display:flex}
.call-box{background:var(--surface);border-radius:20px;padding:36px 40px;min-width:300px;text-align:center;box-shadow:0 24px 64px rgba(0,0,0,.4)}
.call-avatar{width:72px;height:72px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:24px;font-weight:700;margin:0 auto 14px}
.call-name{font-size:18px;font-weight:600;margin-bottom:5px}
.call-status{font-size:13px;color:var(--text3);margin-bottom:28px}
.call-actions{display:flex;gap:14px;justify-content:center}
.call-btn{width:56px;height:56px;border-radius:50%;border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .2s}
.call-btn:hover{transform:scale(1.08)}
.call-btn svg{width:22px;height:22px}
.call-btn-end{background:#DC2626;color:#fff}
.call-btn-mute{background:var(--surface2);color:var(--text)}
.call-btn-mute.muted{background:var(--amber-l);color:var(--amber)}
.call-btn-accept{background:#16A34A;color:#fff}
.call-timer{font-size:13px;color:var(--text3);margin-top:12px;font-family:'DM Mono',monospace}
/* Incoming call animation */
@keyframes ring{0%,100%{transform:scale(1)}50%{transform:scale(1.06)}}
.ringing .call-avatar{animation:ring .8s ease-in-out infinite}
/* Day dividers */
.day-divider{text-align:center;font-size:10px;color:var(--text3);display:flex;align-items:center;gap:8px;margin:4px 0}
.day-divider::before,.day-divider::after{content:'';flex:1;height:.5px;background:var(--border)}
/* Empty state */
.cp-empty{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:8px;color:var(--text3);font-size:12px;background:var(--bg)}
.cp-empty svg{width:36px;height:36px;opacity:.35}
/* ── MEETING ── (kept minimal, no longer used) */
#meeting-panel{display:none}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);font-size:13px;line-height:1.5;min-height:100vh}
.app{display:flex;min-height:100vh}
/* SIDEBAR */
.sb{width:230px;min-width:230px;background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;position:sticky;top:0;height:100vh;overflow-y:auto}
.sb-logo{padding:18px 20px 14px;border-bottom:1px solid var(--border)}
.sb-logo .b1{font-size:14px;font-weight:700;color:var(--blue);letter-spacing:-.3px}
.sb-logo .b2{font-size:11px;color:var(--text3);margin-top:2px}
.sb-nav{padding:10px 10px;flex:1}
.nl{font-size:10px;font-weight:600;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;padding:8px 10px 4px}
.ni{display:flex;align-items:center;gap:9px;padding:8px 10px;border-radius:8px;cursor:pointer;color:var(--text2);font-size:13px;transition:all .15s;margin-bottom:2px}
.ni:hover{background:var(--surface2);color:var(--text)}
.ni.active{background:var(--blue-l);color:var(--blue-t);font-weight:500}
.ni svg{width:15px;height:15px;flex-shrink:0}
.sb-foot{padding:12px 16px;border-top:1px solid var(--border)}
.email-chip{display:flex;align-items:center;gap:7px;padding:6px 8px;border-radius:7px;margin-bottom:4px;background:var(--surface2)}
.email-chip svg{width:13px;height:13px;flex-shrink:0;color:var(--blue)}
.email-chip span{font-size:11px;color:var(--text2);font-family:'DM Mono',monospace;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
/* MAIN */
.main{flex:1;overflow-x:hidden;min-width:0}
.topbar{background:var(--surface);border-bottom:1px solid var(--border);padding:12px 24px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:50;gap:12px}
.tb-title{font-size:15px;font-weight:600}
.tb-sub{font-size:11px;color:var(--text3);margin-top:1px}
.tb-actions{display:flex;gap:7px;align-items:center;flex-shrink:0}
.content{padding:22px 24px}
.page{display:none}.page.active{display:block}
/* METRICS */
.metrics{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:10px;margin-bottom:20px}
.mc{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);padding:14px 16px}
.ml{font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.06em;font-weight:500;margin-bottom:6px}
.mv{font-size:24px;font-weight:600;font-family:'DM Mono',monospace;line-height:1}
.ms{font-size:11px;color:var(--text3);margin-top:3px}
/* BUTTONS */
.btn{display:inline-flex;align-items:center;gap:5px;padding:6px 13px;border-radius:8px;font-size:12px;font-weight:500;border:1px solid var(--border2);background:var(--surface);color:var(--text);cursor:pointer;transition:all .15s;font-family:'DM Sans',sans-serif;white-space:nowrap}
.btn:hover{background:var(--surface2)}.btn:active{transform:scale(.98)}
.btn svg{width:13px;height:13px;flex-shrink:0}
.btn-p{background:var(--blue);color:#fff;border-color:var(--blue)}.btn-p:hover{background:var(--blue-t)}
.btn-g{background:var(--green);color:#fff;border-color:var(--green)}.btn-g:hover{background:#225229}
.btn-a{background:#B45309;color:#fff;border-color:#B45309}.btn-a:hover{background:#92400E}
.btn-pu{background:var(--purple);color:#fff;border-color:var(--purple)}.btn-pu:hover{background:#4C1D95}
.btn-r{background:transparent;color:var(--red);border-color:rgba(139,32,32,.25)}.btn-r:hover{background:var(--red-l)}
.btn-sm{padding:4px 9px;font-size:11px}
/* CONTROLS */
.cbar{display:flex;gap:7px;flex-wrap:wrap;align-items:center;margin-bottom:14px;background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:9px 13px}
.sw{position:relative;flex:1;min-width:180px}
.sw svg{position:absolute;left:9px;top:50%;transform:translateY(-50%);width:13px;height:13px;color:var(--text3);pointer-events:none}
.sw input{padding-left:28px!important;width:100%}
input,select,textarea{font-family:'DM Sans',sans-serif;font-size:12px;color:var(--text);background:var(--bg);border:1px solid var(--border2);border-radius:8px;padding:6px 10px;outline:none;transition:border-color .15s,box-shadow .15s}
input:focus,select:focus,textarea:focus{border-color:var(--blue);box-shadow:0 0 0 3px rgba(27,79,138,.1);background:var(--surface)}
textarea{resize:vertical;line-height:1.5}
/* TABLE */
.tcard{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);overflow:hidden}
.tscroll{overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:11.5px}
thead{background:var(--bg)}
th{padding:9px 10px;text-align:left;font-size:10px;font-weight:600;color:var(--text3);text-transform:uppercase;letter-spacing:.07em;border-bottom:1px solid var(--border);white-space:nowrap}
td{padding:9px 10px;border-bottom:1px solid var(--border);color:var(--text);vertical-align:middle;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
td.actions-cell{overflow:visible;white-space:normal}
tr:last-child td{border-bottom:none}
tbody tr:hover td{background:var(--bg)}
.mono{font-family:'DM Mono',monospace;font-size:11px}
/* BADGES */
.badge{display:inline-flex;align-items:center;gap:4px;padding:2px 8px;border-radius:999px;font-size:10px;font-weight:600;white-space:nowrap}
.badge::before{content:'';width:5px;height:5px;border-radius:50%;flex-shrink:0}
.b-new{background:var(--blue-l);color:var(--blue-t)}.b-new::before{background:var(--blue)}
.b-prog{background:var(--amber-l);color:var(--amber)}.b-prog::before{background:var(--amber)}
.b-done{background:var(--green-l);color:var(--green)}.b-done::before{background:var(--green)}
.b-over{background:#FEE2E2;color:#991B1B}.b-over::before{background:#DC2626}
.b-pend{background:#F0EEE9;color:var(--text2)}.b-pend::before{background:var(--text3)}
.b-sent{background:var(--purple-l);color:var(--purple)}.b-sent::before{background:var(--purple)}
.b-portal{background:var(--teal-l);color:var(--teal)}.b-portal::before{background:var(--teal)}
.b-submit{background:#E0F2FE;color:#0369A1}.b-submit::before{background:#0284C7}
.b-cancel{background:#FEE2E2;color:#7F1D1D}.b-cancel::before{background:#B91C1C}
.b-taxpend{background:#FEF9C3;color:#854D0E}.b-taxpend::before{background:#CA8A04}
.b-taxcall{background:#FFF7ED;color:#9A3412}.b-taxcall::before{background:#EA580C}
.b-typepend{background:#F3E8FF;color:#6B21A8}.b-typepend::before{background:#9333EA}
.b-abstract{background:#E0F7FA;color:#006064}.b-abstract::before{background:#00838F}
.b-quality{background:#E8EAF6;color:#283593}.b-quality::before{background:#3949AB}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.7}}
.avatar{display:inline-flex;align-items:center;justify-content:center;width:24px;height:24px;border-radius:50%;font-size:10px;font-weight:600}
.row-actions{display:flex;gap:3px}
/* FORM */
.fpanel{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);padding:22px;margin-bottom:18px}
.fpanel h3{font-size:14px;font-weight:600;margin-bottom:4px}
.pdesc{font-size:12px;color:var(--text3);margin-bottom:16px}
.sec{font-size:10px;font-weight:600;color:var(--text3);text-transform:uppercase;letter-spacing:.07em;border-bottom:1px solid var(--border);padding-bottom:5px;margin:18px 0 10px}
.fg{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.fg .full{grid-column:1/-1}
.ff{display:flex;flex-direction:column;gap:4px}
.ff label{font-size:11px;font-weight:500;color:var(--text2)}
.ff input,.ff select,.ff textarea{width:100%}
.factions{display:flex;gap:7px;margin-top:18px;flex-wrap:wrap;align-items:center}
.txtprev{background:#1A1917;color:#A8E6A3;font-family:'DM Mono',monospace;font-size:10.5px;padding:12px 14px;border-radius:var(--r);white-space:pre;overflow-x:auto;max-height:180px;overflow-y:auto;line-height:1.6;margin-top:10px}
/* IMPORT TABS */
.itabs{display:flex;border:1px solid var(--border);border-radius:var(--r);overflow:hidden;background:var(--bg);margin-bottom:18px}
.itab{flex:1;padding:9px 12px;text-align:center;cursor:pointer;font-size:12px;font-weight:500;color:var(--text2);border-right:1px solid var(--border);transition:all .15s}
.itab:last-child{border-right:none}
.itab:hover{background:var(--surface2);color:var(--text)}
.itab.active{background:var(--surface);color:var(--blue-t);font-weight:600}
.itab svg{display:block;margin:0 auto 3px;width:16px;height:16px}
.ipanel{display:none}.ipanel.active{display:block}
.pzone{border:2px dashed var(--border2);border-radius:var(--rl);padding:18px;background:var(--bg);margin-bottom:14px}
.pzone textarea{width:100%;min-height:130px;background:var(--surface)}
.pst{display:inline-flex;align-items:center;gap:6px;padding:5px 11px;border-radius:8px;font-size:12px;font-weight:500}
.s-ok{background:var(--green-l);color:var(--green)}.s-err{background:var(--red-l);color:var(--red)}.s-info{background:var(--blue-l);color:var(--blue-t)}
.dzone{border:2px dashed var(--border2);border-radius:var(--rl);padding:36px 20px;text-align:center;background:var(--bg);cursor:pointer;transition:all .2s;margin-bottom:14px}
.dzone:hover,.dzone.dragover{border-color:var(--blue);background:var(--blue-l)}
.dzone input[type=file]{display:none}
.col-map{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.cmr{display:flex;align-items:center;gap:7px}
.cmr label{min-width:120px;font-size:11px;font-weight:500;color:var(--text2)}
.cmr select{flex:1;font-size:11px}
/* TEAM */
.tcards{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px;margin-bottom:20px}
.tc{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);padding:16px;cursor:pointer;transition:all .15s}
.tc:hover{box-shadow:0 2px 8px rgba(0,0,0,.08);border-color:var(--border2)}
.tc.sel{border:2px solid var(--blue);background:var(--blue-l)}
.tc .avl{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:600;margin-bottom:8px}
.tc .tcn{font-size:13px;font-weight:600;margin-bottom:2px}
.tc .tcc{font-size:26px;font-weight:600;font-family:'DM Mono',monospace;color:var(--blue);line-height:1.1}
.tc .tcs{font-size:11px;color:var(--text3);margin-top:2px}
.ovchip{display:inline-block;background:var(--red-l);color:var(--red);font-size:10px;font-weight:600;padding:1px 6px;border-radius:999px}
/* TYPING PACKAGE */
.pkg-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(320px,1fr));gap:14px;margin-bottom:20px}
.pkg-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);overflow:hidden}
.pkg-card-head{padding:14px 16px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;gap:8px}
.pkg-card-head h4{font-size:13px;font-weight:600;color:var(--text)}
.pkg-card-body{padding:14px 16px}
.pkg-progress{height:5px;background:var(--surface2);border-radius:999px;overflow:hidden;margin-bottom:12px}
.pkg-progress-fill{height:100%;background:var(--green);border-radius:999px;transition:width .3s}
.doc-row{display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid var(--border)}
.doc-row:last-child{border-bottom:none}
.doc-num{width:22px;height:22px;border-radius:50%;background:var(--blue-l);color:var(--blue-t);font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.doc-info{flex:1;min-width:0}
.doc-name{font-size:12px;font-weight:500;color:var(--text)}
.doc-sub{font-size:11px;color:var(--text3);margin-top:1px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.doc-check{width:18px;height:18px;border-radius:4px;border:1.5px solid var(--border2);background:var(--bg);display:flex;align-items:center;justify-content:center;cursor:pointer;flex-shrink:0;transition:all .15s}
.doc-check.checked{background:var(--green);border-color:var(--green)}
.doc-check svg{width:11px;height:11px;color:#fff;display:none}
.doc-check.checked svg{display:block}
.doc-upload{font-size:10px;padding:3px 8px;border-radius:6px;border:1px solid var(--border2);background:transparent;color:var(--text2);cursor:pointer;white-space:nowrap;font-family:'DM Sans',sans-serif}
.doc-upload:hover{background:var(--surface2)}
.doc-upload.has-file{background:var(--green-l);color:var(--green);border-color:var(--green)}
.pkg-actions{display:flex;gap:7px;flex-wrap:wrap;padding:12px 16px;border-top:1px solid var(--border);background:var(--bg)}
.pkg-modal-doc{display:flex;align-items:flex-start;gap:12px;padding:10px 0;border-bottom:1px solid var(--border)}
.pkg-modal-doc:last-child{border-bottom:none}
.pkg-modal-num{width:26px;height:26px;border-radius:50%;background:var(--blue-l);color:var(--blue-t);font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:2px}
.pkg-modal-info{flex:1}
.pkg-modal-name{font-size:13px;font-weight:600;margin-bottom:4px}
.pkg-modal-files{font-size:11px;color:var(--text3);margin-top:4px}
.pkg-modal-upload{display:flex;gap:6px;flex-wrap:wrap;margin-top:8px;align-items:center}
.b-ready{background:#DCFCE7;color:#14532D}.b-ready::before{background:#16A34A}
/* ── UPLOAD SYSTEM ── */
.upload-tabs{display:flex;gap:0;border-bottom:1px solid var(--border);margin-bottom:16px}
.upload-tab{padding:8px 18px;font-size:12px;font-weight:500;color:var(--text2);cursor:pointer;border-bottom:2px solid transparent;margin-bottom:-1px;transition:all .15s}
.upload-tab:hover{color:var(--text)}
.upload-tab.active{color:var(--blue-t);border-bottom-color:var(--blue);font-weight:600}
.upload-panel{display:none}.upload-panel.active{display:block}
.order-upload-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);margin-bottom:12px;overflow:hidden}
.ouc-head{padding:12px 16px;display:flex;align-items:center;justify-content:space-between;gap:8px;background:var(--bg);border-bottom:1px solid var(--border);cursor:pointer}
.ouc-head:hover{background:var(--surface2)}
.ouc-info{flex:1;min-width:0}
.ouc-title{font-size:13px;font-weight:600;color:var(--text)}
.ouc-sub{font-size:11px;color:var(--text3);margin-top:1px}
.ouc-body{padding:14px 16px;display:none}
.ouc-body.open{display:block}
.upload-section{margin-bottom:14px}
.upload-section-title{font-size:11px;font-weight:600;color:var(--text2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:8px;display:flex;align-items:center;gap:6px}
.upload-section-num{width:20px;height:20px;border-radius:50%;background:var(--blue-l);color:var(--blue-t);font-size:10px;font-weight:700;display:inline-flex;align-items:center;justify-content:center;flex-shrink:0}
.file-drop{border:2px dashed var(--border2);border-radius:var(--r);padding:14px;text-align:center;cursor:pointer;transition:all .15s;background:var(--bg)}
.file-drop:hover,.file-drop.dragover{border-color:var(--blue);background:var(--blue-l)}
.file-drop input[type=file]{display:none}
.file-drop p{font-size:12px;color:var(--text2);margin-top:4px}
.file-drop svg{width:24px;height:24px;color:var(--text3);margin:0 auto;display:block}
.uploaded-files{margin-top:8px;display:flex;flex-direction:column;gap:5px}
.uploaded-file{display:flex;align-items:center;gap:8px;padding:6px 10px;background:var(--surface);border:1px solid var(--border);border-radius:var(--r);font-size:12px}
.uploaded-file svg{width:14px;height:14px;flex-shrink:0}
.uploaded-file .fname{flex:1;font-weight:500;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.uploaded-file .fsize{font-size:10px;color:var(--text3);white-space:nowrap}
.uploaded-file .fdel{cursor:pointer;color:var(--red);padding:2px 5px;border-radius:4px;flex-shrink:0}
.uploaded-file .fdel:hover{background:var(--red-l)}
.file-pdf{color:#DC2626}.file-img{color:#16A34A}.file-doc{color:#1D4ED8}.file-other{color:var(--text3)}
.upload-progress-bar{height:4px;background:var(--surface2);border-radius:999px;overflow:hidden;margin-top:6px}
.upload-progress-fill{height:100%;background:var(--blue);border-radius:999px;transition:width .3s}
.team-badge{display:inline-flex;align-items:center;gap:5px;padding:2px 8px;border-radius:999px;font-size:10px;font-weight:600}
.upload-summary{display:grid;grid-template-columns:repeat(auto-fit,minmax(110px,1fr));gap:8px;margin-bottom:16px}
.us-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:10px 14px;text-align:center}
.us-val{font-size:20px;font-weight:600;font-family:'DM Mono',monospace}
.us-lbl{font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.05em;margin-top:2px}
.tr-section{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:14px 16px;margin-bottom:12px}
.tr-sec-title{font-size:11px;font-weight:700;color:var(--blue-t);text-transform:uppercase;letter-spacing:.07em;margin-bottom:10px;padding-bottom:6px;border-bottom:1px solid var(--border)}
.tr-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.tr-grid .full{grid-column:1/-1}
.chain-entry{background:var(--bg);border-radius:var(--r);padding:12px;border:1px solid var(--border)}
.empty{text-align:center;padding:40px 20px;color:var(--text3)}
.empty svg{width:36px;height:36px;margin:0 auto 10px;display:block;opacity:.4}
.spinner{width:14px;height:14px;border:2px solid var(--blue-l);border-top-color:var(--blue);border-radius:50%;animation:spin .6s linear infinite;display:inline-block}
@keyframes spin{to{transform:rotate(360deg)}}
.hbox{background:var(--blue-l);border:1px solid rgba(27,79,138,.15);border-radius:var(--r);padding:11px 14px;margin-bottom:14px;font-size:12px;color:var(--blue-t)}
.srow{display:flex;gap:8px;align-items:flex-start;margin-bottom:6px}
.snum{min-width:20px;height:20px;border-radius:50%;background:var(--blue);color:#fff;font-size:10px;font-weight:600;display:flex;align-items:center;justify-content:center}
#notif{position:fixed;bottom:22px;right:22px;background:#1A1917;color:#fff;padding:11px 16px;border-radius:10px;font-size:12px;font-weight:500;opacity:0;transform:translateY(6px);transition:all .25s;z-index:999;pointer-events:none}
#notif.show{opacity:1;transform:translateY(0)}
.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.4);z-index:200;align-items:flex-start;justify-content:center;padding-top:32px;overflow-y:auto}
.overlay.open{display:flex}
.mbox{background:var(--surface);border-radius:var(--rl);border:1px solid var(--border2);padding:22px;width:660px;max-width:96vw;margin-bottom:32px;box-shadow:0 20px 60px rgba(0,0,0,.18)}
.mbox h3{font-size:14px;font-weight:600;margin-bottom:14px}
.mactions{display:flex;justify-content:flex-end;gap:7px;margin-top:18px}
.send-card{background:var(--bg);border:1px solid var(--border);border-radius:var(--r);padding:14px 16px;margin-bottom:10px}
.send-card h4{font-size:12px;font-weight:600;margin-bottom:8px}
.portal-btn{display:flex;align-items:center;gap:10px;background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:11px 14px;margin-bottom:7px;cursor:pointer;text-decoration:none;color:var(--text);transition:all .15s;font-size:13px;font-weight:500}
.portal-btn:hover{border-color:var(--blue);background:var(--blue-l);color:var(--blue-t)}
.portal-btn svg{width:16px;height:16px;flex-shrink:0;color:var(--blue)}
::-webkit-scrollbar{width:5px;height:5px}::-webkit-scrollbar-track{background:transparent}::-webkit-scrollbar-thumb{background:var(--border2);border-radius:3px}
[data-tip]{position:relative}
[data-tip]:hover::after{content:attr(data-tip);position:absolute;bottom:calc(100% + 5px);left:50%;transform:translateX(-50%);background:#1A1917;color:#fff;font-size:10px;white-space:nowrap;padding:3px 7px;border-radius:5px;z-index:100;pointer-events:none}
/* ══════════════════════════════════════════
   MOBILE & PWA STYLES
   ══════════════════════════════════════════ */
@media (max-width: 768px) {

  /* ── Layout ── */
  body { font-size:14px; -webkit-tap-highlight-color:transparent; }
  .app { flex-direction:column; min-height:100vh; min-height:-webkit-fill-available; }

  /* ── Sidebar → hidden on mobile, replaced by bottom nav ── */
  .sb { display:none !important; }

  /* ── Topbar mobile ── */
  .topbar { padding:10px 14px; position:sticky; top:0; z-index:200; }
  .topbar .tb-left { gap:8px; }
  .topbar .tb-left h1 { font-size:14px; }
  #topbar-date { display:none; }
  #topbar-name { font-size:12px; max-width:80px; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }

  /* ── Main content ── */
  .main { padding-bottom:70px; width:100%; }
  .content { padding:14px 12px; }
  .page { padding:0; }

  /* ── Page header ── */
  .ph { padding:12px 14px 10px; }
  .ph h2 { font-size:16px; }
  .ph p  { font-size:11px; }

  /* ── Dashboard table → card list on mobile ── */
  .tbl-wrap { overflow-x:auto; -webkit-overflow-scrolling:touch; }
  table { min-width:600px; font-size:12px; }
  th, td { padding:8px 10px; }

  /* ── Metric cards ── */
  #metrics-row { grid-template-columns:repeat(2,1fr) !important; gap:8px; padding:10px 12px; }
  .mc { padding:10px 12px; }
  .mv { font-size:22px; }

  /* ── Filter bar ── */
  .cbar { flex-wrap:wrap; gap:7px; padding:10px 12px; }
  .cbar select, .cbar input { font-size:13px; }
  .sw input { font-size:13px; }

  /* ── Buttons ── */
  .btn { font-size:12px; padding:7px 12px; }
  .btn-sm { font-size:11px; padding:4px 9px; }

  /* ── Cards ── */
  .card { padding:12px 14px; }
  .fpanel { padding:14px; }

  /* ── Form fields ── */
  .fg { grid-template-columns:1fr !important; gap:10px; }
  .ff.full { grid-column:1; }
  input, select, textarea { font-size:16px !important; /* prevents zoom on iOS */ }

  /* ── Modals ── */
  .modal { padding:14px; border-radius:var(--rl) var(--rl) 0 0; width:100%; max-width:100%; position:fixed; bottom:0; top:auto; max-height:90vh; overflow-y:auto; }
  .modal-overlay { align-items:flex-end; }

  /* ── Upload cards ── */
  .ouc-body.open > div { grid-template-columns:1fr !important; }

  /* ── Chat panel ── */
  #comm-panel { width:100vw !important; height:100vh !important; position:fixed; top:0; left:0; border-radius:0; z-index:500; }
  #comm-fab { bottom:80px; right:14px; }

  /* ── Call overlay ── */
  .call-box { padding:28px 24px; width:90vw; }

  /* ── Login screen ── */
  .login-box { width:calc(100vw - 32px); max-width:420px; padding:24px 20px; }

  /* ── Typing report modal ── */
  #tr-modal .modal { padding:12px; }
  .tr-grid { grid-template-columns:1fr !important; }

  /* ── Section cards ── */
  .upload-section { margin-bottom:10px; }
  .upload-summary { grid-template-columns:repeat(3,1fr) !important; }

  /* ── Order upload card ── */
  .ouc-head { flex-wrap:wrap; gap:6px; }
  .ouc-head > div:last-child { width:100%; justify-content:flex-start; }
}

/* ── BOTTOM NAVIGATION BAR ── */
#mobile-nav {
  display:none;
  position:fixed;
  bottom:0; left:0; right:0;
  height:62px;
  background:var(--surface);
  border-top:1px solid var(--border);
  z-index:300;
  padding:0 4px;
  padding-bottom:env(safe-area-inset-bottom);
}
#mobile-nav.show { display:flex; align-items:center; justify-content:space-around; }
.mnav-item {
  display:flex; flex-direction:column; align-items:center; gap:3px;
  padding:6px 8px; border-radius:10px; cursor:pointer;
  color:var(--text3); font-size:9px; font-weight:500;
  letter-spacing:.02em; text-transform:uppercase; flex:1;
  transition:all .15s; position:relative; min-width:0;
}
.mnav-item:hover, .mnav-item.active { color:var(--blue); background:var(--blue-l); }
.mnav-item svg { width:22px; height:22px; flex-shrink:0; }
.mnav-item span { white-space:nowrap; overflow:hidden; text-overflow:ellipsis; max-width:52px; }
.mnav-badge {
  position:absolute; top:4px; right:8px;
  width:16px; height:16px; border-radius:50%;
  background:#DC2626; color:#fff;
  font-size:9px; font-weight:700;
  display:none; align-items:center; justify-content:center;
  border:2px solid var(--surface);
}
.mnav-badge.show { display:flex; }

/* ── PWA INSTALL BANNER ── */
#pwa-banner {
  display:none;
  position:fixed; bottom:70px; left:12px; right:12px;
  background:var(--blue); color:#fff;
  border-radius:var(--r); padding:12px 14px;
  z-index:400; align-items:center; gap:10px;
  box-shadow:0 4px 20px rgba(0,0,0,.2);
  font-size:12px;
}
#pwa-banner.show { display:flex; }
#pwa-banner p { flex:1; line-height:1.4; }
#pwa-banner strong { display:block; font-size:13px; margin-bottom:2px; }
.pwa-close { background:rgba(255,255,255,.2); border:none; color:#fff; border-radius:6px; padding:4px 10px; font-size:11px; cursor:pointer; white-space:nowrap; }

/* ── MOBILE PAGE TITLE ── */
.mobile-ph {
  display:none;
  padding:10px 14px 6px;
  font-size:15px; font-weight:600; color:var(--text);
}
@media(max-width:768px){ .mobile-ph { display:block; } }

</head>
<body>
<div id="notif"></div>
<!-- ── LOGIN SCREEN ── -->
<div id="login-screen">
  <div class="login-box">
    <div class="login-logo">
      <div class="login-icon">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
      </div>
      <div class="b1">Title Order Management</div>
      <div class="b2">YDeal Title Services &amp; Title Priority</div>
    </div>
    <div class="login-error" id="login-error"></div>
    <div class="login-field">
      <label>Email address</label>
      <input type="email" id="login-email" placeholder="e.g. hb@ydealtitleservices.com" autocomplete="email">
    </div>
    <div class="login-field">
      <label>Password</label>
      <div style="position:relative">
        <input type="password" id="login-pass" placeholder="Enter your password" autocomplete="current-password" style="width:100%;padding-right:40px">
        <button onclick="togglePassVis()" id="pass-eye" type="button"
          style="position:absolute;right:10px;top:50%;transform:translateY(-50%);background:none;border:none;cursor:pointer;color:var(--text3);padding:2px;display:flex;align-items:center">
          <svg id="eye-icon" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:16px;height:16px"><path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/></svg>
        </button>
      </div>
    </div>
    <button class="login-btn" onclick="doLogin()">
      <span id="login-btn-text">Sign In</span>
    </button>
    <div style="text-align:center;margin-top:16px;font-size:11px;color:var(--text3)">
      Secure access &nbsp;·&nbsp; YDeal Title Services &amp; Title Priority
    </div>
  </div>
</div>

<!-- ── MOBILE BOTTOM NAVIGATION ── -->
<nav id="mobile-nav">
  <div class="mnav-item active" id="mnav-dashboard" onclick="mobileGo('dashboard')">
    <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>
    <span>Orders</span>
  </div>
  <div class="mnav-item" id="mnav-uploads" onclick="mobileGo('uploads')">
    <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
    <span>Uploads</span>
  </div>
  <div class="mnav-item" id="mnav-typing" onclick="mobileGo('typing')">
    <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/></svg>
    <span>Typing</span>
  </div>
  <div class="mnav-item" id="mnav-chat" onclick="toggleComm()">
    <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>
    <span>Chat</span>
    <span class="mnav-badge" id="mnav-chat-badge"></span>
  </div>
  <div class="mnav-item" id="mnav-more" onclick="toggleMobileMenu()">
    <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="12" cy="5" r="1"/><circle cx="12" cy="12" r="1"/><circle cx="12" cy="19" r="1"/></svg>
    <span>More</span>
  </div>
</nav>

<!-- ── MOBILE MORE MENU ── -->
<div id="mobile-more-menu" style="display:none;position:fixed;bottom:70px;left:0;right:0;background:var(--surface);border-top:1px solid var(--border);border-radius:var(--rl) var(--rl) 0 0;z-index:350;padding:16px 12px;box-shadow:0 -4px 20px rgba(0,0,0,.1)">
  <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:12px">
    <div class="mnav-more-btn" onclick="mobileGo('team');toggleMobileMenu()" id="mmb-team" style="display:none">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="9" cy="7" r="3"/><path d="M3 20c0-4 2.7-7 6-7h0c3.3 0 6 3 6 7"/></svg>
      <span>Team</span>
    </div>
    <div class="mnav-more-btn" onclick="mobileGo('qualia');toggleMobileMenu()" id="mmb-qualia" style="display:none">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/></svg>
      <span>Qualia</span>
    </div>
    <div class="mnav-more-btn" onclick="mobileGo('new');toggleMobileMenu()" id="mmb-new" style="display:none">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9"/><path d="M12 8v8M8 12h8"/></svg>
      <span>New Order</span>
    </div>
    <div class="mnav-more-btn" onclick="mobileGo('import');toggleMobileMenu()" id="mmb-import" style="display:none">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/></svg>
      <span>Import</span>
    </div>
    <div class="mnav-more-btn" onclick="mobileGo('onedrive');toggleMobileMenu()">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M3 15a4 4 0 004 4h9a5 5 0 10-.1-9.999 5.002 5.002 0 10-9.78 2.096A4.001 4.001 0 003 15z"/></svg>
      <span>OneDrive</span>
    </div>
    <div class="mnav-more-btn" onclick="doLogout();toggleMobileMenu()">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M9 21H5a2 2 0 01-2-2V5a2 2 0 012-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" y1="12" x2="9" y2="12"/></svg>
      <span>Logout</span>
    </div>
  </div>
</div>
<div id="mobile-more-overlay" style="display:none;position:fixed;top:0;left:0;right:0;bottom:0;z-index:340" onclick="toggleMobileMenu()"></div>

<!-- ── PWA INSTALL BANNER ── -->
<div id="pwa-banner">
  <div style="font-size:20px">📱</div>
  <p><strong>Add to Home Screen</strong>Tap Share → "Add to Home Screen" for app-like access</p>
  <button class="pwa-close" onclick="document.getElementById('pwa-banner').classList.remove('show');localStorage.setItem('pwaDismissed','1')">Got it</button>
</div>

<!-- ── MOBILE MORE BTN STYLES ── -->
<style>
.mnav-more-btn{display:flex;flex-direction:column;align-items:center;gap:5px;padding:12px 8px;border-radius:10px;cursor:pointer;background:var(--bg);border:1px solid var(--border);font-size:10px;font-weight:500;color:var(--text2);text-align:center;transition:all .15s}
.mnav-more-btn:hover{background:var(--blue-l);color:var(--blue-t);border-color:var(--blue)}
.mnav-more-btn svg{width:22px;height:22px}
</style>

<!-- ── COMMUNICATION PANEL ── -->
<div id="comm-fab" style="display:none">

  <!-- Main panel -->
  <div id="comm-panel">
    <!-- Header -->
    <div class="cp-head">
      <div class="cp-head-top">
        <h4>
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:15px;height:15px"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>
          <span id="cp-title">Team Chat</span>
        </h4>
        <div class="cp-head-btns">
          <!-- Audio call button — shown when in DM -->
          <button class="cp-head-btn" id="cp-call-btn" onclick="startCall()" style="display:none" title="Start audio call">
            <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 8.8 19.79 19.79 0 01.22 2.18 2 2 0 012.18 0h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L6.91 7.91a16 16 0 006.18 6.18l1.08-1.08a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 16.92z"/></svg>
            Call
          </button>
          <button class="cp-head-btn" onclick="toggleComm()" title="Close">
            <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
          </button>
        </div>
      </div>
      <!-- Contact avatars -->
      <div class="cp-contacts" id="cp-contacts"></div>
    </div>

    <!-- Messages -->
    <div class="cp-msgs" id="cp-msgs">
      <div class="cp-empty">
        <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>
        Select a contact or send a team message
      </div>
    </div>

    <!-- File preview strip -->
    <div class="cp-file-preview-strip" id="cp-file-strip"></div>

    <!-- Input row -->
    <div class="cp-input-row">
      <input type="file" id="cp-file-input" multiple
        accept=".pdf,.doc,.docx,.xls,.xlsx,.png,.jpg,.jpeg,.gif,.tiff,.bmp,.txt,.csv"
        onchange="handleCommFile(event)" style="display:none">
      <button class="cp-icon-btn" onclick="document.getElementById('cp-file-input').click()" title="Attach file (PDF, Word, Excel, Images)">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M21.44 11.05l-9.19 9.19a6 6 0 01-8.49-8.49l9.19-9.19a4 4 0 015.66 5.66l-9.2 9.19a2 2 0 01-2.83-2.83l8.49-8.48"/></svg>
      </button>
      <textarea id="cp-msg-input" placeholder="Type a message... (Enter to send)" rows="1"
        onkeydown="if(event.key==='Enter'&&!event.shiftKey){event.preventDefault();sendCommMsg()}"
        oninput="this.style.height='auto';this.style.height=Math.min(this.scrollHeight,90)+'px'"></textarea>
      <button class="cp-send-btn" onclick="sendCommMsg()">
        <svg fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24" style="width:14px;height:14px"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
      </button>
    </div>
  </div>

  <!-- FAB button -->
  <button id="comm-toggle" onclick="toggleComm()" title="Team Chat">
    <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>
    <span id="comm-badge"></span>
  </button>
</div>

<!-- ── CALL OVERLAY ── -->
<div id="call-overlay">
  <div class="call-box" id="call-box">
    <div class="call-avatar" id="call-avatar"></div>
    <div class="call-name" id="call-name"></div>
    <div class="call-status" id="call-status">Calling...</div>
    <!-- Incoming call buttons -->
    <div class="call-actions" id="call-incoming-btns" style="display:none">
      <button class="call-btn call-btn-end" onclick="rejectCall()" title="Decline">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M10.68 13.31a16 16 0 003.41 2.6l1.27-1.27a2 2 0 012.11-.45 12.84 12.84 0 002.81.7 2 2 0 011.72 2v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 2 2 0 01-.45-2.11c.17-.44.28-.9.33-1.37"/><line x1="1" y1="1" x2="23" y2="23"/></svg>
      </button>
      <button class="call-btn call-btn-accept" onclick="acceptCall()" title="Accept">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 8.8 19.79 19.79 0 01.22 2.18 2 2 0 012.18 0h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L6.91 7.91a16 16 0 006.18 6.18l1.08-1.08a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 16.92z"/></svg>
      </button>
    </div>
    <!-- Active call buttons -->
    <div class="call-actions" id="call-active-btns" style="display:none">
      <button class="call-btn call-btn-mute" id="call-mute-btn" onclick="toggleMute()" title="Mute">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M12 1a3 3 0 00-3 3v8a3 3 0 006 0V4a3 3 0 00-3-3z"/><path d="M19 10v2a7 7 0 01-14 0v-2"/><line x1="12" y1="19" x2="12" y2="23"/><line x1="8" y1="23" x2="16" y2="23"/></svg>
      </button>
      <button class="call-btn call-btn-end" onclick="endCall()" title="End call">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M10.68 13.31a16 16 0 003.41 2.6l1.27-1.27a2 2 0 012.11-.45 12.84 12.84 0 002.81.7 2 2 0 011.72 2v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 2 2 0 01-.45-2.11c.17-.44.28-.9.33-1.37"/><line x1="1" y1="1" x2="23" y2="23"/></svg>
      </button>
    </div>
    <div class="call-timer" id="call-timer" style="display:none">00:00</div>
  </div>
</div>

<!-- ── MEETING PANEL (hidden - removed) ── -->
<div id="meeting-panel" style="display:none"></div>

<div class="app" id="main-app" style="display:none">

<!-- SIDEBAR -->
<aside class="sb">
  <div class="sb-logo">
    <div class="b1">Title Order Management</div>
    <div class="b2">YDeal &amp; Title Priority</div>
  </div>
  <nav class="sb-nav">
    <div class="nl">Orders</div>
    <div class="ni active" onclick="go('dashboard')">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>
      Dashboard
    </div>
    <div class="nl admin-only">Add Orders</div>
    <div class="ni admin-only" onclick="go('import');setIT('email')">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
      Email / PDF Paste
    </div>
    <div class="ni admin-only" onclick="go('import');setIT('excel')">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>
      Excel / CSV Import
    </div>
    <div class="ni admin-only" onclick="go('new')">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9"/><path d="M12 8v8M8 12h8"/></svg>
      Manual Entry
    </div>
    <div class="nl">Work</div>
    <div class="ni" onclick="go('uploads')">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
      Uploads
    </div>
    <div class="ni" onclick="go('typing')">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 21V5a2 2 0 00-2-2h-4a2 2 0 00-2 2v16"/><path d="M6 11h4M6 15h4M14 11h4M14 15h4"/></svg>
      Typing Packages
    </div>
    <div class="nl admin-only">Team</div>
    <div class="ni admin-only" onclick="go('team')">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="9" cy="7" r="3"/><path d="M3 20c0-4 2.7-7 6-7h0c3.3 0 6 3 6 7"/><circle cx="17" cy="8" r="2.5"/><path d="M21 20c0-3.3-1.8-6-4-6"/></svg>
      Team View
    </div>
    <div class="nl admin-only">Export</div>
    <div class="ni admin-only" onclick="exportExcel()">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
      Export to Excel
    </div>
    <div class="ni admin-only" onclick="go('onedrive')">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M3 15a4 4 0 004 4h9a5 5 0 10-.1-9.999 5.002 5.002 0 10-9.78 2.096A4.001 4.001 0 003 15z"/></svg>
      OneDrive Setup
    </div>
    <div class="ni admin-only" onclick="go('qualia')">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/></svg>
      Qualia API
    </div>
  </nav>
  <div class="sb-foot">
    <!-- Open My OneDrive — opens assigned orders folder -->
    <div id="sb-onedrive-btn" style="margin-bottom:10px">
      <button class="btn btn-p" style="width:100%;justify-content:center;gap:7px;font-size:11px" onclick="openMyOneDrive()">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:13px;height:13px"><path d="M3 15a4 4 0 004 4h9a5 5 0 10-.1-9.999 5.002 5.002 0 10-9.78 2.096A4.001 4.001 0 003 15z"/></svg>
        Open My OneDrive Folder
      </button>
    </div>
    <div style="display:flex;gap:6px;margin-bottom:10px">
      <a href="https://ydealtitleservices.com/" target="_blank"
        style="flex:1;display:flex;align-items:center;justify-content:center;gap:5px;padding:6px 8px;background:var(--blue-l);border:1px solid rgba(27,79,138,.18);border-radius:8px;font-size:10px;font-weight:600;color:var(--blue-t);text-decoration:none;transition:all .15s"
        onmouseover="this.style.background='#d4e4f7'" onmouseout="this.style.background='var(--blue-l)'">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px;flex-shrink:0"><circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 014 10 15.3 15.3 0 01-4 10 15.3 15.3 0 01-4-10 15.3 15.3 0 014-10z"/></svg>
        YDeal Site
      </a>
      <a href="https://www.titlepriority.com/" target="_blank"
        style="flex:1;display:flex;align-items:center;justify-content:center;gap:5px;padding:6px 8px;background:var(--green-l);border:1px solid rgba(45,106,53,.18);border-radius:8px;font-size:10px;font-weight:600;color:var(--green);text-decoration:none;transition:all .15s"
        onmouseover="this.style.background='#cce8d0'" onmouseout="this.style.background='var(--green-l)'">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px;flex-shrink:0"><circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 014 10 15.3 15.3 0 01-4 10 15.3 15.3 0 01-4-10 15.3 15.3 0 014-10z"/></svg>
        TP Site
      </a>
    </div>
    <div class="nl" style="padding:0 0 6px">Receiving Emails</div>
    <div class="email-chip">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
      <span>orders@ydealtitleservices.com</span>
    </div>
    <div class="email-chip">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
      <span>orders@titlepriority.com</span>
    </div>
  </div>
</aside>

<!-- MAIN -->
<div class="main">
  <div class="topbar">
    <div>
      <div class="tb-title" id="page-title">All Orders</div>
      <div class="tb-sub" id="page-sub">Title Search Order Management</div>
    </div>
    <div class="tb-actions">
      <div id="topbar-date" style="font-size:11px;color:var(--text3)"></div>
      <!-- User info -->
      <div class="user-topbar-info" id="topbar-user">
        <div class="user-avatar" id="topbar-avatar"></div>
        <div>
          <div class="user-name" id="topbar-name"></div>
          <span class="user-role" id="topbar-role"></span>
        </div>
      </div>
      <button class="btn btn-p" onclick="go('new')" id="btn-new-order">
        <svg fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path d="M12 5v14M5 12h14"/></svg>
        New Order
      </button>
      <button class="btn" onclick="doLogout()" title="Sign out" style="padding:6px 10px">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:14px;height:14px"><path d="M9 21H5a2 2 0 01-2-2V5a2 2 0 012-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" y1="12" x2="9" y2="12"/></svg>
      </button>
    </div>
  </div>

  <div class="content">

    <!-- DASHBOARD -->
    <div id="page-dashboard" class="page active">
      <div class="metrics" id="metrics-row"></div>
      <div class="cbar">
        <div class="sw">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="11" cy="11" r="7"/><path d="M21 21l-4.35-4.35"/></svg>
          <input type="text" id="srch" placeholder="Search order #, borrower, address, parcel..." oninput="render()">
        </div>
        <select id="fCo" onchange="render()">
          <option value="">All companies</option>
          <option value="YDeal">YDeal Title Services</option>
          <option value="TitlePriority">Title Priority</option>
        </select>
        <select id="fType" onchange="render()">
          <option value="">All order types</option>
          <option>Current Owner Search</option>
          <option>Two Owner Search</option>
          <option>Full Search</option>
          <option>Update/Bring Down Search</option>
          <option>Tax Search</option>
          <option>Typing</option>
          <option>Document Retrieval</option>
          <option>Mortgage Search</option>
          <option>Assignment Verification Search</option>
          <option>Deeds and Chains Search</option>
        </select>
        <select id="fSt" onchange="render()">
          <option value="">All statuses</option>
          <option>Open Order</option>
          <option>In Progress</option>
          <option>Completed</option>
          <option>Submitted</option>
          <option>Cancelled</option>
          <option>Pending for Documents</option>
          <option>Tax Pending</option>
          <option>Need to Call for Taxes</option>
          <option>Typing Pending</option>
          <option>Abstractor Order</option>
          <option>Quality/Final Review</option>
        </select>
        <select id="fAs" onchange="render()">
          <option value="">All assignees</option>
          <option value="AJ">AJ</option><option value="KM">KM</option><option value="SR">SR</option><option value="TL">TL</option>
        </select>
        <select id="fState" onchange="render()"><option value="">All states</option></select>
        <button class="btn btn-sm" onclick="clearF()">Clear</button>
      </div>
      <div class="tcard">
        <div class="tscroll">
          <table style="min-width:1280px">
            <thead><tr>
              <th style="width:32px">SL</th>
              <th style="width:115px">Order #</th>
              <th style="width:82px">Order date</th>
              <th style="width:100px">Company</th>
              <th style="width:105px">Client order #</th>
              <th style="width:145px">Order type</th>
              <th style="width:140px">Borrower</th>
              <th style="width:170px">Property address</th>
              <th style="width:82px">County</th>
              <th style="width:32px">ST</th>
              <th style="width:120px">Parcel</th>
              <th style="width:108px">Due date</th>
              <th style="width:88px">Status</th>
              <th style="width:36px">Asgn</th>
              <th style="width:200px">Actions</th>
            </tr></thead>
            <tbody id="tbody"></tbody>
          </table>
        </div>
        <div id="empty-state" class="empty" style="display:none">
          <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"/></svg>
          <p id="empty-msg">No orders yet — add your first order using the sidebar</p>
        </div>
      </div>
    </div>

    <!-- IMPORT -->
    <div id="page-import" class="page">
      <div class="itabs">
        <div class="itab active" id="itab-email" onclick="setIT('email')">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
          Email / PDF Text
        </div>
        <div class="itab" id="itab-excel" onclick="setIT('excel')">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>
          Excel / CSV
        </div>
        <div class="itab" id="itab-tmpl" onclick="setIT('tmpl')">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
          Download Template
        </div>
      </div>

      <div class="ipanel active" id="ipanel-email">
        <div class="fpanel">
          <h3>Paste email or order text</h3>
          <p class="pdesc">Copy and paste the full text from any order email or PDF received at your company inboxes. AI extracts all fields automatically.</p>
          <div class="hbox">
            <div class="srow"><div class="snum">1</div><div>Open the order email or PDF → Select all text → Copy</div></div>
            <div class="srow"><div class="snum">2</div><div>Select which company inbox received this order</div></div>
            <div class="srow"><div class="snum">3</div><div>Paste below → click <strong>Parse with AI</strong> → Review → Save</div></div>
          </div>
          <div style="margin-bottom:10px">
            <label style="font-size:11px;font-weight:500;color:var(--text2);display:block;margin-bottom:4px">Received by</label>
            <select id="parse-co" style="width:280px">
              <option value="YDeal">YDeal Title Services — orders@ydealtitleservices.com</option>
              <option value="TitlePriority">Title Priority — orders@titlepriority.com</option>
            </select>
          </div>
          <div class="pzone">
            <textarea id="emailText" placeholder="Paste order email or document text here...&#10;&#10;Fields extracted: Order #, Client Order #, Order Type, Borrower, Property Address, County, State, Parcel, Due Date, Instructions"></textarea>
          </div>
          <div style="display:flex;gap:8px;align-items:center;flex-wrap:wrap">
            <button class="btn btn-p" onclick="parseEmail()">
              <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:13px;height:13px"><path d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"/></svg>
              Parse with AI
            </button>
            <button class="btn" onclick="loadSample()">Load sample</button>
            <span id="parse-status" style="display:none"></span>
          </div>
        </div>
        <div class="fpanel" id="parsed-preview" style="display:none">
          <h3>Review parsed order — edit if needed</h3>
          <div class="fg" id="parsed-fields"></div>
          <div class="factions">
            <button class="btn btn-p" onclick="saveParsed()">Save order + download Abstract Notes .txt</button>
            <button class="btn" onclick="document.getElementById('parsed-preview').style.display='none'">Discard</button>
          </div>
        </div>
      </div>

      <div class="ipanel" id="ipanel-excel">
        <div class="fpanel">
          <h3>Import from Excel or CSV</h3>
          <p class="pdesc">Upload a spreadsheet with order data. Map your columns and import all rows at once.</p>
          <div class="dzone" id="drop-zone" onclick="document.getElementById('file-input').click()" ondragover="handleDragOver(event)" ondragleave="handleDragLeave()" ondrop="handleDrop(event)">
            <input type="file" id="file-input" accept=".xlsx,.xls,.csv" onchange="handleFileSelect(event)">
            <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24" style="width:32px;height:32px;color:var(--text3);margin:0 auto 8px;display:block"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
            <p style="font-size:13px;color:var(--text2);margin-bottom:3px">Click or drag &amp; drop your file</p>
            <span style="font-size:11px;color:var(--text3)">.xlsx, .xls, .csv</span>
          </div>
          <div id="col-map-section" style="display:none">
            <div class="sec">Map your columns</div>
            <div class="col-map" id="col-map"></div>
            <div class="factions">
              <button class="btn btn-p" onclick="importExcel()">Import all rows</button>
              <button class="btn" onclick="showExcelPreview()">Preview</button>
              <button class="btn btn-r" onclick="resetExcel()">Cancel</button>
            </div>
          </div>
          <div id="import-result" style="display:none;margin-top:10px"></div>
        </div>
      </div>

      <div class="ipanel" id="ipanel-tmpl">
        <div class="fpanel">
          <h3>Download import template</h3>
          <p class="pdesc">Download the pre-formatted template, fill it in, then re-upload using the Excel/CSV tab.</p>
          <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:20px">
            <button class="btn btn-g" onclick="dlTemplate()">Download Excel Template</button>
            <button class="btn btn-a" onclick="dlCsvTemplate()">Download CSV Template</button>
          </div>
          <div class="sec">Template columns</div>
          <table style="min-width:unset;width:100%"><thead><tr><th>Column</th><th>Example</th><th>Required?</th></tr></thead><tbody id="tmpl-cols"></tbody></table>
        </div>
      </div>
    </div>

    <!-- MANUAL ENTRY -->
    <div id="page-new" class="page">
      <div class="fpanel">
        <h3 id="form-title">New Title Search Order</h3>
        <p class="pdesc">Fill in all fields. A .txt file will be downloaded on save for team assignment.</p>
        <div class="sec">Order details</div>
        <div class="fg">
          <div class="ff"><label>Received by (Company) *</label>
            <select id="f-co" onchange="autoFill()">
              <option value="YDeal">YDeal Title Services</option>
              <option value="TitlePriority">Title Priority</option>
            </select>
          </div>
          <div class="ff"><label>Order number *</label><input id="f-on" placeholder="e.g. 01-26027784-03T"></div>
          <div class="ff"><label>Client order number</label><input id="f-cn" placeholder="e.g. CLT-00101"></div>
          <div class="ff"><label>Order date</label><input id="f-od" type="date"></div>
          <div class="ff"><label>Due date &amp; time</label><input id="f-dd" type="datetime-local"></div>
          <div class="ff"><label>Order type *</label>
            <select id="f-type" onchange="onTypeChange()">
              <option>Current Owner Search</option>
              <option>Two Owner Search</option>
              <option>Full Search</option>
              <option>Update/Bring Down Search</option>
              <option>Tax Search</option>
              <option>Typing</option>
              <option>Document Retrieval</option>
              <option>Mortgage Search</option>
              <option>Assignment Verification Search</option>
              <option>Deeds and Chains Search</option>
            </select>
          </div>
          <div class="ff"><label>Status</label>
            <select id="f-st">
              <option>Open Order</option>
              <option>In Progress</option>
              <option>Completed</option>
              <option>Submitted</option>
              <option>Cancelled</option>
              <option>Pending for Documents</option>
              <option>Tax Pending</option>
              <option>Need to Call for Taxes</option>
              <option>Typing Pending</option>
              <option>Abstractor Order</option>
              <option>Quality/Final Review</option>
            </select>
          </div>
          <div class="ff"><label>Assigned to</label>
            <select id="f-ass">
              <option value="AJ">AJ — Alex J.</option><option value="KM">KM — Kim M.</option>
              <option value="SR">SR — Sara R.</option><option value="TL">TL — Tom L.</option>
            </select>
          </div>
          <div class="ff"><label>Agreed fee ($)</label><input id="f-fee" type="number" step="0.01" min="0" placeholder="30.00"></div>
        </div>
        <div class="sec">Borrower &amp; property</div>
        <div class="fg">
          <div class="ff full"><label>Borrower(s) / Buyer(s) *</label><input id="f-bw" placeholder="REESE LANG"></div>
          <div class="ff full"><label>Property address *</label><input id="f-pa" placeholder="49 PEBBLE BEACH CIR CHARLES TOWN, WV 25414"></div>
          <div class="ff"><label>County *</label><input id="f-county" placeholder="JEFFERSON"></div>
          <div class="ff"><label>State (abbr) *</label><input id="f-state" placeholder="WV" maxlength="2"></div>
          <div class="ff full"><label>Parcel *</label><input id="f-pid" placeholder="19-02-13A-0328.0000"></div>
        </div>
        <div class="sec">Instructions</div>
        <div class="fg">
          <!-- CC&RS toggle panel — shown only for order types that have this option -->
          <div class="ff full" id="ccrs-panel" style="display:none">
            <div style="background:var(--blue-l);border:1px solid rgba(27,79,138,.2);border-radius:var(--r);padding:12px 16px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px">
              <div>
                <div style="font-size:12px;font-weight:600;color:var(--blue-t)">CC&RS Required for this order?</div>
                <div style="font-size:11px;color:var(--text3);margin-top:2px">Select to auto-fill the correct ORT instructions</div>
              </div>
              <div style="display:flex;gap:7px">
                <button id="btn-ccrs-yes" class="btn btn-p btn-sm" onclick="applyCCRS(true)">
                  <svg fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24" style="width:11px;height:11px"><polyline points="20 6 9 17 4 12"/></svg>
                  With CC&RS
                </button>
                <button id="btn-ccrs-no" class="btn btn-sm" onclick="applyCCRS(false)">
                  <svg fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24" style="width:11px;height:11px"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
                  Without CC&RS
                </button>
              </div>
            </div>
          </div>

          <!-- Instructions textarea with auto-fill button -->
          <div class="ff full">
            <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:5px">
              <label>Client instructions / special notes</label>
              <div style="display:flex;gap:6px;align-items:center">
                <span id="inst-source-label" style="font-size:10px;color:var(--text3)"></span>
                <button class="btn btn-sm btn-p" onclick="autoFillInst()" id="btn-autofill-inst" style="display:none">
                  <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px"><path d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"/></svg>
                  Auto-fill ORT Instructions
                </button>
              </div>
            </div>
            <textarea id="f-inst" rows="6" placeholder="Instructions will auto-fill based on order type and company, or type manually..."></textarea>
          </div>
        </div>
        <div class="sec">Abstract Notes .txt preview</div>
        <div class="txtprev" id="txt-prev">Fill in the fields above, then click Preview .txt to see the Abstract Notes file</div>
        <div class="factions">
          <button class="btn" onclick="previewTxt()">Preview .txt</button>
          <button class="btn btn-p" onclick="saveOrder()">
            <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M19 21H5a2 2 0 01-2-2V5a2 2 0 012-2h11l5 5v11a2 2 0 01-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg>
            Save + download .txt
          </button>
          <button class="btn btn-r" onclick="clearForm()">Clear</button>
        </div>
      </div>
    </div>

    <!-- TEAM -->
    <div id="page-team" class="page">
      <div class="tcards" id="team-cards"></div>
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px">
        <span id="team-label" style="font-size:13px;color:var(--text2);font-weight:500"></span>
        <button class="btn btn-sm" onclick="clearTF()">Show all</button>
      </div>
      <div class="tcard">
        <div class="tscroll">
          <table style="min-width:1000px">
            <thead><tr>
              <th style="width:32px">SL</th><th style="width:115px">Order #</th><th style="width:82px">Date</th>
              <th style="width:100px">Company</th><th style="width:145px">Order type</th>
              <th style="width:140px">Borrower</th><th style="width:165px">Address</th>
              <th style="width:82px">County</th><th style="width:32px">ST</th>
              <th style="width:108px">Due date</th><th style="width:88px">Status</th><th style="width:110px">Actions</th>
            </tr></thead>
            <tbody id="team-tbody"></tbody>
          </table>
        </div>
        <div id="team-empty" class="empty" style="display:none">
          <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg>
          <p>No orders for this team member</p>
        </div>
      </div>
    </div>

    <!-- TYPING PACKAGES PAGE -->
    <div id="page-typing" class="page">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:16px;flex-wrap:wrap;gap:8px">
        <p style="font-size:12px;color:var(--text2)">Assemble and track the 7-section document package for each completed search, then send to the Typing team.</p>
        <select id="pkg-filter" onchange="renderTypingPage()" style="font-size:12px">
          <option value="">All orders</option>
          <option value="Completed">Completed</option>
          <option value="Typing Pending">Typing Pending</option>
          <option value="Quality/Final Review">Quality/Final Review</option>
          <option value="Submitted">Submitted</option>
        </select>
      </div>
      <div class="pkg-grid" id="pkg-grid"></div>
      <div id="pkg-empty" class="empty" style="display:none">
        <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M9 17H7A5 5 0 017 7h10a5 5 0 110 10h-2M12 12v6m0 0l-2-2m2 2l2-2"/></svg>
        <p>No orders available for packaging</p>
      </div>
    </div>

    <!-- UPLOADS PAGE -->
    <div id="page-uploads" class="page">

      <!-- Summary metrics -->
      <div class="upload-summary" id="upload-summary"></div>

      <!-- Tabs: All Orders / By Team Member -->
      <div class="upload-tabs">
        <div class="upload-tab active" id="utab-all"   onclick="setUploadTab('all')">All Orders</div>
        <div class="upload-tab"        id="utab-AJ"    onclick="setUploadTab('AJ')">Alex J. (AJ)</div>
        <div class="upload-tab"        id="utab-KM"    onclick="setUploadTab('KM')">Kim M. (KM)</div>
        <div class="upload-tab"        id="utab-SR"    onclick="setUploadTab('SR')">Sara R. (SR)</div>
        <div class="upload-tab"        id="utab-TL"    onclick="setUploadTab('TL')">Tom L. (TL)</div>
      </div>

      <!-- Filter bar -->
      <div class="cbar" style="margin-bottom:14px">
        <div class="sw">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="11" cy="11" r="7"/><path d="M21 21l-4.35-4.35"/></svg>
          <input type="text" id="upload-search" placeholder="Search order #, borrower..." oninput="renderUploads()">
        </div>
        <select id="upload-filter-status" onchange="renderUploads()">
          <option value="">All statuses</option>
          <option value="pending">Pending Upload</option>
          <option value="partial">Partially Uploaded</option>
          <option value="complete">Fully Uploaded</option>
        </select>
        <select id="upload-filter-type" onchange="renderUploads()">
          <option value="">All types</option>
          <option value="package">Package Files</option>
          <option value="typing">Typing Report</option>
        </select>
        <button class="btn btn-sm" onclick="document.getElementById('upload-search').value='';document.getElementById('upload-filter-status').value='';document.getElementById('upload-filter-type').value='';renderUploads()">Clear</button>
      </div>

      <!-- Orders list -->
      <div id="upload-orders-list"></div>
      <div id="upload-empty" class="empty" style="display:none">
        <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
        <p>No orders found</p>
      </div>
    </div>

    <!-- QUALIA API PAGE -->
    <div id="page-qualia" class="page">
      <div style="max-width:860px">

        <!-- API Credentials Setup -->
        <div class="card" style="margin-bottom:16px">
          <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;flex-wrap:wrap;gap:10px">
            <div>
              <h3 style="font-size:15px;font-weight:600;margin-bottom:3px">Qualia Marketplace API</h3>
              <p style="font-size:12px;color:var(--text3)">Production: marketplace.qualia.com &nbsp;·&nbsp; GraphQL + Basic Auth</p>
            </div>
            <div style="display:flex;gap:7px;align-items:center">
              <span id="qualia-status-badge" class="badge b-pend">Not Connected</span>
              <button class="btn btn-sm btn-p" onclick="testQualiaConnection()">Test Connection</button>
            </div>
          </div>
          <div class="fg">
            <div class="ff full">
              <label>API Key (Username)</label>
              <input type="text" id="q-username" placeholder="Your Qualia API username" oninput="saveQualiaConfig()">
            </div>
            <div class="ff full">
              <label>API Password</label>
              <div style="position:relative">
                <input type="password" id="q-password" placeholder="Your Qualia API password" style="width:100%;padding-right:40px" oninput="saveQualiaConfig()">
                <button onclick="toggleQualiaPass()" type="button" style="position:absolute;right:10px;top:50%;transform:translateY(-50%);background:none;border:none;cursor:pointer;color:var(--text3)">
                  <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:15px;height:15px"><path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/></svg>
                </button>
              </div>
            </div>
            <div class="ff full">
              <label>Webhook Endpoint URL <span style="font-size:10px;color:var(--text3)">(where Qualia sends notifications)</span></label>
              <input type="text" id="q-webhook" placeholder="https://your-domain.com/qualia-webhook" oninput="saveQualiaConfig()">
            </div>
          </div>
          <div style="background:var(--blue-l);border-radius:var(--r);padding:10px 14px;font-size:11px;color:var(--blue-t);margin-top:12px;line-height:1.7">
            <strong>Status:</strong> Your API credentials are pre-configured. Click <strong>Test Connection</strong> to verify the connection is live.
          </div>
        </div>

        <!-- Tabs -->
        <div class="upload-tabs" style="margin-bottom:16px">
          <div class="upload-tab active" id="qtab-orders"  onclick="setQTab('orders')">Pending Orders</div>
          <div class="upload-tab"        id="qtab-fetch"   onclick="setQTab('fetch')">Fetch Order</div>
          <div class="upload-tab"        id="qtab-submit"  onclick="setQTab('submit')">Submit / Update</div>
          <div class="upload-tab"        id="qtab-webhook" onclick="setQTab('webhook')">Webhooks</div>
        </div>

        <!-- PENDING ORDERS tab -->
        <div id="qpanel-orders" class="upload-panel active">
          <div style="display:flex;gap:8px;margin-bottom:14px;flex-wrap:wrap">
            <button class="btn btn-p" onclick="qualiaFetchOrders()">
              <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:13px;height:13px"><polyline points="23 4 23 10 17 10"/><path d="M20.49 15a9 9 0 11-2.12-9.36L23 10"/></svg>
              Refresh from Qualia
            </button>
            <button class="btn btn-sm" onclick="qualiaClearLog()">Clear log</button>
          </div>
          <div id="qualia-orders-list">
            <div class="empty">
              <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/></svg>
              <p>Click "Refresh from Qualia" to load pending orders</p>
            </div>
          </div>
        </div>

        <!-- FETCH ORDER tab -->
        <div id="qpanel-fetch" class="upload-panel">
          <div class="fg" style="margin-bottom:12px">
            <div class="ff full">
              <label>Qualia Order ID</label>
              <input id="q-fetch-id" placeholder="e.g. bK8bg5tajNkDpDk25">
            </div>
          </div>
          <button class="btn btn-p" onclick="qualiaFetchOrder()">Fetch Order Details</button>
          <div id="qualia-fetch-result" style="margin-top:14px"></div>
        </div>

        <!-- SUBMIT / UPDATE tab -->
        <div id="qpanel-submit" class="upload-panel">
          <div class="fg" style="margin-bottom:12px">
            <div class="ff full">
              <label>Qualia Order ID</label>
              <input id="q-action-id" placeholder="e.g. bK8bg5tajNkDpDk25">
            </div>
          </div>
          <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:16px">
            <button class="btn btn-sm btn-g"  onclick="qualiaAction('accept')">Accept Order</button>
            <button class="btn btn-sm btn-p"  onclick="qualiaAction('submit')">Submit Order</button>
            <button class="btn btn-sm btn-a"  onclick="qualiaAction('decline')">Decline Order</button>
            <button class="btn btn-sm"        onclick="qualiaAction('cancel')">Cancel Order</button>
          </div>

          <!-- Send message -->
          <div style="border-top:1px solid var(--border);padding-top:14px;margin-top:4px">
            <div style="font-size:12px;font-weight:600;color:var(--text);margin-bottom:10px">Send Message to Customer</div>
            <div class="fg">
              <div class="ff full">
                <label>Message</label>
                <textarea id="q-msg-text" rows="3" placeholder="Type your message to the customer..."></textarea>
              </div>
              <div class="ff full">
                <label>Your Name</label>
                <input id="q-msg-from" placeholder="e.g. YDeal Title Services">
              </div>
            </div>
            <button class="btn btn-p" onclick="qualiaSendMessage()" style="margin-top:8px">Send Message</button>
          </div>

          <!-- Upload file -->
          <div style="border-top:1px solid var(--border);padding-top:14px;margin-top:14px">
            <div style="font-size:12px;font-weight:600;color:var(--text);margin-bottom:10px">Upload File to Order</div>
            <div class="fg">
              <div class="ff full">
                <label>File (PDF, Word, etc.)</label>
                <div class="file-drop" onclick="document.getElementById('q-file-upload').click()"
                  ondragover="event.preventDefault();this.classList.add('dragover')"
                  ondragleave="this.classList.remove('dragover')"
                  ondrop="handleQualiaFileDrop(event)">
                  <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
                  <p id="q-file-label">Click or drag file here</p>
                  <input type="file" id="q-file-upload" accept=".pdf,.doc,.docx,.txt" onchange="handleQualiaFileSelect(event)" style="display:none">
                </div>
              </div>
              <div class="ff">
                <label>File type</label>
                <select id="q-file-primary">
                  <option value="true">Primary document (title search)</option>
                  <option value="false">Additional document</option>
                </select>
              </div>
            </div>
            <button class="btn btn-p" onclick="qualiaUploadFile()" style="margin-top:8px">Upload to Qualia</button>
          </div>
          <div id="qualia-action-result" style="margin-top:14px"></div>
        </div>

        <!-- WEBHOOKS tab -->
        <div id="qpanel-webhook" class="upload-panel">

          <!-- Step 1 — Your webhook endpoint -->
          <div class="card" style="margin-bottom:14px">
            <div style="font-size:13px;font-weight:600;margin-bottom:10px;display:flex;align-items:center;gap:7px">
              <span style="width:22px;height:22px;border-radius:50%;background:var(--blue);color:#fff;font-size:11px;font-weight:700;display:inline-flex;align-items:center;justify-content:center;flex-shrink:0">1</span>
              Your Webhook Endpoint URL
            </div>
            <p style="font-size:12px;color:var(--text3);margin-bottom:10px;line-height:1.6">
              This is the URL you register in Qualia so they can notify your dashboard of new orders, cancellations, and messages. After deploying your dashboard to Netlify, your endpoint URL will be:
            </p>
            <div style="display:flex;gap:8px;align-items:center;flex-wrap:wrap">
              <div style="flex:1;background:var(--bg);border:1px solid var(--border2);border-radius:var(--r);padding:9px 12px;font-family:'DM Mono',monospace;font-size:12px;color:var(--text);min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap" id="webhook-url-display">
                https://ydeal144.github.io/title-dashboard/.netlify/functions/qualia-webhook
              </div>
              <button class="btn btn-sm btn-p" onclick="copyWebhookUrl()">
                <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:12px;height:12px"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 01-2-2V4a2 2 0 012-2h9a2 2 0 012 2v1"/></svg>
                Copy
              </button>
            </div>
            <div style="margin-top:10px;display:flex;gap:8px;align-items:center">
              <input type="text" id="q-base-url" placeholder="Paste your Netlify URL here (e.g. https://ydeal-dash.netlify.app)"
                style="flex:1" oninput="updateWebhookUrl(this.value)">
            </div>
          </div>

          <!-- Step 2 — Register in Qualia -->
          <div class="card" style="margin-bottom:14px">
            <div style="font-size:13px;font-weight:600;margin-bottom:10px;display:flex;align-items:center;gap:7px">
              <span style="width:22px;height:22px;border-radius:50%;background:var(--blue);color:#fff;font-size:11px;font-weight:700;display:inline-flex;align-items:center;justify-content:center;flex-shrink:0">2</span>
              Register in Qualia Marketplace
            </div>
            <div style="font-size:12px;color:var(--text2);line-height:1.9">
              <div style="display:flex;gap:8px;margin-bottom:6px;align-items:flex-start">
                <span style="color:var(--blue);font-weight:600;flex-shrink:0">①</span>
                Log in to <strong>marketplace.qualia.com</strong>
              </div>
              <div style="display:flex;gap:8px;margin-bottom:6px;align-items:flex-start">
                <span style="color:var(--blue);font-weight:600;flex-shrink:0">②</span>
                Go to <strong>Manage → API tab</strong>
              </div>
              <div style="display:flex;gap:8px;margin-bottom:6px;align-items:flex-start">
                <span style="color:var(--blue);font-weight:600;flex-shrink:0">③</span>
                Click <strong>"Add Webhook"</strong> or <strong>"Register Endpoint"</strong>
              </div>
              <div style="display:flex;gap:8px;margin-bottom:6px;align-items:flex-start">
                <span style="color:var(--blue);font-weight:600;flex-shrink:0">④</span>
                Paste your endpoint URL from Step 1 above
              </div>
              <div style="display:flex;gap:8px;align-items:flex-start">
                <span style="color:var(--blue);font-weight:600;flex-shrink:0">⑤</span>
                Select the event: <strong>"Activity Created"</strong> — this is the only event you need
              </div>
            </div>
            <a href="https://marketplace.qualia.com" target="_blank" class="btn btn-sm btn-p" style="margin-top:12px;display:inline-flex">
              <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:12px;height:12px"><path d="M18 13v6a2 2 0 01-2 2H5a2 2 0 01-2-2V8a2 2 0 012-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
              Open Qualia Marketplace
            </a>
          </div>

          <!-- Step 3 — Event types reference -->
          <div class="card" style="margin-bottom:14px">
            <div style="font-size:13px;font-weight:600;margin-bottom:12px;display:flex;align-items:center;gap:7px">
              <span style="width:22px;height:22px;border-radius:50%;background:var(--blue);color:#fff;font-size:11px;font-weight:700;display:inline-flex;align-items:center;justify-content:center;flex-shrink:0">3</span>
              Webhook Event Types
            </div>
            <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
              <div style="padding:10px 12px;background:var(--blue-l);border-radius:var(--r);border-left:3px solid var(--blue)">
                <div style="font-size:11px;font-weight:600;color:var(--blue-t);font-family:'DM Mono',monospace;margin-bottom:3px">order_request</div>
                <div style="font-size:11px;color:var(--text2)">New order placed — requires your acceptance</div>
              </div>
              <div style="padding:10px 12px;background:var(--red-l);border-radius:var(--r);border-left:3px solid var(--red)">
                <div style="font-size:11px;font-weight:600;color:var(--red);font-family:'DM Mono',monospace;margin-bottom:3px">order_cancelled</div>
                <div style="font-size:11px;color:var(--text2)">Customer cancelled the order</div>
              </div>
              <div style="padding:10px 12px;background:var(--green-l);border-radius:var(--r);border-left:3px solid var(--green)">
                <div style="font-size:11px;font-weight:600;color:var(--green);font-family:'DM Mono',monospace;margin-bottom:3px">order_completed</div>
                <div style="font-size:11px;color:var(--text2)">Customer accepted your submission</div>
              </div>
              <div style="padding:10px 12px;background:var(--amber-l,#FEF3C7);border-radius:var(--r);border-left:3px solid var(--amber,#D97706)">
                <div style="font-size:11px;font-weight:600;color:var(--amber,#D97706);font-family:'DM Mono',monospace;margin-bottom:3px">order_revision_requested</div>
                <div style="font-size:11px;color:var(--text2)">Customer requested changes</div>
              </div>
              <div style="padding:10px 12px;background:var(--surface2);border-radius:var(--r);border-left:3px solid var(--border2);grid-column:1/-1">
                <div style="font-size:11px;font-weight:600;color:var(--text2);font-family:'DM Mono',monospace;margin-bottom:3px">message</div>
                <div style="font-size:11px;color:var(--text2)">Customer sent you a message — use the order_id to fetch and reply</div>
              </div>
            </div>
          </div>

          <!-- Live event log -->
          <div class="card">
            <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
              <div>
                <div style="font-size:13px;font-weight:600">Live Event Log</div>
                <div style="font-size:11px;color:var(--text3);margin-top:2px">Incoming webhook events from Qualia appear here automatically</div>
              </div>
              <div style="display:flex;gap:6px">
                <button class="btn btn-sm btn-p" onclick="qualiaSimulateWebhook()">Simulate Test Event</button>
                <button class="btn btn-sm" onclick="qualiaClearWebhookLog()">Clear</button>
              </div>
            </div>
            <div id="qualia-webhook-log">
              <div class="empty" style="padding:20px 0">
                <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M18 20V10M12 20V4M6 20v-6"/></svg>
                <p>No webhook events received yet. Click "Simulate Test Event" to preview how events look.</p>
              </div>
            </div>
          </div>

        </div>

      </div>
    </div>
    <!-- END QUALIA PAGE -->
    <div id="page-onedrive" class="page">
      <div class="fpanel">

        <!-- MY ONEDRIVE QUICK ACCESS -->
        <div class="card" style="margin-bottom:18px;border-left:3px solid var(--blue)">
          <div style="display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px;margin-bottom:12px">
            <div>
              <div style="font-size:14px;font-weight:600;color:var(--text);margin-bottom:3px" id="od-greeting">My OneDrive Folders</div>
              <div style="font-size:12px;color:var(--text3)" id="od-user-sub">Your assigned orders organized by date</div>
            </div>
            <button class="btn btn-p" onclick="openMyOneDrive()" style="gap:7px">
              <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:13px;height:13px"><path d="M3 15a4 4 0 004 4h9a5 5 0 10-.1-9.999 5.002 5.002 0 10-9.78 2.096A4.001 4.001 0 003 15z"/></svg>
              Open My OneDrive Folder
            </button>
          </div>

          <!-- Assigned orders list with folder paths -->
          <div id="od-assigned-orders"></div>
        </div>

        <h3>OneDrive Folder Structure</h3>
        <p class="pdesc">Every order file is named and organized by date and order number. Follow this structure to keep all files consistent in OneDrive.</p>

        <!-- FOLDER TREE -->
        <div class="sec">Required folder structure</div>
        <div style="background:#1A1917;border-radius:var(--r);padding:16px 20px;font-family:'DM Mono',monospace;font-size:12px;color:#A8E6A3;line-height:2;margin-bottom:18px">
          <div>📁 OneDrive</div>
          <div>&nbsp;&nbsp;└── 📁 <span style="color:#FFD700">Title Orders</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── 📁 <span style="color:#87CEEB">MM-DD-YYYY</span> &nbsp;<span style="color:#888;font-size:11px">(one folder per order date)</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── 📁 <span style="color:#FFA07A">Order-Number</span> &nbsp;<span style="color:#888;font-size:11px">(one subfolder per order)</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── 📄 <span style="color:#98FB98">OrderNumber.txt</span> &nbsp;<span style="color:#888;font-size:11px">(Abstract Notes)</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── 📄 <span style="color:#98FB98">OrderNumber_Package_MM-DD-YYYY.txt</span> &nbsp;<span style="color:#888;font-size:11px">(Cover Sheet)</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── 📄 <span style="color:#98FB98">OrderNumber_TypingReport_MM-DD-YYYY.txt</span> &nbsp;<span style="color:#888;font-size:11px">(Typing Report)</span></div>
        </div>

        <!-- REAL EXAMPLE -->
        <div class="sec">Real example — order 01-26027784-03T dated April 22, 2026</div>
        <div style="background:#1A1917;border-radius:var(--r);padding:16px 20px;font-family:'DM Mono',monospace;font-size:12px;color:#A8E6A3;line-height:2;margin-bottom:18px">
          <div>📁 OneDrive</div>
          <div>&nbsp;&nbsp;└── 📁 <span style="color:#FFD700">Title Orders</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── 📁 <span style="color:#87CEEB">04-22-2026</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── 📁 <span style="color:#FFA07A">01-26027784-03T</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── 📄 <span style="color:#98FB98">01-26027784-03T.txt</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── 📄 <span style="color:#98FB98">01-26027784-03T_Package_04-22-2026.txt</span></div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── 📄 <span style="color:#98FB98">01-26027784-03T_TypingReport_04-22-2026.txt</span></div>
        </div>

        <!-- STEP BY STEP -->
        <div class="sec">How to set this up in OneDrive — step by step</div>
        <div style="display:flex;flex-direction:column;gap:12px;margin-bottom:18px">
          <div class="hbox" style="display:flex;gap:12px;align-items:flex-start">
            <div class="snum" style="min-width:28px;height:28px;font-size:13px">1</div>
            <div>
              <div style="font-weight:600;margin-bottom:3px">Create the root folder in OneDrive</div>
              <div style="font-size:12px">Open OneDrive on your computer or browser → Create a new folder named exactly: <span style="font-family:'DM Mono',monospace;background:rgba(27,79,138,.15);padding:1px 6px;border-radius:4px">Title Orders</span></div>
            </div>
          </div>
          <div class="hbox" style="display:flex;gap:12px;align-items:flex-start">
            <div class="snum" style="min-width:28px;height:28px;font-size:13px">2</div>
            <div>
              <div style="font-weight:600;margin-bottom:3px">Each day orders arrive — create a date folder</div>
              <div style="font-size:12px">Inside <span style="font-family:'DM Mono',monospace;background:rgba(27,79,138,.15);padding:1px 6px;border-radius:4px">Title Orders</span>, create a folder using the order date in format <span style="font-family:'DM Mono',monospace;background:rgba(27,79,138,.15);padding:1px 6px;border-radius:4px">MM-DD-YYYY</span> — for example <span style="font-family:'DM Mono',monospace;background:rgba(27,79,138,.15);padding:1px 6px;border-radius:4px">04-22-2026</span></div>
            </div>
          </div>
          <div class="hbox" style="display:flex;gap:12px;align-items:flex-start">
            <div class="snum" style="min-width:28px;height:28px;font-size:13px">3</div>
            <div>
              <div style="font-weight:600;margin-bottom:3px">For each order — create an order number subfolder</div>
              <div style="font-size:12px">Inside the date folder, create a subfolder named exactly as the order number — for example <span style="font-family:'DM Mono',monospace;background:rgba(27,79,138,.15);padding:1px 6px;border-radius:4px">01-26027784-03T</span></div>
            </div>
          </div>
          <div class="hbox" style="display:flex;gap:12px;align-items:flex-start">
            <div class="snum" style="min-width:28px;height:28px;font-size:13px">4</div>
            <div>
              <div style="font-weight:600;margin-bottom:3px">Download files from the dashboard and move into the folder</div>
              <div style="font-size:12px">When you click <strong>.txt</strong>, <strong>Pkg</strong>, or <strong>Type</strong> buttons on any order, the file downloads automatically with the correct name. Move it into the matching OneDrive order subfolder.</div>
            </div>
          </div>
          <div class="hbox" style="display:flex;gap:12px;align-items:flex-start">
            <div class="snum" style="min-width:28px;height:28px;font-size:13px">5</div>
            <div>
              <div style="font-weight:600;margin-bottom:3px">Share the Title Orders folder with your team</div>
              <div style="font-size:12px">Right-click the <span style="font-family:'DM Mono',monospace;background:rgba(27,79,138,.15);padding:1px 6px;border-radius:4px">Title Orders</span> folder in OneDrive → Share → enter your team members' email addresses → set permission to <strong>Can edit</strong></div>
            </div>
          </div>
        </div>

        <!-- LIVE PATH GENERATOR -->
        <div class="sec">Generate folder path & Windows Run command for any order</div>
        <p style="font-size:12px;color:var(--text3);margin-bottom:10px">Enter order details to generate the exact folder path, Windows Run command, and batch script command.</p>
        <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-bottom:10px">
          <select id="od-company" style="width:160px">
            <option value="YDeal">YDeal Title Services</option>
            <option value="TitlePriority">Title Priority</option>
          </select>
          <input id="od-ordernum" placeholder="Order number e.g. 01-26027784-03T" style="width:260px">
          <input id="od-date" type="date" style="width:160px">
          <button class="btn btn-p" onclick="generateODPath()">Generate</button>
        </div>
        <div id="od-result" style="display:none;background:#1A1917;border-radius:var(--r);padding:14px 18px;font-family:'DM Mono',monospace;font-size:11px;color:#A8E6A3;line-height:2"></div>

        <!-- NETWORK DRIVE RUN COMMANDS -->
        <div class="sec" style="margin-top:20px">Windows Run commands (Win + R) for all employees</div>
        <p style="font-size:12px;color:var(--text3);margin-bottom:12px">Share these commands with your team. Press <strong>Windows Key + R</strong>, type the command, press Enter.</p>
        <div style="background:#1A1917;border-radius:var(--r);padding:16px 20px;font-family:'DM Mono',monospace;font-size:12px;color:#A8E6A3;line-height:2.2;margin-bottom:14px">
          <div style="color:#888;font-size:10px;margin-bottom:4px"># Open entire shared drive</div>
          <div>Z:\</div>
          <div style="color:#888;font-size:10px;margin-top:8px;margin-bottom:4px"># Open Title Orders root folder</div>
          <div>Z:\Title Orders</div>
          <div style="color:#888;font-size:10px;margin-top:8px;margin-bottom:4px"># Open YDeal orders folder</div>
          <div>Z:\Title Orders\YDeal</div>
          <div style="color:#888;font-size:10px;margin-top:8px;margin-bottom:4px"># Open Title Priority orders folder</div>
          <div>Z:\Title Orders\TitlePriority</div>
          <div style="color:#888;font-size:10px;margin-top:8px;margin-bottom:4px"># Create new order folder (double-click on desktop)</div>
          <div style="color:#FFD700">CreateOrderFolder.bat</div>
        </div>

        <!-- BATCH SCRIPT DOWNLOAD -->
        <div class="sec">Auto-create order folder script</div>
        <p style="font-size:12px;color:var(--text3);margin-bottom:10px">Download this script, put it on every employee's desktop. When they double-click it, it asks for order details and creates all 9 subfolders automatically on the shared drive.</p>
        <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:14px">
          <button class="btn btn-p" onclick="downloadBatchScript()">
            <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:13px;height:13px"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
            Download CreateOrderFolder.bat
          </button>
          <button class="btn btn-sm" onclick="downloadPSScript()">
            <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:12px;height:12px"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
            Download PowerShell Script
          </button>
        </div>
        <div style="background:#1A1917;border-radius:var(--r);padding:14px 18px;font-family:'DM Mono',monospace;font-size:11px;color:#A8E6A3;line-height:1.9">
          <div style="color:#888;margin-bottom:6px"># Preview of CreateOrderFolder.bat</div>
          <div>@echo off</div>
          <div>set /p ORDER_NUM=Enter Order Number: </div>
          <div>set /p EST_DATE=Enter EST Date (MM-DD-YYYY): </div>
          <div>set /p COMPANY=Enter Company (YDeal or TitlePriority): </div>
          <div style="color:#888">...</div>
          <div>mkdir "Z:\Title Orders\%COMPANY%\%EST_DATE%\%ORDER_NUM%\1 - Plat Map"</div>
          <div>mkdir "Z:\Title Orders\%COMPANY%\%EST_DATE%\%ORDER_NUM%\2 - Assessor"</div>
          <div>mkdir "Z:\Title Orders\%COMPANY%\%EST_DATE%\%ORDER_NUM%\3 - Taxes"</div>
          <div style="color:#888">... (9 subfolders total)</div>
          <div style="color:#FFD700">start explorer "Z:\Title Orders\%COMPANY%\%EST_DATE%\%ORDER_NUM%"</div>
        </div>

        <!-- TIPS -->
        <div class="sec">Tips for keeping OneDrive organised</div>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px">
          <div style="background:var(--green-l);border-radius:var(--r);padding:12px 14px;font-size:12px">
            <div style="font-weight:600;color:var(--green);margin-bottom:4px">✓ Do</div>
            <div style="color:var(--text2);line-height:1.8">
              Use exact order number as folder name<br>
              Use MM-DD-YYYY for date folders<br>
              Store all 3 files per order together<br>
              Share the root folder with your whole team<br>
              Keep one <span style="font-family:'DM Mono',monospace">Title Orders</span> folder for all companies
            </div>
          </div>
          <div style="background:var(--red-l);border-radius:var(--r);padding:12px 14px;font-size:12px">
            <div style="font-weight:600;color:var(--red);margin-bottom:4px">✗ Don't</div>
            <div style="color:var(--text2);line-height:1.8">
              Don't rename downloaded files<br>
              Don't mix orders from different dates in one folder<br>
              Don't store files on Desktop instead of OneDrive<br>
              Don't create separate folders per company<br>
              Don't delete old date folders
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</div>
</div>

<!-- TYPING REPORT MODAL -->
<div class="overlay" id="tr-overlay">
  <div class="mbox" style="width:720px;max-height:90vh;overflow-y:auto">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:4px;flex-wrap:wrap;gap:8px">
      <h3 id="tr-title">Typing Report</h3>
      <div style="display:flex;gap:6px;flex-wrap:wrap;align-items:center">
        <span id="tr-co-badge"></span>
        <span id="tr-co-name" style="font-size:11px;color:var(--text3);font-family:'DM Mono',monospace"></span>
      </div>
    </div>
    <p style="font-size:11px;color:var(--text3);margin-bottom:16px">Fill in all fields. The downloaded report will exactly match the <strong id="tr-co-label"></strong> typing report template.</p>

    <!-- ORDER INFO (pre-filled, read-only display) -->
    <div style="background:var(--bg);border-radius:var(--r);padding:12px 14px;margin-bottom:16px;display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;font-size:12px">
      <div><span style="font-size:10px;color:var(--text3);font-weight:600;text-transform:uppercase;display:block;margin-bottom:2px">Order Number</span><span id="tr-ordernum" style="font-weight:600;font-family:'DM Mono',monospace;font-size:11px"></span></div>
      <div><span style="font-size:10px;color:var(--text3);font-weight:600;text-transform:uppercase;display:block;margin-bottom:2px">Product Name</span><span id="tr-product" style="font-weight:500"></span></div>
      <div><span style="font-size:10px;color:var(--text3);font-weight:600;text-transform:uppercase;display:block;margin-bottom:2px">County</span><span id="tr-county" style="font-weight:500"></span></div>
      <div class="full" style="grid-column:1/-1"><span style="font-size:10px;color:var(--text3);font-weight:600;text-transform:uppercase;display:block;margin-bottom:2px">Order Address</span><span id="tr-address" style="font-weight:500"></span></div>
    </div>

    <!-- SEARCH INFORMATION -->
    <div class="tr-section">
      <div class="tr-sec-title">Search Information</div>
      <div class="tr-grid">
        <div class="ff"><label>Search Date</label><input id="tr-search-date" type="date"></div>
        <div class="ff"><label>Effective Date</label><input id="tr-eff-date" type="date"></div>
        <div class="ff full"><label>Record Owner</label><input id="tr-rec-owner" placeholder="Type here"></div>
        <div class="ff full"><label>Address Searched</label><input id="tr-addr-searched" placeholder="Type here"></div>
      </div>
    </div>

    <!-- ASSESSMENT INFORMATION -->
    <div class="tr-section">
      <div class="tr-sec-title">Assessment Information</div>
      <div class="tr-grid">
        <div class="ff"><label>Land ($)</label><input id="tr-land" placeholder="0.00" type="number" step="0.01"></div>
        <div class="ff"><label>Building ($)</label><input id="tr-building" placeholder="0.00" type="number" step="0.01"></div>
        <div class="ff"><label>Total ($)</label><input id="tr-total" placeholder="0.00" type="number" step="0.01"></div>
        <div class="ff"><label>Parcel No.</label><input id="tr-parcel-assess"></div>
      </div>
    </div>

    <!-- TAXES -->
    <div class="tr-section">
      <div class="tr-sec-title">Taxes</div>
      <div style="background:var(--bg);border-radius:var(--r);padding:12px;margin-bottom:10px">
        <div style="font-size:11px;font-weight:600;color:var(--text2);margin-bottom:8px">Half-Year Tax</div>
        <div class="tr-grid">
          <div class="ff"><label>Tax Year</label><input id="tr-tax1-year" placeholder="2026"></div>
          <div class="ff"><label>Status</label><input id="tr-tax1-status" placeholder="Paid / Unpaid"></div>
          <div class="ff"><label>1st Half Amount</label><input id="tr-tax1-1h" placeholder="Type here"></div>
          <div class="ff"><label>1st Half Due Date</label><input id="tr-tax1-1hd" type="date"></div>
          <div class="ff"><label>2nd Half Amount</label><input id="tr-tax1-2h" placeholder="Type here"></div>
          <div class="ff"><label>2nd Half Due Date</label><input id="tr-tax1-2hd" type="date"></div>
        </div>
      </div>
      <div style="background:var(--bg);border-radius:var(--r);padding:12px;margin-bottom:10px">
        <div style="font-size:11px;font-weight:600;color:var(--text2);margin-bottom:8px">Quarterly Tax</div>
        <div class="tr-grid">
          <div class="ff"><label>Tax Year</label><input id="tr-tax2-year" placeholder="2026"></div>
          <div class="ff"><label>Status</label><input id="tr-tax2-status" placeholder="Paid / Unpaid"></div>
          <div class="ff"><label>1st Quarter Amount</label><input id="tr-tax2-1q" placeholder="Type here"></div>
          <div class="ff"><label>1st Quarter Due Date</label><input id="tr-tax2-1qd" type="date"></div>
          <div class="ff"><label>2nd Quarter Amount</label><input id="tr-tax2-2q" placeholder="Type here"></div>
          <div class="ff"><label>2nd Quarter Due Date</label><input id="tr-tax2-2qd" type="date"></div>
        </div>
      </div>
      <div class="ff"><label>Parcel No. (Tax)</label><input id="tr-tax-parcel" placeholder="Type here"></div>
      <div class="ff" style="margin-top:8px"><label>Comments</label><input id="tr-tax-comments" value="No Prior Year Delinquent taxes found"></div>
    </div>

    <!-- DEED INFORMATION -->
    <div class="tr-section">
      <div class="tr-sec-title">Deed Information</div>
      <div class="tr-grid">
        <div class="ff"><label>Deed Type</label><input id="tr-deed-type" placeholder="Warranty Deed"></div>
        <div class="ff"><label>Consideration ($)</label><input id="tr-deed-consid" placeholder="0.00"></div>
        <div class="ff full"><label>Grantor</label><input id="tr-deed-grantor" placeholder="Type here"></div>
        <div class="ff full"><label>Grantee</label><input id="tr-deed-grantee" placeholder="Type here"></div>
        <div class="ff"><label>Dated Date</label><input id="tr-deed-dated" type="date"></div>
        <div class="ff"><label>Rec Date</label><input id="tr-deed-rec" type="date"></div>
        <div class="ff"><label>Book/Page</label><input id="tr-deed-book" placeholder="Type here"></div>
      </div>
    </div>

    <!-- CHAIN OF TITLE (2 entries) -->
    <div class="tr-section">
      <div class="tr-sec-title">Chain of Title</div>
      <div id="chain-entries">
        <div class="chain-entry" data-idx="0">
          <div style="font-size:11px;font-weight:600;color:var(--text2);margin-bottom:6px;display:flex;align-items:center;justify-content:space-between">
            <span>Entry 1</span>
          </div>
          <div class="tr-grid">
            <div class="ff"><label>Deed Type</label><input class="chain-type" placeholder="Type here"></div>
            <div class="ff"><label>Consideration ($)</label><input class="chain-consid" placeholder="0.00"></div>
            <div class="ff full"><label>Grantor</label><input class="chain-grantor" placeholder="Type here"></div>
            <div class="ff full"><label>Grantee</label><input class="chain-grantee" placeholder="Type here"></div>
            <div class="ff"><label>Dated Date</label><input class="chain-dated" type="date"></div>
            <div class="ff"><label>Rec Date</label><input class="chain-rec" type="date"></div>
            <div class="ff"><label>Book/Page</label><input class="chain-book" placeholder="Type here"></div>
          </div>
        </div>
        <div class="chain-entry" data-idx="1" style="margin-top:10px">
          <div style="font-size:11px;font-weight:600;color:var(--text2);margin-bottom:6px">Entry 2</div>
          <div class="tr-grid">
            <div class="ff"><label>Deed Type</label><input class="chain-type" placeholder="Type here"></div>
            <div class="ff"><label>Consideration ($)</label><input class="chain-consid" placeholder="0.00"></div>
            <div class="ff full"><label>Grantor</label><input class="chain-grantor" placeholder="Type here"></div>
            <div class="ff full"><label>Grantee</label><input class="chain-grantee" placeholder="Type here"></div>
            <div class="ff"><label>Dated Date</label><input class="chain-dated" type="date"></div>
            <div class="ff"><label>Rec Date</label><input class="chain-rec" type="date"></div>
            <div class="ff"><label>Book/Page</label><input class="chain-book" placeholder="Type here"></div>
          </div>
        </div>
      </div>
      <button class="btn btn-sm" style="margin-top:8px" onclick="addChainEntry()">+ Add chain entry</button>
    </div>

    <!-- MORTGAGE INFORMATION -->
    <div class="tr-section">
      <div class="tr-sec-title">Mortgage Information 1</div>
      <div class="tr-grid">
        <div class="ff full"><label>Borrower</label><input id="tr-mtg-borrower" placeholder="Type here"></div>
        <div class="ff full"><label>Lender</label><input id="tr-mtg-lender" placeholder="Type here"></div>
        <div class="ff full"><label>Trustee</label><input id="tr-mtg-trustee" placeholder="Type here"></div>
        <div class="ff full"><label>Instrument Name</label><input id="tr-mtg-instrument" placeholder="Type here"></div>
        <div class="ff"><label>Dated Date</label><input id="tr-mtg-dated" type="date"></div>
        <div class="ff"><label>Rec Date</label><input id="tr-mtg-rec" type="date"></div>
        <div class="ff"><label>Book/Page</label><input id="tr-mtg-book" placeholder="Type here"></div>
        <div class="ff"><label>Amount ($)</label><input id="tr-mtg-amount" placeholder="Type here"></div>
        <div class="ff"><label>Maturity Date</label><input id="tr-mtg-maturity" type="date"></div>
        <div class="ff full"><label>PUD Yes/No</label><input id="tr-mtg-pud" placeholder='This property is a part of a planned unit development known as "XXXXXXXXXXXXXXX"'></div>
      </div>
    </div>

    <!-- ASSIGNMENT INFORMATION 1 -->
    <div class="tr-section">
      <div class="tr-sec-title">Assignment Information 1</div>
      <div class="tr-grid">
        <div class="ff full"><label>Assignor</label><input id="tr-asgn-assignor" placeholder="Type here"></div>
        <div class="ff full"><label>Assignee</label><input id="tr-asgn-assignee" placeholder="Type here"></div>
        <div class="ff"><label>Dated Date</label><input id="tr-asgn-dated" type="date"></div>
        <div class="ff"><label>Rec Date</label><input id="tr-asgn-rec" type="date"></div>
        <div class="ff"><label>Book/Page</label><input id="tr-asgn-book" placeholder="Type here"></div>
      </div>
    </div>

    <!-- EXTRA MORTGAGE SECTIONS -->
    <div id="tr-extra-mtg-container"></div>
    <div style="padding:0 0 10px 0">
      <button class="btn btn-sm" onclick="addExtraMtg()">+ Add Mortgage Section</button>
    </div>

    <!-- EXTRA ASSIGNMENT SECTIONS -->
    <div id="tr-extra-asgn-container"></div>
    <div style="padding:0 0 10px 0">
      <button class="btn btn-sm" onclick="addExtraAsgn()">+ Add Assignment Section</button>
    </div>

    <!-- ADDITIONAL MORTGAGE INFORMATION -->
    <div class="tr-section">
      <div class="tr-sec-title">Additional Mortgage Information <span style="font-size:10px;font-weight:400;color:var(--text3)">(if applicable)</span></div>
      <div class="tr-grid">
        <div class="ff full"><label>Borrower</label><input id="tr-mtg2-borrower" placeholder="Type here"></div>
        <div class="ff full"><label>Lender</label><input id="tr-mtg2-lender" placeholder="Type here"></div>
        <div class="ff full"><label>Trustee</label><input id="tr-mtg2-trustee" placeholder="Type here"></div>
        <div class="ff full"><label>Instrument Name</label><input id="tr-mtg2-instrument" placeholder="Type here"></div>
        <div class="ff"><label>Dated Date</label><input id="tr-mtg2-dated" type="date"></div>
        <div class="ff"><label>Rec Date</label><input id="tr-mtg2-rec" type="date"></div>
        <div class="ff"><label>Book/Page</label><input id="tr-mtg2-book" placeholder="Type here"></div>
        <div class="ff"><label>Amount ($)</label><input id="tr-mtg2-amount" placeholder="Type here"></div>
        <div class="ff"><label>Maturity Date</label><input id="tr-mtg2-maturity" type="date"></div>
      </div>
    </div>

    <!-- ADDITIONAL ASSIGNMENT INFORMATION -->
    <div class="tr-section">
      <div class="tr-sec-title">Additional Assignment Information <span style="font-size:10px;font-weight:400;color:var(--text3)">(if applicable)</span></div>
      <div class="tr-grid">
        <div class="ff full"><label>Assignor</label><input id="tr-asgn2-assignor" placeholder="Type here"></div>
        <div class="ff full"><label>Assignee</label><input id="tr-asgn2-assignee" placeholder="Type here"></div>
        <div class="ff"><label>Dated Date</label><input id="tr-asgn2-dated" type="date"></div>
        <div class="ff"><label>Rec Date</label><input id="tr-asgn2-rec" type="date"></div>
        <div class="ff"><label>Book/Page</label><input id="tr-asgn2-book" placeholder="Type here"></div>
      </div>
    </div>

    <!-- JUDGMENT AND LIEN -->
    <div class="tr-section">
      <div class="tr-sec-title">Judgment and Lien Information</div>
      <div class="ff"><label>Findings</label><textarea id="tr-judgment" rows="3" placeholder="Type here"></textarea></div>
    </div>

    <!-- ADDITIONAL INFORMATION -->
    <div class="tr-section">
      <div class="tr-sec-title">Additional Information</div>
      <div class="ff"><label>Findings</label><textarea id="tr-additional" rows="3" placeholder="Type here"></textarea></div>
    </div>

    <!-- NAMES SEARCHED -->
    <div class="tr-section">
      <div class="tr-sec-title">Names Searched</div>
      <div class="ff"><textarea id="tr-names" rows="3" placeholder="Enter all names searched..."></textarea></div>
    </div>

    <!-- LEGAL DESCRIPTION -->
    <div class="tr-section">
      <div class="tr-sec-title">Legal Description</div>
      <div class="ff" style="margin-bottom:6px"><label>Conveyed To</label><input id="tr-leg-to" placeholder="Grantee name"></div>
      <div class="ff" style="margin-bottom:6px"><label>By (Deed type)</label><input id="tr-leg-deed" placeholder="Special Warranty Deed"></div>
      <div class="ff" style="margin-bottom:6px"><label>From</label><input id="tr-leg-from" placeholder="Grantor name"></div>
      <div class="tr-grid" style="margin-bottom:6px">
        <div class="ff"><label>Dated</label><input id="tr-leg-dated" type="date"></div>
        <div class="ff"><label>Recorded</label><input id="tr-leg-recorded" type="date"></div>
        <div class="ff"><label>Book</label><input id="tr-leg-book" placeholder="Book No."></div>
        <div class="ff"><label>Page</label><input id="tr-leg-page" placeholder="Page No."></div>
      </div>
      <div class="tr-grid">
        <div class="ff"><label>County</label><input id="tr-leg-county" placeholder="County"></div>
        <div class="ff"><label>State</label><input id="tr-leg-state" placeholder="State" maxlength="2"></div>
        <div class="ff"><label>Parcel / Tax ID</label><input id="tr-leg-parcel" placeholder="Type here"></div>
      </div>
    </div>

    <div class="mactions">
      <button class="btn" onclick="closeTR()">Close</button>
      <button class="btn btn-g" onclick="dlTypingReport()">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:13px;height:13px"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
        Download Word Report (.docx)
      </button>
      <button class="btn btn-p" onclick="saveTRAndMarkDone()">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:13px;height:13px"><path d="M19 21H5a2 2 0 01-2-2V5a2 2 0 012-2h11l5 5v11a2 2 0 01-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/></svg>
        Save & Mark Ready for Delivery
      </button>
    </div>
  </div>
</div>

<!-- EDIT MODAL -->
<div class="overlay" id="edit-overlay">
  <div class="mbox">
    <h3 id="edit-title">Edit Order</h3>
    <div class="fg">
      <div class="ff"><label>Company</label>
        <select id="e-co"><option value="YDeal">YDeal Title Services</option><option value="TitlePriority">Title Priority</option></select>
      </div>
      <div class="ff"><label>Order number</label><input id="e-on"></div>
      <div class="ff"><label>Client order #</label><input id="e-cn"></div>
      <div class="ff"><label>Order date</label><input id="e-od" type="date"></div>
      <div class="ff"><label>Due date</label><input id="e-dd" type="datetime-local"></div>
      <div class="ff"><label>Order type</label>
        <select id="e-type">
          <option>Current Owner Search</option><option>Two Owner Search</option><option>Full Search</option>
          <option>Update/Bring Down Search</option><option>Tax Search</option><option>Typing</option>
          <option>Document Retrieval</option><option>Mortgage Search</option>
          <option>Assignment Verification Search</option><option>Deeds and Chains Search</option>
        </select>
      </div>
      <div class="ff"><label>Status</label>
        <select id="e-st"><option>Open Order</option><option>In Progress</option><option>Completed</option><option>Submitted</option><option>Cancelled</option><option>Pending for Documents</option><option>Tax Pending</option><option>Need to Call for Taxes</option><option>Typing Pending</option><option>Abstractor Order</option><option>Quality/Final Review</option></select>
      </div>
      <div class="ff"><label>Assigned to</label>
        <select id="e-ass"><option value="AJ">AJ</option><option value="KM">KM</option><option value="SR">SR</option><option value="TL">TL</option></select>
      </div>
      <div class="ff"><label>Fee ($)</label><input id="e-fee" type="number" step="0.01"></div>
      <div class="ff full"><label>Borrower</label><input id="e-bw"></div>
      <div class="ff full"><label>Property address</label><input id="e-pa"></div>
      <div class="ff"><label>County</label><input id="e-county"></div>
      <div class="ff"><label>State</label><input id="e-state" maxlength="2"></div>
      <div class="ff full"><label>Parcel</label><input id="e-pid"></div>
      <div class="ff full">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:5px">
          <label>Instructions</label>
          <button class="btn btn-sm btn-p" onclick="autoFillEditInst()" id="btn-edit-autofill">
            <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px"><path d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"/></svg>
            Auto-fill ORT
          </button>
        </div>
        <div id="edit-ccrs-panel" style="display:none;margin-bottom:8px">
          <div style="background:var(--blue-l);border:1px solid rgba(27,79,138,.2);border-radius:var(--r);padding:9px 13px;display:flex;align-items:center;gap:8px;flex-wrap:wrap">
            <span style="font-size:11px;font-weight:600;color:var(--blue-t)">CC&RS:</span>
            <button class="btn btn-p btn-sm" onclick="applyEditCCRS(true)">With CC&RS</button>
            <button class="btn btn-sm" onclick="applyEditCCRS(false)">Without CC&RS</button>
          </div>
        </div>
        <textarea id="e-inst" rows="5"></textarea>
      </div>
    </div>
    <div class="mactions">
      <button class="btn" onclick="closeEdit()">Cancel</button>
      <button class="btn btn-p" onclick="saveEdit()">Save changes</button>
    </div>
  </div>
</div>

<!-- SEND / PORTAL MODAL -->
<div class="overlay" id="send-overlay">
  <div class="mbox" style="width:520px">
    <h3 id="send-title">Send / Submit Order</h3>
    <div id="send-body"></div>
    <div class="mactions"><button class="btn" onclick="closeSend()">Close</button></div>
  </div>
</div>

<!-- TYPING PACKAGE MODAL -->
<div class="overlay" id="pkg-overlay">
  <div class="mbox" style="width:680px">
    <h3 id="pkg-modal-title">Typing Package</h3>
    <div id="pkg-modal-order-info" style="background:var(--bg);border-radius:var(--r);padding:10px 14px;margin-bottom:16px;font-size:12px;display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px"></div>
    <div class="sec" style="margin-top:0">Document checklist — assemble in this order</div>
    <div id="pkg-modal-docs"></div>
    <div class="sec">Package notes for Typing team</div>
    <textarea id="pkg-notes" rows="3" style="width:100%" placeholder="Any special instructions for the typing team..."></textarea>
    <div class="mactions">
      <button class="btn" onclick="closePkg()">Close</button>
      <button class="btn btn-g" onclick="dlPackageCoverSheet()">Download Cover Sheet</button>
      <button class="btn btn-p" onclick="sendToTyping()">Mark as Ready for Typing</button>
    </div>
  </div>
</div>

<script>
const COMPANIES = {
  YDeal:        { label:'YDeal Title Services', email:'orders@ydealtitleservices.com',  returnEmail:'', portal:'' },
  TitlePriority:{ label:'Title Priority',       email:'orders@titlepriority.com',        returnEmail:'', portal:'https://ortrisvendor.oldrepublictitle.com/LoginPage.aspx?ReturnUrl=%2fDefault.aspx#b' },
};

const ORDER_TYPES = [
  'Current Owner Search','Two Owner Search','Full Search','Update/Bring Down Search',
  'Tax Search','Typing','Document Retrieval','Mortgage Search',
  'Assignment Verification Search','Deeds and Chains Search'
];

const TEAM = {
  AJ:{name:'Alex J.',bg:'#DBEAFE',tc:'#1E40AF'},
  KM:{name:'Kim M.',bg:'#D1FAE5',tc:'#065F46'},
  SR:{name:'Sara R.',bg:'#FCE7F3',tc:'#9D174D'},
  TL:{name:'Tom L.',bg:'#FEF3C7',tc:'#92400E'}
};

// ── OLD REPUBLIC TITLE / YDEAL INSTRUCTIONS PER PRODUCT TYPE ──────────

const COMMON_BODY = `*****NEED ATTORNEY OPINION LETTER*****
Need copies of pertinent pages on all open mortgages

• If the most recent conveyance is a Quit Claim Deed, Divorce Deed, Affidavit of Heirship:
  - Start the search from when the party originally acquired interest in the property
  - Show the Chain of Title from that date forward.
• 24 Month Chain of Title required.
• Please provide a copy of the lease when our borrower holds a leasehold interest.
• Your report must include accurate and legible Vesting Information with a complete copy of the current Vesting Deed and a legible Legal Description.
• If there are no open mortgages found on the property:
  - Provide a copy of the last release of record even if it is from the previous owner unless:
  - The search is outside of a 10 year search period
  - The current owner acquired the property through foreclosure proceedings or a trustee's sale.
• Tax Info is required as part of search. If there is a fee to obtain taxes, please provide only the tax ID number and contact information for tax authority. ORT will not pay for taxes ordered without written fee approval.`;

const ORT_INSTRUCTIONS = {

'Current Owner Search': {
  hasCCRS: true,
  withCCRS:
`Provide a Current Owner Search from the Current Deed holder forward.
Please provide full copies of all recorded documents found within the scope of the search.
PLEASE PROVIDE CC&RS.
Confirm receipt of order and provide an ETA for completion. If the search will be delayed beyond 48 hours for any reason, call 888.877.9880 to let us know.

${COMMON_BODY}`,

  withoutCCRS:
`Provide a Current Owner Search from the Current Deed holder forward.
Please provide full copies of all recorded documents found within the scope of the search.
Confirm receipt of order and provide an ETA for completion. If the search will be delayed beyond 48 hours for any reason, call 888.877.9880 to let us know.

${COMMON_BODY}`
},

'Two Owner Search': {
  hasCCRS: false,
  text:
`Provide a Two Owner Search covering two (2) complete ownership periods from the current deed holder forward.
Please provide full copies of all recorded documents found within the scope of the search.
PLEASE PROVIDE CC&RS.
Confirm receipt of order and provide an ETA for completion. If the search will be delayed beyond 48 hours for any reason, call 888.877.9880 to let us know.

${COMMON_BODY}`
},

'Full Search': {
  hasCCRS: false,
  text:
`Provide a Full Search for the full statutory search period applicable to the state/county.

If no open mortgage found on the property, provide a copy of the last release of record even if it's from the previous owner unless the current owner acquired the property through foreclosure proceedings or trustee's sale.

Please provide full copies of the following:
• VESTING DEED AND COPIES OF DEED CHAIN
• ANY OUTSALE DEEDS
• OPEN MORTGAGES / DEEDS OF TRUST
• ALL LIENS / JUDGEMENTS
• ANY ASSIGNMENTS
• FINANCING STATEMENTS
• AGREEMENTS / EASEMENTS / RIGHTS OF WAY / PLAT MAP
• A FULL YEAR'S HISTORY OF PROPERTY TAXES
  - DUE / DELINQUENT DATES
  - DELINQUENT TAX INFORMATION
  - ANY AVAILABLE BACK UP DOCUMENTATION FROM THE TAXING AUTHORITY REGARDING TAXES (SCREEN SHOTS ARE ACCEPTABLE)
• DIVORCE DOCUMENTS
  - COPY OF DIVORCE DECREE
  - COPY OF SETTLEMENT STATEMENT
• PROBATE DOCUMENTS
  - COPY OF WILL
  - LETTERS OF ADMINISTRATION / TESTAMENTARY
  - ANY ORDERS AUTHORIZING SALE OR POWER OF SALE
  - NO ESTATE TAX DUE
  - CREDITOR'S CLAIMS
  - DISTRIBUTION
  - CLOSED AND DISCHARGED (IF ESTATE IS CLOSED)
• DO NOT OBTAIN COPIES OF DECLARATIONS AND COVENANTS

IF YOU FIND THAT OUR BORROWER IS NOT IN TITLE, PLEASE CONTACT US BEFORE PROCEEDING UNLESS THE VENDOR INSTRUCTIONS ADVISE THAT IT IS OKAY TO PROCEED.

IF THIS PROPERTY IS LEASEHOLD AND INVOLVES THE BUREAU OF INDIAN AFFAIRS, PLEASE DO NOT PROCEED WITH THIS ORDER. PLEASE NOTIFY US SO THAT WE CAN NOTIFY OUR CUSTOMER.`
},

'Update/Bring Down Search': {
  hasCCRS: false,
  text:
`Provide an Update/Bring Down Search from the date of the prior search to present.
Please provide full copies of all recorded documents found within the scope of the search.
Reference prior search order number on your report.
Confirm receipt of order and provide an ETA for completion. If the search will be delayed beyond 48 hours for any reason, call 888.877.9880 to let us know.

${COMMON_BODY}`
},

'Tax Search': {
  hasCCRS: false,
  text:
`Provide a complete Tax Search including current and prior year taxes.
Include tax ID number, current status (paid/unpaid), amounts due, and due dates.
If there is a fee to obtain taxes, provide only the tax ID number and contact information for the tax authority.
ORT will not pay for taxes ordered without written fee approval.
Confirm receipt of order and provide an ETA for completion. If the search will be delayed beyond 48 hours for any reason, call 888.877.9880 to let us know.`
},

'Typing': {
  hasCCRS: false,
  text:
`Please type the completed title search report and return in the required format.
Ensure all data entered is accurate and legible.
Include all deeds, mortgages, judgments, liens, and other encumbrances found within the scope of the search.
Confirm receipt of order and provide an ETA for completion.`
},

'Document Retrieval': {
  hasCCRS: false,
  text:
`Please retrieve the requested document(s) from the county recorder / register of deeds office.
Provide clear, legible copies of all requested documents.
Include recording information: Book, Page, Instrument Number, and Recording Date.
Confirm receipt of order and provide an ETA for completion. If retrieval will be delayed beyond 48 hours, call 888.877.9880 to let us know.`
},

'Mortgage Search': {
  hasCCRS: false,
  text:
`Provide a complete Mortgage Search for the subject property.
Include all open mortgages, deeds of trust, assignments, and releases of record.
Need copies of pertinent pages on all open mortgages.
Confirm receipt of order and provide an ETA for completion. If the search will be delayed beyond 48 hours for any reason, call 888.877.9880 to let us know.

${COMMON_BODY}`
},

'Assignment Verification Search': {
  hasCCRS: false,
  text:
`Provide a complete Assignment Verification Search for the subject mortgage/deed of trust.
Verify the complete chain of assignments from original lender to current holder.
Include copies of all assignments of record.
Confirm receipt of order and provide an ETA for completion. If the search will be delayed beyond 48 hours for any reason, call 888.877.9880 to let us know.`
},

'Deeds and Chains Search': {
  hasCCRS: false,
  text:
`Provide a complete Deeds and Chain of Title Search for the subject property.
Include all deeds of record from the beginning of the search period to present.
Show the complete chain of title with all conveyances.
Please provide full copies of all recorded deeds found within the scope of the search.
PLEASE PROVIDE CC&RS.
Confirm receipt of order and provide an ETA for completion. If the search will be delayed beyond 48 hours for any reason, call 888.877.9880 to let us know.

*****NEED ATTORNEY OPINION LETTER*****

${COMMON_BODY}`
}

};

function getORTInstructions(orderType, withCCRS, company){
  // Pick the right instructions table based on company
  const table = (company === 'TitlePriority') ? TP_INSTRUCTIONS : ORT_INSTRUCTIONS;
  const inst = table[orderType];
  if(!inst) return '';
  if(inst.hasCCRS) return withCCRS ? inst.withCCRS : inst.withoutCCRS;
  return inst.text || '';
}

function hasCCRSOption(orderType, company){
  const table = (company === 'TitlePriority') ? TP_INSTRUCTIONS : ORT_INSTRUCTIONS;
  return !!(table[orderType] && table[orderType].hasCCRS);
}

// ── TITLE PRIORITY / ORT INSTRUCTIONS PER PRODUCT TYPE ───────────────

const TP_COMMON_BODY = `• If the most recent conveyance is a Quit Claim Deed, Divorce Deed, Affidavit of Heirship:
  - Start the search from when the party originally acquired interest in the property
  - Show the Chain of Title from that date forward.
• 24 Month Chain of Title required.
• Please provide a copy of the lease when our borrower holds a leasehold interest.
• Your report must include accurate and legible Vesting Information with a complete copy of the current Vesting Deed and a legible Legal Description.
• If there are no open mortgages found on the property:
  - Provide a copy of the last release of record even if it is from the previous owner unless:
  - The search is outside of a 10 year search period
  - The current owner acquired the property through foreclosure proceedings or a trustee's sale.
• Tax Info is required as part of search. If there is a fee to obtain taxes, please provide only the tax ID number and contact information for tax authority. ORT will not pay for taxes ordered without written fee approval.`;

const TP_FULL_SEARCH_CHECKLIST = `If no open mortgage found on the property, provide a copy of the last release of record even if it's from the previous owner unless the current owner acquired the property through foreclosure proceedings or trustee's sale.

Please provide full copies of the following:
• VESTING DEED AND COPIES OF DEED CHAIN
• ANY OUTSALE DEEDS
• OPEN MORTGAGES / DEEDS OF TRUST
• ALL LIENS / JUDGEMENTS
• ANY ASSIGNMENTS
• FINANCING STATEMENTS
• AGREEMENTS / EASEMENTS / RIGHTS OF WAY / PLAT MAP
• A FULL YEAR'S HISTORY OF PROPERTY TAXES
  - DUE / DELINQUENT DATES
  - DELINQUENT TAX INFORMATION
  - ANY AVAILABLE BACK UP DOCUMENTATION FROM THE TAXING AUTHORITY REGARDING TAXES (SCREEN SHOTS ARE ACCEPTABLE)
• DIVORCE DOCUMENTS
  - COPY OF DIVORCE DECREE
  - COPY OF SETTLEMENT STATEMENT
• PROBATE DOCUMENTS
  - COPY OF WILL
  - LETTERS OF ADMINISTRATION / TESTAMENTARY
  - ANY ORDERS AUTHORIZING SALE OR POWER OF SALE
  - NO ESTATE TAX DUE
  - CREDITOR'S CLAIMS
  - DISTRIBUTION
  - CLOSED AND DISCHARGED (IF ESTATE IS CLOSED)
• DO NOT OBTAIN COPIES OF DECLARATIONS AND COVENANTS`;

const TP_INSTRUCTIONS = {

'Current Owner Search': {
  hasCCRS: false,
  text:
`Please provide all copies within the search.
Provide a Current Owner Search from the Current Deed holder forward.

${TP_COMMON_BODY}`
},

'Two Owner Search': {
  hasCCRS: false,
  text:
`Please provide all copies within the search.
Provide a Two Owner Search covering two (2) complete ownership periods from the current deed holder forward.

${TP_COMMON_BODY}`
},

'Full Search': {
  hasCCRS: false,
  text:
`Please provide all copies within the search.

${TP_FULL_SEARCH_CHECKLIST}`
},

'Update/Bring Down Search': {
  hasCCRS: false,
  text:
`Please provide all copies within the search.
Provide an Update/Bring Down Search from the date of the prior search to present.
Reference prior search order number on your report.

${TP_COMMON_BODY}`
},

'Tax Search': {
  hasCCRS: false,
  text:
`Please provide all copies within the search.
Provide a complete Tax Search including current and prior year taxes.
Include tax ID number, current status (paid/unpaid), amounts due, and due dates.
If there is a fee to obtain taxes, provide only the tax ID number and contact information for the tax authority.
ORT will not pay for taxes ordered without written fee approval.`
},

'Typing': {
  hasCCRS: false,
  text:
`Please type the completed title search report and return in the required format.
Ensure all data entered is accurate and legible.
Include all deeds, mortgages, judgments, liens, and other encumbrances found within the scope of the search.`
},

'Document Retrieval': {
  hasCCRS: false,
  text:
`Please retrieve the requested document(s) from the county recorder / register of deeds office.
Provide clear, legible copies of all requested documents.
Include recording information: Book, Page, Instrument Number, and Recording Date.`
},

'Mortgage Search': {
  hasCCRS: false,
  text:
`Please provide all copies within the search.
Provide a complete Mortgage Search for the subject property.
Include all open mortgages, deeds of trust, assignments, and releases of record.
Need copies of pertinent pages on all open mortgages.

${TP_COMMON_BODY}`
},

'Assignment Verification Search': {
  hasCCRS: false,
  text:
`Please provide all copies within the search.
Provide a complete Assignment Verification Search for the subject mortgage/deed of trust.
Verify the complete chain of assignments from original lender to current holder.
Include copies of all assignments of record.`
},

'Deeds and Chains Search': {
  hasCCRS: false,
  text:
`Please provide all copies within the search.
Provide a complete Deeds and Chain of Title Search for the subject property.
Include all deeds of record from the beginning of the search period to present.
Show the complete chain of title with all conveyances.

${TP_COMMON_BODY}`
}

};

const TMPL = [
  {key:'company',    label:'Company',          example:'YDeal',                  req:true},
  {key:'orderNum',   label:'Order Number',     example:'01-26027784-03T',         req:true},
  {key:'clientNum',  label:'Client Order #',   example:'CLT-00101',               req:false},
  {key:'orderDate',  label:'Order Date',       example:'2026-04-22',              req:true},
  {key:'dueDate',    label:'Due Date',         example:'2026-04-23 11:33',        req:false},
  {key:'orderType',  label:'Order Type',       example:'Current Owner Search',    req:true},
  {key:'borrower',   label:'Borrower',         example:'REESE LANG',              req:true},
  {key:'address',    label:'Property Address', example:'49 PEBBLE BEACH CIR CHARLES TOWN, WV 25414', req:true},
  {key:'county',     label:'County',           example:'JEFFERSON',               req:true},
  {key:'state',      label:'State',            example:'WV',                      req:true},
  {key:'parcel',     label:'Parcel',           example:'19-02-13A-0328.0000',     req:true},
  {key:'status',     label:'Status',           example:'Open Order',                     req:false},
  {key:'assigned',   label:'Assigned To',      example:'AJ',                      req:false},
  {key:'instructions',label:'Instructions',   example:'Current Owner Search required', req:false},
];

// Load orders from localStorage or start empty
function loadOrders(){
  try {
    const saved = localStorage.getItem('dashboardOrders');
    if(saved){
      const parsed = JSON.parse(saved);
      if(Array.isArray(parsed) && parsed.length){
        // Remove any demo/sample orders that may have been saved previously
        const demoNums = ['01-26027784-03T','TP-2026-00201','01-26027786-02T','TP-2026-00202','01-26027788-03T'];
        const clean = parsed.filter(o => !demoNums.includes(o.orderNum));
        if(clean.length !== parsed.length){
          // Demo orders were found — save cleaned version
          localStorage.setItem('dashboardOrders', JSON.stringify(clean));
        }
        return clean;
      }
    }
  } catch(e){ localStorage.removeItem('dashboardOrders'); }
  return [];
}

function saveOrders(){
  try { localStorage.setItem('dashboardOrders', JSON.stringify(orders)); } catch(e){}
}

// Prevent duplicate orders by orderNum
function isDuplicateOrder(orderNum){
  return orders.some(o => o.orderNum && o.orderNum.trim().toLowerCase() === (orderNum||'').trim().toLowerCase());
}

function addOrderSafe(newOrder){
  if(isDuplicateOrder(newOrder.orderNum)){
    notify('⚠ Order ' + newOrder.orderNum + ' already exists — skipped');
    return false;
  }
  newOrder.sl = orders.length + 1;
  orders.unshift(newOrder);
  orders.forEach((o,i) => o.sl = i+1);
  saveOrders();
  return true;
}

let orders = loadOrders();

let editIdx=null, parsedOrder=null, teamFilter=null, formEditIdx=null, sendIdx=null;
let excelRows=[], excelHeaders=[];

document.getElementById('topbar-date').textContent = new Date().toLocaleDateString('en-US',{weekday:'short',month:'short',day:'numeric',year:'numeric'});

const PT={dashboard:'All Orders',import:'Add Orders',new:'Manual Entry',team:'Team View',typing:'Typing Packages',uploads:'Uploads',onedrive:'OneDrive Setup',qualia:'Qualia API Integration'};
const PS={dashboard:'Title Search Order Management',import:'Import from email, file, or download a template',new:'Create a new title search order',team:'Orders by team member',typing:'Assemble & track document packages for the Typing team',uploads:'Upload and manage package files & typing reports per order',onedrive:'Folder structure & file naming guide for OneDrive storage',qualia:'Connect to Qualia Marketplace — fetch, accept, submit and message orders'};

function go(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.ni').forEach(n=>n.classList.remove('active'));
  const pg=document.getElementById('page-'+id);if(pg)pg.classList.add('active');
  document.getElementById('page-title').textContent=PT[id]||id;
  document.getElementById('page-sub').textContent=PS[id]||'';
  const nis=document.querySelectorAll('.ni');
  const map=['dashboard','import','import','new','uploads','team','typing','','onedrive','qualia'];
  nis.forEach((n,i)=>{if(map[i]===id)n.classList.add('active');});
  if(id==='team')renderTeam();
  if(id==='import')renderTmplCols();
  if(id==='typing')renderTypingPage();
  if(id==='uploads'){renderUploads();}
  if(id==='qualia'){ loadQualiaConfig(); setTimeout(testQualiaConnection, 500); }
  if(id==='onedrive'){ renderODAssignedOrders(); }
}

function setIT(n){
  document.querySelectorAll('.itab').forEach(t=>t.classList.remove('active'));
  document.querySelectorAll('.ipanel').forEach(p=>p.classList.remove('active'));
  document.getElementById('itab-'+n).classList.add('active');
  document.getElementById('ipanel-'+n).classList.add('active');
}

function coBadge(key){
  const map={YDeal:{bg:'#DBEAFE',tc:'#1E40AF',label:'YDeal'},TitlePriority:{bg:'#D1FAE5',tc:'#065F46',label:'Title Priority'}};
  const c=map[key]||{bg:'#eee',tc:'#333',label:key};
  return`<span class="badge" style="background:${c.bg};color:${c.tc}">${c.label}</span>`;
}

function bdg(s){
  const m={
    'Open Order':              'b-new',
    'In Progress':             'b-prog',
    'Completed':               'b-done',
    'Submitted':               'b-submit',
    'Cancelled':               'b-cancel',
    'Pending for Documents':   'b-pend',
    'Tax Pending':             'b-taxpend',
    'Need to Call for Taxes':  'b-taxcall',
    'Typing Pending':          'b-typepend',
    'Abstractor Order':        'b-abstract',
    'Quality/Final Review':    'b-quality',
  };
  return`<span class="badge ${m[s]||'b-new'}">${s}</span>`;
}

function av(k){
  const t=TEAM[k]||{bg:'#E6F1FB',tc:'#0C447C'};
  return`<span class="avatar" style="background:${t.bg};color:${t.tc}" data-tip="${(TEAM[k]||{name:k}).name}">${k}</span>`;
}

function renderMetrics(data){
  const fees=orders.reduce((s,o)=>s+parseFloat(o.fee||0),0);
  document.getElementById('metrics-row').innerHTML=`
    <div class="mc"><div class="ml">Total orders</div><div class="mv">${data.length}</div><div class="ms">All searches</div></div>
    <div class="mc"><div class="ml">Open</div><div class="mv" style="color:var(--blue)">${data.filter(o=>o.status==='Open Order').length}</div><div class="ms">Open orders</div></div>
    <div class="mc"><div class="ml">In progress</div><div class="mv" style="color:var(--amber)">${data.filter(o=>o.status==='In Progress').length}</div><div class="ms">Being worked</div></div>
    <div class="mc"><div class="ml">Completed</div><div class="mv" style="color:var(--green)">${data.filter(o=>o.status==='Completed').length}</div><div class="ms">Delivered</div></div>
    <div class="mc"><div class="ml">Submitted</div><div class="mv" style="color:#0369A1">${data.filter(o=>o.status==='Submitted').length}</div><div class="ms">Sent to client</div></div>
    <div class="mc"><div class="ml">Pending docs</div><div class="mv" style="color:var(--text2)">${data.filter(o=>['Pending for Documents','Tax Pending','Need to Call for Taxes'].includes(o.status)).length}</div><div class="ms">Awaiting info</div></div>
    <div class="mc"><div class="ml">Typing / QC</div><div class="mv" style="color:#6B21A8">${data.filter(o=>['Typing Pending','Quality/Final Review'].includes(o.status)).length}</div><div class="ms">In typing queue</div></div>
    <div class="mc"><div class="ml">Cancelled</div><div class="mv" style="color:var(--red)">${data.filter(o=>o.status==='Cancelled').length}</div><div class="ms">Cancelled orders</div></div>`;
}

function populateStates(){
  const sel=document.getElementById('fState');const cur=sel.value;
  sel.innerHTML='<option value="">All states</option>';
  [...new Set(orders.map(o=>o.state).filter(Boolean))].sort().forEach(s=>{
    const o=document.createElement('option');o.value=s;o.textContent=s;if(s===cur)o.selected=true;sel.appendChild(o);
  });
}

function render(){
  const q=document.getElementById('srch').value.toLowerCase();
  const fCo=document.getElementById('fCo').value;
  const fType=document.getElementById('fType').value;
  const fSt=document.getElementById('fSt').value;
  const fAs=document.getElementById('fAs').value;
  const fSta=document.getElementById('fState').value;
  let data=orders.filter(o=>{
    if(fCo&&o.company!==fCo)return false;
    if(fType&&o.orderType!==fType)return false;
    if(fSt&&o.status!==fSt)return false;
    if(fAs&&o.assigned!==fAs)return false;
    if(fSta&&o.state!==fSta)return false;
    if(q&&![o.orderNum,o.clientNum,o.borrower,o.address,o.parcel,o.county].join(' ').toLowerCase().includes(q))return false;
    return true;
  });
  renderMetrics(data);
  const tb=document.getElementById('tbody');tb.innerHTML='';
  const emptyEl = document.getElementById('empty-state');
  const emptyMsg = document.getElementById('empty-msg');
  emptyEl.style.display = data.length ? 'none' : 'block';
  if(emptyMsg){
    if(orders.length === 0){
      emptyMsg.textContent = 'No orders yet — add your first order using the sidebar';
    } else {
      emptyMsg.textContent = 'No orders match your filters';
    }
  }
  data.forEach(o=>{
    tb.innerHTML+=`<tr>
      <td class="mono" style="color:var(--text3)">${o.sl}</td>
      <td class="mono" style="font-weight:600">${o.orderNum}</td>
      <td>${o.orderDate}</td>
      <td>${coBadge(o.company)}</td>
      <td class="mono" style="font-size:11px">${o.clientNum||'—'}</td>
      <td style="max-width:145px">${o.orderType}</td>
      <td style="font-weight:500">${o.borrower}</td>
      <td style="color:var(--text2)">${o.address}</td>
      <td>${o.county}</td><td>${o.state}</td>
      <td class="mono">${o.parcel}</td>
      <td style="color:var(--text2)">${o.dueDate?o.dueDate.replace('T',' '):'—'}</td>
      <td>${bdg(o.status)}</td>
      <td>${av(o.assigned)}</td>
      <td class="actions-cell"><div class="row-actions" style="flex-wrap:wrap;gap:3px">
        <button class="btn btn-sm" onclick="openEdit(${o.sl-1})" data-tip="Edit order">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px"><path d="M11 4H4a2 2 0 00-2 2v14a2 2 0 002 2h14a2 2 0 002-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 013 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
          Edit
        </button>
        <button class="btn btn-sm" onclick="dlTxt(${o.sl-1})" data-tip="Download Abstract Notes .txt">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
          .txt
        </button>
        <button class="btn btn-sm btn-pu" onclick="openSend(${o.sl-1})" data-tip="Send / Portal">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
          Send
        </button>
        <button class="btn btn-sm btn-a" onclick="openPackage(${o.sl-1})" data-tip="Typing Package">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 21V5a2 2 0 00-2-2h-4a2 2 0 00-2 2v16"/></svg>
          Pkg
        </button>
        <button class="btn btn-sm btn-g" onclick="openTypingReport(${o.sl-1})" data-tip="Typing Report">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/></svg>
          Type
        </button>
        <button class="btn btn-sm" onclick="go('uploads')" data-tip="Upload Files" style="background:var(--purple);color:#fff;border-color:var(--purple)">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
          Upload
        </button>
        <button class="btn btn-sm" onclick="downloadSingleOrderTxt(${o.sl-1})" data-tip="Download order info TXT for folder" style="background:#0E6655;color:#fff;border-color:#0E6655">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px"><path d="M3 15a4 4 0 004 4h9a5 5 0 10-.1-9.999"/></svg>
          Drive
        </button>
      </div></td>
    </tr>`;
  });
}

function clearF(){
  ['srch','fCo','fType','fSt','fAs','fState'].forEach(id=>{
    const el=document.getElementById(id);if(el)el.value='';
  });render();
}

// ── TXT (no client email, no fee) ──
function buildTxt(o){
  const star='*'.repeat(75);
  return `\t\t\t Abstract Notes
${star} 
Type of Search  : ${o.orderType||''}
Order No \t: \t${o.orderNum||''}
Borrower\t: \t${o.borrower||''}
Property\t: \t${o.address||''}
County \t\t: \t${o.county||''}
State \t\t: \t${o.state||''}
Property ID\t: \t${o.parcel||''}
Effective Date \t: ${o.dueDate?o.dueDate.replace('T',' '):''}
Short Legal     : 
${star}
Names Searched :


${star}
Document Type Recorded Date Instrument No Book/Page


${star}
\t\t End of Notes`;
}

function getOrderDate(o){
  // Use order date if available, otherwise today
  const raw = o.orderDate || new Date().toISOString().slice(0,10);
  const d = new Date(raw + 'T00:00:00');
  const mm = String(d.getMonth()+1).padStart(2,'0');
  const dd = String(d.getDate()).padStart(2,'0');
  const yyyy = d.getFullYear();
  return `${mm}-${dd}-${yyyy}`;
}

function getTxtFilename(o){
  const dateStr = getOrderDate(o);
  const orderSafe = o.orderNum.replace(/[^a-zA-Z0-9\-]/g,'_');
  return `${orderSafe}.txt`;
}

function getOneDrivePath(o){
  const dateStr = getOrderDate(o);
  const orderSafe = o.orderNum.replace(/[^a-zA-Z0-9\-]/g,'_');
  return `OneDrive / Title Orders / ${dateStr} / ${orderSafe} / ${orderSafe}.txt`;
}

function dlTxt(idx){
  const o=orders[idx];
  const blob=new Blob([buildTxt(o)],{type:'text/plain'});
  const a=document.createElement('a');a.href=URL.createObjectURL(blob);
  a.download=getTxtFilename(o);a.click();
  notify('✓ Downloaded → Title Orders / '+getOrderDate(o)+' / '+o.orderNum);
}

// ── SEND MODAL ──
function openSend(idx){
  sendIdx=idx;const o=orders[idx];const co=COMPANIES[o.company]||{};
  document.getElementById('send-title').textContent='Send / Submit — '+o.orderNum;
  let html='';

  // EMAIL
  html+=`<div class="send-card"><h4>Send completed Abstract Notes by email</h4>`;
  const returnAddr=co.returnEmail||'';
  if(returnAddr){
    html+=`<p style="font-size:12px;color:var(--text2);margin-bottom:10px">Return address: <span class="mono">${returnAddr}</span></p>
    <div style="display:flex;gap:7px;flex-wrap:wrap">
      <button class="btn btn-p" onclick="sendEmail(${idx})">Open email draft</button>
      <button class="btn" onclick="dlTxt(${idx})">Download .txt to attach</button>
    </div>
    <p style="font-size:11px;color:var(--text3);margin-top:8px">Download the .txt first, then open the email draft and attach it before sending.</p>`;
  } else {
    html+=`<div style="display:flex;gap:7px;flex-wrap:wrap">
      <button class="btn btn-p" onclick="dlTxt(${idx})">Download .txt file</button>
    </div>
    <p style="font-size:11px;color:var(--text3);margin-top:8px">No return email configured for ${co.label||o.company}. Add it in the settings. You can still download and attach the .txt manually.</p>`;
  }
  html+=`</div>`;

  // PORTAL
  html+=`<div class="send-card"><h4>Upload to client portal</h4>`;
  if(co.portal){
    html+=`<a href="${co.portal}" target="_blank" class="portal-btn">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M18 13v6a2 2 0 01-2 2H5a2 2 0 01-2-2V8a2 2 0 012-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
      Open Old Republic Title Vendor Portal
    </a>
    <p style="font-size:11px;color:var(--text3)">Download the .txt above, then log in and upload it to this order in the portal.</p>`;
  } else {
    html+=`<p style="font-size:12px;color:var(--text3)">No portal configured for ${co.label||o.company}.</p>`;
  }
  html+=`</div>`;

  // MARK STATUS
  html+=`<div class="send-card"><h4>Update order status</h4>
    <div style="display:flex;gap:6px;flex-wrap:wrap">
      <button class="btn btn-sm" style="background:#E0F2FE;color:#0369A1;border-color:#BAE6FD" onclick="markSt(${idx},'Submitted');closeSend()">Submitted</button>
      <button class="btn btn-sm btn-g" onclick="markSt(${idx},'Completed');closeSend()">Completed</button>
      <button class="btn btn-sm btn-p" onclick="markSt(${idx},'Quality/Final Review');closeSend()">Quality/Final Review</button>
      <button class="btn btn-sm" style="background:#F3E8FF;color:#6B21A8;border-color:#D8B4FE" onclick="markSt(${idx},'Typing Pending');closeSend()">Typing Pending</button>
      <button class="btn btn-sm btn-r" onclick="markSt(${idx},'Cancelled');closeSend()">Cancelled</button>
    </div>
  </div>`;

  document.getElementById('send-body').innerHTML=html;
  document.getElementById('send-overlay').classList.add('open');
}

function sendEmail(idx){
  const o=orders[idx];const co=COMPANIES[o.company]||{};
  const subj=encodeURIComponent('Completed Order: '+o.orderNum+' — '+o.borrower);
  const body=encodeURIComponent('Dear Team,\n\nPlease find the completed title search attached.\n\nOrder Number        : '+o.orderNum+'\nClient Order Number : '+(o.clientNum||'')+'\nOrder Type          : '+o.orderType+'\nBorrower            : '+o.borrower+'\nProperty Address    : '+o.address+'\nCounty              : '+o.county+', '+o.state+'\nParcel              : '+o.parcel+'\nDue Date            : '+(o.dueDate?o.dueDate.replace('T',' '):'')+'\n\nPlease confirm receipt.\n\nThank you,\nYDeal Title Services');
  const to=co.returnEmail||'';
  window.open('mailto:'+to+'?subject='+subj+'&body='+body);
  notify('Email draft opened');
}

function markSt(idx,st){orders[idx].status=st;saveOrders();render();renderTeam();notify('Marked as: '+st);}
function closeSend(){document.getElementById('send-overlay').classList.remove('open');sendIdx=null;}

// ── FORM ──
// Track CC&RS state
let formCCRS = true;

function autoFill(){
  // When company or order type changes, update CC&RS panel and auto-fill button visibility
  const co    = document.getElementById('f-co').value;
  const type  = document.getElementById('f-type').value;
  const isORT = (co === 'YDeal' || co === 'TitlePriority');
  const panel = document.getElementById('ccrs-panel');
  const btnAF = document.getElementById('btn-autofill-inst');
  const lbl   = document.getElementById('inst-source-label');

  if(isORT && hasCCRSOption(type, co)){
    panel.style.display = 'block';
    btnAF.style.display = 'none';
    lbl.textContent = 'ORT — select CC&RS option above';
  } else if(isORT && (ORT_INSTRUCTIONS[type] || TP_INSTRUCTIONS[type])){
    panel.style.display = 'none';
    btnAF.style.display = 'inline-flex';
    lbl.textContent = (co === 'TitlePriority' ? 'Title Priority' : 'ORT') + ' instructions available';
  } else {
    panel.style.display = 'none';
    btnAF.style.display = 'none';
    lbl.textContent = '';
  }
}

function applyCCRS(withCCRS){
  formCCRS = withCCRS;
  const co   = document.getElementById('f-co').value;
  const type = document.getElementById('f-type').value;
  const inst = getORTInstructions(type, withCCRS, co);
  if(inst) document.getElementById('f-inst').value = inst;
  // Update button styles
  document.getElementById('btn-ccrs-yes').className = withCCRS ? 'btn btn-p btn-sm' : 'btn btn-sm';
  document.getElementById('btn-ccrs-no').className  = withCCRS ? 'btn btn-sm' : 'btn btn-p btn-sm';
  notify(withCCRS ? 'Instructions filled — With CC&RS' : 'Instructions filled — Without CC&RS');
}

function autoFillInst(){
  const co   = document.getElementById('f-co').value;
  const type = document.getElementById('f-type').value;
  const inst = getORTInstructions(type, formCCRS, co);
  if(inst){
    document.getElementById('f-inst').value = inst;
    notify('Instructions auto-filled for: '+type);
  }
}

// Edit modal — auto-fill instructions
function autoFillEditInst(){
  if(editIdx===null) return;
  const o    = orders[editIdx];
  const co   = document.getElementById('e-co')?.value || o.company;
  const type = document.getElementById('e-type')?.value || o.orderType;
  const panel = document.getElementById('edit-ccrs-panel');

  if(hasCCRSOption(type, co)){
    panel.style.display = 'block';
  } else {
    panel.style.display = 'none';
    const inst = getORTInstructions(type, false, co);
    if(inst){ document.getElementById('e-inst').value = inst; notify('Instructions filled for: '+type); }
    else { notify('No template available for: '+type); }
  }
}

function applyEditCCRS(withCCRS){
  const co   = document.getElementById('e-co')?.value || '';
  const type = document.getElementById('e-type')?.value || '';
  const inst = getORTInstructions(type, withCCRS, co);
  if(inst) document.getElementById('e-inst').value = inst;
  document.getElementById('edit-ccrs-panel').style.display = 'none';
  notify(withCCRS ? 'Instructions filled — With CC&RS' : 'Instructions filled — Without CC&RS');
}

function autoFillParsedInst(){
  const coEl   = document.getElementById('pf-company');
  const typeEl = document.getElementById('pf-orderType');
  const instEl = document.getElementById('pf-instructions');
  if(!coEl||!typeEl||!instEl) return;
  const co   = coEl.value;
  const type = typeEl.value;
  const supported = (co==='YDeal'||co==='TitlePriority');
  if(!supported){ notify('Instructions available for YDeal and TitlePriority orders only'); return; }
  if(hasCCRSOption(type, co)){
    if(confirm('Does this order require CC&RS?\n\nClick OK for With CC&RS, Cancel for Without CC&RS')){
      instEl.value = getORTInstructions(type, true, co);
      notify('Instructions filled — With CC&RS');
    } else {
      instEl.value = getORTInstructions(type, false, co);
      notify('Instructions filled — Without CC&RS');
    }
  } else {
    const inst = getORTInstructions(type, false, co);
    if(inst){ instEl.value = inst; notify('Instructions filled for: '+type); }
    else { notify('No template available for: '+type); }
  }
}

// When order type changes in form, update instructions panel
function onTypeChange(){
  autoFill();
  const co   = document.getElementById('f-co').value;
  const type = document.getElementById('f-type').value;
  const hasInst = (co==='YDeal' && ORT_INSTRUCTIONS[type]) || (co==='TitlePriority' && TP_INSTRUCTIONS[type]);
  if(hasInst && !document.getElementById('f-inst').value.trim()){
    if(hasCCRSOption(type, co)){
      applyCCRS(true);
    } else {
      autoFillInst();
    }
  }
}

function collectForm(){
  return{
    sl:formEditIdx!==null?orders[formEditIdx].sl:orders.length+1,
    company:document.getElementById('f-co').value,
    orderNum:document.getElementById('f-on').value||'ORD-'+Date.now(),
    clientNum:document.getElementById('f-cn').value,
    orderDate:document.getElementById('f-od').value||new Date().toISOString().slice(0,10),
    dueDate:document.getElementById('f-dd').value,
    orderType:document.getElementById('f-type').value,
    status:document.getElementById('f-st').value,
    assigned:document.getElementById('f-ass').value,
    fee:document.getElementById('f-fee').value,
    borrower:document.getElementById('f-bw').value||'Unknown',
    address:document.getElementById('f-pa').value,
    county:document.getElementById('f-county').value,
    state:document.getElementById('f-state').value,
    parcel:document.getElementById('f-pid').value,
    instructions:document.getElementById('f-inst').value,
  };
}

function previewTxt(){document.getElementById('txt-prev').textContent=buildTxt(collectForm());}

function saveOrder(){
  if(!document.getElementById('f-on').value.trim()){alert('Please enter an Order Number.');return;}
  const o=collectForm();
  if(formEditIdx!==null){
    orders[formEditIdx]=o;
    saveOrders();
    dlTxt(formEditIdx);
    clearForm();populateStates();render();go('dashboard');notify('Order updated: '+o.orderNum);
  } else {
    if(isDuplicateOrder(o.orderNum)){
      alert('Order number '+o.orderNum+' already exists. Please use a different order number.');
      return;
    }
    o.sl=orders.length+1;
    orders.unshift(o);
    orders.forEach((ord,i)=>ord.sl=i+1);
    saveOrders();
    dlTxt(0);
    clearForm();populateStates();render();go('dashboard');notify('Order saved: '+o.orderNum);
  }
}

function clearForm(){
  formEditIdx=null; formCCRS=true;
  document.getElementById('form-title').textContent='New Title Search Order';
  ['f-on','f-cn','f-bw','f-pa','f-county','f-state','f-pid','f-inst','f-fee','f-od','f-dd'].forEach(id=>{const el=document.getElementById(id);if(el)el.value='';});
  document.getElementById('f-co').value='YDeal';
  document.getElementById('f-type').value='Current Owner Search';
  document.getElementById('f-st').value='Open Order';
  document.getElementById('f-ass').value='AJ';
  document.getElementById('txt-prev').textContent='Fill in the fields above, then click Preview .txt';
  // Reset CC&RS panel
  const cp=document.getElementById('ccrs-panel');if(cp)cp.style.display='none';
  const lbl=document.getElementById('inst-source-label');if(lbl)lbl.textContent='';
  // Trigger autoFill to show correct panels
  setTimeout(autoFill, 50);
}

// ── EDIT ──
function openEdit(idx){
  editIdx=idx;const o=orders[idx];
  document.getElementById('edit-title').textContent='Edit — '+o.orderNum;
  document.getElementById('e-co').value=o.company||'YDeal';
  document.getElementById('e-on').value=o.orderNum;
  document.getElementById('e-cn').value=o.clientNum||'';
  document.getElementById('e-od').value=o.orderDate;
  document.getElementById('e-dd').value=o.dueDate||'';
  document.getElementById('e-type').value=o.orderType;
  document.getElementById('e-st').value=o.status;
  document.getElementById('e-ass').value=o.assigned;
  document.getElementById('e-fee').value=o.fee||'';
  document.getElementById('e-bw').value=o.borrower;
  document.getElementById('e-pa').value=o.address;
  document.getElementById('e-county').value=o.county;
  document.getElementById('e-state').value=o.state;
  document.getElementById('e-pid').value=o.parcel;
  document.getElementById('e-inst').value=o.instructions||'';
  document.getElementById('edit-overlay').classList.add('open');
}
function closeEdit(){document.getElementById('edit-overlay').classList.remove('open');editIdx=null;}
function saveEdit(){
  if(editIdx===null)return;const o=orders[editIdx];
  o.company=document.getElementById('e-co').value;
  o.orderNum=document.getElementById('e-on').value;
  o.clientNum=document.getElementById('e-cn').value;
  o.orderDate=document.getElementById('e-od').value;
  o.dueDate=document.getElementById('e-dd').value;
  o.orderType=document.getElementById('e-type').value;
  o.status=document.getElementById('e-st').value;
  o.assigned=document.getElementById('e-ass').value;
  o.fee=document.getElementById('e-fee').value;
  o.borrower=document.getElementById('e-bw').value;
  o.address=document.getElementById('e-pa').value;
  o.county=document.getElementById('e-county').value;
  o.state=document.getElementById('e-state').value;
  o.parcel=document.getElementById('e-pid').value;
  o.instructions=document.getElementById('e-inst').value;
  closeEdit();saveOrders();render();renderTeam();notify('Updated: '+o.orderNum);
}

// ── EMAIL PARSE ──
function loadSample(){
  document.getElementById('emailText').value=`From: client@titlecompany.com
Subject: New Order - 01-26027790-01T

Order No: 01-26027790-01T
Client Order No: CLT-00210
Order Date: 4/25/2026
Order Type: Current Owner Search
Due Date: 4/28/2026 10:00 AM

Borrower: THOMAS & LISA CRAWFORD
Property Address: 220 FAIRVIEW HEIGHTS DR BUNKER HILL, WV 25413
County: BERKELEY  State: WV
Parcel No: 03-09-014A-0221.0000

Instructions: Provide a Current Owner Search from the Current Deed holder forward. 24 Month Chain of Title required. NEED ATTORNEY OPINION LETTER. Please confirm receipt.`;
}

async function parseEmail(){
  const text=document.getElementById('emailText').value.trim();
  if(!text){alert('Please paste order text first.');return;}
  const st=document.getElementById('parse-status');
  st.style.display='inline-flex';st.className='pst s-info';st.innerHTML='<span class="spinner"></span> Parsing...';
  document.getElementById('parsed-preview').style.display='none';
  try{
    const resp=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',headers:{'Content-Type':'application/json'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1000,
        messages:[{role:'user',content:`Extract these fields from this title search order and return ONLY valid JSON (no markdown, no backticks):
orderNum, clientNum (client order number), orderDate (YYYY-MM-DD), dueDate (YYYY-MM-DDTHH:MM or empty string),
orderType (must be one of: Current Owner Search / Two Owner Search / Full Search / Update/Bring Down Search / Tax Search / Typing / Document Retrieval / Mortgage Search / Assignment Verification Search / Deeds and Chains Search),
borrower, address, county, state (2-letter abbr), parcel, instructions

Text:\n${text}`}]})
    });
    const data=await resp.json();
    const raw=data.content.map(c=>c.text||'').join('');
    const parsed=JSON.parse(raw.replace(/```json|```/g,'').trim());
    parsed.company=document.getElementById('parse-co').value;
    parsedOrder=parsed;
    showParsedPreview(parsed);
    st.className='pst s-ok';st.innerHTML='&#10003; Parsed successfully — review below';
  }catch(e){st.className='pst s-err';st.innerHTML='&#10005; Parse failed — check the text and retry';}
}

function showParsedPreview(p){
  const c=document.getElementById('parsed-fields');
  const flds=[
    ['Company','company',''],['Order number','orderNum',''],['Client order #','clientNum',''],
    ['Order date','orderDate',''],['Due date','dueDate',''],['Order type','orderType','select'],
    ['Borrower','borrower','full'],['Property address','address','full'],
    ['County','county',''],['State','state',''],['Parcel','parcel','full'],
    ['Instructions','instructions','full textarea'],
  ];
  c.innerHTML='';
  flds.forEach(([lbl,key,cls])=>{
    if(key==='instructions') return; // handled separately above
    const isTA=cls.includes('textarea');const isFull=cls.includes('full');const isSel=cls==='select';
    let tag;
    if(key==='instructions'){
      const instHtml=`<div style="margin-bottom:5px;display:flex;align-items:center;justify-content:space-between"><span style="font-size:11px;font-weight:500;color:var(--text2)">Instructions</span><button class="btn btn-sm btn-p" onclick="autoFillParsedInst()" style="font-size:10px">Auto-fill ORT Instructions</button></div><textarea id="pf-instructions" rows="5">${p[key]||''}</textarea>`;
      c.innerHTML+=`<div class="ff full">${instHtml}</div>`;
      return;
    }
    if(key==='company'){
      tag=`<select id="pf-company"><option value="YDeal">YDeal Title Services</option><option value="TitlePriority">Title Priority</option></select>`;
    } else if(key==='orderType'){
      const opts=ORDER_TYPES.map(t=>`<option ${p[key]===t?'selected':''}>${t}</option>`).join('');
      tag=`<select id="pf-orderType">${opts}</select>`;
    } else if(isTA){
      tag=`<textarea id="pf-${key}" rows="3">${p[key]||''}</textarea>`;
    } else {
      tag=`<input id="pf-${key}" value="${(String(p[key]||'')).replace(/"/g,'&quot;')}">`;
    }
    c.innerHTML+=`<div class="ff ${isFull?'full':''}"><label>${lbl}</label>${tag}</div>`;
  });
  setTimeout(()=>{const s=document.getElementById('pf-company');if(s)s.value=p.company||'YDeal';},30);
  document.getElementById('parsed-preview').style.display='block';
}

function saveParsed(){
  if(!parsedOrder)return;
  const keys=['orderNum','clientNum','orderDate','dueDate','orderType','borrower','address','county','state','parcel','instructions'];
  const o={sl:orders.length+1,status:'Open Order',assigned:'AJ',fee:''};
  const coEl=document.getElementById('pf-company');
  o.company=coEl?coEl.value:'YDeal';
  keys.forEach(k=>{const el=document.getElementById('pf-'+k);if(el)o[k]=el.value;});
  if(isDuplicateOrder(o.orderNum)){
    notify('⚠ Order '+o.orderNum+' already exists — not imported');
    return;
  }
  o.sl=orders.length+1;
  orders.unshift(o);
  orders.forEach((ord,i)=>ord.sl=i+1);
  saveOrders();
  dlTxt(0);
  document.getElementById('parsed-preview').style.display='none';
  document.getElementById('emailText').value='';
  document.getElementById('parse-status').style.display='none';
  populateStates();render();go('dashboard');notify('Order imported: '+o.orderNum);
}

// ── EXCEL IMPORT ──
function handleDragOver(e){e.preventDefault();document.getElementById('drop-zone').classList.add('dragover');}
function handleDragLeave(){document.getElementById('drop-zone').classList.remove('dragover');}
function handleDrop(e){e.preventDefault();document.getElementById('drop-zone').classList.remove('dragover');const f=e.dataTransfer.files[0];if(f)readFile(f);}
function handleFileSelect(e){const f=e.target.files[0];if(f)readFile(f);}
function readFile(f){
  const r=new FileReader();
  r.onload=function(e){
    try{
      const wb=f.name.endsWith('.csv')?XLSX.read(e.target.result,{type:'string'}):XLSX.read(e.target.result,{type:'array'});
      const ws=wb.Sheets[wb.SheetNames[0]];
      const data=XLSX.utils.sheet_to_json(ws,{header:1,defval:''});
      if(data.length<2){alert('File appears empty.');return;}
      excelHeaders=data[0].map(h=>String(h).trim());
      excelRows=data.slice(1).filter(r=>r.some(c=>c!==''));
      buildColMap();notify('Loaded '+excelRows.length+' rows');
    }catch(err){alert('Could not read file.');}
  };
  f.name.endsWith('.csv')?r.readAsText(f):r.readAsArrayBuffer(f);
}
function buildColMap(){
  document.getElementById('col-map-section').style.display='block';
  const cm=document.getElementById('col-map');cm.innerHTML='';
  const opts='<option value="">— skip —</option>'+excelHeaders.map((h,i)=>`<option value="${i}">${h}</option>`).join('');
  TMPL.forEach(({key,label,req})=>{
    const auto=excelHeaders.findIndex(h=>h.toLowerCase().replace(/[\s_\-]/g,'').includes(key.toLowerCase().slice(0,5)));
    cm.innerHTML+=`<div class="cmr"><label>${label}${req?' *':''}</label><select id="cm-${key}">${opts}</select></div>`;
    if(auto>=0)setTimeout(()=>{const s=document.getElementById('cm-'+key);if(s)s.value=auto;},40);
  });
}
function getMap(){const m={};TMPL.forEach(({key})=>{const s=document.getElementById('cm-'+key);if(s&&s.value!=='')m[key]=parseInt(s.value);});return m;}
function showExcelPreview(){
  const map=getMap();const cols=Object.keys(map);
  let html='<table style="min-width:unset;width:100%;font-size:11px"><thead><tr>'+cols.map(k=>`<th>${k}</th>`).join('')+'</tr></thead><tbody>';
  excelRows.slice(0,4).forEach(row=>{html+='<tr>'+cols.map(k=>`<td>${row[map[k]]||''}</td>`).join('')+'</tr>';});
  document.getElementById('import-result').style.display='block';
  document.getElementById('import-result').innerHTML=html+'</tbody></table>';
}
function importExcel(){
  const map=getMap();if(!Object.keys(map).length){alert('Map at least one column.');return;}
  let n=0, skipped=0;
  excelRows.forEach(row=>{
    const o={status:'Open Order',assigned:'AJ',company:'YDeal',orderType:'Current Owner Search',fee:''};
    TMPL.forEach(({key})=>{if(map[key]!==undefined)o[key]=String(row[map[key]]||'').trim();});
    if(o.orderNum||o.borrower){
      if(isDuplicateOrder(o.orderNum)){ skipped++; return; }
      o.sl=orders.length+1;
      orders.unshift(o);
      orders.forEach((ord,i)=>ord.sl=i+1);
      n++;
    }
  });
  saveOrders();
  const skipMsg = skipped>0 ? ` (${skipped} duplicate${skipped!==1?'s':''} skipped)` : '';
  document.getElementById('import-result').style.display='block';
  document.getElementById('import-result').innerHTML=`<div class="pst s-ok">&#10003; Imported ${n} order${n!==1?'s':''}${skipMsg}. <button class="btn btn-sm btn-p" style="margin-left:8px" onclick="go('dashboard')">View dashboard</button></div>`;
  populateStates();render();notify('Imported '+n+' orders'+skipMsg);
}
function resetExcel(){excelRows=[];excelHeaders=[];document.getElementById('col-map-section').style.display='none';document.getElementById('import-result').style.display='none';document.getElementById('file-input').value='';}

// ── TEMPLATES ──
function renderTmplCols(){
  const tb=document.getElementById('tmpl-cols');if(!tb)return;
  tb.innerHTML=TMPL.map(({label,example,req})=>`<tr><td class="mono" style="font-weight:500">${label}</td><td style="color:var(--text2)">${example}</td><td>${req?'<span class="badge b-new">Required</span>':'<span style="color:var(--text3);font-size:11px">Optional</span>'}</td></tr>`).join('');
}
function dlTemplate(){
  const h=TMPL.map(c=>c.label);const ex=TMPL.map(c=>c.example);
  const wb=XLSX.utils.book_new();const ws=XLSX.utils.aoa_to_sheet([h,ex]);
  ws['!cols']=TMPL.map(()=>({wch:22}));
  XLSX.utils.book_append_sheet(wb,ws,'Orders Template');XLSX.writeFile(wb,'TitleOrders_Template.xlsx');notify('Template downloaded');
}
function dlCsvTemplate(){
  const h=TMPL.map(c=>c.label).join(',');const ex=TMPL.map(c=>'"'+c.example+'"').join(',');
  const blob=new Blob([h+'\n'+ex],{type:'text/csv'});const a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='TitleOrders_Template.csv';a.click();notify('CSV template downloaded');
}

// ── EXPORT ──
function exportExcel(){
  const h=['SL','Company','Order Number','Order Date','Client Order #','Order Type','Borrower','Property Address','County','State','Parcel','Due Date','Status','Assigned To','Instructions'];
  const rows=orders.map(o=>[o.sl,(COMPANIES[o.company]||{label:o.company}).label,o.orderNum,o.orderDate,o.clientNum||'',o.orderType,o.borrower,o.address,o.county,o.state,o.parcel,o.dueDate?o.dueDate.replace('T',' '):'',o.status,o.assigned,o.instructions]);
  const wb=XLSX.utils.book_new();const ws=XLSX.utils.aoa_to_sheet([h,...rows]);
  ws['!cols']=[5,18,18,11,14,22,24,36,12,6,22,18,12,8,50].map(w=>({wch:w}));
  XLSX.utils.book_append_sheet(wb,ws,'Title Search Orders');XLSX.writeFile(wb,'TitleOrders_'+new Date().toISOString().slice(0,10)+'.xlsx');notify('Excel exported');
}

// ── TEAM ──
function renderTeam(){
  const c=document.getElementById('team-cards');c.innerHTML='';
  Object.entries(TEAM).forEach(([k,t])=>{
    const all=orders.filter(o=>o.assigned===k);const ov=all.filter(o=>o.status==='Cancelled').length;const nw=all.filter(o=>o.status==='Open Order').length;
    const pending=all.filter(o=>['Pending for Documents','Tax Pending','Need to Call for Taxes'].includes(o.status)).length;
    c.innerHTML+=`<div class="tc ${teamFilter===k?'sel':''}" onclick="setTF('${k}')">
      <div class="avl" style="background:${t.bg};color:${t.tc}">${k}</div>
      <div class="tcn">${t.name}</div><div class="tcc">${all.length}</div>
      <div class="tcs">${nw>0?nw+' open &nbsp;':''}${ov>0?`<span class="ovchip">${ov} cancelled</span>`:pending>0?`<span style="color:var(--amber)">${pending} pending</span>`:'<span style="color:var(--green)">&#10003; on track</span>'}</div>
    </div>`;
  });
  renderTeamTable();
}
function setTF(k){teamFilter=teamFilter===k?null:k;renderTeam();}
function clearTF(){teamFilter=null;renderTeam();}
function renderTeamTable(){
  const data=teamFilter?orders.filter(o=>o.assigned===teamFilter):orders;
  document.getElementById('team-label').textContent=teamFilter?`${data.length} order${data.length!==1?'s':''} for ${TEAM[teamFilter].name}`:`All ${data.length} orders`;
  const tb=document.getElementById('team-tbody');tb.innerHTML='';
  document.getElementById('team-empty').style.display=data.length?'none':'block';
  data.forEach(o=>{
    tb.innerHTML+=`<tr>
      <td class="mono" style="color:var(--text3)">${o.sl}</td>
      <td class="mono" style="font-weight:600">${o.orderNum}</td>
      <td>${o.orderDate}</td>
      <td>${coBadge(o.company)}</td>
      <td style="max-width:145px">${o.orderType}</td>
      <td style="font-weight:500">${o.borrower}</td>
      <td style="color:var(--text2)">${o.address}</td>
      <td>${o.county}</td><td>${o.state}</td>
      <td style="color:var(--text2)">${o.dueDate?o.dueDate.replace('T',' '):'—'}</td>
      <td>${bdg(o.status)}</td>
      <td><div class="row-actions">
        <button class="btn btn-sm" onclick="openEdit(${o.sl-1})">Edit</button>
        <button class="btn btn-sm" onclick="dlTxt(${o.sl-1})">DL .txt</button>
      </div></td>
    </tr>`;
  });
}

let notifT;
function notify(msg){const el=document.getElementById('notif');el.textContent=msg;el.classList.add('show');clearTimeout(notifT);notifT=setTimeout(()=>el.classList.remove('show'),3000);}

// ── TYPING PACKAGE ──
const PKG_DOCS = [
  { id:'plat',      num:1, name:'Plat Map or GIS Map',          hint:'Include recorded plat or county GIS map' },
  { id:'assessor',  num:2, name:'Assessor',                      hint:'Assessor/property record card' },
  { id:'taxes',     num:3, name:'Taxes',                         hint:'Current & prior year tax records' },
  { id:'deeds',     num:4, name:'Deeds and Back Chains',         hint:'All deeds within chain of title' },
  { id:'mortgage',  num:5, name:'Mortgage and Related Documents',hint:'Open mortgages, assignments, releases' },
  { id:'judgments', num:6, name:'Judgments',                     hint:'Judgment liens, UCC filings' },
  { id:'pacer',     num:7, name:'Pacer and Patriot',             hint:'Federal court & OFAC/Patriot check' },
];

// Store package state per order: packages[orderNum] = { checked:{}, files:{}, notes:'' }
let packages = {};
let pkgIdx = null;

function getPkg(orderNum){
  if(!packages[orderNum]) packages[orderNum] = { checked:{}, files:{}, notes:'' };
  return packages[orderNum];
}

function pkgProgress(orderNum){
  const p = getPkg(orderNum);
  return PKG_DOCS.filter(d => p.checked[d.id]).length;
}

function renderTypingPage(){
  const filter = document.getElementById('pkg-filter').value;
  // Show all orders or filtered by status
  let data = filter ? orders.filter(o => o.status === filter) : orders;
  const grid = document.getElementById('pkg-grid');
  const empty = document.getElementById('pkg-empty');
  grid.innerHTML = '';
  if(!data.length){ empty.style.display='block'; return; }
  empty.style.display='none';

  data.forEach(o => {
    const p = getPkg(o.orderNum);
    const done = pkgProgress(o.orderNum);
    const pct = Math.round((done/PKG_DOCS.length)*100);
    const allDone = done === PKG_DOCS.length;

    let docsHTML = PKG_DOCS.map(d => {
      const isChecked = !!p.checked[d.id];
      const hasFile = !!(p.files[d.id] && p.files[d.id].length);
      return `<div class="doc-row">
        <div class="doc-num">${d.num}</div>
        <div class="doc-info">
          <div class="doc-name">${d.name}</div>
          <div class="doc-sub">${hasFile ? '📎 '+p.files[d.id].map(f=>f.name).join(', ') : d.hint}</div>
        </div>
        <div class="doc-check ${isChecked?'checked':''}" onclick="toggleDocCheck('${o.orderNum}','${d.id}',this)" data-ordernum="${o.orderNum}" data-docid="${d.id}">
          <svg fill="none" stroke="currentColor" stroke-width="3" viewBox="0 0 24 24"><polyline points="20 6 9 17 4 12"/></svg>
        </div>
      </div>`;
    }).join('');

    grid.innerHTML += `<div class="pkg-card">
      <div class="pkg-card-head">
        <div>
          <h4>${o.orderNum}</h4>
          <div style="font-size:11px;color:var(--text3);margin-top:2px">${o.borrower} · ${o.county}, ${o.state}</div>
        </div>
        <div style="display:flex;align-items:center;gap:6px;flex-shrink:0">
          ${bdg(o.status)}
        </div>
      </div>
      <div class="pkg-card-body">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:6px">
          <span style="font-size:11px;color:var(--text2);font-weight:500">${done}/${PKG_DOCS.length} documents</span>
          <span style="font-size:11px;color:${allDone?'var(--green)':'var(--text3)'};font-weight:600">${pct}%</span>
        </div>
        <div class="pkg-progress"><div class="pkg-progress-fill" style="width:${pct}%"></div></div>
        ${docsHTML}
      </div>
      <div class="pkg-actions">
        <button class="btn btn-sm btn-p" onclick="openPackage(${o.sl-1})">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:12px;height:12px"><path d="M11 4H4a2 2 0 00-2 2v14a2 2 0 002 2h14a2 2 0 002-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 013 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
          Manage Package
        </button>
        <button class="btn btn-sm btn-g" onclick="openTypingReport(${o.sl-1})">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:12px;height:12px"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>
          Typing Report
        </button>
        <button class="btn btn-sm btn-g" onclick="pkgIdx=orders.findIndex(x=>x.orderNum==='${o.orderNum}');dlPackageCoverSheet()" style="${allDone?'':'opacity:.5;cursor:not-allowed'}" ${allDone?'':'disabled'}>
          Download Cover Sheet
        </button>
        ${allDone ? `<button class="btn btn-sm btn-a" onclick="sendToTypingDirect('${o.orderNum}')">Send to Typing</button>` : ''}
      </div>
    </div>`;
  });
}

function toggleDocCheck(orderNum, docId, el){
  const p = getPkg(orderNum);
  p.checked[docId] = !p.checked[docId];
  el.classList.toggle('checked');
  renderTypingPage();
  // also refresh modal if open
  if(pkgIdx !== null && orders[pkgIdx] && orders[pkgIdx].orderNum === orderNum) refreshPkgModal();
}

function openPackage(idx){
  pkgIdx = idx;
  const o = orders[idx];
  const p = getPkg(o.orderNum);
  document.getElementById('pkg-modal-title').textContent = 'Typing Package — ' + o.orderNum;
  document.getElementById('pkg-notes').value = p.notes || '';

  // Order info summary
  document.getElementById('pkg-modal-order-info').innerHTML = `
    <div><div style="font-size:10px;color:var(--text3);text-transform:uppercase;font-weight:600;margin-bottom:2px">Order Type</div><div style="font-weight:500">${o.orderType}</div></div>
    <div><div style="font-size:10px;color:var(--text3);text-transform:uppercase;font-weight:600;margin-bottom:2px">Borrower</div><div style="font-weight:500">${o.borrower}</div></div>
    <div><div style="font-size:10px;color:var(--text3);text-transform:uppercase;font-weight:600;margin-bottom:2px">Property</div><div style="font-weight:500">${o.address}</div></div>
    <div><div style="font-size:10px;color:var(--text3);text-transform:uppercase;font-weight:600;margin-bottom:2px">County / State</div><div style="font-weight:500">${o.county}, ${o.state}</div></div>
    <div><div style="font-size:10px;color:var(--text3);text-transform:uppercase;font-weight:600;margin-bottom:2px">Parcel</div><div style="font-weight:500;font-family:'DM Mono',monospace;font-size:11px">${o.parcel}</div></div>
    <div><div style="font-size:10px;color:var(--text3);text-transform:uppercase;font-weight:600;margin-bottom:2px">Company</div><div style="font-weight:500">${(COMPANIES[o.company]||{label:o.company}).label}</div></div>`;

  refreshPkgModal();
  document.getElementById('pkg-overlay').classList.add('open');
}

function refreshPkgModal(){
  if(pkgIdx === null) return;
  const o = orders[pkgIdx];
  const p = getPkg(o.orderNum);
  const container = document.getElementById('pkg-modal-docs');
  container.innerHTML = PKG_DOCS.map(d => {
    const isChecked = !!p.checked[d.id];
    const fileList = p.files[d.id] || [];
    const hasFiles = fileList.length > 0;
    return `<div class="pkg-modal-doc">
      <div class="pkg-modal-num">${d.num}</div>
      <div class="pkg-modal-info">
        <div class="pkg-modal-name">${d.name}</div>
        <div style="font-size:11px;color:var(--text3)">${d.hint}</div>
        ${hasFiles ? `<div class="pkg-modal-files">📎 ${fileList.map(f=>`<span style="background:var(--green-l);color:var(--green);padding:1px 6px;border-radius:4px;margin-right:4px;font-size:10px">${f.name}</span>`).join('')}</div>` : ''}
        <div class="pkg-modal-upload">
          <input type="file" id="file-${d.id}" multiple style="display:none" onchange="handlePkgFile('${o.orderNum}','${d.id}',this)">
          <button class="doc-upload ${hasFiles?'has-file':''}" onclick="document.getElementById('file-${d.id}').click()">
            ${hasFiles ? '✓ '+fileList.length+' file(s) — add more' : '+ Attach file(s)'}
          </button>
          ${hasFiles ? `<button class="doc-upload" onclick="clearPkgFiles('${o.orderNum}','${d.id}')" style="color:var(--red)">✕ Clear</button>` : ''}
        </div>
      </div>
      <div class="doc-check ${isChecked?'checked':''}" onclick="toggleDocCheck('${o.orderNum}','${d.id}',this)" style="margin-top:4px">
        <svg fill="none" stroke="currentColor" stroke-width="3" viewBox="0 0 24 24"><polyline points="20 6 9 17 4 12"/></svg>
      </div>
    </div>`;
  }).join('');
}

function handlePkgFile(orderNum, docId, input){
  const p = getPkg(orderNum);
  if(!p.files[docId]) p.files[docId] = [];
  Array.from(input.files).forEach(f => p.files[docId].push({name:f.name, size:f.size}));
  p.checked[docId] = true; // auto-check when file attached
  refreshPkgModal();
  renderTypingPage();
}

function clearPkgFiles(orderNum, docId){
  const p = getPkg(orderNum);
  p.files[docId] = [];
  refreshPkgModal();
  renderTypingPage();
}

function savePkgNotes(){
  if(pkgIdx === null) return;
  const o = orders[pkgIdx];
  const p = getPkg(o.orderNum);
  p.notes = document.getElementById('pkg-notes').value;
}

function buildCoverSheet(o){
  const p = getPkg(o.orderNum);
  const co = COMPANIES[o.company]||{label:o.company};
  const star = '*'.repeat(65);
  const done = pkgProgress(o.orderNum);
  let docLines = PKG_DOCS.map(d => {
    const chk = p.checked[d.id] ? '[X]' : '[ ]';
    const files = (p.files[d.id]||[]).map(f=>f.name).join(', ');
    return `  ${chk} ${d.num}. ${d.name}${files?' — '+files:''}`;
  }).join('\n');
  return `${star}
  TYPING PACKAGE COVER SHEET
  ${co.label}
${star}
Order Number        : ${o.orderNum}
Client Order #      : ${o.clientNum||''}
Order Type          : ${o.orderType}
Borrower            : ${o.borrower}
Property Address    : ${o.address}
County              : ${o.county}
State               : ${o.state}
Parcel              : ${o.parcel}
Due Date            : ${o.dueDate?o.dueDate.replace('T',' '):''}
Assigned To         : ${o.assigned} — ${(TEAM[o.assigned]||{name:o.assigned}).name}
${star}
DOCUMENT PACKAGE — ${done}/${PKG_DOCS.length} COMPLETED
${star}
${docLines}
${star}
TYPING TEAM NOTES:
${p.notes||'No special instructions.'}
${star}
Package Generated   : ${new Date().toLocaleString()}
${star}`;
}

function dlPackageCoverSheet(){
  savePkgNotes();
  if(pkgIdx === null) return;
  const o = orders[pkgIdx];
  const blob = new Blob([buildCoverSheet(o)], {type:'text/plain'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = o.orderNum.replace(/[^a-zA-Z0-9\-]/g,'_')+'_Package_'+getOrderDate(o)+'.txt';
  a.click();
  notify('Cover sheet downloaded: '+o.orderNum);
}

function sendToTyping(){
  savePkgNotes();
  if(pkgIdx === null) return;
  const o = orders[pkgIdx];
  dlPackageCoverSheet();
  o.status = 'Typing Pending';
  closePkg();
  render();
  renderTypingPage();
  notify('Package sent to Typing: '+o.orderNum);
}

function sendToTypingDirect(orderNum){
  const idx = orders.findIndex(o => o.orderNum === orderNum);
  if(idx < 0) return;
  orders[idx].status = 'Typing In Progress';
  render();
  renderTypingPage();
  notify('Sent to Typing: '+orderNum);
}

function closePkg(){
  savePkgNotes();
  document.getElementById('pkg-overlay').classList.remove('open');
  pkgIdx = null;
}

// ── NAVIGATION UPDATE to include typing ──
const _go_original = go;

// Override go to also handle typing page
const _go = function(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.ni').forEach(n=>n.classList.remove('active'));
  const pg = document.getElementById('page-'+id);
  if(pg) pg.classList.add('active');
  document.getElementById('page-title').textContent = PT[id]||id;
  document.getElementById('page-sub').textContent = PS[id]||'';
  const nis = document.querySelectorAll('.ni');
  const map = ['dashboard','import','import','new','team','typing',''];
  nis.forEach((n,i)=>{if(map[i]===id)n.classList.add('active');});
  if(id==='team') renderTeam();
  if(id==='import') renderTmplCols();
  if(id==='typing') renderTypingPage();
};

// ── TYPING REPORT ──
let trIdx = null;
// Store typing report data per order
let typingReports = {};

function getTR(orderNum){
  if(!typingReports[orderNum]) typingReports[orderNum] = {};
  return typingReports[orderNum];
}

function openTypingReport(idx){
  trIdx = idx;
  const o = orders[idx];
  const co = COMPANIES[o.company]||{label:o.company};

  // Header info
  document.getElementById('tr-title').textContent = 'Typing Report — ' + o.orderNum;
  document.getElementById('tr-co-badge').innerHTML = coBadge(o.company);
  document.getElementById('tr-co-name').textContent = co.label;
  document.getElementById('tr-co-label').textContent = co.label;
  document.getElementById('tr-ordernum').textContent = o.orderNum;
  document.getElementById('tr-product').textContent = o.orderType;
  document.getElementById('tr-county').textContent = o.county + ', ' + o.state;
  document.getElementById('tr-address').textContent = o.address;

  // Pre-fill from order data
  const today = new Date().toISOString().slice(0,10);
  const tr = getTR(o.orderNum);

  // Search info
  document.getElementById('tr-search-date').value    = tr['search-date']    || today;
  document.getElementById('tr-eff-date').value        = tr['eff-date']        || (o.dueDate ? o.dueDate.slice(0,10) : '');
  document.getElementById('tr-rec-owner').value       = tr['rec-owner']       || o.borrower || '';
  document.getElementById('tr-addr-searched').value   = tr['addr-searched']   || o.address  || '';

  // Assessment
  document.getElementById('tr-land').value            = tr['land']            || '';
  document.getElementById('tr-building').value        = tr['building']        || '';
  document.getElementById('tr-total').value           = tr['total']           || '';
  document.getElementById('tr-parcel-assess').value   = tr['parcel-assess']   || o.parcel   || '';

  // Tax
  document.getElementById('tr-tax1-year').value       = tr['tax1-year']       || new Date().getFullYear();
  document.getElementById('tr-tax1-status').value     = tr['tax1-status']     || '';
  document.getElementById('tr-tax1-1h').value         = tr['tax1-1h']         || '';
  document.getElementById('tr-tax1-1hd').value        = tr['tax1-1hd']        || '';
  document.getElementById('tr-tax1-2h').value         = tr['tax1-2h']         || '';
  document.getElementById('tr-tax1-2hd').value        = tr['tax1-2hd']        || '';
  document.getElementById('tr-tax2-year').value       = tr['tax2-year']       || new Date().getFullYear();
  document.getElementById('tr-tax2-status').value     = tr['tax2-status']     || '';
  document.getElementById('tr-tax2-1q').value         = tr['tax2-1q']         || '';
  document.getElementById('tr-tax2-1qd').value        = tr['tax2-1qd']        || '';
  document.getElementById('tr-tax2-2q').value         = tr['tax2-2q']         || '';
  document.getElementById('tr-tax2-2qd').value        = tr['tax2-2qd']        || '';
  document.getElementById('tr-tax-parcel').value      = tr['tax-parcel']      || o.parcel   || '';
  document.getElementById('tr-tax-comments').value    = tr['tax-comments']    || 'No Prior Year Delinquent taxes found';

  // Deed
  document.getElementById('tr-deed-type').value       = tr['deed-type']       || '';
  document.getElementById('tr-deed-consid').value     = tr['deed-consid']     || '0.00';
  document.getElementById('tr-deed-grantor').value    = tr['deed-grantor']    || '';
  document.getElementById('tr-deed-grantee').value    = tr['deed-grantee']    || o.borrower || '';
  document.getElementById('tr-deed-dated').value      = tr['deed-dated']      || '';
  document.getElementById('tr-deed-rec').value        = tr['deed-rec']        || '';
  document.getElementById('tr-deed-book').value       = tr['deed-book']       || '';

  // Mortgage
  document.getElementById('tr-mtg-borrower').value    = tr['mtg-borrower']    || o.borrower || '';
  document.getElementById('tr-mtg-lender').value      = tr['mtg-lender']      || '';
  document.getElementById('tr-mtg-trustee').value     = tr['mtg-trustee']     || '';
  document.getElementById('tr-mtg-instrument').value  = tr['mtg-instrument']  || '';
  document.getElementById('tr-mtg-dated').value       = tr['mtg-dated']       || '';
  document.getElementById('tr-mtg-rec').value         = tr['mtg-rec']         || '';
  document.getElementById('tr-mtg-book').value        = tr['mtg-book']        || '';
  document.getElementById('tr-mtg-amount').value      = tr['mtg-amount']      || '';
  document.getElementById('tr-mtg-maturity').value    = tr['mtg-maturity']    || '';
  document.getElementById('tr-mtg-pud').value         = tr['mtg-pud']         || '';

  // Assignment
  document.getElementById('tr-asgn-assignor').value   = tr['asgn-assignor']   || '';
  document.getElementById('tr-asgn-assignee').value   = tr['asgn-assignee']   || '';
  document.getElementById('tr-asgn-dated').value      = tr['asgn-dated']      || '';
  document.getElementById('tr-asgn-rec').value        = tr['asgn-rec']        || '';
  document.getElementById('tr-asgn-book').value       = tr['asgn-book']       || '';

  // Judgment / Additional
  document.getElementById('tr-judgment').value        = tr['judgment']        || '';
  document.getElementById('tr-additional').value      = tr['additional']      || '';
  document.getElementById('tr-names').value           = tr['names']           || o.borrower || '';

  // Legal
  document.getElementById('tr-leg-to').value          = tr['leg-to']          || o.borrower || '';
  document.getElementById('tr-leg-deed').value        = tr['leg-deed']        || 'Special Warranty Deed';
  document.getElementById('tr-leg-from').value        = tr['leg-from']        || '';
  document.getElementById('tr-leg-dated').value       = tr['leg-dated']       || '';
  document.getElementById('tr-leg-recorded').value    = tr['leg-recorded']    || '';
  document.getElementById('tr-leg-book').value        = tr['leg-book']        || '';
  document.getElementById('tr-leg-page').value        = tr['leg-page']        || '';
  document.getElementById('tr-leg-county').value      = tr['leg-county']      || o.county   || '';
  document.getElementById('tr-leg-state').value       = tr['leg-state']       || o.state    || '';
  document.getElementById('tr-leg-parcel').value      = tr['leg-parcel']      || o.parcel   || '';

  // Chain entries
  resetChainEntries(tr['chain'] || []);

  document.getElementById('tr-overlay').classList.add('open');
}

function resetChainEntries(saved){
  const container = document.getElementById('chain-entries');
  // Keep 2 base entries, restore saved values
  const entries = container.querySelectorAll('.chain-entry');
  entries.forEach((entry, i) => {
    const d = saved[i] || {};
    entry.querySelector('.chain-type').value    = d.type    || '';
    entry.querySelector('.chain-consid').value  = d.consid  || '0.00';
    entry.querySelector('.chain-grantor').value = d.grantor || '';
    entry.querySelector('.chain-grantee').value = d.grantee || '';
    entry.querySelector('.chain-dated').value   = d.dated   || '';
    entry.querySelector('.chain-rec').value     = d.rec     || '';
    entry.querySelector('.chain-book').value    = d.book    || '';
  });
}

function addChainEntry(){
  const container = document.getElementById('chain-entries');
  const idx = container.querySelectorAll('.chain-entry').length;
  const div = document.createElement('div');
  div.className = 'chain-entry';
  div.setAttribute('data-idx', idx);
  div.style.marginTop = '10px';
  div.innerHTML = `<div style="font-size:11px;font-weight:600;color:var(--text2);margin-bottom:6px;display:flex;align-items:center;justify-content:space-between">
    <span>Entry ${idx+1}</span>
    <button class="btn btn-sm btn-r" onclick="this.closest('.chain-entry').remove()" style="padding:2px 7px;font-size:10px">Remove</button>
  </div>
  <div class="tr-grid">
    <div class="ff"><label>Deed Type</label><input class="chain-type" placeholder="Type here"></div>
    <div class="ff"><label>Consideration ($)</label><input class="chain-consid" placeholder="0.00"></div>
    <div class="ff full"><label>Grantor</label><input class="chain-grantor" placeholder="Type here"></div>
    <div class="ff full"><label>Grantee</label><input class="chain-grantee" placeholder="Type here"></div>
    <div class="ff"><label>Dated Date</label><input class="chain-dated" type="date"></div>
    <div class="ff"><label>Rec Date</label><input class="chain-rec" type="date"></div>
    <div class="ff"><label>Book/Page</label><input class="chain-book" placeholder="Type here"></div>
  </div>`;
  container.appendChild(div);
}

function collectChain(){
  const entries = document.querySelectorAll('.chain-entry');
  return Array.from(entries).map(e => ({
    type:    e.querySelector('.chain-type').value,
    consid:  e.querySelector('.chain-consid').value,
    grantor: e.querySelector('.chain-grantor').value,
    grantee: e.querySelector('.chain-grantee').value,
    dated:   e.querySelector('.chain-dated').value,
    rec:     e.querySelector('.chain-rec').value,
    book:    e.querySelector('.chain-book').value,
  }));
}

function saveTRData(){
  if(trIdx === null) return;
  const o = orders[trIdx];
  const tr = getTR(o.orderNum);
  const ids = ['search-date','eff-date','rec-owner','addr-searched',
    'land','building','total','parcel-assess',
    'tax1-year','tax1-status','tax1-1h','tax1-1hd','tax1-2h','tax1-2hd',
    'tax2-year','tax2-status','tax2-1q','tax2-1qd','tax2-2q','tax2-2qd',
    'tax-parcel','tax-comments',
    'deed-type','deed-consid','deed-grantor','deed-grantee','deed-dated','deed-rec','deed-book',
    'mtg-borrower','mtg-lender','mtg-trustee','mtg-instrument','mtg-dated','mtg-rec','mtg-book','mtg-amount','mtg-maturity','mtg-pud',
    'asgn-assignor','asgn-assignee','asgn-dated','asgn-rec','asgn-book',
    'mtg2-borrower','mtg2-lender','mtg2-trustee','mtg2-instrument','mtg2-dated','mtg2-rec','mtg2-book','mtg2-amount','mtg2-maturity',
    'asgn2-assignor','asgn2-assignee','asgn2-dated','asgn2-rec','asgn2-book',
    'judgment','additional','names',
    'leg-to','leg-deed','leg-from','leg-dated','leg-recorded','leg-book','leg-page','leg-county','leg-state','leg-parcel'];
  ids.forEach(id => { const el = document.getElementById('tr-'+id); if(el) tr[id] = el.value; });
  tr['chain'] = collectChain();
}

function fmtDate(val){ if(!val) return 'Type here'; const d=new Date(val+'T00:00:00'); return isNaN(d)?val:d.toLocaleDateString('en-US'); }
function fv(id){ const el=document.getElementById('tr-'+id); return el&&el.value?el.value:'Type here'; }

function buildTypingReport(){
  if(trIdx===null) return '';
  const o = orders[trIdx];
  const co = COMPANIES[o.company]||{label:o.company};
  const chain = collectChain();

  // Build chain of title block — matches exact template format
  let chainBlock = '';
  chain.forEach((c) => {
    chainBlock += `\nDEED TYPE:\t\t\t${c.type||'Type here'}\t\nCONSIDERATION: \t\t$${c.consid||'0.00'}\nGRANTOR:  \t\t\t${c.grantor||'Type here'}\nGRANTEE:  \t\t\t${c.grantee||'Type here'}\nDATED DATE:\t\t\t${fmtDate(c.dated)} \nREC DATE:  \t\t\t${fmtDate(c.rec)}\nBOOK/PAGE:\t\t\t${c.book||'Type here'}\n`;
  });

  // Exact output matching both TitlePriority and YDeal template format
  return `ORDER NUMBER:\t\t${o.orderNum}

PRODUCT NAME: \t\t${o.orderType}

ORDER ADDRESS: \t\t${o.address}

COUNTY:\t\t\t${o.county}

SEARCH INFORMATION

SEARCH DATE:\t\t\t${fmtDate(fv('search-date'))}

EFFECTIVE DATE:\t\t${fmtDate(fv('eff-date'))}

RECORD OWNER:\t\t${fv('rec-owner')}

ADDRESS SEARCHED:\t\t${fv('addr-searched')}

ASSESSMENT INFORMATION

LAND: \t\t\t\t$${fv('land')||''}

BUILDING: \t\t\t$${fv('building')||''}

TOTAL:\t\t\t\t$${fv('total')||''}

\tPARCEL NO.:     \t${fv('parcel-assess')}

TAXES

TAX YEAR:\t\t\t${fv('tax1-year')}

STATUS:\t\t\t${fv('tax1-status')}

1st HALF AMOUNT:\t\t${fv('tax1-1h')}

DUE DATE:\t\t\t${fmtDate(fv('tax1-1hd'))}

2nd HALF AMOUNT:\t\t${fv('tax1-2h')}

DUE DATE: \t\t\t${fmtDate(fv('tax1-2hd'))}

TAX YEAR:\t\t\t${fv('tax2-year')}

STATUS:\t\t\t${fv('tax2-status')}

1st QUARTER AMOUNT:\t\t${fv('tax2-1q')}

DUE DATE:\t\t\t${fmtDate(fv('tax2-1qd'))}

2nd QUARTER AMOUNT:\t\t${fv('tax2-2q')}

DUE DATE: \t\t\t${fmtDate(fv('tax2-2qd'))}

\tPARCEL NO.:     \t${fv('tax-parcel')}

COMMENTS:\t\t\t${fv('tax-comments')||'No Prior Year Delinquent taxes found'}

DEED INFORMATION

DEED TYPE:\t\t\t${fv('deed-type')}

CONSIDERATION: \t\t$${fv('deed-consid')||'0.00'}

GRANTOR:  \t\t\t${fv('deed-grantor')}

GRANTEE:  \t\t\t${fv('deed-grantee')}

DATED DATE:\t\t\t${fmtDate(fv('deed-dated'))}

REC DATE:\t\t\t${fmtDate(fv('deed-rec'))}

BOOK/PAGE:\t\t\t${fv('deed-book')}

CHAIN OF TITLE
${chainBlock}
MORTGAGE INFORMATION

BORROWER:\t\t\t${fv('mtg-borrower')}

LENDER:  \t${fv('mtg-lender')}

TRUSTEE:\t${fv('mtg-trustee')}

INSTRUMENT NAME:  \t${fv('mtg-instrument')}

DATED DATE:\t\t\t${fmtDate(fv('mtg-dated'))}

REC DATE:  \t\t\t${fmtDate(fv('mtg-rec'))}

BOOK/PAGE:\t\t\t${fv('mtg-book')}

AMOUNT:\t\t\t${fv('mtg-amount')}

MATURITY DATE:\t\t${fmtDate(fv('mtg-maturity'))}

PUD YES/NO:\t${fv('mtg-pud')||'This property is a part of a planned unit development known as "XXXXXXXXXXXXXXX"'}

\t\t\t\tASSIGNMENT INFORMATION

ASSIGNOR:\t\t\t${fv('asgn-assignor')} 

ASSIGNEE:\t\t\t${fv('asgn-assignee')}

DATED DATE:\t\t\t${fmtDate(fv('asgn-dated'))} 

REC DATE:  \t\t\t${fmtDate(fv('asgn-rec'))}

BOOK/PAGE:\t\t\t${fv('asgn-book')}

JUDGMENT AND LIEN INFORMATION

FINDINGS:\t\t\t${fv('judgment')}

ADDITIONAL INFORMATION

FINDINGS:\t\t\t${fv('additional')}

NAMES SEARCHED

${fv('names')}

LEGAL DESCRIPTION

Being the same property conveyed to ${fv('leg-to')||'________'} by ${fv('leg-deed')||'Special Warranty Deed'} from ${fv('leg-from')||'_______'}, dated ${fmtDate(fv('leg-dated'))||'_______'} recorded ${fmtDate(fv('leg-recorded'))||'_________'}, of record in Book ${fv('leg-book')||'_______'}, Page ${fv('leg-page')||'______'}, Register's Office for ${fv('leg-county')||'____'} County, ${fv('leg-state')||'____'}.

PARCEL/TAX ID:  \t\t${fv('leg-parcel')}

END OF REPORT`;
}

function collectTRJson(){
  if(trIdx===null) return null;
  const o = orders[trIdx];
  const chain = collectChain();
  return {
    // Order header (auto-filled from order)
    orderNum:      o.orderNum,
    orderType:     o.orderType,
    address:       o.address,
    county:        o.county,
    state:         o.state,
    parcel:        o.parcel,
    borrower:      o.borrower,
    dueDate:       o.dueDate||'',
    // Search info
    searchDate:    document.getElementById('tr-search-date').value,
    effDate:       document.getElementById('tr-eff-date').value,
    recOwner:      document.getElementById('tr-rec-owner').value,
    addrSearched:  document.getElementById('tr-addr-searched').value,
    // Assessment
    land:          document.getElementById('tr-land').value,
    building:      document.getElementById('tr-building').value,
    total:         document.getElementById('tr-total').value,
    parcelAssess:  document.getElementById('tr-parcel-assess').value,
    // Tax half
    tax1Year:      document.getElementById('tr-tax1-year').value,
    tax1Status:    document.getElementById('tr-tax1-status').value,
    tax1_1h:       document.getElementById('tr-tax1-1h').value,
    tax1_1hd:      document.getElementById('tr-tax1-1hd').value,
    tax1_2h:       document.getElementById('tr-tax1-2h').value,
    tax1_2hd:      document.getElementById('tr-tax1-2hd').value,
    // Tax quarterly
    tax2Year:      document.getElementById('tr-tax2-year').value,
    tax2Status:    document.getElementById('tr-tax2-status').value,
    tax2_1q:       document.getElementById('tr-tax2-1q').value,
    tax2_1qd:      document.getElementById('tr-tax2-1qd').value,
    tax2_2q:       document.getElementById('tr-tax2-2q').value,
    tax2_2qd:      document.getElementById('tr-tax2-2qd').value,
    taxParcel:     document.getElementById('tr-tax-parcel').value,
    // Deed
    deedType:      document.getElementById('tr-deed-type').value,
    deedConsid:    document.getElementById('tr-deed-consid').value,
    deedGrantor:   document.getElementById('tr-deed-grantor').value,
    deedGrantee:   document.getElementById('tr-deed-grantee').value,
    deedDated:     document.getElementById('tr-deed-dated').value,
    deedRec:       document.getElementById('tr-deed-rec').value,
    deedBook:      document.getElementById('tr-deed-book').value,
    // Chain of title
    chain: chain,
    // Mortgage
    mtgBorrower:   document.getElementById('tr-mtg-borrower').value,
    mtgLender:     document.getElementById('tr-mtg-lender').value,
    mtgTrustee:    document.getElementById('tr-mtg-trustee').value,
    mtgInstrument: document.getElementById('tr-mtg-instrument').value,
    mtgDated:      document.getElementById('tr-mtg-dated').value,
    mtgRec:        document.getElementById('tr-mtg-rec').value,
    mtgBook:       document.getElementById('tr-mtg-book').value,
    mtgAmount:     document.getElementById('tr-mtg-amount').value,
    mtgMaturity:   document.getElementById('tr-mtg-maturity').value,
    mtgPud:        document.getElementById('tr-mtg-pud').value,
    // Assignment
    asgnAssignor:  document.getElementById('tr-asgn-assignor').value,
    asgnAssignee:  document.getElementById('tr-asgn-assignee').value,
    asgnDated:     document.getElementById('tr-asgn-dated').value,
    asgnRec:       document.getElementById('tr-asgn-rec').value,
    asgnBook:      document.getElementById('tr-asgn-book').value,
    // Extra mortgage sections
    mtgExtra: Array.from(document.querySelectorAll('#tr-extra-mtg-container .tr-section')).map(sec=>({
      borrower:   sec.querySelector('.xmtg-borrower')?.value||'',
      lender:     sec.querySelector('.xmtg-lender')?.value||'',
      trustee:    sec.querySelector('.xmtg-trustee')?.value||'',
      instrument: sec.querySelector('.xmtg-instrument')?.value||'',
      dated:      sec.querySelector('.xmtg-dated')?.value||'',
      rec:        sec.querySelector('.xmtg-rec')?.value||'',
      book:       sec.querySelector('.xmtg-book')?.value||'',
      amount:     sec.querySelector('.xmtg-amount')?.value||'',
      maturity:   sec.querySelector('.xmtg-maturity')?.value||'',
      pud:        sec.querySelector('.xmtg-pud')?.value||'',
    })),
    // Extra assignment sections
    asgnExtra: Array.from(document.querySelectorAll('#tr-extra-asgn-container .tr-section')).map(sec=>({
      assignor: sec.querySelector('.xasgn-assignor')?.value||'',
      assignee: sec.querySelector('.xasgn-assignee')?.value||'',
      dated:    sec.querySelector('.xasgn-dated')?.value||'',
      rec:      sec.querySelector('.xasgn-rec')?.value||'',
      book:     sec.querySelector('.xasgn-book')?.value||'',
    })),
    // Other sections
    judgment:      document.getElementById('tr-judgment').value,
    additional:    document.getElementById('tr-additional').value,
    names:         document.getElementById('tr-names').value,
    // Legal description
    legTo:         document.getElementById('tr-leg-to').value,
    legDeed:       document.getElementById('tr-leg-deed').value,
    legFrom:       document.getElementById('tr-leg-from').value,
    legDated:      document.getElementById('tr-leg-dated').value,
    legRecorded:   document.getElementById('tr-leg-recorded').value,
    legBook:       document.getElementById('tr-leg-book').value,
    legPage:       document.getElementById('tr-leg-page').value,
    legCounty:     document.getElementById('tr-leg-county').value,
    legState:      document.getElementById('tr-leg-state').value,
    parcelTax:     document.getElementById('tr-leg-parcel').value,
    // Additional mortgage
    mtg2Borrower:   document.getElementById('tr-mtg2-borrower')?.value||'',
    mtg2Lender:     document.getElementById('tr-mtg2-lender')?.value||'',
    mtg2Trustee:    document.getElementById('tr-mtg2-trustee')?.value||'',
    mtg2Instrument: document.getElementById('tr-mtg2-instrument')?.value||'',
    mtg2Dated:      document.getElementById('tr-mtg2-dated')?.value||'',
    mtg2Rec:        document.getElementById('tr-mtg2-rec')?.value||'',
    mtg2Book:       document.getElementById('tr-mtg2-book')?.value||'',
    mtg2Amount:     document.getElementById('tr-mtg2-amount')?.value||'',
    mtg2Maturity:   document.getElementById('tr-mtg2-maturity')?.value||'',
    // Additional assignment
    asgn2Assignor:  document.getElementById('tr-asgn2-assignor')?.value||'',
    asgn2Assignee:  document.getElementById('tr-asgn2-assignee')?.value||'',
    asgn2Dated:     document.getElementById('tr-asgn2-dated')?.value||'',
    asgn2Rec:       document.getElementById('tr-asgn2-rec')?.value||'',
    asgn2Book:      document.getElementById('tr-asgn2-book')?.value||'',
  };
}

// ── TYPING REPORT TEMPLATES (base64-encoded, logos preserved) ──
const TP_TEMPLATE_B64='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bwDbEapdG41Bl3RafbkNM/oSOiL7tj2zXOeMfGei+GISL2fzbojMdrFgyN7n+6Pc/rXOeMPGWi+GISL2fzbojKWsWDI3uf7o9z+tVNQ1G2sl/eNuk7IvU/4V8w+MfiT8Qfivq66DpkM8VrcMRFpWnk/OPWV+CwHcnCj0rxvX/F3inxvfDTLOOVIZThLK1z8w9XbuPXOBXjuv+LvFPja+GmWccqQynCWVrn5h6u3ceucD2rnbvUL7UpfJjDBW6Rp3+p/yK9R+HfwU8M+B9L/4Sv4k3tjPNbKJfJkYfZLb0zn/AFre2MZ6A9a7Twp8O9H8OWX9t+Lri2kkhAfy3b9xD9c/fb9PQGuy8KfDzR/Dll/bfi64tpJIgH8tz+4h+v8Afb9PQGtGx0i3s4/tN+6Erzg/dX/E1HqPxD8XfFjXZPCfwzil0fRY8Le6xIpWRY/bH3M9lHzn/ZGaZd+Ktd8cak+ieD0ew09MC4v2XDBfb+7nsB8x9hmm3XirXfG+pPonhBHsNPXAuL9lwwX2/u57AfMfYZoe+utTmNtp4MUI+/KeuP6fzr2P4d+CtE8DaAulaPCcsd9zcycy3Mnd3bufboO1d/4U8Pad4b0sWNhGck7ppX5eZ+7Mf84rvvCnh7TvDemCysIzkndLK3Lyv3Zj/nFalhaQ2cAiiHuzHqx9TXS1r1r1YooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooqK8ubeztZbq7nit4IlLySyOFVFHUkngCmTzRW8LzTypFEgLO7sAqj1JPSmTzRW8LzTypFEg3O7thVHqSelI7KilmYKo5JJ4FfNnxg/aHeQzaN4AbanKSas6cn/rip/9Db8B3ryLx78VmYya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PdT1VhyD+IrwvT7zXvAPilwUMNzEds0LH93On9QeoPb8xXhmn3mveAvFLgoYbmI7ZoWP7udP6g9Qe35iuZikutKvjxtdeGU9GFfZPw38baL478OR6xo8vP3Li3cjzLeTHKMP5HoRyK9/8I+ItP8AEukpf2D/AOzLEx+eJv7p/wAe9e/eEvEWn+JdJS/sH/2ZYmPzxN/dP+PeuqsLyG9gEsR9mU9VPoa6atitirFFFFFFFFFFFFFec/G74o6b8PNGCR+Xd65dIfsdmTwB08yTHIQH8WPA7kcn8RfGdp4V0/auyfUplPkQZ6f7beij9eg745T4i+M7Twrp+1dk+pTKfIgz0/229FH69B3xR1fUY7GLAw0zD5V/qfavlvwZ4W8XfF/xtczyXEk0kkgk1HUpxlIFPQY6ZxwqDt6DmvF/D2i67488RSytK8jOwa7vJBlYx2H1x0UfoK8X8P6LrvjzxFLK0ryM7Bru7kHyxjsPrjoo/QVzlpbXWqXbEsSScySHoP8APpX2L4C8H6B4C8OLpmkQrDEg33FxIR5kzAcvI3+QB0wK998MaDpfhjSRZ2EYjRRullcjdIccsx/yBXvnhnQdL8M6SLOwjEaKN0srkbpDjlmP+QK6mytYLKDy4hgDlmPU+5r5u/aH+M0niaWfwv4XuGTQ0JS5uUODekfwj/pl/wChfTr5H8VviA2sPJo2jSldNU7ZplODcH0H+x/P6dfJPir8QG1h5NG0aUrpqnbNMpwbg+g/2P5/Trg65qpuCba3bEI4Zh/H/wDWrmvgR8K7z4g6wbq8Ett4ftHAupxwZm6+TGfX1P8ACPcisj4aeCrjxTf+fcB4dKgbE0o4Mh/uL7+p7D3rI+Gngq48U3/n3AeLS4GxNKODIf7i+/qew96r6Npr30u58rAp+Y+vsK+0tK0+y0rTrfTtOtorW0t4xHDDGuFRR0AFfQlla29laRWlpCkMEShI40GAoHYV9B2Vrb2VpFaWkKQwRKEjjQYCgdhXWRokcaxxqFVRgAdqs1NU1Ooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo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W3ivTZr61tp7dIpjEVlIySADng+9aGmXqX0LSojIFbbhvpXY1v1v1aoooooooooooori/jF4+tfh54UXWZrcXc8txHBBb79pkJOXOfZAx+uB3rnvH3ieHwrog1CSITyPKsccW7BbJy35KCfyrnvH3ieHwrog1CSITyPKsccW7BbJy35KCfyqpqt6tjbeaV3MWAC56+v6V1mmXttqWnW2oWcoltrmJZoXHRkYAg/ka3LO4hu7SG6t3DwzIJI2HdSMg1uWdxDd2kV1buHhmQSIw7qRkGrMbrJGrocqwyD7VYqWpadRRRRRRRRXK+MfFGsaFfJBYeCNb12EwiRp7F4dqnJGzDuGJ4B4HcVia/rN/ptysdr4d1HU4zHuMts0eAcn5cMwOeM9O9Yuv6zf6bcrHa+HdR1KMx7jLbNHgHJ+XDMDnj071WurmWFwEs5phjO5CPy5NeZ6l+0lo2m30tjqPg/xFZ3ULbZYZxEjofQgtkVyF38XdPtLl7a60HVoJ4zh45Aisp9wTXH3fxc0+0uXtrrQdVgmjOHjkCKyn3BNZ8mvxRuUe1nVh1BwCKr/APDUHhn/AKFrW/8AvuH/AOKqL/hcuj/9AfUf++o/8ai/4XLo/wD0CNR/76j/AMaT/hIbf/n3m/MVe0T9onTdb1BNP0fwT4l1C7cErDbrE7YHU4DcD3PFWNO+K9pqN0trYeHdXup25EcQRjj169PerOnfFa01G6W1sPDur3U7ciOIIxx69envToddjmcJFaXDsey4NekeEPE2sa3fSW+o+Cta0KJYvMWe9kgKucgbAEdjnnPIxxXXaDrF/qNy8V14d1DTECbhJcNGQxyPl+Vic9/wrrdB1i/1G5eK68PahpiKm4SXDRkMcj5flYnPf8K0LW4lmcrJaSwgDOXI59uDXUVs1s1YoooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooorE8c+J9M8H+F7zX9WkK29smQq/elc8KijuxOAP8ACs7xJrFnoOjXGqXz4ihX7o+87HgKPcnis7xJrFnoOjXGqXz4ihX7o+87Hoo9yahvLiO1t3nlPyqOncn0r4S+IPi3VvG3ii517V5Myy/LFCpykEY+7GvsPXuST3r5p8U6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X/QwQ/8AgIf/AIqo/wDhHH/5+1/74/8Ar0+3/Zh1W3mWa38cxQyr9147F1YfQiTIp0XwbvYpBJF4kSNx0ZLZlI/EPT4vg5exSCSLxIkbjoyWzAj8Q9Kvh2RTlbwA+oQj+taS/ADxmowvxW1AD2E//wAeq2Phf4hAwPG10Pwl/wDjlWx8L/EAGB42uh+Ev/xypBol2P8AmJP/AOPf41Wvv2cPEl+my++I812v92e3lkH5NKahufhJq9yu258WvOPSWJ2H6vUNz8JdXuV23Pi15x6SxOw/V6a+g3DjD35b/eBP9ap/8MtX/wD0Odt/4Lm/+OVB/wAKXuf+hgh/8BD/APFVX/4Uxc/9DBD/AOAh/wDiqZ/wjj/8/a/98f8A169V+Bfwyk+G2n6pbzatHqUl/Okm9IDFtCrgDBY55JNdt8NvB7eEbW9ikvku2uZFfcsRTAUYx1Pqa7b4beD38I2t7FJfLdtcyK+5YtmABjHU+prS0fTzYJIplEhcg5C46V6RXW11tX6KKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKK5H4oLnSrV/S4x+amvG/2rYt3hHSZv7moY/OJ/8K+bP2/oN/w88PXH/PPWNv8A31BJ/hWX4kH+jRH0f+hrz2vnKvi+sKiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiivUfh+MeF7b3Z//AEI19Xfs6qR8KNMJ7yzkf9/Wr9AP2NFK/s/6IT/FPdkf+BD10eh/8g2P6n+db9eh17HV6kcZQj1FMnXfC6f3lI/So7pPMtpI/wC8hH5ig8givEWGGI9DXwk42uy+hI/WvyilXZK6HqrFfyOK449aSkptFFFFFFFFFFFFFFFFFFFFFeh/C/8A5BFz/wBfH/sq19H/ALKf/Imap/2Ej/6KSvtP9gL/AJJpr3/YaP8A6Iird8N/8esn/XT+grra9ir6QrUooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo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RRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRR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';
const YD_TEMPLATE_B64='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AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqYd1yJoAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAP//EAAL/2gAMAwEAAgADAAAAIQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAIIABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABFEAAAAAAEBAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABCAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAABAAAFEADAEIAAAAACACCAAAICAAAAAAFEDDCAAAAAAABAABBAAACDAAAAAAAAOAAAADAAAAAAAJAAAAAAHBCOLPEDACAAAAAKHAFBBFLCBCDADBDDBACCABAAAAFFAAAABADDFAAAAAAAIAAAHEKAAAAAAAIAAAAAAAAFFBBLADAPECAKAAFKJDAFJGADKAFAJAJKIDAAAAFFAAAAEEIAAAAAAAAMAAALFEBBAAAAAAJAAAAAAAAFFFFAAEAMBNAKCBIKIAAEECMAKAAAAAABAKGAAAFFAAAAAACADAAAAAACABGBANAJLBCBAABAAAAAAAAFEAEAAJCMMIAKCAAKEAABCAJKKKBAEAIAIFIECAFBDAFDGAMMBIAAAAEAANAGIMBBFEEEIAACAAAAAAAAEEAIMIAAIAAMIAAEEAIIAAEIIAAAIEAACDAJKAMAAAAAIAEAMAAAAAAAALOBBDAMHIOIFIAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEIKAIIAAAAAAAAAAAAAAAAAEBNKAHHJMFAAAECNACAAAADDCAAAAAAAADDDDCAAACCAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAEFNIBLIACJLDCPFAGIAAAEBEEIFICFICANNACFDABIJEAAHGCOHDEAAAAAAAAAAAAAAAAAAAAAAAAAAAEMAAEAABEJPAIPJCKAAAAAEINEDAEECIAAAMIACAFAAOJAMOEAJCCAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMAMMAAIBGAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGMAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAANAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAP/EAAL/2gAMAwEAAgADAAAAEPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPFPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPOKCMIFNOPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPOIIAAAAAAMNPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPMPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPKAAAAAAAAAAOPPPPPPEPPPFIGPPEPPPPPPPPONPPLMHPPPPPPOINMNPPPPPPPNNPOMPPPPNNPPPPPPPHAAAAAAAAAAAABPPPPPHFBAELNBOAHMLPPPKGLBPOLNNOLGOPMKMEFDONONPPPFAPKAPOMDDINPPPPPKIAABGFCAAAAAAAFPPPPPKAPKFGEJAMBIDHPKOIAAIGAGLHCHAIJALBGKLNMHPPFAPKAPPFHLPHPPPPPKAABIMCAAAAAAAAJPPPPPKAPKFKAPAFFBCKPKCGPCIPAHBPDAAPKAAFFLCKLPPPFAPKAPPEPPMNPPPPLCABDGKDBGBFADAAFNPPPPKAPKEOEDAAEHNFPKNPPKAPAAOIJDJFLCDCHPAAHPGPFAPKEPLAIEAHPPPPKACBKDPHHFHECMJAAHPPPPLLPPLPHHLLLHDHPDHPPLLPPHDDPPPHLLPHLPOMPGNPLDDDDDPLLLHPPPPPKAGJLPNPKPGCDKNKAHPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPOJNPHPPPPPPPPPPPPPPPPPPODKEPPLIPFHBPPECKPPPPOPPNPPPONPPOMNNPNPPNMNPPPPPPPPPPPPPPLLPPPPPPPPPPPPPPPPPPPPPLGOPKAHCKLNOKHFAGFPPPPEELDEFBIOCPOEPEGALELIOIHNIAIJHHPPPPPPPPPPPPPPPPPPPPPPPPPPPLHPPCLPPIICKBICBPPPPPPPHKPCPDGNHPPLHBLJPLLPJOHHGHLPOE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';

// ── EMBEDDED TEMPLATES (base64) ──────────────────────────────────────
const TMPL_TP    = "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AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqYd1yJoAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAP//EAAL/2gAMAwEAAgADAAAAIQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAIIABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABFEAAAAAAEBAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABCAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAABAAAFEADAEIAAAAACACCAAAICAAAAAAFEDDCAAAAAAABAABBAAACDAAAAAAAAOAAAADAAAAAAAJAAAAAAHBCOLPEDACAAAAAKHAFBBFLCBCDADBDDBACCABAAAAFFAAAABADDFAAAAAAAIAAAHEKAAAAAAAIAAAAAAAAFFBBLADAPECAKAAFKJDAFJGADKAFAJAJKIDAAAAFFAAAAEEIAAAAAAAAMAAALFEBBAAAAAAJAAAAAAAAFFFFAAEAMBNAKCBIKIAAEECMAKAAAAAABAKGAAAFFAAAAAACADAAAAAACABGBANAJLBCBAABAAAAAAAAFEAEAAJCMMIAKCAAKEAABCAJKKKBAEAIAIFIECAFBDAFDGAMMBIAAAAEAANAGIMBBFEEEIAACAAAAAAAAEEAIMIAAIAAMIAAEEAIIAAEIIAAAIEAACDAJKAMAAAAAIAEAMAAAAAAAALOBBDAMHIOIFIAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEIKAIIAAAAAAAAAAAAAAAAAEBNKAHHJMFAAAECNACAAAADDCAAAAAAAADDDDCAAACCAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAEFNIBLIACJLDCPFAGIAAAEBEEIFICFICANNACFDABIJEAAHGCOHDEAAAAAAAAAAAAAAAAAAAAAAAAAAAEMAAEAABEJPAIPJCKAAAAAEINEDAEECIAAAMIACAFAAOJAMOEAJCCAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMAMMAAIBGAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGMAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAANAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAP/EAAL/2gAMAwEAAgADAAAAEPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPFPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPOKCMIFNOPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPOIIAAAAAAMNPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPMPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPKAAAAAAAAAAOPPPPPPEPPPFIGPPEPPPPPPPPONPPLMHPPPPPPOINMNPPPPPPPNNPOMPPPPNNPPPPPPPHAAAAAAAAAAAABPPPPPHFBAELNBOAHMLPPPKGLBPOLNNOLGOPMKMEFDONONPPPFAPKAPOMDDINPPPPPKIAABGFCAAAAAAAFPPPPPKAPKFGEJAMBIDHPKOIAAIGAGLHCHAIJALBGKLNMHPPFAPKAPPFHLPHPPPPPKAABIMCAAAAAAAAJPPPPPKAPKFKAPAFFBCKPKCGPCIPAHBPDAAPKAAFFLCKLPPPFAPKAPPEPPMNPPPPLCABDGKDBGBFADAAFNPPPPKAPKEOEDAAEHNFPKNPPKAPAAOIJDJFLCDCHPAAHPGPFAPKEPLAIEAHPPPPKACBKDPHHFHECMJAAHPPPPLLPPLPHHLLLHDHPDHPPLLPPHDDPPPHLLPHLPOMPGNPLDDDDDPLLLHPPPPPKAGJLPNPKPGCDKNKAHPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPOJNPHPPPPPPPPPPPPPPPPPPODKEPPLIPFHBPPECKPPPPOPPNPPPONPPOMNNPNPPNMNPPPPPPPPPPPPPPLLPPPPPPPPPPPPPPPPPPPPPLGOPKAHCKLNOKHFAGFPPPPEELDEFBIOCPOEPEGALELIOIHNIAIJHHPPPPPPPPPPPPPPPPPPPPPPPPPPPLHPPCLPPIICKBICBPPPPPPPHKPCPDGNHPPLHBLJPLLPJOHHGHLPOE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";
const TMPL_YDEAL = "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";

// ── DOCX FILLER (browser-side via JSZip) ──────────────────────────────
async function dlTypingReport(){
  saveTRData();
  if(trIdx===null) return;
  const o = orders[trIdx];
  const d = collectTRJson();
  notify('Generating Word report...');

  // Load JSZip if needed
  if(!window.JSZip){
    await new Promise((res,rej)=>{
      const s=document.createElement('script');
      s.src='https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js';
      s.onload=res; s.onerror=rej;
      document.head.appendChild(s);
    });
  }

  // Date formatter
  function fd(v){
    if(!v) return 'MM/DD/YYYY';
    v=String(v).trim();
    try{if(v.includes('T'))v=v.split('T')[0];const p=v.split('-');if(p.length===3&&p[0].length===4)return`${p[1]}/${p[2]}/${p[0]}`;}catch(e){}
    return v;
  }
  function fv(val){const s=val?String(val).trim():'';return s||'Type here';}
  function fdv(val){const s=val?String(val).trim():'';return s?fd(s):'MM/DD/YYYY';}
  function xe(v){return String(v||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}

  // Choose template based on company
  const b64 = (o.company==='TitlePriority') ? TMPL_TP : TMPL_YDEAL;

  // Decode base64 → ArrayBuffer
  const bin = atob(b64);
  const arr = new Uint8Array(bin.length);
  for(let i=0;i<bin.length;i++) arr[i]=bin.charCodeAt(i);

  // Load zip
  const zip = await JSZip.loadAsync(arr.buffer);

  // Get document XML
  let xml = await zip.file('word/document.xml').async('string');

  const ch = d.chain||[];
  const c1 = ch[0]||{};
  const c2 = ch[1]||{};

  // --- PLACEHOLDER REPLACEMENT ---
  // All 61 placeholders in document order (determined from template analysis)
  // Types: TH=Type here, MM=MM/DD/YYYY, DL=$ or $0.00
  const VALS = [
    xe(d.orderNum||''),               // [0]  ORDER NUMBER
    xe(d.orderType||''),              // [1]  PRODUCT NAME
    '',                               // [2]  ADDRESS (handled via MERGEFIELD)
    xe(d.county||''),                 // [3]  COUNTY
    fdv(d.searchDate),                // [4]  SEARCH DATE (MM/DD/YYYY)
    fdv(d.effDate||d.dueDate),        // [5]  EFFECTIVE DATE (MM/DD/YYYY)
    xe(d.recOwner||d.borrower||''),   // [6]  RECORD OWNER
    xe(d.addrSearched||d.address||''),// [7]  ADDRESS SEARCHED
    d.land?`$${xe(d.land)}`:'$',    // [8]  LAND $
    d.building?`$${xe(d.building)}`:'$',// [9] BUILDING $
    d.total?`$${xe(d.total)}`:'$',  // [10] TOTAL $
    xe(d.parcelAssess||d.parcel||''), // [11] TAX YEAR 1 (PARCEL NO handled separately)
    xe(d.tax1Year||''),               // [12] STATUS 1 — wait, let me recheck order
    xe(d.tax1Status||''),             // [13]
    xe(d.tax1_1h||''),                // [14]
    fdv(d.tax1_1hd),                  // [15]
    xe(d.tax1_2h||''),                // [16]
    fdv(d.tax1_2hd),                  // [17]
    xe(d.tax2Year||''),               // [18]
    xe(d.tax2Status||''),             // [19]
    xe(d.tax2_1q||''),                // [20]
    fdv(d.tax2_1qd),                  // [21]
    xe(d.tax2_2q||''),                // [22]
    fdv(d.tax2_2qd),                  // [23]
    xe(d.deedType||''),               // [24] DEED TYPE
    xe(d.deedConsid||'0.00'),         // [25] CONSIDERATION ($0.00)
    xe(d.deedGrantor||''),            // [26] GRANTOR
    xe(d.deedGrantee||d.borrower||''),// [27] GRANTEE
    fdv(d.deedDated),                 // [28] DATED DATE
    fdv(d.deedRec),                   // [29] REC DATE
    xe(d.deedBook||''),               // [30] BOOK/PAGE
    xe(c1.type||''),                  // [31] CHAIN1 DEED TYPE
    xe(c1.consid||'0.00'),            // [32] CHAIN1 CONSIDERATION
    xe(c1.grantor||''),               // [33] CHAIN1 GRANTOR
    xe(c1.grantee||''),               // [34] CHAIN1 GRANTEE
    fdv(c1.dated),                    // [35] CHAIN1 DATED
    fdv(c1.rec),                      // [36] CHAIN1 REC
    xe(c1.book||''),                  // [37] CHAIN1 BOOK
    xe(c2.type||''),                  // [38] CHAIN2 DEED TYPE
    xe(c2.consid||'0.00'),            // [39] CHAIN2 CONSIDERATION
    xe(c2.grantor||''),               // [40] CHAIN2 GRANTOR
    xe(c2.grantee||''),               // [41] CHAIN2 GRANTEE
    fdv(c2.dated),                    // [42] CHAIN2 DATED
    fdv(c2.rec),                      // [43] CHAIN2 REC
    xe(c2.book||''),                  // [44] CHAIN2 BOOK
    xe(d.mtgBorrower||d.borrower||''),// [45] BORROWER
    xe(d.mtgLender||''),              // [46] LENDER
    xe(d.mtgTrustee||''),             // [47] TRUSTEE
    xe(d.mtgInstrument||''),          // [48] INSTRUMENT NAME
    fdv(d.mtgDated),                  // [49] DATED DATE
    fdv(d.mtgRec),                    // [50] REC DATE
    xe(d.mtgBook||''),                // [51] BOOK/PAGE
    xe(d.mtgAmount||''),              // [52] AMOUNT
    fdv(d.mtgMaturity),               // [53] MATURITY DATE
    xe(d.asgnAssignor||''),           // [54] ASSIGNOR  (was 53 before)
    xe(d.asgnAssignee||''),           // [55] ASSIGNEE
    fdv(d.asgnDated),                 // [56] DATED DATE
    fdv(d.asgnRec),                   // [57] REC DATE
    xe(d.asgnBook||''),               // [58] BOOK/PAGE
    xe(d.judgment||''),               // [59] JUDGMENT FINDINGS
    xe(d.additional||''),             // [60] ADDITIONAL FINDINGS
    // [60] PARCEL/TAX ID is handled separately
  ];

  // Replace MERGEFIELD address
  const addr = xe(d.address||'');
  xml = xml.replace(
    /<w:fldChar w:fldCharType="begin"\/>.+?<w:fldChar w:fldCharType="end"\/>/s,
    `<w:t xml:space="preserve">${addr}</w:t>`
  );

  // Replace PARCEL NO (assessment) — uses "     " placeholder
  xml = xml.replace('<w:t xml:space="preserve">     </w:t>',
    `<w:t xml:space="preserve">${xe(d.parcelAssess||d.parcel||'')}</w:t>`, );
  // Note: JS replace only replaces first occurrence by default ✓

  // Replace PARCEL NO (tax) — 2nd occurrence of "     "
  xml = xml.replace('<w:t xml:space="preserve">     </w:t>',
    `<w:t xml:space="preserve">${xe(d.taxParcel||d.parcel||'')}</w:t>`);

  // Replace PUD
  const pudVal = xe(d.mtgPud||'No');
  xml = xml.replace(
    '>This property is a part of a planned unit development known as &#x201C;XXXXXXXXXXXXXXX&#x201D;<',
    `>${pudVal}<`
  );

  // Replace LEGAL DESCRIPTION sentence (first fragment only, rest get blanked)
  const legTo     = xe(d.legTo||d.borrower||'________');
  const legDeed   = xe(d.legDeed||'Special Warranty Deed');
  const legFrom   = xe(d.legFrom||'_______');
  const legDated  = d.legDated ? fdv(d.legDated) : '_______';
  const legRec    = d.legRecorded ? fdv(d.legRecorded) : '_________';
  const legBook   = xe(d.legBook||'_______');
  const legPage   = xe(d.legPage||'______');
  const legCounty = xe(d.legCounty||d.county||'____');
  const legState  = xe(d.legState||d.state||'____');
  const fullLegal = `Being the same property conveyed to ${legTo} by ${legDeed} from ${legFrom}, dated ${legDated} recorded ${legRec}, of record in Book ${legBook}, Page ${legPage}, Register&#x2019;s Office for ${legCounty} County, ${legState}.`;

  xml = xml.replace('>Being the same property conveyed to <', `>${fullLegal}<DONE/><`);

  // Remove remaining blank fragments
  const frags = ['________',' by Special Warranty Deed from ','_______',', dated ','_______',' recorded ','_________',', of record in Book ','_______',', Page ','______',', Register’s Office for ','____',' County, ','____','.'];
  const markerPos = xml.indexOf('<DONE/>');
  if(markerPos>0) {
    let tail = xml.slice(markerPos);
    frags.forEach(f=>{
      const ef = f.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
      // Only replace within 5000 chars of marker
      const searchIn = tail.slice(0, 5000);
      const idx = searchIn.indexOf(`>${ef}<`);
      if(idx>=0) {
        tail = tail.slice(0,idx+1) + tail.slice(idx+1).replace(ef+'</w:t>', '</w:t>');
      }
    });
    xml = xml.slice(0, markerPos) + tail;
  }
  xml = xml.replace('<DONE/>', '');

  // Replace NAMES SEARCHED — insert after section header
  const namesVal = xe(d.names||d.borrower||'');
  if(namesVal) {
    const nsIdx = xml.indexOf('>NAMES SEARCHED<');
    if(nsIdx>0) {
      const paraEnd = xml.indexOf('</w:p>', nsIdx) + 6;
      const newPara = `<w:p><w:pPr><w:spacing w:after="0" w:line="240" w:lineRule="auto"/></w:pPr><w:r><w:rPr><w:sz w:val="23"/><w:szCs w:val="23"/></w:rPr><w:t xml:space="preserve">${namesVal}</w:t></w:r></w:p>`;
      xml = xml.slice(0,paraEnd) + newPara + xml.slice(paraEnd);
    }
  }

  // === ADDITIONAL MORTGAGE SECTION ===
  if(d.mtg2Borrower||d.mtg2Lender||d.mtg2Amount) {
    const mtgSec = xml.indexOf('>MORTGAGE INFORMATION<');
    const asnSec = xml.indexOf('>ASSIGNMENT INFORMATION<');
    if(mtgSec>0 && asnSec>0) {
      // Find the paragraph containing ASSIGNMENT INFORMATION section header
      const asgnParaStart = xml.lastIndexOf('<w:p ', asnSec);
      // Build additional mortgage XML block
      function mkField(label, value) {
        return `<w:p><w:pPr><w:autoSpaceDE w:val="0"/><w:autoSpaceDN w:val="0"/><w:adjustRightInd w:val="0"/><w:spacing w:after="0" w:line="240" w:lineRule="auto"/></w:pPr><w:r><w:rPr><w:rStyle w:val="PlaceholderText"/></w:rPr><w:t xml:space="preserve">${label}</w:t><w:tab/><w:tab/></w:r><w:r><w:rPr><w:b/><w:bCs/><w:sz w:val="23"/><w:szCs w:val="23"/></w:rPr><w:t xml:space="preserve">${xe(value)}</w:t></w:r></w:p>`;
      }
      const extraMtg = [
        `<w:p><w:pPr><w:jc w:val="center"/><w:spacing w:before="120" w:after="120" w:line="240" w:lineRule="auto"/></w:pPr><w:r><w:rPr><w:b/><w:bCs/><w:sz w:val="36"/><w:szCs w:val="36"/><w:u w:val="single"/></w:rPr><w:t>ADDITIONAL MORTGAGE</w:t></w:r></w:p>`,
        mkField('BORROWER:',        d.mtg2Borrower||''),
        mkField('LENDER:  ',        d.mtg2Lender||''),
        mkField('TRUSTEE:',         d.mtg2Trustee||''),
        mkField('INSTRUMENT NAME:', d.mtg2Instrument||''),
        mkField('DATED DATE:',      fdv(d.mtg2Dated)),
        mkField('REC DATE:  ',      fdv(d.mtg2Rec)),
        mkField('BOOK/PAGE:',       d.mtg2Book||''),
        mkField('AMOUNT:',          d.mtg2Amount||''),
        mkField('MATURITY DATE:',   fdv(d.mtg2Maturity)),
      ].join('');
      xml = xml.slice(0, asgnParaStart) + extraMtg + xml.slice(asgnParaStart);
    }
  }

  // === ADDITIONAL ASSIGNMENT SECTION ===
  if(d.asgn2Assignor||d.asgn2Assignee) {
    const jdgSec = xml.indexOf('>JUDGMENT AND LIEN INFORMATION<');
    if(jdgSec>0) {
      const jdgParaStart = xml.lastIndexOf('<w:p ', jdgSec);
      function mkField2(label, value) {
        return `<w:p><w:pPr><w:autoSpaceDE w:val="0"/><w:autoSpaceDN w:val="0"/><w:adjustRightInd w:val="0"/><w:spacing w:after="0" w:line="240" w:lineRule="auto"/></w:pPr><w:r><w:rPr><w:rStyle w:val="PlaceholderText"/></w:rPr><w:t xml:space="preserve">${label}</w:t><w:tab/><w:tab/></w:r><w:r><w:rPr><w:b/><w:bCs/><w:sz w:val="23"/><w:szCs w:val="23"/></w:rPr><w:t xml:space="preserve">${xe(value)}</w:t></w:r></w:p>`;
      }
      const extraAsgn = [
        `<w:p><w:pPr><w:jc w:val="center"/><w:spacing w:before="120" w:after="120" w:line="240" w:lineRule="auto"/></w:pPr><w:r><w:rPr><w:b/><w:bCs/><w:sz w:val="23"/><w:szCs w:val="23"/></w:rPr><w:t>ADDITIONAL ASSIGNMENT INFORMATION</w:t></w:r></w:p>`,
        mkField2('ASSIGNOR:',   d.asgn2Assignor||''),
        mkField2('ASSIGNEE:',   d.asgn2Assignee||''),
        mkField2('DATED DATE:', fdv(d.asgn2Dated)),
        mkField2('REC DATE:  ', fdv(d.asgn2Rec)),
        mkField2('BOOK/PAGE:', d.asgn2Book||''),
      ].join('');
      xml = xml.slice(0, jdgParaStart) + extraAsgn + xml.slice(jdgParaStart);
    }
  }

  // === MAIN PLACEHOLDER LOOP ===
  // Replace all 61 placeholders in document order
  const PH = /<w:t(?:\s[^>]*)?>(?:Type here|MM\/DD\/YYYY|\$0\.00|\$)<\/w:t>/g;
  let idx = 0;
  xml = xml.replace(PH, (match) => {
    if(idx >= VALS.length) return match;
    const v = VALS[idx++];
    return `<w:t xml:space="preserve">${v}</w:t>`;
  });

  // Write back to zip and download
  zip.file('word/document.xml', xml);
  const outBlob = await zip.generateAsync({type:'blob', compression:'DEFLATE', compressionOptions:{level:6}});
  const co = o.company==='TitlePriority'?'TitlePriority':'YDeal';
  const fname = o.orderNum.replace(/[^a-zA-Z0-9\-]/g,'_')+'_'+co+'_TypingReport_'+getOrderDate(o)+'.docx';
  const lnk = document.createElement('a');
  lnk.href = URL.createObjectURL(outBlob);
  lnk.download = fname;
  lnk.click();
  notify('\u2713 Word report downloaded: '+fname);
}
function saveTRAndMarkDone(){
  saveTRData();
  if(trIdx===null) return;
  const o = orders[trIdx];
  dlTypingReport();
  o.status = 'Quality/Final Review';
  closeTR();
  render();
  renderTypingPage();
  notify('Marked Ready for Delivery: '+o.orderNum);
}

function closeTR(){
  saveTRData();
  document.getElementById('tr-overlay').classList.remove('open');
  trIdx = null;
}

// ── ONEDRIVE PATH GENERATOR ──
// ════════════════════════════════════════════════════════════
// ONEDRIVE PERSONAL FOLDER SYSTEM
// ════════════════════════════════════════════════════════════

// Get the network drive path for a specific user + order
function getOrderFolderPath(order){
  const co   = order.company === 'TitlePriority' ? 'TitlePriority' : 'YDeal';
  const d    = order.orderDate ? new Date(order.orderDate+'T00:00:00') : new Date();
  const mm   = String(d.getMonth()+1).padStart(2,'0');
  const dd   = String(d.getDate()).padStart(2,'0');
  const yyyy = d.getFullYear();
  const dateStr = `${mm}-${dd}-${yyyy}`;
  return `Z:\\Title Orders\\${co}\\${dateStr}\\${order.orderNum}`;
}

// Get path for the assigned member's root folder
function getMyRootPath(){
  if(!currentUser) return 'Z:\\Title Orders';
  const u = currentUser;
  // Admins see all; team members see their assigned folder
  if(u.role === 'admin') return 'Z:\\Title Orders';
  // Map user to their assigned key in TEAM
  const assignKey = u.assignKey || u.initials;
  return `Z:\\Title Orders\\${u.initials}`;
}

// Open Windows Explorer to the user's OneDrive folder
function openMyOneDrive(){
  const path = getMyRootPath();
  // Use window.location to trigger Windows file explorer via UNC path
  // On Windows, this opens File Explorer to the mapped drive
  const encodedPath = path.replace(/\\/g, '/');
  // Try to open via file:// protocol (works on Windows with mapped drives)
  try {
    window.open(`file:///${encodedPath}`, '_blank');
  } catch(e){}
  // Also copy the path to clipboard as fallback
  navigator.clipboard.writeText(path).catch(()=>{});
  notify(`📁 Opening: ${path} — also copied to clipboard`);
  // Show instructions if needed
  showODOpenInstructions(path);
}

// Show a small modal with the run command
function showODOpenInstructions(path){
  // Remove existing if any
  const existing = document.getElementById('od-run-modal');
  if(existing) existing.remove();

  const div = document.createElement('div');
  div.id = 'od-run-modal';
  div.style.cssText = 'position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);background:var(--surface);border:1px solid var(--border2);border-radius:var(--rl);padding:20px 24px;z-index:900;width:480px;max-width:95vw;box-shadow:0 8px 40px rgba(0,0,0,.2)';
  div.innerHTML = `
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
      <div style="font-size:14px;font-weight:600;color:var(--text)">Open Your OneDrive Folder</div>
      <button onclick="document.getElementById('od-run-modal').remove()" style="background:none;border:none;font-size:18px;cursor:pointer;color:var(--text3)">✕</button>
    </div>
    <div style="font-size:12px;color:var(--text2);margin-bottom:10px;line-height:1.6">
      Press <strong>Windows Key + R</strong> on your keyboard, paste this path and press Enter:
    </div>
    <div style="background:#1A1917;border-radius:var(--r);padding:12px 14px;font-family:'DM Mono',monospace;font-size:13px;color:#FFD700;margin-bottom:12px;display:flex;align-items:center;justify-content:space-between;gap:8px;word-break:break-all">
      <span>${path}</span>
      <button onclick="navigator.clipboard.writeText('${path}');this.textContent='Copied!';setTimeout(()=>this.textContent='Copy',2000)" style="background:rgba(255,255,255,.1);border:none;color:#fff;cursor:pointer;border-radius:6px;padding:4px 10px;font-size:11px;white-space:nowrap;flex-shrink:0">Copy</button>
    </div>
    <div style="font-size:11px;color:var(--text3);margin-bottom:14px">
      Path copied to clipboard automatically. Make sure your network drive is mapped as Z: on your laptop.
    </div>
    <div style="display:flex;gap:8px;justify-content:flex-end">
      <button class="btn btn-sm" onclick="document.getElementById('od-run-modal').remove()">Close</button>
      <button class="btn btn-sm btn-p" onclick="downloadOrderInfoTxt();document.getElementById('od-run-modal').remove()">Download All Order Info TXT Files</button>
    </div>`;
  document.body.appendChild(div);
}

// Render assigned orders with folder paths on OneDrive page
function renderODAssignedOrders(){
  const el = document.getElementById('od-assigned-orders');
  if(!el || !currentUser) return;

  const greet = document.getElementById('od-greeting');
  const sub   = document.getElementById('od-user-sub');
  if(greet) greet.textContent = currentUser.name + "'s OneDrive Folders";
  if(sub)   sub.textContent   = currentUser.role === 'admin'
    ? 'Admin — full access to all orders and folders'
    : 'Your assigned orders — ' + currentUser.initials;

  const myOrders = currentUser.role === 'admin'
    ? orders
    : orders.filter(o => o.assigned === currentUser.assignKey || o.assigned === currentUser.initials);

  if(!myOrders.length){
    el.innerHTML = '<div style="text-align:center;padding:16px;color:var(--text3);font-size:12px">No orders assigned yet</div>';
    return;
  }

  // Group by date
  const grouped = {};
  myOrders.forEach(o => {
    const d  = o.orderDate ? new Date(o.orderDate+'T00:00:00') : new Date();
    const mm = String(d.getMonth()+1).padStart(2,'0');
    const dd = String(d.getDate()).padStart(2,'0');
    const key = mm+'-'+dd+'-'+d.getFullYear();
    if(!grouped[key]) grouped[key] = [];
    grouped[key].push(o);
  });

  const sortedDates = Object.keys(grouped).sort((a,b) => new Date(b) - new Date(a));
  let html = '';

  sortedDates.forEach(date => {
    const dateOrders = grouped[date];
    html += '<div style="margin-bottom:12px">';
    html += '<div style="font-size:11px;font-weight:600;color:var(--blue-t);background:var(--blue-l);padding:5px 10px;border-radius:6px;margin-bottom:7px;display:flex;align-items:center;justify-content:space-between">';
    html += '<span>EST Date: ' + date + '</span>';
    html += '<span style="color:var(--text3);font-weight:400">' + dateOrders.length + ' order' + (dateOrders.length!==1?'s':'') + '</span></div>';

    dateOrders.forEach(o => {
      const path  = getOrderFolderPath(o);
      const co    = o.company === 'TitlePriority' ? 'Title Priority' : 'YDeal';
      const oidx  = orders.indexOf(o);
      const safePath = path.replace(/\\/g,'\\\\').replace(/'/g,"\\'");

      html += '<div style="display:flex;align-items:center;gap:8px;padding:8px 10px;background:var(--bg);border:1px solid var(--border);border-radius:8px;margin-bottom:5px;flex-wrap:wrap">';
      html += '<div style="flex:1;min-width:180px">';
      html += '<div style="font-size:12px;font-weight:600;color:var(--text)">' + o.orderNum + '</div>';
      html += '<div style="font-size:11px;color:var(--text3)">' + (o.borrower||'') + ' &middot; ' + co + ' &middot; ' + (o.orderType||'') + '</div>';
      html += '<div style="font-size:10px;color:var(--text3);font-family:\'DM Mono\',monospace;margin-top:2px">' + path + '</div>';
      html += '</div>';
      html += '<div style="display:flex;gap:5px;flex-shrink:0;flex-wrap:wrap">';
      html += bdg(o.status);
      html += '<button class="btn btn-sm" onclick="copyODPath(\'' + safePath + '\')" style="font-size:10px;padding:3px 8px">Copy path</button>';
      html += '<button class="btn btn-sm btn-g" onclick="downloadSingleOrderTxt(' + oidx + ')" style="font-size:10px;padding:3px 8px">Download TXT</button>';
      html += '<button class="btn btn-sm btn-p" onclick="showODOpenInstructions(\'' + safePath + '\')" style="font-size:10px;padding:3px 8px">Open</button>';
      html += '</div></div>';
    });
    html += '</div>';
  });

  el.innerHTML = html;
}

function copyODPath(path){
  navigator.clipboard.writeText(path).catch(()=>{});
  notify('✓ Path copied — press Win+R and paste to open folder');
}

// Download TXT info file for a single order
function downloadSingleOrderTxt(idx){
  const o = orders[idx];
  if(!o) return;
  const path = getOrderFolderPath(o);
  const d    = o.orderDate ? new Date(o.orderDate+'T00:00:00') : new Date();
  const mm   = String(d.getMonth()+1).padStart(2,'0');
  const dd   = String(d.getDate()).padStart(2,'0');
  const yyyy = d.getFullYear();

  const txt = `================================================================
ORDER INFORMATION FILE
================================================================
Order Number    : ${o.orderNum}
Company         : ${o.company === 'TitlePriority' ? 'Title Priority' : 'YDeal Title Services'}
Order Type      : ${o.orderType || ''}
Status          : ${o.status || ''}
Assigned To     : ${o.assigned || ''}

BORROWER INFORMATION
----------------------------------------------------------------
Borrower Name   : ${o.borrower || ''}
Property Address: ${o.address || ''}
County          : ${o.county || ''}
State           : ${o.state || ''}
Parcel Number   : ${o.parcel || ''}

ORDER DATES
----------------------------------------------------------------
Order Date      : ${o.orderDate || ''}
Due Date        : ${o.dueDate ? o.dueDate.replace('T',' ') : ''}
EST Date Folder : ${mm}-${dd}-${yyyy}

FINANCIAL
----------------------------------------------------------------
Fee             : ${o.fee ? '$'+o.fee : ''}
Client Order #  : ${o.clientNum || ''}

FOLDER LOCATION
----------------------------------------------------------------
Network Drive   : ${path}
----------------------------------------------------------------
Subfolders:
  ${path}\\1 - Plat Map
  ${path}\\2 - Assessor
  ${path}\\3 - Taxes
  ${path}\\4 - Deeds
  ${path}\\5 - Mortgage Documents
  ${path}\\6 - Judgments
  ${path}\\7 - Pacer and Patriot
  ${path}\\8 - Typing Report
  ${path}\\9 - Supporting Docs

INSTRUCTIONS
----------------------------------------------------------------
${o.instructions || 'No special instructions'}

================================================================
Generated: ${new Date().toLocaleString('en-US')}
Dashboard: https://ydeal144.github.io/title-dashboard
================================================================`;

  const blob = new Blob([txt], {type:'text/plain'});
  const a    = document.createElement('a');
  a.href     = URL.createObjectURL(blob);
  a.download = `${o.orderNum}_OrderInfo.txt`;
  a.click();
  notify(`✓ Order info TXT downloaded for ${o.orderNum} — save it in the order folder`);
}

// Download TXT files for ALL assigned orders at once
function downloadOrderInfoTxt(){
  if(!currentUser) return;
  const myOrders = currentUser.role === 'admin'
    ? orders
    : orders.filter(o => o.assigned === currentUser.assignKey || o.assigned === currentUser.initials);
  if(!myOrders.length){ notify('No orders to download'); return; }
  myOrders.forEach((o,i) => {
    setTimeout(() => downloadSingleOrderTxt(orders.indexOf(o)), i * 300);
  });
  notify('Downloading ' + myOrders.length + ' order info files...');
}

function generateODPath(){
  const raw     = document.getElementById('od-ordernum').value.trim();
  const dateVal = document.getElementById('od-date').value;
  const co      = document.getElementById('od-company')?.value || 'YDeal';
  if(!raw){ notify('Please enter an order number'); return; }
  const orderSafe = raw.replace(/[^a-zA-Z0-9\-]/g,'_');
  const d = dateVal ? new Date(dateVal+'T00:00:00') : new Date();
  const mm = String(d.getMonth()+1).padStart(2,'0');
  const dd = String(d.getDate()).padStart(2,'0');
  const yyyy = d.getFullYear();
  const dateStr = mm+'-'+dd+'-'+yyyy;
  const coLabel = co === 'TitlePriority' ? 'TitlePriority' : 'YDeal';
  const base = 'Z:\\Title Orders\\'+coLabel+'\\'+dateStr+'\\'+orderSafe;
  const res = document.getElementById('od-result');
  res.style.display = 'block';
  let html = '';
  html += '<div style="color:#888;font-size:10px;margin-bottom:4px"># Full folder path</div>';
  html += '<div style="color:#FFD700">'+base+'</div>';
  html += '<div style="color:#888;font-size:10px;margin-top:10px;margin-bottom:4px"># Windows Run command (Win+R)</div>';
  html += '<div>'+base+'</div>';
  html += '<div style="color:#888;font-size:10px;margin-top:10px;margin-bottom:4px"># Subfolders</div>';
  ['1 - Plat Map','2 - Assessor','3 - Taxes','4 - Deeds','5 - Mortgage Documents',
   '6 - Judgments','7 - Pacer and Patriot','8 - Typing Report','9 - Supporting Docs'].forEach(f=>{
    html += '<div>'+base+'\\'+f+'</div>';
  });
  html += '<div style="color:#888;font-size:10px;margin-top:10px;margin-bottom:4px"># Batch script inputs</div>';
  html += '<div style="color:#7EC8E3">Order Number: '+orderSafe+'</div>';
  html += '<div style="color:#7EC8E3">EST Date: '+dateStr+'</div>';
  html += '<div style="color:#7EC8E3">Company: '+coLabel+'</div>';
  res.innerHTML = html;
  notify('Path generated for: '+raw);
}

function downloadBatchScript(){
  const script = `@echo off
title Create Order Folder - YDeal / Title Priority
echo ===============================================
echo  Title Order Folder Creator
echo  YDeal Title Services / Title Priority
echo ===============================================
echo.
set /p ORDER_NUM=Enter Order Number (e.g. 01-26027784-03T): 
set /p EST_DATE=Enter EST Date (MM-DD-YYYY e.g. 04-29-2026): 
echo.
echo Select Company:
echo  1. YDeal Title Services
echo  2. Title Priority
set /p CO_CHOICE=Enter 1 or 2: 
if "%CO_CHOICE%"=="1" set COMPANY=YDeal
if "%CO_CHOICE%"=="2" set COMPANY=TitlePriority
echo.
set BASE=Z:\\Title Orders\\%COMPANY%\\%EST_DATE%\\%ORDER_NUM%
echo Creating folders at: %BASE%
echo.
mkdir "%BASE%" 2>nul
mkdir "%BASE%\\1 - Plat Map" 2>nul
mkdir "%BASE%\\2 - Assessor" 2>nul
mkdir "%BASE%\\3 - Taxes" 2>nul
mkdir "%BASE%\\4 - Deeds" 2>nul
mkdir "%BASE%\\5 - Mortgage Documents" 2>nul
mkdir "%BASE%\\6 - Judgments" 2>nul
mkdir "%BASE%\\7 - Pacer and Patriot" 2>nul
mkdir "%BASE%\\8 - Typing Report" 2>nul
mkdir "%BASE%\\9 - Supporting Docs" 2>nul
echo.
echo ===============================================
echo  SUCCESS! Folders created for: %ORDER_NUM%
echo  Company: %COMPANY%
echo  EST Date: %EST_DATE%
echo ===============================================
echo.
start explorer "%BASE%"
pause`;
  const blob = new Blob([script],{type:'text/plain'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'CreateOrderFolder.bat';
  a.click();
  notify('✓ CreateOrderFolder.bat downloaded — put this on every employee desktop');
}

function downloadPSScript(){
  const script = `# Title Order Folder Creator - PowerShell
# Usage: .\\CreateOrderFolder.ps1 -OrderNum "01-26027784-03T" -EstDate "04-29-2026" -Company "YDeal"
param(
    [string]$OrderNum = "",
    [string]$EstDate  = "",
    [string]$Company  = ""
)
if (-not $OrderNum) { $OrderNum = Read-Host "Enter Order Number" }
if (-not $EstDate)  { $EstDate  = Read-Host "Enter EST Date (MM-DD-YYYY)" }
if (-not $Company)  {
    $choice = Read-Host "Company: 1=YDeal  2=TitlePriority"
    $Company = if ($choice -eq "1") { "YDeal" } else { "TitlePriority" }
}
$Base = "Z:\\Title Orders\\$Company\\$EstDate\\$OrderNum"
@("1 - Plat Map","2 - Assessor","3 - Taxes","4 - Deeds",
  "5 - Mortgage Documents","6 - Judgments","7 - Pacer and Patriot",
  "8 - Typing Report","9 - Supporting Docs") | ForEach-Object {
    New-Item -ItemType Directory -Path "$Base\\$_" -Force | Out-Null
    Write-Host "  Created: $_" -ForegroundColor Green
}
Write-Host "Done: $Base" -ForegroundColor Cyan
Invoke-Item $Base`;
  const blob = new Blob([script],{type:'text/plain'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'CreateOrderFolder.ps1';
  a.click();
  notify('✓ PowerShell script downloaded');
}

// ── UPLOAD SYSTEM ──────────────────────────────────────────────────────
// Store: uploads[orderNum] = { package: { sectionId: [{name,size,type,dataUrl}] }, typing: [{name,size,type,dataUrl}] }
let uploads = {};
let uploadTab = 'all';

const PKG_SECTIONS = [
  {id:'plat',      num:1, name:'Plat Map or GIS Map'},
  {id:'assessor',  num:2, name:'Assessor'},
  {id:'taxes',     num:3, name:'Taxes'},
  {id:'deeds',     num:4, name:'Deeds and Back Chains'},
  {id:'mortgage',  num:5, name:'Mortgage and Related Documents'},
  {id:'judgments', num:6, name:'Judgments'},
  {id:'pacer',     num:7, name:'Pacer and Patriot'},
];

function getUploads(orderNum){
  if(!uploads[orderNum]) uploads[orderNum] = {package:{}, typing:[]};
  return uploads[orderNum];
}

function fileIcon(name){
  const ext = (name||'').split('.').pop().toLowerCase();
  if(['pdf'].includes(ext)) return `<svg class="file-pdf" fill="currentColor" viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8l-6-6zm-1 1.5L18.5 9H13V3.5zM8 17v-1h8v1H8zm0-3v-1h8v1H8zm0-3v-1h5v1H8z"/></svg>`;
  if(['jpg','jpeg','png','gif','tiff','bmp'].includes(ext)) return `<svg class="file-img" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg>`;
  if(['doc','docx'].includes(ext)) return `<svg class="file-doc" fill="currentColor" viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8l-6-6zM13 3.5L18.5 9H13V3.5z"/></svg>`;
  return `<svg class="file-other" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>`;
}

function fmtSize(bytes){
  if(bytes < 1024) return bytes+'B';
  if(bytes < 1048576) return (bytes/1024).toFixed(1)+'KB';
  return (bytes/1048576).toFixed(1)+'MB';
}

function uploadStatus(orderNum){
  const u = getUploads(orderNum);
  const secDone = PKG_SECTIONS.filter(s => (u.package[s.id]||[]).length > 0).length;
  const typingDone = (u.typing||[]).length > 0;
  if(secDone === 0 && !typingDone) return 'pending';
  if(secDone === PKG_SECTIONS.length && typingDone) return 'complete';
  return 'partial';
}

function uploadStatusBadge(status){
  const map = {
    pending:  {cls:'b-pend',   label:'Pending Upload'},
    partial:  {cls:'b-prog',   label:'Partially Uploaded'},
    complete: {cls:'b-done',   label:'Fully Uploaded'},
  };
  const s = map[status]||map.pending;
  return `<span class="badge ${s.cls}">${s.label}</span>`;
}

function setUploadTab(tab){
  uploadTab = tab;
  document.querySelectorAll('.upload-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('utab-'+tab).classList.add('active');
  renderUploads();
}

function renderUploadSummary(){
  const total    = orders.length;
  const pending  = orders.filter(o => uploadStatus(o.orderNum) === 'pending').length;
  const partial  = orders.filter(o => uploadStatus(o.orderNum) === 'partial').length;
  const complete = orders.filter(o => uploadStatus(o.orderNum) === 'complete').length;
  const totalFiles = Object.values(uploads).reduce((sum, u) => {
    const pkgFiles = Object.values(u.package||{}).flat().length;
    const typFiles = (u.typing||[]).length;
    return sum + pkgFiles + typFiles;
  }, 0);
  document.getElementById('upload-summary').innerHTML = `
    <div class="us-card"><div class="us-val">${total}</div><div class="us-lbl">Total Orders</div></div>
    <div class="us-card"><div class="us-val" style="color:var(--text3)">${pending}</div><div class="us-lbl">Pending</div></div>
    <div class="us-card"><div class="us-val" style="color:var(--amber)">${partial}</div><div class="us-lbl">Partial</div></div>
    <div class="us-card"><div class="us-val" style="color:var(--green)">${complete}</div><div class="us-lbl">Complete</div></div>
    <div class="us-card"><div class="us-val" style="color:var(--blue)">${totalFiles}</div><div class="us-lbl">Files Uploaded</div></div>`;
}

function renderUploads(){
  renderUploadSummary();
  const q       = document.getElementById('upload-search').value.toLowerCase();
  const fStatus = document.getElementById('upload-filter-status').value;
  const fType   = document.getElementById('upload-filter-type').value;

  let data = orders.filter(o => {
    if(uploadTab !== 'all' && o.assigned !== uploadTab) return false;
    if(q && ![o.orderNum, o.borrower, o.address, o.county].join(' ').toLowerCase().includes(q)) return false;
    const st = uploadStatus(o.orderNum);
    if(fStatus && st !== fStatus) return false;
    if(fType){
      const u = getUploads(o.orderNum);
      if(fType === 'typing' && (u.typing||[]).length === 0) return false;
      if(fType === 'package' && Object.values(u.package||{}).flat().length === 0) return false;
    }
    return true;
  });

  const list  = document.getElementById('upload-orders-list');
  const empty = document.getElementById('upload-empty');
  list.innerHTML = '';
  empty.style.display = data.length ? 'none' : 'block';

  data.forEach(o => {
    const u   = getUploads(o.orderNum);
    const st  = uploadStatus(o.orderNum);
    const t   = TEAM[o.assigned]||{bg:'#eee',tc:'#333',name:o.assigned};
    const secDone = PKG_SECTIONS.filter(s => (u.package[s.id]||[]).length > 0).length;
    const typDone = (u.typing||[]).length;

    list.innerHTML += `<div class="order-upload-card" id="ouc-${o.orderNum.replace(/[^a-z0-9]/gi,'_')}">
      <div class="ouc-head" onclick="toggleOUC('${o.orderNum}')">
        <div class="ouc-info">
          <div class="ouc-title">${o.orderNum} — ${o.borrower}</div>
          <div class="ouc-sub">${o.orderType} · ${o.county}, ${o.state} · Due: ${o.dueDate?o.dueDate.replace('T',' '):'—'}</div>
        </div>
        <div style="display:flex;align-items:center;gap:8px;flex-shrink:0;flex-wrap:wrap">
          <span class="team-badge" style="background:${t.bg};color:${t.tc}">${o.assigned}</span>
          ${uploadStatusBadge(st)}
          <span style="font-size:11px;color:var(--text3)">${secDone}/7 sections · ${typDone} typing file${typDone!==1?'s':''}</span>
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:14px;height:14px;color:var(--text3);flex-shrink:0"><polyline points="6 9 12 15 18 9"/></svg>
        </div>
      </div>
      <div class="ouc-body" id="ouc-body-${o.orderNum.replace(/[^a-z0-9]/gi,'_')}">
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px">

          <!-- LEFT: Package sections -->
          <div>
            <div style="font-size:12px;font-weight:600;color:var(--text);margin-bottom:10px;display:flex;align-items:center;justify-content:space-between">
              Document Package
              <span style="font-size:11px;font-weight:400;color:${secDone===7?'var(--green)':'var(--text3)'}">${secDone}/7 complete</span>
            </div>
            ${PKG_SECTIONS.map(sec => {
              const files = u.package[sec.id]||[];
              const done  = files.length > 0;
              return `<div class="upload-section">
                <div class="upload-section-title">
                  <span class="upload-section-num" style="${done?'background:var(--green);color:#fff':'background:var(--blue-l);color:var(--blue-t)'}">${sec.num}</span>
                  ${sec.name}
                  ${done ? `<span style="color:var(--green);font-size:10px">✓ ${files.length} file${files.length!==1?'s':''}</span>` : ''}
                </div>
                <div class="file-drop" onclick="triggerUpload('${o.orderNum}','pkg','${sec.id}')"
                  ondragover="ev.preventDefault();this.classList.add('dragover')"
                  ondragleave="this.classList.remove('dragover')"
                  ondrop="handleDropUpload(event,'${o.orderNum}','pkg','${sec.id}')">
                  <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
                  <p>Click or drag files here</p>
                  <input type="file" id="uinput-${o.orderNum.replace(/[^a-z0-9]/gi,'_')}-${sec.id}"
                    multiple accept=".pdf,.jpg,.jpeg,.png,.tiff,.bmp,.doc,.docx,.gif"
                    onchange="handleFileUpload(event,'${o.orderNum}','pkg','${sec.id}')">
                </div>
                ${files.length ? `<div class="uploaded-files">${files.map((f,fi)=>`
                  <div class="uploaded-file">
                    ${fileIcon(f.name)}
                    <span class="fname" title="${f.name}">${f.name}</span>
                    <span class="fsize">${fmtSize(f.size)}</span>
                    <span class="fdel" onclick="removeUploadFile('${o.orderNum}','pkg','${sec.id}',${fi})" title="Remove">✕</span>
                    <a href="${f.dataUrl}" download="${f.name}" class="btn btn-sm" style="padding:2px 7px;font-size:10px" title="Download">⬇</a>
                  </div>`).join('')}</div>` : ''}
              </div>`;
            }).join('')}
          </div>

          <!-- RIGHT: Typing report -->
          <div>
            <div style="font-size:12px;font-weight:600;color:var(--text);margin-bottom:10px;display:flex;align-items:center;justify-content:space-between">
              Typing Report
              <span style="font-size:11px;font-weight:400;color:${typDone>0?'var(--green)':'var(--text3)'}">${typDone} file${typDone!==1?'s':''} uploaded</span>
            </div>
            <div style="background:var(--blue-l);border-radius:var(--r);padding:10px 12px;font-size:11px;color:var(--blue-t);margin-bottom:10px">
              Upload the completed Typing Report (.docx) generated from the Typing Report form. Any supporting documents can also be attached here.
            </div>
            <div class="file-drop" onclick="triggerUpload('${o.orderNum}','typing','report')"
              ondragover="event.preventDefault();this.classList.add('dragover')"
              ondragleave="this.classList.remove('dragover')"
              ondrop="handleDropUpload(event,'${o.orderNum}','typing','report')">
              <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
              <p>Upload Typing Report (.docx, .pdf, etc.)</p>
              <input type="file" id="uinput-${o.orderNum.replace(/[^a-z0-9]/gi,'_')}-typing"
                multiple accept=".pdf,.jpg,.jpeg,.png,.tiff,.bmp,.doc,.docx"
                onchange="handleFileUpload(event,'${o.orderNum}','typing','report')">
            </div>
            ${(u.typing||[]).length ? `<div class="uploaded-files" style="margin-top:8px">${(u.typing||[]).map((f,fi)=>`
              <div class="uploaded-file">
                ${fileIcon(f.name)}
                <span class="fname" title="${f.name}">${f.name}</span>
                <span class="fsize">${fmtSize(f.size)}</span>
                <span class="fdel" onclick="removeUploadFile('${o.orderNum}','typing','report',${fi})" title="Remove">✕</span>
                <a href="${f.dataUrl}" download="${f.name}" class="btn btn-sm" style="padding:2px 7px;font-size:10px" title="Download">⬇</a>
              </div>`).join('')}</div>` : ''}

            <!-- Upload progress & status actions -->
            <div style="margin-top:14px;padding-top:12px;border-top:1px solid var(--border)">
              <div style="font-size:11px;font-weight:600;color:var(--text2);margin-bottom:8px">Update order status</div>
              <div style="display:flex;gap:6px;flex-wrap:wrap">
                <button class="btn btn-sm btn-a" onclick="markStatusFromUpload('${o.orderNum}','Typing Pending')">Typing Pending</button>
                <button class="btn btn-sm btn-p" onclick="markStatusFromUpload('${o.orderNum}','Quality/Final Review')">Quality/Final Review</button>
                <button class="btn btn-sm btn-g" onclick="markStatusFromUpload('${o.orderNum}','Completed')">Completed</button>
                <button class="btn btn-sm" onclick="markStatusFromUpload('${o.orderNum}','Submitted')">Submitted</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>`;
  });
}

function toggleOUC(orderNum){
  const id = orderNum.replace(/[^a-z0-9]/gi,'_');
  const body = document.getElementById('ouc-body-'+id);
  if(body) body.classList.toggle('open');
}

function triggerUpload(orderNum, section, secId){
  const id = orderNum.replace(/[^a-z0-9]/gi,'_');
  const inputId = section === 'typing' ? `uinput-${id}-typing` : `uinput-${id}-${secId}`;
  const el = document.getElementById(inputId);
  if(el) el.click();
}

function handleFileUpload(event, orderNum, section, secId){
  const files = Array.from(event.target.files);
  if(!files.length) return;
  processUploadFiles(files, orderNum, section, secId);
}

function handleDropUpload(event, orderNum, section, secId){
  event.preventDefault();
  event.target.closest('.file-drop')?.classList.remove('dragover');
  const files = Array.from(event.dataTransfer.files);
  if(!files.length) return;
  processUploadFiles(files, orderNum, section, secId);
}

function processUploadFiles(files, orderNum, section, secId){
  const u = getUploads(orderNum);
  let pending = files.length;

  files.forEach(file => {
    const reader = new FileReader();
    reader.onload = (e) => {
      const fileData = { name: file.name, size: file.size, type: file.type, dataUrl: e.target.result };
      if(section === 'typing'){
        if(!u.typing) u.typing = [];
        u.typing.push(fileData);
      } else {
        if(!u.package[secId]) u.package[secId] = [];
        u.package[secId].push(fileData);
      }
      pending--;
      if(pending === 0){
        // Update order status automatically if package complete
        const st = uploadStatus(orderNum);
        if(st === 'complete'){
          const idx = orders.findIndex(o => o.orderNum === orderNum);
          if(idx >= 0 && orders[idx].status === 'Open Order') orders[idx].status = 'Typing Pending';
        }
        renderUploads();
        render();
        notify(`✓ ${files.length} file${files.length!==1?'s':''} uploaded to ${orderNum}`);
      }
    };
    reader.readAsDataURL(file);
  });
}

function removeUploadFile(orderNum, section, secId, fileIdx){
  const u = getUploads(orderNum);
  if(section === 'typing'){
    u.typing.splice(fileIdx, 1);
  } else {
    if(u.package[secId]) u.package[secId].splice(fileIdx, 1);
  }
  renderUploads();
  notify('File removed');
}

function markStatusFromUpload(orderNum, status){
  const idx = orders.findIndex(o => o.orderNum === orderNum);
  if(idx >= 0){ orders[idx].status = status; render(); renderUploads(); notify('Status updated: '+status); }
}

// Also add Upload button to main dashboard row actions
// (patched into render() via the row action HTML)

// ════════════════════════════════════════════════════════════
// AUTH SYSTEM
// ════════════════════════════════════════════════════════════
const USERS = {
  'hb@ydealtitleservices.com':    { pass:'HB@YDeal2024!',  role:'team',  name:'H. Brown',   initials:'HB', color:'#1B4F8A', assignKey:'HB' },
  'hp@ydealtitleservices.com':    { pass:'HP@YDeal2024!',  role:'team',  name:'H. Patel',   initials:'HP', color:'#0E6655', assignKey:'HP' },
  'ybuddh@titlepriority.com':     { pass:'YB@Admin2024!',  role:'admin', name:'Y. Buddh',   initials:'YB', color:'#5B21B6', assignKey:'YB' },
  'yb@ydealtitleservices.com':    { pass:'YB@YDeal2024!',  role:'admin', name:'Y. Bhandari',initials:'YB', color:'#7A4F0D', assignKey:'YB2' },
  'rich_davis@ydealtitleservices.com': { pass:'Rich@Admin2024!', role:'admin', name:'Rich Davis', initials:'RD', color:'#8B2020', assignKey:'RD' },
};

let currentUser = null;

function fillLogin(email, pass){
  document.getElementById('login-email').value = email;
  document.getElementById('login-pass').value  = pass;
  doLogin();
}

function togglePassVis(){
  const inp  = document.getElementById('login-pass');
  const icon = document.getElementById('eye-icon');
  if(inp.type === 'password'){
    inp.type = 'text';
    icon.innerHTML = '<path d="M17.94 17.94A10.07 10.07 0 0112 20c-7 0-11-8-11-8a18.45 18.45 0 015.06-5.94"/><path d="M9.9 4.24A9.12 9.12 0 0112 4c7 0 11 8 11 8a18.5 18.5 0 01-2.16 3.19"/><line x1="1" y1="1" x2="23" y2="23"/>';
  } else {
    inp.type = 'password';
    icon.innerHTML = '<path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/>';
  }
}

function doLogin(){
  const email = document.getElementById('login-email').value.trim().toLowerCase();
  const pass  = document.getElementById('login-pass').value;
  const err   = document.getElementById('login-error');
  const btn   = document.getElementById('login-btn-text');

  if(!email){ err.textContent='Please enter your email address.'; err.classList.add('show'); return; }
  if(!pass){  err.textContent='Please enter your password.';      err.classList.add('show'); return; }

  const u = USERS[email];
  if(!u || u.pass !== pass){
    err.textContent = 'Incorrect email or password. Please check and try again.';
    err.classList.add('show');
    document.getElementById('login-pass').value = '';
    setTimeout(()=>err.classList.remove('show'), 5000);
    return;
  }
  err.classList.remove('show');
  if(btn) btn.textContent = 'Signing in...';
  currentUser = { email, ...u };
  sessionStorage.setItem('tsUser', JSON.stringify(currentUser));
  setTimeout(showApp, 300);
}

function doLogout(){
  currentUser = null;
  sessionStorage.removeItem('tsUser');
  const el = id => document.getElementById(id);
  if(el('main-app'))    el('main-app').style.display   = 'none';
  if(el('comm-fab'))    el('comm-fab').style.display    = 'none';
  if(el('call-overlay'))el('call-overlay').classList.remove('show');
  showMobileNav(false);
  if(el('login-screen'))el('login-screen').style.display = 'flex';
  if(el('login-email')) el('login-email').value = '';
  if(el('login-pass'))  el('login-pass').value  = '';
}

function showApp(){
  const el = id => document.getElementById(id);
  if(el('login-screen'))el('login-screen').style.display = 'none';
  if(el('main-app'))    el('main-app').style.display     = 'flex';
  if(el('comm-fab'))    el('comm-fab').style.display     = 'flex';
  if(isMobile()){ showMobileNav(true); showPWABanner(); }
  initAfterLogin();
}

function initAfterLogin(){
  const u  = currentUser;
  const el = id => document.getElementById(id);
  // Topbar user info
  if(el('topbar-name'))   el('topbar-name').textContent  = u.name;
  if(el('topbar-role')){  el('topbar-role').textContent  = u.role==='admin'?'Admin':'Team Member';
                          el('topbar-role').className    = 'user-role '+(u.role==='admin'?'role-admin':'role-team'); }
  if(el('topbar-avatar')){ el('topbar-avatar').textContent       = u.initials;
                            el('topbar-avatar').style.background  = u.color+'22';
                            el('topbar-avatar').style.color       = u.color; }
  // Hide admin-only columns for team members
  applyRoleVisibility();
  applyMobileRoleVisibility();
  // Re-render with role filter
  populateStates(); render(); renderTmplCols();
  go('dashboard');
  setTimeout(()=>{ autoFill(); onTypeChange(); }, 100);
}

function applyRoleVisibility(){
  const isAdmin = currentUser && currentUser.role === 'admin';
  // Hide fee column and email/return info for team members
  document.querySelectorAll('.admin-only').forEach(el => {
    el.style.display = isAdmin ? '' : 'none';
  });
  // Team members only see their own orders — filter applied in render()
}

function renderWithRoleFilter(data){
  if(!currentUser) return data;
  if(currentUser.role === 'admin') return data;
  // Team members see all orders (not just assigned) — they can see pipeline
  return data;
}

// Check for existing session on load
function checkSession(){
  try {
    const saved = sessionStorage.getItem('tsUser');
    if(saved){
      const u = JSON.parse(saved);
      if(u && u.email && USERS[u.email] && USERS[u.email].pass === u.pass){
        currentUser = { ...USERS[u.email], email: u.email };
        showApp();
        return true;
      } else {
        sessionStorage.removeItem('tsUser');
      }
    }
  } catch(e){ sessionStorage.removeItem('tsUser'); }
  // Show login screen safely
  const ls = document.getElementById('login-screen');
  const ma = document.getElementById('main-app');
  const cf = document.getElementById('comm-fab');
  const mn = document.getElementById('mobile-nav');
  if(ls) ls.style.display = 'flex';
  if(ma) ma.style.display = 'none';
  if(cf) cf.style.display = 'none';
  if(mn) mn.classList.remove('show');
  return false;
}

// Allow Enter key on login form
document.getElementById('login-email')?.addEventListener('keydown', e => {
  if(e.key==='Enter') document.getElementById('login-pass').focus();
});
document.getElementById('login-pass')?.addEventListener('keydown', e => {
  if(e.key==='Enter') doLogin();
});

// ════════════════════════════════════════════════════════════
// COMMUNICATION SYSTEM — Chat + File Attachments + Audio Call
// ════════════════════════════════════════════════════════════

// ── Store ──────────────────────────────────────────────────
// messages keyed by thread id: 'team' or email address
const commMessages = {};
let   commThread   = 'team';   // active thread
let   commFiles    = [];       // pending file attachments
let   commOpen     = false;
let   unreadCounts = {};       // {threadId: count}

// ── Contact list ───────────────────────────────────────────
function getContacts(){
  const contacts = [{ id:'team', label:'Team', initials:'All', color:'#1B4F8A', isGroup:true }];
  Object.entries(USERS).forEach(([email, u]) => {
    if(!currentUser || email !== currentUser.email){
      contacts.push({ id:email, label:u.name.split(' ')[0], initials:u.initials, color:u.color, isGroup:false });
    }
  });
  return contacts;
}

// ── Toggle panel ───────────────────────────────────────────
function toggleComm(){
  commOpen = !commOpen;
  document.getElementById('comm-panel').classList.toggle('open', commOpen);
  if(commOpen){
    unreadCounts[commThread] = 0;
    refreshCommBadge();
    renderContacts();
    renderCommMsgs();
    setTimeout(()=>{ const el=document.getElementById('cp-msg-input'); if(el)el.focus(); },100);
  }
}

function showComm(){ commOpen=false; toggleComm(); }

// ── Contacts strip ─────────────────────────────────────────
function renderContacts(){
  const contacts = getContacts();
  document.getElementById('cp-contacts').innerHTML = contacts.map(c => {
    const unread = unreadCounts[c.id]||0;
    return `<div class="cp-contact ${commThread===c.id?'active':''}" onclick="switchThread('${c.id}')" title="${c.isGroup?'Team group chat':c.label}">
      <div class="cp-contact-av" style="background:${c.color}22;color:${c.color}">
        ${c.initials}
        <span class="online"></span>
        <span class="cp-contact-unread ${unread?'show':''}">${unread||''}</span>
      </div>
      <div class="cp-contact-name">${c.label}</div>
    </div>`;
  }).join('');
  // Show/hide call button — only for DMs
  const isDM = commThread !== 'team';
  const callBtn = document.getElementById('cp-call-btn');
  if(callBtn) callBtn.style.display = isDM ? 'flex' : 'none';
  // Update header title
  const contact = contacts.find(c=>c.id===commThread);
  document.getElementById('cp-title').textContent = contact ? (contact.isGroup?'Team Chat':contact.label) : 'Team Chat';
}

function switchThread(threadId){
  commThread = threadId;
  unreadCounts[threadId] = 0;
  refreshCommBadge();
  renderContacts();
  renderCommMsgs();
  setTimeout(()=>{ const el=document.getElementById('cp-msg-input'); if(el)el.focus(); },50);
}

// ── Render messages ────────────────────────────────────────
function renderCommMsgs(){
  const msgs = commMessages[commThread]||[];
  const el   = document.getElementById('cp-msgs');
  if(!el) return;
  if(!msgs.length){
    const contacts = getContacts();
    const c = contacts.find(x=>x.id===commThread);
    el.innerHTML = `<div class="cp-empty">
      <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>
      ${c&&!c.isGroup ? `Start a conversation with ${c.label}` : 'Send a message to the whole team'}
    </div>`;
    return;
  }

  let html = '';
  let lastDate = '';
  msgs.forEach(m => {
    const isMe = currentUser && m.from === currentUser.email;
    const msgDate = new Date(m.ts).toLocaleDateString('en-US',{month:'short',day:'numeric'});
    if(msgDate !== lastDate){
      html += `<div class="day-divider">${msgDate}</div>`;
      lastDate = msgDate;
    }
    html += `<div class="cp-msg ${isMe?'me':'them'}">
      <div class="cp-msg-meta">${isMe?'You':m.name}</div>
      ${m.text ? `<div class="cp-bubble">${escHtml(m.text)}</div>` : ''}
      ${m.files ? m.files.map(f => renderFileBubble(f, isMe)).join('') : ''}
      <div class="cp-msg-time">${new Date(m.ts).toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit'})}</div>
    </div>`;
  });
  el.innerHTML = html;
  el.scrollTop = el.scrollHeight;
}

function renderFileBubble(f, isMe){
  const ext  = (f.name||'').split('.').pop().toLowerCase();
  const isPdf   = ext==='pdf';
  const isImg   = ['jpg','jpeg','png','gif','bmp','tiff','webp'].includes(ext);
  const isWord  = ['doc','docx'].includes(ext);
  const isExcel = ['xls','xlsx','csv'].includes(ext);

  let iconBg='#F0EEE9', iconColor='#5F5E5A', iconSvg='';
  if(isPdf){  iconBg='#FDEAEA'; iconColor='#DC2626'; iconSvg=`<svg fill="${iconColor}" viewBox="0 0 24 24" style="width:18px;height:18px"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8l-6-6zm4 18H6V4h7v5h5v11z"/></svg>`; }
  else if(isWord){ iconBg='#E6F1FB'; iconColor='#1B4F8A'; iconSvg=`<svg fill="${iconColor}" viewBox="0 0 24 24" style="width:18px;height:18px"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8l-6-6zm1 2l4 4h-4V4zM8 13l1.5-4 1.5 4 1.5-4 1.5 4h-6z"/></svg>`; }
  else if(isExcel){ iconBg='#E8F3EA'; iconColor='#16A34A'; iconSvg=`<svg fill="${iconColor}" viewBox="0 0 24 24" style="width:18px;height:18px"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8l-6-6zm1 2l4 4h-4V4zm-5 9l-2-3h2l1 1.5L12 10h2l-2 3 2 3h-2l-1-1.5-1 1.5H8l2-3z"/></svg>`; }
  else if(isImg){ iconBg='#F0FDF4'; iconColor='#16A34A'; iconSvg=`<svg fill="none" stroke="${iconColor}" stroke-width="2" viewBox="0 0 24 24" style="width:18px;height:18px"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg>`; }
  else { iconSvg=`<svg fill="none" stroke="${iconColor}" stroke-width="2" viewBox="0 0 24 24" style="width:18px;height:18px"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>`; }

  return `<div class="cp-file-bubble" onclick="downloadCommFile('${f.dataUrl}','${escHtml(f.name)}')">
    <div class="cp-file-icon" style="background:${iconBg}">${iconSvg}</div>
    <div class="cp-file-info" style="color:${isMe?'#fff':'var(--text)'}">
      <div class="cp-file-name">${escHtml(f.name)}</div>
      <div class="cp-file-size">${fmtCommSize(f.size)} · Click to download</div>
    </div>
  </div>`;
}

function fmtCommSize(b){ if(!b)return ''; if(b<1024)return b+'B'; if(b<1048576)return (b/1024).toFixed(1)+'KB'; return (b/1048576).toFixed(1)+'MB'; }
function downloadCommFile(dataUrl, name){ const a=document.createElement('a'); a.href=dataUrl; a.download=name; a.click(); }

// ── Send message ───────────────────────────────────────────
function sendCommMsg(){
  if(!currentUser) return;
  const ta   = document.getElementById('cp-msg-input');
  const text = ta ? ta.value.trim() : '';
  if(!text && commFiles.length===0) return;

  const msg = {
    from:  currentUser.email,
    name:  currentUser.name,
    text,
    files: commFiles.length ? [...commFiles] : null,
    ts:    Date.now(),
  };

  if(!commMessages[commThread]) commMessages[commThread] = [];
  commMessages[commThread].push(msg);

  if(ta){ ta.value=''; ta.style.height='auto'; }
  commFiles = [];
  renderFileStrip();
  renderCommMsgs();
}

// ── File attachment ────────────────────────────────────────
function handleCommFile(event){
  const files = Array.from(event.target.files);
  if(!files.length) return;
  let pending = files.length;
  files.forEach(file => {
    const reader = new FileReader();
    reader.onload = e => {
      commFiles.push({ name:file.name, size:file.size, type:file.type, dataUrl:e.target.result });
      pending--;
      if(pending===0) renderFileStrip();
    };
    reader.readAsDataURL(file);
  });
  event.target.value = '';
}

function renderFileStrip(){
  const strip = document.getElementById('cp-file-strip');
  if(!strip) return;
  if(!commFiles.length){ strip.classList.remove('show'); return; }
  strip.classList.add('show');
  strip.innerHTML = commFiles.map((f,i)=>`
    <div class="cp-file-chip">
      <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" style="width:11px;height:11px;flex-shrink:0"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/></svg>
      <span title="${escHtml(f.name)}">${escHtml(f.name)}</span>
      <button onclick="removeCommFile(${i})">✕</button>
    </div>`).join('');
}

function removeCommFile(idx){ commFiles.splice(idx,1); renderFileStrip(); }

// ── Badge ──────────────────────────────────────────────────
function refreshCommBadge(){
  const total = Object.values(unreadCounts).reduce((s,v)=>s+v,0);
  const badge = document.getElementById('comm-badge');
  if(!badge) return;
  if(total>0){ badge.textContent=total>9?'9+':total; badge.style.cssText='position:absolute;top:-2px;right:-2px;width:18px;height:18px;border-radius:50%;background:#DC2626;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;border:2px solid var(--bg)'; }
  else { badge.style.display='none'; }
}

// ── AUDIO CALL SYSTEM (WebRTC) ─────────────────────────────
let callState       = null; // null | 'calling' | 'incoming' | 'active'
let callPeer        = null; // contact object
let callTimer       = null;
let callSeconds     = 0;
let isMuted         = false;
let localStream     = null;
let peerConnection  = null;

function getUserContact(email){
  const u = USERS[email];
  if(!u) return null;
  return { id:email, label:u.name, initials:u.initials, color:u.color };
}

function startCall(){
  if(commThread==='team'){ notify('Select a team member first to start a call'); return; }
  const contact = getUserContact(commThread);
  if(!contact){ notify('Cannot call this contact'); return; }
  callPeer  = contact;
  callState = 'calling';
  showCallOverlay('calling', contact);
  // Request microphone access
  navigator.mediaDevices.getUserMedia({ audio:true, video:false })
    .then(stream => {
      localStream = stream;
      // In a real deployment, you would connect WebRTC peers here via a signalling server.
      // For this demo, simulate the call being answered after 2 seconds.
      setTimeout(()=>{
        if(callState==='calling') connectCall();
      }, 2000);
    })
    .catch(() => {
      // Microphone denied — show simulated call anyway
      setTimeout(()=>{ if(callState==='calling') connectCall(); }, 2000);
    });
}

function showCallOverlay(state, contact){
  const overlay = document.getElementById('call-overlay');
  const av      = document.getElementById('call-avatar');
  const name    = document.getElementById('call-name');
  const status  = document.getElementById('call-status');
  const inBtns  = document.getElementById('call-incoming-btns');
  const actBtns = document.getElementById('call-active-btns');
  const timer   = document.getElementById('call-timer');
  const box     = document.getElementById('call-box');

  av.style.background = contact.color+'22';
  av.style.color      = contact.color;
  av.textContent      = contact.initials;
  name.textContent    = contact.label;
  overlay.classList.add('show');

  if(state==='calling'){
    status.textContent = 'Calling...';
    inBtns.style.display  = 'none';
    actBtns.style.display = 'flex';
    timer.style.display   = 'none';
    box.classList.remove('ringing');
    // Show end button only
    actBtns.querySelector('.call-btn-mute').style.display='none';
  } else if(state==='incoming'){
    status.textContent = 'Incoming call...';
    inBtns.style.display  = 'flex';
    actBtns.style.display = 'none';
    timer.style.display   = 'none';
    box.classList.add('ringing');
  } else if(state==='active'){
    status.textContent = 'Connected';
    inBtns.style.display  = 'none';
    actBtns.style.display = 'flex';
    actBtns.querySelector('.call-btn-mute').style.display='flex';
    timer.style.display   = 'block';
    box.classList.remove('ringing');
    startCallTimer();
  }
}

function connectCall(){
  callState = 'active';
  showCallOverlay('active', callPeer);
}

function acceptCall(){
  callState = 'active';
  showCallOverlay('active', callPeer);
  navigator.mediaDevices.getUserMedia({ audio:true, video:false })
    .then(stream => { localStream = stream; })
    .catch(()=>{});
}

function rejectCall(){
  endCall();
  notify(callPeer ? `Declined call from ${callPeer.label}` : 'Call declined');
}

function endCall(){
  callState = null;
  if(callTimer){ clearInterval(callTimer); callTimer=null; }
  if(localStream){ localStream.getTracks().forEach(t=>t.stop()); localStream=null; }
  callSeconds = 0;
  isMuted     = false;
  document.getElementById('call-overlay').classList.remove('show');
  document.getElementById('call-timer').textContent = '00:00';
  document.getElementById('call-box').classList.remove('ringing');
}

function toggleMute(){
  isMuted = !isMuted;
  const btn = document.getElementById('call-mute-btn');
  if(btn) btn.classList.toggle('muted', isMuted);
  if(localStream) localStream.getAudioTracks().forEach(t=>{ t.enabled=!isMuted; });
  btn.title = isMuted ? 'Unmute' : 'Mute';
}

function startCallTimer(){
  callSeconds = 0;
  if(callTimer) clearInterval(callTimer);
  callTimer = setInterval(()=>{
    callSeconds++;
    const m = String(Math.floor(callSeconds/60)).padStart(2,'0');
    const s = String(callSeconds%60).padStart(2,'0');
    const el = document.getElementById('call-timer');
    if(el) el.textContent = `${m}:${s}`;
  }, 1000);
}

// ── Legacy stubs (keep so nothing breaks) ─────────────────
function toggleChat(){ toggleComm(); }
function openMeetingPanel(){}
function joinRoom(){}
function openWhereby(){}
function closeMeeting(){}
function sendChatMsg(){ sendCommMsg(); }
function handleChatFile(e){ handleCommFile(e); }
function clearChatFilePreview(){ commFiles=[]; renderFileStrip(); }
function setChatTarget(t){ switchThread(t); }
function renderChatUserList(){ renderContacts(); }
function renderChat(){ renderCommMsgs(); }

// ════════════════════════════════════════════════════════════
// QUALIA MARKETPLACE API INTEGRATION
// ════════════════════════════════════════════════════════════

const QUALIA_URL = 'https://marketplace.qualia.com/api/vendor/graphql';
const QUALIA_AUTH = 'Basic eWRsOkZpaldGV0RwRVhDbzRwTzhqOUJ0alYyNkd4SWRGdnRYaFBvaHFyUGl5ZU0=';
let qualiaConfig = { username:'ydl', password:'FijWFWDpEXCo4pO8j9BtjV26GxIdFvtXhPohqrPiyeM', webhook:'https://ydeal144.github.io/title-dashboard/.netlify/functions/qualia-webhook' };
let qualiaWebhookLog = [];
let qualiaFileData = null;
let activeQTab = 'orders';

// Load saved config
function loadQualiaConfig(){
  try {
    const saved = localStorage.getItem('qualiaConfig');
    if(saved){
      const parsed = JSON.parse(saved);
      // Keep credentials but allow webhook to be overridden
      if(parsed.webhook) qualiaConfig.webhook = parsed.webhook;
    }
  } catch(e){}
  const u = document.getElementById('q-username');
  const p = document.getElementById('q-password');
  const w = document.getElementById('q-webhook');
  if(u) u.value = qualiaConfig.username;
  if(p) p.value = qualiaConfig.password;
  if(w) w.value = qualiaConfig.webhook||'';
}

function saveQualiaConfig(){
  qualiaConfig.username = document.getElementById('q-username')?.value||'';
  qualiaConfig.password = document.getElementById('q-password')?.value||'';
  qualiaConfig.webhook  = document.getElementById('q-webhook')?.value||'';
  try { localStorage.setItem('qualiaConfig', JSON.stringify(qualiaConfig)); } catch(e){}
}

function toggleQualiaPass(){
  const inp = document.getElementById('q-password');
  if(inp) inp.type = inp.type==='password' ? 'text' : 'password';
}

function setQTab(tab){
  activeQTab = tab;
  document.querySelectorAll('[id^="qtab-"]').forEach(t=>t.classList.remove('active'));
  document.querySelectorAll('[id^="qpanel-"]').forEach(p=>p.classList.remove('active'));
  document.getElementById('qtab-'+tab)?.classList.add('active');
  document.getElementById('qpanel-'+tab)?.classList.add('active');
}

// Build Basic Auth header — uses pre-built key directly
function qualiaAuthHeader(){
  return QUALIA_AUTH;
}

// Generic GraphQL call
async function qualiaQuery(query, variables={}){
  const res = await fetch(QUALIA_URL, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': qualiaAuthHeader()
    },
    body: JSON.stringify({ query, variables })
  });
  if(!res.ok) throw new Error(`HTTP ${res.status}: ${res.statusText}`);
  const data = await res.json();
  if(data.errors) throw new Error(data.errors.map(e=>e.message).join(', '));
  return data.data;
}

// Test connection
async function testQualiaConnection(){
  const badge = document.getElementById('qualia-status-badge');
  badge.textContent = 'Testing...';
  badge.className = 'badge b-prog';
  try {
    const q = `query { orders { _id product_name customer_name status { open pending } } }`;
    await qualiaQuery(q);
    badge.textContent = 'Connected ✓';
    badge.className = 'badge b-done';
    notify('✓ Qualia API connected successfully');
  } catch(err){
    badge.textContent = 'Connection failed';
    badge.className = 'badge b-err';
    notify('Qualia connection failed: ' + err.message);
  }
}

// Fetch all pending orders
async function qualiaFetchOrders(){
  const el = document.getElementById('qualia-orders-list');
  el.innerHTML = '<div style="padding:20px;text-align:center;color:var(--text3);font-size:12px">Loading orders from Qualia...</div>';
  try {
    const q = `query {
      orders {
        _id product_name customer_name status_label
        created_date due_date address county state
        status { open pending accepted submitted completed cancelled }
        outstanding_tasks
      }
    }`;
    const data = await qualiaQuery(q);
    const orders = data.orders||[];
    if(!orders.length){
      el.innerHTML = '<div class="empty"><p>No orders found in Qualia</p></div>';
      return;
    }
    el.innerHTML = orders.map(o => {
      const st = o.status||{};
      const statusLabel = o.status_label || (st.pending?'Pending':st.open?'Open':st.submitted?'Submitted':st.completed?'Completed':st.cancelled?'Cancelled':'Unknown');
      const badgeCls = st.pending?'b-pend':st.open?'b-prog':st.submitted?'b-done':st.completed?'b-cmpl':'b-pend';
      const tasks = (o.outstanding_tasks||[]);
      return `<div class="order-upload-card" style="margin-bottom:10px">
        <div style="padding:12px 16px;display:flex;align-items:flex-start;justify-content:space-between;gap:10px;flex-wrap:wrap">
          <div style="flex:1;min-width:0">
            <div style="font-size:13px;font-weight:600;color:var(--text);margin-bottom:3px">${o._id} — ${escHtml(o.product_name||'')}</div>
            <div style="font-size:11px;color:var(--text3)">${escHtml(o.customer_name||'')} · ${escHtml(o.address||'')} · ${escHtml(o.county||'')} ${escHtml(o.state||'')}</div>
            ${tasks.length ? `<div style="margin-top:6px;font-size:11px;color:var(--amber)">⚠ ${tasks.length} outstanding task${tasks.length!==1?'s':''}: ${tasks.slice(0,2).map(t=>escHtml(t)).join(', ')}${tasks.length>2?'...':''}</div>` : ''}
          </div>
          <div style="display:flex;align-items:center;gap:7px;flex-shrink:0;flex-wrap:wrap">
            <span class="badge ${badgeCls}">${statusLabel}</span>
            <button class="btn btn-sm btn-g" onclick="qualiaAcceptFromList('${o._id}')">Accept</button>
            <button class="btn btn-sm btn-p" onclick="qualiaImportToBoard('${o._id}','${escHtml(o.product_name||'')}','${escHtml(o.customer_name||'')}','${escHtml(o.address||'')}','${escHtml(o.county||'')}','${escHtml(o.state||'')}')">Import to Dashboard</button>
          </div>
        </div>
      </div>`;
    }).join('');
    notify(`✓ Loaded ${orders.length} order${orders.length!==1?'s':''} from Qualia`);
  } catch(err){
    el.innerHTML = `<div class="empty"><p style="color:var(--red)">Error: ${escHtml(err.message)}</p></div>`;
    notify('Failed to load Qualia orders: ' + err.message);
  }
}

// Accept a single order from the list
async function qualiaAcceptFromList(orderId){
  try {
    await qualiaQuery(`mutation AcceptOrder($input: AcceptOrderInput) { acceptOrder(input: $input) { status } }`,
      { input: { order_id: orderId } });
    notify(`✓ Order ${orderId} accepted in Qualia`);
    qualiaFetchOrders();
  } catch(err){ notify('Accept failed: '+err.message); }
}

// Import a Qualia order into the dashboard order table
function qualiaImportToBoard(id, productName, customerName, address, county, state){
  if(isDuplicateOrder(id)){ notify('⚠ Order '+id+' already in dashboard'); return; }
  const newOrder = {
    sl: orders.length+1,
    company: 'TitlePriority',
    orderNum: id,
    clientNum: '',
    orderDate: new Date().toISOString().split('T')[0],
    dueDate: '',
    orderType: productName || 'Current Owner Search',
    borrower: customerName || '',
    address: address || '',
    county: county || '',
    state: state || '',
    parcel: '',
    status: 'Open Order',
    assigned: 'HB',
    fee: '',
    instructions: '',
    ccrs: false,
    source: 'qualia'
  };
  orders.unshift(newOrder);
  orders.forEach((o,i)=>o.sl=i+1);
  saveOrders();
  render();
  notify('✓ Order '+id+' imported to dashboard');
  go('dashboard');
}

// Fetch a single order by ID
async function qualiaFetchOrder(){
  const id = document.getElementById('q-fetch-id')?.value?.trim();
  const el = document.getElementById('qualia-fetch-result');
  if(!id){ notify('Please enter a Qualia Order ID'); return; }
  el.innerHTML = '<div style="font-size:12px;color:var(--text3)">Fetching...</div>';
  try {
    const q = `query GetOrder($id: ID!) {
      order(_id: $id) {
        order {
          _id product_name customer_name address county state
          primary_document { name _id }
          additional_documents { name _id }
        }
        outstanding_tasks
      }
    }`;
    const data = await qualiaQuery(q, { id });
    const o = data.order;
    el.innerHTML = `<div class="card" style="font-size:12px">
      <div style="font-weight:600;font-size:13px;margin-bottom:10px">${escHtml(o.order.product_name)} — ${escHtml(o.order._id)}</div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:6px 16px;margin-bottom:10px">
        <div><span style="color:var(--text3)">Customer:</span> ${escHtml(o.order.customer_name||'—')}</div>
        <div><span style="color:var(--text3)">Address:</span> ${escHtml(o.order.address||'—')}</div>
        <div><span style="color:var(--text3)">County:</span> ${escHtml(o.order.county||'—')}</div>
        <div><span style="color:var(--text3)">State:</span> ${escHtml(o.order.state||'—')}</div>
      </div>
      ${o.order.primary_document ? `<div style="margin-bottom:6px"><span style="color:var(--text3)">Primary doc:</span> ${escHtml(o.order.primary_document.name)}</div>` : ''}
      ${(o.order.additional_documents||[]).length ? `<div style="margin-bottom:6px"><span style="color:var(--text3)">Additional docs:</span> ${o.order.additional_documents.map(d=>escHtml(d.name)).join(', ')}</div>` : ''}
      ${(o.outstanding_tasks||[]).length ? `<div style="color:var(--amber);margin-top:8px"><strong>Outstanding tasks:</strong><ul style="margin:4px 0 0 16px">${o.outstanding_tasks.map(t=>`<li>${escHtml(t)}</li>`).join('')}</ul></div>` : '<div style="color:var(--green);margin-top:8px">✓ No outstanding tasks</div>'}
      <div style="margin-top:12px">
        <button class="btn btn-sm btn-p" onclick="qualiaImportToBoard('${escHtml(o.order._id)}','${escHtml(o.order.product_name||'')}','${escHtml(o.order.customer_name||'')}','${escHtml(o.order.address||'')}','${escHtml(o.order.county||'')}','${escHtml(o.order.state||'')}')">Import to Dashboard</button>
      </div>
    </div>`;
  } catch(err){
    el.innerHTML = `<div style="color:var(--red);font-size:12px">Error: ${escHtml(err.message)}</div>`;
  }
}

// Order actions: accept / submit / decline / cancel
async function qualiaAction(action){
  const id = document.getElementById('q-action-id')?.value?.trim();
  const el = document.getElementById('qualia-action-result');
  if(!id){ notify('Please enter a Qualia Order ID'); return; }
  const mutations = {
    accept:  `mutation { acceptOrder(input: { order_id: "${id}" }) { status } }`,
    submit:  `mutation { submitOrder(input: { order_id: "${id}" }) { status } }`,
    decline: `mutation { declineOrder(input: { order_id: "${id}" }) { status } }`,
    cancel:  `mutation { cancelOrder(input: { order_id: "${id}" }) { status } }`,
  };
  try {
    const data = await qualiaQuery(mutations[action]);
    const result = data[action+'Order']||data.acceptOrder||data.submitOrder||data.declineOrder||data.cancelOrder;
    const status = result?.status || 'Done';
    el.innerHTML = `<div style="color:var(--green);font-size:12px;padding:8px 12px;background:var(--green-l);border-radius:var(--r)">✓ Order ${action}ed — Status: ${escHtml(status)}</div>`;
    notify(`✓ Order ${id} ${action}ed — ${status}`);
    // Sync status in dashboard if order exists
    const idx = orders.findIndex(o=>o.orderNum===id);
    if(idx>=0){
      const statusMap = {accept:'Open Order',submit:'Submitted',decline:'Declined',cancel:'Cancelled'};
      if(statusMap[action]) orders[idx].status = statusMap[action];
      render();
    }
  } catch(err){
    el.innerHTML = `<div style="color:var(--red);font-size:12px">Error: ${escHtml(err.message)}</div>`;
    notify(`${action} failed: ${err.message}`);
  }
}

// Send message
async function qualiaSendMessage(){
  const id   = document.getElementById('q-action-id')?.value?.trim();
  const text = document.getElementById('q-msg-text')?.value?.trim();
  const from = document.getElementById('q-msg-from')?.value?.trim() || 'YDeal Title Services';
  const el   = document.getElementById('qualia-action-result');
  if(!id||!text){ notify('Please enter Order ID and message text'); return; }
  try {
    await qualiaQuery(
      `mutation SendMessage($input: MessageInput) { sendMessage(input: $input) { success } }`,
      { input: { order_id: id, text, from_name: from } }
    );
    el.innerHTML = `<div style="color:var(--green);font-size:12px;padding:8px 12px;background:var(--green-l);border-radius:var(--r)">✓ Message sent to customer</div>`;
    document.getElementById('q-msg-text').value = '';
    notify('✓ Message sent via Qualia');
  } catch(err){
    el.innerHTML = `<div style="color:var(--red);font-size:12px">Error: ${escHtml(err.message)}</div>`;
  }
}

// File handling for upload
function handleQualiaFileSelect(event){
  const file = event.target.files[0];
  if(!file) return;
  const reader = new FileReader();
  reader.onload = e => {
    qualiaFileData = { name: file.name, base64: e.target.result.split(',')[1] };
    document.getElementById('q-file-label').textContent = `✓ ${file.name}`;
    notify('File ready to upload: ' + file.name);
  };
  reader.readAsDataURL(file);
}

function handleQualiaFileDrop(event){
  event.preventDefault();
  event.target.closest('.file-drop')?.classList.remove('dragover');
  const file = event.dataTransfer.files[0];
  if(!file) return;
  document.getElementById('q-file-upload').files = event.dataTransfer.files;
  handleQualiaFileSelect({ target: { files: event.dataTransfer.files } });
}

// Upload file to Qualia order
async function qualiaUploadFile(){
  const id = document.getElementById('q-action-id')?.value?.trim();
  const el = document.getElementById('qualia-action-result');
  if(!id){ notify('Please enter a Qualia Order ID'); return; }
  if(!qualiaFileData){ notify('Please select a file to upload'); return; }
  const isPrimary = document.getElementById('q-file-primary')?.value === 'true';
  try {
    await qualiaQuery(
      `mutation AddFiles($input: AddFilesInput) { addFiles(input: $input) { outstanding_tasks } }`,
      { input: { order_id: id, files: [{ name: qualiaFileData.name, is_primary: isPrimary, base_64: qualiaFileData.base64 }] } }
    );
    el.innerHTML = `<div style="color:var(--green);font-size:12px;padding:8px 12px;background:var(--green-l);border-radius:var(--r)">✓ File "${escHtml(qualiaFileData.name)}" uploaded to order ${id}</div>`;
    document.getElementById('q-file-label').textContent = 'Click or drag file here';
    qualiaFileData = null;
    notify('✓ File uploaded to Qualia');
  } catch(err){
    el.innerHTML = `<div style="color:var(--red);font-size:12px">Error: ${escHtml(err.message)}</div>`;
  }
}

// Webhook log
function qualiaLogWebhook(payload){
  qualiaWebhookLog.unshift({ ts: Date.now(), payload });
  if(qualiaWebhookLog.length > 50) qualiaWebhookLog.pop();
  renderWebhookLog();
}

function renderWebhookLog(){
  const el = document.getElementById('qualia-webhook-log');
  if(!el) return;
  if(!qualiaWebhookLog.length){
    el.innerHTML = '<div class="empty"><svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M18 20V10M12 20V4M6 20v-6"/></svg><p>No webhook events received yet</p></div>';
    return;
  }
  el.innerHTML = qualiaWebhookLog.map(e => {
    const p = e.payload;
    const typeColor = p.type==='order_request'?'var(--blue)':p.type==='order_completed'?'var(--green)':p.type==='order_cancelled'?'var(--red)':'var(--amber)';
    return `<div style="padding:10px 14px;border:1px solid var(--border);border-radius:var(--r);margin-bottom:7px;font-size:12px">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:5px">
        <span style="font-weight:600;color:${typeColor}">${escHtml(p.type||'event')}</span>
        <span style="font-size:10px;color:var(--text3)">${new Date(e.ts).toLocaleString()}</span>
      </div>
      <div style="color:var(--text2)">${escHtml(p.description||'')}</div>
      ${p.order_id ? `<div style="margin-top:4px;font-size:11px;color:var(--text3)">Order ID: ${escHtml(p.order_id)}
        <button class="btn btn-sm" onclick="document.getElementById('q-action-id').value='${escHtml(p.order_id)}';setQTab('submit')" style="margin-left:8px;padding:1px 8px;font-size:10px">Take action</button>
      </div>` : ''}
    </div>`;
  }).join('');
}

function qualiaClearWebhookLog(){ qualiaWebhookLog=[]; renderWebhookLog(); }
function qualiaClearLog(){ document.getElementById('qualia-orders-list').innerHTML='<div class="empty"><p>Click "Refresh from Qualia" to load orders</p></div>'; }

function updateWebhookUrl(baseUrl){
  const clean = (baseUrl||'').trim().replace(/\/$/, '');
  const full  = clean ? clean : 'https://YOUR-NETLIFY-URL.netlify.app';
  const el = document.getElementById('webhook-url-display');
  if(el) el.textContent = full;
  qualiaConfig.webhook = full;
  const wInput = document.getElementById('q-webhook');
  if(wInput) wInput.value = full;
  saveQualiaConfig();
}

function copyWebhookUrl(){
  const el = document.getElementById('webhook-url-display');
  const url = el ? el.textContent : '';
  if(!url || url.includes('YOUR-NETLIFY')) { notify('Please enter your Netlify URL first'); return; }
  navigator.clipboard.writeText(url).then(()=>notify('✓ Webhook URL copied to clipboard')).catch(()=>{
    const ta = document.createElement('textarea');
    ta.value = url; document.body.appendChild(ta); ta.select();
    document.execCommand('copy'); document.body.removeChild(ta);
    notify('✓ Webhook URL copied');
  });
}

function qualiaSimulateWebhook(){
  const types = ['order_request','order_cancelled','order_completed','order_revision_requested','message'];
  const type  = types[Math.floor(Math.random()*types.length)];
  const msgs  = {
    order_request:           "You've received an order for a Current Owner Search in Nashville, TN",
    order_cancelled:         "Old Republic Title has cancelled order #TP-2026-0042",
    order_completed:         "Old Republic Title has accepted order #TP-2026-0041",
    order_revision_requested:"Old Republic Title has requested a revision on order #TP-2026-0040",
    message:                 "Marty McFly sent you a message"
  };
  qualiaLogWebhook({ type, description: msgs[type], order_id: 'TEST-'+Date.now() });
  notify('Test webhook event simulated: '+type);
}
// ════════════════════════════════════════════════════════════
// MOBILE / PWA SYSTEM
// ════════════════════════════════════════════════════════════
const isMobile = () => window.innerWidth <= 768;

function initPWA(){
  const manifest = {
    name:'Title Order Dashboard', short_name:'Title Orders',
    description:'YDeal Title Services & Title Priority Order Management',
    start_url:'/', display:'standalone',
    background_color:'#ffffff', theme_color:'#1B4F8A', orientation:'portrait',
    icons:[{ src:"data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 192 192'><rect width='192' height='192' fill='%231B4F8A' rx='32'/><path fill='white' d='M48 60h96v16H48zm0 28h96v16H48zm0 28h64v16H48z'/></svg>", sizes:'192x192', type:'image/svg+xml' }]
  };
  try {
    const blob = new Blob([JSON.stringify(manifest)],{type:'application/json'});
    document.getElementById('pwa-manifest').href = URL.createObjectURL(blob);
  } catch(e){}
}

function showMobileNav(show){
  const nav = document.getElementById('mobile-nav');
  if(show) nav.classList.add('show');
  else nav.classList.remove('show');
}

function mobileGo(page){
  go(page);
  document.querySelectorAll('.mnav-item').forEach(i=>i.classList.remove('active'));
  const map={dashboard:'mnav-dashboard',uploads:'mnav-uploads',typing:'mnav-typing'};
  if(map[page]) document.getElementById(map[page])?.classList.add('active');
  const mm=document.getElementById('mobile-more-menu');
  if(mm && mm.style.display!=='none') toggleMobileMenu();
}

function toggleMobileMenu(){
  const mm=document.getElementById('mobile-more-menu');
  const ov=document.getElementById('mobile-more-overlay');
  const open=mm.style.display==='none';
  mm.style.display=open?'block':'none';
  ov.style.display=open?'block':'none';
  document.getElementById('mnav-more')?.classList.toggle('active',open);
}

function showPWABanner(){
  if(!isMobile()) return;
  if(localStorage.getItem('pwaDismissed')) return;
  const isIOS=/iphone|ipad|ipod/i.test(navigator.userAgent);
  const isAndroid=/android/i.test(navigator.userAgent);
  if(isIOS||isAndroid) setTimeout(()=>document.getElementById('pwa-banner')?.classList.add('show'),4000);
}

function applyMobileRoleVisibility(){
  const isAdmin=currentUser&&currentUser.role==='admin';
  ['mmb-team','mmb-qualia','mmb-new','mmb-import'].forEach(id=>{
    const el=document.getElementById(id);
    if(el) el.style.display=isAdmin?'flex':'none';
  });
}

window.addEventListener('resize',()=>{ if(currentUser) showMobileNav(isMobile()); });

// ════════════════════════════════════════════════════════════
// INIT — runs after DOM is fully loaded
// ════════════════════════════════════════════════════════════
document.addEventListener('DOMContentLoaded', function(){
  initPWA();
  if(!checkSession()){
    populateStates(); renderTmplCols();
  }
});
</script>
</body>
</html>
