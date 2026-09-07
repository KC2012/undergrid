# UNDERGRID

**A persistent side-view tactical skirmish game for the browser.**

UNDERGRID is an experimental turn-based tactical RPG about a crew of
fighters surviving, fighting, and changing over the course of a
campaign.

Battles take place across physical 2D battlefields built around
platforms, ladders, elevation, line of sight, cover, jumping, falling,
knockback, explosions, and close combat. Between battles, fighters keep
their equipment, experience, skills, injuries, records, and history.
Rival crews do the same.

The goal is to make every fighter gradually become a person rather than
a disposable unit.

## PLAY

**Live build:** https://undergrid.unaffiliated.page/

UNDERGRID runs directly in a modern desktop browser. No installation is
required.

Campaign progress is stored locally in the browser. Clearing
site/browser storage can erase that campaign data.

## CURRENT BUILD

**1.39.7 --- Fighters Become People / World Careers**

This is an active development build. Systems, balance, interface,
content, and campaign structure are still evolving.

## THE GAME

### Tactical Combat

UNDERGRID uses alternating fighter activations on side-view
battlefields.

Position is physical. Fighters move across platforms, climb ladders,
jump gaps, fall, take cover, fire through real lines of sight, throw
grenades, engage in melee, and can be displaced by impacts and
explosions.

Weapons are intended to create different tactical problems rather than
simply form a ladder of better numbers. Range, accuracy, penetration,
impact, AP cost, mobility, ammunition/reliability, traits, blast
geometry, and close-combat behavior all matter.

Current combat systems include:

-   Ranged and melee combat
-   Physical line of sight and cover
-   Vertical movement, ladders and jumping
-   Falling and knockback
-   Overwatch
-   Weapon traits and status effects
-   Frag, Smoke, Shock and Incendiary grenades
-   Armor and Gear
-   Explosive and area attacks
-   Persistent injuries
-   AI-controlled opposition
-   AUTO battle control

### Fighters Become People

Campaign fighters persist between battles.

Each fighter can accumulate:

-   XP and ranks
-   Skills and advancements
-   Kills, wins and battle history
-   Injuries and recovery
-   Persistent equipment and loadouts
-   Individual combat statistics

Advancement choices belong to skill branches such as **Gunner, Brawler,
Agility, Survival, Tech, and Leadership**, allowing fighters to develop
distinct roles over time.

The **Dossier** is the character-facing side of the system: who the
fighter is, what they have done, what has happened to them, and how they
are developing.

The **Armory** is the equipment-facing side: what they are carrying,
wearing, and bringing into battle.

### Rival Crews

The enemy is persistent too.

Campaign rival crews contain named fighters with their own career
records. Rivals gain battle experience, rank up, receive advancements,
and return in later encounters as the same developing fighters.

The Territory simulation also resolves conflicts elsewhere in the world.
Rival fighters can gain experience and advancements from battles their
crews fight while the player is somewhere else.

The intention is for the campaign to gradually create a population of
allies, enemies, veterans, casualties, grudges, and recognizable
recurring characters.

### Territory

The campaign includes a Territory Network contested by multiple crews.

Territory changes hands as the campaign advances. The player's battles
are only one part of that process: rival crews pursue their own
objectives and fight over locations independently.

This system is still being expanded. The long-term goal is for
territory, population, economy, mission generation, and tactical
battlefields to become increasingly interconnected.

### Equipment

Fighters can equip combinations of:

-   Primary and secondary weapons
-   Armor
-   A dedicated grenade
-   Gear
-   Future cybernetics

The Supply Terminal allows equipment to be purchased during a campaign,
while the Armory manages individual fighter loadouts.

Weapons range from conventional pistols, rifles and shotguns to heavy
weapons, launchers, energy weapons and specialized melee equipment.

### Other Modes

**Campaign**\
The main persistent game. Fighters, rivals, equipment, injuries,
advancement and Territory matter across battles.

**Quick Battle vs CPU**\
A disposable player-vs-AI skirmish using randomized roughly equivalent
teams. No campaign persistence.

**Hotseat PvP**\
Local player-vs-player skirmish mode. No campaign persistence.

## CONTROLS

UNDERGRID is primarily mouse-driven.

Select fighters and actions through the tactical interface, then
interact directly with the battlefield to move, target, shoot, throw,
climb, jump, charge, or use other contextual actions.

The interface displays legal actions, AP, weapon state, status effects,
movement information, and combat feedback as needed.

Developer and experimental tools are currently still included in
development builds.

## VISUAL DIRECTION

UNDERGRID deliberately uses a minimal vector/CRT presentation.

The stripped-down graphics are intended to make the battlefield readable
as a physical tactical space while leaving room for increasingly
expressive fighters, equipment, effects, environments, and campaign
history.

The project is being developed as a game first rather than as a graphics
demo: simulation, interaction, tactical clarity, persistence, and
emergent stories are the priority.

## DEVELOPMENT

UNDERGRID is actively being designed and developed through iterative
playable builds.

The current major development sequence is:

1.  **Combat / equipment / trait foundation** --- established
2.  **Fighters Become People** --- current integration checkpoint
3.  **Injuries → Cybernetics**
4.  **Territory Becomes Battlefield**
5.  **Campaign population and economy expansion**
6.  **Front door, packaging and broader release polish**

The current public build should be considered a playable work in
progress rather than a finished release.

## SAVE DATA

Campaign state is stored using browser local storage.

For the most reliable continuity:

-   Play from the stable public URL
-   Use the same browser/device for an ongoing campaign
-   Avoid clearing site data if you want to retain the campaign

Development builds may occasionally change save structures.
Compatibility is preserved where practical, but this remains an actively
changing project.

## PROJECT STATUS

UNDERGRID is currently in active development.

**Public checkpoint:** `1.39.7`

The present focus is validating the completed Fighters Become People
framework before moving deeper into persistent injuries, cybernetics,
and the campaign world simulation.

------------------------------------------------------------------------

**UNDERGRID**\
*Fighters become people.*
