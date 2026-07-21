---
title: スマートキャンペーン
feature: REST API, Smart Campaigns
description: IDや名前によるクエリ、フィルターの参照、クローン削除の作成、トリガーのスケジュールまたはリクエストなど、Marketo REST APIをスマートキャンペーンに使用する方法について説明します
exl-id: 540bdf59-b102-4081-a3d7-225494a19fdd
TQID: https://experienceleague.adobe.com/iysRjtqd9plkreyIMuNjAF3YVFHtDUIrc-GInB4V8mg
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
subfeature_v2:
  - id: ad89fb33-8541-4339-afe7-bb13d1633714
  - id: d0251300-e25f-466f-9856-7e11ce8fa7aa
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1009
ht-degree: 40%

---

# スマートキャンペーン

[スマートキャンペーンのエンドポイントリファレンス（アセット）](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns)

[Campaigns エンドポイントリファレンス（リード）](https://developer.adobe.com/marketo-apis/api/mapi#tag/Campaigns)

Smart Campaign REST APIを使用して、スマートキャンペーンのクエリ、作成、複製、削除を行います。 また、バッチキャンペーンのスケジュール設定、トリガーキャンペーンのリクエスト、キャンペーンのアクティベーションの管理も可能です。

## クエリ

ID[&#128279;](#by_id)で[、名前](#by_name)で、または[閲覧](#browse)でスマートキャンペーンをクエリします。

### ID 別

[ID によるスマートキャンペーンの取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/getSmartCampaignByIdUsingGET)エンドポイントは、単一のスマートキャンペーン `id` をパスパラメーターとして受け取り、単一のスマートキャンペーンレコードを返します。

```http
GET /rest/asset/v1/smartCampaign/{id}.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "7883#169838a32f0",
    "warnings": [],
    "result": [
        {
            "id": 1001,
            "name": "Process Bounced Emails",
            "description": "System smart campaign for processing bounced email events",
            "createdAt": "2016-09-10T23:16:19Z+0000",
            "updatedAt": "2016-09-10T23:16:19Z+0000",
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 1001,
            "flowId": 1001,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1001A1"
        }
    ]
}
```

エンドポイントは、`result`配列の最初の位置にある1つのレコードを返します。

### 名前別

[名前によるスマートキャンペーンの取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/getSmartCampaignByNameUsingGET)エンドポイントは、単一のスマートキャンペーン `name` をパラメーターとして受け取り、単一のスマートキャンペーンレコードを返します。

```http
GET /rest/asset/v1/smartCampaign/byName.json?name=Test Trigger Campaign
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "14494#16c886ffa44",
    "warnings": [],
    "result": [
        {
            "id": 1069,
            "name": "Test Trigger Campaign",
            "description": "",
            "createdAt": "2018-02-16T01:34:39Z+0000",
            "updatedAt": "2019-08-13T00:45:21Z+0000",
            "folder": {
                "id": 327,
                "type": "Folder"
            },
            "status": "Inactive",
            "type": "trigger",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 2747,
            "flowId": 1088,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1069A1"
        }
    ]
}
```

エンドポイントは、`result`配列の最初の位置にある1つのレコードを返します。

### 参照

[Get Smart Campaigns](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/getAllSmartCampaignsGET) エンドポイントは、フィルターとページネーションのオプションのクエリパラメーターをサポートしています。

`earliestUpdatedAt` パラメーターと `latestUpdatedAt` パラメーターは、ISO-8601 形式（ミリ秒単位なし）で `datetimes` を受け付けます。 両方が設定されている場合は、earliestUpdatedAt が latestUpdatedAt の前に置かれる必要があります。

`folder` パラメーターは、参照する親フォルダーを指定します。 `id`と`type`を含むJSON オブジェクトとして渡します。

`maxReturn`整数は、エントリの最大数を指定します。 デフォルトは20、最大は200です。

`offset`整数は、エントリの取得を開始する場所を指定します。 `maxReturn`と一緒に使用します。 デフォルトは0です。

アクティブなトリガーキャンペーンのみを返すように、`isActive` ブール値パラメーターを設定します。

```http
GET /rest/asset/v1/smartCampaigns.json?earliestUpdatedAt=2016-09-10T23:15:00-00:00&latestUpdatedAt=2016-09-10T23:17:00-00:00
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "626#16983a92965",
    "warnings": [],
    "result": [
        {
            "id": 1001,
            "name": "Process Bounced Emails",
            "description": "System smart campaign for processing bounced email events",
            "createdAt": "2016-09-10T23:16:19Z+0000",
            "updatedAt": "2016-09-10T23:16:19Z+0000",
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 1001,
            "flowId": 1001,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1001A1"
        },
        {
            "id": 1002,
            "name": "Process Unsubscribes",
            "description": "System smart campaign for processing unsubscribe events",
            "createdAt": "2016-09-10T23:16:19Z+0000",
            "updatedAt": "2016-09-10T23:16:19Z+0000",
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 1002,
            "flowId": 1002,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1002A1"
        }
    ]
}
```

エンドポイントは、`result`配列内の1つ以上のレコードを返します。

## 作成

`application/x-www-form-urlencoded` POST リクエストを[&#x200B; スマートキャンペーンの作成](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/createSmartCampaignUsingPOST) エンドポイントに送信します。 `name`および`folder` パラメーターが必要です。 `folder`を`id`と`type`を含むJSON オブジェクトとして渡します。

オプションで、`description` パラメーターを使用してスマートキャンペーンを説明することもできます（最大 2,000 文字）。

```http
POST /rest/asset/v1/smartCampaigns.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=Smart Campaign 02&folder={"type": "folder","id": 640}&description=This is a smart campaign creation test.
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "25bc#16c9138f148",
    "warnings": [],
    "result": [
        {
            "id": 1076,
            "name": "Smart Campaign 02",
            "description": "This is a smart campaign creation test.",
            "createdAt": "2019-08-14T17:42:04Z+0000",
            "updatedAt": "2019-08-14T17:42:04Z+0000",
            "folder": {
                "id": 640,
                "type": "Folder"
            },
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": true,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 5132,
            "flowId": 1095,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1076A1"
        }
    ]
}
```

## 更新

`application/x-www-form-urlencoded` POST リクエストを[&#x200B; スマートキャンペーンの更新](https://developer.adobe.com/marketo-apis/api/asset) エンドポイントに送信します。 スマートキャンペーン `id` パスパラメーターが必要です。 `name`を使用して名前を変更するか、`description`を使用して説明を変更します。

```http
POST /rest/asset/v1/smartCampaign/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```sql
name=Smart Campaign 02 Update&description=This is a smart campaign update test.
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "14b6a#16c924b992f",
    "warnings": [],
    "result": [
        {
            "id": 1076,
            "name": "Smart Campaign 02 Update",
            "description": "This is a smart campaign update test.",
            "createdAt": "2019-08-14T17:42:04Z+0000",
            "updatedAt": "2019-08-14T22:42:04Z+0000",
            "folder": {
                "id": 640,
                "type": "Folder"
            },
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": true,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 5132,
            "flowId": 1095,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1076A1"
        }
    ]
}
```

## 複製

`application/x-www-form-urlencoded` POST リクエストを[Clone Smart Campaign](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5) エンドポイントに送信します。 `id`、`name`および`folder` パラメーターが必要です。 ソースキャンペーン、新しいキャンペーン名、親フォルダーを指定します。 `folder`を`id`と`type`を含むJSON オブジェクトとして渡します。

オプションで、`description` パラメーターを使用してスマートキャンペーンを説明することもできます（最大 2,000 文字）。

```http
POST /rest/asset/v1/smartCampaign/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=Test Trigger Campaign Clone&folder={"type": "folder","id": 640}&description=This is a smart campaign clone test.
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "681d#16c9339499b",
    "warnings": [],
    "result": [
        {
            "id": 1077,
            "name": "Test Trigger Campaign Clone",
            "description": "This is a smart campaign clone test.",
            "createdAt": "2019-08-15T03:01:41Z+0000",
            "updatedAt": "2019-08-15T03:01:41Z+0000",
            "folder": {
                "id": 640,
                "type": "Folder"
            },
            "status": "Inactive",
            "type": "trigger",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 5135,
            "flowId": 1096,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1077A1"
        }
    ]
}
```

## 削除

[スマートキャンペーンを削除](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/deleteSmartCampaignUsingPOST)エンドポイントは、パスパラメーターとして単一のスマートキャンペーン `id` を受け取ります。

```http
POST /rest/asset/v1/smartCampaign/{id}/delete.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "d757#16c934216ac",
    "warnings": [],
    "result": [
        {
            "id": 1077
        }
    ]
}
```

## バッチ

バッチスマートキャンペーンは指定された時間に実行され、定義されたリードのセットを一緒に処理します。

## スケジュール

[&#x200B; キャンペーンのスケジュール &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi#tag/Campaigns/operation/scheduleCampaignUsingPOST)を使用して、バッチキャンペーンをスケジュールします。 キャンペーン `id` パス パラメーターが必要です。 オプションの`tokens`、`runAt`および`cloneToProgram` パラメーターをJSON リクエスト本文に渡します。

`tokens`配列は、この実行の既存のプログラムのマイトークンを上書きします。 Marketoは、キャンペーンの実行後にオーバーライドを破棄します。 各項目には名前と値のペアが含まれており、トークン名には`{{my.name}}`形式を使用する必要があります。

`runAt`日時パラメーターは、キャンペーンを実行するタイミングを指定します。 省略した場合、キャンペーンはリクエストの5分後に実行されます。 将来の値は2年以上である必要があります。

この API 経由でスケジュールされたキャンペーンは、実行される前に常に最低 5 分間待機します。

`cloneToProgram` 文字列パラメーターには、結果として得られるプログラムの名前が含まれます。  設定すると、キャンペーン、親プログラムおよびそのすべてのアセットが、結果として得られる新しい名前で作成されます。 親プログラムが複製され、新しく作成されたキャンペーンがスケジュールされます。 結果として得られるプログラムは、親の下に作成されます。 スニペット、プッシュ通知、アプリ内メッセージ、静的リスト、レポート、ソーシャルアセットを含むプログラムは、この方法では複製できません。 このエンドポイントを使用する場合、1 日あたりの呼び出し回数は 20 回に制限されます。 代替として[プログラムを複製](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5)エンドポイントを使用することをお勧めします。

```http
POST /rest/v1/campaigns/{id}/schedule.json
```

```json
{
   "input":
      {
         "runAt": "2018-03-28T18:05:00+0000",
         "tokens": [
            {
               "name": "{{my.message}}",
               "value": "Updated message"
            },
            {
               "name": "{{my.other token}}",
               "value": "Value for other token"
            }
          ]
      }
}
```

```json
{
    "requestId": "52b#161d90e1743",
    "result": [
        {
            "id": 3713
        }
    ],
    "success": true
}
```

## トリガー

トリガースマートキャンペーンは、イベントに応じて一人ひとりを処理します。

### リクエスト

[Request Campaign](https://developer.adobe.com/marketo-apis/api/mapi#tag/Campaigns/operation/triggerCampaignUsingPOST)を使用して、リードをトリガーキャンペーンのフローに渡します。 キャンペーンでは、Web サービス APIをソースとするCampaign is Requested トリガーを使用する必要があります。

キャンペーン `id` パス パラメーターとリード IDの`leads`整数配列が必要です。 各呼び出しは、最大100件のリードを受け付けます。

オプションで、`tokens` 配列パラメーターを使用して、キャンペーンの親プログラムにローカルなマイトークンを上書きできます。 `tokens` は、最大 100 個のトークンを受け入れます。 各 `tokens` 配列項目には、名前と値のペアが含まれます。 トークンの名前は、「`{{my.name}}`」という形式にする必要があります。 [システムトークンをメール内のリンクとして追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/using-tokens/add-a-system-token-as-a-link-in-an-email)アプローチを使用して「viewAsWebpageLink」システムトークンを追加する場合、`tokens` を使用して上書きすることはできません。 代わりに、[メールにWeb ページとして表示リンクを追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/add-a-view-as-web-page-link-to-an-email)アプローチを使用すれば、`tokens` を使用して「viewAsWebPageLink」を上書きできます。

JSON リクエスト本文に`leads`と`tokens` パラメーターを渡します。

```http
POST /rest/v1/campaigns/{id}/trigger.json
```

```json
{
   "input":
      {
         "leads" : [
            {
               "id" : 318592
            },
            {
               "id" : 318593
            }
         ],
         "tokens" : [
            {
               "name": "{{my.message}}",
               "value": "Updated message"
            },
            {
               "name": "{{my.other token}}",
               "value": "Value for other token"
            }
         ]
      }
}
```

```json
{
    "requestId": "9e01#161d922f1aa",
    "result": [
        {
            "id": 3712
        }
    ],
    "success": true
}
```

### 有効化

[スマートキャンペーンをアクティブ化](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/activateSmartCampaignUsingPOST)エンドポイントは簡単です。 `id` パスパラメーターは必須です。 アクティブ化を成功させるには、キャンペーンに対して次の条件を満たす必要があります。

- キャンペーンが非アクティブ化されました。
- キャンペーンには、少なくとも1つのトリガーと1つのフローステップがあります。
- このキャンペーンには、エラーのないトリガー、フィルター、フローステップが備わっています。

```http
POST /rest/asset/v1/smartCampaign/{id}/activate.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "a33a#161d9c0dcf3",
    "result": [
        {
            "id": 1069
        }
    ]
}
```

### 非アクティブ化

[スマートキャンペーンの非アクティブ化](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/deactivateSmartCampaignUsingPOST)は簡単です。 `id` パスパラメーターは必須です。 非アクティブ化を成功させるには、キャンペーンをアクティブ化する必要があります。

```http
POST /rest/asset/v1/smartCampaign/{id}/deactivate.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6228#161d9c29fbf",
    "result": [
        {
            "id": 1069
        }
    ]
}
```
