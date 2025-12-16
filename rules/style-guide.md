# drawio スタイルガイド

図解生成時のビジュアルルールを定義します。

---

## 1. カラーパレット

### 1.1 基本カラー（用途別）

| 用途 | 背景色（fillColor） | 枠線色（strokeColor） | 使用場面 |
|-----|--------------------|--------------------|---------|
| 入力/開始/プライマリ | `#dae8fc` | `#6c8ebf` | 開始点、入力、主要コンポーネント |
| 処理/中間/セカンダリ | `#fff2cc` | `#d6b656` | 処理中、中間状態、アプリ層 |
| 出力/完了/成功 | `#d5e8d4` | `#82b366` | 終了点、完了、成功状態 |
| 警告/エラー/外部 | `#f8cecc` | `#b85450` | エラー、キャンセル、外部システム |
| その他/補助 | `#e1d5e7` | `#9673a6` | 認証、補助機能、その他 |
| 中立/グレー | `#f5f5f5` | `#666666` | 境界線、背景、中立要素 |

### 1.2 システム構成図のカラールール

| 要素 | 背景色 | 枠線色 | 説明 |
|-----|--------|--------|-----|
| クライアント/フロントエンド | `#dae8fc` | `#6c8ebf` | ユーザーに近い層 |
| アプリケーション層 | `#fff2cc` | `#d6b656` | ビジネスロジック |
| データ層/DB | `#d5e8d4` | `#82b366` | データ永続化 |
| 外部API/サードパーティ | `#f8cecc` | `#b85450` | 外部連携（破線枠推奨） |
| 認証/セキュリティ | `#e1d5e7` | `#9673a6` | 認証関連コンポーネント |

### 1.3 業務フロー図のカラールール

| 要素 | 背景色 | 枠線色 | 説明 |
|-----|--------|--------|-----|
| 開始 | `#d5e8d4` | `#82b366` | フローの開始点（楕円） |
| 終了 | `#f8cecc` | `#b85450` | フローの終了点（楕円） |
| 処理 | `#dae8fc` | `#6c8ebf` | 処理ステップ（長方形） |
| 分岐/判断 | `#fff2cc` | `#d6b656` | 条件分岐（ひし形） |
| サブプロセス | `#e1d5e7` | `#9673a6` | 別フローの参照 |

### 1.4 状態遷移図のカラールール

| 状態 | 背景色 | 枠線色 | 説明 |
|-----|--------|--------|-----|
| 初期状態 | `#dae8fc` | `#6c8ebf` | 最初の状態 |
| 中間状態（正常） | `#fff2cc` | `#d6b656` | 処理中の状態 |
| 完了状態 | `#d5e8d4` | `#82b366` | 正常終了 |
| 異常/キャンセル状態 | `#f8cecc` | `#b85450` | 異常終了、キャンセル |

### 1.5 ER図のカラールール

| エンティティ種類 | 背景色 | 枠線色 | 説明 |
|----------------|--------|--------|-----|
| マスタテーブル | `#dae8fc` | `#6c8ebf` | Users, Products等 |
| トランザクションテーブル | `#fff2cc` | `#d6b656` | Orders, Logs等 |
| 中間テーブル | `#d5e8d4` | `#82b366` | 多対多の中間テーブル |
| 外部参照 | `#f8cecc` | `#b85450` | 外部システムのデータ |

### 1.6 画面遷移図のカラールール

| 画面種類 | 背景色 | 枠線色 | 説明 |
|---------|--------|--------|-----|
| 認証画面 | `#e1d5e7` | `#9673a6` | ログイン、登録等 |
| 一覧/検索画面 | `#dae8fc` | `#6c8ebf` | リスト表示 |
| 詳細/参照画面 | `#dae8fc` | `#6c8ebf` | 詳細表示（読み取り） |
| 入力/編集画面 | `#fff2cc` | `#d6b656` | フォーム入力 |
| 完了/確認画面 | `#d5e8d4` | `#82b366` | 処理完了 |
| エラー画面 | `#f8cecc` | `#b85450` | エラー表示 |

---

## 2. 図形ルール

### 2.1 基本図形

| 図形 | style属性 | 用途 |
|-----|----------|-----|
| 角丸四角形 | `rounded=1` | 汎用ボックス、状態 |
| 四角形 | `rounded=0` | 処理、画面、エンティティ |
| 楕円 | `ellipse` | 開始/終了、ユースケース |
| ひし形 | `rhombus` | 分岐、判断 |
| 円柱 | `shape=cylinder3` | データベース |
| 人型 | `shape=umlActor` | アクター |

### 2.2 図形詳細設定

| 項目 | 値 | style属性 | 説明 |
|-----|-----|----------|-----|
| 角丸の半径 | 10px | `arcSize=10` | rounded=1時の丸みの大きさ |
| 円柱のサイズ | 15px | `size=15` | cylinder3の蓋部分の高さ |
| 影 | なし（推奨） | `shadow=0` | 影を付けない（シンプル優先） |
| 不透明度 | 100% | `opacity=100` | 完全に不透明 |
| 背景アウトライン | 有効 | `backgroundOutline=1` | 円柱等で背景を描画 |
| ラベル境界 | 有効 | `boundedLbl=1` | ラベルを図形内に収める |
| 折り返し | 有効 | `whiteSpace=wrap` | テキストを図形内で折り返し |

### 2.3 図形サイズの目安

| 図形タイプ | 推奨サイズ (W x H) | 備考 |
|-----------|------------------|-----|
| 通常ボックス | 140 x 60 | 4-6文字程度 |
| 大きいボックス | 180 x 80 | 8文字以上、複数行 |
| 円/楕円（プロセス） | 100 x 70 | DFDプロセス |
| 円/楕円（システム） | 160 x 100 | コンテキスト図中央 |
| データベース円柱 | 140 x 80 | size=15推奨 |
| アクター人型 | 30 x 50 | verticalLabelPosition=bottom |
| 凡例サンプル図形 | 25 x 20 | 凡例内の小さいサンプル |

### 2.4 図解種類別の図形

#### 業務フロー図

| 要素 | 図形 | style |
|-----|------|-------|
| 開始/終了 | 楕円 | `ellipse;whiteSpace=wrap;html=1;` |
| 処理 | 四角形 | `rounded=0;whiteSpace=wrap;html=1;` |
| 分岐 | ひし形 | `rhombus;whiteSpace=wrap;html=1;` |

#### システム構成図

| 要素 | 図形 | style |
|-----|------|-------|
| コンポーネント | 角丸四角形 | `rounded=1;whiteSpace=wrap;html=1;` |
| データベース | 円柱 | `shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=15;` |
| 外部システム | 角丸四角形（破線） | `rounded=1;whiteSpace=wrap;html=1;dashed=1;` |

#### ユースケース図

| 要素 | 図形 | style |
|-----|------|-------|
| アクター | 人型 | `shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;` |
| ユースケース | 楕円 | `ellipse;whiteSpace=wrap;html=1;` |
| システム境界 | 四角形（破線） | `rounded=0;whiteSpace=wrap;html=1;dashed=1;verticalAlign=top;` |

#### ER図

| 要素 | 図形 | style |
|-----|------|-------|
| エンティティ | swimlane | `swimlane;fontStyle=1;childLayout=stackLayout;horizontal=1;startSize=30;...` |
| 属性行 | text | `text;strokeColor=none;fillColor=none;align=left;...` |

#### データフロー図（DFD）

| 要素 | 図形 | style |
|-----|------|-------|
| 外部エンティティ | 四角形 | `rounded=0;whiteSpace=wrap;html=1;` |
| プロセス | 角丸四角形/円 | `rounded=1;whiteSpace=wrap;html=1;` または `ellipse;whiteSpace=wrap;html=1;` |
| データストア | 二重線四角 | `shape=partialRectangle;whiteSpace=wrap;html=1;left=0;right=0;fillColor=none;` |
| データフロー | 矢印 | `endArrow=block;html=1;strokeWidth=2;` |

#### シーケンス図

| 要素 | 図形 | style |
|-----|------|-------|
| アクター | 人型 | `shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;` |
| オブジェクト | 四角形 | `rounded=0;whiteSpace=wrap;html=1;` |
| ライフライン | 破線 | `dashed=1;dashPattern=8 8;strokeColor=#999999;` |
| メッセージ（呼び出し） | 実線矢印 | `endArrow=block;html=1;strokeWidth=2;` |
| メッセージ（戻り値） | 破線矢印 | `dashed=1;endArrow=open;html=1;strokeWidth=2;` |
| アクティベーション | 細長い四角 | `rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;` |

#### 画面遷移図

| 要素 | 図形 | style |
|-----|------|-------|
| 画面 | 四角形 | `rounded=0;whiteSpace=wrap;html=1;verticalAlign=top;spacingTop=10;` |
| 遷移（通常） | 実線矢印 | `endArrow=block;html=1;strokeWidth=2;` |
| 遷移（戻る） | 破線矢印 | `dashed=1;endArrow=block;html=1;strokeWidth=2;` |
| モーダル/ダイアログ | 角丸四角形 | `rounded=1;whiteSpace=wrap;html=1;dashed=1;` |

#### コンテキスト図

| 要素 | 図形 | style |
|-----|------|-------|
| 対象システム | 円/楕円 | `ellipse;whiteSpace=wrap;html=1;` |
| 外部エンティティ | 四角形 | `rounded=0;whiteSpace=wrap;html=1;` |
| データフロー | 矢印 | `endArrow=block;html=1;strokeWidth=2;` |

#### 状態遷移図

| 要素 | 図形 | style |
|-----|------|-------|
| 状態 | 角丸四角形 | `rounded=1;whiteSpace=wrap;html=1;` |
| 開始状態 | 黒丸 | `ellipse;whiteSpace=wrap;html=1;fillColor=#000000;strokeColor=#000000;` |
| 終了状態 | 二重丸 | `ellipse;whiteSpace=wrap;html=1;fillColor=#000000;strokeColor=#000000;strokeWidth=3;` + 内側に白丸 |
| 遷移 | 矢印 | `endArrow=block;html=1;strokeWidth=2;` |
| 遷移（異常系） | 赤矢印 | `endArrow=block;html=1;strokeWidth=2;dashed=1;strokeColor=#b85450;` |

---

## 3. 矢印ルール

### 3.1 基本設定

| 項目 | 値 | style属性 | 説明 |
|-----|-----|----------|-----|
| 線の太さ | 2px | `strokeWidth=2` | 視認性確保 |
| 線の色 | 黒 | `strokeColor=#333333` | 視認性のため濃いグレー |
| エッジスタイル | 直交 | `edgeStyle=orthogonalEdgeStyle` | 直角に曲がる |
| 角の丸み | 丸み | `rounded=1` | 曲がり角を丸くする |
| ジェットサイズ | 自動 | `jettySize=auto` | 接続部の長さ |
| ループ処理 | 有効 | `orthogonalLoop=1` | 自己参照時の処理 |
| 矢印の形 | クラシック | `endArrow=classic` | 視認性の高い三角形 |
| 矢印塗りつぶし | 有効 | `endFill=1` | 矢印を塗りつぶす |

### 3.2 エッジスタイルの種類

| スタイル | style属性 | 用途 |
|---------|----------|-----|
| 直交（推奨） | `edgeStyle=orthogonalEdgeStyle` | 通常のフロー、構成図 |
| 直線 | `edgeStyle=none` | シンプルな接続 |
| 曲線 | `edgeStyle=orthogonalEdgeStyle;curved=1` | 複雑な経路（交差回避） |

### 3.3 矢印の種類

| 種類 | style属性 | 用途 |
|-----|----------|-----|
| 実線矢印（推奨） | `endArrow=classic;endFill=1` | 通常のフロー、呼び出し |
| 破線矢印 | `dashed=1;endArrow=classic;endFill=1` | 戻り値、オプション |
| 線のみ | `endArrow=none` | 関連（ユースケース図） |
| 開いた矢印 | `endArrow=open` | 軽い参照、include関係 |

**矢印形状の比較:**
| 形状 | style | 視認性 | 推奨 |
|-----|-------|-------|-----|
| classic | `endArrow=classic;endFill=1` | 高 | 推奨 |
| block | `endArrow=block;endFill=1` | 中 | - |
| open | `endArrow=open` | 低 | 破線用 |

### 3.4 双方向矢印

**重要**: 双方向の矢印は2本の別々の矢印に分離する。1本の矢印に`startArrow`と`endArrow`を両方設定するとラベルが重なるため避ける。

```xml
<!-- 推奨: 2本の矢印で表現 -->
<!-- 往路 -->
<mxCell id="arrow-1" value="リクエスト" edge="1" source="A" target="B">
  <mxGeometry relative="1" as="geometry">
    <mxPoint y="-10" as="offset" />
  </mxGeometry>
</mxCell>
<!-- 復路 -->
<mxCell id="arrow-2" value="レスポンス" edge="1" source="B" target="A">
  <mxGeometry relative="1" as="geometry">
    <mxPoint y="10" as="offset" />
  </mxGeometry>
</mxCell>
```

双方向を1本で表す場合（ラベルなしのみ）:
```
endArrow=classic;startArrow=classic;endFill=1;startFill=1;
```

### 3.5 特殊な矢印

| 用途 | style | 説明 |
|-----|-------|-----|
| 戻り処理/キャンセル | `dashed=1;strokeColor=#b85450` | 赤の破線 |
| include関係 | `dashed=1;endArrow=open` | ユースケース図 |
| ER関係（1:N） | `endArrow=ERmany;startArrow=ERone` | ER図のリレーション |

### 3.6 経路指定（中継点）

複雑な接続で経路をカスタマイズする場合、mxGeometry内にArrayで中継点を指定:

```xml
<mxGeometry relative="1" as="geometry">
  <Array as="points">
    <mxPoint x="300" y="200" />
    <mxPoint x="400" y="200" />
  </Array>
</mxGeometry>
```

| 項目 | 説明 |
|-----|-----|
| `relative="1"` | 相対位置モード |
| `mxPoint` | 経由する座標点 |
| 用途 | 矢印の交差回避、特定経路の強制 |

### 3.7 ラベル設定

| 項目 | 値 | style属性 | 説明 |
|-----|-----|----------|-----|
| フォントサイズ | 12px | `fontSize=12` | 図形より小さく |
| 文字色 | グレー | `fontColor=#666666` | 図形より薄く |
| フォント | Helvetica | `fontFamily=Helvetica` | 統一 |

矢印ラベルの完全なstyle例：
```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;strokeWidth=2;strokeColor=#333333;fontFamily=Helvetica;fontSize=12;fontColor=#666666;endArrow=classic;endFill=1;
```

### 3.8 ラベル配置

| 項目 | ルール |
|-----|-------|
| 位置 | 矢印から20px以上離す |
| 配置 | 矢印の中央または始点/終点付近 |

---

## 4. フォントルール

### 4.1 基本設定

| 項目 | 値 | style属性 |
|-----|-----|----------|
| フォント | Helvetica | `fontFamily=Helvetica;` |
| 基本サイズ | 18px | `fontSize=18;` |
| 文字色 | ダークグレー | `fontColor=#333333;` |

**重要**: `fontColor=#333333;` は必ず明示的に指定すること。省略するとswimlane等でデフォルト白になる場合がある。

### 4.2 サイズ使い分け

| 用途 | サイズ | 説明 |
|-----|-------|-----|
| 図形内テキスト | 18px | ボックス、状態名等 |
| 矢印ラベル | 14px | 遷移条件、メッセージ等 |
| 補足テキスト | 12px | 凡例、注釈等 |
| タイトル/見出し | 16px + 太字 | レイヤー名、グループ名 |

### 4.3 フォントスタイル

| 用途 | style | 説明 |
|-----|-------|-----|
| 通常 | - | 標準テキスト |
| 太字 | `fontStyle=1` | タイトル、重要項目 |
| 斜体 | `fontStyle=2` | FK（外部キー）、補足 |
| 下線 | `fontStyle=4` | PK（主キー） |

### 4.4 日本語テキスト

| 項目 | ルール |
|-----|-------|
| 幅の目安 | 1文字あたり30-40px |
| 改行防止 | 十分な幅を確保 |
| 例 | 4文字 → width="140" 以上 |

---

## 5. グループ/コンテナルール

### 5.1 swimlane（グループコンテナ）

要素をグループ化する際はswimlaneスタイルを使用:

| 項目 | 値 | style属性 | 説明 |
|-----|-----|----------|-----|
| コンテナ方向 | 水平 | `horizontal=1` | ヘッダーが上部 |
| ヘッダー高さ | 25-30px | `startSize=25` | グループ名表示領域 |
| 折りたたみ | 無効 | `collapsible=0` | 折りたたみボタン非表示 |

### 5.2 グループの基本スタイル

```
swimlane;horizontal=1;startSize=25;fillColor=#f5f5f5;strokeColor=#666666;fontFamily=Helvetica;fontSize=14;fontStyle=1;fontColor=#333333;
```

### 5.3 グループ種類別の設定

| グループ用途 | fillColor | strokeColor | 説明 |
|------------|-----------|-------------|-----|
| 凡例 | `#f5f5f5` | `#666666` | グレー（中立） |
| プロキシ層/入力 | `#dae8fc` | `#6c8ebf` | 青 |
| アプリ層/処理 | `#fff2cc` | `#d6b656` | 黄 |
| データ層/出力 | `#d5e8d4` | `#82b366` | 緑 |
| 外部エンティティ | `#fff2cc` | `#d6b656` | 黄（外部） |

### 5.4 親子関係（parent属性）

グループ内に要素を配置する際はparent属性を指定:

```xml
<!-- グループ定義 -->
<mxCell id="group-1" value="グループ名" style="swimlane;..." vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="200" height="150" as="geometry" />
</mxCell>

<!-- グループ内の要素（parent="group-1"） -->
<mxCell id="item-1" value="要素" style="..." vertex="1" parent="group-1">
  <mxGeometry x="20" y="40" width="100" height="50" as="geometry" />
</mxCell>
```

**重要**: グループ内要素の座標はグループ左上からの相対座標。

### 5.5 境界線（破線コンテナ）

Docker Network境界などの論理境界を表す場合:

```
rounded=0;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#666666;strokeWidth=2;dashed=1;verticalAlign=top;spacingTop=10;fontFamily=Helvetica;fontSize=14;fontStyle=1;fontColor=#333333;
```

| 項目 | 説明 |
|-----|-----|
| `fillColor=none` | 背景透明 |
| `dashed=1` | 破線 |
| `verticalAlign=top` | ラベルを上部に配置 |
| `spacingTop=10` | 上部余白 |

---

## 6. レイアウトルール

### 6.1 配置の基本

| 項目 | 推奨値 | 説明 |
|-----|-------|-----|
| グリッドサイズ | 10px | `gridSize="10"` |
| 要素間の最小間隔 | 20px | 視認性確保 |
| グループ間の間隔 | 40px | グループを明確に分離 |

### 6.2 矢印接続時の余白

矢印でつなぐ要素間には、ラベル表示のため十分な余白を確保する：

| 接続方向 | 最小間隔 | 推奨間隔 | 説明 |
|---------|---------|---------|-----|
| 横方向 | 80px | 100-120px | ラベル表示領域確保 |
| 縦方向 | 60px | 80-100px | ラベル表示領域確保 |
| ラベルなし | 40px | 60px | 最小限の余白 |

**重要**: 矢印にラベルを付ける場合は、ラベルの文字数に応じて間隔を調整する。
- 日本語4文字: 約80px以上
- 日本語6文字以上: 約100px以上

### 6.3 ラベル位置設定

| 項目 | style属性 | 説明 |
|-----|----------|-----|
| 垂直位置（上） | `verticalLabelPosition=top` | ラベルを図形上に |
| 垂直位置（下） | `verticalLabelPosition=bottom` | ラベルを図形下に |
| 垂直揃え | `verticalAlign=middle` | 図形内で縦中央 |
| 水平揃え | `align=center` | 図形内で横中央 |
| 上部余白 | `spacingTop=10` | 上からの余白 |
| 左余白 | `spacingLeft=10` | 左からの余白 |

### 6.4 Z軸順序（描画順）

```
図形（vertex）を先に定義 → 最背面
矢印（edge）を後に定義 → 最前面
```

XMLでの記述順序が描画の重なり順を決定。**矢印が図形の上になるよう、edgeを後に記述する。**

記述順序:
1. 凡例グループ（最背面）
2. グループ/コンテナ（swimlane）
3. 図形（vertex）
4. 矢印（edge）（最前面）

### 6.5 mxGraphModelの基本設定

```xml
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
```

| 属性 | 値 | 説明 |
|-----|-----|-----|
| grid | 1 | グリッド有効 |
| gridSize | 10 | 10px単位 |
| guides | 1 | ガイド線有効 |
| page | 0 | ページ境界非表示 |
| background | none | 背景透明 |

---

## 7. 共通style属性

### 7.1 全要素共通

```
fontFamily=Helvetica;fontSize=18;whiteSpace=wrap;html=1;
```

### 7.2 ボックス（vertex）

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontFamily=Helvetica;fontSize=18;fontColor=#333333;
```

### 7.3 矢印（edge）

```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;strokeWidth=2;strokeColor=#333333;fontFamily=Helvetica;fontSize=12;fontColor=#666666;endArrow=classic;endFill=1;
```

### 7.4 テキストラベル

```
text;html=1;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontFamily=Helvetica;fontSize=14;fontColor=#333333;
```

### 7.5 グループコンテナ（swimlane）

```
swimlane;horizontal=1;startSize=25;fillColor=#f5f5f5;strokeColor=#666666;fontFamily=Helvetica;fontSize=14;fontStyle=1;fontColor=#333333;
```

---

## 8. カスタマイズ例

### 8.1 プロジェクト固有のカラー設定

システム連携図で、連携先ごとに色を分ける例：

```markdown
| システム | 背景色 | 枠線色 | 説明 |
|---------|--------|--------|-----|
| 自社システム | #dae8fc | #6c8ebf | メインシステム |
| 外部API A | #f8cecc | #b85450 | 決済システム |
| 外部API B | #e1d5e7 | #9673a6 | 認証システム |
| 外部API C | #fff2cc | #d6b656 | 通知システム |
```

### 8.2 部署別カラー設定

業務フロー図で、担当部署ごとに色を分ける例：

```markdown
| 部署 | 背景色 | 枠線色 |
|-----|--------|--------|
| 営業部 | #dae8fc | #6c8ebf |
| 開発部 | #d5e8d4 | #82b366 |
| 経理部 | #fff2cc | #d6b656 |
| 外部ベンダー | #f8cecc | #b85450 |
```

---

## 9. XMLでの記述例

### 9.1 色付きボックス

```xml
<mxCell
  value="処理名"
  style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontFamily=Helvetica;fontSize=18;"
  vertex="1"
  parent="1">
  <mxGeometry x="100" y="100" width="140" height="60" as="geometry" />
</mxCell>
```

### 9.2 矢印（ラベル付き）

```xml
<mxCell
  value="遷移条件"
  style="edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;strokeWidth=2;strokeColor=#333333;fontFamily=Helvetica;fontSize=12;fontColor=#666666;endArrow=classic;endFill=1;"
  edge="1"
  parent="1"
  source="box-1"
  target="box-2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 9.3 外部システム（破線枠）

```xml
<mxCell
  value="外部API"
  style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;dashed=1;fontFamily=Helvetica;fontSize=18;"
  vertex="1"
  parent="1">
  <mxGeometry x="100" y="100" width="140" height="60" as="geometry" />
</mxCell>
```
