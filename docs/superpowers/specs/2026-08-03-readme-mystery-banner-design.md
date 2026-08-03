# README Mystery Banner Design

## Goal

Replace the current simple SVG banner with a polished, cinematic README hero image while preserving the game's mystery and avoiding major story spoilers.

## Creative Direction

The banner presents 99Knights as a fantasy delivery action roguelite with an unexplained emergency protocol. It should make visitors curious about why an ordinary delivery route has become a kingdom-level operation, without revealing the relationship between the three orders or the final family outcome.

## Composition

- Wide cinematic image suitable for a GitHub README.
- The courier is the main focal point, seen from a three-quarter rear or side angle.
- His red delivery case is visible but not shown together with identifiable food items.
- A glowing route leads toward a distant fortified district or castle.
- Three boss-like silhouettes appear in separate parts of the environment, partially obscured by mist, light, architecture, or distance.
- A Royal Express warning interface may appear as abstract red and gold symbols or an `ERROR` state.
- The visual style should match the bright fantasy map and illustrated cutscene style already used in the game, not dark gothic concept art.

## Spoiler Rules

The banner and README must not reveal:

- that all three orders belong to one family;
- the identities of the father, mother, or child;
- the family dinner ending;
- the true reason behind the Royal Express Protocol error;
- the exact contents of all three deliveries;
- the reconciliation outcomes of the bosses;
- the number or nature of the endings.

## Banner Copy

Primary line:

`THREE ORDERS. ONE IMPOSSIBLE ROUTE.`

Chinese line:

`三个订单，一条不该存在的路线。`

The banner should not include a long synopsis.

## README Copy Direction

### Tagline

Use a mystery-led tagline instead of the current family reveal:

> Three orders. One impossible route.
>
> 三个订单，一条不该存在的路线。

### About

Describe only the inciting incident:

> An ordinary courier accepts three routine deliveries. Before the first order is complete, the Royal Express Protocol declares him a kingdom-level threat.

Do not explain why the protocol is wrong.

### Story

Use a short question-led setup:

> Three deliveries. Three guarded districts. Three commanders standing in the way.
>
> Why has an ordinary delivery route triggered the kingdom's highest emergency protocol?

### Highlights

Keep gameplay features, but remove or generalize story spoilers:

- Keep the 27-room campaign.
- Keep three boss encounters.
- Keep parry, posture, dodge, and execution combat.
- Keep Chinese and bilingual dialogue modes.
- Change `Six illustrated story scenes from protocol failure to family dinner` to `Six illustrated story scenes`.
- Keep campfire upgrades.
- Change `multiple warm endings` to `multiple endings`.

### Current Release

Remove `four family-centered endings` and replace it with `multiple endings shaped by player choices`.

## Files

- Replace: `docs/99knights-banner.svg`
- Create: `docs/99knights-banner.png`
- Modify: `README.md`

README will reference the PNG instead of the SVG.

## Output Requirements

- Target banner size: 1600 × 700 pixels.
- PNG format for reliable GitHub rendering.
- No external image hosting.
- No UI controls embedded in the banner.
- Text must remain readable when README is viewed on desktop and mobile.
- Final README must retain the direct Play in Browser link.

## Acceptance Criteria

- The banner looks like a finished game key visual, not a temporary diagram or flat SVG illustration.
- A new visitor can identify the game as a fantasy delivery action game within five seconds.
- The three-order mystery is established without revealing the family connection or ending.
- README contains no explicit family, meal-content, system-cause, or ending spoilers.
- All image and README links render from the repository itself.
