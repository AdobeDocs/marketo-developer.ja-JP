---
title: REST API
feature: REST API
description: Marketo REST APIの使用方法、API ユーザーとLaunchPointの設定、割り当てと制限の表示、認証ヘッダーによる認証、リードの取得について説明します。
exl-id: 4b9beaf0-fc04-41d7-b93a-a1ae3147ce67
TQID: https://experienceleague.adobe.com/GqhWI816wWX-2zf89wWj-GXpg9i615HRFVl2ljdYVj0
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b13bd2ad-8e65-49e5-9691-2a0d31067b35id: c5f60233-d5ea-4453-a799-0ad258b4d399id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 803
ht-degree: 17%

---

# REST API

Marketo REST APIでは、多くのシステム機能にリモートアクセスできます。 プログラムの作成、リードの一括インポート、Marketoインスタンスの詳細レベルの制御に使用できます。

REST APIは、大きく分けて次のふたつのカテゴリーに分類されます。

- [ リードデータベース ](https://developer.adobe.com/marketo-apis/api/mapi) APIは、Marketoの個人レコードと、商談や企業などの関連するオブジェクトタイプを取得して操作します。
- [Asset](https://developer.adobe.com/marketo-apis/api/asset)のAPIは、マーケティング資料およびワークフロー関連のレコードを操作します。

>[!NOTE]
>
>SOAP APIは非推奨（廃止予定）であり、2026年7月31日以降は使用できなくなります。 すべての新規開発は、Marketo [REST API](./rest-api.md) を使用して行う必要があり、サービスの中断を回避するのに既存のサービスはその日までに移行する必要があります。 SOAP API を使用するサービスがある場合、移行方法について詳しくは、SOAP API [移行ガイド](../soap-api/migration.md)を参照してください。
>

>[!IMPORTANT]
>
>API ゲートウェイ URLのダブルスラッシュの廃止については、この[国の投稿](https://nation.marketo.com/t5/product-blogs/rest-api-double-slash-deprecation/ba-p/358616)を参照してください。
>

- **毎日の割り当て量：**&#x200B;各サブスクリプションには、1日あたり50,000回のAPI呼び出しが割り当てられます。 割り当て量は、毎日12:00 CSTにリセットされます。 1日の割り当てを増やすには、アカウントマネージャーにお問い合わせください。
- **レート制限：**&#x200B;各インスタンスは、20秒あたり100回のAPI呼び出しに制限されています。
- **同時実行数の制限：**&#x200B;各インスタンスでは、最大10回の同時API呼び出しが許可されます。

標準API呼び出しのURIの最大長は8 KB、最大ボディサイズは1 MBです。 Bulk API呼び出しは、最大10 MBのボディサイズをサポートします。

呼び出しにエラーが含まれている場合、APIは通常、HTTP ステータスコード 200を返します。 JSON応答には、値`false`の`success` メンバーと、`errors` メンバーのエラーの配列が含まれています。 エラーの詳細については、[こちら](error-codes.md)を参照してください。

## はじめに

次の手順を実行するには、Marketo インスタンスの管理者権限が必要です。 このワークフローでは、API資格情報を作成し、それを使用してリードレコードを取得します。

まず、API ユーザーを作成し、認証済み呼び出しの資格情報を取得します。 インスタンスにログインし、**[!UICONTROL 管理者]** > **[!UICONTROL ユーザーと役割]**&#x200B;に移動します。

![管理のユーザ＆ロール](assets/admin-users-and-roles.png)

「**[!UICONTROL 役割]**」タブを選択し、「新しい役割」を選択します。 アクセス API グループから「読み取り専用リード」（または「読み取り専用ユーザー」）権限を少なくとも役割に割り当てます。 役割にわかりやすい名前を付け、**[!UICONTROL 作成]**&#x200B;を選択します。

![新規ロール](assets/new-role.png)

[!UICONTROL  ユーザー] タブに戻り、**[!UICONTROL 新規ユーザーの招待]**&#x200B;を選択します。 ユーザーをAPI ユーザーとして識別する記述的な名前を入力し、電子メールアドレスを入力して、**[!UICONTROL 次へ]**&#x200B;を選択します。

![新規ユーザ情報](assets/new-user-info.png)

「[!UICONTROL APIのみ]」オプションを選択し、作成したAPI役割を割り当て、**[!UICONTROL 次へ]**&#x200B;を選択します。

![新規ユーザー権限](assets/new-user-permissions.png)

**[!UICONTROL 送信]**&#x200B;を選択してユーザーを作成します。

![新規ユーザメッセージ](assets/new-user-message.png)

次に、[!UICONTROL 管理者] メニューに移動し、**[!UICONTROL LaunchPoint]**&#x200B;を選択します。

![Launchpoint](assets/admin-launchpoint.png)

**[!UICONTROL 新規]** > **[!UICONTROL 新規サービス]**&#x200B;を選択します。 わかりやすい名前と説明を入力し、[!UICONTROL  サービス ] メニューから&#x200B;**[!UICONTROL カスタム]**&#x200B;を選択します。 [!UICONTROL APIのみユーザー] メニューから新しいユーザーを選択し、**[!UICONTROL 作成]**&#x200B;を選択します。

![新規 Launchpoint サービス](assets/admin-launchpoint-new-service.png)

新しいサービスの&#x200B;**[!UICONTROL 詳細を表示]**&#x200B;を選択して、クライアント IDとクライアント秘密鍵にアクセスします。 「**[!UICONTROL トークンを取得]**」を選択して、1時間有効なアクセストークンを生成します。 最初のAPI呼び出しのトークンを保存します。

![トークンを取得](assets/get-token.png)

**[!UICONTROL 管理者]** > **[!UICONTROL Web サービス]**&#x200B;に移動します。

![Web サービス](assets/admin-web-services.png)

REST API ボックスで[!UICONTROL Endpoint]を見つけ、最初のAPI呼び出しのために保存します。

![REST エンドポイント](assets/admin-web-services-rest-endpoint-1.png)

すべてのREST API呼び出しには、HTTP ヘッダーにアクセストークンを含める必要があります。

```text
Authorization: Bearer cdf01657-110d-4155-99a7-f986b2ff13a0:int
```

>[!IMPORTANT]
>
>**access_token** クエリパラメーターを使用した認証のサポートは、2025年6月30日（PT）に削除されます。 プロジェクトでアクセストークンを渡すのにクエリパラメーターを使用している場合は、できるだけ早く **Authorization** ヘッダーを使用するように更新する必要があります。 新規開発では、**Authorization** ヘッダーのみを使用する必要があります。

新しいブラウザータブを開き、次のURLを入力します。 プレースホルダーをインスタンスのエンドポイントとメールアドレスに置き換えて、[ フィルタータイプでリードを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/getLeadsByFilterUsingGET)を呼び出します。

```text
<Your Endpoint URL>/rest/v1/leads.json?&filterType=email&filterValues=<Your Email Address>
```

データベースに電子メールアドレスを持つリードレコードが含まれていない場合は、既存のリードの電子メールアドレスを使用します。 URLを送信して、次の例のようなJSON応答を受信します。

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

API使用レポートでは、各API ユーザーを個別に追跡します。 各web サービスに個別のユーザーを割り当てると、各統合のAPI使用状況を特定できます。

呼び出しがインスタンスの制限を超え、その後の呼び出しが失敗した場合は、レポートを使用して各サービスの呼び出し量を特定します。 **[!UICONTROL 管理者]** > **[!UICONTROL 統合]** > **[!UICONTROL Web サービス]**&#x200B;に移動し、過去7日間に行われた呼び出しの数を選択します。

毎日および過去7日間の使用状況とエラーの統計を返すREST エンドポイントについては、[使用状況](usage.md)を参照してください。
