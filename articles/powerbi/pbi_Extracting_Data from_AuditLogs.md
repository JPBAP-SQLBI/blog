---
title: 監査ログのAuditDataカラムからデータを抽出する方法
date: 2025-04-30 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - AuditLog
  - 監査ログ
  - Extraction
  - 抽出
  - DAX

---


こんにちは、Power BI サポート チームのファムです。 

Power BI のユーザーアクティビティログには、セキュリティ対策や利用状況の把握、コンプライアンス対応に役立つ情報が含まれています。ログを定期的に確認することで、Power BI をより安心して活用することができます。また、ログの取得だけでなく、監査ログのデータはCSVファイルにエクスポートすることができ、そのファイルの中のAuditData カラムには、監査対象のアクティビティの詳細情報が含まれます。このため、 「AuditData カラムの内容を Power BI 上で分析したい」といったご要望をいただくことがあります。

本ブログでは、監査ログファイルの AuditData カラムから必要な情報を抽出する方法の一例をご紹介します。

<!-- more -->

>[!NOTE]
>本ブログでは、Power BIにおける JSONデータの扱い方の一例として、DAX関数を用いた方法をご紹介しています。
>目的やデータの特性によっては、Power Queryを使用する方法など、他にもさまざまなアプローチが考えられますので、運用シナリオに応じてご検討ください。

</br>

> [!IMPORTANT]
> 弊社サポートをご利用いただいている場合、状況に合わせた調査方針を策定するため、記載の内容とご案内が異なる場合がございます。
> ご不明な点がございましたら弊社サポート担当までお気軽にご質問ください。
> また掲載している画像・手順は投稿時点のものとなります。最新の情報とは異なる可能性がございますので予めご了承ください。

</br>

---
## 目次
---
1. [監査ログとは](#1．監査ログとは)
2. [AuditDataカラムの値を抽出するDAX関数の説明](#2．AuditDataカラムの値を抽出するDAX関数の説明)
3. [AuditDataカラムの値を抽出して新しい列を作成する手順](#3．AuditDataカラムの値を抽出して新しい列を作成する手順)
</br>

---

## 1．監査ログとは

監査ログは、システム内で行われたアクティビティを記録したもので、ユーザーの操作、システムの変更、データのアクセス状況などが含まれます。例えば、Power BI レポートの表示に関するアクティビティログを通じて、誰がいつ、どの環境からレポートにアクセスしたかを追跡することができます。これらの監査ログは、Microsoft Purview ポータルから取得することが可能です。監査ログの取得方法は、以下の手順をご参考ください。

1) Microsoft Purview ポータルのリンクにアクセスします。
https://purview.microsoft.com/audit/

2) 表示されている画面を適宜変更し、“**検索**”ボタンを押下してください。

</br>

<div align="center">
<img src="pic1.png">
</div>

**❶日付と時刻の範囲 (UTC)**
過去7日間がデフォルトで選択されています。日付と時間を選んで、その期間内のイベントを表示します。最大180日まで選択可能です。180日を超えるとエラーが表示されます。
ヒント: 最大180日を選ぶ場合は、開始日を現在の時刻に設定してください。開始日が終了日より後になるとエラーが出ます。また、監査を有効にした日より前の日付は選べません。

**❷キーワード検索**
監査ログで検索するキーワードやフレーズを入力します。特殊文字を含む場合は、アスタリスク(*)に置き換えてください。例: test_search_document → test*search*document
ヒント: キーワード検索はインデックス付きコンテンツ内でのみ行われます。監査データコンテンツは検索されません。

**❸管理単位**
ドロップダウンリストから監査対象の管理単位を選びます。複数選択可能です。すべての管理単位を検索する場合は空白のままにします。

**❹アクティビティ - フレンドリ名**
ドロップダウンリストから監査済みアクティビティのフレンドリ名を選びます。ユーザーと管理者のアクティビティはグループに分かれています。特定のアクティビティやグループを選択できます。検索ボックスでフレンドリ名を検索することも可能です。

**❺アクティビティ - 操作名**
検索結果に含める正確な操作名を入力します。複数の操作名はコンマで区切って入力できます。操作名は正確に入力する必要があります。例: SPOIBIsEnabled,SPOIBIsDisabled
ヒント: 操作名が正しくないと結果は返されません。

**❻レコードの種類**
ドロップダウンリストから監査済みアクティビティのレコードの種類を選びます。複数選択可能です。例: MIPLabel, MipAutoLabelExchangeItem

**❼検索名**
検索ジョブのカスタム名を入力します。名前を入力しない場合、自動的に名前が付けられます。

**❽ユーザー**
検索結果に表示するユーザーの名前を選びます。すべてのユーザーを検索する場合は空白のままにします。

**❾ファイル、フォルダー、またはサイト**
指定したキーワードを含むファイルやフォルダーの名前を入力します。URLを使用する場合は、完全なURLパスを入力するか、特殊文字やスペースを含まない部分的なURLを入力してください。

**❿ワークロード**
関連するアクティビティを検索するワークロードサービスを入力または選択します。


> **参考情報**
>  [監査ログの検索](https://learn.microsoft.com/ja-jp/purview/audit-search)


3) 監査ログのファイルをエクスポートします。
検索結果を選択し、「**エクスポート**」ボタンをクリックしてファイルをダウンロードします。

</br>

<div align="center">
<img src="pic2.png">
</div>


4) 監査ログのCSVファイルを開くと以下のイメージをご確認いただけます。
エクスポートした監査ログのCSVファイルは以下のようなイメージです。

</br>

<div align="center">
<img src="pic3.png">
</div>

エクスポートしたファイルはCSV形式ですが、 AuditData カラムはJSON形式となっています。このJSONを成型すると、例えば、どのアイテムのアクティビティログか、アイテムのワークスペース名は何か、どのオペレーションで実施したか、どの環境で利用されていたか、などの情報が入っています。これらの情報を抽出する方法について次の章で説明します。

</br>

<div align="center">
<img src="pic4.png">
</div>

また、Power BIのユーザーアクティビティ追跡方法について、以下のPower BIサポートチームのブログを詳細にまとめておりますので、併せてご確認ください。

> **参考情報**
>  [Power BI のユーザーアクティビティ追跡方法の比較](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_activity_log_usage_metrics/)



## 2．AuditDataカラムの値を抽出するDAX関数の説明
例えば、AuditDataカラムの値から、アイテム名（ItemName）を抽出したい場合のシナリオを考えます。

</br>

<div align="center">
<img src="pic5.png">
</div>

DAX関数の利用方法については、Power BI Desktopでレポートを開き、「**ホーム**」 ＞ 「**新しい列**」をクリックします。以下のイメージの青枠にDAX関数を入力し、新しい列を作成します。

</br>

<div align="center">
<img src="pic6.png">
</div>

以下のDAX式はAuditDataカラムの値から、特定のキーである"**ItemName**"に関連する値を抽出します。SEARCH、MID、IF、TRIMといったDAX関数を組み合わせて作成されます。

>[!NOTE]
>本DAX式および手法は一つのサンプルであり、Power BIサポートチームはDAX関数に関する開発支援をサポートしかねますので、予めご理解ください。お客様のシナリオに合わせて適宜ご活用いただければ幸いです。

```CMD

ItemName = 
VAR StartPos = SEARCH("""ItemName"":""", 'auditLog'[AuditData], 1, BLANK()) + LEN("""ItemName"":""")
VAR EndPos = SEARCH(""",""WorkSpaceName"":""", 'auditLog'[AuditData], StartPos, BLANK())
VAR ExtractedText = IF(
    NOT ISBLANK(StartPos) && NOT ISBLANK(EndPos) && EndPos > StartPos,
    MID('auditLog'[AuditData], StartPos, EndPos - StartPos),
    BLANK()
)
RETURN
    TRIM(ExtractedText)

```

**StartPosの計算** 
```CMD
VAR StartPos = SEARCH("""ItemName"":""", 'auditLog'[AuditData], 1, BLANK()) + LEN("""ItemName"":""")
```

・SEARCH関数は、'auditLog'[AuditData]カラムの中から特定の文字列"ItemName":"を探し、その開始位置を返します。
・見つかった位置に、LEN("""ItemName"":""")を加算することで、"ItemName":"の直後の位置、つまり実際に抽出したいテキストの開始位置を求めます。
・もし"ItemName":"が見つからなければ、SEARCH関数はBLANK()を返します。

**EndPosの計算**
```CMD
VAR EndPos = SEARCH(""",""WorkSpaceName"":""", 'auditLog'[AuditData], StartPos, BLANK())
```

・SEARCH関数を使って、"WorkSpaceName":"という文字列を探します。ただし、検索の開始位置をStartPosからに設定しています。これによって、"ItemName":"の後から"WorkSpaceName":"までの間のテキストを抽出する準備をします。
・もし"WorkSpaceName":"が見つからなければ、SEARCH関数はBLANK()を返します。

**ExtractedTextの計算**
```CMD
VAR ExtractedText = IF(
    NOT ISBLANK(StartPos) && NOT ISBLANK(EndPos) && EndPos > StartPos,
    MID('auditLog'[AuditData], StartPos, EndPos - StartPos),
    BLANK()
)
```

・IF関数を使って、StartPosとEndPosがともにBLANK()でなく、さらにEndPosがStartPosよりも大きい場合にのみ、MID関数を使ってテキストを抽出します。
・MID関数は、'auditLog'[AuditData]からStartPosの位置から始まり、長さがEndPos - StartPosのテキストを抽出します。
・条件を満たさない場合は、BLANK()を返します。

**最終的な結果の返却**
RETURN
    TRIM(ExtractedText)

・TRIM関数を使って、抽出されたテキストの前後の余分なスペースを取り除きます。
・最終的に整形されたテキストがItemName列として返されます。




## 3．AuditDataカラムの値を抽出して新しい列を作成する手順
1) Power BI Desktopを起動します。
「**データを取得**」 ＞ 「**テキスト/CSV**」 をクリックし、監査ログのCSVファイルを選択します。

</br>

<div align="center">
<img src="pic7.png">
</div>

2) CSVファイルを読み込み後、以下のデータビューをご確認できます。

</br>

<div align="center">
<img src="pic8.png">
</div>


3) ItemNameの新しい列を作成します。
「**テーブル ビュー**」 ＞ 「**ホーム**」 ＞ 「**新しい列**」をクリックし、第2章で説明したDAX関数を入力します。“**ItemName**”という列が作成されており、アイテム名を取得できることをご確認いただけます。

>[!NOTE]
>今回の検証では、**AuditLog**のテーブル名にしましたが、お客様のシナリオに合わせてDAX関数の'auditLog'[AuditData]の部分については適宜変更してください。

</br>

<div align="center">
<img src="pic9.png">
</div>

4) ItemNameの列と同様に取得したい情報を他の列にも作成します。
例えば、WorkSpaceNameの値を抽出する場合のDAXの関数は、以下のイメージの通りです。ItemNameのDAX関数と同様で、ハイライト部分を適宜変更してください。

</br>

<div align="center">
<img src="pic10.png">
</div>


同様に、Operation、UserID、ConsumptionMethod、DistributionMethodなどを新しい列で値を取得できます。取得後の列は、以下のイメージをご確認ください。その他の情報を取得されたい場合、同様の手順でカスタマイズしてみてください。

</br>

<div align="center">
<img src="pic11.png">
</div>


</br>
以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
