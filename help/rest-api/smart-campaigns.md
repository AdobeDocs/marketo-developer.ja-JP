---
title: スマートキャンペーン
feature: REST API, Smart Campaigns
description: スマートキャンペーンの概要
exl-id: 540bdf59-b102-4081-a3d7-225494a19fdd
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '989'
ht-degree: 100%

---

# スマートキャンペーン

[スマートキャンペーンエンドポイント参照（アセット）](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns)

[キャンペーンエンドポイント参照（リード）](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns)

Marketo は、スマートキャンペーンで操作を実行する一連の REST API を備えています。これらの API は、クエリ、作成、複製、削除のオプションを提供するアセット API の標準インターフェイスパターンに従います。また、バッチキャンペーンをスケジュールしたり、トリガーキャンペーンをリクエストしたりして、スマートキャンペーンの実行を管理することもできます。

## クエリ

スマートキャンペーンのクエリは、[ID 別](#by_id)、[名前別](#by_name)および[参照](#browse)のアセットに対する標準のクエリタイプに従います。

### ID 別

[ID によるスマートキャンペーンの取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getSmartCampaignByIdUsingGET)エンドポイントは、単一のスマートキャンペーン `id` をパスパラメーターとして受け取り、単一のスマートキャンペーンレコードを返します。

```
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

このエンドポイントでは、`result` 配列の最初の位置に常に 1 つのレコードがあります。

### 名前別

[名前によるスマートキャンペーンの取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getSmartCampaignByNameUsingGET)エンドポイントは、単一のスマートキャンペーン `name` をパラメーターとして受け取り、単一のスマートキャンペーンレコードを返します。

```
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

このエンドポイントでは、`result` 配列の最初の位置に常に 1 つのレコードがあります。

### 参照

[スマートキャンペーンを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getAllSmartCampaignsGET)エンドポイントは、他のアセット API 参照エンドポイントと同様に機能し、オプションで複数のクエリパラメーターでフィルタリング条件を指定できます。

`earliestUpdatedAt` パラメーターと `latestUpdatedAt` パラメーターは、ISO-8601 形式（ミリ秒単位なし）で `datetimes` を受け付けます。両方が設定されている場合は、earliestUpdatedAt が latestUpdatedAt の前に置かれる必要があります。

`folder` パラメーターは、参照する親フォルダーを指定します。形式は、`id` 属性と `type` 属性を含む JSON ブロックです。

`maxReturn` パラメーターは、返されるエントリの最大数を指定する整数です。初期設定は 20 です。最大値は 200 です。

`offset` パラメーターは、エントリの取得を開始する場所を指定する整数です。`maxReturn` と併用できます。初期設定は 0 です。

`isActive` パラメーターは、アクティブなトリガーキャンペーンのみを返すように指定するブール値です。

```
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

このエンドポイントでは、`result` の配列に 1 つ以上のレコードが含まれます。

## 作成

[スマートキャンペーンを作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/createSmartCampaignUsingPOST)エンドポイントは、2 つの必須パラメーターを含む application/x-www-form-urlencoded POST で実行されます。`name` パラメーターは、作成するスマートキャンペーンの名前を指定します。`folder` パラメーターは、スマートキャンペーンが作成される親フォルダーを指定します。形式は、`id` 属性と `type` 属性を含む JSON ブロックです。

オプションで、`description` パラメーターを使用してスマートキャンペーンを説明することもできます（最大 2,000 文字）。

```
POST /rest/asset/v1/smartCampaigns.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

[スマートキャンペーンを更新](https://developer.adobe.com/marketo-apis/api/asset/)エンドポイントは、application/x-www-form-urlencoded POST で実行されます。パスパラメーターとして単一のスマートキャンペーン `id` を受け取ります。`name` パラメーターを使用してスマートキャンペーンの名前を更新したり、`description` パラメーターを使用してスマートキャンペーンの説明を更新したりできます。

```
POST /rest/asset/v1/smartCampaign/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

[スマートキャンペーンを複製](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5)エンドポイントは、3 つの必須パラメーターを含む application/x-www-form-urlencoded POST で実行されます。複製するスマートキャンペーンを指定する `id` パラメーター、新しいスマートキャンペーンの名前を指定する `name` パラメーターおよび新しいスマートキャンペーンが作成される親フォルダーを指定する `folder` パラメーターを受け取ります。形式は、`id` 属性と `type` 属性を含む JSON ブロックです。

オプションで、`description` パラメーターを使用してスマートキャンペーンを説明することもできます（最大 2,000 文字）。

```
POST /rest/asset/v1/smartCampaign/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

[スマートキャンペーンを削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/deleteSmartCampaignUsingPOST)エンドポイントは、パスパラメーターとして単一のスマートキャンペーン `id` を受け取ります。

```
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

バッチスマートキャンペーンは、特定の時間に開始され、特定のリードのセットに一度に影響を与えます。

## スケジュール

[キャンペーンをスケジュール](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns/operation/scheduleCampaignUsingPOST)エンドポイントを使用して、バッチキャンペーンをすぐに実行するか、今後の日付で実行するようにスケジュールします。キャンペーン `id` は、必須のパスパラメーターです。オプションのパラメーターは、`tokens`、`runAt`、`cloneToProgram` で、これらはリクエスト本文で application/json として渡されます。

tokens 配列パラメーターは、既存のプログラムトークンを上書きするマイトークンの配列です。キャンペーンの実行後、トークンは破棄されます。各トークン配列項目には、名前と値のペアが含まれます。トークンの名前は、「{{my.name}}」という形式にする必要があります。

runAt datetime パラメーターは、キャンペーンを実行するタイミングを指定します。指定しない場合は、エンドポイントが呼び出されてから 5 分後にキャンペーンが実行されます。datetime 値は、2 年を超える今後の値にすることはできません。

この API 経由でスケジュールされたキャンペーンは、実行される前に常に最低 5 分間待機します。

`cloneToProgram` 文字列パラメーターには、結果として得られるプログラムの名前が含まれます。設定すると、キャンペーン、親プログラムおよびそのすべてのアセットが、結果として得られる新しい名前で作成されます。親プログラムが複製され、新しく作成されたキャンペーンがスケジュールされます。結果として得られるプログラムは、親の下に作成されます。スニペット、プッシュ通知、アプリ内メッセージ、静的リスト、レポート、ソーシャルアセットを含むプログラムは、この方法では複製できません。このエンドポイントを使用する場合、1 日あたりの呼び出し回数は 20 回に制限されます。代替として[プログラムを複製](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5)エンドポイントを使用することをお勧めします。

```
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

トリガースマートキャンペーンは、トリガー起動イベントに基づいて、一度に 1 人のユーザに影響を与えます。

### リクエスト

[キャンペーンをリクエスト](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns/operation/triggerCampaignUsingPOST)エンドポイントを使用して、リードのセットをトリガーキャンペーンに渡し、キャンペーンのフローを通じて実行します。キャンペーンには、「Web Service API」をソースとする「キャンペーンをリクエスト」トリガーが必要です。

このエンドポイントには、パスパラメーターとしてキャンペーン `id` と、リード ID を含む `leads` 整数配列パラメーターが必要です。1 回の呼び出しでは、最大 100 個のリードが許可されます。

オプションで、`tokens` 配列パラメーターを使用して、キャンペーンの親プログラムにローカルなマイトークンを上書きできます。`tokens` は、最大 100 個のトークンを受け入れます。各 `tokens` 配列項目には、名前と値のペアが含まれます。トークンの名前は、「{{my.name}}」という形式にする必要があります。[システムトークンをメール内のリンクとして追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/using-tokens/add-a-system-token-as-a-link-in-an-email)アプローチを使用して「viewAsWebpageLink」システムトークンを追加する場合、`tokens` を使用して上書きすることはできません。代わりに、[メールにWeb ページとして表示リンクを追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/add-a-view-as-web-page-link-to-an-email)アプローチを使用すれば、`tokens` を使用して「viewAsWebPageLink」を上書きできます。

`leads` パラメーターと `tokens` パラメーターは、リクエスト本文で application/json として渡されます。

```
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

[スマートキャンペーンをアクティブ化](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/activateSmartCampaignUsingPOST)エンドポイントは簡単です。`id` パスパラメーターは必須です。アクティブ化を成功させるには、キャンペーンに対して次の条件を満たす必要があります。

- 非アクティブ化する必要があります。
- 1 つ以上のトリガーと 1 つのフローステップが必要です。
- エラーのないトリガー、フィルター、フローステップが必要です。

```
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

[スマートキャンペーンの非アクティブ化](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/deactivateSmartCampaignUsingPOST)は簡単です。`id` パスパラメーターは必須です。非アクティブ化を成功させるには、キャンペーンをアクティブ化する必要があります。

```
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
