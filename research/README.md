# Claude × drawio 図解自動生成 - 実現性・可用性レポート

> 調査日: 2025-12-15

## 目次

- [1. エグゼクティブサマリー](#1-エグゼクティブサマリー)
  - [1.1 目的](#11-目的)
  - [1.2 結論](#12-結論)
  - [1.3 評価サマリ](#13-評価サマリ)
- [2. 実現性評価](#2-実現性評価)
  - [2.1 技術的実現性](#21-技術的実現性)
  - [2.2 課題と対策](#22-課題と対策)
  - [2.3 リスク分析](#23-リスク分析)
- [3. 可用性評価](#3-可用性評価)
  - [3.1 プラットフォーム別可用性](#31-プラットフォーム別可用性)
  - [3.2 運用面の評価](#32-運用面の評価)
- [4. プラットフォーム別対応方法](#4-プラットフォーム別対応方法)
  - [4.1 Claude Code](#41-claude-code)
  - [4.2 Claude Web / Desktop](#42-claude-web--desktop)
  - [4.3 Claude API](#43-claude-api)
  - [4.4 Claude Skills（将来対応）](#44-claude-skills将来対応)
- [5. drawio生成コアルール](#5-drawio生成コアルール)
  - [5.1 フォント設定](#51-フォント設定)
  - [5.2 矢印と配置](#52-矢印と配置)
  - [5.3 テキストサイズ](#53-テキストサイズ)
  - [5.4 背景設定](#54-背景設定)
  - [5.5 XML構造テンプレート](#55-xml構造テンプレート)
- [6. チェックリスト](#6-チェックリスト)
  - [6.1 生成前チェックリスト](#61-生成前チェックリスト)
  - [6.2 生成後チェックリスト](#62-生成後チェックリスト)
- [7. 推奨ディレクトリ構造](#7-推奨ディレクトリ構造)
- [8. プロンプトテンプレート](#8-プロンプトテンプレート)
  - [8.1 基本テンプレート](#81-基本テンプレート)
  - [8.2 図解種類別テンプレート](#82-図解種類別テンプレート)
- [9. 運用フロー](#9-運用フロー)
  - [9.1 基本フロー](#91-基本フロー)
  - [9.2 PNG変換コマンド](#92-png変換コマンド)
- [10. 次のステップ](#10-次のステップ)
- [11. 参考リンク](#11-参考リンク)

---

## 1. エグゼクティブサマリー

### 1.1 目的

ユーザーがローカルに配置した元ソース（画像、プログラムソース、ドキュメント等）をClaudeが解析し、依頼に応じた図解資料をdrawio XML形式で生成する状態を実現する。

#### ターゲットユーザー

**要件定義を実施しているディレクター向け**のツール。

#### 運用フロー

1. ユーザーが作業ディレクトリにルールファイル（CLAUDE.md）とテンプレートを配置
2. 元ソース（画像、コード、ドキュメント等）を投入
3. Claudeに図解を依頼
4. drawio形式（.drawio）のXMLファイルが生成される
5. drawioアプリで開いて簡単な手直し → 完成

#### 対象レベル

| レベル | 要素数目安 | 対応状況 |
|-------|-----------|---------|
| シンプル | 3-5要素 | 対応 |
| 中程度 | 10-20要素 | 対応（メイン対象） |
| 複雑 | 20要素以上、多層構造 | 対象外 |

#### 品質基準

- **ドラフト品質**で十分とする
- 簡単な手直しで完成する状態を目指す
- 完璧な出力は求めない

#### 入力ソース

Claudeが認識できるデータであれば何でも可：
- 画像データ（スクリーンショット、既存図解など）
- プログラムソース
- ドキュメント（テキスト、Markdown等）
- その他テキストベースのデータ

#### 想定する図解の種類

要件定義で使用される図解：

| カテゴリ | 図解種類 | 用途 |
|---------|---------|-----|
| プロセス系 | 業務フロー図 | 業務手順の可視化 |
| プロセス系 | データフロー図 | データの流れを表現 |
| プロセス系 | シーケンス図 | 処理の時系列表現 |
| 構造系 | システム構成図 | システム全体像 |
| 構造系 | ER図 | データベース設計 |
| 構造系 | コンテキスト図 | システム境界と外部との関係 |
| 振る舞い系 | 画面遷移図 | UI/UXの流れ |
| 振る舞い系 | 状態遷移図 | 状態変化の定義 |
| 振る舞い系 | ユースケース図 | アクターと機能の関係 |

### 1.2 結論

**総合評価: 実現可能**

| 項目 | 評価 |
|-----|------|
| **実現性** | 高い |
| **可用性** | 中〜高（プラットフォームによる） |

このプロジェクトは以下の理由から実現可能と判断：

1. **技術基盤が整っている**: CLAUDE.md、Projects機能、Skills機能が公式サポート
2. **先行事例がある**: Zenn記事でdrawio生成の基本ルールが実証済み
3. **効果が期待できる**: プロンプト最適化による精度向上の実績あり（Arize調査で+5〜11%）

### 1.3 評価サマリ

| 評価項目 | 評価 | 根拠 |
|---------|------|-----|
| 技術的実現性 | 高い | CLAUDE.md公式サポート、drawio XML生成実証済み |
| 導入容易性 | 高い | ファイル配置のみで利用開始可能 |
| 運用コスト | 低い | 追加コストなし、既存プランで対応可能 |
| 品質向上効果 | 期待できる | 明示的ルールで+5〜11%精度向上（Arize調査） |
| クロスプラットフォーム | 中 | Claude Codeは即利用可、Web/DesktopはProjects対応 |

---

## 2. 実現性評価

### 2.1 技術的実現性

#### CLAUDE.mdでのルール定義

| 観点 | 評価 | 詳細 |
|-----|------|-----|
| 公式サポート | ✅ | Anthropic公式ドキュメントで推奨 |
| 実績 | ✅ | 多くのプロジェクトで採用済み |
| 自動認識 | ✅ | Claude Code起動時に自動読み込み |

#### drawio XML生成

| 観点 | 評価 | 詳細 |
|-----|------|-----|
| 生成可能性 | ✅ | Zenn記事で実証済み |
| 品質 | ✅ | ルール明示で改善可能 |
| 形式 | ✅ | XML/SVGともにテキストベースで生成しやすい |

#### ルール遵守率向上（Arize研究より）

| 改善タイプ | 精度向上 |
|-----------|---------|
| 汎用的改善（異なるリポジトリ間） | +5.19% |
| リポジトリ特化的改善（同一コードベース内） | +10.87% |

### 2.2 課題と対策

| 課題 | 影響度 | 対策 |
|-----|-------|-----|
| Web/Desktopでの手動アップロード | 中 | Projects機能で一度アップロードすれば継続利用可能 |
| プラットフォーム間の一貫性 | 中 | Markdown形式で統一、同一ルールファイルを共有 |
| drawio固有挙動の初期認識不足 | 高 | 詳細ルール・チェックリスト・テンプレート提供 |
| 生成結果のばらつき | 中 | チェックリストによる検証、テンプレート活用 |

### 2.3 リスク分析

#### 低リスク

| リスク | 理由 |
|-------|-----|
| 技術的実現性 | 既存の仕組みを活用するため、技術的障壁は低い |
| コスト | 追加コストなし（既存プランで対応可能） |

#### 中リスク

| リスク | 対策 |
|-------|-----|
| 生成品質 - Claudeがルールを完全に遵守するとは限らない | チェックリストで検証、テンプレート活用 |
| ルール最適化 - 効果的なルールの発見には試行錯誤が必要 | 反復的な改善、ユーザーフィードバック収集 |

#### 高リスク

| リスク | 対策 |
|-------|-----|
| drawio特有の挙動 - Claudeはdrawioの細かい挙動を初期認識していない | 詳細なルール文書、具体例の提供、テンプレートXML |

---

## 3. 可用性評価

### 3.1 プラットフォーム別可用性

| プラットフォーム | 可用性 | 認識方法 | 自動読み込み | 必要プラン |
|-----------------|-------|---------|------------|-----------|
| Claude Code | **高** | CLAUDE.md | Yes | なし |
| Claude Web | 中 | Projects | No（手動） | Pro/Max/Team |
| Claude Desktop | 中 | Projects | No（手動） | Pro/Max/Team |
| Claude API | **高** | System Prompt | - | API利用 |

### 3.2 運用面の評価

| 項目 | 評価 | 備考 |
|-----|------|-----|
| 導入コスト | 低 | ファイル配置のみ |
| 学習コスト | 低 | ルールはMarkdownで記述 |
| メンテナンス | 低〜中 | ルール改善は継続的に必要 |
| チーム共有 | 高 | gitでバージョン管理可能 |

---

## 4. プラットフォーム別対応方法

### 4.1 Claude Code

**最も推奨される方法**

#### CLAUDE.mdファイル

Claude Codeは会話開始時に`CLAUDE.md`を自動的にコンテキストに読み込む。

**配置場所と優先順位:**

| 優先度 | 配置場所 | 用途 |
|-------|---------|-----|
| 1 | `./CLAUDE.md`（リポジトリルート） | 最も一般的 |
| 2 | `~/.claude/CLAUDE.md`（ホームディレクトリ） | 全セッション共通 |
| 3 | 親ディレクトリ | モノレポ構成で有用 |
| 4 | 子ディレクトリ | オンデマンドで読み込み |

**ファイル種類:**

| ファイル | 用途 |
|---------|-----|
| `CLAUDE.md` | gitにコミット可能（チーム共有） |
| `CLAUDE.local.md` | .gitignoreに追加して個人用 |

**読み込みタイミング:**
- 会話開始時にシステムプロンプト直後のユーザーメッセージとして提供

#### 利用手順

```bash
# 1. プロジェクトディレクトリに移動
cd your-project/

# 2. CLAUDE.mdを配置（ルールを記述）
# 3. テンプレートを配置
# 4. Claude Codeを起動して図解を依頼
```

#### --append-system-prompt フラグ（代替方法）

```bash
claude --append-system-prompt "Always generate drawio files following rules in CLAUDE.md"
```

### 4.2 Claude Web / Desktop

**Projects機能を使用**

#### 概要

Projectsは専用ワークスペースで、ドキュメントとカスタム指示を一元管理。

#### 主な機能

| 機能 | 説明 |
|-----|-----|
| Knowledge Base | ドキュメントをアップロードしてClaudeと共有 |
| カスタム指示 | プロジェクト固有の振る舞いを設定 |
| コンテキスト | 200K（約500ページ分）の容量 |

#### 設定手順

1. [claude.ai/projects](https://claude.ai/projects) にアクセス
2. 「+ New Project」をクリック
3. プロジェクト名・説明を入力
4. Knowledge Baseにルールファイル（core-rules.md）をアップロード
5. カスタム指示を設定

#### 制限事項

- Pro/Max/Teamプランが必要
- ファイルは手動アップロード必要
- チャット間でコンテキストは共有されない（Knowledge Baseのみ共有）

### 4.3 Claude API

#### System Prompt方式

```python
import anthropic

client = anthropic.Anthropic()

# ルールファイルを読み込み
with open("rules/core-rules.md", "r") as f:
    drawio_rules = f.read()

response = client.messages.create(
    model="claude-sonnet-4-20250514",
    system=f"""
    あなたはdrawio形式の図解を生成するアシスタントです。
    以下のルールに従って図解を生成してください：

    {drawio_rules}
    """,
    messages=[
        {"role": "user", "content": "システムアーキテクチャ図を作成してください"}
    ]
)
```

### 4.4 Claude Skills（将来対応）

2025年11月より提供開始。専門的なタスク実行のためのカスタムオンボーディング材料。

#### 特徴

| 特徴 | 説明 |
|-----|-----|
| 選択的読み込み | 関連するスキルのみ活性化 |
| 積層可能性 | 複数スキルが協調動作 |
| 移植性 | Claude apps、Claude Code、APIで同一形式 |
| 効率性 | パフォーマンス最適化 |

#### ファイル構造

```
skill-folder/
├── SKILL.md          # スキル定義
├── instructions/     # 詳細指示
├── scripts/          # スクリプト
└── resources/        # リソース
```

---

## 5. drawio生成コアルール

> 出典: [Zenn: Claude Code での draw.io 図作成ガイド](https://zenn.dev/genda_jp/articles/2025-12-12-drawio-tips-claude-code)

### 5.1 フォント設定

**最重要ルール: mxGraphModel属性だけでは不十分**

| ルール | 詳細 |
|-------|-----|
| mxGraphModel属性だけでは不十分 | `defaultFontFamily`属性を設定しても各要素には反映されない |
| 全テキスト要素に個別設定必須 | すべてのテキスト要素のstyleに`fontFamily=フォント名;`を追加 |
| PNG出力時の注意 | 各要素レベルでの指定がないとフォントが反映されない |

**正しい例:**

```xml
<mxCell style="text;fontFamily=Helvetica;fontSize=18;" ... />
```

**誤った例:**

```xml
<!-- これだけでは不十分 -->
<mxGraphModel defaultFontFamily="Helvetica">
  <mxCell style="text;" ... />  <!-- fontFamilyが欠落 -->
</mxGraphModel>
```

### 5.2 矢印と配置

| ルール | 詳細 |
|-------|-----|
| XML記述順 = 描画順 | 先に記述した要素が背面に配置される |
| 図形を先に記述 | 図形（vertex）を最背面に配置するため、XMLの先頭に記述 |
| 矢印は後に記述 | 矢印（edge）を最前面に配置するため、図形の後に記述 |
| ラベル間隔 | 矢印ラベルは矢印から最低20px以上離す |
| 接続方法 | テキスト要素への接続は`exitY/entryY`より明示的座標が確実 |

### 5.3 テキストサイズ

| ルール | 詳細 |
|-------|-----|
| フォントサイズ | 標準の1.5倍（18px程度）を推奨 |
| 日本語テキスト | 1文字あたり約30-40pxを確保 |
| 改行防止 | 十分な幅を確保して意図しない改行を防止 |

### 5.4 背景設定

| ルール | 詳細 |
|-------|-----|
| 背景色 | 透明に設定（`background="none"`） |
| page属性 | `page="0"`を指定 |

### 5.5 XML構造テンプレート

```xml
<mxfile host="app.diagrams.net" agent="Claude" version="26.0.0">
  <diagram name="Page-1" id="unique-id">
    <mxGraphModel
      dx="0"
      dy="0"
      grid="1"
      gridSize="10"
      guides="1"
      tooltips="1"
      connect="1"
      arrows="1"
      fold="1"
      page="0"
      pageScale="1"
      pageWidth="827"
      pageHeight="1169"
      background="none"
      defaultFontFamily="Helvetica">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- ========================================
             図形（vertex）を先に配置 → 背面になる
             ======================================== -->
        <mxCell id="box-1"
                value="開始"
                style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontFamily=Helvetica;fontSize=18;fontColor=#333333;"
                vertex="1"
                parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>

        <mxCell id="box-2"
                value="終了"
                style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontFamily=Helvetica;fontSize=18;fontColor=#333333;"
                vertex="1"
                parent="1">
          <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
        </mxCell>

        <!-- ========================================
             矢印（edge）を後に配置 → 最前面になる
             ======================================== -->
        <mxCell id="arrow-1"
                style="edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;strokeWidth=2;strokeColor=#333333;fontFamily=Helvetica;fontSize=12;fontColor=#666666;endArrow=classic;endFill=1;"
                edge="1"
                parent="1"
                source="box-1"
                target="box-2">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 6. チェックリスト

### 6.1 生成前チェックリスト

Claudeに渡すルールに含めるべき項目：

- [ ] mxGraphModelに`defaultFontFamily`設定
- [ ] mxGraphModelに`background="none"`設定
- [ ] mxGraphModelに`page="0"`設定
- [ ] 図形（vertex）をXML先頭（背面）に配置するルール
- [ ] 矢印（edge）を図形の後（最前面）に配置するルール
- [ ] すべてのテキスト要素に`fontFamily`を明示するルール
- [ ] フォントサイズ18px以上のルール
- [ ] 日本語テキスト幅30-40px/文字のルール

### 6.2 生成後チェックリスト

生成されたdrawioファイルの確認項目：

- [ ] 全テキスト要素にfontFamily設定済み
- [ ] フォントサイズ18px以上
- [ ] 矢印が最前面に配置されている
- [ ] 矢印とラベルの間隔20px以上
- [ ] 日本語テキストに意図しない改行なし
- [ ] drawioアプリで開いて視覚確認
- [ ] PNG出力で最終確認

---

## 7. 推奨ディレクトリ構造

```
drawio_rule_for_claude/
├── CLAUDE.md              # メインルール（Claude Code自動認識）
├── SKILL.md               # Skills機能用（将来対応）
├── README.md              # プロジェクト説明
│
├── research/              # 調査資料（本ディレクトリ）
│   ├── README.md          # ← 本ドキュメント
│   ├── _index.md
│   ├── platform-comparison.md
│   ├── feasibility-report.md
│   └── drawio-rules-summary.md
│
├── rules/
│   ├── core-rules.md      # コアルール（Web/Desktop用にも）
│   ├── style-guide.md     # カラー・図形・フォントのルール
│   ├── layout-guide.md    # 座標・サイズ・間隔・接続のルール
│   ├── checklist.md       # 生成前後チェックリスト
│   └── prompt-template.md # 依頼用プロンプトテンプレート
│
├── templates/
│   ├── drawio/            # drawio形式テンプレート
│   │   ├── basic.drawio
│   │   ├── flowchart.drawio
│   │   ├── architecture.drawio
│   │   ├── context.drawio
│   │   ├── er-diagram.drawio
│   │   ├── screen-flow.drawio
│   │   ├── sequence.drawio
│   │   ├── state-transition.drawio
│   │   └── usecase.drawio
│   │
│   └── xml/               # XML形式テンプレート（他ツール連携用）
│       ├── basic.xml
│       ├── flowchart.xml
│       ├── architecture.xml
│       ├── context.xml
│       ├── er-diagram.xml
│       ├── screen-flow.xml
│       ├── sequence.xml
│       ├── state-transition.xml
│       └── usecase.xml
│
└── examples/
    ├── good-example.drawio  # 良い例
    ├── good-example.png     # 出力結果
    └── bad-example.drawio   # 悪い例（アンチパターン）
```

---

## 8. プロンプトテンプレート

Claudeに図解生成を依頼する際のテンプレートです。詳細は `rules/prompt-template.md` を参照してください。

### 8.1 基本テンプレート

```
## 依頼

以下の情報を元に、{図解の種類}をdrawio形式で生成してください。

## 図解の種類

{業務フロー図 / システム構成図 / 画面遷移図 / データフロー図 / ER図 / シーケンス図}

## 入力情報

{ここに元ソースを貼り付け、またはファイルパスを指定}

## 出力要件

- ファイル名: {output.drawio}
- 要素数目安: {10-15個程度}
```

### 8.2 図解種類別テンプレート

| 図解の種類 | 主な用途 | 含めるべき要素 |
|-----------|---------|---------------|
| 業務フロー図 | 業務手順の可視化 | 開始/終了、処理ステップ、分岐、担当者 |
| システム構成図 | システム全体像 | コンポーネント、データフロー、外部連携 |
| 画面遷移図 | UI/UX設計 | 画面名、遷移矢印、アクション |
| データフロー図 | データ処理の流れ | 外部エンティティ、プロセス、データストア |
| ER図 | データベース設計 | エンティティ、属性、リレーション |
| シーケンス図 | 処理順序 | アクター、ライフライン、メッセージ |
| ユースケース図 | アクターと機能の関係 | アクター、ユースケース楕円、関連線 |
| コンテキスト図 | システム境界の明示 | 中央システム、外部エンティティ、データフロー |
| 状態遷移図 | 状態変化の定義 | 状態、遷移矢印、イベント/条件 |

### 8.3 クイックプロンプト

急いでいる場合の最短形式：

```
{入力情報}を元に{図解の種類}を作成して。drawio形式で出力。
```

---

## 9. 運用フロー

### 9.1 基本フロー

```
┌─────────────────────────────────────────────────────────────┐
│                        準備フェーズ                          │
├─────────────────────────────────────────────────────────────┤
│  1. CLAUDE.md をプロジェクトルートに配置                      │
│  2. テンプレート（.drawio）を templates/ に配置              │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                        生成フェーズ                          │
├─────────────────────────────────────────────────────────────┤
│  3. Claudeに図解を依頼（例: 「システム構成図を作成して」）    │
│  4. Claudeがdrawio形式のXMLを生成                            │
│  5. .drawioファイルとして保存                                │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                        検証フェーズ                          │
├─────────────────────────────────────────────────────────────┤
│  6. drawioアプリで開いて確認                                 │
│  7. 必要に応じて手動調整                                     │
│  8. PNG/SVG出力                                              │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                        改善フェーズ                          │
├─────────────────────────────────────────────────────────────┤
│  9. 問題があればCLAUDE.mdのルールを調整                      │
│ 10. 反復的に品質向上                                         │
└─────────────────────────────────────────────────────────────┘
```

### 9.2 PNG変換コマンド

```bash
# drawio CLIでPNG出力
drawio -x -f png -s 2 -t -o output.png input.drawio
```

**オプション説明:**

| オプション | 意味 |
|-----------|-----|
| `-x` | エクスポートモード |
| `-f png` | PNG形式 |
| `-s 2` | 2倍スケール（高解像度） |
| `-t` | 透明背景 |
| `-o` | 出力ファイル指定 |

---

## 10. 次のステップ

### Phase 1: 基盤構築（推奨最初のアクション）

1. CLAUDE.mdにdrawioコアルールを記述
2. 基本テンプレートファイル（basic.drawio）を作成
3. Claude Codeで簡単な図を生成してテスト

### Phase 2: 品質検証

1. 複数パターンの図（フローチャート、アーキテクチャ図等）を生成
2. 生成結果をチェックリストで検証
3. 問題点を洗い出し

### Phase 3: ルール改善

1. 問題点を基にCLAUDE.mdを更新
2. テンプレートを追加・改善
3. 良い例・悪い例をexamples/に蓄積

### Phase 4: クロスプラットフォーム対応

1. Web/Desktop用にProjects用ファイルを整備
2. API利用者向けのドキュメント整備
3. Skills対応（将来）

---

## 11. 参考リンク

### 公式ドキュメント

| リソース | URL |
|---------|-----|
| Claude Projects - Anthropic | https://www.anthropic.com/news/projects |
| Claude Skills - Anthropic | https://claude.com/blog/skills |
| How to create and manage projects | https://support.claude.com/en/articles/9519177-how-can-i-create-and-manage-projects |
| Claude Code Best Practices | https://www.anthropic.com/engineering/claude-code-best-practices |

### 技術リソース

| リソース | URL |
|---------|-----|
| CLAUDE.md Best Practices - Arize | https://arize.com/blog/claude-md-best-practices-learned-from-optimizing-claude-code-with-prompt-learning/ |
| Zenn: drawio-tips-claude-code | https://zenn.dev/genda_jp/articles/2025-12-12-drawio-tips-claude-code |

---

## 付録: Claude向け指示テンプレート

以下はCLAUDE.mdに記述する際の参考テンプレートです：

```markdown
# drawio図解生成ルール

以下のルールに従ってdrawio形式のXMLを生成してください：

## 1. mxGraphModel設定
- `defaultFontFamily`を設定
- `background="none"`で透明背景
- `page="0"`を指定

## 2. フォント設定（最重要）
- すべてのテキスト要素に`fontFamily=フォント名;`を明示
- フォントサイズは18px以上
- 図形には`fontColor=#333333`を指定

## 3. 要素配置順（描画順序）
- 凡例グループ（最背面）
- 図形（vertex）を先に記述（背面に配置）
- 矢印（edge）を後に記述（最前面に配置）

## 4. 日本語テキスト
- 1文字あたり30-40pxの幅を確保
- 意図しない改行を防止

## 5. 矢印ラベル
- フォントサイズ12px、文字色`fontColor=#666666`
- 矢印から20px以上離す
```
