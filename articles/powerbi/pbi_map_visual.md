---
title: Power BIのマップビジュアル
date: 2021-12-27 16:00:00
tags:
  - Power BI
  - マップビジュアル
  - 地図
  - 地理データ
  - Azure Map
  - Bing Map
  - ArcGIS Map
  - Creator
---

こんにちは、Power BI サポート チームのチャンです。

Power BI で地理データを可視化する際に、利用できるマップビジュアルは、 Bing マップ、Azure マップや ArcGIS マップなど複数の選択肢がありますが、本ブログでは、それぞれの特徴と地理的データを使用する際の注意事項をご紹介いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


---
## 更新履歴
---
Update: 2025/07/30
Azure マップのテナント設定や利用要件に変更点がありましたので、 [Azure マップ](#Azure-マップ) セッションの内容を更新しました。


---
## 目次
---
1. [マップ](#マップ)
2. [塗り分け地図](#塗り分け地図)
3. [図形のビジュアル](#図形のビジュアル)
4. [Azure マップ](#Azure-マップ)
5. [ArcGIS Maps for Power BI](#ArcGIS-Maps-for-Power-BI)

---
## マップ
---
<div align="center">
<img src="map_visual1.png" alt="Power BIマップ" title="Power BIマップ">
</div>
Power BI マップは Bing マップと統合されており、緯度経度の地理的なデータ以外に、国名、都道府県、市区町村、郵便番号などの情報を持つデータでも、可視化できます。

また、 Bing マップがジオコーディング（地理座標を付与するプロセス）する際に、以下のURLへアクセスすることがあるため、ネットワーク環境に応じて以下のURLを許可する必要がございます。
 - https://dev.virtualearth.net/REST/V1/Locations
 - https://platform.bing.com/geo/spatial/v1/public/Geodata
 - https://www.bing.com/api/maps/mapcontrol

地理データをマップで使用する際に、都道府県や市区町村、緯度経度のデータカテゴリを設定しておくことが必要です。設定した後、対象のデータフィールドに地球のマークが付くようになります。

<div align="center">
<img src="map_visual2.png" alt="市区町村のデータカテゴリ" title="市区町村のデータカテゴリ">
</div>

特に緯度経度の場合、データカテゴリを指定すると共に、概要を「集計しない」に設定しないと正しく使用できない場合がありますため、ご留意くださいませ。

<div align="center">
<img src="map_visual3.png" alt="緯度経度の集計しない設定" title="緯度経度の集計しない設定">
</div>

マップビジュアルでは、地図の上に、場所ごとでプロットしたデータの数値の大きさによって、バブル・円グラフ・バブルのグラデーション（ヒートマップ）で表現することが可能です。

#### ■マップ上のバブルチャート
<div align="center">
<img src="map_bubble_chart.png" alt="マップ上のバブルチャート" title="画像4_マップ上のバブルチャート">
</div>

#### ■マップ上の円グラフ
<div align="center">
<img src="map_pie_chart.png" alt="マップ上の円グラフ" title="マップ上の円グラフ">
</div>

#### ■マップ上のバブルグラデーション（ヒートマップ）
<div align="center">
<img src="map_bubble_heatmap.png" alt="マップ上のバブルグラデーション（ヒートマップ）" title="マップ上のバブルグラデーション（ヒートマップ）">
</div>

> **参考情報**
> - [マップに関するヒントとテクニック (Bing マップの統合を含む) - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/visuals/power-bi-map-tips-and-tricks)

<br>
<br>

---
## 塗り分け地図
---

<div align="center">
<img src="map_filledmap.png" alt="塗り分け地図" title="塗り分け地図">
</div>

塗り分け地図は、前項で紹介したマップと同様に、 Bing マップと統合されていますので、注意事項につきましては、上述の内容をご確認ください。

ビジュアルはマップと異なり、地図上の地形によって、国・都道府県・市区町村などを塗りつぶして、色の色相や濃淡によってデータを表します。

メリットとしては、地形によって色が塗りつぶされるため、見栄えがよくわかりやすいところです。デメリットとしては、地形上面積が大きいところに目が惹かれやすく、データによっては誤った印象や直感を与えてしまうところです。

塗り分け地図を使用する最適な場合は以下を挙げられます。
- 量的な情報を地図に表示する。
- 空間的なパターンと関係を示す。
- データが標準化されている。
- 社会経済的なデータを扱っている。
- 特定の地域に関心がある。
- 異なる地理的位置への分散状況を全体的に理解する。

<div align="center">
<img src="map_filledmap_example.png" alt="塗り分け地図ビジュアル" title="塗り分け地図ビジュアル">
</div>

> **参考情報**
> - [Power BI の塗り分け地図 (コロプレス) - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/visuals/power-bi-visualization-filled-maps-choropleths)

<br>
<br>

---
## 図形のビジュアル
---

<div align="center">
<img src="map_sharpmap_icon.png" alt="図形のビジュアル" title="図形のビジュアル">
</div>

図形のビジュアルは、正しい地理座標を表示させることが目的ではなく、各地域のデータを比較する目的で作成されたビジュアルです。

執筆時点では、まだプレビュー機能であり、既定値で使用できる図形は、以下の国・地域のみ対応しており、日本のデータは対応しておりません。

- オーストラリア
- オーストリア
- ブラジル
- カナダ
- フランス
- ドイツ
- アイルランド
- イタリア
- メキシコ
- オランダ
- 英国
- 米国

日本のデータを使用したい場合、 TopoJSON ファイルをご用意いただく必要がございます。（シェイプファイルや GeoJSON マップの場合は変換が必要です。）

国土交通省が公開している地域ごとのポリゴン（塗り分け地図用に適している）データはシェイプファイルがありますので、 Map Shaper などのオンラインツールを使用して TopoJSON ファイルに変換することができます。

- [国土数値情報ダウンロード](https://nlftp.mlit.go.jp/ksj/gml/datalist/KsjTmplt-N03-v3_0.html)
- [Map Shaper](https://mapshaper.org/)

<div align="center">
<img src="map_sharpmap.png" alt="図形のビジュアル" title="図形のビジュアル">
</div>

> **参考情報**
> - [Power BI Desktop で図形マップを使用する (プレビュー) - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/visuals/desktop-shape-map)

<br>
<br>

---
## Azure マップ
---
<div align="center">
<img src="map_azuremap_icon.png" alt="Azure マップ" title="Azure マップ">
</div>

#### テナント設定


現時点で、 Azure マップを利用するには、利用するリージョンや機能によって、[管理ポータル]>[テナント設定]にて、以下の 3 つのテナント設定を必要に応じて有効化しておく必要があります。

<b>1. ユーザーは Azure Maps 視覚エフェクトを使用できます</b>

まず Azure マップを利用するためには、こちらのテナント設定を有効化する必要がございます。
<div align="center">
<img src="azuremap_tenant_settings1.png">
</div>

<b>2. Azure Maps に送信されたデータを、テナントの地理的リージョン、コンプライアンス境界、または国内クラウド インスタンスの外部で処理することが可能</b>

ご利用のテナントリージョン（※）によって、こちらのテナント設定を有効化しないと Azure マップを利用できません。
具体的に、現時点では米国と [ヨーロッパ](https://learn.microsoft.com/ja-jp/privacy/eudb/eu-data-boundary-learn#eu-data-boundary-countries-and-datacenter-locations) のリージョン以外のテナントで Azure マップを利用するには、こちらのテナント設定を有効化する必要がございます。

<div align="center">
<img src="azuremap_tenant_settings2.png">
</div>

※ テナントリージョンの確認方法は以下の公開情報をご確認ください。
- [Azure Maps Power BI ビジュアルのデータ所在地](https://learn.microsoft.com/ja-jp/azure/azure-maps/power-bi-visual-data-residency)

> **参考情報**
> - [Azure Maps サービスの地域スコープ](https://learn.microsoft.com/ja-jp/azure/azure-maps/geographic-scope)

<b>3. Azure Maps に送信されたデータは、Microsoft Online Services のサブプロセッサーで処理されます</b>

Azure マップ内の一部の機能、例えば選択ツールや一部のリージョン内での場所名の処理は、Microsoft Online Services サブプロセッサー（※）によって部分的に提供されるマッピング機能が必要となる場合がございます。

それらを正しく機能させるには、本テナント設定を有効化する必要がございます。

<div align="center">
<img src="azuremap_tenant_settings3.png">
</div>

具体的例としては、本設定を無効化している場合は、Azure マップビジュアル内のコントロールにある [選択項目] がグレイアウトされ利用できません。

<div align="center">
<img src="azuremap_selection_tools.png">
</div>

※ Microsoft Online Services サブプロセッサーの説明につきまして、以下の公開情報をご確認ください。

> **参考情報**
> - [Microsoft のデータ アクセス管理](https://www.microsoft.com/ja-jp/trust-center/privacy/data-access)


> [!TIP]
> Azure マップの利用要件やテナント設定が 2025 年 6 月から、上記の通りに変更されたことにより、 Azure マップを利用するには、Power BI Desktop 2025 年 4 月バージョン以降を利用する必要があります。 


#### 通信要件
こちらのマップビジュアルは Azure マップが使用されており、 Azure マッププラットフォームへのアクセスを許可するために、ネットワーク環境に応じて以下の URL を許可する必要がございます。
- https://atlas.microsoft.com
- https://us.atlas.microsoft.com
- https://eu.atlas.microsoft.com


また、 Azure マップには、多彩なマップレイヤーが用意されており、例えば、バブルレイヤー、 3D 棒グラフレイヤー、参照レイヤー（GeoJSON ファイルを使用する）、タイル レイヤー、トラフィックのオーバーレイなどをご利用いただけます。

#### ■バブルレイヤー
バブル レイヤーは、場所データをマップ上で拡大縮小された円として表現できる優れた方法です。

例えば、以下の画像は、ノースカロライナ州で自転車の事故が発生した場所を示しています。円の色は事故が発生した道路の速度制限を表し、円のサイズは事故に巻き込まれた人の数に基づいています。
<div align="center">
<img src="bubble-layer-thumb.png" alt="Azure マップバブルレイヤー" width=600 title="Azure マップバブルレイヤー">
</div>

#### ■3D 棒グラフレイヤー
3D 棒グラフを使用すると、ユーザーは、データをさまざまな視点から見るために、マウスの右ボタンを押しながらドラッグするか、ナビゲーション コントロールのいずれかを使用することで、マップを傾けたり回転させたりすることができます。

以下のマップは、店舗の場所を示しています。棒の高さは各場所から生み出される収益を表し、販売地域ごとに色分けされています。

<div align="center">
<img src="3d-column-layer-thumb.png" alt="Azure マップ3D 棒グラフレイヤー" width=600 title="Azure マップ3D 棒グラフレイヤー">
</div>

#### ■参照レイヤー
参照レイヤーを使用すると、カスタムの場所データを含む GeoJSON ファイルをアップロードして、マップ上にオーバーレイすることができます。 GeoJSON ファイルに含まれるプロパティを使用すると、形状のスタイルをカスタマイズできます。

例えば、以下のマップ画像は、人口で色分けされた国勢調査地域の境界線の GeoJSON ファイルを、不動産価値で色分けされた住所のレイヤーの下に追加したものです。

<div align="center">
<img src="reference-layer-thumb.png" alt="Azure マップ参照レイヤー" width=600 title="Azure マップ参照レイヤー">
</div>

#### ■タイルレイヤー
タイル レイヤーを使用することで、Azure Maps ベース マップ タイルの上に画像を重ねることができます。

以下のマップでは、サングラスを販売する店舗の売上データのバブル レイヤーが、Azure Maps から取得した現在の気象レーダーを示すタイル レイヤーの上に表示されています。

<div align="center">
<img src="tile-layer-thumb.png" alt="Azure マップタイルレイヤー" width=600 title="Azure マップタイルレイヤー">
</div>

#### ■トラフィックのオーバーレイ
リアルタイムの交通流量データをオーバーレイすることで、交通渋滞と独自データの関連性を知ることができます。

例えば以下のマップでは、フィールド技術者の現在地がマップ上でバブル レイヤーとしてレンダリングされ示されています。

<div align="center">
<img src="traffic-layer-thumb.png" alt="Azure マップトラフィックのオーバーレイ" width=600 title="Azure マップトラフィックのオーバーレイ">
</div>


> **参考情報**
> - [Azure Maps の Power BI 視覚エフェクトの概要 | Microsoft Docs](https://learn.microsoft.com/ja-jp/azure/azure-maps/power-bi-visual-get-started)
> - [Azure Maps Power BI ビジュアルのジオコーディング | Microsoft Docs](https://learn.microsoft.com/ja-jp/azure/azure-maps/power-bi-visual-geocode)
> - [Azure Maps Power BI ビジュアルのレイヤーの概要 | Microsoft Docs](https://learn.microsoft.com/ja-jp/azure/azure-maps/power-bi-visual-understanding-layers)

<br>
<br>

---
## ArcGIS Maps for Power BI
---
<div align="center">
<img src="map_arcgismap_icon.png" alt="ArcGIS Maps for Power BI" title="ArcGIS Maps for Power BI">
</div>

ArcGIS for Power BI は Esri (https://www.esri.com) によって提供されます。 ArcGIS for Power BI のご利用の際には、Esri の[使用条件](https://go.microsoft.com/fwlink/?LinkID=826322)および[プライバシー ポリシー](https://go.microsoft.com/fwlink/?LinkID=826323)が適用されます。 ArcGIS for Power BI 視覚化の使用を希望される Power BI ユーザーは、同意ダイアログを受け入れる必要があります。

<div align="center">
<img src="map_arcgismap_options.png" alt="Azure マップオプション" title="ArcGIS Maps for Power BIオプション">
</div>

また、Power BI サービスで使用するには、[管理ポータル]>[テナント設定]にて
[ArcGIS Maps for Power BI を使用する]を有効化しておく必要があります。

<div align="center">
<img src="arcgismap_tenant_settings.png" alt="ArcGIS Maps for Power BI テナント設定" title="ArcGIS Maps for Power BI テナント設定">
</div>

こちらのマップビジュアルを使用する際に、住所のジオコーディング、対象ポイントの検索、参照レイヤーの追加など、さまざまな処理を実行するために、多くのホスト サーバーと外部 URL を利用しています。ネットワーク環境に応じて以下サイトに記載されているURLを許可する必要がございます。
 - [ネットワークのセキュリティ保護—ArcGIS for Power BI | ドキュメント](https://doc.arcgis.com/ja/power-bi/get-started/secure-networks.htm)

ArcGIS Maps for Power BIでは、幅広いビジュアル表現や、地図のレイヤーをご利用いただけますが、詳細につきましては、以下のドキュメントをご参照ください。

<div align="center">
<img src="map_arcgismap.png" alt="ArcGIS Maps for Power BIビジュアル" title="ArcGIS Maps for Power BIビジュアル">
</div>

> **参考情報**
> - [他のユーザーから共有された ArcGIS マップとの対話 - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/visuals/power-bi-visualizations-arcgis)
> - [ArcGIS for Power BI—ArcGIS for Power BI | ドキュメント](https://doc.arcgis.com/ja/power-bi/get-started/about-maps-for-power-bi.htm)

<br>
<br>

---

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)