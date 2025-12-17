# drawio_rule_for_claude

Claudeを使ってdrawio形式の図解を生成するためのルール集です。

## 概要

このリポジトリは、Claude（Claude Code / Web / Desktop / API）がdrawio形式（.drawio / XML）の図解を生成する際に従うべきルールとテンプレートを提供します。

### 対象ユーザー

要件定義を実施しているディレクターやエンジニア向けのツールです。

### 何ができるか

- 画像、ソースコード、ドキュメントなどを入力として、Claudeに図解を生成させる
- フローチャート、システム構成図、ER図、画面遷移図など9種類の図解に対応
- drawioで開ける形式で出力されるため、生成後の手直しが容易

### 品質レベル

ドラフト品質を目標としています。完璧な出力ではなく、簡単な手直しで完成できる状態を目指します。

## ディレクトリ構成

```
.
├── CLAUDE.md           # Claude向けメインルール（Claude Codeはこれを自動読み込み）
├── rules/              # 詳細ルール（スタイル、レイアウト、チェックリスト等）
├── templates/          # 図解種類別テンプレート
│   ├── drawio/         # .drawio形式（9種類）
│   └── xml/            # .xml形式（同内容）
└── research/           # 調査資料・実現性レポート
```

## 使い方

### Claude Code

このリポジトリをクローンしてディレクトリ内で作業すると、`CLAUDE.md`が自動的に読み込まれます。

### Claude Web / Desktop（Projects機能）

`CLAUDE.md`の内容をProject instructionsに貼り付けてください。

### Claude API

システムプロンプトに`CLAUDE.md`の内容を含めてください。

## 詳細

各ディレクトリ内のMarkdownファイルを参照してください。
