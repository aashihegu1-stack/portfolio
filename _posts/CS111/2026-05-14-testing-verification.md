---
layout: post
title: Testing & Verification
description: Testing & Verification — CS 111 Review.
permalink: /cs111/testing
---

<style>
.oop-wrap { max-width: 900px; margin: 0 auto; }

.section-label { font-weight: bold; font-size: 1.4em; margin: 28px 0 8px 0; }
.section-sub { color: #888; font-size: 0.9em; margin-bottom: 12px; }

.game-btn-wrap { margin: 20px 0 30px 0; }
.game-btn {
    display: inline-flex; align-items: center; gap: 10px;
    padding: 12px 22px; border: 1px solid #FA8072; border-radius: 6px;
    color: #FA8072; font-weight: bold; text-decoration: none;
    transition: background 0.15s, color 0.15s;
}
.game-btn:hover { background: #FA8072; color: #14142b; text-decoration: none; }
.game-btn .arrow { font-family: monospace; }

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
    padding: 12px 14px; cursor: pointer; font-weight: bold; white-space: nowrap;
    font-size: 0.92em; opacity: 0.6; transition: opacity 0.15s;
    outline: none; -webkit-tap-highlight-color: transparent;
}
.tab-btn:hover { opacity: 1; }
.tab-btn:focus, .tab-btn:focus-visible { outline: none; }
.tab-btn.active { opacity: 1; color: #FA8072; border-bottom: 2px solid #FA8072; }
.tab-panel { display: none; padding: 18px; }
.tab-panel.active { display: block; }
.tab-panel h3 { margin-top: 0; }

.checklist-table { margin: 16px 0; }
.checklist-row {
    display: grid; grid-template-columns: 1fr 2fr 2fr; gap: 16px;
    padding: 10px 4px; border-bottom: 1px solid #333; align-items: center;
}
.checklist-row.head { font-weight: bold; color: #FA8072; border-bottom: 1px solid #FA8072; }

.ref-list { margin: 16px 0; }
.ref-row {
    display: grid; grid-template-columns: 1fr 2fr 1fr; gap: 16px;
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

<div class="section-label">Testing & Verification</div>

Testing and verification cover four layers of "proving the code works" — from comments that document intent, to live gameplay walkthroughs, to integration checks that hit real APIs, to error handling that keeps the game alive when something goes wrong. Each layer catches problems the others miss.

<div class="game-btn-wrap">
<a class="game-btn" href="https://moopa01.opencodingsociety.com/testing" target="_blank" rel="noopener">
🧪 View Testing Source <span class="arrow">→</span>
</a>
</div>

<div class="section-label">Verification Layers</div>
<div class="section-sub">Click any layer to see what it covers.</div>

<div class="hier-tree">
    <div class="hier-node" data-node="Verify" data-parents="">Verify</div>
    <div class="hier-line" data-line="top-mid"></div>
    <div class="hier-node" data-node="Testing" data-parents="Verify">Testing</div>
    <div class="hier-row" data-row="bottom">
        <div class="hier-node" data-node="JSDoc" data-parents="Verify,Testing">JSDoc</div>
        <div class="hier-node" data-node="Gameplay" data-parents="Verify,Testing">Gameplay</div>
        <div class="hier-node" data-node="Integration" data-parents="Verify,Testing">Integration</div>
        <div class="hier-node" data-node="Errors" data-parents="Verify,Testing">Error Handling</div>
    </div>
</div>

<div class="hier-info" id="hier-info">
<p class="hint">Pick a layer above to see what it covers.</p>
</div>

<div class="section-label">The Four Layers</div>

<ol class="concept-list">
<li><strong>Code Documentation (JSDoc).</strong> Solid documentation means anyone — including future-you — can read the code six months later without guessing. The engine uses JSDoc-style comments on every class and method, with <code>@param</code>, <code>@returns</code>, and <code>@property</code> tags. Target: at least 1 line of comments per 10 lines of code.</li>

<li><strong>Gameplay Testing.</strong> Manual playthroughs catch the bugs no unit test can find. Walk through each level and check movement, jump physics, coin pickups, enemy collisions, level transitions, and screen boundaries. If it feels wrong while playing, it is wrong.</li>

<li><strong>API Integration Testing.</strong> Once an API endpoint is wired up, integration tests confirm the whole path works — request goes out, data actually persists, and the next read returns it. For the leaderboard, that means POSTing a score then GETting the list back to verify it saved.</li>

<li><strong>API Error Handling.</strong> Every <code>fetch</code> needs a <code>try/catch</code> and an <code>!response.ok</code> check. The try/catch handles network failures (CORS, server down), the response.ok check handles HTTP errors (404, 500). Without both, a single bad request can crash the game.</li>
</ol>

<div class="section-label">The Four Layers — Tabbed View</div>
<div class="section-sub">Click a layer to switch tabs.</div>

<div class="tabs">
<div class="tab-bar">
    <button class="tab-btn active" data-tab="docs">JSDoc</button>
    <button class="tab-btn" data-tab="play">Gameplay</button>
    <button class="tab-btn" data-tab="api">Integration</button>
    <button class="tab-btn" data-tab="err">Error Handling</button>
</div>

<div class="tab-panel active" data-panel="docs">
<h3>JSDoc — Documentation as Verification</h3>
<p>JSDoc comments describe what a class or method is supposed to do — and a reader can verify the implementation against the description. From a typical class:</p>

```javascript
/**
 * ScoreTracker manages player score and high score for a game session.
 *
 * @property {number} score      - Current session score.
 * @property {number} highScore  - All-time high score.
 * @property {string} playerName - The player's display name.
 */
class ScoreTracker {
    /**
     * @param {string} playerName - Display name shown on leaderboard.
     */
    constructor(playerName) {
        this.playerName = playerName;
        this.score      = 0;
        this.highScore  = 0;
    }

    /**
     * Adds points to the current score. Updates high score if beaten.
     * @param {number} points - Points to add (must be positive).
     * @returns {number} The updated score.
     */
    addPoints(points) {
        if (points > 0) this.score += points;
        if (this.score > this.highScore) this.highScore = this.score;
        return this.score;
    }
}
```

<p>Rule of thumb: comment density above 10% — at least one comment line for every ten lines of code.</p>
</div>

<div class="tab-panel" data-panel="play">
<h3>Gameplay Testing — Manual Verification</h3>
<p>The gameplay checklist used to test each level:</p>

<div class="checklist-table">
<div class="checklist-row head">
<div>Test</div><div>What to verify</div><div>Pass criteria</div>
</div>
<div class="checklist-row">
<div>Player movement</div><div>W/A/S/D and arrow keys</div><div>Moves in correct direction, stops at boundary</div>
</div>
<div class="checklist-row">
<div>Jump physics</div><div>Press W with gravity on</div><div>Rises then falls naturally</div>
</div>
<div class="checklist-row">
<div>Coin collision</div><div>Walk into a coin</div><div>Coin disappears, score goes up</div>
</div>
<div class="checklist-row">
<div>Enemy collision</div><div>Shark touches player</div><div>Explosion plays, level restarts</div>
</div>
<div class="checklist-row">
<div>Level completion</div><div>Reach end platform</div><div>Transitions to next level</div>
</div>
<div class="checklist-row">
<div>Boundary check</div><div>Move to canvas edge</div><div>Player can't leave the screen</div>
</div>
</div>

<p>The collision handler being verified — from <code>Shark.js</code>:</p>

```javascript
handleCollisionEvent() {
    var player = this.gameEnv.gameObjects.find(obj => obj instanceof Player);
    this.velocity.x = 0;
    this.velocity.y = 0;
    this.explode(player.position.x, player.position.y);
    player.destroy();
    this.playerDestroyed = true;
    setTimeout(() => {
        this.gameEnv.gameControl.currentLevel.restart = true;
    }, 2000);  // check: does the 2-second pause feel right?
}
```
</div>

<div class="tab-panel" data-panel="api">
<h3>API Integration Testing — End-to-End</h3>
<p>After wiring up the Leaderboard API, this test confirms a score actually round-trips through the server:</p>

```javascript
async function testLeaderboardIntegration() {
    const testPayload = { playerName: 'TestUser', score: 9999 };

    // Step 1: POST score
    const postRes = await fetch(`${javaURI}/api/scores`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        credentials: 'include',
        body: JSON.stringify(testPayload)
    });
    console.log('POST status:', postRes.status);  // expect 200 or 201

    // Step 2: GET leaderboard and look for the test entry
    const getRes  = await fetch(`${javaURI}/api/scores`, { credentials: 'include' });
    const scores  = await getRes.json();
    const found   = scores.find(s => s.playerName === 'TestUser' && s.score === 9999);
    console.log('Score saved correctly:', !!found);  // expect true
}
```

<p>Integration tests prove the connection works — not just that one endpoint runs in isolation.</p>
</div>

<div class="tab-panel" data-panel="err">
<h3>Error Handling — Surviving Failures</h3>
<p>Every <code>fetch</code> needs to cover both kinds of failure. From <code>login.js</code>:</p>

```javascript
fetch(options.URL, requestOptions)
    .then(response => {
        if (!response.ok) {                          // HTTP errors (4xx, 5xx)
            const errorMsg = 'Login error: ' + response.status;
            console.log(errorMsg);
            document.getElementById(options.message).textContent = errorMsg;
            return;                                  // exit early
        }
        options.callback();                          // success path
    })
    .catch(error => {                                // network errors (CORS, server down)
        console.log('Possible CORS or Service Down error: ' + error);
        document.getElementById(options.message).textContent =
            'Possible CORS or service down error: ' + error;
    });
```

<p>A reusable async wrapper that handles both branches at once:</p>

```javascript
async function fetchWithErrorHandling(url, label) {
    try {
        const response = await fetch(url);
        if (!response.ok) {
            throw new Error(`HTTP ${response.status}: ${response.statusText}`);
        }
        const data = await response.json();
        console.log(`[${label}] SUCCESS — got data:`, Object.keys(data));
        return data;
    } catch (error) {
        // Catches both network failures AND thrown HTTP errors
        console.error(`[${label}] ERROR:`, error.message);
        return null;
    }
}
```
</div>
</div>

<div class="section-label">Quick Reference</div>

<div class="ref-list">
<div class="ref-row head">
<div>Area</div><div>What to do</div><div>Tool</div>
</div>
<div class="ref-row">
<div>Documentation</div><div>JSDoc <code>/** */</code> on every class and method; > 10% comment density</div><div>Code review</div>
</div>
<div class="ref-row">
<div>Gameplay testing</div><div>Play through each level; check collisions, movement, transitions</div><div>Live demo</div>
</div>
<div class="ref-row">
<div>Integration testing</div><div>POST score → GET leaderboard; confirm persistence</div><div>DevTools Network tab</div>
</div>
<div class="ref-row">
<div>Error handling</div><div><code>try/catch</code> + <code>!response.ok</code> on every fetch</div><div>Code review</div>
</div>
</div>

<div class="section-label">Key Things to Remember</div>

<ul class="takeaways">
<li><strong>JSDoc is more than comments</strong> — typed params and return values become hints in your IDE, so you catch bugs while typing.</li>
<li><strong>Manual playthroughs catch the bugs unit tests miss</strong> — feel, timing, "does this hit register?" — those are human judgments.</li>
<li><strong>Integration tests verify the full path</strong>. If the POST works but the GET doesn't return the data, the test still fails. That's the point.</li>
<li><strong>Error handling needs both branches</strong> — <code>try/catch</code> covers network failures, <code>!response.ok</code> covers HTTP errors. Drop either and the next bad response crashes the game.</li>
</ul>

</div>

<script>
(function() {
    const nodeInfo = {
        Verify: { title: "Verify", blurb: "Proving the code does what it's supposed to — at every layer of the stack.", props: ["+four layers", "+catch what others miss"] },
        Testing: { title: "Testing", blurb: "The tools and techniques used to prove correctness, catch bugs, and document behavior.", props: ["+manual + automated"] },
        JSDoc: { title: "JSDoc Documentation", blurb: "Structured comments that describe what classes and methods are supposed to do.", props: ["+@param", "+@returns", "+@property", "+> 10% density"] },
        Gameplay: { title: "Gameplay Testing", blurb: "Manual playthroughs to verify movement, collisions, and transitions feel right.", props: ["+test checklist", "+live demo"] },
        Integration: { title: "API Integration Testing", blurb: "End-to-end checks that confirm requests reach the server and data actually persists.", props: ["+POST → GET", "+verify state"] },
        Errors: { title: "API Error Handling", blurb: "try/catch plus response.ok checks so failures don't crash the game.", props: ["+try/catch", "+!response.ok"] }
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
            if (name !== 'Verify') {
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
