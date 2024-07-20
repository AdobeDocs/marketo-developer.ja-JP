---
title: スマートリスト
feature: REST API
description: スマート・リストを作成および編集します。
exl-id: 4ba37e57-ee56-48c3-bb2b-b4ec8e907911
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 1%

---

# スマートリスト

[ スマートリストエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists)

Marketoは、スマートリストで操作を実行するための一連の REST API を備えています。 これらの API は、クエリ、削除、複製のオプションを提供するアセット API の標準インターフェイスパターンに従います。

メモ：これらの API は、ユーザー作成のスマートリストでのみサポートされます。 [ 組み込み/システムのスマートリスト ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/using-smart-lists/use-built-in-system-smart-lists) には使用できません。

## クエリ

スマートリストのクエリは、[id 別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByIdUsingGET)、[ 名前 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET) および [ 参照 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListsUsingGET) のアセットに対する標準のクエリタイプに従います。

### Id 別

[ID でクエリ ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByIdUsingGET) は、単一のスマート リスト `id` をパス パラメーターとして受け取り、単一のスマート リスト レコードを返します。 オプションで、`includeRules` のブール値パラメーターを渡して、応答にスマートリストルールを含めることもできます。

![ スマートリストルール ](assets/smartlist-rules.png)

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

[ スマートキャンペーン ID でクエリ ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getSmartListBySmartCampaignIdUsingGET) 単一のスマートキャンペーン `id` をパスパラメーターとして受け取り、単一のスマートリストレコードを返します。 オプションで、`includeRules` のブール値パラメーターを渡して、応答にスマートリストルールを含めることもできます。

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

[ プログラム ID でクエリ ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getSmartListByProgramIdUsingGET) は、1 つの電子メールプログラム `id` をパスパラメーターとして受け取り、1 つのスマートリストレコードを返します。 オプションで、`includeRules` のブール値パラメーターを渡して、応答にスマートリストルールを含めることもできます。

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

[ 名前によるクエリ ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET) は、スマート・リスト・レコードをパラメータとして受け取り、単一のスマート・リスト・`name` コードを返します。  完全一致文字列は、インスタンス内のすべてのスマートリスト名に対して実行され、その名前に一致するスマートリストの結果を返します。

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

スマート・リストは [ バッチで取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListsUsingGET) することもできます。 `folder` パラメーターは、クエリの実行対象となる親フォルダーを指定するために使用されます。 `id` と `type` を含む JSON オブジェクトとしてフォーマットされています。 他の一括アセット取得エンドポイントと同様に、`offset` および `maxReturn` は、ページングに使用できるオプションのパラメーターです。 オプションの `earliestUpdatedAt` および `latestUpdatedAt` の datetime パラメーターを使用して、UpdatedAt の日付範囲で結果をフィルタリングできます。

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

[ スマート・リストのクローニング ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/cloneSmartListUsingPOST) は、application/x-www-form-urlencodedPOSTを使用して実行されます。 複製するスマートリストは、`id` のパスパラメーターで指定します。 `folder` パラメーターは、スマートリストを作成する親フォルダーを指定するために使用され、ID とタイプを含む JSON オブジェクトとしてフォーマットされます。 親フォルダは、プログラムまたはスマート・リスト・フォルダのいずれかである必要があります。 `name` パラメーターは、新しいスマート リストに名前を付けるために使用され、一意である必要があります。 必要に応じて、`description` パラメーターを使用してスマートリストを記述できます。

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

[ スマートリストの削除 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/deleteSmartListByIdUsingPOST) では、単一のスマートリスト `id` がパスパラメーターとして使用されます。

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
