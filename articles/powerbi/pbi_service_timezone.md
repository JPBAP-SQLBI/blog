---
title: Power BI サービスに発行したレポートの時刻のずれについて
date: 2023-02-28 00:00:00 
tags: 
  - Power BI
  - Power BI サービス
  - Power BI Service
  - UTC
  - 相対時間
  - タイムゾーン
  - TimeZone
---


こんにちは、Power BI サポート チームの山崎です。
Power BI Desktopで作成したレポートを Power BI サービスに発行した後、相対時間のスライサー、フィルターの結果、Now 関数や DateTimeZone 関数などで取得した日付と時刻のデータにずれが生じて困ったことはありませんか。
今回は、この日付と時刻のデータにずれが生じる理由と対処策をご案内いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

</br>

---
## Power BI サービスの協定世界時 (UTC) の時刻に基づいている


Power BI のデータ モデルには、タイムゾーン情報が含まれていません。
Power BI Desktop は、アプリをインストールした PC のシステム時間に基づき動作します。
このため、日本の時間に合わせた PC 上で、例えば DAX の Now 関数や Power Query の `DateTimeZone.LocalNow` 関数を使用した場合は、日本時間に合わせて日付と時刻の情報を取得します。
一方で Power BI サービスは、グローバルでのコンテンツ共有を想定しており、統一したタイムゾーンベースでの可視化をベースとすることを理由に、テナントのリージョンや言語設定、ユーザーが使用する PC のシステム時間やブラウザ言語にかかわらず、 協定世界時 (UTC) の時刻に基づき動作します。 
この違いにより、Power BI サービスに発行したレポート上の日付と時刻の情報にずれが生じる場合があります。

参考情報： 
[日付と時刻関数]( https://learn.microsoft.com/ja-jp/dax/date-and-time-functions-dax) 
[DateTimeZone 関数]( https://learn.microsoft.com/ja-jp/powerquery-m/datetimezone-functions) 

</br>

## 日本のユーザーは 9 時間のずれを考慮する必要がある

協定世界時 (UTC) と日本標準時 (JST) の時差は 9 時間です。
このため、Power BI サービス上でレポートを使用する場合は、 9 時間の差を考慮する必要があります。 
具体的には、取得した時間に +9 時間する計算をしたり、タイムゾーン情報を変更する関数を使用するなどして工夫することで対処します。
次の項では、2つの例をご案内いたします。 

参考情報： 
[Power BI で相対時間のスライサーおよびフィルターを作成する- 考慮事項と制限事項](https://learn.microsoft.com/ja-jp/power-bi/create-reports/slicer-filter-relative-time#considerations-and-limitations) 


</br> 

## 対処策の例 

**例１：Now 関数で現在の日付と時刻の情報を取得している場合**
以下のように、[UTCNow](https://learn.microsoft.com/ja-jp/dax/utcnow-function-dax) 関数で UTC の現在の日付と時刻を取得し +9 時間する列を作成します。

> UTCNow+9 = <font color="DodgerBlue">UTCNOW</font>() + <font color="DodgerBlue">TIME</font>(<font color="DarkTurquoise">9</font>,<font color="DarkTurquoise">0</font>,<font color="DarkTurquoise">0</font>)

Power BI Desktop 上では、どちらも日本時間で表示されます。

<div align="center">
<img src="1.png">
</div>
</p>

Power BI サービスに発行すると、`Now` 関数で取得した [Now] 列のデータは UTC の時間ですが、 `UTCNow` 関数で UTC の現在の日付と時刻を取得し +9 時間した [UTCNow＋9] 列は、日本時間で表示することができます。

<div align="center">
<img src="2.png">
</div>
</p>

</br>

**例２：Power Query で現在の日付と時刻情報を取得する場合**
Power Query で `DateTime.LocalNow` などの関数を使用すると、現在の日付と時刻の情報を取得できます。
しかしながら、上述の通りこのまま Power BI サービスに発行すると 9 時間のずれが発生するため、タイムゾーン情報を変更する関数 [DateTimeZone.SwitchZone](https://learn.microsoft.com/ja-jp/powerquery-m/datetimezone-switchzone) を使用することで時間のずれを回避し、Power BI サービス上でも日本時間にて日付と時刻の情報を取得することができます。

Power Query で `DateTime.LocalNow` 関数を用いて現在の日付と時刻の情報を取得した場合：
PCのシステム時間に基づきます。

>＝ DateTime.LocalNow()

<div align="center">
<img src="3.png">
</div>
</p>

`DateTimeZone.SwitchZone` 関数を用いて、タイムゾーン情報を +9 時間に変更した場合：
UTC に +9 時間するので、結果として日本の時間になります。

>= DateTimeZone.SwitchZone(DateTimeZone.UtcNow(),<font color="DarkTurquoise">09</font>)

<div align="center">
<img src="4.png">
</div>
</p>

Power BI Desktop 上では、どちらも日本時間で表示されます。
<div align="center">
<img src="5.png">
</div>
</p>

Power BI サービス に発行すると、`DateTime.LocalNow` 関数を用いたほうは UTC の時間で表示されますが、`DateTimeZone.SwitchZone` 関数を用いたほうは UTC に+9 時間しているため、日本の時間になります。

<div align="center">
<img src="6.png">
</div>
</p>

</br>

このように、時刻のずれが生じた場合は、UTC とのずれを考慮したレポート作成を実施していただきますようお願いいたします。

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)