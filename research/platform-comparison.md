---
created: 2025-12-15
tags: [tech/tool, claude, status/done]
aliases: []
---

# Claude各プラットフォーム カスタム指示認識方法比較

## 概要

Claudeの各プラットフォーム（Code、Web、Desktop、API）でカスタム指示をどのように認識させるかを比較調査。

## プラットフォーム比較表

| プラットフォーム | 認識方法 | 形式 | 自動読み込み | 必要プラン |
|-----------------|---------|------|------------|-----------|
| Claude Code | CLAUDE.md | Markdown | Yes | - |
| Claude Web | Projects | 任意 | No（手動） | Pro/Max/Team |
| Claude Desktop | Projects | 任意 | No（手動） | Pro/Max/Team |
| Claude API | System Prompt / Skills | 任意 | - | API利用 |

## 各プラットフォーム詳細

### Claude Code

#### CLAUDE.mdファイル

Claude Codeは会話開始時に`CLAUDE.md`を自動的にコンテキストに読み込む。

**配置場所と優先順位:**
1. リポジトリルート: `./CLAUDE.md`（最も一般的）
2. ホームディレクトリ: `~/.claude/CLAUDE.md`（全セッション共通）
3. 親ディレクトリ: モノレポ構成で有用
4. 子ディレクトリ: オンデマンドで読み込み

**ファイル種類:**
- `CLAUDE.md` - gitにコミット可能
- `CLAUDE.local.md` - .gitignoreに追加して個人用

**読み込みタイミング:**
- 会話開始時にシステムプロンプト直後のユーザーメッセージとして提供

#### --append-system-prompt フラグ

システムプロンプト末尾に直接追加する方法。高レベルの永続的ルールに適している。

```bash
claude --append-system-prompt "Always use TypeScript"
```

### Claude Web / Desktop (Projects機能)

#### 概要

Projectsは専用ワークスペースで、ドキュメントとカスタム指示を一元管理。

#### 主な機能

- **Knowledge Base**: ドキュメントをアップロードしてClaudeと共有
- **カスタム指示**: プロジェクト固有の振る舞いを設定
- **200Kコンテキスト**: 約500ページ分の容量

#### 設定手順

1. claude.ai/projects にアクセス
2. 「+ New Project」をクリック
3. プロジェクト名・説明を入力
4. Knowledge Baseにファイルをアップロード
5. カスタム指示を設定

#### 制限事項

- Pro/Max/Teamプランが必要
- ファイルは手動アップロード必要
- チャット間でコンテキストは共有されない（Knowledge Baseのみ共有）

### Claude Skills (2025年11月〜)

#### 概要

Skillsは専門的なタスク実行のためのカスタムオンボーディング材料。

#### 特徴

- **選択的読み込み**: 関連するスキルのみ活性化
- **積層可能性**: 複数スキルが協調動作
- **移植性**: Claude apps、Claude Code、APIで同一形式
- **効率性**: パフォーマンス最適化

#### ファイル構造

```
skill-folder/
├── SKILL.md          # スキル定義
├── instructions/     # 詳細指示
├── scripts/          # スクリプト
└── resources/        # リソース
```

#### API

`/v1/skills` エンドポイントでプログラム的に管理可能。

### Claude API

#### System Prompt

```python
response = client.messages.create(
    model="claude-sonnet-4-20250514",
    system="ここにカスタム指示を記述",
    messages=[...]
)
```

#### Skills API (Beta)

Code Execution Toolベータで利用可能。

## 共通利用のための推奨アプローチ

### Markdown形式で統一

全プラットフォームで読み取り可能なMarkdown形式を採用。

### 推奨ファイル構造

```
project/
├── CLAUDE.md              # Claude Code用（自動認識）
├── SKILL.md               # Skills機能用（将来対応）
├── rules/
│   └── core-rules.md      # Web/Desktop Projects用
└── templates/
    └── *.drawio           # テンプレート
```

### プラットフォーム別利用方法

| プラットフォーム | 利用手順 |
|-----------------|---------|
| Claude Code | CLAUDE.mdを配置するだけ |
| Claude Web | Projects作成 → core-rules.mdをアップロード |
| Claude Desktop | 同上 |
| API | system promptにルールを直接記載 |

## 参考リンク

- [CLAUDE.md Best Practices - Arize](https://arize.com/blog/claude-md-best-practices-learned-from-optimizing-claude-code-with-prompt-learning/)
- [Claude Projects - Anthropic](https://www.anthropic.com/news/projects)
- [Claude Skills - Anthropic](https://claude.com/blog/skills)
- [How to create and manage projects - Claude Help](https://support.claude.com/en/articles/9519177-how-can-i-create-and-manage-projects)
