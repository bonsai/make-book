# make-book

素材として完成した本・原稿を受け取り、**マーチャンダイズをリサーチして商品化・出版・販売チャネルへの展開を設計するrepo**。

本文そのものはここで制作しない。テキスト制作・編集は別repoで行い、完成した成果物を持ち込んで商品化する。

## Role

`make-book` は「本を書く場所」ではなく、

> **ある作品を、どんな商品にして、どのチャネルで、どの価格・仕様・供給方式で届けるかを研究・計画する場所**

## Input

外部で制作された完成素材を受け取る。

- TXT
- Markdown
- PDF
- EPUB
- 必要に応じて画像・音声などの関連asset

```
TEXT / CREATIVE REPOS
  ↓
TXT / MD / PDF / EPUB
  ↓
make-book
  ↓
MERCHANDISE RESEARCH
  ↓
PRODUCT PLAN
  ↓
EDITION / PRICE / COST
  ↓
CHANNEL PLAN
  ↓
PUBLISH / SELL
```

KDPは電子書籍・ペーパーバックを扱い、EPUB等を電子書籍原稿として利用できる。紙書籍ではPDF等を原稿として扱える。 citeturn0search2turn0search5turn0search8

## Merchandise Research

作品そのものを変更するのではなく、商品としての成立条件を調査する。

### Research
- 読者・購入者
- 類似商品・競合
- 市場価格
- ページ数
- 判型
- カラー / モノクロ
- 電子 / 紙
- 印刷コスト
- 送料・手数料
- 販売チャネル
- 権利・独占条件
- オンデマンド供給
- オフライン販売
- ギフト・限定版などの商品形態

### Product Plan

同じ作品から複数の商品形態を設計する。

```
ONE WORK
  ├── Kindle edition
  ├── Paperback
  ├── PDF edition
  ├── EPUB edition
  ├── note edition
  ├── BOOTH edition
  ├── BASE edition
  ├── physical / event edition
  └── bundle / limited edition
```

noteでは文章作品だけでなく音声なども有料コンテンツとして販売できるため、作品に応じて電子・音声・記事などの組み合わせも検討する。 citeturn0search0turn0search12

## Merchandise Flow

```
01 RECEIVE
    TXT / MD / PDF / EPUB
        ↓
02 INSPECT
    metadata / pages / format / rights
        ↓
03 RESEARCH
    market / audience / competitors / channels
        ↓
04 DESIGN
    product / edition / format / package
        ↓
05 PRICE
    cost / price / margin / fee
        ↓
06 CHANNEL
    KDP / note / BOOTH / BASE / offline
        ↓
07 SUPPLY
    on-demand print / digital delivery / physical stock
        ↓
08 PUBLISH
    upload / listing / sales page
        ↓
09 MEASURE
    sales / views / conversion / feedback
        ↓
10 ITERATE
    revise product / price / channel / edition
```

## On-demand / Offline

### On-demand

在庫を持たず、注文に応じて製造・提供する方式。

例：
- KDP paperback
- 電子書籍
- PDF / EPUB download

KDPのペーパーバックはオンデマンド印刷で、印刷コストは販売時のロイヤリティ計算に組み込まれる。 fileciteturn0file0L88-L115

### Offline

物理的な商品として持ち、イベント・店舗・直接販売などで届ける方式。

例：
- 文学フリマ
- 即売会
- イベント
- 個人販売
- 委託販売
- 著者本人からの直接販売

同じ作品について、オンデマンドとオフラインを併用できるようにする。

## Canonical Product Model

本文ではなく、**商品化情報**をcanonicalにする。

```
product.json
  ├── work
  ├── source
  ├── edition
  ├── format
  ├── specification
  ├── price
  ├── cost
  ├── margin
  ├── channel
  ├── supply
  ├── rights
  └── listing
```

### Core entities
- `work`: 元作品
- `source`: 持ち込まれたTXT/MD/PDF/EPUB等
- `product`: 商品
- `edition`: 版・商品形態
- `format`: TXT/MD/PDF/EPUB/紙/音声等
- `specification`: 判型・ページ数・カラー等
- `price`: 販売価格
- `cost`: 原価・手数料・送料等
- `channel`: 販売・配布先
- `supply`: オンデマンド / 在庫 / デジタル配信等
- `rights`: 権利・独占条件
- `listing`: 各チャネルの商品掲載情報

## Repository Boundary

### ここでやる
- マーチャンダイズ調査
- 商品企画
- 出版仕様の設計
- 原価・価格計算
- チャネル選択
- オンデマンド / オフライン供給設計
- 販売計画
- 商品データ管理
- チャネル別の掲載計画
- 販売結果の分析

### ここではやらない
- 本文執筆
- 小説生成
- 台本生成
- 大規模な文章編集
- STTそのもの
- 作品そのもののクリエイティブ制作

それらは別repo / agentから完成素材として受け取る。

## Design Principle

**Create elsewhere. Merchandise here. Distribute everywhere.**

```
CREATE
  ↓
IMPORT
  ↓
RESEARCH
  ↓
MERCHANDISE
  ↓
PUBLISH
  ↓
DISTRIBUTE
  ↓
MEASURE
  ↓
ITERATE
```

make-bookは、作品を「本」にするだけでなく、**作品を複数の商品・版・チャネルへ展開するためのMerchandise Planning Agent**を目指す。