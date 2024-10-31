---
title: Power BI ユーザーから見た Microsoft Fabric について
date: 2024-08-30 00:00:00 
tags:
  - Power BI
  - Microsoft Fabric

---

こんにちは、Power BI サポート チームの中川です。

新たなデータ分析プラットフォーム「 Microsoft Fabric 」（以下、 Fabric ）が 2023 年 11 月に正式にリリース（ GA ）されました。 Fabric は、 Power BI に加え、 Data Factory 、 Synapse Data Science などのエクスペリエンスが加わり多彩な機能を提供していますが、 Power BI ユーザーとしては、「 Fabric とは一体何なのか？」、「 Fabric の導入や移行が必要なのか？」といった疑問を抱える方も多いのではないでしょうか。 

本ブログでは、 Power BI ユーザーや運用担当者の視点から、データ分析環境の変遷や Fabric のメリット、移行の要否について解説します。なお、 Microsoft Fabric の各エクスペリエンスに関する詳細については、以下をご参照ください。 

>[!NOTE]
> 参考情報：[Microsoft Fabric パブリック プレビュー | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/microsoft_fabric/)


<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [Power BI と Microsoft Fabric の関係について](#Power-BI-と-Microsoft-Fabric-の関係について)
* [データ分析基盤のコンポーネント](#データ分析基盤のコンポーネント)
* [従来のデータ分析基盤における課題](#従来のデータ分析基盤における課題)
* [Microsoft Fabric がもたらすメリット](#Microsoft-Fabric-がもたらすメリット)
* [Microsoft Fabric の移行について](#Microsoft-Fabric-の移行について)
* [おわりに](#おわりに)


---
## Power BI と Microsoft Fabric の関係について
---

Power BI ユーザーの視点から見ると、 Fabric は、 Power BI というデータ分析の SaaS サービスを中心に、その他のエクスペリエンスを加えられた包括的なプラットフォームです。 前述の通り、Power BI に Data Factory や Synapse Data Engineering などの新しい機能と統合され、より強力で一貫性のあるデータ分析基盤が提供されるようになりました。このため、他のエクスペリエンスとのシームレスな連携が可能となる一方で、 Fabricのリリースに伴うPower BI に大きな変化はありません。（もちろん、 Power BI 自体は常に機能はアップデートされています。）

Power BI そのものには大きな変化はないものの、データ分析環境全体が大きく進化しています。いくつかのエクスペリエンスが加わることで、データ整備や機械学習といった高度な分析機能が、ビジネスユーザーや市民開発者にも扱いやすい形で提供され、 Power BI ユーザーにとっても利便性が大幅に向上しています。



<div align="center">
<img src="Microsoft_Fabric_01.png">
</div>

画像引用： [【B4】AI データ基盤の新時代 - Microsoft Fabric の最新アップデートでビジネスインテリジェンスを再定義](https://www.youtube.com/watch?v=khqAGkD01T0)</br></br>

---
## データ分析基盤のコンポーネント
---
Fabric は、データ分析基盤としての SaaS サービスを提供しますが、どのような変遷で登場したのでしょうか。まずは、従来のデータ分析基盤について見てみます。以下は一般的なデータ分析基盤のコンポーネントの図です。


<div align="center">
<img src="Components_of_DataAnalysisInfrastructure_01.png">
</div>

画像引用： [Azure Synapse Analytics 概要とデータ分析における位置づけ](https://www.youtube.com/watch?v=3OQh3f7EoX0)</br></br>

たとえば、右側の [分析レポート] に位置する Power BI が直接左側のデータソースを参照しているケースもあれば、データをバッチ処理等でデータレイクに格納し、その後クレンジングや加工を行いデータストアに保存し、最終的にレポートを作成する、といった複数のプロセスが考えられます。

従来の Microsoft のサービスに当てはめると、 Power BI を除き、ほとんどのプロセスが PaaS サービスとして提供されてきました。たとえば、バッチデータ取込やデータレイク、分散データ処理は、 Azure Data Factory 、 Azure Data Lake Storage Gen2 、 Azure Databricks 等の PaaS サービスで対応していました。

<div align="center">
<img src="Components_of_DataAnalysisInfrastructure_02.png">
</div>

画像引用： [Azure Synapse Analytics 概要とデータ分析における位置づけ](https://www.youtube.com/watch?v=3OQh3f7EoX0)</br></br>


その後、これらのサービスの一部が統合され、 Azure Synapse Analytics という包括的なプラットフォームに置き換えられ、より一貫性のあるデータ分析基盤が提供されるようになりました。


<div align="center">
<img src="Components_of_DataAnalysisInfrastructure_03.png">
</div>

画像引用： [Azure Synapse Analytics 概要とデータ分析における位置づけ](https://www.youtube.com/watch?v=3OQh3f7EoX0)</br></br>



この流れが、さらに進化した形が Microsoft Fabric で、データ分析基盤の変遷を図にしたものが以下となります。

<div align="center">
<img src="Components_of_DataAnalysisInfrastructure_04.png">
</div>

画像引用： [【A1-6】Microsoft Fabric - AI 時代のデータ分析（詳細編）](https://www.youtube.com/watch?v=jPzELeyv4jA)</br></br>



Fabric によりデータ分析基盤が SaaS サービス として提供され、利用者や管理者に多くの利点が生まれました。これまでは、データエンジニアリングやデータサイエンス、データ分析の各領域で PaaS サービスを分けて利用していましたが、 Fabric という SaaS のプラットフォームにリメイクされ、様々な領域の担当者（ペルソナ）が一つの環境でコラボレーションできるようになります。

<div align="center">
<img src="Components_of_DataAnalysisInfrastructure_05.png"></div>

画像引用： [【A1-6】Microsoft Fabric - AI 時代のデータ分析（詳細編）](https://www.youtube.com/watch?v=jPzELeyv4jA)</br></br>


---
## 従来のデータ分析基盤における課題
---

従来のデータ分析基盤における課題を、 Power BI 利用者であるレポート開発者と分析基盤管理者の目線で考えてみます。

### レポート開発者
データ分析を行う際、 Power BI のレポート開発者が直面する課題はいくつかあります。簡単なデータ加工であれば、GUI ツールである Power Query やデータフローを用いて Power BI ユーザーでも比較的簡単に対応できますが、大容量のデータや複雑なデータ加工が必要な場合、 Power BI 側で処理を行うとパフォーマンスの問題が生じる可能性があります。そのため、これらの処理は可能な限りデータソース側のリソースを使ってで行うのが望ましいとされています。しかし、これには例えばデータベース管理者に新しいビューやテーブルの作成を依頼する必要があり、 Power BI ユーザーには扱えない領域が出てきます。

さらに、バッチ処理やクレンジング処理などの高度な処理が必要になると、 Power BI のスキルセットだけでは対応しきれない場面が多く、これもまた Power BI ユーザーには手が届かない領域が出てきます。

### Power BI および データ分析基盤の運用管理者
Power BI やデータ分析基盤の運用管理を担当する管理者にとっては、複数のサービスを管理する必要があるため、その管理負荷が大きな課題となります。サービスごとに管理ポリシーやセキュリティ設定を適用する必要があり、これが一貫性の欠如を招くリスクや、人為的ミスが発生しやすくなる原因となります。また、異なるサービス間でのデータの移動や変換、統合においても、運用の複雑さが増し、効率が低下する可能性があります。

加えて、従来のデータ分析基盤では、管理者がそれぞれのサービスに対して個別にモニタリングやパフォーマンスの最適化を行わなければならず、これもまた管理業務の煩雑さを増加させる要因となっていました。これにより、意思決定に必要な情報を迅速に提供することが難しくなる場合があります。
 




---
## Microsoft Fabric がもたらすメリット
---
これらの課題に対し、 Fabric の登場は大きな改善が期待できます。繰り返しになりますが、 Fabric では、従来は PaaS サービスで対応していた領域を SaaS サービスとして統合されたことにより、異なるペルソナ間でのコラボレーションが容易になり、運用管理の効率が向上します。
 
さらに、 Power BI の使いやすさを継承した各エクスペリエンスに加え、 Copilot の導入により、市民開発者や Power BI ユーザーでもデータの統合、クレンジング、機械学習といった専門知識を要する領域をより簡単に扱えるようになりました。これにより、より柔軟で効率的にデータ分析を進めらるようになり、また運用管理者の負担が軽減されています。



<div align="center">
<img src="Power_BI_strategy.png">
</div>

画像引用： [【D1-5】Microsoft Fabric - AI 時代のデータ分析（概要編）](https://www.youtube.com/watch?v=W5T_7FC6F88)</br></br>


---
## Microsoft Fabric の移行について
---
これまで提供されていた Power BI Premium 容量（ Premium Per Capacity ）は、新規購入ができなくなりました。現在、容量の新規購入を検討する場合、 Fabric が唯一の選択肢となります。しかしながら、 Fabric の試用版ライセンスを利用できるため、ぜひお試しください。

>[!NOTE]
> 参考情報：[試用版の開始 - Microsoft Fabric パブリック プレビュー | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/microsoft_fabric/#Fabric-%E8%A9%A6%E7%94%A8%E7%89%88%E3%81%AE%E9%96%8B%E5%A7%8B)

また、現在 Power BI Premium 容量をお使いの場合、 EA ライセンスの有無や更新日によって、 Power BI Premium 容量の更新可否が異なります。移行の要否および移行方法につきましては、以下の公開ブログをご参照ください。

>[!NOTE]
> 参考情報：[Premium容量からFabric容量への移行](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_premium_to_fabric/)



---
## おわりに
本ブログでは、 Fabric について、Power BI ユーザーや運用担当者の視点から、データ分析環境の変遷や Fabric のメリット、移行の要否について解説しました。 Fabric は、 Power BI をはじめとする従来のサービスに新たな機能を加え、より包括的で一貫性のあるデータ分析基盤を提供します。
Fabric は新しいサービスであり、慣れない方も多いかと思います。ぜひ Fabric の試用版をお試しいただき、また、弊社のサポートサービスへもお気軽にお問い合わせいただければと思います。

最後に、 Fabric についてさらに理解を深めるための参考ブログやセッション動画を以下にご紹介しますので、ぜひご一読ください。


### 公開情報
>[!NOTE]
> 参考情報：[Microsoft Fabric パブリック プレビュー | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/microsoft_fabric/)
> 参考情報：[Microsoft Fabric の OneLake について | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/fabric_onelake/)
> 参考情報：[Microsoft Fabricの登場 - テクテク日記 (hatenablog.com)](https://marshal115.hatenablog.com/entry/2023/05/24/155319)
> 参考情報：[Microsoft Fabricとの向き合い方 - テクテク日記 (hatenablog.com)](https://marshal115.hatenablog.com/entry/2023/06/06/185447)



### セッションアーカイブ動画
>[!NOTE]
> 参考情報：[【D1-5】Microsoft Fabric - AI 時代のデータ分析（概要編）](https://www.youtube.com/watch?v=W5T_7FC6F88)
> 参考情報：[【A1-6】Microsoft Fabric - AI 時代のデータ分析（詳細編）](https://www.youtube.com/watch?v=jPzELeyv4jA)
> 参考情報：[【B4】AI データ基盤の新時代 - Microsoft Fabric の最新アップデートでビジネスインテリジェンスを再定義](https://www.youtube.com/watch?v=khqAGkD01T0)


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)