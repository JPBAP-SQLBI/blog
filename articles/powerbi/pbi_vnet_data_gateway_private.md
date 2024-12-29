---
title: 仮想ネットワーク (VNet) データ ゲートウェイからプライベートデータソースへの接続
date: 2024-11-29 00:00:00 
tags:
  - Power BI
  - Microsoft Fabric
  - Power BI サービス
  - 仮想ネットワーク (VNet) データゲートウェイ
  - プライベートエンドポイント
  - VNet データゲートウェイ
  - virtual network (VNet) data gateway
  - VNet data gateway
  - private endpoint

---

こんにちは、Power BI サポート チームの中川です。

Microsoft Fabric からプライベートなデータソースに接続する際には、従来、オンプレミス データ ゲートウェイが主に利用されてきましたが、VNet データ ゲートウェイを利用することで、同様にプライベートなデータソースへの接続が可能となります。

本ブログでは、 VNet データゲートウェイを利用し、Private Endpoint を有効にした SQL Server に接続する手順についてご紹介します。


<!-- more -->
> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [はじめに](#はじめに)
* [作成する構成](#作成する構成)
* [VNet/Private Endpoint を有効にした SQL Server の構築](#vnetprivate-endpoint-を有効にした-sql-server-の構築)
* [Microsoft Fabric で VNet データ ゲートウェイを利用するための設定](#microsoft-fabric-で-vnet-データ-ゲートウェイを利用するための設定)
* [おわりに](#おわりに)


---
## はじめに
---

オンプレミス データ ゲートウェイの記事でご紹介した構成と同様に、今回も Private Endpoint を有効化した SQL Server を例に、接続の構成例をご紹介します。具体的なイメージは以下の通りです。


<div align="center">
<img src="1_Configuration_image.png">
</div>


</br>
ユーザーはインターネットを経由して Microsoft Fabric にアクセスすることが可能ですが、SQL Server にはパブリック アクセスが禁止されているため、直接接続することはできません。
また、Microsoft Fabric も同様に、SQL Server に直接アクセスすることはできません。

</br>
この制約を解決するため、仮想ネットワーク (VNet) 内に構築された VNet データ ゲートウェイを経由して SQL Server にアクセスする構成を作成します。この方法により、プライベートなデータソースへ接続することが可能になります。
今回は、この構成を データフロー Gen2 を使用して作成する例をご紹介します。

>[!NOTE]
> 参考情報：[初めての Microsoft Fabric データフローを作成する - Microsoft Fabric | Microsoft Learn)](https://learn.microsoft.com/ja-jp/fabric/data-factory/create-first-dataflow-gen2)


なお、オンプレミスデータゲートウェイを利用したプライベートなデータソースへ接続する方法につきましては、以下の公開ブログをご参照ください。
>[!NOTE]
> 参考情報：[Private なデータソースへ接続する | Japan CSS Support Power BI Blogn)](https://jpbap-sqlbi.github.io/blog/powerbi/PrivateDatasource/)


VNet データゲートウェイの紹介に関する前回のブログはこちらをご参照ください。
>[!NOTE]
> 参考情報：[仮想ネットワーク (VNet) データ ゲートウェイ について | Japan CSS Support Power BI Blog)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_vnet%20data%20gateway/)

---
## 作成する構成
---
VNet データ ゲートウェイを利用する構成について、以下の項目ごとにご説明します。
1. VNet / Private Endpoint を有効にした SQL Server の構築
2. Microsoft Fabric でVNet データ ゲートウェイを利用するための設定

</br>
<div align="center">
<img src="1_Configuration_image_per_phase.png">
</div>



---
## VNet/Private Endpoint を有効にした SQL Server の構築
---
以下の公開情報を参考に VNet および SQL Server を作成します。
なお、手順には Azure VM や Azure Bastion の作成が含まれていますが、今回は VM からの接続を行わないため、これらのリソースは作成しません。

>[!NOTE]
> 参考情報：[チュートリアル: Azure プライベート エンドポイントを使用して Azure SQL サーバーに接続する - Azure portal | Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/private-link/tutorial-private-endpoint-sql-portal)

上記の手順に従い、Azure SQL Server の作成が完了したら、[ネットワーク] タブで次の点を確認します。
- [パブリック アクセス] が「無効」になっていること
- [プライベート エンドポイント]が作成されていること


<div align="center">
<img src="2_Public_Access_Disabled.png">
</div>

</br>

<div align="center">
<img src="2_Private_Endpoint_Status.png">
</div>

[パブリック アクセス] が無効になっている場合、Microsoft Fabric のデータフロー Gen2 から SQL Server に対して VNet データ ゲートウェイを利用せずにアクセスを試みると、以下のようなエラーメッセージが表示され、接続できないことが確認できます。


<div align="center">
<img src="3_Connection_to_Vnet_failed.png">
</div>

</br>
エラーメッセージの機械翻訳

>SQL Server への接続を確立する際にインスタンス固有のエラーが発生しました。接続は「パブリックネットワークアクセスを拒否」が「はい」に設定されているため拒否されました。このサーバーに接続するには、仮想ネットワーク内からプライベートエンドポイントを使用してください 


このエラーメッセージからも分かるように、SQL Server への接続には仮想ネットワーク内からプライベートエンドポイントを経由して接続する必要があります。

現在の構成状況は以下のようなイメージです。

</br>
<div align="center">
<img src="3_Configuration_image_df2_Failed.png">
</div>



---
## Microsoft Fabric で VNet データ ゲートウェイを利用するための設定
---
これまでの手順で作成した VNet に、VNet データ ゲートウェイ用のサブネットおよび VNet データ ゲートウェイを作成します。
詳細な手順については、以下のブログを参考にしてください。

>[!NOTE]
> 参考情報：[仮想ネットワーク (VNet) データ ゲートウェイ について | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_vnet%20data%20gateway/#3-%E3%82%B5%E3%83%96%E3%83%8D%E3%83%83%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90%E3%80%81Microsoft-Power-Platform-%E3%81%AE%E9%96%A2%E9%80%A3%E4%BB%98%E3%81%91)

</br>
<div align="center">
<img src="3_Vnet_GW_Created.png">
</div>

</br>
Microsoft Fabric で VNet データ ゲートウェイの作成が完了したら、接続の作成を行います。

1. Microsoft Fabric で [設定（歯車アイコン）] > [接続とゲートウェイの管理] を選択します。
2. [接続] タブを開き、[+ 新規] > [仮想ネットワーク] を選択します。
3. 各項目を入力し、[作成] をクリックします。

これで、VNet データ ゲートウェイを使用した接続の作成が完了します。

</br>
<div align="center">
<img src="4_vnet_gw_connect_create.png">
</div>

</br>
[接続] の作成が完了した後は、データフロー Gen2 を使用して SQL Server にアクセスします。この際、VNet データ ゲートウェイを利用し、接続が正しく設定されていれば、SQL Server からデータを取得できることを確認できます。

これにより、仮想ネットワーク内でのセキュアなデータ接続が実現されていることを確認できます。

</br>
<div align="center">
<img src="5_Dataflow_SQLDB_VnetGW.png">
</div>

</br>
<div align="center">
<img src="5_vnet_gw_connect_get_data.png">
</div>

---
## おわりに
この記事では、VNet データ ゲートウェイを使用してプライベートなデータソースに接続する手順についてご説明しました。

今回ご案内した構成例はあくまで一例ですので、ご利用いただいているデータソースや想定している構成をもとに十分なご検証の上ご利用をご検討ください。
弊サポートは一問一答形式としており、コンサルティングに該当するご案内はサポート範囲外でございます。例えば以下のようなご質問には回答することができかねますのでご留意ください。

- データソースは ○○ を利用しているが、接続のための詳細な設定手順を教えてほしい。
- ×× の要件があるが、どういった構成であれば満たすことができるか。

しかし、ご検証いただくうえで、Power BI からデータソースに接続できないなどのトラブルシューティング観点ではご案内することが可能です。こういった観点で問題がございましたらお気兼ねなくお問い合わせください。

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)