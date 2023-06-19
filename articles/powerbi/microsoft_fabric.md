---
title: Microsoft Fabric パブリック プレビュー
date: 2023-06-18 00:00:00 
tags:
  - Fabric
  - Power BI
---

こんにちは、Power BI サポート チームの亀田です。  
この度、Microsoft Fabric (以下 Fabric) がパブリック プレビューとして公開されました。  
Fabric はデータサイエンスやリアルタイム分析、可視化などデータに関する操作が行えるオールインワンの分析ソリューションです。  
本記事では、Fabricとはどのような製品なのかご説明します。また、Fabricは 2023 年 7 月 1 日より既定で有効化されますので、設定についてご案内いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。
> また、冒頭でもお伝えしました通り、Fabric は現在パブリックプレビュー中でございますので、ご案内した内容が今後変更される可能性が十分にございますことをご了承いただきますようお願いいたします。

## 目次

* [Microsoft Fabricとは](#Microsoft-Fabricとは)
* [Fabric の利用](#Fabric-の利用)
  * [Fabric 試用版の開始](#Fabric-試用版の開始)
  * [Fabric 容量の作成](#Fabric-容量の作成)
* [ライセンス](#ライセンス)
* [Fabric に関するテナント設定](#Fabric-に関するテナント設定)
* [Fabric に関するお問い合わせについて](#Fabric-に関するお問い合わせについて)

## Microsoft Fabricとは  
Fabric は 端的に表現するとPower BI、Azure Synapse Analytics、Azure Data Factory を1つのSaaS環境で利用できるオールインワンの分析ソリューションです。この統合によって、データを一元管理でき、コラボレーションをより容易に行うことが可能となります。Fabric で利用できる機能は以下になります。
<div align="center">
<img src="Fabric01.png">
</div>  

- **Data Engineering**  
  ユーザーが構造化データ/非構造化データを一元管理できるレイクハウスを作成することや、Python や R、Scala を利用した対話型のノートブックを作成したデータ分析、データを収集･処理･変換するデータ パイプラインを実行することが可能です。
  > [!NOTE]
  > 参考# [Microsoft Fabric のデータ エンジニアリングとは - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-engineering/data-engineering-overview)
  > 参考# [Lakehouse のエンド ツー エンドのシナリオ: 概要とアーキテクチャ - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-engineering/tutorial-lakehouse-introduction)
  <div align="center">
  <img src="Fabric02.png">
  </div>  

- **Data Factory**  
  さまざまなデータ ソースからデータを取り込み、変換できるデータフローを作成できるほか、データ パイプラインを使用して、複数のタスクを実行できるワークフローを構築することができます。
  > [!NOTE]
  > 参考# [Data Factory とは - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/data-factory-overview)
  > 参考# [Data Factory のエンド ツー エンドのシナリオ - 概要とアーキテクチャ - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/tutorial-end-to-end-introduction)
  <div align="center">
  <img src="Fabric03.png">
  </div>

- **Data Science**  
  データの取得、クレンジングから、モデルのトレーニングといった機械学習モデルの構築から、デプロイ、運用までを実行できます。
  > [!NOTE]
  > 参考# [Microsoft Fabric のデータ サイエンス - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-science/data-science-overview)
  > 参考# [データ サイエンスのチュートリアル - 作業の開始 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-science/tutorial-data-science-introduction)
  <div align="center">
  <img src="Fabric04.png">
  </div>  

- **Data Warehouse**  
  さまざまなデータ ソースに接続し、ウェアハウスを構築することができます。ウェアハウスでは、接続されたデータを簡単に結合することができるため、より少ないリソースで分析が可能となります。
  > [!NOTE]
  > 参考# [Microsoft Fabric のデータ ウェアハウスとは - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-warehouse/data-warehousing)
  > 参考# [データ ウェアハウスのチュートリアル - 概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-warehouse/tutorial-introduction)
  <div align="center">
  <img src="Fabric05.png">
  </div>  

- **Real-Time Analytics**
  Fabric の Real-Time Analytics は、ストリーミングと時系列データに最適化されており、構造化データだけでなく、半構造化データ、非構造化データに対して優れたパフォーマンスを備えています。
  > [!NOTE]
  > 参考# [Microsoft Fabric のReal-Time Analytics の概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/real-time-analytics/overview)
  <div align="center">
  <img src="Fabric06.png">
  </div>  

- **Power BI**
  Power BI は、データに迅速かつ直感的にアクセスして、データを使用してより適切な意思決定を行うことができます。 

これらのように、Fabric ではデータの取得から可視化まで、エンドツーエンドで扱うことができる SaaS プラットフォームとなります。
より詳細に Fabric について知りたい方は、以下の公開情報やトレーニングをご参照ください。
> [!NOTE]
> 参考# [Microsoft Fabric とは - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/get-started/microsoft-fabric-overview)
> 参考# [Microsoft Fabric のドキュメント - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/)
> 参考# [Microsoft Fabric のエンド ツー エンドのチュートリアル - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/get-started/end-to-end-tutorials)
> 参考# [Microsoft Fabric の概要 - Training | Microsoft Learn](https://learn.microsoft.com/ja-jp/training/paths/get-started-fabric/)

## Fabric の利用
### Fabric 試用版の開始
Fabric は、現在 60 日間の試用が可能です。
> [!NOTE]
> 参考# [Fabric (プレビュー) 試用版 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/get-started/fabric-trial)

試用版の利用を開始するには、アカウント マネージャーを開き、 **[無料体験する]** を選択するか、
<div align="center">
<img src="Fabric07.png">
</div> 
<div align="center">
<img src="Fabric08.png">
</div>  

ワークスペースを開き、 **[+ 新規]** > **[すべて表示]** を選択し、
<div align="center">
<img src="Fabric09.png">
</div>  

Fabric アイテムを選択すると、ワークスペースのアップグレードが求められるため、
<div align="center">
<img src="Fabric10.png">
</div>  

**[アップグレード]** を選択してワークスペースを試用版容量ワークスペースにアップグレードし、Fabric の試用を開始します。
<div align="center">
<img src="Fabric11.png">
</div>  

Fabric 試用版をキャンセルするか、60 日の試用版の利用期限が終了したのち Fabric 容量へ移行しない場合には、試用版容量が削除されますのでご注意ください。

### Fabric 容量の作成
Fabric を利用するには、Azure Portal 上から Fabric 容量を購入する必要があります。

Azure Portal にアクセスし、 **[Microsoft Fabric (プレビュー)]** を選択します。
<div align="center">
<img src="Fabric12.png">
</div>  

**[ファブリック容量 の作成]** を選択します。
<div align="center">
<img src="Fabric13.png">
</div>  

サブスクリプション、リソースグループ、容量の名前、リージョン、サイズ、Fabric 容量管理者を設定し、 **[確認と作成]** を選択します。
<div align="center">
<img src="Fabric14.png">
</div>  

## ライセンス
これまで、Power BI では Power BI Free、Power BI Pro、Power BI Premium Per User (PPU)、Power BI Premium Per Capacity (Premium容量)の4つのライセンスがあり、ワークスペースについては Pro、Premium Per User、Premium 容量、Embedded の4つのライセンス モードがありました。  
Fabric によって、ワークスペースのライセンスモードには、Fabric 容量と、Fabric 試用版が追加されました。
<div align="center">
<img src="Fabric15.png">
</div>  

Fabric のワークロードを利用する場合には、Fabric 容量を作成し、Fabric 容量を割り当てたワークスペースに Fabric アイテムを作成するほか、従来のPremium 容量にも Fabric アイテムを作成することが可能です。以下はライセンスとワークスペースのライセンスについて整理した表になります。

|                                                              | Pro                        | Premium Per User (PPU)     | Premium容量                | Embedded                    | Fabric                                                       |
| ------------------------------------------------------------ | -------------------------- | -------------------------- | -------------------------- | --------------------------- | ------------------------------------------------------------ |
| SKU                                                          | なし                       | P3                         | P1 ~ P5                    | EM ~ EM3 / A1~ A8           | F2 ~ F2048                                                   |
| ワークスペースにあるコンテンツを参照できるユーザー ライセンス | Pro、PPU                   | PPU                        | Free、Pro、PPU             | 埋め込みの方法によって (*1) | F64 未満の SKU の場合は Pro、F64 以上の場合は Free、Pro、PPU |
| Fabric アイテムの作成                                        | 不可                       | 不可                       | 可                         | 不可                        | 可                                                           |
| Embedded での利用                                            | 不可                       | 不可                       | 可                         | 可                          | 可                                                           |
| ライセンスの管理                                             | Microsoft 365 管理センター | Microsoft 365 管理センター | Microsoft 365 管理センター | Azure Portal                | Azure Portal                                                 |

*1 埋め込みの方法によって異なります。詳しくは以下の記事をご参照ください。
参考# [Power BI Embedded とは？ライセンスと埋め込み方法 | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_embedded_license/)

ライセンスについては以下の公開情報もご参照ください。
> [!NOTE]
> 参考# [Microsoft Fabric ライセンス - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/licenses)

また、従来のライセンスについては以下のブログをご確認ください。
> [!NOTE]
> 参考# [Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded） | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license/)

## Fabric に関するテナント設定
**[管理ポータル]** > **[テナント設定]** > **[ユーザーは Fabric アイテムを作成できます (パブリック プレビュー)]** を有効化することで、ユーザーが Fabric アイテムを作成することができるようになります。
<div align="center">
<img src="Fabric16.png">
</div>  

テナント全体で有効にしたくない場合には、Premium 容量単位で有効にすることも可能です。 **[管理ポータル]** > **[容量の設定]** から Premium 容量を選択し、 **[委任されたテナントの設定]** > **[ユーザーは Fabric アイテムを作成できます (パブリック プレビュー)]** を有効化します。このとき、 **[テナント設定]** でこの設定を無効にしている場合には、 **[テナント管理者の選択をオーバーライドする]** にチェックが入っていることを確認します。
<div align="center">
<img src="Fabric17.png">
</div>  

> [!IMPORTANT]
> なお、上記設定を無効にしない場合には、【2023 年 7 月 1 日】 にすべての Power BI ユーザーに対して Microsoft Fabric が有効になりますのでご注意ください。
> 参考# [organizationに対して Microsoft Fabric を有効にする - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/fabric-switch)
<div align="center"> 
<img src="Fabric18.png"> 
</div>  

## Fabric に関するお問い合わせについて
Power BI サポートでは、Fabric に関するお問い合わせもご支援が可能でございますが、プレビュー機能でございますため、ご案内ができない内容を含むためご回答が難しい場合や、その後機能が変更される場合などがございます。予めご了承いただくとともに、スムーズな回答のため、お問い合わせの際には事前に以下の公開情報やブログ記事をご一読いただけますと幸いでございます。
> [!NOTE]
> 参考# [Power BI Pro、Power BI Premium、Fabric のサポート オプション - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/support/service-support-options)
> 参考# [Power BI のお問い合わせについて | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/support_boundary/)
> 参考# [Power BI の開発支援・コンサルティングを含む内容に関するお問い合わせについて | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/support_boundary2/)

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。
