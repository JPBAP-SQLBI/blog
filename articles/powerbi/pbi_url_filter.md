---
title: URL フィルターの使い方 
date: 2025-09-30 00:00:00 
tags:
  - Power BI
  - URL フィルター
  - URL filter
  - Power BI サービス
  - Power BI Service
  - embedded
  - 埋め込み
---
こんにちは、Power BI サポート チームの呂です。

Power BI でコンテンツを共有する際には、共有リンクや埋め込みで「開いたときにどの状態を初期表示にするか」を制御したいことがあります。たとえば、営業チーム向けには担当エリアに絞り込んだ状態で開き、経営層向けには全体の KPI を表示させる、といった使い分けです。
こうした要件に応える機能の一つが URL フィルターです。これは、リンクや埋め込みコードにフィルター条件を付与して、レポートの初期表示を調整するための方法です。この記事では、その基本的な構文と注意点、さらに実務で役立つ活用ポイントを解説します。

<!-- more -->
> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## URL フィルターとは 
Power BI サービスでレポートを開くと、各ページには固有の URL が割り当てられています。その URL にクエリ文字列パラメーターを追加することで、レポートを開いたときに自動的にでフィルターを適用できます。 
フィルター適用後の URL は、ブラウザーによって自動的に標準のエスケープ文字に置き換えられる場合があります。 
<div align="left">
<img src="Picture1.png">
</div>
</br>

## 類似機能との使い分け
類似の機能として共有ビューがあります。これはレポートを特定の状態で保存し、そのビューを他のユーザーと共有できる仕組みです。共有ビューは簡単に作成でき、アクセス権限の付与も可能ですが、URL フィルターのようにパラメーターを自由に変更することはできず、埋め込みでも利用できません。
[フィルター処理された Power BI レポートの共有 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-share-reports)

また、RLS（行レベル セキュリティ）も類似の機能として挙げられます。これはユーザーごとに参照できるデータ範囲を制御する仕組みで、同じレポートでもユーザーによって異なるデータを表示できます。RLS はデータアクセスを厳格に分けたい場合に有効です。
[Power BI での行レベルのセキュリティ (RLS) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/security/service-admin-row-level-security)
</br>

## 基本の使い方
> [!TIP]
以下の小売りの分析サンプルレポートを使って、ここで紹介する例文を検証するすることができます。
[Power BI の小売りの分析サンプル: ツアーに参加する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/sample-retail-analysis#get-the-built-in-sample-in-the-power-bi-service)

URL フィルターの構文は非常にシンプルです。URL の末尾に ?filter= を付けて、以下のように記述します：
```
...?filter=Table/Column eq 'Value'
```

例①	1 つの条件を指定：Store テーブルの Territory 列を「NC」に絞り込む（上記画像）
```
...?filter=Store/Territory eq 'NC'
```

例②	複数の値を指定（in）：Store テーブルの Territory 列を「NC」または「TN」に絞り込む
```
...?filter=Store/Territory in ('NC','TN')
```

例③	複数の条件を組み合わせ（and）：Store テーブルの Territory 列を「NC」かつ Chain 列を「Fashions Direct」に絞り込む
```
...?filter=Store/Territory eq 'NC' and Store/Chain eq 'Fashions Direct'
```

よく使われる演算子については、以下公式ドキュメントをご参照ください。
[URL のクエリ文字列パラメーターを使用してレポートをフィルター処理する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-url-filters#operators)

</br>

## 特殊文字の扱い
URL フィルターでよくつまずくポイントが 特殊文字です。テーブル名や列名にスペース、記号、日本語、または数字で始まる場合は、そのままではフィルターが効きません。特殊文字を含む場合は、_x ＋「4桁のUnicode」＋ _ のUnicode 形式（エスケープコード）に変換する必要があります。

> [!TIP]
URL フィルターを利用する場合は、テーブル名や列名に特殊文字を含めないよう設計しておくことをおすすめします。そうすることでフィルター指定がシンプルになり、運用も容易になります。
Unicode エスケープシーケンスへの変換が必要な場合は、以下のような外部の変換ツールを活用すると便利です。
[Unicodeエスケープシーケンス変換 | Tech-Unlimited](https://tech-unlimited.com/escape-unicode.html)

例①	Table Name/Column+Plus eq 3 を変換する
```
...?filter=Table_x0020_Name/Column_x002B_Plus eq 3
```

例②	Table Special/[Column Brackets] eq '[C]' を変換する
```
...?filter=Table_x0020_Special/_x005B_Column_x0020_Brackets_x005D_ eq '[C]'
```

テーブル名と列名には、Unicode 形式で表される日本語の文字を含めることができます。その場合、すべての日本語文字をエスケープコード（Unicode 形式） に変換する必要があります。

例③	テーブル1/列名 eq 'HR 日本語' の場合は、以下のように変換する
```
?filter=_x30c6__x30fc__x30d6__x30eb_1/_x5217__x540d_ eq 'HR 日本語'
```
</br>

## 値のデータ型ごとの書き方
**文字列：**' ' で囲みます
**数値：**クォート不要、そのまま記載します
**日付：**日付の URL フィルターは、日付型の場合は YYYY-MM-DD と記入すれば自動的に T00:00:00 と解釈され、日時型の場合は datetime'YYYY-MM-DDThh:mm:ss' の形式で指定します。
**特殊文字：**値にほとんどの特殊文字をサポートしていますが、エスケープ コードが必要となるケースもあります。たとえば、単一引用符文字を検索するには、2 つの単一引用符 ('') を使用します。値にエスケープ コードが必要な特殊文字の一覧は公開情報をご確認ください。
[URL のクエリ文字列パラメーターを使用してレポートをフィルター処理する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-url-filters#special-characters-in-values)

## 制限と非対応シナリオ
・テーブルおよび列名は大文字と小文字が区別されますが、値は区別されません
・条件は最大 10 個まで指定でき、URL の長さは最大 2000 文字までです
・既存フィルターの上書きや解除はできず、ページ単位での指定もできません
・Webに公開 、PDF エクスポート、Teams、SharePoint Web Part ではご利用いただけません
・大文字の INF で始まるテーブル名や列名をフィルタリングすることはできません
・JavaScript の制限により、long データ型の最大値は 2^53 - 1 までです。

## おまけ
埋め込み URL の場合、filter に加えて pageName パラメーターを指定することで、最初に表示するページをコントロールできます。
pageName は、Power BI サービスでレポートを開いたときに URL の末尾に表示されます。
https://app.powerbi.com/groups/xxxxxxxx/reports/xxxxxxxx/**ReportSection2**
埋め込み URL例：
```
https://app.powerbi.com/reportEmbed?reportId=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx&autoAuth=true&pageName=ReportSection&filter=Industries/Industry eq 'Energy'
```

> [!TIP]
URL フィルターを利用する場合は、テーブル名や列名に特殊文字を含めないよう設計しておくことをおすすめします。そうすることでフィルター指定がシンプルになり、運用も容易になります。
Unicode エスケープシーケンスへの変換が必要な場合は、以下のような外部の変換ツールを活用すると便利です。
[セキュリティで保護されたポータルまたは Web サイトにレポートを埋め込む - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-embed-secure#customize-your-embed-experience-by-using-url-settings)

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。
<br>

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)