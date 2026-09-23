# UNDERGRID

**Version 1.40.7 — Public Tablet Release**  
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

## Running locally

There is no build step or dependency installation. Download `index.html` and open it in a modern browser. The release is a self-contained HTML file; a local web server is optional for ordinary play. For the published version, deploy the same file as your site's root `index.html`.

## Deployment

The existing site is deployed through a GitHub-to-Vercel workflow:

1. Back up the currently published `index.html` and keep the previous release available for rollback.
2. Replace the repository's existing `index.html` with the v1.40.7 file.
3. Commit and push to the branch used by the production Vercel project.
4. Wait for the Vercel deployment to complete, then open the live URL and hard-refresh if necessary.
5. Smoke-test a Quick Battle on desktop and an iPad in landscape orientation. Check fighter visibility, touch pan/pinch, HUD toggle, toolbar layout, climb endpoints, and shooting through a top ladder aperture.
6. Open the existing campaign on the **same site origin** and verify that saved progress is still available.

**Save-data caution:** Campaign progress uses browser-local storage. Different browsers, private browsing, clearing site data, or moving the game to a different domain may make an existing save unavailable. Preserve the current production domain and avoid clearing browser storage during the update.

## Release checks

The 1.40.7 release includes a developer-facing **Public Release Audit**. It combines existing checks for core stability, all live battlefield families, battlefield mechanisms, ladder/LOS cases, fighter deployment visibility, responsive canvas layout, and required UI elements. Some live-battle checks are deferred until a battle is active. The audit is a regression aid, not a substitute for a real iPad/browser smoke test after deployment.

To access development controls, use `Ctrl` + `Shift` + `D` in the desktop browser. Development and experimental level-lab controls are not part of the normal player flow.

## Troubleshooting

**Fighters do not appear after deployment:** Try **VIEW** to refit the battlefield. If the problem persists, capture the battle seed and use the in-game debug export so the exact map and state can be reproduced.

**A ladder is visible but CLIMB will not use it:** Only connected ladder endpoints are climb destinations. Some highlighted endpoints are too far away for the current free approach; move closer before climbing. A ladder merely passing behind a platform does not necessarily connect to that platform.

**A shot cannot pass through a ladder:** Only the opening at a ladder's top landing is projectile-permeable. The actual shot line must intersect the opening; proximity to a ladder does not grant permission to shoot through an otherwise solid floor.

**Tablet controls are crowded:** Rotate to landscape, try VIEW to refit the battlefield, and use HUD to temporarily hide the lower panels.

**A campaign save seems missing:** Confirm that you are using the original site address and the same browser/profile, with local site data intact.

## Project and release notes

UNDERGRID is part of **Unaffiliated**, the home for experimental games and creative projects. Version 1.40.7 is the public tablet-capable release built on the 1.40.6 full battlefield candidate. The emphasis of this release is readable vertical tactics, dependable deployment, and the ability to play the full battlefield experience on an iPad without sacrificing desktop controls.

**Version:** 1.40.7  
**Release:** Public Tablet Release  
**Site:** https://undergrid.unaffiliated.page/
