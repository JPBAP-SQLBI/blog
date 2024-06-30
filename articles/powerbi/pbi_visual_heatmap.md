---
title: 条件付き書式で作るヒートマップ
date: 2022-07-31 00:00:00
tags:
  - Power BI
  - ビジュアル
  - マトリックス
  - ヒートマップ
  - 条件付き書式
  - Creator
---

こんにちは、Power BI サポート チームの山本です。

「ヒートマップ」と呼ばれる表現方法についてご存知でしょうか。
ヒートマップは具体的な量や数値によらず、全体的な傾向を把握したいときに用いられます。
Power BI では標準のビジュアルとして用意されておりませんが、テーブルビジュアルやマトリックスビジュアルと条件付き書式を使用することで、簡単にヒートマップを表現することが可能です。

今回は、上記方法でヒートマップを作成する手順について紹介いたします。

*地理的データを表現する「ヒートマップ」については、今回の記事では取り上げません。
マップビジュアルについては、「[Power BIのマップビジュアル](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_map_visual/)」の記事をご参考ください。


<!-- more -->

> [!IMPORTANT]
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 予めご了承ください。

---
## 目次
---
1. [ヒートマップとは](#ヒートマップとは)
2. [Power BI での表現方法](#Power-BI-での表現方法)

---
## ヒートマップとは
---

ヒートマップは、データに対して色の濃淡で値を表現する可視化グラフの一つです。
Web サイト解析として、滞在時間の傾向把握として使用されたり、地図データ上の地域ごとの傾向を把握するために使用されます。

<div align="center">
<a title="Miguel Andrade at English Wikipedia, Public domain, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Heatmap.png"><img width="512" alt="Heatmap" src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Heatmap.png/512px-Heatmap.png"></a>
</div>


> **参考情報**
> - [ヒートマップ | Wikipedia](https://ja.wikipedia.org/wiki/%E3%83%92%E3%83%BC%E3%83%88%E3%83%9E%E3%83%83%E3%83%97#cite_note-6)

<br>
<br>

---
## Power BI での表現方法
---

前述の通り、Power BI では標準のビジュアルとして用意されておりませんが、テーブルビジュアルやマトリックスビジュアルと条件付き書式を使用することで、簡単にヒートマップを表現することが可能です。

本記事では、Power BI Desktop のサンプルデータにもなっている「financials」テーブルを使用して、ヒートマップのサンプルをご紹介いたします。

</br>

### どのように分析するか

ヒートマップは細かい数値や情報を確認することには不向きですが、全体的な傾向把握に用いられ、商品情報・時系列情報といった切り口やある数値の関係について、仮説探索や傾向の把握に向いている分析方法だといえます。

例えば、以下のような仮説探索などの表現が可能です。
・市場ごとの売上には、季節ごと・月ごとにばらつきがあるのか？
・製品と市場の相関関係はあるのか？

今回は、売上は国ごとに季節性のばらつきがあるのかをヒートマップで表現したいと思います。

</br>

### どのように表現するか

ヒートマップを表現するビジュアルとして、今回はマトリックスビジュアルを使用します。

<div align="center">
<img src="1.png">
</div>

</br>

行に「国情報(Country)」を、列に「月情報」を入れ、値に「売上」を入れます。

<div align="center">
<img src="2.png">
</div>

</br>

> [!TIP]
> 売上金額の合計で優劣がつかないよう、集計方法は平均として、月ごとの比較ができるようにします。

</br>

[ビジュアルの書式設定 - ビジュアル] に移動し、[列の小計] ・ [行の小計] は表示されないようにオフにします。

<div align="center">
<img src="3.png">
</div>

</br>

[セル要素] の設定内にある [背景色] をオンにし、[fx] ボタンをクリックします。

<div align="center">
<img src="4.png">
</div>

</br>

データ形式スタイルは「グラデーション」として、[中間色を追加する] チェックをつけ、最小値から最大値まで、グラデーションが表現できるように色味を設定します。

<div align="center">
<img src="5.png">
</div>

</br>

次のような形で、値の大小でグラデーション表現ができるようになりました。
例えばアメリカは、月ごとにも大きく濃淡はなく、まんべんなく売上が取れている一方、ドイツやフランスは、10月(Oct) に売上が偏っていることが視覚的にわかります。


<div align="center">
<img src="9.png">
</div>

</br>

#### // ヒートマップ内の値を隠したい場合

同様に [セル要素] の設定内にある [フォントの色] をオンにし、[fx] ボタンをクリックします。

<div align="center">
<img src="6.png">
</div>

</br>

同様に、データ形式スタイルは「グラデーション」として、[中間色を追加する] チェックをつけ、最小値から最大値まで色味を設定します。
このとき設定する各色は、[背景色] のグラデーションと同じ色に設定するようにご注意ください。

<div align="center">
<img src="7.png">
</div>

</br>

[背景色] と [フォントの色] が同色となることで、文字が同化し、各セルで色のみを表現することができるようになります。

<div align="center">
<img src="8.png">
</div>

</br>


更に書式を合わせて作り込み、以下のように国ごとの業界(Segment)ごとの情報で月のばらつきがあるか表現できるようにしました。
フィルターやビジュアル間の相互作用を使用することで、ヒートマップのデータをフィルタリングして動的に表示される内容を変えることも可能です。

</br>

<iframe title="heatmap_sample - Heatmap Sample" width="800" height="400" src="https://app.powerbi.com/view?r=eyJrIjoiMTIyNjEyZjctOTYwMC00YjQxLWJhM2ItZjUzMzRjOTMxNjJhIiwidCI6ImI1OTkzM2Q0LWMzMTUtNDNhZC05ODhlLWZiYmQ2NjIxZjAxMyJ9" frameborder="0" allowFullScreen="true"></iframe>

*[全画面表示モードで開く]ことで大きな画面でヒートマップを確認できます。

</br>

[レポートのダウンロード(右クリックで[名前を付けてリンクを保存])](https://github.com/JPBAP-SQLBI/blog/raw/main/articles/powerbi/pbi_visual_heatmap/sample_pbix/heatmap_sample.pbix)

> **参考情報**
> - [How To Create A Power BI Heat Map | Enterprise DNA](https://blog.enterprisedna.co/power-bi-heat-map-a-custom-visualization-tutorial/)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
