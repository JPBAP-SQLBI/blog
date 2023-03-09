---
title: セルフサービス サインアップの無効化
date: 2022-12-29 00:00:00 
tags:
  - Power BI　　
  - ライセンス
  - Power BI Free
  - セルフサービス サインアップ
---

こんにちは、Power BI サポート チームの山崎です。

Power BI にはいくつかのライセンスがあることを、こちらのブログ「 [Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license/) 」でご紹介させていただきました。

無償版の Power BI Free ライセンスについては、組織において無制限でライセンスを取得しご利用いただけますが、ライセンス管理者様が割り当てを行わずとも、ユーザー自身でライセンスの利用を開始すること (セルフサービス サインアップ) が可能です。

今回は、管理者が組織内のユーザーに対して、”ユーザー自身で Power BI Free ライセンスの利用を開始できるようにするかどうかを制御する方法” についてご案内いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## ユーザー自身が Power BI Free ライセンスの利用開始することを制御したいのはどんな時？
---

Power BI 管理者様や IT 管理者様、これから Power BI 導入のプロジェクトを進められるご担当者様などから、「ユーザーが勝手に Power BI Freeライセンスの利用を開始することを制御したい」とご要望をいただくことがたくさんあります。
組織によって背景は様々ですが、多くのお問合せは以下のような場合の時にいただきます。
このようなシナリオに該当する場合は、”セルフサービス サインアップ” 機能を無効にすることをご検討ください。

- ライセンス割り当ては管理者側で完全に制御したい
- Power BI を組織内で徐々に展開していることを検討しているため、知らないうちにユーザーが勝手に利用することを防ぎたい
- 有償ライセンスのみを利用することを検討しているため、Power BI Free を利用させたくない

</br>

---
## セルフサービス サインアップとは？
---

セルフサービス サインアップとは、管理者側が各ユーザーへのライセンス割り当てをしなくてもユーザー側のサインアップ作業によってライセンスの取得およびサービスの利用開始が可能となる機能です。

本機能を無効化することで、ユーザーが勝手に Power BI Free ライセンスを利用開始することを制御できます。

</br>

> [!WARNING]
> 無効化の設定は他のセルフサービス プログラムと一括で管理されているため、例えば Power Apps のセルフサービス サインアップなども無効化されます。
> サービスごとに制御する方法はご用意がないことを、ご注意くださいますようお願いいたします。

</br>

> **参考情報**
> セルフ サービスサインアップが有効なプログラムの一覧はこちらでご案内しております。
> [セルフサービスでのサインアップと購入を有効または無効にする - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/microsoft-365/admin/misc/self-service-sign-up?view=o365-worldwide)   

---
## セルフサービス サインアップの無効化手順
---

セルフサービス サインアップ無効化手順は以下公開情報にてご案内しておりますが、一連の設定手順を詳細におまとめいたしました。

</br>

> **参考情報**
> [組織でのセルフサービス サインアップの使用 - Microsoft 365 admin | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-disable-self-service#use-powershell-azure-ad-and-microsoft-365-to-enable-and-disable-self-service)

</br>

#### ＜手順＞

管理者として Windows Power Shell を起動し、以下項番１から順番にコマンドを実行します。


1. 資格情報の入力
```ps
$credential = Get-Credential
```
認証画面が表示されたら、 Office 365 管理者 ID と Pass を入力します。

2. $credential 値の確認
```ps
$credential
```

3. MsOnline モジュールの取得
```ps
Install-Module MsOnline
```
ご環境によってはエラーとなる場合があります。その際は、“Import-Module MsOnline” をお試しください。

4. Azure Active Directory への接続
```ps
Connect-MsolService -Credential $credential
```

5. Azure Active Directory 内のドメイン取得
```ps
Get-MsolDomain
```
アクセス先ドメインを確認します。

6. 各テナント情報の取得
```ps
Get-MsolCompanyInformation | fl allow*

AllowAdHocSubscriptions : True
AllowEmailVerifiedUsers : True
```
Office 365 内の設定にてすでにブロックされているか確認します。
この時点で両方の値が False の場合、以降の 項番７を実施する必要はありません。
既にセルフサービス サインアップの機能は無効になっています。

7. 上記機能が True の場合、下記のコマンドにて各機能を無効に設定します。
```ps
Set-MsolCompanySettings -AllowEmailVerifiedUsers $false
Set-MsolCompanySettings -AllowAdHocSubscriptions $false
```
※各機能はそれぞれ以下のような意味を持ちます。
新規ユーザーに対してテナントの自動参加の可否を決める機能: **-AllowEmailVerifiedUsers**
既存ユーザーに対してライセンスの自動配布の可否を決める機能: **-AllowAdHocSubscriptions**

8. 設定後、再度項番６のコマンドを実行して、設定が更新されていることを確認します。

**実行結果例：**
<div align="center">
<img src="1.png">
</div>
</br>

上記設定後、Power BI のライセンスをもたないユーザーが Power BI（app.powerbi.com）にサインインしようとしても、以下画面の通りセルフサービス サインアップができなくなります。

<div align="center">
<img src="2.png">
</div>
</br>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)