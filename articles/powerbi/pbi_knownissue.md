---
title: Power BI の既知の問題や障害に関する公開情報について
date: 2023-04-28 00:00:00 
tags:
  - PowerBI　　
  - known issue
  - 既知の問題
  - 不具合
  - bug
  - 障害
  - Outage
  - Power BI Desktop
  - Power BI サービス
  - Power BI Service
---


こんにちは、Power BI サポート チームの山崎です。   
Power BI Desktop や Power BI サービスを使用していて、「この動作は不具合なのでは？」「もしかして障害が発生しているのかな？」と思ったことはありますか？  
そのようなときは、まずは落ち着いて以下でご案内する公開情報をもとに既知の問題や障害に該当している可能性がないかご確認いただきますようお願いいたします。  

<!-- more -->
> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---

##  <font color="DodgerBlue">公開情報のご案内 </font>  

### <font color="HotPink">Power BI の既知の問題</font> 
<font color="SlateGray">対象：ユーザー様、管理者様向け</font>  

影響度がおおきいものについては以下公開情報に既知の問題として一覧でまとめられています。  
不具合が疑われる動作を確認した際は、まずは以下一覧にある問題に該当していないかご確認ください。  

参考情報：   
[Power BI の既知の問題](https://learn.microsoft.com/ja-jp/power-bi/troubleshoot/known-issues/power-bi-known-issues) 

### <font color="HotPink">サービスレベルの停止</font> 
<font color="SlateGray">対象：ユーザー様、管理者様向け</font>  

クラウドサービスである Power BI サービスにアクセスできない、レポートを表示できないなど、サービスの停止や低下が疑われる場合は、こちらサポートページの [ リージョンごとのサービス状態 ] [ サービスの停止/低下 ] をご確認ください。  
また、こちらのページの [ 認識 ] には、修正が近い将来に行われるような緊急度の高い問題について、その問題の詳細や今後予定されている修正スケジュールが報告されることもあり、解決されるとお知らせから削除されます。  


<div align="center">
<img src="1.png">
</div>
</p>

参考情報：   
[Power BI のサポート](https://powerbi.microsoft.com/ja-jp/support/) 

   

### <font color="HotPink">Microsoft 365 サービス 正常性</font> 
<font color="SlateGray">対象：管理者様向け</font>  

クラウドサービスで問題が発生している場合に、対象テナントやリージョンの Microsoft 365 管理センターの “サービス正常性” ページで報告されることもあります。
“未解決の問題”の[影響を受けたサービス]や、”Microsoft サービスの正常性” の[サービス]の覧に Power BI に関する報告がないかご確認ください。

参考情報：   
[How to check Microsoft 365 service health](https://learn.microsoft.com/ja-jp/microsoft-365/enterprise/view-service-health?view=o365-worldwide)
<div align="center">
<img src="2.png">
</div>
</p>


### <font color="HotPink">Azure 正常性（Embedded）</font> 
<font color="SlateGray">対象：管理者様向け</font>  
Embedded をご運用されている場合は、Azure ポータルの Power BI Embedded リソースの “リソースの正常性” にてリソースの状況をご確認ください。

<div align="center">
<img src="3.png">
</div>
</p>

### <font color="HotPink">サービス中断の通知</font> 
<font color="SlateGray">対象：管理者様向け</font>  
Premium 容量のみとなりますが、サービスの中断や停止がある場合に、Power BI からのインシデント通知をメールで受け取ることができます。
以下公開情報にて設定方法やメール送信されるシナリオ等をご案内しています。

[サービス中断の通知](https://learn.microsoft.com/ja-jp/power-bi/support/service-interruption-notifications)


## <font color="DodgerBlue">サポートからのご案内</font>  
・公開情報で報告されている問題についてお問合せいただいても、基本的には公開情報以上の内部情報はご案内できませんので、定期的に公開情報の更新をご確認いただきますようお願いいたします。  
</p>

・公開情報で報告されているもの以外に、弊社サポートサービスへいただいたお問合せの調査の中で見つかる問題があります。  
  影響範囲がおおきいものについては、公開情報にてお知らせされる場合がありますが、基本的にその他の問題については、セキュリティや機密情報保持等の関係上公開しておりません。  
  なお、問題が確認されたあと、開発部門にて今後の修正スケジュールの調整・対応が行われますが、数か月以上かかるものがほとんどで、なかには半年以上かかるものや影響度や暫定対処策の有無によって今後のスケジュールが未定のままとなることもあります。  
  このような公開されていない問題については、お問合せベースで進捗状況や今後のスケジュールをご案内することはできませんので、あらかじめご了承ください。  
  Power BI Desktop および Power BI サービスは定期的に更新が行われていますので、ユーザー様・管理者様にて動作をご確認いただきますようお願いいたします。  


</p>
</p>   
以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。


  
**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)