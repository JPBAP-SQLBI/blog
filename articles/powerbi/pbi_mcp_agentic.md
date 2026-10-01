---
title: Power BI MCP と Power BI Agentic の全体像
date: 2026-09-30 00:00:00
tags:
  - Power BI
  - Microsoft Fabric
  - Fabric IQ
  - MCP
  - Model Context Protocol
  - Power BI Agentic
  - AI エージェント
---

# Power BI MCP と Power BI Agentic の全体像と導入方法

<a id="introduction"></a>

こんにちは、Power BI サポート チームの中川です。

Power BI では、GitHub Copilot などの AI エージェントからセマンティック モデルを操作したり、データに関する質問を行ったりするための MCP サーバーが公開されています。また、AI エージェントによるモデルやレポートの作成を支援するスキルとツールをまとめた、Power BI Agentic も紹介されています。

一方で、関連するドキュメントには MCP サーバー、スキル、プラグイン、Desktop Bridge といった用語が登場するため、それぞれが何を担当し、何を導入すればよいのかを整理しにくい場合があります。

本ブログでは、Power BI に関連する各種 MCP サーバーをはじめ、スキルやツールの役割と導入方法についてご紹介いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。
>また、パブリックプレビュー中の機能が含まれており、ご案内した内容が今後変更される可能性が十分にございますことをご了承いただきますようお願いいたします。



---

## 目次

- [Power BI の MCP サーバーについて](#mcp-servers)
- [Power BI Agentic とは](#agentic)
- [Power BI MCP・プラグインの導入方法](#installation)
- [Power BI Desktop Bridge](#desktop-tools)
- [PBIX・PBIP の使い分け](#file-formats)
- [おわりに](#conclusion)

---

<a id="mcp-servers"></a>

## Power BI の MCP サーバーについて

Power BI の MCP サーバーは、AI エージェントが Power BI に対して操作を行うためのツールを提供します。AI エージェントは、これらのツールを呼び出すことで、モデルの構造を取得・変更したり、DAX クエリを実行して結果を受け取ったりできます。

なお、本記事では、Power BI Authoring MCP server を **Authoring MCP**、Power BI Consumption MCP server を **Consumption MCP**、Fabric IQ MCP server を **Fabric IQ MCP** と表記します。

各 MCP サーバーの主な機能や提供状態を、以下の表にまとめます。


| 項目 | Authoring MCP | Consumption MCP | Fabric IQ MCP |
| --- | --- | --- | --- |
| 主な機能 | モデルの作成・変更、DAX クエリの実行 | メタデータの取得、DAX クエリの生成、DAX クエリの実行 | レポート・モデルの検索、メタデータの取得、値の検索、DAX クエリの実行 |
| サーバーが動作する場所 | Microsoft がホストする環境、または利用者のコンピューター | Microsoft がホストするリモートのエンドポイント | リモートのエンドポイント |
| 提供状態 | プレビュー | プレビュー | 一般提供（GA） |
| 位置付け | モデルの作成・変更用 | ワークスペース上のセマンティック モデルのデータへの問い合わせ用 | ワークスペース上のセマンティック モデルのデータへの問い合わせ用（推奨） |

> [!TIP]
> 以前 Remote MCP サーバーとして公開されていたものは、現在のドキュメントでは Consumption MCP として案内されています。また、Local MCP は、Authoring MCP の Local 方式にあたります。
>
> 参考情報: [MCP サーバーの概要 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/mcp/mcp-servers-overview)
> 参考情報:[Power BI 従量制 MCP サーバーのセットアップ - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/mcp/remote-mcp-server-get-started)

### Power BI Authoring MCP

Power BI Authoring（作成用）MCP サーバーは、セマンティック モデルの作成・変更や確認に関するツールを提供する MCP サーバーです。主に以下のような操作ができます。

- テーブル、列、メジャー、リレーションシップなどの確認・作成・変更
- 複数のモデル オブジェクトの名前変更や翻訳などの一括操作
- TMDL や PBIP のモデル定義を扱う作業
- DAX クエリの実行による、メジャーの計算結果や計算ロジックの確認

たとえば、メジャーを追加した後、そのメジャーを使う DAX クエリを実行して計算結果を確認するなど、モデルの変更とその結果の検証を AI エージェントにて実行できます。

#### Hosted と Local の使い分け

Authoring MCP サーバーには、Microsoft がホストする **Hosted** と、利用者のコンピューターで動作する **Local** の2つの方式があります。

| 比較項目 | Hosted | Local |
| --- | --- | --- |
| サーバーの稼働場所 | Microsoft がホストする環境 | 利用者のコンピューター |
| ワークスペース上のセマンティック モデル | 対応 | 対応 |
| Power BI Desktop で開いているモデル | 非対応 | 対応 |
| ディスク上の PBIP・TMDL のモデル定義 | 非対応 | 対応 |
| サーバーの導入・更新 | 利用者によるインストールは不要。更新は Microsoft が管理 | 拡張機能やパッケージを利用者が導入・更新 |

ワークスペース上のセマンティック モデルは、どちらの方式でも操作できますが、インストールが不要で Microsoft によって管理されている Hosted が推奨されています。一方、Power BI Desktop で開いているモデルや、ローカルの PBIP・TMDL を扱う場合は Local を利用します。

> [!NOTE]
> Authoring MCP サーバーが扱うのは、モデリングに関する操作です。レポートのページやビジュアル、モデル ビューの図のレイアウトは変更できません。
>
> 参考情報: [Power BI 作成用 MCP サーバー - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/mcp/power-bi-authoring-mcp)
> 参考情報:[GitHub - microsoft/powerbi-modeling-mcp](https://github.com/microsoft/powerbi-modeling-mcp)

### Power BI Consumption MCP

Power BI Consumption MCP サーバーは、AI エージェントがワークスペース上のセマンティック モデルに問い合わせるための MCP サーバーです。

Consumption MCP サーバーでは、以下のツールが提供されています。

| ツール | 内容 |
| --- | --- |
| クエリ実行ツール<br>（Execute Query tool） | セマンティック モデルに対して DAX クエリを実行し、結果を AI エージェントに返す |
| セマンティック モデル スキーマの取得ツール<br>（Get Semantic Model Schema tool） | テーブル、列、メジャー、リレーションシップなど、セマンティック モデルの構造を取得する |
| レポート メタデータの取得ツール<br>（Get Report Metadata tool） | 既存レポートのページ、ビジュアル、フィルターなどのメタデータを取得する |
| クエリ生成ツール<br>（Generate Query tool） | Power BI の Copilot を使って、自然言語の質問から DAX クエリを生成する |

たとえば、対象のセマンティック モデルを指定し、売上が多い上位 10 製品を調べるよう AI エージェントに指示できます。


なお、日本語ドキュメントの「従量課金」という表記については、既存のデータを利用する用途を示す名称であり、呼び出しごとの課金方式を表すものではありません。

また、データへの問い合わせに利用する MCP サーバーについては、次の　Fabric IQ MCP が推奨されています。

> セマンティック モデルを使用する場合は、[Fabric IQ MCP サーバー](https://learn.microsoft.com/ja-jp/fabric/iq/connectors/fabric-iq-mcp)を使用することが推奨されています。 Fabric IQ は、ビジネス データとコンテキストを、Power BIセマンティック モデルとレポートから AI クライアントに取り込むための主要な MCP サーバーです。
>
> 参考情報:[Power BI 従量制 MCP サーバーのセットアップ - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/mcp/remote-mcp-server-get-started)

### Fabric IQ MCP

Fabric IQ MCP は、AI エージェントが Power BI の既存レポートやセマンティック モデルを探し、そのデータに問い合わせるためのリモート MCP サーバーです。読み取り専用のツールを提供しており、モデルやレポートの作成・変更は行いません。

Fabric IQ MCP サーバーでは、以下のツールが提供されています。

| ツール | 内容 |
| --- | --- |
| `DiscoverArtifacts` | 名前で Power BI のレポートやセマンティック モデルを検索する |
| `ResolveFabricItem` | 対応するアイテムの URL から、ほかのツールで使用する対象を特定する |
| `GetReportMetadata` | レポートのメタデータを取得する |
| `GetSemanticModelSchema` | セマンティック モデルのスキーマ情報を取得する |
| `ValueSearch` | セマンティック モデル内の特定の格納値を検索する |
| `ExecuteQuery` | セマンティック モデルに対して DAX クエリを実行する |

たとえば、売上レポートを名前で探し、そのデータから直近の四半期の地域別売上を調べるよう AI エージェントに指示できます。


> 参考情報: [Fabric IQ MCPサーバーを始めましょう - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/iq/connectors/fabric-iq-mcp)

<div align="center">
<img src="powerbi_mcp_servers.png" alt="Power BI の MCP サーバーの役割と接続先" width="1200" style="max-width: 100%; height: auto;">
</div>

---

<a id="agentic"></a>

## Power BI Agentic とは

Power BI Agentic は、AI エージェントによる Power BI のモデルやレポートの開発を支援する、スキルとツール群の呼び名です。スキルは作業の進め方を示し、ツールはモデルの変更などの操作を実行する手段を提供します。GitHub Copilot などの AI エージェントは、これらを組み合わせて開発を進めます。

### エージェント プラグインとは

エージェント プラグインは、スキルや MCP サーバーの設定などをまとめて導入できる、AI エージェント向けの拡張パッケージです。

Power BI Agentic の利用を始めるには、`powerbi-authoring` プラグインの導入が推奨されています。このプラグインをインストールすると、モデル用・レポート用の2つのスキルと、Local の Authoring MCP サーバーの登録設定をまとめて追加できます。

### スキルとツールの役割

それぞれの役割は、以下のように整理できます。

| 構成要素 | 役割 | 例 |
| --- | --- | --- |
| AI エージェント | 利用者の指示を受け、スキルを参照し、ツールを呼び出して作業を進める | GitHub Copilot、Claude Code、Cursor など |
| スキル | AI エージェントが必要に応じて読み込む指示・スクリプト・参考資料を通じて、作業の進め方や判断基準を示す | `semantic-model-authoring`、`powerbi-report-cli` |
| ツール | モデルの確認・変更、DAX の実行、レポート定義の検証、Desktop の操作などを実行する | 各 MCP サーバーが提供するツール（例: クエリ実行ツール、セマンティック モデル スキーマの取得ツール 等） |


> [!NOTE]
> 参考情報: [Power BI Agentic の概要 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/agentic/power-bi-agentic-overview)
> 参考情報: [skills-for-fabric/plugins/powerbi-authoring/skills/powerbi-report-cli](https://github.com/microsoft/skills-for-fabric/blob/a31549e4690e03b78c507c7a81cebdbe0caefc5b/plugins/powerbi-authoring/skills/powerbi-report-cli/references/authoring.md)

### 主なスキルと役割

Power BI Agentic の主なスキルには、モデルの作成・変更を支援するものと、レポートの設計・作成・公開を支援するものがあります。


| スキル | 主な役割 |
| --- | --- |
| `semantic-model-authoring` | セマンティック モデルの作成・変更、DAX の記述・検証、モデルの配置や更新などの進め方を示す |
| `powerbi-report-cli` | レポートの要件整理・設計、PBIR 定義の編集・検証、Fabric への公開・管理の進め方を示す |

`powerbi-report-cli` は、以前は個別に提供されていた4つのレポート用スキル（planning・design・authoring・management）を統合したものです。統合後は、各スキルが担っていた役割が、以下の4つの「モード」として用意されています。AI エージェントは、指示された内容に応じてモードを使い分けます。

> [!NOTE]
> Microsoft Learn では、レポート用の機能が4つのスキルとして紹介されていますが、本記事では、GitHub の公開スキル定義に基づき、統合後の `powerbi-report-cli` と4つのモードを説明します。

| モード | 主な役割 |
| --- | --- |
| `planning` | 新規レポートの要件や対象範囲を整理し、仕様をまとめる |
| `design` | グラフの種類、レイアウト、色、フォント、アクセシビリティなどの設計方針をまとめる |
| `authoring` | PBIR 定義のページ・ビジュアル・フィルターなどを作成・変更し、検証する |
| `management` | ワークスペース上のレポートや定義を取得・公開・更新・削除し、接続先モデルの変更などを扱う |


たとえば、新規レポートを要件整理から作成する場合、AI エージェントはスキルに記載された手順に沿って、次のように作業を進めます。


1. **要件とモデルの確認**: `planning` で、レポートの利用者・目的・対象範囲を整理します。モデルの構造の確認には、`semantic-model-authoring` を利用します。
2. **設計と仕様の承認**: `design` でグラフやレイアウトを具体化し、仕様をまとめて利用者の承認を得ます。
3. **実装と検証**: `authoring` でレポートを作成し、定義や Desktop での表示を確認します。必要なモデル変更は `semantic-model-authoring` が担当します。
4. **必要に応じた公開**: 利用者が公開を指示・承認した場合に、`management` でワークスペースへレポートを公開します。

たとえば、メジャーの追加にはモデル用スキルを、既存ページの色や配置の変更にはレポート用スキルの `authoring` モードを利用します。

> [!NOTE]
> 参考情報: [skills-for-fabric/plugins/powerbi-authoring/skills/powerbi-report-cli](https://github.com/microsoft/skills-for-fabric/blob/a31549e4690e03b78c507c7a81cebdbe0caefc5b/plugins/powerbi-authoring/skills/powerbi-report-cli/SKILL.md)
> 参考情報:[skills-for-fabric](https://github.com/microsoft/skills-for-fabric/blob/a31549e4690e03b78c507c7a81cebdbe0caefc5b/CHANGELOG.md)

---

<a id="installation"></a>

## Power BI MCP・プラグインの導入方法

以下に、MCP サーバーとプラグインの導入手順を確認できる公開情報をまとめます。Authoring MCP、`powerbi-authoring` プラグイン、Consumption MCP の参照先には、Windows 上の VS Code と GitHub Copilot を使った手順が記載されています。Fabric IQ MCP の参照先には、GitHub Copilot CLI を使った接続・認証・確認の手順が記載されています。

導入手順や前提条件は、利用する MCP サーバーやクライアントに応じて、以下の公開情報をご参照ください。

| 導入対象 | 手順の参照先 |
| --- | --- |
| Authoring MCP サーバー（Hosted） | [Power BI 作成用 MCP サーバー - Power BI \| Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/mcp/power-bi-authoring-mcp#set-up-the-hosted-server) 「ホストされるサーバーを設定する」 |
| Authoring MCP サーバー（Local） | [Power BI 作成用 MCP サーバー - Power BI \| Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/mcp/power-bi-authoring-mcp#set-up-the-local-server) 「ローカル サーバーを設定する」 |
| Consumption MCP サーバー | [Power BI 従量制 MCP サーバーのセットアップ - Power BI \| Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/mcp/remote-mcp-server-get-started) |
| Fabric IQ MCP サーバー | [Fabric IQ MCPサーバーを始めましょう - Microsoft Fabric \| Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/iq/connectors/fabric-iq-mcp)（GitHub Copilot CLI の手順） |
| `powerbi-authoring` プラグイン | [Power BI Agentic の概要 - Power BI \| Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/agentic/power-bi-agentic-overview) |

> [!NOTE]
> Authoring MCP サーバーでは、Hosted と Local の同時登録を避け、用途に応じてどちらか一方を利用することが推奨されています。両方を登録するとツールが重複し、AI エージェントがどちらを使うか判断しにくくなり、また、リクエストごとのトークン消費も増えるためです。
>
> 参考情報:[Power BI 作成用 MCP サーバー - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/mcp/power-bi-authoring-mcp#choose-hosted-or-local)

プラグインの導入については、VS Code ではエージェント カスタマイズ エディターの「プラグイン」で `powerbi-authoring` を検索できます。以下は、プラグインの検索画面です。

![エージェント カスタマイズ エディターで powerbi-authoring プラグインを検索してインストールする画面](powerbi-authoring-plugin-install.png)

---

<a id="desktop-tools"></a>

## Power BI Desktop Bridge

Power BI Desktop Bridge は、外部ツールや AI エージェントから、同じコンピューター上で起動している Power BI Desktop を操作するための機能です。

効果的な活用例の1つが、AI エージェントによる PBIP のレポート編集後の表示確認です。AI エージェントは、`powerbi-report-cli` の `authoring` モードでグラフの追加や色・配置の変更を行います。その後、Desktop Bridge を使ってレポート定義を Desktop に読み込み直し、スクリーンショットで表示を確認します。

上記の例では、利用者は対象のレポートと変更したい内容をエージェントに指示します。再読み込みやスクリーンショット取得に必要なコマンドは、エージェントがスキルの手順に従って実行するため、利用者がこれらのコマンドを逐一入力する必要は基本的にありません。

こうした Desktop の操作には、`powerbi-desktop` CLI を使います。コマンドは AI エージェントから実行するほか、利用者が手動で実行することもできます。代表的なコマンドは、以下のとおりです。

| コマンド | 概要 |
| --- | --- |
| `status` | 起動中の Desktop と、開いているファイルや Bridge の接続状態を確認する |
| `open` | 指定した PBIX または PBIP ファイルを Desktop で開く |
| `reload` | 外部で変更した PBIP のレポート定義を Desktop に読み込み直す |
| `screenshot` | 指定したレポートページを PNG 画像として取得する |

Bridge を利用するには、Power BI Desktop 側で Bridge が有効になっている必要があります。Desktop 側の設定や CLI の導入手順、各コマンドの引数・オプションなどの詳細は、以下の公開情報をご参照ください。

> [!NOTE]
> 参考情報: [Power BI デスクトップ ブリッジとは (プレビュー) - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/agentic/power-bi-desktop-bridge-overview)
> 参考情報:[Visual Studio Code Power BIデスクトップ プロジェクト ファイルを編集する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/projects/projects-external-editing)
> 参考情報:[Secure AI-assisted development in VS Code](https://code.visualstudio.com/docs/copilot/security)

<div align="center">
<img src="powerbi_desktop_bridge.png" alt="Power BI Desktop Bridge を使ったレポート編集と表示確認の流れ" width="1200" style="max-width: 100%; height: auto;">
</div>

---

<a id="file-formats"></a>

## PBIX・PBIP の使い分け

Power BI Desktop の保存形式には、PBIX と Power BI Project（PBIP）があります。PBIX は、レポートやモデルを1つのファイルに保存する形式で、PBIP は、レポートやモデルの定義をフォルダー内のテキストファイルに保存する形式です。

Power BI Desktop のモデルやレポートを AI エージェントで扱う場合、必要な保存形式は作業内容によって異なります。以下に、PBIX のまま利用できる作業と、PBIP が必要な作業をまとめます。

| 行う作業 | Desktop の保存形式 |
| --- | --- |
| Local の Authoring MCP サーバーで Desktop のモデルを確認・変更したり、DAX クエリを実行したりする | PBIX のままで利用可能。 |
| Power BI Agentic のレポート用スキル `powerbi-report-cli` の `authoring` モードで、ローカルのレポートのページやビジュアルを作成・変更する | PBIP が必要。レポート定義は PBIR 形式。 |
| テーブルやリレーションシップの定義を VS Code 等で編集し、Git で差分管理する（MCP は任意） | PBIP が必要。モデル定義は TMDL 形式。 |

> [!NOTE]
> ワークスペース上のセマンティック モデルに接続する場合は、Desktop の保存形式にかかわらず MCP で利用できます。（Authoring MCP サーバーの Hosted・Local、Consumption MCP サーバー、Fabric IQ MCP サーバー。）
>
> 参考情報: [MCP サーバーの概要 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/mcp/mcp-servers-overview)

### PBIX のまま利用できる場合

Local の Authoring MCP サーバーで Desktop に接続する場合、操作対象は Desktop に読み込まれたモデルです。そのため、PBIX のままモデルの確認・変更や DAX クエリの実行に利用できます。

たとえば、既存の PBIX を Desktop で開き、そのモデルに接続してメジャーを追加し、DAX クエリで計算結果を確認できます。

> [!NOTE]
> 参考情報: [Power BI セマンティック モデル作成スキル - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/agentic/semantic-model-authoring-skill-overview)

### PBIP にする必要がある場合

たとえば、Power BI Agentic のレポート用スキル `powerbi-report-cli` の `authoring` モードで、ローカルのレポートにページやグラフを追加したり、配置や色を変更したりする場合は、PBIP が必要です。

AI エージェントは、スキルの指示に従って、PBIP のフォルダー内にある **PBIR 形式のレポート定義ファイル**を編集します。

なお、PBIP は MCP を使わない場合にも活用できます。モデル定義（TMDL）の編集、レポート定義（PBIR）を使ったページの再利用、Git による差分・変更履歴の管理などが代表例です。

PBIP の保存方法や、このほかの活用例、外部編集に対応するファイル・操作の詳細は、以下の公開情報をご参照ください。

> [!NOTE]
> 参考情報: [Power BI Desktop プロジェクト (PBIP) - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/projects/projects-overview)
> 参考情報: [Power BI Desktop プロジェクト レポート フォルダー - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/projects/projects-report)
> 参考情報: [Visual Studio Code Power BIデスクトップ プロジェクト ファイルを編集する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/projects/projects-external-editing)

---

<a id="conclusion"></a>

## おわりに

本ブログでは、Power BI の MCP サーバーと Power BI Agentic の役割、および導入方法についてご紹介しました。

モデルの作成・変更には Authoring MCP を利用します。Consumption MCP では、ワークスペース上のセマンティック モデルに問い合わせることができます。現在、既存のレポートやモデルのデータについて質問する場合には、Fabric IQ MCP の利用が推奨されています。

モデルやレポートの開発には、Power BI Agentic のスキルとツールも活用できますので、利用したい作業に合わせて環境を準備し、Power BI と AI エージェントの連携をお試しください。

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**

Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。

※ 所要時間は1分程度となります。

[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)

