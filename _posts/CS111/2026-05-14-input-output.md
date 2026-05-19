---
layout: post
title: Input/Output
description: Input/Output — CS 111 Review.
permalink: /cs111/input-output
---

<style>
.oop-wrap { max-width: 900px; margin: 0 auto; }

.section-label { font-weight: bold; font-size: 1.4em; margin: 28px 0 8px 0; }
.section-sub { color: #888; font-size: 0.9em; margin-bottom: 12px; }

.hier-tree { padding: 20px 0; display: flex; flex-direction: column; align-items: center; margin: 16px 0 0 0; }
.hier-node {
    background: transparent; border: 1px solid #888; border-radius: 6px;
    padding: 8px 18px; min-width: 130px; text-align: center; cursor: pointer;
    font-family: monospace; font-weight: bold; color: inherit;
    transition: border-color 0.15s, color 0.15s; user-select: none; position: relative;
}
.hier-node:hover { border-color: #FA8072; }
.hier-node.active, .hier-node.ancestor { border-color: #FA8072; color: #FA8072; }
.hier-line { width: 1px; height: 22px; background: #888; }
.hier-line.lit { background: #FA8072; }
.hier-row {
    display: flex; gap: 30px; justify-content: center;
    position: relative; margin-top: 22px; padding-top: 22px; flex-wrap: wrap;
}
.hier-row::before {
    content: ""; position: absolute; top: 0; left: 50%;
    width: 1px; height: 22px; background: #888; transform: translateX(-0.5px);
}
.hier-row.lit::before { background: #FA8072; }
.hier-row::after {
    content: ""; position: absolute; top: 22px; left: 65px; right: 65px;
    height: 1px; background: #888;
}
.hier-row.lit::after { background: #FA8072; }
.hier-row > .hier-node { margin-top: 0; }
.hier-row > .hier-node::before {
    content: ""; position: absolute; top: -22px; left: 50%;
    width: 1px; height: 22px; background: #888; transform: translateX(-0.5px);
}
.hier-row > .hier-node.active::before, .hier-row > .hier-node.ancestor::before { background: #FA8072; }

.hier-info {
    margin: 20px auto 0 auto; max-width: 600px; padding: 14px 0;
    border-top: 1px solid #444; text-align: left;
}
.hier-info h4 { margin: 0 0 6px 0; font-family: monospace; color: #FA8072; }
.hier-info p { margin: 4px 0 8px 0; line-height: 1.5; }
.hier-info ul { margin: 6px 0 0 0; padding-left: 20px; }
.hier-info li { font-family: monospace; font-size: 0.92em; margin-bottom: 3px; }
.hier-info .hint { color: #888; font-style: italic; text-align: center; }

.concept-list { counter-reset: concept; padding-left: 0; list-style: none; }
.concept-list li { margin-bottom: 14px; counter-increment: concept; line-height: 1.6; }
.concept-list li::before { content: counter(concept) ". "; color: #FA8072; font-weight: bold; }
.concept-list strong { color: #FA8072; }

.tabs { border: 1px solid #444; border-radius: 6px; overflow: hidden; margin: 0 0 20px 0; }
.tab-bar { display: flex; border-bottom: 1px solid #444; overflow-x: auto; }
.tab-btn {
    flex: 1; background: transparent; border: none; color: inherit;
    padding: 12px 16px; cursor: pointer; font-weight: bold; white-space: nowrap;
    font-size: 0.95em; opacity: 0.6; transition: opacity 0.15s;
    outline: none; -webkit-tap-highlight-color: transparent;
}
.tab-btn:hover { opacity: 1; }
.tab-btn:focus, .tab-btn:focus-visible { outline: none; }
.tab-btn.active { opacity: 1; color: #FA8072; border-bottom: 2px solid #FA8072; }
.tab-panel { display: none; padding: 18px; }
.tab-panel.active { display: block; }
.tab-panel h3 { margin-top: 0; }

.ref-list { margin: 16px 0; }
.ref-row {
    display: grid; grid-template-columns: 1fr 1fr 2fr; gap: 16px;
    padding: 10px 4px; border-bottom: 1px solid #333; align-items: center;
}
.ref-row.head { font-weight: bold; color: #FA8072; border-bottom: 1px solid #FA8072; }
.ref-row code { font-family: monospace; }

.takeaways { padding-left: 0; list-style: none; margin: 16px 0; }
.takeaways li { padding: 10px 0; border-bottom: 1px solid #333; line-height: 1.5; }
.takeaways li:last-child { border-bottom: none; }
.takeaways strong { color: #FA8072; }
</style>

<div class="oop-wrap">

<div class="section-label">Input / Output</div>

I/O is the conversation your game has with the world. Information flows in — from the keyboard, from the config, from the network — your code reacts, and something gets sent back out to the screen. Every interactive moment runs through this loop.

<div class="section-label">I/O Channels</div>
<div class="section-sub">Click any channel to see how it moves data.</div>

<div class="hier-tree">
    <div class="hier-node" data-node="Game" data-parents="">Game</div>
    <div class="hier-line" data-line="top-mid"></div>
    <div class="hier-node" data-node="IO" data-parents="Game">I / O</div>
    <div class="hier-row" data-row="bottom">
        <div class="hier-node" data-node="Keyboard" data-parents="Game,IO">Keyboard</div>
        <div class="hier-node" data-node="Env" data-parents="Game,IO">GameEnv</div>
        <div class="hier-node" data-node="API" data-parents="Game,IO">API</div>
        <div class="hier-node" data-node="Canvas" data-parents="Game,IO">Canvas</div>
    </div>
</div>

<div class="hier-info" id="hier-info">
<p class="hint">Pick a channel above to see what it does.</p>
</div>

<div class="section-label">The Four Systems</div>

<ol class="concept-list">
<li><strong>Canvas Rendering (Output).</strong> Draws every visible pixel, every frame. <code>ctx.fillRect(x, y, w, h)</code> paints rectangles; <code>ctx.drawImage(sprite, x, y)</code> paints sprites. Used for sprites, backgrounds, UI, and animations.</li>

<li><strong>Keyboard Events (Input).</strong> Listens for physical key presses. <code>window.addEventListener("keydown", (e) =&gt; { ... })</code> fires whenever a key goes down. Used for movement, jumping, attacking, and menu navigation.</li>

<li><strong>GameEnv Config (Input).</strong> A bundle of startup settings that defines the rules — gravity, debug mode, canvas size, difficulty. Loaded once at boot and read by every system after that.</li>

<li><strong>API Calls (I/O).</strong> Sends data out to a server and waits for data back. <code>fetch("/api/score")</code> returns a Promise with the response. Used for leaderboards, cloud saves, dynamic AI behavior, and multiplayer sync.</li>
</ol>

<div class="section-label">The Four Systems — Tabbed View</div>
<div class="section-sub">Click a system to switch tabs.</div>

<div class="tabs">
<div class="tab-bar">
    <button class="tab-btn active" data-tab="kb">Keyboard</button>
    <button class="tab-btn" data-tab="env">GameEnv</button>
    <button class="tab-btn" data-tab="api">API</button>
    <button class="tab-btn" data-tab="canvas">Canvas</button>
</div>

<div markdown="1" class="tab-panel active" data-panel="kb">
<h3>Keyboard Events — Input</h3>
<p>Translates physical key presses into in-game actions.</p>

```javascript
window.addEventListener("keydown", (e) => {
  if (e.key === " ") player.jump();
});
```

<p><code>keydown</code> fires on press, <code>keyup</code> on release. Used for movement, jumping, attacking, menu navigation.</p>
</div>

<div markdown="1" class="tab-panel" data-panel="env">
<h3>GameEnv Config — Input</h3>
<p>System-level input that's set once at startup — not from the player, from your own code.</p>

```javascript
const gameEnv = { gravity: 0.4, debug: false };
```

<p>Defines canvas size, gravity, physics, difficulty, and asset paths. Everything else builds on top of these values.</p>
</div>

<div markdown="1" class="tab-panel" data-panel="api">
<h3>API Calls — Input + Output</h3>
<p>Two-way communication with a server.</p>

```javascript
fetch("/api/score")
  .then(res => res.json())
  .then(data => show(data));
```

<p>Sends data out and gets data back. Used for leaderboards, cloud saves, dynamic AI, multiplayer.</p>
</div>

<div markdown="1" class="tab-panel" data-panel="canvas">
<h3>Canvas Rendering — Output</h3>
<p>Draws everything the player sees, every frame.</p>

```javascript
ctx.fillRect(x, y, w, h);
ctx.drawImage(sprite, x, y);
```

<p>Renders sprites, backgrounds, UI, effects. The final step in the loop: state updates first, then the canvas draws it.</p>
</div>
</div>

<div class="section-label">Quick Reference</div>

<div class="ref-list">
<div class="ref-row head">
<div>Channel</div><div>Direction</div><div>Game use</div>
</div>
<div class="ref-row">
<div>Keyboard</div><div>Input</div><div>Movement, jumping, menus</div>
</div>
<div class="ref-row">
<div>GameEnv</div><div>Input (startup)</div><div>Gravity, canvas size, difficulty</div>
</div>
<div class="ref-row">
<div>API</div><div>Input + Output</div><div>Scores, saves, multiplayer</div>
</div>
<div class="ref-row">
<div>Canvas</div><div>Output</div><div>All visuals every frame</div>
</div>
</div>

<div class="section-label">Key Things to Remember</div>

<ul class="takeaways">
<li><strong>Input updates state. Output draws state.</strong> The game loop is the bridge between them — it runs every frame.</li>
<li><strong>Keyboard events</strong> are asynchronous — they fire when the OS notices them, not on a fixed schedule.</li>
<li><strong>GameEnv</strong> is read-only after startup. It sets the rules everything else plays by.</li>
<li><strong>APIs return Promises</strong> — don't use the response before it actually arrives. <code>await</code> it or chain <code>.then()</code>.</li>
</ul>

</div>

<script>
(function() {
    const nodeInfo = {
        Game: { title: "Game", blurb: "The running loop. Needs data flowing in and visuals flowing out every frame.", props: ["+state", "+frame loop"] },
        IO: { title: "Input / Output", blurb: "Every channel through which data enters or leaves your game.", props: ["+input updates state", "+output draws state"] },
        Keyboard: { title: "Keyboard Events", blurb: "Player presses keys → game reacts.", props: ["+keydown", "+keyup", "+e.key"] },
        Env: { title: "GameEnv Config", blurb: "Startup settings the game reads once and uses everywhere.", props: ["+gravity", "+canvas size"] },
        API: { title: "API Calls", blurb: "Two-way network communication with a server.", props: ["+fetch", "+async/await"] },
        Canvas: { title: "Canvas Rendering", blurb: "Pixels on the screen — the visible output of every frame.", props: ["+ctx.fillRect", "+ctx.drawImage"] }
    };

    const info = document.getElementById('hier-info');
    document.querySelectorAll('.hier-node').forEach(n => {
        n.addEventListener('click', () => {
            document.querySelectorAll('.hier-node').forEach(x => x.classList.remove('active','ancestor'));
            document.querySelectorAll('.hier-line').forEach(x => x.classList.remove('lit'));
            document.querySelectorAll('.hier-row').forEach(x => x.classList.remove('lit'));

            n.classList.add('active');
            const parents = (n.dataset.parents || '').split(',').filter(Boolean);
            parents.forEach(p => {
                document.querySelector(`.hier-node[data-node="${p}"]`)?.classList.add('ancestor');
            });

            const name = n.dataset.node;
            if (name !== 'Game') {
                document.querySelector('[data-line="top-mid"]')?.classList.add('lit');
            }
            if (n.parentElement?.classList.contains('hier-row')) {
                n.parentElement.classList.add('lit');
            }

            const d = nodeInfo[name];
            info.innerHTML = `
                <h4>${d.title}</h4>
                <p>${d.blurb}</p>
                <ul>${d.props.map(p => `<li>${p}</li>`).join('')}</ul>
            `;
        });
    });

    document.querySelectorAll('.tab-btn').forEach(btn => {
        btn.addEventListener('click', () => {
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
            btn.classList.add('active');
            document.querySelector(`.tab-panel[data-panel="${btn.dataset.tab}"]`)?.classList.add('active');
            btn.blur();
        });
    });
})();
</script>
