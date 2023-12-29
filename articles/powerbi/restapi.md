---
title: REST API を組み合わせて情報を取得する
date: 2023-12-29 00:00:00 
tags:
  - Power BI
  - REST API
---
こんにちは、Power BI サポート チームの亀田です。

Power BI では多くの REST API が用意されていますが、すべての情報を REST API で取得することができるわけではなく、 REST API を組み合わせることで初めて取得することのできる情報があります。今回は例として、[Admin - Reports GetReportsAsAdmin](https://learn.microsoft.com/ja-jp/rest/api/power-bi/admin/reports-get-reports-as-admin) と [Admin - Reports GetReportUsersAsAdmin](https://learn.microsoft.com/ja-jp/rest/api/power-bi/admin/reports-get-report-users-as-admin) を組み合わせて、テナント内のすべてのレポートのアクセス権限を取得する方法についてご案内します。REST API の開発の際に参考にしていただけますと幸いです。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 目次

* [はじめに](#はじめに)
* [コマンドの解説](#コマンドの解説)
	* [1) サインイン](#1-サインイン)
	* [2) GetReportsAsAdmin を実行し、レポート ID とレポート名を取得](#2-GetReportsAsAdmin-を実行し、レポート-ID-とレポート名を取得)
    * [3) 各レポート ID に対して GetReportUsersAsAdmin を実行し、結果をリストに追加](#3-各レポート-ID-に対して-GetReportUsersAsAdmin-を実行し、結果をリストに追加)
    * [4) CSV ファイルに出力](#4-CSV-ファイルに出力)
* [注意事項](#注意事項)

## はじめに

今回は PowerShell で実行するスクリプトを作成します。早速ですが、作成するスクリプトは以下になります。それぞれのコマンドについて詳しく解説していきます。コマンドを実行する際には、管理者として実行することをおすすめします。管理者として実行しない場合には、エラーが発生する可能性があります。

```powershell
# モジュールのインポート
Import-Module -Name MicrosoftPowerBIMgmt 

# 1) サインイン
Connect-PowerBIServiceAccount

# 2) GetReportsAsAdmin を実行し、レポート ID とレポート名を取得
$apiUrl = "https://api.powerbi.com/v1.0/myorg/admin/reports"
$response = Invoke-PowerBIRestMethod -Url $apiUrl -Method GET | ConvertFrom-Json
$reports = $response.value | Select-Object id,name

# 3) 各レポート ID に対して GetDatasetUsersAsAdmin を実行し、結果を追加
$allUsers = New-Object 'System.Collections.Generic.List[object]'
foreach ($report in $reports) {
    $reportId = $report.id
    $reportName = $report.name
    $url = "https://api.powerbi.com/v1.0/myorg/admin/reports/$reportId/users"
    $response = Invoke-PowerBIRestMethod -Url $url -Method Get | ConvertFrom-Json 
    foreach ($user in $response.value) {
        $customObject = New-Object -TypeName PSObject -Property @{
            ReportId = $reportId
            ReportName = $reportName
            DisplayName = $user.displayName
            EmailAddress = $user.emailAddress
            GroupUserAccessRight = $user.reportUserAccessRight
        }
        $allUsers.Add($customObject)
    }
}

# 4) CSV ファイルに出力
$csvFilePath = './AllReportUsers.csv'
$allUsers | Export-Csv -Path $csvFilePath -NoTypeInformation -Encoding UTF8
```

もし、MicrosoftPowerBIMgmt をインストールしていない場合には、あらかじめ以下の公開情報を参考にしていただきインストールをしていただく必要があります。

参考# [Windows PowerShellと PowerShell Core 用の Microsoft Power BI コマンドレット - インストール | Microsoft Learn](https://learn.microsoft.com/ja-jp/powershell/power-bi/overview?view=powerbi-ps#installation)

```powershell
Install-Module -Name MicrosoftPowerBIMgmt
```

## コマンドの解説

### 1) サインイン

以下のコマンドを実行して、 Power BI へのサインインを行います。

```powershell
# 1) サインイン
Connect-PowerBIServiceAccount
```

もしもサインインを自動で行いたい場合には、以下のスクリプトを実行することでサインインが可能です。ただし、スクリプトにユーザー アカウントやパスワード、サービス プリンシパルのシークレット キーを記載することは危険ですので、セキュリティの観点からこのまま利用することは避け、実運用時には別ファイルから取得するなどの構成としてください。

```powershell
# ユーザー アカウントを利用する場合
$PowerBILogin = "<メールアドレス>"
$PowerBIPassword = ConvertTo-SecureString "<パスワード>" -AsPlainText -Force
$credential = New-Object System.Management.Automation.PSCredential ($PowerBILogin, $PowerBIPassword)
Connect-PowerBIServiceAccount -Credential $credential

# サービス プリンシパルを利用する場合
$clientId = "<アプリケーションID>"
$clientSecret = ConvertTo-SecureString "<シークレット キー>" -AsPlainText -Force
$tenantId = "<テナントID>"
$credential = New-Object System.Management.Automation.PSCredential $clientId, $clientSecret
Connect-PowerBIServiceAccount -ServicePrincipal -Credential $credential -TenantId $tenantId
```

もしサービス プリンシパルをご利用いただく場合には、以下の記事についてもご参照ください。

参考# [Power BI Service でサービス プリンシパルを利用する | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/ServicePrincipal/)

### 2) GetReportsAsAdmin を実行し、レポート ID とレポート名を取得

以下のコマンドで、[Admin - Reports GetReportsAsAdmin](https://learn.microsoft.com/ja-jp/rest/api/power-bi/admin/reports-get-reports-as-admin) の REST API を実行します。  
実行結果を変数 *response* として格納します。

```powershell
# 2) GetReportsAsAdmin を実行し、レポート ID とレポート名を取得
$apiUrl = "https://api.powerbi.com/v1.0/myorg/admin/reports"
$response = Invoke-PowerBIRestMethod -Url $apiUrl -Method GET | ConvertFrom-Json
```

Invoke-PowerBIRestMethod は、サインインしているプロファイルを利用して Power BI Service への REST API を実行する コマンドです。

参考# [Invoke-PowerBIRestMethod (MicrosoftPowerBIMgmt.Profile) | Microsoft Learn](https://learn.microsoft.com/ja-jp/powershell/module/microsoftpowerbimgmt.profile/invoke-powerbirestmethod?view=powerbi-ps)

今回実行する Admin - Reports GetReportsAsAdmin は、 GET の API ですので、 Invoke-PowerBIRestMethod での -Method オプションは GET を指定します。

<div align="center">
<img src="restapi01.png">
</div>  

この API では、レポート ID やレポート名、作成日時などを取得することができますが、この後の手順に必要なレポート ID とレポート名のみを変数 *reports* に格納します。

参考# [Select-Object (Microsoft.PowerShell.Utility) - PowerShell | Microsoft Learn](https://learn.microsoft.com/ja-jp/powershell/module/microsoft.powershell.utility/select-object?view=powershell-7.4)

```powershell
$reports = $response.value | Select-Object id,name
```

### 3) 各レポート ID に対して GetReportUsersAsAdmin を実行し、結果をリストに追加

以下のコマンドで、 [Admin - Reports GetReportUsersAsAdmin](https://learn.microsoft.com/ja-jp/rest/api/power-bi/admin/reports-get-report-users-as-admin) の REST API を実行します。はじめに結果を格納するための空の配列を作成し、その後、取得したレポート ID ごとにユーザーのアクセス権限を取得･格納しています。今回は、レポート ID 、レポート名、ユーザー名、メールアドレス、アクセス権限を出力するよう設定しています。

```powershell
# 3) 各レポート ID に対して GetDatasetUsersAsAdmin を実行し、結果を追加
$allUsers = New-Object 'System.Collections.Generic.List[object]'
foreach ($report in $reports) {
    $reportId = $report.id
    $reportName = $report.name
    $url = "https://api.powerbi.com/v1.0/myorg/admin/reports/$reportId/users"
    $response = Invoke-PowerBIRestMethod -Url $url -Method Get | ConvertFrom-Json 
    foreach ($user in $response.value) {
        $customObject = New-Object -TypeName PSObject -Property @{
            ReportId = $reportId
            ReportName = $reportName
            DisplayName = $user.displayName
            EmailAddress = $user.emailAddress
            GroupUserAccessRight = $user.reportUserAccessRight
        }
        $allUsers.Add($customObject)
    }
}
```

### 4) CSV ファイルに出力

最後に、取得した配列をもとに CSV ファイルを作成します。

```powershell
# 4) CSV ファイルに出力
$csvFilePath = './AllReportUsers.csv'
$allUsers | Export-Csv -Path $csvFilePath -NoTypeInformation -Encoding UTF8
```

以下のような CSV ファイルが作成されます。

<div align="center">
<img src="restapi02.png">
</div> 

## 注意事項

* REST API ごとに制限事項 (呼び出し回数等) がありますので、実行する際はご注意ください。例えば、GetReportsAsAdmin の REST API は 10 分間で 1 要求までの制限があります。
* 重ねてとなりますが、スクリプトにユーザー アカウントやパスワード、サービス プリンシパルのシークレット キーを記載することは危険ですので、実運用時には別ファイルから取得するなどの構成としてください。

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。
