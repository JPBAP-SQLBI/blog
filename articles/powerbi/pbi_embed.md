---
title: Power BI レポートの埋め込み方法の種類について
date: 2021-11-30 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Power BI Service
  - 埋め込み
  - Embed
  - Embedded
---


こんにちは、Power BI サポート チームの山崎です。   

Power BI で作成したレポートを Power BI サービス上で共有する方法は以前に以下 Blog でご紹介させていただきましたが、Web サイトや SharePoint Online、Web アプリケーションにレポートを埋め込むことができるのをご存じでしょうか？  
他の Web サイトなどのコンテンツにレポートを埋め込むことは、より多くのユーザーにレポートを閲覧してもらいやすいようにするために大変有効な方法であり、弊社サポートへお問い合わせとしてもいただくことが多い課題となります。  
埋め込み方法ごとに必要なライセンスや手順などが異なりますので、本ブログではメリット・デメリットもあわせてご紹介いたします。

<!-- more -->

参考情報：[Power BIサービスでのコンテンツ共有方法の種類](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_contents_share_1/)  

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


---

## 埋め込み方法の種類について

レポートの埋め込み方法は、以下４つに分けられ、対象レポートの “ファイル” ＞ “レポートの埋め込み” から埋め込み操作を開始できます。  
選択肢に表示されない場合は、Power BI 管理者にて機能の使用を制限されているか、各埋め込み機能における制限事項に該当している可能性がありますので、本メールの最後にご案内する参考情報にて詳細をご確認ください。

・SharePoint Online  
・Web サイトまたはポータル  
・Web に公開（パブリック）  
・Power BI Embedded による埋め込み（開発者playグラウンド）

<div align="center">
<img src="1.png">
</div>


#### １．SharePoint Online にレポート Web パーツを埋め込む

SharePoint Online 用レポート Web パーツとして、Power BI レポートを SharePoint Online のページに簡単に埋め込むことができます。  
簡単ですべてのPower BI ユーザーにおいて最も頻繁に使用されている方法となりますが、Power BI サービス上のレポートに SharePoint Online 上でアクセスすることになりますので、共有されるときと同様に閲覧する側が Pro または PPU のライセンスを持っているか、対象のレポートが Premium 領域のワークスペース内に作成されている必要があります。  

//  要件  
・閲覧する側が Pro または PPU のライセンスを持っているか、対象のレポートが Premium 領域のワークスペース内に作成されている  
・閲覧者は Power BI にサインインする必要がある  
・閲覧者は、対象のレポートに対して閲覧権限を持っている  
　（Power BI サービス上で、管理者が明示的に設定する必要があり、埋め込みによって自動的には設定されません。）

<div align="center">
<img src="2.png">
</div>


#### ２．Web サイトまたはポータル

URL または i Frame の埋め込みを受け取るあらゆるポータルにノーコードで、安全にレポートを埋め込むことができます。  
上記１と同様、閲覧する側が Pro または PPU のライセンスを持っているか、対象のレポートが Premium 領域のワークスペース内に作成されている必要があります。

//  要件  
・閲覧する側が Pro または PPU のライセンスを持っているか、対象のレポートが Premium 領域のワークスペース内に作成されている  
・閲覧者は Power BI にサインインする必要がある  
・閲覧者は、対象のレポートに対して閲覧権限を持っている  
　（ Power BI サービス上で、管理者が明示的に設定する必要があり、埋め込みによって自動的には設定されません。）

<div align="center">
<img src="3.png">
</div>


#### ３．Webに公開（パブリック）

レポートをブログ記事、Web サイト、メールやソーシャル メディアなどに簡単に埋め込むことができます。  
閲覧者はインターネット上のすべてのユーザーとなり、Power BI ライセンスは不要となります。  
Web に公開したレポートはインターネット上で公開されてしまい、URL さえ辿り着けば誰でも閲覧できてしまいますので、機密データでの Web 公開はおすすめしません。  
本機能を使用される場合は、取り扱うデータに十分ご注意くださいますようお願いいたします。

//  要件  
・閲覧者はインターネット上のすべてのユーザーとなり、Power BI ライセンスは不要

<div align="center">
<img src="4.png">
</div>

#### ４．Power BI Embeddedによる埋め込み（開発者playグラウンド）

こちらは上記１～３とは異なり、Power BI Embedded の環境と開発が必要となりますが、レポート、ダッシュボードおよびタイルなどの Power BI コンテンツをアプリケーションに埋め込むことができます。  
閲覧ユーザー一人ひとりが Power BI ライセンスを持つ必要がなく、閲覧用の環境を自由に作成することが可能でございますが、別途開発環境が必要で自由に作成できる分、開発コストがかかります。  
なお、埋め込みには顧客向け埋め込みと組織向け埋め込みの２つの方法がありますので、詳細については後述の参考情報をご確認いただければと思います。

//  要件  
・Power BI Embedded 環境が必要  
・ユーザー自身で開発を行う

<div align="center">
<img src="5.png">
</div>

以下、上記埋め込みにつきまして、公開情報もあわせてあらためて表におまとめいたしました。  

|種類|必要なライセンス|埋め込み方法|埋め込み対象|公開情報|
|:----|:----|:----|:----|:----|
|Webに公開|閲覧者はインターネット上のすべてのユーザー（Power BI ライセンス不要）|[Web に公開] を使用して埋め込みコードを作成し使う|ブログ記事、Web サイト、メールやソーシャル メディアなど|[Power BI から Web への公開](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-publish-to-web)  |
|SharePoint Online にレポート Web パーツを埋め込む|閲覧者はProまたはPPUのライセンスを持っているか、対象のレポートがPremium 容量のワークスペース内に作成されている（Premium＋Freeライセンス）|レポートの URL を取得し、SharePoint Online の Power BI Web パーツでその URL を使う|SharePoint Online のページ|[SharePoint Online にレポート Web パーツを埋め込む](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-embed-report-spo)  |
|セキュリティで保護されたポータルまたは Web サイトにレポートを埋め込む|閲覧者はProまたはPPUのライセンスを持っているか、対象のレポートがPremium 容量のワークスペース内に作成されている（Premium＋Freeライセンス）|安全な埋め込みコードまたはiFrameのコードを作成し使う|内部 Web ポータル（ポータルは クラウドベース か、SharePoint 2019 など、ホステッド オンプレミス ）|[セキュリティで保護されたポータルまたは Web サイトにレポートを埋め込む](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-embed-secure)|
|Embeddedによる埋め込み（顧客向け）|・Embeddedライセンス<br>・閲覧者はPower BI ライセンス不要|.NET FrameworkやJavaなどのフレームワークを使用し、APIを用いてアプリケーションを開発する|SaaSサービス以外のWebアプリケーション|[Power BI 埋め込み分析アプリケーションにコンテンツを埋め込む](https://learn.microsoft.com/ja-jp/power-bi/developer/embedded/embed-sample-for-customers?tabs=net-core)|
|Embeddedによる埋め込み（組織向け）|・閲覧者はProまたはPPUのライセンスを持っているか、対象のレポートがPremium または Embedded 容量のワークスペース内に作成されている（容量＋Freeライセンス）|.NET FrameworkやJavaなどのフレームワークを使用し、APIを用いてアプリケーションを開発する|SaaSサービス以外のWebアプリケーション|[組織向けの埋め込み BI 分析情報を向上させるため、Power BI 埋め込み分析アプリケーションにコンテンツを埋め込む](https://learn.microsoft.com/ja-jp/power-bi/developer/embedded/embed-sample-for-your-organization?tabs=net-core)|


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)


