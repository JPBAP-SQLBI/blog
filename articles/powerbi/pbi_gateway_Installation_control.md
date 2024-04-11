---
title: Power Platform管理センターからオンプレミス データ ゲートウェイのインストールの制御方法
date: 2023-01-31 00:00:00 
tags:
  - Power BI
  - オンプレミスデータゲートウェイ
  - Admin
---


こんにちは、Power BI サポート チームのファムです。

本ブログでは、Power Platform管理センターから組織内のユーザーに対してオンプレミス データ ゲートウェイのインストールを制御する手順をご紹介します。

<!-- more -->

> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。
</br>

---
## 目次
---
1. [オンプレミス データ ゲートウェイとは](#オンプレミス-データ-ゲートウェイとは)
2. [Power Platform 管理センターからオンプレミス データ ゲートウェイのインストールの制御手順](#Power-Platform-管理センターからオンプレミス-データ-ゲートウェイのインストールの制御手順)
3. [オンプレミス データ ゲートウェイをインストールできるユーザーの場合の挙動](#オンプレミス-データ-ゲートウェイをインストールできるユーザーの場合の挙動)
4. [オンプレミス データ ゲートウェイをインストールできないユーザーの場合の挙動](#オンプレミス-データ-ゲートウェイをインストールできないユーザーの場合の挙動)
5. [オンプレミス データ ゲートウェイ (個人用モード)のインストール制御について](#オンプレミス-データ-ゲートウェイ-個人用モード-のインストール制御について)
</br>

---
## オンプレミス データ ゲートウェイとは
---
Power BI サービス上のレポートを最新データに更新するためには、データセットとデータソースを接続する必要がありますが、データソースがオンプレミス環境にある場合は、オンプレミス データゲートウェイが必要です。

オンプレミス データ ゲートウェイとは、オンプレミス環境のデータとPower BIサービス間においてセキュリティで保護されたデータ転送を行うための「ブリッジ」です。オンプレミス データ ゲートウェイのイメージは、以下のPower BI構成の概要図をご参考ください。

<div align="center">
<img src="image1.png">
</div>

 **参考情報：**
 [オンプレミス ゲートウェイについて](https://learn.microsoft.com/ja-jp/power-platform/admin/wp-onpremises-gateway)


---
## Power Platform 管理センターからオンプレミス データ ゲートウェイのインストールの制御手順
---

[Microsoft Power Platform 管理センター](https://admin.powerplatform.microsoft.com/)にサインインします。「**データ（プレビュー）**」  ＞ 「**オンプレミス データ ゲートウェイ**」　＞　「**ゲートウェイのテナント管理**」にオンを設定し、　「**ゲートウェイのインストール担当者の管理**」をクリックします。

<div align="center">
<img src="image2.png">
</div>

**・ユーザーを追加する場合**
「**ゲートウェイのインストール担当者の管理**」画面から、ゲートウェイをインストールさせたいユーザーを追加します。追加されているユーザーは、「**現在のゲートウェイ インストーラー**」の一覧から確認できます。こちらの一覧に表示されているユーザーは、ゲートウェイをインストール可能であり、この一覧に表示されていないユーザーはゲートウェイをインストールできないようになります。
</br>

<div align="center">
<img src="image3.png">
</div>


**・ユーザーを削除する場合**
追加したユーザーに対して、オンプレミス データ ゲートウェイをインストールさせたくない場合は、「**現在のゲートウェイ インストーラー**」の一覧から「**×**」をクリックし、削除します。

<div align="center">
<img src="image4.png">
</div>


---
## オンプレミス データ ゲートウェイをインストールできるユーザーの場合の挙動
---

オンプレミス データ ゲートウェイをインストールできるユーザーは、オンプレミス データ ゲートウェイからサインインを試みると、以下のように正常にサインインできます。また、構成しているゲートウェイをご確認できます。

<div align="center">
<img src="image5.png">
</div>

---
## オンプレミス データ ゲートウェイをインストールできないユーザーの場合の挙動
---

オンプレミス データ ゲートウェイをインストールできないユーザーは、オンプレミス データ ゲートウェイからサインインを試みると、エラーメッセージ「**インストールに失敗しました。オンプレミス データ ゲートウェイをインストールできるユーザーが組織により制限されています。サービス管理者またはテナント管理者にお問い合わせください。**」が表示されます。
こちらのエラーメッセージが表示されるユーザーが、オンプレミス データ ゲートウェイをインストールできるようにしたい場合は、管理者ロールのユーザーからPower Platform管理センターでゲートウェイのインストール担当者として追加してもらう必要があります。

<div align="center">
<img src="image6.png">
</div>
<div align="center">
<img src="image7.png">
</div>

</br>

---
## オンプレミス データ ゲートウェイ (個人用モード) のインストール制御について
---

オンプレミス データ ゲートウェイには、Power BI でのみ機能するオンプレミス データ ゲートウェイ (個人用モード) (以下、個人用ゲートウェイと表記します) という異なる種類のゲートウェイがあります。
名前の通り自分専用のゲートウェイとして、ローカルコンピューターに配置し、ローカルのデータソースとの接続・データセットの更新に使用されるゲートウェイです。

> [参考情報]
> [Power BI で個人用ゲートウェイを使用する](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-gateway-personal-mode)

</br>

Power Platform 管理センターや Power BI サービスの [接続とゲートウェイの管理] 画面からは、個人用ゲートウェイのインストール制御は行なえません。
しかし、テナント内すべてのゲートウェイに対して管理コマンドの実行が可能な**オンプレミス データ ゲートウェイ管理用の PowerShell コマンドレット**を使用することで、個人用ゲートウェイに対してもインストールの制御・ユーザーの追加などが可能になります。

このセクションでは、個人用ゲートウェイのインストールを制御し、特定のユーザーのみにインストール権限を付与する手順について説明いたします。

> [!TIP]
> ・ オンプレミス データ ゲートウェイ管理用の PowerShell コマンドレットは、パブリックプレビューの機能となります。
> ・ また、オンプレミス データ ゲートウェイ管理用の PowerShell コマンドレットでインストール制御を行なうためには、テナント管理者 (Power BI 管理者またはPower Platform 管理者、グローバル管理者) 権限を持っている必要があります。

</br>

### 個人用ゲートウェイの制御手順

#### 1. オンプレミス データ ゲートウェイ管理用の PowerShell コマンドレットをインストール

```ps
Install-Module -Name DataGateway
```

> [!TIP]
> `DataGateway` コマンドレットを使用するためには、Windows OS 標準の Windows PowerShell とは別に Powershell 6.2.2 以降のバージョンが必要です。
> PowerShell は以下 Github からダウンロード可能です。
> [Github - PowerShell](https://github.com/PowerShell/PowerShell)

</br>

#### 2. テナント管理者のアカウントでデータ ゲートウェイ サービスに接続

ブラウザで認証画面が表示されますので、テナント管理者のアカウントで接続をお試しください。

```ps
Connect-DataGatewayServiceAccount
```

</br>

#### 3. テナントのゲートウェイインストールの制御状態を確認

```ps
Get-DataGatewayTenantPolicy
```

通常のオンプレミス データ ゲートウェイのみがインストール制御されている場合、`Policy` が `EnterpriseInstallRestricted` という状態である結果が得られます。

```ps
#実行結果
TenantObjectId                                            Policy
--------------                                            ------
12345678-xxxx-xxxx-xxxx-8ce9ff2d5099 EnterpriseInstallRestricted
```

</br>

#### 4. 個人用ゲートウェイのインストール制御を追加

ゲートウェイのインストールポリシーを設定する `Set-DataGatewayTenantPolicy` コマンドを実行します。

```ps
Set-DataGatewayTenantPolicy -PersonalGatewayInstallPolicy Restricted
Get-DataGatewayTenantPolicy
```

`Policy` に `PersonalInstallRestricted` が追加され、個人用ゲートウェイのインストールも制御された状態となりました。

```ps
#実行結果
TenantObjectId                                                                       Policy
--------------                                                                       ------
12345678-xxxx-xxxx-xxxx-8ce9ff2d5099 PersonalInstallRestricted, EnterpriseInstallRestricted
```

</br>

実際に、個人用ゲートウェイをインストールしようとすると以下の画面のように、インストールが制限されている旨が表示されます。

<div align="center">
<img src="image8.png">
</div>

</br>

#### 5. ユーザーごとに制御

一部のユーザーにのみインストールを許可させたい場合、続けて本手順も実施します。
まずは許可させたいユーザーの `ObjectId` を取得します。
`ObjectId` は Azure Active Directry のユーザー情報から確認できる他、Az PowerShell モジュールの `Get-AzADUser` コマンドで取得することも可能です。

> [!TIP]
> Az PowerShell モジュールの詳細については以下公開情報をご覧ください。
> [Azure Az PowerShell モジュールをインストールする](https://learn.microsoft.com/ja-jp/powershell/azure/install-az-ps)

</br>

```ps
Connect-AzAccount
$user1 = $(Get-AzADUser -ObjectId "user1@contoso.onmicrosoft.com").Id
```

</br>

<div align="center">
<img src="image9.png">
</div>

</br>

取得した `ObjectId` を `Set-DataGatewayInstaller` コマンドでインストールを許可するユーザーとして追加します。
このとき `GatewayType` パラメーターを `Personal` とすることで、個人用ゲートウェイを対象にすることができます。

```ps
Set-DataGatewayInstaller -PrincipalObjectIds $user1 -Operation Add -GatewayType Personal
Get-DatagatewayInstaller
```

以下のように、`ObjectId` に対して `Personal` の `GatewayType` が付与されていれば、許可された状態となります。
```ps
#実行結果
PrincipalObjectId                    GatewayType
-----------------                    -----------
12345678-xxxx-xxxx-xxxx-571d358d8e63 Personal
```

</br>

> [参考情報]
> [オンプレミス データ ゲートウェイ管理用の PowerShell コマンドレット (パブリック プレビュー)](https://learn.microsoft.com/ja-jp/powershell/gateway/overview?view=datagateway-ps)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)