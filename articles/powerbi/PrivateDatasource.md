---
title: Private なデータソースへ接続する
date: 2024-03-29 00:00:00 
tags:
  - Power BI
  - オンプレミス データ ゲートウェイ
  - On-Premises Data Gateway
  - セマンティック モデル
---

# Private なデータソースへ接続する

こんにちは、Power BI サポート チームの亀田です。

Power BI では様々なデータソースに接続し、レポートを作成することが可能です。インターネット経由でアクセスできるデータソースであれば、Power BI Service から資格情報を設定することですぐに接続することが可能です。しかし、必ずしもインターネット経由でアクセスすることができるデータソースのみを利用されていることはなく、例えば社内イントラネットなど、Private な環境からのアクセスのみに制限している場合もあるかと思います。サポートチームにも、このようなデータソースを利用するにはどうすればよいかというお問い合わせをいただくことがあります。

今回は例として、Private Endpoint を有効にした SQL Server に接続するためにはどのような構成となるかをご案内します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 目次

* [はじめに](#はじめに)
* [構成および設定](#構成および設定)
	* [VNet / Azure VM / Private Endpoint を有効にした SQL Server の構築](#VNet-Azure-VM-Private-Endpoint-を有効にした-SQL-Server-の構築)
	* [Power BI でゲートウェイを利用するための設定](#Power-BI-でゲートウェイを利用するための設定)
        * [1 ゲートウェイの構成](#1-ゲートウェイの構成)
        * [2 Power BI Service での設定](#2-Power-BI-Service-での設定)
        * [3 セマンティック モデルでの接続の割り当て](#3-セマンティック-モデルでの接続の割り当て)
* [おわりに](#おわりに)

## はじめに

今回は Private Endpoint を有効にした SQL Server を例に接続例をご紹介します。具体的なイメージは以下のとおりです。

<div align="center">
<img src="PrivateDatasource01.png">
</div>  

ユーザーはインターネットを経由して Power BI にアクセスすることはできますが、  SQL Server へはパブリックアクセスが禁止されているためアクセスすることができません。Power BI も同様に SQL Server に直接アクセスすることができません。そのため、Vnet (仮想ネットワーク) 内に構築された Azure VM (仮想マシン) 内にインストールされたオンプレミス データ ゲートウェイを経由して SQL Server にアクセスする構成とします。

Private Endpoint については以下の公開情報をご参照ください。

> [!NOTE]
> [プライベート エンドポイントとは - Azure Private Link | Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/private-link/private-endpoint-overview)

Private Endpoint への接続に限らず、インターネット経由でアクセスできないデータソースへの接続へはゲートウェイを利用する必要があります。

> [!NOTE]
> [Power BI サービスのデータセット更新手順について | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_refresh_settings/)
参考# [オンプレミス データ ゲートウェイとは | Microsoft Learn](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-onprem)

また、マシンにインストールする必要がなく、データソースの接続に利用できるリソースとして VNet データ ゲートウェイもございます。こちらは 2024年2月に一般公開となりましたが、 Premium 容量または Fabric 容量で利用できるリソースとなりますので、これらの容量をご契約いただいていない場合には オンプレミス データ ゲートウェイをご利用ください。

> [!NOTE]
> [VNet Data Gateway for Fabric and Power BI is now Generally Available | Microsoft Power BI Blog | Microsoft Power BI](https://powerbi.microsoft.com/en-au/blog/vnet-data-gateway-for-fabric-and-power-bi-is-now-generally-available/)
> [仮想ネットワーク (VNet) データ ゲートウェイとは | Microsoft Learn](https://learn.microsoft.com/ja-jp/data-integration/vnet/overview)

上記構成の場合、 Power BI から VNet 内の Azure VM へは Microsoft のネットワークを利用して通信が行われるため、インターネットを経由しない通信となります。また、Azure VM から SQL Server へは VNet を経由するプライベートな通信となるため、 Power BI から SQL Server へはインターネットを経由しないプライベートな通信となります。

## 構成および設定

今回は、オンプレミス データ ゲートウェイを利用する構成について、以下の項目ごとにご説明します。

1. VNet / Azure VM / Private Endpoint を有効にした SQL Server の構築 
2. Power BI でゲートウェイを利用するための設定

<div align="center">
<img src="PrivateDatasource02.png">
</div>

### VNet / Azure VM / Private Endpoint を有効にした SQL Server の構築 

以下の公開情報を参考にし、VNet / Azure VM / SQL Server を作成します。

> [!NOTE]
> [チュートリアル: Azure プライベート エンドポイントを使用して Azure SQL サーバーに接続する - Azure portal | Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/private-link/tutorial-private-endpoint-sql-portal)

SQL Server の [ネットワーク] から、[パブリック アクセス] が無効になっていることを確認します。

正しく設定が行えていれば、インターネットからアクセスしようとする場合には以下のメッセージが表示され SQL Server へのアクセスができません。

> Connect to Server
> ------------------------------
>
> Cannot connect to private-sqldb.database.windows.net.
>
> ------------------------------
> ADDITIONAL INFORMATION:
>
> Reason: An instance-specific error occurred while establishing a connection to SQL Server. Connection was denied since Deny Public Network Access is set to Yes (https://docs.microsoft.com/azure/azure-sql/database/connectivity-settings#deny-public-network-access). To connect to this server, use the Private Endpoint from inside your virtual network (https://docs.microsoft.com/azure/sql-database/sql-database-private-endpoint-overview#how-to-set-up-private-link-for-azure-sql-database). (Microsoft SQL Server, Error: 47073)
>
> For help, click: https://docs.microsoft.com/sql/relational-databases/errors-events/mssqlserver-47073-database-engine-error
>

<div align="center">
<img src="PrivateDatasource03.png">
</div>  

一方、 VNet 内に作成された VM からは正常にアクセスすることが可能です。

<div align="center">
<img src="PrivateDatasource04.png">
</div>  

### Power BI でゲートウェイを利用するための設定

#### 1. ゲートウェイの構成

接続が確認できたら、 Power BI から接続するためのゲートウェイを構築します。ゲートウェイのインストーラーは [Power BI ゲートウェイ | Microsoft Power BI](https://powerbi.microsoft.com/ja-jp/gateway/) からダウンロードが可能です。標準版のゲートウェイをダウンロードし、インストールを行ってください。

> [!NOTE]
> [オンプレミス データ ゲートウェイをインストールする | Microsoft Learn](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-install)

<div align="center">
<img src="PrivateDatasource05.png">
</div>  

インストールが完了したら、サインインを行い、ゲートウェイ名と回復キーを設定し構成します。

<div align="center">
<img src="PrivateDatasource07.png">
</div> 

#### 2. Power BI Service での設定

ゲートウェイのインストールが完了したら、Power BI Service 上で、[設定] > [接続とゲートウェイの管理] を選択します。

正しく構成されていれば、構成時に入力したゲートウェイがあることが確認できます。

<div align="center">
<img src="PrivateDatasource08.png">
</div>  

次に、[接続] タブを開き、[+ 新規] を選択します。

<div align="center">
<img src="PrivateDatasource09.png">
</div>  

新しい接続の作成から、以下の通り設定します。

> ゲートウェイ クラスター名 : <構成したゲートウェイ名> (例: private-sqldb-gw)
> 接続名 : 適当な名前を設定
> 接続の種類 : SQL Server
> サーバー : <SQL Server のサーバー名> (例: private-sqldb.database.windows.net)
> データベース : <接続したいデータベース名> (例: private-sqldb)
> 認証 : 認証方式に応じて設定

<div align="center">
<img src="PrivateDatasource10.png">
</div>  

入力したら、 [作成] を押下すると、入力した資格情報で接続テストが行われ、接続ができれば [<接続名> が作成済み。] と表示され、接続が作成されます。

<div align="center">
<img src="PrivateDatasource11.png">
</div>  

#### 3. セマンティック モデルでの接続の割り当て

このデータソースを利用しているセマンティック モデルに接続を割り当てます。

セマンティック モデルの [設定] > [ゲートウェイとクラウド接続] を選択し、[オンプレミスまたは VNet データ ゲートウェイを使用する] がオンになっていることを確認します。

作成したゲートウェイを選択し、[このセマンティック モデルに含まれるデータ ソース] から、[マップ先] で先程手順2で作成した接続を設定し、[適用] を押下します。

<div align="center">
<img src="PrivateDatasource12.png">
</div>  

接続の割り当てが完了したら、セマンティック モデルが更新できることを確認します。

## おわりに

今回ご案内した構成例はあくまで一例ですので、ご利用いただいているデータソースや想定している構成をもとに十分なご検証の上ご利用をご検討ください。

弊サポートは一問一答形式としており、コンサルティングに該当するご案内はサポート範囲外でございます。例えば以下のようなご質問には回答することができかねますのでご留意ください。 

* データソースは ○○ を利用しているが、接続のための詳細な設定手順を教えてほしい。
* ×× の要件があるが、どういった構成であれば満たすことができるか。

しかし、ご検証いただくうえで、Power BI からデータソースに接続できないなどのトラブルシューティング観点ではご案内することが可能です。こういった観点で問題がございましたらお気兼ねなくお問い合わせください。

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。
