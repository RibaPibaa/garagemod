# Garage Auction — Forge 1.20.1

Standalone Forge mod project. Target: Minecraft 1.20.1 / Forge 47.4.10 / Java 17.

## Build

Push this folder to a GitHub repository. The workflow `.github/workflows/build.yml` runs `gradle build` and publishes `garageauction-jar` as a workflow artifact. Put the resulting reobfuscated JAR in the instance `mods` folder.

## Commands currently implemented

- `/garages small|medium|large` — generate the marketplace, garage shells, loot chests and three arena shells.
- `/clearstructure` — removes blocks from the generator's current palette in a radius around the executing player.
- `/cleargarages` — clears the generator palette nearby and resets in-memory auction state.
- `/garageloot` — scans the Forge item registry and reports discovered mod namespaces/items.
- `/garagejoin <id>` — join an auction session by numeric garage id.
- `/rate100 <amount>` — bid in the active auction.
- `/arenajoin <0..2>` — register for an arena session.
- `/garagebalance` — show the player's balance.
- `/mystorage` — retrieve the most recent saved inventory snapshot (temporary implementation; not yet a persistent room GUI).
- `/mystorageleave` — placeholder exit command.

## Current implementation status — read before use

This is an **in-progress development build**, not a finished gameplay release. Implemented so far: procedural market/arena shell generation, registry-based item discovery, namespace-first loot selection, heuristic complete armor-set grouping, basic in-memory auction/bid timer state, basic arena registration/countdown/death tracking, and initial storage snapshot handling.

Not yet implemented or not yet production-safe: persistent SavedData across restarts, sign-click registration and winner signage, actual garage door unlocking/loot ownership, correct arena boundary/spawn management, robust multiplayer disconnect handling, complete death/inventory recovery and anti-duplication, physical personal storage rooms with multiple accessible snapshots, per-language message localization, reliable money reset/forced arena flow, TaCZ pack/NBT gun integration, vehicle-specific loot adapters, and full clear-structure ownership tracking.

The registry scanner can discover ordinary registered items from all installed mods at runtime. That does **not** guarantee every modded weapon/vehicle is usable: mods that encode content in item NBT, datapacks, or custom capability systems need dedicated adapters. Armor-set grouping is heuristic and will need per-mod refinement for unusual naming schemes.

No in-game test has been performed in this environment. A successful CI build only confirms compilation; it does not certify gameplay. Do not use this build on an important world without a backup.
