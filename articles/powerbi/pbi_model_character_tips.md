---
title: Power BI での大文字小文字の区別
date: 2022-03-31 00:00:00 
tags:
  - Power BI
  - Power Query
  - データセット
---

こんにちは、Power BI サポート チームの山本です。   

よくお問い合わせを頂くPower BI における大文字小文字の区別について、
Power BI における取り扱いと、同一文字列として扱われないように回避する方法についてご紹介いたします。

<!-- more -->


> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 予めご了承ください。


---
## 目次
---
1. [Power BI では大文字と小文字が区別されない？](#Power-BI-では大文字と小文字が区別されない？)
2. [大文字と小文字を区別させる方法について](#大文字と小文字を区別させる方法について)
3. [本方法での注意点](#本方法での注意点)
</br>

---
## Power BI では大文字と小文字が区別されない？
---

次のようなテーブルがあるとします。
ID 1 と 2、 3 と 4 はそれぞれ Name が大文字小文字で区別されています。

| ID | Name | Value |
| - | - | - |
| 1 | aaa | 10 |
| 2 | AAA | 10 |
| 3 | bbb | 10 |
| 4 | BBB | 10 |

このテーブルをPower BI へ取り込むと、ID 2 と 4 の Name が小文字に変わっています。

<div align="center">
<img src="1.png">
</div>

Power BI のモデルでは、大文字と小文字を区別しないロケールが使用されているため、大文字の "AAA" と 小文字の "aaa" は同等に扱われます。例として "aaa" が最初にデータベースに読み込まれた場合、"AAA" のように大文字と小文字だけが異なる他の文字列は、"aaa" として読み込まれ、同じ値として認識されます。

読み込み順序については、実際に弊社サポートで検証した結果、次のような挙動になることを確認しています。

| Power Query エディタ上の表示 | Power BI レポート上の表示 |
| - | - |
| 先に小文字が含まれる文字列が保存される場合</br> <div align="center"><img src="2.png"></div> | <div align="center"><img src="2-1.png"> |
| 同じ文字列が存在しない場合</br> <div align="center"><img src="2-2.png"></div> | <div align="center"><img src="2-3.png"> |
| 先に大文字が含まれる文字列が保存される場合</br> <div align="center"><img src="2-4.png"></div> | <div align="center"><img src="2-5.png"> |


</br>

---
## 大文字と小文字を区別させる方法について
---

上記は Power BI の製品上の挙動にはなるのですが、「それでも意味が変わるので大文字と小文字は別のデータとして扱いたい！」という方には、以下の方法をお試しいただければと思います。

> [!TIP]
> この手法では、大文字と小文字の区別を行なうために、Unicode の Zero-Width Space 文字と Character.FromNumber 関数を使用しています。

1. Power Query エディターを開き、[ホーム]タブの[新しいソース - 空のクエリ]をクリックします。

<div align="center">
<img src="11.png">
</div>


2. [ホーム]タブの[詳細エディター]をクリックし、次のクエリを入力します。
Source = table1 には、区別をしたいテーブル名を、Text.ToList([Name]) には区別をしたい列名に置き換えてください。

```
let
  Source = table1,
  ToList = 
    Table.AddColumn(
      Source, 
      "Chars", 
      each Text.ToList([Name])
    ),
  LowerCaseChars = {"a".."z"},
  AddInvisibleChars = 
    Table.AddColumn(
      ToList, 
      "AddInvisibleChars",
      each List.Transform(
        [Chars],
        each if List.Contains(LowerCaseChars, _) 
          then _ & Character.FromNumber(8203) 
          else _
      )
    ),
  RecombineList =
    Table.AddColumn(
      AddInvisibleChars,
      "OutputText",
      each Text.Combine([AddInvisibleChars]),
        type text
    ),
  RemovedOtherColumns =
    Table.SelectColumns(
      RecombineList,
      {"OutputText"}
    )

in 
  RemovedOtherColumns
```
</br>

<div align="center">
<img src="3.png">
</div>

3. 右側 [クエリの設定] より、[適用したステップ] の [RecombineList] ステップを選択します。

<div align="center">
<img src="4.png">
</div>

4. [ホーム]タブの[列の選択]をクリックし、ステップの挿入に関するポップアップが表示されますが、[挿入]をクリックします。

<div align="center">
<img src="5.png">
</div>

5. 列の選択に関するポップアップ内の変換後の列(OutputText)と他の列(今回の場合[ID]や[Value])を選択し、[OK]をクリックします。

<div align="center">
<img src="6.png">
</div>

6. 最後の[RemovedOtherColumns] ステップを削除します。

<div align="center">
<img src="7.png">
</div>

7. Power BI へデータを読み込み、大文字と小文字が区別されているかご確認ください。

<div align="center">
<img src="8.png">
</div>


*元のテーブルの読み込みが不要な場合は、Power Query エディターで クエリを右クリックし、[読み込みを有効にする]のチェックを解除してください。

<div align="center">
<img src="9.png">
</div>


</br>

---
## 本方法での注意点
---

大文字小文字を区別している Web リンクへ当方法を適用する場合、
Zero-Width Space もエンコードされてしまい、結果として意図したリンクに遷移できなくなる点、ご注意ください。

// “Uri.EscapeDataString” にて対象の文字(“support”) の特殊文字をエスケープすることで、実際の URL には”%E2%80%8B”(Zero-Width Space) が付与されています。

<div align="center">
<img src="10.png">
</div>

Power BI レポートにおいて、大文字小文字を区別するURL が必要となる場合、
Web サーバー側などアクセス先でURL を書き換えていただいたり、ページ分割されたレポートをご活用いただく方法をご検討ください。

> [!TIP]
> ページ分割されたレポートでは Power BI レポートとはアーキテクチャが異なり、データソースから取得したデータは大文字小文字が区別されて表示されます。また、クリック時のアクションとしてURLが格納されている列を指定してURLへ遷移することが可能です。
> 詳しくはこちら：[Power BI のページ分割されたレポートとは](https://learn.microsoft.com/ja-jp/power-bi/paginated-reports/paginated-reports-report-builder-power-bi)


</br>

#### 参考情報
- [Power BI でサポートされる言語と国または地域 - Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/supported-languages-countries-regions#choose-the-language-for-the-model-in-power-bi-desktop)
- [Power BI And Case Sensitivity](https://blog.crossjoin.co.uk/2019/10/06/power-bi-and-case-sensitivity/)

</br>

[このPower BIレポートのサンプルダウンロードはこちら](https://github.com/JPBAP-SQLBI/blog/raw/main/articles/powerbi/pbi_model_character_tips/sample_pbix/CaseSensitivitySample.pbix)

</br>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)