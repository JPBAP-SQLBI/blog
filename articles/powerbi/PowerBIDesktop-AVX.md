---
title: 2025 年 3 月版以降の Power BI Desktop では CPU で AVX 命令がサポートされている必要があります
date: 2025-08-31 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - アナウンス
---

こんにちは、Power BI サポート チームの亀田です。

2025 年 3 月版以降の Power BI Desktop / Power BI Report Server 向けの Power BI Desktop では CPU で AVX  (Advanced Vector Extensions)  命令がサポートされている必要があります。サポートされていない CPU では予期しない動作となる場合がございますので、この変更についてご案内いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 概要

[2025 年 3 月の更新 (2.141.1228.0)](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/desktop-latest-update-archive?tabs=powerbi-desktop#march-2025-update-214112280) に含まれるご案内のとおり、2025 年 3 月版以降の Power BI Desktop / 2025 年 5 月版以降の Power BI Report Server 向けの Power BI Desktop で動作するコードの制限により、 CPU で AVX 命令がサポートされている必要があります。

<div align="center">
<img src="PowerBIDesktop-AVX_01.png">
</div>  

AVX は、Intel と AMD が提供する拡張命令セットです。2011年に Intel の Sandy Bridge プロセッサで初めて導入されました。2025 年 3 月版以降の Power BI Desktop では内部動作のために CPU で AVX 命令がサポートされている必要がございます。サポートされない CPU で Power BI Desktop を利用していると、以下のようなエラーが表示されることがございます。

> このビジュアルのデータのフェッチ中にエラーが発生しました
>
> 予期しないエラーが発生しました (ファイル ''、 行 、 関数 '')。

<div align="center">
<img src="PowerBIDesktop-AVX_02.png">
</div>  

## 影響を受ける環境

影響を受ける環境は、 AVX 命令をサポートしていない CPU を搭載した端末や仮想マシンです。2011 年以前の Intel CPU や、ARM CPU を搭載した端末が対象となります。また、 CPU が AVX 命令をサポートしている場合でも、 Hyper-V や VMware、 VirtualBox の設定で AVX 命令が無効化されている場合があり、このような環境も対象となります。

## CPU の AVX サポート確認方法

Microsoft が提供している Sysinternals の Coreinfo を利用することで、 CPU が AVX 命令をサポートしているか確認することができます。

1. [Coreinfo - Sysinternals | Microsoft Learn](https://learn.microsoft.com/en-us/sysinternals/downloads/coreinfo) から Coreinfo をダウンロードします。

2. ダウンロードした Coreinfo.zip を解凍します。

3. 管理者としてコマンドプロンプトを起動します。

4. coreinfo.exeが展開されたフォルダに移動します。以下は C ドライブ直下に解凍したフォルダを配置した場合の例です。

   ```cmd
   cd "C:\Coreinfo"
   ```

<div align="center">
<img src="PowerBIDesktop-AVX_03.png">
</div>  

5. 次のコマンドを実行します。

   ```cmd
   coreinfo.exe -f
   ```

<div align="center">
<img src="PowerBIDesktop-AVX_04.png">
</div>  

6. 出力から AVX 命令の行を探します。命令の後に記載された記号は以下のとおりです。画像の環境では AVX 行は ”－” となっていますのでサポートされていません。

   > ＊ : サポートされています。
   >
   > ー : サポートされていません。

<div align="center">
<img src="PowerBIDesktop-AVX_05.png">
</div>  

 ## 必要な対応

AVX をサポートしていない CPU での動作につきましては今後のリリースでの対応予定はございません。そのため、対象となる CPU を搭載した環境では以下のどちらかの対応をお願いいたします。

1. 対応する CPU へのアップグレード

2. 2025 年 2 月以前の Power BI Desktop を利用する 

   Power BI Desktop は最新版のみをサポートしており、最新版では不具合の修正などが含まれますため、お問い合わせをいただいた際には問題の切り分けのためサポートよりバージョン アップを依頼する場合がございます。旧バージョンを利用するのは暫定的な対応であり、十分なサポートが提供できない場合もございますため、できる限り CPU のアップグレードをご検討いただきますようお願い申し上げます。

## おわりに

2025 年 3 月版以降の Power BI Desktop では CPU で AVX 命令がサポートされている必要があることをご案内いたしました。本ブログが少しでも皆さまのお役に立てますと幸いでございます。
