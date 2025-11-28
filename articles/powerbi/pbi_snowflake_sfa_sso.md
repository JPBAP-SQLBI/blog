---
title: Snowflake 単一要素パスワード認証廃止に伴う Power BI としての対応と Power BI からの接続方法について
date: 2025-06-27 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Snowflake
---

こんにちは、Power BI サポート チームの中川です。

Power BI では データソースとして Snowflake に接続することが可能ですが、Snowflake では 2025 年 11 月以降、単一要素パスワード (SFA: Single Factor Authentication) による認証が廃止されます。この変更に関して今後利用できる認証方式について多くのお問い合わせをいただいております。<br>
また、Power BI の Snowflake コネクタで Microsoft アカウントを使った接続には、Snowflake 側での SSO (シングルサインオン) 設定などの追加対応が必要な点もあり、こちらも多くのお問い合わせをいただいております。

本ブログでは、Snowflake の単一要素パスワード認証の廃止に伴う Power BI としての対応方法や、Microsoft アカウントによる接続方法についてご紹介します。



<!-- more -->
> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [Snowflake 公式アナウンスの概要](#Snowflake-公式アナウンスの概要)
* [Power BI から利用可能な接続方法](#Power-BI-から利用可能な接続方法)
* [Snowflake コネクタのキーペア認証のサポート予定について](#Snowflake-コネクタのキーペア認証のサポート予定について)
* [Microsoft アカウントで接続する方法](#Microsoft-アカウントで接続する方法)
* [よくあるご質問（FAQ）](#よくあるご質問faq)
* [おわりに](#おわりに)

---
## Snowflake 公式アナウンスの概要
---
単一要素パスワード認証の廃止について、Snowflake 社の公開情報では大きく以下の 2 点が案内されています。

- 2025 年 11 月からすべてのユーザーに対して単一要素パスワード認証がブロックされる
- 今後は多要素認証 (MFA)、SSO (SAML/OAuth)、またはキーペアなどのセキュアな認証方式を利用する必要がある

詳細については、必ず Snowflake 社の公開情報をご参照ください。

>[!NOTE]
> 参考情報：[Snowflake Will Block Single-Factor Password Authentication by November 2025](https://www.snowflake.com/en/blog/blocking-single-factor-password-authentification/)


---
## Power BI から利用可能な接続方法
---
単一要素パスワード認証の廃止に伴い、Power BI から Snowflake に接続する方法としては、主に以下の2種類が挙げられます。

### ODBC コネクタ
Snowflake の ODBC ドライバーを使って接続が可能です。キーペア認証に対応しているとされており、SFA 廃止後はキーペア認証が選択肢であると考えられます。
ただし、キーペアの生成や設定方法については Snowflake 側のドキュメントやサポートをご確認ください。

>[!NOTE]
> 参考情報：[キーペア認証とキーペアローテーション | Snowflake Documentation](https://docs.snowflake.com/ja/user-guide/key-pair-auth)


なお、 ODBC コネクタでは Power BI の DirectQuery は利用できません。
>[!NOTE]
> 参考情報：[Power Query ODBC コネクタ - Power Query | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-query/connectors/odbc)



### Snowflake コネクタ
Snowflake コネクタでは、Microsoft アカウントを用いた認証が可能です。ただし、Snowflake 側での設定などが別途必要になります。接続手順は [Microsoft アカウントで接続する方法](#Microsoft-アカウントで接続する方法) のセクションにてご紹介します。

なお、本コネクタは DirectQuery に対応しており、ロールやデータベースの指定などの詳細オプションも利用可能です。

>[!NOTE]
> 参考情報：[Power Query Snowflake コネクタ - Power Query | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-query/connectors/snowflake)

下表は、単一要素パスワード認証の廃止に伴い可能となる接続方法を整理したものです。

| 項目 | ODBC コネクタ | Snowflake コネクタ |
|------|----------------|----------------------|
| 認証方式 | キーペア認証 | Microsoft アカウント（Microsoft Entra ID） |
| キーペア認証対応 | 対応 | 非対応（詳細は後述） |
| 接続モード | インポート | インポート<br>Direct Query<br>※ Entra ID SSO は Direct Query のみ |
| 接続に必要な準備 | ・ODBC ドライバのインストール<br>・キーペアの生成と設定 | ・Snowflake 側での設定<br>・Power BI 側でのオプション有効化、テナント設定 |


---
## Snowflake コネクタのキーペア認証のサポート予定について
---
2025 年 6 月現在、Snowflake コネクタにおけるキーペア認証はサポートされていません。ただし、正式なリリース時期は未定ですが、今後サポートが予定されています。 リリース予定日などの最新情報については公開情報からご確認ください。 

>[!NOTE]
> 参考情報：[Power Query Snowflake コネクタ - Microsoft Learn](https://learn.microsoft.com/ja-jp/power-query/connectors/snowflake)
> 参考情報：[Microsoft Power BI プロダクト ロードマップ](https://roadmap.fabric.microsoft.com/?product=powerbi)
> 参考情報：[Power BI ブログ — 更新とニュース](https://powerbi.microsoft.com/ja-jp/blog/)


キーペア認証が正式にサポートされるまでの間は、当ブログでご紹介している他の認証方法の活用をご検討ください。

---
## Microsoft アカウントで接続する方法
---

Snowflake に対して、Microsoft アカウント (Microsoft Entra ID) を使用して Power BI から接続する方法についても、多くのお問い合わせをいただいています。本セクションでは、Microsoft アカウントを使用した Snowflake 接続に必要な設定についてご紹介します。

### Snowflake 側の設定

Snowflake に対して Microsoft Entra ID で認証を行うには、Snowflake 側で Entra ID との統合設定が必要です。
詳細な手順については、以下の公開情報をご参照ください。

>[!NOTE]
> 参考情報：[Power BI SSO to Snowflake | Snowflake Documentation
](https://docs.snowflake.com/en/user-guide/oauth-powerbi#getting-started)


###  Power BI 側の接続方法
Power BI から Snowflake に接続する方法は、以下の 公開情報をご確認ください。

>[!NOTE]
> 参考情報：[Power Query Snowflake コネクタ - Microsoft Learn](https://learn.microsoft.com/ja-jp/power-query/connectors/snowflake)
> 参考情報：[Power BI で Snowflake に接続する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-connect-snowflake#admin-portal)

### Power BI サービスでの SSO 利用に関する補足

Microsoft アカウント (Entra ID) を利用した認証は、インポートモード と Direct Query モードの両方でサポートされていますが、レポートを閲覧するユーザーの資格情報で  Snowflake へ接続する Microsoft Entra ID シングル サインオンは、Direct Query のみでサポートされています。

下表は、Direct Query モードで Microsoft Entra ID によるシングル サインオンを構成する際に必要な設定を、接続方式ごとに整理したものです。

| 接続方式                     | 接続の設定①<br>Azure AD 経由での SSO を有効 | テナント設定②<br>Snowflake SSO を有効 | テナント設定③<br>ゲートウェイ用 SSO を有効 |
|----------------------------|:-------------------------------------------:|:--------------------------------------:|:--------------------------------------------:|
| 個人 / 共有クラウド接続       | ON                                           | ON                                     | OFF（設定不要）                             |
| オンプレミス データ ゲートウェイ | ON                                           | ON                                     | ON                                           |
| VNet データ ゲートウェイ      | ON                                           | ON                                     | OFF（設定不要）                             |


上記表に該当する設定項目と公開情報は以下の通りです。

1. データ ソースの接続設定で「Direct Query クエリに Azure AD 経由で SSO を使用する」を有効にする

<div align="left">
<img src="DirectQuery_Azure_AD_SSO_Personal.png">
</div>
<div align="center"><em>個人用クラウド接続の場合</em></div>
</br>

<div align="left">
<img src="DirectQuery_Azure_AD_SSO.png">
</div>
<div align="center"><em>共有クラウド接続またはゲートウェイを利用の場合</em></div>
</br>

>[!NOTE]
> 参考情報：[Power BI で Snowflake に接続する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-connect-snowflake#configure-a-semantic-model-with-microsoft-entra-id)
 
 

2. Power BI 管理ポータルの「テナント設定」＞「Snowflake SSO」を有効化する
 
<div align="left">
<img src="tenant_snowflake_sso.png">
</div>
</br>

>[!NOTE]
> 参考情報：[Power BI で Snowflake に接続する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-connect-snowflake#admin-portal)
 

3. Power BI 管理ポータルの「テナント設定」＞「データ ゲートウェイ向け Microsoft Entra シングル サインオン」を有効化する

<div align="left">
<img src="tenant_gateway_sso.png">
</div>
</br>

>[!NOTE]
> 参考情報：[統合管理者の設定 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/service-admin-portal-integration#microsoft-entra-single-sign-on-sso-for-gateway)
 

---
## よくあるご質問（FAQ）
---

<font color="HotPink">**Q1：Snowflake で設定を行ったが、Power BI Desktop から接続できない**  </font>   
A：Snowflake で設定したにもかかわらず Power BI Desktop から接続できない場合、その多くは Snowflake 側の設定の誤りや、接続しようとしているアカウントに必要な権限が不足していることが原因です。まずは Snowflake の設定内容やアカウントの権限を改めてご確認ください。<br>
Snowflake の公開情報では Power BI から認証する際に発生するエラーやトラブルシューティングの事例がございますので、合わせてご参考ください。

>[!NOTE]
> 参考情報：[Power BI SSO to Snowflake | Snowflake Documentation](https://docs.snowflake.com/en/user-guide/oauth-powerbi#troubleshooting)

また、発生しているエラーメッセージや事象を Snowflake のコミュニティで検索することで、同様の事象や解決策が見つかる場合がありますので、適宜ご活用いただければ幸いです。弊社サポートの回答でも当コミュニティの内容をもとにご案内させていただくことが多くございます。

>[!NOTE]
> 参考情報：[Snowflake Data Heroes Community](https://community.snowflake.com/s)

<font color="HotPink">**Q2：Power BI サービスから Snowflake に接続できない**  </font>   
A：Power BI Desktop から接続できる一方で、Power BI サービスからは接続できない場合、ネットワークポリシーによって Power BI サービスからの通信が Snowflake 側でブロックされている可能性があります。

対応策としては、Azure IP Ranges に記載されている Azure パブリック IP アドレス範囲を Snowflake 側のホワイトリストやファイアウォール設定に追加する必要があります。しかし、これらの IP アドレス範囲は 1 週間ごとに更新があるため、継続的なメンテナンスが必要です。

この運用負荷を回避するための代替手段として、「オンプレミス データ ゲートウェイ」をサーバー (または VM) 上にインストールし、Snowflake 側ではこのサーバーの固定 IP からの接続のみを許可する、という方法が推奨されます。

>[!NOTE]
> 参考情報：[Power BI の通信設定 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_pbiservice_network/)



---
## おわりに
本ブログでは、Snowflake の単一要素パスワード認証の廃止に伴う Power BI としての対応方法や、Microsoft アカウントによる接続方法についてご説明しました。
Microsoft アカウント (Microsoft Entra ID) を用いた接続については、Snowflake 側の SSO 設定や Power BI テナント構成の適切な設定で、従来の単純な ID/パスワード接続と比較して準備が必要となるため、早めの対応を検討いただくことをおすすめします。

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。


---
**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)