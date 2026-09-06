---
title: Scanner API と Microsoft Fabric を使用してテナントのメタデータを確認する ① フル スキャンと Power BI レポート
date: 2026-09-07 00:00:00
tags:
  - Power BI
  - Power BI Service
  - Microsoft Fabric
  - Scanner API
---

こんにちは、Power BI サポート チームの亀田です。

Power BI や Microsoft Fabric の利用が広がると、組織内にどのようなワークスペースやアイテムが存在するかを継続的に把握したい場面が増えてきます。

Microsoft Fabric では、Scanner API を使用してテナント内のメタデータを取得できます。本記事では、Scanner API の概要を説明し、Semantic Link (SemPy) と Fabric Notebook を使用してフル スキャンを実行します。取得結果を Lakehouse に保存し、分析テーブル、Direct Lake セマンティック モデル、Power BI レポートを作成するところまでをご紹介します。

増分スキャン、Fabric Data Factory による定期実行、削除済みアイテムの反映などは、第 2 回の記事で説明します。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 目次

* [Scanner API の説明](#Scanner-API-の説明)
  - [取得できる主な情報](#取得できる主な情報)
  - [Scanner API の処理フロー](#Scanner-API-の処理フロー)
* [Notebook からフル スキャンを実行する](#Notebook-からフル-スキャンを実行する)
  - [今回作成する構成](#今回作成する構成)
  - [前提条件](#前提条件)
  - [Lakehouse と Notebook を作成する](#Lakehouse-と-Notebook-を作成する)
  - [Semantic Link を更新する](#Semantic-Link-を更新する)
  - [フル スキャンを実装する](#フル-スキャンを実装する)
  - [実行結果を確認する](#実行結果を確認する)
* [分析テーブルを作成する](#分析テーブルを作成する)
  - [分析用 Notebook](#分析用-Notebook)
  - [分析テーブルを確認する](#分析テーブルを確認する)
* [Power BI レポートを作成する](#Power-BI-レポートを作成する)
  - [Direct Lake セマンティック モデル](#Direct-Lake-セマンティック-モデル)
  - [基本メジャー](#基本メジャー)
  - [レポート ページ](#レポート-ページ)
* [注意事項](#注意事項)
* [おわりに](#おわりに)

## Scanner API の説明

Scanner API は、Power BI および Microsoft Fabric の管理 REST API の一部です。組織内の Fabric アイテムをカタログ化し、ガバナンスや棚卸しに利用できるメタデータを取得します。

Scanner API はデータ ソース内の業務データを取得する API ではありません。取得対象は、ワークスペース、レポート、セマンティック モデル、データフローなどのアイテム情報や、それらの構成を表すメタデータです。

> [!NOTE]
> 参考# [メタデータ スキャンの概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/governance/metadata-scanning-overview)

### 取得できる主な情報

Scanner API では、主に以下の情報を取得できます。

| 分類 | 取得できる情報の例 |
| --- | --- |
| ワークスペース | ID、名前、種類、状態、容量 ID |
| Fabric アイテム | アイテム名、所有者、作成日時、更新日時、秘密度ラベル、保証の状態 |
| Power BI レポート | レポート ID、名前、関連するセマンティック モデル、更新日時 |
| セマンティック モデル | テーブル、列、メジャー、リレーションシップ、ストレージ モード |
| データ ソース | データ ソースの種類、接続先、ゲートウェイとの関連情報 |
| 系列 | 上流および下流のアイテム間の依存関係 |
| 式 | DAX 式、Power Query のマッシュアップ式 |

本記事のサンプルでは、セマンティック モデル スキーマと系列情報を取得します。DAX 式、マッシュアップ式、アイテムのユーザー情報は取得しません。最初の実装では取得範囲と機密情報の取り扱いを必要最小限にします。。

> [!NOTE]
> 参考# [Admin - WorkspaceInfo GetScanResult - REST API (Power BI Power BI REST APIs) | Microsoft Learn](https://learn.microsoft.com/ja-jp/rest/api/power-bi/admin/workspace-info-get-scan-result)

### Scanner API の処理フロー

Scanner API の処理は、以下の 4 つの API で構成されます。

| 順序 | API | 用途 |
| ---: | --- | --- |
| 1 | GetModifiedWorkspaces | スキャン対象となるワークスペース ID を取得する |
| 2 | PostWorkspaceInfo | ワークスペースのスキャンを開始し、scanId を取得する |
| 3 | GetScanStatus | scanId を使用して処理状態を確認する |
| 4 | GetScanResult | 完了したスキャンの結果を取得する |

PostWorkspaceInfo で開始したスキャンは非同期で実行されます。GetScanStatus の結果が Succeeded になるまで待ってから、GetScanResult を呼び出します。

1 回の呼び出しでスキャンできるワークスペースは最大 100 件です。100 件を超える場合は、ワークスペース ID を 100 件ごとに分割します。

本記事では 4 つの API を個別に実装せず、Semantic Link の sempy.fabric.admin パッケージを使用します。scan_workspaces 関数は、PostWorkspaceInfo、GetScanStatus、GetScanResult の呼び出しと状態確認をまとめて実行します。

> [!NOTE]
> 参考# [メタデータのスキャンを実行する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/governance/metadata-scanning-run)https://learn.microsoft.com/ja-jp/rest/api/power-bi/admin/workspace-info-get-scan-result)
> 参考# [sempy.fabric.admin パッケージ - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/python/api/semantic-link-sempy/sempy.fabric.admin?view=semantic-link-python)

## Notebook からフル スキャンを実行する

### 今回作成する構成

第 1 回では、以下の構成を作成します。

```text
Scanner API
    │
    ▼
nb_scanner_metadata (レイクハウス)
    │
    ├── scanner_raw
    └── scanner_runs
          │
          ▼
nb_build_scanner_inventory (ノートブック)
    │
    ├── workspace_inventory
    ├── artifact_inventory
    └── scan_run_inventory
          │
          ▼
sm_scanner_inventory (Direct Lake セマンティック モデル)
          │
          ▼
rpt_scanner_inventory (レポート)
```

すべてのテーブルは、1 つの Lakehouse ”lh_scanner_metadata” に作成します。

<div align="center">
<img src="pbi_scanner_api_1_01.png">
</div>

### 前提条件

本記事のサンプルを実行するには、以下の条件を満たす必要があります。

- Microsoft Fabric 容量に割り当てられたワークスペースを使用できること
- Lakehouse と Notebook を作成できること
- Notebook を実行するユーザーが Fabric 管理者であること
- Fabric 管理ポータルで **[詳細なメタデータを使用して管理者 API の応答を強化する]** が有効であること
- sempy.fabric.admin を含む Semantic Link を利用できること

本記事では DAX 式とマッシュアップ式を取得しないため、**[DAX 式とマッシュアップ式を使用して管理者 API の応答を強化する]** は必須ではありません。

<div align="center">
<img src="pbi_scanner_api_1_02.png">
</div>

> [!WARNING]
> Scanner API の結果には、ユーザー名、メール アドレス、データ ソース情報、セマンティック モデルの構造など、組織内の管理情報が含まれる場合があります。Lakehouse と Notebook へのアクセスは、管理上必要なユーザーに限定してください。

> [!NOTE]
> 参考# [組織でメタデータ スキャンを設定する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/metadata-scanning-setup)

### Lakehouse と Notebook を作成する

1. Fabric 容量に割り当てられたワークスペースを開きます。
2. **[新しい項目]** から Lakehouse を作成します。例として ”lh_scanner_metadata” という名前を使用します。
3. 同じワークスペースで Notebook を作成します。例として ”nb_scanner_metadata” という名前を使用します。
4. Notebook の Lakehouse エクスプローラーから ”lh_scanner_metadata” を追加し、既定の Lakehouse として設定します。
5. Lakehouse を新たに既定として設定した場合は、Notebook のセッションを再起動します。

<div align="center">
<img src="pbi_scanner_api_1_03.png">
</div>

> [!NOTE]
> 参考# [Notebook の使用方法 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-engineering/how-to-use-notebook)
> 参考# [Lakehouse と Delta テーブル - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-engineering/lakehouse-and-delta-tables)

### Semantic Link を更新する

次のコード セルでバージョンとインポートを確認します。
※画像は 2026 年 8 月実行時点でのバージョンです。更新時期によりバージョンが異なる場合がございます。

```python
import sempy
import sempy.fabric.admin as fabric_admin

print(f"Semantic Link version: {sempy.__version__}")
print("sempy.fabric.admin is available.")
```

<div align="center">
<img src="pbi_scanner_api_1_04.png">
</div>

> [!NOTE] 
> 参考# [Semantic Link の概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-science/semantic-link-overview)

Fabric Runtime に含まれる Semantic Link が古い場合、以下のエラーが発生します。

```text
ModuleNotFoundError: No module named 'sempy.fabric.admin'
```

その場合、 Notebook の最初のコード セルで、Semantic Link を更新してください。

```python
%pip install -U semantic-link
```


### フル スキャンを実装する

次のコード セルに、以下のスクリプトを貼り付けます。

このスクリプトは、個人用ワークスペースと非アクティブなワークスペースを除外してフル スキャンを実行します。Scanner API の応答は ”scanner_raw、実行結果は scanner_runs に保存します。

```python
from datetime import datetime, timezone
import json
import sempy.fabric.admin as fabric_admin

RAW_TABLE = "scanner_raw"
RUN_TABLE = "scanner_runs"
BATCH_SIZE = 100

scan_started = datetime.now(timezone.utc).replace(microsecond=0)
scan_started_text = scan_started.isoformat().replace("+00:00", "Z")
run_id = scan_started.strftime("%Y%m%dT%H%M%SZ")

modified_workspaces = fabric_admin.list_modified_workspaces(
    modified_since=None,
    exclude_inactive_workspaces=True,
    exclude_personal_workspaces=True,
)

workspace_ids = (
    modified_workspaces["Workspace Id"]
    .astype(str)
    .tolist()
)

batch_count = (len(workspace_ids) + BATCH_SIZE - 1) // BATCH_SIZE

print(f"Run ID: {run_id}")
print("Scan mode: full")
print(f"Workspace count: {len(workspace_ids)}")
print(f"Batch count: {batch_count}")


raw_schema = """
    run_id string,
    scan_started_utc string,
    scan_mode string,
    modified_since_utc string,
    batch_number int,
    workspace_count int,
    payload_json string
"""

for batch_number, start in enumerate(
    range(0, len(workspace_ids), BATCH_SIZE),
    start=1,
):
    batch_ids = workspace_ids[start:start + BATCH_SIZE]

    print(
        f"Scanning batch {batch_number}/{batch_count}: "
        f"{len(batch_ids)} workspaces"
    )

    scan_result = fabric_admin.scan_workspaces(
        workspace=batch_ids,
        data_source_details=False,
        dataset_schema=True,
        dataset_expressions=False,
        lineage=True,
        artifact_users=False,
        return_dataframe=False,
        retry_after_seconds=30,
        timeout_seconds=900,
        backoff_factor=1.0,
    )

    raw_df = spark.createDataFrame(
        [(
            run_id,
            scan_started_text,
            "full",
            None,
            batch_number,
            len(batch_ids),
            json.dumps(scan_result, ensure_ascii=False),
        )],
        schema=raw_schema,
    )

    (
        raw_df.write
        .format("delta")
        .mode("append")
        .saveAsTable(RAW_TABLE)
    )


completed = datetime.now(timezone.utc).replace(microsecond=0)
completed_text = completed.isoformat().replace("+00:00", "Z")

run_schema = """
    run_id string,
    scan_started_utc string,
    completed_utc string,
    scan_mode string,
    modified_since_utc string,
    workspace_count int,
    batch_count int,
    status string
"""

run_df = spark.createDataFrame(
    [(
        run_id,
        scan_started_text,
        completed_text,
        "full",
        None,
        len(workspace_ids),
        batch_count,
        "Succeeded",
    )],
    schema=run_schema,
)

(
    run_df.write
    .format("delta")
    .mode("append")
    .saveAsTable(RUN_TABLE)
)

print(
    f"Scanner API completed. "
    f"Run ID: {run_id}, Workspaces: {len(workspace_ids)}"
)
```

”scanner_raw” には 1 バッチにつき 1 行を追加します。 ”scanner_runs” には、すべてのバッチが成功した場合だけ 1 行を追加します。

### 実行結果を確認する

初回実行の出力例は以下のとおりです。

```text
Run ID: 20260824T141148Z
Scan mode: full
Workspace count: 28
Batch count: 1
Scanning batch 1/1: 28 workspaces
Scanner API completed. Run ID: 20260824T141148Z, Workspaces: 28
```

Lakehouse を開き、 ”scanner_raw” と ”scanner_runs” が作成されていることを確認します。

<div align="center">
<img src="pbi_scanner_api_1_05.png">
</div>

”scanner_raw.payload_json” には、 workspaces 配列としてワークスペースの情報が保存されています。  
以下のスクリプトを実行することで、実行内容を確認することができます。

```python
from pyspark.sql import functions as F

latest_run = (
    spark.table("scanner_runs")
    .filter(
        (F.col("status") == "Succeeded")
        & (F.col("scan_mode") == "full")
    )
    .orderBy(F.col("scan_started_utc").desc())
    .select("run_id")
    .first()
)

if latest_run is None:
    raise RuntimeError("成功したフル スキャンがありません。")

latest_payload = (
    spark.table("scanner_raw")
    .filter(F.col("run_id") == latest_run["run_id"])
    .orderBy("batch_number")
    .select("payload_json")
    .collect()
)

workspaces = []

for row in latest_payload:
    workspaces.extend(
        json.loads(row["payload_json"]).get("workspaces", [])
    )

display([
    {
        "workspace_id": workspace.get("id"),
        "workspace_name": workspace.get("name"),
        "state": workspace.get("state"),
        "capacity_id": workspace.get("capacityId"),
    }
    for workspace in workspaces
])
```

<div align="center">
<img src="pbi_scanner_api_1_06.png">
</div>

## 分析テーブルを作成する

Power BI から ”payload_json” を直接参照すると、JSON の展開処理がレポート側で必要となります。
変換処理を別の Notebook で行い、ワークスペースとアイテムを分析用 Delta テーブルへ展開します。

### 分析用 Notebook

”nb_build_scanner_inventory” という Notebook を作成し、 ”lh_scanner_metadata” を既定の Lakehouse として設定します。  
本記事ではレポート作成に必要なワークスペースと主要アイテムだけを展開します。列、メジャー、データ ソース、系列の詳細は、今後の拡張として必要に応じて追加できます。
以下がスクリプト例です。

```python
import json

from pyspark.sql import functions as F
from pyspark.sql.types import StringType, StructField, StructType


ARTIFACT_COLLECTIONS = {
    "reports": "Report",
    "datasets": "SemanticModel",
    "dashboards": "Dashboard",
    "dataflows": "Dataflow",
    "datamarts": "Datamart",
    "Lakehouse": "Lakehouse",
    "lakehouses": "Lakehouse",
    "Warehouse": "Warehouse",
    "warehouses": "Warehouse",
    "DataPipeline": "DataPipeline",
    "dataPipelines": "DataPipeline",
    "Notebook": "Notebook",
    "notebooks": "Notebook",
}

# 同じアイテム種別に複数のキー名を定義しても、後段の
# dropDuplicates で workspace_id、artifact_id、artifact_type の重複を除去する

# 最新の成功したフル スキャンを取得
latest_run = (
    spark.table("scanner_runs")
    .filter(
        (F.col("status") == "Succeeded")
        & (F.col("scan_mode") == "full")
    )
    .orderBy(F.col("scan_started_utc").desc())
    .first()
)

if latest_run is None:
    raise RuntimeError("成功したフル スキャンがありません。")

latest_run_id = latest_run["run_id"]
scan_started_utc = latest_run["scan_started_utc"]

payload_rows = (
    spark.table("scanner_raw")
    .filter(F.col("run_id") == latest_run_id)
    .orderBy("batch_number")
    .select("payload_json")
    .collect()
)

workspaces = []

for payload_row in payload_rows:
    payload = json.loads(payload_row["payload_json"])
    workspaces.extend(payload.get("workspaces", []))


workspace_rows = []
artifact_rows = []

for workspace in workspaces:
    workspace_id = workspace.get("id")

    if not workspace_id:
        continue

    workspace_rows.append((
        workspace_id,
        workspace.get("name"),
        workspace.get("type"),
        workspace.get("state"),
        workspace.get("capacityId"),
        latest_run_id,
        scan_started_utc,
    ))

    for property_name, artifact_type in ARTIFACT_COLLECTIONS.items():
        for artifact in workspace.get(property_name, []) or []:
            artifact_id = artifact.get("id") or artifact.get("objectId")

            if not artifact_id:
                continue

            artifact_rows.append((
                workspace_id,
                artifact_id,
                artifact.get("name") or artifact.get("displayName"),
                artifact_type,
                artifact.get("state"),
                artifact.get("modifiedDateTime") or artifact.get("modifiedDate"),
                artifact.get("configuredBy") or artifact.get("modifiedBy"),
                latest_run_id,
                json.dumps(artifact, ensure_ascii=False),
            ))


workspace_schema = StructType([
    StructField("workspace_id", StringType(), False),
    StructField("workspace_name", StringType(), True),
    StructField("workspace_type", StringType(), True),
    StructField("state", StringType(), True),
    StructField("capacity_id", StringType(), True),
    StructField("last_scan_run_id", StringType(), False),
    StructField("last_seen_utc", StringType(), False),
])

artifact_schema = StructType([
    StructField("workspace_id", StringType(), False),
    StructField("artifact_id", StringType(), False),
    StructField("artifact_name", StringType(), True),
    StructField("artifact_type", StringType(), False),
    StructField("state", StringType(), True),
    StructField("modified_utc", StringType(), True),
    StructField("owner", StringType(), True),
    StructField("last_scan_run_id", StringType(), False),
    StructField("raw_json", StringType(), False),
])

workspace_df = (
    spark.createDataFrame(workspace_rows, workspace_schema)
    .dropDuplicates(["workspace_id"])
)

artifact_df = (
    spark.createDataFrame(artifact_rows, artifact_schema)
    .dropDuplicates(["workspace_id", "artifact_id", "artifact_type"])
)

# フル スキャンの結果で最新状態を全件置換
(
    workspace_df.write
    .format("delta")
    .mode("overwrite")
    .option("overwriteSchema", "true")
    .saveAsTable("workspace_inventory")
)

(
    artifact_df.write
    .format("delta")
    .mode("overwrite")
    .option("overwriteSchema", "true")
    .saveAsTable("artifact_inventory")
)

scan_run_df = (
    spark.table("scanner_runs")
    .withColumn("scan_started_at", F.to_timestamp("scan_started_utc"))
    .withColumn("completed_at", F.to_timestamp("completed_utc"))
    .select(
        "run_id",
        "scan_started_at",
        "completed_at",
        "scan_mode",
        "workspace_count",
        "batch_count",
        "status",
    )
)

(
    scan_run_df.write
    .format("delta")
    .mode("overwrite")
    .option("overwriteSchema", "true")
    .saveAsTable("scan_run_inventory")
)

print(
    f"Analysis tables created. Workspaces: {workspace_df.count()}, "
    f"Artifacts: {artifact_df.count()}"
)
```

### 分析テーブルを確認する

Lakehouse に以下の 3 テーブルが作成されます。

- artifact_inventory
- scan_run_inventory
- workspace_inventory

<div align="center">
<img src="pbi_scanner_api_1_07.png">
</div>

続いて、Lakehouse の表示を **[SQL 分析エンドポイント]** に切り替えます。エクスプローラーに 3 テーブルが表示されない場合は、エクスプローラー上部の **[更新]** を選択します。  
SQL 分析エンドポイントでは、Lakehouse に作成した Delta テーブルのメタデータがバックグラウンドで同期されます。新しいテーブルが反映されるまで時間がかかる場合があるため、3 テーブルが表示されてからセマンティック モデルを作成します。

> [!NOTE]
> 参考# [SQL 分析エンドポイントのメタデータ同期 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-engineering/sql-analytics-endpoint-metadata-sync#manual-refresh)
> 参考# [Lakehouse チュートリアル: セマンティック モデルとレポートを作成する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-engineering/tutorial-lakehouse-build-report#create-a-semantic-model)

## Power BI レポートを作成する

### Direct Lake セマンティック モデル

1. ”lh_scanner_metadata” の **[SQL 分析エンドポイント]** を開きます。
    <div align="center">
    <img src="pbi_scanner_api_1_08.png">
    </div>

2. エクスプローラーに ”workspace_inventory”、”artifact_inventory”、”scan_run_inventory” が表示されていることを確認します。表示されない場合は、エクスプローラー上部の **[更新]** を選択します。
    <div align="center">
    <img src="pbi_scanner_api_1_09.png">
    </div>

3. **[新しいセマンティック モデル]** を選択します。
    <div align="center">
    <img src="pbi_scanner_api_1_10.png">
    </div>

4. モデル名として ”sm_scanner_inventory” を入力します。

5. **[OneLake の Direct  Lake]** で ”workspace_inventory”、 ”artifact_inventory”、 ”scan_run_inventory” を選択します。
    <div align="center">
    <img src="pbi_scanner_api_1_11.png">
    </div>

6. ”workspace_inventory” の [workspace_id] を 1 側、 ”artifact_inventory” の [workspace_id] を多側とする 1 対多のリレーションシップを作成します。

    <div align="center">
    <img src="pbi_scanner_api_1_12.png">
    </div>

7. raw_json や ID など、レポート作成者が使用しない列を非表示にします。

scan_run_inventory は実行履歴を表す独立したテーブルとして使用します。

<div align="center">
<img src="pbi_scanner_api_1_13.png">
</div>

### 基本メジャー

以下のメジャーを作成します。

```dax
Workspace Count =
COUNTROWS ( workspace_inventory )

Artifact Count =
COUNTROWS ( artifact_inventory )

Report Count =
CALCULATE (
    [Artifact Count],
    artifact_inventory[artifact_type] = "Report"
)

Semantic Model Count =
CALCULATE (
    [Artifact Count],
    artifact_inventory[artifact_type] = "SemanticModel"
)

Last Successful Scan =
CALCULATE (
    MAX ( scan_run_inventory[completed_at] ),
    scan_run_inventory[status] = "Succeeded"
)
```

"scan_run_inventory" は独立したテーブルであるため、 "Last Successful Scan" はテナント全体の最終成功スキャン日時を返します。

> [!NOTE]
> 参考# [Direct Lake の概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/fundamentals/direct-lake-overview)
> 参考# [スター スキーマと Power BI での重要性について理解する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/star-schema)

### レポート ページ

上記で作成したセマンティック モデル ”sm_scanner_inventory” をもとにレポートを作成します。 

<div align="center">
<img src="pbi_scanner_api_1_14.png">
</div>

## 注意事項

- Scanner API の結果には組織内の管理情報が含まれる場合があります。Lakehouse、Notebook、セマンティック モデルへのアクセスを適切に管理してください。
- 更新または再発行されていないセマンティック モデルや特定の接続方式では、テーブル、列、式などのサブアーティファクト メタデータが返されない場合があります。
- 本記事のフル スキャンを再実行すると、 "scanner_raw" と "scanner_runs" に新しい実行が追加されます。分析テーブルは最新の成功したフル スキャンで置き換えられます。

> [!NOTE]
> 参考# [メタデータのスキャンを実行する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/governance/metadata-scanning-run)

## おわりに

本記事では、Scanner API の概要を説明し、Semantic Link と Fabric Notebook を使用してテナントのフル スキャンを実行しました。また、結果を Lakehouse の Delta テーブルへ保存し、分析テーブル、Direct Lake セマンティック モデル、Power BI レポートを作成しました。

第 2 回では、前回成功したスキャンの開始時刻を利用した増分スキャン、Fabric Data Factory による定期実行、増分結果を分析テーブルへ反映する方法をご紹介します。

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。
