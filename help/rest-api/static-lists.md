---
title: 静的リスト
feature: REST API, Static Lists
description: Marketo REST APIを使用して、ID、名前、参照、フォルダー範囲、ページング、日付フィルターのエンドポイントを含む静的リストをクエリ、作成、更新、削除します。
exl-id: 20679fd2-fae2-473e-84bc-cb4fdf2f5151
source-git-commit: e2606d6cb12c572603ff069617de58417e43ca63
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 71%

---

# 静的リスト

[静的リストのエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists)

Marketo は、静的リストで CRUD 操作を実行する一連の REST API を備えています。 これらの API は、クエリ、作成、更新、削除のオプションを提供するアセット API の標準インターフェイスパターンに従います。

リスト メンバーに対するリード データベース操作については、[ リスト メンバーシップ ](list-membership.md)を参照してください。

## クエリ

静的リストのクエリは、アセットに対する標準のクエリタイプ（[IDによるクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET)、[名前によるクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET)、および[参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET)）に従います。

### ID 別

[ID によるクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET)は、単一の静的リスト `id` をパスパラメーターとして受け取り、単一の静的リストレコードを返します。

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

[名前によるクエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET)は、静的リスト `name` をパラメーターとして受け取り、単一の静的リストレコードを返します。 インスタンス内のすべての静的リスト名に対して正確な文字列一致検索が実行され、その名前に一致する静的リストの結果が返されます。

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

静的リストは、[バッチで取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET)することもできます。 `folder` パラメーターを使用して、クエリを実行する親フォルダーを指定できます。このフォルダーは、`id`と`type`を含むJSON オブジェクトとしてフォーマットされます。 他の一括アセット取得エンドポイントと同様に、`offset` と `maxReturn` はページングに使用できるオプションパラメーターです。 `earliestUpdatedAt` および `latestUpdatedAt` パラメーターを使用すると、指定した範囲内で作成または更新された静的リストを返すための日時の日時透かし（低および高）を設定できます。 Datetime値は、有効なISO-8601文字列である必要があり、ミリ秒を含めないでください。

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

[静的リストの作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/createStaticListUsingPOST)は、2つの必須パラメーターを含む`application/x-www-form-urlencoded` POSTで実行されます。 `folder` パラメーターは、静的リストを作成する親フォルダーを指定するために使用され、`id`と`type`を含むJSON オブジェクトとしてフォーマットされます。 `name` パラメーターは、静的リストに名前を付けるために使用され、一意である必要があります。 オプションで、`description` パラメーターを使用して静的リストについて説明することもできます。

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

[静的リスト ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/updateStaticListUsingPOST)の更新は、2つのオプションのパラメーターを持つ別のエンドポイントを通じて行われます。 `description` パラメーターは、静的リストの説明を更新するために使用できます。 `name` パラメーターは、静的リスト名を更新するために使用でき、一意である必要があります。

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

[静的リストの削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/deleteStaticListByIdUsingPOST)では、パスパラメーターとして単一の静的リスト `id` を受け取ります。 読み込みまたは書き出し操作で使用されている静的リストや、他のアセットで使用されている静的リストは削除できません。

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
