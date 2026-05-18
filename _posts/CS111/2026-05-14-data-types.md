---
layout: post
title: Data Types
description: Data Types — CS 111 Review.
permalink: /cs111/data-types
---

<style>
.oop-wrap { max-width: 900px; margin: 0 auto; }

.section-label { font-weight: bold; font-size: 1.4em; margin: 28px 0 8px 0; }
.section-sub { color: #888; font-size: 0.9em; margin-bottom: 12px; }

.hier-tree { padding: 20px 0; display: flex; flex-direction: column; align-items: center; margin: 16px 0 0 0; }
.hier-node {
    background: transparent; border: 1px solid #888; border-radius: 6px;
    padding: 8px 18px; min-width: 120px; text-align: center; cursor: pointer;
    font-family: monospace; font-weight: bold; color: inherit;
    transition: border-color 0.15s, color 0.15s; user-select: none; position: relative;
}
.hier-node:hover { border-color: #FA8072; }
.hier-node.active, .hier-node.ancestor { border-color: #FA8072; color: #FA8072; }
.hier-line { width: 1px; height: 22px; background: #888; }
.hier-line.lit { background: #FA8072; }
.hier-row {
    display: flex; gap: 24px; justify-content: center;
    position: relative; margin-top: 22px; padding-top: 22px; flex-wrap: wrap;
}
.hier-row::before {
    content: ""; position: absolute; top: 0; left: 50%;
    width: 1px; height: 22px; background: #888; transform: translateX(-0.5px);
}
.hier-row.lit::before { background: #FA8072; }
.hier-row::after {
    content: ""; position: absolute; top: 22px; left: 60px; right: 60px;
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
    display: grid; grid-template-columns: 2fr 1fr; gap: 16px;
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

<div class="section-label">Data Types</div>

Data types tell your code what kind of value it's working with — and what that value can do. Pick the wrong one and things crash, slow down, or just produce weird results. Pick the right one and the rest of your code stays readable and clean.

<div class="section-label">Type Tree</div>
<div class="section-sub">Click any type to see how it shows up in a game.</div>

<div class="hier-tree">
    <div class="hier-node" data-node="Data" data-parents="">Data</div>
    <div class="hier-line" data-line="top-mid"></div>
    <div class="hier-node" data-node="Type" data-parents="Data">Type</div>
    <div class="hier-row" data-row="bottom">
        <div class="hier-node" data-node="Number" data-parents="Data,Type">Number</div>
        <div class="hier-node" data-node="String" data-parents="Data,Type">String</div>
        <div class="hier-node" data-node="Boolean" data-parents="Data,Type">Boolean</div>
        <div class="hier-node" data-node="Array" data-parents="Data,Type">Array</div>
        <div class="hier-node" data-node="Object" data-parents="Data,Type">Object</div>
    </div>
</div>

<div class="hier-info" id="hier-info">
<p class="hint">Pick a type above to see what it stores.</p>
</div>

<div class="section-label">The Five Core Types</div>

<ol class="concept-list">
<li><strong>Number.</strong> Anything you'd write as a numeric value — health, speed, position, frame count. Example: <code>velocity: 3</code>. Used for physics, damage math, timers, and pretty much anything that changes over time.</li>

<li><strong>String.</strong> Text in any form — names, modes, file paths, dialogue. Example: <code>"hostile"</code>. Used for NPC states, sprite paths, UI labels, and item or quest IDs.</li>

<li><strong>Boolean.</strong> A simple yes/no switch — only ever <code>true</code> or <code>false</code>. Example: <code>isPaused: true</code>. Used for any binary game state: <code>isJumping</code>, <code>isAlive</code>, <code>isAttacking</code>, pause flags, visibility toggles.</li>

<li><strong>Array.</strong> An ordered list of similar items. Example: <code>gameObjects[]</code>. Used for collections — every enemy on screen, every bullet in flight, every inventory slot.</li>

<li><strong>JSON Object.</strong> A bundle of named properties grouped together. Example: <code>{ hitbox: { width: 40 } }</code>. Used for anything with more than one piece of info: NPC configs, level definitions, save files, dialogue trees.</li>
</ol>

<div class="section-label">The Five Types — Tabbed View</div>
<div class="section-sub">Click a type to switch tabs.</div>

<div class="tabs">
<div class="tab-bar">
    <button class="tab-btn active" data-tab="num">Number</button>
    <button class="tab-btn" data-tab="str">String</button>
    <button class="tab-btn" data-tab="bool">Boolean</button>
    <button class="tab-btn" data-tab="arr">Array</button>
    <button class="tab-btn" data-tab="obj">Object</button>
</div>

<div class="tab-panel active" data-panel="num">
<h3>Number</h3>
<p>Numbers cover anything that ticks, counts, or measures.</p>

```javascript
velocity: 3
```

<p>Physics, health, movement speed, animation timing, hit detection — if it changes frame by frame, it's a number.</p>
</div>

<div class="tab-panel" data-panel="str">
<h3>String</h3>
<p>Strings hold text — labels, modes, identifiers.</p>

```javascript
state: "hostile"
```

<p>NPC behavior modes, sprite paths, dialogue, item and quest IDs all live as strings.</p>
</div>

<div class="tab-panel" data-panel="bool">
<h3>Boolean</h3>
<p>The simplest type in the language. Just <code>true</code> or <code>false</code> — nothing else.</p>

```javascript
isPaused: true
```

<p>Game loop control, AI flags, visibility toggles, invincibility frames, input handling — anything that has only two states.</p>
</div>

<div class="tab-panel" data-panel="arr">
<h3>Array</h3>
<p>An ordered list of values, usually all of the same kind.</p>

```javascript
gameObjects[]
```

<p>Every active sprite, every enemy or bullet group, particle effects, inventory slots, level layouts.</p>
</div>

<div class="tab-panel" data-panel="obj">
<h3>JSON Object</h3>
<p>A bundle of related properties grouped under one name.</p>

```javascript
{ hitbox: { width: 40, height: 60 } }
```

<p>NPC configs, level definitions, save files, game settings, dialogue trees.</p>
</div>
</div>

<div class="section-label">Quick Reference</div>

<div class="ref-list">
<div class="ref-row head">
<div>If you need to store…</div><div>Use</div>
</div>
<div class="ref-row">
<div>A count, position, or measurement</div><div><code>Number</code></div>
</div>
<div class="ref-row">
<div>A name, mode, or file path</div><div><code>String</code></div>
</div>
<div class="ref-row">
<div>A yes/no state</div><div><code>Boolean</code></div>
</div>
<div class="ref-row">
<div>A collection of similar things</div><div><code>Array</code></div>
</div>
<div class="ref-row">
<div>A thing with many properties</div><div><code>JSON Object</code></div>
</div>
</div>

<div class="section-label">Key Things to Remember</div>

<ul class="takeaways">
<li>Watch the <strong>"true" vs true</strong> trap — one is a string, the other is a boolean. They look identical but behave totally differently in logic checks.</li>
<li>Numbers do math; strings concatenate. <code>"5" + 3</code> gives <code>"53"</code>, not <code>8</code>.</li>
<li>Arrays are best when all items are similar; objects are better when each property is different.</li>
<li>A <strong>JSON object</strong> doesn't have to come from a file — it's just a way of bundling named values.</li>
</ul>

</div>

<script>
(function() {
    const nodeInfo = {
        Data: { title: "Data", blurb: "Every value in your code is a piece of data. The type decides what it can do.", props: ["+typed", "+manipulable"] },
        Type: { title: "Data Type", blurb: "The shape of a value — what operations are valid, how comparisons work.", props: ["+primitive or complex"] },
        Number: { title: "Number", blurb: "Numeric values for physics, health, timing, and movement.", props: ["+velocity = 3", "+math operations"] },
        String: { title: "String", blurb: "Text — labels, names, file paths, dialogue.", props: ["+\"hostile\"", "+concatenation"] },
        Boolean: { title: "Boolean", blurb: "A two-state value — only true or false.", props: ["+isPaused = true", "+&& || !"] },
        Array: { title: "Array", blurb: "An ordered list of similar items.", props: ["+gameObjects[]", "+for...of"] },
        Object: { title: "JSON Object", blurb: "Structured data with multiple named properties.", props: ["+{ width: 40 }", "+nested"] }
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
            if (name !== 'Data') {
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
