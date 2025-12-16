---
created: 2025-12-15
tags: [tech/tool, drawio, claude, status/done]
aliases: []
---

# drawioルール書 実現性・可用性レポート

## 概要

ClaudeがdrawioでSVG/XML形式の図解を生成する際のルール書を作成するプロジェクトの実現性と可用性を評価。

## 評価サマリ

| 項目 | 評価 | 根拠 |
|-----|------|-----|
| **実現性** | 高い | CLAUDE.md公式サポート、drawio生成実証済み |
| **可用性** | 中〜高 | Claude Code即利用可能、Web/DesktopはProjects対応 |
| **効果** | 期待できる | 明示的ルールで+5〜11%精度向上（Arize調査） |

## 実現性評価

### 高い実現性がある点

#### 1. CLAUDE.mdでのルール定義

| 観点 | 評価 |
|-----|------|
| 公式サポート | Anthropic公式ドキュメントで推奨 |
| 実績 | 多くのプロジェクトで採用済み |
| 自動認識 | Claude Code起動時に自動読み込み |

#### 2. drawio XML生成

| 観点 | 評価 |
|-----|------|
| 生成可能性 | Zenn記事で実証済み |
| 品質 | ルール明示で改善可能 |
| 形式 | XML/SVGともにテキストベースで生成しやすい |

#### 3. ルール遵守率向上

Arizeの研究によると：
- **汎用的改善**: 異なるリポジトリ間で+5.19%の精度向上
- **リポジトリ特化的改善**: 同一コードベース内で+10.87%の向上

### 課題と対策

| 課題 | 影響度 | 対策 |
|-----|-------|-----|
| Web/Desktopでの手動アップロード | 中 | Projects機能で一度アップロードすれば継続利用可能 |
| プラットフォーム間の一貫性 | 中 | Markdown形式で統一、同一ルールファイルを共有 |
| drawio固有挙動の初期認識不足 | 高 | 詳細ルール・チェックリスト・テンプレート提供 |
| 生成結果のばらつき | 中 | チェックリストによる検証、テンプレート活用 |

## 可用性評価

### プラットフォーム別

| プラットフォーム | 可用性 | 備考 |
|-----------------|-------|-----|
| Claude Code | 高 | CLAUDE.md配置で即利用可能 |
| Claude Web | 中 | Pro/Maxプラン必要、手動アップロード |
| Claude Desktop | 中 | Pro/Maxプラン必要、手動アップロード |
| Claude API | 高 | system promptに直接記載可能 |

### 運用面

| 項目 | 評価 | 備考 |
|-----|------|-----|
| 導入コスト | 低 | ファイル配置のみ |
| 学習コスト | 低 | ルールはMarkdownで記述 |
| メンテナンス | 低〜中 | ルール改善は継続的に必要 |
| チーム共有 | 高 | gitでバージョン管理可能 |

## リスク分析

### 低リスク

- **技術的実現性**: 既存の仕組みを活用するため、技術的障壁は低い
- **コスト**: 追加コストなし（既存プランで対応可能）

### 中リスク

- **生成品質**: Claudeがルールを完全に遵守するとは限らない
  - 対策: チェックリストで検証、テンプレート活用
- **ルール最適化**: 効果的なルールの発見には試行錯誤が必要
  - 対策: 反復的な改善、ユーザーフィードバック収集

### 高リスク

- **drawio特有の挙動**: Claudeはdrawioの細かい挙動を初期認識していない
  - 対策: 詳細なルール文書、具体例の提供、テンプレートXML

## 推奨ディレクトリ構造

```
drawio_rule_for_claude/
├── CLAUDE.md              # メインルール（Claude Code自動認識）
├── SKILL.md               # Skills機能用（将来対応）
├── README.md              # プロジェクト説明
├── research/              # 調査資料（現在のディレクトリ）
│   ├── _index.md
│   ├── platform-comparison.md
│   ├── feasibility-report.md
│   └── drawio-rules-summary.md
├── rules/
│   ├── core-rules.md      # コアルール（Web/Desktop用にも）
│   └── checklist.md       # 生成前後チェックリスト
├── templates/
│   ├── basic.drawio       # 基本テンプレートXML
│   ├── flowchart.drawio   # フローチャート用
│   └── architecture.drawio # アーキテクチャ図用
└── examples/
    ├── good-example.drawio
    ├── good-example.png
    └── bad-example.drawio
```

## 結論

### 総合評価: 実現可能

このプロジェクトは以下の理由から実現可能と判断：

1. **技術基盤が整っている**: CLAUDE.md、Projects機能、Skills機能が公式サポート
2. **先行事例がある**: Zenn記事でdrawio生成の基本ルールが実証済み
3. **効果が期待できる**: プロンプト最適化による精度向上の実績あり

### 推奨アクション

1. **Phase 1**: CLAUDE.mdにコアルールを記述し、Claude Codeでテスト
2. **Phase 2**: テンプレートファイルを作成し、生成品質を検証
3. **Phase 3**: フィードバックを基にルールを改善
4. **Phase 4**: Web/Desktop向けにProjects用ファイルを整備

## 参考資料

- [CLAUDE.md Best Practices - Arize](https://arize.com/blog/claude-md-best-practices-learned-from-optimizing-claude-code-with-prompt-learning/)
- [Claude Code Best Practices - Anthropic](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Zenn: drawio-tips-claude-code](https://zenn.dev/genda_jp/articles/2025-12-12-drawio-tips-claude-code)
