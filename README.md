# LOTWORKS

**Inventory-based workshop management × asynchronous auction PvP**  
Status: pre-production / Godot 4.x scaffold (2026-10-30)

LOTWORKS is a prototype-oriented indie game project. Each player runs an independent workshop economy: acquire items primarily through asynchronous auctions, inspect and process them, use them for production, or relist them.

## Core premise

- **Workshop (PvE):** inspect, repair, dismantle, process, craft, manage inventory and equipment.
- **Auctions (asynchronous PvP):** competitors create listings; other players assess their value and bid independently.
- **Independent economies:** there is no requirement for a global shared economy or simultaneous online presence.
- **Reusable listing snapshots:** publishing removes one item from its seller's inventory. The server retains a snapshot that may be presented to different buyers more than once.
- **Exactly one seller payout per listing:** subsequent purchases of the saved snapshot do not generate further seller income.
- **Auction venues:** begin with a flea market, with materials and machinery auctions as potential expansion.

This repository contains a minimal Godot project and design documents, **not a playable MVP yet**.

## Start in Godot

1. Install Godot **4.x** (standard desktop editor).
2. Clone this repository.
3. In Godot Project Manager, import `project.godot`.
4. Run the project (F5). The starter scene displays the project title.

## Documents

- [Game design](docs/GAME_DESIGN.md)
- [Auction design and invariants](docs/AUCTION_DESIGN.md)
- [MVP scope](docs/MVP_SCOPE.md)
- [Architecture notes](docs/ARCHITECTURE.md)
- [Decisions / open questions](docs/DECISIONS.md)
- [Contributor / AI agent rules](AGENTS.md)

## Scope

The first slice tests whether appraisal, value improvement, and auction-based purchasing are compelling. Multiplayer synchronization, a live shared marketplace, advanced manufacturing simulation, and complex visuals are intentionally excluded from the initial scaffold.

No external dependencies, services, or game assets are required to open the starter scene.
