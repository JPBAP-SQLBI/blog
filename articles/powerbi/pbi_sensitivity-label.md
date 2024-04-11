---
title: Power BI Service へのアクセス制御③ 秘密度ラベル
date: 2023-01-31 00:00:00 
tags:
  - Power BI
  - アクセス制御
  - 秘密度ラベル
---

こんにちは、Power BI サポート チームの亀田です。
セキュリティの観点から、Power BI Service へのアクセスを制限したいというお問い合わせをいただくことがあります。「[条件付きアクセス](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_conditional-access/)」、｢[Azure Private Link](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_privatelink/)｣と説明してきましたが、今回は  ｢秘密度ラベル｣ について説明します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---

## 目次

* [秘密度ラベル とは](#秘密度ラベル-とは)
* [秘密度ラベル の設定手順](#秘密度ラベルの設定手順)
  * [1.テナント設定から秘密度ラベルを有効化する](#1-テナント設定から秘密度ラベルを有効化する)
  * [2.秘密度ラベルを適用する](#2-秘密度ラベルを適用する)
  * [3.秘密度ラベルを追加する](#3-秘密度ラベルを追加する)
  * [4.秘密度ラベルに関する設定](#4-秘密度ラベルに関する設定)
* [データ保護メトリック レポート](#データ保護メトリック-レポート)

## 秘密度ラベル とは

Power BI の秘密度ラベルは、データのセキュリティとアクセス制御を管理するための機能です。これにより、特定のデータセットやレポートにアクセスできるユーザーを制限することができます。例えば、特定のレポートファイル (.pbixファイル) に「機密」というラベルを設定し、それに対してアクセス権を持つのは特定のグループのみに限定することができます。秘密度ラベルはPower BI Desktopでご利用いただける機能です。Power BI Serviceでは秘密度ラベルを設定している場合であってもコンテンツへのアクセスには影響しません。Power BI Serviceでのアクセス制御にはワークスペースやレポート単位のアクセス許可を設定する必要があります。

> [!NOTE]
> 参考＃[Power BI での Microsoft Purview Information Protection の秘密度ラベル - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-security-sensitivity-label-overview)  
<div align="center">
<img src="sensitivity12.png">
</div>  

秘密度ラベルはPower BIのコンテンツのみではなく、Power BIからエクスポートしたExcel、Power Point、PDFファイルでも適用されるため、機密データはどこであっても保護することができます。

> [!WARNING]
> 画像ファイルやcsvには秘密度ラベルを適用することができませんのでご注意ください。  
<div align="center">
<img src="sensitivity13.png">
</div>  


## 秘密度ラベルの設定手順

Power BI で秘密度ラベルを利用するためには、以下の設定を行います。

[1.テナント設定から秘密度ラベルを有効化する](#1-テナント設定から秘密度ラベルを有効化する)
[2.秘密度ラベルを適用する](#2-秘密度ラベルを適用する)
[3.秘密度ラベルを追加する](#3-秘密度ラベルを追加する)
[4.秘密度ラベルに関する設定](#4-秘密度ラベルに関する設定)

それぞれの詳細な手順について、以下に説明します。なお、秘密度ラベルの適用には以下のライセンスが必要となります。

* Azure Information Protection Premium P1 または Premium P2 ライセンス
* Power BI Pro または Premium Per Userライセンス
> [!NOTE]
> 参考＃[Power BI で秘密度ラベルを有効にする - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-security-enable-data-sensitivity-labels)

### 1.テナント設定から秘密度ラベルを有効化する

テナントで秘密度ラベルを有効化するには、管理ポータルにアクセスし、 **[テナント設定]** > **[情報の保護]** > **[ユーザーによるコンテンツへの秘密度ラベルの適用を許可]** を有効化します。  
<div align="center">
<img src="sensitivity01.png">
</div>  


### 2.秘密度ラベルを適用する

 **[ユーザーによるコンテンツへの秘密度ラベルの適用を許可]** が有効化されている場合、Power BI Desktop/Service で秘密度ラベルの設定が可能となります。それぞれの設定手順について説明します。

#### Power BI Desktopで秘密度ラベルを適用する

Power BI Desktopを開き、 **[ホーム]** > **[秘密度]** を選択します。  
<div align="center">
<img src="sensitivity02.png">
</div>  

設定可能な秘密度ラベルの一覧が表示されるので、設定したい秘密度ラベルを選択します。  
<div align="center">
<img src="sensitivity03.png">
</div>  

秘密度ラベルが設定されている場合、左下に表示されます。以下の例では、"Highly Confidential\All Employees"が設定されています。  
<div align="center">
<img src="sensitivity04.png">
</div>  


#### Power BI Serviceで秘密度ラベルを適用する

レポート、ダッシュボードに秘密度ラベルを適用する場合、 **[その他のオプション]** `> **[設定]** を選択します。  
<div align="center">
<img src="sensitivity05.png">
</div>  

**[秘密度ラベル]** を選択し、保存します。  
<div align="center">
<img src="sensitivity06.png">
</div>  


データセット、データフローに秘密度ラベルを適用する場合、 **[その他のオプション]** `> **[設定]** を選択します。  
<div align="center">
<img src="sensitivity07.png">
</div>  

**[秘密度ラベル]** を選択し、保存します。  
<div align="center">
<img src="sensitivity08.png">
</div>  


設定されている秘密度ラベルはワークスペースから確認できるほか、  
<div align="center">
<img src="sensitivity09.png">
</div>  

レポートやダッシュボードの上部でも確認することができます。  
<div align="center">
<img src="sensitivity10.png">
</div>  


### 3.秘密度ラベルを追加する

秘密度ラベルは標準で用意されているものもありますが、管理者が設定することも可能です。手順について説明します。なお、設定にはPower BIとは異なるライセンスが必要となりますのでご注意ください。
> [!NOTE]
> 参考# [秘密度ラベルの概要 - Microsoft Purview (compliance) | Microsoft Learn](https://learn.microsoft.com/ja-jp/microsoft-365/compliance/get-started-with-sensitivity-labels?view=o365-worldwide)
> 参考# [秘密度ラベルを使用して暗号化を適用する - Microsoft Purview (compliance) | Microsoft Learn](https://learn.microsoft.com/ja-jp/microsoft-365/compliance/encryption-sensitivity-labels?view=o365-worldwide)



[Microsoft Purview コンプライアンス ポータル](https://aka.ms/dpfwl15)にアクセスし、 **[+ ラベルの作成]** を選択します。  
<div align="center">
<img src="sensitivity11.png">
</div>  

名前、表示名、説明を入力し、 **[次へ]** を選択します。  
<div align="center">
<img src="sensitivity14.png">
</div>  

**[アイテム]** にチェックし、 **[次へ]** を選択します。  
<div align="center">
<img src="sensitivity15.png">
</div>  

**[項目の暗号化]** にチェックし、 **[次へ]** を選択します。  
<div align="center">
<img src="sensitivity16.png">
</div>  

暗号化の設定をします。 **[特定のユーザーとグループにアクセス許可を付与する]** により設定したユーザーまたはグループが、このラベルの設定されたコンテンツを操作することができます。一般的にはユーザーではなくグループを利用をすることで構成が簡単になるため推奨されます。

この際に設定する **[アクセス許可の選択]** は、[使用権限と説明](https://learn.microsoft.com/ja-jp/azure/information-protection/configure-usage-rights#usage-rights-and-descriptions)をご確認ください。

テナント設定と秘密度ラベルでは、制限の厳しいものが適用されます。例えば、テナント設定でデータのエクスポートを有効にしている場合でも、秘密度ラベルでエクスポートが無効になっている場合、ユーザーはエクスポートをすることができません。  
<div align="center">
<img src="sensitivity17.png">
</div>  

**[ファイルとメールの自動ラベル付け]** の設定をしたら、 **[次へ]** を選択します。  
<div align="center">
<img src="sensitivity18.png">
</div>  

**[グループとサイトの保護設定を定義]** の設定をしたら、 **[次へ]** を選択します。  
<div align="center">
<img src="sensitivity19.png">
</div>  

**[スキーマ化されたデータ アセットの自動ラベル付け]** の設定をしたら、 **[次へ]** を選択します。  
<div align="center">
<img src="sensitivity20.png">
</div>  

設定を確認したら、 **[ラベルを作成]** を選択します。  
<div align="center">
<img src="sensitivity21.png">
</div>  

秘密度ラベルが作成されたことを確認し、 **[完了]** を選択します。秘密度ラベルの反映は、すぐに行われず10分~最大24時間ほどかかる場合があります。  
<div align="center">
<img src="sensitivity22.png">
</div>  


### 4.秘密度ラベルに関する設定

管理ポータルから設定できる、秘密度ラベルに関する設定について説明します。

* データ ソースから秘密度ラベルを Power BI のそのデータに適用する(プレビュー)
  データ ソースで秘密度ラベルが設定されている場合、その秘密度ラベルを継承してPower BI データセットに設定することができる機能です。
  > [!NOTE]
  > 参考# [Power BI でのデータ ソースからの秘密度ラベルの継承 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-security-sensitivity-label-inheritance-from-data-sources)  
  <div align="center">
  <img src="sensitivity23.png">
  </div>  

* ダウンストリーム コンテンツに秘密度ラベルを自動的に適用する
  秘密度ラベルが適用されたデータセットから作成される他のデータセット、レポート、ダッシュボードや、秘密度ラベルが適用されたレポートから作成されたダッシュボードに、作成元の秘密度ラベルを適用することができる機能です。
  > [!NOTE]
  > 参考# [Power BI での秘密度ラベルの下流への継承 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-security-sensitivity-label-downstream-inheritance)  
  <div align="center">
  <img src="sensitivity24.png">
  </div>  
  
* ワークスペース管理者が自動的に適用された秘密度ラベルをオーバーライドすることを許可する(プレビュー)
  自動的に秘密度ラベルが適用された場合、コンテンツに対する秘密度ラベル発行者のユーザーがいなくなる場合があり、その場合ラベルの変更や削除ができるユーザーがいなくなることがあります。この設定はそのような状況を回避するための機能であり、ワークスペース管理者が秘密度ラベルをオーバーライドできるようになります。
  > [!NOTE]
  > 参考# [自動ラベル付けのシナリオに対応するための緩和策](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-security-sensitivity-label-change-enforcement#relaxations-to-accommodate-automatic-labeling-scenarios)  
  <div align="center">
  <img src="sensitivity25.png">
  </div>  
  
* 保護されたラベルを持つコンテンツが、組織内の全ユーザーとリンクを介して共有されないように制御する
  この設定が有効な場合、秘密度ラベルに"保護"が設定されているコンテンツに対して組織内のユーザーとの共有リンクが生成できなくなります。
  > [!NOTE]
  > 参考# [保護されたラベルが付けられたコンテンツがリンクを介して組織内のすべてのユーザーと共有されないように制限する](https://learn.microsoft.com/ja-jp/power-bi/admin/service-admin-portal-information-protection#restrict-content-with-protected-labels-from-being-shared-via-link-with-everyone-in-your-organization)  
  <div align="center">
  <img src="sensitivity26.png">
  </div>  


## データ保護メトリック レポート

Power BI管理者は、テナント内で利用されている秘密度ラベルを監視したり追跡することができます。このデータ保護メトリック レポートは、管理ポータル内の **[保護メトリック]** から確認することができます。  
<div align="center">
<img src="sensitivity27.png">
</div>  


秘密度ラベルを設定いただくことで、よりセキュアにPower BIをご利用いただけます。

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)

