---
title: オンプレミスデータゲートウェイのセキュリティーロール
date: 2022-05-31 00:00:00 
tags:
  - Power BI
  - オンプレミスデータゲートウェイ
  - On-Premises Data Gateway
  - セキュリティーロール
  - Security Roles
  - 管理者
  - Creator
---

<span style="color: red; ">
Update: 2022/5/31</br>
2022年5月6日、Power BI サービスの「ゲートウェイの管理」画面が刷新され、
新しいセキュリティロールについても Power BI サービス上で追加/変更できるようになりました。
これに伴い、本記事も一部内容を修正いたしました。
</span>

</dr>

こんにちは、Power BI サポート チームのチャンです。 

Power BI では、オンプレミス環境にあるデータソースへ接続するために、オンプレミスデータゲートウェイの機能が用意されていますが、そのオンプレミスデータゲートウェイに新たなセキュリティーロールが追加されていますので、以下にてご紹介いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は 弊社公式ブログ「Microsoft Power BI ブログ」の公開情報を元に構成しておりますが、本記事編集時点と実際の機能やリリース時期に相違がある場合がございます。
> 元記事は以下よりご確認ください（英語）。
> <Span style="font-size: 100%">[Additional gateway security roles for Power BI](https://powerbi.microsoft.com/en-us/blog/additional-gateway-security-roles-for-power-bi/)</span>
> </br>
> 本機能は開発段階 (プレビュー)でございますため、今後予告なしに機能が削除されたり、
> 動作変更が発生する可能性がありますことをあらかじめご了承くださいますようお願い申し上げます。

</br>

---

## オンプレミスデータゲートウェイとは

---

オンプレミス データ ゲートウェイは橋渡しとしての役割を果たし、クラウド内に存在しないオンプレミス データといくつかの Microsoft クラウド サービスとの間で迅速かつ安全なデータ転送を行います。
オンプレミスデータゲートウェイをご利用いただけるサービスは、Power BI、Power Apps、Power Automate、Azure Analysis Services、および Azure Logic Apps が含まれています。

具体的に、オンプレミスデータゲートウェイからデータソースへの接続において、どのような処理を行われているかにつきましては、以下のドキュメントをご参照ください。

> **参考情報：**
> - [オンプレミス データ ゲートウェイのアーキテクチャ](https://docs.microsoft.com/ja-jp/data-integration/gateway/service-gateway-onprem-indepth)

また、Power BI サービスで、オンプレミスデータゲートウェイを管理するには、[設定] > [ゲートウェイの管理] から実施いただけます。

ゲートウェイを使用した接続手順は以下のブログ記事をご参考ください。
> **参考情報：**
> - [Power BI サービスのデータセット更新手順について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_refresh_settings/)

<div align="center">
<img src="pbi_service_gateway.png" alt="オンプレミスデータゲートウェイの管理" title="オンプレミスデータゲートウェイの管理">
</div>


</br>

---

## オンプレミスデータゲートウェイのセキュリティーロール

---

より細かな管理を行えるように、 Power BI でも Power Platform で設定できる新規のセキュリティーロールが適用されるようになりました。
ゲートウェイ全体に対して適用するロール（[ゲートウェイロール](#ゲートウェイロール)）と、それぞれのデータソースに対して設定するロール（[接続ロール](#接続（データソース）ロール)）の2種類がございます。

---
### ゲートウェイロール
---

オンプレミス データゲートウェイにある 3 つのセキュリティ ロールは次の通りです。

| ゲートウェイロール | 今回の</br>新ロール | 説明 | コメント |
| - | - | - | - |
| 管理者 | <div align="center">-</div> | ✓ オンプレミス データ ゲートウェイの管理および更新 </br> ✓ ゲートウェイに新たな接続 (データ ソース) の作成 </br> ✓ 管理者、接続作成者、およびゲートウェイでロールを共有する接続作成者を持つユーザーの管理 (追加/削除) </br> ✓ ゲートウェイで作成されたすべての接続へのアクセスの管理 | ゲートウェイの最上位権限で、</br>ゲートウェイに関するすべてを管理できますため、接続（データソース）ロールの権限を上回っています。 |
| 接続作成機能 | <div align="center">〇</div> | ✓ ゲートウェイ上に接続/データ ソースの作成 </br> ✓ ゲートウェイにゲートウェイがオンラインかオフラインかをテストすること </br> × ゲートウェイを管理や更新したり、ゲートウェイ上の他のユーザーを追加または削除したりすることはできません | 接続（データソース）を追加できる権限で、</br>データセットを新規作成して、</br>ゲートウェイを使用したデータ接続を設定するユーザーに対して付与することをおすすめします。 |
| 再共有による接続作成機能 | <div align="center">〇</div> | ✓ ゲートウェイ上に接続/データ ソースの作成 </br> ✓ ゲートウェイの状態をテストすること </br> ✓ 接続作成者として他のユーザーとゲートウェイを共有すること </br> × ゲートウェイからユーザーを削除することはできません | 上記の「接続作成機能」に加え、</br>さらに新規のユーザーと共有できる権限です。 |

**■[Power BI サービス](https://app.powerbi.com/groups/me/gateways/)で設定する場合（ゲートウェイ管理者のみ）**

[設定] > [ゲートウェイの管理] > [オンプレミスデータゲートウェイ] > […] > [ユーザーの管理]

<div align="center">
<img src="pbi_service_gateway3.png" alt="Power BI サービス上のゲートウェイ管理" title="Power BI サービス上のゲートウェイ管理">
</div>

**■[Power Platform 管理センター](https://admin.powerplatform.microsoft.com/)で設定する場合**

[データ（プレビュー] > [オンプレミス データ ゲートウェイ] > [ゲートウェイ]のオプション > [ユーザー管理] 

<div align="center">
<img src="power_platform_gateway.png" alt="Power Platform管理センターでのゲートウェイ管理" title="Power Platform管理センターでのゲートウェイ管理">
</div>


</br>

---
### 接続（データソース）ロール
---

オンプレミス データ ゲートウェイで接続 (データ ソース) を作成すると、接続 (データ ソース) の所有者になります。

| 接続ロール | 今回の</br>新ロール | 説明 | コメント |
| - | - | - | - |
| 所有者 | <div align="center">〇</div> | ✓ 資格情報の表示と更新を許可されています。 </br> ✓ 接続（データソース）を削除することもできます。  </br> ✓所有者、ユーザー、または共有アクセス許可のあるユーザーとの接続に他のユーザーを割り当てることができます。 | データソースごとの資格情報の</br>更新を許可する場合にこちらのロールをご利用ください。 |
| ユーザー | <div align="center">-</div> | ✓ Power BI レポートおよび Power BI データフロー、または Power Apps で接続 (データ ソース) を使用できます。 </br> × 資格情報を表示または更新することはできません。 | データセットの更新作業で</br>特定のデータソースを使用する必要がある場合におすすめです。 |
| 再共有できるユーザー | <div align="center">〇</div> | ✓ Power BI レポートおよび Power BI データフロー、または Power Apps で接続 (データ ソース) を使用できます</br> ✓ ユーザーのアクセス許可を使用してデータ ソースを他のユーザーと共有できます。 | 上記の「ユーザー」に加え、</br>さらにデータソースを新規のユーザーと共有できる権限です。 |

**■[Power BI サービス](https://app.powerbi.com/groups/me/gateways/)で設定する場合（ユーザーのみ）**

[設定] > [ゲートウェイの管理] > [データソース] > [ユーザーの管理]


<div align="center">
<img src="pbi_service_datasource2.png" alt="Power BI サービス上のデータソース管理" title="Power BI サービス上のデータソース管理">
</div>

**■[Power Platform 管理センター](https://admin.powerplatform.microsoft.com/)で設定する場合**

[データ（プレビュー] > [データソース] > [データソース]のオプション > [ユーザー管理] 

<div align="center">
<img src="power_platform_datasource.png" alt="Power Platform管理センターでのデータソース管理" title="Power Platform管理センターでのデータソース管理">
</div>


</br>

> **参考情報：**
> - [オンプレミス データ ゲートウェイのセキュリティ ロールを管理する](https://docs.microsoft.com/ja-jp/data-integration/gateway/manage-security-roles)
> - [オンプレミス データ ゲートウェイの管理 (プレビュー)](https://docs.microsoft.com/ja-jp/power-platform/admin/onpremises-data-gateway-management?msclkid=9458b01bc42a11ecac3c3ed358d0c10a)

</br>
以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。
