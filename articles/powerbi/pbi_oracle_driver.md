---
title: Oracle データベースとの接続におけるトラブルシューティング
date: 2022-10-31 14:00:00 
tags:
  - Power BI　　
  - Power BI Desktop
  - 資格情報
  - 認証　
  - データソース設定
  - オンプレミスデータゲートウェイ
  - Oracle
  - トラブルシューティング
  - ドライバー
---


こんにちは、Power BI サポート チームの山崎です。  
Power BI には現在 、様々なコネクタが実装され、[接続がサポートされているデータソース](https://learn.microsoft.com/ja-jp/power-bi/connect-data/power-bi-data-sources) が多くありますが、データソースによっては端末とデータソース間の接続を確立するためにドライバーの インストールが必要となります。  

このため、弊社サポートには、 Power BI Desktop やオンプレミスデータゲートウェイから対象のデータソースに接続できないというお問い合わせをいただくことがありますが、まずは前提条件として、ドライバーの観点でその端末とデータソース間の接続が確立されているかをご確認、いただくようにしております。  

ドライバーのインストールや設定方法については 対象データソースの開発元にお問い合わせいただく必要がありますが、今回は特によくお問い合わせをいただく Oracle データベースとの接続シナリオについて、ご参考情報をご案内いたします。

<!-- more -->


> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---

## Oracle データベースへの接続に必要なドライバー

Power BI Desktop やオンプレミスデータゲートウェイから Oracle データベースに接続するには、Power BI Desktopやオンプレミスデータゲートウェイ アプリを実行しているコンピューター上に適切な Oracle クライアント ソフトウェアをインストールする必要があります。

### 1.Power BI Desktop からの接続の場合

使用している Power BI Desktop のビットバージョンにあわせた Oracle クライアントをインストールします。
つまり、32 ビットバージョンの Power BI Desktop を使用している場合は 32 ビット Oracle クライアントをインストールし、64 ビットバージョンの Power BI Desktop を使用している場合は 64 ビット Oracle クライアントをインストールします。  

### 2.オンプレミスデータゲートウェイからの接続の場合

オンプレミスデータゲートウェイは 64 ビットアプリとなりますので、64 ビット Oracle クライアントをインストールします。

インストール方法の詳細につきましては以下参考情報をご確認くださいますようお願いいたします。

参考情報：
[Power BI Desktop を使用して Oracle データベースに接続する](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-connect-oracle-database#64-bit-and-32-bit-drivers-for-power-bi-desktop)
[データ ソースの管理 - Oracle](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-gateway-onprem-manage-oracle#install-the-oracle-client)  

## Oracle データベースへの接続テスト

Oracle データベースへ接続できない場合、Power BI Desktop やオンプレミスデータゲートウェイからの接続のみで問題が発生しているのか、対象の端末からの接続自体が確立されていないのか、を切り分ける必要あります 。
その際に、以下 PowerShell スクリプトにて確認が可能です。

```PowerShell
$ORAServer = ""
$UserId = ""
$Password = ""
 
[void][System.Reflection.Assembly]::LoadWithPartialName("Oracle.DataAccess")
 
$oraCon = New-Object Oracle.DataAccess.Client.OracleConnection("User ID=$($UserId);Data Source=$($ORAServer);Password=$($Password)")
 
$oraCmd = $oraCon.CreateCommand()
$oraCmd.CommandText = "select user from dual"
 
$oraCon.Open()
“Connected to database: {0} running on host: {1} – Servicename: {2} – Serverversion: {3}” -f $oraCon.DatabaseName, $oraCon.HostName, $oraCon.ServiceName, $oraCon.ServerVersion
 
$reader = $oraCmd.ExecuteReader()
 
if($reader.Read()) {

    $reader.GetString(0)
}
 
$oraCon.Close()

```

**結果の例：**
上記スクリプトを ODPNET_ACCESSTEST.ps1 として実行した場合、接続に成功すると以下結果が返ってきます。


```
PS C:Work> .\ODPNET_ACCESSTEST.ps1
Connected to database: orcldb running on host: ***** ? Srvicename: ***** ? Serverversion:*.*.*.*.*
```

成功している場合は、対象の端末からの接続自体は確立されているということになりますので、問題が生じている Power BI Desktop やオンプレミスデータゲートウェイの観点で引き続き調査が必要となります。 
 
もしエラーとなる場合は、対象の端末からの接続自体が確立できていないということになりますので、Power BI サポートチームへ Power BI の事象としてお問い合わせをいただく前に、対象の端末とデータソース間の接続において発生している問題のトラブルシューティングを実施いただきますようお願いいたします。  

    
以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)