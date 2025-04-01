---
title: Power BI 用 Copilot を利用する
date: 2024-01-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Power BI Service
  - テナント設定
  - Admin
  - 管理者
---


こんにちは、Power BI サポート チーム 丸山です。

Power BI 用 Copilot は 2024年1月31日 時点でパブリックプレビューの状態で、いくつかの条件を満たしている場合にご利用いただくことができます。今回は現時点における、Power BI 用 Copilot のご利用条件、機能概要、制限事項などをご紹介します。

<!-- more -->

（Power BI 用 Copilot によって生成されるコンテンツの品質向上は継続的に取り組まれていますが、Copilot が生成する結果については何かを保証するものではなく、あくまで人間の見識によって責任をもって管理と判断をする必要がございます）

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## ・目次
---
 [・使用条件](#・使用条件)
 [・機能概要](#・機能概要)
 [・ご留意点と制限事項](#・ご留意点と制限事項)

---
## ・使用条件
---
**■ライセンス要件**
Power BI 用 Copilot をご利用いただけるのは、Premium 容量 (P1 以上)　またはFabric 容量（F64 以上) のワークスペースのみでございます。試用版 SKU はサポートされていません。かつ、ご利用の容量が以下の公開情報に記載のいずれかのリージョンにある必要があります。

// 公開情報：[Fabric が使用できるリージョン - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/region-availability)
※Power BI 用 Copilot は、現在、段階的に展開がされている状況であるため、上記の条件を満たしている場合でも、お客様のテナントのリージョンによっては、試せる機能が限られる可能性がございます。

該当ワークスペースの共同作成者 or メンバー or 管理者のアクセス権を持っている必要があります。
また、ワークスペースの使用には、Power BI Pro ライセンス以上（または試用版ライセンス）が必要です。


**■テナント設定**
以下２つが有効化されている必要がございます（どちらも既定では無効）

・	[ユーザーは Copilot のプレビューや、Azure OpenAI によって提供されるその他の機能を使用できます] 
・	[Azure OpenAI に送信されたデータは、テナントの地理的リージョン、コンプライアンス境界、または国内クラウド インスタンスの外部で処理できます] 

<div align="center">
<img src="1.png">
</div>

※	テナント設定「ユーザーはFabricアイテムを作成できます」は関係しておらず、上記２つのテナント設定の有効化のみで Power BI 用 Copilot　はご利用可能です。

// 公開情報：[Copilot の管理者設定 (プレビュー) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/service-admin-portal-copilot)

</br>

上記の使用条件については以下の公開情報にまとめがございますので、必要に応じてご参照ください。

// 公開情報：[Power BI 用 Copilot (プレビュー) の概要 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-introduction)
<div align="center">
<img src="2.png">
</div>

</br>

---
## ・機能概要
---
Power BI 用 Copilot における主な機能は以下でございます。

**機能:１： Power BI 用 Copilot を使用してレポートを作成する**
Power BI サービス上のセマンティックモデルをもとに、Copilot に指示をすることで、レポートを自動的に作成することができます。具体的な動作については、以下の公開情報、ならびに弊社 Power BI スペシャリストのブログなどをご参照ください。

// 公開情報：[Power BI サービス用の Copilot を使用してレポート ページを作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-create-report)
// ご参考：[Copilot for Power BI（レポート作成） - テクテク日記 (hatenablog.com)](https://marshal115.hatenablog.com/entry/2023/12/22/082056)


**機能:２： Power BI 用 Copilot を使用してレポートページに関する説明を作成する**
Power BI Desktop と Power BI サービスでは、Power BI 用 Copilot を使用して、数回クリックするだけでレポート ページに関する説明をすばやく作成できます。この説明とは、レポート全体、特定のページ、さらには選択した特定のビジュアルを要約したものになります。

// 公開情報：[Power BI 用 Copilot を使用して説明を作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-create-narrative?tabs=powerbi-service)

**機能:３： Power BI 用の Copilot を使用して Q&A を強化する**
通常の Q&A ビジュアルとその自然言語処理機能は、生成 AI に依存しませんが、Power BI 用の Copilot を使用すると、ユーザーの質問を理解する能力を迅速に向上させることができます。

// 公開情報：[Power BI 用の Copilot を使用して Q&A を強化する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/natural-language/q-and-a-copilot-enhancements)

Power BI Desktop の場合は、オプション設定で以下にチェックを入れておきます。
<div align="center">
<img src="3.png">
</div>
</br>

**（ 機能 : クイックメジャーの提案　）**
クイックメジャーでも [Copilot による提案] がご利用いただけますが、こちらは旧来のクイックメジャーの提案に代わるものであるため、先述した以下２つのテナント設定の有効化は不要でございます。

・	[ユーザーは Copilot のプレビューや、Azure OpenAI によって提供されるその他の機能を使用できます] 
・	[Azure OpenAI に送信されたデータは、テナントの地理的リージョン、コンプライアンス境界、または国内クラウド インスタンスの外部で処理できます] 

ただし、クイックメジャーの使用自体で以下２つのテナント設定が有効化されている必要があります。

・	[ユーザーはPower BI サービスでデータ モデルを編集できます (プレビュー)]  ※既定で有効
・	[ユーザー データが地域を離れられるようにする]　※既定で無効
　→クイックメジャーの提案機能は、現在米国のデータセンターにのみデプロイされている機械学習モデルが利用されるため、お客様のテナントリージョンが米国以外の場合、このテナント設定を有効にしない限り、クイックメジャーの機能が既定で無効になります。

<div align="center">
<img src="4.png">
</div>
</br>

■ Power BI Desktop 
オプションと設定 > オプション
<div align="center">
<img src="5.png">
</div>
</br>

クイックメジャーの使用画面のイメージは以下です。
<div align="center">
<img src="6.png">
</div>
</br>

// 公開情報：[クイック メジャーの提案 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/quick-measure-suggestions)


---
## ・ご留意点と制限事項
---

**Power BI 用 Copilot のご利用の際、データのセキュリティとプライバシーに関しては以下の公開情報をご参照ください。**

// 公開情報：[Microsoft Fabric での Copilot のプライバシー、セキュリティ、責任ある使用 (プレビュー) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/get-started/copilot-privacy-security)


**また、Power BI 用 Copilot はたくさんの制限事項があり代表的なものを以下に上げますが、機能それぞれの制限事項の詳細は、随時それぞれの最新の公開情報をご確認ください。**

・Copilot で作成するビジュアルの種類は指定できません
・生成されたビジュアルを指示で変更することはできません（手動で変更が可能）
・Copilot は複雑な意図を理解できません（意図しないビジュアルや説明が生成される場合もあります）
・etc

上述してきました各公開情報に「考慮事項と制限事項」がございますのでご参照ください。
// 公開情報：[Power BI サービス用の Copilot を使用してレポート ページを作成する - Power BI | Microsoft Learn - 考慮事項と制限事項](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-create-report#considerations-and-limitations)
// 公開情報：[Power BI 用 Copilot を使用して説明を作成する - Power BI | Microsoft Learn - 考慮事項と制限事項](https://learn.microsoft.com/ja-jp/power-bi/create-reports/copilot-create-narrative?tabs=powerbi-service#considerations-and-limitations)
// 公開情報：[Power BI 用の Copilot を使用して Q&A を強化する - Power BI | Microsoft Learn - 考慮事項と制限事項](https://learn.microsoft.com/ja-jp/power-bi/natural-language/q-and-a-copilot-enhancements#limitations-and-considerations)
// 公開情報：[クイック メジャーの提案 - Power BI | Microsoft Learn  - 考慮事項と制限事項](https://learn.microsoft.com/ja-jp/power-bi/transform-model/quick-measure-suggestions#limitations-and-considerations)


**また、出力された結果のレビューは、コンテンツの正確性と妥当性を有意義に評価できる人が行う必要がございます。Copilot で出力される結果については十分にご確認いただいた上でご利用をお願いします。**
 
</br>
</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)