---
title: Power BI の新しいレポートフォーマット PBIR について  
date: 2026-02-27 15:00:00  
tags:  
  - Power BI Desktop
  - PBIR
  - PBIX
  - PBIP
---
    
こんにちは、Power BI サポート チームのチャンです。   

2026 年 1 月以降、Power BI サービスで作成されたすべての新規レポートはデフォルトで PBIR 形式を使用し、1 月に開始され 2 月末までに変更がすべて適用されます。既存のサービスレポートは編集・保存時に自動的に PBIR に変換されます。

本記事は、Power BI レポートの新しいフォーマット "PBIR" についてご案内し、具体的にレポート利用への影響や既存のレポートフォーマット PBIX や PBIP についても合わせて紹介いたします。

 </br>

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## PBIR フォーマットとは
---

PBIR フォーマットとは、一般的に保存される Power BI レポートファイル（.pbix）の内部のレポート定義フォーマットの仕様です。pbix ファイルとして保存する場合、内部的な動作として PBIR に変換して保存されます。

従来の Power BI レポートでは、この PBIR 定義は単一の report.json ファイルに集約された構造で管理されていました。本記事や Microsoft 公式ドキュメントでは、この旧来の構造を 「PBIRレガシー(PBIR-Legacy)” と呼びます。

PBIR（新フォーマット）はレポートを開発する際に、開発者にとってより利便性の高い機能を備えています。
 
具体的には、PBIR レガシーとは異なり、PBIR は、Power BI 以外のアプリケーションからの変更をサポートする公開文書形式です。 各ファイルにはパブリック JSON スキーマがあり、ファイルを文書化するだけでなく、Visual Studio Code などのコード エディターで、編集中に構文検証を実行することもできます。

新しいフォーマット PBIR により実施できるようになった機能は以下の通りでございます。

- レポート間でのページ/ビジュアル/ブックマークのコピーする。
- ビジュアル ファイルをコピーして貼り付けることで、すべてのページで一連のビジュアルの一貫性を確保する。
- 複数のレポート ファイル間で簡単に検索するおよび置き換える。
- スクリプトを使用してすべてのビジュアルにバッチ編集を適用する (ビジュアル レベル フィルターの非表示など)
 
また、pbip ファイル (Power BI Desktop プロジェクトレポート)として保存する場合、具体的に pbip プロジェクトフォルダーには、以下の点の差異がございます。

- definition.pbir 内に記載されるバージョンによって、レポート定義が PBIR レガシーの report.json ファイルか、PBIR (\definition フォルダー) に保存できるかを決めます。
- PBIR レガシーの場合は 、レポート定義は report.json ファイルが使用されます。
- PBIR (新) の場合は、レポート定義は definition\ フォルダーが使用されます。


> **参考情報：**
> - [強化されたレポート形式で Power BI レポートを作成する](https://learn.microsoft.com/ja-jp/power-bi/developer/embedded/projects-enhanced-report-format)
> - [PBIR 形式 | Power BI Desktop プロジェクト レポート フォルダー](https://learn.microsoft.com/ja-jp/power-bi/developer/projects/projects-report?tabs=v2%2Cdesktop#pbir-format)

</br>

---
## PBIX ファイルへの影響
---
PBIX ファイルは、これまでと変わらず、引き続き主要なファイル形式です。PBIR フォーマットの変更は、Power BI レポートの PBIX 内の保存方法に影響しますが、ユーザー体験には全く影響しません。

> **参考情報：**
> - [PBIR will become the default Power BI Report Format – Get Ready for the Transition](https://powerbi.microsoft.com/en-us/blog/pbir-will-become-the-default-power-bi-report-format-get-ready-for-the-transition/)

</br>

---
##  テナント設定 
---

現在 Power BI 管理ポータルのテナント設定に、新たに以下のテナント設定が追加されています。

**Power BI 拡張メタデータ形式 (PBIR) を使用してレポートを自動的に変換し保存する (プレビュー)**

<div align="left">
<img src="1.png">
</div>

PBIR フォーマットは現在パブリックプレビュー中です。パブリックプレビュー期間中に、本設定を無効化することで、PBIR レガシーフォーマットを利用することができますが、
一般提供後には PBIR が PBIR レガシーフォーマットに代わり、唯一サポートされるフォーマットとなり、変換が必要ですので、ご留意ください。
 

---
##  Power BI Desktop の設定
---

Power BI Desktop を使用して既存の Power BI プロジェクト ファイルを作成したり PBIR に変換したりすることが可能です。 変換するには、 Power BI Desktop プレビュー機能で有効にする必要があります。

1. [ファイル]>[オプションと設定]>[オプション]>[プレビュー機能] に移動します。
2. PBIP ファイルの場合、[拡張メタデータ形式を使用してレポートを保存する (PBIR) ] の横にあるチェック ボックスをオンにします。
3. PBIX ファイルの場合、[拡張メタデータ形式 (PBIR) を使用して PBIX レポートを保存する  ] の横にあるチェック ボックスをオンにします。

<div align="left">
<img src="2.png">
</div>
<br>

---
##  PBIR の一般提供の時期 
---

PBIR フォーマットは現在 2026 年 7 月から 9 月ごろ (Q3 2026) に一般提供される予定でございます。

> **参考情報：**
> - [Developer Mode| Microsoft Fabric Roadmap](https://roadmap.fabric.microsoft.com/?product=powerbi)

</br>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)