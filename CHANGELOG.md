# Changelog - Psy Stress Remake (formerly PsyStressOverhaulByExpand)

Newest last (same as the shipped readme). Earlier builds: PsyStress_GAMMA_1.06.04-gamma1..gamma4.

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
