---
created: 2025-12-15
tags: [tech/tool, drawio, claude, status/done]
aliases: [drawio調査まとめ]
---

# drawioルール書 調査まとめ

## 概要

ClaudeがdrawioでSVG/XML形式の図解を生成する際のルール書を作成するための事前調査。
Claude Code、Claude Web/Desktop、Claude APIで共通利用可能な形式を検討。

## ドキュメント一覧

| ファイル | 内容 |
|---------|------|
| [[platform-comparison]] | Claude各プラットフォームでのカスタム指示認識方法比較 |
| [[feasibility-report]] | 実現性・可用性の総合評価レポート |
| [[drawio-rules-summary]] | Zenn記事から抽出したdrawioコアルール |

## 調査日

2025-12-15

## 結論

- **実現性: 高い** - CLAUDE.md形式は公式サポート、drawio XML生成は実証済み
- **可用性: 中〜高** - Claude Codeは即時利用可能、Web/DesktopはProjects機能で対応可能

## 次のステップ

1. CLAUDE.mdにdrawioコアルールを記述
2. テンプレートファイル（.drawio）を作成
3. 実際にClaudeに生成させて検証・調整

## 参考リンク

- [Zenn: drawio-tips-claude-code](https://zenn.dev/genda_jp/articles/2025-12-12-drawio-tips-claude-code)
- [CLAUDE.md Best Practices - Arize](https://arize.com/blog/claude-md-best-practices-learned-from-optimizing-claude-code-with-prompt-learning/)
- [Claude Projects - Anthropic](https://www.anthropic.com/news/projects)
- [Claude Skills - Anthropic](https://claude.com/blog/skills)
