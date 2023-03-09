---
title: 「インポート」と「Direct Query」データセットの違い
date: 2021-11-30 16:00:00
tags:
  - Power BI
  - データセット
  - データ接続
  - ストレージモード
  - インポート
  - Direct Query
---

こんにちは、Power BI サポート チームのチャンです。

Power BI ご利用のユーザー様から、データ接続の際にインポートモードかDirect Query モードを選択できるが、どの場合にどれを使用すれば良いのか？などの質問をよく頂いていますが、
本ブログでは、インポートモードとDirect Query モードの概要及び利用シーンにつきまして、ご紹介いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
1. [ストレージモードとは？](#ストレージモードとは？)
2. [インポートモードのデータセット](#インポートモードのデータセット)
3. [DirectQueryモードのデータセット](#DirectQueryモードのデータセット)
4. [インポートとDirectQueryの比較](#インポートとDirectQueryの比較)

---
## ストレージモードとは？
---

Power BIからデータソースに接続する際に、データを取得してレポートとして可視化する必要がありますが、データの取得方法（= データセットの作成方法）の種類が「ストレージモード」です。
ストレージモードの種類は、以下の4 つがございます。

- インポート モード
- Direct Query モード
- ライブ接続 モード
- Push モード

今回は上記の4 つから、最も使用されているインポート モードと Direct Query モードについてご説明します。
各データソースでサポートされているストレージモードにつきましては、下記のドキュメントからご確認いただけます。

- 参考情報：[Power BI データ ソース - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/connect-data/power-bi-data-sources)

> [!NOTE]
> **ライブ接続モード**に関しては、Power BI データセット、Analysis Services へ接続する際にのみ使用できます。
> // 参考情報 (1)：[Power BI Desktop から Power BI サービスのデータセットに接続する - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-report-lifecycle-datasets)
> // 参考情報 (2)：[Power BI Desktop で Analysis Services の表形式データに接続する - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-analysis-services-tabular-data)

<p>

> [!NOTE]
> **Push モード**のデータセットに関しては、以下のドキュメントをご参照ください。
> // 参考情報：[Power BI のリアルタイム ストリーミング - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-real-time-streaming)


---
## インポートモードのデータセット
---

Power BI Desktop では、接続済みのテーブルに対して、「>」部分にマウスオーバーすると、ストレージモードをご確認いただけます。

<div align="center">
<img src="desktop_import_mode.png" alt="画像1_インポートモード" title="画像1_インポートモード">
</div>

インポートモードを使用する場合は、外部のデータソースから必要なデータをPower BI 専用の形に変換され、Power BI Desktop の.pbixファイルに実際のデータが取り込まれます。

.pbix ファイル内にインポート時のデータを**保持する**形となりますので、Power BI サービスへ発行された後に、定期的データ更新を行なっていただき、データの鮮度を保つ必要があります。Power BI Pro の共有容量を使用する場合は、1 日最大8 回まで更新スケジュールを設定いただけますが、Premium 容量は1日最大48 回（30 分ごとに）データ更新を設定いただけます。

データ更新の手順につきましては、下記のブログ記事をご参考ください。

- 参考情報：[Power BI サービスのデータセット更新手順について](../pbi_refresh_settings/)

また、Power BI Pro ライセンスのみお持ちで、共有容量へレポートとデータセットを発行する場合、アップロード可能な.pbix ファイルサイズの上限は1GB となります。Premium 容量を使用する場合は、もう少し上限が緩和されますが、詳細につきましては、下記ドキュメントをご確認ください。

| 容量の種類 | 最大データセット サイズ | 
| ---- | ---- | 
| 共有、A1、A2、または A3  | 1 GB | 
| A4 または P1 | 3 GB | 
| A5 または P2 | 6 GB | 
| A6 または P3 | 10 GB | 

- 参考情報：[Power BI でのデータの更新 - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/connect-data/refresh-data#datasets-in-import-mode)


あまりにも大規模のデータを読み込む場合、データのリアルタイム性を保つ必要がある場合、またはデータソース側でユーザーごとのセキュリティー規則を設定していた場合、Direct Query モードのご利用をご検討ください。

---
## DirectQueryモードのデータセット
---

Power BI Desktop では、接続済みのテーブルに対して、「>」部分にマウスオーバーすると、ストレージモードをご確認いただけます。

<div align="center">
<img src="desktop_dq_mode.png" alt="画像2_DirectQueryモード" title="画像2_DirectQueryモード">
</div>

Direct Query モードを使用する場合、レポートまたはダッシュボードからデータを読み込む操作を行なう際に、Power BI でその操作を変換し、データソースへクエリを発行します。

そのため、.pbix ファイル内ではデータをインポートせず、データを**保持しない**形となります。Power BI サービスへ発行後でも、データセットのスケジュール更新を設定する必要はございません。ただし、データソースとの接続において、資格情報の入力、または状況によってゲートウェイの設定も必要ありますので、ご留意ください。

しかしながら、Direct Query モードを使用する場合の影響及び制限事項が多くあります。以下にて一部の例を挙げます。

#### 1. データソースの負荷

Power BI から、都度データソースへクエリが発行されますので、レポートの利用頻度や、実際発行されるクエリによって読み込まれるデータ量などによって、データソースへ大きな負荷となってしまう場合が考えられます。

実際、都度データソースとの通信が必要となるため、インポートモードのデータセットを使用しているレポートと比較して、レスポンスが遅いと感じるケースが多くあります。通常は5 秒未満のレスポンスタイムが妥当であると想定いただければ幸いです。

データのモデリングで複雑な処理が含まれる場合、クエリがタイムアウトとなることもあります（Power BI サービス内の個々のクエリには、4 分のタイムアウトが適用されます）。

#### 2. データ変換及びモデリングの制限

一部のDAX 関数やPower Query エディターを使用するデータ変換の処理は、Direct Query モードではサポートされません。

例えば、日付データに関して、Direct Query モードでは秒までの精度のみサポートされ、ミリ秒や組み込みの日付階層はサポートされません。

他に計算テーブルの使用もサポートされません。なお、計算列の DAX を作成するとき、サポートされない関数はオートコンプリートにリストされず、使用するとエラーが発生します。

Power Query エディターでデータ変換を行う場合、Direct Query モードでサポートされない変換に関しては、エラーが発生します。具体的には、共通テーブル式を使うクエリや、ストアド プロシージャを呼び出すクエリを使うことはできません。

#### 3. ストレージモードの切替

Direct Query モードから、インポートモードへの切替は可能ですが、逆の場合、インポートモードからDirect Query モードへの切替はできません。Direct Query モードを使用する場合は、最初から接続のストレージモードをご指定いただき、データの読み込みや変換を行なっていただく必要がございます。

上記ご案内した内容の他にも、制限事項や影響がありますので、それらにつきましては、下記のドキュメントをご確認ください。

- 参考情報：[Power BI で DirectQuery を使用する - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-directquery-about#implications-of-using-directquery)

---
## インポートとDirectQueryの比較
---

以下にてインポートモードとDirect Query モードの違いにつきまして、下記の比較表にまとめておきました。

|  | **インポート**  | **Direct Query** | 
| ----- | ----- | ----- | 
| **データの保持** | 〇 | ×  | 
| **スケジュールされたデータ更新**  | 〇 | × |
| **データのリアルタイム性** | △ <br>※別途データ更新の設定が必要 | ◎ <br>※都度データソースへクエリが発行される | 
| **非常に大きなデータ** | △ <br>※発行可能な.pbix ファイルのサイズ制限がある | 〇 <br>※ビジュアルを読み込む度に、クエリが発行される | 
| **制限事項の少なさ** | ◎ <br>※データセットのサイズ制限はある | △ <br>※データ変換やモデリングにおいて制限事項が多い  | 
| **データソース側の負荷**  | 〇 <br>※データ更新時のみ | △ <br>※レポートを閲覧される際に都度クエリが発行される | 

<p>

> **参考情報**
> - [Power BI での DirectQuery の使用について - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-directquery-about)
> - [Power BI Desktop でストレージ モードを管理する - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-storage-mode)
> - [Power BI でのデータの更新 - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/connect-data/refresh-data)

> **本ブログの関連記事**
> - [Power BI サービスのデータセット更新手順について](../pbi_refresh_settings/)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)