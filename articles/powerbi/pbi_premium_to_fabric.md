---
title: Premium容量からFabric容量への移行
date: 2024-07-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Microsoft Fabric
  - 容量
---


こんにちは、Power BI サポート チーム 金沢です。  
今後、Power BI Premium容量（以下、Premium容量）が廃止され、Fabric容量に一本化されることはご存じでしょうか。この記事では、Premium容量がいつまで使えるのか、Premium容量とFabric容量の違いや容量の移行方法についてご案内いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
- [目次](#目次)
- [1.	Premium容量を購入・更新できる期限](#1premium容量を購入更新できる期限)
  - [1-1.    新規にPremium容量の購入を検討している場合](#1-1----新規にpremium容量の購入を検討している場合)
  - [1-2.	既存のPremium容量を更新する場合](#1-2既存のpremium容量を更新する場合)
- [2. Premium容量とFabric容量の違い](#2-premium容量とfabric容量の違い)
  - [2-1.	機能面での違い](#2-1機能面での違い)
  - [2-2.	課金形態の違い](#2-2課金形態の違い)
- [3.	Premium容量からFabric容量への移行方法](#3premium容量からfabric容量への移行方法)
  - [3-1.	ワークスペースの設定から容量を変更する](#3-1ワークスペースの設定から容量を変更する)
  - [3-2.	管理ポータルから容量を変更する](#3-2管理ポータルから容量を変更する)
    - [3-2-1. ワークスペースから変更する方法](#3-2-1-ワークスペースから変更する方法)
    - [3-2-2. 容量の設定から変更する方法](#3-2-2-容量の設定から変更する方法)

---
## 1.	Premium容量を購入・更新できる期限
---

### 1-1.    新規にPremium容量の購入を検討している場合
Premium容量の新規購入は2024年7月1日に終了いたしました。  
現在では新規にPremium容量を購入することはできませんため、今後新規に容量をご契約いただく場合はFabric容量をご購入いただきます。

### 1-2.	既存のPremium容量を更新する場合
Enterprise Agreement契約（以下、EA契約）をお持ちでない場合は、2025年1月1日までPremium容量を更新いただけます。更新日が2025年1月1日以降のお客様は、契約終了時にFabric容量をご購入いただく必要があります。
既存のEA契約を結んでいるお客様は、EA契約が終了するまで、Premium容量を更新し続けることができます。既存の EA 契約の終了が2025年1月1日以降である場合、契約が終了したらFabric 容量に移行する必要があります。

>[!NOTE]
> 参考情報：[Important update coming to Power BI Premium licensing | Microsoft Power BI Blog | Microsoft Power BI](https://powerbi.microsoft.com/en-us/blog/important-update-coming-to-power-bi-premium-licensing/)

<div align="center">
<img src="Premium容量の更新可能期間.png">
図1. Premium容量購入可能期間
</div>


---
## 2. Premium容量とFabric容量の違い
---

### 2-1.	機能面での違い
Power BIの利用において、Premium容量とFabric容量では以下のような主要な機能面での違いがあります。

<div align=center>
表1. Premium容量とFabric容量の機能比較
</div>
|  | Premium容量 | Fabric容量 |
| --- | --- | --- |
| Power BI Report Server | 〇 | 〇(1) |
| Power BI Embedded | × | 〇 |
| Microsoft Fabric(無料)ユーザーのコンテンツの閲覧 (2) | 〇 | 〇(1) |
| 容量の自動スケーリング(3) | 〇 | × |
| 容量の手動スケーリング(4) | × | 〇 |
| Copilot | 〇(2) | 〇(2) |
| 容量の一時停止と再開(5) | × | 〇 |

>[!NOTE]
> (1):F64以上のSKUが必要です。
> (2):Premium容量またはFabric容量を割り当てたワークスペースに閲覧対象のコンテンツを格納する必要があります。[Power BI Premium のよく寄せられる質問 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-faq#f-sku---p-sku--------------)
> (3):[Power BI Premium で自動スケーリングを使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-auto-scale)
> (4):[Fabric の容量をスケーリングする - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/scale-capacity)
> (5):[容量を一時停止して再開する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/pause-resume)


### 2-2.	課金形態の違い

Premium容量は月単位・年単位で購入するのに対し、Fabric容量では月単位・年単位で容量を予約いただくか、従量課金制でご購入いただきます。
Fabric容量の詳細な料金については、以下の価格オプションの詳細にて説明があります。

> [!NOTE]
> 参考情報：[Microsoft Fabric - 価格 | Microsoft Azure](https://azure.microsoft.com/ja-jp/pricing/details/microsoft-fabric/)

また、現在ご利用いただいているPremium容量と同等のSKUのFabric容量をお探しいただくには、以下の公開情報の比較表が参考となります。

> [!NOTE]
> 参考情報：[Microsoft Fabric の概念 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/licenses#capacity-license)


---
## 3.	Premium容量からFabric容量への移行方法
---

Premium容量からFabric容量へ移行するには、Premium容量が割り当てられているワークスペースをFabric容量へ再割り当てする作業が必要です。再割り当てには各ワークスペースから容量を変更いただく方法と管理ポータルから変更する方法があります。

### 3-1.	ワークスペースの設定から容量を変更する

ワークスペースの設定＞ライセンス情報＞ライセンスの構成＞編集　よりご変更いただけます。

<div align="center">
<img src="ワークスペースからの容量再割り当て.png">
図2. ワークスペースの設定からの容量割り当て
</div>

### 3-2.	管理ポータルから容量を変更する
管理ポータルから容量を変更する方法は2通りあります。

#### 3-2-1. ワークスペースから変更する方法
管理ポータル＞ワークスペースを選択し、対象のワークスペースを選択し、「ワークスペースの再割り当て」にて容量をご変更いただけます。

<div align="center">
<img src="管理ポータルからの容量再割り当て.png">
図2. 管理ポータルのワークスペースからの容量割り当て
</div>

#### 3-2-2. 容量の設定から変更する方法

管理ポータル＞容量の設定から容量を選択し、「ワークスペースの割り当て」より容量を割り当てられます。

<div align="center">
<img src="容量の設定からの容量の再割り当て.png">
図3. 管理ポータルの容量の設定からの容量割り当て
</div>


なお、Premium サブスクリプションまたは容量ライセンスの有効期限が切れてから 90 日間の移行期間があります。

> [!NOTE]
> 参考情報：[Fabric と Power BI、終了、クローズ、キャンセル - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/fabric-close-end-cancel?tabs=admin#migrate-an-expiring-p-sku-capacity)



以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)