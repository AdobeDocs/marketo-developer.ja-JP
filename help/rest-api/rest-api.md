---
title: "REST API"
feature: REST API
description: "REST API の概要"
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---


# REST API

Marketoは、システムの機能の多くをリモートで実行できる REST API を公開しています。 プログラムの作成からリードの一括読み込みまで、Marketo インスタンスの詳細な制御を可能にするオプションが多数あります。

これらの API は、通常、次の 2 つの大きなカテゴリに分類されます。 [リードデータベース](https://developer.adobe.com/marketo-apis/api/mapi/)、および [アセット](https://developer.adobe.com/marketo-apis/api/asset/). Lead Database API を使用すると、Marketoの人物レコードおよび関連するオブジェクトタイプ（商談や会社など）の取得とやり取りをおこなうことができます。 Asset API を使用すると、マーケティング用販促物やワークフロー関連のレコードを操作できます。

- **毎日のクォータ：** 購読には、1 日あたり 50,000 回の API 呼び出しが割り当てられます（毎日 12:00 にリセットされます）。 アカウントマネージャーを通じて、1 日の割り当て量を増やすことができます。
- **レート制限：** インスタンスごとの API アクセスは、20 秒あたり 100 回の呼び出しに制限されています。
- **同時実行制限：**  最大 10 回の同時 API 呼び出し。

標準呼び出しのサイズは、URI の長さが 8 KB、本文のサイズが 1 MB に制限されていますが、バルク API の本文は 10 MB にすることができます。 呼び出しでエラーが発生した場合、API は通常、ステータスコード 200 を返しますが、JSON 応答には、値がの「success」メンバーが含まれます `false`、および「errors」メンバーのエラーの配列。 エラーの詳細 [こちら](error-codes.md).

## はじめに

次の手順では、Marketo インスタンスでの管理者権限が必要です。

Marketoへの最初の呼び出しでは、リードレコードを取得します。 Marketoの使用を開始するには、インスタンスに対して認証済み呼び出しを行うための API 資格情報を取得する必要があります。 インスタンスにログインし、に移動します **[!UICONTROL Admin]** -> **[!UICONTROL ユーザーと役割]**.

![管理者ユーザーと役割](assets/admin-users-and-roles.png)

「」をクリックします [!UICONTROL 役割] タブに続いて「新しい役割」をクリックし、「読み取り専用リード」（または「読み取り専用ユーザー」）以上の権限をアクセス API グループの役割に割り当てます。 必ずわかりやすい名前を付けて、 [!UICONTROL 作成].

![新しい役割](assets/new-role.png)

「ユーザー」タブに戻り、「新規ユーザーを招待」をクリックします。 ユーザーに、API ユーザーであることを示すわかりやすい名前とメールアドレスを指定し、 **[!UICONTROL 次]**.

![新規ユーザー情報](assets/new-user-info.png)

次に、「API のみ」オプションをオンにし、作成した API の役割をユーザーに付与して、クリックします **[!UICONTROL 次]**.

![新規ユーザー権限](assets/new-user-permissions.png)

ユーザー作成プロセスを完了するには、 **[!UICONTROL 送信]**.

![新規ユーザーメッセージ](assets/new-user-message.png)

次に、管理者メニューに移動し、 **[!UICONTROL LaunchPoint]**.

![Launchpoint](assets/admin-launchpoint.png)

「新規」メニューをクリックし、次の項目を選択します [!UICONTROL 新しいサービス]. サービスにわかりやすい名前を付け、サービス ドロップダウンメニューから「カスタム」を選択します。 説明を入力し、API のみのユーザーのドロップダウンメニューから新しいユーザーを選択して、クリックします [!UICONTROL 作成].

![新しい起動ポイント サービス](assets/admin-launchpoint-new-service.png)

新しいサービスの「詳細を表示」をクリックして、クライアント ID とクライアント秘密鍵にアクセスします。 今のところ、をクリックできます [!UICONTROL トークンを取得] 1 時間有効なアクセストークンを生成するボタン。 現時点では、トークンをメモに保存します。

![トークンを取得](assets/get-token.png)

次に、管理メニューに移動し、次にアクセスします **[!UICONTROL Web サービス]**.

![Web サービス](assets/admin-web-services.png)

「REST API」ボックスでエンドポイントを見つけて、今はメモに保存します。

![REST エンドポイント](assets/admin-web-services-rest-endpoint-1.png)

新しいブラウザータブを開き、適切な情報を使用して以下を入力して呼び出します [フィルタータイプ別のリードの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET):

```
<Your Endpoint URL>/rest/v1/leads.json?access_token=<Your Access Token>&filterType=email&filterValues=<Your Email Address>
```

データベースにメールアドレスを含むリードレコードがない場合は、存在することが分かっているメールアドレスに置き換えます。 URL バーで Enter キーを押すと、次のような JSON 応答が返されます。

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

各 API ユーザーは API 使用状況レポートで個別にレポートされるので、ユーザーごとに web サービスを分割すると、各統合の使用状況を簡単に説明できます。 インスタンスへの API 呼び出し数が制限を超え、以降の呼び出しが失敗した場合は、この方法を使用すると、各サービスのボリュームを考慮して、問題の解決方法を評価できます。 に移動して、使用状況を確認します。 **[!UICONTROL Admin]** -> **[!UICONTROL 統合]** > **[!UICONTROL Web サービス]** 過去 7 日間の通話数をクリックします。
