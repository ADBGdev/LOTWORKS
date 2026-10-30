# LOTWORKS — Agent / contributor instructions

## Project and priorities
- Engine: **Godot 4.x**, 2D / Control-centric interface, prefer GDScript for initial prototypes.
- Solo-indie feasibility and a compelling, repeatable core interaction are more important than visual scope or elaborate architecture.
- Authoritative design references are `docs/GAME_DESIGN.md`, `docs/AUCTION_DESIGN.md`, `docs/MVP_SCOPE.md`, and `docs/DECISIONS.md`.
- Distinguish **agreed constraints** from **proposals** and **open decisions**. Do not silently settle an open decision.

## Non-negotiable game constraints (current)
1. Each player operates a mostly independent local economy. Do not introduce a global synchronized market by default.
2. Primary procurement may be through auctions, with local processing, crafting, repair and inventory management as the main single-player loop.
3. On listing, an item leaves the seller's inventory immediately.
4. The server retains a listing **snapshot**, which may participate in multiple independent buyers' auction experiences.
5. **One listing gives the seller at most one payout.** Replays/purchases never pay the seller again. The exact settlement trigger is undecided.
6. No simultaneous player presence is required; normal auctions must work asynchronously.
7. Do not implement global demand-capture competition as the central PvP mode.
8. Multiple venues (flea market, materials, machinery) are planned; only flea market is required by the first MVP.
9. Product misrepresentation, advanced inspections, bid policies and anti-abuse details remain proposals; do not treat them as confirmed production mechanics.

## Engineering boundaries
- Keep items, inventory, auction listing snapshots, and financial settlement as separate domain concepts.
- Use deterministic, testable business rules for item transformation and auction resolution. Avoid making an LLM an economic arbiter.
- Never equate reusable listing data with transferable ownership of a unique item.
- Ensure payout **exactly once** and distinguish `listing_id` from `buyer_instance_id` in any future persistence layer.
- Do not add a backend, plugins, third-party dependencies, online services, or generated art without a clear MVP need.
- Keep initial code small; prefer one working vertical slice over broad speculative systems.

## Workflow
1. Read design/decision docs before modifying game rules.
2. Make the smallest coherent change and update affected docs.
3. Validate Godot import / headless run if Godot is available. If unavailable, state that explicitly; never claim testing succeeded.
4. Add focused tests for deterministic domain rules when implementing them.
5. Never commit machine-local cache (`.godot/`), secrets, or user save data.
6. Keep file and directory names in ASCII; write game design docs in Japanese.

## Definition of first milestone
A Godot 4 project that opens and shows a starter screen. **This scaffold is not a functional auction MVP.**
