---
title: Power BI Desktop 32 ビット バージョン のサポート終了についてのお知らせ  
date: 2025-04-30 00:00:00  
tags:  
  - Power BI Desktop
  - 32 bit
---
    
こんにちは、Power BI サポート チームの山崎です。   
日頃から、Power BI をご利用いただき誠にありがとうございます。

本記事は、Power BI Desktop 32 ビット バージョンのサポート終了に関するご案内となります。  
Power BI Desktop をご利用中のユーザーの皆さまに影響する可能性があるため、今後の対応やよくあるご質問についておまとめしました。


 </br>

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


##  <font color="DodgerBlue">1. サポート終了の概要</font> 

**2025 年 7 月 31 日以降**、Power BI Desktop の 32 ビット バージョンはサポートされなくなります。  
不具合修正や機能改善を含むアップデートは、64 ビット バージョンのみが対象となります。

🔗ご参考情報：[Power BI Desktop の取得 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/desktop-get-the-desktop)

> 抜粋：  
> 2025 年 7 月 31 日以降、Power BI Desktop の 32 ビット バージョンはサポートされなくなります。引き続き更新プログラムを受け取り、サポートを受けるためには、64 ビット バージョンの Power BI Desktop にアップグレードします。



##  <font color="DodgerBlue">2. 現時点でのサポート対応について</font> 

32 ビット バージョンをご利用のユーザー様からの Power BI の機能や操作に関するお問い合わせや、既存の公開情報に基づくご案内については、これまで通りご支援させていただきますのでご安心くださいませ。

ただし、下記のような場合はご注意ください：

- 特定の環境や構成下でのみ発生するような 32 ビット バージョン特有の不具合の可能性がある場合
- 64 ビット バージョンでの再現が確認できないなど、32 ビット バージョン環境固有の事象であると判断されるケース

私たちとしても、できる限りユーザーの皆さまのお困りごとに寄り添いたいと考えておりますが、32 ビット バージョンの Power BI Desktop に起因する事象の調査・修正は、今後のサポート対象外となる点、ご理解いただきますようお願いいたします。

---

##  <font color="DodgerBlue">3. ユーザーの皆さまにお願いしたいこと</font> 

今後も安定して Power BI をご利用いただくために、以下の対応をご検討ください：

### 🔄 Power BI Desktop 64 ビット バージョンへの移行

現在、ほとんどの Windows 環境は 64 bit OS が主流となっており、Power BI のように大規模データを扱うツールでは、より多くのメモリを活用できる 64 ビット バージョンのご利用が推奨されています。  
32 ビット バージョンは設計上メモリ使用量に制限があり、メモリ不足などの問題が発生しやすくなります。  
このことからも、64 ビット バージョンの Power BI Desktop への移行を推奨しています。

### 🔁 定期的なバージョンアップ

Power BI Desktop は毎月アップデートが提供されており、常に最新のバージョンをご利用いただくことで、より快適なデータ分析が可能となります。

---

##  <font color="DodgerBlue">4. よくあるご質問（FAQ）</font> 

<font color="HotPink">**Q1：今すぐ 32 ビット バージョンは使えなくなりますか？**  </font>   
A：いいえ。インストール済みの 32 ビット バージョンは引き続きご利用いただけますが、更新や修正は提供されません。  
Microsoft では、最新バージョンの Power BI Desktop のみがサポートされていることをご理解いただきますようお願いいたします。

<font color="HotPink">**Q2：64 ビット バージョンに切り替えるにはどうしたらよいですか？**   </font>     
A：Microsoft 公式サイトより 64 ビット バージョンの Power BI Desktop をダウンロード・インストールいただけます。  
32 ビット バージョンをアンインストールしてから、インストールしていただきますようお願いいたします。  
🔗 ご参考情報：[Download Microsoft Power BI Desktop from Official Microsoft Download Center](https://www.microsoft.com/ja-jp/download/details.aspx?id=45331)

<font color="HotPink">**Q3：現在利用中のファイルは 64 ビット バージョンでそのまま開けますか？**   </font>     
A：基本的には同じ .pbix ファイルをそのまま 64 ビット バージョンで開くことができます。  
ただし、Access や .xls のデータソースに接続している場合は、Power BI Desktop のビット数と、インストールされているドライバーのビット数が一致していないと接続エラーになる場合があります。  
必要に応じて 64 ビット 版のドライバーを別途インストールしてください。  
🔗 ご参考情報：[Power BI での Access と XLS のインポートに関する問題のトラブルシューティング - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-access-database-errors)

---

## <font color="DodgerBlue">最後に</font> 

Power BI をより快適にご利用いただくためのサポート体制のアップデートに伴い、ご不便をおかけすることもあるかもしれませんが、皆さまに安心して Power BI をご利用いただけるよう、今後も変わらぬ姿勢でサポートに取り組んでまいります。  
以上、本ブログが少しでも皆様のお役に立てますと幸いです。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)