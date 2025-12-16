# drawio図解生成コアルール

このドキュメントはClaude Web/Desktop（Projects機能）およびAPI利用時に使用するルールです。

## 概要

drawio形式（.drawio）のXMLファイルを生成する際に遵守すべきルールを定義します。

---

## 1. mxGraphModel設定

XMLのルート構造に以下の属性を設定してください：

```xml
<mxfile host="Electron">
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
        ...
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### 必須属性

| 属性 | 値 | 理由 |
|-----|-----|-----|
| `background` | `"none"` | 透明背景にする |
| `page` | `"0"` | ページ境界を非表示にする |
| `defaultFontFamily` | `"Helvetica"` | デフォルトフォントを設定 |

---

## 2. フォント設定（最重要）

### 注意: mxGraphModelのdefaultFontFamily属性だけでは不十分

`defaultFontFamily`を設定しても、各要素のstyleには反映されません。
PNG出力時にフォントが正しく適用されない原因になります。

### 必須対応

すべてのmxCell要素のstyle属性に以下を必ず含めてください：

| 属性 | 値 | 理由 |
|-----|-----|-----|
| `fontFamily` | `Helvetica` | フォントを明示的に指定 |
| `fontSize` | `18` | 標準の1.5倍、視認性確保 |

### 正しい例

```xml
<mxCell
  value="テキスト"
  style="rounded=1;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=18;"
  vertex="1"
  parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 誤った例

```xml
<!-- fontFamilyとfontSizeが欠落 - PNG出力でフォントが反映されない -->
<mxCell
  value="テキスト"
  style="rounded=1;whiteSpace=wrap;html=1;"
  vertex="1"
  parent="1">
  ...
</mxCell>
```

---

## 3. 要素配置順（描画順序）

### ルール

XMLの記述順序が描画順序を決定します：

| 記述順 | 配置 |
|-------|-----|
| 先に記述 | 背面に配置 |
| 後に記述 | 前面に配置 |

### 推奨順序

```xml
<root>
  <mxCell id="0" />
  <mxCell id="1" parent="0" />

  <!-- 1. 凡例グループ（最背面） -->
  <mxCell id="legend" style="swimlane;..." vertex="1" ... />

  <!-- 2. 図形（vertex）を先に記述 → 背面 -->
  <mxCell id="box-1" vertex="1" ... />
  <mxCell id="box-2" vertex="1" ... />

  <!-- 3. 矢印（edge）を後に記述 → 最前面 -->
  <mxCell id="arrow-1" edge="1" ... />
  <mxCell id="arrow-2" edge="1" ... />
</root>
```

### 理由

矢印を最前面に配置することで、図形と重なった際も矢印の接続が明確に視認できます。

---

## 4. 日本語テキスト

### サイズ計算

| 項目 | 推奨値 |
|-----|-------|
| 1文字あたりの幅 | 30-40px |
| フォントサイズ | 18px以上 |

### 例

```xml
<!-- 4文字の日本語テキスト「処理開始」 → 幅120-160px必要 -->
<mxCell value="処理開始" ...>
  <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
</mxCell>
```

### 注意点

- 幅が不足すると意図しない改行が発生する
- 十分な幅を確保して視認性を維持する

---

## 5. 矢印ラベル

### ルール

| 項目 | 推奨値 |
|-----|-------|
| ラベルと矢印の間隔 | 20px以上 |
| 接続方法 | 明示的座標を推奨 |

### 理由

- `exitY/entryY`より明示的座標のほうが確実に接続される
- ラベルが矢印と重なると読みづらい

---

## 6. よく使うスタイル

### 角丸矩形（ボックス）

```
rounded=1;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=18;
```

### 矢印（エッジ）

```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;strokeWidth=2;strokeColor=#333333;fontFamily=Helvetica;fontSize=12;fontColor=#666666;endArrow=classic;endFill=1;
```

### 色付きボックス

| 用途 | fillColor | strokeColor |
|-----|-----------|-------------|
| 開始/入力 | `#dae8fc` | `#6c8ebf` |
| 処理 | `#fff2cc` | `#d6b656` |
| 終了/出力 | `#d5e8d4` | `#82b366` |
| 警告/注意 | `#f8cecc` | `#b85450` |

---

## 7. 完全なテンプレート

```xml
<mxfile host="app.diagrams.net" agent="Claude" version="26.0.0">
  <diagram name="Page-1" id="template">
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

        <!-- 図形を先に配置（背面） -->
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

        <!-- 矢印を後に配置（最前面） -->
        <mxCell id="edge-1"
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
