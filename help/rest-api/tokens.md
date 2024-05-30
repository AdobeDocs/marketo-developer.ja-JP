---
title: 「トークン」
feature: REST API, Tokens
description: 「Marketoのトークンの管理」
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%

---


# トークン

[トークンエンドポイントの参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens)

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

[フォルダー ID によるトークンの取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/getTokensByFolderIdUsingGET) 次を取ります `id` 「プログラム」タイプまたは「フォルダー」タイプのパスパラメーターとして。 このタイプは、 `folderType` パラメーター。

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

この [トークンを作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/addTokenTOFolderUsingPOST) エンドポイントがトークンを作成するか、トークンが存在する場合は、送信された値で更新します。 トークンは、フォルダーまたはプログラムのコンテキストで作成されます。 必須 `id` path パラメーターは、トークンが関連付けられるフォルダーの id です。 この `name`, `type`, `value`、および `folderType` は、トークンに必要なすべてのパラメーターです。 データは、JSON としてではなく、POST x-www-form-urlencoded として渡されます。 この `name` トークンのフィールドは 50 文字以下にする必要があります。

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

[名前によるトークンの削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/deleteTokenByNameUsingPOST) プログラムまたはフォルダータイプのパスパラメーターとして ID を受け取ります。 このタイプは、 `folderType` パラメーター。 トークンは、その親フォルダー、 `name`、および `type` トークンのうち、それぞれが必須です。 データは、JSON としてではなく、POST x-www-form-urlencoded として渡されます。

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
