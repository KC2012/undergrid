# UNDERGRID

**Version 1.40.8 — Rules Integrity & Tactical AI / Deployment Candidate**  
A turn-based, side-view tactical skirmish game about positioning, vertical combat, weapons, and the consequences of a bad move.

**Published site:** https://undergrid.unaffiliated.page/ (may still run the previous build until this package is deployed)  
**Format:** Standalone HTML5 browser game  
**Recommended:** Desktop browser or iPad in landscape orientation

---

## The game

UNDERGRID is a tactical firefight played across layered industrial battlefields. Command a four-fighter crew through platforms, ladders, exposed crossings, cover, and hazardous machinery. Fighters take alternating activations and spend action points to move, climb, jump, shoot, reload, fight in melee, throw grenades, or use battlefield interactions. Position and line of sight matter: a good firing lane can be decisive, but a fighter caught in the wrong place may be exposed from several elevations.

Play a disposable Quick Battle or develop a persistent crew through the campaign's territory, equipment, and rival systems. Different mission objectives and battlefield layouts reward different approaches.

## Play modes and objectives

- **Campaign:** Build and equip a persistent crew, fight for territory, manage the armory, and follow the progress of rival crews. Campaign state is saved locally in the browser.
- **Quick Battle:** Jump into a disposable fight without changing your persistent campaign. Includes human-versus-CPU play and selectable battle setups.
- **AUTO:** Let the computer handle tactical activations, including for observation and testing.
- **Elimination:** Defeat the opposing crew.
- **Relay Control:** Contest and hold the marked objective to accumulate control points.
- **Salvage Run:** Recover battlefield caches and bring them to your team's extraction area.

Available setups and controls may differ by mode.

## Core tactical systems

### Alternating activations and action points
Each fighter has limited action points per activation. Choose when to reposition, take a shot, reload, climb, or commit to a costly attack. Weapon profiles, fighter characteristics, range, armor, and the battlefield all affect the result.

### Vertical movement and real line of sight
The side-view battlefield is part of the combat system. Ladders, jumps, platforms, and cover determine which positions can be reached and which shots are possible. Fire is resolved using actual shot geometry rather than simply checking whether two fighters are nearby.

**New in 1.40.7: ladder-top firing apertures.** The *top landing* of a ladder can have a small shoot-through opening. Fighters above and below can fire through it when the actual shot ray passes through the opening. A ladder running behind or past another floor does **not** make that floor transparent. The aperture is visually distinguished from solid flooring, and climb destinations indicate which ladder endpoints are usable and whether the fighter is close enough to approach.

### Weapons, injuries, and equipment
Use firearms with distinct ranges and firing behavior, close-combat weapons, grenades, armor, and other equipment. The persistent armory supports crew loadouts and progression. Combat includes knockback and other weapon- and status-specific effects.

### Battlefields and mechanisms
The full battlefield release brings **14 live battlefield families** into the game, including large vertical spaces and distinctive industrial layouts. Battlefield mechanisms and objective placement are tied to the generated environment. The same battlefield grammar is used by live play and development validation.

## Controls

### Mouse and keyboard
Use the on-screen action toolbar to select **MOVE, CLIMB, JUMP, SHOOT, RELOAD, MELEE, GRENADE**, and other actions when available. Click a highlighted legal destination or target to execute the selected action. The **END** button finishes the current activation.

Keyboard shortcuts in battle:

| Key | Action |
| --- | --- |
| `1` | Move |
| `2` | Climb |
| `3` | Jump |
| `4` | Shoot |
| `5` | Grenade |
| `6` | Melee |
| `R` | Reload |
| `Enter` | End activation |
| `A` | Toggle AUTO |
| `Home` | Reset tactical view |
| `H` | Show/hide lower HUD |

On-screen controls remain available if you prefer not to use shortcuts. Some commands are disabled when the active fighter lacks the action points, equipment, or legal target needed.

### iPad and touch controls
**Landscape orientation is recommended.** The 1.40.7 release supports a responsive tactical view designed for tablet play:

- Tap action buttons and legal targets or destinations.
- Drag empty battlefield space with one finger to pan the tactical camera.
- Pinch with two fingers to zoom.
- Long-press to preview battlefield information.
- Use **VIEW** to reset/fit the camera and **HUD** to hide or restore the lower information panels.

The action toolbar and view controls reflow at intermediate screen widths rather than overlapping. Portrait tablet orientation displays a landscape recommendation.

## What's new in v1.40.7

This release combines the full battlefield candidate with the iPad/touch interface and a targeted stability pass.

- **Tablet tactical view:** Touch pan, pinch zoom, long-press preview, landscape layout, safe-area handling, and a collapsible lower HUD.
- **Mid-width toolbar fix:** View and utility controls move away from the action toolbar when the screen is too narrow for a single row.
- **Ladder-top firing lanes:** A narrow line-of-sight opening at the *top* of connected ladders, without opening unrelated or intermediate floors.
- **Ladder readability:** Visible ladder landing treatment and clearer distinction between reachable endpoints and destinations that require moving closer.
- **Deployment render protection:** Guards against invisible fighter miniatures and checks fighter visibility when deployment completes; the release fixes the active-game reference used by the visibility audit.
- **Public Release Audit:** A development-lab check that brings together core stability, battlefield generation, mechanisms, ladder/LOS geometry, deployment visibility, responsive view, and key interface checks.
- **Release seal:** No intentional changes to weapon balance, campaign economy, or progression as part of this final stability pass.

## v1.40.7a — Live render hotfix

The original public tablet build had a reproducible empty-battlefield failure on some Sewer Warren maps. The game correctly deployed all eight fighters, but the decorative SLUDGE platform renderer could calculate a negative bubble radius on platforms extending into negative world coordinates. The browser then stopped drawing the frame before it reached the fighter miniatures.

This hotfix uses platform-local bubble indices (always nonnegative), protects canvas state when platform decoration fails, and allows the main renderer to fall back to a plain platform rather than lose the entire battlefield. The deployment audit now verifies that a frame reached and completed the fighter-rendering stage in addition to checking fighter positions. The public build label is also corrected. No combat, ladder geometry, campaign, or save-data rules changed.

**Reproduction:** Quick Battle, Sewer Warren // Pipe Junction, seed `654236803`. The original build displayed no fighters; v1.40.7a renders all eight.

## v1.40.7b — Fall trajectory and branding footer

A left-edge knockback bug could select the **opposite (right) edge** of a platform when a fighter was pushed just inside its left boundary. The fall resolver then treated the fighter as falling at that distant location, making the miniature appear to teleport across the battlefield. The bug was reproduced in v1.40.7a and corrected in this build.

- **Correct ledge direction:** A fighter knocked off the left or right edge now departs from that actual edge.
- **Vertical landing:** Falls search downward from the real departure X. A landing may catch a fighter within a small body-width edge graze; it cannot pull a fighter horizontally across a large gap. A fall without a supporting deck continues into the void.
- **Displacement animation:** Grenades, launchers, melee exchanges, AI shots, and direct AI overwatch damage animate knocked fighters rather than instantly displaying their final coordinates. Human projectile hits retain their existing arrival-timed presentation.
- **Permanent miniature footer:** A low-profile, theme-aware Unaffiliated strip is visible at the bottom of menus and gameplay, including collapsed HUD and iPad layouts. `UNAFFILIATED.PAGE` links to the creative site on the left; `UNDERGRID // v1.40.7b` appears on the right. The footer has its own layout row rather than covering controls.
- **Release diagnostics:** The developer Public Release Audit includes a left/right ledge regression and footer check. Debug exports identify the current public build.

**Verification:** Reproduced the old opposite-edge error in v1.40.7a; all six targeted fall cases passed in v1.40.7b. 61 browser-rendered battlefields passed across all 14 families and desktop/tablet viewports; the previous platform-art recovery also passed fault injection. Five desktop/tablet/phone layouts passed footer visibility, no-overlap and collapsed-HUD checks. All 109 JavaScript blocks passed syntax validation.

**Known limitation:** In a separate 300-match headless AUTO stress sample, 285 battles finished and 15 reached the activation limit. The same sample on v1.40.7a finished 287 with 13 stalls; most stalled seeds are shared. AUTO navigation can still repeat movement patterns on some maps. This patch does not attempt an AI overhaul. No large horizontal landing snaps were observed in the 376 recorded falls in the new sample.

## v1.40.7c — Footer viewport fix

The v1.40.7b footer had its own layout row during combat, but Crew Loadout, Territory Network, and other full-screen overlays still measured themselves against the entire viewport. Their panels could extend behind the footer, particularly at desktop/iPad landscape heights and short desktop windows.

- **Reserved footer space everywhere:** Every full-screen screen and developer overlay now ends above the permanent Unaffiliated footer. Crew Loadout, Territory Network, Armory, Supply, dossiers, and auxiliary screens use the same remaining visual viewport.
- **Responsive panel heights:** Tall panels shrink to the available space. On short or narrow screens, existing scrolling remains available instead of hiding buttons or content behind the footer.
- **Consistent branding:** The footer remains the same low-profile, theme-aware 18px strip, with `UNAFFILIATED.PAGE` on the left and `UNDERGRID // v1.40.7c` on the right.
- **Diagnostics:** The Public Release Audit now includes a footer/overlay clearance check. This is a presentation-only update; combat, campaign, save format, fall physics, and weapon balance are unchanged.

**Verification:** 96 overlay/layout cases across eight desktop, iPad, tablet, portrait, and phone viewports passed, including the screenshot-size desktop layout and a short-height window. Real Crew → Territory → Crew → Quick Battle navigation passed on desktop and an iPad-sized touch viewport, with 16 territory nodes, eight visible fighters, passing fall and public audits, and no browser page errors. All 110 JavaScript blocks passed syntax validation. Existing AUTO navigation limitations noted in v1.40.7b remain unchanged.

## v1.40.7d — Shock activation and manual fighter selection

The normal activation system correctly removed 1 AP when SHOCK triggered, but manually selecting a different unacted fighter bypassed the activation-start status processor and reset their AP to 2. Switching away from a previously shocked fighter could also restore AP when the regular turn order selected them again later in the round.

- **One canonical activation path:** Selecting an unacted fighter now uses the same start-of-activation lifecycle as normal turn progression and AI. Pending SHOCK, BURN, TOXIN, campaign start skills, and battlefield environmental effects run on the selected fighter.
- **Exactly once per round:** A fighter prepared earlier in the round retains their remaining AP and does not repeat status damage or environmental AP loss when selected again. A shocked fighter may switch before taking an action without restoring their lost AP.
- **Combat diagnostic:** In desktop developer tools, `UNDERGRID_SHOCK_AUDIT.inspect()` returns current fighter AP/status and the latest ACTIVATE, SELECT, STATUS_APPLIED, STATUS_TICK, environmental shock, skill-trigger, and END events without modifying the match.
- **Rule clarification:** SHOCK removes 1 AP at the fighter's next activation. Shock weapon hits apply it on a 55% roll after damage; Shock Grenades apply it to fighters caught in the burst. The FOLLOW THROUGH skill can legitimately refund 1 AP after a melee takedown, and Overwatch can fire later as a reaction.

**Verification:** Reproduced the manual-selection bypass on v1.40.7c, then passed 14 targeted browser checks covering direct/selected/AI shock, grenade application, repeated selection, later-round-order resumption, reactor hazards, campaign activation skills, and the non-mutating diagnostic. Desktop and iPad Quick Battle navigation passed with eight rendered fighters, fall and public audits, and zero page errors on the fixed regression seed `654236803`. All 111 JavaScript blocks passed syntax validation. The existing 96-case footer/overlay layout suite passed in the prior v1.40.7c release; the v1.40.7d change does not modify CSS.

## v1.40.8 — Rules integrity, tactical relay AI and crane redesign

This build addresses the additional combat-rule bugs found during the 1.40.7d review and the reported relay AI and Scrap Yard crane problems. It preserves the responsive Unaffiliated footer, ladder firing apertures, fall trajectory fixes, and existing browser-local campaign save format.

### Combat rules

- **Prepared-fighter status timing:** If an unacted fighter is selected, switched away from, then receives SHOCK, BURN or TOXIN, the newly inflicted effect processes when that fighter resumes. Existing BURN/TOXIN ticks are not repeated simply because the fighter was reselected. SHOCK still removes 1 AP, then clears.
- **FOLLOW THROUGH:** The once-per-activation AP refund cannot be reset by switching fighters. An attack that refunded AP still counts as a committed action, so it cannot be used to bypass the selection restriction.
- **SUPPRESSION:** A fighter suppressed during an activation retains the penalty until the end of their *next* activation, rather than immediately clearing when the current one ends. Suppression received before activation clears after that activation. RALLY can still clear it earlier.
- **Radial knockback:** Frag grenades, launcher impacts and explosive splash push fighters away from the actual blast center, not the attacker's location. Damage attribution remains with the attacker.
- **Kill credit:** Self-inflicted and friendly takedowns do not increment the attacking fighter's kill count or grant FOLLOW THROUGH. The actual damage/down event is still recorded.
- **Combat feedback:** Pending status application and actual activation ticks are formatted separately, without undefined labels. The non-mutating `UNDERGRID_RULES_1408.inspect()` and `UNDERGRID_SHOCK_AUDIT.inspect()` diagnostics expose AP, statuses, skills, and recent tactical decisions.

### Enemy tactics and level design

- **Relay Control:** When a nearby enemy presents an immediate danger or occupies the objective, the AI can take a viable shot before rushing the relay. It also evaluates likely incoming fire at prospective positions, seeks different capture positions rather than piling onto the same point, and can still commit to an immediate winning capture.
- **Elimination:** When an enemy on the same platform cannot be shot, the AI can seek a better firing angle rather than repeatedly waiting. Objective-carrier behavior in Salvage Run remains separate from this fallback to avoid disrupting extraction routes.
- **Dual salvage cranes:** The two cranes now land on *separate* upper platforms, divided by a solid suspended machinery mast that blocks direct fire and top-deck jumps. Each landing connects to its own gantry, with a connected lower underpass for flanking. The mast is drawn in combat, the Territory schematic and the Level Lab preview.
- **Combat coordinates:** Engagement and charge distance use the game's actual battlefield width, rather than depending on the current UI canvas size. This also keeps headless AUTO tests faithful to normal play.

### Verification

- **14/14 targeted browser tests** passed, including re-applied SHOCK, fresh versus existing BURN/TOXIN, suppression, FOLLOW THROUGH, real self-frag kill credit, grenade knockback, crane topology, hard mast LOS and the underpass route.
- **Relay-specific tests** confirmed threat-first shooting and dispersal from a crowded capture position.
- **120/120 crane layouts** generated successfully across six Level Lab presets; both crane landings remained distinct and valid.
- **500/500 headless AUTO battles** completed in one 650-activation-per-match stress batch across all 14 battlefield families and all three mission types. The diagnostic still recorded 34 prevented AI oscillation patterns and 17 repeated-pattern warnings: this is a stress-test result, not proof that all navigation edge cases are gone.
- **96/96 overlay/layout checks** passed at eight viewport sizes, with eight rendered fighters and no page errors. Desktop and iPad Crew → Territory → Quick Battle flows passed their built-in public and fall audits. **112 inline JavaScript blocks** passed syntax validation.

**Deployment status:** This package is prepared locally and has not been pushed to the production site. Use the deployment instructions below and keep the same site origin to preserve browser-local campaign data.

## Running locally

There is no build step or dependency installation. Download `index.html` and open it in a modern browser. The release is a self-contained HTML file; a local web server is optional for ordinary play. For the published version, deploy the same file as your site's root `index.html`.

## Deployment

The existing site is deployed through a GitHub-to-Vercel workflow:

1. Back up the currently published `index.html` and keep the previous release available for rollback.
2. Replace the repository's existing `index.html` with the v1.40.8 file.
3. Commit and push to the branch used by the production Vercel project.
4. Wait for the Vercel deployment to complete, then open the live URL and hard-refresh if necessary.
5. Smoke-test a Quick Battle on desktop and an iPad in landscape orientation. Check fighter visibility, touch pan/pinch, HUD toggle, toolbar layout, climb endpoints, and shooting through a top ladder aperture.
6. Open the existing campaign on the **same site origin** and verify that saved progress is still available.

**Save-data caution:** Campaign progress uses browser-local storage. Different browsers, private browsing, clearing site data, or moving the game to a different domain may make an existing save unavailable. Preserve the current production domain and avoid clearing browser storage during the update.

## Release checks

The 1.40.8 release includes a developer-facing **Public Release Audit**. It combines existing checks for core stability, all live battlefield families, battlefield mechanisms, ladder/LOS cases, fighter deployment visibility **and completed-frame health**, responsive canvas layout, fall trajectory, branding footer, overlay/footer clearance, shock/AP and rules/tactical diagnostics, and required UI elements. Some live-battle checks are deferred until a battle is active. The audit is a regression aid, not a substitute for a real iPad/browser smoke test after deployment.

To access development controls, use `Ctrl` + `Shift` + `D` in the desktop browser. Development and experimental level-lab controls are not part of the normal player flow.

## Troubleshooting

**A fighter appears to teleport when knocked off a ledge:** Check the header for **1.40.8**. If it still happens, export the debug JSON with the battle seed and the `LEDGE`/`FALL` action records. These now include departure side, departure X, landing X, and the horizontal landing correction in pixels.


**Fighters do not appear after deployment:** Confirm the page header says **1.40.8**, then try **VIEW** to refit the battlefield. If the problem persists, export the in-game debug JSON and include the seed. The export now records completed-frame health and any recovered platform-rendering errors.

**A ladder is visible but CLIMB will not use it:** Only connected ladder endpoints are climb destinations. Some highlighted endpoints are too far away for the current free approach; move closer before climbing. A ladder merely passing behind a platform does not necessarily connect to that platform.

**A shot cannot pass through a ladder:** Only the opening at a ladder's top landing is projectile-permeable. The actual shot line must intersect the opening; proximity to a ladder does not grant permission to shoot through an otherwise solid floor.

**Tablet controls are crowded:** Rotate to landscape, try VIEW to refit the battlefield, and use HUD to temporarily hide the lower panels.

**A campaign save seems missing:** Confirm that you are using the original site address and the same browser/profile, with local site data intact.

## Project and release notes

UNDERGRID is part of **Unaffiliated**, the home for experimental games and creative projects. Version 1.40.8 is the current prepared release candidate, building on the 1.40.7a rendering fix, 1.40.7b fall-trajectory fix and 1.40.7d shock activation fix. This pass strengthens combat-rule consistency, relay tactics and the dual-crane battlefield while preserving tablet and desktop controls.

**Version:** 1.40.8  
**Release:** Rules Integrity & Tactical AI / Deployment Candidate  
**Site:** https://undergrid.unaffiliated.page/
