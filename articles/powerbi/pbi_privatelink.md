---
title: Power BI Service へのアクセス制御② Azure Private Link
date: 2022-12-29 00:00:00 
tags:
  - Power BI　　
  - ダッシュボード
---

こんにちは、Power BI サポート チームの亀田です。
セキュリティの観点から、Power BI Service へのアクセスを制限したいというお問い合わせを受けることがあります。前回は「[条件付きアクセス](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_conditional-access/)」について説明しましたが、今回は  ｢Private Link｣ について説明します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
# 目次

* [Azure Private Link とは](#Azure-Private-Link-とは)
* [Azure Private Link の設定手順](#Azure-Private-Link-の設定手順)
	* [1.事前準備](#1.事前準備)
	* [2.Power BI のプライベート エンドポイントを有効にする](#2-Power-BI-のプライベート-エンドポイントを有効にする)
	* [3.Azure portal で Power BI リソースを作成する](##3.Azure-portal-で-Power-BI-リソースを作成する)
	* [4.仮想ネットワークを作成する](#4.仮想ネットワークを作成する)
	* [5.仮想マシン (VM) を作成する](#5.仮想マシン-(VM)-を作成する)	
	* [6.プライベート エンドポイントを作成する](#6.プライベート-エンドポイントを作成する)
	* [7.リモート デスクトップ (RDP) を使用して VM に接続する](#7.リモート-デスクトップ-(RDP)-を使用して-VM-に接続する)
	* [8.仮想マシンから Power BI にプライベート アクセスする](#8.仮想マシンから-Power-BI-にプライベート-アクセスする)
	* [9.Power BI のパブリック アクセスを無効にする](#9.Power-BI-のパブリック-アクセスを無効にする)

## Azure Private Link とは

Azure Private Linkは、 仮想ネットワーク内のプライベート エンドポイントを経由してAzureサービスやその他のサービスにアクセスする機能です。この仮想ネットワークとサービス間の通信では、Microsoftのネットワークが利用されるため、インターネットを経由するよりもセキュアな通信が可能です。
参考＃[Azure Private Link とは | Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/private-link/private-link-overview)

## Azure Private Link の設定手順

Power BI Service でAzure Private Linkを有効にし、パブリックネットワークからの通信を制限するためには、以下の設定を行います。

[1.事前準備](#1.事前準備)
[2.Power BI のプライベート エンドポイントを有効にする](#2-Power-BI-のプライベート-エンドポイントを有効にする)
[3.Azure portal で Power BI リソースを作成する](##3.Azure-portal-で-Power-BI-リソースを作成する)
[4.仮想ネットワークを作成する](#4.仮想ネットワークを作成する)
[5.仮想マシン (VM) を作成する](#5.仮想マシン-(VM)-を作成する)	
[6.プライベート エンドポイントを作成する](#6.プライベート-エンドポイントを作成する)
[7.リモート デスクトップ (RDP) を使用して VM に接続する](#7.リモート-デスクトップ-(RDP)-を使用して-VM-に接続する)
[8.仮想マシンから Power BI にプライベート アクセスする](#8.仮想マシンから-Power-BI-にプライベート-アクセスする)
[9.Power BI のパブリック アクセスを無効にする](#9.Power-BI-のパブリック-アクセスを無効にする)

それぞれの詳細な手順について、以下に説明します。なお、この設定はAzure Portalから構築するものが多くあり、Power BI管理者とは異なる権限が必要となりますのでご注意ください。
参考＃[Power BI にアクセスするためのプライベート エンドポイント - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-security-private-links)

### 1.事前準備

後の手順で利用するため、テナントIDと、Power BIで利用しているリージョン情報を取得します。
はじめにテナントIDを取得します。Azure Portalを開き、メニューから［Azure Active Directory］を選択します。
<div align="center">
<img src="privatelink01.png">
</div>  

表示されるテナントIDを控えます。
<div align="center">
<img src="privatelink02.png">
</div>

次にPower BIのリージョン情報を取得します。Power BI Service にアクセスし、［ヘルプとサポート］＞［Power BI について］を選択します。
<div align="center">
<img src="privatelink10.png">
</div>

［データの保存先］に記載されている情報を控えます。以下の画像では［東日本（東京、埼玉）］です。
<div align="center">
<img src="privatelink11.png">
</div>

テナントIDとリージョン情報が取得できたら、次の手順に進みます。

### 2.Power BI のプライベート エンドポイントを有効にする

Power BI Service の管理ポータルにアクセスし、[テナント設定］>［高度なネットワーク］＞［Azure Private Link］を有効化します。
<div align="center">
<img src="privatelink03.png">
</div>

［Azure Private Link］の設定を変更すると、テナント用に個別のFQDNを構成するなどで15分程度の時間がかかります。これ以降の手順でリソースを作成するのには影響しないので、次の手順に進みます。

### 3.Azure portal で Power BI リソースを作成する

次に、Azureテンプレートを使用してPower BI リソースグループを作成します。Azure Portalを開き、画面上部の検索欄に”テンプレート”と入力し、［サービス］にある［テンプレート］を選択します。
<div align="center">
<img src="privatelink04.png">
</div>

［テンプレートの作成］から新しくテンプレートを作成します。
<div align="center">
<img src="privatelink05.png">
</div>

［名前］と［説明］を入力し、［ARM テンプレート］を選択します。
<div align="center">
<img src="privatelink06.png">
</div>

ARMテンプレートでは以下のように入力します。マーカー部分の ”name” : ”resource-name" は適当に設定をし、 ”tenantId” : "tenant-object-id" は事前準備で控えたテナントIDを入力します。

```json
 {
   "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
   "contentVersion": "1.0.0.0",
   "parameters": {},
   "resources": [
       {
           "type":"Microsoft.PowerBI/privateLinkServicesForPowerBI",
           "apiVersion": "2020-06-01",
           "name" : "<resource-name>",
           "location": "global",
           "properties" : 
           {
                "tenantId": "<tenant-object-id>"
           }
       }
   ]
 }
```

<div align="center">
<img src="privatelink07.png">
</div>

テンプレートが作成できたら、［…］＞［デプロイ］を選択します。
<div align="center">
<img src="privatelink08.png">
</div>

［サブスクリプション］、［リソースグループ］は適当に選択をします。［場所］は事前準備で控えたリージョンと同じ場所を選択します。設定ができたら［上記の使用条件に同意する］にチェックを入れ［購入］を選択します。
<div align="center">
<img src="privatelink09.png">
</div>

デプロイが完了したら次の手順に進みます。

### 4.仮想ネットワークを作成する

次に、仮想ネットワークとサブネットを作成します。メニューから［仮想ネットワーク］を選択します。
<div align="center">
<img src="privatelink13.png">
</div>

［仮想ネットワークの作成］から新しく仮想ネットワークを作成します。
<div align="center">
<img src="privatelink14.png">
</div>

［地域］についてはリージョン情報と同じ場所を選択し、それ以外を適当に設定したら［次：セキュリティ＞］を選択します。
<div align="center">
<img src="privatelink15.png">
</div>

セキュリティについては今回は設定を変更せず［次：IPアドレス＞］を選択します。
<div align="center">
<img src="privatelink16.png">
</div>

［IPアドレス］は設定されている内容に問題がなければ特に変更せず［確認＋作成］を選択します。
<div align="center">
<img src="privatelink17.png">
</div>

確認し、［作成］を選択します。
<div align="center">
<img src="privatelink18.png">
</div>

デプロイが完了したら、次の手順に進みます。

### 5.仮想マシン (VM) を作成する

次に仮想マシンを作成します。メニューから［Virtual Machines］を選択します。
<div align="center">
<img src="privatelink20.png">
</div>

［作成］から新しいVMを作成します。
<div align="center">
<img src="privatelink21.png">
</div>

［地域］についてはリージョン情報と同じ場所を選択し、それ以外を適当に設定したら［次：ディスク＞］を選択します。
<div align="center">
<img src="privatelink22.png">
</div>
<div align="center">
<img src="privatelink23.png">
</div>

今回は特に変更せず［次：ネットワーク＞］を選択します。
<div align="center">
<img src="privatelink24.png">
</div>

［仮想ネットワーク］、［サブネット］が手順4で作成したものに設定されていることを確認し、［確認および作成］を選択します。
<div align="center">
<img src="privatelink25.png">
</div>

［作成］を選択します。
<div align="center">
<img src="privatelink26.png">
</div>

デプロイが完了したら次の手順に進みます。

### 6.プライベート エンドポイントを作成する

次の手順では、Power BI のプライベート エンドポイントを作成します。メニューから［リソースの作成］を選択します。
<div align="center">
<img src="privatelink28.png">
</div>

検索欄に”private link”と入力し、Enterキーを押します。
<div align="center">
<img src="privatelink29.png">
</div>

［Private Link］の［作成］＞［Private Link］を選択します。
<div align="center">
<img src="privatelink30.png">
</div>

［Private Link センター］が開けたら、［プライベート エンドポイントの作成］を選択します。
<div align="center">
<img src="privatelink31.png">
</div>

［地域］についてはリージョン情報と同じ場所を選択し、それ以外を適当に設定したら［次：リソース＞］を選択します。
<div align="center">
<img src="privatelink32.png">
</div>

［リソースの種類］は［Microsoft.PowerBI/privateLinkServicesForPowerBI］を選択します。［リソース］は手順3で作成したリソースを選択し、［対象サブリソース］は［tenant］を選択します。［次：仮想ネットワーク＞］を選択します。
<div align="center">
<img src="privatelink33.png">
</div>

［仮想ネットワーク］［サブネット］が、手順4で作成されたものに設定されていることを確認し、［次：DNS＞］を選択します。
<div align="center">
<img src="privatelink34.png">
</div>

今回は特に設定を変更せず、［次：タグ＞］を選択します。
<div align="center">
<img src="privatelink35.png">
</div>

タグは必要に応じて設定し、［次：確認および作成＞］を選択します。
<div align="center">
<img src="privatelink44.png">
</div>

［作成］を選択します。
<div align="center">
<img src="privatelink36.png">
</div>

デプロイが完了したら次の手順に進みます。

### 7．リモート デスクトップ (RDP) を使用して VM に接続する

Power BI にプライベートアクセスするため、手順5で作成したVMに接続します。ホームに戻り、手順5で作成したVMを選択します。
<div align="center">
<img src="privatelink38.png">
</div>

［接続］＞［RDP］を選択します。
<div align="center">
<img src="privatelink39.png">
</div>

［RDPファイルのダウンロード］を選択します。
<div align="center">
<img src="privatelink40.png">
</div>

ダウンロードされたRDPファイルをダブルクリックします。［Connect］を選択します。
<div align="center">
<img src="privatelink45.png">
</div>

認証情報を求められるため、［More choices］＞［Use a different account］を選択し、VMを作成するときに設定したアカウント名とパスワードを入力し［OK］を選択します。
<div align="center">
<img src="privatelink46.png">
</div>

接続ができたら次の手順に進みます。

### 8.VMから Power BI にプライベート アクセスする

VMに接続できたら、PowerShellを開き、以下のコマンドを入力します。［tenant-object-id-without-hyphens］は、事前準備で取得したテナントIDから、ハイフンを抜き入力します。例えば、テナントIDが”AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE”の場合に入力するコマンドは”nslookup AAAAAAAABBBBCCCCDDDDEEEEEEEEEEEE-api.privatelink.analysis.windows.net"となります。

``` ps
nslookup [tenant-object-id-without-hyphens]-api.privatelink.analysis.windows.net
```

入力すると以下のような応答があり、プライベートIPで名前解決されていることが確認できます。
<div align="center">
<img src="privatelink41.png">
</div>

### 9.Power BI のパブリック アクセスを無効にする

最後に、Power BIのパブリックアクセスを無効にします。Power BI Service の管理ポータルにアクセスし、[テナント設定］>［高度なネットワーク］＞［パブリック インターネット アクセスのブロック］を有効化します。
<div align="center">
<img src="privatelink42.png">
</div>

有効化には10～20分程度かかります。しばらく時間をおいて、外部ネットワークからPower BIにアクセスしようとすると、以下のようなメッセージが表示され、アクセスできないことが確認できます。
<div align="center">
<img src="privatelink43.png">
</div>

以上で設定は完了となります。プライベート エンドポイントを利用する際には、いくつかの制限事項がございます。公開情報にてご案内しておりますのでご確認いただけますと幸いでございます。
参考＃ [Power BI にアクセスするためのプライベート エンドポイント - 考慮事項と制限事項](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-security-private-links#considerations-and-limitations)



以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
