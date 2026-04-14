---
title: リストメンバーシップ（静的リスト）
feature: REST API, Static Lists
description: Marketo Lead Database REST APIを使用して、リードを静的リストに追加し、リードを削除し、リストメンバーを取得し、リストメンバーシップを確認します。
exl-id: b8f74bcf-834a-44db-81fd-621048afeba4
source-git-commit: 59684e1c5a8082ad12f1e4bfc854c0d2dde35d2a
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 54%

---

# リストメンバーシップ（静的リスト）

[リスト メンバーシップ エンドポイント リファレンス](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists)

リストメンバーシップ APIは、静的リストメンバーを操作するためのリードデータベースエンドポイントを提供します。 これらのエンドポイントを使用すると、リストにリードを追加したり、リストからリードを削除したり、リストのメンバーを取得したり、1つ以上のリードがリストのメンバーであるかどうかを判断したりできます。

## エンドポイント

| エンドポイント | メソッド | パス |
| --- | --- | --- |
| リストに追加 | POST | `/rest/v1/lists/{listId}/leads.json` |
| リストから削除 | DELETE | `/rest/v1/lists/{listId}/leads.json` |
| リスト ID によるリードを取得 | GET | `/rest/v1/lists/{listId}/leads.json` |
| リストのメンバー | GET | `/rest/v1/lists/{listId}/leads/ismember.json` |

## リストに追加

リストに追加[ リストに追加](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/addLeadsToListUsingPOST) エンドポイントは、1人以上のメンバーをリストに追加するために使用されます。 エンドポイントは、必須の `listId` パスパラメーターと、リード ID を含む 1 つ以上の `id` クエリパラメーター（最大許容値は 300）を受け取ります。

応答には、リクエストで指定した各リード ID のステータスを含む JSON オブジェクトで構成された `result` 配列が含まれます。

```http
POST /rest/v1/lists/{listId}/leads.json?id=318594&id=318595
```

```json
{
    "requestId": "6860#1706170ba29",
    "result": [
        {
            "id": 318594,
            "status": "added"
        },
        {
            "id": 318595,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1004",
                    "message": "Lead not found"
                }
            ]
        }
    ],
    "success": true
}
```

## リストから削除

リストから削除[ リストから削除](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/removeLeadsFromListUsingDELETE) エンドポイントは、リストから1人以上のメンバーを削除するために使用されます。 エンドポイントは、必須の `listId` パスパラメーターと、リード ID を含む 1 つ以上の `id` クエリパラメーター（最大許容値は 300）を受け取ります。

応答には、リクエストで指定した各リード ID のステータスを含む JSON オブジェクトで構成された `result` 配列が含まれます。

```http
DELETE /rest/v1/lists/{listId}/leads.json?id=318603&id=318595&id=999999
```

```json
{
    "requestId": "9e79#17061689ac3",
    "result": [
        {
            "id": 318603,
            "status": "removed"
        },
        {
            "id": 318595,
            "status": "removed"
        },
        {
            "id": 999999,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1004",
                    "message": "Lead not found"
                }
            ]
        }
    ],
    "success": true
}
```

## リスト ID によるリードを取得

[リスト ID によるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/getLeadsByListIdUsingGET)エンドポイントは、リストのメンバーを取得するのに使用されます。 エンドポイントは、必須の `listId` パスパラメーターを受け取り、フィルタリング条件を指定するのにオプションで複数のクエリパラメーターを許可します。

`batchSize` パラメーターは、1回の呼び出しで返されるリード レコードの数を指定するために使用されます。 デフォルトと最大値は300です。

`nextPageToken` パラメーターは、大きな結果セットをページ分割するのに使用されます。 このパラメーターは、最初の呼び出しでは渡されませんが、ページネーションの後続の呼び出しでのみ渡されます。

`fields` パラメーターには、応答で返されるフィールド名のコンマ区切りのリストが含まれます。 `fields` パラメーターがこのリクエストに含まれていない場合、次のデフォルトフィールドが返されます：`email`、`updatedAt`、`createdAt`、`lastName`、`firstName`、および`id`。

応答には、リクエストで指定したリードフィールドを含む JSON オブジェクトで構成された `result` 配列が含まれます。

```http
GET /rest/v1/lists/{listId}/leads.json?batchSize=3
```

```json
{
    "requestId": "ddae#170615ba0cc",
    "result": [
        {
            "id": 318594,
            "firstName": "Hanna",
            "lastName": "Crawford",
            "email": "208161Robert.L.Deacon@pookmail.com",
            "updatedAt": "2015-04-06T17:13:50Z",
            "createdAt": "2015-04-06T17:13:50Z"
        },
        {
            "id": 318595,
            "firstName": "Bertha",
            "lastName": "Fulton",
            "email": "208160Tyrone.V.Dyer@trashymail.com",
            "updatedAt": "2015-04-06T17:13:50Z",
            "createdAt": "2015-04-06T17:13:50Z"
        },
        {
            "id": 318596,
            "firstName": "Faith",
            "lastName": "England",
            "email": "208159Rex.M.Bailey@dodgit.com",
            "updatedAt": "2015-04-06T17:13:50Z",
            "createdAt": "2015-04-06T17:13:50Z"
        }
    ],
    "success": true,
    "nextPageToken": "PS5VL5WD4UOWGOUCJR6VY7JQO24LC2U5DRBU4WO4RQMPHDHTK2T3BEZOR75VLQXYB3245WW2GMDSK==="
}
```

## リストのメンバー

[リストのメンバー](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/areLeadsMemberOfListUsingGET)エンドポイントは、1 つ以上のリードがリストのメンバーであるかどうかを確認するのに使用されます。 エンドポイントは、必須の `listId` パスパラメーターと、リード ID を含む 1 つ以上の `id` クエリパラメーター（最大許容値は 300）を受け取ります。

応答には、リクエストで指定した各リード ID のステータスを含む JSON オブジェクトで構成された `result` 配列が含まれます。

```http
GET /rest/v1/lists/{listId}/leads/ismember.json?id=309901&id=318603&id=999999
```

```json
{
    "requestId": "693a#17061475cf9",
    "result": [
        {
            "id": 309901,
            "status": "memberof"
        },
        {
            "id": 318603,
            "status": "notmemberof"
        },
        {
            "id": 999999,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1004",
                    "message": "Lead not found"
                }
            ]
        }
    ],
    "success": true
}
```
