---
title: 作成したレポートを組織内で共有するために必要なライセンスは？~ Power BIライセンス（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）の違い ~
date: 2021-07-21 16:00:00
tags:
  - ライセンス
  - Power BIサービス
  - Power BI
---

こんにちは、Power BI サポート チームです。

前回のブログ Power BIでレポート作成・分析を行うために必要なものは？ ~ Power BI DesktopとPower BI サービスの違い ~ では、Power BI DesktopとPower BI サービスの違いについて説明しました。Power BI DesktopはPCにインストールして使用するアプリなので、ライセンスがなくても (サインインしなくても) 使用でき、おもにPower BI サービス上の機能を使用する際にライセンスの違いがでてきます。

本ブログでは、Power BI のライセンスについて詳細にご案内いたします。

<!-- more -->

---
## Power BIライセンス（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）の違い
---

Power BI のライセンスは、ユーザー単位と容量単位に分かれています。

ユーザー単位は関しては、Free、ProとPremium Per Userの三種類を用意しており、Freeは個人利用を目的としたライセンス、Proは他者との共有・共同作業を目的としたライセンス、Premium Per Userは高度な機能をご利用いただけるProの上位ライセンスとしてご理解いただければと思います。

容量単位につきましては、組織向けの容量プランPremium Per Capacityと開発者向けの容量プランEmbeddedがございます。
上記のライセンスにつきまして、以下に詳細をご案内いたします。

---
## Power BI Freeとは？
---

Power BI Free（Power BI （無料））は、Office365/ Microsoft 365のいずれのプランにおいても、無償かつユーザー数無制限でご利用いただけるライセンスです。

個人利用を目的としたライセンスであるため、作成したレポートやダッシュボードを、他社に共有する機能を使用することができません。

Power BI サービス上で、1ユーザーあたり、10GBの容量を使用することができます。

1つのレポートにおいて作成できるデータセットの最大サイズは1 GBです。

---
## Power BI Proとは？
---

月額制の有償ライセンスで、1ユーザーごとに1ライセンスが必要となります。（¥1,090 / 月）

Office365/Microsoft 365 E3以下のプランには含まれませんので、必要数をご契約いただく必要がありますが、E5プランにはもとから含まれますので、別途Proライセンスをご契約いただく必要はありません。Proライセンスを所持することで、Proライセンスユーザー同士でのコンテンツ共有が可能となります。

Power BI サービス上で、1ユーザーあたり、10GBの容量を使用することができます。

1つのレポートにおいて作成できるデータセットの最大サイズは1 GBです。

---
## Power BI Premium Per Userとは？
---

月額制の有償ライセンスで、1ユーザーごとに1ライセンスが必要となります。（¥2,170 / 月）

Proライセンスより使用可能なデータモデルサイズ、ストレージ容量が大幅に向上する上に、ページ分割されたレポート、データフロー、高度ななAIなどPremium機能が利用可能です。

共有につきまして、Premium Per Userの容量に保存されたコンテンツは、Premium Per Userユーザーしかアクセスできません。

Premium Per User容量が割り当てられたワークスペースには、ダイヤモンドと人のアイコンが表示されます。
![](./ppu.png)

> **参考情報**
> - [Power BI Premium Per Userについて](https://docs.microsoft.com/ja-jp/power-bi/admin/service-premium-per-user-faq)

---
## Power BI Premium Per Capacityとは？
---

Power BI Premium Per Capacityとは、ProかPremium Per Userに追加可能な容量ベースのプランとなります。（¥543,030 から / 月）

Free、Pro、Premium Per Userはユーザーに紐づくライセンスですが、Premium Per Capacityはテナントの容量に紐づくライセンスとご理解いただければと思います。

FreeとProでは、Azure上の共有リソースが割り当てられますが、Premium Per Capacityをご契約いただくことで組織専用の拡張リソースを確保し、大容量のリソースを柔軟に運用いただくことが可能となります。

また、上述で、コンテンツ共有にはお互いにProライセンスが必要であることをお伝えしていましたが、Premium Per Capacity容量に保存されたコンテンツは、Freeライセンスのユーザーも閲覧することが可能となります。

Premium Per Capacity容量が割り当てられたワークスペースには、ダイヤモンドアイコンが表示されます。
![](./PPC.png)

Power BI Premium Per Capacityの詳細については以下公開情報をご参考にしていただけますと幸いです。

> **参考情報**
> - [Power BI各ライセンスの比較](https://powerbi.microsoft.com/ja-jp/pricing/#powerbi-comparison-table)
> - [Power BI Premium とは​](https://docs.microsoft.com/ja-jp/power-bi/service-premium-what-is)
> - [Power BI Premium のよく寄せられる質問](https://docs.microsoft.com/ja-jp/power-bi/service-premium-faq)

---
## Power BI Embeddedとは？
---
Power BI Embeddedとは、アプリケーションの開発者向けにご用意した、利用時間ごとで従量課金される容量プランとなります。（¥112.9072から / 時間）

アプリケーション内にPower BIのインタラクティブなレポートを埋め込むことで、組織内外問わず、どなたでもコンテンツを閲覧いただけます。

Power BI Embeddedの詳細については以下公開情報をご参考にしていただけますと幸いです。

> **参考情報**
> - [Power BI Embedded の価格](https://azure.microsoft.com/ja-jp/pricing/details/power-bi-embedded/)
> - [Power BI Embedded とは](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/embedded-analytics-power-bi)
> - [Power BI Embedded のよく寄せられる質問](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/embedded-faq)

---

上記で紹介させていただきまました、各ライセンスの機能や特徴を以下の表にまとめました。

![](./pbi_license_features.png)

> [!NOTE]
> Premium Per CapacityとEmbedded につきましては、Premium Generation 2及びEmbedded Gen2の仕様を基づき記載しております。

最後に、非常にたくさんのお問い合わせをいただく、「各ライセンスの組み合わせにおけるコンテンツの作成・閲覧可否」について表にまとめておきました。

![](./pbi_license_share.png)

> **参考情報**
> - [同僚や他のユーザーと Power BI ダッシュボードやレポートを共有する](https://docs.microsoft.com/ja-jp/power-bi/collaborate-share/service-share-dashboards)
> - [Power BI Premium Per Userについて](https://docs.microsoft.com/ja-jp/power-bi/admin/service-premium-per-user-faq)

以上、本Blogが少しでも皆様のお役に立てますと幸いでございます。

---

> **本ブログの関連記事**
> - [Power BIでレポート作成・分析を行うために必要なものは？ ~ Power BI DesktopとPower BI サービスの違い ~](./pbi_desktop_service/)



