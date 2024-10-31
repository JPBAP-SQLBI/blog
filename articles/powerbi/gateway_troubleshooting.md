---
title: オンプレミス データ ゲートウェイのトラブルシューティング：構成時に発生するエラー
date: 2023-05-31 00:00:00 
tags:
  - PowerBI　　
  - オンプレミス データ ゲートウェイ
  - on-premises data gateway
  - troubleshooting
  - トラブルシューティング
---


こんにちは、Power BI サポート チームの山崎です。  
オンプレミス上のデータを取得するなどの目的で、対象のサーバーと Power BI サービスをブリッジする機能としてオンプレミス データ ゲートウェイ (※1) がありますが、このゲートウェイの構成時にエラーが発生するというお問合せをいただくことがよくあります。  
今回は、ゲートウェイ構成時にエラーが発生した際にまずお試しいただきたいトラブルシューティングをご案内いたします。  

※1 [オンプレミス データ ゲートウェイとは]( https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-gateway-onprem)

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

<br />
<br />

---  
##  <font color="RoyalBlue">構成時に発生するエラー</font>   
---  

ゲートウェイ アプリをインストールした後に、ゲートウェイの管理者となるユーザーアカウントにてサインインし、新しいゲートウェイの登録を行い構成を完了させます。  
この構成作業中に、ゲートウェイ アプリ上に以下のようなエラーメッセージが表示され、後続の処理に進めないことがあります。  

<br /> 

「ゲートウェイの詳細を更新できませんでした。ゲートウェイを実行するアカウントの変更が必要な場合があります。」  
「ゲートウェイ サービスの正常性チェックがタイムアウトになり失敗しました。」   
「ゲートウェイを作成できませんでした、もう一度お試しください。」  
「ネットワーク要求で予期しないエラーが返されました。」   
「ネットワーク接続が制限されています。」   
「ゲートウェイは正しく構成されているがローカルネットワーク接続の問題によりアクセスできません。」   

<br />

---  
##  <font color="RoyalBlue">トラブルシューティング</font>   
---  

上記いずれかのエラーが発生している場合は、ゲートウェイを構成するための前提条件を満たせていない可能性があります。  
このため、まずは以下の点をご確認くださいますようお願いいたします。  

<br />

### <font color="LightCoral">1. 最新版のゲートウェイをインストールする</font> 
ゲートウェイの更新プログラムは毎月リリースしており、古いバージョンで発生する問題が解消している可能性があります。  
古いバージョンをインストールしている場合は、最新版で事象が解消するかご確認いただきますようお願いいたします。  

ご参考情報：  
[オンプレミスのデータ ゲートウェイの更新](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-update?source=recommendations)  

<br />  

### <font color="LightCoral">2. ゲートウェイに必要な通信を許可する</font>   

ゲートウェイは、以下公式ドキュメント “オンプレミス データ ゲートウェイの通信設定を調整する” でご案内しているFQDN、送信ポートの許可設定が必要となります。  
ファイアウォールにて通信の接続を制限しているご環境の場合は、ドキュメントに記載されている通信許可の設定がお済みであるかご確認いただきますようお願いいたします。　  

ご参考情報：  
[オンプレミス データ ゲートウェイの通信設定を調整する](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-communication)  


<br />  

### <font color="LightCoral">3. ゲートウェイ 構成ファイルの設定</font>   
対象のご環境にプロキシサーバーが存在している場合、以下公式ドキュメント “オンプレミス データ ゲートウェイのプロキシ設定を構成する” の通り、事前にゲートウェイの構成ファイルの設定が必要となります。

ご参考情報：  
[オンプレミス データ ゲートウェイのプロキシ設定を構成する]( https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-proxy) 


#### **<詳細手順>**  

1) 次の２つのファイルを確認し、テキストエディタなどで開きます。  

>C:\Program Files\On-premises data gateway\enterprisegatewayconfigurator.exe.config  
>C:\Program Files\On-premises data gateway\Microsoft.PowerBI.EnterpriseGateway.exe.config  

2) 以下表記の部分を変更します。  
  ※　"http\://192.168.1.10:3128" の部分には、実際のプロキシサーバーのアドレスを入力いただきます。  


**変更前 例**
 ```  
<system.net>  
    <defaultProxy useDefaultCredentials="true" />  
</system.net>  
 ```

**変更後 例**  
 ``` 
<system.net>
    <defaultProxy useDefaultCredentials="true">
        <proxy 
            autoDetect="false" 
            proxyaddress=" http://192.168.1.10:3128" 
            bypassonlocal="false" 
            usesystemdefault="true"
        /> 
    </defaultProxy>
</system.net>  
 ``` 

変更後、各ファイルを保存します。


※　ゲートウェイがプロキシを介してクラウド データ ソースに接続する場合や、対象のご環境によっては、以下構成ファイルを編集する必要があります。  
 
>C:\Program Files\On-premises data gateway\m\Microsoft.Mashup.Container.NetFX45.exe.config  


**変更前 例**
 ``` 
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
  </startup>
</configuration>
 ``` 

**変更後 例**
 ``` 
<configuration>
    <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
        <proxy proxyaddress="http://192.168.1.10:3128" bypassonlocal="true" />
        </defaultProxy>
    </system.net>
</configuration>
 ``` 


#### **<プロキシサーバー有無のご確認方法>**
コマンドプロンプトから、以下のコマンドを実行します。  
 ```   
  netsh winhttp show proxy
 ``` 

実行結果が以下結果の場合は、プロキシ設定がされていませんが、以下結果 <font color="red">**以外**</font>の場合、プロキシ設定がされております。

――――――――――――――――  
現在の WinHTTP プロキシ設定:  
直接アクセス (プロキシ サーバーなし)。  
――――――――――――――――   


<br />  

### <font color="LightCoral">4．サービスアカウントの変更</font>   
以下公式ドキュメント “オンプレミスのデータ ゲートウェイ サービス アカウントを変更する” に記載される通り、ゲートウェイのサービスは、ゲートウェイ専用のサービスアカウント “NT SERVICE\PBIEgwService” によって実行されますが、対象のご環境によっては、そのままだとエラーが発生する場合があります。  
上記 １～3 の設定確認をクリアしている場合、サービス アカウントをドメインユーザーまたは PC にサインインしているローカルユーザーに変更することで事象に変化があるかご確認いただきますようお願いいたします。  

ご参考情報：  
[オンプレミスのデータ ゲートウェイ サービス アカウントを変更する](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-service-account)

<br /> 

---  
##  <font color="RoyalBlue">その他ご参考情報</font>  
---  
以下公式ドキュメントでもゲートウェイのトラブルシューティングに関する情報をご案内していますので、合わせてご参考にしていただきますようお願いいたします。　　

ご参考情報：   
[オンプレミス データ ゲートウェイのトラブルシューティング](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-tshoot)

<br /> 
<br /> 
以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)

