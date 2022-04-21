
---
title: Power BI Embedded とは？ライセンスと埋め込み方法
date: 2022-03-31 15:00:00 
tags:
  - Power BI　　
  - 埋め込み
  - Embed
  - Embedded
  - 開発者向け
  - 顧客向け埋め込み
  - 組織向け埋め込み
  - App Owns Data
  - User Owns Data
---


こんにちは、Power BI サポート チームです。   

Power BI で作成したレポートを埋め込み方法について、以前に以下のBlog 記事でご紹介させていただきましたが、その中にある「 Power BI Embedded 」による埋め込みに関して、顧客向け埋め込み (Apps Own Data) や組織向け埋め込み (Users Own Data) など複数の種類がありますが、そもそも「 Power BI Embedded とは」という質問もたくさん受けておりますので、本ブログにて「 Power BI Embedded 」について詳しくご紹介いたします。

<!-- more -->

> **参考情報：**
> - [Power BI レポートの埋め込み方法の種類について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_embed/)  


> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


---
## Power BI Embedded とは
---

Power BI Embedded という言葉について、「ライセンス」と「実装方法」という二つの概念が存在します。

### ■ライセンス

「ライセンス」の Power BI Embedded に関しては、Power BI Premium Per Capacity (Premium 容量) と同じように容量ごとのライセンスとなります。

詳細の機能比較表については、以下のブログ記事でも紹介いたしましたが、

> **参考情報：**
> - [Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）](../pbi_license/)  

Power BI Premium Per Capacity（Premium 容量）と最も大きな違いとして、購入方法及び費用計算方法を挙げられます。

Power BI Premium Per Capacity は Microsoft 365 管理センターで購入できるライセンスに対して、Power BI Embedded は Azure ポータルで作成できるAzure のリソースです。そのため、Azure のサブスクリプションの購入が必要となります。

Power BI Premium Per Capacity は月額または年単位の請求に対して、Power BI Embedded はリソースが有効にされている時間によって、従量課金制の請求となります。

Azure ポータルで、Power BI Embedded のリソースを作成する方法の詳細につきましては、以下のドキュメントをご参照ください。

> **参考情報：**
> - [Azure Portal での Power BI Embedded 容量の作成 - Power BI | Microsoft Docs](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/azure-pbie-create-capacity?tabs=portal%2Cui)


### ■実装方法

Power BI Embedded の実装方法では、以下の2種類がございます。
- 顧客向けに埋め込む (App owns data)
- 組織向けの埋め込み (User owns data)

> [!TIP]
> 注意点として、Power BI Embedded 分析の埋め込みアプリケーションを作成するのに、必ずしも上記 Azure ポータルで作成される Power BI Embedded リソースが**必要ではありません**。

以下にて 2 種類の埋め込みの比較を記載いたします。

|     |  **顧客向けに埋め込む**  |  **組織向けに埋め込む**  | 
| ------------ | ------------ | ------------ | 
| **対象** | 外部ユーザー（顧客） | 内部ユーザー（組織内） | 
| **認証方法** | 独自の認証方法  | Azure AD 認証  | 
| **ユーザーごとのライセンス** | 必要なし | Power BI ライセンス必要 | 
| **対話型・非対話型認証** | 非対話型認証：アプリの認証には、「サービス プリンシパル」または「マスタ ーユーザー」が使用される | 対話型認証：アプリの認証には、アプリ ユーザーの資格情報が使用される | 


続きまして、「顧客向け埋め込み」と「組織向けの埋め込み」の詳細条件についてご紹介いたします。

---
## 顧客向け埋め込み
---

顧客向け埋め込みは、ユーザーごとのPower BI ライセンスを所持して**いない**場合に使用される埋め込み方法です。

実装するための前提条件は以下が必要となります。
- 独自の Azure Active Directory テナント
- 認証方法：サービス プリンシパル または マスターユーザー (Pro ライセンス または Premium Per User ライセンスのユーザー）
- [容量の購入](#埋め込み用容量の種類)と割り当て (Power BI Premium Per Capacity または Power BI Embedded )

> [!NOTE]
> ※ 開発を行う際には、容量の購入は不要ですが、実際本番環境で運用開始される際には、容量の購入が必要です。


詳細な実装方法につきましては、以下のドキュメントにて、ステップバイステップのチュートリアルが記載されていますので、よろしければ、ご参考ください。

> **参考情報：**
> - [チュートリアル:"顧客向けの埋め込み" サンプル アプリケーションを使用して Power BI コンテンツを埋め込む](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/embed-sample-for-customers?tabs=net-core)


---
## 組織向け埋め込み
---

組織向け埋め込みは、ユーザーごとの Power BI ライセンスを所持して**いる**場合に使用される埋め込み方法です。

実装するための前提条件は以下が必要となります。
- 独自の Azure Active Directory テナント
- Power BI Pro ライセンスまたは Premium Per User ライセンス
- 運用に移す際は、以下の**いずれか**の組み合わせのライセンスが必要です。
   - Pro ライセンスを持つすべてのユーザー
   - PPU ライセンスを持つすべてのユーザー
   - [P または EM容量](#埋め込み用容量の種類)。この構成を使用すると、すべてのユーザーが無料ライセンスを持つことができます

詳細な実装方法につきましては、以下のドキュメントにて、ステップバイステップのチュートリアルが記載されていますので、よろしければ、ご参考ください。

> **参考情報：**
> - [チュートリアル:"組織向けの埋め込み" サンプル アプリケーションを使用して Power BI コンテンツを埋め込む](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/embed-sample-for-your-organization?tabs=net-core)


---
## 埋め込み用容量の種類
---

埋め込み用の容量の種類に関しては、以下の比較表及びドキュメントをご確認ください。

| **支払いと使用方法** | **Power BI Embedded** | **Power BI Premium**  | **Power BI Premium**    | 
| ------------ | ------------ | ------------ | ------------ | 
| **プラン**  | Azure | Office  | Office  | 
| **SKU**  | A  | EM  | P  | 
| **請求** | 1 時間ごと  | 月単位  | 月単位 | 
| **コミットメント**  | なし | 年単位  | 月単位または年単位  | 
| **使用方法**  | Azure リソースは以下が可能です:<br> - [スケールアップまたはダウン](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/azure-pbie-scale-capacity) <br> - [一時停止と再開](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/azure-pbie-pause-start) | アプリ、Microsoft アプリケーションへの埋め込み | アプリ、Power BI サービスへの埋め込み | 

> **参考情報：**
> - [Power BI Embedded の分析の容量と SKU](https://docs.microsoft.com/ja-jp/power-bi/developer/embedded/embedded-capacity?tabs=gen2)

-----


以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。


