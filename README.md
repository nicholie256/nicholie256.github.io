<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>nicholasfranklin.com</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&display=swap');

  :root {
    --bg: #15110c;
    --fg: #f5e6d3;
    --dim: #9c8769;
    --accent: #ff9f43;
    --accent-2: #7fd1d9;
    --cursor: #ff9f43;
  }

  * { box-sizing: border-box; }

  html, body {
    margin: 0;
    height: 100%;
    background: var(--bg);
    color: var(--fg);
    font-family: 'JetBrains Mono', 'Courier New', monospace;
  }

  body {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 24px;
    background-image:
      radial-gradient(ellipse at top left, rgba(255,159,67,0.06), transparent 60%),
      radial-gradient(ellipse at bottom right, rgba(127,209,217,0.05), transparent 60%);
  }

  .terminal {
    width: 100%;
    max-width: 720px;
    background: #1b1612;
    border: 1px solid #2e2620;
    border-radius: 8px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.6), 0 0 0 1px rgba(255,159,67,0.04);
    overflow: hidden;
  }

  .titlebar {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 10px 14px;
    background: #201a15;
    border-bottom: 1px solid #2e2620;
  }
  .dot { width: 11px; height: 11px; border-radius: 50%; }
  .dot.red { background: #ff5f56; }
  .dot.yellow { background: #ffbd2e; }
  .dot.green { background: #27c93f; }
  .titlebar-label {
    margin-left: auto;
    color: var(--dim);
    font-size: 0.78rem;
    letter-spacing: 0.5px;
  }

  .body {
    padding: 26px 28px 32px;
    font-size: 0.98rem;
  }

  .line { margin: 0 0 10px; white-space: pre-wrap; word-break: break-word; }
  .prompt { color: var(--dim); }
  .prompt .user { color: var(--accent); }
  .prompt .path { color: var(--accent-2); }
  .out { color: var(--fg); }
  .dimtext { color: var(--dim); }
  .accent { color: var(--accent); font-weight: 700; }

  .ascii {
    color: var(--accent);
    font-size: 1.1rem;
    font-weight: 700;
    line-height: 1.2;
    letter-spacing: 2px;
    margin: 4px 0 4px;
    white-space: pre;
    overflow-x: auto;
  }
  .ascii-sub {
    color: var(--dim);
    font-size: 0.8rem;
    letter-spacing: 4px;
    margin: 0 0 18px;
  }

  a { color: var(--accent-2); text-decoration: none; border-bottom: 1px dotted rgba(127,209,217,0.4); }
  a:hover { color: var(--accent); border-bottom-color: var(--accent); }

  .tags { display: flex; flex-wrap: wrap; gap: 8px; margin: 6px 0 4px; }
  .tag {
    border: 1px solid #3a3128;
    color: var(--fg);
    padding: 2px 8px;
    border-radius: 4px;
    font-size: 0.78rem;
  }

  .cursor {
    display: inline-block;
    width: 9px;
    height: 1.05em;
    background: var(--cursor);
    margin-left: 4px;
    vertical-align: -2px;
    animation: blink 1s steps(1) infinite;
  }
  @keyframes blink { 50% { opacity: 0; } }

  @media (max-width: 480px) {
    .body { padding: 18px 16px 26px; font-size: 0.88rem; }
    .ascii { font-size: 0.85rem; letter-spacing: 1px; }
  }
</style>
</head>
<body>
  <div class="terminal">
    <div class="titlebar">
      <span class="dot red"></span>
      <span class="dot yellow"></span>
      <span class="dot green"></span>
      <span class="titlebar-label">guest@nicholasfranklin.com — zsh</span>
    </div>
    <div class="body">

<div class="ascii">##    ##  ########
###   ##  ##
####  ##  ######
## ## ##  ##
##  ####  ##
##   ###  ##
##    ##  ##</div>

<div class="line"><span class="prompt"><span class="user">guest@nfranklin</span>:<span class="path">~</span>$ </span>whoami</div>
<div class="line out">Nicholas C. Franklin</div>
<div class="line out">Director of Cybersecurity for Operational Technology (OT) &amp; Tactical Systems @ <a href="https://www.leidos.com/" target="_blank" rel="noopener">Leidos</a></div>

<div class="line"><span class="prompt"><span class="user">guest@nfranklin</span>:<span class="path">~</span>$ </span>cat status.txt</div>
<div class="line out">&gt; Focus: OT / ICS / Tactical Systems cybersecurity<br>&gt; Clearance: ACTIVE - TOP SECRET<br>&gt; Availability: not accepting consideration for other positions at this time</div>

<div class="line"><span class="prompt"><span class="user">guest@nfranklin</span>:<span class="path">~</span>$ </span>ls ./focus</div>
<div class="line">
  <div class="tags">
    <span class="tag">OT / ICS Security</span>
    <span class="tag">Critical Infrastructure</span>
    <span class="tag">CEMA &amp; Pen Testing</span>
    <span class="tag">Team Leadership</span>
    <span class="tag">R&amp;D / Strategy</span>
  </div>
</div>

<div class="line"><span class="prompt"><span class="user">guest@nfranklin</span>:<span class="path">~</span>$ </span>cat contact.txt</div>
<div class="line out">email&nbsp;&nbsp;&nbsp;:: <a href="mailto:nicholascfranklin@gmail.com">nicholascfranklin@gmail.com</a><br>linkedin:: <a href="https://www.linkedin.com/in/nicholas-franklin-bab45375/" target="_blank" rel="noopener">linkedin.com/in/nicholas-franklin</a></div>

<div class="line"><span class="prompt"><span class="user">guest@nfranklin</span>:<span class="path">~</span>$ </span><span class="cursor"></span></div>

    </div>
  </div>
</body>
</html>
