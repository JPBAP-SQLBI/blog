---
title: Power BI Service へのアクセス制御① 条件付きアクセス
date: 2022-11-30 00:00:00 
tags:
  - Power BI　　
  - アクセス制御
  - 条件付きアクセス
  - Conditional Access
---

こんにちは、Power BI サポート チームの亀田です。
セキュリティの観点から、Power BI Service へのアクセスを制限したいというお問い合わせを受けることがあります。今回はアクセス制御を行う方法の1つである  ｢条件付きアクセス｣ について説明します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [条件付きアクセスとは](#条件付きアクセスとは)
* [条件付きアクセスの設定](#条件付きアクセスの設定)
* [設定手順](#設定手順)
	[1.アクセスを許可するIPアドレスの登録](#1-アクセスを許可するIPアドレスの登録)
	[2.条件付きアクセスのポリシーの作成](#2-条件付きアクセスのポリシーの作成)

---
## 条件付きアクセスとは
---
条件付きアクセスは、 Azure Active Directory (以降AAD) で設定できる機能となります。条件付きアクセスを設定することで、ユーザーのIPアドレスやデバイス、アプリケーションを条件としてアクセスを制御することが可能となります。なお、設定にはAAD Premium P1ライセンスが必要となりますこと、ご留意ください。

参考# [Azure Active Directory の条件付きアクセスとは - Microsoft Entra | Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/active-directory/conditional-access/overview)

---
## 条件付きアクセスの設定
---
Power BI Service へのアクセスを制限するためには、以下のポリシーを設定します。

* Power BI Service へのアクセスをブロック
* 特定のIPアドレスからのアクセスを例外として許可

このように設定することで、例えば社内ネットワーク内からのみ Power BI Service にアクセスさせることが可能になります。

---
## 設定手順
---
条件付きアクセスの設定は、次のような手順となります。

1. アクセスを許可するIPアドレスの登録
2. 条件付きアクセスのポリシーの作成

それぞれの詳細な手順について、以下に説明します。なお、この設定はAzure Portal上での設定となり、Power BI管理者とは異なる権限が必要となりますのでご注意ください。

参考# [条件付きアクセス - 場所ごとにアクセスをブロックする - Azure Active Directory - Microsoft Entra | Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/active-directory/conditional-access/howto-conditional-access-policy-location)

---
### 1.アクセスを許可するIPアドレスの登録
---
まずはじめに、[Azure Portal] にアクセスし、[Azure Active Directory] > [セキュリティ] をクリックします。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig01.png">
</div>  

このあとの条件付きアクセスの設定で利用するため、[ネームド ロケーション] > [IP 範囲の場所] を選択し、IPアドレスを登録します。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig02.png">
</div>  

IPアドレスが登録できたら、次に案内する手順で条件付きアクセス ポリシーを作成します。

---
### 2.条件付きアクセスのポリシーの作成
---
[条件付きアクセス] をクリックします。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig03.png">
</div>  

[新しいポリシー] をクリックします。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig04.png">
</div>  

名前を入力し、[ユーザーまたはワークロード] で対象を選択します。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig05.png">
</div>  

今回は、Power BI Service を対象にアクセスを制御したいため、[クラウド アプリまたは操作] > [対象] > [アプリを選択] > [選択] の [なし] をクリックし、[Power BI Service] にチェックをいれ [選択] をクリックします。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig06.png">
</div>  

[条件] > [場所] > [構成] の [はい] を選択します。[対象外] > [選択された場所] > [なし] をクリックすると、右側にネームド ロケーションを選択する欄が表示されます。手順1で作成したIPアドレスのネームド ロケーションを選択し、[選択] をクリックします。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig07.png">
</div>  

[アクセス制御] > [許可] で、[アクセスのブロック] を選択し、[選択] をクリックします。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig08.png">
</div>  

最後に、[ポリシーの有効化] を”オン”にすることで、このポリシーが適用されます。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig09.png">
</div>  

上記設定後、設定したIPアドレス外からアクセスをすると以下のようにPower BI Serviceにアクセスすることができなくなります。
<div align="center">
<img src="2022-11_アクセス制御-条件付きアクセス_fig10.png">
</div>  



以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)