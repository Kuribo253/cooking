# 設計書 - Cookingゲーム（ダンジョン編）

## 更新履歴
| 日付 | 更新内容 | Claudeの意見 |
|------|----------|--------------|
| 2025-01-08 | 初版作成 - 基本システム設計を定義 | MVCパターンを採用し、各システムを疎結合に設計することで、将来的な機能追加や変更に対応しやすい構造にしています。簡略版でも拡張性を考慮した設計が重要だと考えます。 |
| 2025-01-08 | スプリント0の最小構成を追加 | プロトタイプ段階では複雑な設計パターンを避け、動作確認を優先。後のリファクタリングで構造化を進める方針が効率的です。 |

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

## 6. スプリント0：最小構成設計

### 6.1 プロトタイプの目的
- Unity環境での基本的な操作確認
- カードのドラッグ＆ドロップ実装の検証
- ダメージ計算ロジックの動作確認

### 6.2 実装クラス（最小限）

#### PrototypeCard.cs
```csharp
- damage: int = 6（固定値）
- OnBeginDrag()
- OnDrag()
- OnEndDrag()
```

#### PrototypeEnemy.cs
```csharp
- currentHP: int = 20（固定値）
- maxHP: int = 20
- TakeDamage(int damage)
- UpdateHPDisplay()
```

#### PrototypeBattleManager.cs
```csharp
- CheckVictory()
- ShowVictoryMessage()
```

### 6.3 シーン構成
- BattleScene
  - Canvas
    - EnemyArea（敵表示エリア）
    - CardArea（カード表示エリア）
    - VictoryPanel（勝利時表示）

### 6.4 操作フロー
1. シーン開始時、カード1枚と敵1体が表示される
2. カードをドラッグして敵にドロップ
3. 敵にダメージが入り、HP表示が更新
4. HPが0になったら勝利メッセージ表示

### 6.5 プロトタイプで実装しないもの
- エナジーシステム
- ターン制
- 複数カード
- アニメーション
- 音響効果
- セーブ/ロード