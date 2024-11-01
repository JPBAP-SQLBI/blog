---
title: Microsoft Fabric Capacity Metrics アプリの見方
date: 2024-10-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Microsoft Fabric
  - Power BI Premium
  - 容量
  - Microsoft Fabric Capacity Metrics アプリ
---


こんにちは、Power BI サポート チーム 金沢です。
Microsoft Fabric Capacity Metrics アプリは、Microsoft Fabric や Premium の容量を監視し、リソースの使用状況を把握するためのアプリです。
これにより、キャパシティの消費量を確認し、必要に応じてスケールアップや最適化の判断ができます。アプリには様々なデータが表示されるため、何を見たらよいか困惑することもあるかと思います。
そこで今回は、Microsoft Fabric Capacity Metrics アプリの各データの見方をご紹介します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


---
## 目次
---
- [目次](#目次)
- [1. Microsoft Fabric Capacity Metrics アプリの概要](#1-microsoft-fabric-capacity-metrics-アプリの概要)
    - [1-1. 使用要件](#11-使用要件)
    - [1-2. インストール方法](#1-2-インストール方法)
- [2.Microsoft Fabric Capacity Metrics アプリの各アイテムの見方](#2-microsoft-fabric-capacity-metrics-アプリの各アイテムの見方)
    - [2-1.コンピューティング ページ](#21-コンピューティング-ページ)
    - [2-2.ストレージ ページ](#2-2-ストレージ-ページ)

---
## 1. Microsoft Fabric Capacity Metrics アプリの概要
---

Microsoft Fabric Capacity Metrics アプリは、Microsoft Fabric や Premium の容量を監視し、リソースの使用状況を把握するためのアプリです。

## 1.1 使用要件

Microsoft Fabric Capacity Metrics アプリをご使用いただくには、容量管理者である必要があります。容量管理者になるには、すでに容量管理者となっているユーザーに容量管理者へ追加してもらう必要がございます。容量管理者へ追加する操作の詳細については、参考情報をご参照ください。

>[!NOTE]
> 参考情報：[Fabric 容量を管理する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/capacity-settings?tabs=power-bi-premium#add-and-remove-admins)

また、Entra ID アカウントに、グローバル管理者、Fabric 管理者、またはPower Platform 管理者のロールが付与されている場合は、容量管理者の権限も付与されております。

なお、Microsoft Fabric Capacity Metrics アプリを使用できる容量は、Premium、Fabric、Embedded、Fabric 試用版です。Pro ライセンスで作成できる共有容量や Premium Per User の容量については、Microsoft Fabric Capacity Metrics アプリで確認できません。

## 1-2. インストール方法

Microsoft Fabric Capacity Metrics アプリをインストールし、各容量の使用状況を表示する手順を紹介します。

### 1-2-1. Microsoft Fabric Capacity Metrics アプリのインストール

[アプリ]＞[Microsoft Fabric Capacity Metrics]よりインストールします。
※アプリ一覧に表示されない場合は[Microsoft Fabric Capacity Metrics]を検索してください。

<div align="center">
<img src="FCMアプリのインストール方法.png">
図1. アプリのインストール方法
</div>

### 1-2-2. Capacity ID を取得

[管理ポータル]>[容量の設定]より、アプリを使用したい容量を選択します。

<div align="center">
<img src="FCM容量IDの取得1.png">
図2. 容量の表示
</div>

容量の詳細画面の、URL内の、/capacities/ の後の文字列が Capacity ID のため、この部分をコピーします。
たとえば、https ://app.powerbi.com/admin-portal/capacities/9B77CC50-E537-40E4-99B9-2B356347E584 という URL の容量 ID は9B77CC50-E537-40E4-99B9-2B356347E584 です。

### 1-2-3. 容量へ接続

Microsoft Fabric Capacity Metrics アプリを開き、[接続]を選択します。[詳細オプション]の[CapacityID]へ、2 で取得した Capacity ID をペーストし、[UTC_offset]へタイムゾーンを 14 から -12 の値を設定します。日本のタイムゾーンに設定したい場合は、日本時間が UTC+9 のため、9 を設定します。その他の設定は規定値のままでご使用いただけます。[次へ]を選択し、[サインインして続行]を選択します。

アプリを構成した直後では、アプリがデータを取得するまでに数分かかることがあるため、アプリを実行してもデータが表示されない場合があります。この場合は時間をおいてアプリを更新すると表示されます。

>[!NOTE]
> 参考情報：[Microsoft Fabric Capacity Metrics (Microsoft Fabric 容量メトリック) アプリをインストールする - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app-install?tabs=1st)


---
## 2. Microsoft Fabric Capacity Metrics アプリの各アイテムの見方
---

Microsoft Fabric Capacity Metrics アプリには、コンピューティング ページ（[Compute]タブ）とストレージ ページ（[Storage]タブ）があります。それぞれのページについて、次の節で説明します。

<div align="center">
<img src="FCMページ.png">
図3. Microsoft Fabric Capacity Metrics アプリのタブ
</div>

### 2.1 コンピューティング ページ

コンピューティング ページは、複数メトリックのリボン グラフ、容量使用率と調整、項目と操作別のマトリックスから構成され、以下の項で説明します。
2-1-1：複数メトリックのリボン グラフ
2-1-2：容量使用率と調整
2-1-3：項目と操作別のマトリックス

<div align="center">
<img src="コンピューティングページ.png">
図4. コンピューティング ページ
</div>

#### 2-1-1. 複数メトリックのリボン グラフ

複数メトリックのリボン グラフでは、CU 、期間 [Duration]、操作[Operation]、ユーザ[Users]について過去 14 日間の利用状況を閲覧できます。

CU タブは、容量ユニット (CU) の処理時間 (秒単位) を表示します。
積み上げ棒グラフの上でマウスをかざすと、その日、そのアイテムのCU処理時間が表示されます。また、ドリルダウンすることで時間別の各アイテムの CU 処理時間が表示されます。

期間タブは処理時間 (秒) を表示します。
積み上げ棒グラフの上でマウスをかざすと、その日、そのアイテムの処理時間が表示されます。また、ドリルダウンすることで時間別の各アイテムの処理時間が表示されます。

操作タブは操作が行われた回数を表示します。
積み上げ棒グラフの上でマウスをかざすと、その日、そのアイテムの操作回数が表示されます。また、ドリルダウンすることで時間別の各アイテムの操作回数が表示されます。

ユーザータブは操作を実行したユーザーの数を表示します。
積み上げ棒グラフの上でマウスをかざすと、その日、そのアイテムで操作を実行したユーザー数が表示されます。また、ドリルダウンすることで時間別の各アイテムのユーザー数が表示されます。

#### 2-1-2. 容量使用率と調整

容量使用率と調整では、稼働率[Utilization]　、調整[Throttling]、超過分[Overages]、システム イベント[System Events]について過去14日間の利用状況を閲覧できます。

稼働率は各時間の CU の使用状況を表示します。バックグラウンド型と対話型のそれぞれについて、課金対象と課金対象外の CU 消費量を閲覧できます。また、オートスケールを設定している場合は、オートスケールされた容量での CU 消費量も表示されます。なお、フィールドを選択し、[Explore]を押すと、各 CU 消費量の詳細をテーブルにて確認できます。
バックグラウンド型と対話型について、またオートスケールについては以下の公開情報に詳細が記載されています。

>[!NOTE]
> 参考情報：[Fabric の操作 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/fabric-operations)
> 参考情報：[Power BI Premium で自動スケーリングを使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-auto-scale)

調整は各時間のスロットリングの発生状況を表示します。スロットリングの発生状況は、対話型遅延、対話型拒否、バックグラウンド拒否の3種のタブで確認できます。スロットリングの詳細については、以下のブログ記事にてまとめられています。

>[!NOTE]
> 参考情報：[Premium / Fabric 容量のスロットリングについて | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_throttling/)

超過分は現在の容量を超過して利用している場合に、その使用率を表示します。Power BI では購入した容量で使用可能なリソースを超えた場合、将来の 10 分間で使用するリソースを前借して使用するため、この前借分が超過分として表示されます。容量の消費量が減少した後は、前借した容量を返済するまで、このグラフ上で超過分として表示されます。
容量を将来の 10 分間分を超えて消費し、スロットリングが発生した場合はこのグラフが 100% として表示されます。容量の消費量を減らす対処策を実施した後、前述の前借分を返済し始めるとグラフの値が減少します。
このグラフではフィールドを選択し、[Explore]を押すと、各項目の詳細をテーブルにて確認できます。

システム イベントは容量の一時停止や再開のイベントを表示します。容量の状態が過去 14 日間変更されていない場合は、このテーブルは空白で表示されます。

#### 2-1-3. 項目と操作別のマトリックス

項目と操作別のマトリックスでは、容量の各アイテムのメトリックが表示されます。このマトリックスでは、データフロー等のアイテム別に、CU 処理時間やユーザー数を閲覧できます。アイテムがオレンジ色、赤色の場合は以前と比較してパフォーマンスが悪化していることを示しております。

>[!NOTE]
> 参考情報：[メトリック アプリのコンピューティング ページについて - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app-compute-page)

### 2-2. ストレージ ページ

ストレージ ページでは選択した容量内の Fabric アイテムに対する、カード、課金対象ストレージ別の上位ワークスペース (%)　、日付別ストレージ (GB) 、日付別の累積課金対象ストレージ (GB) が表示されます。それぞれの項目について以下の項で説明します。
2-2-1：カード
2-2-2：課金対象ストレージ別の上位ワークスペース (%)
2-3-3：日付別ストレージ (GB)
2-4-3：日付別の累積課金対象ストレージ (GB)

<div align="center">
<img src="ストレージページ.png">
図5. ストレージ ページ
</div>

#### 2-2-1. カード

カードでは、ワークスペース、現在のストレージ (GB) 、課金対象ストレージ (GB) について表示されます。
ワークスペースは、 [Workspace]で表示されるカードで、ストレージを使用するワークスペースの合計数を表示します。
現在のストレージ (GB) は、 [Current storage (GB) ]で表示されるカードで、現在使用しているストレージを GB 単位で表示します。
課金対象ストレージ (GB) は、 [Billable storage (GB) ]で表示されるカードで、現在使用している課金対象ストレージを GB 単位で表示します。


#### 2-2-2. 課金対象ストレージ別の上位ワークスペース (%)

各ワークスペースの、操作名、削除の状態、課金の種類、現在のストレージ (GB) 、課金対象のストレージ (GB) 、課金対象のストレージ (%) を表示します。ストレージサイズが大きい順に並べられています。

#### 2-3-3. 日付別ストレージ (GB)

過去30日間の日別の平均ストレージ サイズを GB 単位で表示します。ドリルダウンすることで、時間別のストレージ サイズを閲覧できます。

#### 2-3-4. 日付別の累積課金対象ストレージ (GB)

過去30日間の日別の累積課金対象ストレージサイズを GB 単位で表示します。 これは、選択した日付における課金対象ストレージの合計値を計算しています。

>[!NOTE]
> 参考情報：[メトリック アプリのストレージ ページについて - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app-storage-page)




以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)