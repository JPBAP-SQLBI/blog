---
title: トラブル発生時の事象調査における情報採集
date: 2023-08-31 00:00:00 
tags:
  - Power BI
  - Troubleshooting
  - Fiddler
  - PSR
  - Power BI Desktop trace
  - browser trace
  - Process Monitor
  - Xbox Game Bar
---


こんにちは、Power BI サポート チームのファムです。
Power BI を利用される際に、エラーが発生するなど想定したとおりに動作しない場合、事象が起こる原因を特定するための調査が必要になる場合があります。
以前[「トラブル発生時の事象調査に必要な情報の採取手順について(通信編)」](https://jpbap-sqlbi.github.io/blog/powerbi/all_howto_trace/)について記載しましたが、現象によって必要な情報は異なりますので、以下は複数のパターンを想定して問題が発生する場合の情報採取手順についてご紹介いたします。

<!-- more -->

</br>

> [!IMPORTANT]
> 弊社サポートをご利用いただいている場合、状況に合わせた調査方針を策定するため、記載の内容とご案内が異なる場合がございます。
> ご不明な点がございましたら弊社サポート担当までお気軽にご質問ください。
> また掲載している画像・手順は投稿時点のものとなります。最新の情報とは異なる可能性がございますので予めご了承ください。

</br>

---
## 目次
---
1. [Fiddlerトレースとステップ記録ツール（PSR）の採取手順](#1．Fiddlerトレースとステップ記録ツール（PSR）の採取手順)
2. [Power BI Desktopトレースとステップ記録ツール（PSR）の採取手順](#2．Power-BI-Desktopトレースとステップ記録ツール（PSR）の採取手順)
3. [ブラウザトレースとステップ記録ツール（PSR）の採取手順](#3．ブラウザトレースとステップ記録ツール（PSR）の採取手順)
4. [FiddlerトレースとPower BI Desktopトレースとステップ記録ツール（PSR）の採取手順](#4．FiddlerトレースとPower-BI-Desktopトレースとステップ記録ツール（PSR）の採取手順)
5. [プロセス モニターとPower BI DesktopトレースとXbox Game Barによる録画の採取手順](#5．プロセス-モニターとPower-BI-DesktopトレースとXbox-Game-Barによる録画の採取手順)
</br>

---

## 1．Fiddlerトレースとステップ記録ツール（PSR）の採取手順

・HTTP/S トレース（Fiddler トレース）： クライアントに導入するソフトウェア。使用するアプリケーションなどを通じて端末と接続先のHTTP/S 通信を記録し通信状況の差異を確認するツール
・PSR（ステップ記録ツール）：　操作ごとに画面キャプチャを記録するツール

**1．Fiddlerのインストール**
1) Telerik 社の Web サイトより、適宜必要項目を入力し「Download for Windows」を選択し、インストーラをダウンロードします。その後、採取対象の環境へインストールします。
https://www.telerik.com/download/fiddler

</br>

<div align="center">
<img src="pic1.png">
</div>

2) 採取対象の環境で、Fiddler を起動します。
※Fiddler の採取時は可能な限り不要なアプリケーションを閉じ、事象再現のみのトレースが取れるように設定ください。
3) 自動的にトレースが開始されるため、メニュー バーの[File] - [Capture Traffic] を選択し、トレースを停止します。または[F12]キーでもトレースの停止/再開が可能です。

</br>

<div align="center">
<img src="pic2.png">
</div>

4) メニュー バーから [Tools] - [Options] を選択します。

</br>

<div align="center">
<img src="pic3.png">
</div>

5) HTTPS タブをクリックし、”Capture HTTPS CONNECTS” および “Decrypt HTTPS traffic” のチェック ボックスをオンにし、OK ボタンをクリックし、Fiddler Options を閉じます。

</br>

<div align="center">
<img src="pic4.png">
</div>

“Decrypt HTTPS traffic” のチェック ボックスをオンにすることで、以下の警告が表示されることがございます。Yes ボタンをクリックします。
“Fiddler generates a unique root CA certificate to intercept HTTPS traffic. You may choose to have Windows trust this root certificate to avoid security warnings about the untrusted root certificate. You should ONLY click ‘Yes’ on a computer used exclusively for TEST purposes.”
上記警告で Yes を選択すると、セキュリティ警告が表示されますので、”はい” を選択します。
これにより、ログインユーザーの個人ストアならびに、ローカルコンピューターの信頼されたルート証明機関ストアに発行者が “DO_NOT_TRUST_FiddlerRoot” である証明書が追加されます。
 
6) 画面右側にある Filters - User Filter がオフになっていることを確認します。

</br>

<div align="center">
<img src="pic5.png">
</div>

**2．画面キャプチャ準備・開始 「ステップ記録ツール (PSR)」**
1) コマンドプロンプトを右クリックで [管理者として実行] を選択の上起動します。
※[管理者として実行] を選択しなかった場合、一部手順のスクリーンショットが記録されないことがあります。
2)以下のコマンドを実行し、ステップ記録ツールを起動します。
psr.exe
3) "問題ステップ記録ツール" が起動しましたら、右端の ▼ をクリックし、表示されるメニューから [設定] をクリックします。
4) "保存する最新の取り込み画像数" を 25 から 100 に変更し、 OK をクリックします。
5) [記録の開始] をクリックします。

</br>

<div align="center">
<img src="pic6.png">
</div>

**3．Fiddler トレースの開始**
Fiddler のメニューバーの[File] - [Capture Traffic] を選択し、トレースを再開します。
この時左側のウィンドウでトレースが取れていることをご確認ください。

**4．事象の再現**
実際の事象が起きる操作を再現します。
 
**5．Fiddler トレースの停止**
1) 事象再現後、Fiddler メニュー バーの[File] - [Capture Traffic] を選択し、トレースを停止します。
2) Fiddler のメニュー バーから [File] - [Save] - [All Sessions] を選択し、.saz 形式でログを保存します。

</br>

<div align="center">
<img src="pic7.png">
</div>


3) 一度 Fiddler を終了し、閉じます。
 
**6．画面キャプチャの停止**
1) [記録の停止] をクリックします。
2) "名前を付けて保存" のダイアログが表示されますので、ファイルの保存場所、ファイル名を指定し、 [保存] をクリックします。
※本ツールは、ボタンクリックやマウスドラッグなど、マウスクリックの際に画像が記録されます。手順の最後にエラーが発生するような現象の場合、エラー画面も把握できるようにクリックしてください。
※保存したファイルを開き、画像が採取できていることをご確認ください。画像数が100 を超える場合、古いものから順に削除されますので手順 4 の数値を 100 より大きな数値にご変更ください。

</br>

<div align="center">
<img src="pic8.png">
</div>

Fiddlerトレースとステップ記録ツール (PSR)の採取手順は以上となります。必要に応じて弊社サポートまで採取いただいた情報をご提供ください。

Fiddler 自体が Proxy の役目となるため、ご利用環境からインターネットへの通信において Proxy サーバーがございましたら、利用する貴社の Proxy を通るようにご設定ください。
※外部サイトではございますが、手順についてまとめられたサイトがありますので、ご参考ください。
参考情報：[プロキシ環境でのfiddler](http://did2.blog64.fc2.com/blog-entry-8.html)


**ネットワーク環境においてプロキシをご利用いただいている場合**

Fiddler 自体が Proxy の役目となるため、ご利用環境からインターネットへの通信において Proxy サーバーがございましたら、利用する貴社の Proxy を通るようにご設定ください。

※外部サイトではございますが、手順についてまとめられたサイトがありますので、ご参考ください。
参考情報：[プロキシ環境でのfiddler](http://did2.blog64.fc2.com/blog-entry-8.html)


## 2．Power BI Desktopトレースとステップ記録ツール（PSR）の採取手順

・Desktop トレース  ：Power BI Desktopの処理を記録するためのトレース
・PSR（ステップ記録ツール） ：操作ごとに画面キャプチャを記録するツール

**1．画面キャプチャ準備・開始 「ステップ記録ツール (PSR)」**
1) コマンドプロンプトを右クリックで [管理者として実行] を選択の上起動します。
※[管理者として実行] を選択しなかった場合、一部手順のスクリーンショットが記録されないことがあります。
2)以下のコマンドを実行し、ステップ記録ツールを起動します。
psr.exe
3) "問題ステップ記録ツール" が起動しましたら、右端の ▼ をクリックし、表示されるメニューから [設定] をクリックします。
4) "保存する最新の取り込み画像数" を 25 から 100 に変更し、 OK をクリックします。
5) [記録の開始] をクリックします。


</br>

<div align="center">
<img src="pic6.png">
</div>

</br>

**2．Power BI Desktopトレースの採取手順**
開いている Power BI Desktop をすべて閉じます。
以下の Traces フォルダーおよびその配下のフォルダーにあるログファイルをすべて削除します。

%LOCALAPPDATA%\Microsoft\Power BI Desktop\Traces
または
%USERPROFILE%\Microsoft\Power BI Desktop Store App\Traces

1)「環境変数」の「ユーザー変数」に 変数名：PBI_forceTracing、変数値： 1 を設定します。


</br>

<div align="center">
<img src="pic9.png">
</div>

2)左上にあるキャプチャウィンドウから、マイクをオフにし、●ボタンをクリックすると、録画が開始されます。

</br>

<div align="center">

<img src="pic10.png">
</div>

**3．事象再現**
実際の事象が起きる操作を再現します。

**4．Power BI Desktop トレース停止**
Power BI Desktop を閉じます。
現象再現後、トーレスに関しましては、以下の Power BI Desktop フォルダーに生成されます。
該当の Traces フォルダーを以下の弊社アップロードサイトへご送付ください。

%LOCALAPPDATA%\Microsoft\Power BI Desktop\Traces
または
%USERPROFILE%\Microsoft\Power BI Desktop Store App\Traces

<トレース無効化手順>
「環境変数」の「ユーザー変数」に 設定した PBI_forceTracing  1 を削除します。

**5．画面キャプチャの停止**
1) [記録の停止] をクリックします。
2) "名前を付けて保存" のダイアログが表示されますので、ファイルの保存場所、ファイル名を指定し、 [保存] をクリックします。
※本ツールは、ボタンクリックやマウスドラッグなど、マウスクリックの際に画像が記録されます。手順の最後にエラーが発生するような現象の場合、エラー画面も把握できるようにクリックしてください。
※保存したファイルを開き、画像が採取できていることをご確認ください。画像数が100 を超える場合、古いものから順に削除されますので手順 4 の数値を 100 より大きな数値にご変更ください。

</br>

<div align="center">
<img src="pic8.png">
</div>

Power BI Desktopトレースとステップ記録ツール (PSR) の採取手順は以上となります。必要に応じて弊社サポートまで採取いただいた情報をご提供ください。

## 3．ブラウザトレースとステップ記録ツール（PSR）の採取手順

・ブラウザ トレース  ：ブラウザの処理を記録するためのトレース
・PSR（ステップ記録ツール）　：操作ごとに画面キャプチャを記録するツール

**1．画面キャプチャ準備・開始 「ステップ記録ツール (PSR)」**
1) コマンドプロンプトを右クリックで [管理者として実行] を選択の上起動します。
※[管理者として実行] を選択しなかった場合、一部手順のスクリーンショットが記録されないことがあります。
2)以下のコマンドを実行し、ステップ記録ツールを起動します。
psr.exe
3) "問題ステップ記録ツール" が起動しましたら、右端の ▼ をクリックし、表示されるメニューから [設定] をクリックします。
4) "保存する最新の取り込み画像数" を 25 から 100 に変更し、 OK をクリックします。
5) [記録の開始] をクリックします。

</br>

<div align="center">
<img src="pic6.png">
</div>

</br>

**2．ブラウザトレースの開始**
1) ブラウザを起動し、Chrome のシークレットモードまたはEdge のIn-Private モードで新しいウィンドウを開きます。
2) F12 を押下し、ネットワーク を選択し、セッションをクリアした後、開始ボタンを押下します。
 
Microsoft Edge の場合： 
</br>

<div align="center">
<img src="pic11.png">
</div>

</br>

Chrome の場合： 
</br>

<div align="center">
<img src="pic12.png">
</div>

</br>

**3．事象再現**
実際の事象が起きる操作を再現します。

**4．ブラウザトレースの停止**
停止 ボタンを押下し、HARファイルとしてエクスポート ボタンよりファイルをエクスポートします。
※取得したトレース上で右クリックしていただき、「HAR としてすべて保存する」からでもエクスポート可能です。
 
Microsoft Edgeの場合：
</br>

<div align="center">
<img src="pic13.png">
</div>

Chrome の場合： 
</br>

<div align="center">
<img src="pic14.png">
</div>

**5．画面キャプチャの停止**
1) [記録の停止] をクリックします。
2) "名前を付けて保存" のダイアログが表示されますので、ファイルの保存場所、ファイル名を指定し、 [保存] をクリックします。
※本ツールは、ボタンクリックやマウスドラッグなど、マウスクリックの際に画像が記録されます。手順の最後にエラーが発生するような現象の場合、エラー画面も把握できるようにクリックしてください。
※保存したファイルを開き、画像が採取できていることをご確認ください。画像数が100 を超える場合、古いものから順に削除されますので手順 4 の数値を 100 より大きな数値にご変更ください。

</br>

<div align="center">
<img src="pic8.png">
</div>

ブラウザトレースとステップ記録ツール (PSR) の採取手順は以上となります。必要に応じて弊社サポートまで採取いただいた情報をご提供ください。

</br>

## 4．FiddlerトレースとPower BI Desktopトレースとステップ記録ツール（PSR）の採取手順

・HTTP/S トレース（Fiddler トレース） ：クライアントに導入するソフトウェア。使用するアプリケーションなどを通じて端末と接続先のHTTP/S 通信を記録し通信状況の差異を確認するツール
・Desktop トレース    ：Power BI Desktopの処理を記録するためのトレース
・PSR（ステップ記録ツール）　：操作ごとに画面キャプチャを記録するツール

**1．Fiddlerのインストール**
1) Telerik 社の Web サイトより、適宜必要項目を入力し「Download for Windows」を選択し、インストーラをダウンロードします。その後、採取対象の環境へインストールします。
https://www.telerik.com/download/fiddler

</br>

<div align="center">
<img src="pic1.png">
</div>

2) 採取対象の環境で、Fiddler を起動します。
※Fiddler の採取時は可能な限り不要なアプリケーションを閉じ、事象再現のみのトレースが取れるように設定ください。
 
3) 自動的にトレースが開始されるため、メニュー バーの[File] - [Capture Traffic] を選択し、トレースを停止します。または[F12]キーでもトレースの停止/再開が可能です。

</br>

<div align="center">
<img src="pic2.png">
</div>

4) メニュー バーから [Tools] - [Options] を選択します。

</br>

<div align="center">
<img src="pic3.png">
</div>

5) HTTPS タブをクリックし、”Capture HTTPS CONNECTS” および “Decrypt HTTPS traffic” のチェック ボックスをオンにし、OK ボタンをクリックし、Fiddler Options を閉じます。

</br>

<div align="center">
<img src="pic4.png">
</div>

“Decrypt HTTPS traffic” のチェック ボックスをオンにすることで、以下の警告が表示されることがございます。Yes ボタンをクリックします。
“Fiddler generates a unique root CA certificate to intercept HTTPS traffic. You may choose to have Windows trust this root certificate to avoid security warnings about the untrusted root certificate. You should ONLY click ‘Yes’ on a computer used exclusively for TEST purposes.”
上記警告で Yes を選択すると、セキュリティ警告が表示されますので、”はい” を選択します。
これにより、ログインユーザーの個人ストアならびに、ローカルコンピューターの信頼されたルート証明機関ストアに発行者が “DO_NOT_TRUST_FiddlerRoot” である証明書が追加されます。
 
6) 画面右側にある Filters - User Filter がオフになっていることを確認します。

</br>

<div align="center">
<img src="pic5.png">
</div>

**2．画面キャプチャ準備・開始 「ステップ記録ツール (PSR)」**
1) コマンドプロンプトを右クリックで [管理者として実行] を選択の上起動します。
※[管理者として実行] を選択しなかった場合、一部手順のスクリーンショットが記録されないことがあります。
2)以下のコマンドを実行し、ステップ記録ツールを起動します。
psr.exe
3) "問題ステップ記録ツール" が起動しましたら、右端の ▼ をクリックし、表示されるメニューから [設定] をクリックします。
4) "保存する最新の取り込み画像数" を 25 から 100 に変更し、 OK をクリックします。
5) [記録の開始] をクリックします。

</br>

<div align="center">
<img src="pic6.png">
</div>

**3．Fiddler トレースの開始**
Fiddler のメニューバーの[File] - [Capture Traffic] を選択し、トレースを再開します。
この時左側のウィンドウでトレースが取れていることをご確認ください。

**4．Power BI Desktopトレースの採取手順**
開いている Power BI Desktop をすべて閉じます。
以下の Traces フォルダーおよびその配下のフォルダーにあるログファイルをすべて削除します。

%LOCALAPPDATA%\Microsoft\Power BI Desktop\Traces
または
%USERPROFILE%\Microsoft\Power BI Desktop Store App\Traces

1)「環境変数」の「ユーザー変数」に 変数名：PBI_forceTracing、変数値： 1 を設定します。


</br>

<div align="center">
<img src="pic9.png">
</div>

2)左上にあるキャプチャウィンドウから、マイクをオフにし、●ボタンをクリックすると、録画が開始されます。

</br>

<div align="center">

<img src="pic10.png">
</div>

**5．事象の再現**
実際の事象が起きる操作を再現します。

**6．Fiddler トレースの停止**
1) 事象再現後、Fiddler メニュー バーの[File] - [Capture Traffic] を選択し、トレースを停止します。
2) Fiddler のメニュー バーから [File] - [Save] - [All Sessions] を選択し、.saz 形式でログを保存します。

</br>

<div align="center">
<img src="pic7.png">
</div>

3) 一度 Fiddler を終了し、閉じます。
 
**7．Power BI Desktop トレース停止**
Power BI Desktop を閉じます。
現象再現後、トーレスに関しましては、以下の Power BI Desktop フォルダーに生成されます。
該当の Traces フォルダーを以下の弊社アップロードサイトへご送付ください。

%LOCALAPPDATA%\Microsoft\Power BI Desktop\Traces
または
%USERPROFILE%\Microsoft\Power BI Desktop Store App\Traces

<トレース無効化手順>
「環境変数」の「ユーザー変数」に 設定した PBI_forceTracing  1 を削除します。


**8．画面キャプチャの停止**
1) [記録の停止] をクリックします。
2) "名前を付けて保存" のダイアログが表示されますので、ファイルの保存場所、ファイル名を指定し、 [保存] をクリックします。
※本ツールは、ボタンクリックやマウスドラッグなど、マウスクリックの際に画像が記録されます。手順の最後にエラーが発生するような現象の場合、エラー画面も把握できるようにクリックしてください。
※保存したファイルを開き、画像が採取できていることをご確認ください。画像数が100 を超える場合、古いものから順に削除されますので手順 4 の数値を 100 より大きな数値にご変更ください。

</br>

<div align="center">
<img src="pic8.png">
</div>

FiddlerトレースとPower BI Desktopトレースとステップ記録ツール (PSR)の採取手順は以上となります。必要に応じて弊社サポートまで採取いただいた情報をご提供ください。

**ネットワーク環境においてプロキシをご利用いただいている場合**
Fiddler 自体が Proxy の役目となるため、ご利用環境からインターネットへの通信において Proxy サーバーがございましたら、利用する貴社の Proxy を通るようにご設定ください。

※外部サイトではございますが、手順についてまとめられたサイトがありますので、ご参考ください。
参考情報：[プロキシ環境でのfiddler](http://did2.blog64.fc2.com/blog-entry-8.html)


## 5．プロセス モニターとPower BI DesktopトレースとXbox Game Barによる録画の採取手順

・プロセス モニター ：リアルタイムのファイル システム、レジストリ、プロセス/スレッド アクティビティを示す Windows 用の高度な監視ツール
・Desktop トレース    ：Power BI Desktopの処理を記録するためのトレース
・Xbox Game Barによる録画    ：操作ごとに録画するツール

**1．プロセス モニターのインストール**
1) 以下のWebサイトより、インストーラーをダウンロードします。
[プロセス モニター - Sysinternals | Microsoft Learn](https://learn.microsoft.com/ja-jp/sysinternals/downloads/procmon)

</br>

<div align="center">
<img src="pic15.png">
</div>

2) 採取対象の環境で、Procmon.exe を 管理者権限で起動します。
※プロセス モニターを実施時に、可能な限り不要なアプリケーションを閉じ、事象再現のみのトレースが取れるように設定ください。

"Process Monitor License Agreement" が表示された場合は、内容をご確認の上 [Agree] を選択します。
</br>

<div align="center">
<img src="pic16.png">
</div>

3) フィルタ指定メニューが自動表示された場合は [Cancel] を選択します。
※ [Cancel] を選択後、情報採取が開始されます。

4) 開始された情報採取を一旦停止するため、[File] - [Capture Events] を選択し、チェックを外します。
　[Edit] – [Clear Display]を選択します。
※ ツールバーに存在する "虫眼鏡" のアイコンをクリックすることにより、同様に情報採取を停止することが可能となります。
</br>

<div align="center">
<img src="pic17.png">
</div>

**2．Power BI Desktopトレースの採取手順**
開いている Power BI Desktop をすべて閉じます。
以下の Traces フォルダーおよびその配下のフォルダーにあるログファイルをすべて削除します。

%LOCALAPPDATA%\Microsoft\Power BI Desktop\Traces
または
%USERPROFILE%\Microsoft\Power BI Desktop Store App\Traces

「環境変数」の「ユーザー変数」に 変数名：PBI_forceTracing、変数値： 1 を設定します。


</br>

<div align="center">
<img src="pic9.png">
</div>

**3．Xbox Game Barによる録画開始**
1) XBOX Game Barが起動します。
Windowsのスタートボタンから、[Xbox]と入力するとアプリが表示されますので、こちらを選択して起動できます。

</br>

<div align="center">
<img src="pic18.png">
</div>

2) 左上にあるキャプチャウィンドウから、マイクをオフにし、●ボタンをクリックすると、録画が開始されます。

</br>

<div align="center">
<img src="pic19.png">
</div>

**4．プロセス モニターの開始**
情報採取準備が完了した後、以下の手順でプロセス モニターによるトレース採取を開始します。
[File] - [Capture Events] を選択し、チェックを付けます。

**5．事象再現**
実際の事象が起きる操作を再現します。

**6．Power BI Desktop トレース停止**
Power BI Desktop を閉じます。
現象再現後、トーレスに関しましては、以下の Power BI Desktop フォルダーに生成されます。
該当の Traces フォルダーを以下の弊社アップロードサイトへご送付ください。

%LOCALAPPDATA%\Microsoft\Power BI Desktop\Traces
または
%USERPROFILE%\Microsoft\Power BI Desktop Store App\Traces
<トレース無効化手順>
「環境変数」の「ユーザー変数」に 設定した PBI_forceTracing  1 を削除します。

**7．プロセス モニターの停止**
1) [File] - [Capture Events] を選択し、チェックを外します。

2) メニューの [File] から [Save] メニューを選択し、プロセス モニタートレース情報を任意のパスに保存します。
※ オプションは既定のままで問題ございません。

</br>

<div align="center">
<img src="pic20.png">
</div>

**8．録画停止**
1) 画面右上に表示されているウィンドウの■ボタンをクリックし、停止します。
</br>

<div align="center">
<img src="pic21.png">
</div>

2) キャプチャのギャラリーにてファイルの場所を開きます。
</br>

<div align="center">
<img src="pic22.png">
</div>

こちらの画面が出ない場合は、Xbox Game Barの[キャプチャを表示する]をクリックすると、ギャラリーが表示されます。
</br>

<div align="center">
<img src="pic23.png">
</div>

3) 保存先の動画を確認します。
デフォルト設定での保存先は、C:\Users\[アカウント名]\Videos\Captures
や、エクスプローラ画面における[ビデオ]フォルダ内の[キャプチャ]フォルダとなっております。

</br>

<div align="center">
<img src="pic24.png">
</div>

プロセス モニターとPower BI DesktopトレースとXbox Game Barによる録画の採取手順は以上となります。必要に応じて弊社サポートまで採取いただいた情報をご提供ください。
</br>
以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
