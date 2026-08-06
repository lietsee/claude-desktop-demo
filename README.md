# Claude Desktop 業務デモ教材

形式の異なる複数CSVを使い、Claude Desktopで資料の理解、データ分析、Excel・PDF作成、Artifact作成、コネクタ利用、批判的レビューまでを体験する初心者向け教材です。

## 対象

- Claudeを業務で使い始めたい非エンジニア
- 複数ファイルの整理、集計、報告書作成を効率化したい方
- Claude Codeの前に、GUI中心でClaudeの使い方を理解したい方

## この教材の方針

追加の拡張機能がなくても、基本編は完走できます。

- **基本編**：Project、ファイルアップロード、コード実行、Excel・PDF作成、Artifacts
- **応用編**：Google Drive等のリモートコネクタ、ローカルDesktop Extension、Cowork
- **再利用編**：Project instructions、定型プロンプト、必要に応じてPlugin／Skill

## 開始方法

```bash
git clone https://github.com/lietsee/claude-desktop-demo.git
cd claude-desktop-demo
```

その後、Claude Desktopを開き、`docs/00-course-guide.md`から進めます。

Gitを使わない場合は、GitHubの「Code」→「Download ZIP」でも構いません。

## 教材構成

```text
.
├─ input/                         # デモ用CSV
├─ reference/                     # Claudeへ渡す業務要件
├─ docs/                          # 各フェーズの教科書
├─ demo-prompts.md                # コピペ用プロンプト集
├─ instructor-notes.md            # 講師向け進行メモ
└─ README.md
```

## 関連教材

ターミナル、Git、スクリプト、サブエージェント、Project Skillまで扱う版：

- https://github.com/lietsee/claude-code-demo

## 教師用の正解

期待値は `instructor-answer` ブランチに分離します。通常の実演中は開かないでください。
