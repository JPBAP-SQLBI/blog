---
title: Power BI のマップビジュアルで地名が正常に認識されない場合
date: 2023-01-31 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - マップビジュアル
  - 地図
  - 地理データ
  - Azure Map
  - Bing Map
  - ArcGIS Map
---


こんにちは、Power BI サポート チーム 丸山です。

Power BI のマップビジュアルは、地名ごとに集計された数値をマップ上に自動でバブル表示できるとても便利なビジュアルですが、データソースの地名の持ち方によっては地名が正常に認識されず、マップ上に結果が表示されないことがあります。
今回はこの問題が起きたときの原因と対応策についてご紹介します。

<div align="center">
<img src="image1.png">
</div>

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
1. [マップビジュアルで地名が正常に認識されない原因](#マップビジュアルで地名が正常に認識されない原因)
2. [対応策](#対応策)

---
## マップビジュアルで地名が正常に認識されない原因
---
Power BI のマップビジュアルは Bing Maps（ https://www.bing.com/maps/ ）を使用しているため、Bing Maps上の地名に基づいてビジュアルが表示されます。このため、データソースの地名が Bing Maps 上の地名と相違する文字列である場合、マップビジュアルで認識することができず該当地域に集計結果が表示されません。

例えばアメリカは、Bing Maps 上では「アメリカ合衆国」ですが、データソース側で「アメリカ」という文字列でデータを持っている場合は、マップビジュアルのアメリカの欄に集計結果が表示されないという問題が起きます。つまり、Bing Maps 上の表記とデータソースの国名データ表記が一致していないことが原因となります。

<div align="center">
<img src="image1.png">
</div>

---
## 対応策
---

対応策としては、データ側の地名を Bing Maps の表記に合わせるということになります。
上述 ”アメリカ” の例では、Bing Maps の表記 ”アメリカ合衆国” に合わせることで正常に地図に表示されます。

なお、地名の正式名称や定義などは時勢に応じて都度変わることから、一覧情報としてのご提供はご用意がないため、もしマップビジュアルで正しく認識されていない地名がある場合、Bing Maps（ https://www.bing.com/maps/ ）で表記をチェックしてください。

<div align="center">
<img src="image2.png">
</div>
 
データ側の地名を変更する方法については、データソース自体で地名を変更する他に、データ取得の際に Power Query でデータ変換をすることも可能です。この方法であれば、データソースのデータはそのままであるため、業務影響や対応負荷は最小限にできる可能性があります。
以下に具体的な手順をご案内いたします。


１．Power BI Desktop から Power Query エディターを開く

ホーム > データの変換
<div align="center">
<img src="image3.png">
</div>


２．該当の列で右クリック > 値の置換 > 任意の地名を入力 > OK
<div align="center">
<img src="image4.png">
</div>


３．データが置換されたことを確認
<div align="center">
<img src="image5.png">
</div>


４．Power Query エディターを閉じて適用する
<div align="center">
<img src="image6.png">
</div>


下記図のように、無事にマップビジュアルに「「アメリカ合衆国」でバブルの表示がされるようになりました。
<div align="center">
<img src="image7.png">
</div>


> [!NOTE]
> // 参考情報：[値の置換 (Power Query) - Microsoft サポート](https://support.microsoft.com/ja-jp/office/%E5%80%A4%E3%81%AE%E7%BD%AE%E6%8F%9B-power-query-28256517-f1e9-4dc3-832f-45786e9cf721)


また補足ではございますが、よりマップビジュアルの精度を上げたいという場合は、
地名ではなく緯度経度の情報もご利用をご検討いただけますと幸いでございます。

<div align="center">
<img src="image8.png">
</div>

> [!NOTE]
> // 参考情報：[Power BI マップの視覚エフェクトに関するヒントとテクニック](https://learn.microsoft.com/ja-jp/power-bi/visuals/power-bi-map-tips-and-tricks#in-power-bi-tips-to-get-better-results-when-using-map-visualizations)
> <div align="center">
  <img src="image9.png">
  </div>



---

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。


---

> **本ブログの関連記事**
> - [Power BIのマップビジュアル](../pbi_map_visual/)