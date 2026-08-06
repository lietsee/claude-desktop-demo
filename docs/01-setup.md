# フェーズ0：Claude Desktopの準備

## 目的

Claude Desktopで、ファイル分析と成果物作成ができる状態を確認します。

## 事前準備

- Claude Desktopを最新版へ更新する
- Claudeへログインする
- このリポジトリをクローンまたはZIP展開する
- `input/` の4ファイルと `reference/requirements.md` が読めることを確認する

## 必須機能

### Code execution and file creation

Excel、PDF、グラフなどを作るために必要です。

個人プランでは、Claude Desktopの設定からCapabilitiesを開き、コード実行とファイル作成が有効であることを確認します。Team／Enterpriseでは組織管理者の設定により無効化されている場合があります。

## 推奨：Projectを作成する

1. Claude DesktopでProjectsを開く
2. 新しいProjectを作る
3. 名前を `CSV業務デモ` にする
4. Project knowledgeへ次を追加する
   - `input/tokyo.csv`
   - `input/nagoya.csv`
   - `input/osaka.csv`
   - `input/returns.csv`
   - `reference/requirements.md`
5. Project instructionsはフェーズ8まで空欄でもよい

## Projectを使う理由

- 複数チャットで同じ資料を参照できる
- 実装用チャットと監査用チャットを分けられる
- 毎回同じファイルを添付し直す必要がない
- 後から共通指示を追加できる

## Projectを使わない場合

通常の新規チャットに5ファイルをまとめて添付しても基本編は実施できます。ただし、敵対的レビュー用の新しいチャットでは再度ファイルを添付する必要があります。

## 完了確認

Claudeへ次だけを聞きます。

```text
添付またはProject knowledgeにあるファイル名だけを列挙してください。まだ内容分析や成果物作成はしないでください。
```

5ファイルが認識されていれば完了です。

## 講師が説明すること

- Claudeはファイルを渡されただけでは、望ましい処理規則までは確定できない
- Project knowledgeは資料、Project instructionsは仕事の進め方を置く場所
- ファイルに個人情報や機密情報を含める前に、会社の利用ルールを確認する

## よくある問題

### ファイルが認識されない

- 一度に添付し直す
- CSVをExcelで開いたままにしている場合は閉じる
- ファイル名を短くする
- Projectではなく通常チャットで切り分ける

### ファイル作成ができない

- Capabilitiesの設定を確認する
- 組織管理者へ確認する
- 代替としてCSVやMarkdown成果物を作らせる
