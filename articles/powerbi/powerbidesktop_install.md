---
title: Power BI Desktop のインストール・更新方法について
date: 2023-09-29 00:00:00 
tags:
  - PowerBIDesktop　　
  - インストール
  - ストアアプリ
  - MicrosoftStore
  - 更新
  - アップデート
---
  
こんにちは、Power BI サポート チームの山崎です。   
Power BI Desktop にはインストール方法が 2 種類あることをご存じですか？   
最小要件や提供される機能は基本的には同じですが、いくつかの制限事項や違いがあります。   
本記事では、両者の違いをわかりやすくご案内しておりますので、どちらのインストール方法を採用するか迷った際にはご参考にしていただけますと幸いです。   

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---

##  <font color="DodgerBlue">Power BI Desktop のインストール方法は２種類</font>  
Power BI Desktop は、以下２つの方法で Windows 8.1 以上の PC にインストールして使用できる無償のアプリケーションです。   

・[ダウンロードセンター]( https://www.microsoft.com/ja-jp/download/details.aspx?id=58494)から Power BI Desktop のインストーラをダウンロードしてインストールする   
・Microsoft Store からインストールする  

ご参考情報：[Power BI Desktop の取得](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/desktop-get-the-desktop) 

### <font color="HotPink">Power BI Desktop のインストーラをダウンロードしてインストールする</font> 
ダウンロードセンターから、ご使用の OS と同じ bit 数のインストーラをダウンロードしインストールします。  
この方法でインストールした場合、次回以降の更新は毎回同じように、ダウンロードセンターからインストーラを取得して上書きインストールする必要があります。  
また、インストール時には管理者権限が必要です。   
組織やユーザーのタイミングで更新を行いたい場合や、Microsoft Store を利用できない場合はこちらの方法をご検討いただければと思います。     


### <font color="HotPink">Microsoft Store からインストールする</font> 

Microsoft Store からストアアプリとしてインストールします。 
インストール後の Power BI Desktop アプリとしての機能は基本的にはダウンロードセンターから入手したものと差はありません。  
ストアアプリとは Microsoft Store から入手・自動更新できるアプリであり、管理者権限を必要とせず標準ユーザーでもインストールできるように設計されています。  
サンドボックスという、他のアプリケーションやシステムとは隔離された仮想的な空間で動作するため、セキュリティが高い特徴があります。   
その他ストアプリのメリットとして、各更新のダウンロード量が少なくなること、言語サポートなどがあります。   
Microsoft Store を利用できる場合や、その後自動更新をしたい場合、ユーザー権限でインストールさせたい場合はこちらの方法をご検討いただければと思います。 


### <font color="HotPink">比較表 </font>   

|  | ダウンロードセンターからインストーラをダウンロードしてインストール  | Microsoft Store からストアアプリとしてインストール  |
| :-: | - | - |
| 最小要件  | ・Windows 8.1 または Windows Server 2012 R2 以降 <br>・.NET 4.6.2 以降 <br>・メモリ (RAM): 2 GB 以上使用可能、4 GB 以上を推奨) <br>・WebView2 <br>その他以下公開情報を参照 <br>[最小要件](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/desktop-get-the-desktop#minimum-requirements)  | ・Windows 8.1 または Windows Server 2012 R2 以降 <br>・.NET 4.6.2 以降 <br>・メモリ (RAM): 2 GB 以上使用可能、4 GB 以上を推奨) <br>・WebView2 <br>その他以下公開情報を参照 <br>[最小要件](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/desktop-get-the-desktop#minimum-requirements)  |
| 金額  | 無償 | 無償  |
| インストールに必要な権限  | 管理者特権が必要  | 標準ユーザーの権限にてインストール可能  |
| インストールパス（既定）  | C:\Program Files\Microsoft Power BI Desktop\(既定)  | C:\Program Files\WindowsApps  |
| 更新方法  | ダウンロードセンターから都度インストーラを入手  | 自動更新が可能  |
| 更新頻度  | 月1回程度（マイナーアップデートが発生することもあり） <br>ご参考：[Power BIのアップデート情報について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_feature_roadmap/)  | 月1回程度（マイナーアップデートが発生することもあり） <br>ご参考：[Power BIのアップデート情報について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_feature_roadmap/)  |
| その他制限事項  | ー | ・SAP コネクタを使用する場合、SAP ドライバー ファイルを Windows\System32 フォルダーに移動することが必要な場合がある <br>・Microsoft Store から Power BI Desktop をインストールしても、.exe バージョンのユーザー設定はコピーされないため、最近使ったデータ ソースに再接続し、資格情報を再入力することが必要な場合がある <br>・Oracle データベース コネクタを使用する場合場合、ドライバーの問題によりOracleデータベースに接続できない可能性がある <br>対処策は以下公開情報を参照 <br>  [Oracle データソース - トラブルシューティング](https://learn.microsoft.com/ja-jp/power-query/connectors/oracle-database#troubleshooting)  |

 </br>

##  <font color="DodgerBlue">使用しているPower BI Desktopがどちらのインストール方法でインストールされたか確認する方法 
 </font>   

Power BI Desktop を起動した状態で、タスク マネージャーを起動し、プロセス タブの一覧から Power BI Desktop アプリを展開し、“Microsoft Power BI Desktop” で右クリック ＞ プロパティを開きます。  
“場所” に表示されるパスで確認できます。   
以下例では、パスが “C:\Program Files\Microsoft Power BI Desktop\” 配下なので、ダウンロードセンターから入手した Power BI Desktop であることが確認できます。 

<div align="left">
<img src="1.png">
</div>
</p>

 </br>


## <font color="DodgerBlue">組織での一括インストールや更新方法について
 </font>  

上記ダウンロードセンターから入手する従来のデスクトップアプリとストアアプリのどちらを採用するかにより、検討可能な方法は異なってまいります。   
Power BI Desktop に特化した運用方法のベストプラクティスはご用意がありませんので、ユーザー様の組織において、既存のデスクトップアプリやストアアプリをどのように運用されているかをご確認の上ご検討いただければと存じます。   

 </br>
 
  


以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。



---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)