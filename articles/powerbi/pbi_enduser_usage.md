---
title: Power BI ビジネスユーザー向けの使い方紹介
date: 2022-02-28 16:00:00
tags:
  - Power BI
  - Power BI サービス
  - Power BI Service
  - ビジネスユーザー
  - 閲覧者
---

こんにちは、Power BI サポート チームのチャンです。

これまで、Power BI というツールを導入検討されている方、Power BI レポートを作成される方、管理者や開発者向けにライセンスや様々な機能を紹介してきました。
そもそも、レポートやデータだけを閲覧する方は、Power BI ってどんなことができますか？という質問を持つことも多いと思います。

本ブログでは、Power BI のビジネスユーザー向けにレポートやダッシュボードを見る際に便利な使い方の詳細をご案内いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


---
## レポート閲覧・操作
---

#### データポイント
Power BI のグラフやテーブルはインタラクティブに動作するもので、例えばグラフやテーブル上の数字やデータポイントにカーソルを合わせると、詳細なデータが表示されます。

<div align="center">
<img src="power-bi-hover.gif" alt="画像1_データポイント" title="画像1_データポイント">
</div>

#### 相互作用

さらに、そのデータポイントにカーソルを合わせて、クリックすると、他のビジュアルに影響する部分がハイライトされたり、フィルターされたりします。

例えば月ごとの売上が右下の棒グラフに表示されていますが、個別の月を選択した際に、製品ごとの売上や利益がどう変化するか、別のグラフのどの部分に該当するか、どれぐらいの割合なのかなどを、この相互作用によってご確認いただけます。

また、空白の分をクリックすると、フィルターを解除し、前の状態に戻ります。

<div align="center">
<img src="interactive_effect.gif" alt="画像2_相互作用" title="画像2_相互作用">
</div>

#### フォーカスモード

複数のビジュアルやテーブルが同じページに配置されているときには、各グラフやテーブルが一つ一つ小さくなっている場合が多いため、個別のビジュアルを拡大して確認したい場合に、フォーカスモードのボタンをクリックすると、全画面表示にすることができます。

例えば、列や行がたくさんある会計帳票があって、縦や横にスクロールしないと表示しきれなかったものについては、拡大するとより見やすくなります。

<div align="center">
<img src="power-bi-fullscreen.png" width="600" alt="画像3_フォーカスモード" title="画像3_フォーカスモード">
</div>

また、「レポートに戻る」ボタンで、複数ビジュアルが表示されている画面に戻ることが可能です。
<div align="center">
<img src="power-bi-fullscreen-after.png" width="600"  alt="画像4_フォーカスモード（戻る）" title="画像4_フォーカスモード（戻る）">
</div>

#### 並べ替え

グラフの内容によって、数値の大きさによって並べ替えて順位を確認したり、またはカテゴリ（年月）によって並べ替えて時系列で見たい場合が多くありますが、降順や昇順で選択できる他、並べ替え基準となるデータフィールドを選択することができます。

<div align="center">
<img src="sorting.png" width="600" alt="画像5_並べ替え" title="画像5_並べ替え">
</div>

#### テーブルとして表示

ビジュアルの直感重視で作成されたグラフは、詳細データの数値が表示されていない場合が多いですが、[テーブルとして表示]をクリックすると、詳細データがテーブル形式で表示されますので、気になる部分に関して、正確な数値を確認したい場合にご活用いただけます。

<div align="center">
<img src="view_as_table.png" width="600" alt="画像6_テーブルとして表示" title="画像6_テーブルとして表示">
</div>

---
## メールを受け取る
---

#### 受信登録

営業成績や KPI などの数字を毎日 Excel ファイルの日報として受け取る代わりに、Power BI 上でレポートを作成して受信登録をご利用いただけます。

データ更新後や決まった時間に毎日そのレポートやデータを確認したい場合に、[受信登録]を行なうことで、選択された送信頻度によって、毎日、毎時間、毎月、毎週 メールが届きます。

<div align="center">
<img src="subscription.png" width="700" alt="画像7_受信登録" title="画像7_受信登録">
</div>

送信されたメールでは、その時点のレポートの状態が表示される画像が添付されます。画像から、レポートへ直接アクセスすることも可能です。

<div align="center">
<img src="mail_sample.png" alt="画像8_受信メールサンプル" title="画像8_受信メールサンプル">
</div>

#### データアラート

さらに、ダッシュボードのタイルにあるゲージ、KPI 、カードのビジュアルに対して、データアラートを設定することができます。

<div align="center">
<img src="powerbi-alert-types-new.png" alt="画像9_ゲージ、KPI、カード" title="画像9_ゲージ、KPI、カード">
</div>

例えばダッシュボード上にある「今年の売上 (This Year's Sales) 」に対して、しきい値を設定し、そのしきい値を超えた場合、または未達の場合に、データアラートをメールにて受け取ることが可能です。

毎日の売上目標に対してや、制限の既定数値を超えた要注意の状況に、お知らせを受け取ることで、すぐに次のアクションに繋げられます。

<div align="center">
<img src="data_alert.png" alt="画像10_データアラート" title="画像10_データアラート">
</div>

</br>

> **参考情報**
> - [クイックスタート: "ビジネス ユーザー" 向けの Power BI の機能について学習する​](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-reading-view)
> - [Power BI のレポート内でビジュアルがどのように相互作用するか​](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-interactions)
> - [コンテンツを詳細に表示する: フォーカス モードと全画面表示モード​](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-focus)
> - [Power BI レポートでのグラフの並べ替え方法の変更​](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-change-sort)
> - [Power BI サービスでレポートまたはダッシュボードをサブスクライブする​](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-subscribe)
> - [Power BI サービスのデータ アラート](https://learn.microsoft.com/ja-jp/power-bi/create-reports/service-set-data-alerts)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
