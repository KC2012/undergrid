# UNDERGRID 1.38.2 — Equipment Tuning Lab

Base: 1.38.1a Gear Armory Integrity.

## Purpose
Designer-facing live balancing environment for final tuning of the expanding equipment catalog. The lab changes in-memory base definitions only; it does not mutate campaign inventory, ownership, fighter state, or localStorage.

## Entry
UNDERGRID LAB → EQUIPMENT LAB → OPEN EQUIPMENT TUNING.

## Weapons
Live editable mechanical fields include:
- damage min / max
- ranged accuracy
- penetration
- impact / knockback
- AP cost
- optimal range / max range
- mobility / jump modifiers
- weapon-specific advanced fields when present: blast, cone width, cone angle, melee attacks, melee accuracy
- resource reliability / discrete capacity
- Supply value
- rarity
- role text
- live traits list

Structural identity fields such as melee/ranged class, sidearm status, hands, family, and visual identity are displayed but intentionally not editable because changing them would affect Armory composition and derived-combo architecture.

The existing Combat Lab remains the authoritative presentation/FX test range and is linked directly from the tuning lab.

## Armor
Live editing:
- save
- move modifier
- jump modifier
- Supply value
- rarity
- role
- traits

Includes a reference-fighter mobility/jump readout.

## Gear
Gear mechanics were made data-driven so tuning controls affect actual gameplay:
- Field Medkit: heal, AP cost, uses/battle
- Climbing Rig: jump bonus, ladder approach maximum, ladder move factor
- Respirator: toxin blocking toggle
- Targeter: ranged accuracy bonus
- all Gear: Supply value, rarity, role

## Balance tools
- modified-item markers
- build-default deltas beside numeric controls
- derived weapon average damage / damage-per-AP
- representative armor expected-damage strip
- three-weapon comparison view
- sortable all-equipment Catalog Overview
- search/filter
- Reset Item
- Reset Category
- Reset All

## Import / Export
Schema: `UNDERGRID_EQUIPMENT_DESIGN_V1`

Two exports:
- `CHANGES_ONLY` — compact batch of values changed from this build
- `FULL_CATALOG` — complete current weapon / armor / gear design state

Payload also carries:
- weapon resource tuning
- weapon Supply values
- armor Supply values
- current Combat Lab weapon presentation export
- current Grenade Designer presentation export

The lab can import its own schema and apply the design live for continued tuning.

## Validation
- Combined embedded JavaScript passes `node --check`.
- No duplicate HTML IDs detected.
- Structural checks passed for all tabs, import/export, change tracking, reset flows, weapon/armor/gear live application, resource and trait editing, compare/overview screens, and all four data-driven Gear effects.

## Intentional boundary
This is a development sandbox. Reloading the page restores shipped values unless a design JSON is exported first and re-imported. This prevents tuning experiments from contaminating campaign saves.
