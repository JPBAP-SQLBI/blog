---
title: Power BI Copilot　のセキュリティと使用制限方法
date: 2026-02-28 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - Power BI サービス
  - Microsoft Fabric
  - Copilot
---


こんにちは、Power BI サポート チームの金沢です。

以前のブログ[Copilotのセキュリティと使用制限方法] (https://jpbap-sqlbi.github.io/blog/powerbi/pbi_copilot_security/)では、 Power BIでCopilot を使用するにあたって、セキュリティの観点でどのような制限が必要であるかをまとめました。

一方で、「 Power BI の Copilot では具体的に何ができるのか」、「どの機能を利用するために、どのライセンスや容量が必要なのか」といった、機能面・利用条件に関する全体像を把握したいという声も多く聞かれます。

本記事では、 Power BI における 各Copilot 機能の種類や位置づけを整理し、利用にあたって必要となるライセンスや前提条件についてまとめました。
Power BIでCopilotの導入を検討している方や、どの機能が自社環境で利用可能なのかを整理したい方の参考になれば幸いです。


<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
- [目次](#目次)
- [1. Power BI でCopilot を利用するための共通要件](#1-power-bi-でcopilot-を利用するための共通要件)
- [1-1. ライセンス要件](#1-1-ライセンス要件)
- [1-2. テナント設定](#1-2-テナント設定)
- [2. Power BI の Copilot 機能](#2-power-bi-の-copilot-機能)
- [2-1. スタンドアロン](#2-1-スタンドアロン)
- [2-2. レポート・セマンティックモデル](#2-2-レポートセマンティックモデル)
- [2-3. アプリ](#2-3-アプリ)
- [2-4. Power BI Desktop](#2-4-power-bi-desktop)
- [2-5. Power BI モバイルアプリ](#2-5-power-bi-モバイルアプリ)

---
## 1. Power BI でCopilot を利用するための共通要件
---

はじめに、Power BI のCopilot 機能で共通している要件をライセンスとテナント設定にわけて紹介します。

### 1-1. ライセンス要件
Power BIでCopilot を使用する場合は、有料のFabric容量（F2以上）またはPower BI Premium 容量（P1以上）が必要となります。
Power BI Pro 、Premium per User ライセンスや、 Fabric 試用版容量のみではご使用いただけません。

Fabric Copilot 容量（FCC）と呼ばれる Copilotの使用量を1つの容量に課金できるようにする機能があり、上記 Fabric 容量や Power BI Premium容量をFCCに指定することができます。FCCを構成することで、Power BI Pro 、Premium per User の容量を割り当てたワークスペース上でも Copilot を使用することができます。

FCCの詳細な機能説明や設定方法については、以下の公開情報をご確認ください。
>[!NOTE]
> 参考情報：[Fabric の Copilot 容量 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/fabric-copilot-capacity)

また、 Fabric容量を使用する場合は、容量が以下の公開情報で「すべてのワークロード」に記載されているリージョンに配置されている必要があります。
>[!NOTE]
> 参考情報：[Fabric が使用できるリージョン - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/region-availability#all-workloads)

なお、 Power BI Premium 容量については、現在新規にご購入いただけないため、これから Copilot を利用したい方は、 Fabric 容量をご購入ください。
>[!NOTE]
> 参考情報：[Premium容量からFabric容量への移行 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_premium_to_fabric/)

### 1-2. テナント設定
以下のテナント設定は、[設定]>[管理ポータル]>[テナント設定]より制御できます。 多くの設定は一部ユーザーやセキュリティグループだけに許可することも可能なため、機能の利用を許可する対象を制限できます。また、一部設定は容量単位で制御することも可能です。容量単位で制御する場合は、[容量の設定]を開いて容量名を選択して設定を変更することができます。

- <b>ユーザーは、Azure OpenAI に対応する Copilot やその他の機能を使用できます</b>
 Fabric 全体での Copilot の利用可否を制御します。この設定を許可することでユーザーは Power BI を含む Fabric　ワークロード全体で Copilot にアクセスできるようになります。
 なお、スタンドアロン Copilot を使用する場合は、容量レベルではなく、テナントレベルでこの設定を有効化する必要があります。

- <b>Azure OpenAI に送信されたデータは、容量の地理的リージョン、コンプライアンス境界、または国内クラウド インスタンスの外部で処理できます</b>
 Azure OpenAI を利用している Fabric で Copilot および AI 機能を使用する必要があり、容量の地理的リージョンが EU データ境界または米国の外部にある場合、Copilot やその他の生成 AI 機能に送信されるデータが、容量の地理的リージョン、コンプライアンス境界、または国内クラウド インスタンスの外部で処理される可能性があるため、本設定を有効化する必要があります。
 
 お手持ちの Fabric　容量のリージョンに対する、 Azure OpenAI サービスがホストされる地理的領域については、以下の参考情報をご確認ください。
 >[!NOTE]
 > 出典：[Fabric の Copilot の概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/fundamentals/copilot-fabric-overview#data-processing-across-geographic-areas)

- <b>容量は Fabric Copilot 容量として指定できます</b>
 Fabric Copilot 容量（FCC）は、1-1で説明した通り、 Power BI Desktop、Pro、Premium の各ユーザー ワークスペースから Copilot の使用量を 1つの容量に課金できるようにする機能であり、この機能の利用を制御しています。

なお、[Azure OpenAI に送信されたデータは、容量の地理的リージョン、コンプライアンス境界、または国内クラウド インスタンスの外部に格納できます]の設定については、Power BI ではなくノートブックでCopilot を使用する際に必要となるテナント設定です。本設定の詳細については、以下の公開情報に記載されています。

>[!NOTE]
> 参考情報：[Fabric の Copilot の概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/fundamentals/copilot-fabric-overview#data-storage-of-conversation-history-cross-geographic-regions)

---
## 2. Power BI の Copilot 機能
---

続いて、各 Copilot 機能を紹介します。はじめに機能ごとに必要な要件をこの章でまとめ、各節で機能の詳細を説明します。
各 Copilot 機能とその機能に求められる要件は以下の通りです。

<div align="center">
表1. Copilot 機能別要件
</div>
| 機能名 | 要件 |
|---|---|
| スタンドアロン | テナント設定（ユーザーは、スタンドアロンのクロスアイテム Power BI Copilot エクスペリエンス（プレビュー）にアクセスできます）の有効化 |
| レポートとセマンティックモデル | 要約された分析情報を生成する：ワークスペースまたはレポートへの読み取りアクセス権<br>レポートの編集：レポートのあるワークスペースでの共同作成者以上のロール |
| アプリ | 「アプリスコープの Copilot」を利用する場合、アプリの詳細設定にある「アプリナビゲーションに Copilot を表示します。」にチェックを入れる |
| Power BI Desktop | Copilot が有効になっている有料の Fabric 容量または Power BI Premium 容量（P1 以上）が割り当てられている少なくとも 1 つのワークスペースにおいて、管理者、メンバー、または共同作成者ロールが割り当てられている |
| Power BI モバイルアプリ | モバイルアプリのスタンドアロン Copilot を利用するには「スタンドアロン」の要件が、レポート内 Copilot を利用するには「レポートとセマンティックモデル」の要件が適用される |

### 2-1. スタンドアロン
スタンドアロン Copilot は、特定のレポートや編集画面に依存せず、 Power BI サービス全体を横断してデータに対話的にアクセスできるという特徴があります。
ユーザーが現在開いているレポートに限定されることなく、自身がアクセス権を持つレポート、セマンティック モデル、アプリ、Fabric データ エージェントを横断的に対象として質問を行うことができます。

スタンドアロン Copilot を開くには、 Power BI サービスの左側ナビゲーション バーに表示される Copilot アイコンを押下します。

<div align="center">
<img src="スタンドアロンの開き方.png">
図1. スタンドアロン Copilot の開き方 
</div>

また、テナント管理者によってスタンドアロン Copilot が有効になっており、Fabric Copilot容量（FCC容量）が使用可能な場合は、Power BI のホーム画面上にもスタンドアロン Copilot が表示されます。

<div align="center">
<img src="スタンドアロンの開き方_ホーム.png">
図2. ホーム画面上でのスタンドアロンを開き方
</div>

<b>スタンドアロン Copilot 特有のテナント設定と容量要件</b>
スタンドアロン Copilot を利用するためには、第1章の共通要件に加えて、テナント設定で[ユーザーは、スタンドアロンのクロスアイテム Power BI Copilot エクスペリエンス (プレビュー) にアクセスできます]の有効化が必要です。

また、スタンドアロン Copilot の利用にあたって、容量の観点では、1-1で説明した専用の Fabric Copilot容量（FCC容量）を指定するか、Copilotをサポートする容量を割り当てられたワークスペースにアクセスできる必要があります。
>[!NOTE]
> 参考情報：[Copilot for Power BI の概要 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-introduction#requirements-for-the-standalone-copilot)

### 2-2. レポート・セマンティックモデル
レポートとセマンティックモデルのための Copilot では、開いているレポート内のデータに関して質問をしたり、新しいレポートの作成を行ったりすることができます。

レポートとセマンティックモデルで Copilot を使用する場合、 Power BI サービスで対象のレポートを開いて Copilot ボタンを押下すると利用できます。

<div align="center">
<img src="レポート分析.png">
図3. レポート上でCopilot を開く
</div>

なお、レポートやセマンティックモデルで Copilot を利用するには、1-1で説明した Copilot 共通要件を満たしている他、レポートで要約された分析情報を生成するには、少なくともワークスペースまたはレポートへの読み取りアクセス権が必要です。
また、レポートにビジュアルを追加するなど、レポートに対して編集を行うには、レポートのあるワークスペースで共同作成者以上のロールが必要です。

>[!NOTE]
> 参考情報：[Power BI レポートとセマンティック モデルで Copilot を使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-reports-overview)

### 2-3. アプリ
Power BI アプリで Copilot を利用すると、アプリに含まれるレポートやセマンティック モデルを対象に、内容の要約や質問応答を行うことができます。
アプリで利用できる Copilot 機能には、「レポートスコープの Copilot 」と、「アプリスコープの Copilot 」の2種類があります。

レポートスコープの Copilot は、Power BI サービスでワークスペース アプリまたは組織アプリを開いたときに、アプリのナビゲーション内に表示されます。
ワークスペースアプリと組織アプリの違いについては、以下の公開情報をご参照ください。
>[!NOTE]
> 参考情報：[Org Apps を始めよう (プレビュー) - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/explore-reports/org-app-items#key-ways-that-org-app-items-are-different-from-workspace-apps-also-known-as-power-bi-apps)

<div align="center">
<img src="アプリCopilotの開き方.png">
図4. レポートスコープのCopilot
</div>

一方で、アプリスコープの Copilotは組織アプリでは利用できず、ワークスペース アプリでのみ使用できます。
アプリスコープのCopilot の特徴としては、アプリ内のレポートを横断してCopilot と対話できることが挙げられます。

<div align="center">
<img src="アプリスコープのCopilot.png">
図5. アプリスコープのCopilot
</div>

なお、アプリスコープのCopilotサポートされているアイテムは以下の通りであり、アプリでサポートされている一部のアイテムは、アプリ スコープの Copilotではサポートされていません。
- Power BI レポート
- セマンティック モデル

「レポートスコープの Copilot 」と、「アプリスコープの Copilot 」のどちらも、利用するには1-1で記載されている要件を満たしており、「アプリスコープの Copilot 」を利用するには、アプリの詳細設定で[アプリナビゲーションに Copilot を表示します。] にチェックを入れる必要があります。

>[!NOTE]
> 参考情報：[Copilot Power BI アプリ用: アプリスコープのAI機能とレポート - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-apps-overview)

### 2-4. Power BI Desktop
Power BI Desktop の Copilotではビジュアル作成や DAX 作成など、 Copilot がレポート作成を支援します。

Power BI Desktop で Copilot を使用するには、レポート編集画面のリボンに表示される Copilot ボタンを押下します。

<div align="center">
<img src="Desktop Copilotの開き方.png">
図6. Power BI Desktopで Copilot を開く
</div>

Power BI Desktop で Copilot を利用するためには、1-1の共通要件のほか、 Copilot が有効になっている有料の Fabric 容量または Power BI Premium 容量 (P1 以上) が割り当てられている少なくとも 1つのワークスペースにおいて、管理者、メンバー、または共同作成者権限が必要です。

>[!NOTE]
> 参考情報：[Power BI Desktop で Copilot を使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-power-bi-desktop)

### 2-5. Power BI モバイルアプリ
Power BI モバイル アプリの Copilot は iPhone 、 iPad 、 Android スマートフォン、 Android タブレット上で使用できる Copilot機能です。
外出先やモバイル環境でAIを利用した分析情報を利用して、データ主導の意思決定を行うことができます。モバイル アプリでは、スタンドアロン Copilot とレポート内 Copilot の 2 種類のエクスペリエンスが提供されています。 

スタンドアロン Copilot は、Power BI モバイル アプリのホーム画面から起動できる全画面表示のチャット形式の Copilot です。特定のレポートを事前に開かなくても、ユーザーがアクセス権を持つレポート、セマンティック モデル、データ エージェントに対して横断的に質問できます。

一方で、レポート内 Copilot は、モバイル アプリで特定のレポートを開いている状態で利用します。
レポート ヘッダーに表示される Copilot アイコンから起動し、現在表示しているレポートの内容に限定した要約や分析情報を取得できます。

Power BI モバイル アプリで Copilot を利用するためには、1-1で説明した Copilot 共通要件を満たしているほか、スタンドアロン Copilotを利用するには2-1の要件を、レポート内 Copilotを利用するには2-2の要件を満たす必要があります。

>[!NOTE]
> 参考情報：[Power BI Mobile Apps での Copilot の概要 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/explore-reports/mobile/mobile-copilot-overview)

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

※本情報の内容（添付文書、リンク先などを含む）は作成日時点でのものであり、予告なく変更される場合があります。

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)