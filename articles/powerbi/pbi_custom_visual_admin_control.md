---
title: Power BI でカスタム ビジュアルの利用を制御する方法
date: 2026-06-03 00:00:00
tags:
  - Power BI
  - Power BI Service
  - Power BI Desktop
  - Admin
  - Custom Visuals
  - カスタム ビジュアル
  - 組織の視覚化
---

こんにちは、Power BI サポート チームの亀田です。

Power BI では、標準で用意されているビジュアルに加えて、AppSource から取得したビジュアルや、組織で独自に開発したカスタム ビジュアルを利用できます。一方で、組織のセキュリティ ポリシーやガバナンスの観点から、利用できるビジュアルを制御したいというお問い合わせをいただくことがあります。

本記事では、Power BI Service と Power BI Desktop でカスタム ビジュアルの利用を制御する方法、および管理ポータルの [組織の視覚化] から、特定のカスタム ビジュアルを組織内のユーザーに利用可能にする方法についてご紹介します。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 目次

* [Power BI ビジュアルの種類](#Power-BI-ビジュアルの種類)
* [Power BI Service でカスタム ビジュアルを制御する](#Power-BI-Service-でカスタム-ビジュアルを制御する)
  * [AppSource またはファイルからのビジュアルを制御する](#AppSource-またはファイルからのビジュアルを制御する)
  * [認定済み Power BI ビジュアルのみを許可する](#認定済み-Power-BI-ビジュアルのみを許可する)
  * [カスタム ビジュアルからのデータ ダウンロードを制御する](#カスタム-ビジュアルからのデータ-ダウンロードを制御する)
  * [AppSource カスタム ビジュアル SSO](#AppSource-カスタム-ビジュアル-SSO)
  * [ローカル ストレージ](#ローカル-ストレージ)
* [Power BI Desktop でカスタム ビジュアルを制御する](#Power-BI-Desktop-でカスタム-ビジュアルを制御する)
* [管理ポータルの [組織の視覚化] で特定のビジュアルを利用可能にする](#管理ポータルの-組織の視覚化-で特定のビジュアルを利用可能にする)
  * [ファイルからビジュアルを追加する](#ファイルからビジュアルを追加する)
  * [AppSource からビジュアルを追加する](#AppSource-からビジュアルを追加する)
  * [[視覚化] ペインに自動表示する](#視覚化-ペインに自動表示する)
* [管理者向けの構成例](#管理者向けの構成例)
* [注意事項](#注意事項)
* [おわりに](#おわりに)

## Power BI ビジュアルの種類

Power BI のビジュアルは、大きくコア ビジュアルとカスタム ビジュアルの 2 つに分けられます。

| 種類 | 概要 | 管理上のポイント |
| --- | --- | --- |
| コア ビジュアル | Power BI Desktop および Power BI Service の [視覚化] ペインに標準で用意されているビジュアル | Power BI が標準で提供するビジュアルであり、本記事で説明するカスタム ビジュアルの制御対象には含まれません。 |
| カスタム ビジュアル | AppSource から取得する Power BI ビジュアル、Power BI SDK で作成された .pbiviz ファイル、管理者が [組織の視覚化] から配布する組織のビジュアルなど | テナント設定、Power BI Desktop のグループ ポリシー、[組織の視覚化] により利用範囲を制御します。 |

本記事で扱う「カスタム ビジュアル」は、標準のコア ビジュアル以外のビジュアルを指します。具体的には、AppSource から取得するビジュアル、.pbiviz ファイルとして提供されるビジュアル、管理者が組織向けに配布する組織のビジュアルなどが含まれます。

カスタム ビジュアルは、標準ビジュアルでは表現しにくい要件を実現できる一方で、外部サービスへの通信、データの送信、独自コードの実行などを伴う場合があります。そのため、組織で Power BI を利用する場合は、どの経路から取得したカスタム ビジュアルを許可するかを整理しておくことが重要です。

> [!NOTE]
> 参考# [Power BI のカスタム ビジュアルとは何であり、それらをどこで取得できるのか - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/visuals/power-bi-custom-visuals)

## Power BI Service でカスタム ビジュアルを制御する

Power BI Service でカスタム ビジュアルの利用を制御する場合は、Fabric 管理ポータルのテナント設定を使用します。管理ポータルには、管理者アカウントで Microsoft Fabric または Power BI Service にサインインし、画面右上の [設定] から [管理ポータル] を選択してアクセスします。

<div align="center">
<img src="pbi_custom_visual_admin_control-001.png">
</div>

管理ポータルを開いたら、[テナント設定] から [Power BI の視覚エフェクト] まで移動します。このセクションでは、組織内のユーザーが Power BI ビジュアルに対して実行できる操作を制御できます。

<div align="center">
<img src="pbi_custom_visual_admin_control-002.png">
</div>

### AppSource またはファイルからのビジュアルを制御する

ユーザーが AppSource からビジュアルを追加したり、.pbiviz ファイルをアップロードしたりする操作は、[Power BI SDK を使用して作成された視覚エフェクトの許可] で制御します。

この設定を有効化すると、指定したユーザーまたはセキュリティ グループが、AppSource のビジュアルや .pbiviz ファイルをレポートやダッシュボードに追加できます。組織全体に許可することも、特定のセキュリティ グループに限定することも可能です。

一方で、この設定は [組織の視覚化] のビジュアルには影響しません。ここでいう [組織の視覚化] は、ユーザーが [その他のビジュアルの取得] を開いた際の [組織の視覚化] タブに表示される領域です。

<div align="center">
<img src="pbi_custom_visual_admin_control-003.png">
</div>

つまり、一般ユーザーによる任意の AppSource ビジュアルや .pbiviz ファイルの追加を抑止しつつ、管理者が承認したビジュアルだけを [組織の視覚化] から配布する、という構成が可能です。

> [!NOTE]
> 参考# [Power BI ビジュアルの管理設定を管理する (AppSource またはファイルからのビジュアル) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#visuals-from-appsource-or-a-file)

### 認定済み Power BI ビジュアルのみを許可する

[認定済みのビジュアルのみの追加と使用] を有効化すると、組織のレポートやダッシュボードでは認定済み Power BI ビジュアルのみが表示されます。認定済みのビジュアルには、”Power BI 認定” のアイコンが表示されています。認定されていない AppSource のビジュアルやファイルから追加されたビジュアルは、インポートしようとするとエラーとなります。

<div align="center">
<img src="pbi_custom_visual_admin_control-004.png">
</div>

認定済み Power BI ビジュアルは、Microsoft Power BI チームのコード要件とテストを満たしたビジュアルです。テストでは、ビジュアルが外部サービスまたは外部リソースにアクセスしていないことが確認されます。ただし、Microsoft 以外が作成したビジュアルの動作や機能の詳細については、必要に応じてビジュアルの提供元にも確認してください。

なお、この設定も [組織のストア] のビジュアルには適用されません。組織として利用を許可したい未認定ビジュアルがある場合は、管理者が内容を確認したうえで [組織の視覚化] から配布する方法を検討します。

> [!NOTE]
> 参考# [Power BI ビジュアルの管理設定を管理する (認定済み Power BI ビジュアル) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#certified-power-bi-visuals)
> 参考# [認定済み Power BI ビジュアルを取得する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/visuals/power-bi-custom-visuals-certified)
> 参考# [認定済み Power BI ビジュアル - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/visuals/power-bi-custom-visuals-certified)

### カスタム ビジュアルからのデータ ダウンロードを制御する

カスタム ビジュアルによっては、ビジュアル上のデータをファイルとしてダウンロードする機能を持つ場合があります。この操作は、[カスタム ビジュアルからのダウンロードを許可する] で制御します。

この設定は、組織のエクスポートと共有のテナント設定で制御されるダウンロード制限とは別の設定です。また、組織のストアで管理されるビジュアルを含む、すべてのビジュアルに適用されます。

> [!NOTE]
> 参考# [Power BI ビジュアルの管理設定を管理する (データをファイルにエクスポートする) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#export-data-to-file)

### AppSource カスタム ビジュアル SSO

AppSource のカスタム ビジュアルでは、機能によって Microsoft Entra ID のアクセス トークンを使用する場合があります。この操作は、[AppSource カスタム ビジュアル SSO] の設定で制御します。

この設定を有効化すると、AppSource のカスタム ビジュアルは、サインインしているユーザーに対して対象が制限された Microsoft Entra ID のアクセス トークンを取得できます。アクセス トークンにはユーザー名やメール アドレスなどの情報が含まれる場合があります。対象のビジュアルがどのような情報を扱うか、どの外部サービスと連携するかを確認したうえで、必要なユーザーまたはセキュリティ グループに限定して有効化することを推奨します。

> [!NOTE]
> 参考# [Power BI ビジュアルの管理設定を管理する (AppSource カスタム ビジュアル SSO) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#appsource-custom-visuals-sso)

### ローカル ストレージ

カスタム ビジュアルでは、パフォーマンス向上などを目的として、ブラウザーのローカル ストレージにデータを保存する場合があります。この操作は、[ブラウザーのローカル ストレージへのアクセスを許可する] の設定で制御します。

この設定は、組織のストアで管理されるビジュアルを含む、すべてのビジュアルに適用されます。ローカル ストレージの利用を許可する場合は、ビジュアルが保存するデータの内容や、組織のデータ保持ポリシーに抵触しないかを確認してください。

> [!NOTE]
> 参考# [Power BI ビジュアルの管理設定を管理する (ローカル ストレージ) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#local-storage)

## Power BI Desktop でカスタム ビジュアルを制御する

Power BI Service の管理ポータルで変更するテナント設定の UI は、基本的に Power BI Service に対して適用されます。Power BI Desktop で同様の制御を行うには、AD グループ ポリシーを使用します。

管理対象端末に対して、以下のポリシー値を `Software\Policies\Microsoft\Power BI Desktop\` 配下に構成します。

| 制御内容 | ポリシー値 | 値 |
| --- | --- | --- |
| AppSource や .pbiviz ファイルのカスタム ビジュアルを有効化する | `EnableCustomVisuals` | `0` = 無効、`1` = 有効 |
| 未認定ビジュアルを有効化する | `EnableUncertifiedVisuals` | `0` = 無効、`1` = 有効 |
| カスタム ビジュアルからデータをファイルにエクスポートする | `AllowCVToExportDataToFile` | `0` = 無効、`1` = 有効 |

たとえば、Power BI Desktop でも AppSource や .pbiviz ファイルからの任意のカスタム ビジュアル追加を抑止したい場合は、`EnableCustomVisuals` を `0` に設定します。また、認定済みビジュアルのみを利用させたい場合は、`EnableUncertifiedVisuals` を `0` に設定します。

Power BI Desktop は各ユーザーの端末で動作するため、Power BI Service 側のテナント設定だけでは、Desktop 上でのビジュアル追加操作を完全には制御できません。Power BI Service と Power BI Desktop の両方を運用対象とする場合は、管理ポータルのテナント設定と AD グループ ポリシーをあわせて構成してください。

> [!NOTE]
> 参考# [Power BI ビジュアルの管理設定を管理する (AppSource またはファイルからのビジュアル) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#visuals-from-appsource-or-a-file)
> 参考# [Power BI ビジュアルの管理設定を管理する (認定済み Power BI ビジュアル) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#certified-power-bi-visuals)
> 参考# [Power BI ビジュアルの管理設定を管理する (データをファイルにエクスポートする) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#export-data-to-file)

## 管理ポータルの [組織の視覚化] で特定のビジュアルを利用可能にする

特定のカスタム ビジュアルだけを組織内のユーザーに利用させたい場合は、管理ポータルの [組織の視覚化] を使用します。公開ドキュメントでは [組織のビジュアル] と表記される場合がありますが、いずれも管理者が組織向けの Power BI ビジュアルを追加、削除、管理する機能を指します。

[組織の視覚化] では、以下のような操作が可能です。

* .pbiviz ファイルからビジュアルを追加する
* AppSource からビジュアルを追加する
* 組織内のユーザーの [視覚化] ペインに自動表示する
* ビジュアルを無効化する
* ビジュアルを更新する
* ファイルから追加したビジュアルを削除する

<div align="center">
<img src="pbi_custom_visual_admin_control-005.png">
</div>

なお、[組織の視覚化] には、認定されていないビジュアルや .pbiviz ファイルのビジュアルも追加できます。これは管理者が明示的に承認したビジュアルを配布するための仕組みとして利用できますが、追加前にはビジュアルの作成者、入手元、通信先、更新方法、サポート体制を確認してください。

### ファイルからビジュアルを追加する

組織で独自に開発したビジュアルや、提供元から .pbiviz ファイルとして受領したビジュアルを配布する場合は、[ビジュアルの追加] > [ファイルから] を選択します。アップロード時には、.pbiviz ファイル、ビジュアル名、アイコン、説明、アクセス可否を設定します。

> [!WARNING]
> ファイルからアップロードされた Power BI ビジュアルには、セキュリティやプライバシー上のリスクがあるコードが含まれている場合があります。組織のリポジトリに展開する前に、ビジュアルの作成者と提供元が信頼できることを確認してください。

<div align="center">
<img src="pbi_custom_visual_admin_control-006.png">
</div>

<div align="center">
<img src="pbi_custom_visual_admin_control-007.png">
</div>

> [!NOTE]
> 参考# [Power BI ビジュアルの管理設定を管理する (ファイルからビジュアルを追加する) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#add-a-visual-from-a-file)

### AppSource からビジュアルを追加する

AppSource に公開されているビジュアルを組織として利用可能にする場合は、[ビジュアルの追加] > [AppSource から] を選択します。表示された Power BI ビジュアルの一覧から対象のビジュアルを選択し、[追加] を実行します。

AppSource から追加したビジュアルは自動的に更新されます。そのため、組織内のユーザーは常に最新バージョンのビジュアルを使用できますが、更新による挙動変更が懸念される場合は、事前検証用の運用プロセスを用意しておくことを推奨します。

<div align="center">
<img src="pbi_custom_visual_admin_control-008.png">
</div>

<div align="center">
<img src="pbi_custom_visual_admin_control-009.png">
</div>

> [!NOTE]
> 参考# [Power BI ビジュアルの管理設定を管理する (AppSource から視覚エフェクトを追加する) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#add-a-visual-from-appsource)

### [視覚化] ペインに自動表示する

[組織の視覚化] に追加したビジュアルは、ユーザーが [その他のビジュアルの取得] から [自分の組織] タブを開いて取得できます。さらに、管理者が対象のビジュアルを選択して [視覚化ウィンドウを有効にする] を実行すると、組織内のユーザーの [視覚化] ペインに自動的に表示されます。

よく利用する社内標準ビジュアルや、組織として利用を推奨するビジュアルは、[視覚化] ペインに表示させておくことで、レポート作成者が迷わず利用できます。

<div align="center">
<img src="pbi_custom_visual_admin_control-010.png">
</div>

[組織の視覚化] の設定は Power BI Desktop にも自動的に展開されます。そのため、Power BI Service だけではなく、Power BI Desktop でレポートを作成するユーザーに対しても、管理者が承認したビジュアルを見つけやすくすることができます。

> [!NOTE]
> 参考# [Power BI ビジュアルの管理設定を管理する ([視覚化] ペインに視覚エフェクトを追加する) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/organizational-visuals#add-a-visual-to-the-visualization-pane)
> 参考# [Power BI 組織のビジュアル - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/visuals/power-bi-custom-visuals-organization)

## 管理者向けの構成例

ユーザーが任意のカスタム ビジュアルを追加する経路を抑制しつつ、管理者が承認したビジュアルのみを組織内で利用させるためには、以下のような構成が考えられます。

1. Power BI Service では、[Power BI SDK を使用して作成された視覚エフェクトの許可] を必要なユーザーまたは管理者グループに限定します。
2. Power BI Desktop では AD グループ ポリシーで `EnableCustomVisuals` を `0` に設定し、任意のカスタム ビジュアル追加を抑止します。
3. 組織として利用を許可するビジュアルは、管理者が事前に確認したうえで [組織の視覚化] に追加します。
4. 必要に応じて、[視覚化ウィンドウの有効化] により、ユーザーの [視覚化] ペインへ自動表示します。
5. カスタム ビジュアルからのデータ ダウンロード、SSO、ローカル ストレージは、ビジュアルの機能要件とセキュリティ要件を確認したうえで、必要な範囲に限定して有効化します。

また、認定済みビジュアルは広く許可し、未認定ビジュアルは個別承認したい場合は、認定済みビジュアルのみを利用できるように構成したうえで、例外的に利用を許可するビジュアルを [組織の視覚化] に追加する方法も考えられます。

## 注意事項

これまで説明したカスタム ビジュアルの管理について、運用上は以下の点にご注意ください。

* Power BI Desktop でテナント設定と同等の制御を行うには、AD グループ ポリシーの構成が必要です。
* [組織の視覚化] の設定は Power BI Desktop に自動的に展開されます。
* 組織のビジュアルは、PowerPoint へのエクスポートやレポート ページのサブスクライブ時に送信されるメール内で表示できない場合があります。
* ファイルから追加したビジュアルを削除すると、削除されたビジュアルを使用している既存レポートで当該ビジュアルがエラーになります。削除は元に戻せないため、一時的に利用を止めたい場合は無効化を検討します。
* AppSource から追加したビジュアルは自動更新されます。

> [!NOTE]
> 参考# [Power BI 組織のビジュアル - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/visuals/power-bi-custom-visuals-organization#considerations-and-limitations)

## おわりに

今回は、Power BI でカスタム ビジュアルの利用を制御する方法について紹介しました。Power BI Service では管理ポータルのテナント設定、Power BI Desktop では AD グループ ポリシーを使用することで、AppSource や .pbiviz ファイルからのカスタム ビジュアル利用を制御できます。

また、組織として利用を許可するビジュアルは、[組織の視覚化] に追加することで、管理者が承認したビジュアルとしてユーザーに展開できます。カスタム ビジュアルは表現力を高める有用な機能ですが、組織のセキュリティ要件に合わせて、利用経路と許可範囲を設計していただければと思います。

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。
