
---
title: Power BI レポートの埋め込み方法の種類について
date: 2021-11-30 00:00:00 
tags:
  - Power BI　　
  - 埋め込み
  - embed
  - embedded
  - SharePoint Online
  - Webに公開
  - Webパーツ
---


こんにちは、Power BI サポート チームです。   

Power BIで作成したレポートをPower BI サービス上で共有する方法は以前に以下Blogでご紹介させていただきましたが、WebサイトやSharePoint Online、Webアプリケーションにレポートを埋め込むことができるのをご存じでしょうか？  
他のWebサイトなどのコンテンツにレポートを埋め込むことは、より多くのユーザーにレポートを閲覧してもらいやすいようにするために大変有効な方法であり、弊社サポートへお問い合わせとしてもいただくことが多い課題となります。  
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
・Webに公開（パブリック）  
・Power BI Embeddedによる埋め込み（開発者playグラウンド）

<div align="center">
<img src="1.png">
</div>


#### １．SharePoint Online にレポート Web パーツを埋め込む

SharePoint Online 用レポート Web パーツとして、Power BI レポートを SharePoint Online のページに簡単に埋め込むことができます。  
簡単ですべてのPower BI ユーザーにおいて最も頻繁に使用されている方法となりますが、Power BI サービス上のレポートにSharePoint Online上でアクセスすることになりますので、共有されるときと同様に閲覧する側がProまたはPPUのライセンスを持っているか、対象のレポートがPremium領域のワークスペース内に
作成されている必要があります。

//  要件  
・閲覧する側がProまたはPPUのライセンスを持っているか、対象のレポートがPremium領域のワークスペース内に作成されている  
・閲覧者はPower BIにサインインする必要がある  
・閲覧者は、対象のレポートに対して閲覧権限を持っている  
　（Power BI サービス上で、管理者が明示的に設定する必要があり、埋め込みによって自動的には設定されません。）

<div align="center">
<img src="2.png">
</div>


#### ２．Web サイトまたはポータル

URL または i Frame の埋め込みを受け取るあらゆるポータルにノーコードで、安全にレポートを埋め込むことができます。  
上記１と同様、閲覧する側がProまたはPPUのライセンスを持っているか、対象のレポートがPremium領域のワークスペース内に作成されている必要があります。

//  要件  
・閲覧する側がProまたはPPUのライセンスを持っているか、対象のレポートがPremium領域のワークスペース内に作成されている  
・閲覧者はPower BIにサインインする必要がある  
・閲覧者は、対象のレポートに対して閲覧権限を持っている  
　（Power BI サービス上で、管理者が明示的に設定する必要があり、埋め込みによって自動的には設定されません。）

<div align="center">
<img src="3.png">
</div>


#### ３．Webに公開（パブリック）

レポートをブログ記事、Web サイト、メールやソーシャル メディアなどに簡単に埋め込むことができます。  
閲覧者はインターネット上のすべてのユーザーとなり、Power BI ライセンスは不要となります。  
Webに公開したレポートはインターネット上で公開されてしまい、URLさえ辿り着けば誰でも閲覧できてしまいますので、機密データでのWeb公開はおすすめしません。  
本機能を使用される場合は、取り扱うデータに十分ご注意くださいますようお願いいたします。

//  要件  
・閲覧者はインターネット上のすべてのユーザーとなり、Power BI ライセンスは不要

<div align="center">
<img src="4.png">
</div>

#### ４．Power BI Embeddedによる埋め込み（開発者playグラウンド）

こちらは上記１～３とは異なり、Power BI Embeddedの環境と開発が必要となりますが、レポート、ダッシュボードおよびタイルなどのPower BI コンテンツをアプリケーションに埋め込むことができます。  
閲覧ユーザー一人ひとりがPower BI ライセンスを持つ必要がなく、閲覧用の環境を自由に作成することが可能でございますが、別途開発環境が必要で自由に作成できる分、開発コストがかかります。  
なお、埋め込みには顧客向け埋め込みと組織向け埋め込みの２つの方法がありますので、詳細については後述の参考情報をご確認いただければと思います。

//  要件  
・Power BI Embedded環境が必要  
・ユーザー自身で開発を行う

<div align="center">
<img src="5.png">
</div>

以下、上記埋め込みにつきまして、公開情報もあわせてあらためて表におまとめいたしました。  

|種類|必要なライセンス|埋め込み方法|埋め込み対象|公開情報|
|:----|:----|:----|:----|:----|
|Webに公開|閲覧者はインターネット上のすべてのユーザー（Power BI ライセンス不要）|[Web に公開] を使用して埋め込みコードを作成し使う|ブログ記事、Web サイト、メールやソーシャル メディアなど|[Power BI から Web への公開](https://docs.microsoft.com/ja-jp/power-bi/collaborate-share/service-publish-to-web)  |
|SharePoint Online にレポート Web パーツを埋め込む|閲覧者はProまたはPPUのライセンスを持っているか、対象のレポートがPremium領域のワークスペース内に作成されている（Premium＋Freeライセンス）|レポートの URL を取得し、SharePoint Online の Power BI Web パーツでその URL を使う|SharePoint Online のページ|[SharePoint Online にレポート Web パーツを埋め込む](https://docs.microsoft.com/ja-jp/power-bi/collaborate-share/service-embed-report-spo)  |
|セキュリティで保護されたポータルまたは Web サイトにレポートを埋め込む|閲覧者はProまたはPPUのライセンスを持っているか、対象のレポートがPremium領域のワークスペース内に作成されている（Premium＋Freeライセンス）|安全な埋め込みコードまたはiFrameのコードを作成し使う|内部 Web ポータル（ポータルは クラウドベース か、SharePoint 2019 など、ホステッド オンプレミス ）|[セキュリティで保護されたポータルまたは Web サイトにレポートを埋め込む](https://docs.microsoft.com/ja-jp/power-bi/collaborate-share/service-embed-secure)|
|Embeddedによる埋め込み（顧客向け）|・Embeddedライセンス<br>・閲覧者はPower BI ライセンス不要|.NET FrameworkやJavaなどのフレームワークを使用し、APIを用いてアプリケーションを開発する|SaaSサービス以外のWebアプリケーション|[Power BI 埋め込み分析アプリケーションにコンテンツを埋め込む](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/embed-sample-for-customers?tabs=net-core)|
|Embeddedによる埋め込み（組織向け）|・Embeddedライセンス<br>・閲覧者はPower BI ライセンス不要|.NET FrameworkやJavaなどのフレームワークを使用し、APIを用いてアプリケーションを開発する|SaaSサービス以外のWebアプリケーション|[組織向けの埋め込み BI 分析情報を向上させるため、Power BI 埋め込み分析アプリケーションにコンテンツを埋め込む](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/embed-sample-for-your-organization?tabs=net-core)|


以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。


