# 売上データ統合・経営報告資料の作成要件

## 1. 目的

`input/` 内にある形式の異なる売上CSVと返金CSVを統合し、経営者が確認できるExcel、報告書、インタラクティブなダッシュボードを作成する。

Claude Desktop上での単発作業を想定するが、処理ルールと検証内容を記録し、翌月も同じ考え方で再実行できるようにする。

## 2. 原則

- 元CSVは変更しない
- 判断できない行を黙って削除・補完しない
- 事実、業務ルール、推測を分ける
- 集計値は元データから再計算して検証する
- 「作成できた」だけでなく、件数と金額の整合を確認する

## 3. 入力ファイル

- `input/tokyo.csv`
- `input/nagoya.csv`
- `input/osaka.csv`
- `input/returns.csv`

すべてUTF-8のCSVで、1行目はヘッダーである。

## 4. 正規化後の列

1. `transaction_id`
2. `original_transaction_id`
3. `date`
4. `branch`
5. `category`
6. `amount_yen`
7. `visitor_count`
8. `record_type`
9. `source_file`
10. `source_row`

### 値のルール

- `date`: `YYYY-MM-DD`
- `branch`: `東京支店`、`名古屋支店`、`大阪支店`
- `category`: 空欄は `未分類`
- `amount_yen`: 整数
- `visitor_count`: 0以上の整数。空欄は0
- `record_type`: 売上は `sale`、返金は `refund`
- 売上の `original_transaction_id`: 空欄
- 返金の `original_transaction_id`: 元取引ID

## 5. 列名の対応

### 売上

| 正規化列 | 東京 | 名古屋 | 大阪 |
|---|---|---|---|
| transaction_id | transaction_id | 取引ID | id |
| date | date | 取引日 | sold_at |
| branch | branch | 支店名 | store |
| category | category | 商品区分 | category |
| amount_yen | amount | 税込金額 | total_yen |
| visitor_count | customer_count | 来店人数 | visitors |

### 返金

- `refund_id` → `transaction_id`
- `original_transaction_id` → `original_transaction_id`
- `processed_date` → `date`
- `refund_amount` → `amount_yen`
- `visitor_count` は0
- `record_type` は `refund`

## 6. 変換ルール

### 日付

次を受け付け、`YYYY-MM-DD`へ統一する。

- `YYYY-MM-DD`
- `YYYY/MM/DD`
- `YYYY.MM.DD`
- `MM/DD/YYYY`
- `YYYY年M月D日`

実在しない日付はエラーとする。

### 金額

前後の空白、桁区切りカンマ、`¥`、`円`を除去して整数化する。

- 売上の0円は有効
- 売上の負数はエラー
- 返金は入力の符号にかかわらず `-abs(金額)`
- 整数化できない値はエラー

### 支店名

前後の半角・全角空白を除去し、次を正規化する。

- `東京`、`東京支店` → `東京支店`
- `名古屋`、`名古屋支店` → `名古屋支店`
- `大阪`、`大阪支店`、`大阪営業所` → `大阪支店`

それ以外はエラーとする。

## 7. 重複と返金

- 全項目が同じ完全重複行は1行だけ採用する
- 同じ取引IDで内容が異なる場合は、該当する全行を採用せずエラー一覧へ記録する
- 返金も同じ重複ルールで扱う
- 返金の元取引IDは、正常採用された売上に存在しなければエラーとする

## 8. 作成する成果物

### 8.1 Excel

ファイル名：`integrated_sales.xlsx`

最低限、次のシートを含める。

1. `正規化データ`
2. `支店別集計`
3. `エラー一覧`
4. `検証結果`
5. `処理ルール`

要件：

- 見出しを固定する
- 金額列は円表記にする
- フィルターを設定する
- 列幅を読みやすく調整する
- 支店別集計に売上件数、返金件数、来店人数、純売上額を含める
- 支店順は東京、名古屋、大阪

### 8.2 経営報告書

ファイル名：`management_report.pdf`

最低限、次を含める。

- 処理の概要
- 支店別の純売上額と件数
- 全体合計
- エラーと要確認事項
- 集計結果を利用する際の注意点
- 主要な検証結果

### 8.3 インタラクティブダッシュボード

ClaudeのArtifactとして作成する。

- 支店別の件数、来店人数、純売上額を表示する
- 支店で絞り込める
- 金額順に並び替えられる
- 返金を区別して確認できる
- 外部サービスの秘密情報を埋め込まない

## 9. 検証

最低限、次を検証する。

- 入力データ行数
- 採用行数
- 完全重複として除外した行数
- エラー行数
- 入力件数と採用・重複・エラー件数の整合
- 支店別金額と全体金額の整合
- 返金が負数であること
- 元取引不明の返金が採用されていないこと
- 同一IDで内容が異なる取引が採用されていないこと

## 10. 完了報告

最後に次を報告する。

- 作成したファイル
- 採用・重複・エラー件数
- 全体の純売上額
- 実施した検証と結果
- Claudeが判断せず人間に残した確認事項
