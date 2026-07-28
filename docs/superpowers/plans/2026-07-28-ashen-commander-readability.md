# Ashen Commander Readability & Fairness Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Produce `99Knights_ArcadeJourney_v0.7.7_BossReadability.html` from the accepted v0.7.6 standalone baseline with explicit Boss attack states, fair tracking locks, readable punish windows, a debug overlay, and a direct Ashen Commander test route.

**Architecture:** Keep the single-file HTML architecture. Add a compact Ashen Commander timing/config layer and authoritative `combatState` transitions around the existing Boss AI. Preserve existing attack definitions, damage helpers, generated sprite assets, journey flow, and Combat Feel feedback.

**Tech Stack:** HTML5 Canvas, vanilla JavaScript, embedded PNG/audio assets, Python static verification, Node.js JavaScript syntax validation, optional Playwright/Chromium smoke testing.

## Global Constraints

- Preserve v0.7.6 Combat Feel behaviour and the `J` toggle.
- Add no new attacks, phases, enemies, weapons, or external assets.
- Damage may occur only during `Active`.
- Tracking must lock before `Active` and remain locked through damage resolution.
- Lunge and Sweep must be distinguishable during `Anticipation`.
- Parry must create a stronger punish opportunity than ordinary avoidance.
- Debug overlay defaults OFF and does not affect gameplay.
- Normal progression remains unchanged; the direct Boss route is debug-only.

---

### Task 1: Add Verification Harness

**Files:**
- Create: `tools/verify_v077.py`
- Test target: `99Knights_ArcadeJourney_v0.7.7_BossReadability.html`

**Interfaces:**
- Consumes: complete standalone HTML text.
- Produces: process exit `0` only when required constants, states, key bindings, debug route, title/version and safety markers exist.

- [ ] **Step 1: Write the failing verifier**

Create a Python script that checks for the exact markers:

```python
REQUIRED = [
    'v0.7.7 Boss Readability',
    'const ASHEN_COMMANDER_COMBAT',
    'Idle', 'Anticipation', 'Active', 'Recovery',
    'Staggered', 'ExecutionVulnerable',
    'trackingLocked', 'damageActive',
    'function updateBossAttackState',
    'function drawBossDebugOverlay',
    'function startAshenCommanderDebugFight',
    'key === "b"', 'key === "g"',
]
```

Also reject any output that removes the existing `key === "j"` Combat Feel toggle.

- [ ] **Step 2: Run verifier and confirm failure**

Run:

```bash
python3 tools/verify_v077.py 99Knights_ArcadeJourney_v0.7.6_CombatFeelSystem.html
```

Expected: non-zero exit with missing v0.7.7 markers.

- [ ] **Step 3: Commit verifier**

```bash
git add tools/verify_v077.py
git commit -m "test: add v0.7.7 boss readability verifier"
```

### Task 2: Implement Explicit Boss State Machine and Tracking Lock

**Files:**
- Create from baseline: `99Knights_ArcadeJourney_v0.7.7_BossReadability.html`

**Interfaces:**
- Produces:
  - `ASHEN_COMMANDER_COMBAT` named timing constants.
  - `setBossCombatState(state, durationMs)`.
  - `updateBossAttackState(dt)`.
  - `trackBossAttackTarget(atk, dt)`.
  - Boss fields `combatState`, `stateTimer`, `trackingLocked`, `damageActive`, `vulnerable`.

- [ ] **Step 1: Add named constants**

Define Lunge, Sweep and Slam anticipation, tracking-lock, active and recovery durations plus capped anticipation turn speed. Phase 2 may scale anticipation/recovery but the lock lead must remain at least 180 ms.

- [ ] **Step 2: Initialise authoritative state fields**

Add state fields to `resetGame()` and make `startBossAttack()` enter `Anticipation` with a distinct state timer.

- [ ] **Step 3: Add bounded anticipation tracking**

During the early Anticipation interval, rotate `atk.angle` toward the player using `approachAngle` and the capped turn rate. Set `trackingLocked=true` once the remaining anticipation reaches the attack lock threshold.

- [ ] **Step 4: Split release from damage resolution**

Transition Anticipation → Active without immediately clearing the attack. Set `damageActive=true`, execute the attack exactly once within Active, then transition to Recovery and clear damage flags.

- [ ] **Step 5: Run verifier and Node syntax check**

```bash
python3 tools/verify_v077.py 99Knights_ArcadeJourney_v0.7.7_BossReadability.html
node --check /tmp/99knights-v077.js
```

Expected: verifier may still fail only for later debug/UI markers; JavaScript syntax passes.

### Task 3: Defensive Outcomes and Punish Windows

**Files:**
- Modify: `99Knights_ArcadeJourney_v0.7.7_BossReadability.html`

**Interfaces:**
- Consumes: existing `damagePlayer`, `addBossPosture`, `startBossRecovery`, `isBossVulnerable`.
- Produces: `startBossParryStagger()` and explicit `Staggered`/`ExecutionVulnerable` states.

- [ ] **Step 1: Make normal recovery explicit**

`startBossRecovery(type)` must enter `Recovery`, expose vulnerability for the existing per-attack window, and visibly clear vulnerability before returning to `Idle`.

- [ ] **Step 2: Strengthen Ashen Commander parry outcome**

On a successful parry against Ashen Commander during Active, cancel the active attack, prevent stale damage, enter a named stronger stagger interval, and preserve existing parry feedback/posture effects.

- [ ] **Step 3: Preserve dodge correctness**

Ensure each active attack resolves at most once and cannot apply a delayed hit after the player has already escaped or become invulnerable.

- [ ] **Step 4: Confirm no recovery cancel**

Boss AI must return early during Recovery/Staggered/ExecutionVulnerable, preventing immediate damaging attack cancellation.

### Task 4: Telegraph Presentation, Debug Overlay and Direct Test Route

**Files:**
- Modify: `99Knights_ArcadeJourney_v0.7.7_BossReadability.html`

**Interfaces:**
- Produces:
  - `drawBossDebugOverlay()` toggled by `B`.
  - `startAshenCommanderDebugFight()` triggered by `G` from title/boss-select screens.

- [ ] **Step 1: Differentiate anticipation presentation**

Use attack-specific sprite key/transform logic: Lunge shows a forward-set windup and narrow path; Sweep shows a rotational windup and wide arc. Keep character animation primary and ground cues restrained.

- [ ] **Step 2: Add debug overlay**

Display Boss state, current attack, remaining state time, tracking lock, damage active and vulnerability. Default `bossDebugEnabled=false`.

- [ ] **Step 3: Add direct Boss shortcut**

`G` starts the existing Golden Kingdom Ashen Commander encounter with no permanent progression mutation. The shortcut is ignored during active combat.

- [ ] **Step 4: Update version/title/help copy**

Change title and footer to v0.7.7 and document `B` and `G` only in a small development hint.

### Task 5: Verification, Packaging and GitHub Delivery

**Files:**
- Final: `99Knights_ArcadeJourney_v0.7.7_BossReadability.html`
- Final: `tools/verify_v077.py`
- Update: `docs/verification/v0.7.7-results.md`

**Interfaces:**
- Produces: shareable standalone HTML and source-backed verification record.

- [ ] **Step 1: Run static verifier**

```bash
python3 tools/verify_v077.py 99Knights_ArcadeJourney_v0.7.7_BossReadability.html
```

Expected: PASS.

- [ ] **Step 2: Extract and syntax-check JavaScript**

Extract the final inline script to `/tmp/99knights-v077.js`, then run:

```bash
node --check /tmp/99knights-v077.js
```

Expected: no output and exit `0`.

- [ ] **Step 3: Run available headless smoke test**

Load the HTML through a local HTTP server, capture console/page errors, trigger `G`, `B`, and `J`, and confirm Boss state progression reaches Anticipation, Active and Recovery. If browser automation is unavailable, record that limitation and complete deterministic static/runtime-JS checks instead.

- [ ] **Step 4: Write verification record**

Record exact commands, output, SHA-256, changed timing values, and any unresolved limitations.

- [ ] **Step 5: Commit and publish branch**

Commit the final HTML, verifier and results on `codex/ashen-commander-readability-v0.7.7`, then open a draft pull request to `main`.
