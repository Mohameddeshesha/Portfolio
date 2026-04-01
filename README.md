<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Mohamed E. Deshesha — AI & Data Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=JetBrains+Mono:wght@300;400;500&family=Crimson+Pro:ital,wght@0,300;1,300&display=swap" rel="stylesheet">

<style>
:root {
  --bg:        #020408;
  --surface:   #080f1a;
  --panel:     #0c1624;
  --border:    #0f2540;
  --accent:    #00e5ff;
  --accent2:   #00ff99;
  --accent3:   #7c3aed;
  --text:      #c8dff0;
  --muted:     #4a6880;
  --white:     #eef6ff;
  --glow:      rgba(0,229,255,0.15);
  --glow2:     rgba(0,255,153,0.12);
}

*,*::before,*::after { box-sizing:border-box; margin:0; padding:0; }
html { scroll-behavior:smooth; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'JetBrains Mono', monospace;
  font-size: 14px;
  line-height: 1.7;
  overflow-x: hidden;
}

/* ── CANVAS BACKGROUND ── */
#neuralCanvas {
  position:fixed; top:0; left:0; width:100%; height:100%;
  z-index:0; opacity:.45; pointer-events:none;
}

/* ── GRAIN OVERLAY ── */
body::before {
  content:'';
  position:fixed; inset:0; z-index:1;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='.04'/%3E%3C/svg%3E");
  pointer-events:none; opacity:.6;
}

/* ── LAYOUT ── */
main { position:relative; z-index:2; max-width:960px; margin:0 auto; padding:0 32px 120px; }

/* ── HERO ── */
.hero {
  min-height:100vh; display:flex; flex-direction:column;
  justify-content:center; padding:80px 0 60px;
  position:relative;
}

.hero-label {
  font-size:11px; letter-spacing:.25em; text-transform:uppercase;
  color:var(--accent); margin-bottom:24px;
  display:flex; align-items:center; gap:12px;
  opacity:0; animation: fadeUp .6s .2s ease forwards;
}
.hero-label::before {
  content:''; display:block; width:32px; height:1px; background:var(--accent);
}

.hero-name {
  font-family:'Syne', sans-serif;
  font-size: clamp(52px, 9vw, 100px);
  font-weight:800; line-height:.95;
  color:var(--white);
  letter-spacing:-.03em;
  opacity:0; animation: fadeUp .8s .35s ease forwards;
}
.hero-name span { color:var(--accent); }

.hero-title {
  font-family:'Crimson Pro', serif;
  font-size:clamp(20px, 3vw, 28px);
  font-weight:300; font-style:italic;
  color:var(--muted); margin-top:16px;
  opacity:0; animation: fadeUp .7s .55s ease forwards;
}

.hero-bio {
  max-width:560px; margin-top:32px; font-size:13px;
  color:var(--text); line-height:1.9;
  opacity:0; animation: fadeUp .7s .7s ease forwards;
}

.hero-cta {
  margin-top:48px; display:flex; gap:16px; flex-wrap:wrap;
  opacity:0; animation: fadeUp .7s .85s ease forwards;
}

.btn {
  display:inline-flex; align-items:center; gap:8px;
  padding:12px 28px; font-family:'Syne',sans-serif;
  font-size:13px; font-weight:700; letter-spacing:.06em;
  text-transform:uppercase; text-decoration:none;
  border-radius:2px; cursor:pointer; transition:all .25s ease;
  position:relative; overflow:hidden;
}
.btn-primary {
  background:var(--accent); color:#000;
}
.btn-primary:hover { background:#fff; transform:translateY(-2px); box-shadow:0 0 40px rgba(0,229,255,.5); }
.btn-ghost {
  border:1px solid var(--border); color:var(--accent);
  background:transparent;
}
.btn-ghost:hover { border-color:var(--accent); background:var(--glow); }

/* ── METRICS ROW ── */
.metrics {
  display:grid; grid-template-columns: repeat(4, 1fr);
  gap:1px; background:var(--border);
  border:1px solid var(--border); margin:80px 0;
  opacity:0; animation: fadeUp .7s 1s ease forwards;
}
.metric {
  background:var(--surface); padding:32px 24px;
  position:relative; overflow:hidden;
  transition:background .3s;
}
.metric:hover { background:var(--panel); }
.metric::after {
  content:''; position:absolute; bottom:0; left:0;
  width:100%; height:2px; background:var(--accent);
  transform:scaleX(0); transform-origin:left;
  transition:transform .4s ease;
}
.metric:hover::after { transform:scaleX(1); }
.metric-num {
  font-family:'Syne',sans-serif; font-size:40px; font-weight:800;
  color:var(--white); line-height:1;
}
.metric-num span { color:var(--accent); font-size:28px; }
.metric-label { font-size:11px; letter-spacing:.15em; text-transform:uppercase; color:var(--muted); margin-top:8px; }

/* ── SECTION HEADER ── */
.section-header {
  display:flex; align-items:center; gap:20px;
  margin-bottom:48px;
}
.section-tag {
  font-size:11px; letter-spacing:.25em; text-transform:uppercase;
  color:var(--accent2); padding:4px 12px;
  border:1px solid rgba(0,255,153,.25);
}
.section-title {
  font-family:'Syne',sans-serif; font-size:clamp(28px,4vw,40px);
  font-weight:800; color:var(--white); letter-spacing:-.02em;
}

section { margin:120px 0; }

/* ── SKILLS GRID ── */
.skills-grid {
  display:grid; grid-template-columns:repeat(auto-fill,minmax(280px,1fr)); gap:2px;
  background:var(--border);
}
.skill-card {
  background:var(--surface); padding:28px;
  position:relative; overflow:hidden;
  transition:background .3s, transform .3s;
  cursor:default;
}
.skill-card:hover { background:var(--panel); transform:scale(1.01); z-index:1; }
.skill-card-icon { font-size:24px; margin-bottom:16px; }
.skill-card-name {
  font-family:'Syne',sans-serif; font-size:15px; font-weight:700;
  color:var(--white); margin-bottom:8px;
}
.skill-bar-track {
  height:2px; background:var(--border); margin-top:12px;
  position:relative; overflow:hidden;
}
.skill-bar-fill {
  height:100%; background:linear-gradient(90deg, var(--accent2), var(--accent));
  width:0; transition:width 1.5s cubic-bezier(.16,1,.3,1);
}
.skill-card small { font-size:11px; color:var(--muted); letter-spacing:.08em; }

/* ── EXPERIENCE ── */
.exp-list { display:flex; flex-direction:column; gap:2px; }
.exp-item {
  background:var(--surface); padding:36px 40px;
  display:grid; grid-template-columns:200px 1fr;
  gap:32px; position:relative; overflow:hidden;
  transition:background .3s;
  border-left:3px solid transparent;
}
.exp-item:hover { background:var(--panel); border-left-color:var(--accent); }
.exp-meta { }
.exp-period {
  font-size:11px; letter-spacing:.15em; color:var(--accent);
  text-transform:uppercase;
}
.exp-company {
  font-size:12px; color:var(--muted); margin-top:6px; line-height:1.5;
}
.exp-role {
  font-family:'Syne',sans-serif; font-size:18px; font-weight:700;
  color:var(--white); margin-bottom:12px;
}
.exp-desc { font-size:13px; color:var(--text); line-height:1.8; }
.exp-tags { display:flex; flex-wrap:wrap; gap:8px; margin-top:16px; }
.tag {
  font-size:10px; letter-spacing:.1em; text-transform:uppercase;
  padding:4px 10px; border:1px solid var(--border);
  color:var(--muted);
}

/* ── PROJECTS ── */
.projects-grid { display:grid; grid-template-columns:1fr 1fr; gap:2px; background:var(--border); }
.project-card {
  background:var(--surface); padding:40px;
  transition:background .3s; position:relative;
  overflow:hidden;
}
.project-card::before {
  content:''; position:absolute; top:0; left:0; right:0; height:3px;
  background:linear-gradient(90deg, var(--accent), var(--accent2));
  transform:scaleX(0); transform-origin:left;
  transition:transform .5s ease;
}
.project-card:hover::before { transform:scaleX(1); }
.project-card:hover { background:var(--panel); }
.project-num {
  font-size:64px; font-weight:800; color:var(--border);
  font-family:'Syne',sans-serif; line-height:1; margin-bottom:24px;
  transition:color .3s;
}
.project-card:hover .project-num { color:var(--glow); }
.project-title {
  font-family:'Syne',sans-serif; font-size:18px; font-weight:700;
  color:var(--white); margin-bottom:12px; line-height:1.3;
}
.project-desc { font-size:13px; color:var(--text); line-height:1.8; }
.project-tech { display:flex; flex-wrap:wrap; gap:6px; margin-top:20px; }
.tech-pill {
  font-size:10px; background:rgba(0,229,255,.08);
  border:1px solid rgba(0,229,255,.2); color:var(--accent);
  padding:3px 10px; letter-spacing:.08em;
}

/* ── CERTS ── */
.cert-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(260px,1fr)); gap:2px; background:var(--border); }
.cert-card {
  background:var(--surface); padding:28px;
  display:flex; gap:16px; align-items:flex-start;
  transition:background .3s;
}
.cert-card:hover { background:var(--panel); }
.cert-dot {
  width:8px; height:8px; min-width:8px; border-radius:50%;
  background:var(--accent2); margin-top:6px;
  box-shadow:0 0 8px var(--accent2);
}
.cert-name { font-size:13px; color:var(--white); line-height:1.5; font-weight:500; }
.cert-org { font-size:11px; color:var(--muted); margin-top:4px; letter-spacing:.06em; }

/* ── CONTACT ── */
.contact-row {
  display:grid; grid-template-columns:1fr 1fr; gap:2px;
  background:var(--border); margin-top:48px;
}
.contact-item {
  background:var(--surface); padding:40px;
  text-decoration:none; display:flex; flex-direction:column; gap:8px;
  transition:background .3s, transform .3s;
  position:relative; overflow:hidden;
}
.contact-item:hover { background:var(--panel); transform:translateY(-3px); }
.contact-icon { font-size:28px; }
.contact-label { font-size:11px; letter-spacing:.2em; text-transform:uppercase; color:var(--muted); }
.contact-value { font-family:'Syne',sans-serif; font-size:16px; font-weight:700; color:var(--white); }

/* ── FOOTER ── */
footer {
  text-align:center; padding:60px 0 40px;
  border-top:1px solid var(--border);
  font-size:11px; color:var(--muted); letter-spacing:.15em; text-transform:uppercase;
}

/* ── SCROLLBAR ── */
::-webkit-scrollbar { width:4px; }
::-webkit-scrollbar-track { background:var(--bg); }
::-webkit-scrollbar-thumb { background:var(--border); }

/* ── ANIMATIONS ── */
@keyframes fadeUp {
  from { opacity:0; transform:translateY(24px); }
  to   { opacity:1; transform:translateY(0); }
}
.reveal {
  opacity:0; transform:translateY(32px);
  transition:opacity .8s ease, transform .8s ease;
}
.reveal.visible { opacity:1; transform:translateY(0); }

/* ── CURSOR DOT ── */
.cursor-dot {
  width:6px; height:6px; background:var(--accent);
  border-radius:50%; position:fixed; pointer-events:none;
  z-index:9999; transition:transform .15s ease;
  box-shadow:0 0 12px var(--accent);
}
.cursor-ring {
  width:32px; height:32px; border:1px solid rgba(0,229,255,.4);
  border-radius:50%; position:fixed; pointer-events:none;
  z-index:9998; transition:left .12s ease, top .12s ease;
  transform:translate(-50%,-50%);
}

/* PROGRESS BAR */
.progress-bar {
  position:fixed; top:0; left:0; height:2px; z-index:999;
  background:linear-gradient(90deg,var(--accent2),var(--accent));
  width:0; transition:width .1s linear;
}

/* LANG TOGGLE */
.lang-toggle {
  position:fixed; top:24px; right:32px; z-index:100;
  display:flex; gap:2px;
}
.lang-btn {
  padding:8px 16px; font-family:'JetBrains Mono',monospace;
  font-size:11px; letter-spacing:.12em; text-transform:uppercase;
  cursor:pointer; border:1px solid var(--border);
  background:var(--surface); color:var(--muted);
  transition:all .2s; text-decoration:none;
}
.lang-btn.active, .lang-btn:hover { background:var(--accent); color:#000; border-color:var(--accent); }

/* MOBILE */
@media(max-width:680px){
  main { padding:0 20px 80px; }
  .metrics { grid-template-columns:1fr 1fr; }
  .exp-item { grid-template-columns:1fr; gap:8px; padding:24px; }
  .projects-grid { grid-template-columns:1fr; }
  .contact-row { grid-template-columns:1fr; }
  .lang-toggle { top:16px; right:16px; }
}
</style>
</head>
<body>

<div class="cursor-dot" id="dot"></div>
<div class="cursor-ring" id="ring"></div>
<div class="progress-bar" id="progress"></div>

<canvas id="neuralCanvas"></canvas>

<div class="lang-toggle">
  <a href="#en" class="lang-btn active" id="btn-en" onclick="setLang('en')">EN</a>
  <a href="#ar" class="lang-btn" id="btn-ar" onclick="setLang('ar')">عربي</a>
</div>

<!-- ════════════════════ ENGLISH ════════════════════ -->
<div id="lang-en">
<main>

  <!-- HERO -->
  <section class="hero" id="en">
    <div class="hero-label">AI & Data Analytics Portfolio</div>
    <h1 class="hero-name">Mohamed<br><span>Deshesha</span></h1>
    <div class="hero-title">AI Analyst · Tech-Law Expert · Strategic Leader</div>
    <p class="hero-bio">
      A results-driven professional at the intersection of Artificial Intelligence, Data Science, and Law. 
      Transforming raw data into strategic intelligence — leveraging machine learning, advanced analytics, 
      and a decade of leadership to drive decisions that matter.
    </p>
    <div class="hero-cta">
      <a href="https://www.linkedin.com/in/mohamedelsayeddeshesha" class="btn btn-primary" target="_blank">↗ Connect on LinkedIn</a>
      <a href="mailto:deshesha@gmail.com" class="btn btn-ghost">✉ deshesha@gmail.com</a>
    </div>
  </section>

  <!-- METRICS -->
  <div class="metrics reveal">
    <div class="metric">
      <div class="metric-num">5<span>+</span></div>
      <div class="metric-label">Years Leadership</div>
    </div>
    <div class="metric">
      <div class="metric-num">8<span>+</span></div>
      <div class="metric-label">Certifications</div>
    </div>
    <div class="metric">
      <div class="metric-num">3<span></span></div>
      <div class="metric-label">AI Projects</div>
    </div>
    <div class="metric">
      <div class="metric-num">2<span></span></div>
      <div class="metric-label">Languages</div>
    </div>
  </div>

  <!-- SKILLS -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-tag">Capabilities</span>
      <h2 class="section-title">Tech Stack</h2>
    </div>
    <div class="skills-grid">
      <div class="skill-card">
        <div class="skill-card-icon">🐍</div>
        <div class="skill-card-name">Python · Pandas</div>
        <small>EDA, Data Wrangling, ML Pipelines</small>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-w="75"></div></div>
      </div>
      <div class="skill-card">
        <div class="skill-card-icon">🤖</div>
        <div class="skill-card-name">Machine Learning</div>
        <small>Regression, Classification, Clustering</small>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-w="70"></div></div>
      </div>
      <div class="skill-card">
        <div class="skill-card-icon">📊</div>
        <div class="skill-card-name">Power BI · DAX</div>
        <small>Interactive Dashboards, KPI Tracking</small>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-w="80"></div></div>
      </div>
      <div class="skill-card">
        <div class="skill-card-icon">🗄️</div>
        <div class="skill-card-name">SQL</div>
        <small>Queries, Joins, Aggregations</small>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-w="72"></div></div>
      </div>
      <div class="skill-card">
        <div class="skill-card-icon">🌐</div>
        <div class="skill-card-name">HTML · CSS · JS</div>
        <small>Responsive Web Applications</small>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-w="78"></div></div>
      </div>
      <div class="skill-card">
        <div class="skill-card-icon">⚖️</div>
        <div class="skill-card-name">Tech-Law & Cybersecurity</div>
        <small>Blockchain, IP, Cybercrime Regulations</small>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-w="90"></div></div>
      </div>
    </div>
  </section>

  <!-- EXPERIENCE -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-tag">Timeline</span>
      <h2 class="section-title">Experience</h2>
    </div>
    <div class="exp-list">
      <div class="exp-item">
        <div class="exp-meta">
          <div class="exp-period">Dec 2025 → Sep 2026</div>
          <div class="exp-company">Egyptian Military Academy<br>Digilians Initiative</div>
        </div>
        <div>
          <div class="exp-role">Data Analytics & AI Trainee</div>
          <div class="exp-desc">Designing interactive Power BI dashboards to translate raw data into actionable business intelligence. Applying ML algorithms for Exploratory Data Analysis and predictive modeling in high-stakes environments.</div>
          <div class="exp-tags">
            <span class="tag">Power BI</span><span class="tag">Machine Learning</span><span class="tag">EDA</span><span class="tag">Python</span>
          </div>
        </div>
      </div>
      <div class="exp-item">
        <div class="exp-meta">
          <div class="exp-period">2021 → Present</div>
          <div class="exp-company">Deshisha Law Firm</div>
        </div>
        <div>
          <div class="exp-role">Founder & Lead Attorney</div>
          <div class="exp-desc">Analyzing extensive structured and unstructured legal documentation to formulate winning case strategies. Applying analytical frameworks to complex, multi-variable legal situations.</div>
          <div class="exp-tags">
            <span class="tag">Legal Analytics</span><span class="tag">Strategic Thinking</span><span class="tag">Leadership</span>
          </div>
        </div>
      </div>
      <div class="exp-item">
        <div class="exp-meta">
          <div class="exp-period">2018 → 2021</div>
          <div class="exp-company">Telecom Egypt (WE)</div>
        </div>
        <div>
          <div class="exp-role">Team Leader & Sales Representative</div>
          <div class="exp-desc">Analyzed customer acquisition data, sales metrics, and market trends to optimize targeted sales strategies. Evaluated team performance datasets leading to enhanced operational efficiency and revenue growth.</div>
          <div class="exp-tags">
            <span class="tag">Data Analysis</span><span class="tag">Team Leadership</span><span class="tag">KPI Optimization</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-tag">Work</span>
      <h2 class="section-title">Projects</h2>
    </div>
    <div class="projects-grid">
      <div class="project-card">
        <div class="project-num">01</div>
        <div class="project-title">Sales Performance & Market Trends Dashboard</div>
        <div class="project-desc">Interactive dashboard tracking KPIs, purchasing patterns, and regional performance after full data cleaning and transformation pipeline.</div>
        <div class="project-tech">
          <span class="tech-pill">Power BI</span>
          <span class="tech-pill">DAX</span>
          <span class="tech-pill">Excel</span>
        </div>
      </div>
      <div class="project-card">
        <div class="project-num">02</div>
        <div class="project-title">Customer Behavior & Churn Analysis</div>
        <div class="project-desc">Full EDA pipeline using Python to identify churn factors from behavioral data, with actionable retention strategy recommendations.</div>
        <div class="project-tech">
          <span class="tech-pill">Python</span>
          <span class="tech-pill">Pandas</span>
          <span class="tech-pill">Data Mining</span>
        </div>
      </div>
      <div class="project-card">
        <div class="project-num">03</div>
        <div class="project-title">Data-Driven Web Application</div>
        <div class="project-desc">Responsive web interface displaying dynamic data and user metrics with clean architecture and real-time updates.</div>
        <div class="project-tech">
          <span class="tech-pill">HTML</span>
          <span class="tech-pill">CSS</span>
          <span class="tech-pill">JavaScript</span>
        </div>
      </div>
      <div class="project-card" style="background:var(--panel); display:flex; align-items:center; justify-content:center; min-height:220px;">
        <div style="text-align:center; color:var(--muted);">
          <div style="font-size:40px; margin-bottom:16px; opacity:.3;">+</div>
          <div style="font-size:11px; letter-spacing:.2em; text-transform:uppercase;">More Coming Soon</div>
        </div>
      </div>
    </div>
  </section>

  <!-- CERTIFICATIONS -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-tag">Credentials</span>
      <h2 class="section-title">Education & Certifications</h2>
    </div>
    <div class="cert-grid">
      <div class="cert-card">
        <div class="cert-dot" style="background:var(--accent);box-shadow:0 0 8px var(--accent)"></div>
        <div>
          <div class="cert-name">AI & Data Analysis Diploma</div>
          <div class="cert-org">Egyptian Military Academy · 2026</div>
        </div>
      </div>
      <div class="cert-card">
        <div class="cert-dot" style="background:var(--accent);box-shadow:0 0 8px var(--accent)"></div>
        <div>
          <div class="cert-name">Web Programming & AI Diploma</div>
          <div class="cert-org">Kafr El-Sheikh University · 2025</div>
        </div>
      </div>
      <div class="cert-card">
        <div class="cert-dot"></div>
        <div>
          <div class="cert-name">Supervised Machine Learning</div>
          <div class="cert-org">Stanford / DeepLearning.AI · Coursera</div>
        </div>
      </div>
      <div class="cert-card">
        <div class="cert-dot"></div>
        <div>
          <div class="cert-name">Become a Data Analyst</div>
          <div class="cert-org">LinkedIn Learning · Learning Path</div>
        </div>
      </div>
      <div class="cert-card">
        <div class="cert-dot"></div>
        <div>
          <div class="cert-name">Digital Transformation (FDTC)</div>
          <div class="cert-org">Supreme Council of Universities</div>
        </div>
      </div>
      <div class="cert-card">
        <div class="cert-dot"></div>
        <div>
          <div class="cert-name">Master's in Public Law</div>
          <div class="cert-org">University of Sadat City · 2022</div>
        </div>
      </div>
      <div class="cert-card">
        <div class="cert-dot" style="background:var(--accent3);box-shadow:0 0 8px var(--accent3)"></div>
        <div>
          <div class="cert-name">Strategy & National Security</div>
          <div class="cert-org">Military Academy Postgraduate Studies</div>
        </div>
      </div>
      <div class="cert-card">
        <div class="cert-dot" style="background:var(--accent3);box-shadow:0 0 8px var(--accent3)"></div>
        <div>
          <div class="cert-name">Cybercrime & Blockchain Regulations</div>
          <div class="cert-org">ITI — Information Technology Institute</div>
        </div>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-tag">Contact</span>
      <h2 class="section-title">Get In Touch</h2>
    </div>
    <div class="contact-row">
      <a href="https://www.linkedin.com/in/mohamedelsayeddeshesha" class="contact-item" target="_blank">
        <div class="contact-icon">in</div>
        <div class="contact-label">LinkedIn</div>
        <div class="contact-value">mohamedelsayeddeshesha</div>
      </a>
      <a href="mailto:deshesha@gmail.com" class="contact-item">
        <div class="contact-icon">✉</div>
        <div class="contact-label">Email</div>
        <div class="contact-value">deshesha@gmail.com</div>
      </a>
    </div>
  </section>

  <footer>
    <div>© 2025 Mohamed E. Deshesha — AI & Data Analytics Portfolio</div>
    <div style="margin-top:8px;font-size:10px;opacity:.4;">Cairo, Egypt · Open to opportunities</div>
  </footer>

</main>
</div>

<!-- ════════════════════ ARABIC ════════════════════ -->
<div id="lang-ar" dir="rtl" style="display:none">
<main style="font-family:'Syne',sans-serif; direction:rtl; text-align:right;">

  <section class="hero" id="ar">
    <div class="hero-label" style="font-family:'JetBrains Mono',monospace;">محفظة الذكاء الاصطناعي وتحليل البيانات</div>
    <h1 class="hero-name" style="font-family:'Syne',sans-serif;">محمد<br><span>دشيشه</span></h1>
    <div class="hero-title" style="font-family:'Crimson Pro',serif;">محلل ذكاء اصطناعي · خبير قانون تقني · قائد استراتيجي</div>
    <p class="hero-bio" style="font-family:'JetBrains Mono',monospace; font-size:13px;">
      محترف يقف عند تقاطع الذكاء الاصطناعي وعلم البيانات والقانون.
      يحوّل البيانات الخام إلى استخبارات استراتيجية — مستفيداً من التعلم الآلي والتحليلات المتقدمة
      وعقد من الخبرة القيادية لاتخاذ قرارات ذات أثر حقيقي.
    </p>
    <div class="hero-cta">
      <a href="https://www.linkedin.com/in/mohamedelsayeddeshesha" class="btn btn-primary" target="_blank">↗ تواصل عبر لينكد إن</a>
      <a href="mailto:deshesha@gmail.com" class="btn btn-ghost">✉ deshesha@gmail.com</a>
    </div>
  </section>

  <div class="metrics reveal">
    <div class="metric"><div class="metric-num">5<span>+</span></div><div class="metric-label">سنوات قيادة</div></div>
    <div class="metric"><div class="metric-num">8<span>+</span></div><div class="metric-label">شهادات</div></div>
    <div class="metric"><div class="metric-num">3</div><div class="metric-label">مشاريع ذكاء اصطناعي</div></div>
    <div class="metric"><div class="metric-num">2</div><div class="metric-label">لغات</div></div>
  </div>

  <section class="reveal">
    <div class="section-header" style="flex-direction:row-reverse;">
      <span class="section-tag">القدرات</span>
      <h2 class="section-title">المهارات التقنية</h2>
    </div>
    <div class="skills-grid">
      <div class="skill-card"><div class="skill-card-icon">🐍</div><div class="skill-card-name">Python · Pandas</div><small>التحليل الاستكشافي وهندسة البيانات</small><div class="skill-bar-track"><div class="skill-bar-fill" data-w="75"></div></div></div>
      <div class="skill-card"><div class="skill-card-icon">🤖</div><div class="skill-card-name">تعلم الآلة</div><small>الانحدار، التصنيف، التجميع</small><div class="skill-bar-track"><div class="skill-bar-fill" data-w="70"></div></div></div>
      <div class="skill-card"><div class="skill-card-icon">📊</div><div class="skill-card-name">Power BI · DAX</div><small>لوحات القيادة التفاعلية</small><div class="skill-bar-track"><div class="skill-bar-fill" data-w="80"></div></div></div>
      <div class="skill-card"><div class="skill-card-icon">🗄️</div><div class="skill-card-name">SQL</div><small>الاستعلامات والتجميعات</small><div class="skill-bar-track"><div class="skill-bar-fill" data-w="72"></div></div></div>
      <div class="skill-card"><div class="skill-card-icon">🌐</div><div class="skill-card-name">HTML · CSS · JS</div><small>تطبيقات الويب</small><div class="skill-bar-track"><div class="skill-bar-fill" data-w="78"></div></div></div>
      <div class="skill-card"><div class="skill-card-icon">⚖️</div><div class="skill-card-name">القانون التقني والأمن السيبراني</div><small>البلوكتشين، الملكية الفكرية</small><div class="skill-bar-track"><div class="skill-bar-fill" data-w="90"></div></div></div>
    </div>
  </section>

  <section class="reveal">
    <div class="section-header" style="flex-direction:row-reverse;">
      <span class="section-tag">الخبرات</span>
      <h2 class="section-title">المسيرة المهنية</h2>
    </div>
    <div class="exp-list">
      <div class="exp-item" style="grid-template-columns:1fr 200px;">
        <div><div class="exp-role">متدرب في تحليل البيانات والذكاء الاصطناعي</div><div class="exp-desc">تصميم لوحات قيادة تفاعلية باستخدام Power BI لتحويل البيانات الخام إلى رؤى استراتيجية. تطبيق خوارزميات تعلم الآلة للتحليل الاستكشافي والنمذجة التنبؤية.</div><div class="exp-tags"><span class="tag">Power BI</span><span class="tag">ML</span><span class="tag">Python</span></div></div>
        <div class="exp-meta" style="text-align:right;"><div class="exp-period">ديسمبر 2025 ← سبتمبر 2026</div><div class="exp-company">الأكاديمية العسكرية المصرية<br>مبادرة Digilians</div></div>
      </div>
      <div class="exp-item" style="grid-template-columns:1fr 200px;">
        <div><div class="exp-role">مؤسس ومدير مكتب محاماة</div><div class="exp-desc">تحليل الوثائق القانونية المعقدة لصياغة استراتيجيات قضايا ناجحة.</div><div class="exp-tags"><span class="tag">التحليل القانوني</span><span class="tag">القيادة</span></div></div>
        <div class="exp-meta" style="text-align:right;"><div class="exp-period">2021 ← الآن</div><div class="exp-company">مكتب دشيشه للمحاماة</div></div>
      </div>
      <div class="exp-item" style="grid-template-columns:1fr 200px;">
        <div><div class="exp-role">قائد فريق وممثل مبيعات</div><div class="exp-desc">تحليل بيانات اكتساب العملاء ومقاييس المبيعات لتحسين الاستراتيجيات المستهدفة.</div><div class="exp-tags"><span class="tag">تحليل البيانات</span><span class="tag">KPI</span></div></div>
        <div class="exp-meta" style="text-align:right;"><div class="exp-period">2018 ← 2021</div><div class="exp-company">المصرية للاتصالات (WE)</div></div>
      </div>
    </div>
  </section>

  <section class="reveal">
    <div class="section-header" style="flex-direction:row-reverse;">
      <span class="section-tag">المشاريع</span>
      <h2 class="section-title">الأعمال التقنية</h2>
    </div>
    <div class="projects-grid">
      <div class="project-card"><div class="project-num">01</div><div class="project-title">لوحة أداء المبيعات واتجاهات السوق</div><div class="project-desc">لوحة قيادة تفاعلية لتتبع مؤشرات الأداء الرئيسية وتصور الأداء الإقليمي.</div><div class="project-tech"><span class="tech-pill">Power BI</span><span class="tech-pill">DAX</span><span class="tech-pill">Excel</span></div></div>
      <div class="project-card"><div class="project-num">02</div><div class="project-title">تحليل سلوك العملاء ومعدل الاستغناء</div><div class="project-desc">تحليل EDA كامل باستخدام Python لتحديد عوامل تسرب العملاء.</div><div class="project-tech"><span class="tech-pill">Python</span><span class="tech-pill">Pandas</span><span class="tech-pill">Data Mining</span></div></div>
      <div class="project-card"><div class="project-num">03</div><div class="project-title">تطبيق ويب مبني على البيانات</div><div class="project-desc">واجهة ويب متجاوبة لعرض البيانات الديناميكية ومقاييس المستخدمين.</div><div class="project-tech"><span class="tech-pill">HTML</span><span class="tech-pill">CSS</span><span class="tech-pill">JavaScript</span></div></div>
      <div class="project-card" style="background:var(--panel);display:flex;align-items:center;justify-content:center;min-height:220px;"><div style="text-align:center;color:var(--muted);"><div style="font-size:40px;margin-bottom:16px;opacity:.3;">+</div><div style="font-size:11px;letter-spacing:.2em;text-transform:uppercase;">المزيد قريباً</div></div></div>
    </div>
  </section>

  <section class="reveal">
    <div class="section-header" style="flex-direction:row-reverse;">
      <span class="section-tag">الشهادات</span>
      <h2 class="section-title">التعليم والشهادات</h2>
    </div>
    <div class="cert-grid">
      <div class="cert-card"><div class="cert-dot" style="background:var(--accent);box-shadow:0 0 8px var(--accent)"></div><div><div class="cert-name">دبلومة الذكاء الاصطناعي وتحليل البيانات</div><div class="cert-org">الأكاديمية العسكرية المصرية · 2026</div></div></div>
      <div class="cert-card"><div class="cert-dot" style="background:var(--accent);box-shadow:0 0 8px var(--accent)"></div><div><div class="cert-name">دبلومة برمجة الويب والذكاء الاصطناعي</div><div class="cert-org">جامعة كفر الشيخ · 2025</div></div></div>
      <div class="cert-card"><div class="cert-dot"></div><div><div class="cert-name">التعلم الآلي الخاضع للإشراف</div><div class="cert-org">جامعة ستانفورد · Coursera</div></div></div>
      <div class="cert-card"><div class="cert-dot"></div><div><div class="cert-name">مسار محلل البيانات</div><div class="cert-org">LinkedIn Learning</div></div></div>
      <div class="cert-card"><div class="cert-dot"></div><div><div class="cert-name">ماجستير في القانون العام</div><div class="cert-org">جامعة مدينة السادات · 2022</div></div></div>
      <div class="cert-card"><div class="cert-dot" style="background:var(--accent3);box-shadow:0 0 8px var(--accent3)"></div><div><div class="cert-name">الاستراتيجية والأمن القومي</div><div class="cert-org">الأكاديمية العسكرية للدراسات العليا</div></div></div>
      <div class="cert-card"><div class="cert-dot" style="background:var(--accent3);box-shadow:0 0 8px var(--accent3)"></div><div><div class="cert-name">الجرائم السيبرانية والبلوكتشين</div><div class="cert-org">معهد تكنولوجيا المعلومات (ITI)</div></div></div>
      <div class="cert-card"><div class="cert-dot"></div><div><div class="cert-name">ليسانس الحقوق</div><div class="cert-org">جامعة طنطا · 2018</div></div></div>
    </div>
  </section>

  <section class="reveal">
    <div class="section-header" style="flex-direction:row-reverse;">
      <span class="section-tag">تواصل</span>
      <h2 class="section-title">للتواصل</h2>
    </div>
    <div class="contact-row">
      <a href="https://www.linkedin.com/in/mohamedelsayeddeshesha" class="contact-item" target="_blank"><div class="contact-icon">in</div><div class="contact-label">لينكد إن</div><div class="contact-value">mohamedelsayeddeshesha</div></a>
      <a href="mailto:deshesha@gmail.com" class="contact-item"><div class="contact-icon">✉</div><div class="contact-label">البريد الإلكتروني</div><div class="contact-value">deshesha@gmail.com</div></a>
    </div>
  </section>

  <footer>
    <div>© 2025 محمد السيد دشيشه — محفظة الذكاء الاصطناعي وتحليل البيانات</div>
    <div style="margin-top:8px;font-size:10px;opacity:.4;">القاهرة، مصر · متاح للفرص</div>
  </footer>
</main>
</div>

<!-- ════════════════════ SCRIPTS ════════════════════ -->
<script>
// ── LANG TOGGLE ──
function setLang(l) {
  document.getElementById('lang-en').style.display = l==='en' ? '' : 'none';
  document.getElementById('lang-ar').style.display  = l==='ar' ? '' : 'none';
  document.getElementById('btn-en').classList.toggle('active', l==='en');
  document.getElementById('btn-ar').classList.toggle('active', l==='ar');
  document.documentElement.dir = l==='ar' ? 'rtl' : 'ltr';
}

// ── NEURAL NETWORK CANVAS ──
const canvas = document.getElementById('neuralCanvas');
const ctx = canvas.getContext('2d');
let W, H, nodes=[], mouse={x:-9999,y:-9999};

function resize(){ W=canvas.width=window.innerWidth; H=canvas.height=window.innerHeight; }
resize(); window.addEventListener('resize',resize);

class Node {
  constructor(){
    this.x = Math.random()*W;
    this.y = Math.random()*H;
    this.vx = (Math.random()-.5)*.35;
    this.vy = (Math.random()-.5)*.35;
    this.r  = Math.random()*2+1;
    this.pulse = Math.random()*Math.PI*2;
  }
  update(){
    this.x+=this.vx; this.y+=this.vy; this.pulse+=.02;
    if(this.x<0||this.x>W) this.vx*=-1;
    if(this.y<0||this.y>H) this.vy*=-1;
  }
}

for(let i=0;i<90;i++) nodes.push(new Node());

function draw(){
  ctx.clearRect(0,0,W,H);
  // Connections
  for(let i=0;i<nodes.length;i++){
    for(let j=i+1;j<nodes.length;j++){
      const d=Math.hypot(nodes[i].x-nodes[j].x, nodes[i].y-nodes[j].y);
      if(d<150){
        const alpha=(1-d/150)*.4;
        ctx.beginPath();
        ctx.strokeStyle=`rgba(0,229,255,${alpha})`;
        ctx.lineWidth=.5;
        ctx.moveTo(nodes[i].x,nodes[i].y);
        ctx.lineTo(nodes[j].x,nodes[j].y);
        ctx.stroke();
      }
    }
    // Mouse interactions
    const dm=Math.hypot(nodes[i].x-mouse.x, nodes[i].y-mouse.y);
    if(dm<180){
      ctx.beginPath();
      ctx.strokeStyle=`rgba(0,255,153,${(1-dm/180)*.6})`;
      ctx.lineWidth=.8;
      ctx.moveTo(nodes[i].x,nodes[i].y);
      ctx.lineTo(mouse.x,mouse.y);
      ctx.stroke();
    }
  }
  // Nodes
  nodes.forEach(n=>{
    const pulse = .5+Math.sin(n.pulse)*.3;
    ctx.beginPath();
    ctx.arc(n.x,n.y,n.r*pulse,0,Math.PI*2);
    ctx.fillStyle='rgba(0,229,255,.7)';
    ctx.fill();
    n.update();
  });
  requestAnimationFrame(draw);
}
draw();

document.addEventListener('mousemove',e=>{mouse.x=e.clientX;mouse.y=e.clientY;});

// ── CURSOR ──
const dot=document.getElementById('dot'), ring=document.getElementById('ring');
document.addEventListener('mousemove',e=>{
  dot.style.left=e.clientX-3+'px'; dot.style.top=e.clientY-3+'px';
  ring.style.left=e.clientX+'px'; ring.style.top=e.clientY+'px';
});
document.querySelectorAll('a,.btn,.metric,.skill-card').forEach(el=>{
  el.addEventListener('mouseenter',()=>{ dot.style.transform='scale(3)'; ring.style.transform='translate(-50%,-50%) scale(1.5)'; });
  el.addEventListener('mouseleave',()=>{ dot.style.transform='scale(1)'; ring.style.transform='translate(-50%,-50%) scale(1)'; });
});

// ── PROGRESS BAR ──
const progress=document.getElementById('progress');
window.addEventListener('scroll',()=>{
  const p=window.scrollY/(document.body.scrollHeight-window.innerHeight);
  progress.style.width=(p*100)+'%';
});

// ── REVEAL ON SCROLL ──
const observer=new IntersectionObserver(entries=>{
  entries.forEach(e=>{ if(e.isIntersecting) e.target.classList.add('visible'); });
},{threshold:.15});
document.querySelectorAll('.reveal').forEach(el=>observer.observe(el));

// ── SKILL BARS ──
const barObserver=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.querySelectorAll('.skill-bar-fill').forEach(bar=>{
        bar.style.width=bar.dataset.w+'%';
      });
    }
  });
},{threshold:.3});
document.querySelectorAll('.skills-grid').forEach(g=>barObserver.observe(g));

// ── COUNTER ANIMATION ──
function animateCount(el, target, suffix=''){
  let start=0; const dur=1800; const startTime=performance.now();
  function update(now){
    const t=Math.min((now-startTime)/dur,1);
    const ease=1-Math.pow(1-t,3);
    el.innerHTML=Math.floor(ease*target)+'<span>'+suffix+'</span>';
    if(t<1) requestAnimationFrame(update);
  }
  requestAnimationFrame(update);
}
const counterObs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.querySelectorAll('.metric-num').forEach(el=>{
        const txt=el.textContent;
        const num=parseInt(txt);
        const suffix=txt.includes('+') ? '+' : '';
        animateCount(el,num,suffix);
      });
    }
  });
},{threshold:.5,once:true});
document.querySelectorAll('.metrics').forEach(m=>counterObs.observe(m));
</script>
</body>
</html>
