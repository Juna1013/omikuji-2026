# 🎍 2026年 新年おみくじアプリ 設計書

## 📋 概要

Vue.jsを使用した新年のおみくじWebアプリケーション。
ユーザーが「おみくじを引く」ボタンをクリックすると、運勢が表示される和風デザインのアプリケーション。

## 🎯 プロジェクト目標

- **技術スタック**: Vue 3 + Vite + Tailwind CSS 4 + VueUse エコシステム
- **デザインテーマ**: 和風・お正月・神社をモチーフにしたモダンデザイン
- **ターゲット**: 2026年の新年を祝う一般ユーザー

### 技術スタック詳細

| カテゴリ | ライブラリ | バージョン | 用途 |
|----------|------------|------------|------|
| フレームワーク | Vue 3 | ^3.4.0 | UIフレームワーク |
| ビルドツール | Vite | ^5.0.0 | 高速ビルド・HMR |
| スタイリング | Tailwind CSS | ^4.0.0 | ユーティリティCSS |
| アニメーション | @vueuse/motion | ^2.2.0 | 宣言的アニメーション |
| ユーティリティ | @vueuse/core | ^11.0.0 | Composition API ユーティリティ |
| エフェクト | canvas-confetti | ^1.9.0 | 紙吹雪演出 |
| アイコン | lucide-vue-next | ^0.460.0 | モダンアイコン |
| 画像保存 | html-to-image | ^1.11.0 | 結果の画像保存 |

## ✨ 機能要件

### 1. コア機能

| 機能 | 説明 |
|------|------|
| おみくじを引く | ボタンクリックでランダムにおみくじを表示 |
| 運勢表示 | 大吉〜大凶までの運勢をアニメーション付きで表示 |
| 詳細運勢 | 恋愛運・仕事運・金運などの詳細を表示 |
| リセット | 再度おみくじを引くためのリセット機能 |

### 2. 運勢の種類

```
大吉 > 吉 > 中吉 > 小吉 > 末吉 > 凶 > 大凶
```

各運勢には以下の詳細情報を含む:
- **総合運**: 一言メッセージ
- **恋愛運**: ★1〜5で評価 + コメント
- **仕事運**: ★1〜5で評価 + コメント  
- **金運**: ★1〜5で評価 + コメント
- **健康運**: ★1〜5で評価 + コメント
- **ラッキーカラー**: 色名
- **ラッキーナンバー**: 数字

### 3. 追加機能

| 機能 | 説明 | 使用ライブラリ |
|------|------|----------------|
| 🎊 紙吹雪演出 | 大吉時に紙吹雪を降らせる | canvas-confetti |
| 🌙 ダークモード | ライト/ダーク切り替え | @vueuse/core (`useDark`) |
| 📷 画像保存 | 結果を画像として保存 | html-to-image |
| 📤 シェア機能 | Web Share APIでシェア | @vueuse/core (`useShare`) |
| 💾 履歴保存 | 過去のおみくじ結果を保存 | @vueuse/core (`useLocalStorage`) |
| 📋 コピー機能 | 結果をクリップボードにコピー | @vueuse/core (`useClipboard`) |

## 🎨 デザイン仕様

### カラーパレット

| 用途 | カラー | 説明 |
|------|--------|------|
| プライマリ | `#B71C1C` (深紅) | 神社の鳥居をイメージ |
| セカンダリ | `#FFD700` (金) | 豪華さ・おめでたさ |
| アクセント | `#1A237E` (紺) | 和の落ち着き |
| 背景 | `#FFF8E1` (生成り) | 和紙のような温かみ |
| テキスト | `#3E2723` (こげ茶) | 墨の色 |

### タイポグラフィ

- **メインフォント**: `Noto Serif JP` (見出し、運勢表示)
- **サブフォント**: `Noto Sans JP` (本文、説明文)

### アニメーション (@vueuse/motion)

`@vueuse/motion`を使用して、Framer Motion風の宣言的アニメーションを実装:

```vue
<template>
  <div
    v-motion
    :initial="{ opacity: 0, y: 100 }"
    :enter="{ opacity: 1, y: 0 }"
    :variants="{ shake: { x: [-10, 10, -10, 10, 0] } }"
  >
    <!-- コンテンツ -->
  </div>
</template>
```

| アニメーション | 実装方法 |
|----------------|----------|
| おみくじ箱のシェイク | `v-motion` + カスタムvariant |
| おみくじの出現 | `v-motion` initial/enter |
| 運勢表示 | `v-motion` + stagger |
| 星評価 | `v-motion` + delay |

### レスポンシブデザイン (Tailwind CSS)

Tailwind CSS 4のブレークポイントを使用:

| デバイス | ブレークポイント | Tailwindプレフィックス |
|----------|------------------|------------------------|
| モバイル | 〜767px | デフォルト |
| タブレット | 768px〜 | `md:` |
| デスクトップ | 1024px〜 | `lg:` |

## 🏗️ システム設計

### ディレクトリ構成

```
omikuji-2026/
├── docs/                      # ドキュメント
│   ├── design.md              # 設計書（このファイル）
│   └── api.md                 # データ仕様書
├── public/
│   ├── favicon.ico
│   └── images/                # 画像アセット
├── src/
│   ├── assets/
│   │   └── main.css           # Tailwind CSSエントリーポイント
│   ├── components/            # Vueコンポーネント
│   │   ├── OmikujiBox.vue     # おみくじ箱
│   │   ├── OmikujiResult.vue  # 結果表示
│   │   ├── FortuneDetail.vue  # 詳細運勢
│   │   ├── StarRating.vue     # 星評価
│   │   └── ShareButtons.vue   # シェアボタン
│   ├── composables/           # Vue Composables
│   │   └── useOmikuji.js      # おみくじロジック
│   ├── data/
│   │   └── fortunes.json      # 運勢データ
│   ├── App.vue                # ルートコンポーネント
│   └── main.js                # エントリーポイント
├── index.html
├── package.json
├── vite.config.js
└── README.md
```

### コンポーネント構成

```
App.vue
├── Header (タイトル・年号表示)
├── OmikujiBox.vue
│   └── ボタン「おみくじを引く」
├── OmikujiResult.vue (条件付きレンダリング)
│   ├── 運勢タイトル
│   ├── FortuneDetail.vue
│   │   └── StarRating.vue (x4: 恋愛・仕事・金・健康)
│   ├── ラッキーカラー・ナンバー
│   └── ShareButtons.vue
└── Footer
```

### 状態管理

Vue 3のComposition APIを使用したシンプルな状態管理:

```javascript
// useOmikuji.js
const state = reactive({
  isDrawing: false,      // おみくじを引いている最中か
  hasResult: false,      // 結果が表示されているか
  currentFortune: null,  // 現在の運勢データ
})
```

## 📊 データ仕様

### 運勢データ構造 (fortunes.json)

```json
{
  "fortunes": [
    {
      "id": 1,
      "type": "大吉",
      "level": 7,
      "message": "最高の一年になります！",
      "details": {
        "love": {
          "stars": 5,
          "comment": "素敵な出会いがあるでしょう"
        },
        "work": {
          "stars": 5,
          "comment": "大きな成果を得られます"
        },
        "money": {
          "stars": 4,
          "comment": "思わぬ収入があるかも"
        },
        "health": {
          "stars": 5,
          "comment": "元気いっぱいの一年に"
        }
      },
      "luckyColor": "赤",
      "luckyNumber": 7
    }
  ]
}
```

## 🚀 開発フェーズ

### Phase 1: 基盤構築 (Day 1)
- [x] 設計書作成
- [x] Vite + Vue 3 プロジェクトセットアップ
- [x] Tailwind CSS 4 設定
- [x] ライブラリインストール

### Phase 2: UI実装 (Day 2-3)
- [ ] App.vue レイアウト
- [ ] OmikujiBox.vue 実装
- [ ] OmikujiResult.vue 実装
- [ ] FortuneDetail.vue 実装
- [ ] StarRating.vue 実装

### Phase 3: 機能実装 (Day 3-4)
- [ ] useOmikuji composable 実装
- [ ] 運勢データ作成
- [ ] ランダム抽選ロジック
- [ ] アニメーション実装

### Phase 4: 仕上げ (Day 4-5)
- [ ] レスポンシブ対応
- [ ] シェア機能実装
- [ ] パフォーマンス最適化
- [ ] テスト・デバッグ

## 🔧 技術仕様

### 依存関係

```json
{
  "dependencies": {
    "vue": "^3.4.0",
    "@vueuse/core": "^11.0.0",
    "@vueuse/motion": "^2.2.0",
    "canvas-confetti": "^1.9.0",
    "lucide-vue-next": "^0.460.0",
    "html-to-image": "^1.11.0"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.0.0",
    "tailwindcss": "^4.0.0",
    "@tailwindcss/vite": "^4.0.0",
    "vite": "^5.0.0"
  }
}
```

### ライブラリ活用例

#### canvas-confetti（大吉演出）

```javascript
import confetti from 'canvas-confetti'

const celebrateDaikichi = () => {
  confetti({
    particleCount: 100,
    spread: 70,
    origin: { y: 0.6 },
    colors: ['#B71C1C', '#FFD700', '#FFF8E1']
  })
}
```

#### @vueuse/core（機能実装）

```javascript
import { useDark, useLocalStorage, useShare, useClipboard } from '@vueuse/core'

// ダークモード
const isDark = useDark()

// 履歴保存
const history = useLocalStorage('omikuji-history', [])

// シェア機能
const { share, isSupported } = useShare()
await share({
  title: '2026年おみくじ結果',
  text: `今年の運勢は「大吉」です！`,
  url: location.href
})

// クリップボード
const { copy } = useClipboard()
await copy('おみくじ結果をコピーしました')
```

#### html-to-image（画像保存）

```javascript
import { toPng } from 'html-to-image'

const saveAsImage = async () => {
  const element = document.getElementById('omikuji-result')
  const dataUrl = await toPng(element)
  
  const link = document.createElement('a')
  link.download = 'omikuji-2026.png'
  link.href = dataUrl
  link.click()
}
```

### ブラウザサポート

- Chrome (最新2バージョン)
- Firefox (最新2バージョン)
- Safari (最新2バージョン)
- Edge (最新2バージョン)

## 📝 備考

- 2026年の干支は「午（うま）」年
- アクセシビリティ: キーボード操作対応、スクリーンリーダー対応
- SEO: 適切なmetaタグ、OGP設定
