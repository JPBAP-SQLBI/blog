---
title: Power BI サービスでデータモデルを編集する
date: 2023-05-31 15:00:00
tags:
  - Power BI
  - データモデル
  - Power BIサービス
  - モデル編集
  - リレーションシップ
  - メジャー
  - 計算列
  - 行レベルのセキュリティー
---

こんにちは、Power BI サポート チームのチャンです。 

2023 年 4 月 下旬より、新機能リリースによって、Power BI サービスでもデータセット（データモデル）の編集が可能となりました！

これまでは、 Power BI サービス上で複数ユーザーで実施可能な共同作業はレポートの編集のみでしたが、本機能により、新しいメジャーや計算列の作成、リレーションシップの管理、行レベルセキュリティのロール作成などといったデータセットの編集作業が、毎回.PBIX ファイルをダウンロードせずとも、Power BI サービス上で、直接実施することができます。早速本機能について詳細をご紹介していきます。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。
> <br><br>
> また、本機能は開発段階 (プレビュー) でございますため、今後予告なしに機能が削除されたり、
> 動作変更が発生する可能性がありますことをあらかじめご了承くださいますようお願い申し上げます。

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

 既定値では有効となっていますが、 Power BI 管理者権限を持つアカウントにて、[管理ポータル] > [テナント設定] にて以下の設定「ユーザーはPower BI サービスでデータ モデルを編集できます (プレビュー)」を有効化します。

<div align="center">
<img src="tenant_settings.png">
</div>

#### ワークスペースの設定

本機能を使用したいワークスペースに対して、ワークスペースの管理者にて、[設定]を開き、[Power BI] [全般] > データモデルの設定の中に、「ユーザーは Power BI サービスでデータ モデルを編集できます (プレビュー)」にチェックを入れてください。

<div align="center">
<img src="workspace_settings.png">
</div>

チェックを入れて、有効化されたら、発行済みのデータセットに対して、[...]でオプションを展開すると、「オープンデータモデル」という選択肢が有効になっていることがわかります。

<div align="center">
<img src="dataset_options.png">
</div>

[オープンデータモデル]をクリックすると、モデルの編集画面へアクセスできます。

<div align="center">
<img src="open_data_model.png">
</div>

---
## 使用方法・メリット
---

####  使用方法

以下の画像の選択肢の通り、Power BI サービス上で、新しいメジャー、計算列と計算テーブル、行レベルセキュリティ用の新しいロールを作成できます。

<div align="center">
<img src="open_data_model2.png">
</div>

> **参考情報**
> メジャーの作成
> - [チュートリアル: Power BI Desktop で独自のメジャーを作成する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-tutorial-create-measures)
> 
> 計算列の作成
> - [チュートリアル: Power BI Desktop で計算列を作成する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-tutorial-create-calculated-columns)
> 
> 計算テーブルの作成
> - [Power BI Desktop で計算テーブルを作成する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-calculated-tables)
> 
> 行レベルセキュリティについて
> - [Power BI での行レベルのセキュリティ (RLS)](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-rls)

リレーションシップにつきましても作成できますが、現状アイコンがないため、例えば以下の例で示すように Calendar テーブルと financials テーブルの間でリレーションシップを作成する場合、まずリレーションシップとして設定したい両方の「 Date 」列に対して、片方のテーブルの列をドラッグして、もう片方の列にドロップします。

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

> **参考情報**
> モデルのリレーションシップについて
> - [Power BI Desktop でのモデル リレーションシップ](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-relationships-understand)


####  メリット

メジャー・計算列・計算テーブルの作成機能においては、数式のオートコンプリート（入力すると、自動的に利用可能な関数や完全な数式を提示してくれる機能）が実装されているため、 Power BI Desktop でのモデル編集と比較しても全く劣りません。

また、物理的にレポートファイルの受け渡しをせずとも、簡単に複数のユーザーによる編集が可能な点、会社のルールや端末のスペックにより Power BI Desktop アプリケーションのインストールができないユーザーでも実施できることなども、大きなメリットでございます。

行レベルセキュリティの作成に関して、特に Power BI Desktop より便利な点としては、ロールを定義したら、すぐに、作成したロールに適用したいユーザーまで設定できることです。

<div align="center">
<img src="rls_role.png">
</div>

これまでは、まずは Power BI Desktop でロールを作成し、 Power BI サービスへ発行してから、データセットの[セキュリティ]から行レベルセキュリティの適用ユーザーを設定する必要がありましたが、本機能を利用することで、一連の流れとして同じ画面内で設定できるため、よりスムーズなオペレーションを実施できます。

---
## 考慮事項と制限事項
---

本記事を執筆した時点では、プレビュー機能なため、Power BI Desktop との機能差異や制限事項がまだ多く存在しています。
その中から、一部ご紹介いたします。

- データ モデルを変更すると、変更は自動的に保存されます。 変更は永続的であり、元に戻すオプションはございませんので十分にご注意ください。

- 本機能はモデルの編集のみなため、新しいデータソースへの接続や、 Power Query によるデータ加工は実施できません。代わりにデータフローやデータマートのご利用をご検討ください。

> [!NOTE]
> [Power BI データフローとデータセット及びデータマートの紹介と比較](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_dataflow_dataset/)

- 増分更新が設定されているデータセット、デプロイパイプラインによるデプロイされたデータセット、 XMLA エンドポイントによって変更されたデータセット、ライブ接続を持つデータセットなどはサポートされていません。

- 現在はマイワークスペースを含め、すべてのライセンスのワークスペースでご利用可能ですが、 今後一部の Pro ライセンスのワークスペースでは利用できなくなります。

- データソース側のテーブルや列に対して、名前を変更することはできません。

- テーブルのストレージモードの変更ができません。


上述した考慮事項の他にもございますので、詳細につきまして、以下の公開情報にて最新状況をご確認ください。

> [!NOTE]
> [考慮事項と制限事項 | Power BI サービスでデータ モデルを編集する (プレビュー)](https://learn.microsoft.com/ja-jp/power-bi/transform-model/service-edit-data-models?source=recommendations#considerations-and-limitations)

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。 

> **参考情報**
> - [Power BI サービスでデータ モデルを編集する (プレビュー)](https://learn.microsoft.com/ja-jp/power-bi/transform-model/service-edit-data-models) 



