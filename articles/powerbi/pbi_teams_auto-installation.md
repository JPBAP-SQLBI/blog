---
title: Microsoft Teams の Power BI アプリの自動インストール機能について
date: 2021-09-30 00:00:00 
tags:
  - Power BI
  - Teams
---


<span style="color: red; ">Update: 2021/10/6
現在下記機能の追加について、11月初旬から12月末までに実施されることを確認いたしました。
今後の予定についても変更されることがあることから、一部スケジュールの記載を変更しております。詳しくは記事内をご確認ください。
</span>



こんにちは、Power BI サポート チームの山本です。 

Power BI では、 Microsoft Teams との統合 を通じて、 Microsoft Teams 上で Power BI サービスを利用することができる Power BI アプリが用意されています。
今回は、2021年11月にリリース予定とアナウンスされている「Microsoft Teams の Power BI アプリの自動インストール機能」についてご案内します。

※Microsoft Meesage Center から「MC288054 Configuration Change: Power BI app for Microsoft Teams automatic installation and availability for government customers」のタイトルで通知されているものと同様になります。

<!-- more -->

</br>

> [!IMPORTANT]
> 本記事は 弊社公式ブログ「Microsoft Power BI ブログ」の公開情報を元に構成しておりますが、本記事編集時点と実際の機能やリリース時期に相違がある場合がございます。
>元記事は以下よりご確認ください（英語）
><Span style="font-size: 90%">[Pre-Announcing Automatic Installation of the Power BI app for Microsoft Teams](https://powerbi.microsoft.com/ja-jp/blog/pre-announcing-automatic-installation-of-the-power-bi-app-for-microsoft-teams/)</span>


</br>


---

## Microsoft Teams の Power BI アプリ とは

Microsoft Teams の Power BI アプリは、Teams で Power BI を利用して共同作業できる方法の 1 つです。 
Power BI アプリをインストールすると、Power BI サービスのように、次のような操作を Microsoft Teams で行うことができます。

- ダッシュボード、レポート、アプリを作成、表示、編集する。
- ワークスペースを作成し、参加する。
- メールまたは Microsoft Teams を使用してコンテンツを共有する。

また、通常の Power BI サービスにはない、Teams で表示したすべての Power BI タブを表示する機能も備わっています。

<div align="center">
<img src="pic0.png" alt="画像1_Power BI アプリ" title="画像1_Power BI アプリ">
</div>


</br>

参考情報：[Power BI アプリを Microsoft Teams に追加する](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-microsoft-teams-app)

<!-- そして、今回自動インストール機能により、より多くのユーザーがこれらの機能を利用できるようになりました。また、Power BIと Teams の管理者にとっても、ユーザーに Power BI エクスペリエンスを Teams にインストールするためだけに、Microsoft Teams アプリのセットアップポリシーを作成・管理する必要性が減るため、助かります。-->

</br>

## Microsoft Teams 用の Power BI アプリの自動インストール機能について

今回事前アナウンスされている機能は以下の通りです。

- Power BIは、ユーザーが Power BI サービスにアクセスした際に、自動的に Teams の Power BI アプリのインストールを開始する。
- Power BI 管理者は、Power BI 管理ポータルのテナント設定を通じて、自動インストールしないことを選択できる。
- このテナント設定は、今後順次追加される予定。
- この設定を「有効」にした組織では、Teams 用の Power BI アプリの自動インストールが開始される予定。

</br>

## 自動インストール機能を無効にしたい場合

Power BI 管理ポータルのテナント設定から自動インストール機能を無効にすることが可能です。

今後順次、テナント設定に「Install Power BI app for Microsoft Teams automatically tenant」の設定が追加され、Power BI 管理者は、ここから自動インストールの有効・無効を設定することができます。
デフォルトでは、自動インストールが有効になっています。

<div align="center">
<img src="pic3.png" alt="画像2_テナント設定" title="画像2_テナント設定">
</div>

</br>

## 自動インストールの条件・タイミング

自動インストールは、以下の条件のユーザーに対して行われます。

- Microsoft Teams の管理ポータルで Power BI app for Microsoft Teams が許可に設定されている。
- Power BI テナントの設定「Install Power BI app for Microsoft Teams automatically」が有効になっている。
- ユーザーが Microsoft Teams のライセンスを持っている
- ユーザーが Power BI サービス（例：app.powerbi.com）へサインインし、アクティブ化している

当機能のリリース当初においては、自動インストールは、新規ユーザーが初めて Web ブラウザーで Power BI サービスにアクセスしたときに適用されます。
将来的には、条件を満たした Power BI サービスのすべてのアクティブユーザーに自動インストールの実施が予定されています。

自動インストールが行われると、Power BI サービスの通知ペインに以下の通知が表示されます。

<div align="center">
<img src="pic2.png" alt="画像3_インストール通知" title="画像3_インストール通知">
</div>

</br>
</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)