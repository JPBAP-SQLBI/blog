---
title: メジャーと計算列（新しい列）の比較
date: 2024-03-29 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - Creator
  - Learning
---


こんにちは、Power BI サポート チームの中川です。

Power BI は、既存のセマンティックモデルにデータを追加したいときに、DAX式を使用してメジャーまたは計算列を作成することができますが、それぞれの特徴を理解し、適切な用途で使用する必要があります。例えば、計算列を多用するとモデルの更新時間や表示速度の低下につながることがあります。

本ブログでは、2つの概念を紹介し、これらを利用した効果的なデータモデリングについてご紹介いたします。

<!-- more -->

</br>

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
 1.[作成方法](#作成方法)
 2.[メジャー](#メジャー)
 3.[計算列](#計算列)
 4.[モデルサイズの比較](#モデルサイズの比較)
 5.[まとめ](#まとめ)


---
## 作成方法
---
Power BI Desktop でメジャーおよび計算列を作成する方法は以下の2通りがございます。

・「データ」フィールドのテーブルを右クリックして選択
・「モデリング」タブから選択

1つ目は意図するテーブルに作成できるため、この方法を推奨いたします。
2つ目は意図したテーブルと異なる場所に作成される可能性があり、データモデルの管理コストが上がってしまうため、可能な限り1つ目の方法の利用を推奨します。

</br>
<div align="center">
<img src="1.png">
</div>

// 参考情報：[Data Model / DAXの基礎 2_ルールいろいろ① - テクテク日記 (hatenablog.com)](https://marshal115.hatenablog.com/entry/2021/04/29/111308)

</br>

---
## メジャー
---
メジャーは DAX 式を用いて定義され、データモデル全体で利用される特定の計算や集計を実行できます。特に集約関数（SUM, AVERAGE, MIN, MAXなど）を用いてデータの集計を行いますが、後述の計算列とは異なり、メジャーはコンテキストが変わると動的に計算され、その時々のコンテキストに応じた集計値を提供します。

メジャーによる計算結果はモデルに格納されず、クエリ実行時に毎回計算されます。セマンティックモデルの更新時間やサイズに直接的な影響を与えることはありません。ただし、複雑な計算や大量のデータに基づくメジャーは、クエリの応答時間を遅延させる可能性があるため、パフォーマンスへの影響に留意する必要があります。


使用例：
データの集約：各地域の総売上や期間ごとの平均販売数を計算します。
動的分析：同期比較や前年比較などの成長率を計算します。

 「データ」ペインでは、メジャーは電卓アイコン付きで表示されます。 次の例は、Sales テーブルの 3つのメジャーを示しています (Cost, Profit, Revenue)。

<div align="center">
<img src="2.png">
</div>
</br>

// 参考情報：[Power BI Desktop のメジャー - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-measures)
// 参考情報：[チュートリアル: Power BI Desktop で独自のメジャーを作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-tutorial-create-measures)

</br>

---
## 計算列
---
計算列はセマンティックモデル内の特定テーブルに DAX 式を用いて新しく追加される列で、テーブルの各行に対し個別に評価されることで行ごとに値を生成します。セマンティックモデルの更新に一度だけ計算され、その結果がモデル内に物理的に格納されるため、モデルの全体サイズを増加させる可能性があります。特にインポートモードのテーブルでの使用時は、サイズ増加がより顕著になります。

この特性から、レポートやビジュアルを表示する際に追加の計算が不要となり、結果としてビジュアルの応答性が向上します。しかし、計算列の数や計算式の複雑さが増すほど、データモデルの更新に要する時間が増加し、最終的にユーザーエクスペリエンスに影響を与える可能性があるため、計算列の使用は慎重に計画する必要があります。

使用例：
テキスト値の結合： 「都道府県」フィールドと「市区町村」フィールドを結合して「場所」フィールド（例: "東京都新宿区"）を生成します。
新たな計算： 「売上」列と「コスト」列から「利益」列を計算します。

「データ」ペインでは、計算列は特別なアイコンで強調されています。 次の例は、Customer テーブルの Age という 1つの計算列を示しています。

<div align="center">
<img src="3.png">
</div>
</br>

// 参考情報：[Power BI Desktop で計算列を使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-tutorial-create-calculated-columns)
// 参考情報：[チュートリアル: Power BI Desktop で計算列を作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-calculated-columns)


メジャーと計算列の特徴を表にまとめると以下の通りになります。

| **特徴** | **メジャー**  | **計算列** | 
| ----- | ----- | ----- | 
| **計算タイミング** | レポートのクエリ実行時に毎回動的に計算する | モデルの更新時に一度だけ  | 
| **データサイズ**  | ほとんど変わらない（クエリ実行時に動的に計算） | 追加した列の数に伴い増加（セマンティックモデル内に静的に格納） |
| **使用例** | データの集約や分析 | 新しいデータ項目の作成 | 

</br>
</br>


---
## モデルサイズの比較
---
データサイズについて、メジャー、計算列を使用した場合のサイズについて比較してみます。
試用するデータは [チュートリアル: Power BI Desktop で計算列を作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-tutorial-create-calculated-columns) の中にある [Contoso Sales Sample for Power BI Desktop](<https://download.microsoft.com/download/4/6/A/46AB5E74-50F6-4761-8EDB-5AE077FD603C/Contoso Sales Sample for Power BI Desktop.zip>) を使用します。

ファイルをダウンロード、開いた際に表示される「今すぐ更新」ボタンを押下・保存時のファイルのサイズは「49,763KB」でした。

<div align="center">
<img src="4.png">
</div>
</br>

メジャー用、計算列用にそれぞれファイルを用意し、以下のDAX式で作成を行った結果のデータサイズを確認してみます。

【メジャー】
```sql
Gross Profit = SUM(Sales[SalesAmount]) - SUM(Sales[TotalCost])
Net Sales = SUM(Sales[SalesAmount]) - SUM(Sales[DiscountAmount]) - SUM(Sales[ReturnAmount])
Net Sales Quantity = SUM(Sales[SalesQuantity]) - SUM(Sales[ReturnQuantity]) - SUM(Sales[DiscountQuantity])
```
【計算列】
```sql
 Gross Profit = Sales[SalesAmount] - Sales[TotalCost]
 Net Sales = Sales[SalesAmount] - Sales[DiscountAmount] - Sales[ReturnAmount]  
 Net Sales Quantity = Sales[SalesQuantity] - Sales[ReturnQuantity] - Sales[DiscountQuantity]   
```
メジャーまたは計算列を追加した.pbixファイルのサイズは以下の通りとなりました。
オリジナル：49,763KB
メジャー　：49,768KB
計算列　　：57,721KB

これらから、計算列を使用するとデータモデルのサイズが大きく増加することが確認できました。一方で、メジャーはデータサイズにほとんど影響を与えていません。そのため、不必要に計算列を多用せず、必要に応じてメジャーの使用を検討することが、効率的なデータモデル設計において推奨されます。

<div align="center">
<img src="5.png">
</div>
</br>

DAX 式を使用したレポートのパフォーマンス測定や最適化については以下をご一読ください。

// 参考情報：[Power BI 利用時のパフォーマンス測定や最適化について | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/performance/)

</br>

---
## 適切な使用方法
---
メジャーと計算列の違いを理解した上で、それぞれの使用目的や適切な使用法を考えてみます。それぞれの特徴を踏まえ、適したシナリオまたは注意点について整理します。

【メジャー】
● 集約や複雑な計算が必要な場合、またはフィルターやスライサーのコンテキストに基づいて結果が動的に変わる必要がある場合に有効です。
● メジャーは再利用性が高いため、複数のビジュアルで同じ計算を使用する場合に便利です。類似の計算が必要な場合は、既存のメジャーを再利用することで、モデルの整合性を保ちつつ、開発時間を短縮できます。
● 複雑なメジャーは計算コストが高い可能性があり、特に大規模なデータセットや多くのフィルターを使用する場合、パフォーマンスに影響を与えることがあります。メジャーの複雑な計算能力を活用する際には、そのパフォーマンスへの影響を常に意識し、パフォーマンスアナライザー等を用いて定期的に分析を行うことが重要です。

// 参考情報：[Power BI Desktop でパフォーマンス アナライザーを使用してレポート要素のパフォーマンスを確認する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/desktop-performance-analyzer)


【計算列】
●	テーブルや列の関係を参照する必要がある場合に使います。異なるテーブルにある列を結合したり、関連する列の値を取得したりする場合には、計算列を使います。
●	計算結果が変わらない場合に利用します。商品のカテゴリーや顧客の地域など、データの属性を表す場合には、計算列が有効です。
●	計算列を多用するとモデルの更新時間や表示速度の低下につながることがあります。そのため、計算列は、必要不可欠なものだけを作成することを推奨します。

</br>

---
## まとめ
---
この記事では、メジャーと計算列を利用した効果的なデータモデリングについて解説しました。メジャーと計算列は、Power BIでデータを加工するための計算式を作成する方法ですが、その役割や仕組みは異なります。メジャーと計算列の違いを理解し、それぞれのパフォーマンスや使用目的、適切な使用法を把握することで、データ分析の効率や品質を向上させることができます。
この記事で紹介した内容は、データモデリングの基礎的な部分についてのものです。データモデリングには、他にもさまざまなテクニックやベストプラクティスがあります。データモデリングのスキルをさらに向上させるためには、以下のリソースも参考にしてください。

// 参考情報：[Power BI を学習するために役に立つコンテンツのご紹介 | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_useful_learning_link/)
// 参考情報：[Power BI Desktop で DAX を使用する - Training | Microsoft Learn](https://learn.microsoft.com/ja-jp/training/paths/dax-power-bi/)
// 参考情報：[Data Model / DAXの基礎 2_ルールいろいろ① - テクテク日記 (hatenablog.com)](https://marshal115.hatenablog.com/entry/2021/04/29/111308)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。


※本情報の内容（添付文書、リンク先などを含む）は作成日時点でのものであり、予告なく変更される場合があります。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)