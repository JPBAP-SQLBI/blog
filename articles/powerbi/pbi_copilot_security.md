---
title: Copilotのセキュリティと使用制限方法 
date: 2025-10-31 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - Power BI サービス
  - Microsoft Fabric
  - Copilot
---


こんにちは、Power BI サポート チームの金沢です。 

Copilot の登場により、Power BI でも自然言語でのレポート作成やデータ分析が手軽にできるようになりました。 
一方で、「Copilotを使うことで自社のデータが社外に漏れないか」「Copilot に入力したデータはどこで、どのように処理されるのか」「Copilot の利用を一部のユーザーだけに制限したい」といったご相談を多くいただきます。 
 
本記事では、Power BIでCopilot を安心してご利用いただくために、データの処理の流れと、管理者がCopilotの利用を制限する方法について説明し、最後によくある質問をまとめました。 

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
- [目次](#目次)
- [1.	Copilotのデータ処理](#1-Copilotのデータ処理)
- [2. Copilotの使用の制御 ](#2-Copilotの使用の制御)
- [3.	よくある質問](#3-よくある質問)

---
## 1. Copilotのデータ処理
---

はじめに、Copilot　へプロンプトを入力してから応答が返るまでに、どのデータが、どの範囲で、どう扱われるのかについて説明します。 
1-1ではCopilot　がデータ処理を行うにあたっての前提を説明し、1-2でCopilot　がデータを処理する流れについて解説します。 

### 1-1. Copilotのデータ処理の前提 
Copilot では Microsoft が管理している Azure OpenAI を使用して、ユーザーによる入力、グラウンディング データ、Copilot 出力を含むすべてのデータを処理しています。 
このため、お客様のデータはモデルのトレーニングに使用されず、他のテナントへのデータ流出はありません。 

また、Copilot との対話は、各ユーザーに固有であるため、Copilot は、現在のユーザーがアクセス許可を持っているデータのみにアクセスが可能です。これに加え、Copilot　の出力は、そのユーザーにのみ表示され、他のユーザーからのデータは使用されません。 

>[!NOTE]
> 参考情報：[Fabric での Copilot のプライバシー、セキュリティ、責任ある AI の使用 - Microsoft Fabric | Microsoft Learn ](https://learn.microsoft.com/ja-jp/fabric/fundamentals/copilot-privacy-security#how-copilot-works)

### 1-2. Copilot　がデータを処理する流れ
Copilot　は次の流れでデータを処理します。

<div align="center">
<img src="処理の流れ.png">
図1. Copilotがデータ処理する流れ 
</div>

<b>①インプット</b>
Copilot がユーザーからプロンプトを受け取ります。

<b>②データの前処理と接地</b>
Copilot　はユーザーのプロンプトに応じて、データセット スキーマ、特定のデータ ポイント、およびユーザーの現在のタスクに関連するその他の情報の組み合わせを取得する場合があります。 

データ取得の範囲は、そのユーザーにアクセス許可があるデータに限られます。

<b>③後処理</b>
Copilot　を利用した場所に応じて、Copilot はさまざまな方法で大規模言語モデル (LLM) 応答を処理します。 
たとえば、DAX クエリ ビュー エクスペリエンスでは、生成された DAX クエリが確実に実行できるように、DAX パーサーを介して LLM 応答から DAX を実行します。 

<b>④アウトプット</b>
チャット メッセージやDAX　式などの形でCopilot　がユーザーに応答します。 

>[!NOTE]
> 出典：[Copilot in Power BI 統合 - Power BI | Microsoft Learn をもとに作成](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-integration#overview-of-how-copilot-in-power-bi-works)

---
## 2.Copilotの使用の制御 
---

Copilot を安全かつ計画的ユーザーへ展開するには、どのユーザーに、どの機能を使えるのかをテナント設定で明確に制御する必要があります。 
本章では2‑1 で Copilot の利用可否と、利用できる機能の範囲を制御する主要なテナント設定をまとめています。  

### 2-1.テナント設定 
以下のテナント設定は、[設定]>[管理ポータル]>[テナント設定]より制御できます。 多くの設定は一部ユーザーやセキュリティグループだけに許可することも可能なため、機能の利用を許可する対象を制限できます。また、一部設定は容量単位で制御することも可能です。容量単位で制御する場合は、[容量の設定]を開いて容量名を選択して設定を変更することができます。 

- <b>ユーザーは、Azure OpenAI に対応する Copilot やその他の機能を使用できます</b>
Fabric 全体での Copilot の利用可否を制御します。この設定を許可することでユーザーはPower BI を含む Fabric　ワークロード全体で Copilot にアクセスできるようになります。 

- <b>Azure OpenAI に送信されたデータは、容量の地理的リージョン、コンプライアンス境界、または国内クラウド インスタンスの外部で処理できます</b>
Azure OpenAI を利用している Fabric で Copilot および AI 機能を使用する必要があり、容量の地理的リージョンが EU データ境界または米国の外部にある場合、Copilot やその他の生成 AI 機能に送信されるデータが、容量の地理的リージョン、コンプライアンス境界、または国内クラウド インスタンスの外部で処理される可能性があるため、本設定を有効化する必要があります。 
お手持ちの Fabric　容量のリージョンにおける、Azure OpenAI サービスがホストされている地理的領域については、以下の参考情報をご確認ください。 

>[!NOTE]
> 参考情報：[Fabric の Copilot の概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/fundamentals/copilot-fabric-overview#data-processing-across-geographic-areas)

- <b>ユーザーは、スタンドアロンのクロスアイテム Power BI Copilot エクスペリエンス (プレビュー) にアクセスできます</b>
この設定を有効化すると、以下のイメージのように画面左側のバーに Copilot ボタンが表示され、ユーザーがアクセス可能なセマンティックモデルやレポートを横断した質問に対して回答が得られます。

<div align="center">
<img src="copilot-standalone-screen.png">
図2. スタンドアロンの Copilot ボタンの表示  
</div>

スタンドアロン Copilot 機能（プレビュー）の詳細については、以下の公開情報をご確認ください。

>[!NOTE]
> 参考情報：[Power BI でのスタンドアロン Copilot エクスペリエンス (プレビュー) - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-chat-with-data-standalone)

- <b>Power BI エクスペリエンス (プレビュー) でスタンドアロン Copilot に AI で事前に準備された項目のみを表示する</b>
本設定は、上記[ユーザーは、スタンドアロンのクロスアイテム Power BI Copilot エクスペリエンス (プレビュー) にアクセスできます]を有効している場合に、スタンドアロンの Power BI Copilot 機能が、AI の準備済みとしてマークされているコンテンツをのみを検索の対象として使用するように制限されます。 
この設定はドメイン単位、ワークスペース単位で制御することができます。 

- <b>容量は Fabric Copilot 容量として指定できます</b>
Fabric Copilot 容量とは、ユーザーが Power BI Desktop、Pro、Premium の各ユーザー ワークスペースから Copilot の使用量を 1 つの容量に課金できるようにする機能であり、この機能の利用を制御しています。 
Fabric Copilot 容量の詳細は以下の公開情報に記載されています。

>[!NOTE]
> 参考情報：[Fabric の Copilot 容量 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/fabric-copilot-capacity)

なお、[Azure OpenAI に送信されたデータは、容量の地理的リージョン、コンプライアンス境界、または国内クラウド インスタンスの外部に格納できます]の設定については、Power BI ではなくノートブックでCopilot を使用する際に必要となるテナント設定です。本設定の詳細については、以下の公開情報に記載されています。

>[!NOTE]
> 参考情報：[Fabric の Copilot の概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/fundamentals/copilot-fabric-overview#data-storage-of-conversation-history-cross-geographic-regions)

---
## 3. よくある質問
---
Q1.管理者がなにも設定を変更していない場合、Power BI ユーザーは Copilot を勝手に使うことができますか？ 
A1. テナントまたは容量が米国またはフランス以外の場合、 Copilot は既定で無効になっています。

>[!NOTE]
> 参考情報：[Power BI 用の Copilot を使用してストーリービジュアルを作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-create-narrative?tabs=powerbi-service)


Q2. ユーザーが Copilot を使っているか、確認することはできますか？ 
A2. 監査ログで確認することが可能です。Fabricで Copilot を使用すると、監査ログ上の操作名に”RequestCopilot”が記録されます。

>[!NOTE]
> 参考情報：[Power BI のユーザーアクティビティ追跡方法の比較 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_activity_log_usage_metrics/)

Q3. Power BI で Copilot を使用すると課金されますか？ 
A3.  Copilot 自体の追加課金はありませんが、要求ごとに CU を消費し、容量料金として請求に反映されます。 

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

※本情報の内容（添付文書、リンク先などを含む）は作成日時点でのものであり、予告なく変更される場合があります。

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
