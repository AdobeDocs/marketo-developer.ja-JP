---
title: 静的リスト
feature: REST API, Static Lists
description: 静的リストに対して CRUD 操作を実行します。
exl-id: 20679fd2-fae2-473e-84bc-cb4fdf2f5151
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# 静的リスト

[ 静的リストエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists)

[ リストメンバーシップエンドポイントの参照 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)

Marketoは、静的リストに対して CRUD 操作を実行するための一連の REST API を提供します。 これらの API は、クエリ、作成、更新、削除のオプションを提供するアセット API の標準インターフェイスパターンに従います。

## クエリ

静的リストのクエリは、[by id](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET)、[by name](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET) および [browse](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET) のアセットに対する標準のクエリタイプに従います。

### Id 別

[ID でクエリ ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET) は、単一の静的リストレコードをパスパラメーターとして受け取 `id`、単一の静的リストレコードを返します。

```
GET /rest/asset/v1/staticList/{id}.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "843c#1641f969e96",
    "result": [
        {
            "id": 1021,
            "name": "Foundation Seed List",
            "createdAt": "2017-07-27T01:38:33Z+0000",
            "updatedAt": "2017-07-27T01:39:26Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1021A1"
        }
    ]
}
```

#### 名前別

[ 名前でクエリ ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET) は、静的リスト `name` をパラメーターとして受け取り、単一の静的リストレコードを返します。 完全な文字列一致は、インスタンス内のすべての静的リスト名に対して実行され、その名前に一致する静的リストの結果を返します。

```
GET /rest/asset/v1/staticList/byName.json?name=Foundation Seed List
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "28ab#1641fa246b9",
    "result": [
        {
            "id": 1021,
            "name": "Foundation Seed List",
            "createdAt": "2017-07-27T01:38:33Z+0000",
            "updatedAt": "2017-07-27T01:39:26Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1021A1"
        }
    ]
}
```

#### 参照

静的リストは [ バッチで取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET) することもできます。 `folder` パラメーターを使用すると、クエリを実行する親フォルダーを指定でき、ID とタイプを含む JSON オブジェクトとしてフォーマットされます。 他の一括アセット取得エンドポイントと同様に、`offset` および `maxReturn` は、ページングに使用できるオプションのパラメーターです。 `earliestUpdatedAt` パラメーターおよび `latestUpdatedAt` パラメーターを使用すると、指定された範囲内で作成または更新された静的リストを返すための低日時透かしおよび高日時透かしを設定できます。 日時の値は、有効な ISO-8601 文字列である必要があり、ミリ秒を含めることはできません

```
GET /rest/asset/v1/staticLists.json?folder={"id":13,"type":"Folder"}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "2dc0#1641f846633",
    "result": [
        {
            "id": 1021,
            "name": "Foundation Seed List",
            "createdAt": "2017-07-27T01:38:33Z+0000",
            "updatedAt": "2017-07-27T01:39:26Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1021A1"
        },
        {
            "id": 1022,
            "name": "Blacklist Seed List",
            "createdAt": "2017-07-27T23:19:33Z+0000",
            "updatedAt": "2017-07-27T23:21:29Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1022A1"
        },
        {
            "id": 1023,
            "name": "Possible Duplicates Seed List",
            "createdAt": "2017-07-28T00:10:02Z+0000",
            "updatedAt": "2017-07-28T00:11:22Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1023A1"
        }
    ]
}
```

## 作成と更新

[ 静的リストの作成 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/createStaticListUsingPOST) は、2 つの必須パラメーターを持つ application/x-www-form-urlencoded POSTを使用して実行されます。 `folder` パラメーターは、静的リストが作成される親フォルダーを指定するために使用され、ID とタイプを含む JSON オブジェクトとしてフォーマットされます。 `name` パラメーターは、静的リストに名前を付けるために使用され、一意である必要があります。 オプションで、`description` パラメーターを使用して静的リストを記述できます。

```
POST /rest/asset/v1/staticLists.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
folder={"id":1034,"type":"Program"}&name=My Static List
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "1269d#164209d6e1e",
    "result": [
        {
            "id": 1027,
            "name": "My Static List",
            "createdAt": "2018-06-21T04:32:25Z+0000",
            "updatedAt": "2018-06-21T04:32:25Z+0000",
            "folder": {
                "id": 1034,
                "type": "Program"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1027A1"
        }
    ]
}
```

[ 静的リストの更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/updateStaticListUsingPOST) は、2 つのオプションパラメーターを持つ別のエンドポイントを通じて行われます。 `description` パラメーターを使用すると、静的リストの説明を更新できます。 `name` パラメーターは、静的リスト名の更新に使用でき、一意である必要があります。

```
POST /rest/asset/v1/staticList/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
description=This is a static list used for testing
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "f84f#16420b4c746",
    "result": [
        {
            "id": 1027,
            "name": "My Static List",
            "description": "This is a static list used for testing",
            "createdAt": "2018-06-21T04:32:26Z+0000",
            "updatedAt": "2018-06-21T04:57:55Z+0000",
            "folder": {
                "id": 1034,
                "type": "Program"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1027A1"
        }
    ]
}
```

### 削除

[ 静的リストの削除 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/deleteStaticListByIdUsingPOST) は、単一の静的リスト `id` をパスパラメーターとして受け取ります。 インポートまたはエクスポート操作で使用されている静的リスト、または他のアセットで使用されている静的リストには削除を実行できません。

```
POST /rest/asset/v1/staticList/{id}/delete.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "2c79#16420ded0e9",
    "result": [
        {
            "id": 1027
        }
    ]
}
```

## List Membership

リスト メンバシップ エンドポイントは、静的リスト メンバの追加、削除、およびクエリを実行する機能を提供します。 また、静的なリストメンバーシップに対してクエリを実行することもできます。

### リストに追加

[ リストに追加 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/addLeadsToListUsingPOST) エンドポイントを使用して、1 つ以上のメンバーをリストに追加します。 このエンドポイントは、必須の `listId` パスパラメーターと、リード ID を含む 1 つ以上の ID クエリパラメーター（最大許容値は 300）を受け取ります。

応答には、リクエストで指定された各リード ID のステータスを持つ JSON オブジェクトで構成される `result` 配列が含まれています。

```
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

### リストから削除

[ リストから削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/removeLeadsFromListUsingDELETE) エンドポイントは、リストから 1 つ以上のメンバーを削除するために使用します。 このエンドポイントは、必須の `listId` パスパラメーターと、リード ID を含む 1 つ以上の `id` クエリパラメーター（最大許容値は 300）を受け取ります。

応答には、リクエストで指定された各リード ID のステータスを持つ JSON オブジェクトで構成される `result` 配列が含まれています。

```
DELETE /rest/v1/lists/{listId}/leads.json?id=318603&id=318595&id=999999
```

```
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

### クエリリスト

[ リスト ID でリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/getLeadsByListIdUsingGET) エンドポイントは、リストのメンバーを取得するために使用されます。 エンドポイントは必須の `listId` パスパラメーターを受け取り、オプションで複数のクエリパラメーターを使用してフィルタリング条件を指定できます。

`batchSize` パラメーターは、1 回の呼び出しで返されるリードレコードの数を指定するために使用されます（デフォルトは最大 300）。

`nextPageToken` パラメーターは、大きな結果セットをページ分割するために使用されます。 このパラメーターは、最初の呼び出しでは渡されず、後続のページネーションの呼び出しでのみ渡されます。

`fields` パラメーターには、応答で返されるフィールド名のコンマ区切りリストが含まれます。 fields パラメーターがこのリクエストに含まれていない場合は、デフォルトのフィールド email、updatedAt、createdAt、lastName、firstName、id が返されます。

応答には、リクエストで指定されたリードフィールドを含む JSON オブジェクトで構成される `result` 配列が含まれています。

```
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

#### リード Id 別のクエリリストメンバーシップ

[ リストのメンバー ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/areLeadsMemberOfListUsingGET) エンドポイントは、1 人以上のリードがリストのメンバーであるかどうかを確認するために使用されます。 このエンドポイントは、必須の `listId` パスパラメーターと、リード ID を含む 1 つ以上の `id` クエリパラメーター（最大許容値は 300）を受け取ります。

応答には、リクエストで指定された各リード ID のステータスを持つ JSON オブジェクトで構成される `result` 配列が含まれています。

```
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
