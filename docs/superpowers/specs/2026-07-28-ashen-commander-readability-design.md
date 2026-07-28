# 99 Knights v0.7.7 — Ashen Commander Readability & Fairness Design

## Goal

Make the Ashen Commander fight consistently readable and fair without adding attacks, phases, enemies, weapons, or unrelated systems. A player should be able to distinguish Lunge from Sweep during anticipation, understand when damage is active, evade with correct movement, and recognise punish windows.

## Scope

This pass modifies the standalone v0.7.6 HTML baseline only. It preserves the v0.7.6 Combat Feel system and the `J` toggle.

## State Model

The Ashen Commander uses authoritative gameplay states:

- `Idle`
- `Anticipation`
- `Active`
- `Recovery`
- `Staggered`
- `ExecutionVulnerable`

The existing `currentAttack`, recovery, stagger and execution data remain compatible, but a single `combatState` field becomes the readable source of truth for debug display and transition checks.

Each major attack follows:

1. Anticipation — tracking is allowed early and locks before release.
2. Active — damage exists only in this interval; facing no longer tracks the player.
3. Recovery — no damage; the Boss exposes a visible punish opportunity.

## Timing and Tracking

Attack timings are centralised under named Ashen Commander constants.

- Lunge: distinct anticipation, short active dash window, normal recovery.
- Sweep: distinct rotational anticipation, wider frontal arc, short active window, normal recovery.
- Slam retains existing behaviour but receives the same explicit state sequencing.
- Phase 2 may reduce anticipation and recovery using existing multipliers, but never removes the tracking-lock interval or collapses the active state to an unobservable instant.

During early anticipation, the Boss angle can track the player at a capped turn rate. Tracking locks before the Active state. Active attacks use the locked angle and cannot rotate toward the player.

## Defensive Outcomes

Existing block/parry/dodge mechanics remain intact.

- Dodge invulnerability prevents attack damage and must not be followed by a stale hit from an escaped active window.
- Parry uses the existing parry feedback and posture reward, and now forces a stronger explicit stagger/punish state for the Ashen Commander.
- Ordinary avoidance leads to normal recovery, weaker than the parry punish.

## Telegraphs and Visual Readability

No new art dependency is introduced.

- Lunge uses a narrow directional path and forward-lean presentation.
- Sweep uses a broad arc and rotational presentation.
- The existing generated Ashen Commander sprite states are reused, with state-specific transforms and restrained ground cues.
- Recovery and vulnerability remain yellow/gold and end visibly.

## Debug and Test Support

A separate debug toggle defaults OFF and shows:

- Boss state
- current attack
- state time remaining
- tracking locked
- damage active
- Boss vulnerable

A direct Ashen Commander test shortcut is added without changing normal progression. It starts the existing Golden Kingdom boss encounter for rapid manual checks.

## Validation

Required checks:

- JavaScript syntax passes.
- Static assertions confirm named states, timing constants, tracking lock, debug overlay and direct test route.
- Manual/headless smoke test confirms load, no console errors, `J` still toggles Combat Feel, debug toggle works, and Ashen Commander can enter Anticipation → Active → Recovery.
- Existing standalone title and normal journey flow remain available.

## Non-goals

- No new Boss attacks or phases.
- No stamina redesign.
- No broad combat rewrite.
- No new external assets.
- No unrelated UI or progression changes.
