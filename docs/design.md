# 設計書 - Cookingゲーム（ダンジョン編）

## 更新履歴
| 日付 | 更新内容 | Claudeの意見 |
|------|----------|--------------|
| 2025-01-08 | 初版作成 - 基本システム設計を定義 | MVCパターンを採用し、各システムを疎結合に設計することで、将来的な機能追加や変更に対応しやすい構造にしています。簡略版でも拡張性を考慮した設計が重要だと考えます。 |

## 1. システム構成

### 1.1 アーキテクチャ概要
```
┌─────────────────┐
│  UIレイヤー      │ ← Unity UI (Canvas)
├─────────────────┤
│  ゲームロジック   │ ← C# Scripts
├─────────────────┤
│  データ管理      │ ← ScriptableObject
└─────────────────┘
```

### 1.2 主要コンポーネント

#### GameManager
- ゲーム全体の進行管理
- シーン遷移制御
- ゲーム状態管理（メニュー、マップ、バトル、ゲームオーバー）

#### MapManager
- マップの生成と表示
- ノード間の接続管理
- プレイヤーの現在位置管理

#### BattleManager
- バトルの進行管理
- ターン制御
- 勝敗判定

#### CardManager
- 手札の管理
- デッキのシャッフル
- カードの配布と破棄

#### PlayerData
- HP、最大HP
- 現在のデッキ
- 所持金
- バフ・デバフ状態

## 2. 画面設計

### 2.1 マップ画面
- ノード形式のマップ表示
- 現在位置のハイライト
- 選択可能な次のノードの表示

### 2.2 バトル画面
```
┌─────────────────────────────┐
│         敵エリア             │
│    [敵キャラ] [意図表示]      │
├─────────────────────────────┤
│         バトルフィールド       │
├─────────────────────────────┤
│    [手札エリア]              │
│ [カード1][カード2][カード3]... │
├─────────────────────────────┤
│ HP: XX/XX  エナジー: X/X     │
└─────────────────────────────┘
```

### 2.3 報酬画面
- カード選択（3枚から1枚選択）
- 獲得金額表示
- スキップオプション

## 3. データ設計

### 3.1 カードデータ (ScriptableObject)
```csharp
- cardID: string
- cardName: string
- cost: int
- cardType: enum (Attack, Skill, Power)
- effectValue: int
- description: string
- sprite: Sprite
```

### 3.2 敵データ (ScriptableObject)
```csharp
- enemyID: string
- enemyName: string
- maxHP: int
- attackPatterns: List<AttackPattern>
- sprite: Sprite
```

### 3.3 ノードデータ
```csharp
- nodeType: enum
- position: Vector2
- connectedNodes: List<Node>
- isVisited: bool
```

## 4. 実装優先順位

1. **フェーズ1**: 基本バトルシステム
   - カード表示と選択
   - ダメージ計算
   - ターン進行

2. **フェーズ2**: マップシステム
   - マップ生成
   - ノード選択と移動

3. **フェーズ3**: デッキ構築要素
   - 報酬システム
   - カード追加・除去

4. **フェーズ4**: 追加要素
   - ショップ
   - イベント
   - 複数の敵パターン

## 5. 技術仕様

### 使用アセット（想定）
- Unity 2022.3 LTS
- TextMeshPro（テキスト表示）
- DOTween（アニメーション）※任意

### プロジェクト構造
```
Assets/
├── Scripts/
│   ├── Managers/
│   ├── Battle/
│   ├── Map/
│   ├── Cards/
│   └── UI/
├── Prefabs/
├── ScriptableObjects/
│   ├── Cards/
│   └── Enemies/
├── Sprites/
└── Scenes/
```