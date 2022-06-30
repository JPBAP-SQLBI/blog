---
title: トラブル発生時の事象調査に必要な情報の採取手順について(通信編)
date: 2021-10-31 00:00:00 
tags:
  - Troubleshooting
  - Fiddler
  - PSR
---


こんにちは、Power BI サポート チームの山本です。 

Power BI を利用される際に、エラーが発生するなど想定したとおりに動作しない場合、事象が起こる原因を特定するための調査が必要になる場合があります。現象によって必要な情報は異なりますが、多くの場合、事象が起こっている画面や通信状況から原因となる情報が取得できる場合がございます。


今回は、Power BI を実行するクライアントからPower BI サービスへの通信時に問題が発生する場合の情報採取手順についてご紹介いたします。 

<!-- more -->

</br>

> [!IMPORTANT]
> 弊社サポートをご利用いただいている場合、状況に合わせた調査方針を策定するため、記載の内容とご案内が異なる場合がございます。
> ご不明な点がございましたら弊社サポート担当までお気軽にご質問ください。
> また掲載している画像・手順は投稿時点のものとなります。最新の情報とは異なる可能性がございますので予めご了承ください。


</br>


---

## 情報採取１：ステップ記録ツール (PSR) 

ステップ記録ツールは Windows OS に標準搭載されているツールです。
このツールを利用することで、事象発生時の操作と画面を記録し、その様子をまとめたレポートを自動で作成します。
弊社サポートで認識の齟齬なく事象再現時の状況を確認することに役立てることが可能です。

<div align="center">
<img src="pic0.png" alt="画像1_PSR" title="画像1_PSR">
</div>


## 情報採取２：Fiddler (HTTP トレースツール)

弊社サポート製品ではございませんが、Fiddler と呼ばれる HTTP トレースツールを利用することで HTTPS の通信を含めたキャプチャを取得することが可能です。
これを利用することで通信にエラーが生じているかどうか、またそのエラーから原因となる情報が特定できる場合がございます。
本ツールをご利用いただくには、対象の端末に本ツールをインストールしていただく必要があります。
以下に、HTTPS 通信を含めたネットワークアクセスのキャプチャ手順をご案内いたします。

※Fiddler は Telerik 社の製品となります。


<div align="center">
<img src="pic1.png" alt="画像2_Fiddler" title="画像2_Fiddler">
</div>



</br>

## 情報採取手順について

### Fiddler のインストール

1) Telerik 社の Web サイトより、適宜必要項目を入力し「Download for Windows」を選択し、インストーラをダウンロードします。
その後、採取対象の環境へインストールします。
https://www.telerik.com/download/fiddler

<div align="center">
<img src="pic7.png" alt="画像3_Fiddler インストール" title="画像3_Fiddler インストール">
</div>

### PSR 採取開始
ステップ記録ツール (PSR) を起動し、記録を開始します。

1) 採取対象の環境にて、Win + R キーを押し、[ファイル名を指定して実行] より “psr” と入力し、[OK] をクリックします。

2) [ステップ記録ツール] が起動しましたら、右端の ▼ をクリックし、[設定] をクリックします。

3) [保存する最新の取り込み画像数] を “25” から “150” に変更し [OK] をクリックします。

<div align="center">
<img src="pic2.png" alt="画像4_PSR設定画面" title="画像4_PSR設定画面">
</div>

4) [記録の開始] をクリックします。


</br>

### Fiddler トレースの採取と PSR の採取

1) 採取対象の環境で、Fiddler を起動します。
※Fiddler の採取時は可能な限り不要なアプリケーションを閉じ、事象再現のみのトレースが取れるように設定ください。

2) 自動的にトレースが開始されるため、メニュー バーの[File] - [Capture Traffic] を選択し、トレースを停止します。
または[F12]キーでもトレースの停止/再開が可能です。

<div align="center">
<img src="pic6.png" alt="画像5_Fiddler Capture Traffic のオフ" title="画像5_Fiddler Capture Traffic のオフ">
</div>

3) メニュー バーから [Tools] - [Options] を選択します。

<div align="center">
<img src="pic3.png" alt="画像6_Fiddler Option" title="画像6_Fiddler Option">
</div>

4) HTTPS タブをクリックし、”Capture HTTPS CONNECTS” および “Decrypt HTTPS traffic” のチェック ボックスをオンにし、OK ボタンをクリックし、Fiddler Options を閉じます。

<div align="center">
<img src="pic4.png" alt="画像7_HTTPS 通信の復号" title="画像7_HTTPS 通信の復号">
</div>

“Decrypt HTTPS traffic” のチェック ボックスをオンにすることで、以下の警告が表示されることがございます。Yes ボタンをクリックします。
“Fiddler generates a unique root CA certificate to intercept HTTPS traffic. You may choose to have Windows trust this root certificate to avoid security warnings about the untrusted root certificate. You should ONLY click ‘Yes’ on a computer used exclusively for TEST purposes.”
上記警告で Yes を選択すると、セキュリティ警告が表示されますので、”はい” を選択します。
これにより、個人ストア、および信頼されたルート証明機関ストアに発行者が “DO_NOT_TRUST_FiddlerRoot” である証明書が追加されます。

> [!TIP]
> <b>この手順が必要な理由</b>
> 通常HTTPS 通信は暗号化されているため、Fiddler 側でTraffic の情報を復号化できるように準備する必要がございます。


5) 画面右側にある Filters - User Filter がオフになっていることを確認します。

<div align="center">
<img src="pic5.png" alt="画像8_User Filter のオフ" title="画像8_User Filter のオフ">
</div>


6) 再度メニュー バーの[File] - [Capture Traffic] を選択し、トレースを再開します。
この時左側のウィンドウでトレースが取れていることをご確認ください。

7) 事象を再現させます。

8) トレースから現象やエラー等を確認できましたら、メニュー バーの[File] - [Capture Traffic] を選択し、トレースを停止してください。

9) Fiddler のメニュー バーから [File] - [Save] - [All Sessions] を選択し、.saz 形式でログを保存します。

<div align="center">
<img src="pic8.png" alt="画像9_Fiddler トレースの保存" title="画像9_Fiddler トレースの保存">
</div>

9) PSR の画面で [記録の停止] をクリックします。

10) 記録されたステップで事象の再現が確認できましたら [保存] をクリックし、ファイルの保存場所、ファイル名を指定し、[保存] をクリックします。

<div align="center">
<img src="pic9.png" alt="画像10_PSR ステップの保存" title="画像10_PSR ステップの保存">
</div>

11) PSR と Fiddler を終了します。

12) 必要に応じて弊社サポートまで採取いただいた情報をご提供ください。

</br>

### ネットワーク環境においてプロキシをご利用いただいている場合

Fiddler 自体が Proxy の役目となるため、ご利用環境からインターネットへの通信において Proxy サーバーがございましたら、
利用する貴社の Proxy を通るようにご設定ください。

※外部サイトではございますが、手順についてまとめられたサイトがありますので、ご参考ください。
参考情報：[プロキシ環境でのfiddler](http://did2.blog64.fc2.com/blog-entry-8.html)


</br>

以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。
