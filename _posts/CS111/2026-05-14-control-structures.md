---
layout: post
title: Control Structures
description: Control Structures — CS 111 Review.
permalink: /cs111/control-structures
---

<style>
.oop-wrap { max-width: 900px; margin: 0 auto; }

.section-label { font-weight: bold; font-size: 1.4em; margin: 28px 0 8px 0; }
.section-sub { color: #888; font-size: 0.9em; margin-bottom: 12px; }

.hier-tree { padding: 20px 0; display: flex; flex-direction: column; align-items: center; margin: 16px 0 0 0; }
.hier-node {
    background: transparent; border: 1px solid #888; border-radius: 6px;
    padding: 8px 18px; min-width: 140px; text-align: center; cursor: pointer;
    font-family: monospace; font-weight: bold; color: inherit;
    transition: border-color 0.15s, color 0.15s; user-select: none; position: relative;
}
.hier-node:hover { border-color: #FA8072; }
.hier-node.active, .hier-node.ancestor { border-color: #FA8072; color: #FA8072; }
.hier-line { width: 1px; height: 22px; background: #888; }
.hier-line.lit { background: #FA8072; }
.hier-row {
    display: flex; gap: 50px; justify-content: center;
    position: relative; margin-top: 22px; padding-top: 22px; flex-wrap: wrap;
}
.hier-row::before {
    content: ""; position: absolute; top: 0; left: 50%;
    width: 1px; height: 22px; background: #888; transform: translateX(-0.5px);
}
.hier-row.lit::before { background: #FA8072; }
.hier-row::after {
    content: ""; position: absolute; top: 22px; left: 70px; right: 70px;
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

<div class="section-label">Control Structures</div>

Control structures decide which lines of code actually run, when they run, and how many times. They're the difference between a flat script and a program that reacts to whatever is happening in the moment — without them, code just plays out top-to-bottom with nothing branching, repeating, or responding to input.

<div class="section-label">Execution Flow</div>
<div class="section-sub">Click any block to read about it. The chain it depends on will light up.</div>

<div class="hier-tree">
    <div class="hier-node" data-node="Execution" data-parents="">Execution</div>
    <div class="hier-line" data-line="top-mid"></div>
    <div class="hier-node" data-node="Control" data-parents="Execution">Control Flow</div>
    <div class="hier-row" data-row="bottom">
        <div class="hier-node" data-node="Loop" data-parents="Execution,Control">Loop</div>
        <div class="hier-node" data-node="If" data-parents="Execution,Control">If / Else</div>
        <div class="hier-node" data-node="Nested" data-parents="Execution,Control">Nested If</div>
    </div>
</div>

<div class="hier-info" id="hier-info">
<p class="hint">Pick a block above to see how it shapes flow.</p>
</div>

<div class="section-label">The Three Categories</div>

<ol class="concept-list">
<li><strong>Iteration (Loops).</strong> A loop runs the same block of code over and over while a condition stays true. <code>for (let i = 0; i &lt; 5; i++)</code> repeats five times. In a game, loops are how you update every sprite on screen each frame or sweep through a list of enemies checking for collisions.</li>

<li><strong>Conditions (If / Else).</strong> A condition checks whether something is true and picks which branch of code to run. <code>if (health &lt;= 0) { die(); }</code> only runs if the player is out of health. Games rely on conditions for game-over screens, keyboard input, damage handling, and almost every reactive moment.</li>

<li><strong>Nested Conditions.</strong> A nested condition is a check inside another check — useful when one decision only matters after a previous one has gone a certain way. AI uses this constantly: an enemy might first check whether it's alert, then check whether the player is within attack range.

<pre><code class="language-javascript">if (enemy.isHostile) {
  if (distance &lt; 50) {
    enemy.attack();
  }
}</code></pre>
</li>
</ol>

<div class="section-label">The Three Structures — Tabbed View</div>
<div class="section-sub">Click a structure to switch tabs.</div>

<div class="tabs">
<div class="tab-bar">
    <button class="tab-btn active" data-tab="iter">Iteration</button>
    <button class="tab-btn" data-tab="cond">Conditions</button>
    <button class="tab-btn" data-tab="nest">Nested</button>
</div>

<div class="tab-panel active" data-panel="iter">
<h3>Iteration — Repeat</h3>
<p>Loops let you write a block once and have the computer run it as many times as you need. Pick the loop type that matches how the repetition ends.</p>

| Loop | Use when… |
|------|-----------|
| `for` | You know the count up front |
| `while` | You repeat until something changes |
| `for...of` | You're walking through an array |

<p>In games: updating sprites every frame, scanning collisions, running AI ticks, processing inventory.</p>
</div>

<div class="tab-panel" data-panel="cond">
<h3>Conditions — Decide</h3>
<p><code>if / else</code> is how your code reacts to what's actually happening right now.</p>

```javascript
if (health <= 0)       { die(); }
else if (health < 25)  { playWarning(); }
else                   { continue(); }
```

<p>In games: state changes, input handling, damage, win/lose logic, AI reactions.</p>
</div>

<div class="tab-panel" data-panel="nest">
<h3>Nested Conditions — Refine</h3>
<p>Putting one condition inside another lets you express layered logic — where the second check only matters if the first one passed.</p>

```javascript
if (enemy.isHostile) {
    if (distance < 50) {
        enemy.attack();  // only if BOTH are true
    }
}
```

<p>In games: AI decision trees, proximity checks, multi-state interactions.</p>
</div>
</div>

<div class="section-label">Quick Reference</div>

<div class="ref-list">
<div class="ref-row head">
<div>Structure</div><div>Keyword</div><div>Purpose</div>
</div>
<div class="ref-row">
<div>Iteration</div><div><code>for, while, for...of</code></div><div>Repeat actions</div>
</div>
<div class="ref-row">
<div>Condition</div><div><code>if, else if, else</code></div><div>Branch on truth</div>
</div>
<div class="ref-row">
<div>Nested Condition</div><div><code>if</code> inside <code>if</code></div><div>Layer decisions</div>
</div>
</div>

<div class="section-label">Key Things to Remember</div>

<ul class="takeaways">
<li>If something needs to <strong>repeat</strong>, that's a loop.</li>
<li>If something needs to <strong>choose</strong>, that's a condition.</li>
<li>If a choice <strong>depends on another choice</strong>, nest them.</li>
<li>Avoid stacking five layers deep — if your nesting gets that bad, the logic itself probably needs to be redesigned.</li>
</ul>

</div>

<script>
(function() {
    const nodeInfo = {
        Execution: {
            title: "Execution",
            blurb: "How code actually runs — line by line, top to bottom, unless something interrupts the order.",
            props: ["+sequential by default"]
        },
        Control: {
            title: "Control Flow",
            blurb: "Any structure that bends the order of execution — branching, repeating, or stopping early.",
            props: ["+changes the path", "+drives game logic"]
        },
        Loop: {
            title: "Iteration (Loop)",
            blurb: "Repeats a block of code until a condition turns false.",
            props: ["+for", "+while", "+for...of"]
        },
        If: {
            title: "Condition (If / Else)",
            blurb: "Chooses which branch runs based on a true/false test.",
            props: ["+if", "+else if", "+else"]
        },
        Nested: {
            title: "Nested Condition",
            blurb: "A check placed inside another check, for decisions that depend on previous decisions.",
            props: ["+layered logic", "+AI decisions"]
        }
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
            if (name !== 'Execution') {
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
