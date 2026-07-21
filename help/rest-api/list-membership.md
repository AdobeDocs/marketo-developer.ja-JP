---
title: リストメンバーシップ（静的リスト）
feature: REST API, Static Lists
description: Marketo Lead Database REST APIを使用して、リードを静的リストに追加し、リードを削除し、リストメンバーを取得し、リストメンバーシップを確認します。
exl-id: b8f74bcf-834a-44db-81fd-621048afeba4
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 8%

---

# リストメンバーシップ（静的リスト）

[リスト メンバーシップ エンドポイント リファレンス](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists)

リストメンバーシップ APIは、静的リストメンバーを管理するためのリードデータベースエンドポイントを提供します。 これらのエンドポイントを使用して、以下を行います。

- リストにリードを追加します。
- リストからリードを削除します。
- リストのメンバーを取得します。
- リードがリストに含まれているかどうかを判断します。

## エンドポイント

| エンドポイント | メソッド | パス |
| --- | --- | --- |
| リストに追加 | POST | `/rest/v1/lists/{listId}/leads.json` |
| リストから削除 | DELETE | `/rest/v1/lists/{listId}/leads.json` |
| リスト ID によるリードを取得 | GET | `/rest/v1/lists/{listId}/leads.json` |
| リストのメンバー | GET | `/rest/v1/lists/{listId}/leads/ismember.json` |

## リストに追加

リストに追加[ リストに追加](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/addLeadsToListUsingPOST) エンドポイントを使用して、1人以上のメンバーをリストに追加します。 必要な`listId` パスパラメーターと、リード IDを含む1つ以上の`id` クエリパラメーターを渡します。 リード IDの最大数は300です。

応答には、リクエスト内の各リード IDのステータスを含む`result`配列が含まれています。

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

リストから[ リストから削除](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/removeLeadsFromListUsingDELETE) エンドポイントを使用して、1人以上のメンバーをリストから削除します。 必要な`listId` パスパラメーターと、リード IDを含む1つ以上の`id` クエリパラメーターを渡します。 リード IDの最大数は300です。

応答には、リクエスト内の各リード IDのステータスを含む`result`配列が含まれています。

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

リスト ID ](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/getLeadsByListIdUsingGET)でリードを取得エンドポイントを使用して、リストのメンバーを取得します。 [必要な`listId` パスパラメーターを渡します。 オプションのクエリパラメーターを渡して、フィルタリング条件を指定することもできます。

オプションのクエリパラメーターは次のとおりです。

- `batchSize`: 1回の呼び出しで返されるリード レコードの数を指定します。 デフォルト値と最大値は300です。
- `nextPageToken`：大きな結果セットでページ化します。 このパラメーターを最初の呼び出しから省略し、後続の呼び出しに含めます。
- `fields`：返すフィールド名のコンマ区切りリストを指定します。 このパラメーターを省略すると、応答には`email`、`updatedAt`、`createdAt`、`lastName`、`firstName`および`id`が含まれます。

応答には、リクエストで指定されたリードフィールドを含む`result`配列が含まれています。

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

リストの[ メンバー](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/areLeadsMemberOfListUsingGET) エンドポイントを使用して、1つ以上のリードがリストのメンバーであるかどうかを判断します。 必要な`listId` パスパラメーターと、リード IDを含む1つ以上の`id` クエリパラメーターを渡します。 リード IDの最大数は300です。

応答には、リクエスト内の各リード IDのステータスを含む`result`配列が含まれています。

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
