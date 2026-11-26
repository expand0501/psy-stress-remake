**Psy Stress Remake by Expand 1.0.2**

Psy Stress remake for G.A.M.M.A. by Expand, based on Psy Stress / Stressfull Zone 1.06.04 by livvan
(https://www.moddb.com/mods/stalker-anomaly/addons/psy-stress). Single version for S.T.A.L.K.E.R. Anomaly G.A.M.M.A.

**What it does (unchanged from the original)**
- Constant psy-health drain from the stress of the Zone.
- Stress increases: combat, being hit, being wounded, near active anomalies and anomaly zones, surges and psi storms, underground, at night, hunger, thirst, lack of sleep.
- Stress decreases: emission cover, non-hostile camps, lit campfires.
- Psy-health recovery: natural regeneration while calm, sleep, items with a psy booster (Psy-Block and similar), psy-protecting artefacts, anabiotic (full restore).
- Psy damage from psy fields and controllers, low-psy effects (blur, sound shock, voices, phantoms), death or zombification at zero psy health.
- Everything configurable in MCM (Psy Stress Remake tab).

**Campfires**
- MCM > Psy Stress Remake > Gameplay Modes > Campfire psy effect:
  - Campfires reduce stress (default): near a lit campfire psy drain is lowered by "Campfire stress reduction" (default 75%).
  - Campfires regenerate psy health: near a lit campfire psy health goes up by "Campfire psy regeneration" (% per 10 in-game minutes, also set by the psy regeneration preset); normal drain still applies.
- Range: "Campfire calming distance" (default 15 m).
- D.O.G.M.A.: its Campfire Healing no longer heals psy (its psy slider is ignored), so campfire psy works only through Psy Stress. D.O.G.M.A.'s body and limb healing still work.

**Phantoms**
- MCM > Psy Stress Remake > Gameplay Modes > Phantom appearance: Realistic mutants (default) or Classic phantoms.
- Realistic mutants use "Phantoms at low psy health" (xcvb) together with "Maybelline's Restore XCV phantoms" (both in G.A.M.M.A.): phantoms look like real mutants and vanish from one hit. Without them, classic phantoms are used.
- Both kinds appear only below the Psy Stress phantom threshold (Stress Stages), with the Psy Stress delay and max count. The xcvb mod's own automatic spawning is turned off.

**Presets**
Two drop-down lists at the top of MCM > Psy Stress Remake > General Configuration. Selecting a preset moves the sliders below it to the preset values (press Accept to apply); the sliders can be fine-tuned afterwards.
- Psy damage preset: Uneasy (3x original), Tense (5x), Harsh (8x), Brutal (10x), Nightmare (15x). Sets basic psy drain, psy stress on receiving damage, psy stress from wounds, Controller psy damage (30% / 40% / 50% / 75% / 100%) and psy anomaly damage (10% / 20% / 35% / 45% / 70% of base G.A.M.M.A.). Default: Harsh.
- Psy regeneration preset: Steady (1x, original, easiest), Shaken (0.7x), Fragile (0.3x), Broken (0.1x). Sets basic psy regeneration and campfire regeneration. Psy boosters (Psy-Block etc.), psy-protecting artefacts, sleep and surge cover recovery follow the basic regeneration slider. Anabiotic still restores psy health fully. Default: Steady.

**Changes from the original**
- G.A.M.M.A. hit fix: GAMMA's Actor Damage Balancer cancels engine hits on the player, so being shot or bitten never caused psy stress. psy_stress_gamma_hit_patch.script forwards the real damage to Psy Stress.
- Psy damage and psy regeneration presets in MCM.
- Removed: installer, ARX and EFPv4 versions, and the optional smokes/alcohol item rebalance. This mod changes no item stats.

**Version history**
- 0.1.0: original mod + installer + GAMMA hit patch (superseded).
- 0.2.0: GAMMA-only core mod, hit fix built in, no item changes.
- 0.3.0: first psy damage / regeneration presets (1x-10x).
- 0.4.0: new presets - damage 3x-15x, regen 0.1x-1x.
- 0.5.0: regen list ordered easiest first; 1x preset renamed to Steady. Mod renamed to PsyStressOverhaulByExpand.
- 0.5.1: MCM tab renamed to "Psy Stress Overhaul"; author line (Expand) at the top of the MCM page.
- 0.6.0: presets now move the MCM sliders instead of multiplying them in the background; wider slider ranges; slider defaults match the default presets (Uneasy / Steady).
- 0.6.1: fixed presets not moving the sliders - now uses MCM's built-in preset option (MCM 1.7.1+); with older MCM the presets are plain lists.
- 0.6.2: preset lists use text keys instead of numbers (fix for regeneration presets not moving the sliders).
- 0.7.0: "Phantom appearance" option (classic phantoms / realistic mutants via the xcvb phantoms mod); xcvb's own phantom spawning turned off, all phantoms follow the Psy Stress threshold; fixed phantoms appearing at high psy health with "Maybelline's Restore XCV phantoms" (get_ppe_intensity now uses the G.A.M.M.A. Psy rework scale).
- 0.7.1: new defaults - realistic phantoms, Harsh psy damage preset, voice/sound mods compatibility on; Russian name of the MCM tab ("Переработка пси-стресса"); campfire regeneration fallback without MCM matches the MCM default.
- 0.8.0: performance pass, same gameplay. Main loop gated by real time; anomaly zone, safe camp, campfire, hunger/thirst/sleep and night checks run once per real second; anomaly zone positions cached and compared with squared distance; one campfire search per second instead of two per tick (none for Cozy Campfires bonus when it is off); artefact psy immunity cached per section; no new closures every tick; debug logging no longer evaluated when debug is off; non-psy hits leave the hit handler immediately; anomaly zone list rebuilt per level.
- 0.8.1: review fixes - slow environment checks every 0.5 s (faster reaction); realistic phantoms only when their squads can be tracked (needs Maybelline's Restore XCV phantoms), otherwise classic; 3-second grace period before an offline phantom squad is released (new squads were at risk of vanishing before appearing); xcvb takeover re-applied on every load; get_psy_health safe if another mod calls it before the save is loaded; per-camp debug text only built in debug mode; consistent campfire fallback value.
- 0.8.2: fixed psy attacks (controllers, psy fields, phantom hits) sometimes doing double psy damage: the G.A.M.M.A. damage balancer and Psy Stress both subtracted psy health for the same hit, depending on callback order. Psy hits now skip the balancer's psy subtraction; its heartbeat sound and screen effect stay.
- 0.8.3: stability and cleanup - a save made during the psy death scene no longer leaves input disabled or NPCs ignoring the player; psy health functions are safe when another mod calls them before the player exists; no global variables left in the scripts.
- 0.8.4: mod renamed from PsyStressOverhaulByExpand to Psy Stress Remake: MCM tab "Psy Stress Remake" (Russian: "Ремейк пси-стресса"), zip name, log lines "[Psy Stress Remake]". Gameplay unchanged; MCM settings keep their IDs, so your settings are kept.
- 0.8.5: test build, not released (changes are listed under 0.8.6).
- 0.8.6: the psy damage preset now also sets Controller psy damage (Uneasy 30%, Tense 40%, Harsh 50%, Brutal 75%, Nightmare 100%; default was 40%). New "Psy anomaly damage" slider: psy anomalies deal a % of the base G.A.M.M.A. psy anomaly damage (calculated by G.A.M.M.A.'s Actor Damage Balancer with its psy protection), set by the preset from 10% (Uneasy) over 20% / 35% (Harsh, default) / 45% to 70% (Nightmare). Covers psy fields, other psy anomalies and the psy aura of Dynamic Anomalies Overhaul / Arrival (new psy_stress_dao_patch.script; the aura's direct psy damage no longer bypasses Psy Stress). Russian MCM tab name: "Пси-стресс ремейк". Saved MCM values are kept: pick the psy damage preset again (and Accept) to get the new values.
- 0.8.7: new Stress Stages defaults - first stage (blur) at 60% psy health (was 75%), second stage at 40% (was 50%), voices at 50% (was 70%), phantoms at 30% (was 25%). New "Screen blur strength" slider (0-100%, default 100% = as before; applies live). Stage descriptions in MCM now say what each stage really does. Saved MCM values are kept: set the sliders by hand to get the new defaults.
- 0.8.8: test build, not released (changes are listed under 1.0.0).
- 0.8.9: test build, not released (changes are listed under 1.0.0).
- 1.0.0: first stable release. campfire psy effect is now a choice in MCM (Gameplay Modes > Campfire psy effect): "Campfires reduce stress" (default, as before; "Campfire stress reduction" slider, default 75%) or "Campfires regenerate psy health" ("Campfire psy regeneration" slider, set by the psy regeneration preset). It replaces the "Use Cozy Campfires by Voland33" checkbox, which was this same built-in regen mode and not a compatibility option: if you had it on, pick the regen mode again. D.O.G.M.A. compatibility: D.O.G.M.A.'s Campfire Healing no longer heals psy (new psy_stress_dogma_patch.script; Psy Stress already cancelled it, but the psy bar could twitch and D.O.G.M.A.'s orange tint showed); its body and limb healing still work. Without MCM the campfire distance is now 15 m like the MCM default (was 4 m).
- 1.0.1: fixed two cases where the psy death scene never ended (black screen, no input, NPCs ignoring the player): psy health restored above 0 while the scene runs, and a second psy death in the same session after one that did not kill (god mode, Marked by the Zone, a revive mod). Psy health above 5% now ends the scene and the player survives; a small gradual restore (a cigarette) does not interrupt it. Input is given back before the death, so revive mods can take over.
- 1.0.2: fixed cover not calming during emissions and psi-storms. New Safe Zones and Dynamic Emission Cover (both in G.A.M.M.A.) report a sheltered player as "underground"; Psy Stress took that as a real underground level, skipped the cover and camp stress reduction and added the underground stress. Underground is now read from the level; shelter found by those two mods counts as emission cover too. While sheltered, the emission stress still applies, the cover reduction outweighs it.

**Requirements**
- MCM 1.7.1 or newer for presets that move the sliders (GAMMA ships MCM by RavenAscendant).

**Installation (MO2)**
- Install the zip as a new mod.
- Place it below "G.A.M.M.A. Psy rework" (both replace arszi_psy.script).
- Disable any previous Psy Stress install (including Psy Stress GAMMA edition gamma1-gamma5) and the separate GAMMA hit patch.
- No new game needed. When updating from another Psy Stress version, removing old "psy_stress/" lines from axr_options.ltx is recommended. After updating from a version before 0.6.2, select both presets once in MCM and press Accept.

**Check**
After loading a save, the log (F:\Anomaly\appdata\logs) should contain:
"hit stress forwarded from GAMMA damage balancer to Psy Stress".
