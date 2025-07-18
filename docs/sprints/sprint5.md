# スプリント5：バトルシステムの深化

## 期間
1週間（6週目）

## 目標
バトルシステムに深みを追加し、より戦略的なゲームプレイを実現する。

## タスク一覧

### 敵の多様化
- [ ] 敵データをScriptableObject化
- [ ] 敵5種類の実装
  - [ ] 通常敵3種
  - [ ] エリート敵1種
  - [ ] ボス1種
- [ ] 複雑な行動パターンの実装

### バフ・デバフシステム
- [ ] バフ・デバフの基礎システム
- [ ] 主要なバフ・デバフの実装
  - [ ] 筋力（攻撃力上昇）
  - [ ] 敏捷（ブロック値上昇）
  - [ ] 弱体（与ダメージ減少）
  - [ ] 脆弱（被ダメージ増加）
- [ ] バフ・デバフのUI表示

### パワーカードの実装
- [ ] 永続効果システム
- [ ] パワーカード3種類の実装

### カード追加（合計30種類目標）
- [ ] 新規カード15種類
- [ ] レアカードの実装
- [ ] カードのバランス調整

### 戦闘演出
- [ ] ダメージ数値のポップアップ
- [ ] カード使用時の簡易エフェクト
- [ ] 画面振動効果（大ダメージ時）

## 完了基準
- 様々な敵との戦闘が楽しめる
- バフ・デバフを活用した戦略的プレイが可能
- 30種類のカードが実装されている
- 戦闘に臨場感がある

## 技術メモ
- バフ・デバフはListで管理
- エフェクトはParticleSystemを使用