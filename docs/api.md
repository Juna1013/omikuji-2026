# 📜 運勢データ仕様書

## 概要

おみくじアプリで使用する運勢データの詳細仕様を定義します。

## 運勢タイプ一覧

| ID | タイプ | レベル | 出現確率 |
|----|--------|--------|----------|
| 1 | 大吉 | 7 | 10% |
| 2 | 吉 | 6 | 20% |
| 3 | 中吉 | 5 | 25% |
| 4 | 小吉 | 4 | 20% |
| 5 | 末吉 | 3 | 15% |
| 6 | 凶 | 2 | 8% |
| 7 | 大凶 | 1 | 2% |

※ レベルが高いほど良い運勢

## データスキーマ

### Fortune オブジェクト

```typescript
interface Fortune {
  id: number;           // 一意のID
  type: FortuneType;    // 運勢タイプ
  level: number;        // 運勢レベル (1-7)
  message: string;      // 総合メッセージ
  details: FortuneDetails;
  luckyColor: string;   // ラッキーカラー
  luckyNumber: number;  // ラッキーナンバー
}

type FortuneType = 
  | "大吉" 
  | "吉" 
  | "中吉" 
  | "小吉" 
  | "末吉" 
  | "凶" 
  | "大凶";
```

### FortuneDetails オブジェクト

```typescript
interface FortuneDetails {
  love: CategoryDetail;    // 恋愛運
  work: CategoryDetail;    // 仕事運
  money: CategoryDetail;   // 金運
  health: CategoryDetail;  // 健康運
}

interface CategoryDetail {
  stars: number;    // 1-5の星評価
  comment: string;  // 詳細コメント
}
```

## サンプルデータ

### 大吉

```json
{
  "id": 1,
  "type": "大吉",
  "level": 7,
  "message": "2026年は最高の一年になるでしょう！すべてが順調に進み、幸運が舞い込みます。",
  "details": {
    "love": {
      "stars": 5,
      "comment": "運命的な出会いがあるかも。既にパートナーがいる方は絆が深まります。"
    },
    "work": {
      "stars": 5,
      "comment": "大きなプロジェクトが成功し、評価が上がります。"
    },
    "money": {
      "stars": 4,
      "comment": "臨時収入の予感。ただし散財には注意。"
    },
    "health": {
      "stars": 5,
      "comment": "心身ともに充実した一年に。新しい運動を始めると良いでしょう。"
    }
  },
  "luckyColor": "赤",
  "luckyNumber": 7
}
```

### 吉

```json
{
  "id": 2,
  "type": "吉",
  "level": 6,
  "message": "良い一年になりそうです。努力が実を結ぶ年。",
  "details": {
    "love": {
      "stars": 4,
      "comment": "積極的なアプローチが吉。素直な気持ちを大切に。"
    },
    "work": {
      "stars": 4,
      "comment": "地道な努力が認められます。チームワークを大切に。"
    },
    "money": {
      "stars": 4,
      "comment": "堅実な金運。貯蓄を心がけると更に良し。"
    },
    "health": {
      "stars": 4,
      "comment": "規則正しい生活が開運の鍵。"
    }
  },
  "luckyColor": "金",
  "luckyNumber": 3
}
```

### 中吉

```json
{
  "id": 3,
  "type": "中吉",
  "level": 5,
  "message": "穏やかで安定した一年。小さな幸せが積み重なります。",
  "details": {
    "love": {
      "stars": 3,
      "comment": "焦らず自然体で。良い縁は突然やってきます。"
    },
    "work": {
      "stars": 4,
      "comment": "コツコツと続けることで成果が出ます。"
    },
    "money": {
      "stars": 3,
      "comment": "大きな変動はなし。計画的な支出を。"
    },
    "health": {
      "stars": 4,
      "comment": "適度な運動と休息のバランスが大切。"
    }
  },
  "luckyColor": "緑",
  "luckyNumber": 5
}
```

### 小吉

```json
{
  "id": 4,
  "type": "小吉",
  "level": 4,
  "message": "小さな幸運があなたを待っています。日々の感謝を忘れずに。",
  "details": {
    "love": {
      "stars": 3,
      "comment": "友人からの紹介に期待。人との繋がりを大切に。"
    },
    "work": {
      "stars": 3,
      "comment": "新しいスキルを学ぶと良いでしょう。"
    },
    "money": {
      "stars": 3,
      "comment": "無駄遣いに注意。必要なものを見極めて。"
    },
    "health": {
      "stars": 3,
      "comment": "季節の変わり目に体調管理を。"
    }
  },
  "luckyColor": "青",
  "luckyNumber": 2
}
```

### 末吉

```json
{
  "id": 5,
  "type": "末吉",
  "level": 3,
  "message": "後半に運気が上昇。辛抱強く待つことが大切。",
  "details": {
    "love": {
      "stars": 2,
      "comment": "今は自分磨きの時期。焦りは禁物です。"
    },
    "work": {
      "stars": 3,
      "comment": "準備期間と捉えて。学びの時。"
    },
    "money": {
      "stars": 2,
      "comment": "大きな買い物は慎重に。"
    },
    "health": {
      "stars": 3,
      "comment": "ストレス発散を心がけて。"
    }
  },
  "luckyColor": "白",
  "luckyNumber": 8
}
```

### 凶

```json
{
  "id": 6,
  "type": "凶",
  "level": 2,
  "message": "慎重に行動する一年。困難は成長のチャンス。",
  "details": {
    "love": {
      "stars": 2,
      "comment": "誤解が生じやすい時期。言葉を大切に。"
    },
    "work": {
      "stars": 2,
      "comment": "確認を怠らず。ミスに注意。"
    },
    "money": {
      "stars": 2,
      "comment": "衝動買いは厳禁。節約を心がけて。"
    },
    "health": {
      "stars": 2,
      "comment": "無理は禁物。十分な睡眠を。"
    }
  },
  "luckyColor": "紫",
  "luckyNumber": 4
}
```

### 大凶

```json
{
  "id": 7,
  "type": "大凶",
  "level": 1,
  "message": "試練の年。しかし乗り越えれば大きな成長があります。凶を吉に変える力があなたにはあります。",
  "details": {
    "love": {
      "stars": 1,
      "comment": "今は静かに過ごす時期。自分を見つめ直して。"
    },
    "work": {
      "stars": 1,
      "comment": "慎重に。大きな決断は先延ばしに。"
    },
    "money": {
      "stars": 1,
      "comment": "節約モードで。貯蓄を優先。"
    },
    "health": {
      "stars": 2,
      "comment": "定期的な健康チェックを。"
    }
  },
  "luckyColor": "黒",
  "luckyNumber": 9
}
```

## ラッキーカラー一覧

| カラー名 | カラーコード | 意味 |
|----------|--------------|------|
| 赤 | `#E53935` | 情熱・勝利 |
| 金 | `#FFD700` | 富・繁栄 |
| 緑 | `#43A047` | 健康・成長 |
| 青 | `#1E88E5` | 信頼・冷静 |
| 白 | `#FAFAFA` | 純粋・新しい始まり |
| 紫 | `#8E24AA` | 神秘・直感 |
| 黒 | `#212121` | 守護・忍耐 |
| 桃 | `#EC407A` | 恋愛・優しさ |
| 橙 | `#FF7043` | 活力・社交 |

## ラッキーナンバー

1〜9の数字を使用。
各数字には以下の意味があります：

| 数字 | 意味 |
|------|------|
| 1 | 始まり・リーダーシップ |
| 2 | 調和・協力 |
| 3 | 創造・表現 |
| 4 | 安定・基盤 |
| 5 | 変化・自由 |
| 6 | 愛情・責任 |
| 7 | 知恵・探求 |
| 8 | 成功・豊かさ |
| 9 | 完成・慈悲 |
