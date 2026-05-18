---
layout: post
title: Operators
description: Operators — CS 111 Review.
permalink: /cs111/operators
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

<div class="section-label">Operators</div>

Operators are the little symbols that actually do the work — combining values, comparing them, calculating new ones. Every move, every decision, and every UI update in a game runs through some operator.

<div class="section-label">Operator Categories</div>
<div class="section-sub">Click any category to see what it covers.</div>

<div class="hier-tree">
    <div class="hier-node" data-node="Op" data-parents="">Operator</div>
    <div class="hier-line" data-line="top-mid"></div>
    <div class="hier-node" data-node="Cat" data-parents="Op">Category</div>
    <div class="hier-row" data-row="bottom">
        <div class="hier-node" data-node="Math" data-parents="Op,Cat">Math</div>
        <div class="hier-node" data-node="Str" data-parents="Op,Cat">String</div>
        <div class="hier-node" data-node="Bool" data-parents="Op,Cat">Boolean</div>
    </div>
</div>

<div class="hier-info" id="hier-info">
<p class="hint">Pick a category above to see its operators.</p>
</div>

<div class="section-label">The Three Categories</div>

<ol class="concept-list">
<li><strong>String Operations.</strong> Concatenation joins text with <code>+</code>. Template literals embed values inside backticks: <code>`HP: ${hp}`</code>. You can pull out single characters by index: <code>"wolf"[0]</code> returns <code>"w"</code>. Used for dynamic UI text, file paths, and NPC state labels.</li>

<li><strong>Mathematical Operations.</strong> The basics — <code>+</code>, <code>-</code>, <code>*</code>, <code>/</code> — plus modulo (<code>%</code>), which gives the remainder of a division. Modulo is surprisingly useful for game timing: <code>frame % 60</code> cycles once every second at 60fps. Used everywhere movement, physics, damage, and animation timing show up.</li>

<li><strong>Boolean Expressions.</strong> Logical operators (<code>&amp;&amp;</code>, <code>||</code>, <code>!</code>) combine true/false values. Comparison operators (<code>===</code>, <code>&gt;</code>, <code>&lt;</code>) test relationships between values. Together they drive AI decisions, collision detection, and any toggle in game state.</li>
</ol>

<div class="section-label">The Three Categories — Tabbed View</div>
<div class="section-sub">Click a category to switch tabs.</div>

<div class="tabs">
<div class="tab-bar">
    <button class="tab-btn active" data-tab="math">Math</button>
    <button class="tab-btn" data-tab="str">String</button>
    <button class="tab-btn" data-tab="bool">Boolean</button>
</div>

<div class="tab-panel active" data-panel="math">
<h3>Mathematical Operators</h3>
<p>Math operators handle anything where numbers change.</p>

```javascript
frame % 60   // modulo — great for timing events
health - 10  // subtraction — take damage
velocity * 2 // multiplication — accelerate
```

<p>Used for movement, physics, gravity, damage, animation timing, and cooldowns. Anything that updates over time is built on math.</p>
</div>

<div class="tab-panel" data-panel="str">
<h3>String Operators</h3>
<p>String operators are for stitching text together and pulling parts out.</p>

```javascript
"Player " + name      // concatenation
`Health: ${hp}`       // template literal
"wolf"[0]             // character access → "w"
```

<p>Used for NPC state labels, sprite file paths, dynamic UI text, and dialogue.</p>
</div>

<div class="tab-panel" data-panel="bool">
<h3>Boolean Expressions</h3>
<p>Boolean operators decide whether something is true or not.</p>

```javascript
health > 0                  // comparison
state === "hostile"         // equality
isAlive && isVisible        // AND — both must be true
isPaused || isMenuOpen      // OR — either is enough
!isAttacking                // NOT — flip the value
```

<p>Used for AI decisions, collision logic, game loop control, and input handling. Booleans are the switches that turn behavior on and off.</p>
</div>
</div>

<div class="section-label">Quick Reference</div>

<div class="ref-list">
<div class="ref-row head">
<div>Category</div><div>Operators</div><div>Game purpose</div>
</div>
<div class="ref-row">
<div>Math</div><div><code>+ - * / %</code></div><div>Calculate movement, physics, timing</div>
</div>
<div class="ref-row">
<div>String</div><div><code>+</code> <code>`${ }`</code> <code>[]</code></div><div>Build dynamic text and paths</div>
</div>
<div class="ref-row">
<div>Boolean</div><div><code>&& || ! === &gt; &lt;</code></div><div>Make decisions and comparisons</div>
</div>
</div>

<div class="section-label">Key Things to Remember</div>

<ul class="takeaways">
<li><strong>Modulo (<code>%</code>)</strong> returns the remainder. <code>frame % 60 === 0</code> fires logic exactly once per second at 60fps — perfect for timed events.</li>
<li><strong><code>==</code> vs <code>===</code></strong> — always prefer <code>===</code>. It checks both value and type, so <code>5 === "5"</code> is <code>false</code> like you'd expect.</li>
<li><strong><code>&amp;&amp;</code> short-circuits</strong> — if the left side is already false, the right side never runs. Useful for guards.</li>
<li>Be careful with <code>+</code> on mixed types — <code>"5" + 3</code> gives <code>"53"</code>, not <code>8</code>. Convert first.</li>
</ul>

</div>

<script>
(function() {
    const nodeInfo = {
        Op: { title: "Operator", blurb: "A symbol that performs a specific action on one or more values.", props: ["+small, powerful", "+everywhere"] },
        Cat: { title: "Category", blurb: "Operators get grouped by the kind of data they work on.", props: ["+math, string, boolean"] },
        Math: { title: "Math Operators", blurb: "Arithmetic — calculate values that change over time.", props: ["+ - * / %"] },
        Str: { title: "String Operators", blurb: "Build text, join pieces, pull out characters.", props: ["++", "+`${ }`", "+[]"] },
        Bool: { title: "Boolean Expressions", blurb: "Compare values and combine true/false results.", props: ["+&&", "+||", "+!", "+===", "+>", "+<"] }
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
            if (name !== 'Op') {
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
