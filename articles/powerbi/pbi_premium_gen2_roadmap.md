
---
title: Power BI Premium Gen2 について
date: 2021-08-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - ライセンス
---

こんにちは、Power BI サポート チームです。

Power BI のライセンスについては過去記事「[作成したレポートを組織内で共有するために必要なライセンスは？~ Power BI ライセンス（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）の違い ~](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license/)」でもご紹介させていただきましたが、今回は、新世代のPower BI Premium であるPower BI Premium Gen2 についてご紹介させていただきます。

<!-- more -->


<br>

> [!IMPORTANT]
> 本記事は 弊社公式ブログ「Microsoft Power BI ブログ」の公開情報を元に構成しておりますが、本記事編集時点と実際の機能やリリース時期に相違がある場合がございます。
>元記事は以下よりご確認ください（英語）
><Span style="font-size: 90%">[Updated Timeline and milestones for Premium Gen2 General Availability](https://powerbi.microsoft.com/en-us/blog/updated-timeline-and-milestones-for-premium-gen2-general-availability/)</span>

<br>

## Power BI Premium Gen2 とは？
---

Power BI Premium の機能強化を目的に、アーキテクチャを再設計した新世代のPower BI Premium です。
現在はプレビューであり、容量ベースのPower BI Premium Per Capacity をご利用のテナントでGen2 への切り替えを行なうことが可能です。

具体的には、CPU やメモリなどのリソースをより最適化するような設計に代わった一方、リソースは全てMicrosoft 側で自動調整を行なうためその手間を感じさせない設計になっています。
以前と同じ容量プランにおいても、Gen2ではCPUやメモリにおいて物理的な制限が大幅に緩和され、データセットの更新、レポートのクエリ実行の速度という面では、パフォーマンスが向上されます。
また処理量に応じた仮想コアの自動スケーリングにも対応し、過負荷による速度低下を防ぐことが可能です。


ユーザー単位のライセンスであるPower BI Premium Per User もPower BI Premium Gen2 のアーキテクチャを採用しています。

### Power BI Premium Gen2 の使用方法


Power BI サービスの管理ポータルより[容量の設定]から割当している容量をクリックし、
容量の設定画面上部からPremium Generation 2 (プレビュー)を有効化することでGen2 への切り替えが可能です。

<div align="center">
<img src="pic1.gif" alt="画像1_Gen2 の使用方法" title="画像1_Gen2 の使用方法">
</div>

<br>
<br>

##  Power BI Premium Gen1(従来版) との比較
---

従来のPower BI Premium と具体的にどう違うのか、表形式でまとめしました。

|                    | Premium Gen1                                                                                                                                                  | Premium Gen2                                                                                                                                                                                                                                                                       | 
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | 
| リソースの使い方   | <b>「ユーザー側で手動調整」</b><br>予約されたリソースは組織専用で排他的に使用されますので、物理的な制限があります。                                                      | <b>「Microsoft側で自動調整」</b><br>バックエンドコアに関しては、組織専用ではなく、クラウド内の物理ノードのリージョン クラスターに実装され、Power BI リージョン内の Premium 容量を使用しているすべてのテナントによって共有されます。                                                           | 
| CPU／仮想コア      | <b>「物理的な制限」</b>物理的なリソース制限があります。例えば、P1なら仮想コア8個、バックエンドコア4個、メモリ25GB まで。<br><img src="pic2.png" width="150" height="150">                                                             | <b>「クラスター内でリソースが共有される理論上の制限」</b>各SKUにおいては理論上の仮想コアで、物理的にはもっと多い仮想コアが使用されます。<br>仮想コア数はCPU時間で定量化されます。P1容量に4つのバックエンドVコアがあり、30秒ごとにCPU使用率を計算します。したがって、バックエンドで最大4*30s=120sのCPU時間が処理に利用できることになります。<br><img src="pic3.png" width="150" height="150"> | 
| メモリー           | <b>「合計値の上限」</b>同時に実行する全てのワークロードによって使用されるメモリーの上限が決まっています。<br>例えばP1の場合、同時実行可能なワークロードの合計の上限は25GB までです。 | <b>「コンテンツごとの上限」</b>一つの成果物（データセット、データフロー、ページ分割されたレポートなど）に対して利用可能なメモリーの上限はあります。<br>P1は一つの成果物あたりに25GBの上限がありますが、例えば、20GBのデータセットが二つあって、同じP1容量で同時に実行することは可能です。                         | 
| ワークロード       | <b>「リソース競合が発生しうる」</b>同時に実行するワークロードは組織内のメモリー上限によって制限がありますので、リソースの競合が起きる可能性が高いです。                                          | <b>「リソース競合が回避される」</b>Power BI ワークロード (データセット、データフロー、またはページ分割されたレポート) は複数の特殊なノード グループに分かれますため、異なるワークロード間のリソース競合を回避することが可能です。                                                                                     | 
| ストレージ         | SKUごとに 100 TB                                                                                                                                              | SKUごとに 100 TB                                                                                                                                                                                                                                                                   | 
| 自動スケーリング   | 非対応                                                                                                                                                        | 対応。24時間に最大1つのコアが追加されます。料金は利用時間の従量課金制。                                                                                                                                                                                                            | 
| データ更新並列処理 | P1はデータ更新並列処理6個まで、P2は12個までなど制限があります。                                                                                               | データ更新の並列処理数に制限はありません。<br>並行して更新実行されたデータセットは、1つまたは複数のノードにロードされ、ロードされたすべてのデータセットのメモリの合計に物理的な制限がないため、CPU時間を累積してカウントすることができます。                                       | 
| スケーリング方法   | スケールアップ（P1-＞P2など）                                                                                                                                 | スケールアウト（並列処理の仮想コアの追加）                                                                                                                                                                                                                                         | 

*2021年8月時点の情報です。

[//参考①：Introducing Power BI Premium Gen2 - YouTube](https://www.youtube.com/watch?v=j17y_BPlhvU)
[//参考②：Power BI Premium Gen2 (プレビュー) について - Power BI | Microsoft Docs](https://docs.microsoft.com/ja-jp/power-bi/admin/service-premium-concepts)
[//参考③：Microsoft Power BI Premium とは何ですか? - Power BI | Microsoft Docs](https://docs.microsoft.com/ja-jp/power-bi/admin/service-premium-what-is)



<br>

## よくある質問
---


### Q.Premium Gen2 はいつリリースされる予定ですか？

Power BI Premium Gen 2 は、9月27日の週に一般公開される予定です。
今後、Gen1 をGen2 に移行するためのスケジュールについてもお知らせする予定です。

> [!IMPORTANT]
> 今利用されているGen1 が自動的にGen2 に移行されるわけではございませんのでご安心ください。 

</br>

### Q.Power BI Premium Gen2 にもメトリックアプリはありますか？

プレビュー版として、Power BI Premium Gen2 Metrics アプリの提供がございます。
Gen2 をご利用の場合はこちらのアプリをご利用ください。
詳しくは以下公式ドキュメントをご覧ください。

[Power BI Premium Gen2 Metrics アプリ (プレビュー)](https://docs.microsoft.com/ja-jp/power-bi/admin/service-premium-gen2-metrics-app)


</br>

### Q.自動スケーリングへの課金はいつから発生しますか？

Power BI Premium Gen2 が一般提供されてから30日後に開始される予定です。
それまでは、自動スケーリング利用時の課金はありません。

</br>
</br>


以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。 



