# UNDERGRID

**Current working build:** 1.40.4 — Variable Worlds + Terrain Lab  
**Stable game milestone:** 1.40.2 — Living Battlefields + Deployment  
**Format:** Single-file browser game (HTML / JavaScript / Canvas)  
**Status:** Active development / playable campaign

---

## What is UNDERGRID?

**UNDERGRID is a retro-futurist side-view tactical RPG where a persistent customizable crew fights through vertical physical battlefields, accumulates equipment, skills, injuries and history, and can either be commanded turn-by-turn or allowed to fight autonomously.**

The game combines:

- persistent gang/campaign development
- alternating-activation tactical combat
- physical 2D side-view battlefields
- jumping, climbing, falling and knockback
- cover, exposure, range and line of sight
- distinct ranged and melee weapon roles
- grenades, gear and cybernetics
- persistent rival crews
- procedural territory battlefields
- optional autonomous play through AUTO

The minimalist vector/CRT presentation is part of the simulation language: silhouettes, platforms, ladders, projectiles, cover and effects are intended to make the state of the fight readable without hiding it beneath decorative art.

---

# CORE GAME LOOP

1. Manage a persistent crew.
2. Equip fighters from the Armory and Supply Terminal.
3. Select fighters for a campaign battle.
4. Deploy them onto a territory-specific battlefield.
5. Fight using alternating activations.
6. Resolve objectives, casualties and victory.
7. Gain XP, injuries, scars, advances, money and campaign history.
8. Watch rival fighters and territories develop alongside the player.
9. Repair, re-equip, install cybernetics and prepare for the next fight.

Fighters are persistent campaign entities first and battlefield units second.

Campaign consequences apply to player fighters and persistent rival fighters. Disposable modes intentionally do not modify the campaign.

---

# TACTICAL COMBAT

Combat takes place on a physical side-view battlefield rather than a tile grid.

Fighters can:

- move along platforms
- climb ladders
- jump between elevations
- fall
- use cover
- shoot
- fight in melee
- throw grenades
- use equipment
- enter Overwatch
- interact with mission objectives
- be knocked from positions by attacks and explosions

Movement, range, cover and line of sight are spatial. Vertical position matters.

## Activations

Teams alternate fighter activations. Action Points determine what a fighter can accomplish during an activation.

Overwatch commits the fighter's remaining activation and reserves the appropriate AP for a reaction shot.

## AUTO

AUTO allows the AI to control combat rather than requiring manual orders.

The long-term rule is strict:

> Player, AI and AUTO should operate under the same battlefield rules.

Environmental systems, terrain costs, weapons, traversal and mission interactions should not rely on hidden AI privileges.

---

# FIGHTERS BECOME PEOPLE

Persistent fighter development is one of UNDERGRID's central systems.

A campaign fighter tracks:

- stable identity
- crew/faction
- base statistics
- permanent stat changes
- XP
- advancement eligibility
- skills
- injuries
- scars
- battles
- kills
- downs
- behavior history
- loadout
- cybernetics
- career history/status

## Advancement

XP thresholds create advancement opportunities.

Advancement can provide raw stat improvements or skills. Skill families are influenced by how a fighter actually behaves during their career.

### Skill families

**GUNNER**
- Braced
- Point Blank
- Marksman

**BRAWLER**
- Scrapper
- Brutalist
- Follow Through

**AGILITY**
- Sure Footed
- Finesse Fighter
- Vaulter

**SURVIVAL**
- Tough
- Iron Nerve
- Second Wind

**TECH**
- Grenadier
- Field Medic
- Gearhead

**LEADERSHIP**
- Rally
- Command Presence
- Field Captain

A fresh fighter begins essentially **UNFORMED**. Their eventual strengths emerge partly from battlefield behavior.

---

# INJURIES, SCARS & CYBERNETICS

Campaign fighters can suffer persistent injuries.

Examples include:

### Minor
- Bruised
- Twisted Ankle
- Concussion

### Lasting
- Rattled
- Bad Knee
- Cracked Rib
- Burn Marks
- Nerve Damage

### Critical
- Mangled Arm
- Shattered Leg
- Ruined Eye
- Spinal Damage

Critical injuries provide natural hooks for cybernetic replacement.

Non-stat scars such as Facial Scar, Burn Scar and Impact Scar also become part of a fighter's history.

## Cybernetics

Permanent body slots:

- ARM
- LEG
- EYE
- SPINE

Current implants include restorative and enhanced replacements such as:

- Scrap Arm
- Servo Arm
- Scrap Leg
- Piston Leg
- Optical Implant
- Targeting Eye
- Spinal Brace
- Reflex Spine

Cybernetics can neutralize appropriate critical injuries and enhanced versions can provide permanent stat bonuses.

Installed cybernetics are permanent; replacing an implant destroys the old implant in that slot.

---

# WEAPONS & COMBAT TRAITS

UNDERGRID uses distinct weapon roles rather than a collection of interchangeable damage numbers.

The combat system supports ranged weapons, melee weapons, multi-hit attacks, blast weapons, indirect fire, status weapons and specialized penetration/cover behavior.

Canonical trait vocabulary includes:

- RAPID
- SPRAY
- SUPPRESSION
- SCATTER
- BLAST
- INDIRECT
- COVER BREAK
- IGNORE COVER
- ARMOR PUNCH
- ARMOR RIP
- BURN
- TOXIN
- SHOCK
- PARRY
- KNOCKBACK
- UNWIELDY
- FINESSE
- BRUTAL

Status provenance is retained where necessary so delayed BURN/TOXIN effects can still credit the responsible attacker.

---

# GRENADES

Every fighter has a dedicated grenade slot separate from normal Gear and Cybernetics.

Default campaign rule: **one equipped grenade per battle.**

Current grenade families:

### FRAG
Blast damage and knockback.

### SMOKE
Creates a physical LOS-blocking smoke volume.

### SHOCK
Applies the canonical SHOCK/AP-disruption status.

### INCENDIARY
Applies BURN and creates temporary fire.

Grenades use explicit combat profiles rather than inheriting the thrower's weapon statistics.

---

# GEAR

Current Gear foundation:

### Field Medkit
Battlefield healing.

### Climbing Rig
Improves mobility/jumping.

### Respirator
Protects against TOXIN.

### Targeter
Improves ranged accuracy.

Gear occupies its own equipment layer and is separate from grenades and cybernetics.

---

# CAMPAIGN

The campaign contains persistent player fighters, persistent named rival fighters, territory ownership, money/supply and off-screen rival career activity.

## Rival crews

Current persistent rival factions include:

- Iron Choir
- Pale Dogs
- Static Saints
- Grin Company
- Children of the Sump

Each has a persistent named roster and doctrine weighting. Rival fighters gain battles, XP and advances through both direct tactical encounters and appropriate off-screen territory conflicts.

Rival autonomous weapon purchasing/upgrading is **not yet fully implemented**.

## Supply Terminal

The Supply Terminal supports:

- Common stock
- rotating uncommon stock
- item information before purchase
- selling from stash
- cybernetics
- live Armory refresh after purchases

Rare/exotic equipment is intended to remain outside the ordinary terminal economy.

---

# GAME MODES

## Campaign
The persistent game. Fighter careers, injuries, XP, equipment, rival progression, territory and economy matter.

## Quick Battle
Player vs CPU with randomized equivalent disposable teams.

Quick Battle does **not** mutate campaign progression.

## Player vs Player
Local disposable multiplayer.

Player vs Player does **not** mutate campaign progression.

---

# CURRENT CAMPAIGN MISSIONS

The existing mission framework includes objective-based battles such as:

- Elimination
- Salvage Run
- Relay Control

Mission generation is designed to validate required objective routes rather than assuming every generated battlefield is legal.

Salvage generation includes a conservative post-pickup encumbered-route check so a carrier should not be given an impossible route to extraction.

---

# FUTURE MISSION: CORE RUN

**CORE RUN** is a planned mission type inspired by Bombing Run-style objective play.

The important architectural decision is that Core Run is a **mission layer**, not a special map family.

A compatible battlefield supplies:

- neutral Core spawn socket
- opposing Uplink/goal sockets
- valid end-to-end routes
- compatibility with normal traversal infrastructure

The intended mode:

1. A neutral Core begins in contested territory.
2. A fighter can take possession.
3. Teams fight to deliver the Core to the opposing Uplink.
4. The Core can eventually be passed/thrown using physical battlefield rules.
5. A downed carrier drops possession.
6. Normal combat remains fully active around the objective.

Existing and future battlefield grammars should therefore be designed so unusual traversal systems, gaps, verticality and routes can also support Core Run later.

---

# BATTLEFIELD DNA

UNDERGRID's procedural level system is called **Battlefield DNA**.

The goal is not merely to rearrange the same platforms. Territories should produce battlefields with genuinely different:

- silhouettes
- dimensions
- verticality
- route structures
- density
- openness
- cover
- traversal problems
- environmental identity

The system separates several conceptual layers:

1. **Structural Grammar** — the actual topology.
2. **Decoration Layer** — visual identity without gameplay consequences.
3. **Mechanical Layer** — terrain and interactive infrastructure.
4. **Event Layer** — timed/cycling battlefield behavior.

This separation allows wild visual experimentation without silently changing collision or tactical rules.

---

# BATTLEFIELD GRAMMARS

Current grammar families include:

- Vertical Shaft
- Vault Bunker
- Industrial Works
- Arena Pit
- Sump Lab
- Reactor Core
- Scrap Yard
- Growth Vats
- Hab Stack
- Transit Line
- Cathedral Nave
- Sewer Warren
- Bridgeworks
- Tower Ascent

The last four began as Level Lab experimental grammars.

---

# VARIABLE WORLD SIZE

As of 1.40.4, battlefields are no longer constrained to the same invisible normalized rectangle.

Different grammars can have genuinely different physical dimensions.

Examples:

- Tower Ascent — extremely tall/narrow
- Vertical Shaft — tall
- Transit Line — extra wide/flat
- Sewer Warren — long and low
- Cathedral Nave — giant chamber
- Bridgeworks — broad void battlefield
- Scrap Yard — sprawling/low

The camera begins in **FIT** mode so oversized battlefields can be seen in context, while manual pan and zoom remain available.

This change has already proven tactically meaningful: extreme vertical maps such as Sky Needle create substantially different movement, range and positioning decisions.

---

# LEVEL LAB

Development access:

**Ctrl+Shift+D → UNDERGRID LAB → LEVEL LAB**

Level Lab is a disposable battlefield-design harness. It does not intentionally mutate campaign state.

It can control:

- archetype
- mission
- exact seed
- extremity
- world shape
- signature features
- territory mutator tags
- active mechanic prototype

World-shape experiments include:

- Auto / Archetype
- Compact
- Extra Tall
- Needle Tower
- Extra Wide
- Tunnel Run
- Giant Field

Extremity modes include:

- Standard
- Max Vertical
- Max Dense
- Max Open
- Min Cover
- Max Cover
- Route Chaos

Useful presets include:

- Standard Works
- Sky Needle
- Rat Warren
- Drowned Maze
- Reactor Abyss
- Cathedral Void
- Bridge Hell
- Scrap Fortress
- Hab Ratnest
- Longshot Line

Lab functions include:

- Generate
- Reroll Variant
- Next Archetype
- Random Weird
- Playtest
- AUTO ×20
- Validate ×200
- Export Report
- local Great / Good / Boring / Broken ratings

### Preview/playtest parity

The Lab now bypasses campaign territory routing when launching a disposable test.

The exact previewed:

- archetype
- DNA identity
- generated variant

must match the playtest map. If they do not, the playtest aborts instead of silently displaying the wrong battlefield.

---

# TERRAIN

Battlefield surfaces are beginning to carry both visual and mechanical identity.

Current surface language includes:

- jagged scrap
- pipes
- stonework
- rails
- trusses
- ribbed industrial decking
- sludge
- segmented technical/vault floors

Current difficult-terrain prototypes include:

- RUBBLE
- SLUDGE
- FLOODED
- SLICK

Difficult terrain modifies MOVE and AI route cost using the same underlying rule.

**Current issue / next improvement:** difficult terrain is not yet visually unmistakable enough. Sludge, flooding, rubble and slick surfaces need stronger direct battlefield rendering so the player can recognize their movement consequences without relying on text labels.

---

# ENVIRONMENTAL MECHANICS

The environmental-mechanics layer is beginning experimentally in Level Lab.

## Vent Cycle

Current prototype:

**VENT CYCLE // SMOKE LOS**

A steam vent telegraphs before activating and then creates a smoke volume using the existing canonical Smoke LOS system.

This is intentionally built from an established combat rule so player, AI and AUTO receive identical information and restrictions.

Further manual testing is still required.

---

# PLANNED TRAVERSAL INFRASTRUCTURE

Extreme world dimensions create new tactical play, but very large battlefields also need topology-changing infrastructure.

The current next target is **Transit Stations**.

Proposed behavior:

- physical stations appear at separated locations
- a fighter enters a station
- spends an action/AP cost
- rides the transit system
- emerges at another linked station
- player, AI and AUTO use the same transit graph

This can create flanking routes and rapid movement behind enemy lines on long Transit maps.

The same reusable interaction architecture can later support:

- freight elevators
- moving gantries
- flood gates
- blast doors
- conveyors
- maintenance tubes
- reactor lifts
- crushers
- other territory-specific machinery

A key design goal is that environmental machinery belongs to the place rather than feeling like arbitrary map gimmicks.

---

# BATTLEFIELD DESIGN TARGETS

The current direction intentionally favors **extreme battlefield premises**.

Examples:

### Sky Needle
An extremely tall fight where elevation, climbing and long vertical firing lanes dominate.

### Rat Warren
Low, dense, laterally sprawling tunnels with difficult terrain.

### Longshot Line
An extremely long Transit battlefield favoring ranged control and future transit-station flanking.

### Drawbridge Raid — planned benchmark
Two dense towers at extreme distance from one another, connected by a single exposed gantry/drawbridge, with low difficult-terrain tunnels providing a dangerous alternate route beneath.

This kind of map is the target: a battlefield whose strategic premise can be understood from its silhouette.

### Cathedral Void
A giant architectural combat space with huge nave/balcony/crypt relationships.

**Current issue:** the extreme Cathedral Void configuration can fail validation and needs a grammar/route repair rather than weakened validation.

---

# VISUAL DESIGN PRINCIPLES

UNDERGRID uses a minimal 1-bit/vector/CRT-inspired presentation.

Important rules:

- Tactical information should be visually legible.
- Legal actions should have visible affordances.
- Visual effects should explain simulation rather than obscure it.
- Difficult terrain should be recognizable from its appearance.
- Grates/shoot-through structures should remain obvious.
- Decorative geometry must not imply false collision.
- Environmental hazards should telegraph before activation.
- If something important happens in simulation but the UI does not communicate it, that is considered a gameplay problem.

Background identity has expanded significantly with animated territory-specific scenery including machinery, vats, water, windows, reactor structures, transit elements and other archetype-specific motifs.

---

# DEPLOYMENT

Battlefield DNA uses formation-based deployment rather than placing an entire crew in a single conga line.

Deployment attempts to spread fighters across meaningful platforms and height bands.

The player receives fixed legal deployment slots and can swap selected fighters between them before battle.

Formation identities include patterns such as:

- Shaft Stagger
- Bunker Echelon
- Arena Fan
- Transit Echelon

---

# TERRITORY

Territories persist as campaign locations with Battlefield DNA.

Territory identity can influence:

- archetype
- verticality
- density
- openness
- cover
- routes
- signature features
- environmental presentation
- deployment style
- world dimensions

The longer-term goal is for territory to become increasingly synonymous with battlefield identity: controlling or attacking a place should mean knowing what kind of physical fight happens there.

---

# INTERACTION CONVENTIONS

Current person-centric UI convention:

- left-click fighter card → Armory
- explicit Dossier control → Dossier
- right-click fighter → Dossier
- touch-hold fighter → Dossier where supported

Right-click is supplemental rather than mandatory because touch/iPad compatibility remains important.

---

# SAVE / PERSISTENCE

Campaign state is browser-local.

Development builds include campaign data controls such as:

- Reset Campaign
- Export Save
- Import Save

When testing deployed builds, using the same origin/browser is important for continued localStorage persistence.

Public deployment has used:

**https://undergrid.unaffiliated.page/**

---

# DEVELOPMENT ARCHITECTURE

UNDERGRID remains a self-contained single HTML application.

Important protected architecture principles include:

- battle completion has a single gameplay authority
- campaign aftermath owns persistent campaign resolution
- disposable modes remain isolated from campaign mutation
- Armory/setup/refresh composition should remain canonical rather than accumulating competing wrappers
- new systems should prefer explicit public APIs over cross-module reach-through
- stable systems should not be reopened without a reproducible defect

The protected architecture baseline is:

**1.37.3 — Stability Seal**

The current stable battlefield/game milestone is:

**1.40.2 — Living Battlefields + Deployment**

Current experimental development branch:

**1.40.4 — Variable Worlds + Terrain Lab**

---

# CURRENT DEVELOPMENT PRIORITY

The project is presently concentrating on making procedural battlefields a major pillar of the game.

Immediate direction:

1. Make difficult terrain visually unmistakable.
2. Repair Cathedral Void / giant-space validation without weakening legality checks.
3. Build Transit Stations as the first interactive traversal infrastructure.
4. Continue extreme structural grammars and benchmark battlefield premises.
5. Test and refine Vent Cycle.
6. Generalize traversal/environment interactions for elevators, gates, gantries, conveyors and related machinery.
7. Make mission placement exploit battlefield architecture.
8. Keep future Core Run requirements in the objective-socket and traversal architecture.
9. Promote successful Level Lab experiments into campaign generation.
10. After the level system matures, perform a broader UI/presentation polish pass.

---

# MAJOR REMAINING DEVELOPMENT AREAS

Beyond the current battlefield push:

- richer campaign population/economy simulation
- autonomous rival procurement/upgrading
- more complete environmental-mechanics library
- additional mission types, including Core Run
- UI consistency/polish across Territory, Rival Intel, Dossier, Armory and Supply
- front door / packaged-game flow
- New Campaign / Continue / Options presentation
- formal campaign victory/end-state
- final balancing and content expansion

---

# DEVELOPMENT RULES

Several rules have become important enough to treat as project invariants:

> **No silent failures.**  
> If the simulation does something important, the player must be able to understand that it happened.

> **Affordances represent legal actions.**  
> UI should not advertise actions that the rules will reject.

> **Same rules for player and AI.**  
> AI should understand the game rather than bypass it.

> **Protect stable systems.**  
> Experimental battlefield work should not casually reopen solved campaign/combat architecture.

> **Difficult is allowed. Impossible is not.**  
> Procedural missions must validate required routes.

> **A battlefield should have a premise.**  
> The long-term target is not “another arrangement of platforms,” but locations whose topology changes how the fight is played.

---

# CURRENT STATE

UNDERGRID is already a functioning tactical campaign game rather than a combat prototype.

Its strongest established pillars are:

- side-view physical tactical combat
- weapon/trait identity
- grenades and Gear
- AUTO
- persistent player and rival fighters
- XP / advancement / skills
- injuries / scars
- cybernetics
- campaign territory and world careers
- Supply and Armory
- Quick Battle and Player vs Player boundaries
- procedural Battlefield DNA
- animated battlefield identity
- tactical deployment formations
- Level Lab generation/playtest/stress workflow
- true variable-size battlefields

The current development challenge is to make the battlefield system as deep and memorable as the fighter/campaign systems already are.

---

## Current build note

1.40.4 passes JavaScript syntax validation, but manual browser playtesting remains authoritative for runtime behavior.

Recent manual results:

- **Sky Needle:** successful; extreme verticality creates genuinely new strategies.
- **Rat Warren:** structurally promising; difficult terrain needs much stronger visual communication.
- **Cathedral Void:** extreme configuration currently fails validation and requires repair.
- **Longshot Line:** successful extreme horizontal layout; highlights the need for rapid horizontal traversal infrastructure.
- **Vent Cycle:** implemented experimentally; awaiting meaningful manual playtest.

---

**UNDERGRID**  
*Persistent fighters. Physical battlefields. Places worth fighting over.*
