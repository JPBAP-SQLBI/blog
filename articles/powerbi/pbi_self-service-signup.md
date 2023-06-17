---
title: セルフサービス サインアップの無効化
date: 2023-06-09 00:00:00 
tags:
  - Power BI　　
  - ライセンス
  - Power BI Free
  - セルフサービス サインアップ
---

こんにちは、Power BI サポート チームの山崎です。

Power BI にはいくつかのライセンスがあることを、こちらのブログ「 [Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license/) 」でご紹介させていただきました。

無償版の Power BI Free ライセンスについては、組織において無制限でライセンスを取得しご利用いただけますが、ライセンス管理者様が割り当てを行わずとも、ユーザー自身でライセンスの利用を開始すること (セルフサービス サインアップ) が可能です。

今回は、管理者が組織内のユーザーに対して、”ユーザー自身で Power BI Free ライセンスの利用を開始できるようにするかどうかを制御する方法” についてご案内いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---

- [目次](#目次)
- [更新履歴](#更新履歴)
- [ユーザー自身が Power BI Free ライセンスの利用開始することを制御したいのはどんな時？](#ユーザー自身が-power-bi-free-ライセンスの利用開始することを制御したいのはどんな時)
- [セルフサービス サインアップとは？](#セルフサービス-サインアップとは)
- [セルフサービス サインアップの無効化手順](#セルフサービス-サインアップの無効化手順)
    - [1. 事前準備](#1-事前準備)
    - [2. Microsoft.Graph モジュールの実行](#2-microsoftgraph-モジュールの実行)
    - [3. セルフサービス サインアップを有効に戻したいとき](#3-セルフサービス-サインアップを有効に戻したいとき)


---
## 更新履歴
---
2023/6/09 (記: 山本)
MSOnline モジュールが2023年6月30日に廃止予定であることに伴い、[セルフサービス サインアップの無効化手順](#セルフサービス-サインアップの無効化手順) に使用するモジュールの変更およびスクリプトの修正を行ないました。MSOnline モジュールの廃止に関する詳細については Azure Identity サポートチームのブログをご参照ください。

> **参考情報**
> [Azure AD Graph / MSOnline PowerShell モジュール利用状況の調べ方](https://jpazureid.github.io/blog/azure-active-directory/how-to-determine-depreacated-azuread-msol/)

</br>

---
## ユーザー自身が Power BI Free ライセンスの利用開始することを制御したいのはどんな時？
---

Power BI 管理者様や IT 管理者様、これから Power BI 導入のプロジェクトを進められるご担当者様などから、「ユーザーが勝手に Power BI Freeライセンスの利用を開始することを制御したい」とご要望をいただくことがたくさんあります。
組織によって背景は様々ですが、多くのお問合せは以下のような場合の時にいただきます。
このようなシナリオに該当する場合は、”セルフサービス サインアップ” 機能を無効にすることをご検討ください。

- ライセンス割り当ては管理者側で完全に制御したい
- Power BI を組織内で徐々に展開していることを検討しているため、知らないうちにユーザーが勝手に利用することを防ぎたい
- 有償ライセンスのみを利用することを検討しているため、Power BI Free を利用させたくない

</br>

---
## セルフサービス サインアップとは？
---

セルフサービス サインアップとは、管理者側が各ユーザーへのライセンス割り当てをしなくてもユーザー側のサインアップ作業によってライセンスの取得およびサービスの利用開始が可能となる機能です。

本機能を無効化することで、ユーザーが勝手に Power BI Free ライセンスを利用開始することを制御できます。

</br>

> [!WARNING]
> 無効化の設定は他のセルフサービス プログラムと一括で管理されているため、例えば Power Apps のセルフサービス サインアップなども無効化されます。
> サービスごとに制御する方法はご用意がないことを、ご注意くださいますようお願いいたします。

</br>

> **参考情報**
> セルフ サービスサインアップが有効なプログラムの一覧はこちらでご案内しております。
> [セルフサービスでのサインアップと購入を有効または無効にする - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/microsoft-365/admin/misc/self-service-sign-up?view=o365-worldwide)   

---
## セルフサービス サインアップの無効化手順
---

セルフサービス サインアップ無効化の一連の設定手順を詳細におまとめいたしました。

> [!NOTE]
> 本操作はすべて PowerShell 上で実行することを想定しています。
> また本操作は、テナント管理者を想定した操作手順となります。

</br>

#### 1. 事前準備

セルフサービス サインアップの無効化には、PowerShell の Microsoft.Graph モジュール (Microsoft Graph PowerShell SDK) を使用します。
次の4つの前提条件を満たしておく必要がありますので、各種準備をします。

- PowerShell 5.1 以降
- .NET Framework 4.7.2以降
- PowerShellGet 最新バージョン
- PowerShellスクリプトの実行ポリシーは、リモート署名またはそれ以下に制限されていること

</br>

> **参考情報**
> [Install the Microsoft Graph PowerShell SDK](https://learn.microsoft.com/ja-jp/powershell/microsoftgraph/installation?view=graph-powershell-1.0#prerequisites)

</br>

**1) PowerShell のバージョンを確認する**

管理者として Windows PowerShell を起動し、以下のコマンドを実行します。

```ps
$PSVersionTable
```

次のように `PSVersion` の値が 5.1 以上であればサポートされます。

```ps
Name                           Value
----                           -----
PSVersion                      5.1.20348.1366
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
BuildVersion                   10.0.20348.1366
CLRVersion                     4.0.30319.42000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

バージョンが満たない場合、ご利用の環境に合わせて、PowerShell のインストールやアップデートをお試しください。

</br>

**2) .NET Framework 4.7.2 以降のインストール状況を確認する**

.NET Framework のインストール状況の確認には、いくつかの方法がございますが、ここでは PowerShell を使用して .NET 4.7.2 以上のバージョンがインストールされているかどうか確認します。

次のコマンドを実行し、`True` が返ってきたら .NET Framework 4.7.2 に対応していることが確認できます。

```ps
(Get-ItemPropertyValue -LiteralPath 'HKLM:SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full' -Name Release) -ge 461808
```

`False` の場合には [インストール ガイド](https://learn.microsoft.com/ja-jp/dotnet/framework/install/) を参考に、アップデートをお試しください。

> **参考情報**
> [方法: インストールされている .NET Framework バージョンを確認する](https://learn.microsoft.com/ja-jp/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)

</br>

**3) PowerShellGet を最新バージョンにする**

次のコマンドを実行し、`PowerShellGet` を最新バージョンにしておきます。

```ps
Install-Module PowerShellGet -Force
```

次のプロンプトが表示される場合は `Y` を入力し、`Enter` キーで続行します。

```ps
続行するには NuGet プロバイダーが必要です
PowerShellGet で NuGet ベースのリポジトリを操作するには、'2.8.5.201' 以降のバージョンの NuGetプロバイダーが必要です。
NuGet プロバイダーは 'C:\Program Files\PackageManagement\ProviderAssemblies' または'C:\Users\XX\AppData\Local\PackageManagement\ProviderAssemblies'
に配置する必要があります。'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force' を実行して NuGet プロバイダーをインストールすることもできます。今すぐ PowerShellGet で NuGet プロバイダーをインストールしてインポートしますか?
[Y] はい(Y)  [N] いいえ(N)  [S] 中断(S)  [?] ヘルプ (既定値は "Y"):
```

</br>

次の警告が表示されアップデートが中断される場合、PowerShell の SecurityProtocol が TLS1.2 に設定されていない可能性があります。

```ps
警告: Unable to resolve package source 'https://www.powershellgallery.com/api/v2'.
PackageManagement\Install-Package : 指定された検索条件とパッケージ名 'PowerShellGet' と一致するものが見つかりませんでした。登録されている使用可能なすべてのパッケージ ソースを確認するには、Get-PSRepository を使用します。
発生場所 C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1772 文字:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], Exception
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage
```

次のコマンドを実行し、`Tls12` が含まれていない場合、

```ps
[Net.ServicePointManager]::SecurityProtocol
```

次のコマンドで `Tls12` を強制し、再度 `Install-Module PowerShellGet -Force` をお試しください。

```ps
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```

</br>

また場合によっては、次の警告が表示され、`PowerShellGet` のインストールが中断されることがあります。

```ps
信頼されていないリポジトリ
信頼されていないリポジトリからモジュールをインストールしようとしています。このリポジトリを信頼する場合は、Set-PSRepository
コマンドレットを実行して、リポジトリの InstallationPolicy の値を変更してください。'PSGallery' からモジュールをインストールしますか?
[Y] はい(Y)  [A] すべて続行(A)  [N] いいえ(N)  [L] すべて無視(L)  [S] 中断(S)  [?] ヘルプ (既定値は "N"):
```

この場合には、`Set-ExecutionPolicy` を `Unrestricted` に変更するコマンドを実行し、再度お試しください。

```ps
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser
```

</br>

**4) PowerShell スクリプトの実行ポリシーを変更する**

続けて次のコマンドを実行し、PowerShell スクリプトの実行ポリシーを変更します。

```ps
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

コマンドを実行後、次のようなプロンプトが表示される場合、`A` を入力し、`Enter` キーで続行します。

```ps
実行ポリシーの変更
実行ポリシーは、信頼されていないスクリプトからの保護に役立ちます。実行ポリシーを変更すると、about_Execution_Policies
のヘルプ トピック (http://go.microsoft.com/fwlink/?LinkID=135170)
で説明されているセキュリティ上の危険にさらされる可能性があります。実行ポリシーを変更しますか?
[Y] はい(Y)  [A] すべて続行(A)  [N] いいえ(N)  [L] すべて無視(L)  [S] 中断(S)  [?] ヘルプ (既定値は "N"):
```

次のコマンドを実行し、実行ポリシーが `RemoteSigned` となっていることを確認します。

```ps
Get-ExecutionPolicy -Scope CurrentUser
```

</br>

**5) Microsoft.Graph をインストールする**

次のコマンドを実行し、Microsoft.Graph モジュールをインストールします。

```ps
Install-Module Microsoft.Graph -Scope CurrentUser
```

`信頼されていないレポジトリ` と表示される場合がありますが、`A` を入力し、`Enter` キーで続行します。

```ps
信頼されていないリポジトリ
信頼されていないリポジトリからモジュールをインストールしようとしています。このリポジトリを信頼する場合は、Set-PSRepository
コマンドレットを実行して、リポジトリの InstallationPolicy の値を変更してください。'PSGallery' からモジュールをインストールしますか?
[Y] はい(Y)  [A] すべて続行(A)  [N] いいえ(N)  [L] すべて無視(L)  [S] 中断(S)  [?] ヘルプ (既定値は "N"):
```

Microsoft.Graph のインストール後、次のコマンドでモジュールが確認できれば、インストールは成功です。

```ps
Get-InstalledModule Microsoft.Graph
```

```ps
Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.27.0     Microsoft.Graph                     PSGallery            Microsoft Graph PowerShell module
```

</br>

#### 2. Microsoft.Graph モジュールの実行

**1) Microsoft Graph にサインインする**

次のコマンドを実行し、Microsoft.Graph にサインインします。

```ps
Connect-MgGraph -Scopes "Policy.ReadWrite.Authorization"
```

ブラウザに遷移し、Microsoft 365 へのサインイン画面が表示されますので、
テナント管理者のアカウントでサインインします。

初めて上記コマンドを実行する場合、スコープに従ってアクセス許可が要求されます。
[組織の代理として同意する] にチェックをつけ [承諾] をクリックします。

<div align="center">
<img src="3.png" width=50%>
</div>
</br>

その後 `Welcome To Microsoft Graph!` と表示されると、認証成功となります。

</br>

**2) Azure Active Directory 内のドメイン取得**

アクセス先ドメインを確認します。

```ps
Get-MgDomain
```

**3) セルフサービス サインアップに関するテナント設定を確認する**

次のコマンドを実行し、セルフサービス サインアップに関するテナント設定の状態を確認します。

```ps
Get-MgPolicyAuthorizationPolicy | Format-List *Email*
```

AllowEmailVerifiedUsersToJoinOrganization が新規ユーザーに対するテナントの自動参加の可否を決める機能であり、AllowedToSignUpEmailBasedSubscriptions　既存ユーザーに対するライセンスの自動配布の可否を決める機能です。
この時点で両方の値が False の場合、次の項番4を実施する必要はありません。
既にセルフサービス サインアップの機能は無効になっています。

```ps
AllowEmailVerifiedUsersToJoinOrganization : True
AllowedToSignUpEmailBasedSubscriptions    : True
```

</br>

**4) セルフサービス サインアップを無効化する**

セルフサービス サインアップを無効化したい場合、次のコマンドを実行し、両機能を `false` にします。

```ps
Update-MgPolicyAuthorizationPolicy -AllowEmailVerifiedUsersToJoinOrganization:$false -AllowedToSignUpEmailBasedSubscriptions:$false
```


> **参考情報**
> [Update-MgPolicyAuthorizationPolicy (Microsoft.Graph.Identity.SignIns) | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.graph.identity.signins/update-mgpolicyauthorizationpolicy?view=graph-powershell-1.0)


</br>

上記設定後、Power BI のライセンスをもたないユーザーが Power BI にサインインしようとしても、以下画面の通りセルフサービス サインアップができなくなります。

<div align="center">
<img src="2.png">
</div>

</br>

**5) Microsoft Graph のサインイン セッションを切断**

最後に次のコマンドを実行し、Microsoft Graph へのセッションを切断します。

```ps
Disconnect-MgGraph
```

</br>

#### 3. セルフサービス サインアップを有効に戻したいとき

セルフサービス サインアップを有効化したい場合、次のコマンドを実行し、両機能を `true` にします。

```ps
Update-MgPolicyAuthorizationPolicy -AllowEmailVerifiedUsersToJoinOrganization:$true -AllowedToSignUpEmailBasedSubscriptions:$true
```

</br>


> **参考情報**
> [組織でのセルフサービス サインアップの使用 - Microsoft 365 admin | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-disable-self-service#use-powershell-azure-ad-and-microsoft-365-to-enable-and-disable-self-service)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)