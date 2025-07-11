# スクリプト設定ガイド

## 概要
プロトタイプ版の3つのスクリプトをUnityオブジェクトに適用し、動作させるための設定手順書です。

## 前提条件
- BattleSceneが作成されている
- UI要素（Card、Enemy、VictoryPanel）が配置されている
- 3つのスクリプトファイルが`Assets/Scripts/Battle/`に配置されている

## 1. PrototypeCard.csの設定

### 1.1 スクリプトの適用
1. HierarchyでCard（カード画像）を選択
2. Inspector → Add Component → Scripts → PrototypeCard
3. スクリプトがアタッチされることを確認

### 1.2 必要なコンポーネントの追加
1. Cardオブジェクトに以下を追加（存在しない場合）：
   - Image コンポーネント（既に存在するはず）
   - Text コンポーネント（子要素として追加）
   - CanvasGroup コンポーネント（自動追加される）

### 1.3 設定値の調整
Inspectorで以下を設定：
- **Damage**: 6（デフォルト値）
- **Card Name**: "基本攻撃"
- **Card Image**: CardオブジェクトのImageコンポーネントをドラッグ
- **Card Text**: 子要素のTextコンポーネントをドラッグ
- **Canvas**: 自動取得されるが、必要に応じて手動設定
- **Raycaster**: 自動取得されるが、必要に応じて手動設定

## 2. PrototypeEnemy.csの設定

### 2.1 スクリプトの適用
1. HierarchyでEnemy（敵画像）を選択
2. Inspector → Add Component → Scripts → PrototypeEnemy
3. スクリプトがアタッチされることを確認

### 2.2 設定値の調整
Inspectorで以下を設定：
- **Max HP**: 20（デフォルト値）
- **Current HP**: 20（デフォルト値）
- **Enemy Name**: "スライム"
- **HP Text**: 子要素のHPTextコンポーネントをドラッグ
- **Enemy Image**: EnemyオブジェクトのImageコンポーネントをドラッグ
- **Battle Manager**: 自動取得されるが、必要に応じて手動設定

## 3. PrototypeBattleManager.csの設定

### 3.1 空のGameObjectの作成
1. Hierarchy → 右クリック → Create Empty
2. 名前を"BattleManager"に変更

### 3.2 スクリプトの適用
1. BattleManagerオブジェクトを選択
2. Inspector → Add Component → Scripts → PrototypeBattleManager
3. スクリプトがアタッチされることを確認

### 3.3 設定値の調整
Inspectorで以下を設定：
- **Victory Panel**: VictoryPanelオブジェクトをドラッグ
- **Victory Text**: VictoryPanel内のTextコンポーネントをドラッグ
- **Restart Button**: 必要に応じて追加（オプション）
- **Cards**: Cardオブジェクトを配列に追加（サイズ1に設定してCardをドラッグ）
- **Enemies**: Enemyオブジェクトを配列に追加（サイズ1に設定してEnemyをドラッグ）

## 4. 動作確認

### 4.1 基本動作のテスト
1. Play ボタンを押してシーンを実行
2. Consoleウィンドウを開いて初期化ログを確認
3. カードをドラッグしてスライムにドロップ
4. ダメージが入りHPが減ることを確認
5. スライムのHPが0になったら勝利パネルが表示されることを確認

### 4.2 トラブルシューティング

#### カードがドラッグできない場合
- CardオブジェクトにGraphic Raycasterがアタッチされているか確認
- CanvasにGraphic Raycasterコンポーネントがあるか確認
- Event Systemがシーンに存在するか確認

#### ダメージが入らない場合
- Console でエラーメッセージを確認
- PrototypeCard の GetDropTarget() メソッドがEnemyを検出しているか確認
- EnemyオブジェクトにPrototypeEnemyスクリプトがアタッチされているか確認

#### 勝利パネルが表示されない場合
- VictoryPanel オブジェクトがBattleManagerに正しく設定されているか確認
- VictoryPanel が初期状態で非アクティブになっているか確認

## 5. デバッグ機能

### 5.1 Context Menu機能
BattleManagerオブジェクトを選択し、Inspectorの右上の「…」メニューから：
- **Debug - Instant Victory**: 即座に勝利
- **Debug - Set All Enemies HP to 1**: 全敵のHPを1に設定

### 5.2 ログ出力
Console ウィンドウで以下のログを確認：
- "カード初期化完了"
- "エネミー初期化完了"
- "バトル初期化完了"
- "ドラッグ開始"
- "ダメージ処理"
- "勝利!"

## 6. 完了基準

以下の動作が確認できればスプリント0完了：
- [ ] カードがドラッグできる
- [ ] スライムにドロップするとダメージが入る
- [ ] HPが表示され、ダメージに応じて減少する
- [ ] スライムのHPが0になると勝利パネルが表示される
- [ ] Console にエラーが出ていない

## 7. 次のステップ

プロトタイプが完成したら、スプリント1へ進む：
- エナジーシステムの実装
- 複数カードの手札管理
- ターン制の実装
- ScriptableObjectを使用したカードデータ管理