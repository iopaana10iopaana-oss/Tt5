# Tt5

This repo contains a lightweight front-end prototype for a Travian-like builder.

## Game configuration notes

The client consumes `civitas-data/game-config.json`. The latest update introduces:

### `unitTypes`

* Top-level object where the key is the unit id used throughout the UI and simulator.
* Each entry exposes: `name`, `role`, `class`, `stats` (attack/defense/speed/range), `cost` (resource object), `upkeep`, `trainingTime`, `carry`, and a `requires` object describing the minimum building + level needed to unlock the unit.
* Optional knobs include `bonusVsClass` (map of target class => multiplier delta) and `raidBonus` (float applied when evaluating raid loot/odds).

### `aiOpponents[].armyProfile`

* `weights`: map of unit ids -> relative weight when rolling that opponent's army composition.
* `baseArmySize`: optional override for the nominal army size (defaults to `army` if omitted).
* Any other numeric toggles (e.g., `preferredRaiders`, `minWave`, `maxWave`, `siegePreference`) are optional and allow the battle simulator to tweak how aggressive the AI behaves.

### `initialState.troops`

Every unit id defined in `unitTypes` should appear in the initial troop map (even if zero) so the client can track counts without checking for undefined keys.
