---
title: 組織外のユーザーとPower BIコンテンツの共有
date: 2021-09-30 16:00:00
tags:
  - Power BI
  - ゲストユーザー
  - 共有
  - 組織外ユーザー
  - B2B
---

こんにちは、Power BI サポート チームのチャンです。

Power BI ご利用のユーザー様から、「組織外のユーザーはPower BI のレポートを共有できますか？制限する方法はありますか？」などの質問をよく頂いていますが、
本ブログでは、組織外のユーザーを招待し、組織内のゲストユーザーとしてコンテンツを共有する方法、及び権限を制御する方法につきまして、ご紹介いたします。

<!-- more -->

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
1. [組織外のユーザーとは？](#組織外のユーザーとは？)
2. [組織外のユーザーをゲストユーザーとして招待するには](#組織外のユーザーをゲストユーザーとして招待するには)
3. [ゲストユーザーとコンテンツを共有するには](#ゲストユーザーとコンテンツを共有するには)
4. [ゲストユーザーの権限を制御するには](#ゲストユーザーの権限を制御するには)

---
## 組織外のユーザーとは？
---

組織外のユーザー（または外部ユーザー）とは、ご利用のAzure Active Directory（AAD）テナントのドメイン以外のユーザーを指します。
具体的には、メールアドレスの@ マーク後の表記が異なるユーザーです。
gmail.com、outlook.com、hotmail.com などの個人用メールアカウントのユーザーにつきましても、組織外のユーザーと見なします。

組織外のユーザーと、Power BI内のレポートを共有するには、組織外のユーザーをゲストユーザーとして招待する必要があります。

---
## 組織外のユーザーをゲストユーザーとして招待するには
---

ゲストユーザーとして招待するには、計画的招待とアドホック招待という二つの方法があります。

#### ■ 計画的招待

Azure Active Directory（AAD）からゲストユーザーを招待する方法です。

まず、[Azureポータル](https://portal.azure.com/) へアクセスし、Azure Active Directoryを選択します。
次に、Azure Active Directoryで、[ユーザー]>[＋新しいゲストユーザー]の順で選択し、ゲストユーザーのメールアドレスを入力し、招待メールを送信します。

![](./aad_guestuser.png)

招待されたユーザーは、下記画像のようなメールが届きますので、メールに記載されているリンクをクリックし、指示に従いアカウントの有効化を行なってください。

![](./guestuser_mail.png)

> [!TIP]
> Azure Active Directory （AAD）側でゲストユーザーを招待できるユーザーを制限することも可能ですので、その詳細については下記のドキュメントをご参考ください。
> 参考：[B2B 外部コラボレーションを有効にしてゲストを招待できるユーザーを管理する](https://docs.microsoft.com/ja-jp/azure/active-directory/external-identities/delegate-invitations)

#### ■ アドホック招待

レポートやダッシュボードの共有機能、またはアプリ発行のアクセスページで、AADに存在しない組織外のユーザーを招待する方法です。

レポートの直接アクセスから追加する方法には、レポートの[アクセス許可の管理]にアクセスし、
直接アクセスで、[+ユーザーの追加]を行ない、組織外のユーザーのメールアドレスを入力すると、招待メールが対象のユーザーに届きます。

![](./adhoc_invitation.png)

また、招待されたユーザーは、保留のリストで表示されます。

![](./pending.png)

レポートからの招待の場合は、下記のような招待メールが届きますが、リンクからアカウントを作成したら、直接アクセスの一覧に表示されるようになります。

![](./adhoc_invite_mail.png)

> [!TIP]
> 管理ポータルで、テナント設定「組織への外部ユーザーの招待」を無効化することによって、アドホック招待を使用できないように設定することができます。

> **参考情報**
> - [Azure AD B2B で外部ゲスト ユーザーに Power BI コンテンツを配布する](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-azure-ad-b2b)

計画的招待で、ゲストユーザーとして招待されたユーザーは、ワークスペースのアクセス許可、レポートやダッシュボード、アプリのアクセス許可でも追加できるようになります。
また、アドホック招待を通してアカウントを作成したゲストユーザーも、招待元のレポート・ダッシュボード・アプリを閲覧できる上に、計画的招待のゲストユーザーと同様、他のレポートやダッシュボード、アプリのアクセス許可にも追加されることが可能です。

ただし、ゲストユーザーがコンテンツを閲覧するには、以下のライセンス条件が必要です。

- ゲストユーザーにPower BI Pro ライセンスまたはPremium Per User ライセンスの付与
- Premium Per Capacity のワークスペースで、ゲストユーザーにはライセンスなしで閲覧可能
- ゲストユーザーが本来所属しているテナントで、Power BI Pro ライセンスまたはPremium Per User ライセンスを所持している


また、対象のゲストユーザーが、コンテンツを編集・作成・管理できるようになるには、Power BI Pro ライセンスまたはPremium Per User ライセンスを所持する上で、管理ポータルのテナント設定で、「Azure Active Directory のゲスト ユーザーによる組織内のコンテンツの編集および管理を許可する」を有効化しておく必要があります。
こちらのテナント設定は、既定値では、無効となっています。

![](./tenant_setting1.png)

しがしながら、通常のユーザーと異なり、コンテンツを編集・作成・管理できるようになったとしても、ゲストユーザーには一部利用できない機能があります。
詳細につきましては、下記参考情報のドキュメントに記載されている、「考慮事項と制限事項」の内容をご確認ください。

> **参考情報**
> - [Azure AD B2B で外部ゲスト ユーザーに Power BI コンテンツを配布する（考慮事項と制限事項）](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-azure-ad-b2b#considerations-and-limitations)

---
## ゲストユーザーの権限を制御するには
---

管理ポータルのテナント設定で、ゲストユーザーがPower BIサービスのテナントへアクセスできないようにすることや、アドホック招待を無効化にすることができます。

#### ■ Azure Active Directory のゲスト ユーザーによる Power BI へのアクセスを許可する

既定値は有効化されていますが、この設定を無効にすると、Power BI サービスにアクセスしようとしたときに、ゲストユーザーにエラーが表示されます。

![](./tenant_setting2.png)

#### ■ 組織への外部ユーザーの招待

既定値は有効化されていますが、この設定を無効にすると、アドホック招待でレポートやダッシュボード、アプリから組織外のユーザーを招待することができません。
ただし、計画的招待、Azure Active Directoryでゲストユーザーを招待することは引き続き可能です。

![](./tenant_setting3.png)

> [!TIP]
> 計画的招待－Azure Active Directory （AAD）側でゲストユーザーを招待できるユーザーを制限することも可能ですので、その詳細については下記のドキュメントをご参考ください。
> 参考：[B2B 外部コラボレーションを有効にしてゲストを招待できるユーザーを管理する](https://learn.microsoft.com/ja-jp/azure/active-directory/external-identities/external-collaboration-settings-configure)

#### ■ Azure Active Directory のゲスト ユーザーによる組織内のコンテンツの編集および管理を許可する

既定値では無効となっていますが、この設定を有効にすると、適切なライセンスを持つゲストユーザーは、組織内のコンテンツを編集および管理できます。
また、左側のワークスペースの一覧タブも利用できるようになります。

![](./tenant_setting1.png)

> **参考情報**
> - [管理ポータルでの Power BI の管理](https://learn.microsoft.com/ja-jp/power-bi/admin/service-admin-portal#export-and-sharing-settings)

> **本ブログの関連記事**
> - [Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）](../pbi_license/)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)