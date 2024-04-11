---
title: Power BI の通信設定
date: 2022-04-28 00:00:00 
tags:
  - 通信設定　　
  - 許可リスト
  - ホワイトリスト
  - エンドポイント
  - オンプレミスデータゲートウェイ
  - IP アドレス
  - Azure IP Ranges
---


こんにちは、Power BI サポート チームの山崎です。  
今回は、IT 管理者様やネットワークご担当者様必読の内容となります。  
Power BI サービスを使用するためにはインターネット接続が必要となりますが、ご環境によっては最低限の通信のみを許可されている場合も多くあるかと思います。  
このため、弊社サポートには、Power BI サービスに必要な通信が許可されていないことで Power BI サービスにアクセスできない・データ更新ができないなどの問題が発生しお問い合わせをいただくことがよくあります。  
そこで、Power BI サービスではどのような通信が発生しているか、どのような通信設定が必要かご案内いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---

#### 必要な通信設定は２つあります

Power BI サービスを利用するためには、対象のご環境にて以下 2 つの通信許可設定を行っていただく必要があります。


##### ①  ホワイトリスト登録用の Power BI の URL
Power BI サービスではインターネットへの接続が必要です。  
以下公開情報にて案内しているエンドポイントが使用されますが、 [目的] の欄が “必須” となっているエンドポイントにつきましては、すべて許可していただくことを推奨しております。  
これらの通信が許可されていないと、Power BI サービスを正常に使用できないことがあります。  

ご参考情報
[ホワイトリスト登録用の Power BI の URL](https://learn.microsoft.com/ja-jp/power-bi/power-bi-whitelist-urls)　  


##### ②　Azure IP Ranges  

Power BI サービスの通信に使用される IP アドレスにつきましては、リージョンごとに振られた IP アドレスの範囲内の IP アドレスが動的に割り当てられます。  
以下 URL より IP アドレス一覧をダウンロードいただき、対象のご環境のリージョンに振られている IP アドレスの範囲を登録していただく必要があります。  

ご参考情報
[Azure IP Ranges and Service Tags – Public Cloud](https://www.microsoft.com/en-us/download/details.aspx?id=56519)　  

上記 URL より .json ファイルをダウンロードし、"AzureCloud.XXXX” 配下にある IP アドレスの範囲を確認します。  
例：東日本リージョンの場合は、"AzureCloud.japaneast” 配下にある IP アドレスの範囲を確認します。  
※　対象のご環境のリージョンは以下公開情報で案内している方法でご確認いただけます。  

ご参考情報  
[Power BI テナントの場所を確認する方法](https://learn.microsoft.com/ja-jp/power-bi/service-admin-where-is-my-tenant-located#how-to-determine-where-your-power-bi-tenant-is-located)　  


###### <span style="color: orange; ">考慮事項1</span>
Power BI サービスで使用される IP アドレスはリージョンごとに割り当てられた範囲内で動的に変わり、事前にキャッチできる情報ではありません。  
そのため、IP アドレスの範囲内で現在使われている IP アドレスを固定でファイアウォールのホワイトリストに登録するのではなく、 IP アドレスの範囲でご登録いただくことをお勧めいたします。

###### <span style="color: orange; ">考慮事項2</span> 
データソースと Power BI サービスの接続は各製品に接続が確立できているかご確認が必要となりますが、Azure リソースは NSG や Azure Firewall を使用して IP ranges の代替として Power BI サービスタグの設定でも通信できるようになります。


<br>


##### <span style="color: orange; ">上記内容につきまして、よりイメージしていただきやすいよう画像と例をもとにご案内いたします</span>

① ホワイトリスト登録用の Power BI の URL と ②　Azure IP Ranges は、Power BI サービスをお使いいただく上でそれぞれ設定が有効な範囲が異なるため、両方必要となります。  

_クライアント <--**① ホワイトリスト登録用の Power BI の URL** --> PBI サービス <--**②　Azure IP Ranges** --> Azure サービス・他社サービス・On-Premises data gateway_
 
<div align="center">
<img src="1.png">
</div> 


例：ユーザーが Power BI サービスにサインインし、レポートを参照する場合の通信  

（１） ユーザーが Web ブラウザから Power BI サービスにサインインします。  
 **① ホワイトリスト登録用の Power BI の URL** のリストにあるエンドポイントとの通信が発生いたします。   

（２） ユーザーは、Power BI サービス上に保管されているレポートを参照します。  
Power BI サービスは、データ更新時など必要に応じて Azure 内で使用している各種サービスやデータソースと通信します。  
  このタイミングで、**② Azure IP Ranges** 内で動的に割り当てられたIP アドレスによる通信が発生いたします。

<br>

##### <span style="color: orange; ">オンプレミス データ ゲートウェイを経由しデータ ソースと接続する場合　※１</span>

オンプレミス データ ゲートウェイを使用する場合、上記に加えて、ご環境によっては送信ポートの許可設定や、プロキシ関連の設定が必要となりますので、以下公開情報もあわせてご参考にしていただきますようお願いいたします。

ご参考情報  
・オンプレミス データ ゲートウェイで使用される送信ポートの許可または HTTPS 通信の強制設定が必要となります。  
[オンプレミス データ ゲートウェイのコミュニケーション設定を調整](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-communication)  

・プロキシ経由でインターネットにアクセスしている場合は、オンプレミス データ ゲートウェイの構成ファイルの変更が必要となります。  
[オンプレミス データ ゲートウェイのプロキシ設定の構成](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-proxy)   

<br>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
