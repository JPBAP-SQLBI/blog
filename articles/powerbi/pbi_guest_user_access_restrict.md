---
title: Microsoft Entra ID の外部コラボレーションの設定が与える影響について
date: 2023-04-30 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Power BI Service
  - ゲストユーザー
  - external user
  - アクセス許可
  - 管理者
  - Admin
---

こんにちは、Power BI サポート チームの山本です。
ゲスト ユーザーに関する Power BI の動作については、以前私たちのブログ記事 [組織外のユーザーに対する Power BI コンテンツの共有](https://jpbap-sqlbi.github.io/blog/powerbi/aad_guestuser/) でご紹介させていただきました。

ゲスト ユーザーを招待する側のテナントの管理者様によっては「Power BI のコンテンツはアクセスさせてもよいが、テナント内のユーザー情報が見えてしまうのは避けたい」というようなご意見をいただくことがあります。
上記動作は Microsoft Entra ID (旧 Azure Active Directory、以下 Entra ID) に存在する外部コラボレーションの設定 (ゲストユーザーのアクセス許可に関する設定) で変更することが可能です。
今回は、外部コラボレーションの設定とは何か、また設定がどのように影響するか、各設定値による動作を検証ベースで確認した内容をご紹介いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に検証を踏まえた結果として構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 更新履歴
---
Update: 2024/07/03
Microsoft Fabric 一般提供に伴い、テナント設定の表記が変わったため、内容を一部修正しました。
[エクスポートと共有のテナント設定](https://learn.microsoft.com/ja-jp/fabric/admin/service-admin-portal-export-sharing)

---
## 目次
---
- [目次](#目次)
- [外部コラボレーションの設定とは](#外部コラボレーションの設定とは)
- [どのように影響するか](#どのように影響するか)
  - [前提](#前提)
  - [制限が最も少ない](#制限が最も少ない)
  - [制限付きアクセス (既定) / 最も制限が多い](#制限付きアクセス-既定--最も制限が多い)
- [どのように設定しておくべきか](#どのように設定しておくべきか)

---
## 外部コラボレーションの設定とは
---

Microsoft Entra ID (旧 Azure Active Directory、以下 Entra ID)  には、テナントに招待したゲスト ユーザーに対して、組織内のユーザーとグループ メンバーシップの表示を制限する設定があります。

> [!TIP]
> 遷移方法：
> Microsoft Entra ID の管理メニュー [ユーザーのプロパティ] をクリックし、[外部コラボレーションの設定を管理します] の文字をクリックすると、設定画面が表示されます。

この設定には、以下３つのアクセス レベルがあります。

| アクセス許可レベル | アクセス レベル |
| - | - |
| 制限が最も少ない | ゲスト ユーザーは、メンバーと同じアクセス権を持ちます |
| 制限付きアクセス (既定) | ゲスト ユーザーは、ディレクトリ オブジェクトのプロパティとメンバーシップへのアクセスが制限されます |
| 最も制限が多い | ゲスト ユーザーのアクセスは、各自のディレクトリ オブジェクトのプロパティとメンバーシップに制限されます |

<div align="center">
<img src="1.png">
</div>


既定値は「制限付きアクセス」レベルとなっており、特定のオブジェクト ID を元に照会することはできるものの、ユーザー一覧が確認できなかったり、グループが確認できない状態です。
さらに制限の強い「最も制限が多い」レベルでは、ゲスト ユーザー自身のプロパティ情報のみが確認できる状態となります。
一方「制限が最も少ない」レベルでは、管理者ではないメンバー ユーザーと同じアクセス権で組織内のユーザーとグループ メンバーシップの表示を行なうことができるようになります。

より詳細な動作については、弊社 Azure ID サポートチームのブログ記事「[外部コラボレーションの設定 (ゲスト ユーザーのアクセス制限) について](https://jpazureid.github.io/blog/azure-active-directory/external-collaboration-setting-b2b-access/)」にて紹介されておりますので、こちらも合わせてご確認ください。


> [!TIP]
> ゲスト ユーザー アクセスを構成するには、全体管理者ロールである必要があります。 
> またゲスト アクセスを制限するための追加のライセンス要件はありません。
> 
> [Microsoft Entra ID でゲスト アクセス許可を制限する](https://learn.microsoft.com/ja-jp/entra/identity/users/users-restrict-guest-permissions#update-in-the-azure-portal)

</br>

---
## どのように影響するか
---

各アクセス レベルは、Power BI サービスでテナント ディレクトリのユーザーやグループを参照する機能で影響を受けることになります。
ユーザーやグループを参照する具体的な機能は以下です。

- [コメント機能](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-comment)
- [共有リンク機能](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-share-dashboards#share-a-report-via-link)
- [直接アクセス許可の追加](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-share-dashboards#manage-permissions-to-a-report)
- [ワークスペース アクセスの追加](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-give-access-new-workspaces)


上記機能においてアクセス レベルを変更した場合、結論として以下のような動作となります。

| アクセス許可レベル | Power BI でのゲストユーザーの動作 |
| - | - |
| 制限が最も少ない | ゲストユーザーはテナント内のユーザーやグループの候補検索やメールアドレスの指定が可能 |
| 制限付きアクセス (既定) ／ </br>最も制限が多い | ゲストユーザーはテナント内のユーザーやグループの候補検索やメールアドレスの指定が不可 |

> [!TIP]
> ゲストユーザーに Power BI 管理者の役割が割り当てられている場合、全てのリソースの基本プロパティを読み取るアクセス許可が付与されるため、本機能の制限は受けません。
> 
> 参考: [Azure AD の組み込みロール - Power BI 管理者](https://learn.microsoft.com/ja-JP/azure/active-directory/roles/permissions-reference?WT.mc_id=365AdminCSH#power-bi-administrator)


</br>

### 前提

今回、テストシナリオとして、テナント B のユーザー「Adele」が、テナント A のゲスト ユーザーとして、Power BI ワークスペース「Guest Share」のビューアーロールとしてアクセス権を持っているものとします。

<div align="center">
<img src="6.png">
</div>

またワークスペース「Guest Share」には「Guest Share Report」があり、Adele には再共有のアクセスが付与されています。

<div align="center">
<img src="7.png">
</div>

さらにゲスト ユーザーに関するテナント設定「ゲスト ユーザーが Microsoft Fabric へのアクセスが可能」「ユーザーはゲスト ユーザーを招待して、項目の共有とアクセス許可を通じて共同作業できます」「ゲスト ユーザーは Fabric コンテンツを閲覧およびアクセスできます」は有効化されている状態とします。
候補リストにゲスト ユーザーが表示される「ユーザーは、提案されているユーザーの一覧でゲスト ユーザーを確認できます」も有効化されています。

<div align="center">
<img src="8.png">
</div>

</br>

### 制限が最も少ない

制限が最も少ないアクセス レベルでは、テナントのユーザーやグループの候補検索が制限なく可能になります。
またテナント設定「ユーザーは、提案されているユーザーの一覧でゲスト ユーザーを確認できます」が有効化されている場合、テナント A に属する自身以外のゲスト ユーザーも候補検索が可能です。
（レポートやダッシュボードのコメント機能についてはゲスト ユーザーへのメンション機能はありません）

//リンク共有
<div align="center">
<img src="9.png" width=40%>
</div>

</br>

//コメント機能でのメンション
<div align="center">
<img src="11.png" width=40%>
</div>

</br>


### 制限付きアクセス (既定) / 最も制限が多い

制限付きアクセス (既定) や最も制限が多いアクセス レベルでは、候補検索もできず、メールアドレスでの一致指定もできません。
Power BI に影響する部分としては両設定に違いはありません。

//リンク共有
<div align="center">
<img src="10.png" width=40%>
</div>

</br>

//コメント機能でのメンション
<div align="center">
<img src="2.png" width=40%>
</div>

</br>


またテナント設定「ユーザーはゲスト ユーザーを招待して、項目の共有とアクセス許可を通じて共同作業できます」を有効化している場合でも、ゲスト ユーザーからの [アドホック招待](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-azure-ad-b2b#ad-hoc-invites) はできなくなります。

<div align="center">
<img src="14.png">
</div>

</br>

---
## どのように設定しておくべきか
---

ゲスト ユーザーに対して Power BI の機能は使わせたいが、組織内のユーザー情報は検索候補に表示させたくない、という場合にはアクセス レベルを「制限付きアクセス (既定)」または「最も制限が多い」に変更しておくことをお勧めいたします。


</br>
</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)