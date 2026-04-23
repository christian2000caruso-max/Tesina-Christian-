<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Tesina Christian V4</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Share+Tech+Mono&family=Exo+2:wght@300;400;600&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{--b:#00aaff;--bb:#33ccff;--bd:#0066cc;--bg:#000d1a;--glow:rgba(0,170,255,.35);--w:#e8f4ff;--dim:#7ab8d4;--gold:#c9a227}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--w);font-family:'Exo 2',sans-serif;overflow-x:hidden}
::-webkit-scrollbar{width:5px}
::-webkit-scrollbar-thumb{background:var(--bd);border-radius:3px}

/* ── GLOBAL MATRIX BG ── */
#mx{position:fixed;inset:0;z-index:0;opacity:.5;pointer-events:none}
#sl{position:fixed;inset:0;z-index:9999;pointer-events:none;
  background:repeating-linear-gradient(to bottom,transparent 0,transparent 3px,rgba(0,120,255,.04) 3px,rgba(0,120,255,.04) 4px)}

/* ── SCREENS ── */
.screen{position:fixed;inset:0;z-index:10;overflow-y:auto;overflow-x:hidden;
  opacity:0;pointer-events:none;transition:opacity .6s}
.screen.active{opacity:1;pointer-events:all}

/* ── BLACK TRANSITION ── */
#tblack{position:fixed;inset:0;z-index:600;background:#000;
  opacity:0;pointer-events:none;transition:opacity .7s}
#tblack.on{opacity:1;pointer-events:all}
#tblack.show-content{display:flex;flex-direction:column;align-items:center;justify-content:center}

/* ── INTRO ── */
#scIntro{background:linear-gradient(180deg,#000d1a,#001833)}
.hc{position:absolute;width:50px;height:50px;border-color:var(--b);border-style:solid}
.hc.tl{top:18px;left:18px;border-width:1px 0 0 1px}
.hc.tr{top:18px;right:18px;border-width:1px 1px 0 0}
.hc.bl{bottom:18px;left:18px;border-width:0 0 1px 1px}
.hc.br{bottom:18px;right:18px;border-width:0 1px 1px 0}
.intro-wrap{display:flex;flex-direction:column;align-items:center;justify-content:center;
  min-height:100vh;gap:24px;position:relative;z-index:2}
.prod{font-family:'Share Tech Mono',monospace;font-size:.6rem;letter-spacing:7px;
  color:var(--gold);text-shadow:0 0 12px rgba(201,162,39,.6);animation:fup 1.4s .2s both}
.mtitle{font-family:'Orbitron',sans-serif;font-size:clamp(3rem,10vw,7rem);font-weight:900;
  letter-spacing:.12em;text-transform:uppercase;text-shadow:0 0 40px var(--glow);
  animation:tin 1.8s .5s both;position:relative}
.mtitle::after{content:'';display:block;height:2px;width:0;
  background:linear-gradient(90deg,transparent,var(--bb),transparent);margin-top:10px;
  animation:lg 1.4s 2.2s forwards}
@keyframes lg{to{width:100%}}
@keyframes tin{from{opacity:0;letter-spacing:.4em;filter:blur(6px)}to{opacity:1;letter-spacing:.12em;filter:blur(0)}}
@keyframes fup{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.sysline{font-family:'Share Tech Mono',monospace;font-size:.58rem;letter-spacing:3px;
  color:rgba(51,204,255,.5);min-height:1.2em}
.cur{display:inline-block;width:7px;height:.85em;background:var(--bb);
  vertical-align:middle;animation:bl .7s step-end infinite}
@keyframes bl{0%,100%{opacity:1}50%{opacity:0}}
#btnS{padding:14px 50px;background:transparent;border:1px solid var(--b);
  color:var(--bb);font-family:'Orbitron',sans-serif;font-size:.72rem;
  letter-spacing:5px;text-transform:uppercase;cursor:pointer;position:relative;
  overflow:hidden;animation:fup 1.4s 1.2s both;
  clip-path:polygon(10px 0%,100% 0%,calc(100% - 10px) 100%,0% 100%);transition:color .3s,box-shadow .3s}
#btnS::before{content:'';position:absolute;inset:0;background:linear-gradient(90deg,var(--bd),var(--b));
  transform:scaleX(0);transform-origin:left;transition:transform .35s;z-index:-1}
#btnS:hover{color:#fff;box-shadow:0 0 30px var(--glow)}
#btnS:hover::before{transform:scaleX(1)}

/* ── HERO SECTION ── */
.hero{position:relative;min-height:100vh;display:flex;align-items:center;justify-content:center;overflow:hidden}
.hw{transform:scale(2.5);opacity:0;filter:blur(10px) brightness(0);z-index:2}
.hw.zi{animation:heroZ 4s cubic-bezier(.16,1,.3,1) forwards}
@keyframes heroZ{0%{transform:scale(2.5);opacity:0;filter:blur(10px) brightness(0)}
  15%{opacity:.25;filter:blur(4px) brightness(.3)}
  100%{transform:scale(1);opacity:1;filter:blur(0) brightness(1)}}
.hcanvas{width:min(88vw,500px);height:auto;filter:drop-shadow(0 0 18px rgba(0,170,255,.55))}
.beam{position:absolute;left:0;right:0;height:3px;top:0;z-index:5;
  background:linear-gradient(90deg,transparent,var(--bb),transparent);
  box-shadow:0 0 20px var(--b);opacity:0}
.beam.go{animation:bd 3.2s linear .2s forwards}
@keyframes bd{0%{top:0;opacity:.9}100%{top:100%;opacity:0}}
.hfade{position:absolute;bottom:0;left:0;right:0;height:200px;
  background:linear-gradient(transparent,var(--bg));z-index:3;pointer-events:none}

/* ── FIXED TITLE OVERLAYS ── */
.ftitle{position:fixed;font-family:'Orbitron',sans-serif;font-weight:900;
  text-transform:uppercase;pointer-events:none;z-index:50;
  color:transparent;opacity:0;white-space:nowrap}
.ftitle.top-right{top:22px;right:22px;text-align:right}
.ftitle.top-left{top:22px;left:22px}
.ftitle.center{top:50%;left:50%;transform:translate(-50%,-50%);text-align:center;white-space:normal}
.ftitle.active-title{opacity:1;transition:none}
.flash-anim{animation:tf 1.1s steps(1) forwards}
.move-right{animation:tmvR .9s cubic-bezier(.4,0,.2,1) forwards}
.move-left{animation:tmvL .9s cubic-bezier(.4,0,.2,1) forwards}
@keyframes tf{0%{opacity:0;color:transparent}8%{opacity:1;color:var(--bb);text-shadow:0 0 80px var(--bb),0 0 160px var(--b);letter-spacing:.35em}16%{opacity:0}27%{opacity:1;color:#fff;text-shadow:0 0 60px var(--b);letter-spacing:.08em}35%{opacity:0;letter-spacing:.28em}46%{opacity:1;color:var(--bb);text-shadow:0 0 100px var(--bb)}62%{color:#fff}100%{opacity:1;color:#fff;text-shadow:0 0 20px var(--glow)}}
@keyframes tmvR{to{top:22px;left:auto;right:22px;transform:none;font-size:clamp(.6rem,1.5vw,.9rem);letter-spacing:.2em;color:var(--gold);text-shadow:0 0 12px rgba(201,162,39,.7)}}
@keyframes tmvL{to{top:22px;left:22px;right:auto;transform:none;font-size:clamp(.55rem,1.4vw,.85rem);letter-spacing:.18em;color:var(--gold);text-shadow:0 0 12px rgba(201,162,39,.7)}}

/* ── LE PROTESI center text ── */
#lpHero{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);
  z-index:6;text-align:center;opacity:0;pointer-events:none;
  transition:opacity 1s,transform 1s;transform:translate(-50%,-45%)}
#lpHero.on{opacity:1;transform:translate(-50%,-50%)}
#lpHero .lpsub{display:block;font-family:'Share Tech Mono',monospace;font-size:.55rem;
  letter-spacing:6px;color:var(--b);margin-bottom:8px}
#lpHero .lptitle{display:block;font-family:'Orbitron',sans-serif;font-size:clamp(1.8rem,5.5vw,3.8rem);
  font-weight:900;letter-spacing:.22em;text-transform:uppercase;
  color:#fff;text-shadow:0 0 30px var(--glow)}

/* ── SECTIONS ── */
.sec{max-width:900px;margin:0 auto;padding:60px 28px 28px;position:relative;z-index:10}
.stag{font-family:'Share Tech Mono',monospace;font-size:.58rem;letter-spacing:6px;
  color:var(--b);text-transform:uppercase;margin-bottom:10px;
  display:flex;align-items:center;gap:10px}
.stag::before{content:'';width:28px;height:1px;background:var(--b)}
.sec h2{font-family:'Orbitron',sans-serif;font-size:clamp(1.4rem,3.5vw,2.4rem);
  font-weight:700;color:var(--bb);text-shadow:0 0 28px var(--glow);margin-bottom:22px;line-height:1.2}
.sec p{font-size:.97rem;line-height:1.82;color:var(--dim);margin-bottom:14px}
.sec p strong{color:var(--bb)}
.divider{height:1px;background:linear-gradient(90deg,transparent,var(--bd),transparent);
  margin:50px auto;max-width:900px}
.rv{opacity:0;transform:translateY(26px);transition:opacity .7s,transform .7s}
.rv.vis{opacity:1;transform:none}

/* CARDS */
.cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:16px;margin-top:24px}
.card{background:rgba(0,30,60,.7);border:1px solid rgba(0,120,255,.25);border-top:2px solid var(--b);
  padding:20px 18px;position:relative;
  clip-path:polygon(0 0,calc(100% - 10px) 0,100% 10px,100% 100%,10px 100%,0 calc(100% - 10px));
  transition:border-color .3s,box-shadow .3s,transform .3s}
.card:hover{border-color:var(--bb);box-shadow:0 0 20px var(--glow);transform:translateY(-4px)}
.cn{font-family:'Orbitron',sans-serif;font-size:2rem;font-weight:900;
  color:rgba(0,170,255,.12);position:absolute;top:10px;right:14px}
.ci{font-size:1.6rem;margin-bottom:8px}
.card h3{font-family:'Orbitron',sans-serif;font-size:.78rem;color:var(--bb);
  letter-spacing:2px;text-transform:uppercase;margin-bottom:7px}
.card p{font-size:.84rem;color:var(--dim);line-height:1.62;margin:0}

/* 3D ARM */
#armbox{background:rgba(0,10,28,.97);border:1px solid rgba(0,150,255,.35);
  border-top:2px solid var(--bb);overflow:hidden;margin-top:28px;
  clip-path:polygon(0 0,calc(100% - 14px) 0,100% 14px,100% 100%,14px 100%,0 calc(100% - 14px))}
.awh{background:rgba(0,20,50,.9);padding:12px 20px;border-bottom:1px solid rgba(0,100,200,.2);
  font-family:'Orbitron',sans-serif;font-size:.7rem;letter-spacing:4px;color:var(--bb)}
#armwrap{position:relative;width:100%;height:340px;cursor:grab;user-select:none;touch-action:none}
#armwrap:active{cursor:grabbing}
#ac{width:100%;height:100%;display:block}
.ahint{position:absolute;bottom:8px;left:50%;transform:translateX(-50%);
  font-family:'Share Tech Mono',monospace;font-size:.58rem;letter-spacing:3px;
  color:rgba(0,200,255,.45);pointer-events:none;white-space:nowrap}
.actrl{padding:14px 18px;border-top:1px solid rgba(0,100,200,.2);display:flex;flex-direction:column;gap:10px}
.ast{font-family:'Share Tech Mono',monospace;font-size:.58rem;letter-spacing:3px;color:rgba(0,200,255,.5)}
.arow{display:flex;gap:10px;flex-wrap:wrap}
.abtn{flex:1;min-width:100px;padding:11px 14px;background:rgba(0,20,55,.8);
  border:1px solid var(--bd);color:var(--bb);font-family:'Orbitron',sans-serif;
  font-size:.65rem;letter-spacing:3px;text-transform:uppercase;cursor:pointer;
  clip-path:polygon(6px 0%,100% 0%,calc(100% - 6px) 100%,0% 100%);transition:all .25s}
.abtn:hover,.abtn.act{background:rgba(0,80,200,.35);border-color:var(--bb);box-shadow:0 0 14px var(--glow)}
.sub{display:none;flex-wrap:wrap;gap:8px;padding:10px 12px;
  background:rgba(0,10,30,.8);border:1px solid rgba(0,80,180,.2)}
.sub.show{display:flex}
.fbtn,.actbtn{padding:9px 13px;background:rgba(0,15,40,.9);
  border:1px solid rgba(0,100,200,.35);color:var(--dim);
  font-family:'Share Tech Mono',monospace;font-size:.62rem;letter-spacing:2px;
  cursor:pointer;clip-path:polygon(5px 0%,100% 0%,calc(100% - 5px) 100%,0% 100%);transition:all .2s}
.fbtn:hover,.fbtn.sel{border-color:var(--bb);color:#fff;background:rgba(0,60,160,.4);box-shadow:0 0 10px var(--glow)}
.actbtn{background:rgba(0,30,80,.8);border-color:var(--b);color:var(--bb);font-size:.68rem;padding:10px 18px}
.actbtn:hover{background:rgba(0,80,200,.3);box-shadow:0 0 14px var(--glow)}

/* SPORT GRID */
.sgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(145px,1fr));gap:14px;margin-top:24px}
.sbtn{background:rgba(0,20,50,.8);border:1px solid rgba(0,120,255,.3);
  color:var(--bb);font-family:'Orbitron',sans-serif;font-size:.65rem;
  letter-spacing:3px;text-transform:uppercase;padding:14px 10px;
  cursor:pointer;clip-path:polygon(8px 0%,100% 0%,calc(100% - 8px) 100%,0% 100%);
  transition:all .3s;display:flex;flex-direction:column;align-items:center;gap:8px}
.sbtn:hover{border-color:var(--bb);box-shadow:0 0 18px var(--glow);color:#fff;transform:translateY(-3px)}
.si{font-size:1.9rem}

/* TIMELINE */
.tl{margin-top:24px;position:relative}
.tl::before{content:'';position:absolute;left:18px;top:0;bottom:0;width:1px;
  background:linear-gradient(to bottom,var(--bb),transparent)}
.ti{position:relative;padding:0 0 22px 46px;cursor:pointer}
.td{position:absolute;left:11px;top:4px;width:14px;height:14px;border-radius:50%;
  background:var(--bd);border:2px solid var(--bb);box-shadow:0 0 8px var(--glow);transition:all .3s}
.ti:hover .td,.ti.act .td{background:var(--bb);box-shadow:0 0 18px var(--bb)}
.ty{font-family:'Orbitron',sans-serif;font-size:.7rem;color:var(--b);letter-spacing:3px;margin-bottom:3px}
.tt{font-size:.9rem;font-weight:600;color:var(--w);margin-bottom:4px}
.tx{font-size:.83rem;color:var(--dim);line-height:1.55;max-height:0;overflow:hidden;transition:max-height .4s}
.ti.act .tx{max-height:200px}

/* NEURON TOUCH */
.nwrap{background:rgba(0,8,25,.97);border:1px solid rgba(0,150,255,.35);
  border-top:2px solid var(--bb);overflow:hidden;margin-top:24px;
  clip-path:polygon(0 0,calc(100% - 12px) 0,100% 12px,100% 100%,12px 100%,0 calc(100% - 12px))}
.nwh{background:rgba(0,20,50,.9);padding:12px 20px;border-bottom:1px solid rgba(0,100,200,.2);
  font-family:'Orbitron',sans-serif;font-size:.68rem;letter-spacing:4px;color:var(--bb)}
.ncwrap{position:relative;width:100%;height:min(55vw,360px);touch-action:none;overflow:hidden}
.ncwrap img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:.55;pointer-events:none}
.ncwrap canvas{position:absolute;inset:0;width:100%;height:100%}
.nhint{position:absolute;bottom:8px;left:50%;transform:translateX(-50%);
  font-family:'Share Tech Mono',monospace;font-size:.58rem;letter-spacing:3px;
  color:rgba(0,200,255,.45);pointer-events:none;white-space:nowrap}

/* STAT BARS */
.bars{display:flex;flex-direction:column;gap:12px;margin-top:22px}
.brow{display:flex;flex-direction:column;gap:5px}
.blbl{display:flex;justify-content:space-between;font-family:'Share Tech Mono',monospace;font-size:.68rem;color:var(--b);letter-spacing:2px}
.btrack{height:5px;background:rgba(0,50,100,.4);border-radius:3px;overflow:hidden}
.bfill{height:100%;width:0;border-radius:3px;background:linear-gradient(90deg,var(--bd),var(--bb));
  box-shadow:0 0 8px var(--glow);transition:width 1.4s cubic-bezier(.4,0,.2,1)}

/* STEPS */
.steps{display:flex;flex-direction:column;gap:12px;margin-top:22px}
.step{display:flex;gap:16px;background:rgba(0,15,40,.6);border:1px solid rgba(0,100,200,.2);
  padding:14px 18px;clip-path:polygon(0 0,calc(100% - 8px) 0,100% 8px,100% 100%,0 100%);transition:border-color .3s}
.step:hover{border-color:var(--b)}
.sn{font-family:'Orbitron',sans-serif;font-size:1rem;font-weight:900;color:var(--bb);min-width:32px;line-height:1.5}
.stxt div{font-size:.9rem;line-height:1.65;color:var(--dim)}
.stxt div strong{color:var(--bb)}

/* INFOBOX */
.infobox{background:rgba(0,15,40,.85);border:1px solid rgba(0,120,255,.28);border-left:3px solid var(--bb);padding:18px 22px;margin-top:22px}
.irow{display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:1px solid rgba(0,100,200,.1);flex-wrap:wrap;gap:6px}
.irow:last-child{border:none}
.ilbl{font-family:'Share Tech Mono',monospace;font-size:.7rem;letter-spacing:2px;color:var(--b);text-transform:uppercase}
.ival{font-size:.88rem;color:var(--w)}
.ival strong{color:var(--bb)}

/* POPUP GRID */
.pgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(145px,1fr));gap:13px;margin-top:24px}
.pbtn{background:rgba(0,20,50,.8);border:1px solid rgba(0,120,255,.3);color:var(--bb);
  font-family:'Orbitron',sans-serif;font-size:.62rem;letter-spacing:3px;text-transform:uppercase;
  padding:16px 10px;cursor:pointer;clip-path:polygon(8px 0%,100% 0%,calc(100% - 8px) 100%,0% 100%);
  transition:all .3s;display:flex;flex-direction:column;align-items:center;gap:8px}
.pbtn:hover{border-color:var(--bb);box-shadow:0 0 18px var(--glow);color:#fff;transform:translateY(-3px)}
.pi{font-size:1.8rem}

/* QUIZ */
.qbox{background:rgba(0,12,32,.9);border:1px solid rgba(0,120,255,.3);border-left:3px solid var(--bb);
  padding:24px 22px;margin-top:24px;clip-path:polygon(0 0,calc(100% - 10px) 0,100% 10px,100% 100%,0 100%)}
.qbox h3{font-family:'Orbitron',sans-serif;font-size:.72rem;letter-spacing:3px;color:var(--bb);text-transform:uppercase;margin-bottom:11px}
.qq{font-size:.93rem;color:var(--w);margin-bottom:13px;line-height:1.5}
.qopts{display:flex;flex-direction:column;gap:8px}
.qo{background:rgba(0,20,50,.7);border:1px solid rgba(0,100,200,.3);color:var(--dim);
  font-size:.87rem;padding:10px 15px;cursor:pointer;text-align:left;
  clip-path:polygon(6px 0%,100% 0%,calc(100% - 6px) 100%,0% 100%);transition:all .2s}
.qo:hover{border-color:var(--b);color:var(--w)}
.qo.ok{border-color:#00ff88;color:#00ff88;background:rgba(0,80,40,.4);pointer-events:none}
.qo.ko{border-color:#ff4444;color:#ff4444;background:rgba(80,0,0,.4);pointer-events:none}
.qfb{display:none;margin-top:11px;padding:10px 14px;font-family:'Share Tech Mono',monospace;font-size:.76rem;border-radius:2px}
.qfb.show{display:block}
.qfb.ok{background:rgba(0,80,40,.3);color:#00ff88;border:1px solid #00ff88}
.qfb.ko{background:rgba(80,0,0,.3);color:#ff6666;border:1px solid #ff4444}
.qnx{display:none;margin-top:11px;background:transparent;border:1px solid var(--b);
  color:var(--bb);font-family:'Orbitron',sans-serif;font-size:.65rem;letter-spacing:3px;
  padding:8px 22px;cursor:pointer;clip-path:polygon(7px 0%,100% 0%,calc(100% - 7px) 100%,0% 100%);transition:all .2s}
.qnx:hover{background:rgba(0,100,200,.2)}
.qnx.show{display:inline-block}

/* PROSEGUI BUTTON */
.pgbtn{padding:16px 60px;background:transparent;border:1px solid var(--bb);
  color:var(--bb);font-family:'Orbitron',sans-serif;font-size:.95rem;
  letter-spacing:5px;text-transform:uppercase;cursor:pointer;position:relative;
  overflow:hidden;clip-path:polygon(13px 0%,100% 0%,calc(100% - 13px) 100%,0% 100%);
  transition:color .3s;animation:pgpulse 2s ease-in-out infinite}
.pgbtn::before{content:'';position:absolute;inset:0;background:linear-gradient(90deg,var(--bd),var(--b));
  transform:scaleX(0);transform-origin:left;transition:transform .4s;z-index:-1}
.pgbtn:hover{color:#fff}
.pgbtn:hover::before{transform:scaleX(1)}
@keyframes pgpulse{0%,100%{box-shadow:0 0 10px var(--glow)}50%{box-shadow:0 0 28px var(--bb),0 0 50px var(--glow)}}

/* MODAL */
#ov{position:fixed;inset:0;z-index:1200;background:rgba(0,5,15,.88);backdrop-filter:blur(8px);
  display:flex;align-items:center;justify-content:center;opacity:0;pointer-events:none;transition:opacity .3s;padding:20px}
#ov.open{opacity:1;pointer-events:all}
.mbox{background:linear-gradient(135deg,#001428,#001e3c);border:1px solid var(--bd);border-top:2px solid var(--bb);
  max-width:560px;width:100%;max-height:80vh;overflow-y:auto;padding:30px 26px;position:relative;
  clip-path:polygon(0 0,calc(100% - 16px) 0,100% 16px,100% 100%,16px 100%,0 calc(100% - 16px));
  box-shadow:0 0 50px var(--glow);transform:scale(.9) translateY(16px);transition:transform .3s}
#ov.open .mbox{transform:scale(1) translateY(0)}
.mtag{font-family:'Share Tech Mono',monospace;font-size:.56rem;letter-spacing:5px;color:var(--b);text-transform:uppercase;margin-bottom:5px}
.mico{font-size:2rem;margin-bottom:6px}
.mbox h2{font-family:'Orbitron',sans-serif;font-size:1.3rem;color:var(--bb);margin-bottom:14px;text-shadow:0 0 16px var(--glow)}
.mbox p{font-size:.9rem;line-height:1.72;color:var(--dim);margin-bottom:11px}
.mbox p strong{color:var(--bb)}
.mbox ul{list-style:none;margin:8px 0}
.mbox li{font-size:.86rem;color:var(--dim);padding:6px 0 6px 18px;border-bottom:1px solid rgba(0,100,200,.1);position:relative;line-height:1.5}
.mbox li::before{content:'▸';position:absolute;left:0;color:var(--bb)}
.mcl{position:absolute;top:13px;right:16px;background:transparent;border:1px solid rgba(0,120,255,.4);
  color:var(--bb);font-family:'Orbitron',sans-serif;font-size:.6rem;letter-spacing:2px;padding:5px 11px;cursor:pointer;transition:all .2s}
.mcl:hover{background:rgba(0,120,255,.2)}

/* ROBOT */
#rb{position:fixed;bottom:126px;right:20px;background:rgba(0,15,35,.97);border:1px solid var(--bb);
  border-radius:14px 14px 4px 14px;padding:0;width:0;height:0;overflow:hidden;opacity:0;z-index:1100;
  transition:opacity .3s;pointer-events:none}
#rb.show{width:auto;height:auto;opacity:1;pointer-events:all;padding:15px 17px 13px;
  min-width:200px;max-width:280px;animation:bpop .35s cubic-bezier(.34,1.56,.64,1) forwards}
@keyframes bpop{from{transform:scale(.7) translateY(10px);opacity:0}to{transform:scale(1) translateY(0);opacity:1}}
#rb::after{content:'';position:absolute;bottom:-9px;right:24px;border-left:9px solid transparent;border-top:9px solid var(--bb)}
.rbtag{font-family:'Share Tech Mono',monospace;font-size:.5rem;letter-spacing:4px;color:var(--b);margin-bottom:5px}
.rbtxt{font-family:'Exo 2',sans-serif;font-size:.78rem;line-height:1.55;color:var(--w)}
.rbtxt strong{color:var(--bb)}
.rbcl{position:absolute;top:7px;right:9px;background:transparent;border:none;color:var(--b);font-size:.7rem;cursor:pointer}
.rbcl:hover{color:#fff}
#rm{position:fixed;bottom:26px;right:22px;z-index:1100;cursor:pointer;width:82px;
  animation:rf 3s ease-in-out infinite;filter:drop-shadow(0 0 10px rgba(0,170,255,.6));
  transition:filter .3s;user-select:none}
#rm:hover{filter:drop-shadow(0 0 22px rgba(0,200,255,.95));transform:scale(1.1) translateY(-4px)}
@keyframes rf{0%,100%{transform:translateY(0) rotate(-1deg)}50%{transform:translateY(-9px) rotate(1deg)}}
.ad{animation:ab 1.2s step-end infinite}
@keyframes ab{0%,100%{opacity:1}50%{opacity:0}}

/* MAC BG for part3 */
#macbg{position:fixed;inset:0;z-index:0;opacity:0;pointer-events:none;transition:opacity 1s}
#macbg.show{opacity:.28}
</style>
</head>
<body>
<canvas id="mx"></canvas>
<div id="sl"></div>
<canvas id="macbg"></canvas>

<!-- ══════════════ SCREEN 1: INTRO ══════════════ -->
<div class="screen active" id="scIntro">
  <div class="hc tl"></div><div class="hc tr"></div><div class="hc bl"></div><div class="hc br"></div>
  <div class="intro-wrap">
    <p class="prod">✦ from Christian Caruso Production ✦</p>
    <h1 class="mtitle">La Robotica</h1>
    <p class="sysline" id="sline"><span class="cur"></span></p>
    <button id="btnS" onclick="startP1()">Inizia Presentazione</button>
  </div>
</div>

<!-- ══════════════ SCREEN 2: PARTE 1 — ED FISICA ══════════════ -->
<div class="screen" id="scP1">
  <div class="hero" id="heroP1">
    <div class="hw" id="hwP1"><canvas class="hcanvas" id="hcP1"></canvas></div>
    <div class="beam" id="beamP1"></div>
    <div class="hfade"></div>
  </div>
  <div class="sec rv"><div class="stag">CAPITOLO 01</div>
    <h2>Cosa sono le Protesi?</h2>
    <p>Una <strong>protesi</strong> è un dispositivo artificiale che sostituisce una parte del corpo mancante. Nate come semplici ausili in legno, oggi le protesi sono <strong>capolavori di ingegneria robotica</strong> che integrano sensori, motori e intelligenza artificiale.</p>
    <p>Le protesi moderne sono il punto di incontro tra <strong>biologia e tecnologia</strong>: vengono indossate e in molti casi anche "sentite", grazie a sistemi di feedback sensoriale.</p>
  </div>
  <div class="sec rv"><div class="stag">CAPITOLO 02</div>
    <h2>Come Funzionano?</h2>
    <p>Il cervello invia <strong>segnali elettrici ai muscoli</strong> — anche a quelli di un arto amputato. Elettrodi sulla pelle li captano, un microprocessore li interpreta e ordina ai motori della protesi di muoversi.</p>
    <div class="cards">
      <div class="card"><span class="cn">01</span><div class="ci">⚡</div><h3>EMG</h3><p>Elettromiografia: elettrodi captano l'attività elettrica dei muscoli residui e la trasformano in comandi.</p></div>
      <div class="card"><span class="cn">02</span><div class="ci">🧠</div><h3>Microprocessore</h3><p>Chip AI che interpreta i segnali in tempo reale e calcola il movimento ottimale della protesi.</p></div>
      <div class="card"><span class="cn">03</span><div class="ci">⚙️</div><h3>Attuatori</h3><p>Motori elettrici ultra-leggeri che eseguono i movimenti con precisione millimetrica.</p></div>
      <div class="card"><span class="cn">04</span><div class="ci">📡</div><h3>Sensori</h3><p>Accelerometri e giroscopi forniscono dati continui su posizione, forza e equilibrio.</p></div>
      <div class="card"><span class="cn">05</span><div class="ci">🔁</div><h3>Feedback</h3><p>Sistemi sensoriali stimolano i nervi per simulare il tatto: puoi "sentire" ciò che tocchi.</p></div>
      <div class="card"><span class="cn">06</span><div class="ci">🔋</div><h3>Batteria</h3><p>Batterie al litio: 12–24 ore di autonomia per uso quotidiano intensivo.</p></div>
    </div>
  </div>
  <!-- 3D ARM -->
  <div class="sec rv"><div class="stag">LABORATORIO 3D</div>
    <h2>Braccio Bionico 3D — Interattivo</h2>
    <p>Trascina per ruotare. Usa <strong>DITA</strong> o <strong>BRACCIO</strong> per controllare i movimenti.</p>
    <div id="armbox">
      <div class="awh">🦾 PROTESI BIONICA — SIMULATORE 3D</div>
      <div id="armwrap"><canvas id="ac"></canvas><div class="ahint">↔ TRASCINA PER RUOTARE</div></div>
      <div class="actrl">
        <div class="ast" id="ast">▸ SISTEMA PRONTO — SELEZIONA UN'AZIONE</div>
        <div class="arow">
          <button class="abtn" id="bdt" onclick="showF()">🖐 DITA</button>
          <button class="abtn" id="bbr" onclick="showA()">💪 BRACCIO</button>
        </div>
        <div class="sub" id="fp">
          <button class="fbtn" onclick="selF(0,this)">👍 POLLICE</button>
          <button class="fbtn" onclick="selF(1,this)">☝️ INDICE</button>
          <button class="fbtn" onclick="selF(2,this)">🖕 MEDIO</button>
          <button class="fbtn" onclick="selF(3,this)">💍 ANULARE</button>
          <button class="fbtn" onclick="selF(4,this)">🤙 MIGNOLO</button>
        </div>
        <div class="sub" id="fa"><button class="actbtn" id="fab" onclick="togF()">▶ CHIUDI DITO</button></div>
        <div class="sub" id="aa"><button class="actbtn" id="aab" onclick="togA()">▶ PIEGA BRACCIO</button></div>
      </div>
    </div>
  </div>
  <!-- QUIZ P1 -->
  <div class="sec rv"><div class="stag">QUIZ INTERATTIVO</div>
    <h2>Metti alla Prova le Conoscenze</h2>
    <div class="qbox" id="qb1">
      <h3>⚡ QUIZ — LE PROTESI</h3>
      <div class="qq" id="q1t"></div>
      <div class="qopts" id="q1o"></div>
      <div class="qfb" id="q1f"></div>
      <button class="qnx" id="q1n" onclick="nxQ1()">PROSSIMA ▶</button>
    </div>
  </div>
  <!-- TIMELINE -->
  <div class="sec rv"><div class="stag">STORIA INTERATTIVA</div>
    <h2>L'Evoluzione delle Protesi</h2>
    <div class="tl">
      <div class="ti" onclick="togTL(this)"><div class="td"></div><div class="ty">950 A.C.</div><div class="tt">Il primo alluce artificiale</div><div class="tx">Trovato su una mummia egizia: alluce in legno e cuoio. Funzionale per camminare con i sandali dell'epoca.</div></div>
      <div class="ti" onclick="togTL(this)"><div class="td"></div><div class="ty">1500 D.C.</div><div class="tt">Il braccio di ferro</div><div class="tx">Cavaliere tedesco Götz von Berlichingen perse il braccio in battaglia. Si fece costruire una mano meccanica in ferro con dita articolate.</div></div>
      <div class="ti" onclick="togTL(this)"><div class="td"></div><div class="ty">1945</div><div class="tt">Rivoluzione post-bellica</div><div class="tx">Dopo la WWII i veterani USA spinsero lo sviluppo. Nasce la protesi mioelettrica che legge i segnali muscolari.</div></div>
      <div class="ti" onclick="togTL(this)"><div class="td"></div><div class="ty">1996</div><div class="tt">Cheetah Blade alle Paralimpiadi</div><div class="tx">La lama in fibra di carbonio debutta ad Atlanta. Rivoluziona le protesi sportive: si può competere ai massimi livelli.</div></div>
      <div class="ti" onclick="togTL(this)"><div class="td"></div><div class="ty">2024</div><div class="tt">Protesi neurali e AI</div><div class="tx">Neuralink ha impiantato chip cerebrali in pazienti umani. Le protesi leggono il pensiero puro.</div></div>
    </div>
  </div>
  <!-- SPORT -->
  <div class="sec rv"><div class="stag">CAPITOLO 03</div>
    <h2>Protesi e Sport</h2>
    <p>Le protesi non limitano più la vita sportiva. Clicca per scoprire ogni disciplina:</p>
    <div class="sgrid">
      <button class="sbtn" onclick="OM('corsa')"><span class="si">🏃</span>CORSA</button>
      <button class="sbtn" onclick="OM('nuoto')"><span class="si">🏊</span>NUOTO</button>
      <button class="sbtn" onclick="OM('ciclismo')"><span class="si">🚴</span>CICLISMO</button>
      <button class="sbtn" onclick="OM('basket')"><span class="si">🏀</span>BASKET</button>
      <button class="sbtn" onclick="OM('scherma')"><span class="si">🤺</span>SCHERMA</button>
      <button class="sbtn" onclick="OM('arrampicata')"><span class="si">🧗</span>ARRAMPICATA</button>
    </div>
  </div>
  <div class="divider"></div>
  <div style="text-align:center;padding:36px 20px 80px;position:relative;z-index:10">
    <div style="font-family:'Share Tech Mono',monospace;font-size:.52rem;letter-spacing:6px;color:var(--b);opacity:.7;margin-bottom:14px">── FINE PRIMA PARTE ──</div>
    <button class="pgbtn" onclick="goToP2()">PROSEGUI ▶</button>
  </div>
</div>

<!-- ══════════════ SCREEN 3: PARTE 2 — SCIENZE ══════════════ -->
<div class="screen" id="scP2">
  <div class="hero" id="heroP2">
    <div class="hw" id="hwP2"><canvas class="hcanvas" id="hcP2"></canvas></div>
    <div class="beam" id="beamP2"></div>
    <div class="hfade"></div>
  </div>
  <div class="sec rv"><div class="stag">CAPITOLO 01</div>
    <h2>Cosa sono i Neuroni?</h2>
    <p>I <strong>neuroni</strong> sono le cellule fondamentali del sistema nervoso. Il cervello umano ne contiene circa <strong>86 miliardi</strong> — quasi quante le stelle della Via Lattea — connessi in una rete più complessa dell'universo conosciuto.</p>
    <p>A differenza delle altre cellule, i neuroni quasi <strong>non si riproducono</strong> dopo la nascita. Ma le connessioni tra loro cambiano continuamente: ogni volta che impari qualcosa, il tuo cervello cambia fisicamente.</p>
    <div class="infobox">
      <div class="irow"><span class="ilbl">🔢 Neuroni nel cervello</span><span class="ival"><strong>86 miliardi</strong></span></div>
      <div class="irow"><span class="ilbl">🔗 Connessioni totali</span><span class="ival"><strong>100 trilioni</strong> di sinapsi</span></div>
      <div class="irow"><span class="ilbl">⚡ Velocità segnale</span><span class="ival">fino a <strong>120 m/s</strong></span></div>
      <div class="irow"><span class="ilbl">🔋 Energia consumata</span><span class="ival"><strong>20 watt</strong> (20% del corpo)</span></div>
    </div>
    <div class="bars" id="statbars">
      <div class="brow"><div class="blbl"><span>NEURONI (86 MLD)</span><span>86%</span></div><div class="btrack"><div class="bfill" data-w="86%"></div></div></div>
      <div class="brow"><div class="blbl"><span>SINAPSI PER NEURONE</span><span>100%</span></div><div class="btrack"><div class="bfill" data-w="100%"></div></div></div>
      <div class="brow"><div class="blbl"><span>VELOCITÀ SEGNALE</span><span>72%</span></div><div class="btrack"><div class="bfill" data-w="72%"></div></div></div>
      <div class="brow"><div class="blbl"><span>ENERGIA USATA</span><span>20%</span></div><div class="btrack"><div class="bfill" data-w="20%"></div></div></div>
    </div>
  </div>
  <div class="sec rv"><div class="stag">CAPITOLO 02</div>
    <h2>La Struttura di un Neurone</h2>
    <div class="cards">
      <div class="card"><div class="ci">🔵</div><h3>Soma</h3><p>Il corpo cellulare. Contiene il nucleo con il DNA e gestisce il metabolismo.</p></div>
      <div class="card"><div class="ci">🌿</div><h3>Dendriti</h3><p>Rami che <strong>ricevono</strong> i segnali dagli altri neuroni. Un neurone può averne migliaia.</p></div>
      <div class="card"><div class="ci">➡️</div><h3>Assone</h3><p><strong>Trasmette</strong> il segnale elettrico lontano dal soma. Può essere lungo fino a 1 metro!</p></div>
      <div class="card"><div class="ci">⚡</div><h3>Guaina Mielinica</h3><p>Rivestimento grasso che aumenta la velocità del segnale fino a <strong>100 volte</strong>.</p></div>
      <div class="card"><div class="ci">🔗</div><h3>Sinapsi</h3><p>Punto di contatto tra neuroni. Rilascia <strong>neurotrasmettitori</strong> tra le cellule.</p></div>
      <div class="card"><div class="ci">🧪</div><h3>Neurotrasmettitori</h3><p>Molecole come <strong>dopamina</strong>, serotonina, GABA che portano il segnale tra i neuroni.</p></div>
    </div>
  </div>
  <div class="sec rv"><div class="stag">CAPITOLO 03</div>
    <h2>Come Comunicano i Neuroni?</h2>
    <p>La comunicazione neuronale avviene in due fasi: <strong>elettrica</strong> dentro il neurone, e <strong>chimica</strong> tra neuroni — il potenziale d'azione.</p>
    <div class="steps">
      <div class="step"><div class="sn">01</div><div class="stxt"><div><strong>Ricezione:</strong> i dendriti ricevono segnali chimici dagli altri neuroni.</div></div></div>
      <div class="step"><div class="sn">02</div><div class="stxt"><div><strong>Integrazione:</strong> il soma somma i segnali. Se superano la soglia, il neurone si attiva.</div></div></div>
      <div class="step"><div class="sn">03</div><div class="stxt"><div><strong>Trasmissione:</strong> il potenziale d'azione viaggia lungo l'assone a 120 m/s.</div></div></div>
      <div class="step"><div class="sn">04</div><div class="stxt"><div><strong>Rilascio:</strong> i terminali rilasciano neurotrasmettitori verso il neurone successivo.</div></div></div>
      <div class="step"><div class="sn">05</div><div class="stxt"><div><strong>Risposta:</strong> il neurone vicino riceve il segnale e il ciclo ricomincia.</div></div></div>
    </div>
  </div>
  <div class="sec rv"><div class="stag">CAPITOLO 04</div>
    <h2>Il Cervello: Centro di Controllo</h2>
    <p>Il cervello pesa <strong>1,4 kg</strong> — solo il 2% del peso corporeo — ma consuma il <strong>20% dell'energia</strong>. È diviso in quattro lobi specializzati.</p>
    <div class="cards">
      <div class="card"><div class="ci">🧠</div><h3>Lobo Frontale</h3><p>Ragionamento, pianificazione, personalità, movimento volontario.</p></div>
      <div class="card"><div class="ci">👂</div><h3>Lobo Temporale</h3><p>Memoria, linguaggio, udito. Sede dell'ippocampo per i ricordi.</p></div>
      <div class="card"><div class="ci">✋</div><h3>Lobo Parietale</h3><p>Tatto, dolore, temperatura. Integra sensazioni fisiche con lo spazio.</p></div>
      <div class="card"><div class="ci">👁️</div><h3>Lobo Occipitale</h3><p>Interamente dedicato alla vista: colori, forme, movimento, profondità.</p></div>
    </div>
  </div>
  <!-- APPROFONDIMENTI -->
  <div class="sec rv"><div class="stag">APPROFONDIMENTI</div>
    <h2>Esplora i Neuroni</h2>
    <div class="pgrid">
      <button class="pbtn" onclick="OM('plasticita')"><span class="pi">🔄</span>NEUROPLASTICITÀ</button>
      <button class="pbtn" onclick="OM('sogno')"><span class="pi">💤</span>SONNO E MEMORIA</button>
      <button class="pbtn" onclick="OM('dopamina')"><span class="pi">😊</span>DOPAMINA</button>
      <button class="pbtn" onclick="OM('aineuroni')"><span class="pi">🤖</span>NEURONI E AI</button>
      <button class="pbtn" onclick="OM('malattie')"><span class="pi">⚠️</span>MALATTIE</button>
      <button class="pbtn" onclick="OM('record')"><span class="pi">🏆</span>RECORD</button>
    </div>
  </div>
  <!-- NEURON TOUCH -->
  <div class="sec rv"><div class="stag">LABORATORIO INTERATTIVO</div>
    <h2>Rete Neurale — Tocca per Attivare</h2>
    <p>Tocca o clicca per generare impulsi elettrici!</p>
    <div class="nwrap">
      <div class="nwh">🧠 RETE NEURALE — SIMULAZIONE IMPULSI</div>
      <div class="ncwrap" id="ncwrap">
        <img id="nbg" src="eeg_sketch.jpg" alt="neuroni"/>
        <canvas id="nc"></canvas>
        <div class="nhint">⚡ TOCCA O CLICCA PER ATTIVARE I NEURONI</div>
      </div>
    </div>
  </div>
  <!-- QUIZ P2 -->
  <div class="sec rv"><div class="stag">QUIZ INTERATTIVO</div>
    <h2>Quiz — I Neuroni e il Cervello</h2>
    <div class="qbox" id="qb2">
      <h3>🧠 QUIZ — NEURONI</h3>
      <div class="qq" id="q2t"></div>
      <div class="qopts" id="q2o"></div>
      <div class="qfb" id="q2f"></div>
      <button class="qnx" id="q2n" onclick="nxQ2()">PROSSIMA ▶</button>
    </div>
  </div>
  <div class="divider"></div>
  <div style="text-align:center;padding:36px 20px 80px;position:relative;z-index:10">
    <div style="font-family:'Share Tech Mono',monospace;font-size:.52rem;letter-spacing:6px;color:var(--b);opacity:.7;margin-bottom:14px">── FINE SECONDA PARTE ──</div>
    <button class="pgbtn" onclick="goToP3()">PROSEGUI ▶</button>
  </div>
</div>

<!-- ══════════════ SCREEN 4: PARTE 3 — TECNOLOGIA ══════════════ -->
<div class="screen" id="scP3">
  <div class="hero" id="heroP3">
    <div class="hw" id="hwP3"><canvas class="hcanvas" id="hcP3"></canvas></div>
    <div class="beam" id="beamP3"></div>
    <div class="hfade"></div>
  </div>
  <div class="sec rv"><div class="stag">CAPITOLO 01</div>
    <h2>Come si Osservano i Neuroni?</h2>
    <p>Vedere i neuroni in azione è una delle sfide più affascinanti della scienza moderna. Il cervello è protetto da una barriera ossea e dalla <strong>barriera emato-encefalica</strong>. Tuttavia, grazie a tecnologie avanzate, oggi possiamo "vedere" il cervello funzionare in tempo reale senza aprire il cranio.</p>
    <p>Ogni tecnologia usa un principio fisico diverso: chi misura l'<strong>elettricità</strong> dei neuroni, chi misura il <strong>flusso di sangue</strong>, chi usa i <strong>campi magnetici</strong>.</p>
  </div>
  <div class="sec rv"><div class="stag">CAPITOLO 02</div>
    <h2>I Principali Macchinari</h2>
    <div class="cards">
      <div class="card"><div class="ci">🧠</div><h3>EEG</h3><p><strong>Elettroencefalogramma.</strong> Misura i segnali elettrici dei neuroni con elettrodi sul cuoio capelluto. Velocissimo ed economico.</p></div>
      <div class="card"><div class="ci">🔬</div><h3>fMRI</h3><p><strong>Risonanza Magnetica Funzionale.</strong> Misura il flusso di sangue ossigenato. Alta precisione spaziale, ritardo di 2-5 secondi.</p></div>
      <div class="card"><div class="ci">⚛️</div><h3>PET</h3><p><strong>Tomografia a Emissione di Positroni.</strong> Usa un tracciante radioattivo per visualizzare le aree cerebrali più attive.</p></div>
      <div class="card"><div class="ci">📡</div><h3>MEG</h3><p><strong>Magnetoencefalografia.</strong> Misura i campi magnetici dei neuroni. Precisissima ma costa milioni di euro.</p></div>
      <div class="card"><div class="ci">💉</div><h3>Microscopia</h3><p><strong>Microscopia elettronica.</strong> Permette di vedere i neuroni singolarmente, anche le sinapsi.</p></div>
      <div class="card"><div class="ci">🌊</div><h3>TMS</h3><p><strong>Stimolazione Magnetica Transcranica.</strong> Non solo osserva ma <strong>stimola</strong> i neuroni con impulsi magnetici.</p></div>
    </div>
  </div>
  <div class="sec rv"><div class="stag">APPROFONDIMENTI</div>
    <h2>Esplora i Macchinari</h2>
    <div class="pgrid">
      <button class="pbtn" onclick="OM('eeg')"><span class="pi">🧠</span>EEG</button>
      <button class="pbtn" onclick="OM('fmri')"><span class="pi">🔬</span>fMRI</button>
      <button class="pbtn" onclick="OM('pet')"><span class="pi">⚛️</span>PET</button>
      <button class="pbtn" onclick="OM('meg')"><span class="pi">📡</span>MEG</button>
      <button class="pbtn" onclick="OM('neuralink')"><span class="pi">🔩</span>NEURALINK</button>
      <button class="pbtn" onclick="OM('futuro')"><span class="pi">🚀</span>FUTURO</button>
    </div>
  </div>
  <div class="divider"></div>
  <div class="sec rv"><div class="stag">CAPITOLO 03</div>
    <h2>Tecnologia nella Vita Quotidiana</h2>
    <div class="cards">
      <div class="card"><div class="ci">🎮</div><h3>BCI Gaming</h3><p>Interfacce cervello-computer permettono di controllare videogame <strong>con il pensiero</strong>. Già disponibili come Emotiv e Muse.</p></div>
      <div class="card"><div class="ci">♿</div><h3>Riabilitazione</h3><p>Pazienti con ictus usano <strong>neurofeedback EEG</strong> per ri-allenare le aree cerebrali danneggiate.</p></div>
      <div class="card"><div class="ci">😴</div><h3>Monitor del Sonno</h3><p>Dispositivi come il <strong>Dreem</strong> usano EEG miniaturizzato per analizzare le fasi del sonno.</p></div>
      <div class="card"><div class="ci">🧘</div><h3>Meditazione</h3><p>App come <strong>Muse</strong> usano sensori EEG per misurare il livello di concentrazione in tempo reale.</p></div>
      <div class="card"><div class="ci">🚗</div><h3>Sicurezza Stradale</h3><p>Sistemi di <strong>monitoraggio dell'attenzione</strong> leggono i segnali cerebrali per rilevare sonnolenza al volante.</p></div>
      <div class="card"><div class="ci">🏥</div><h3>Diagnosi Precoce</h3><p>fMRI e PET rilevano l'<strong>Alzheimer fino a 20 anni prima</strong> dei sintomi.</p></div>
    </div>
  </div>
  <!-- QUIZ P3 -->
  <div class="sec rv"><div class="stag">QUIZ INTERATTIVO</div>
    <h2>Quiz — Tecnologia e Neuroni</h2>
    <div class="qbox" id="qb3">
      <h3>🔬 QUIZ — MACCHINARI</h3>
      <div class="qq" id="q3t"></div>
      <div class="qopts" id="q3o"></div>
      <div class="qfb" id="q3f"></div>
      <button class="qnx" id="q3n" onclick="nxQ3()">PROSSIMA ▶</button>
    </div>
  </div>
  <div class="divider"></div>
  <div style="text-align:center;padding:36px 20px 80px;position:relative;z-index:10">
    <div style="font-family:'Share Tech Mono',monospace;font-size:.52rem;letter-spacing:6px;color:var(--b);opacity:.7;margin-bottom:14px">── FINE TESINA ── GRAZIE! ──</div>
    <button class="pgbtn" onclick="goToP1()">◀ RICOMINCIA</button>
  </div>
</div>

<!-- FIXED TITLE OVERLAYS (shared across screens) -->
<div class="ftitle" id="ftLA" style="font-size:clamp(2.5rem,10vw,8rem);letter-spacing:.1em;top:50%;left:50%;transform:translate(-50%,-50%)">LA ROBOTICA</div>
<div class="ftitle" id="ftEF" style="font-size:clamp(2rem,7vw,5.5rem);letter-spacing:.12em;top:50%;left:50%;transform:translate(-50%,-50%);text-align:center;line-height:1.4">
  <span style="display:block;font-size:clamp(.6rem,1.8vw,1rem);letter-spacing:.5em;color:#00aaff;font-family:'Orbitron',sans-serif;font-weight:700">PRIMA PARTE</span>
  <span id="ftEFmain">ED FISICA</span>
</div>
<div id="lpHero"><span class="lpsub">── presenta ──</span><span class="lptitle">LE PROTESI</span></div>
<div class="ftitle" id="ftS2" style="font-size:clamp(1.2rem,4vw,3rem);letter-spacing:.1em;top:50%;left:50%;transform:translate(-50%,-50%);text-align:center;line-height:1.5">
  <span style="display:block;font-size:clamp(.5rem,1.3vw,.75rem);letter-spacing:.5em;color:#00aaff;font-family:'Orbitron',sans-serif;font-weight:700">SECONDA PARTE</span>
  <span>SCIENZE</span>
</div>
<div class="ftitle" id="ftNE" style="font-size:clamp(1.4rem,4.5vw,3.5rem);letter-spacing:.1em;top:50%;left:50%;transform:translate(-50%,-50%);white-space:normal;text-align:center">I NEURONI E IL CERVELLO</div>
<div class="ftitle" id="ftT3" style="font-size:clamp(1.2rem,4vw,3rem);letter-spacing:.1em;top:50%;left:50%;transform:translate(-50%,-50%);text-align:center;line-height:1.5">
  <span style="display:block;font-size:clamp(.5rem,1.3vw,.75rem);letter-spacing:.5em;color:#00aaff;font-family:'Orbitron',sans-serif;font-weight:700">TERZA PARTE</span>
  <span>TECNOLOGIA</span>
</div>
<div class="ftitle" id="ftMC" style="font-size:clamp(.75rem,2vw,1.3rem);letter-spacing:.08em;top:50%;left:50%;transform:translate(-50%,-50%);text-align:center;white-space:normal;max-width:80vw;line-height:1.5">I MACCHINARI CON CUI<br>SI VEDONO I NEURONI</div>

<!-- MODAL -->
<div id="ov" onclick="if(event.target===this)CM()">
  <div class="mbox"><button class="mcl" onclick="CM()">✕ CHIUDI</button>
    <div class="mtag" id="mt"></div><div class="mico" id="mi"></div>
    <h2 id="mh"></h2><div id="mb"></div>
  </div>
</div>

<!-- ROBOT -->
<div id="rb">
  <button class="rbcl" onclick="CRB()">✕</button>
  <div class="rbtag">🤖 FUN FACT</div>
  <p class="rbtxt" id="rbt"></p>
</div>
<svg id="rm" onclick="SFF()" viewBox="0 0 100 130" xmlns="http://www.w3.org/2000/svg">
  <line x1="50" y1="12" x2="50" y2="22" stroke="#33ccff" stroke-width="2.5" stroke-linecap="round"/>
  <circle class="ad" cx="50" cy="9" r="4" fill="#00aaff"/>
  <rect x="18" y="22" width="64" height="52" rx="12" fill="#001e3c" stroke="#33ccff" stroke-width="2"/>
  <rect x="25" y="29" width="50" height="32" rx="6" fill="#002a50"/>
  <circle cx="38" cy="43" r="7" fill="#001428"/><circle cx="38" cy="43" r="4.5" fill="#00aaff" opacity=".9"/><circle cx="39.5" cy="41.5" r="1.5" fill="#fff"/>
  <circle cx="62" cy="43" r="7" fill="#001428"/><circle cx="62" cy="43" r="4.5" fill="#00aaff" opacity=".9"/><circle cx="63.5" cy="41.5" r="1.5" fill="#fff"/>
  <path d="M38 54 Q50 62 62 54" stroke="#33ccff" stroke-width="2.5" fill="none" stroke-linecap="round"/>
  <rect x="10" y="36" width="9" height="14" rx="3" fill="#001e3c" stroke="#00aaff" stroke-width="1.5"/>
  <rect x="81" y="36" width="9" height="14" rx="3" fill="#001e3c" stroke="#00aaff" stroke-width="1.5"/>
  <rect x="40" y="74" width="20" height="10" rx="3" fill="#001a30" stroke="#0066cc" stroke-width="1.5"/>
  <rect x="22" y="84" width="56" height="38" rx="10" fill="#001428" stroke="#0066cc" stroke-width="2"/>
  <rect x="32" y="91" width="36" height="22" rx="5" fill="#002244"/>
  <circle cx="42" cy="100" r="4" fill="#00aaff" opacity=".8"/>
  <circle cx="50" cy="100" r="4" fill="#33ccff" opacity=".6"/>
  <circle cx="58" cy="100" r="4" fill="#0066cc" opacity=".8"/>
  <rect x="30" y="116" width="12" height="6" rx="2" fill="#0066cc"/>
  <rect x="58" y="116" width="12" height="6" rx="2" fill="#0066cc"/>
</svg>

<script>
var curPart = 0; // 0=intro, 1=p1, 2=p2, 3=p3

// ── MATRIX ──
(function(){var c=document.getElementById('mx'),x=c.getContext('2d');function r(){c.width=innerWidth;c.height=innerHeight;}r();addEventListener('resize',r);var ch='アイウエオ01ABCDEF{}if for return void int',fs=13,dr=[];setInterval(function(){var cols=Math.floor(c.width/fs);while(dr.length<cols)dr.push(1);x.fillStyle='rgba(0,8,20,.045)';x.fillRect(0,0,c.width,c.height);x.font=fs+'px Share Tech Mono,monospace';for(var i=0;i<cols;i++){var s=ch[Math.floor(Math.random()*ch.length)];x.fillStyle=Math.random()>.95?'#fff':Math.random()>.5?'#33ccff':'#00aaff';x.fillText(s,i*fs,dr[i]*fs);if(dr[i]*fs>c.height&&Math.random()>.975)dr[i]=0;dr[i]++;}},42);})();

// ── MACCHINARI BG ──
(function(){var c=document.getElementById('macbg'),cx=c.getContext('2d');function resize(){c.width=innerWidth;c.height=innerHeight;}resize();addEventListener('resize',resize);var syms=['EEG','fMRI','PET','MEG','TMS','BCI','∿∿∿','⊗','◎','⊕','∫∫','ΔV'],shapes=[];for(var i=0;i<28;i++){shapes.push({x:Math.random()*innerWidth,y:Math.random()*innerHeight,vx:(Math.random()-.5)*.4,vy:(Math.random()-.5)*.35,sym:syms[Math.floor(Math.random()*syms.length)],size:10+Math.random()*18,alpha:.15+Math.random()*.22,rot:Math.random()*Math.PI*2,rotV:(Math.random()-.5)*.012});}function draw(){cx.clearRect(0,0,c.width,c.height);shapes.forEach(function(s){s.x+=s.vx;s.y+=s.vy;s.rot+=s.rotV;if(s.x<-50)s.x=c.width+50;if(s.x>c.width+50)s.x=-50;if(s.y<-50)s.y=c.height+50;if(s.y>c.height+50)s.y=-50;cx.save();cx.translate(s.x,s.y);cx.rotate(s.rot);cx.globalAlpha=s.alpha;cx.font='bold '+s.size+'px Share Tech Mono,monospace';cx.fillStyle='#33ccff';cx.fillText(s.sym,-cx.measureText(s.sym).width/2,s.size/3);cx.restore();});requestAnimationFrame(draw);}draw();})();

// ── TYPING ──
var tlines=['SYSTEM BOOT... OK','ROBOTICS MODULE LOADED','PRESS START >>'],tl=0,tc=0,tel=document.getElementById('sline');
function TN(){var s=tlines[tl%tlines.length];if(tc<=s.length){tel.innerHTML=s.slice(0,tc)+'<span class="cur"></span>';tc++;setTimeout(TN,65);}else{setTimeout(function(){tl++;tc=0;TN();},1600);}}
setTimeout(TN,800);

// ── SKETCH FUNCTION ──
function SKETCH(imgSrc, canvasId, cb){
  var img=new Image();
  img.onload=function(){
    var cv=document.getElementById(canvasId);
    var mw=Math.min(innerWidth*.85,500),sc=mw/img.width;
    cv.width=img.width*sc;cv.height=img.height*sc;
    var cx=cv.getContext('2d');cx.drawImage(img,0,0,cv.width,cv.height);
    var id=cx.getImageData(0,0,cv.width,cv.height),d=id.data,w=cv.width,h=cv.height;
    var gr=new Uint8Array(w*h);
    for(var i=0;i<w*h;i++)gr[i]=.299*d[i*4]+.587*d[i*4+1]+.114*d[i*4+2];
    var out=cx.createImageData(w,h),o=out.data;
    for(var y=1;y<h-1;y++)for(var x=1;x<w-1;x++){
      var gx=-gr[(y-1)*w+(x-1)]+gr[(y-1)*w+(x+1)]-2*gr[y*w+(x-1)]+2*gr[y*w+(x+1)]-gr[(y+1)*w+(x-1)]+gr[(y+1)*w+(x+1)];
      var gy=-gr[(y-1)*w+(x-1)]-2*gr[(y-1)*w+x]-gr[(y-1)*w+(x+1)]+gr[(y+1)*w+(x-1)]+2*gr[(y+1)*w+x]+gr[(y+1)*w+(x+1)];
      var m=Math.min(255,Math.sqrt(gx*gx+gy*gy)*1.5),idx=(y*w+x)*4;
      if(m>18){o[idx]=Math.max(0,200-m*.3);o[idx+1]=Math.max(0,220-m*.2);o[idx+2]=255;o[idx+3]=Math.min(255,m*1.3);}
      else{o[idx]=o[idx+1]=o[idx+2]=0;o[idx+3]=0;}
    }
    cx.putImageData(out,0,0);
    if(cb)cb();
  };
  img.src=imgSrc;
}

// Pre-render all sketches
SKETCH('brain_sketch.jpg','hcP1');
SKETCH('robot_sketch.jpg','hcP2');
SKETCH('neuro_bg.jpg','hcP3');

// ── AUDIO ──
function AUD(){var ac=new(window.AudioContext||window.webkitAudioContext)(),now=ac.currentTime;function T(f,s,d,t,v){t=t||'sine';v=v||.07;var o=ac.createOscillator(),g=ac.createGain();o.type=t;o.frequency.setValueAtTime(f,now+s);g.gain.setValueAtTime(0,now+s);g.gain.linearRampToValueAtTime(v,now+s+.06);g.gain.linearRampToValueAtTime(0,now+s+d);o.connect(g);g.connect(ac.destination);o.start(now+s);o.stop(now+s+d+.1);}function S(f0,f1,s,d,t,v){t=t||'sine';v=v||.05;var o=ac.createOscillator(),g=ac.createGain();o.type=t;o.frequency.setValueAtTime(f0,now+s);o.frequency.linearRampToValueAtTime(f1,now+s+d);g.gain.setValueAtTime(0,now+s);g.gain.linearRampToValueAtTime(v,now+s+.07);g.gain.linearRampToValueAtTime(0,now+s+d);o.connect(g);g.connect(ac.destination);o.start(now+s);o.stop(now+s+d+.1);}[220,440,660,880].forEach(function(f,i){T(f,i*.14,.1,'square',.02);});S(60,350,.8,3.5,'sawtooth',.04);S(350,1400,.8,3,'sine',.04);T(80,1.2,1.5,'triangle',.09);T(160,1.6,1,'sine',.07);S(200,50,2.5,2,'sawtooth',.04);T(55,3,1,'triangle',.1);S(100,1400,3.8,.7,'sine',.08);[1760,880,440].forEach(function(f,i){T(f,4.5+i*.1,.1,'square',.03);});S(1500,180,4.55,1,'sine',.09);T(110,4.7,.6,'triangle',.11);}

// ── SCREEN TRANSITIONS ──
function showScreen(id){
  document.querySelectorAll('.screen').forEach(function(s){s.classList.remove('active');});
  document.getElementById(id).classList.add('active');
  document.getElementById(id).scrollTop=0;
}

function hideAllTitles(){
  ['ftLA','ftEF','lpHero','ftS2','ftNE','ftT3','ftMC'].forEach(function(id){
    var el=document.getElementById(id);
    el.className='ftitle';
    el.style.cssText='font-size:'+el.style.fontSize+';top:50%;left:50%;transform:translate(-50%,-50%);opacity:0';
  });
}

function animTitle(id, delay, movDir, fontSize){
  setTimeout(function(){
    var el=document.getElementById(id);
    el.style.fontSize=fontSize||'';
    el.classList.add('active-title','flash-anim');
    setTimeout(function(){
      el.classList.remove('flash-anim');
      el.classList.add(movDir);
    },delay+3600);
  },delay);
}

// BLACK FADE TRANSITION
function blackFade(cb){
  var bl=document.getElementById('tblack');
  bl.style.transition='opacity .7s';
  bl.style.opacity='1';bl.style.pointerEvents='all';
  setTimeout(function(){cb();bl.style.opacity='0';bl.style.pointerEvents='none';},800);
}

// ── START PART 1 ──
function startP1(){
  AUD();
  curPart=1;
  document.getElementById('scIntro').classList.remove('active');
  hideAllTitles();
  showScreen('scP1');
  setTimeout(function(){
    document.getElementById('hwP1').classList.add('zi');
    document.getElementById('beamP1').classList.add('go');
  },100);
  // LA ROBOTICA → top right
  var la=document.getElementById('ftLA');
  la.style.cssText='position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);font-family:Orbitron,sans-serif;font-size:clamp(2.5rem,10vw,8rem);font-weight:900;letter-spacing:.1em;text-transform:uppercase;color:transparent;opacity:0;white-space:nowrap;z-index:50;pointer-events:none';
  setTimeout(function(){la.classList.add('active-title','flash-anim');setTimeout(function(){la.classList.remove('flash-anim');la.classList.add('move-right');},3600);},4500);
  // ED FISICA → top left
  var ef=document.getElementById('ftEF');
  ef.style.cssText='position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);font-family:Orbitron,sans-serif;font-size:clamp(2rem,7vw,5.5rem);font-weight:900;text-transform:uppercase;color:transparent;opacity:0;z-index:50;pointer-events:none;text-align:center;line-height:1.4';
  setTimeout(function(){ef.classList.add('active-title','flash-anim');setTimeout(function(){ef.classList.remove('flash-anim');ef.classList.add('move-left');},3200);},9800);
  // LE PROTESI center
  setTimeout(function(){document.getElementById('lpHero').classList.add('on');},15000);
  RV('scP1');
}

// ── GO TO PART 2 ──
function goToP2(){
  blackFade(function(){
    curPart=2;
    // hide p1 titles
    ['ftLA','ftEF','lpHero'].forEach(function(id){var el=document.getElementById(id);el.className='ftitle';el.style.opacity='0';});
    hideP1Titles();
    showScreen('scP2');
    document.getElementById('macbg').classList.remove('show');
    setTimeout(function(){
      document.getElementById('hwP2').classList.add('zi');
      document.getElementById('beamP2').classList.add('go');
    },100);
    // I NEURONI E IL CERVELLO → top right
    var ne=document.getElementById('ftNE');
    ne.style.cssText='position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);font-family:Orbitron,sans-serif;font-size:clamp(1.4rem,4.5vw,3.5rem);font-weight:900;text-transform:uppercase;color:transparent;opacity:0;white-space:nowrap;z-index:50;pointer-events:none;text-align:center';
    setTimeout(function(){ne.classList.add('active-title','flash-anim');setTimeout(function(){ne.classList.remove('flash-anim');ne.classList.add('move-right');},3600);},4500);
    // SECONDA PARTE SCIENZE → top left
    var s2=document.getElementById('ftS2');
    s2.style.cssText='position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);font-family:Orbitron,sans-serif;font-size:clamp(1.2rem,4vw,3rem);font-weight:900;text-transform:uppercase;color:transparent;opacity:0;z-index:50;pointer-events:none;text-align:center;line-height:1.5';
    setTimeout(function(){s2.classList.add('active-title','flash-anim');setTimeout(function(){s2.classList.remove('flash-anim');s2.classList.add('move-left');},3200);},9800);
    initNeuronTouch();
    initStatBars();
    RV('scP2');
    initQ2();
  });
}

function hideP1Titles(){['ftLA','ftEF','lpHero'].forEach(function(id){var el=document.getElementById(id);if(el){el.className='ftitle';el.style.opacity='0';}});}
function hideP2Titles(){['ftNE','ftS2'].forEach(function(id){var el=document.getElementById(id);if(el){el.className='ftitle';el.style.opacity='0';}});}

// ── GO TO PART 3 ──
function goToP3(){
  blackFade(function(){
    curPart=3;
    hideP2Titles();
    showScreen('scP3');
    document.getElementById('macbg').classList.add('show');
    setTimeout(function(){
      document.getElementById('hwP3').classList.add('zi');
      document.getElementById('beamP3').classList.add('go');
    },100);
    // TERZA PARTE TECNOLOGIA → top left
    var t3=document.getElementById('ftT3');
    t3.style.cssText='position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);font-family:Orbitron,sans-serif;font-size:clamp(1.2rem,4vw,3rem);font-weight:900;text-transform:uppercase;color:transparent;opacity:0;z-index:50;pointer-events:none;text-align:center;line-height:1.5';
    setTimeout(function(){t3.classList.add('active-title','flash-anim');setTimeout(function(){t3.classList.remove('flash-anim');t3.classList.add('move-left');},3600);},4500);
    // I MACCHINARI → top right
    var mc=document.getElementById('ftMC');
    mc.style.cssText='position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);font-family:Orbitron,sans-serif;font-size:clamp(.75rem,2vw,1.3rem);font-weight:700;text-transform:uppercase;color:transparent;opacity:0;z-index:50;pointer-events:none;text-align:center;max-width:80vw;line-height:1.5';
    setTimeout(function(){mc.classList.add('active-title','flash-anim');setTimeout(function(){mc.classList.remove('flash-anim');mc.classList.add('move-right');},3200);},9800);
    RV('scP3');
    initQ3();
  });
}

function goToP1(){
  blackFade(function(){
    curPart=1;
    hideP2Titles();
    ['ftT3','ftMC'].forEach(function(id){var el=document.getElementById(id);if(el){el.className='ftitle';el.style.opacity='0';}});
    document.getElementById('macbg').classList.remove('show');
    showScreen('scIntro');
  });
}

// ── REVEAL ──
var rvObs={};
function RV(screenId){
  var sc=document.getElementById(screenId);
  if(!sc)return;
  var obs=new IntersectionObserver(function(entries){entries.forEach(function(e){if(e.isIntersecting){e.target.classList.add('vis');obs.unobserve(e.target);}});},{threshold:.1,root:sc});
  sc.querySelectorAll('.rv').forEach(function(el){obs.observe(el);});
}

// ── STAT BARS ──
function initStatBars(){
  var obs=new IntersectionObserver(function(entries){entries.forEach(function(e){if(e.isIntersecting){e.target.querySelectorAll('.bfill').forEach(function(b){b.style.width=b.getAttribute('data-w');});obs.unobserve(e.target);}});},{threshold:.2,root:document.getElementById('scP2')});
  var sb=document.getElementById('statbars');if(sb)obs.observe(sb);
}

// ── 3D ARM ENGINE ──
(function(){
  var cv=document.getElementById('ac');
  var wp=document.getElementById('armwrap');
  var cx=cv.getContext('2d');
  var rY=.5,rX=-.2,drag=false,lx=0,ly=0;
  window.fingerAngles=[0,0,0,0,0];
  window.elbowAngle=0;
  window.selectedFinger=-1;
  window.fingerOpen=[true,true,true,true,true];
  window.armStraight=true;
  function resize(){cv.width=wp.offsetWidth||400;cv.height=340;}
  resize();try{new ResizeObserver(resize).observe(wp);}catch(e){}
  function P(x,y,z){var cY=Math.cos(rY),sY=Math.sin(rY),cX=Math.cos(rX),sX=Math.sin(rX);var rx=x*cY+z*sY,rz=-x*sY+z*cY;var ry=y*cX-rz*sX,rz2=y*sX+rz*cX;var d=500/(500+rz2+400);var cx2=cv.width/2,cy2=cv.height/2+40;return{x:cx2+rx*d,y:cy2+ry*d,d:d};}
  function CYL(ax,ay,az,bx,by,bz,r,col){var A=P(ax,ay,az),B=P(bx,by,bz);var dx=B.x-A.x,dy=B.y-A.y,L=Math.sqrt(dx*dx+dy*dy);if(L<1)return;var rad=r*(A.d+B.d)*.5*90;var px=-dy/L*rad,py=dx/L*rad;var g=cx.createLinearGradient(A.x-px,A.y-py,A.x+px,A.y+py);g.addColorStop(0,'rgba(180,220,255,.3)');g.addColorStop(.35,col);g.addColorStop(.65,col);g.addColorStop(1,'rgba(0,15,50,.85)');cx.beginPath();cx.moveTo(A.x-px,A.y-py);cx.lineTo(B.x-px,B.y-py);cx.lineTo(B.x+px,B.y+py);cx.lineTo(A.x+px,A.y+py);cx.closePath();cx.fillStyle=g;cx.fill();}
  function SPH(x,y,z,r,col){var p2=P(x,y,z),rs=r*p2.d*90;if(rs<1)return;var g=cx.createRadialGradient(p2.x-rs*.3,p2.y-rs*.3,0,p2.x,p2.y,rs);g.addColorStop(0,'rgba(160,225,255,.95)');g.addColorStop(.4,col);g.addColorStop(1,'rgba(0,8,35,.9)');cx.beginPath();cx.arc(p2.x,p2.y,rs,0,Math.PI*2);cx.fillStyle=g;cx.fill();}
  function DRAW(){cx.clearRect(0,0,cv.width,cv.height);var bg=cx.createRadialGradient(cv.width/2,cv.height/2,0,cv.width/2,cv.height/2,180);bg.addColorStop(0,'rgba(0,40,100,.2)');bg.addColorStop(1,'rgba(0,0,0,0)');cx.fillStyle=bg;cx.fillRect(0,0,cv.width,cv.height);var ARM='rgba(12,50,95,.95)',JNT='rgba(0,100,158,.95)',FNG='rgba(8,72,125,.95)',HLT='rgba(0,175,255,.95)';var eb=window.elbowAngle*.85;var sX=0,sY=-80;var eX=Math.sin(eb)*90,eY=-80+Math.cos(eb)*80;var wX=eX+Math.sin(eb*.6)*50,wY=eY+52-Math.cos(eb*.6)*8;CYL(sX,sY,0,eX,eY,0,.2,ARM);SPH(sX,sY,0,.24,JNT);SPH(eX,eY,0,.2,JNT);CYL(eX,eY,0,wX,wY,0,.16,ARM);SPH(wX,wY,0,.18,JNT);var pw=22;CYL(wX-pw,wY+5,-12,wX+pw,wY+5,-12,.07,ARM);CYL(wX-pw,wY+5,12,wX+pw,wY+5,12,.07,ARM);CYL(wX-pw,wY+5,-12,wX-pw,wY+5,12,.07,ARM);CYL(wX+pw,wY+5,-12,wX+pw,wY+5,12,.07,ARM);var fps=[{x:wX-pw-3,y:wY+16,z:-2},{x:wX-pw/2,y:wY+16,z:-1},{x:wX,y:wY+16,z:0},{x:wX+pw/2,y:wY+16,z:1},{x:wX+pw+3,y:wY+16,z:2}];for(var i=0;i<5;i++){var f=fps[i],t=window.fingerAngles[i],sel=(i===window.selectedFinger),col=sel?HLT:FNG;var L1=i===0?14:20,L2=i===0?10:14;var c1=t*1.15,c2=t*1.6;var p1x=f.x+(i===0?-Math.sin(c1)*L1:0),p1y=f.y+Math.cos(c1)*L1;var p2x=p1x+(i===0?-Math.sin(c2)*L2:0),p2y=p1y+Math.cos(c2)*L2;var p3x=p2x,p3y=p2y+9*(1-t*.4);CYL(f.x,f.y,f.z,p1x,p1y,f.z,i===0?.06:.055,col);CYL(p1x,p1y,f.z,p2x,p2y,f.z,.048,col);CYL(p2x,p2y,f.z,p3x,p3y,f.z,.038,col);SPH(p1x,p1y,f.z,.058,JNT);SPH(p2x,p2y,f.z,.05,JNT);if(sel){var gp=P(p1x,p1y,f.z);cx.beginPath();cx.arc(gp.x,gp.y,16,0,Math.PI*2);cx.fillStyle='rgba(0,175,255,.15)';cx.fill();cx.strokeStyle='rgba(0,200,255,.55)';cx.lineWidth=1.5;cx.stroke();}}cx.strokeStyle='rgba(0,150,255,.07)';cx.lineWidth=.8;[[sX,sY,eX,eY],[eX,eY,wX,wY]].forEach(function(l){for(var oi=-1;oi<=1;oi++){var s2=P(l[0]+oi*3,l[1],oi),e2=P(l[2]+oi*3,l[3],oi);cx.beginPath();cx.moveTo(s2.x,s2.y);cx.lineTo(e2.x,e2.y);cx.stroke();}});requestAnimationFrame(DRAW);}
  DRAW();
  wp.addEventListener('mousedown',function(e){drag=true;lx=e.clientX;ly=e.clientY;e.preventDefault();});
  document.addEventListener('mousemove',function(e){if(!drag)return;rY+=(e.clientX-lx)*.014;rX+=(e.clientY-ly)*.012;lx=e.clientX;ly=e.clientY;});
  document.addEventListener('mouseup',function(){drag=false;});
  wp.addEventListener('touchstart',function(e){drag=true;lx=e.touches[0].clientX;ly=e.touches[0].clientY;},{passive:true});
  wp.addEventListener('touchmove',function(e){if(!drag)return;rY+=(e.touches[0].clientX-lx)*.014;rX+=(e.touches[0].clientY-ly)*.012;lx=e.touches[0].clientX;ly=e.touches[0].clientY;},{passive:true});
  wp.addEventListener('touchend',function(){drag=false;});
})();

function animateTo(arr,idx,target,ms){var s=arr[idx],t0=performance.now();(function step(now){var p=Math.min((now-t0)/ms,1),e=p<.5?2*p*p:1-Math.pow(-2*p+2,2)/2;arr[idx]=s+(target-s)*e;if(p<1)requestAnimationFrame(step);})(t0);}
function animEA(target,ms){var s=window.elbowAngle,t0=performance.now();(function step(now){var p=Math.min((now-t0)/ms,1),e=p<.5?2*p*p:1-Math.pow(-2*p+2,2)/2;window.elbowAngle=s+(target-s)*e;if(p<1)requestAnimationFrame(step);})(t0);}
var FN=['POLLICE','INDICE','MEDIO','ANULARE','MIGNOLO'];
function STAT(t){var e=document.getElementById('ast');if(e)e.textContent='▸ '+t;}
function showF(){document.getElementById('fp').classList.add('show');document.getElementById('aa').classList.remove('show');document.getElementById('fa').classList.remove('show');document.getElementById('bdt').classList.add('act');document.getElementById('bbr').classList.remove('act');STAT('SELEZIONA UN DITO');}
function showA(){document.getElementById('aa').classList.add('show');document.getElementById('fp').classList.remove('show');document.getElementById('fa').classList.remove('show');document.getElementById('bbr').classList.add('act');document.getElementById('bdt').classList.remove('act');STAT('CONTROLLO BRACCIO');}
function selF(i,btn){window.selectedFinger=i;document.querySelectorAll('.fbtn').forEach(function(b){b.classList.remove('sel');});btn.classList.add('sel');document.getElementById('fa').classList.add('show');var open=window.fingerOpen[i];document.getElementById('fab').textContent=open?'▶ CHIUDI DITO':'▶ APRI DITO';STAT(FN[i]+': '+(open?'APERTO':'CHIUSO'));}
function togF(){var i=window.selectedFinger;if(i<0)return;window.fingerOpen[i]=!window.fingerOpen[i];var open=window.fingerOpen[i];animateTo(window.fingerAngles,i,open?0:1,450);document.getElementById('fab').textContent=open?'▶ CHIUDI DITO':'▶ APRI DITO';STAT(FN[i]+': '+(open?'APERTURA...':'CHIUSURA...'));setTimeout(function(){STAT(FN[i]+': '+(open?'APERTO':'CHIUSO'));},470);}
function togA(){window.armStraight=!window.armStraight;var s=window.armStraight;animEA(s?0:1,600);document.getElementById('aab').textContent=s?'▶ PIEGA BRACCIO':'▶ ESTENDI BRACCIO';STAT('BRACCIO: '+(s?'DISTENSIONE...':'FLESSIONE...'));setTimeout(function(){STAT('BRACCIO: '+(s?'ESTESO':'PIEGATO'));},620);}

// ── NEURON TOUCH ──
function initNeuronTouch(){
  var cv=document.getElementById('nc');var wp2=document.getElementById('ncwrap');var cx2=cv.getContext('2d');
  var pressed=false,px=0,py=0,particles=[],sparks=[];
  function resize(){cv.width=wp2.offsetWidth||600;cv.height=wp2.offsetHeight||360;}
  resize();try{new ResizeObserver(resize).observe(wp2);}catch(e){}
  function pulse(x,y){var i,n=8+Math.floor(Math.random()*8);for(i=0;i<n;i++){var a=Math.random()*Math.PI*2,sp=1.5+Math.random()*4;sparks.push({x:x,y:y,vx:Math.cos(a)*sp,vy:Math.sin(a)*sp,life:1,decay:.03+Math.random()*.04,size:1.5+Math.random()*2.5,col:'hsl('+(180+Math.random()*60)+',100%,'+(70+Math.random()*30)+'%)'});}for(i=0;i<3+Math.floor(Math.random()*3);i++){var len=30+Math.random()*80,angle=Math.random()*Math.PI*2,segs=5+Math.floor(Math.random()*5),pts=[{x:x,y:y}];for(var j=1;j<=segs;j++){var t2=j/segs,jit=20*(1-t2);pts.push({x:x+Math.cos(angle)*len*t2+(Math.random()-.5)*jit*2,y:y+Math.sin(angle)*len*t2+(Math.random()-.5)*jit*2});}particles.push({pts:pts,life:1,decay:.08+Math.random()*.06,w:1+Math.random()*2});}sparks.push({x:x,y:y,vx:0,vy:0,life:.8,decay:.04,size:0,maxSize:55+Math.random()*35,isRipple:true});}
  function draw(){cx2.clearRect(0,0,cv.width,cv.height);if(pressed&&Math.random()<.4)pulse(px,py);var i;for(i=particles.length-1;i>=0;i--){var p2=particles[i];p2.life-=p2.decay;if(p2.life<=0){particles.splice(i,1);continue;}cx2.globalAlpha=p2.life;cx2.strokeStyle='hsl('+(200+Math.random()*40)+',100%,'+(80+Math.floor(Math.random()*20))+'%)';cx2.lineWidth=p2.w*p2.life;cx2.shadowBlur=12;cx2.shadowColor='rgba(100,200,255,.8)';cx2.beginPath();p2.pts.forEach(function(pt,j){j===0?cx2.moveTo(pt.x,pt.y):cx2.lineTo(pt.x,pt.y);});cx2.stroke();cx2.shadowBlur=0;}for(i=sparks.length-1;i>=0;i--){var s2=sparks[i];s2.life-=s2.decay;if(s2.life<=0){sparks.splice(i,1);continue;}if(s2.isRipple){s2.size=(1-s2.life)*s2.maxSize;cx2.globalAlpha=s2.life*.6;cx2.strokeStyle='rgba(100,210,255,.8)';cx2.lineWidth=2*s2.life;cx2.shadowBlur=8;cx2.shadowColor='rgba(0,180,255,.6)';cx2.beginPath();cx2.arc(s2.x,s2.y,s2.size,0,Math.PI*2);cx2.stroke();cx2.shadowBlur=0;}else{s2.x+=s2.vx;s2.y+=s2.vy;s2.vx*=.92;s2.vy*=.92;cx2.globalAlpha=s2.life;var g2=cx2.createRadialGradient(s2.x,s2.y,0,s2.x,s2.y,s2.size*2);g2.addColorStop(0,s2.col);g2.addColorStop(1,'rgba(0,0,0,0)');cx2.fillStyle=g2;cx2.beginPath();cx2.arc(s2.x,s2.y,s2.size*2,0,Math.PI*2);cx2.fill();}}cx2.globalAlpha=1;requestAnimationFrame(draw);}
  draw();
  function pos(e){var r=cv.getBoundingClientRect();return{x:(e.clientX-r.left)*cv.width/r.width,y:(e.clientY-r.top)*cv.height/r.height};}
  cv.addEventListener('mousedown',function(e){var p3=pos(e);pressed=true;px=p3.x;py=p3.y;pulse(px,py);e.preventDefault();});
  document.addEventListener('mousemove',function(e){if(!pressed)return;var p4=pos(e);px=p4.x;py=p4.y;});
  document.addEventListener('mouseup',function(){pressed=false;});
  cv.addEventListener('touchstart',function(e){var r=cv.getBoundingClientRect(),t=e.touches[0];px=(t.clientX-r.left)*cv.width/r.width;py=(t.clientY-r.top)*cv.height/r.height;pressed=true;pulse(px,py);e.preventDefault();},{passive:false});
  cv.addEventListener('touchmove',function(e){var r=cv.getBoundingClientRect(),t=e.touches[0];px=(t.clientX-r.left)*cv.width/r.width;py=(t.clientY-r.top)*cv.height/r.height;e.preventDefault();},{passive:false});
  cv.addEventListener('touchend',function(){pressed=false;});
}

// ── QUIZ 1 ──
var Q1=[{q:'Qual \u00e8 il materiale pi\u00f9 usato nelle protesi sportive?',o:['Alluminio','Fibra di carbonio','Titanio','Acciaio'],a:1,e:'✅ Fibra di carbonio! Leggera e resistente — usata nella Cheetah Blade.'},{q:'Come captano i segnali le protesi mioelettriche?',o:['Telecamere','Elettrodi EMG','Infrarossi','Magneti'],a:1,e:'✅ EMG: rileva segnali elettrici dei muscoli residui.'},{q:'Quante prese diverse fa una mano bionica avanzata?',o:['5','10','24','50'],a:2,e:'✅ 24 prese! Programmabili via app.'},{q:'Chi ha vinto l\'oro con 4 protesi contemporaneamente?',o:['F.Pellegrini','Bebe Vio','S.Goggia','V.Vezzali'],a:1,e:'✅ Bebe Vio! Oro paralimpico di scherma.'},{q:'La prima protesi della storia risale a:',o:['100 d.C.','950 a.C.','1500 d.C.','1800 d.C.'],a:1,e:'✅ 950 a.C.! Un alluce in legno su una mummia egizia.'}];
var q1i=0,q1s=0;
function initQ1(){q1i=0;q1s=0;showQ1();}
function showQ1(){if(q1i>=Q1.length){endQ('qb1','🦾',q1s,Q1.length,'initQ1');return;}var q=Q1[q1i];document.getElementById('q1t').textContent='Domanda '+(q1i+1)+'/'+Q1.length+': '+q.q;var el=document.getElementById('q1o');el.innerHTML='';q.o.forEach(function(o,i){var b=document.createElement('button');b.className='qo';b.textContent=o;b.onclick=function(){ansQ('q1',i,q1i,Q1,1);};el.appendChild(b);});document.getElementById('q1f').className='qfb';document.getElementById('q1n').className='qnx';}
function nxQ1(){q1i++;showQ1();}

// ── QUIZ 2 ──
var Q2=[{q:'Quanti neuroni ha il cervello umano?',o:['1 miliardo','10 miliardi','86 miliardi','1 trilione'],a:2,e:'✅ 86 miliardi! Quasi quante le stelle della Via Lattea.'},{q:'Come si chiama la capacit\u00e0 del cervello di formare nuove connessioni?',o:['Neurogenesi','Neuroplasticit\u00e0','Sinapsi','Mielinizzazione'],a:1,e:'✅ Neuroplasticit\u00e0! Il cervello si rimodella ogni volta che impari.'},{q:'Quale neurotrasmettitore \u00e8 legato al piacere?',o:['Serotonina','GABA','Dopamina','Glutammato'],a:2,e:'✅ Dopamina! Rilasciata quando raggiungi un obiettivo.'},{q:'A che velocit\u00e0 viaggia un segnale nervoso?',o:['10 m/s','50 m/s','120 m/s','300 m/s'],a:2,e:'✅ 120 m/s! Grazie alla guaina mielinica.'},{q:'Quanta energia consuma il cervello?',o:['5%','10%','20%','30%'],a:2,e:'✅ 20%! Lavora senza sosta anche mentre dormi.'}];
var q2i=0,q2s=0;
function initQ2(){q2i=0;q2s=0;showQ2();}
function showQ2(){if(q2i>=Q2.length){endQ('qb2','🧠',q2s,Q2.length,'initQ2');return;}var q=Q2[q2i];document.getElementById('q2t').textContent='Domanda '+(q2i+1)+'/'+Q2.length+': '+q.q;var el=document.getElementById('q2o');el.innerHTML='';q.o.forEach(function(o,i){var b=document.createElement('button');b.className='qo';b.textContent=o;b.onclick=function(){ansQ('q2',i,q2i,Q2,2);};el.appendChild(b);});document.getElementById('q2f').className='qfb';document.getElementById('q2n').className='qnx';}
function nxQ2(){q2i++;showQ2();}

// ── QUIZ 3 ──
var Q3=[{q:'Quale macchinario misura i segnali elettrici con elettrodi sul cuoio capelluto?',o:['fMRI','PET','EEG','MEG'],a:2,e:'✅ EEG! Economico, veloce, usato anche a casa.'},{q:'Cosa misura la fMRI?',o:['Segnali elettrici','Flusso di sangue ossigenato','Campi magnetici','Radiazioni gamma'],a:1,e:'✅ Flusso di sangue ossigenato — le zone attive consumano pi\u00f9 ossigeno.'},{q:'Quale usa traccianti radioattivi?',o:['EEG','MEG','TMS','PET'],a:3,e:'✅ PET — Tomografia a Emissione di Positroni.'},{q:'Quanto prima rileva l\'Alzheimer la PET/fMRI?',o:['1 anno','5 anni','10 anni','20 anni'],a:3,e:'✅ 20 anni prima dei sintomi! Apre la strada a terapie preventive.'},{q:"Cos\'\u00e8 la TMS?",o:['Uno scanner','Stimolazione Magnetica Transcranica','Un analgesico','Un microprocessore'],a:1,e:'✅ TMS stimola i neuroni con impulsi magnetici!'}];
var q3i=0,q3s=0;
function initQ3(){q3i=0;q3s=0;showQ3();}
function showQ3(){if(q3i>=Q3.length){endQ('qb3','🔬',q3s,Q3.length,'initQ3');return;}var q=Q3[q3i];document.getElementById('q3t').textContent='Domanda '+(q3i+1)+'/'+Q3.length+': '+q.q;var el=document.getElementById('q3o');el.innerHTML='';q.o.forEach(function(o,i){var b=document.createElement('button');b.className='qo';b.textContent=o;b.onclick=function(){ansQ('q3',i,q3i,Q3,3);};el.appendChild(b);});document.getElementById('q3f').className='qfb';document.getElementById('q3n').className='qnx';}
function nxQ3(){q3i++;showQ3();}

function ansQ(pfx,i,qi,QArr,n){var q=QArr[qi];var opts=document.querySelectorAll('#'+pfx+'o .qo');opts.forEach(function(b){b.style.pointerEvents='none';});var fb=document.getElementById(pfx+'f');if(i===q.a){opts[i].classList.add('ok');if(n===1)q1s++;else if(n===2)q2s++;else q3s++;fb.textContent=q.e;fb.className='qfb show ok';}else{opts[i].classList.add('ko');opts[q.a].classList.add('ok');fb.textContent='❌ '+q.e;fb.className='qfb show ko';}document.getElementById(pfx+'n').className='qnx show';}

function endQ(boxId,ico,score,total,restartFn){var qb=document.getElementById(boxId);qb.innerHTML='<h3>'+ico+' QUIZ COMPLETATO!</h3><div style="font-family:Orbitron,sans-serif;font-size:2rem;font-weight:900;color:#33ccff;text-align:center;margin:16px 0">'+score+'/'+total+'</div><div style="text-align:center;color:#7ab8d4">'+(score===total?'🏆 Perfetto!':score>=total/2?'👍 Ottimo!':'📚 Rileggi e riprova!')+'</div><button class="qnx show" style="margin:12px auto;display:block;cursor:pointer" onclick="'+restartFn+'()">RICOMINCIA ↺</button>';}
function togTL(el){el.parentElement.querySelectorAll('.ti').forEach(function(i){if(i!==el)i.classList.remove('act');});el.classList.toggle('act');}

// ── MODAL DATA ──
var MD={
  corsa:{ico:'🏃',tag:'ATLETICA',h:'Protesi nella Corsa',b:'<p>La <strong>Cheetah Blade</strong> in fibra di carbonio funziona come una molla biologica. Alcuni atleti corrono i 100m in meno di 11 secondi.</p><ul><li>Fibra di carbonio, peso sotto 500g</li><li>Ritorno energetico fino all\'80%</li></ul>'},
  nuoto:{ico:'🏊',tag:'NUOTO',h:'Protesi nel Nuoto',b:'<p>Protesi idrodinamiche ispirate ai delfini. <strong>Jessica Long</strong> ha vinto 13 ori paralimpici.</p><ul><li>Materiali idrofobi anti-corrosione</li><li>Forme testate in vasca</li></ul>'},
  ciclismo:{ico:'🚴',tag:'CICLISMO',h:'Protesi nel Ciclismo',b:'<p>Attacchi rigidi migliorano l\'efficienza della pedalata del <strong>40%</strong>.</p><ul><li>Adattatori SPD/Look universali</li><li>Sensori di potenza integrati</li></ul>'},
  basket:{ico:'🏀',tag:'BASKET',h:'Protesi nel Basket',b:'<p>La <strong>i-Limb Ultra</strong> risponde in 100ms. 24 prese programmate via app.</p><ul><li>Resistenza agli urti IP67</li><li>Batteria 8 ore</li></ul>'},
  scherma:{ico:'🤺',tag:'SCHERMA',h:'Protesi nella Scherma',b:'<p><strong>Bebe Vio</strong> ha vinto l\'oro con 4 protesi. Adattatori in alluminio aeronautico con sgancio rapido.</p><ul><li>Compatibile con fioretto, sciabola, spada</li></ul>'},
  arrampicata:{ico:'🧗',tag:'ARRAMPICATA',h:'Protesi nell\'Arrampicata',b:'<p>Punte in carbonio o gomma Vibram. Terminali a gancio per prese impossibili per mani biologiche.</p><ul><li>Alta aderenza Vibram</li><li>Peso minimo</li></ul>'},
  plasticita:{ico:'🔄',tag:'NEUROPLASTICIT\u00c0',h:'Il Cervello che si Riscrive',b:'<p>La <strong>neuroplasticit\u00e0</strong> \u00e8 la capacit\u00e0 del cervello di cambiare struttura. Ogni volta che studi, nuove connessioni si formano.</p><ul><li>I musicisti hanno il corpo calloso pi\u00f9 grande del normale</li><li>I tassisti londinesi hanno l\'ippocampo ingrandito</li><li>Bastano 21 giorni di pratica per nuove connessioni durature</li></ul>'},
  sogno:{ico:'💤',tag:'SONNO E MEMORIA',h:'Dormi e Impara Meglio',b:'<p>Durante il sonno <strong>REM</strong> il cervello consolida i ricordi. Dormire dopo aver studiato migliora la memorizzazione del <strong>40%</strong>.</p><ul><li>La privazione di sonno uccide neuroni in 72 ore</li><li>I sogni "ordinano" i ricordi importanti</li></ul>'},
  dopamina:{ico:'😊',tag:'NEUROTRASMETTITORI',h:'La Chimica delle Emozioni',b:'<p>Molecole che i neuroni usano per comunicare:</p><ul><li><strong>Dopamina:</strong> piacere, motivazione</li><li><strong>Serotonina:</strong> umore, benessere, sonno</li><li><strong>Adrenalina:</strong> risposta al pericolo</li><li><strong>Ossitocina:</strong> amore, fiducia</li><li><strong>GABA:</strong> il "freno" del cervello</li></ul>'},
  aineuroni:{ico:'🤖',tag:'AI E NEURONI',h:'Neuroni Biologici vs Artificiali',b:'<p>Le <strong>reti neurali AI</strong> sono copiate dai neuroni biologici. Il cervello \u00e8 1000 volte pi\u00f9 efficiente energeticamente dell\'AI migliore.</p><ul><li>Il primo modello matematico del neurone: 1943</li><li>Neuralink legge 1.024 neuroni simultaneamente</li></ul>'},
  malattie:{ico:'⚠️',tag:'NEUROLOGIA',h:'Malattie del Sistema Nervoso',b:'<ul><li><strong>Alzheimer:</strong> proteine tossiche distruggono i neuroni della memoria</li><li><strong>Parkinson:</strong> morte dei neuroni dopaminergici</li><li><strong>Sclerosi multipla:</strong> il sistema immunitario attacca la guaina mielinica</li><li><strong>Epilessia:</strong> scariche elettriche anomale</li></ul>'},
  record:{ico:'🏆',tag:'RECORD',h:'I Record del Cervello',b:'<ul><li>Memoria stimata: <strong>2.5 petabyte</strong></li><li>Neuroni: <strong>86 miliardi</strong></li><li>Sinapsi: <strong>100-500 trilioni</strong></li><li>Velocit\u00e0: <strong>120 m/s</strong></li><li>Energia: <strong>20 watt</strong></li></ul>'},
  eeg:{ico:'🧠',tag:'EEG',h:'EEG — Ascoltare il Cervello',b:'<p>L\'EEG usa <strong>elettrodi sul cuoio capelluto</strong> per misurare l\'attivit\u00e0 elettrica dei neuroni.</p><ul><li>Risoluzione temporale: millisecondi — il pi\u00f9 veloce</li><li>Usato per epilessia, disturbi del sonno, coma</li><li>Oggi esistono versioni portatili da indossare</li></ul>'},
  fmri:{ico:'🔬',tag:'fMRI',h:'fMRI — Vedere i Pensieri',b:'<p>La <strong>fMRI</strong> misura il flusso di sangue ossigenato. Alta precisione spaziale ma ritardo di 2-5 secondi.</p><ul><li>Risoluzione spaziale: 1-3 mm</li><li>Costo: 1-3 milioni di euro</li><li>Usata prima di operazioni neurochirurgiche</li></ul>'},
  pet:{ico:'⚛️',tag:'PET',h:'PET — Radioattivit\u00e0 e Cervello',b:'<p>La <strong>PET</strong> inietta un tracciante radioattivo. Le zone pi\u00f9 attive lo assorbono di pi\u00f9.</p><ul><li>Diagnostica tumori e Alzheimer</li><li>Rileva l\'Alzheimer 20 anni prima dei sintomi</li><li>Costo esame: 2.000-4.000€</li></ul>'},
  meg:{ico:'📡',tag:'MEG',h:'MEG — Campi Magnetici del Pensiero',b:'<p>La <strong>MEG</strong> misura i debolissimi campi magnetici dei neuroni. Precisissima ma rarissima.</p><ul><li>Nel mondo esistono meno di 200 macchine MEG</li><li>Costo: 2-5 milioni di euro per installazione</li></ul>'},
  neuralink:{ico:'🔩',tag:'NEURALINK',h:'Neuralink e il Futuro',b:'<p><strong>Neuralink</strong> ha impiantato chip cerebrali in pazienti umani nel 2024. Legge 1.024 neuroni simultaneamente.</p><ul><li>Il primo paziente controlla il mouse col pensiero</li><li>Obiettivo: ripristinare mobilit\u00e0 in paralizzati</li><li>Il futuro: upload e download di ricordi?</li></ul>'},
  futuro:{ico:'🚀',tag:'IL FUTURO',h:'La Neurotecnologia del Futuro',b:'<ul><li><strong>Neuroni artificiali:</strong> chip che sostituiscono neuroni danneggiati</li><li><strong>Terapia diretta:</strong> stimolazione precisa per curare depressione e Parkinson</li><li><strong>Comunicazione telepatica:</strong> gi\u00e0 dimostrata tra due cervelli in laboratorio</li></ul>'},
};
function OM(k){var s=MD[k];if(!s)return;document.getElementById('mt').textContent=s.tag;document.getElementById('mi').textContent=s.ico;document.getElementById('mh').textContent=s.h;document.getElementById('mb').innerHTML=s.b;document.getElementById('ov').classList.add('open');}
function CM(){document.getElementById('ov').classList.remove('open');}

// ── ROBOT FUN FACTS ──
var ROBOT_FACTS=[
  // Parte 1 (protesi)
  'La prima protesi risale al <strong>950 a.C.</strong>: alluce in legno su mummia egizia!',
  'Le protesi usano l\'<strong>AI</strong> per adattarsi al passo di ogni persona.',
  'Bebe Vio: oro olimpico con <strong>4 protesi</strong> contemporaneamente.',
  'La <strong>LUKE Arm</strong> ha 10 gradi di libert\u00e0 e pu\u00f2 sentire la pressione!',
  // Parte 2 (neuroni)
  'Il tuo cervello genera <strong>23 watt</strong> — abbastanza per una lampadina!',
  'Hai <strong>86 miliardi</strong> di neuroni — quasi quante le stelle della Via Lattea.',
  'Un segnale nervoso viaggia a <strong>120 m/s</strong> — pi\u00f9 veloce di un\'auto da corsa.',
  'Ogni pensiero che fai <strong>cambia fisicamente il cervello</strong>.',
  // Parte 3 (tecnologia)
  'L\'EEG fu inventato nel <strong>1924</strong> e tenuto segreto per 5 anni!',
  'Una fMRI usa un magnete <strong>60.000 volte pi\u00f9 potente</strong> del campo terrestre.',
  'La PET pu\u00f2 rilevare l\'<strong>Alzheimer 20 anni prima</strong> dei sintomi.',
  'Esistono gi\u00e0 <strong>caschi EEG da 50-200€</strong> per uso domestico.',
];
var lf=-1;
function SFF(){var i;do{i=Math.floor(Math.random()*ROBOT_FACTS.length);}while(i===lf);lf=i;document.getElementById('rbt').innerHTML=ROBOT_FACTS[i];document.getElementById('rb').classList.add('show');}
function CRB(){document.getElementById('rb').classList.remove('show');}

// Init quizzes
document.addEventListener('DOMContentLoaded',function(){initQ1();});
</script>
</body>
</html>
