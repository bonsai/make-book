# AW merchandise planning

## 起点
**200P・1冊**を最小単位にして、持ち込まれた TXT / MD / PDF / EPUB から商品化条件を分岐させる。

## 分岐
完成素材 → format / pages / rights → 200P? → 1冊? → オンデマンド最小実験 → supply → channel → 価格 / 原価 / 粗利 → 実績

GitHub Actions の workflow_dispatch では入力を受け取り、if 条件でジョブを分岐できるため、この判断をAWに持たせる。 citeturn0search1turn0search0

## 最初のケース
source = TXT / MD / PDF / EPUB
pages = 200
quantity = 1
supply = auto

まず「200Pを1冊だけ作る」ケースを実験単位にする。

### 1冊
- 初期在庫を持たない
- オンデマンドを第一候補として計画
- 電子版は別editionとして比較
- オフライン販売は必要冊数が発生した時点で別分岐

### 複数冊
1冊オンデマンド / 小ロット / オフライン在庫を原価・販売条件で比較する。

## AWの役割
AWは本文を作らない。
**入力 → 条件判定 → 商品候補 → チャネル候補 → 価格/原価計画 → 次のIssue** までを自動化する。

各分岐の根拠・調査結果は research/、決定した商品案は plans/、チャネル別仕様は channels/ に保存する。

## 最小データ
work: example
source_format: pdf
pages: 200
quantity: 1
supply: ondemand
edition: paperback
channel: kdp
status: plan

ここから実売データを蓄積し、**1冊 → 10冊 → 100冊**へ計画を拡張する。