---
title: フクロウエラーについて  
date: 2023-12-29 00:00:00  
tags:  
  - Power BI
  - Power BI サービス
  - Power BI Service
  - エラー
  - error
  - troubleshooting
  - トラブルシューティング
---
    
こんにちは、Power BI サポート チームの山崎です。   
Power BI サービスでは、何かしら問題が発生している場合にエラーメッセージが表示されますが、このようなフクロウの画像付きのエラーに遭遇したことはありますか。  
頻度としては低いため突然フクロウが画面に現れると驚かれるかと思いますが、そんな時に落ち着いてトラブルシューティングや対処を進められるように、本記事ではこのフクロウエラーについて詳細をご紹介いたします。  

<!-- more -->

<div align="left">
<img src="1.png">
</div>
</p>


> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


 </br>

##  <font color="DodgerBlue">フクロウエラーとは</font>  
フクロウエラーの画面は、Power BI サービスとの接続において何らかの問題が発生した際に Power BI 内でリダイレクトされるページとなります。  
画像は一例となりますが、フクロウエラーの画面は大きく ３ つの情報から構成されますので、フクロウが表示されたときは落ち着いて以下のポイントに注目しましょう。  

<div align="left">
<img src="2.png">
</div>
</p>

### <font color="HotPink">1. フクロウの画像</font> 
事象によって、フクロウの画像が異なる場合があります。  
冒頭で案内したようなフクロウのこともあれば、上の画像のように虫眼鏡をのぞいているフクロウだったり、ケガをしているフクロウのこともあります。  
フクロウの様子の違いがサポートチームでの調査において有益な情報になることがあります。  


### <font color="HotPink">2. エラーメッセージ</font> 
上の画面のように、何かしらのメッセージが表示されることがあり、調査開始にあたり調査箇所の絞り込みのために有効な情報となります。ただし、このメッセージは汎用的である場合が多いです。  
例えば、この 「お探しのページが見つかりませんでした。」  というメッセージの場合、“ページ自体が存在しないのか”、“存在するページにアクセスできないのか” は、後述の切り分けや次の項番 3 のエラー情報をもとに詳細調査を進める必要があります。  

### <font color="HotPink">3. エラー情報詳細</font>   
技術的な詳細情報や、サポートチームにて調査を進める際に必要なエラーメッセージ、日付と時刻、アクティビティ ID などが表示されます。  
これらの情報をもとに、 Microsoft のデータセンター側に記録された内部ログにアクセスし、詳細な調査を行います。  

※	事象によっては、内部ログに詳細が記載されず、原因の特定に至らない場合もあります。  





###  <font color="OrangeRed">サポートチームからのお願い</font>   

フクロウエラーの事象について詳細調査を進める場合、上記の情報が必須となります。  
サポートチームへのお問い合わせを検討される場合は、後述の切り分け結果と共に、1 ～ 3 の情報が含まれる Power BI 画面全体の画面ショットと 2 , 3 のテキスト コピーをお問い合わせ時に必ず送付いただきますようお願いいたします。  
これらの情報がそろっていない場合は、じゅうぶんな調査ができませんことを、何卒ご了承くださいませ。  


 </br>


## <font color="DodgerBlue">フクロウエラーの原因は？</font>  

フクロウエラーが発生するシナリオは実に様々です。  
“ Power BI サービスとの接続において何らかの問題が発生した” と一言で言っても、その原因がユーザーの環境のネットワークに起因していることもあれば、特定のユーザーのアカウント状況に起因していることもあります。また、Power BI サービス側で何か障害が起きている可能性も考えられます。  
発生する期間についても、一過性の事象であったり、継続している事象のこともあります。  
これまで弊社サポートチームに寄せられたお問い合わせの中で確認できている事例としては、以下のものがあります。  
  
### <font color="HotPink">1. アカウントやライセンスの問題</font> 

・Microsoft Entra ID (旧 Azure AD ) で対象のユーザーが無効となっている  
・Microsoft Entra ID  (旧 Azure AD ) で対象のユーザーが削除されている  
・Microsoft Entra ID  (旧 Azure AD ) または Microsoft 365 管理センターで対象のユーザーに Power BI ライセンスが正しく割り当てられていない  
・対象のユーザーがゲストアカウントであり、そのアカウントに問題が発生しており、招待されたテナントの Power BI にサインインできない   

これらの事象に合致または類似しているかどうかは、アカウントやライセンス割り当て状況の確認や、同じ環境にて別のユーザーでも事象が発生しているかを確認してください。  
新規でテストアカウントを作成して再現するか確認することも有効です。  

### <font color="HotPink">2. テナント移行/バックグランドメンテナンス（デプロイ）</font> 

・バックエンド テナントのスケジュールされたメンテナンス/移行アクティビティが発生する  
  
これらはユーザー様の環境起因ではなく、Power BI サービス側のメンテナンス等によるものです。  
時間をおくことで事象が解消するかしばらく様子を見るか、以下サイトにて、障害やメンテナンスが発生していないか確認してください。  


[Microsoft Fabric のサポート]( https://support.fabric.microsoft.com/ja-JP/support/)  
[Microsoft 365 サービス正常性を確認する方法](https://learn.microsoft.com/ja-jp/microsoft-365/enterprise/view-service-health?view=o365-worldwide)
 
### <font color="HotPink">3. ネットワークの問題</font>   

・Power BI のテナント設定で Azure Private Links が有効かつ、パブリック インターネット アクセスが無効になっていることで、Power BI サービスにアクセスできない  
・ユーザー環境にて VPN ブロックされている  
・ユーザー環境にてファイアウォールブロックされている   

対象のご環境にてネットワーク関連の設定変更やメンテナンスが発生していなかったかや、異なるネットワークにて同じアカウントで事象が再現するか確認することで、ネットワークに起因しているかどうか切り分けをしてください。  

 </br>

## <font color="DodgerBlue">事象発生条件の切り分けチェックポイント</font>  
上記含め、以下のリストに沿って事象発生条件の切り分けを行い、被疑箇所を絞り込んだ上で弊社サポートへお問合せいただくことで、スムーズな調査が開始できます。 
解決しない場合は、上述でご案内のエラー情報と本切り分け結果を添えて、サポートまでお問い合わせください。  
 

 </br>

(1) 異なるネットワーク環境でも再現しますか。  

(2) ネットワーク環境を変更すると再現しない場合、対象ネットワークにおいて何か設定変更やメンテナンスはありましたか。  

(3) 複数アカウントでも再現しますか。それとも、特定のアカウントのみで発生しますか。  

(4) 特定のアカウントのみで発生している場合、以下設定状況はいかがですか。  
　　‐ アカウントが無効になっていないか  
　　- Power BI のライセンスは割り当たっているか（何のライセンスが割り当たっているか）  
　　‐ Power BI のライセンスの再割り当て後、Power BI に再度サインインすることで事象が解消するか  

(5) 特定のアカウントがゲストユーザーの場合、招待受け入れはされましたか。  
  
(6) Power BI 管理ポータルのテナント設定にアクセスできる場合、[高度ネットワーク](https://learn.microsoft.com/ja-jp/fabric/admin/tenant-settings-index#advanced-networking)の以下２項目の設定状況をご確認ください。　  
　　‐　Azure Private Link   
　　‐　パブリック　インターネット アクセスのブロック  

(7) 異なるブラウザを使用しても再現しますか。  

(8) ブラウザの履歴を削除しても再現しますか。  

(9) インプライベートモードのブラウザを起動しても再現しますか。    


</br>
</br>

以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)