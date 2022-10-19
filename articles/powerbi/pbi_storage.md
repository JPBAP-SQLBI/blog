---
title: Power BI Pro のワークスペース容量について
date: 2022-01-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - データセット
  - ストレージ
  - Pro
  - 容量
  - storage
---


こんにちは、Power BI サポート チームの山崎です。  
Power BI サービスでは、ユーザー個別に用意されるマイ ワークスペースや、他者と共同作業を行うために使用するアプリ ワークスペースにコンテンツが格納されますが、このワークスペースのストレージ上限が気になったことはありませんか？  
ストレージ上限は、ご利用のライセンスやワークスペースに割り当てられている容量によって異なりますので、本ブログにて詳細をご案内いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---

##### 前提

以下はPro容量を前提にご説明しています。  
テナント内でPremiumまたはPPUをご契約いただいている場合は、いずれもテナント全体で最大100TBの容量が提供され、ユーザーごとやワークスペースごとに制限はございません。



#### ワークスペースごとに 10GB の容量が割り当てられる
まず、ワークスペースごとの考え方としては、マイ ワークスペースもアプリのワークスペースも、ワークスペースごとに 10GB の容量が割り当てられます。  
これは、テナント内の Power BI ユーザー数や、それぞれのワークスペースにアクセス可能なユーザー数に左右されません。  
なお、アプリ ワークスペースについては、テナント全体でどれだけの容量が使用できるかという観点では、 10GB× 有償ライセンス（ Pro または PPU ）のライセンス数を掛けた値を超えることができません。  
例えば、有償ライセンスのユーザーが4名いた場合、“ 10GB×4 ユーザー“ となるので、テナント全体で使用できるアプリ ワークスペースの総合計容量は 40GB となります。


#### ユーザーは、マイワークスペースで10GB、アプリ ワークスペースで 10GB の容量が使用できる
ユーザーが Power BI サービス上で使用できるストレージ容量につきましては、以下の通りマイワークスペースとアプリ ワークスペース（マイワークスペース以外の、他者と共同作業を行うために使用するワークスペースを指します）に分けて考えます。

###### // マイ ワークスペース  
・割り当てられたライセンスの種類にかかわらず、１ユーザーにつき最大10GBの容量が割り当てられます。  

###### // アプリ ワークスペース  
・マイワークスペースとは別に、アプリ ワークスペースごとに最大 10GB の容量が使用できます。（Freeライセンスユーザーは使用できません。）  
これはユーザーがアクセス可能なワークスペース数に左右されません。  
例えば、アクセスできるワークスペースが 3 個でも 100 個の場合も、1 ユーザーに許可されるアプリワークスペースにおける使用可能な容量は、アプリワークスペースごとで最大 10GB となります。

<div align="center">
<img src="1.png">
</div> 

上記内容をもとに、例として以下シナリオの場合の容量について ご説明いたします。   
例  ：  
・テナント内で Power BI Pro のライセンスを持っているユーザーが 4 名  
・マイワークスペースの他にアプリ ワークスペース A, B, C, D が存在する  

 
上記前提を基にした場合、各ワークスペースで使用できる容量の計算は下記の通りになります ：  
・各ユーザーに、マイワークスペース 10GB が割り当てられます。  
・アプリのワークスペース A, B, C, D の最大容量はそれぞれ、10GBとなります。  
・テナントで使用可能なアプリ ワークスペースの最大容量(つまり、ワークスペース A, B, C, D の総合計容量)は、ユーザー数 4×10GB=40GB となります。こちらは1名で使うことも複数名で使うことも可能です。
・アプリのワークスペース A, B, C, D で最大容量の 40GB を使用した場合、新規にアプリのワークスペースEをご用意いただいても、容量超過となりご利用出来ません。  
・アプリのワークスペース A, B, C, D で最大容量の 40GB を使用していない場合は、 40GB 未満の範囲でワークスペース E, F… をご用意・ご使用いただくことが可能です。 

<div align="center">
<img src="2.png">
</div>   


###### ご参考情報1  
[Power BI ワークスペースでデータ ストレージを管理する](https://learn.microsoft.com/ja-jp/power-bi/admin/service-admin-manage-your-data-storage-in-power-bi#manage-items-you-own)

###### ご参考情報2  
冒頭の ”前提” でもご説明したように、テナント内で Premium または PPU をご契約いただいている場合は、いずれもテナント全体で最大 100TB の容量が提供されます。この容量とは別に、既定で割り当てられている Pro の最大容量は変わらずご使用いただけます。  
Premium と PPU 両方導入している場合、 Premium の容量 100TB + PPU の容量 100TB + 既定のPro の容量をご使用いただけるということになります。
 



以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

