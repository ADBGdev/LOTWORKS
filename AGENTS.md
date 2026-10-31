# LOTWORKS — Agent / contributor instructions

## Project and priorities
- Engine: **Godot 4.x**, 2D / Control-centric UI, initial language GDScript.
- Solo-indie feasibility, small system count, and a compelling repeatable interaction take priority over an expansive simulation.
- Read `docs/DECISIONS.md`, `docs/GAME_DESIGN.md`, `docs/SESSION_DESIGN.md`, `docs/AUCTION_DESIGN.md`, and `docs/MVP_SCOPE.md` before revising game rules.
- Maintain distinct statuses: **confirmed user constraints**, **design direction**, **illustrative proposals**, **open questions**. Do not silently promote a suggestion to a settled rule.

## Agreed design constraints
1. Individual players have mostly **independent** workshop economies. Global shared demand is not the PvP core.
2. The auction is the principal potential procurement interface, with other auction venues planned as optional expansions.
3. **Players bring their own inventory items to an auction, actively use them there, and consume them on use.** The focus is on consumable tactical choices, not permanent equipment or automatic collateral.
4. Items used in the auction have an actual opportunity cost regardless of winning a lot. Specific effects (appraisal, intel, interference, defense) are **examples only**.
5. Listing consumes the seller's item **immediately**; server keeps its immutable listing snapshot.
6. The same snapshot may be encountered/acquired by different players independently.
7. Seller gets **one payout per listing only**, regardless of repeated purchases. Payout trigger is not settled.
8. No real-time connection or global single-owner item transfer is required for encounters.
9. The desired experience has higher PvP presence and **extraction-style tension**, but **loot loss, withdrawal, session failure and risk escalation are not defined yet**. Do not invent them as agreed mechanics.
10. No return to dungeon/ecosystem subsystems in current MVP; simplify rather than add extra game modes.

## Engineering boundaries
- Separate item definition, owned instance, brought loadout, item consumption event, reusable listing snapshot, buyer acquisition, and seller settlement.
- Only a successful deliberate **use** consumes a consumable, subject to future explicit rules. Do not implement implicit loss of every brought item.
- Keep deterministic, testable state transitions. No LLM arbitrator for item effects or auction outcomes.
- Model server-facing operations with idempotent consume/list/acquire/settle boundaries; avoid duplicate charges and payouts.
- No backend, unnecessary dependencies, generated art, advanced crafting simulation or unrelated mechanics before a focused prototype proves the core.
- Do not interpret auction session = conventional extraction raid as an already established rule.

## Workflow
1. Read latest design documents.
2. Make the smallest coherent change and keep decisions and design docs synchronized.
3. Validate a Godot import/headless run if the engine is available; otherwise clearly mark untested.
4. Add focused deterministic tests when introducing business logic.
5. Never commit `.godot/`, runtime saves, credentials or machine-local files.
6. Paths in ASCII; gameplay docs in Japanese.

## Current technical state
Godot starter screen only. No playable auction, consumable items, PvP or extraction mechanics yet.
