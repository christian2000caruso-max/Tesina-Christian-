<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Consulenza Bagno — Manuale Operativo</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,300&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
<style>
:root{
  --navy:#0a1628;
  --navy2:#112040;
  --blue:#1a4fd6;
  --blue-light:#3b6ef0;
  --sky:#e8eeff;
  --accent:#f0a500;
  --accent2:#ffe8b0;
  --slate:#4a5568;
  --muted:#8896a8;
  --line:#e2e8f0;
  --white:#ffffff;
  --bg:#f5f7fa;
  --green:#16a34a;
  --green-bg:#dcfce7;
  --amber:#b45309;
  --amber-bg:#fef3c7;
  --red:#dc2626;
  --red-bg:#fee2e2;
  --indigo:#3730a3;
  --indigo-bg:#e0e7ff;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html,body{width:100%;height:100%;overflow:hidden;font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--navy)}

/* ══════════════════════════════════
   APP SHELL
══════════════════════════════════ */
#app{position:fixed;inset:0;overflow:hidden}
.slide{
  position:absolute;inset:0;
  display:flex;flex-direction:column;
  opacity:0;pointer-events:none;
  transition:opacity .45s ease,transform .45s cubic-bezier(.4,0,.2,1);
  transform:translateX(48px);
}
.slide.active{opacity:1;pointer-events:all;transform:translateX(0)}
.slide.out{opacity:0;transform:translateX(-48px)}

/* ══════════════════════════════════
   SIDEBAR NAV
══════════════════════════════════ */
.layout{display:grid;grid-template-columns:72px 1fr;height:100%;overflow:hidden}
.sidebar{
  background:var(--navy);
  display:flex;flex-direction:column;
  align-items:center;
  padding:1.2rem 0;
  gap:6px;
  z-index:20;
}
.sidebar-logo{
  width:36px;height:36px;background:var(--blue);
  display:flex;align-items:center;justify-content:center;
  font-family:'DM Serif Display',serif;font-size:16px;font-weight:400;color:#fff;
  margin-bottom:.8rem;border-radius:8px;
  flex-shrink:0;
}
.step-dot{
  width:36px;height:36px;border-radius:50%;
  display:flex;align-items:center;justify-content:center;
  font-size:10px;font-weight:600;color:rgba(255,255,255,.35);
  cursor:pointer;transition:all .2s;position:relative;
  flex-shrink:0;
}
.step-dot:hover{background:rgba(255,255,255,.08);color:rgba(255,255,255,.7)}
.step-dot.visited{color:rgba(255,255,255,.55)}
.step-dot.visited::after{
  content:'';position:absolute;right:8px;top:8px;
  width:6px;height:6px;border-radius:50%;background:var(--blue-light);
}
.step-dot.current{
  background:var(--blue);color:#fff;font-weight:600;
  box-shadow:0 0 0 3px rgba(59,110,240,.3);
}
.step-dot.current::after{display:none}
.sidebar-bottom{margin-top:auto;display:flex;flex-direction:column;align-items:center;gap:8px;padding-bottom:.5rem}
.nav-arrow{
  width:32px;height:32px;border-radius:50%;border:1px solid rgba(255,255,255,.15);
  background:transparent;color:rgba(255,255,255,.5);cursor:pointer;
  display:flex;align-items:center;justify-content:center;font-size:13px;
  transition:all .2s;
}
.nav-arrow:hover:not(:disabled){background:rgba(255,255,255,.1);color:#fff;border-color:rgba(255,255,255,.4)}
.nav-arrow:disabled{opacity:.25;cursor:default}

/* ══════════════════════════════════
   MAIN CONTENT AREA
══════════════════════════════════ */
.main{
  display:flex;flex-direction:column;overflow:hidden;
  background:var(--bg);
}

/* Top header bar */
.topbar{
  display:flex;align-items:center;justify-content:space-between;
  padding:.75rem 2rem;
  background:var(--white);
  border-bottom:1px solid var(--line);
  flex-shrink:0;
  gap:1rem;
}
.topbar-phase{
  font-size:11px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;
  color:var(--blue);background:var(--sky);
  padding:4px 12px;border-radius:20px;
  white-space:nowrap;
}
.topbar-title{font-size:14px;font-weight:500;color:var(--navy);flex:1;text-align:center}
.topbar-right{display:flex;align-items:center;gap:.75rem;white-space:nowrap}
.topbar-counter{font-size:12px;color:var(--muted);font-weight:500}
.topbar-time{
  font-size:11px;font-weight:600;color:var(--amber);
  background:var(--amber-bg);padding:3px 10px;border-radius:20px;
}

/* Progress bar */
.progress-wrap{height:3px;background:var(--line);flex-shrink:0}
.progress-bar{height:100%;background:linear-gradient(90deg,var(--blue),var(--blue-light));transition:width .5s ease;border-radius:0 2px 2px 0}

/* Scroll body */
.content-body{flex:1;overflow-y:auto;padding:2rem 2.5rem 3rem}
.content-body::-webkit-scrollbar{width:4px}
.content-body::-webkit-scrollbar-track{background:transparent}
.content-body::-webkit-scrollbar-thumb{background:var(--line);border-radius:2px}
.content-body::-webkit-scrollbar-thumb:hover{background:#c0ccd8}

/* ══════════════════════════════════
   CONTENT ATOMS
══════════════════════════════════ */
.section-header{margin-bottom:1.8rem}
.section-tag{
  display:inline-flex;align-items:center;gap:6px;
  font-size:11px;font-weight:600;letter-spacing:.1em;text-transform:uppercase;
  color:var(--muted);margin-bottom:.6rem;
}
.section-tag .tag-num{
  display:inline-flex;align-items:center;justify-content:center;
  width:20px;height:20px;border-radius:50%;
  background:var(--navy);color:#fff;font-size:9px;font-weight:700;
}
.section-h{
  font-family:'DM Serif Display',serif;
  font-size:clamp(22px,2.8vw,34px);
  font-weight:400;color:var(--navy);line-height:1.2;
  margin-bottom:.5rem;
}
.section-sub{font-size:14px;color:var(--slate);line-height:1.6;max-width:620px}

/* Goal banner */
.goal-banner{
  display:flex;align-items:flex-start;gap:12px;
  background:var(--sky);border-left:3px solid var(--blue);
  padding:.85rem 1.1rem;border-radius:0 8px 8px 0;
  margin-bottom:1.6rem;
}
.goal-icon{font-size:16px;flex-shrink:0;margin-top:1px}
.goal-text{font-size:13.5px;color:var(--navy2);line-height:1.55;font-weight:500}

/* Card grid */
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:1rem}
.grid-3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:1rem}
@media(max-width:720px){.grid-2,.grid-3{grid-template-columns:1fr}}

.card{
  background:var(--white);border:1px solid var(--line);
  border-radius:10px;padding:1.1rem 1.2rem;
}
.card-tag{font-size:10px;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:var(--muted);margin-bottom:.5rem}
.card-h{font-size:14px;font-weight:600;color:var(--navy);margin-bottom:.4rem}
.card-p{font-size:13.5px;color:var(--slate);line-height:1.6}
.card.accent{border-color:var(--blue);background:var(--sky)}
.card.warn{border-color:var(--amber);background:var(--amber-bg)}
.card.success{border-color:var(--green);background:var(--green-bg)}

/* Script block */
.script{
  background:var(--navy);border-radius:10px;
  padding:1rem 1.3rem;margin-bottom:.85rem;
}
.script-lbl{font-size:10px;font-weight:700;letter-spacing:.12em;text-transform:uppercase;color:var(--blue-light);margin-bottom:.5rem}
.script-body{font-size:14px;color:#e2e8f0;line-height:1.7;font-style:italic}

/* Highlight bubble */
.bubble{
  display:inline-flex;align-items:center;gap:6px;
  background:var(--white);border:1px solid var(--line);
  border-radius:8px;padding:.6rem .9rem;margin:.3rem .3rem .3rem 0;
  font-size:13px;color:var(--navy);font-weight:500;
}
.bubble-dot{width:8px;height:8px;border-radius:50%}

/* Objection table */
.obj-table{background:var(--white);border:1px solid var(--line);border-radius:10px;overflow:hidden;margin-bottom:.5rem}
.obj-header{display:grid;grid-template-columns:1fr 1.8fr;gap:0;background:var(--navy);padding:.55rem 1rem}
.obj-header span{font-size:10px;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:rgba(255,255,255,.5)}
.obj-row{display:grid;grid-template-columns:1fr 1.8fr;gap:0;border-top:1px solid var(--line);padding:.85rem 1rem;align-items:start;transition:background .15s}
.obj-row:hover{background:var(--bg)}
.obj-q{font-size:13px;font-weight:600;color:var(--red);line-height:1.5;padding-right:1rem}
.obj-a{font-size:13px;color:var(--slate);line-height:1.55}
.obj-note{font-size:11px;color:var(--muted);margin-top:.3rem;font-style:italic}

/* Price cards */
.price-level{
  background:var(--white);border:1px solid var(--line);border-radius:10px;
  padding:1rem 1.2rem;margin-bottom:.75rem;
  display:grid;grid-template-columns:auto 1fr auto;gap:.5rem 1rem;align-items:start;
  transition:border-color .2s;
}
.price-level:hover{border-color:#b0bfd0}
.price-badge{
  display:inline-flex;align-items:center;justify-content:center;
  width:32px;height:32px;border-radius:8px;font-size:12px;font-weight:700;flex-shrink:0;margin-top:2px;
}
.price-name{font-size:13px;font-weight:700;color:var(--navy)}
.price-sub{font-size:12.5px;color:var(--slate);line-height:1.5;grid-column:2;margin-top:-.2rem}
.price-chip{
  font-size:10px;font-weight:700;letter-spacing:.05em;
  padding:3px 10px;border-radius:20px;white-space:nowrap;
  align-self:start;margin-top:4px;
}
.price-note{font-size:11.5px;color:var(--muted);grid-column:2/-1;font-style:italic;border-top:1px solid var(--line);padding-top:.5rem;margin-top:.3rem}

/* Checklist */
.checklist{background:var(--white);border:1px solid var(--line);border-radius:10px;overflow:hidden}
.check-item{
  display:flex;align-items:center;gap:.9rem;
  padding:.8rem 1.1rem;border-bottom:1px solid var(--line);cursor:pointer;
  transition:background .15s;
}
.check-item:last-child{border-bottom:none}
.check-item:hover{background:var(--bg)}
.checkbox{
  width:20px;height:20px;border-radius:5px;border:2px solid var(--line);
  flex-shrink:0;display:flex;align-items:center;justify-content:center;
  transition:all .2s;
}
.check-item.done .checkbox{background:var(--green);border-color:var(--green)}
.check-item.done .checkbox::after{content:'✓';font-size:12px;font-weight:700;color:#fff}
.check-label{font-size:13.5px;color:var(--navy);transition:color .2s;font-weight:400}
.check-item.done .check-label{color:var(--muted);text-decoration:line-through}
.check-footer{
  display:flex;align-items:center;justify-content:space-between;
  padding:.75rem 1.1rem;background:var(--bg);border-top:1px solid var(--line);
  font-size:12px;color:var(--muted);font-weight:500;
}
.check-progress-bar{height:4px;background:var(--line);border-radius:2px;width:120px;overflow:hidden}
.check-progress-fill{height:100%;background:var(--green);border-radius:2px;transition:width .3s}

/* Rules */
.rule-card{
  display:flex;gap:1rem;align-items:flex-start;
  background:var(--white);border:1px solid var(--line);border-radius:10px;
  padding:1rem 1.2rem;margin-bottom:.75rem;
  transition:border-color .2s,box-shadow .2s;
}
.rule-card:hover{border-color:var(--blue);box-shadow:0 2px 12px rgba(26,79,214,.08)}
.rule-n{
  width:32px;height:32px;background:var(--navy);color:#fff;
  border-radius:8px;display:flex;align-items:center;justify-content:center;
  font-size:13px;font-weight:700;flex-shrink:0;
}
.rule-text{font-size:14px;color:var(--slate);line-height:1.6}
.rule-text strong{color:var(--navy);font-weight:600}

/* Divider */
.divider{height:1px;background:var(--line);margin:1.5rem 0}

/* ══════════════════════════════════
   SLIDE 0 — COVER
══════════════════════════════════ */
#s0{background:var(--navy);align-items:center;justify-content:center}
.cover-inner{
  display:flex;flex-direction:column;align-items:flex-start;
  max-width:680px;padding:3rem;
}
.cover-kicker{
  font-size:11px;font-weight:700;letter-spacing:.15em;text-transform:uppercase;
  color:var(--blue-light);margin-bottom:1.5rem;
  display:flex;align-items:center;gap:10px;
}
.cover-kicker::before{content:'';display:block;width:24px;height:2px;background:var(--blue-light)}
.cover-h{
  font-family:'DM Serif Display',serif;
  font-size:clamp(30px,5vw,58px);font-weight:400;
  color:#fff;line-height:1.1;margin-bottom:1.2rem;
}
.cover-h em{color:var(--accent);font-style:italic}
.cover-sub{font-size:16px;color:rgba(255,255,255,.5);line-height:1.7;margin-bottom:2.5rem;max-width:480px}
.cover-meta{
  display:flex;align-items:center;gap:1.5rem;margin-bottom:2.5rem;
  padding-bottom:1.5rem;border-bottom:1px solid rgba(255,255,255,.1);width:100%;
}
.meta-item{display:flex;align-items:center;gap:6px;font-size:13px;color:rgba(255,255,255,.45)}
.meta-dot{width:6px;height:6px;border-radius:50%;background:var(--blue-light);flex-shrink:0}
.btn-cover{
  display:inline-flex;align-items:center;gap:.6rem;
  background:var(--blue);color:#fff;border:none;
  padding:.9rem 2rem;border-radius:8px;font-size:14px;font-weight:600;
  cursor:pointer;font-family:'DM Sans',sans-serif;
  transition:background .2s,transform .15s;letter-spacing:.01em;
}
.btn-cover:hover{background:var(--blue-light);transform:translateY(-1px)}
.btn-cover:active{transform:translateY(0)}
.btn-cover .arrow{font-size:16px;transition:transform .2s}
.btn-cover:hover .arrow{transform:translateX(3px)}
.cover-phases{
  display:flex;flex-wrap:wrap;gap:.5rem;margin-top:2rem;
}
.phase-pill{
  font-size:11px;font-weight:500;color:rgba(255,255,255,.4);
  background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.1);
  padding:4px 12px;border-radius:20px;
}

/* ══════════════════════════════════
   FINAL SLIDE
══════════════════════════════════ */
.final-wrap{
  flex:1;display:flex;align-items:center;justify-content:center;
  background:var(--bg);
}
.final-card{
  background:var(--white);border:1px solid var(--line);border-radius:16px;
  padding:3rem;text-align:center;max-width:520px;
  box-shadow:0 8px 40px rgba(10,22,40,.08);
}
.final-icon{font-size:48px;margin-bottom:1.2rem}
.final-h{font-family:'DM Serif Display',serif;font-size:28px;color:var(--navy);margin-bottom:.8rem}
.final-p{font-size:15px;color:var(--slate);line-height:1.7;margin-bottom:2rem}

/* ══════════════════════════════════
   ANIMATIONS
══════════════════════════════════ */
@keyframes fadeUp{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}
.cover-inner > *{animation:fadeUp .6s ease both}
.cover-inner > *:nth-child(1){animation-delay:.1s}
.cover-inner > *:nth-child(2){animation-delay:.2s}
.cover-inner > *:nth-child(3){animation-delay:.3s}
.cover-inner > *:nth-child(4){animation-delay:.4s}
.cover-inner > *:nth-child(5){animation-delay:.5s}
.cover-inner > *:nth-child(6){animation-delay:.6s}
</style>
</head>
<body>
<div id="app">

<!-- ══════════════════════════════
     SLIDE 0 — COVER
══════════════════════════════ -->
<div class="slide active" id="s0">
  <div class="cover-inner">
    <div class="cover-kicker">Massimiliano Production · Formazione Vendita</div>
    <h1 class="cover-h">Manuale Operativo<br>Consulenza Bagno<br><em>Domiciliare</em></h1>
    <p class="cover-sub">Guida completa alle 14 fasi della consulenza — dall'apertura alla chiusura. Metodo strutturato, script pronti, gestione obiezioni.</p>
    <div class="cover-meta">
      <div class="meta-item"><div class="meta-dot"></div>14 Fasi operative</div>
      <div class="meta-item"><div class="meta-dot"></div>Script pronti all'uso</div>
      <div class="meta-item"><div class="meta-dot"></div>Checklist interattiva</div>
    </div>
    <button class="btn-cover" onclick="goTo(1)">Inizia il corso <span class="arrow">→</span></button>
    <div class="cover-phases">
      <span class="phase-pill">Apertura</span><span class="phase-pill">Intervista</span><span class="phase-pill">Bisogni</span>
      <span class="phase-pill">Sopralluogo</span><span class="phase-pill">Materiali</span><span class="phase-pill">Proposta</span>
      <span class="phase-pill">Valore</span><span class="phase-pill">Prezzo</span><span class="phase-pill">Chiusura</span>
      <span class="phase-pill">Obiezioni</span><span class="phase-pill">Checklist</span><span class="phase-pill">Regole d'Oro</span>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 1 — APERTURA & POSIZIONAMENTO
══════════════════════════════ -->
<div class="slide" id="s1">
  <div class="layout">
    <div class="sidebar" id="sb1"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 1</span>
        <span class="topbar-title">Apertura & Posizionamento</span>
        <div class="topbar-right">
          <span class="topbar-time">⏱ 10–15 min</span>
          <span class="topbar-counter">1 / 14</span>
        </div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:7.1%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">1</span>Prima impressione</div>
          <h2 class="section-h">Apertura &amp; Posizionamento</h2>
          <p class="section-sub">Il primo contatto definisce tutto il resto. Professionale, chiaro, rassicurante.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Ottenere il primo micro-impegno. Stabilire il metodo e il tuo ruolo come consulente, non come venditore.</div></div>
        <div class="grid-2">
          <div>
            <div class="card" style="margin-bottom:.85rem">
              <div class="card-tag">Azione d'ingresso</div>
              <div class="card-h">Gestisci il primo minuto</div>
              <div class="card-p">Sedetevi e levatevi il giubbino. Se offrono il caffè, rifiutate — chiedete un po' d'acqua. Segnala disponibilità, non fretta.</div>
            </div>
            <div class="card" style="margin-bottom:.85rem">
              <div class="card-tag">Osservazione ambiente</div>
              <div class="card-h">Leggi la stanza</div>
              <div class="card-p">Fotografie, bambini, animali domestici, oggetti personali → punti di contatto per entrare in sintonia naturale.</div>
            </div>
            <div class="card" style="margin-bottom:.85rem">
              <div class="card-tag">Domanda chiave</div>
              <div class="card-h">Complimenti alla casa</div>
              <div class="card-p">Falli sempre — anche se la casa non è bella. Poi chiedi: <em>"È di proprietà?"</em> → serve per valutare la detrazione fiscale.</div>
            </div>
          </div>
          <div>
            <div class="card" style="margin-bottom:.85rem">
              <div class="card-tag">Profilazione finanziaria</div>
              <div class="card-h">Occupazione del cliente</div>
              <div class="card-p">Chiedete di cosa si occupa o occupava. Serve a valutare le possibilità di finanziamento e la sua capacità di spesa.</div>
            </div>
            <div class="card accent" style="margin-bottom:.85rem">
              <div class="card-tag" style="color:var(--blue)">⚠ Punto Critico</div>
              <div class="card-h">Identifica il decisore</div>
              <div class="card-p">Se sembra solo: <em>"Bella casa, vive da solo?"</em> — Capisci se c'è un secondo decisore. Se non lo fai adesso, pagherai in fase di chiusura con "ne devo parlare con…"</div>
            </div>
            <div class="card warn">
              <div class="card-tag" style="color:var(--amber)">Regola d'Oro</div>
              <div class="card-h">Mai procedere senza decisore</div>
              <div class="card-p">Se il decisore non è presente, l'obiettivo della visita è solo raccogliere info e fissare una seconda visita con entrambi.</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 2 — INTERVISTA
══════════════════════════════ -->
<div class="slide" id="s2">
  <div class="layout">
    <div class="sidebar" id="sb2"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 2</span>
        <span class="topbar-title">Intervista Iniziale</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 5–10 min</span><span class="topbar-counter">2 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:14.2%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">2</span>Costruire il rapporto</div>
          <h2 class="section-h">Intervista Iniziale</h2>
          <p class="section-sub">Far percepire al cliente che non stai vendendo — stai decidendo insieme a lui.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Raccogliere le motivazioni d'acquisto e ottenere il consenso al metodo di lavoro — il tuo primo micro-sì esplicito.</div></div>
        <div class="script" style="margin-bottom:1rem">
          <div class="script-lbl">🔄 Script 1 — Come è arrivato a noi</div>
          <div class="script-body">"Come è arrivato a conoscerci? È stato qualcuno a consigliarla?"</div>
        </div>
        <div class="script" style="margin-bottom:1rem">
          <div class="script-lbl">🔄 Script 2 — Motivazione principale</div>
          <div class="script-body">"Cosa l'ha spinta a chiamarci? Rapidità dei lavori, prezzo, possibilità di rateizzare…?"</div>
        </div>
        <div class="script" style="margin-bottom:1.5rem">
          <div class="script-lbl">🔄 Script 3 — Impostazione del metodo (il più importante)</div>
          <div class="script-body">"Oggi il mio obiettivo non è solo capire il bagno, ma decidere insieme se e come rifarlo. Le va se lavoriamo così?"</div>
        </div>
        <div class="card success">
          <div class="card-tag" style="color:var(--green)">✅ Attendi questa risposta</div>
          <div class="card-h">Il Primo Micro-Sì</div>
          <div class="card-p">Non continuare finché non ottieni una risposta affermativa esplicita allo Script 3. È il fondamento dell'intera consulenza — senza questo sì, non hai il suo consenso a procedere.</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 3 — SCOPERTA BISOGNI
══════════════════════════════ -->
<div class="slide" id="s3">
  <div class="layout">
    <div class="sidebar" id="sb3"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 3</span>
        <span class="topbar-title">Scoperta dei Bisogni</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 5–10 min</span><span class="topbar-counter">3 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:21.4%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">3</span>Leve emotive</div>
          <h2 class="section-h">Scoperta dei Bisogni</h2>
          <p class="section-sub">Scavare su motivazioni, urgenze, emozioni e potere decisionale. Ogni risposta è munizione per la chiusura.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Raccogliere almeno 3 micro-sì e identificare la leva emotiva principale. Non proporre soluzioni — ascolta e annota.</div></div>
        <div class="grid-2">
          <div>
            <div class="script"><div class="script-lbl">🔄 Motivazione</div><div class="script-body">"Cosa la spinge a rifare il bagno proprio ora?"</div></div>
            <div class="script"><div class="script-lbl">🔄 Dolore principale</div><div class="script-body">"Qual è la cosa che più la infastidisce oggi nel suo bagno?"</div></div>
            <div class="script"><div class="script-lbl">🔄 Urgenza</div><div class="script-body">"Se non fosse fatto entro 3-6 mesi, che problema le creerebbe?"</div></div>
            <div class="script"><div class="script-lbl">🔄 Decisore</div><div class="script-body">"Chi oltre a lei prende la decisione finale?"</div></div>
          </div>
          <div>
            <div class="card" style="margin-bottom:.85rem">
              <div class="card-tag">Leve emotive — Annota queste</div>
              <div class="card-p" style="margin-top:.2rem">
                <div class="bubble"><div class="bubble-dot" style="background:#3b6ef0"></div>Comfort</div>
                <div class="bubble"><div class="bubble-dot" style="background:#16a34a"></div>Sicurezza</div>
                <div class="bubble"><div class="bubble-dot" style="background:#9333ea"></div>Pulizia facile</div>
                <div class="bubble"><div class="bubble-dot" style="background:#f0a500"></div>Valore casa</div>
                <div class="bubble"><div class="bubble-dot" style="background:#dc2626"></div>Estetica</div>
                <div class="bubble"><div class="bubble-dot" style="background:#0891b2"></div>Salute</div>
              </div>
            </div>
            <div class="card accent">
              <div class="card-tag" style="color:var(--blue)">Tecnica Micro-Sì</div>
              <div class="card-h">Rispecchia le sue parole</div>
              <div class="card-p">Dopo ogni risposta ripeti la parola chiave usata dal cliente: <em>"Quindi per lei la pulizia facile è fondamentale…"</em> — il cliente annuisce e tu accumuli impegno progressivo.</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 4 — ALLINEAMENTO
══════════════════════════════ -->
<div class="slide" id="s4">
  <div class="layout">
    <div class="sidebar" id="sb4"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 4</span>
        <span class="topbar-title">Allineamento e Consenso</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 2 min</span><span class="topbar-counter">4 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:28.5%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">4</span>Conferma e impegno</div>
          <h2 class="section-h">Allineamento e Consenso</h2>
          <p class="section-sub">Il momento di massima fiducia — il cliente si sente compreso. Cristallizza i bisogni prima di passare ai fatti.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Ottenere un "Sì esplicito" di conferma. Questo è il checkpoint che autorizza il passaggio al sopralluogo tecnico.</div></div>
        <div class="script" style="margin-bottom:1.5rem">
          <div class="script-lbl">🔄 Script di Riepilogo — Recita questo con calma e precisione</div>
          <div class="script-body" style="font-size:16px;line-height:1.8">
            "Quindi per lei è fondamentale:<br>
            [lavori rapidi / nessun imprevisto / bagno comodo e facile da pulire].<br><br>
            Ho capito bene?"
          </div>
        </div>
        <div class="card success" style="margin-bottom:1rem">
          <div class="card-tag" style="color:var(--green)">✅ Attendi "Sì, esatto."</div>
          <div class="card-p">Solo con questa conferma procedi alla fase successiva. Il silenzio che segue la domanda è potente — non riempirlo tu.</div>
        </div>
        <div class="grid-2">
          <div class="card"><div class="card-tag">Personalizza le parentesi</div><div class="card-p">Usa le parole <em>esatte</em> del cliente. Se ha detto "sicurezza", non dire "protezione". La precisione crea fiducia.</div></div>
          <div class="card"><div class="card-tag">Perché funziona</div><div class="card-p">Il riepilogo dimostra che hai ascoltato davvero. Più sei preciso, più il cliente si fida — e la fiducia precede l'acquisto.</div></div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 5 — SOPRALLUOGO
══════════════════════════════ -->
<div class="slide" id="s5">
  <div class="layout">
    <div class="sidebar" id="sb5"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 5</span>
        <span class="topbar-title">Sopralluogo Tecnico</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 10–15 min</span><span class="topbar-counter">5 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:35.7%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">5</span>Analisi tecnica sul campo</div>
          <h2 class="section-h">Sopralluogo Tecnico</h2>
          <p class="section-sub">Ogni problema che rilevi è una ragione tecnica per agire adesso. Misura, osserva, spiega.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">📐</div><div class="goal-text">Regola d'Oro: Spiega MENTRE misuri. Non misurare mai in silenzio — ogni azione deve creare valore percepito e urgenza tecnica.</div></div>
        <div class="grid-2">
          <div>
            <div class="script"><div class="script-lbl">🔄 Impianto idrico</div><div class="script-body">"Qui rifare l'impianto ora evita problemi futuri e disagi ben più costosi."</div></div>
            <div class="script"><div class="script-lbl">🔄 Pendenza / Scolo</div><div class="script-body">"Questa pendenza va corretta, altrimenti la doccia darebbe problemi di scolo — e lei lo sente già."</div></div>
            <div class="script"><div class="script-lbl">🔄 Spazio recuperabile</div><div class="script-body">"Possiamo guadagnare spazio con questa soluzione qui — vede come cambierebbe la percezione del bagno?"</div></div>
          </div>
          <div>
            <div class="card" style="margin-bottom:.85rem">
              <div class="card-tag">Lista di controllo tecnica</div>
              <div class="card-p">
                <div style="display:flex;flex-direction:column;gap:6px;margin-top:.3rem">
                  <div style="font-size:13px;color:var(--slate)">☐ Stato impianto idrico e scarichi</div>
                  <div style="font-size:13px;color:var(--slate)">☐ Piastrellatura e condizione pareti</div>
                  <div style="font-size:13px;color:var(--slate)">☐ Ventilazione e umidità</div>
                  <div style="font-size:13px;color:var(--slate)">☐ Spazio movimentazione</div>
                  <div style="font-size:13px;color:var(--slate)">☐ Altezza piano d'appoggio</div>
                  <div style="font-size:13px;color:var(--slate)">☐ Posizione attuale sanitari</div>
                </div>
              </div>
            </div>
            <div class="card warn">
              <div class="card-tag" style="color:var(--amber)">Crea Urgenza Tecnica</div>
              <div class="card-p">Ogni criticità rilevata diventa un argomento per agire oggi — non tra 6 mesi. Collegala sempre al disagio che il cliente ha espresso in fase 3.</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 6 — VISUALIZZAZIONE
══════════════════════════════ -->
<div class="slide" id="s6">
  <div class="layout">
    <div class="sidebar" id="sb6"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 6</span>
        <span class="topbar-title">Visualizzazione &amp; Scelta Materiali</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 5–10 min</span><span class="topbar-counter">6 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:42.8%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">6</span>Dal concetto al progetto</div>
          <h2 class="section-h">Visualizzazione &amp; Scelta Materiali</h2>
          <p class="section-sub">Trasforma idee in progetto concreto. Chi visualizza il risultato finale, compra.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Far "vedere" il bagno finito nella mente del cliente. L'attaccamento emotivo al progetto rende la chiusura quasi automatica.</div></div>
        <div class="grid-2" style="margin-bottom:1rem">
          <div class="card"><div class="card-tag">Step 1 — Piantina</div><div class="card-h">Mostra la nuova disposizione</div><div class="card-p">Anche uno schizzo a mano basta. Crea il senso di progetto — il cliente passa da "voglio rifare" a "questo è il mio bagno".</div></div>
          <div class="card"><div class="card-tag">Step 2 — Campioni fisici</div><div class="card-h">Falli toccare</div><div class="card-p">La sensazione tattile aumenta l'attaccamento emotivo. Non mostrare foto — usa campioni reali di materiale.</div></div>
        </div>
        <div class="script" style="margin-bottom:1rem">
          <div class="script-lbl">🔄 Script — Scelta materiali</div>
          <div class="script-body">"Per l'effetto, preferisce questo gres mat o questa ceramica lucida?"</div>
        </div>
        <div class="grid-2">
          <div class="card"><div class="card-tag">Step 3 — Combinazioni</div><div class="card-h">Proponi 2–3 opzioni complete</div><div class="card-p">Rivestimento + Pavimento + Sanitari. Non vendere à la carte — guida tu verso una delle combinazioni preconfigurate.</div></div>
          <div class="script" style="margin:0">
            <div class="script-lbl">🔄 Annuncio Rendering</div>
            <div class="script-body">"Con queste scelte, le preparo un rendering per vedere esattamente come sarà il suo nuovo bagno."</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 7 — PROPOSTA SOLUZIONE
══════════════════════════════ -->
<div class="slide" id="s7">
  <div class="layout">
    <div class="sidebar" id="sb7"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 7</span>
        <span class="topbar-title">Proposta Soluzione Unica</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 5 min</span><span class="topbar-counter">7 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:50%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">7</span>La soluzione perfetta</div>
          <h2 class="section-h">Proposta Soluzione Unica</h2>
          <p class="section-sub">Una sola proposta. Non due, non tre — quella giusta per lui, come conclusione logica del percorso fatto insieme.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Presentare la soluzione come inevitabile conclusione del percorso. Parla sempre di benefici — mai di caratteristiche tecniche isolate.</div></div>
        <div class="script" style="margin-bottom:1.5rem">
          <div class="script-lbl">🔄 Script Soluzione Unica — Recita questo con sicurezza</div>
          <div class="script-body" style="font-size:15px;line-height:1.8">
            "La soluzione perfetta per lei, come abbiamo visto anche nella bozza, è proprio questo progetto:<br><br>
            con [doccia filo pavimento, sanitari sospesi, materiali facili da pulire].<br><br>
            Così avrà [comfort, sicurezza, zero sorprese], esattamente come ci siamo detti."
          </div>
        </div>
        <div class="grid-2">
          <div class="card">
            <div class="card-tag">❌ Non fare così</div>
            <div class="card-p" style="color:var(--red)">"Proponiamo una doccia walk-in da 140cm con piatto antiscivolo."</div>
          </div>
          <div class="card success">
            <div class="card-tag" style="color:var(--green)">✅ Fai così</div>
            <div class="card-p">"Così avrà uno spazio doccia ampio, senza barriere, sicuro e facilissimo da pulire — come mi ha detto che voleva."</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 8 — SINTESI VALORE
══════════════════════════════ -->
<div class="slide" id="s8">
  <div class="layout">
    <div class="sidebar" id="sb8"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 8</span>
        <span class="topbar-title">Sintesi del Valore Commerciale</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 3 min</span><span class="topbar-counter">8 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:57.1%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">8</span>Prima del prezzo</div>
          <h2 class="section-h">Sintesi del Valore Commerciale</h2>
          <p class="section-sub">Riassumi TUTTO il valore creato prima di pronunciare qualsiasi cifra. Il prezzo deve sembrare adeguato — non caro.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Alzare la percezione del valore al massimo. Più valore percepisci prima del numero, meno il numero spaventa.</div></div>
        <div class="script" style="margin-bottom:1.2rem">
          <div class="script-lbl">🔄 Script di apertura</div>
          <div class="script-body">"Prima di vedere i numeri, mi permetta di riassumere cosa compone esattamente il progetto:"</div>
        </div>
        <div class="grid-2" style="margin-bottom:1rem">
          <div class="card"><div class="card-tag">① Progetto Completo</div><div class="card-p">Rendering e soluzione su misura che risolve i suoi problemi specifici.</div></div>
          <div class="card"><div class="card-tag">② Materiali Selezionati</div><div class="card-p">Tutti i materiali scelti oggi, altissima qualità — 5 anni di garanzia.</div></div>
          <div class="card"><div class="card-tag">③ Servizio Chiavi in Mano</div><div class="card-p">Gestione totale, unico referente, tempi certi. Zero pensieri per il cliente.</div></div>
          <div class="card"><div class="card-tag">④ Garanzia e Assistenza</div><div class="card-p">2 anni di assicurazione sui lavori + supporto post-realizzazione.</div></div>
        </div>
        <div class="card accent">
          <div class="card-tag" style="color:var(--blue)">⑤ Risultato Garantito</div>
          <div class="card-p">La certezza del bagno esattamente come visto nel rendering. Zero sorprese.</div>
        </div>
        <div class="script" style="margin-top:1rem">
          <div class="script-lbl">🔄 Script di chiusura sintesi</div>
          <div class="script-body">"Questo è il pacchetto di valore completo che andiamo a realizzare." [Pausa. Poi presenta il prezzo.]</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 9 — LEVE FINANZIARIE
══════════════════════════════ -->
<div class="slide" id="s9">
  <div class="layout">
    <div class="sidebar" id="sb9"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 9</span>
        <span class="topbar-title">Investimento e Leve Finanziarie</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 5–7 min</span><span class="topbar-counter">9 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:64.2%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">9</span>Prezzo come opportunità</div>
          <h2 class="section-h">Presentazione Investimento</h2>
          <p class="section-sub">Il prezzo non è un costo — è un investimento con ritorni fiscali e condizioni flessibili.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Trasformare la percezione del prezzo usando le leve fiscali e finanziarie prima di rivelare la cifra finale.</div></div>
        <div class="script" style="margin-bottom:1.2rem">
          <div class="script-lbl">🔄 Script di apertura</div>
          <div class="script-body">"È importante considerare due vantaggi finanziari prima di guardare i numeri:"</div>
        </div>
        <div class="grid-2" style="margin-bottom:1rem">
          <div class="card" style="border-color:#16a34a;background:var(--green-bg)">
            <div class="card-tag" style="color:var(--green)">① Recupero Fiscale 50% IRPEF</div>
            <div class="card-h" style="color:var(--green)">Il costo reale si dimezza</div>
            <div class="card-p">Trattandosi di ristrutturazione, metà dell'importo torna in detrazione IRPEF in 5 o 10 anni. Il costo netto è la metà di quello che vede.</div>
            <div class="divider" style="margin:.7rem 0"></div>
            <div class="card-p" style="font-size:12px;color:var(--green)">📋 È legge (art. 16-bis DPR 917/86), prorogata per tutto il 2026. Forniamo noi tutta la documentazione per la dichiarazione dei redditi.</div>
          </div>
          <div class="card" style="border-color:var(--blue);background:var(--sky)">
            <div class="card-tag" style="color:var(--blue)">② Finanziamento Agevolato</div>
            <div class="card-h" style="color:var(--blue)">Rata comoda, zero interessi</div>
            <div class="card-p">Tasso zero fino a 24 mesi. Per una rata ancora più bassa: piano personalizzato fino a 60 mesi.</div>
            <div class="divider" style="margin:.7rem 0"></div>
            <div class="script-body" style="font-size:13px">"La soluzione più comoda: rata fissa di € RRR/mese, nessun interesse."</div>
          </div>
        </div>
        <div class="card warn">
          <div class="card-tag" style="color:var(--amber)">💡 La domanda magica</div>
          <div class="card-p">Chiedi: <em>"Chi può beneficiare della detrazione fiscale?"</em> — attendi la risposta.<br>Poi subito: <em>"Ho bisogno della carta d'identità e della tessera sanitaria."</em><br>Il cliente si attiverà automaticamente.</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 10 — CHIUSURA GUIDATA
══════════════════════════════ -->
<div class="slide" id="s10">
  <div class="layout">
    <div class="sidebar" id="sb10"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 10</span>
        <span class="topbar-title">Chiusura Guidata</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 5 min</span><span class="topbar-counter">10 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:71.4%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">10</span>Assumere il sì</div>
          <h2 class="section-h">Chiusura Guidata</h2>
          <p class="section-sub">Non chiedere "lo facciamo?" — assumi l'accordo e fai scegliere tra due opzioni entrambe positive.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Guidare il cliente verso la scelta di COME procedere — non SE procedere. La domanda presuppone già il sì.</div></div>
        <div class="script" style="margin-bottom:1rem">
          <div class="script-lbl">🔄 Script A — Scelta della modalità di pagamento</div>
          <div class="script-body" style="font-size:15px;line-height:1.8">"Per approfittare dello sconto, della detrazione e della rata comoda, preferirebbe procedere con il pagamento in contanti o con la rata a tasso zero?<br><br>Possiamo attivare la pratica in 10 minuti."</div>
        </div>
        <div class="script" style="margin-bottom:1.5rem">
          <div class="script-lbl">🔄 Script B — Scelta della data di inizio</div>
          <div class="script-body" style="font-size:15px;line-height:1.8">"Ottimo. Ha fretta nella realizzazione dei lavori?<br><br>Noi solitamente necessitiamo di una quarantina di giorni prima di poter iniziare, a causa della grande mole di richieste."</div>
        </div>
        <div class="grid-2">
          <div class="card"><div class="card-tag">Tecnica — Alternativa Positiva</div><div class="card-p">Mai "vuole procedere?". Presenta sempre DUE opzioni che implicano entrambe il sì. Il cliente sceglie <em>come</em>, non <em>se</em>.</div></div>
          <div class="card warn"><div class="card-tag" style="color:var(--amber)">I 40 giorni di attesa</div><div class="card-p">Crea scarsità reale. Se siete effettivamente pieni di lavoro, detto con naturalezza spinge ad accelerare la decisione.</div></div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 11 — QUATTRO LIVELLI PREZZO
══════════════════════════════ -->
<div class="slide" id="s11">
  <div class="layout">
    <div class="sidebar" id="sb11"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 11</span>
        <span class="topbar-title">I Quattro Livelli di Prezzo</span>
        <div class="topbar-right"><span class="topbar-time">⏱ 10–15 min</span><span class="topbar-counter">11 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:78.5%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">11</span>Struttura prezzo</div>
          <h2 class="section-h">I Quattro Livelli di Prezzo</h2>
          <p class="section-sub">Scrivi su carta o modulistica. Non presentare a voce sola. L'ancora alta rende ogni sconto successivo una vittoria per il cliente.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🎯</div><div class="goal-text">Obiettivo: Ancorare la percezione in alto, poi guidare verso "Decido Oggi" come scelta logica e vantaggiosa.</div></div>
        <div class="script" style="margin-bottom:1.2rem">
          <div class="script-lbl">🔄 Script di apertura prezzi</div>
          <div class="script-body">"Per ricevere tutto questo pacchetto di valore, l'investimento totale è di € XXXX." [Pausa breve, poi procedi]</div>
        </div>

        <div class="price-level">
          <div class="price-badge" style="background:#dcfce7;color:#16a34a">🟢</div>
          <div><div class="price-name">Valore Commerciale — "Primo Prezzo"</div></div>
          <div class="price-chip" style="background:#dcfce7;color:#16a34a">€ YYYY</div>
          <div class="price-sub">Il valore pieno del pacchetto completo. Punto di ancoraggio alto — il cliente capisce quanto vale davvero il servizio.</div>
          <div class="price-note">Ideale come riferimento. Crea il frame di confronto per tutto ciò che segue.</div>
        </div>
        <div class="price-level">
          <div class="price-badge" style="background:#fef3c7;color:#b45309">🟡</div>
          <div><div class="price-name">Prezzo di Listino — "Standard"</div></div>
          <div class="price-chip" style="background:#fef3c7;color:#b45309">€ XXXX</div>
          <div class="price-sub">Tutto il pacchetto al prezzo intero con sconto di base. Listino praticato in quest'area d'Italia.</div>
          <div class="price-note">Opzione costosa — esiste solo per rendere le successive più attraenti.</div>
        </div>
        <div class="price-level">
          <div class="price-badge" style="background:var(--indigo-bg);color:var(--indigo)">🔵</div>
          <div><div class="price-name">Offerta Preventivo — Valida 30 giorni</div></div>
          <div class="price-chip" style="background:var(--indigo-bg);color:var(--indigo)">€ WWWW</div>
          <div class="price-sub">Include eventuali 2ª e 3ª visita. Solo il 30% dei clienti sceglie questa opzione.</div>
          <div class="price-note">Crea urgenza relativa — ma lascia ancora spazio di procrastinazione.</div>
        </div>
        <div class="price-level" style="border-color:#dc2626;background:#fff5f5">
          <div class="price-badge" style="background:#fee2e2;color:#dc2626">🔴</div>
          <div><div class="price-name">Decido Oggi — Solo in Consulenza ⭐</div></div>
          <div class="price-chip" style="background:#fee2e2;color:#dc2626">€ ZZZZ</div>
          <div class="price-sub">Progetto + materiali + gestione totale + finanziamento + eventuale omaggio. Il 70% dei clienti sceglie questa opzione.</div>
          <div class="price-note">Opzione target. Urgenza massima. Il differenziale economico giustifica la decisione immediata.</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 12 — GESTIONE OBIEZIONI
══════════════════════════════ -->
<div class="slide" id="s12">
  <div class="layout">
    <div class="sidebar" id="sb12"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 12</span>
        <span class="topbar-title">Gestione delle Obiezioni</span>
        <div class="topbar-right"><span class="topbar-counter">12 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:85.7%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">12</span>Risposta alle resistenze</div>
          <h2 class="section-h">Gestione delle Obiezioni</h2>
          <p class="section-sub">Un buon venditore anticipa le obiezioni — non le subisce. Se arrivano, spesso dipende da una fase precedente incompleta.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">🛡️</div><div class="goal-text">Regola d'Oro: Identifica prima il blocco reale (budget? fiducia? tempo?), poi rispondi. Mai difendere il prezzo senza aver capito l'obiezione vera.</div></div>
        <div class="obj-table">
          <div class="obj-header"><span>Obiezione</span><span>Risposta Pronta</span></div>
          <div class="obj-row"><div class="obj-q">"Devo pensarci"</div><div class="obj-a">"Capisco. È più una questione di budget o di fiducia su come lavoriamo?"<div class="obj-note">Identifica il blocco reale prima di rispondere.</div></div></div>
          <div class="obj-row"><div class="obj-q">"Devo parlare con…"</div><div class="obj-a">"Capisco, ed è giusto. Chiamiamolo adesso, così gli illustriamo il progetto insieme."<div class="obj-note">Nota: avete sbagliato in fase 1 a non identificare il decisore.</div></div></div>
          <div class="obj-row"><div class="obj-q">"È più caro degli altri"</div><div class="obj-a">"La differenza di prezzo sta nel valore: progetto completo, materiali altissima qualità, gestione totale, rapidità e detrazione inclusa. Come scegliere un ristorante stellato."<div class="obj-note">Usa l'analogia del ristorante o dell'auto premium.</div></div></div>
          <div class="obj-row"><div class="obj-q">"Ho paura dei lavori"</div><div class="obj-a">"È normale, la comprendo perfettamente. Per questo realizziamo il rendering — vede tutto prima. E gestiamo ogni aspetto noi: referente unico, tempi definiti, zero sorprese."</div></div>
          <div class="obj-row"><div class="obj-q">"Perché decidere oggi?"</div><div class="obj-a">"Perché programmando oggi ottimizziamo costi e logistica. Quel differenziale è il vantaggio che passo direttamente a lei per la decisione rapida."</div></div>
          <div class="obj-row" style="border-bottom:none"><div class="obj-q">"La detrazione è sicura?"</div><div class="obj-a">"Assolutamente sì, è legge (art. 16-bis DPR 917/86), prorogata per tutto il 2026. Forniamo noi tutta la documentazione per la dichiarazione dei redditi."</div></div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 13 — CHECKLIST
══════════════════════════════ -->
<div class="slide" id="s13">
  <div class="layout">
    <div class="sidebar" id="sb13"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 13</span>
        <span class="topbar-title">Checklist Operativa Visita</span>
        <div class="topbar-right"><span class="topbar-counter">13 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:92.8%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">13</span>Verifica finale</div>
          <h2 class="section-h">Checklist Operativa Visita</h2>
          <p class="section-sub">Prima di uscire, spunta ogni punto. Se un punto manca, la visita non è finita.</p>
        </div>
        <div class="goal-banner"><div class="goal-icon">✅</div><div class="goal-text">Obiettivo: Uscire dalla visita con TUTTI i punti completati — o con un prossimo passo chiaramente definito per ciascuno incompleto.</div></div>
        <div class="checklist" id="cl">
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">Lead analizzato e informazioni pre-visita raccolte</div></div>
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">Materiali pronti (campioni fisici, tablet, cataloghi)</div></div>
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">Script di apertura eseguito e decisore identificato</div></div>
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">Almeno 3 micro-sì raccolti durante l'intervista</div></div>
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">Sopralluogo tecnico eseguito e commentato al cliente</div></div>
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">Scelta materiali guidata e rendering annunciato</div></div>
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">5 punti del Valore Commerciale sintetizzati</div></div>
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">4 livelli di prezzo presentati su carta/modulistica</div></div>
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">2 opzioni di pagamento proposte</div></div>
          <div class="check-item" onclick="tc(this)"><div class="checkbox"></div><div class="check-label">Prossimo passo definito (ordine / pratica finanziaria / data inizio lavori)</div></div>
        </div>
        <div class="check-footer">
          <span id="cl-score">0 / 10 completati</span>
          <div class="check-progress-bar"><div class="check-progress-fill" id="cl-fill" style="width:0%"></div></div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════
     SLIDE 14 — REGOLE D'ORO
══════════════════════════════ -->
<div class="slide" id="s14">
  <div class="layout">
    <div class="sidebar" id="sb14"></div>
    <div class="main">
      <div class="topbar">
        <span class="topbar-phase">Fase 14</span>
        <span class="topbar-title">Le 5 Regole d'Oro</span>
        <div class="topbar-right"><span class="topbar-counter">14 / 14</span></div>
      </div>
      <div class="progress-wrap"><div class="progress-bar" style="width:100%"></div></div>
      <div class="content-body">
        <div class="section-header">
          <div class="section-tag"><span class="tag-num">14</span>Principi fondamentali</div>
          <h2 class="section-h">Le 5 Regole d'Oro</h2>
          <p class="section-sub">Interiorizzale prima di ogni visita. Il venditore eccellente esegue il metodo con disciplina — non improvvisa.</p>
        </div>
        <div class="rule-card"><div class="rule-n">I</div><div class="rule-text"><strong>Vendi tranquillità e risultato</strong>, non prodotti. Il cliente non compra un bagno — compra la fine dei problemi e l'inizio del comfort.</div></div>
        <div class="rule-card"><div class="rule-n">II</div><div class="rule-text"><strong>Mai lasciare senza un prossimo passo definito.</strong> Se esci senza un appuntamento, una pratica o un ordine, la visita è incompleta.</div></div>
        <div class="rule-card"><div class="rule-n">III</div><div class="rule-text"><strong>Il tuo atteggiamento non verbale è il 50% della chiusura.</strong> Postura, voce, sguardo, ritmo. Il cliente compra anche te, non solo il servizio.</div></div>
        <div class="rule-card"><div class="rule-n">IV</div><div class="rule-text"><strong>I micro-sì sono lo strumento di guida della conversazione.</strong> Accumuli impegno progressivo — il "sì grande" finale è la continuazione logica di tanti piccoli sì.</div></div>
        <div class="rule-card" style="border-color:var(--blue);background:var(--sky)"><div class="rule-n" style="background:var(--blue)">V</div><div class="rule-text" style="color:var(--navy2)"><strong>Se il cliente è decisore + ha urgenza + ha compreso il valore → CHIUDI IN PRIMA VISITA.</strong> Non rimandare. Il tempo è il peggior nemico della vendita.</div></div>
        <div class="divider"></div>
        <div style="text-align:center">
          <button class="btn-cover" onclick="goTo(0)" style="background:var(--navy)">← Torna all'inizio</button>
        </div>
      </div>
    </div>
  </div>
</div>

</div><!-- #app -->
<script>
const TOTAL=14;
let cur=0;
const slides=document.querySelectorAll('.slide');

const LABELS=[
  '','Apertura','Intervista','Bisogni','Consenso','Sopralluogo',
  'Materiali','Proposta','Valore','Finanza','Chiusura',
  'Prezzi','Obiezioni','Checklist','Regole d\'Oro'
];

function buildSidebar(id,currentSlide){
  const el=document.getElementById(id);
  if(!el)return;
  el.innerHTML='<div class="sidebar-logo">M</div>';
  for(let i=1;i<=TOTAL;i++){
    const d=document.createElement('div');
    d.className='step-dot'+(i<currentSlide?' visited':'')+(i===currentSlide?' current':'');
    d.textContent=i;
    d.title=LABELS[i];
    d.onclick=()=>goTo(i);
    el.appendChild(d);
  }
  const bot=document.createElement('div');
  bot.className='sidebar-bottom';
  const up=document.createElement('button');
  up.className='nav-arrow';up.textContent='↑';up.disabled=currentSlide<=1;
  up.onclick=()=>prev();
  const dn=document.createElement('button');
  dn.className='nav-arrow';dn.textContent='↓';dn.disabled=currentSlide>=TOTAL;
  dn.onclick=()=>next();
  bot.appendChild(up);bot.appendChild(dn);
  el.appendChild(bot);
}

function goTo(n){
  slides[cur].classList.remove('active');
  slides[cur].classList.add('out');
  setTimeout(()=>slides[cur].classList.remove('out'),480);
  cur=n;
  slides[cur].classList.add('active');
  for(let i=1;i<=TOTAL;i++) buildSidebar('sb'+i,cur);
}
function next(){if(cur<TOTAL)goTo(cur+1)}
function prev(){if(cur>0)goTo(cur-1)}

function tc(el){
  el.classList.toggle('done');
  const done=document.querySelectorAll('#cl .check-item.done').length;
  const total=document.querySelectorAll('#cl .check-item').length;
  document.getElementById('cl-score').textContent=done+' / '+total+' completati';
  document.getElementById('cl-fill').style.width=(done/total*100)+'%';
}

document.addEventListener('keydown',e=>{
  if(e.key==='ArrowRight'||e.key==='ArrowDown')next();
  if(e.key==='ArrowLeft'||e.key==='ArrowUp')prev();
});

for(let i=1;i<=TOTAL;i++) buildSidebar('sb'+i,1);
</script>
</body>
</html>
