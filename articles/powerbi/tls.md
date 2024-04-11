---
title: TLS1.0/1.1のサポート終了
date: 2023-05-31 00:00:00 
tags:
  - Power BI
---

こんにちは、Power BI サポート チームの亀田です。
この度、Power BIにおいてTLS1.0/1.1を使用した通信のサポートが終了しますので、その詳細やユーザーさまにて必要な設定等についてご案内いたします。Power BIを管理されているユーザーさまは、いま一度ご確認いただきますようお願いいたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## TLSとは
TLSとは、正称をTransport Layer Security (トランスポート層セキュリティ プロトコル) といい、インターネットを介して行われる通信のプライバシーを保護するために設計された、業界標準のプロトコルです。TLSプロトコルを利用することで、メッセージの改ざんや傍受、偽造を検知することができます。1999年に初めてTLS1.0が定義され、現在はTLS1.3がリリースされています。  
> [!NOTE]
> 参考# [トランスポート層セキュリティ プロトコル - Win32 apps | Microsoft Learn](https://learn.microsoft.com/ja-jp/windows/win32/secauthn/transport-layer-security-protocol)

<div align="center">
<img src="TLS01.png">
</div>  

TLS1.0/1.1は古いプロトコルのため、新たに脆弱性が発見され、悪意のある第三者からの攻撃を受ける可能性があります。そのため、Microsoftでは様々なアプリケーションでTLS1.0/1.1のサポートを終了し、TLS1.2を利用するように移行しています。  
> [!NOTE]
> 参考# [更新: トランスポート層セキュリティ 1.0 および 1.1 の無効化 - Microsoft Lifecycle | Microsoft Learn](https://learn.microsoft.com/ja-jp/lifecycle/announcements/transport-layer-security-1x-disablement)

<div align="center">
<img src="TLS02.png">
</div>  

## TLS1.0/1.1のサポート終了
2023年4月26日に、Microsoft365管理センターのメッセージ センターに、以下の案内が送付されています。
> 件名: Power BI notification for discontinuation of support for TLS 1.0 and 1.1 (MC546936)
>
> We will be retiring the support of TLS 1.0 and TLS 1.1 for outgoing requests from Power BI. Instead, we recommend the utilization of TLS 1.2 or above for outgoing requests, which is where we will continue to invest our development resources. TLS 1.0 and TLS 1.1 have already been disabled for incoming requests long ago. For security documentation, please refer: [Power BI Security - Power BI](https://learn.microsoft.com/power-bi/enterprise/service-admin-power-bi-security).
>
> (自動翻訳)
>
> Power BI からの送信リクエストにおける TLS 1.0 および TLS 1.1 のサポートは終了となります。その代わりに、発信リクエストにはTLS 1.2以上の利用を推奨しており、今後も開発リソースを投入していく予定です。TLS 1.0とTLS 1.1は、すでにかなり前に受信リクエストに対して無効化されています。セキュリティに関するドキュメントは、こちらをご参照ください： Power BI セキュリティ - Power BI.

<div align="center">
<img src="TLS03.png">
</div>  

こちらは、Power BIからクライアントへの通信について、TLS1.0/1.1のサポートが終了するために送られた案内でございます。すでに、クライアントからPower BIへの通信についてはサポートが終了しており、送信/受信ともにPower BIではTLS1.0/1.1のサポートが終了となります。  
今回の発信リクエストのサポート終了にともない影響が考えられるシナリオとしましては、レガシーなデータソースを利用している場合がございます。データソースがTLS1.0/1.1へフォールバックされる場合には、Power BIではデータの取り込みに利用できなくなります。  
今後は、TLS1.0/1.1を利用したPower BI Serviceとの通信は行うことができません。TLS1.0/1.1を利用したクライアントでの通信は失敗しますのでご注意ください。例えば、以下のクライアントではTLS1.2を利用することができません。以下のクライアントを利用している場合にはご注意ください。
> [!NOTE]
> 参考# [Deprecating TLS 1.0 and 1.1 support in Power BI | Microsoft Power BI ブログ | Microsoft Power BI](https://powerbi.microsoft.com/ja-jp/blog/deprecating-tls-1-0-and-1-1-support-in-power-bi/)

* Android 4.3 以前のバージョン
* Firefox バージョン 5.0 以前のバージョン
* Windows 7 以前のバージョンの Internet Explorer 8-10
* Windows Phone 8 の Internet Explorer 10
* Safari 6.0.4/OS X10.8.4以前のバージョン

<div align="center">
<img src="TLS04.png">
</div>  

## ユーザーさまが実施する必要のある操作(Power BI Service)
TLS1.0/1.1のサポート終了によって、テナント設定の変更等、ユーザーさまがPower BI Service上で行う必要のある操作は**ございません**。

## ユーザーさまが実施する必要のある操作(クライアント)
TLS1.0/1.1を利用するクライアントを利用している場合には、TLS1.2を利用するように構成する必要があります。例えば、.NETアプリケーションを使用している場合には、.NET Framework4.6以上で実行されている場合には、規制の構成を変更していない限りTLS1.2を利用しますが、.NET Framework4.6より前で実行されている場合には、以下のコードを使用することで、アプリケーションの起動時にTLS1.2を有効にすることができます。
```
System.Net.ServicePointManager .SecurityProtocol |= SecurityProtocolType.Tls11 | SecurityProtocolType.Tls12; 
```

また、PowerShellを使用している場合には、以下のコードでTLSのバージョンをアップグレードすることができます。

```
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12  
```
> [!NOTE]
> 参考# [Power BI アプリケーションの TLS バージョンを TLS 1.2 にアップグレードする | Azure の更新情報 | Microsoft Azure](https://azure.microsoft.com/ja-jp/updates/power-bi-support-for-transportlayer-security/)

<div align="center">
<img src="TLS05.png">
</div>  

## おわりに
Power BIは、皆さまが安心してご利用いただけるように改善に取り組んでおり、今後も改善を続けていきます。セキュリティについては以下の公開情報に記載をしておりますのでよろしければご一読ください。
> [!NOTE]
> 参考# [Power BI のセキュリティに関するホワイト ペーパー - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/whitepaper-powerbi-security)
> 参考# [Power BI のセキュリティ - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-power-bi-security)

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。