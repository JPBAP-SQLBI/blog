---
title: Power BI ブログ更新情報
date: 2024-06-28 00:00:00 
tags:
  - Power BI
---
こんにちは、Power BI サポートチームです。

いつもPower BI CSS ブログをご覧いただき、誠にありがとうございます。これまで多くのサポートチームのブログ有志の尽力により、約100本のブログが作成されてきました。

これらの記事をより活用いただけるように、新規記事や更新記事の情報をまとめ、また、カテゴリごとに整理しました。

今後も新しい記事が作成され次第、随時ブログを更新してまいりますので、皆様のお役に立てるよう努めます。引き続きご支援のほど、よろしくお願いいたします。

<!-- more -->　

> [!IMPORTANT]  
> ブログの内容は弊社の公式ドキュメントに基づいて構成されておりますが、最新の機能に相違がある場合がございます。
> 最新情報については、ブログ記載されている公式ドキュメントをご確認ください。


</br>

## 目次
・[ブログ更新情報](#ブログ更新情報)

・[Power BI Desktop](#Power-BI-Desktop)
・[ビジュアルと表示](#ビジュアルと表示)
・[Power Query](#Power-Query)
・[コンテンツ共有](#コンテンツ共有)
・[データ ゲートウェイ](#データ-ゲートウェイ)
・[ワークスペース管理](#ワークスペース管理)
・[テナント及びユーザー管理](#テナント及びユーザー管理)
・[REST API](#REST-API)
・[データ接続](#データ接続)
・[トラブルシューティング](#トラブルシューティング)
・[ライセンス](#ライセンス)
・[増分更新](#増分更新)
・[機能紹介](#機能紹介)
・[Premium 機能](#Premium-機能)
・[通信設定](#通信設定)
・[Report Server](#Report-Server)
・[サポート関連](#サポート関連)
・[その他](#その他)

</br>


## ブログ更新情報

### 2025年9月の記事

#### 新規記事
[URL フィルターの使い方](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_url_filter/)
Power BI の Premium 機能として提供されていた Cognitive service と Azure ML を利用する AI 機能廃止に伴う必要な対応についてご案内しております。

#### 更新した記事

今月の更新した記事はございません。

### 2025年8月の記事

#### 新規記事
[Cognitive service と Azure ML の廃止](https://jpbap-sqlbi.github.io/blog/powerbi/Retirement-CognitiveServices-and-AzureML/)
Power BI の Premium 機能として提供されていた Cognitive service と Azure ML を利用する AI 機能廃止に伴う必要な対応についてご案内しております。
</br>

[2025 年 3 月版以降の Power BI Desktop では CPU で AVX 命令がサポートされている必要があります](https://jpbap-sqlbi.github.io/blog/powerbi/PowerBIDesktop-AVX/)
サポートされていない CPU では予期しない動作となる場合とその対応についてご案内いたします。
</br>

[アプリ・レポートを閲覧できないときの対処法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_cannot_view_report/)
Power BI サービスでレポートやアプリを共有されたユーザーが、そのコンテンツを表示できない場合に想定される原因と対処法をご紹介しております。
</br>

[ホーム テナント リージョンの変更についてのご案内](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_region_move/)
Power BI Datamart サポート終了の背景や影響、移行方法等についてご案内しております。


#### 更新した記事

今月の更新した記事はございません。

---

</br>

### 2025年7月の記事

#### 新規記事
[データフローの更新方法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_dataflow_refresh/)
各種データフロー（データフロー Gen1,Gen2,Gen2 CI/CD）の更新方法についてご案内しております。
</br>

[Power BI データマートの廃止と Fabric Data Warehouse への移行について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_datamart_retirement/)
Power BI Datamart サポート終了の背景や影響、移行方法等についてご案内しております。
</br>

#### 更新した記事
[Power BIのマップビジュアル](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_map_visual/)
Azure マップのテナント設定や利用要件に変更点がありましたので、 Azure マップ セッションの内容を更新しました。 
</br>

[Power BI Service でサービス プリンシパルを利用する](https://jpbap-sqlbi.github.io/blog/powerbi/ServicePrincipal/)
テナント設定の名称に変更がありましたので、 Power BI のテナント設定 セクションの内容を更新しました。
</br>

---

## Power BI Desktop
[「メモリ不足のため完了できません」エラーの対処策 - Power BI Desktop](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_desktop_outofmemory_error/)
[Power BI Desktop のインストール・更新方法について](https://jpbap-sqlbi.github.io/blog/powerbi/powerbidesktop_install/)
[Power BI Desktop のコンポーネント変更について(Webview2)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_desktop_webview2/)
[Power BI Desktopのトラブルシューティング：提供された資格情報で認証できない　](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_datasource_authentication/)
[Power BI 利用時のパフォーマンス測定や最適化について](https://jpbap-sqlbi.github.io/blog/powerbi/performance/)

## ビジュアルと表示
[Power BI 「レーダーチャート」 ビジュアル](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_visual_radarchart/)
[Power BI テーマについて](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_theme_introduction/)
[Power BI での大文字小文字の区別](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_model_character_tips/)
[Power BI のマップビジュアルで地名が正常に認識されない場合](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_map_areaname/)
[Power BIのマップビジュアル](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_map_visual/)
[Power BIのレポート機能「スパークライン」](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_visual_sparkline/)
[よくある「並べ替え」のお問い合わせ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_sorting/)
[動的にビジュアル変換ができる「フィールドパラメーター」](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_field_parameter/)
[条件付き書式で作るヒートマップ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_visual_heatmap/)
[Power BI サービスに発行したレポートの時刻のずれについて](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_service_timezone/)
[Power BI サービスにおける固定フィルター](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_persistent_filters/)
[**NEW! 3月** ブックマークとボタンで動的にレポート画面を切り替える方法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_button_bookmark/)

## Power Query
[pbix ファイルのデータソースのファイル格納場所が変更される場合の対処策](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_changing_datasource_file_place/)
[Power BI サービスでデータモデルを編集する](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_modify_model_in_service/)
[Power BIにおけるデータソースのパラメーター化](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_datasource_parameter/)
[メジャーと計算列（新しい列）の比較](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_measures_calculatedcolumns/)
[横持ちのデータを縦持ちに変換する「列のピボット解除」](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_dataset_unpivot/)

## コンテンツ共有
[Power BI サービスでのコンテンツ共有方法の種類](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_contents_share_1/)
[組織外のユーザーとPower BIコンテンツの共有](https://jpbap-sqlbi.github.io/blog/powerbi/aad_guestuser/)
[Power BIでデータに接続しレポートを作成・共有する手順](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_how_to_create_report/)

## データ ゲートウェイ
[オンプレミス データ ゲートウェイのインストールの手順](https://jpbap-sqlbi.github.io/blog/powerbi/all_gateway_howto_Installation/)
[オンプレミス データ ゲートウェイのトラブルシューティング：構成時に発生するエラー](https://jpbap-sqlbi.github.io/blog/powerbi/gateway_troubleshooting/)
[オンプレミス データ ゲートウェイのトラブルシューティング：運用時に発生するエラー](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_gateway_troubleshooting2/)
[オンプレミスデータゲートウェイのセキュリティーロール](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_gateway_role/)
[Power Platform管理センターからオンプレミス データ ゲートウェイのインストールの制御方法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_gateway_Installation_control/)
[仮想ネットワーク (VNet) データ ゲートウェイ について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_vnet%20data%20gateway/)
[仮想ネットワーク (VNet) データ ゲートウェイからプライベートデータソースへの接続](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_vnet_data_gateway_private/)
[オンプレミス データ ゲートウェイのサービスが自動起動しない場合の対処策](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_pbiegwservice/)

## ワークスペース管理
[Power BI Pro のワークスペース容量について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_storage/)
[Power BI ワークスペースに関するよくあるお問い合わせ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_workspace_qna/)
[Power BIワークスペースのガバナンス](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_workspace_governance/)
[ワークスペースの使用量を確認する](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_workspace_capacity/)
[組織内のユーザーのマイ ワークスペースへアクセスする方法](組織内のユーザーのマイワークスペースへアクセスする方法)

## テナント及びユーザー管理
[Azure AD の外部コラボレーションの設定が与える影響について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_guest_user_access_restrict/)
[Power BI Service へのアクセス制御① 条件付きアクセス](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_conditional-access/)
[Power BI Service へのアクセス制御② Azure Private Link](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_privatelink/)
[Power BI Service へのアクセス制御③ 秘密度ラベル](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_sensitivity-label/)
[Power BI のユーザーアクティビティ追跡方法の比較](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_activity_log_usage_metrics/)
[Power BIユーザーの退職・異動への備え](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_user_handover/)
[コンテンツの承認（昇格・認定）と検出について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_endorsement/)
[ユーザーの操作におけるPower BIのアクティビティログ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_track_activity_log/)
[Power BI の管理について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_admin/)

## REST API
[Power BI Service でサービス プリンシパルを利用する](https://jpbap-sqlbi.github.io/blog/powerbi/ServicePrincipal/)
[Power BI のテナント設定の状況を一括抽出する方法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_api_export_tenant_settings/)
[REST API を組み合わせて情報を取得する](https://jpbap-sqlbi.github.io/blog/powerbi/restapi/)
[セマンティック モデルの更新履歴を REST API で取得する方法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_refreshhistory/)

## データ接続
[「インポート」と「Direct Query」データセットの違い](https://jpbap-sqlbi.github.io/blog/powerbi/storage_mode/)
[Power BI のリアルタイム分析](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_realtime_analytics/)
[Private なデータソースへ接続する](https://jpbap-sqlbi.github.io/blog/powerbi/PrivateDatasource/)
[プライバシー レベルの選択について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_privacylevels/)
[Power BI 複合モデル](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_composite_mode/)

## トラブルシューティング
[「テーブルの列 ‘***’ が見つかりませんでした。」Power BI更新エラーについて](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_reflesh_error/)
[レポート発行後の「ファイルは公開されましたが、切断されました」メッセージについて](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_publish_error/)
[Oracle データベースとの接続におけるトラブルシューティング](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_oracle_driver/)
[Power BI の既知の問題や障害に関する公開情報について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_knownissue/)
[セマンティック モデル更新遅延のトラブル シューティング](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_reflesh_delay/)
[トラブル発生時の事象調査における情報採集](https://jpbap-sqlbi.github.io/blog/powerbi/all_howto_trace_NewVer/)
[トラブル発生時の事象調査に必要な情報の採取手順について(通信編)](https://jpbap-sqlbi.github.io/blog/powerbi/all_howto_trace/)
[フクロウエラーについて](https://jpbap-sqlbi.github.io/blog/powerbi/owl_error/)

## ライセンス
[Power BI ライセンスに関するよくある質問(FAQ)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license_faq/)
[Power BI ライセンスの導入：利用目的による組み合わせ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license2/)
[Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded・Fabric）](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license/)
[セルフサービス サインアップの無効化](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_self-service-signup/)
[Power BI 試用版（無料体験）を無効化する方法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_disable_trial_version/)
[**NEW! 1月** ライセンスとワークスペースの運用・棚卸方法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_tanaoroshi/)

## 増分更新
[Power BI でフォルダー・SharePointフォルダーコネクタを使用した増分更新](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_folder_incremental_refresh/)
[増分更新の概要と設定方法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_incremental_refresh/)

## 機能紹介
[Microsoft Fabric パブリック プレビュー](https://jpbap-sqlbi.github.io/blog/powerbi/microsoft_fabric/)
[Power BI Desktop とPower BI サービスの違い：Power BIでレポート作成・分析を行うために必要なものは？](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_desktop_service/)
[Microsoft Fabric の OneLake について](https://jpbap-sqlbi.github.io/blog/powerbi/fabric_onelake/)
[Power BI と Power Automate の連携](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_power%20automate/)
[Power BI Embedded とは？ライセンスと埋め込み方法](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_embedded_license/)
[Power BI アプリの紹介](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_app_introduction/)
[Power BI サービスのデータセット更新手順について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_refresh_settings/)
[Power BI データフローとデータセット及びデータマートの紹介と比較](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_dataflow_dataset/)
[Power BI とData Activator のデータアラート機能の比較](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_data_activator_alert/)
[Power BI のダッシュボードについて](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_service_dashboard/)
[Power BI の行レベルのセキュリティー (RLS)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_rls/)
[Power BI ビジネスユーザー向けの使い方紹介](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_enduser_usage/)
[Power BI レポートの埋め込み方法の種類について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_embed/)
[エクスポート可能なファイルの種類について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_export/)
[ページ分割されたレポート①](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_paginated_report_1/)
[ページ分割されたレポート② パラメーターを利用したレポートページ分割されたレポート①](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_paginated_report_parameter/)
[Power BI 新規機能のご紹介（2024年5月～ 7月）](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_New_Features_Introduction/)
[ビジュアル計算](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_visual_calculation/)
[**NEW! 1月** Power BI モバイル アプリについて](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_mibile_app/)
[**NEW! 2月** 閲覧者がセマンティックモデルを更新する方法について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_viewer_refresh/)

## Premium 機能
[Power BI Premium Gen2 について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_premium_gen2_roadmap/)
[Power BI 用 Copilot を利用する](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_copilot_for_PBI/)
[Premium / Fabric 容量のスロットリングについて](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_throttling/)
[XMLAエンドポイント](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_xmlaendpoint/)
[Premium容量からFabric容量への移行](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_premium_to_fabric/)
[Power BI ユーザーから見た Microsoft Fabric について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_fabric_component/)
[**NEW! 2月** デプロイパイプラインについて](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_deployment_pipelines/)

## 通信設定
[Power BI で ExpressRoute の使用について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_expressroute/)
[Power BI の通信設定](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_pbiservice_network/)

## Report Server
[Apache Log4j の脆弱性とPower BI, Power BI Report Server への影響について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_log4j_impact/)
[Power BI Report Server とは](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_pbirs/)

## サポート関連
[Power BI のお問い合わせについて](https://jpbap-sqlbi.github.io/blog/powerbi/support_boundary/)
[Power BI サポートチームへのお問い合わせ時に気をつけるポイント](https://jpbap-sqlbi.github.io/blog/powerbi/creating_sr/)
[Power BI の開発支援・コンサルティングを含む内容に関するお問い合わせについて](https://jpbap-sqlbi.github.io/blog/powerbi/support_boundary2/)
[Power BI Report Server のサポートについて](https://jpbap-sqlbi.github.io/blog/powerbi/pbirs_support_boundary/)
[「Power BI Windows アプリ」のサポート終了](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_windows_app_reach_retirement/)
[TLS1.0/1.1のサポート終了](https://jpbap-sqlbi.github.io/blog/powerbi/tls/)

## その他
[Power BI を学習するために役に立つコンテンツのご紹介](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_useful_learning_link/)
[Power BI のアップデート情報について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_feature_roadmap/)
[Power BI CSS Blog でよく閲覧されているページランキング](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blog_reflection2022/)
[Microsoft Teams の Power BI アプリの自動インストール機能について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_teams_auto-installation/)
[Power BI サービスのデザイン変更について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_service_ui_change/)
[Power BI ワークスペースについて \~クラシックワークスペースと新しい(アプリ)ワークスペース\~](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_workspace_classic_and_app/)
[従来の Power BI アプリ (プレオーディエンス) 廃止について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_retirement_of_legacy_apps/)
[Teams アクティビティ分析レポートの廃止について（MC907531）](https://refactored-guacamole-p99p6r945j436q5-4000.app.github.dev/blog/powerbi/pbi_teams_activity_analytics_report_deprecation/)
[【2022年4月27日より】クラシックワークスペースの自動アップグレード](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_workspace_v1upgrade/)
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)