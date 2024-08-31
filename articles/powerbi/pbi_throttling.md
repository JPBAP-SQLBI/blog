---
title: Premium / Fabric 容量のスロットリングについて
date: 2024-04-30 00:00:00
tags:
  - Power BI
  - Premium Capacity
  - Microsoft Fabric 
  - CapacityLimitExceed
  - throttling
  - スロットリング
  - エラー
  - error
---  


こんにちは、 Power BI サポート チームの山崎です。  
Premium / Fabric 容量に割り当てられたワークスペース上で、「容量制限に達したため、モデルを読み込めません」（Capacity operation failed with error code CapacityLimitExceeded）といったエラーが発生し、データ更新、レポートの編集、閲覧などができなくなった場合、ご使用中の容量においてスロットリングが発生している可能性があります。  

<div align="left">
<img src="1.png">
</div>
</p>  

本記事では、このスロットリングとはどういうものか、対処策と回避策もあわせてご紹介いたします。  

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


 </br>

##  <font color="DodgerBlue">1. スロットリングとは何か</font>    

スロットリング（調整）とは、一般的には、システムやサービスにおいて一定の制限値を超えたときに一時的に特定の操作やリクエストを制限することを指します。  
Power BI の Premium / Fabric 容量においても、このスロットリングが適用されています。  
ご使用中の容量のリソース使用量が許容範囲を超えた場合に発生し、スロットリングが解除されるまで、データ更新、レポートの編集、閲覧などの操作が遅延するまたは続行できなくなる場合があります。  

 </br>

## <font color="DodgerBlue">2. どのようにスロットリングが発生するか</font>  

上述の通り、 Power BI では、リソースの使用量が許容範囲を超えた場合に発生することがあります。  
具体的には、購入した容量で使用可能なリソースを超え、将来使用するはずだったリソースを 10 分間すべて使い果たした時点で、スロットリングが開始されます。  
Power BI　における操作は、 「対話型」 操作と 「バックグラウンド」 操作の2つのカテゴリに分けられます。  
対話型操作は短い期間で実行される操作で、通常は UI を使用したユーザー操作によってトリガーされ、例えばデータフローで Direct Query を使用するなどが該当します。  
一方バックグラウンド操作は長期間実行される操作を指し、例えばデータフローの更新はこちらに該当します。  
スロットリングが開始され、その後も超過した状態でリソースが使用され続けた場合、「対話型操作の遅延」 → 「対話型操作の拒否」 → 「バックグラウンド操作の拒否」 という順で操作に制限がかかっていきます。  
スロットリング ポリシーの詳細や操一覧は以下公開情報をご参考にしていただきますようお願いいたします。  

参考情報：[Fabric のスロットリング ポリシー]( https://learn.microsoft.com/ja-jp/fabric/enterprise/throttling)  
参考情報：[インタラクティブおよびバックグラウンドの操作]( https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-interactive-background-operations)  
 

なお、弊社にお問合せいただくスロットリングの事象としては、すでにご使用中の容量のリソース使用率が高負荷な状態となっている中で、大量データの処理や、複数ユーザーの一斉アクセス、セマンティックモデルの更新、レポートのレンダリング、タイルの更新などを行おうとした際に、操作に遅延や拒否が発生していることが多くみられます。  

</br>
  

## <font color="DodgerBlue">3. スロットリングが発生した際の対処策</font>  

スロットリングが発生した場合、次の対処策があります。  
ユーザー様のご環境やご運用方針、業務への影響度・緊急度をもとに可能な対処策をご検討ください。  

### <font color="HotPink">(1) SKUのアップグレード</font> 
使用中の容量を上位の SKU にアップグレードします。  
この対処策が特に有効なシナリオとしては、調査によって、容量に多くの過負荷インシデントが存在することがわかった場合です。  
継続的にリソース使用率が高くスロットリングが発生しやすい状況であることが想定されますので、上位SKUにアップグレードすることで過負荷状態の解消が期待できます。  

参考情報：[容量と SKU](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-what-is#capacities-and-skus)  


### <font color="HotPink">(2) 自動スケーリングの有効化</font> 

組織の Power BI コンテンツに応じたスケールとパフォーマンスが提供される自動スケーリングを使用します。  
自動スケーリングによって、リソース使用率の増加時にも処理速度が低下しないようにコンピューティング容量が自動で追加されます。  
※　自動スケーリングは課金制となります。  
この対処策が特に有効なシナリオとしては、日中いくつかの過負荷インシデントが存在することがわかった場合です。（1）の SKU アップグレードを行った場合とコストを比較し検討いただくことをお勧めします。  

参考情報：[Power BI Premium で自動スケーリングを使用する](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-auto-scale)  



### <font color="HotPink">(3) スロットリングが解除されるまで待つ</font>   

スロットリングは、一定の期間が経過すれば解除されます。  
このため、この対処策が特に有効なシナリオとしては、スロットリングが夜間や業務に大きな影響を与えない時間・頻度で発生しており、 SKU アップグレードや自動スケーリングまでの対処が必要ないと判断している場合です。  
なお、スロットリングが発生してから解除されるまでの時間は計算することができません。  
目安として “何時間後に解除される“ といった予測をたてることはできませんので、その点はあらかじめご理解いただければと存じます。  

参考情報：[過負荷を解決する方法](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-smoothing#how-to-resolve-overload)  

### <font color="HotPink">(4) その他</font>   

上記以外に、スロットリング発生時に有効な場合がある暫定対処策は以下があります。  

・他に Premium / Fabric 容量がある場合は、対象のワークスペースをそちらの容量に割りあてる  
・処理負荷がかかっているコンテンツを他の容量のワークスペースに退避させる（またはバックアップを取得しPower BI サービス上からいったん削除する）  
・対象セマンティックモデルの更新スケジュールの無効化や進行中の更新処理の中止  


 </br>



## <font color="DodgerBlue">4. 事前に回避するための運用策</font>  

スロットリングを発生させないために、以下ご運用をご検討ください。  

### <font color="HotPink">(1) Microsoft Fabric Capacity Metrics アプリによるパフォーマンス監視</font> 

スロットリングを発生させないためには、日頃から [Microsoft Fabric Capacity Metrics アプリ]( https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app) を使用し、対象の容量のパフォーマンスを監視することがとても重要です。  
Microsoft Fabric Capacity Metrics アプリでは、時系列で容量の利用率や上限を超過しているかどうかの推移や、各アイテムのリソースの利用状況をご確認いただけます。  
確認の結果から、例えば、いつも同じタイミングで負荷が高くなる場合はその時間にどのような処理が発生しているか分析し、セマンティックモデルの更新が集中している場合は更新時間をずらしてみるなどの対処が行えますし、特定のレポートの処理に課題がありそうなら、レポートの最適化やワークロード構成の見直しなどが効果的かもしれません。  
スロットリングの状況を確認する方法は以下公開情報でもご案内していますのでご参考にしていただきますようお願いいたします。  

参考情報：[メトリック アプリのコンピューティング ページについて – 調整](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app-compute-page#throttling)  
参考情報：[サポートチームブログ：Power BI 利用時のパフォーマンス測定や最適化について](https://jpbap-sqlbi.github.io/blog/powerbi/performance/)  


### <font color="HotPink">(2) 容量の通知設定</font> 

容量の通知を設定することで、使用可能な容量が、設定したしきい値を超えた時や使用可能な容量を超過した時にメールで通知することが可能です。  

参考情報：[通知の構成](https://learn.microsoft.com/ja-jp/fabric/admin/service-admin-premium-capacity-notifications?source=recommendations#configure-capacity-notifications)  

 </br>

以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。  

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)