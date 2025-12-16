---
created: 2025-12-15
tags: [tech/tool, drawio, claude, status/done]
aliases: []
---

# drawio生成ルール サマリ

## 概要

Zenn記事「Claude Code での draw.io 図作成ガイド」から抽出したコアルール。
Claudeがdrawio形式のXMLを生成する際に遵守すべき事項をまとめる。

## 出典

- [Zenn: drawio-tips-claude-code](https://zenn.dev/genda_jp/articles/2025-12-12-drawio-tips-claude-code)

## コアルール

### 1. フォント設定

| ルール | 詳細 |
|-------|-----|
| mxGraphModel属性だけでは不十分 | `defaultFontFamily`属性を設定しても各要素には反映されない |
| 全テキスト要素に個別設定必須 | すべてのテキスト要素のstyleに`fontFamily=フォント名;`を追加 |
| PNG出力時の注意 | 各要素レベルでの指定がないとフォントが反映されない |

**正しい例:**
```xml
<mxCell style="text;fontFamily=Helvetica;fontSize=18;" ... />
```

### 2. 矢印と配置

| ルール | 詳細 |
|-------|-----|
| XML記述順 = 描画順 | 先に記述した要素が背面に配置される |
| 図形を先に記述 | 図形（vertex）を最背面に配置するため、XMLの先頭に記述 |
| 矢印は後に記述 | 矢印（edge）を最前面に配置するため、図形の後に記述 |
| ラベル間隔 | 矢印ラベルは矢印から最低20px以上離す |
| 接続方法 | テキスト要素への接続は`exitY/entryY`より明示的座標が確実 |

### 3. テキストサイズ

| ルール | 詳細 |
|-------|-----|
| フォントサイズ | 標準の1.5倍（18px程度）を推奨 |
| 日本語テキスト | 1文字あたり約30-40pxを確保 |
| 改行防止 | 十分な幅を確保して意図しない改行を防止 |

### 4. 背景設定

| ルール | 詳細 |
|-------|-----|
| 背景色 | 透明に設定（`background="none"`） |
| page属性 | `page="0"`を指定 |

## XML構造テンプレート

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

        <!-- 図形を先に配置（背面） -->
        <mxCell id="box-1" value="テキスト" style="rounded=1;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=18;fontColor=#333333;..." vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>

        <!-- 矢印を後に配置（最前面） -->
        <mxCell id="arrow-1" style="edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;strokeWidth=2;strokeColor=#333333;fontFamily=Helvetica;fontSize=12;fontColor=#666666;endArrow=classic;endFill=1;" edge="1" parent="1" source="..." target="...">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Claude向け指示テンプレート

以下のルールに従ってdrawio形式のXMLを生成してください：

1. **mxGraphModel設定**
   - `defaultFontFamily`を設定
   - `background="none"`で透明背景
   - `page="0"`を指定

2. **フォント設定**
   - すべてのテキスト要素に`fontFamily=フォント名;`を明示
   - フォントサイズは18px以上

3. **要素配置順**
   - 図形（vertex）をXMLの先頭に記述（背面）
   - 矢印（edge）を後に記述（最前面）

4. **日本語テキスト**
   - 1文字あたり30-40pxの幅を確保
   - 意図しない改行を防止

5. **矢印ラベル**
   - 矢印から20px以上離す

## 生成前チェックリスト

- [ ] mxGraphModelに`defaultFontFamily`設定済み
- [ ] mxGraphModelに`background="none"`設定済み
- [ ] mxGraphModelに`page="0"`設定済み
- [ ] 図形（vertex）がXML先頭（背面）に配置されている
- [ ] 矢印（edge）が図形の後（最前面）に配置されている
- [ ] すべてのテキスト要素に`fontFamily`設定済み
- [ ] フォントサイズ18px以上

## 生成後チェックリスト

- [ ] 全テキスト要素にfontFamily設定済み
- [ ] フォントサイズ18px以上
- [ ] 矢印が最前面に配置されている
- [ ] 矢印とラベルの間隔20px以上
- [ ] 日本語テキストに意図しない改行なし
- [ ] PNG出力で視覚確認完了

## PNG変換コマンド

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

## 重要な注意点

1. **Claudeはdrawio特有の挙動を初期認識していない**
   - 明確なルール定義が必須
   - チェックリストで確認を徹底

2. **テスト・検証が重要**
   - 生成後は必ずPNG出力して視覚確認
   - 問題があればルールを調整

3. **反復改善**
   - 生成結果を基にルールを継続的に改善
