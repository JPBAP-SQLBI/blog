---
title: 仮想ネットワーク (VNet) データ ゲートウェイ について
date: 2024-09-30 00:00:00 
tags:
  - Power BI
  - Microsoft Fabric
  - Power BI サービス
  - 仮想ネットワーク (VNet) データゲートウェイ
  - VNet データゲートウェイ
  - virtual network (VNet) data gateway
  - VNet data gateway

---

こんにちは、Power BI サポート チームの中川です。

仮想ネットワーク (VNet) データゲートウェイ（以降、VNet データゲートウェイと呼称）を利用することで、オンプレミスデータゲートウェイを必要とせず、Microsoft Fabricから直接 Azure の仮想ネットワーク内のデータソースに対してセキュアな通信が可能となります。

本ブログでは、 VNet データゲートウェイの概要および前提条件、作成手順についてご紹介します。


<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [仮想ネットワーク (VNet) データ ゲートウェイとは](#仮想ネットワーク-%28VNet%29-データ-ゲートウェイとは)
* [前提条件と制限事項](#前提条件と制限事項)
* [作成手順](#作成手順)
* [おわりに](#おわりに)


---
## 仮想ネットワーク (VNet) データ ゲートウェイとは
---

Power BI とデータソースをセキュアに接続するための標準的な方法として、オンプレミスデータゲートウェイが用いられていました。しかし、オンプレミス データ ゲートウェイはオンプレミスまたは VM へのインストールが必要となり、月次の更新や監視などの運用負担がかかる課題がありました。

VNet データゲートウェイは、仮想マシンへのインストールやハードウェア管理を不要にし、運用負担の大幅な軽減が期待できます。

VNet データゲートウェイを使用すると、Azure やその他のデータサービスと Microsoft Fabric に接続をすることが可能となります。
また、すべてのトラフィックは インターネットを介さずに Azure バックボーンを使用するため、安全に通信が行われます。


<div align="center">
<img src="vnet-overview.png">
</div>


---
## 前提条件と制限事項
---
VNet データゲートウェイではいくつかの前提条件や制限事項がございます。


### 利用可能なアイテム
- Fabric Dataflow Gen2
- Power BI セマンティック モデル
- Power Platform データフロー
- Power BI 改ページ対応レポート

※ データフロー（Gen1）とデータマートはサポートされていません。


### 利用可能なSKU
- Power BI Premium 容量（P SKU）
- Microsoft Fabric 容量（F SKU）
- Power BI Embedded （A4～A7 SKU）

なお、F2 SKU でもご利用いただけますが、ゲートウェイ メンバーあたりの消費ユニット (CU) 消費レートは 1 時間あたり 4 CU であるため、複数のゲートウェイを同時に実行することはできません。
そのため、複数のゲートウェイを十分に機能させるには、F8 SKU 以上を推奨しております。

### サポートされるデータソース
Azure 内でのプライベートリソースへの接続と、Azure 外部およびパブリックリソースでサポートされるデータソースが異なります。
サポートされるデータソースについては以下のリンクをご参照ください。

>[!NOTE]
> 参考情報：[サポートされている Azure データ サービス - Power BI の Virtual Network データ ゲートウェイとデータ ソースを使用する | Microsoft Learn)](https://learn.microsoft.com/ja-jp/data-integration/vnet/use-data-gateways-sources-power-bi#supported-azure-data-services)



補足として、Power Platform データフローは、Power BIと同様のデータソースに対応しています。ページ分割されたレポートでサポートされるデータソースについては以下のリンクをご参照ください。

>[!NOTE]
> 参考情報：[Power BI のページ分割されたレポートでサポートされるデータ ソース - Power BI | Microsoft Learn)](https://learn.microsoft.com/ja-jp/power-bi/paginated-reports/paginated-reports-data-sources)

### 利用可能なリージョン
VNet データゲートウェイの利用可能なリージョンについては、次の制限があります。
- VNet データゲートウェイは、Power BI のホームリージョンに作成が必要です。
- 仮想ネットワーク（VNet）は、サポートされるリージョンである必要があります。
- テナント間のシナリオはサポートされていません。

>[!NOTE]
> 参考情報：[VNet データ ゲートウェイでサポートされるリージョン - 仮想ネットワーク (VNet) データ ゲートウェイの作成 | Microsoft Learn)](https://learn.microsoft.com/ja-jp/data-integration/vnet/create-data-gateways#regions-supported-for-vnet-data-gateways)


なお、VNet とサブネットは任意のリージョンを選択できます。
例えば、以下の構成の場合、
- テナントのホームリージョン: 東日本 (Japan East)
- VNet のリージョン: 米国東部 (East US)

実際のデータ（クエリ結果やデータ）は選択したリージョン内（East US）のサブネットで処理され、メタデータはホームリージョン（Japan East）に送信されます。


### その他の制限事項
上記以外にも制限事項などがございますので、詳細については、以下のリンクをご参照ください。

>[!NOTE]
> 参考情報：[制限事項 - 仮想ネットワーク (VNet) データ ゲートウェイとは | Microsoft Learn)](https://learn.microsoft.com/ja-jp/data-integration/vnet/overview#limitations)
> 参考情報：[仮想ネットワーク データ ゲートウェイに関する FAQ | Microsoft Learn)](https://learn.microsoft.com/ja-jp/data-integration/vnet/data-gateway-faqs)




---
## 作成手順
---
今回は、仮想ネットワーク（VNet）の作成から、VNet データゲートウェイの作成までの手順を説明します。

### 1. 前準備：リソースプロバイダーに Microsoft.PowerPlatform を登録する
Azure ポータルにログインし、以下の手順で登録を行います。
- ご利用のサブスクリプション -> リソースプロバイダー へ移動
- 「Microsoft.PowerPlatform」を検索して選択
- [登録] を選択して有効化します。

<div align="center">
<img src="resource provider.png">
</div>

### 2. 仮想ネットワーク（Vnet）の作成
Azure ポータルにて、[仮想ネットワーク]を選択し、必要な設定を入力し、仮想ネットワークを作成します。

<div align="center">
<img src="vnet_create.png">
</div>

### 3. サブネットの作成、Microsoft Power Platform の関連付け
仮想ネットワーク画面にて、[サブネットの追加] を選択し、サブネット名や IP アドレス範囲を入力します。

**注意点：**
以下の点に注意してサブネットを作成します。
- サブネット名には "gatewaysubnet" または "AzureBastionSubnet" を使用しない。
- IPV6 アドレススペースがサブネットに追加されていない。
- サブネットの IP 範囲が他の範囲 (例: 10.0.1.x) と重複しない。

<div align="center">
<img src="subnet_1.png">
</div>


サブネットの追加画面にて、[サブネットをサービスに委任]で、[Microsoft.PowerPlatform/vnetaccesslinks] を選択します。  
なお、この操作にはネットワーク共同作成者ロール または、VNet に対する Microsoft.Network/virtualNetworks/subnets/join/action の権限が必要です。

<div align="center">
<img src="subnet_2.png">
</div>


### 4. VNet データゲートウェイを作成する
仮想ネットワークおよびサブネットが作成できたら、次の手順で VNet データゲートウェイを作成します。

- Power BI サービスにアクセスします。
- 右上の設定（歯車アイコン）をクリックし、[接続とゲートウェイの管理] を選択します。
- [仮想ネットワークデータゲートウェイ] -> [新規] をクリックし、新しいゲートウェイ接続を作成します。

なお、このアクションの実行には、サブスクリプションの Azure ネットワーク共同作成者ロールが必要です。

<div align="center">
<img src="vnetgw-create.png">
</div>

作成した VNet データゲートウェイが Power BI サービスに反映されていることを確認します。  

<div align="center">
<img src="vnetgw_result.png">
</div>


その後、セマンティックモデルの設定画面にて "ゲートウェイ接続" を確認し、作成した VNet データゲートウェイをデータソースに紐付けます。


---
## おわりに
この記事では、仮想ネットワーク (VNet) データゲートウェイの概要と、作成手順についてご説明しました。

VNet データゲートウェイを使用することで、オンプレミスデータゲートウェイを必要とせず、Azure の仮想ネットワーク内のデータソースに対して安全な通信を実現できる利点があります。また、ハードウェア管理の負担を軽減し、セキュリティを強化することが可能ですので、ぜひご利用をご検討いただければと思います。

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。



---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)