# make-book

素材から本を作り、複数の出版・販売チャネルへ出力する出版基盤。

## Concept

「声で残す半生記」を入口にするが、特定の本の種類に限定しない。

- 自分史・半生記
- 小説
- 詩集
- エッセイ
- インタビュー集
- 写真集
- 研究書
- 脚本
- 家族史・会社史
- 音声作品
- ZINE

## Core pipeline

```
INPUT
  voice / text / photo / PDF / video
      ↓
UNDERSTAND
  STT / OCR / classification / episode extraction
      ↓
EDIT
  episode cards → chapters → book
      ↓
PUBLISH
  EPUB / PDF / HTML / AUDIO
      ↓
DISTRIBUTE
  Kindle / note / BOOTH / BASE / physical book
```

## Voice-first memoir

長時間の録音を30分以下・30MB以下の単位でSTTし、時系列を保持したままエピソードカードへ変換する。

```
voice memo
  ↓
STT
  ↓
episode
  ↓
card
  ↓
arrange
  ↓
chapter
  ↓
book
```

本人の肉声を原音として保存し、文章だけでなく「本になった半生記 + 元になった声」まで残せるようにする。

## Canonical book model

出版先ごとに原稿を作り直さず、共通の中間表現から各形式を生成する。

```
book.json
  ├── EPUB
  ├── PDF
  ├── HTML
  ├── AUDIO
  └── cover
```

### Suggested entities

- `work`: 作品全体
- `episode`: 原素材から抽出した出来事
- `card`: 編集可能なエピソード単位
- `chapter`: カードを束ねた章
- `book`: 出版可能な成果物
- `asset`: 音声・画像・動画・原稿など
- `edition`: 電子・紙・音声などの版
- `channel`: 販売・公開先

## Distribution

想定する出力先：

- Amazon KDP / Kindle
- note
- BOOTH
- BASE
- 紙の本
- その他の販売・配布チャネル

KDP Selectなど独占条件が発生する場合は、チャネル間の権利条件を確認してから配信する。

## Design principle

**素材 → 構造化 → 編集 → 出版 → 配信**

を分離する。

「本を作る人」を増やすのではなく、本人が声や素材を残すだけで、編集可能なカードと出版可能な本へ変換できる仕組みを目指す。
