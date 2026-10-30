# LOTWORKS — 技術構成メモ v0.1

## 確定技術
- Godot 4.x、初期はGDScript。
- 2D / Controlを中心とするUI。
- まだバックエンドは採用していない。

## フォルダ構成
- `scenes/main/`: 初期起動シーン。
- `scenes/workshop/`, `scenes/auction/`, `scenes/inventory/`: 今後のUIシーン用。
- `scripts/core/`: アプリケーションの共通処理。
- `scripts/domain/items/`: アイテム定義・個体・加工規則。
- `scripts/domain/auctions/`: 出品スナップショット・入札・競売解決。
- `scripts/domain/workshop/`: 店舗経営・生産。
- `scripts/ui/`: UIとドメインを接続するコード。
- `data/items/`, `data/recipes/`, `data/venues/`: 調整可能な定義データ。
- `assets/`: art、audio、fonts。
- `tests/`: unit、integration、fixtures。
- `tools/`, `addons/`: 開発ツール / Godot拡張。
- `docs/`: 企画、仕様、決定ログ、研究資料。

## ドメイン境界（採用候補）
```text
UI (Godot Control)
  -> Commands (inspect / transform / list / acquire / settle)
  -> Deterministic domain rules
     -> ItemDefinition + ItemInstance
     -> Inventory and workshop state (per player)
     -> AuctionListingSnapshot (reusable, immutable)
     -> BuyerAcquisition (new item instance per buyer)
     -> SellerSettlement (at most one payout per listing)
  -> Persistence adapter (local first; service later if needed)
```

### 設計上の注意
- UIが在庫・資金の状態を直接、複数箇所から変更する構造を避ける。
- 元の出品商品と購入者に生成される個体のIDを混同しない。
- ネットワークが未導入でもドメインルールの入力/出力をテストできるようにする。
- サーバー実装時には競売の整合性と冪等な決済をサーバー側で検証する。
- Godot上の大規模な共通経済シミュレーションは必要としない。
- 現時点では「将来の境界の案」であり、クラスやAPIの実装確定ではない。

## 初期起動
`project.godot` → `scenes/main/main.tscn`。タイトルと「未実装」を表示するだけ。
