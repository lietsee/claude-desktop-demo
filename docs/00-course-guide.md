# Claude Desktop 業務デモ講座ガイド

## この講座の目的

Claude Desktopを「質問に答えるチャット」ではなく、複数資料を読み、成果物を作り、外部サービスと連携し、別視点で検証する業務環境として体験します。

題材は、支店ごとに形式が異なる売上CSVです。参加者はコードを書きません。

## 推奨コース

### 基本コース：60分

| フェーズ | 内容 | 目安 |
|---|---|---:|
| 0 | DesktopとProjectの準備 | 10分 |
| 1 | 複数ファイルの調査 | 10分 |
| 2 | ExcelとPDFの作成 | 20分 |
| 3 | Artifactダッシュボード | 10分 |
| 4 | 新しいチャットで監査 | 10分 |

### 応用込み：90分

基本コースに次を追加します。

- Google Drive等のリモートコネクタ
- Desktop Extensionによるローカル資源への接続
- Cowork／コンピュータ操作
- Project instructionsと定型プロンプトによる再利用

## 各フェーズの教科書

1. `01-setup.md`：Desktopの準備
2. `02-project-and-files.md`：Projectとファイル投入
3. `03-investigation.md`：調査と確認
4. `04-file-creation.md`：Excel・PDF作成
5. `05-artifact-dashboard.md`：Artifact作成
6. `06-connectors-and-extensions.md`：コネクタとDesktop Extension
7. `07-adversarial-review.md`：敵対的レビュー
8. `08-reuse.md`：Project instructionsと再利用
9. `09-troubleshooting.md`：やり直しとトラブル対応

Claudeへ入力する文章は `demo-prompts.md` にあります。

## 3つの実施方法

### A. ファイルアップロード方式

最も確実です。Projectへ4つのCSVと `reference/requirements.md` を追加します。

- GitHub接続不要
- Desktop Extension不要
- 初心者向けデモの標準方式

### B. GitHubコネクタ方式

GitHubコネクタからこのリポジトリのファイルを選択します。

- ファイル選択が容易
- リポジトリ更新を反映しやすい
- GitHub認証が必要

### C. ローカルフォルダ方式

Desktop ExtensionまたはCoworkへクローン済みフォルダへのアクセスを許可します。

- ローカルファイルの読み書きまで見せられる
- 権限確認と安全説明が必要
- 環境差があるため応用編向け

## この教材の重要原則

1. 最初に調査だけを依頼する
2. Claudeが理解した処理ルールを人間が確認する
3. 元データは変更しない
4. 判断不能な行はエラー一覧へ残す
5. 数値の整合を機械的に検証する
6. 作成した本人の説明だけで完了にしない
7. 外部サービスへの書き込みは対象と権限を確認してから行う

## 講師の到達目標

参加者が最後に次を説明できれば成功です。

- Projectは、資料と指示を共有する継続的な作業場所
- Artifactは、会話から独立して編集・操作できる成果物
- コネクタはクラウドサービス、Desktop Extensionはローカル資源に向く
- Claudeの回答は、別チャットと数値検算で監査する
- 成功した依頼はProject instructionsや定型プロンプトとして再利用する
