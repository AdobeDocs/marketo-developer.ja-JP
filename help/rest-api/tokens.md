---
title: トークン
feature: REST API, Tokens
description: Asset REST API を使用したMarketo マイトークンの管理。 サポートされるデータタイプ、フォルダーまたはプログラムによる取得、フォームエンコードされた POST を使用した作成または更新、名前別の削除を参照してください。
exl-id: 4f8d87d7-ba2a-4c90-8b39-4d20679d404a
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 91%

---

# トークン

[トークンエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens)

Marketo のトークンは、実行時に別のデータに置き換えられるショートコードに類似した特殊な文字列です。Marketo で使用できるトークンにはいくつかのタイプのトークンがありますが、API 経由で編集できるのはマイトークンのみです。マイトークンは、特定のフォルダーまたはプログラムに対してローカルな子トークンです。トークンは、API 経由で読み取り、作成、削除できます。

## データタイプ

トークンは、次のデータタイプで作成できます。

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| date | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| rich text | HTML 文字列 |
| score | 符号付き 32 ビット整数 |
| sfdc campaign | Salesforce キャンペーン管理の統合で使用 |
| text | テキスト文字列 |

これらは、API 経由でトークンを作成する際に使用できる唯一のデータタイプです。

## クエリ

[フォルダー ID によるトークンを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/getTokensByFolderIdUsingGET)では、プログラムタイプまたはフォルダータイプのパスパラメーターとして `id` を受け取ります。このタイプは、`folderType` パラメーターで指定されます。

```curl
GET /rest/asset/v1/folder/{id}/tokens.json?folderType=Folder
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "4fbe#14e27fc9bbf",
    "result": [
        {
            "folder": {
                "type": "Folder",
                "value": 416
            },
            "tokens": [
                {
                    "name": "AprilFool - deverly",
                    "type": "date",
                    "value": "2015-04-01",
                    "computedUrl": "https://app-abm.marketo.com/#MF1047C3"
                }
            ]
        }
    ]
}
```

## 作成と更新

[トークンを作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/addTokenTOFolderUsingPOST)エンドポイントでは、トークンを作成するか、トークンが存在する場合は送信された値でトークンを更新します。トークンは、フォルダーまたはプログラムのコンテキストで作成されます。必須の `id` パスパラメーターは、トークンが関連付けられるフォルダーの ID です。`name`、`type`、`value`、`folderType` は、すべてトークンの必須パラメーターです。データは、JSON ではなく、POST x-www-form-urlencoded として渡されます。トークンの `name` フィールドは 50 文字を超えることはできません。

```
POST /rest/asset/v1/folder/{id}/tokens.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=April Fools&type=date&value=2015-04-01&folderType=Folder
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "e3c2#14e280db5dc",
    "result": [
        {
            "folder": {
                "type": "Folder",
                "value": 416
            },
            "tokens": [
                {
                    "name": "April Fools",
                    "type": "date",
                    "value": "2015-04-01",
                    "computedUrl": "https://app-abm.marketo.com/#MF1047C3"
                }
            ]
        }
    ]
}
```

## 削除

[名前によるトークンを削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/deleteTokenByNameUsingPOST)では、プログラムまたはフォルダータイプのパスパラメーターとして ID を受け取ります。このタイプは、`folderType` パラメーターで指定されます。トークンは、それぞれ必須である親フォルダー、`name`、トークンの `type` に基づいて削除されます。データは、JSON ではなく、POST x-www-form-urlencoded として渡されます。

```
POST /rest/asset/v1/folder/{id}/tokens/delete.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=AprilFool - deverly&type=date&folderType=Program
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "12ed2#14e2800f89c",
    "result": [
        {
            "id": 416
        }
    ]
}
```
