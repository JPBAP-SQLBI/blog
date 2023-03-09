---
title: Power BI Report Server とは
date: 2022-06-30 00:00:00 
tags:
  - Power BI
  - Power BI Report Server
  - 管理者
---


</dr>

こんにちは、Power BI サポート チームの山本です。 

Power BI には SaaS サービスである Power BI サービスとは異なる Power BI Report Server という製品があることをご存知でしょうか。
本記事では、Power BI Report Server はどのようなもので、どんなことができるのか、基本的な部分についてご紹介いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
1. [Power BI Report Server とは](#Power-BI-Report-Server-とは)
2. [Power BI サービスとの違い](#Power-BI-サービスとの違い)
3. [利用される製品の関係性](#利用される製品の関係性)
4. [Power BI Report Server のサポートについて](#Power-BI-Report-Server-のサポートについて)

---
## Power BI Report Server とは
---

Power BI Report Server は、 Report Server という名の通り、お客様が管理されているオンプレミスのサーバー上に Power BI のレポートを配信・共有できる Web サービスの仕組みを構築できる製品です。

Power BI サービスは、SaaS サービスとして Microsoft が提供するクラウド上に展開されておりますが、Power BI Report Server は、展開する場所をお客様ご自身で管理できるため、外部インターネットを経由できないセキュリティ要件の高いエリアでの利用や一定のネットワークからしか接続を許可しない閉域網においても Power BI の機能を利用したい場合に有効な手段となります。
また、お客様ご自身のサーバーでホストされるため、利用するユーザー数に応じて Power BI Pro ライセンスといった有償ライセンスを買い増す必要はありません。

<div align="center">
<img src="2.png">
</div>

</br>

また Power BI Report Server は、SQL Server のレポート機能である SQL Server Reporting Services の上位互換(スーパーセット)であり、SQL Server Reporting Services の機能も兼ね備えた製品です。

</br>

### Power BI Report Server を利用するためには

Power BI Report Server を利用するには、以下いずれかを購入いただくことでライセンスが付帯されます。

1. ソフトウェアアシュアランス付きの SQL Server Enterprise Edition
2. Power BI Premium ライセンス(P1~)

</br>

また Power BI Report Server にPower BI レポートを発行するために、Power BI Pro ライセンスが1つ必要となります。

加えて、レポート定義や資格情報などは SQL Server データベースエンジンに格納されるため（レポートサーバーデータベースと呼称します）、Power BI Premium ライセンスと併用してご利用頂く場合には、別途 SQL Server をご用意いただく必要がございます。

Power BI Premium をご利用いただいている場合、ライセンスは Power BI サービスの管理ポータルの[容量の設定]の画面から Power BI Report Server キーを確認することが可能です。

<div align="center">
<img src="1.png">
</div>

</br>

> **参考情報：**
> - [Power BI Report Server とは](https://learn.microsoft.com/ja-jp/power-bi/report-server/get-started)
> - [Power BI レポート サーバーをインストールするためのハードウェアとソフトウェアの要件](https://learn.microsoft.com/ja-jp/power-bi/report-server/system-requirements)

</br>

---
## Power BI サービスとの違い
---

Power BI サービスと比較したときに、次のような違いや対応していない機能があります。
(詳細については参考情報も合わせてご参照ください)

| 各機能について | Power BI Report Server |
| - | - |
| pbix レポートの開発・作成 | Report Server 向けの Power BI Desktop を使用 |
| リリースサイクル | 年3回(1月、5月、9月)を予定 |
| ダッシュボードの作成・閲覧 | 非対応 |
| アプリ機能(アプリの開発・共有・インストール) | 非対応 |
| オンプレミスデータゲートウェイ | 非対応 |
| 複合モデルのデータセット | 非対応 |
| R や Python 機能 | 非対応 |
| リアルタイムストリーミングデータセット | 非対応 |
| データフロー・データマート | 非対応 |
| Power BI レポートの電子メールサブスクリプション | 非対応(ページ分割されたレポートのサブスクリプションには対応) |
|  |


</br>

> **参考情報：**
> - [Power BI Report Server と Power BI サービスの比較](https://learn.microsoft.com/ja-jp/power-bi/report-server/compare-report-server-service)

</br>

---
## 利用される製品の関係性
---

Power BI Report Server を利用してレポートを組織に展開したい場合に、どのような流れとなるのでしょうか。
以下図を元に、開発、発行・管理、閲覧の順に、それぞれ使用される製品や機能を紹介します。

<div align="center">
<img src="3.png">
</div>

</br>

### 1. レポート開発

#### Power BI Desktop

Power BI サービス同様に Power BI レポートの開発・作成には「Power BI Desktop」が使用できますが、Power BI Report Server 用に最適化された Power BI Desktop が用意されており、Power BI サービスとは異なるデスクトップアプリケーションを利用することになります。

見た目の違いとして、アイコン右下に「RS (Report Server)」の文字が表示されています。

<div align="center">
<img src="4.png">
</div>

</br>

> **参考情報：**
> - [Power BI Report Server とは](https://learn.microsoft.com/ja-jp/power-bi/report-server/get-started)
> - [Power BI レポート サーバーをインストールするためのハードウェアとソフトウェアの要件](https://learn.microsoft.com/ja-jp/power-bi/report-server/system-requirements)


#### Power BI Report Builder / Microsoft Report Builder / SQL Server Data Tools for Visual Studio

Power BI Report Server では、ページ分割されたレポート (rdl) を表現することもでき、ページ分割されたレポートの開発には「[Power BI Report Builder](https://learn.microsoft.com/ja-jp/power-bi/paginated-reports/report-builder-power-bi)」または「[Microsoft Report Builder](https://learn.microsoft.com/ja-jp/sql/reporting-services/install-windows/install-report-builder?view=sql-server-ver16)」、「[SQL Server Data Tools for Visual Studio](https://learn.microsoft.com/ja-jp/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-ver16)」を利用します。
過去に SQL Server Reporting Services でレポート運用を行なってきた組織では、そのままレポート資産を移行して利用することができる強みがあります。

</br>

### 2. レポート発行・管理

#### レポートサーバーコンポーネント (Power BI Report Server と レポートサーバーデータベース)

Power BI Report Server では、Web ポータルの役割の担う“Power BI Report Server”と、保有するレポート定義が格納されるレポートサーバーデータベースの2つが大きな基礎となります。
レポートを表現するために必要なデータソースとの資格情報や接続情報(接続文字列など)はレポートサーバーデータベースに保管されます。
その他レポートの実行結果なども保管されており、例えば SQL Server Management Studio (SSMS) を使用してレポートサーバーデータベースへ接続し、Execution Log 3 ビューから実行履歴を抽出することができます。


<div align="center">
<img src="6.png" alt="Power BI Report Server 構成マネージャー(サーバーアプリケーション)" title="Power BI Report Server 構成マネージャー(サーバーアプリケーション)">
</div>

</br>

<div align="center">
<img src="7.png" alt="SQL Server に格納されるレポートサーバーデータベース" title="SQL Server に格納されるレポートサーバーデータベース">
</div>

</br>

### 3. 閲覧

#### Power BI Report Server Web ポータル

開発されたレポートは、レポートサーバーデータベースに保存され、主なユーザーインターフェースとなる「Web ポータル」からアクセスすることが可能です。
Power BI サービスのワークスペース同様にアクセス制御ができる「フォルダ」機能によって、閲覧できるレポートをユーザーや部署ごとに制御することが可能です。

<div align="center">
<img src="5.png">
</div>

</br>

#### モバイルアプリ

Power BI サービスで提供されている「Power BI モバイルアプリ」は、Power BI Report Server にも接続することが可能で、モバイル最適化されたレポートを開発・閲覧することができます。

<div align="center">
<img src="8.png">
</div>

</br>

---
## Power BI Report Server のサポートについて
---

Microsoft で提供している技術サポートについて、Power BI Report Server はオンプレミスサーバーで稼働する製品の特性上、クラウド製品のPower BI サービスとは異なり、基本的に有償のサポートとなります。

Microsoft の Premier サポート契約や Unified サポート、Performance サポート契約をお持ちのお客様の方は、各ご契約に従ってお問い合わせいただけます。
それ以外のお客様については、Microsoft Professional サポートのインシデントをご購入いただき、技術サポートまでご相談ください。
Professional サポートのサービス詳細やサポート範囲、お問い合わせ方法については、以下よりご確認いただけます。

[Microsoft プロフェッショナル サポートをご利用になる皆様へ](https://www.microsoft.com/ja-jp/services/professional.aspx)

例外として Azure サポートプランにご加入されており、Azure の仮想マシン上に Power BI Report Server を配置されている場合には、Azure サポート要求の画面からお問い合わせをいただくことで、Professional サポートの対応範囲に限り無償でのサポートを受けることが可能です。

[Azure サポート要求を作成する](https://learn.microsoft.com/ja-jp/azure/azure-portal/supportability/how-to-create-azure-support-request)

また英語対応となりますが、コミュニティでの投稿については無料でどなたでも投稿することができますので、まずはこちらで検索や相談を行っていただくこともおすすめいたします。

[Report Server - Microsoft Power BI Community](https://community.powerbi.com/t5/Report-Server/bd-p/ReportServer)

</br>

以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。