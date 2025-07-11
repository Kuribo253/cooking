# Unityプロジェクト構築ガイド

## 1. プロジェクトフォルダ構成

Unityプロジェクト内で以下のフォルダ構成を作成してください：

```
Assets/
├── Scripts/           # C#スクリプト
│   ├── Battle/       # バトル関連
│   └── UI/           # UI関連
├── Prefabs/          # プレハブ
├── Sprites/          # 画像素材
│   ├── Background/   # 背景画像
│   ├── Cards/        # カード画像
│   ├── Enemies/      # 敵画像
│   ├── UI/           # UI用画像（将来的に）
│   └── Characters/   # キャラクター画像（将来的に）
├── Scenes/           # シーンファイル
└── Materials/        # マテリアル（必要に応じて）
```

## 2. シーン作成手順

### 2.1 BattleSceneの作成
1. File → New Scene
2. File → Save As... → "BattleScene"として保存
3. ScenesフォルダにBattleScene.unityが作成される

### 2.2 UI配置手順

#### Canvas作成
1. Hierarchy → 右クリック → UI → Canvas
2. CanvasのRender Mode: Screen Space - Overlay
3. Canvas Scaler設定:
   - UI Scale Mode: Scale With Screen Size
   - Reference Resolution: 1920 x 1080

#### UI要素の配置
1. **EnemyArea（敵表示エリア）**
   - Canvas右クリック → Create Empty
   - 名前を"EnemyArea"に変更
   - Rect Transform設定:
     - Anchor: Top Center
     - Pos Y: -200
     - Width: 400, Height: 400

2. **CardArea（カード表示エリア）**
   - Canvas右クリック → Create Empty
   - 名前を"CardArea"に変更
   - Rect Transform設定:
     - Anchor: Bottom Center
     - Pos Y: 150
     - Width: 200, Height: 300

3. **VictoryPanel（勝利画面）**
   - Canvas右クリック → UI → Panel
   - 名前を"VictoryPanel"に変更
   
   **非アクティブ化の手順：**
   - HierarchyでVictoryPanelを選択
   - Inspectorの名前欄の左側にあるチェックボックスをオフにする
   - または、VictoryPanelを右クリック → Active → チェックを外す
   
   **子要素としてText追加：**
   - VictoryPanelを右クリック → UI → Text - TextMeshPro
   - 名前を"VictoryText"に変更
   - Text欄に"Victory!"と入力
   - Font Size: 48
   - Alignment: Center and Middle
   - Color: 白または目立つ色に設定

## 3. 画像素材の準備と配置

### 3.1 画像ファイルの配置
以下の画像ファイルをUnityプロジェクトに配置します：

1. **カード画像の配置**
   - `C:\dev\cooking\claude\画像提供\カード画像\` から以下のファイルをコピー
   - `基本攻撃.png` → `Assets/Sprites/Cards/`
   - `基本防御.png` → `Assets/Sprites/Cards/`
   - `木の実.png` → `Assets/Sprites/Cards/`

2. **敵画像の配置**
   - `C:\dev\cooking\claude\画像提供\敵画像\` から以下のファイルをコピー
   - `スライム.jpg` → `Assets/Sprites/Enemies/`

3. **背景画像の配置**
   - `C:\dev\cooking\claude\画像提供\` から以下のファイルをコピー
   - `戦闘背景.png` → `Assets/Sprites/Background/`

### 3.2 画像のインポート設定
1. Projectウィンドウで配置した画像を選択
2. Inspectorで以下を設定：
   - Texture Type: Sprite (2D and UI)
   - Pixels Per Unit: 100
   - Filter Mode: Point (no filter)
   - Compression: None

### 3.3 背景画像の配置
1. Hierarchy → 右クリック → UI → Image
2. 名前を"Background"に変更
3. **背景を最背面に配置する手順：**
   - HierarchyでBackgroundをドラッグ
   - Canvasの子要素の中で一番上（最初）の位置にドロップ
   - 結果：Canvas → Background → 他のUI要素 の順序になる
   - ※Hierarchyでは上にあるほど背面に描画される
4. Rect Transform設定:
   - Anchor: Stretch（四隅を選択）
   - Left/Top/Right/Bottom: 0
5. Image Component:
   - Source Image: 戦闘背景.png を設定

### 3.4 カード画像の適用
1. Hierarchy → 右クリック → UI → Image
2. CardAreaの子要素として配置
3. 名前を"Card"に変更
4. Image Component:
   - Source Image: 基本攻撃.png を設定
5. サイズ: 150 x 150（正方形の画像に合わせて調整）

### 3.5 敵画像の適用
1. Hierarchy → 右クリック → UI → Image
2. EnemyAreaの子要素として配置
3. 名前を"Enemy"に変更
4. Image Component:
   - Source Image: スライム.jpg を設定
5. サイズ: 200 x 200

### 3.6 HP表示
1. 敵画像の子要素としてText追加
   - Enemy右クリック → UI → Text - TextMeshPro
   - 名前を"HPText"に変更
2. **簡単な設定方法：**
   - Text Input: "HP: 20/20"と入力
   - Font Size: 24
   - Vertex Color: 白色に設定
   - Font Asset: **Arial SDF**を選択（LiberationSans SDFの代わりに）
3. **確実に表示させる方法：**
   - 右側のInspectorでTextMeshPro - Text (UI)を探す
   - Main Settingsセクションで：
     - Font Asset: Arial SDF を選択
     - Font Size: 24
     - Vertex Color: 白色（255, 255, 255, 255）
   - Extra Settingsセクションで：
     - Outline: チェックを入れる
     - Outline Color: 黒色に設定
     - Outline Width: 0.2
4. 位置調整:
   - Rect Transform: 敵画像の下部に配置
   - Anchor: Bottom Center
   - Width: 150, Height: 50

## 4. 次のステップ

これらの準備が完了したら、Scripts/Battle/フォルダに以下のスクリプトを作成：
- PrototypeCard.cs
- PrototypeEnemy.cs
- PrototypeBattleManager.cs

## 注意事項
- プロトタイプ段階では見た目は気にしない
- まずは動作確認を優先
- エラーが出たら基本的な設定を確認