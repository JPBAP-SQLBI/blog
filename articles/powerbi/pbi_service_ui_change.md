---
title: Power BI サービスのデザイン変更について
date: 2022-09-30 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Admin
---

</br>

こんにちは、Power BI サポート チームの山本です。
Power BI では、日々管理者やユーザーの意見を取り入れ、ユーザーインターフェース (UI) の変更や改善、機能追加を進めています。
本記事では、デザイン変更の実験的機能や実際にデザインが変更された事例についてご紹介いたします。

<!-- more -->


<br>

> [!IMPORTANT]
> 本記事は弊社公開情報を元に構成しておりますが、
> 本記事編集時点と実際の見解に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


---
## 目次
---
1. [Power BI におけるデザイン変更・管理者設定について](#Power-BI-におけるデザイン変更・管理者設定について)
2. [事例① - Power BI アプリ作成時のデザイン変更](#事例①-Power-BI-アプリ作成時のデザイン変更)
3. [事例② - ナビゲーションペインのデザイン変更](#事例②-ナビゲーションペインのデザイン変更)

<br>

---
## Power BI におけるデザイン変更・管理者設定について
---

通常 Power BI ではユーザーインターフェースや動作に変更があった場合に、マイクロソフトの公開情報である [Power BI ドキュメント](https://learn.microsoft.com/ja-jp/power-bi/) や [Power BI Blog](https://powerbi.microsoft.com/en-us/blog/) で変更点について紹介しています。
しかし、新機能として紹介されていないデザイン変更について、一部のユーザーにいち早く展開し、小規模なエクスペリエンステストを行い、ユーザーの使用感を測ることがあります。例えば「特に公開情報やブログでは紹介されていないが、以前と比べてデザインが変わっている」というような場合、このエクスペリエンステストに該当している可能性があります。

このデザイン変更は Power BI を使用しているすべてのユーザーがテスト対象になる可能性がありますが、エクスペリエンステストを機能させたくない場合には Power BI 管理者によって、テナント設定で無効化することが可能です。

</br>

<div align="center">
<img src="1.png" alt="[設定 - 管理ポータル - テナント設定 - ユーザー エクスペリエンスの実験 - Power BI でのエクスペリエンスの最適化を支援する]" title="[設定 - 管理ポータル - テナント設定 - ユーザー エクスペリエンスの実験 - Power BI でのエクスペリエンスの最適化を支援する]">
</div>

</br>

### 注意点

・[Power BI でのエクスペリエンスの最適化を支援する] が有効化されている場合でも、テスト対象とはならない場合があります。
・クラウドサービスの特性上、すべてのデザイン変更について、エクスペリエンステストを行なっているわけではございません。エクスペリエンステストなくデザインが変更になる場合があることをご理解ください。

<br>

> **参考情報**
> - [Power BI でのエクスペリエンスの最適化を支援する](https://learn.microsoft.com/ja-jp/power-bi/admin/service-admin-portal-user-experience-experiments)

<br>

---
## 事例① - Power BI アプリ作成時のデザイン変更
---

従来 Power BI アプリは、各ワークスペースごとに選択されたレポートやダッシュボードなどのコンテンツをパッケージ化して発行できるものでしたが、新たにオーディエンス機能が追加されたことで、1つのアプリで、複数のグループに異なるコンテンツを表示したり非表示にしたりすることができるようになりました。

</br>

<div align="center">
<img src="3.png" alt="従来のアプリ作成画面" title="従来のアプリ作成画面">
</div>

</br>

<div align="center">
<img src="4.png" alt="新しいアプリ作成画面" title="新しいアプリ作成画面">
</div>



</br>

> **参考情報**
> - [Power BI でアプリを発行する](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-create-distribute-apps)
> - [Announcing Public Preview of Multiple Audiences for Power BI Apps](https://powerbi.microsoft.com/en-us/blog/announcing-public-preview-of-multiple-audiences-for-power-bi-apps/)

<br>

---
## 事例② - ナビゲーションペインのデザイン変更
---

Power BI サービスの左側に表示される、ホームや作成、ワークスペースなどのリンクが表示されるナビゲーションペインについて、2022年3月から6月の間に、エクスペリエンステストが実施されました。

2022年9月現時点では既にすべてのユーザーでデザインが変更されたこのナビゲーションペインですが、以下の部分で変更が実施されています。

1. ナビゲーション変更 - 「参照」項目が新たに作成され、「最近」、「お気に入り」、「自分と共有」のリストが統合
2. 表示の変更 - 「最近」、「お気に入り」、「アプリ」リストには、最初の12件だけでなく、リストに含まれるすべてのコンテンツが表示されるように変更
3. スタイルの更新 - Power BI のスタイル（色、アイコン、フォントなど）が更新され、[Fluent](https://www.microsoft.com/design/fluent/#/) デザインシステムに準拠するように変更

</br>

<div align="center">
<img src="2.png">
</div>

</br>

> **参考情報**
> - [Coming soon: Changes to the Power BI service – simpler navigation, improvements to lists on Home, and style updates](https://powerbi.microsoft.com/en-us/blog/coming-soon-changes-to-the-power-bi-service-simpler-navigation-improvements-to-lists-on-home-and-style-updates/)

<br>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/) 