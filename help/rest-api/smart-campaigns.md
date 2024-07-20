---
title: スマートキャンペーン
feature: REST API, Smart Campaigns
description: スマートキャンペーンの概要
exl-id: 540bdf59-b102-4081-a3d7-225494a19fdd
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 1%

---

# スマートキャンペーン

[ スマートキャンペーンエンドポイント参照（アセット） ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns)

[ キャンペーンエンドポイント参照（リード） ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns)

Marketoは、スマートキャンペーンで操作を実行するための一連の REST API を備えています。 これらの API は、クエリ、作成、複製、削除のオプションを提供するアセット API の標準インターフェイスパターンに従います。 また、バッチキャンペーンをスケジュールしたり、トリガーキャンペーンをリクエストしたりして、スマートキャンペーンの実行を管理することもできます。

## クエリ

スマートキャンペーンのクエリは、[ID 別 ](#by_id)、[ 名前別 ](#by_name) および [ ブラウジング ](#browse) のアセットに対する標準のクエリタイプに従います。

### Id 別

[ID によるスマートキャンペーンの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getSmartCampaignByIdUsingGET) エンドポイントは、単一のスマートキャンペーン `id` をパスパラメーターとして受け取り、単一のスマートキャンペーンレコードを返します。

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

[ 名前によるスマートキャンペーンの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getSmartCampaignByNameUsingGET) エンドポイントは、単一のスマートキャンペーン `name` をパラメーターとして受け取り、単一のスマートキャンペーンレコードを返します。

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

[ スマートキャンペーンを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getAllSmartCampaignsGET) エンドポイントは、他の Asset API 参照エンドポイントと同様に機能し、オプションで複数のクエリパラメーターでフィルタリング条件を指定できます。

`earliestUpdatedAt` パラメーターと `latestUpdatedAt` パラメーターは、ISO-8601 形式（ミリ秒単位なし）で `datetimes` を受け付けます。 両方が設定されている場合は、earliestUpdatedAt が latestUpdatedAt の前に置かれる必要があります。

`folder` パラメーターは、参照する親フォルダーを指定します。 形式は、`id` 属性と `type` 属性を含む JSON ブロックです。

`maxReturn` パラメーターは、返されるエントリの最大数を指定する整数です。 デフォルトは 20 です。 最大値は 200 です。

`offset` パラメーターは、エントリの取得を開始する場所を指定する整数です。 `maxReturn` と共に使用できます。 デフォルトは 0 です。

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

このエンドポイントを使用すると、`result` の配列に 1 つ以上のレコードが含まれます。

## 作成

[ スマートキャンペーンを作成 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/createSmartCampaignUsingPOST) エンドポイントは、2 つの必須パラメーターを持つ application/x-www-form-urlencoded POSTで実行されます。 `name` パラメーターは、作成するスマートキャンペーンの名前を指定します。 `folder` パラメーターは、スマートキャンペーンが作成される親フォルダーを指定します。 形式は、`id` 属性と `type` 属性を含む JSON ブロックです。

オプションで、`description` パラメーター（最大 2,000 文字）を使用してスマートキャンペーンを記述できます。

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

[ スマートキャンペーンを更新 ](https://developer.adobe.com/marketo-apis/api/asset/) エンドポイントは、application/x-www-form-urlencoded POSTを使用して実行されます。 単一のスマートキャンペーン `id` をパスパラメーターとして受け取ります。 `name` パラメーターを使用してスマートキャンペーンの名前を更新するか、`description` パラメーターを使用してスマートキャンペーンの説明を更新できます。

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

[ クローンスマートキャンペーン ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) エンドポイントは、3 つの必須パラメーターを持つ application/x-www-form-urlencoded POSTで実行されます。 複製するスマートキャンペーンを指定する `id` パラメーター、新しいスマートキャンペーンの名前を指定する `name` パラメーター、新しいスマートキャンペーンが作成される親フォルダーを指定する `folder` パラメーターが必要です。 形式は、`id` 属性と `type` 属性を含む JSON ブロックです。

オプションで、`description` パラメーター（最大 2,000 文字）を使用してスマートキャンペーンを記述できます。

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

[ スマートキャンペーンを削除 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/deleteSmartCampaignUsingPOST) エンドポイントは、単一のスマートキャンペーン `id` をパスパラメーターとして受け取ります。

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

スマートキャンペーンを特定の時間にバッチ開始すると、特定のリードセットにすべて一度に影響します。

## スケジュール

[ キャンペーンのスケジュール ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns/operation/scheduleCampaignUsingPOST) エンドポイントを使用して、バッチキャンペーンがすぐに実行されるか後日に実行されるようにスケジュールします。 キャンペーン `id` は必須のパスパラメーターです。 オプションのパラメーターは、application/json としてリクエスト本文に渡される `tokens`、`runAt`、`cloneToProgram` です。

tokens 配列パラメーターは、既存のプログラムトークンを上書きするマイトークンの配列です。 キャンペーンの実行後、トークンは破棄されます。  各トークン配列項目には、名前と値のペアが含まれます。 トークン名は、「{{my.name}}」の形式にする必要があります。

runAt datetime パラメーターは、キャンペーンを実行するタイミングを指定します。 指定しない場合、キャンペーンは、エンドポイントが呼び出されてから 5 分後に実行されます。 datetime 値は 2 年以上先にする必要があります。

この API でスケジュールされたキャンペーンは、常に最低 5 分待ってから実行されます。

`cloneToProgram` 文字列パラメーターには、結果のプログラムの名前が含まれます。  設定すると、キャンペーン、親プログラム、そのすべてのアセットが、結果として生成される新しい名前で作成されます。 親プログラムのクローンが作成され、新しく作成されたキャンペーンがスケジュールされます。 結果のプログラムは親の下に作成されます。 スニペット、プッシュ通知、アプリ内メッセージ、静的リスト、レポート、ソーシャルアセットを含むプログラムは、この方法では複製できません。 使用する場合、このエンドポイントは 1 日あたり 20 回の呼び出しに制限されます。 [ クローンプログラム ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) エンドポイントを使用することをお勧めします。

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

トリガースマートキャンペーンは、トリガーされたイベントに基づいて、一度に 1 人のユーザーに影響を与えます。

### リクエスト

[ リクエストキャンペーン ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns/operation/triggerCampaignUsingPOST) エンドポイントを使用して、一連のリードをトリガーのキャンペーンに渡し、キャンペーンのフローを通じて実行します。 キャンペーンには、「Web サービス API」をソースとする「キャンペーンはリクエストされました」トリガーが必要です。

このエンドポイントには、パスパラメーターとして campaign `id` と、リード ID を含む `leads` の整数配列パラメーターが必要です。 1 回の呼び出しでは最大 100 件のリードを使用できます。

オプションで、`tokens` 配列パラメーターを使用して、キャンペーンの親プログラムに対してローカルのマイトークンを上書きできます。 `tokens` は最大 100 個のトークンを受け入れます。 各 `tokens` 配列項目には、名前と値のペアが含まれます。 トークン名は、「{{my.name}}」の形式にする必要があります。 [ システムトークンをメール内のリンクとして追加 ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/using-tokens/add-a-system-token-as-a-link-in-an-email) を使用して「viewAsWebpageLink」システムトークンを追加するアプローチを使用する場合、`tokens` を使用して上書きすることはできません。 代わりに、`tokens` を使用して「viewAsWebPageLink」を上書きできる [ メールに web ページリンクとして表示を追加 ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/add-a-view-as-web-page-link-to-an-email) アプローチを使用します。

`leads` パラメーターと `tokens` パラメーターは、application/json としてリクエスト本文に渡されます。

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

[ スマートキャンペーンのアクティブ化 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/activateSmartCampaignUsingPOST) エンドポイントは簡単です。 `id` パス パラメーターが必要です。 アクティベーションを成功させるには、キャンペーンに対して次の条件を満たす必要があります。

- 非アクティブ化する必要があります
- 少なくとも 1 つのトリガーと 1 つのフローステップが必要です
- エラーのないトリガー、フィルターおよびフローステップが必要です

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

### 無効化

[ スマートキャンペーンの非アクティブ化 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/deactivateSmartCampaignUsingPOST) は簡単です。 `id` パス パラメーターが必要です。 非アクティブ化を成功させるには、キャンペーンをアクティブ化する必要があります。

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
