---
layout: post
title: Debugging
description: Debugging — CS 111 Review.
permalink: /cs111/debugging
---

<style>
.oop-wrap { max-width: 900px; margin: 0 auto; }

.section-label { font-weight: bold; font-size: 1.4em; margin: 28px 0 8px 0; }
.section-sub { color: #888; font-size: 0.9em; margin-bottom: 12px; }

.hier-tree { padding: 20px 0; display: flex; flex-direction: column; align-items: center; margin: 16px 0 0 0; }
.hier-node {
    background: transparent; border: 1px solid #888; border-radius: 6px;
    padding: 8px 14px; min-width: 110px; text-align: center; cursor: pointer;
    font-family: monospace; font-weight: bold; color: inherit;
    transition: border-color 0.15s, color 0.15s; user-select: none; position: relative;
    font-size: 0.9em;
}
.hier-node:hover { border-color: #FA8072; }
.hier-node.active, .hier-node.ancestor { border-color: #FA8072; color: #FA8072; }
.hier-line { width: 1px; height: 22px; background: #888; }
.hier-line.lit { background: #FA8072; }
.hier-row {
    display: flex; gap: 18px; justify-content: center;
    position: relative; margin-top: 22px; padding-top: 22px; flex-wrap: wrap;
}
.hier-row::before {
    content: ""; position: absolute; top: 0; left: 50%;
    width: 1px; height: 22px; background: #888; transform: translateX(-0.5px);
}
.hier-row.lit::before { background: #FA8072; }
.hier-row::after {
    content: ""; position: absolute; top: 22px; left: 55px; right: 55px;
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
    padding: 12px 14px; cursor: pointer; font-weight: bold; white-space: nowrap;
    font-size: 0.9em; opacity: 0.6; transition: opacity 0.15s;
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
    display: grid; grid-template-columns: 1.2fr 2fr 1fr; gap: 16px;
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

<div class="section-label">Debugging</div>

Debugging is the loop of finding a bug, working out where it lives, and fixing it. Across Gem.js, Guard.js, heistMusic.js, and the Heist.exe level files, six different debugging techniques were used to track problems down.

<div class="section-label">Debug Techniques</div>
<div class="section-sub">Click any technique to see how it was used.</div>

<div class="hier-tree">
    <div class="hier-node" data-node="Bug" data-parents="">Bug Found</div>
    <div class="hier-line" data-line="top-mid"></div>
    <div class="hier-node" data-node="Tools" data-parents="Bug">DevTools</div>
    <div class="hier-row" data-row="bottom">
        <div class="hier-node" data-node="Console" data-parents="Bug,Tools">Console</div>
        <div class="hier-node" data-node="Hitbox" data-parents="Bug,Tools">Hitbox</div>
        <div class="hier-node" data-node="Source" data-parents="Bug,Tools">Source</div>
        <div class="hier-node" data-node="Network" data-parents="Bug,Tools">Network</div>
        <div class="hier-node" data-node="App" data-parents="Bug,Tools">App</div>
        <div class="hier-node" data-node="Element" data-parents="Bug,Tools">Element</div>
    </div>
</div>

<div class="hier-info" id="hier-info">
<p class="hint">Pick a technique above to see where it was applied.</p>
</div>

<div class="section-label">The Six Techniques</div>

<ol class="concept-list">
<li><strong>Console Debugging.</strong> Scattered <code>console.log</code> calls across Gem.js, Guard.js, and heistMusic.js make runtime behavior visible. Gem.js logs gem creation and collection. Guard.js logs velocity every time the guard bounces off a wall. heistMusic.js logs the active track and warns when a fetch fails.

<pre><code class="language-javascript">console.log('Gem created:', this.spriteData?.id, 'at position', this.position);
console.log(this.velocity.y); // Guard bounce
console.warn('Background music: failed to start', error);</code></pre>
</li>

<li><strong>Hitbox Visualization.</strong> In HeistL1.js and HeistL3.js, every Barrier object is set with <code>visible: true</code> and a green semi-transparent color. The collision zones get drawn directly on top of the map so you can literally see where the walls and edges live.

<pre><code class="language-javascript">const border_top = {
  color: 'rgba(0, 255, 136, 0.5)',
  visible: true,
  hitbox: { widthPercentage: 1.0, heightPercentage: 1.0 }
};</code></pre>
</li>

<li><strong>Source-Level Debugging.</strong> Guard.js and Gem.js have <code>console.log</code> calls placed at meaningful execution points — collisions, velocity flips, gem collection — making it easy to set DevTools breakpoints right where the bug happens and step through frame by frame.

<pre><code class="language-javascript">// Guard.js — set a breakpoint here to inspect collision state
console.log('Collision has occurred, player has been destroyed.');

// Gem.js — breakpoint here to check permanentlyCollected state
if (this.permanentlyCollected) return;</code></pre>
</li>

<li><strong>Network Debugging.</strong> heistMusic.js fetches from the iTunes Search API. It checks <code>response.ok</code> before parsing and throws a descriptive error on failure, so problems show up clearly in the Network tab.

<pre><code class="language-javascript">const response = await fetch(this.endpoint);
if (!response.ok) {
  throw new Error('API request failed (' + response.status + ')');
}
const data = await response.json();</code></pre>
</li>

<li><strong>Application Debugging.</strong> Gem totals live on <code>gameEnv.stats.coinsCollected</code>. Boolean flags like <code>permanentlyCollected</code> and <code>isPlaying</code> track game state at runtime — all inspectable in the Application tab.

<pre><code class="language-javascript">// Gem.js — state stored on gameEnv
this.gameEnv.stats.coinsCollected = (this.gameEnv.stats.coinsCollected || 0) + this.value;

// heistMusic.js — runtime flags
this.started = true;
this.isPlaying = true;</code></pre>
</li>

<li><strong>Element Inspection.</strong> heistMusic.js builds a toggle button at runtime and appends it to <code>document.body</code>. Gem.js hides its canvas after collection by setting <code>canvas.style.display</code>. Both changes show up live in the Elements tab.

<pre><code class="language-javascript">// heistMusic.js — button added to DOM
document.body.appendChild(btn);

// Gem.js — canvas hidden after collection
if (this.canvas) this.canvas.style.display = 'none';</code></pre>
</li>
</ol>

<div class="section-label">The Six Techniques — Tabbed View</div>
<div class="section-sub">Click a technique to switch tabs.</div>

<div class="tabs">
<div class="tab-bar">
    <button class="tab-btn active" data-tab="console">Console</button>
    <button class="tab-btn" data-tab="hitbox">Hitbox</button>
    <button class="tab-btn" data-tab="source">Source</button>
    <button class="tab-btn" data-tab="network">Network</button>
    <button class="tab-btn" data-tab="app">Application</button>
    <button class="tab-btn" data-tab="element">Element</button>
</div>

<div markdown="1" class="tab-panel active" data-panel="console">
<h3>Console Debugging — Gem.js · Guard.js · heistMusic.js</h3>
<p>Print whatever needs to be visible right now.</p>

```javascript
console.log('Gem created:', this.spriteData?.id, 'at position', this.position);
console.log(this.velocity.y); // logs every time Guard bounces
console.warn('Background music: failed to start', error);
```
</div>

<div markdown="1" class="tab-panel" data-panel="hitbox">
<h3>Hitbox Visualization — HeistL1.js · HeistL3.js</h3>
<p>Render collision zones as semi-transparent green overlays so you can see where walls actually are.</p>

```javascript
const border_top = {
  color: 'rgba(0, 255, 136, 0.5)',
  visible: true,
  hitbox: { widthPercentage: 1.0, heightPercentage: 1.0 }
};
```
</div>

<div markdown="1" class="tab-panel" data-panel="source">
<h3>Source-Level Debugging — Guard.js · Gem.js</h3>
<p>Strategic log calls double as breakpoint targets in DevTools.</p>

```javascript
if (this.permanentlyCollected) return;           // Gem.js
console.log("Collision has occurred...");         // Guard.js
```
</div>

<div markdown="1" class="tab-panel" data-panel="network">
<h3>Network Debugging — heistMusic.js</h3>
<p>Check the response and throw a descriptive error when a fetch fails.</p>

```javascript
const response = await fetch(this.endpoint);
if (!response.ok) throw new Error('API request failed (' + response.status + ')');
const data = await response.json();
```
</div>

<div markdown="1" class="tab-panel" data-panel="app">
<h3>Application Debugging — Gem.js · heistMusic.js</h3>
<p>State stored on <code>gameEnv</code> and runtime flags — all inspectable in DevTools.</p>

```javascript
this.gameEnv.stats.coinsCollected += this.value; // Gem.js
this.started = true;                              // heistMusic.js
```
</div>

<div markdown="1" class="tab-panel" data-panel="element">
<h3>Element Inspection — heistMusic.js · Gem.js</h3>
<p>Runtime DOM changes you can inspect in the Elements tab.</p>

```javascript
document.body.appendChild(btn);             // heistMusic.js
this.canvas.style.display = 'none';         // Gem.js
```
</div>
</div>

<div class="section-label">Quick Reference</div>

<div class="ref-list">
<div class="ref-row head">
<div>Technique</div><div>File</div><div>DevTools Tab</div>
</div>
<div class="ref-row">
<div>Console Debugging</div><div>Gem.js, Guard.js, heistMusic.js</div><div>Console</div>
</div>
<div class="ref-row">
<div>Hitbox Visualization</div><div>HeistL1.js, HeistL3.js</div><div>Canvas overlay</div>
</div>
<div class="ref-row">
<div>Source-Level Debugging</div><div>Guard.js, Gem.js</div><div>Sources</div>
</div>
<div class="ref-row">
<div>Network Debugging</div><div>heistMusic.js</div><div>Network</div>
</div>
<div class="ref-row">
<div>Application Debugging</div><div>Gem.js, heistMusic.js</div><div>Application</div>
</div>
<div class="ref-row">
<div>Element Inspection</div><div>heistMusic.js, Gem.js</div><div>Elements</div>
</div>
</div>

<div class="section-label">Key Things to Remember</div>

<ul class="takeaways">
<li>Start with <strong><code>console.log</code></strong> to narrow down where the bug lives, then switch to a more specific DevTools tab to dig in.</li>
<li>Use <strong><code>console.warn</code></strong> or <strong><code>console.error</code></strong> when something is actually wrong — they stand out from regular logs.</li>
<li><strong>Hitbox visualization</strong> is invaluable for collision bugs. You can't fix what you can't see.</li>
<li>Match the <strong>DevTools tab</strong> to the bug: network failures go to Network, saved state goes to Application, DOM issues go to Elements.</li>
</ul>

</div>

<script>
(function() {
    const nodeInfo = {
        Bug: { title: "Bug Found", blurb: "Something went wrong. The first job is figuring out where to look.", props: ["+narrow down location", "+pick the right tool"] },
        Tools: { title: "DevTools", blurb: "The browser's developer tools have a tab for almost every kind of bug.", props: ["+six core tabs"] },
        Console: { title: "Console Debugging", blurb: "Quick runtime visibility through console.log.", props: ["+console.log", "+console.warn", "+console.error"] },
        Hitbox: { title: "Hitbox Visualization", blurb: "Render collision zones so you can literally see them.", props: ["+visible: true", "+green overlay"] },
        Source: { title: "Source-Level Debugging", blurb: "Breakpoints in DevTools let you pause and step through code.", props: ["+breakpoints", "+step over/into"] },
        Network: { title: "Network Debugging", blurb: "Inspect HTTP requests and responses in the Network tab.", props: ["+response.ok", "+status codes"] },
        App: { title: "Application Debugging", blurb: "View runtime state and storage in the Application tab.", props: ["+gameEnv state", "+localStorage"] },
        Element: { title: "Element Inspection", blurb: "Inspect live DOM and CSS in the Elements tab.", props: ["+appendChild", "+style.display"] }
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
            if (name !== 'Bug') {
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
