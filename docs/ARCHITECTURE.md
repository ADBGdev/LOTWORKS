# LOTWORKS — 技術構成メモ v0.2

更新: 2026-10-31 / エンジンと骨格は維持。持ち込み・使用・消費のデータ境界を追加。

## 確定技術
- Godot 4.x、初期はGDScript。
- 2D / Controlを中心とするUI。
- まだバックエンド、オンラインサービス、競売ルールは採用していない。

## リポジトリ内の配置
- `scenes/main/`: 最小起動シーン。
- `scenes/workshop/`, `scenes/auction/`, `scenes/inventory/`: 準備・競売・在庫のUI。
- `scripts/core/`: 共通処理。
- `scripts/domain/items/`: 定義、個体、数量、利用と消費。
- `scripts/domain/auctions/`: 出品スナップショット、入札、競合、競売解決。
- `scripts/domain/workshop/`: 独立した拠点経済。
- `scripts/ui/`: UIとドメイン処理の接続。
- `data/items/`, `data/recipes/`, `data/venues/`: 調整用データ。
- `assets/`, `tests/`, `tools/`, `addons/`: 各種素材・テスト・ツール。

## ドメインの区分案（実装未確定）
```text
Godot Control UI
    -> Commands:
       select_loadout / enter_auction / use_consumable
       inspect / bid / acquire / list / settle / return_home
    -> Deterministic domain rules
       Inventory and workshop state (per player)
       ItemDefinition + ItemInstance
       AuctionLoadout + ConsumableUseEvent
       AuctionListingSnapshot (immutable/reusable)
       AuctionEncounter (buyer-specific, other-player data)
       BuyerAcquisition (distinct instance per buyer)
       SellerSettlement (single seller payout per listing)
    -> Persistence adapters (local prototype -> service only if needed)
```

### 基本整合性
- **持ち込みは消費ではない。** 所有物のうち使用可能なものを選ぶ状態遷移として扱う。
- **使用は消費を伴う。** アイテム効果・消費・再試行を一意の操作として検証できる構成にする。
- 未使用品の帰還、消耗品の不発時処理、戦利品の没収は未決定。仮実装を本採用と見なさない。
- 出品は元個体を消費し、不変のlistingスナップショットを登録。出品決済と使用消費は別処理。
- 出品者の一出品一報酬、購入者ごとの独立生成、二重処理防止を保つ。
- UIから複数箇所で資金や所持数を直接変更しない。
- 競合の人間由来データとNPCデータを区別できるようにする。
- アーキテクチャはプロトタイプで検証してから固定。不要な汎用基盤は作らない。

## 初期起動
`project.godot` -> `scenes/main/main.tscn`。タイトルのみ表示。ゲーム処理は未実装。
