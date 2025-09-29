---
title: REST API
feature: REST API
description: Marketo REST API の使用方法、API ユーザーと LaunchPoint の設定方法、割り当て量と制限の表示方法、Authorization ヘッダーによる認証方法およびリードの取得方法について説明します。
exl-id: 4b9beaf0-fc04-41d7-b93a-a1ae3147ce67
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 95%

---

# REST API

Marketo は、システムの多くの機能をリモートで実行できる REST API を公開しています。プログラムの作成からリードの一括読み込みまで、Marketo インスタンスの詳細な制御を可能にするオプションが多数あります。

一般に、これらの API は、[リードデータベース](https://developer.adobe.com/marketo-apis/api/mapi/)と[アセット](https://developer.adobe.com/marketo-apis/api/asset/)という 2 つの大きなカテゴリに分類されます。Lead Database API を使用すると、Marketo のユーザレコードや、商談や会社などの関連オブジェクトタイプを取得および操作できます。Asset API を使用すると、マーケティングの販促物やワークフロー関連のレコードとのインタラクションが可能になります。

>[!NOTE]
>SOAP API は非推奨（廃止予定）となり、2025年10月31日（PT）以降は使用できなくなります。すべての新規開発は、Marketo [REST API](./rest-api.md) を使用して行う必要があり、サービスの中断を回避するのに既存のサービスはその日までに移行する必要があります。SOAP API を使用するサービスがある場合、移行方法について詳しくは、SOAP API [移行ガイド](../soap-api/migration.md)を参照してください。
>

- **毎日の割り当て量：** 購読には、1 日あたり 50,000 回の API 呼び出しが割り当てられます（毎日 12:00AM CST にリセットされます）。 アカウントマネージャーを通じて、毎日の割り当て量を増やすことができます。
- **レートの制限：**&#x200B;インスタンスあたりの API アクセスは、20 秒あたり 100 回の呼び出しに制限されます。
- **同時実行の制限：**&#x200B;同時 API 呼び出しは最大 10 回までです。

標準呼び出しのサイズは、URI の長さが 8 KB、本文のサイズが 1 MB に制限されていますが、一括 API の場合、本文は 10 MB まで可能です。呼び出しでエラーが発生した場合、API は通常、ステータスコード 200 を返しますが、JSON 応答には、値が `false` の「success」メンバーと、「errors」メンバー内のエラーの配列が含まれます。エラーについて詳しくは、[こちら](error-codes.md)を参照してください。

## はじめに

次の手順では、Marketo インスタンスの管理者権限が必要です。

Marketo への最初の呼び出しでは、リードレコードを取得します。Marketo の操作を開始するには、インスタンスへの認証された呼び出しを行う API 資格情報を取得する必要があります。インスタンスにログインし、**[!UICONTROL 管理]**／**[!UICONTROL ユーザ＆ロール]**&#x200B;に移動します。

![管理のユーザ＆ロール](assets/admin-users-and-roles.png)

「**[!UICONTROL ロール]**」タブをクリックし、「新規ロール」をクリックして、Access API グループのロールに少なくとも「読み取り専用リード」（または「読み取り専用ユーザ」）権限を割り当てます。わかりやすい名前を付けて、「**[!UICONTROL 作成]**」をクリックします。

![新規ロール](assets/new-role.png)

次に、「[!UICONTROL ユーザ]」タブに戻り、「**[!UICONTROL 新規ユーザを招待]**」をクリックします。ユーザに、API ユーザであることを示すわかりやすい名前とメールアドレスを指定して、「**[!UICONTROL 次へ]**」をクリックします。

![新規ユーザ情報](assets/new-user-info.png)

次に、「[!UICONTROL API のみ]」オプションをオンにして、作成した API ロールをユーザに付与し、「**[!UICONTROL 次へ]**」をクリックします。

![新規ユーザー権限](assets/new-user-permissions.png)

ユーザ作成プロセスを完了するには、「**[!UICONTROL 送信]**」をクリックします。

![新規ユーザメッセージ](assets/new-user-message.png)

次に、[!UICONTROL 管理]メニューに移動して、「**[!UICONTROL Launchpoint]**」をクリックします。

![Launchpoint](assets/admin-launchpoint.png)

**[!UICONTROL 新規]**&#x200B;メニューをクリックして、「**[!UICONTROL 新規サービス]**」を選択します。サービスにわかりやすい名前を付け、[!UICONTROL サービス]ドロップダウンメニューから「**[!UICONTROL カスタム]**」を選択します。説明を入力し、[!UICONTROL API のみのユーザ]ドロップダウンメニューから新規ユーザを選択して、「**[!UICONTROL 作成]**」をクリックします。

![新規 Launchpoint サービス](assets/admin-launchpoint-new-service.png)

新しいサービスの「**[!UICONTROL 詳細を表示]**」をクリックして、クライアント ID とクライアント秘密鍵にアクセスします。現時点では、「**[!UICONTROL トークンを取得]**」ボタンをクリックして、1 時間有効なアクセストークンを生成できます。現時点では、トークンをメモに保存します。

![トークンを取得](assets/get-token.png)

次に、**[!UICONTROL 管理]**&#x200B;メニューに移動し、**[!UICONTROL Web サービス]**&#x200B;に移動します。

![Web サービス](assets/admin-web-services.png)

現時点では、「REST API」ボックスで[!UICONTROL エンドポイント]を見つけて、メモに保存します。

![REST エンドポイント](assets/admin-web-services-rest-endpoint-1.png)

REST API メソッドを呼び出す場合、呼び出しが成功するには、すべての呼び出しにアクセストークンを含める必要があります。アクセストークンは、HTTP ヘッダーとして送信する必要があります。

```
Authorization: Bearer cdf01657-110d-4155-99a7-f986b2ff13a0:int
```

>[!IMPORTANT]
>
>**access_token** クエリパラメーターを使用した認証のサポートは、2025年6月30日（PT）に削除されます。プロジェクトでアクセストークンを渡すのにクエリパラメーターを使用している場合は、できるだけ早く **Authorization** ヘッダーを使用するように更新する必要があります。新規開発では、**Authorization** ヘッダーのみを使用する必要があります。

新しいブラウザータブを開き、適切な情報を使用して、[フィルタータイプによりリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET)を呼び出します。

```
<Your Endpoint URL>/rest/v1/leads.json?&filterType=email&filterValues=<Your Email Address>
```

データベース内に自分のメールアドレスを含むリードレコードがない場合は、存在すると分かっているレコードで代用します。URL バーで Enter キーを押すと、次のような JSON 応答が返されます。

```json
{
    "requestId":"c493#1511ca2b184",
    "result":[
       {
           "id":1,
           "updatedAt":"2015-08-24T20:17:23Z",
           "lastName":"Elkington",
           "email":"developerfeedback@marketo.com",
           "createdAt":"2013-02-19T23:17:04Z",
           "firstName":"Kenneth"
        }
    ],
    "success":true
}
```

## API 使用量

各 API ユーザは API 使用量レポートで個別に報告されるので、web サービスをユーザごとに分割すると、各統合の使用量を簡単に把握できます。インスタンスへの API 呼び出しの数が制限を超え、後続の呼び出しが失敗する場合は、この方法を使用すると、各サービスからのボリュームを把握し、問題を解決する方法を評価できます。使用量を確認するには、**[!UICONTROL 管理]**／**[!UICONTROL 統合]**／**[!UICONTROL Web サービス]**&#x200B;に移動し、過去 7 日間の呼び出し回数をクリックします。
