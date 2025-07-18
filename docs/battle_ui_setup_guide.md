# バトルシーンUI改善手順書

## 概要
参考画像に基づいてバトルシーンの見た目を改善し、TcgEngineの画像リソースを活用してプロフェッショナルな外観にします。

## 前提条件
- BattleSceneが作成済み
- TcgEngineから画像リソースがコピー済み
- 基本的なプロトタイプが動作している

---

## 1. 画像インポート設定

### 1.1 新しい画像ファイルの設定
1. **Projectウィンドウで以下の画像を順番に選択**
   - `Assets/Sprites/Cards/fire_sword.png`
   - `Assets/Sprites/Cards/shield.png`
   - `Assets/Sprites/Enemies/frog.png`
   - `Assets/Sprites/UI/mana_full.png`
   - `Assets/Sprites/UI/mana_empty.png`
   - `Assets/Sprites/UI/button_endturn.png`
   - `Assets/Sprites/UI/quantity_bar.png`
   - `Assets/Sprites/UI/quantity_bar2.png`

2. **各画像のInspector設定**
   - **Texture Type**: Sprite (2D and UI)
   - **Pixels Per Unit**: 100
   - **Filter Mode**: Point (no filter)
   - **Compression**: None
   - **Apply**ボタンをクリック

---

## 2. カード画像の変更

### 2.1 基本攻撃カードの画像変更
1. **Hierarchyで「Card」オブジェクトを選択**
2. **Inspector → Image Component → Source Image**
3. **現在の「基本攻撃.png」から「fire_sword.png」に変更**
4. **カードのサイズ調整**（必要に応じて）
   - Width: 150
   - Height: 200

### 2.2 防御カードの追加（オプション）
1. **Cardオブジェクトを複製**
   - Hierarchy → Card → 右クリック → Duplicate
   - 名前を「DefenseCard」に変更
2. **Image Component → Source Image**
   - 「shield.png」に設定
3. **位置調整**
   - CardAreaの右側に配置

---

## 3. 敵画像の変更

### 3.1 スライムから青いカエルに変更
1. **Hierarchyで「Enemy」オブジェクトを選択**
2. **Inspector → Image Component → Source Image**
3. **現在の「スライム.jpg」から「frog.png」に変更**
4. **敵のサイズ調整**
   - Width: 180
   - Height: 180
5. **色調整（オプション）**
   - Color: 少し青みがかった色に調整

---

## 4. エナジー表示エリアの追加

### 4.1 エナジーエリアの作成
1. **Canvas → 右クリック → Create Empty**
2. **名前を「EnergyArea」に変更**
3. **Rect Transform設定**
   - Anchor: Bottom Left
   - Pos X: 80
   - Pos Y: 80
   - Width: 120
   - Height: 60

### 4.2 エナジーアイコンの追加
1. **EnergyArea → 右クリック → UI → Image**
2. **名前を「EnergyIcon1」に変更**
3. **Image Component設定**
   - Source Image: mana_full.png
   - Width: 40
   - Height: 40
4. **Position設定**
   - Pos X: -30
   - Pos Y: 0

### 4.3 複数エナジーアイコンの作成
1. **EnergyIcon1を複製 × 2回**
   - EnergyIcon2（Pos X: 0）
   - EnergyIcon3（Pos X: 30）
2. **EnergyIcon2のImage**
   - Source Image: mana_full.png
3. **EnergyIcon3のImage**
   - Source Image: mana_full.png

### 4.4 エナジーテキストの追加
1. **EnergyArea → 右クリック → UI → Text - TextMeshPro**
2. **名前を「EnergyText」に変更**
3. **TextMeshPro設定**
   - Text: "3/3"
   - Font Size: 18
   - Color: 白色
   - Alignment: Center
4. **Position設定**
   - Pos Y: -25

---

## 5. HPバーの改善

### 5.1 HPバー背景の追加
1. **Enemy → 右クリック → UI → Image**
2. **名前を「HPBarBackground」に変更**
3. **Image Component設定**
   - Source Image: quantity_bar2.png
   - Color: 暗い灰色 (100, 100, 100, 255)
4. **Position設定**
   - Pos Y: 120
   - Width: 150
   - Height: 20

### 5.2 HPバー前景の追加
1. **HPBarBackground → 右クリック → UI → Image**
2. **名前を「HPBarForeground」に変更**
3. **Image Component設定**
   - Source Image: quantity_bar.png
   - Color: 赤色 (255, 50, 50, 255)
   - Image Type: Filled
   - Fill Method: Horizontal
4. **Position設定**
   - Stretch to fill parent
   - Left/Top/Right/Bottom: 2（枠の内側に配置）

### 5.3 HPテキストの調整
1. **既存の「HPText」を選択**
2. **Position調整**
   - HPBarBackgroundの上に配置
   - Pos Y: 140
3. **TextMeshPro設定調整**
   - Font Size: 16
   - Color: 白色
   - Outline: 黒色（Width: 0.3）

---

## 6. ターン終了ボタンの追加

### 6.1 ターン終了ボタンの作成
1. **Canvas → 右クリック → UI → Button - TextMeshPro**
2. **名前を「EndTurnButton」に変更**
3. **Rect Transform設定**
   - Anchor: Bottom Right
   - Pos X: -80
   - Pos Y: 80
   - Width: 120
   - Height: 50

### 6.2 ボタン画像の設定
1. **Image Component設定**
   - Source Image: button_endturn.png
   - Image Type: Sliced（必要に応じて）
2. **Color設定**
   - Normal: 白色
   - Highlighted: 薄い青色
   - Pressed: 濃い青色

### 6.3 ボタンテキストの設定
1. **EndTurnButton → Text (TMP) を選択**
2. **TextMeshPro設定**
   - Text: "ターン終了"
   - Font Size: 16
   - Color: 白色
   - Alignment: Center and Middle

---

## 7. レイアウト最終調整

### 7.1 全体のレイアウト確認
1. **Game View でレイアウトを確認**
2. **参考画像と比較して位置調整**

### 7.2 位置の微調整
- **CardArea**: 下部中央
- **EnemyArea**: 中央上部
- **EnergyArea**: 左下
- **EndTurnButton**: 右下

### 7.3 階層順序の調整
1. **Hierarchy で要素の順序を調整**
2. **UI要素が背景より前面に表示されることを確認**

---

## 8. 動作確認

### 8.1 基本動作テスト
1. **Play ボタンで実行**
2. **以下を確認**
   - カード画像が正しく表示される
   - 敵画像（青いカエル）が表示される
   - エナジーアイコンが表示される
   - HPバーが表示される
   - ターン終了ボタンが表示される

### 8.2 ドラッグ＆ドロップテスト
1. **カードをドラッグして敵にドロップ**
2. **ダメージが正常に入ることを確認**
3. **HP表示が更新されることを確認**

---

## 9. トラブルシューティング

### 9.1 画像が表示されない場合
- 画像のインポート設定を確認
- Sprite (2D and UI) に設定されているか確認
- パスが正しいか確認

### 9.2 UI要素が正しく配置されない場合
- Anchor設定を確認
- Parent-Child関係を確認
- Canvas Scaler設定を確認

### 9.3 ボタンが機能しない場合
- Button Componentが正しくアタッチされているか確認
- Event System が存在するか確認

---

## 10. 完了基準

以下がすべて確認できれば作業完了：
- [ ] カードが新しい画像（fire_sword.png）で表示される
- [ ] 敵が青いカエル（frog.png）で表示される
- [ ] エナジー表示（3/3）が左下に表示される
- [ ] HPバーが敵の上部に表示される
- [ ] ターン終了ボタンが右下に表示される
- [ ] ドラッグ&ドロップが正常に動作する
- [ ] 全体のレイアウトが参考画像に近い

---

## 11. 次のステップ

この手順完了後、以下の機能実装に進むことができます：
- エナジーシステムの実装
- ターン制の実装
- 複数カードの手札管理
- カードコストシステム

## 注意事項
- 見た目の改善が主目的であり、機能は後から実装
- まずは参考画像に近い外観を目指す
- エラーが出た場合は基本設定を再確認する