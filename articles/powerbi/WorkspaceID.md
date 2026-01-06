---
title: ワークスペース ID と信頼されたワークスペース アクセス
date: 2025-12-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Microsoft Fabric
  - セマンティック モデル
  - ワークスペースID
---

こんにちは、Power BI サポート チームの亀田です。

Microsoft Fabric で新しく利用できるようになった認証方式として、ワークスペース ID があります。ワークスペース ID は、Microsoft Fabric 内のワークスペースに関連付けられたサービス プリンシパルで、信頼されたワークスペース アクセスを通じてファイアウォールが有効な Azure Data Lake Storage Gen2 (以降 ADLS Gen2) アカウントへの接続が可能です。今回は、ワークスペース ID を利用した信頼されたワークスペース アクセスで ADLS Gen2 に接続する方法をご紹介します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 目次

* [ワークスペース ID](#ワークスペース-ID)
   * [ワークスペース ID の作成](#ワークスペース-ID-の作成)
* [信頼されたワークスペース アクセス](#信頼されたワークスペース-アクセス)
   * [信頼されたワークスペース アクセスの利用](#信頼されたワークスペース-アクセスの利用)
* [おわりに](#おわりに)

## ワークスペース ID

ワークスペース IDは、Microsoft Fabric のワークスペースに紐付けられたサービス プリンシパルです。マイ ワークスペースを除く任意のワークスペースの設定から作成することができ、作成すると Microsoft Entra ID 上にサービス プリンシパルが作成されます。ワークスペース ID に関連付けられた資格情報は Microsoft Fabric で自動的に管理するため、ユーザーが資格情報を覚えておく必要がなく、資格情報の漏洩や一時的な資格情報の無効によるダウンタイムを防ぐことができます。現在は、ADLS Gen2 のほか、SQL Server、Azure Analysis Services などで利用できます。データソースでワークスペース ID を用いた認証が利用できるかは、利用したいデータソースのコネクタのページをご確認ください。

> 参考#
>  [ワークスペース ID - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/security/workspace-identity)
> [Microsoft Fabric ワークスペース ID を使用して認証する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/security/workspace-identity-authenticate)
> [すべての Power Query コネクタのリスト - Power Query | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-query/connectors/)

### ワークスペース ID の作成

ワークスペース ID を作成するための条件は以下のとおりです。

- 作成するユーザーのワークスペース ロールが ”管理者” である
- マイ ワークスペース以外のワークスペースである

それでは、具体的にワークスペース ID の作成方法をご紹介します。

1. ワークスペースを開き、 [ワークスペースの設定] を選択します。
   <div align="center">
   <img src="WorkspaceID_01.png">
   </div>  
2. [ワークスペース ID] タブを開き、 [+ ワークスペース ID] を選択します。
   <div align="center">
   <img src="WorkspaceID_02.png">
   </div>  

作成は以上で完了です。ワークスペース ID の詳細、許可されているユーザーの一覧の情報が表示されます。
<div align="center">
<img src="WorkspaceID_03.png">
</div>  

Microsoft Entra ID を確認すると、ワークスペース名と同名のサービス プリンシパルが作成されていることが確認できます。
<div align="center">
<img src="WorkspaceID_04.png">
</div>  

## 信頼されたワークスペース アクセス

信頼されたワークスペース アクセス機能は、作成したワークスペース ID を利用して ADLS Gen2 にアクセスできる機能です。 ADLS Gen2 でファイアウォールを有効にしている場合でも、ワークスペース ID を利用して認証を行うことができます。

利用できる条件は、以下のとおりです。

- ワークスペース が F SKU 容量上にあること
- 試用版容量ではないこと

また、現在使用できるのは、OneLake のショートカット、パイプライン、セマンティック モデル、T-SQL COPY ステートメント、および AzCopy のみです。

参考＃
[Microsoft Fabric での信頼されたワークスペース アクセス - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/security/security-trusted-workspace-access)
[Private ADLS Gen2 access made easy with OneLake Shortcuts: a step-by-step guide | Microsoft Fabric Blog | Microsoft Fabric](https://blog.fabric.microsoft.com/en-us/blog/private-adls-gen2-access-made-easy-with-onelake-shortcuts-a-step-by-step-guide?ft=All)

### 信頼されたワークスペース アクセスの利用

信頼されたワークスペース アクセスの利用例として、ADLS Gen2 へのショートカットを作成します。

#### 1.リソース インスタンス ルールの作成

ワークスペース ID を利用して ADLS Gen2 にアクセスするため、Fabric ワークスペースのリソース インスタンス ルールを作成します。ARM テンプレートをデプロイします。
参考＃ [ARM テンプレートを使用したリソース インスタンス ルール](https://learn.microsoft.com/ja-jp/fabric/security/security-trusted-workspace-access#resource-instance-rule-via-arm-template)

Azure Portal にアクセスし、[カスタム テンプレートのデプロイ] を選択します。
<div align="center">
<img src="WorkspaceID_05.png">
</div>  

[エディターで独自のテンプレートを作成する] を選択します。
<div align="center">
<img src="WorkspaceID_06.png">
</div>  

テンプレートには以下を利用します。
参考＃ [信頼されたワークスペース アクセス - ARM テンプレートのサンプル](https://learn.microsoft.com/ja-jp/fabric/security/security-trusted-workspace-access#arm-template-sample)

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2023-01-01",
            "name": "<storage account name>",
            "id": "/subscriptions/<subscription id of storage account>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name>",
            "location": "<region>",
            "kind": "StorageV2",
            "properties": {
                "networkAcls": {
                    "resourceAccessRules": [
                        {
                            "tenantId": "<tenantid>",
                            "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabric/providers/Microsoft.Fabric/workspaces/<workspace-id>"
                        }]
                }
            }
        }
    ]
}
```

それぞれの情報は、以下のように取得します。

- storage account name /  subscription id of storage account / resource group name / region
  Azure Portal 上のストレージ アカウントの概要タブ
   <div align="center">
   <img src="WorkspaceID_07.png">
   </div>  

- tenantid
  Power BI を開き、[ヘルプとサポート] > [Power BI について] を選択して表示されたウインドウ内にある ”テナントの URL" に記載された ctid= 以降の英数字
   <div align="center">
   <img src="WorkspaceID_08.png">
   </div>  

- workspace-id
  ワークスペースを開き、表示された URL の groups/ から /list までに記載された英数字
   <div align="center">
   <img src="WorkspaceID_09.png">
   </div>  

入力ができたら保存して、デプロイします。

#### 2.ワークスペース ID への ADLS Gen2 アクセス権の付与

アクセスに使用するワークスペース ID には、以下のアクセス権が必要です。
参考＃ [信頼されたワークスペース アクセス - ADLS Gen2 で信頼されたワークスペース アクセスを構成する (Prerequisites)](https://learn.microsoft.com/ja-jp/fabric/security/security-trusted-workspace-access#prerequisites)

> - ショートカットの認証に使用されるプリンシパルには、ストレージ アカウントに対する Azure RBAC ロールが必要です。 プリンシパルには、ストレージ アカウント スコープでのストレージ BLOB データ共同作成者、ストレージ BLOB データ所有者、またはストレージ BLOB データ閲覧者ロール、またはコンテナー内のフォルダー レベルでのアクセス権とともにストレージ アカウント スコープでのストレージ BLOB デリゲータのロールが必要です。 フォルダー レベルでのアクセスは、コンテナー レベルの RBAC ロールまたは特定のフォルダー レベルのアクセスを通じて提供できます。

Azure Portal からアクセスしたいストレージ アカウントを開き、[アクセス制御 (IAM)] > [ロールの割り当て] からアクセス権を設定していきます。
<div align="center">
<img src="WorkspaceID_10.png">
</div>  

1. [+ 追加] を選択します。
   <div align="center">
   <img src="WorkspaceID_11.png">
   </div>  

2. 今回はストレージ BLOB データ共同作成者を割り当てます。[次へ] を選択します。
   <div align="center">
   <img src="WorkspaceID_12.png">
   </div>  

3. [+ メンバーを選択する] を選択して、表示されたウインドウで作成したワークスペース ID を選択します。[レビューと割り当て] でロールを割り当てます。
   <div align="center">
   <img src="WorkspaceID_13.png">
   </div>  

#### 3.ショートカットの作成

今回はレイクハウスにショートカットを作成します。

1. レイクハウスを開き、Files を右クリック > [新しいショートカット] を選択します。
   <div align="center">
   <img src="WorkspaceID_14.png">
   </div>  
2. [Azure Data Lake Storage Gen2] を選択します。
   <div align="center">
   <img src="WorkspaceID_15.png">
   </div>  
3. 接続先のストレージ アカウントの URL を入力します。https://<ストレージ アカウント名>.dfs.core.windows.net/ です。[認証の種類] は ”ワークスペース ID” を選択します。
   <div align="center">
   <img src="WorkspaceID_16.png">
   </div>  
4. 正しく設定がされていれば、ADLS Gen2 内のコンテナーが表示されます。ショートカットを作成したいコンテナーを選択します。[次へ] を選択します。
   <div align="center">
   <img src="WorkspaceID_17.png">
   </div>  
5. [作成] を選択してショートカットを作成します。
   <div align="center">
   <img src="WorkspaceID_18.png">
   </div>  

レイクハウスから ADLS Gen2 へのショートカットが作成でき、コンテナー内に格納されたファイルを確認することができました。
<div align="center">
<img src="WorkspaceID_19.png">
</div>  

## おわりに

今回はワークスペース ID と信頼されたワークスペース アクセスについて紹介しました。利用できるアイテムは限られておりますが、ADLS Gen2 を利用するシナリオでは資格情報の管理の手間が少なく、より安全にアクセスできる方法です。ぜひご利用いただけますと幸いです。

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。