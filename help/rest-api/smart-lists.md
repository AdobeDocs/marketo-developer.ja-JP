---
title: 「スマート・リスト」
feature: REST API
description: 「スマートリストの作成と編集。」
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 1%

---


# スマートリスト

[スマート リスト エンドポイント リファレンス](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists)

Marketoは、スマートリストで操作を実行するための一連の REST API を備えています。 これらの API は、クエリ、削除、複製のオプションを提供するアセット API の標準インターフェイスパターンに従います。

メモ：これらの API は、ユーザー作成のスマートリストでのみサポートされます。 以下に使用することはできません [組み込み/システムのスマートリスト](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/using-smart-lists/use-built-in-system-smart-lists).

## クエリ

スマート・リストのクエリーは、次のアセットの標準クエリー・タイプに従います [id 別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByIdUsingGET), [名前別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET)、および [参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListsUsingGET).

### Id 別

[ID でクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByIdUsingGET) 単一のスマートリストを取得 `id` をパスパラメーターとして使用し、単一のスマートリストレコードを返します。 オプションで、 `includeRules` ブール・パラメータを指定して、スマート・リスト・ルールを応答に含めます。

![スマートリストルール](assets/smartlist-rules.png)

```
GET /rest/asset/v1/smartList/{id}.json?includeRules=true
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6efc#16c8967a21f",
    "warnings": [],
    "result": [
        {
            "id": 4363,
            "name": "Smart List Test 01",
            "createdAt": "2019-06-03T23:01:13Z+0000",
            "updatedAt": "2019-06-04T17:37:45Z+0000",
            "url": "https://app-sjqe.marketo.com/#SL4363A1LA1",
            "folder": {
                "id": 1041,
                "type": "Program"
            },
            "workspace": "Default",
            "rules": {
                "filterMatchType": "all",
                "triggers": [],
                "filters": [
                    {
                        "id": 459,
                        "name": "Visited Web Page",
                        "ruleTypeId": 1,
                        "ruleType": "Activity",
                        "operator": "occurs",
                        "conditions": [
                            {
                                "activityAttributeId": 1,
                                "activityAttributeName": "Web Page",
                                "operator": "is",
                                "values": [
                                    "Program Test.Landing Page Test 01"
                                ],
                                "isPrimary": true
                            },
                            {
                                "activityAttributeId": 6,
                                "activityAttributeName": "Browser",
                                "operator": "is",
                                "values": [
                                    "Chrome"
                                ],
                                "isPrimary": false
                            },
                            {
                                "activityAttributeId": -101,
                                "activityAttributeName": "Date of Activity",
                                "operator": "in past",
                                "values": [
                                    "30 days"
                                ],
                                "isPrimary": false
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```

### スマートキャンペーン Id 別

[スマートキャンペーン ID でクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getSmartListBySmartCampaignIdUsingGET) 単一のスマートキャンペーンを実行 `id` をパスパラメーターとして使用し、単一のスマートリストレコードを返します。 オプションで、 `includeRules` ブール・パラメータを指定して、スマート・リスト・ルールを応答に含めます。

```
GET /rest/asset/v1/smartCampaign/{smartCampaignId}/smartList.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6efc#16c8967a21f",
    "warnings": [],
    "result": [
        {
            "id": 4363,
            "name": "Smart List Test 01",
            "createdAt": "2019-06-03T23:01:13Z+0000",
            "updatedAt": "2019-06-04T17:37:45Z+0000",
            "url": "https://app-sjqe.marketo.com/#SL4363A1LA1",
            "folder": {
                "id": 1041,
                "type": "Program"
            },
            "workspace": "Default"
         }
    ]
}
```

### プログラム Id 別

[プログラム ID でクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getSmartListByProgramIdUsingGET) 1 つの電子メールプログラムを使用 `id` をパスパラメーターとして使用し、単一のスマートリストレコードを返します。 オプションで、 `includeRules` ブール・パラメータを指定して、スマート・リスト・ルールを応答に含めます。

```
GET /rest/asset/v1/program/{programId}/smartList.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6efc#16c8967a21f",
    "warnings": [],
    "result": [
        {
            "id": 4363,
            "name": "Smart List Test 01",
            "createdAt": "2019-06-03T23:01:13Z+0000",
            "updatedAt": "2019-06-04T17:37:45Z+0000",
            "url": "https://app-sjqe.marketo.com/#SL4363A1LA1",
            "folder": {
                "id": 1041,
                "type": "Program"
            },
            "workspace": "Default"
         }
    ]
}
```

### 名前別

[名前でクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET) スマートリストを取得 `name` パラメーターとして指定し、単一のスマートリストレコードを返します。  完全一致文字列は、インスタンス内のすべてのスマートリスト名に対して実行され、その名前に一致するスマートリストの結果を返します。

```
GET /rest/asset/v1/smartList/byName.json?name=2018 Leads
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "115d7#16423bc13b4",
    "result": [
        {
            "id": 283988,
            "name": "2018 Leads",
            "createdAt": "2008-10-07T15:20:39Z+0000",
            "updatedAt": "2010-04-13T15:34:32Z+0000",
            "url": "https://app-abm.marketo.com/#SL283988A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        }
    ]
}
```

### 参照

スマート・リストは、次の場合にも使用できます [バッチで取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListsUsingGET). この `folder` パラメーターは、クエリを実行する親フォルダーを指定するために使用されます。 次を含む JSON オブジェクトとしてフォーマットされます `id` および `type`. 他の一括アセット取得エンドポイントと同様、 `offset` および `maxReturn` は、ページングに使用できるオプションのパラメーターです。 オプション `earliestUpdatedAt` および `latestUpdatedAt` datetime パラメーターを使用すると、UpdatedAt の日付範囲で結果をフィルタリングできます。

```
GET /rest/asset/v1/smartLists.json?folder={"id":31,"type":"Folder"}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "9aa4#16423c0e969",
    "result": [
        {
            "id": 283988,
            "name": "2018 Leads",
            "createdAt": "2008-10-07T15:20:39Z+0000",
            "updatedAt": "2010-04-13T15:34:32Z+0000",
            "url": "https://app-abm.marketo.com/#SL283988A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        },
        {
            "id": 299697,
            "name": "Active Prospects",
            "createdAt": "2008-10-17T02:09:49Z+0000",
            "updatedAt": "2010-03-27T18:27:46Z+0000",
            "url": "https://app-abm.marketo.com/#SL299697A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        },
        {
            "id": 400517,
            "name": "Leads by Score",
            "createdAt": "2009-01-07T18:52:52Z+0000",
            "updatedAt": "2010-04-13T15:36:09Z+0000",
            "url": "https://app-abm.marketo.com/#SL400517A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        }
    ]
}
```

## 複製

[スマート・リストのクローニング](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/cloneSmartListUsingPOST) は、application/x-www-form-urlencoded POSTで実行されます。 複製するスマートリストは、で指定します。 `id` パスパラメーター。 この `folder` パラメーターは、スマートリストを作成する親フォルダーを指定するために使用され、ID とタイプを含む JSON オブジェクトとしてフォーマットされます。 親フォルダは、プログラムまたはスマート・リスト・フォルダのいずれかである必要があります。 この `name` パラメーターは、新しいスマートリストに名前を付けるために使用され、一意である必要があります。 オプションで、 `description` パラメーターを使用して、スマートリストを記述できます。

```
POST /rest/asset/v1/smartList/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
folder={"id":31,"type":"Folder"}&name=2018 Leads Qualified
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "a672#16423d755ed",
    "result": [
        {
            "id": 788645,
            "name": "2018 Leads Qualified",
            "createdAt": "2018-06-21T19:34:32Z+0000",
            "updatedAt": "2018-06-21T19:34:32Z+0000",
            "url": "https://app-abm.marketo.com/#SL788645A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        }
    ]
}
```

## 削除

[スマート・リストの削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/deleteSmartListByIdUsingPOST) 単一のスマートリストを取得 `id` パスパラメーターとして使用します。

```
POST /rest/asset/v1/smartList/{id}/delete.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "8f5#16423dd0fbe",
    "result": [
        {
            "id": 788645
        }
    ]
}
```
