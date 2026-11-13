# Psy Stress Remake

Renamed from "Psy Stress Overhaul" / PsyStressOverhaulByExpand to "Psy Stress Remake" (2026-11-13; zip name changes with the next version, 0.8.4). Workspace folder and GitHub repo renamed to `psy-stress-remake` the same day.

Remake of livvan's Psy Stress / Stressfull Zone 1.06.04 for G.A.M.M.A. Single GAMMA-only version.
Shipped readme: `src/readme.md` (full feature list, presets, version history, install notes).

## Files
- `src/gamedata/scripts/arszi_psy.script`: main mod (replaces the same file from "G.A.M.M.A. Psy rework";
  must load below it in MO2).
- `src/gamedata/scripts/psy_stress_gamma_hit_patch.script`: forwards real damage from GAMMA's Actor Damage
  Balancer to Psy Stress; makes psy hits skip the balancer's own psy subtraction.
- `src/gamedata/scripts/stress_mcm.script`: MCM menu (tab "Psy Stress Remake" / "Ремейк пси-стресса").
- `src/gamedata/configs/text/{eng,rus}/st_psy_stress_mcm.xml`: strings (rus = Windows-1251).

## Version
Scheme 0.x.y, bumped every delivered iteration. The version appears in: `mod.json`, `src/readme.md` (title +
history), header line of both scripts, author line (`ui_mcm_psy_stress_author_info`) in eng and rus xml.

## Decisions (keep)
- Keep all original psy-lowering and psy-raising logic (combat, hits, wounds, anomalies, surges, night, hunger,
  camps, campfires, sleep, regen, anabiotic) **except smokes/drinks**: this mod changes no item stats.
  Smokes & alcohol go to a separate mod (see ROADMAP.md).
- Items with a psy booster (Psy-Block etc.) still restore psy health.
- ARX and EFP variants dropped; no installer.
- MCM presets as drop-downs using MCM's built-in preset option (text keys); names don't show multipliers:
  damage Uneasy 3x / Tense 5x / Harsh 8x / Brutal 10x / Nightmare 15x (default Harsh),
  regen Steady 1x / Shaken 0.7x / Fragile 0.3x / Broken 0.1x (default Steady), easiest first.
- "Phantom appearance": realistic mutants (default, via xcvb's phantoms mod) or classic phantoms; all phantoms
  follow the Psy Stress threshold; xcvb's own spawning is turned off.
- Author credit "Expand" at the top of the MCM page.

## Check in game
After loading a save the log should contain:
`hit stress forwarded from GAMMA damage balancer to Psy Stress`.

## Open items
- Planned: post on a mod page with English and Russian descriptions in Discord markdown.
