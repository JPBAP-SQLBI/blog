
---
title: Power BI Desktop のコンポーネント変更について(Webview2)
date: 2021-11-30 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
---


こんにちは、Power BI サポート チームです。 

来年2022年1月以降 Power BI Desktop をご利用いただくにあたり、新しいコンポーネント「WebView2」への切り替えが発表され、インストールが必須となることが発表されました。
WebView2 への切り替えは、Power BI Desktop の開発とリリースのプロセスを従来よりも最適化することを目的としています。また WebView2 によって、従来 Power BI Desktop のアップデートごとに行なわれていたセキュリティパッチも、リアルタイムで最新のセキュリティパッチを自動的に提供できるようになります。

基本的に WebView2 は Power BI Desktop のインストールに合わせて自動的にインストールが行なわれるため、皆様に特別な操作を求めることはございませんが、オフライン環境などで Power BI Desktop をご利用されている方や一部の対象者は、別途 WebView2 のインストールが必要になる場合がありますので、本記事をご確認いただき、Power BI Desktop のバージョンアップに備えましょう。

<!-- more -->

</br>

> [!IMPORTANT]
> 本記事は 弊社公式ブログ「Microsoft Power BI ブログ」の公開情報を元に構成しておりますが、本記事編集時点と実際の機能やリリース時期に相違がある場合がございます。
>元記事は以下よりご確認ください（英語）
><Span style="font-size: 90%">[Power BI Desktop Installer Changes & WebView2](https://powerbi.microsoft.com/en-us/blog/power-bi-desktop-installer-changes-webview2/)</span>


</br>


---


## Power BI Desktop に必要なスペックについて

前提として Power BI Desktop では、以下の通り最小要件が定められています。

- Windows 8.1 / Windows Server 2012 R2 以降
- .NET 4.6.2 以降
- Internet Explorer 11 以降
- メモリ (RAM): 2 GB 以上使用可能、4 GB 以上を推奨します。
- ディスプレイ: 1440 x 900 以上または 1600 x 900 (16:9) が必要です。 1024 x 768 または 1280 x 800 などの低い解像度はサポートされていません。
- Windows の表示設定: 表示設定でテキスト、アプリ、その他の項目を 100% より大きいサイズに変更してある場合、Power BI Desktop を使い続けるために対話する必要がある特定のダイアログを表示できないことがあります。 この問題が発生した場合は、Windows で [設定] > [システム] > [表示] に移動して表示設定を確認し、スライダーを使って表示設定を 100% に戻します。
- CPU: 1 ギガヘルツ (GHz) 64 ビット (x64) プロセッサ以上が推奨されます。

[Power BI Desktop の最小要件について](https://docs.microsoft.com/ja-jp/power-bi/fundamentals/desktop-get-the-desktop#minimum-requirements)

</br>

## WebView2 について

</br>

### WebView2 とは

WebView2 は、Microsoft Edge をWeb コンテンツを表示するための部品としてアプリケーションで利用できるようにするコンポーネントの一つです。
Power BI Desktop では、従来 Web コンテンツの表示においては Chromium ベースの「CefSharp」が使用されてきましたが、今後 WebView2 への切り替えによって、より開発とリリースのプロセスを最適化していくことを目指しています。
また、Power BI Desktopのアップデートを待たずに、WebView2 を通じて最新のセキュリティパッチが自動的に提供できるようになります。

</br>

### 切り替えが必要になるバージョンについて

2022年1月にリリースされる Power BI Report Server 向けのPower BI Desktop と、2022年2月にリリースされる Power BI Desktop では、WebView2 が必要になる予定です。

</br>

### Webview2 がインストールされているか確認する方法

お使いの端末に「Microsoft Edge WebView2 Runtime」がインストールされていれば、WebView2はすでにインストールされているため、これ以上の操作は必要ありません。

ご利用の端末の[アプリと機能]から「Microsoft Edge WebView2 Runtime」が表示されるかどうかご確認ください。

<div align="center">
<img src="pic1.png" alt="画像1_Webview2 の確認方法" title="画像1_Webview2 の確認方法">
</div>

</br>


### Webview2 のインストールが必要な場合

WebView2 は、Microsoft 365 アプリケーションのアップデートや 実行ファイルからPower BI をアップデートする場合、自動的にインストールが行われますが、
以下のいずれにも当てはまる場合は、別途インストールする必要があります。

1. Microsoft 365 アプリケーションが端末にインストールされていない
2. Windows 10 以下を使用している (Windows 11 を使用している場合は、WebView2 がデフォルトでインストールされているため、対応する必要はありません。)
3. Microsoft Store 版 Power BI Desktop を使用している
   *端末の管理者権限で使用している場合、Power BI Desktop にインストールするように通知が表示されます。

上記いずれにも当てはまる場合や、オフライン環境で Power BI Desktop を利用している方、誤って端末から削除してしまった方は、以下のリンクから別途インストールすることが可能です。

[WebView2 ランタイムのダウンロード](https://developer.microsoft.com/ja-jp/microsoft-edge/webview2/#download-section)

<div align="center">
<img src="pic2.png" alt="画像2_Webview2 ランタイムのダウンロード" title="画像2_Webview2 ランタイムのダウンロード">
</div>


</br>


また管理者の方は、WebView2ランタイムの組織への導入についての詳細も合わせてご覧ください。
弊社公開情報：[WebView2 ランタイムのインストール](https://docs.microsoft.com/ja-jp/DeployOffice/webview2-install#webview2-runtime-installation)

</br>


### Power BI Desktop へのWebview2 の有効化

来年からの切り替えが始まる前に、WebView2 をすぐに使用したい場合は、Power BI Desktop のプレビュー機能で WebView2 を有効にすることができます。
このオプションは、WebView2 がインストールされている場合にのみ表示され、現時点（2021年11月）では、Microsoft Store 版ではなく、.exeインストーラーを使用してインストールされた Power BI Desktop でのみ利用可能です。

<div align="center">
<img src="pic0.png" alt="画像3_Webview2 の有効化" title="画像3_Webview2 の有効化">
</div>

これをオンにしてPower BI Desktopを再起動すると、自動的にWebView2の使用が開始されます。
特に Power BI Desktop の操作や挙動が変わることはありません。

</br>

以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。
