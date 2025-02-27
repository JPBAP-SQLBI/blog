---
title: Power BIのレポート機能「スパークライン」 
date: 2022-02-28 00:00:00
tags:
  - Power BI
  - ビジュアル
  - テーブル
  - table
  - マトリックス
  - matrix
  - プレビュー
  - preview
  - スパークライン
  - sparkline
---

こんにちは、Power BI サポート チームの丸山です。 

テーブルやマトリックスによる表形式のレポートを、もっと充実させたいと思ったことはないでしょうか。本ブログではそんなときに役立つ機能、スパークライン（2022年1月リリース）をご紹介します。 

<!-- more -->

<div align="center">
<img src="pic001.PNG" alt="画像1_スパークライン" title="画像1_スパークライン">
</div>

スパークラインはテーブルやマトリックスのセル内に表示される「小さなグラフ」であり、表の数値だけでは把握ができない傾向をすばやく確認したり比較したりするのに便利です。季節的な増減や景気サイクルなどトレンドを示したり、最大値や最小値を強調したりする場合に使います。（2022.02現在プレビュー段階） 


> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。
> 
> また、本機能は開発段階 (プレビュー) でございますため、今後予告なしに機能が削除されたり、
> 動作変更が発生する可能性がありますことをあらかじめご了承くださいますようお願い申し上げます。

---
## 目次
---
1. [設定方法](#設定方法)
2. [考慮事項と制限事項](#考慮事項と制限事項)
3. [活用事例](#活用事例)

---
## 設定方法
---

### スパークラインのプレビューを有効にしておく 

スパークラインは既定で有効になっていますが、もし有効になっていない場合は次の方法で機能を有効にします。 

[ファイル][オプションと設定][オプション][プレビュー機能] に移動し、[スパークライン] を選択。 

<div align="center">
<img src="pic002.PNG" alt="画像2_プレビューを有効にする" title="画像2_プレビューを有効にする">
</div>


### スパークラインを追加する 
スパークラインはテーブルとマトリックスの両方の視覚エフェクトに追加できます。 

1. テーブルまたはマトリックスを作成します。 
2. 数値フィールドの横にあるドロップダウン矢印を選び、[スパークラインの追加] を選びます。

<div align="center">
<img src="pic003.PNG" alt="画像3_スパークラインの追加1" title="画像3_スパークラインの追加1">
</div>

3. ダイアログ ボックスで、スパークラインの詳細を構成します。 [Y 軸] には、開始した数値フィールドがあらかじめ設定されています。 必要に応じて、フィールドと [概要] の種類の両方を変更できます。 また、スパークラインの [X 軸] として使うフィールド (日付フィールドなど) を選ぶ必要があります。 

<div align="center">
<img src="pic004.PNG" alt="画像4_スパークラインの追加2" title="画像4_スパークラインの追加2">
</div>

4. ［作成］ を選択します。スパークラインは自動的に新しい列としてテーブルやマトリックスに追加されます。 

<div align="center">
<img src="pic005.PNG" alt="画像5_スパークラインの追加3" title="画像5_スパークラインの追加3">
</div>



### スパークラインを編集する 

1. スパークラインの隣にあるドロップダウン矢印を選び、[スパークラインの編集] を選びます。 

2. [書式] ペイン内の [スパークライン] カードで、スパークラインの線とマーカーの書式が変更できます。グラフ種類（折れ線、棒）を選んだり、線の色や幅を変更したり、特定の値（最高、最低、最後など）にマーカーを付けて傾向を浮き彫りにすることが可能です。 

<div align="center">
<img src="pic006.PNG" alt="画像6_スパークラインの編集1" title="画像6_スパークラインの編集1">
</div>

例1) 折れ線グラフで最高値に赤丸を付けた場合がこちら

<div align="center">
<img src="pic007.PNG" alt="画像7_スパークライン折れ線グラフ" title="画像7_スパークライン折れ線グラフ">
</div>

例2) 棒グラフにした場合がこちら 

<div align="center">
<img src="pic008.PNG" alt="画像8_スパークライン棒グラフ" title="画像8_スパークライン棒グラフ">
</div>


---
## 考慮事項と制限事項
---

- Power BI は、1 つの視覚エフェクトにつき最大 5 本のスパークラインをサポートしており、スパークラインごとに最大 52 ポイントが表示されます。 

- また、パフォーマンス上の理由から、スパークラインが有効な場合、マトリックスの最大列数も 20 個に制限されます。 

- スパークラインは、Azure Analysis Services ではサポートされていますが、オンプレミスの SQL Server Analysis Services では現在サポートされていません。 



---
## 活用事例
---

テーブルやマトリックスの数値だけではわからなかったことが、スパークラインによって情報が豊かになり、データ分析で深掘りするべきポイントを浮き彫りにすることができます。 

例えば、マトリックス（画像9）から得られる大まかな情報の２つが以下だとして、 

- 製品別で「Paseo」は年間収益TOP 
- 国別で「France」は年間収益TOP 

<div align="center">
<img src="pic009.PNG" alt="画像9_マトリックスのみ" title="画像9_マトリックスのみ">
</div>


スパークラインを追加（画像10）することで、深掘り分析をしたほうがいいポイントや施策が効きそうなポイントがわかるため、次のアクションに繋げやすくなります。 

- 製品別で「Paseo」は年間収益TOP 
  + USA だけ最高値となる月が他国と離れている ＝ キャンペーンなどの施策タイミングの深掘りへ 
- 国別で France は年間収益TOP 
  + France と Germany は最高値のタイミングが同じ製品が多い = 成功事例をGermany に横展開して収益を伸ばせるかも？ 

<div align="center">
<img src="pic010.PNG" alt="画像10_マトリックス+スパークライン" title="画像10_マトリックス+スパークライン">
</div>

</br>

[このPower BIレポートのダウンロードはこちら(右クリックで[名前をつけてリンクを保存])](https://github.com/JPBAP-SQLBI/blog/raw/main/articles/powerbi/pbi_visual_sparkline/sample_pbix/sparkline_sample.pbix)

</br>


上記は一部の例にすぎません。 
もちろん気付きを得たあとはもっと深掘りの分析が必要ですが、今まで議論や施策に発展しなかった数値だけの表データが、スパークラインを追加するだけでビジネスを前に進めるための気づきが得られ、議論や施策の一歩を踏み出す材料になります。ぜひご活用をご検討ください。 

</br>

> **参考情報**
> - [Power BI レポートでテーブルまたはマトリックスにスパークラインを作成する (プレビュー)](https://learn.microsoft.com/ja-jp/power-bi/create-reports/power-bi-sparklines-tables)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/) 


 



