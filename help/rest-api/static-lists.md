---
title: 静的リスト
feature: REST API, Static Lists
description: Marketo REST API を使用して、ID、名前、参照のエンドポイント、フォルダースコーピング、ページング、日付フィルターを含む、静的リストのクエリ、作成、更新、削除を行います。
exl-id: 20679fd2-fae2-473e-84bc-cb4fdf2f5151
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 96%

---

# 静的リスト

[静的リストエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists)

[リストメンバーシップエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)

Marketo は、静的リストで CRUD 操作を実行する一連の REST API を備えています。これらの API は、クエリ、作成、更新、削除のオプションを提供するアセット API の標準インターフェイスパターンに従います。

## クエリ

静的リストのクエリは、アセットに対する標準のクエリタイプ（[IDによるクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET)、[名前によるクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET)、および[参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET)）に従います。

### ID 別

[ID によるクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET)は、単一の静的リスト `id` をパスパラメーターとして受け取り、単一の静的リストレコードを返します。

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

[名前によるクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET)は、静的リスト `name` をパラメーターとして受け取り、単一の静的リストレコードを返します。 インスタンス内のすべての静的リスト名に対して正確な文字列一致検索が実行され、その名前に一致する静的リストの結果が返されます。

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

静的リストは、[バッチで取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET)することもできます。`folder` パラメーターは、クエリが実行される親フォルダーを指定するために使用でき、ID とタイプを含む JSON オブジェクトの形式で指定されます。他の一括アセット取得エンドポイントと同様に、`offset` と `maxReturn` はページングに使用できるオプションパラメーターです。`earliestUpdatedAt` および `latestUpdatedAt` パラメーターを使用すると、指定した範囲内で作成または更新された静的リストを返すための日時の日時透かし（低および高）を設定できます。日時値は、有効な ISO-8601 文字列にする必要があります。ミリ秒を含めないでください。

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

[静的リストの作成](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/createStaticListUsingPOST)は、2 つの必須パラメーターを含む application/x-www-form-urlencoded POST で実行されます。`folder` パラメーターは、静的リストが作成される親フォルダーを指定するために使用され、ID とタイプを含む JSON オブジェクトの形式で指定されます。`name` パラメーターは、静的リストに名前を付けるために使用され、一意である必要があります。オプションで、`description` パラメーターを使用して静的リストについて説明することもできます。

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

[静的リストの更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/updateStaticListUsingPOST)は、2 つのオプションパラメーターを持つ別のエンドポイントを通じて行われます。`description` パラメーターは、静的リストの説明を更新するために使用できます。`name` パラメーターは、静的リスト名を更新するために使用でき、一意である必要があります。

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

[静的リストの削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/deleteStaticListByIdUsingPOST)では、パスパラメーターとして単一の静的リスト `id` を受け取ります。読み込みまたは書き出し操作で使用されている静的リストや、他のアセットで使用されている静的リストは削除できません。

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

## リストメンバーシップ

リストメンバーシップエンドポイントは、静的リストメンバーの追加、削除、クエリを実行する機能を提供します。また、静的リストメンバーシップに対してクエリを実行することもできます。

### リストに追加

[リストに追加](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/addLeadsToListUsingPOST)エンドポイントは、リストに 1 人以上のメンバーを追加するのに使用されます。エンドポイントは、必須の `listId` パスパラメーターと、リード ID を含む 1 つ以上の id クエリパラメーター（最大許容値は 300）を受け取ります。

応答には、リクエストで指定した各リード ID のステータスを含む JSON オブジェクトで構成された `result` 配列が含まれます。

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

[リストから削除](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/removeLeadsFromListUsingDELETE)エンドポイントは、リストから 1 人以上のメンバーを削除するのに使用されます。エンドポイントは、必須の `listId` パスパラメーターと、リード ID を含む 1 つ以上の `id` クエリパラメーター（最大許容値は 300）を受け取ります。

応答には、リクエストで指定した各リード ID のステータスを含む JSON オブジェクトで構成された `result` 配列が含まれます。

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

### リストのクエリの実行

[リスト ID によるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/getLeadsByListIdUsingGET)エンドポイントは、リストのメンバーを取得するのに使用されます。エンドポイントは、必須の `listId` パスパラメーターを受け取り、フィルタリング条件を指定するのにオプションで複数のクエリパラメーターを許可します。

`batchSize` パラメーターは、1 回の呼び出しで返されるリードレコードの数を指定するのに使用されます（デフォルトおよび最大は 300）。

`nextPageToken` パラメーターは、大きな結果セットをページ分割するのに使用されます。このパラメーターは、最初の呼び出しでは渡されず、ページネーションの後続の呼び出しでのみ渡されます。

`fields` パラメーターには、応答で返されるフィールド名のコンマ区切りのリストが含まれます。このリクエストに fields パラメーターが含まれていない場合、email、updatedAt、createdAt、lastName、firstName、id のデフォルトフィールドが返されます。

応答には、リクエストで指定したリードフィールドを含む JSON オブジェクトで構成された `result` 配列が含まれます。

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

#### リード ID によるリストメンバーシップのクエリの実行

[リストのメンバー](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/areLeadsMemberOfListUsingGET)エンドポイントは、1 つ以上のリードがリストのメンバーであるかどうかを確認するのに使用されます。エンドポイントは、必須の `listId` パスパラメーターと、リード ID を含む 1 つ以上の `id` クエリパラメーター（最大許容値は 300）を受け取ります。

応答には、リクエストで指定した各リード ID のステータスを含む JSON オブジェクトで構成された `result` 配列が含まれます。

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
