# UNDERGRID

**Version 1.40.7c — Public Tablet Release / Footer Viewport Fix**  
A turn-based, side-view tactical skirmish game about positioning, vertical combat, weapons, and the consequences of a bad move.

**Play:** https://undergrid.unaffiliated.page/  
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

## v1.40.7c — Footer viewport fix

The v1.40.7b footer had its own layout row during combat, but Crew Loadout, Territory Network, and other full-screen overlays still measured themselves against the entire viewport. Their panels could extend behind the footer, particularly at desktop/iPad landscape heights and short desktop windows.

- **Reserved footer space everywhere:** Every full-screen screen and developer overlay now ends above the permanent Unaffiliated footer. Crew Loadout, Territory Network, Armory, Supply, dossiers, and auxiliary screens use the same remaining visual viewport.
- **Responsive panel heights:** Tall panels shrink to the available space. On short or narrow screens, existing scrolling remains available instead of hiding buttons or content behind the footer.
- **Consistent branding:** The footer remains the same low-profile, theme-aware 18px strip, with `UNAFFILIATED.PAGE` on the left and `UNDERGRID // v1.40.7c` on the right.
- **Diagnostics:** The Public Release Audit now includes a footer/overlay clearance check. This is a presentation-only update; combat, campaign, save format, fall physics, and weapon balance are unchanged.

**Verification:** 96 overlay/layout cases across eight desktop, iPad, tablet, portrait, and phone viewports passed, including the screenshot-size desktop layout and a short-height window. Real Crew → Territory → Crew → Quick Battle navigation passed on desktop and an iPad-sized touch viewport, with 16 territory nodes, eight visible fighters, passing fall and public audits, and no browser page errors. All 110 JavaScript blocks passed syntax validation. Existing AUTO navigation limitations noted in v1.40.7b remain unchanged.

## Running locally

There is no build step or dependency installation. Download `index.html` and open it in a modern browser. The release is a self-contained HTML file; a local web server is optional for ordinary play. For the published version, deploy the same file as your site's root `index.html`.

## Deployment

The existing site is deployed through a GitHub-to-Vercel workflow:

1. Back up the currently published `index.html` and keep the previous release available for rollback.
2. Replace the repository's existing `index.html` with the v1.40.7c file.
3. Commit and push to the branch used by the production Vercel project.
4. Wait for the Vercel deployment to complete, then open the live URL and hard-refresh if necessary.
5. Smoke-test a Quick Battle on desktop and an iPad in landscape orientation. Check fighter visibility, touch pan/pinch, HUD toggle, toolbar layout, climb endpoints, and shooting through a top ladder aperture.
6. Open the existing campaign on the **same site origin** and verify that saved progress is still available.

**Save-data caution:** Campaign progress uses browser-local storage. Different browsers, private browsing, clearing site data, or moving the game to a different domain may make an existing save unavailable. Preserve the current production domain and avoid clearing browser storage during the update.

## Release checks

The 1.40.7c release includes a developer-facing **Public Release Audit**. It combines existing checks for core stability, all live battlefield families, battlefield mechanisms, ladder/LOS cases, fighter deployment visibility **and completed-frame health**, responsive canvas layout, fall trajectory, branding footer, overlay/footer clearance, and required UI elements. Some live-battle checks are deferred until a battle is active. The audit is a regression aid, not a substitute for a real iPad/browser smoke test after deployment.

To access development controls, use `Ctrl` + `Shift` + `D` in the desktop browser. Development and experimental level-lab controls are not part of the normal player flow.

## Troubleshooting

**A fighter appears to teleport when knocked off a ledge:** Check the header for **1.40.7c**. If it still happens, export the debug JSON with the battle seed and the `LEDGE`/`FALL` action records. These now include departure side, departure X, landing X, and the horizontal landing correction in pixels.


**Fighters do not appear after deployment:** Confirm the page header says **1.40.7c**, then try **VIEW** to refit the battlefield. If the problem persists, export the in-game debug JSON and include the seed. The export now records completed-frame health and any recovered platform-rendering errors.

**A ladder is visible but CLIMB will not use it:** Only connected ladder endpoints are climb destinations. Some highlighted endpoints are too far away for the current free approach; move closer before climbing. A ladder merely passing behind a platform does not necessarily connect to that platform.

**A shot cannot pass through a ladder:** Only the opening at a ladder's top landing is projectile-permeable. The actual shot line must intersect the opening; proximity to a ladder does not grant permission to shoot through an otherwise solid floor.

**Tablet controls are crowded:** Rotate to landscape, try VIEW to refit the battlefield, and use HUD to temporarily hide the lower panels.

**A campaign save seems missing:** Confirm that you are using the original site address and the same browser/profile, with local site data intact.

## Project and release notes

UNDERGRID is part of **Unaffiliated**, the home for experimental games and creative projects. Version 1.40.7c is the current public tablet-capable release, building on the 1.40.7a rendering fix and 1.40.7b fall-trajectory fix. The emphasis of this release is readable vertical tactics, dependable deployment, and the ability to play the full battlefield experience on an iPad without sacrificing desktop controls.

**Version:** 1.40.7c  
**Release:** Public Tablet Release / Footer Viewport Fix  
**Site:** https://undergrid.unaffiliated.page/
