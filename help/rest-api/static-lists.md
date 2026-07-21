---
title: 静的リスト
feature: REST API, Static Lists
description: Marketo REST APIを使用して、ID、名前、参照、フォルダー範囲、ページング、日付フィルターのエンドポイントを含む静的リストをクエリ、作成、更新、削除します。
exl-id: 20679fd2-fae2-473e-84bc-cb4fdf2f5151
TQID: https://experienceleague.adobe.com/DSV9h6d4F3ZrIUT-VtqlmFAnpdxOuTf05ajCqiGegqk
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 360
ht-degree: 3%

---

# 静的リスト

[静的リストのエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists)

静的リスト REST APIを使用して、静的リストをクエリ、作成、更新、削除します。

リスト メンバーに対するリード データベース操作については、[ リスト メンバーシップ ](list-membership.md)を参照してください。

## クエリ

静的リスト [をID](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET)別、[名前](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET)別、または[閲覧](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListsUsingGET)別にクエリします。

### ID 別

[IDによるクエリ ](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET)は、1つの静的リスト `id` パス パラメーターを受け取り、一致するレコードを返します。

```http
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

[名前によるクエリ ](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET)は、静的リスト `name` パラメーターを使用します。 エンドポイントは、静的リスト名に対して完全一致を実行し、一致するレコードを返します。

```http
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

参照エンドポイントを使用して、[一括で静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListsUsingGET)。 オプションの`folder` パラメーターは、クエリを親フォルダーにスコープします。 フォルダーを`id`と`type`を含むJSON オブジェクトとして渡します。

ページネーションに`offset`と`maxReturn`を使用します。 `earliestUpdatedAt`と`latestUpdatedAt`を低い日時と高い日時の境界として使用します。 これらのパラメーターは、範囲内で作成または更新されたリストを返します。 ミリ秒なしでISO-8601値を使用します。

```http
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

`application/x-www-form-urlencoded` POST リクエストを[静的リストの作成](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/createStaticListUsingPOST)に送信します。 `folder`および`name` パラメーターが必要です。

`folder`を`id`と`type`を含むJSON オブジェクトとして渡します。 `name`は一意である必要があります。 オプションの`description` パラメーターは、リストを記述します。

```http
POST /rest/asset/v1/staticLists.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

更新エンドポイントを使用して[静的リストを変更](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/updateStaticListUsingPOST)します。 オプションの`description` パラメーターによって説明が変更されます。 オプションの`name` パラメーターは名前を変更し、一意である必要があります。

```http
POST /rest/asset/v1/staticList/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

## 削除

静的リスト ](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/deleteStaticListByIdUsingPOST)を[削除するには、その`id`をパスパラメーターとして渡します。 読み込み、書き出し、または別のアセットで使用されているリストは削除できません。

```http
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
