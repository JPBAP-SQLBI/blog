---
title: 監査ログを活用した Power BI 有償ライセンスの利用状況確認方法
date: 2026-04-30 00:00:00
tags:
  - Power BI
  - Power BI Pro
  - PPU
  - Power BI サービス
  - Admin
  - Audit Log
  - License
  - 監査ログ
  - ライセンス
  - 管理者
  - 棚卸
  - Premium Per User
---

こんにちは、Power BI サポート チームの山崎です。

Power BI の有償ライセンス（Pro / Premium Per User）の棚卸のため、「ライセンスを割り当てたユーザーが、実際に有償ライセンス固有の機能を利用しているかどうかを確認したい」というお問い合わせを多くいただきます。Microsoft 365 管理センターではライセンスの割り当て状況は確認できますが、割り当て済みのユーザーが本当にそのライセンスを必要とする操作を行っているかまでは判断できません。

本ブログでは、監査ログを活用して有償ライセンスが必要な操作を行っているユーザーを特定する方法をご紹介いたします。未使用ライセンスの把握やコスト最適化にお役立てください。

<!-- more -->

> [!NOTE]
> 本記事では Power BI Pro および Premium Per User (PPU) をまとめて「有償ライセンス」と表記します。監査ログの確認方法はどちらのライセンスでも同じ手順で実施いただけます。

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---

## <font color="DodgerBlue">有償ライセンスが必要な操作とは</font>

まず、有償ライセンス（Pro / PPU）が必要となる操作と、不要な操作を整理いたします。

### <font color="HotPink">有償ライセンスが不要な操作</font>

- **Power BI Desktop の利用**: Power BI Desktop はライセンスの有無にかかわらずインストール・利用が可能です。Desktop の起動ログのみでは有償ライセンスの利用実績を判別することはできません。
- **マイ ワークスペースでの操作**: 各ユーザーに割り当てられるマイ ワークスペースでの操作（レポートの作成・データの更新など）は、Fabric (Free) ライセンスでも実行可能です。

### <font color="HotPink">有償ライセンスが必要な代表的な操作</font>

- **共有ワークスペースへのレポート発行**: 他のユーザーと共同利用する共有ワークスペースにレポートを発行するには、Pro または PPU ライセンスが必要です。
- **共有ワークスペース内のセマンティック モデルの更新**: 共有ワークスペースにあるセマンティック モデル（データセット）の更新操作も同様です。
- **コンテンツの共有**: レポートやダッシュボードを他のユーザーに共有する操作には有償ライセンスが必要です。
- **アプリの発行**: 組織内にアプリとしてコンテンツを配布する操作にも有償ライセンスが必要です。
- **Pro 容量ワークスペースのコンテンツ閲覧**: Premium 容量や Fabric 容量に割り当てられていない共有ワークスペース（Pro 容量）では、レポートの閲覧だけでも Pro または PPU ライセンスが必要です。

> [!NOTE]
> Premium 容量（P SKU）や Fabric 容量（F64 以上）に割り当てられたワークスペースでは、閲覧者は Fabric (Free) ライセンスでもコンテンツを参照可能です。ただし、コンテンツの作成・発行・共有を行うユーザーには引き続き有償ライセンスが必要です。**一方、これらの容量に割り当てられていない共有ワークスペース（Pro 容量）では、閲覧のみのユーザーにも有償ライセンスが必要です。**

このように、**有償ライセンスが実際に必要かどうかは「共有ワークスペース上で特定の操作を行っているかどうか」が判断基準**となります。ただし、Pro 容量のワークスペースでは閲覧も有償ライセンスが必要な操作に含まれる点にご注意ください。

---

## <font color="DodgerBlue">監査ログの概要</font>

Power BI の操作は **監査ログ** として記録されます。監査ログを確認することで、どのユーザーがいつどのような操作を行ったかを把握できます。

### <font color="HotPink">監査ログの確認方法</font>

監査ログは以下の方法で取得できます。

1. **Microsoft Purview ポータル**: Web UI から対話形式で検索・取得できます。
2. **PowerShell（Get-PowerBIActivityEvent コマンドレット）**: コマンドラインからアクティビティ ログを取得できます。

本記事では、Microsoft Purview ポータルでの検索手順を中心にご説明し、PowerShell による取得方法についても概要をご紹介いたします。

> [!NOTE]
> 監査ログの検索には、Fabric 管理者ロールまたは監査ログの閲覧権限が必要です。また、監査ログは最大 180 日間（E5 ライセンスの場合は 1 年間）保持されます。

---

## <font color="DodgerBlue">監査ログで有償ライセンスの利用実績を確認する方法</font>

有償ライセンスの利用実績を確認するためには、「共有ワークスペースでの操作」を示す監査ログを検索します。以下に、代表的な監査ログのアクティビティを紹介いたします。

### <font color="HotPink">確認すべき主要なアクティビティ</font>

| アクティビティ（フレンドリ名） | 操作名 | 概要 |
|---|---|---|
| Power BI レポートの作成 | CreateReport | ワークスペースへのレポート発行 |
| 要求された Power BI セマンティック モデルの更新 | RefreshDataset | セマンティック モデルの手動更新 |
| 共有 Power BI レポート | ShareReport | レポートの共有 |
| Power BI アプリの作成 | CreateApp | アプリの発行 |
| Power BI レポートの表示 | ViewReport | レポートの閲覧（※下記注記参照） |

> [!NOTE]
> `ViewReport`（レポートの閲覧）は、Pro 容量ワークスペースで閲覧のみを行っているユーザーの利用実績を把握するために有効です。Premium 容量や Fabric 容量（F64 以上）のワークスペースでは閲覧に有償ライセンスが不要なため、お客様の環境に応じて監査対象に含めるかどうかをご判断ください。なお、`ViewReport` は記録件数が多くなる傾向がありますので、集計時にはユーザー単位での重複排除をご検討ください。

### <font color="HotPink">手順: Microsoft Purview ポータルでの検索</font>

1. [Microsoft Purview ポータル](https://purview.microsoft.com/) にアクセスし、管理者アカウントでサインインします。

2. **[監査ソリューション]** カードを選択します。

3. 検索条件を以下のように設定します。
   - **日付範囲**: 棚卸対象の期間
   - **アクティビティ**: 前述の主要なアクティビティ表を参考に、確認したいアクティビティを選択（例: 「Power BI レポートの作成」（CreateReport）など）

  ![監査ログの検索条件設定画面](1.png)

4. **[検索]** をクリックすると、該当する操作の一覧が出力されます。

5. 検索結果を CSV でエクスポートし、ログに記録されているユーザーを確認します。

### <font color="HotPink">マイ ワークスペースの操作を除外する</font>

監査ログには、マイ ワークスペースでの操作も含まれます。有償ライセンスが不要なマイ ワークスペースの操作を除外するには、エクスポートした CSV の **AuditData** カラムに含まれる **WorkSpaceName** の値を確認してください。

- `WorkSpaceName` が `PersonalWorkspace-xxxx` の形式 → **マイ ワークスペース**での操作（除外対象）
- それ以外 → **共有ワークスペース**での操作（有償ライセンスが必要な操作）

AuditData カラムは JSON 形式の文字列となっているため、データの抽出にはひと手間必要です。弊社ブログにて AuditData カラムからの詳細情報の抽出方法をご紹介しておりますので、あわせてご参照ください。

> 参考: [監査ログのAuditDataカラムからデータを抽出する方法 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_Extracting_Data%20from_AuditLogs/)

### <font color="HotPink">PowerShell を使って取得する方法</font>

PowerShell の `Get-PowerBIActivityEvent` コマンドレットでも同等のアクティビティを取得可能です。このコマンドレットで取得できるデータは Microsoft Purview の統合監査ログに由来する同一のものですが、Power BI REST API を経由してアクセスするため、取得可能な期間は**最大 4 週間**となります。棚卸の対象期間がこれを超える場合は、前述の Microsoft Purview の監査ログをご利用ください。

具体的な利用手順やスクリプト例については、以下の弊社ブログおよび公式ドキュメントをご参照ください。

> 参考:
> - [Power BI のユーザーアクティビティ追跡方法の比較 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_activity_log_usage_metrics/)
> - [Get-PowerBIActivityEvent | Microsoft Learn](https://learn.microsoft.com/ja-jp/powershell/module/microsoftpowerbimgmt.admin/get-powerbiactivityevent)
> - [Access the Power BI activity log | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/admin-activity-log)

---

## <font color="DodgerBlue">有償ライセンス棚卸の全体フロー（参考例）</font>

以下は、有償ライセンスの棚卸を行う際の運用フローの一例としてご紹介いたします。お客様の環境やポリシーに合わせて適宜ご調整ください。

### <font color="HotPink">Step 1: ライセンスの割り当て状況を確認する</font>

Microsoft 365 管理センターの **[課金] > [ライセンス]** から、Power BI Pro および Premium Per User ライセンスが割り当てられているユーザーの一覧を取得します。

> 参考: [ライセンスとワークスペースの運用・棚卸方法 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_tanaoroshi/)

### <font color="HotPink">Step 2: 監査ログで利用実績を確認する</font>

前述の方法で、お客様の環境に応じたアクティビティの監査ログを取得し、マイ ワークスペースの操作を除外します。

### <font color="HotPink">Step 3: 突合せを行う</font>

Step 1 のライセンス割り当て一覧と Step 2 の利用実績を突合せし、以下のカテゴリに分類します。

| カテゴリ | 説明 | 対応 |
|---|---|---|
| **利用あり** | 共有ワークスペースで操作を行っている | ライセンス継続 |
| **利用なし** | 監査ログに該当操作が存在しない | ライセンスの剥奪を検討（※下記注記参照） |
| **マイ ワークスペースのみ** | マイ ワークスペースでのみ操作を行っている | Fabric (Free) への切り替えを検討 |

> [!WARNING]
> 監査ログの保持期間は限られているため（既定では最大 180 日）、保持期間外の操作は確認できません。棚卸の対象期間と監査ログの保持期間にご留意ください。

> [!IMPORTANT]
> 「利用なし」に分類されたユーザーの中には、Pro 容量ワークスペースでレポートの閲覧のみを行っているユーザーが含まれている可能性があります。`ViewReport` アクティビティも監査対象に含めていない場合は、ライセンスを剥奪する前に対象ユーザーへ利用状況を確認されることをお勧めいたします。

---

## <font color="DodgerBlue">参考情報</font>

- [操作一覧 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/operation-list)
- [Track user activities in Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/powerbi/service-admin-auditing)
- [組織向けの Power BI ライセンス ガイド | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-licensing-organization)
- [ライセンスとワークスペースの運用・棚卸方法 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_tanaoroshi/)
- [監査ログのAuditDataカラムからデータを抽出する方法 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_Extracting_Data%20from_AuditLogs/)
- [ユーザーの操作におけるPower BIのアクティビティログ | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_track_activity_log/)
- [Power BI のユーザーアクティビティ追跡方法の比較 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_activity_log_usage_metrics/)

以上、本ブログが少しでも皆様のお役に立てれば幸いです。

---

## <font color="DodgerBlue">アンケートご協力のお願い</font>

Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。

※ 所要時間は 1 分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)

※ 本情報の内容（添付文書、リンク先などを含む）は、作成日時点でのものであり、予告なく変更される場合があります。
