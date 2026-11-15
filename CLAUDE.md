# Psy Stress Remake

Renamed from "Psy Stress Overhaul" / PsyStressOverhaulByExpand to "Psy Stress Remake" (2026-11-13; zip `Psy_Stress_Remake_by_Expand_<version>.zip` from 0.8.4 on). Workspace folder and GitHub repo renamed to `psy-stress-remake` the same day.

Remake of livvan's Psy Stress / Stressfull Zone 1.06.04 for G.A.M.M.A. Single GAMMA-only version.
Shipped readme: `src/readme.md` (full feature list, presets, version history, install notes).

## Files
- `src/gamedata/scripts/arszi_psy.script`: main mod (replaces the same file from "G.A.M.M.A. Psy rework";
  must load below it in MO2).
- `src/gamedata/scripts/psy_stress_dao_patch.script`: DAO / Arrival psy aura follows the psy anomaly slider.
- `src/gamedata/scripts/psy_stress_gamma_hit_patch.script`: forwards real damage from GAMMA's Actor Damage
  Balancer to Psy Stress; makes psy hits skip the balancer's own psy subtraction.
- `src/gamedata/scripts/stress_mcm.script`: MCM menu (tab "Psy Stress Remake" / "Пси-стресс ремейк").
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
- Damage preset also sets Controller psy damage 30/40/50/75/100% and psy anomaly damage 10/20/35/45/70% of base GAMMA (0.8.6).
- Psy anomaly hits (draftsman is an anomaly zone) go through GAMMA's Actor Damage Balancer `shit_booster` (exact base
  GAMMA damage), scaled by the slider in `arszi_psy.apply_gamma_anomaly_psy_hit`; without the balancer, Psy Stress's
  own formula x slider. DAO (`zone_mine_radar`) / Arrival (`zone_mine_cdf`) psy aura: `psy_stress_dao_patch.script` wraps
  `drx_da_main.anomalies_near_actor_functions[sec]` (300 ms window: actor-sourced psy hits count as anomaly hits) and
  replaces `drx_da_main.change_psy_health` (only the aura uses it; DAO's cached psy table goes stale after a load).
  Psy emitters / psi-storms hit with draftsman = actor and are not covered.
- Name everywhere: "Psy Stress Remake"; Russian MCM tab "Пси-стресс ремейк" (0.8.6).
- "Phantom appearance": realistic mutants (default, via xcvb's phantoms mod) or classic phantoms; all phantoms
  follow the Psy Stress threshold; xcvb's own spawning is turned off.
- Author credit "Expand" at the top of the MCM page.

## Check in game
After loading a save the log should contain:
`hit stress forwarded from GAMMA damage balancer to Psy Stress`; with DAO or Arrival also
`DAO / Arrival psy aura follows the Psy Stress psy anomaly damage slider`.

## Open items
- Planned: post on a mod page with English and Russian descriptions in Discord markdown.
