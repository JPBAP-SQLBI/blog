
---
title: Apache Log4j の脆弱性とPower BI, Power BI Report Server への影響について
date: 2021-12-21 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - Power BI Report Server
  - オンプレミスデータゲートウェイ
  - onpremisedatagateway
  - Apache log4j
---


こんにちは、Power BI サポート チームの山本です。 
12月9日に公開されたJava ベースのロギングライブラリ「Apache Log4j」の脆弱性とPower BI の関係性についてまとめています。

Power BI サービスにおいては、この脆弱なライブラリへの既知の依存はなく、影響はないと判断しております。
また、Power BI Desktop 、オンプレミスデータゲートウェイや Power BI Report Server においても、関連の影響は確認しておりません。

<!-- more -->

</br>

> [!IMPORTANT]
> 本記事は12月21日時点の情報を元にまとめておりますが、本記事編集時点とその後の見解に相違がある場合がございます。
> 最新の情報は弊社Microsoft Security Response Center のブログも合わせてご確認ください（英語）
><Span style="font-size: 90%">[MSRC-blog](https://msrc-blog.microsoft.com/)</span>


</br>


---
## Apache Log4j の脆弱性について
---


Apache Log4j は、 Apache Software Foundation がオープンソースで提供している Java ベースのロギングライブラリです。
この Apache Log4j において、遠隔の第三者が細工したデータを送る事で、任意のコマンドを実行される可能性があります。

今回の脆弱性のインスタンスとして CVE-2021-44228 と CVE-2021-45046 が割り当てられています。


参照(情報処理推進機構)：[Apache Log4j の脆弱性対策について(CVE-2021-44228)](https://www.ipa.go.jp/security/ciadr/vul/alert20211213.html)

</br>


---
## Power BI への影響について
---


当社 Microsoft 全体として、Log4j の悪用について認識しており、あらゆる問題を修正するためにすべてのサービスで積極的に取り組んでいます。
Power BI サービスにおいては、この脆弱なライブラリへの既知の依存はなく、**影響はない**と判断しております。
また、Power BI Desktop 、オンプレミスデータゲートウェイや Power BI Report Server においても、関連の影響は確認しておりません。

その他当問題の状態に関する最新の情報については、MSRC Advisory および Microsoft Security Threat Intelligence のサイトをご参照ください。

//参考①：[CVE-2021-44228 Apache Log4j 2 に対するマイクロソフトの対応 – Microsoft Security Response Center](https://msrc-blog.microsoft.com/2021/12/12/microsofts-response-to-cve-2021-44228-apache-log4j2-jp/)
//参考②：[Guidance for preventing, detecting, and hunting for CVE-2021-44228 Log4j 2 exploitation - Microsoft Security Blog](https://www.microsoft.com/security/blog/2021/12/11/guidance-for-preventing-detecting-and-hunting-for-cve-2021-44228-log4j-2-exploitation/)


---
## よくある質問
---

### Q. Log4j の脆弱性は、AppSource から取得したサードパーティのカスタムビジュアルには影響ないのでしょうか。</br>また、AppSource のPower BI 認定ビジュアルは、Log4j ライブラリを使用していますか。

Log4j の脆弱性は、AppSoure から取得したサードパーティのカスタムビジュアルには影響しません。また Java が含まれる場合、カスタムビジュアルのコードレビューはパスできないため、Power BI 認定ビジュアルは、脆弱なライブラリの影響を受けません。

### Log4j の脆弱性は、Power BI のアクティビティおよび監査ログを取得するために使用される PowerShell スクリプトに影響はありますか。

Microsoft Power BI Cmdlets for Windows PowerShell および PowerShell Core は、本脆弱性の影響を受けません。（ただし Power BI が提供する以外のリソースを呼び出すような任意のカスタムコードについては、弊社責任の範囲外となります）


</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)