---
title: Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）
date: 2021-07-30 16:00:00
tags:
  - Power BI
  - ライセンス
  - Power BI サービス
---

こんにちは、Power BI サポート チームのチャンです。

前回のブログ「[Power BI Desktop とPower BI サービスの違い：Power BIでレポート作成・分析を行うために必要なものは？ ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_desktop_service/)」では、Power BI DesktopとPower BI サービスの違いについて説明しました。

本ブログでは、Power BI のライセンスについて詳細にご案内いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## Power BI ライセンス（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）の違い
---

Power BI のライセンスは、ユーザー単位と容量単位に分かれています。

ユーザー単位は関しては、Power BI Free（以下Free）、Power BI Pro （以下Pro）とPower BI Premium Per User（以下Premium Per User）の三種類を用意しており、Free は個人利用を目的としたライセンス、Pro は他者との共有・共同作業を目的としたライセンス、Premium Per User は高度な機能をご利用いただけるProの上位ライセンスとしてご理解いただければと思います。

容量単位につきましては、組織向けの容量プランPower BI Premium Per Capacity（以下Premium Per Capacity）と開発者向けの容量プランPower BI Embedded（以下Embedded）がございます。
上記のライセンスにつきまして、以下に詳細をご案内いたします。

---
## Power BI Free とは？
---

Power BI Free（Power BI （無料））（以下Free）は、Office365/ Microsoft 365 のいずれのプランにおいても、無償かつユーザー数無制限でご利用いただけるライセンスです。

個人利用を目的としたライセンスであるため、作成したレポートやダッシュボードを、他者に共有する機能を使用することができません。

---
## Power BI Pro とは？
---

Power BI Pro （以下Pro）は、月額制の有償ライセンスで、1ユーザーごとに1ライセンスが必要となります。（¥1,090 / 月）

Office365/ Microsoft 365 E3 以下のプランには含まれませんので、必要数をご契約いただく必要がありますが、E5 プランにはもとから含まれますので、別途Pro ライセンスをご契約いただく必要はありません。Pro ライセンスを所持することで、Proライセンスユーザー同士でのコンテンツ共有が可能となります。

---
## Power BI Premium Per User とは？
---

Power BI Premium Per User（以下Premium Per User）は、月額制の有償ライセンスで、1ユーザーごとに1ライセンスが必要となります。（¥2,170 / 月）

Proライセンスより使用可能なデータモデルサイズ、ストレージ容量が大幅に向上する上に、ページ分割されたレポート、データフロー、高度なAI などPremium 機能が利用可能です。

共有につきまして、Premium Per User の容量に保存されたコンテンツは、Premium Per User ユーザーしかアクセスできません。

Premium Per User 容量が割り当てられたワークスペースには、ダイヤモンドと人のアイコンが表示されます。
![](./ppu.png)

> **参考情報**
> - [Power BI Premium Per User について](https://learn.microsoft.com/ja-jp/power-bi/admin/service-premium-per-user-faq)

---
## Power BI Premium Per Capacity とは？
---

Power BI Premium Per Capacity （以下Premium Per Capacity）とは、Pro か Premium Per User に追加可能な容量ベースのプランとなります。（¥543,030 から / 月）

Free、Pro、Premium Per User はユーザーに紐づくライセンスですが、Premium Per Capacity はテナントの容量に紐づくライセンスとご理解いただければと思います。

Free と Pro では、Azure 上の共有リソースが割り当てられますが、Premium Per Capacity をご契約いただくことで組織専用の拡張リソースを確保し、大容量のリソースを柔軟に運用いただくことが可能となります。

また、上述で、コンテンツ共有にはお互いに Pro ライセンスが必要であることをお伝えしていましたが、Premium Per Capacity 容量に保存されたコンテンツは、Free ライセンスのユーザーも閲覧することが可能となります。

Premium Per Capacity 容量が割り当てられたワークスペースには、ダイヤモンドアイコンが表示されます。
![](./PPC.png)

Power BI Premium Per Capacity の詳細については以下公開情報をご参考にしていただけますと幸いです。

> **参考情報**
> - [Power BI 各ライセンスの比較](https://powerbi.microsoft.com/ja-jp/pricing/#powerbi-comparison-table)
> - [Power BI Premium とは​](https://learn.microsoft.com/ja-jp/power-bi/service-premium-what-is)
> - [Power BI Premium のよく寄せられる質問](https://learn.microsoft.com/ja-jp/power-bi/service-premium-faq)

---
## Power BI Embeddedとは？
---
Power BI Embedded（以下Embedded）とは、アプリケーションの開発者向けにご用意した、利用時間ごとで従量課金される容量プランとなります。（¥112.9072から / 時間）

Embedded には、顧客向け埋め込みと組織向け埋め込みという2種類の埋め込みがあります。

顧客向け埋め込みは、事前にサービスプリンシパル、またはマスターアカウントの認証をアプリケーションで設定しておくことで、組織外のどなたでもコンテンツを閲覧いただけます。

組織向け埋め込みは、アプリケーション側のユーザー認証によって、適切なライセンスを持つ組織内のユーザーはアプリケーションから直接Power BI サービス上のレポートへアクセスできます。

Power BI Embedded の詳細については以下公開情報をご参考にしていただけますと幸いです。

> **参考情報**
> - [Power BI Embedded の価格](https://azure.microsoft.com/ja-jp/pricing/details/power-bi-embedded/)
> - [Power BI Embedded とは](https://learn.microsoft.com/ja-jp/power-bi/developer/embedded/embedded-analytics-power-bi)
> - [Power BI Embedded のよく寄せられる質問](https://learn.microsoft.com/ja-jp/power-bi/developer/embedded/embedded-faq)
> - [顧客向けにコンテンツを埋め込む](https://learn.microsoft.com/ja-jp/power-bi/developer/embedded/embed-sample-for-customers)
> - [組織向けにコンテンツを埋め込む](https://learn.microsoft.com/ja-jp/power-bi/developer/embedded/embed-sample-for-your-organization)
---

---
## 機能比較表
---

上記で紹介させていただきまました、各ライセンスの機能や特徴を以下の表にまとめました。

|   | **Free** | **Pro** | **Premium Per User** | **Premium	Per Capacity** | **Embedded** |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| **価格** | 無償（ユーザー数無制限） |	¥1,090/月額・ユーザー | ¥2,170/月額・ユーザー | ¥543,030 ～/月額・容量 | ¥112.9～/ 時間・容量 |
| **用途** | 個人利用 | 複数人共同作業 | 高度な機能利用、複数人共同作業 | 大規模組織専用 | アプリケーション開発者用 |
| **レポート・データセット作成** | 〇 ※1 | 〇 |	〇 | × ※2 | × ※2 |
| **レポート・データセット発行** | 〇 ※1 | 〇 | 〇 | × ※2 | × ※2 |
| **コンテンツ共有と共同作業** | × | 〇 | 〇 | × ※2 | × ※2 |
| **無償ユーザーのコンテンツ閲覧** | × | × | × | 〇 | × |
| **ストレージ上限** ※5 <br>① マイワークスペース<br>② 共有ワークスペース<br>③ Premiumワークスペース | ① 10GB/ ユーザー <br> ② × <br>  ③ × | ① 10GB/ ユーザー<br> ② 10GB/ ワークスペース <br>③ ×  | ① 10GB/ ユーザー<br> ② 10GB/ ワークスペース <br>③ 100TB/テナント | ① 10GB/ ユーザー<br> ② 10GB/ ワークスペース <br>③ 100TB/ 容量 | ① 10GB/ ユーザー<br> ② 10GB/ ワークスペース <br>③ 100TB/ 容量 |
| **データセットサイズ制限** | 1GB | 1GB | 100GB ※4 | 25GB～100GB ※4 | 3GB～100GB ※4 |
| **自動更新** | 8回/日 | 8回/日 | 48回/日 | 48回/日 | 48回/日 |
| **ページ分割レポート** | 〇 | 〇 | 〇 |	〇 | 〇 |
| **データフロー** | × | 〇 ※3 | 〇 | 〇 | 〇 |
| **デプロイパイプライン** | × | × | 〇 | 〇 | 〇 |
| **高度なAI（言語処理、画像処理、自動化機械学習）** | × | × | 〇 | 〇 | 〇※6 |
| **XMLAエンドポイント利用** | × | × | 〇 | 〇 | 〇 |
| **自動スケーリングのアドオン** | × | × | × | 〇 （¥9,521 /仮想コア/24 時間単位） | × |
| **Multi-Geo（複数地域・リージョン利用）** | × | × | × | 〇 | 〇 |

※1：マイワークスペース内のみ
※2：別途ユーザーライセンスが必要
※3：[Premiumデータフロー機能](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dataflows/dataflows-premium-features) は利用できない
※4：Power BI Desktopから発行する際の[アップロード時のサイズ上限が10GBまで](https://learn.microsoft.com/ja-jp/power-bi/admin/service-premium-large-models)。
※5：共有ワークスペースの総容量はライセンス数による上限がございます。詳細はこちらのブログ記事「[Power BI Pro のワークスペース容量について](../pbi_storage)」をご参照ください。
※6：Embedded容量のA2以降でサポートされます。

> [!NOTE]
> Premium Per Capacity とEmbedded につきましては、Premium Generation 2 及びEmbedded Generation 2 の仕様を基づき記載しております。

---
## ライセンス組み合わせのコンテンツ閲覧可否
---

最後に、非常にたくさんのお問い合わせをいただく、**「各ライセンスの組み合わせにおけるコンテンツの閲覧可否」**について表にまとめておきました。

| ユーザーライセンス / ワークスペースの種類  | Power BI Pro | Premium Per User | Premium Per Capacity | Embedded |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| Free | × | × | 〇 | × |
| Pro | 〇 | × | 〇 | 〇 |
| Premium Per User | 〇 | 〇 | 〇 | 〇 |

> **参考情報**
> - [同僚や他のユーザーと Power BI ダッシュボードやレポートを共有する](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-share-dashboards)
> - [Power BI Premium Per User について](https://learn.microsoft.com/ja-jp/power-bi/admin/service-premium-per-user-faq)

> **本ブログの関連記事**
> - [Power BI Desktop とPower BI サービスの違い：Power BIでレポート作成・分析を行うために必要なものは？](../pbi_desktop_service/)
> - [Power BI ライセンスの導入：利用目的による組み合わせ](../pbi_license2/)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)



