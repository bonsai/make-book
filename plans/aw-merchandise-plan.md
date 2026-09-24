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

## 1000円自伝：コスト最適化ケース

目的：200Pの自伝を、販売価格1,000円（税込）を目標に、1冊から成立させる。

- Decision: 判型 / 白黒・カラー / POD / 電子版 / 販売チャネル / 作業量
- Constraint: 200P、初回1冊、在庫ゼロ、本文は別repoで完成済み
- Objective: 金銭コスト + 作業コスト + 在庫リスクを最小化しつつ商品成立
- Baseline: Amazon.co.jp KDP paperback。黒インク標準判200Pなら印刷費は公式式で 206円 + 200×2円 = 606円。実際の設定時にKDP計算ツールで確認する。
- Price branch: 1,000円はKDP日本の紙書籍で60%ロイヤリティ区分の境界。税抜価格・実際の設定条件をAWで確認する。
- OR branches: `POD_1copy`, `digital_first`, `POD_plus_digital`, `offline_small_lot`
- Output: plan.yaml と比較表を生成し、次のIssueへ渡す。

### 最小ケース

`200P / 1冊 / 1,000円 / 黒白POD / 在庫ゼロ`

ここをベースラインにして、電子版追加・価格変更・冊数増加の各ケースをAWで再計算する。
