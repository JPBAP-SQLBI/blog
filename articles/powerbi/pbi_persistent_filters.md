---
title: Power BI サービスにおける固定フィルター
date: 2024-11-30 00:00:00 
tags:
  - Power BI
  - Power BI Service
  - Power BI サービス
  - Persistent Filters
  - 固定フィルター

---


こんにちは、Power BI サポート チームのファムです。

Power BI サービスでレポートを閲覧するとき、「前回と同じフィルター条件をまた設定しないといけない」と感じたことはありませんか。そんなお悩みを解決するのが 「**固定フィルター**」 機能です。この機能を使えば、前回のフィルター条件が自動的に保存され、次回レポートを開いた際にそのまま適用されます。これにより、手間を省き、効率的にレポートを閲覧することが可能になります。一方、他のユーザーに共有する際にスライサーの条件を保持させたくない場合、固定フィルターを無効に設定することで実現可能です。

本ブログでは、固定フィルターにについて詳細にご紹介いたします。

<!-- more -->

</br>

> [!IMPORTANT]
> 弊社サポートをご利用いただいている場合、状況に合わせた調査方針を策定するため、記載の内容とご案内が異なる場合がございます。
> ご不明な点がございましたら弊社サポート担当までお気軽にご質問ください。
> また掲載している画像・手順は投稿時点のものとなります。最新の情報とは異なる可能性がございますので予めご了承ください。

</br>

---
## 目次
---
1. [固定フィルターとは](#1．固定フィルターとは)
2. [固定フィルターの設定方法](#2．固定フィルターの設定方法)
3. [固定フィルターが有効な場合の挙動](#3．固定フィルターが有効な場合の挙動)
4. [固定フィルターが無効な場合の挙動](#4．固定フィルターが無効な場合の挙動)
5. [その他　Teamsでのチャットでリンク共有](#5．その他-Teamsでのチャットでリンク共有)
</br>

---

## 1．固定フィルターとは

固定フィルターは、レポートに適用したフィルターやスライサーなどの変更が自動的に保存されます。これにより、再度レポートを開いたときに前回の状態から続けて作業ができます。固定フィルターは有効となっており、Power BIに発行したレポートの状態に変更が行われたかどうか、「**Reset**」ボタンを見ることで判断することが可能です。

以下のようなイメージの通り、フィルターやスライサーの変更が行われない場合、「**Reset**」ボタンが灰色となっており、クリックできません。こちらは、レポートがPower BIサービスに発行した状態のレポートです。

</br>

<div align="center">
<img src="pic1.png">
</div>


一方、フィルターやスライサーの変更が行われる場合、「**Reset**」ボタンが青色となっており、クリックするとレポートが発行した状態をリセットできます。

<div align="center">
<img src="pic2.png">
</div>

</br>

> **参考情報**
>  [Power BI サービスの固定フィルター](https://powerbi.microsoft.com/en-us/blog/announcing-persistent-filters-in-the-service/)

</br>

## 2．固定フィルターの設定方法

固定フィルターはレポート単位で設定できます。デフォルト設定では、有効になっておりますが、無効に設定されたい場合、以下の2つの方法があります。

１．Power BI Desktopの設定画面のオプションから、「**レポートの設定**」 ＞ 「**固定フィルター**」に移動します。
「**エンドーユーザーがこのファイルのフィルターをPower BIサービスに保存することを許可しない**」にチェックを入れます。


<div align="center">
<img src="pic3.png">
</div>


２．レポートの三点リーダー「**…**」から、「**設定**」 ＞ 「**固定フィルター**」に移動します。
「**このレポートのフィルターを保存することをエンドーユーザーに許可しません。**」にチェックを入れます。


<div align="center">
<img src="pic4.png">
</div>


</br>

## 3．固定フィルターが有効な場合の挙動

固定フィルターが有効な場合、ユーザーは再度レポートを開いたときに自分自身が前回のフィルター条件から作業を続けられます。
また、ユーザー自身が変更したフィルター条件を保持したまま、他のユーザーにリンクを共有したい場合、リンクの共有を作成したときに、「**自分の変更を含める**」にチェックを入れます。


<div align="center">
<img src="pic5.png">
</div>


一方、Power BIサービスに発行した状態のレポートを他のユーザーにリンクを共有したい場合、リンクの共有を作成したときに、「**自分の変更を含める**」にチェックを外します。


<div align="center">
<img src="pic6.png">
</div>

</br>

## 4．固定フィルターが無効な場合の挙動

固定フィルターが無効な場合は、他のユーザーにリンクを共有する場合、「**自分の変更を含める**」が表示されません。以下のイメージでは、固定フィルターが無効と有効の場合のイメージをご確認ください。

<div align="center">
<img src="pic7.png">
</div>

固定フィルターが無効になった場合は、他のユーザーにリンクを共有しても、自分の変更したフィルター条件は保持されません。また、以下のイメージの通り、ユーザーはフィルターを変更しても、「**Reset**」ボタンが灰色のままとなっており、変更したフィルター条件が保持されないことをご確認いただけます。


<div align="center">
<img src="pic8.png">
</div>

</br>

## 5．その他　Teamsでのチャットでリンク共有

固定フィルターの設定の有無に関わらず、Teamsでのチャットでリンクを共有した場合、ユーザーはリンクを共有した時点で変更したフィルター状態のレポートを共有することとなりますので、ご留意ください。


</br>

<div align="center">
<img src="pic9.png">
</div>


</br>
以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)