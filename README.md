# LOTWORKS

**Inventory-based workshop management × asynchronous auction PvP**  
Status: design revision / Godot 4.x scaffold (2026-10-31)

LOTWORKSは、独立した経済を持つ競合業者が、非同期オークションを主な仕入れ先にして、商品を鑑定・加工・売買するインベントリベースの経営ゲーム企画です。

**現在の検証方向:** 拠点で蓄積したアイテムをオークション会場へ持ち込み、**対戦中に使って消費する**。これにより、入札資金だけでなく、用意した消耗品も勝負のコストになります。小さな画面のままエクストラクション的な緊張と対人の駆け引きを追求します。ただし、**戦利品ロストや撤退失敗の方式は未決定**で、実装済みではありません。

## Core constraints

- **Workshop / inventory:** safe base for appraisal, limited repair or processing, storage and sale; larger manufacturing systems are later candidates.
- **Bring and consume:** bring owned items from home to the auction session, **use them for an effect and consume them**. Effects, loadout limits and encounter rules are not yet fixed.
- **Auctions (asynchronous PvP):** player-generated listings and potentially recorded competitor decisions; no simultaneous login requirement.
- **Independent economies:** no global shared demand or live shared marketplace.
- **Reusable listing snapshots:** listing removes an item from the seller's inventory; other players can encounter copies of that saved listing independently.
- **Exactly one seller payout per listing:** later buyers do not pay the seller again. Payout timing remains undecided.
- **Venues:** flea market first; materials and machinery auction venues are expansion candidates.
- **Risks:** spent consumables and purchase costs are meaningful even on failure; whether/how already acquired goods can be lost is still an open design problem.

This repository is a Godot project scaffold and design documents, **not yet a playable MVP**.

## Run

1. Install Godot **4.x** (standard editor).
2. Clone the repository and import `project.godot` in Godot Project Manager.
3. Run (F5) to display the placeholder scene.

## Design documentation

- [Current game design](docs/GAME_DESIGN.md)
- [Current auction / session and risk design](docs/SESSION_DESIGN.md)
- [Auction listing data invariants](docs/AUCTION_DESIGN.md)
- [MVP validation plan](docs/MVP_SCOPE.md)
- [Decision log](docs/DECISIONS.md)
- [Architecture notes](docs/ARCHITECTURE.md)
- [Agent rules](AGENTS.md)

No third-party dependencies, online services, or game assets are required to open the starter scene.
