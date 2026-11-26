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
- `src/gamedata/scripts/psy_stress_dogma_patch.script`: turns off D.O.G.M.A. Campfire Healing's psy heal.
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
- Campfire psy effect: MCM list `campfire_psy_mode` = stress (default, slider `campfire_stress_reduction`) / regen
  (slider `campfire_regen`, set by the regen preset); it replaced the checkbox `cozy_campfire_enabled` ("Use Cozy
  Campfires by Voland33", a built-in mode, not a compatibility option; saved value not migrated).
- D.O.G.M.A. Campfire Healing must not touch psy: `psy_stress_dogma_patch.script` wraps `__dogma_mcm.float` so
  `dogma/game/campfire_healing` `psy_pct` reads 0 (patched at script load, before D.O.G.M.A.'s on_game_start reads it).
  Body/limb healing untouched. Same in D.O.G.M.A. 0.6.5 and DOGMA_Russian_by_Expand 0.6.5.2.

## Check in game
After loading a save the log should contain:
`hit stress forwarded from GAMMA damage balancer to Psy Stress`; with DAO or Arrival also
`DAO / Arrival psy aura follows the Psy Stress psy anomaly damage slider`; with D.O.G.M.A. also
`[psy_stress_dogma_patch] D.O.G.M.A. Campfire Healing psy heal turned off`.

## Open items
- Discord descriptions (eng/rus, rules: skill `gamma-discord-description`): `docs/discord_en.md`, `docs/discord_ru.md` (1.0.0).
- In-game tests 2026-11-24 (`tools\autotest`, `-Suite psy`, profile `Claude Test`, installed 0.8.9 = 1.0.0 code, only version
  texts differ). Two bugs, both **verified** in game, fixed in 1.0.1 (**verified** in game 2026-11-24; `arszi_psy.script`, `manage_zombification`):
  1. Psy health raised above 0 during the death scene (`change_psy_health(0.3)`): the counter stops, so input stays
     disabled, `psy_death_scene` stays true (NPCs ignore the player) and stage 8 stays while psy < stage 2.
  2. `arszi_zombification_time_counter` is reset only on first update, the scene ends only at exactly 25: a second psy
     death without a load between (first one did not kill: immune, revive mod) never ends. Tested with
     `level_environment.is_actor_immune` forced true; with Revival System **inference**.
- Not tested in game: the default GAMMA engine (QUARK is installed), MCM page clicks / preset buttons, anything judged by eye or ear.
- 1.0.1 scene rules (keep): counter starts at 0 for every scene; psy above 5 % ends it (player survives), below it goes on; cleanup
  (`end_psy_death_scene`) runs before the kill, because Revival System disables input itself.
- 1.0.1 retest (installed 1.0.1, profile `Claude Test`): all 12 scenarios, 118 checks, PASS; `scene_interrupted`, `second_death` and
  `scene_load` failed on 0.8.9. No Lua errors or FATAL in the logs of the `death` and regression launches.
- 1.0.1 more tests (2026-11-24, profile `Claude Test`, no Lua errors or FATAL in the triaged logs): Revival System + psy death twice, PASS;
  difficulties 1-4, PASS; real psi-storm (its electric hits off) PASS; real emission in the open PASS (psy 0, real death, no stuck scene);
  `level` PASS on Cordon, Garbage, Agroprom, Rostok, Bar, Army Warehouses, Pripyat, Trucks Cemetery. Emission in cover: one FAIL (next).
- **Found (1 fixed in 1.0.2, **verified** in game 2026-11-24; 2 and 3 open, ask Expand):**
  1. Until 1.0.1 cover did not calm during an emission; it works before one. Base GAMMA's `125- New Safe Zones` and `426- Dynamic Emission Cover` set the event `underground`
     to true while the player is in cover during an emission; `update_psy_env_state` takes that as a real underground level, so `surface` is
     false: cover and camp calming are skipped and +0.33 is added. **Verified**: multiplier -0.75 before, 1.33 for the whole emission, and
     the code of both mods. Cause **verified** with 1.0.2: event true, level flag false in cover. In a spot outside every real safe zone: Dynamic Emission Cover (**verified**, 1.0.2); New Safe Zones has no
     coordinates for Trucks Cemetery (read in its code). `actor_status` then copies the event into `current_safe_cover` as `true` (a real zone gives its number). Both are enabled in `G.A.M.M.A` and `Claude Test`. Same code in 0.8.9.
     Fix: underground = `level_weathers.bLevelUnderground` (event only when nil); the event during a surge / psi-storm on a surface
     level counts as cover. Surge stress still applies in cover (original logic): 1 - 1.25 + 0.66. Test: `logic`, `emission_cover`, `storm_cover`.
  2. Radiation zone hits (`zone_field_radioactive_weak`, 10 per s) each count as hit stress: -0.045 psy per 10 s on Harsh (**verified**,
     Agroprom). Original logic (every engine hit counts); a design question.
  3. Non-anomaly psy hits (no draftsman; controllers and storms: **inference**) get no difficulty factor on any difficulty (**verified**; reason, callback order before the
     balancer, **inference**). Psy anomalies scale with difficulty twice (base GAMMA balancer). Hit stress follows real damage.
- In the psi-storm the electric hits (Momopate's Improved Pulses, base GAMMA, radius 100 m) killed the player of `claude_test` (no test god mode)
  at psy 0.34-0.57 in four runs.
- 1.0.2 retest (installed 1.0.2 = build, profile `Claude Test`): all scenarios PASS, no Lua errors or FATAL, except `revival` with phantoms
  (next). In cover -0.75 -> -0.09 -> -0.75 for emission and psi-storm. `level` only on Trucks Cemetery; the other levels were 1.0.1.
- 1.0.2 (2026-11-24, profile `Claude Test`, no Lua errors or FATAL): `shelter_dynamic` PASS, real spot on Trucks Cemetery that only Dynamic Emission Cover
  shelters (GAMMA's setting 95 %): 1.00 -> 0.41 -> 1.00, whole emission survived, psy 1.00. `ug_agroprom` and `ug_x18` PASS after a real level
  change: level flag and event true, underground +0.33 and no cover calming (1.58 difference to the flag off, = 0.33 + 1.25), regen, hits,
  death scene. Other underground levels: not tested. An emission while underground: not tested.
- **Revival System + realistic phantoms** (Revival System 0.6.55, **verified**): the phantoms are ordinary mutant sections, Revival System
  counts them as fighters; 2 of 2 runs with phantoms on 1.0.2 ended in a lost calculated fight and a real death, with phantoms off
  (`phantoms_enabled`) the rescue passes twice. Not caused by 1.0.2 (that code is unchanged). Scenario `revival_phantoms` = phantoms on.
- 1.0.2 in profile **`G.A.M.M.A`** (2026-11-24/25, new game on Cordon, save `claude_test2`, installed 1.0.2 = build, QUARK engine, separate save
  folder): all psy scenarios except the Revival ones (Revival disabled) and the save-bound ones (`level_military`, `level_pripyat`), no Psy Stress Lua
  errors. Some checks failed on the first try, all explained by the test or the place, none by the mod: `zombie` (a camp shoots a zombified
  player, hits by `sim_default_stalker_0` seen in the log; `zombie_away` passes), `live_rate` underground (the test counted the mod's own negative rate as
  an outside drain), `storm_ended` (no psy protection, psy 0, real death), `multiplier_back` in `shelter_dynamic` (NPCs pushed the player into a real safe zone;
  -1.25 is right; check adjusted, scenario not rerun). `shelter_dynamic` there on Cordon: the cover flag and -0.59 **verified**.
- After a real death, loading crashed in `G.A.M.M.A` too (Ledge Grabbing line 244, `db.actor` nil; 1 of 1 there): not Psy Stress, same as before.
  Base GAMMA Lua errors in that profile, not ours: `a_faction_prices`, `mags_patches`, `zz_ui_inventory_better_stats_bars`, `zzz_mspizza_godis_zoomcalc`.
