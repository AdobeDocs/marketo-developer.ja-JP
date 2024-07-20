---
title: トークン
feature: REST API, Tokens
description: Marketoでトークンを管理します。
exl-id: 4f8d87d7-ba2a-4c90-8b39-4d20679d404a
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%

---

# トークン

[ トークンエンドポイントの参照 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens)

Marketoのトークンは、ショートコードに似た特殊な文字列で、実行時に別のデータに置き換えられます。 Marketoで使用できるトークンにはいくつかの種類がありますが、API で編集できるのはマイトークンのみです。 マイトークンは、特定のフォルダーまたはプログラムに対してローカルな子トークンです。 トークンは、API を介して読み取り、作成および削除できます。

## データタイプ

トークンは、次のデータタイプで作成できます。

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| 日 | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| リッチテキスト | HTML文字列 |
| スコア | 符号付き 32 ビット整数 |
| sfdc キャンペーン | Salesforce キャンペーン管理統合で使用 |
| テキスト | テキスト文字列 |


これらは、API を使用してトークンを作成する際に使用できる唯一のデータタイプです。

## クエリ

[ フォルダー ID によるトークンの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/getTokensByFolderIdUsingGET) プログラムまたはフォルダータイプのパスパラメーターとして `id` を受け取ります。 このタイプは `folderType` パラメーターで指定されます。

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

[ トークンを作成 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/addTokenTOFolderUsingPOST) エンドポイントはトークンを作成します。トークンが存在する場合は、送信された値で更新します。 トークンは、フォルダーまたはプログラムのコンテキストで作成されます。 必須の `id` パスパラメーターは、トークンが関連付けられるフォルダーの ID です。 `name`、`type`、`value`、`folderType` はすべて、トークンの必須パラメーターです。 データは、JSON としてではなく、POST x-www-form-urlencoded として渡されます。 トークンの `name` フィールドは 50 文字以下にする必要があります。

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

[ 名前によるトークンの削除 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/deleteTokenByNameUsingPOST):ID をプログラムタイプまたはフォルダータイプのパスパラメーターとして受け取ります。 このタイプは `folderType` パラメーターで指定されます。 トークンは、その親フォルダー、トークンの `name`、トークンの `type` に基づいて削除されます。各トークンは必須です。 データは、JSON としてではなく、POST x-www-form-urlencoded として渡されます。

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
