<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>nicholasfranklin.com</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&display=swap');

  :root {
    --bg: #0a0e0c;
    --fg: #c9f7d4;
    --dim: #5b8a6b;
    --accent: #5fffb0;
    --cursor: #5fffb0;
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
      radial-gradient(ellipse at top left, rgba(95,255,176,0.05), transparent 60%),
      radial-gradient(ellipse at bottom right, rgba(95,255,176,0.04), transparent 60%);
  }

  .terminal {
    width: 100%;
    max-width: 720px;
    background: #0d1310;
    border: 1px solid #1f2e25;
    border-radius: 8px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.6), 0 0 0 1px rgba(95,255,176,0.04);
    overflow: hidden;
  }

  .titlebar {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 10px 14px;
    background: #111813;
    border-bottom: 1px solid #1f2e25;
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
    min-height: 360px;
  }

  .line { margin: 0 0 10px; white-space: pre-wrap; word-break: break-word; }
  .prompt { color: var(--dim); }
  .prompt .user { color: var(--accent); }
  .prompt .path { color: #7aa9ff; }
  .out { color: var(--fg); }
  .dimtext { color: var(--dim); }
  .accent { color: var(--accent); font-weight: 700; }

  .ascii {
    color: var(--accent);
    font-size: 1.1rem;
    font-weight: 700;
    line-height: 1.2;
    letter-spacing: 2px;
    margin: 4px 0 18px;
    white-space: pre;
    overflow-x: auto;
  }
  .ascii-sub {
    color: var(--dim);
    font-size: 0.8rem;
    letter-spacing: 4px;
    margin: -10px 0 18px;
  }

  a { color: #7aa9ff; text-decoration: none; border-bottom: 1px dotted rgba(122,169,255,0.4); }
  a:hover { color: var(--accent); border-bottom-color: var(--accent); }

  .tags { display: flex; flex-wrap: wrap; gap: 8px; margin: 6px 0 4px; }
  .tag {
    border: 1px solid #28402f;
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

  .hidden { visibility: hidden; }

  footer.term {
    color: var(--dim);
    font-size: 0.75rem;
    margin-top: 18px;
  }

  @media (max-width: 480px) {
    .body { padding: 18px 16px 26px; font-size: 0.88rem; }
    .ascii { font-size: 0.5rem; }
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
    <div class="body" id="termBody"></div>
  </div>

<script>
const lines = [
  { type: 'ascii', text:
`##    ##  ########
###   ##  ##
####  ##  ######
## ## ##  ##
##  ####  ##
##   ###  ##
##    ##  ##` },
  { type: 'cmd', prompt: 'guest@nfranklin', path: '~', cmd: 'whoami' },
  { type: 'out', text: 'Nicholas C. Franklin' },
  { type: 'out', text: 'Director of Cybersecurity for Operational Technology (OT) & Tactical Systems @ <a href="https://www.leidos.com/" target="_blank" rel="noopener">Leidos</a>' },
  { type: 'cmd', prompt: 'guest@nfranklin', path: '~', cmd: 'cat status.txt' },
  { type: 'cmd', prompt: 'guest@nfranklin', path: '~', cmd: 'ls ./focus' },
  { type: 'tags', items: ['OT / ICS Security', 'Critical Infrastructure', 'CEMA & Pen Testing', 'Team Leadership', 'R&D / Strategy'] },
  { type: 'cmd', prompt: 'guest@nfranklin', path: '~', cmd: 'cat contact.txt' },
  { type: 'out', text: 'email   :: <a href="mailto:nicholascfranklin@gmail.com">nicholascfranklin@gmail.com</a>\nlinkedin:: <a href="https://www.linkedin.com/in/nicholas-franklin-bab45375/" target="_blank" rel="noopener">linkedin.com/in/nicholas-franklin</a>' },
  { type: 'cmd', prompt: 'guest@nfranklin', path: '~', cmd: '', final: true }
];

const body = document.getElementById('termBody');
let lineIndex = 0;

function makePromptSpan(prompt, path) {
  const span = document.createElement('span');
  span.className = 'prompt';
  span.innerHTML = `<span class="user">${prompt}</span>:<span class="path">${path}</span>$ `;
  return span;
}

function typeText(el, text, speed, cb) {
  let i = 0;
  function step() {
    if (i <= text.length) {
      el.textContent = text.slice(0, i);
      i++;
      setTimeout(step, speed);
    } else if (cb) cb();
  }
  step();
}

function renderNext() {
  if (lineIndex >= lines.length) return;
  const item = lines[lineIndex];
  const div = document.createElement('div');
  div.className = 'line';
  body.appendChild(div);

  if (item.type === 'ascii') {
    div.className = 'ascii';
    div.textContent = item.text;
    lineIndex++;
    setTimeout(renderNext, 200);
    return;
  }

  if (item.type === 'asciisub') {
    div.className = 'ascii-sub';
    div.textContent = item.text;
    lineIndex++;
    setTimeout(renderNext, 150);
    return;
  }

  if (item.type === 'cmd') {
    div.appendChild(makePromptSpan(item.prompt, item.path));
    const cmdSpan = document.createElement('span');
    div.appendChild(cmdSpan);
    const cursor = document.createElement('span');
    cursor.className = 'cursor';
    div.appendChild(cursor);

    if (item.final) {
      // last line: just blinking cursor, no command typed
      lineIndex++;
      return;
    }

    typeText(cmdSpan, item.cmd, 38, () => {
      cursor.remove();
      lineIndex++;
      setTimeout(renderNext, 260);
    });
    return;
  }

  if (item.type === 'out') {
    div.className = 'line out';
    div.innerHTML = item.text.replace(/\n/g, '<br>');
    lineIndex++;
    setTimeout(renderNext, 180);
    return;
  }

  if (item.type === 'tags') {
    div.className = 'line';
    const wrap = document.createElement('div');
    wrap.className = 'tags';
    item.items.forEach(t => {
      const tag = document.createElement('span');
      tag.className = 'tag';
      tag.textContent = t;
      wrap.appendChild(tag);
    });
    div.appendChild(wrap);
    lineIndex++;
    setTimeout(renderNext, 180);
    return;
  }
}

renderNext();
</script>
</body>
</html>

