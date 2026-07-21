---
title: トークン
feature: REST API, Tokens
description: Asset REST APIでMarketoのマイトークンを管理します。 サポートされているデータタイプ、フォルダーまたはプログラムによる取得、フォームエンコードされたPOSTを使用した作成または更新、名前による削除を参照してください。
exl-id: 4f8d87d7-ba2a-4c90-8b39-4d20679d404a
TQID: https://experienceleague.adobe.com/uqOpu2vDuiQiZhILKuxZJQGadd0K14zwIaAdmNfK1-I
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 290
ht-degree: 20%

---

# トークン

[トークンエンドポイントの参照](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens)

トークンは、Marketoが実行時に他のデータと置き換える文字列です。 APIは、フォルダーまたはプログラムにローカルな子トークンであるマイトークンのみを編集できます。

トークン APIを使用して、マイトークンを読み取り、作成、更新、削除します。

## データタイプ

トークンは、次のデータタイプで作成できます。

| タイプ | 説明 |
| --- | --- |
| date | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| rich text | HTML 文字列 |
| score | 符号付き 32 ビット整数 |
| sfdc campaign | Salesforce キャンペーン管理の統合で使用 |
| text | テキスト文字列 |

APIは、トークンの作成時にこれらのデータタイプのみをサポートします。

## クエリ

[ フォルダーIDでトークンを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens/operation/getTokensByFolderIdUsingGET)は、プログラムまたはフォルダーのIDをパスパラメーターとして受け取ります。 `folderType` パラメーターを使用して、型を指定します。

```http
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

[ トークンを作成](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens/operation/addTokenTOFolderUsingPOST) エンドポイントは、送信された値でトークンを作成するか、既存のトークンを更新します。 トークンはフォルダーまたはプログラムに属します。

`id` パス パラメーターは、親フォルダーを識別します。 `name`、`type`、`value`および`folderType`のパラメーターが必要です。 データをJSONではなくPOST `x-www-form-urlencoded`として渡します。 トークン `name`は50文字を超えることはできません。

```http
POST /rest/asset/v1/folder/{id}/tokens.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

[名前でトークンを削除](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens/operation/deleteTokenByNameUsingPOST)は、プログラムまたはフォルダーのIDをパスパラメーターとして受け取ります。 `folderType`を使用してタイプを指定します。

親フォルダー、トークン `name`およびトークン `type`が必要です。 データをJSONではなくPOST `x-www-form-urlencoded`として渡します。

```http
POST /rest/asset/v1/folder/{id}/tokens/delete.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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
