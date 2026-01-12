# Claude Code Configuration

このリポジトリは、Claude Code CLI のユーザー設定ファイルを管理しています。

## 概要

Claude Code は Anthropic が提供する公式 CLI ツールで、このディレクトリには個人的なカスタマイズ設定やスキルコマンドが含まれています。

## ディレクトリ構成

```
.claude/
├── settings.json       # Claude Code の設定ファイル
├── commands/           # カスタムスキルコマンド
│   └── handle-issue.md # Issue対応ワークフロー自動化コマンド
└── .gitignore          # Git管理対象の設定
```

## 設定ファイル

### settings.json

Claude Code の動作を制御する設定ファイルです。以下の設定が含まれています：

- **permissions**: ツールの実行権限設定
  - `allow`: 許可する操作（ファイル読み取り、Git コマンドなど）
  - `deny`: 拒否する操作（危険なコマンド、機密ファイルへのアクセスなど）
- **env**: 環境変数の設定

## カスタムスキルコマンド

### /handle-issue

GitHub Issue に対応するための自動化ワークフローコマンドです。

#### 機能
- Issue番号の指定または最新オープンIssueの自動取得
- 作業ブランチの自動作成（`feature/[番号]-[タイトル]` 形式）
- Issue内容に基づく実装
- 変更のコミット
- プルリクエストの自動作成

#### 使用方法
```bash
/handle-issue [Issue番号]
```

引数を省略すると、最新のオープンIssueが自動選択されます。

## Git管理について

以下のファイルのみをGit管理対象としています：

- `.gitignore`
- `settings.json`
- `commands/` ディレクトリとその配下のファイル

その他のファイル（キャッシュ、履歴、セッション情報など）は除外されています。

## 使用方法

このリポジトリをクローンまたはプルした後、Claude Code は自動的に設定を読み込みます。

```bash
# 設定の確認
claude --version

# カスタムコマンドの使用
claude
> /handle-issue 3
```

## 注意事項

- `.credentials.json` などの機密情報は `.gitignore` で除外されており、Git管理対象外です
- `settings.json` の `deny` セクションで機密ファイルへのアクセスが制限されています
- 新しいカスタムコマンドを追加する場合は、`commands/` ディレクトリに `.md` ファイルを作成してください

## 参考

- [Claude Code 公式ドキュメント](https://github.com/anthropics/claude-code)
