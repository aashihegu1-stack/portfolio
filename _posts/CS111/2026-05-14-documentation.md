---
layout: post
title: Documentation
description: Documentation — CS 111 Review.
permalink: /cs111/documentation
---

<style>
.oop-wrap { max-width: 900px; margin: 0 auto; }

.section-label { font-weight: bold; font-size: 1.4em; margin: 28px 0 8px 0; }
.section-sub { color: #888; font-size: 0.9em; margin-bottom: 12px; }

.game-btn-wrap { margin: 20px 0 30px 0; }
.game-btn {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    padding: 12px 22px;
    border: 1px solid #FA8072;
    border-radius: 6px;
    color: #FA8072;
    font-weight: bold;
    text-decoration: none;
    transition: background 0.15s, color 0.15s;
}
.game-btn:hover {
    background: #FA8072;
    color: #14142b;
    text-decoration: none;
}
.game-btn .arrow { font-family: monospace; }

.class-table { margin: 16px 0; }
.class-row {
    display: grid;
    grid-template-columns: 1fr 1.6fr 2fr;
    gap: 16px;
    padding: 10px 4px;
    border-bottom: 1px solid #333;
    align-items: center;
}
.class-row.head { font-weight: bold; color: #FA8072; border-bottom: 1px solid #FA8072; }
.class-row code { font-family: monospace; font-size: 0.92em; }

.doc-card {
    border: 1px solid #444;
    border-radius: 6px;
    padding: 12px 16px;
    margin-bottom: 10px;
    cursor: pointer;
}
.doc-card[open] { border-color: #FA8072; }
.doc-card summary {
    font-weight: bold;
    list-style: none;
    color: #FA8072;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 1.02em;
}
.doc-card summary::-webkit-details-marker { display: none; }
.doc-card summary::after {
    content: "▼";
    font-size: 0.8em;
    transition: transform 0.15s;
}
.doc-card[open] summary::after { transform: rotate(180deg); }
.doc-card .doc-body { margin-top: 12px; padding-top: 10px; border-top: 1px solid #333; }
.doc-card .doc-item {
    padding: 8px 0;
    border-bottom: 1px solid #2a2a2a;
    line-height: 1.5;
}
.doc-card .doc-item:last-child { border-bottom: none; }
.doc-card .doc-item strong { color: #FA8072; display: inline-block; min-width: 200px; }
.doc-card .doc-item code { font-family: monospace; font-size: 0.92em; }

.takeaways { padding-left: 0; list-style: none; margin: 16px 0; }
.takeaways li { padding: 10px 0; border-bottom: 1px solid #333; line-height: 1.5; }
.takeaways li:last-child { border-bottom: none; }
.takeaways strong { color: #FA8072; }
</style>

<div class="oop-wrap">

<div class="section-label">Documentation</div>

Documentation is everything around the code that explains how the code actually works — class hierarchies, in-line comments, README walkthroughs, and the running examples themselves. For CS 111, the clearest documentation is the project itself: PirateMegaGame, where every CS 111 concept shows up in a real, runnable place.

<div class="game-btn-wrap">
<a class="game-btn" href="https://piratemegagame.opencodingsociety.com/gamify/PirateMegaGame" target="_blank" rel="noopener">
☠️🦜 Play PirateMegaGame <span class="arrow">→</span>
</a>
</div>

<div class="section-label">Game Object Class Overview</div>
<div class="section-sub">Here's how each major game object slots into the engine's class hierarchy.</div>

<div class="class-table">
<div class="class-row head">
<div>Game Object</div><div>Class</div><div>Role</div>
</div>
<div class="class-row">
<div>McArchie</div><div><code>Player extends Character</code></div><div>Player-controlled character</div>
</div>
<div class="class-row">
<div>Pirate</div><div><code>Pirate extends Character</code></div><div>"Enemy" NPC with reaction logic</div>
</div>
<div class="class-row">
<div>Map</div><div><code>Background extends GameObject</code></div><div>Layered scrolling environment</div>
</div>
<div class="class-row">
<div>Shields</div><div><code>Barrier extends GameObject</code></div><div>Collision boundaries</div>
</div>
</div>

<div class="section-label">Concepts in Practice</div>
<div class="section-sub">Click any topic to see where it shows up in the codebase.</div>

<details class="doc-card">
<summary>🧬 Object-Oriented Programming</summary>
<div class="doc-body">
<div class="doc-item"><strong>Inheritance</strong> <code>GameObject → Character → Player / Pirate</code></div>
<div class="doc-item"><strong>Writing Classes</strong> Custom subclasses like <code>Player</code> and <code>Pirate</code></div>
<div class="doc-item"><strong>Method Overriding</strong> Custom <code>update()</code>, <code>draw()</code>, <code>handleCollision()</code></div>
<div class="doc-item"><strong>Constructor Chaining</strong> <code>super(data, gameEnv)</code> ensures engine initialization</div>
</div>
</details>

<details class="doc-card">
<summary>🔁 Control Structures</summary>
<div class="doc-body">
<div class="doc-item"><strong>Iteration</strong> <code>forEach</code> loops in update + cleanup passes</div>
<div class="doc-item"><strong>Conditionals</strong> Collision checks, AI decisions, state transitions</div>
<div class="doc-item"><strong>Nested Conditions</strong> NPC type → proximity → inventory (3 layers)</div>
</div>
</details>

<details class="doc-card">
<summary>🔢 Data Types</summary>
<div class="doc-body">
<div class="doc-item"><strong>Numbers</strong> <code>x</code>, <code>y</code>, <code>velocity</code>, <code>score</code></div>
<div class="doc-item"><strong>Strings</strong> Names, sprite paths, game states</div>
<div class="doc-item"><strong>Booleans</strong> <code>isPaused</code>, <code>isJumping</code>, <code>isVulnerable</code></div>
<div class="doc-item"><strong>Arrays</strong> <code>gameObjects[]</code>, level arrays</div>
<div class="doc-item"><strong>JSON Objects</strong> NPC config + GameLevel setup</div>
</div>
</details>

<details class="doc-card">
<summary>➗ Operators</summary>
<div class="doc-body">
<div class="doc-item"><strong>Math Ops</strong> <code>+=</code>, <code>*</code>, <code>Math.pow()</code></div>
<div class="doc-item"><strong>String Ops</strong> Template literals for sprite paths</div>
<div class="doc-item"><strong>Boolean Expressions</strong> <code>&amp;&amp;</code>, <code>||</code>, <code>!</code></div>
</div>
</details>

<details class="doc-card">
<summary>🎨 Input / Output</summary>
<div class="doc-body">
<div class="doc-item"><strong>Canvas Rendering</strong> <code>draw()</code> via <code>requestAnimationFrame</code></div>
<div class="doc-item"><strong>Keyboard Events</strong> <code>keydown</code> / <code>keyup</code> for movement</div>
<div class="doc-item"><strong>GameEnv Config</strong> Object literal world configuration</div>
</div>
</details>

<details class="doc-card">
<summary>🧪 Software Engineering Practices</summary>
<div class="doc-body">
<div class="doc-item"><strong>Single Responsibility</strong> Each method handles one behavior</div>
<div class="doc-item"><strong>Data-Driven Design</strong> GameBuilder uses Object Literals</div>
<div class="doc-item"><strong>Instantiation</strong> Level config spawns all objects</div>
<div class="doc-item"><strong>Documentation</strong> Inline comments throughout</div>
<div class="doc-item"><strong>Testing</strong> Objects validated before merge</div>
<div class="doc-item"><strong>SDLC Practices</strong> Kanban, feature branches, selective PRs</div>
</div>
</details>

<div class="section-label">Key Things to Remember</div>

<ul class="takeaways">
<li><strong>Class hierarchies</strong> are easier to read at a glance than walls of comments — naming the relationship in code (<code>extends</code>) doubles as documentation.</li>
<li><strong>The game itself</strong> is the most honest documentation. If you want to know what a class actually does, run the code and watch it.</li>
<li><strong>Inline comments</strong> should explain <em>why</em> something is done a certain way, not <em>what</em> the code is literally doing.</li>
<li><strong>Naming</strong> does most of the heavy lifting — good variable and method names cut the number of comments you need by half.</li>
</ul>

</div>
