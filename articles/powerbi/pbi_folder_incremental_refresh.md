---
title: Power BI でフォルダー・SharePointフォルダーコネクタを使用した増分更新
date: 2022-09-27 18:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - Power BI サービス
  - Power BI Service
  - Power Query
  - データセット
  - 増分更新
  - Incremental Refresh
  - Folder Connector
  - Sharepoint Folder Connector
  - フォルダーコネクタ
  - Sharepoint フォルダーコネクタ
---

こんにちは、Power BI サポート チームのチャンです。   

ローカル環境やファイルサーバーのフォルダーに保存されている Excel や Csv ファイル、SharePoint にあるフォルダーに保存されているExcel や Csv ファイルに対して、 Power BI サービスでデータ更新を実施する際に、毎回全てのファイルを取り込まずに、一部のファイルのみ読み込んで増分更新する方法はよくお問い合わせをいただきますが、
通常のデータベースの増分更新の設定より、少し工夫しておく必要がございますので、以下にてその詳細をご紹介いたします。

<!-- more -->


> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 予めご了承ください。


---
## 目次
---
1. [増分更新の基本条件](#増分更新の基本条件)
2. [フォルダーの複数ファイルに対して増分更新を設定する方法](#フォルダーの複数ファイルに対して増分更新を設定する方法)
3. [参考情報](#参考情報)
4. [ダウンロード](#ダウンロード)
</br>

---
## 増分更新の基本条件
---

#### 1. 日付列
増分更新を行なうテーブルには、日付/時刻の日付列が含まれている必要があります。 RangeStart および RangeEnd というパラメーター (日付/時刻データ型である必要があります) を作成し、その日付列に基づいてテーブル データをフィルター処理し、増分更新を行ないます。 

#### 2. クエリ フォールディング
増分更新は、クエリ フォールディング をサポートするデータ ソース用に設計されています。 SQL クエリをサポートするほとんどのデータ ソースは、クエリ フォールディングをサポートしています。 フラット ファイル、BLOB、一部の Web フィードなどのデータ ソースでは、サポートされません。

#### 3. その他データソースの場合
通常フォルダーコネクタや SharePoint フォルダーコネクタからファイルを読み込む場合、上述したクエリ フォールディングをサポートしておりません。
ただし、追加のカスタム クエリ関数とクエリ ロジックを使用することにより、RangeStart と RangeEnd に基づくフィルターを 1 つのクエリで渡すことができる場合は、増分更新を他の種類のデータ ソースで使用できます。 たとえば、フォルダーに格納されている Excel ブック ファイル、SharePoint 内のファイル、RSS フィードなどです。 

> [!TIP]
> 参考：[データセットの増分更新とリアルタイム データ](https://learn.microsoft.com/ja-jp/power-bi/connect-data/incremental-refresh-overview#requirements)

</br>

---
## フォルダーの複数ファイルに対して増分更新を設定する方法
---

今回は、カスタマイズしたクエリロジックを使用して、フォルダーコネクタを使用した増分更新を設定した手順をご紹介いたします。

1. Power Query エディターを開き、[ホーム] タブの [データを取得] ボタンをクリックし、 [フォルダー] を選択します。
（ SharePoint フォルダーの場合は [SharePoint フォルダー] を選択します。）

<div align="center">
<img src="1.png">
</div>


2. 結合予定のファイルが保存されているフォルダーを指定し、 [OK] ボタンをクリックします。
対象フォルダー内のファイルがすべて表示されますので、 [データの変換] を選択します。

<div align="center">
<img src="2.png">
</div>


3. [ホーム] タブの [パラメーターの管理]から、増分更新の設定に必要な RangeStart パラメーターと RangeEnd パラメーターを作成します。

> [!TIP]
> 種類は日付／時刻を指定する必要がありますが、現在の値は任意の開始値と終了値を入力してください。

<div align="center">
<img src="3.png">
</div>

4. ファイルの作成日によって増分更新を設定できるように、 Date Created 列に対して RangeStart と Range End のパラメーターを使用してフィルターを設定します。

> [!TIP]
> 最初の条件で [次より後] を選んだ場合は、 [次の値以前] を選びます。あるいは、最初の条件で [次の値以降] を選んだ場合は、2 番目の条件で [次の前] を選び、 [パラメーター] を選択してから [RangeEnd] を選びます。 たとえば、次のように入力します。 

<div align="center">
<img src="4.png">
</div>


5. 他のフィルター条件などを設定し、ファイルの結合を行ないます。

<div align="center">
<img src="5.png">
</div>


6. 引き続きその他のデータ整形ステップを実施し、最終系のデータが整えましたら、増分更新を設定する際に、エラーを回避するために、以下の部分の追加・変更を行ないます。

> [!TIP]
> この詳細エディターで修正するステップは、フォルダーや SharePoint フォルダーを使用して、増分更新を実施する際のキーポイントとなります。
> Date Created 列を使用した増分更新を設定する際に、Power BIサービス上で増分更新のパーティションが作成されますが、その後のファイル結合ステップの前に、フィルター条件によってデータのないパーティションが生成され、展開・結合できないエラーが発生します。
> そのエラーを回避するために、データのない場合は別のステップを指定するように変更します。

<div align="center">
<img src="6-1.png">
</div>

- 最後のステップの後ろに、「 , 」を追加します。

- 以下のような3行を追加します。それぞれ次の理由となります。
  - Table.IsEmpty() の中身で指定するステップは、展開（結合）される前のステップを指定します。
  - SchemaのTableの中身<font color="DarkSalmon"> [Source.Name = text, Date = datetime, Value = number, Category = text, Book = text, Sheet = text] </font>は最終的なテーブルフォーマットに沿って、列名とデータ型を指定する必要があります。
  - #"Result" のステップで、 else の後ろに指定するステップは直前のステップ名です。

```
    #"IsEmpty" = Table.IsEmpty(削除された他の列1),
   Schema = #table( type table [Source.Name = text, Date = datetime, Value = number, Category = text, Book = text, Sheet = text], {}),
    #"Result" = if #"IsEmpty" = true then Schema else 変更された型
```

- 締めの「In …」ステートメントは最後のステップの名前に合わせて変更します。

```
in
    #"Result"

```

</br>

変更前と変更後の違いについて、下記の画像にてご確認ください。

<div align="center">
<img src="6-2.png">
</div>


</br>

7. Power Queryを [閉じて適用] し、保存して Power BI Desktop に戻り、増分更新のアーカイブ分と更新分の設定を実施します。

<div align="center">
<img src="7.png">
</div>

8. 最後にpbixファイルを保存し、Power BIサービスへ発行し、以下のブログ記事に記載されている手順を沿ってデータ更新を実施してください。

参考：[Power BI サービスのデータセット更新手順について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_refresh_settings/)

</br>

---
### 参考情報
---
-  [Incremental refresh for files in a Folder or SharePoint – Power BI](https://www.thepoweruser.com/2020/01/19/incremental-refresh-for-files-in-a-folder-or-sharepoint-power-bi/)

</br>

---
### ダウンロード
---

- [フォルダーコネクタで読み込むサンプルファイルのダウンロードはこちら](Incremental.zip)
- [このPower BIレポートのサンプルダウンロードはこちら](Folder_Incremental.pbix)

</br>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)