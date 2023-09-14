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
---

こんにちは、Power BI サポート チームのチャンです。

Power BI で地理データを可視化する際に、利用できるマップビジュアルは、Bing マップ、Azure マップやArcGISマップなど複数の選択肢がありますが、本ブログでは、それぞれの特徴と地理的データを使用する際の注意事項をご紹介いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
1. [マップ](#マップ)
2. [塗り分け地図](#塗り分け地図)
3. [図形のビジュアル](#図形のビジュアル)
4. [Azure マップ](#Azureマップ)
5. [ArcGIS Maps for Power BI](#ArcGIS-Maps-for-Power-BI)

---
## マップ
---
<div align="center">
<img src="map_visual1.png" alt="Power BIマップ" title="Power BIマップ">
</div>
Power BI マップはBing マップと統合されており、緯度経度の地理的なデータ以外に、国名、都道府県、市区町村、郵便番号などの情報を持つデータでも、可視化できます。

また、Bing マップがジオコーディング（地理座標を付与するプロセス）する際に、以下のURLへアクセスすることがあるため、ネットワーク環境に応じて以下のURLを許可する必要がございます。
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

塗り分け地図は、前項で紹介したマップと同様に、Bingマップと統合されていますので、注意事項につきましては、上述の内容をご確認ください。

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

日本のデータを使用したい場合、TopoJSON ファイルをご用意いただく必要がございます。（シェイプファイルやGeoJSON マップの場合は変換が必要です。）

国土交通省が公開している地域ごとのポリゴン（塗り分け地図用に適している）データはシェイプファイルがありますので、Map Shaper などのオンラインツールを使用してTopoJSON ファイルに変換することができます。

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
## Azureマップ
---
<div align="center">
<img src="map_azuremap_icon.png" alt="Azure マップ" title="Azure マップ">
</div>

Azureマップは現在プレビュー機能であり、Power BI Desktopで使用するには、[ファイル] > [オプションと設定] からオプション パネルを開き、[プレビュー機能] のオプションに移動し、[Azure Maps Visual] を選択する必要がございます。

<div align="center">
<img src="map_azuremap_preview.png" alt="Azure マッププレビュー機能" title="Azure マッププレビュー機能">
</div>

Power BI サービスで使用するには、[管理ポータル]>[テナント設定]にて、
[Azure Maps ビジュアルの使用]を有効化しておく必要があります。

<div align="center">
<img src="azuremap_tenant_settings.png" alt="Azure マップテナント設定" title="Azure マップテナント設定">
</div>

こちらのマップビジュアルはAzure マップが使用されており、Azure マッププラットフォームへのアクセスを許可するために、ネットワーク環境に応じて以下のURLを許可する必要がございます。
- https://atlas.microsoft.com


また、Azure マップには、多彩なマップレイヤーが用意されており、例えば、バブルレイヤー、3D 棒グラフレイヤー、参照レイヤー（GeoJSON ファイルを使用する）、タイル レイヤー、トラフィックのオーバーレイなどをご利用いただけます。

#### ■バブルレイヤー
バブル レイヤーは、場所データをマップ上で拡大縮小された円として表現できる優れた方法です。

例えば、以下の画像は、ノースカロライナ州で自転車の事故が発生した場所を示しています。円の色は事故が発生した道路の速度制限を表し、円のサイズは事故に巻き込まれた人の数に基づいています。
<div align="center">
<img src="https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/f7453509-dda9-48d6-b960-ecbebd696e4e.png" alt="Azure マップバブルレイヤー" width=600 title="Azure マップバブルレイヤー">
</div>

#### ■3D 棒グラフレイヤー
3D 棒グラフを使用すると、ユーザーは、データをさまざまな視点から見るために、マウスの右ボタンを押しながらドラッグするか、ナビゲーション コントロールのいずれかを使用することで、マップを傾けたり回転させたりすることができます。

以下のマップは、店舗の場所を示しています。棒の高さは各場所から生み出される収益を表し、販売地域ごとに色分けされています。

<div align="center">
<img src="https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/56bc9253-8365-4187-9d79-72010f1606b7.png" alt="Azure マップ3D 棒グラフレイヤー" width=600 title="Azure マップ3D 棒グラフレイヤー">
</div>

#### ■参照レイヤー
参照レイヤーを使用すると、カスタムの場所データを含む GeoJSON ファイルをアップロードして、マップ上にオーバーレイすることができます。GeoJSON ファイルに含まれるプロパティを使用すると、形状のスタイルをカスタマイズできます。

例えば、以下のマップ画像は、人口で色分けされた国勢調査地域の境界線の GeoJSON ファイルを、不動産価値で色分けされた住所のレイヤーの下に追加したものです。

<div align="center">
<img src="https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/aee4e91e-b5ad-41a8-8f40-0011547cdfb6.png" alt="Azure マップ参照レイヤー" width=600 title="Azure マップ参照レイヤー">
</div>

#### ■タイルレイヤー
タイル レイヤーを使用することで、Azure Maps ベース マップ タイルの上に画像を重ねることができます。

以下のマップでは、サングラスを販売する店舗の売上データのバブル レイヤーが、Azure Maps から取得した現在の気象レーダーを示すタイル レイヤーの上に表示されています。

<div align="center">
<img src="https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c519e5e6-ad28-4cd6-a6c8-e4c451dee7ac.png" alt="Azure マップタイルレイヤー" width=600 title="Azure マップタイルレイヤー">
</div>

#### ■トラフィックのオーバーレイ
リアルタイムの交通流量データをオーバーレイすることで、交通渋滞と独自データの関連性を知ることができます。

例えば以下のマップでは、フィールド技術者の現在地がマップ上でバブル レイヤーとしてレンダリングされ示されています。

<div align="center">
<img src="https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/e25c79de-b33a-46a9-a059-e23641094d1f.png" alt="Azure マップトラフィックのオーバーレイ" width=600 title="Azure マップトラフィックのオーバーレイ">
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