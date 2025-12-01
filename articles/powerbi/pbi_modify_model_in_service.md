---
title: Power BI サービスでデータモデルを編集する
date: 2023-05-31 15:00:00
tags:
  - Power BI
  - Power BI Service
  - データモデル
  - Power BI サービス
  - モデル編集
  - リレーションシップ
  - DAX
  - メジャー
  - measure
  - calculated column
  - 計算列
  - 行レベルのセキュリティ
---

こんにちは、Power BI サポート チームのチャンです。 

2023 年 4 月 下旬より、Power BI サービスでもセマンティック モデルの編集が可能となりました！また 2025 年 9 月に本機能が正式に一般提供されるようになりました。

これまでは、 Power BI サービス上で複数ユーザーで実施可能な共同作業はレポートの編集のみでしたが、本機能により、Power Query エディターによるデータ加工、新しいメジャーや計算列の作成、リレーションシップの管理、行レベルセキュリティのロール作成などといったセマンティック モデルの編集作業が、毎回.PBIX ファイルをダウンロードせずとも、Power BI サービス上で、直接実施することができます。早速本機能について詳細をご紹介していきます。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 更新履歴
---
Update: 2025/11/28
本機能の一般提供により、内容を修正しました。

- [Power BI September 2025 Feature Summary](https://powerbi.microsoft.com/ja-jp/blog/power-bi-september-2025-feature-summary/#post-30998-_Toc208591567)

---
## 目次
---
1. [本機能を有効化する設定](#本機能を有効化する設定)
2. [使用方法・メリット](#使用方法・メリット)
3. [考慮事項と制限事項](#考慮事項と制限事項)


---
## 本機能を有効化する設定
---

#### テナント設定

 既定値では有効となっていますが、 Power BI 管理者権限を持つアカウントにて、[管理ポータル] > [テナント設定] にて以下の設定「ユーザーは Power BI サービスでセマンティック モデルを編集できます」を有効化します。

<div align="center">
<img src="tenant_settings.png">
</div>

#### 編集画面を開く

発行済みのセマンティック モデルに対して、[...]でオプションを展開すると、[セマンティック モデルを開く] という選択肢を選択します。

<div align="center">
<img src="dataset_options.png">
</div>

[セマンティック モデルを開く] をクリックすると、モデルの詳細を確認できる画面へアクセスできます。
右上の[表示中] タブをクリックして、[編集] を選択すると編集する画面へ遷移されます。
その際に、セマンティック モデルは自動的に [大規模セマンティック モデルのストレージ形式](https://learn.microsoft.com/ja-jp/power-bi/transform-model/service-semantic-model-version-history#considerations-with-large-semantic-model-storage-format) に変換されます。

<div align="center">
<img src="open_data_model.png">
</div>
</br>
---
## 使用方法・メリット
---

####  使用方法

以下の画像の通り、Power BI サービス上で、Power Query エディターによるデータ加工や、新しいメジャー、計算列と計算テーブル、計算グループ、パラメーター、行レベルセキュリティ用の新しいロールを作成できます。

<div align="center">
<img src="open_data_model2.png">
</div>

> **参考情報** <br>
> 
> Power Query エディターによるデータ加工
> - [Power Query のユーザー インターフェイス](https://learn.microsoft.com/ja-jp/power-query/power-query-ui)
> 
> メジャーの作成
> - [チュートリアル: Power BI Desktop で独自のメジャーを作成する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-tutorial-create-measures)
> 
> 計算列の作成
> - [チュートリアル: Power BI Desktop で計算列を作成する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-tutorial-create-calculated-columns)
> 
> 計算テーブルの作成
> - [Power BI Desktop で計算テーブルを作成する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-calculated-tables)
> 
> 計算グループの作成
> - [計算グループを作成する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/calculation-groups)
> 
> フィールドパラメーターの作成
> - [レポート閲覧者がフィールド パラメーターを使用してビジュアルを変更できるようにする](https://learn.microsoft.com/ja-jp/power-bi/create-reports/power-bi-field-parameters)
>
> 行レベルセキュリティについて
> - [Power BI での行レベルのセキュリティ (RLS)](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-rls)
> 
> モデルのリレーションシップについて
> - [Power BI Desktop でのモデル リレーションシップ](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-relationships-understand)

例えば、リレーションシップにつきましても、以下の例で示すように Calendar テーブルと financials テーブルの間でリレーションシップを作成する場合、まずリレーションシップとして設定したい両方の「 Date 」列に対して、片方のテーブルの列をドラッグして、もう片方の列にドロップします。

<div align="center">
<img src="tables.png">
</div>

そうすると、リレーションシップを設定するウィザードが表示されますので、そこから詳細なリレーションシップを設定できます。

<div align="center">
<img src="relationship.png">
</div>
</br>
<div align="center">
<img src="relationship2.png">
</div>
</br>

####  メリット

メジャー・計算列・計算テーブルの作成機能においては、数式のオートコンプリート（入力すると、自動的に利用可能な関数や完全な数式を提示してくれる機能）が実装されているため、 Power BI Desktop でのモデル編集と比較しても全く劣りません。

また、物理的にレポートファイルの受け渡しをせずとも、簡単に複数のユーザーによる編集が可能な点、会社のルールや端末のスペックにより Power BI Desktop アプリケーションのインストールができないユーザーでも実施できることなども、大きなメリットでございます。

行レベルセキュリティの作成に関して、特に Power BI Desktop より便利な点としては、ロールを定義したら、すぐに、作成したロールに適用したいユーザーまで設定できることです。

<div align="center">
<img src="rls_role.png">
</div>

これまでは、まずは Power BI Desktop でロールを作成し、 Power BI サービスへ発行してから、セマンティック モデルの [セキュリティ] から行レベルセキュリティの適用ユーザーを設定する必要がありましたが、本機能を利用することで、一連の流れとして同じ画面内で設定できるため、よりスムーズなオペレーションを実施できます。

---
## 考慮事項と制限事項
---

本機能は Power BI Desktop との機能差異や制限事項が多く存在しています。その中から、一部ご紹介いたします。

- セマンティック モデルを変更すると、変更が自動的に保存されます。 [セマンティック モデルのバージョン履歴](https://learn.microsoft.com/ja-jp/power-bi/transform-model/service-semantic-model-version-history) は、Web で編集されたセマンティック モデルでサポートされています。 この機能を使用すると、重大なミスから回復できます。

- Power Query エディターを使用してデータを変換するか、新しいデータ ソースに接続することは、インポート ストレージ モードでのみサポートされます。

- Power Query エディター で [キャンセル] を選択するか、[Power Query] ダイアログを閉じると、クエリに加えられた変更は破棄されます。

- 以下の種類のセマンティック モデルは編集機能がサポートされていません。
  - 増分更新が設定されているセマンティック モデル
  - デプロイ パイプラインを介してデプロイされたセマンティック モデルは、開発ワークスペース内の Web でのみ編集できます。 テスト ワークスペースと運用ワークスペースでの編集はサポートされていません。
  - 自動集計が構成されているセマンティック モデル
  - ライブ接続があるセマンティック モデル
  - Azure Analysis Services (AAS) から移行されたセマンティック モデル

- テーブルのストレージモードの変更ができません。

上述した考慮事項の他にもございますので、詳細につきまして、以下の公開情報にて最新状況をご確認ください。

> [!NOTE]
> [考慮事項と制限事項 | Power BI サービスでデータ モデルを編集する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/service-edit-data-models?source=recommendations#considerations-and-limitations)

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

> **参考情報**
> - [Power BI サービスでデータ モデルを編集する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/service-edit-data-models) 


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)