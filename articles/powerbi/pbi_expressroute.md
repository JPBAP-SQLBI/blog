---
title: Power BI で ExpressRoute の使用について
date: 2023-03-31 16:00:00 
tags:
  - Power BI　　
  - Express Route
  - 通信
---

こんにちは、Power BI サポート チームのチャンです。
オンプレミス環境と Microsoft クラウドサービスの間に、プライベートな通信ルートで接続できる Microsoft Azure ExpressRoute という機能がございます。
Power BI の公式情報では詳細な記載がない場合が多いため、お客様よりよくご質問いただく内容につきまして、本ブログにてまとめてご紹介いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## Microsoft Azure ExpressRoute とは
---
Microsoft Azure ExpressRoute では、専用のプライベート接続を使用してオンプレミスのネットワークを Microsoft Cloud Services に接続できます。
サービスの名前は Azure ExpressRoute ですが、Microsoft 365、Microsoft Power Platform、Dynamics 365 などの Azure 上に構築されたサービスへのプライベート接続もサポートしています。

<div align="center">
<img src="https://learn.microsoft.com/ja-jp/power-platform/guidance/expressroute/media/expressroute-overview.png">
</div>

---
## Power BI で ExpressRoute を使用するには
---

#### 概要

お客様のオンプレミスのご環境から、 Power BI への接続において ExpressRoute をご利用いただくには、ExpressRoute のプロバイダーをご契約いただいた上で、お客様側の企業ネットワークにて ExpressRoute を経由するよう、ネットワークのルーティングを設定いただく必要がございます。

Power BI への接続においては、 Microsoft ピアリングを利用することとなりますが、ExpressRoute 回線が Azure Microsoft ピアリングに対して有効になっている場合は、Azure 内で使用されている [パブリック IP アドレスの範囲](https://learn.microsoft.com/ja-jp/azure/virtual-network/ip-services/public-ip-addresses#public-ip-addresses) に回線経由でアクセスできます。

Power BI は Azure 上に構築されており、 Azure リージョン コミュニティを介して ExpressRoute を使用できます。Power BI テナントのリージョンを確認する方法については、[こちら](https://learn.microsoft.com/ja-jp/power-bi/service-admin-where-is-my-tenant-located) をご確認ください。

> **参考情報**
> - [ExpressRoute のピアリングの場所と接続パートナー - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/expressroute/expressroute-locations-providers)
> - [Microsoft ピアリング | ExpressRoute の FAQ - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/expressroute/expressroute-faqs#microsoft-peering)

</br>

#### 設定方法

ExpressRoute の利用において、Power BI 側にて管理者による特別の設定は必要ございません。

お客様のネットワークから、Power BI への接続に関して、ExpressRoute を経由するよう、「 [Power BI URL を許可リストに追加する](https://learn.microsoft.com/ja-jp/power-bi/admin/power-bi-allow-list-urls)」という公開情報に記載されているエンドポイント に対してお客様の企業ネットワークのルーティング対象として設定いただくことが必要な作業として考えられます。

> **参考情報** 
> - [Power BI URL を許可リストに追加する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/admin/power-bi-allow-list-urls)
</br>

しかしながら、上記の許可リストに記載されている一部の通信においては、ExpressRoute を経由することがサポートされていません。

一例としては、[Microsoft 365 Common と Office Online の URL](https://learn.microsoft.com/ja-jp/microsoft-365/enterprise/urls-and-ip-address-ranges?view=o365-worldwide#microsoft-365-common-and-office-online) に記載されているエンドポイントで、「認証」セッションに含まれる Power BI サービスへサインイン時に使用される Azure AD 認証など、 ExpressRoute 非対応のものが一部含まれています。

そのため、Power BI へのアクセスにおいて、すべてのエンドポイントを ExpressRoute へ経由することができませんので、企業ネットワークにてインターネット接続をブロックしてしまうと、Power BI をご利用いただくのに支障が出る可能性があることをご理解ください。

> [!NOTE] 
> なお、ExpressRoute をお客様の企業内のネットワークにて、どのようにルーティングされるかは、各企業様によって実際の方法が異なりますので、弊サポートから詳細な手順をご案内することができません。予めご了承ください。
</br>

---
## よくある質問
---
#### Q1：ExpressRoute を利用して Power BI へ接続したいが、Power BI で何か設定する必要がありますか。
**A1：** Power BI 側にて管理者による特別の設定は必要ございません。お客様のネットワークで ExpressRoute を経由するよう設定いただく必要があります。

</br>

#### Q2：ExpressRoute を設定したらインターネット経由の接続ができなくなりますか。
**A2：** Power BI サービス側では、インターネットから直接受信するトラフィックはブロックしません。また、ExpressRoute は、インターネットから直接受信したトラフィックからの応答をブロックしません。

ExpressRoute をご利用いただくにあたり、以下の2点を認識いただくことが重要です。
- お客様の企業ネットワーク内からのトラフィックが ExpressRoute を使用することを保証しないこと。 企業ネットワーク内のプロキシルールとルーティング ルールがこれを決定するため、企業ネットワーク内からの要求が ExpressRoute を使用するように設定する必要があること。

- 他の接続 (たとえば、インターネット上のユーザー) が Power BI へのダイレクト アクセスすることをブロックしないこと

> **参考情報** 
> - [クライアント トラフィック | ExpressRoute を Microsoft Power Platform 用に設定する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-platform/guidance/expressroute/setup#client-traffic)

もし Power BI サービス側で、インターネットからのアクセスを禁止したい場合は、代わりに、Azure Private Link のご利用をご検討ください。

詳細につきましては、以下のブログ記事と公開情報をご参照いただけますと幸いです。

> **参考情報** 
> - [Power BI Service へのアクセス制御② Azure Private Link](../pbi_privatelink)
> - [Power BI へのセキュリティで保護されたアクセスのためのプライベート エンドポイント - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-security-private-links)

</br>

#### Q3：オンプレミスデータゲートウェイがインストールされている環境で、ExpressRoute を利用できますか。
**A3：** はい、ご利用いただけます。Power BI サービスと同様に、オンプレミスデータゲートウェイ側にて特別の設定は必要ございません。お客様の企業ネットワークにて対象の通信設定を実施する場合、以下の公開情報にて必要な通信エンドポイントをご確認ください。

> **参考情報** 
> - [Port | オンプレミス データ ゲートウェイの通信設定を調整する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-communication)


しかしながら、オンプレミスデータゲートウェイがインストールされている環境でインターネットアクセスを完全にブロックしてしまった場合、一部正しく通信できないエンドポイントがございますので、ご留意ください。

具体的には、Azure Active Directory (Azure AD) と OAuth2 認証部分において、ExpressRoute 非対応のエンドポイントが含まれています。

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

> **本ブログの関連記事**
> - [Power BI の通信設定](../pbi_pbiservice_network/)
> - [Power BI Service へのアクセス制御② Azure Private Link](../pbi_privatelink)

</br>

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)

