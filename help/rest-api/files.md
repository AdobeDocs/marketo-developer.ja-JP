---
title: ファイル
feature: REST API
description: Marketo REST API ファイルのガイド IDまたは名前によるクエリ、フォルダーとオフセットによる参照、マルチパートアップロードによる作成または更新、insertOnly、MIME タイプ、ストリーミングなし
exl-id: 17361cdc-2309-442c-803c-34ce187aee1a
TQID: https://experienceleague.adobe.com/qH8zFwjJkTWHlCj1VHNiTiLK3mNOJFS83cnjEj2qjpA
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 7%

---

# ファイル

[ファイル エンドポイント リファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Files)

Files REST APIを使用して、Marketo サブスクリプションに保存されている画像、スクリプト、ドキュメント、スタイルシート、その他のファイルを管理します。

Marketoのファイルストレージは、帯域幅が多いアプリケーション向けに最適化されていません。 オーディオとビデオ専用のストリーミングサービスを利用できます。

## クエリ

ID](https://developer.adobe.com/marketo-apis/api/asset#tag/Files/operation/getFileByIdUsingGET)で[、名前](https://developer.adobe.com/marketo-apis/api/asset#tag/Files/operation/getFileByNameUsingGET)で[、または[閲覧](https://developer.adobe.com/marketo-apis/api/asset#tag/Files/operation/getFilesUsingGET)でファイルをクエリします。

### ID 別

```http
GET /rest/asset/v1/file/{id}.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":null,
   "result":[
      {
         "id":147,
         "size":61346,
         "mimeType":"image/jpeg",
         "url":"http://mlm.devlocal.marketo.com/rs/test/assets/rYXNeQFFVu",
         "folder":{
            "type":"Email",
            "id":10613
         },
         "name":"rYXNeQFFVu",
         "description":null,
         "createdAt":"2014-12-09T22:33:57Z+0000",
         "updatedAt":"2014-12-09T22:33:57Z+0000"
      }
   ]
}
```

### 名前別

必須の `name` パラメーターを使用して、ファイルの名前を指定します。

```http
GET /rest/asset/v1/file/byName.json?name=foo.png
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "9049#15918a76619",
    "result": [
        {
            "id": 46488,
            "size": 13987,
            "mimeType": "image/png",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/foo.png",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images"
            },
            "name": "foo.png",
            "description": "This is a test file.",
            "createdAt": "2015-05-06T22:16:58Z+0000",
            "updatedAt": "2015-05-06T22:19:29Z+0000"
        }
    ]
}
```

### 参照

参照エンドポイントは、次の3つのオプションのパラメーターを受け入れます。

- `folder` – 親フォルダーは、`id`および`type`属性を含むJSON オブジェクトです。
- `offset` - エントリの取得を開始する位置。 デフォルトは0です。 `maxReturn`で使用します。
- `maxReturn` – 返されるエントリの最大数。 デフォルトは20、最大は200です。

```http
GET /rest/asset/v1/files.json?folder={"id":436, "type": "Folder"}&maxReturn=3
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "17e4e#14e23372d80",
    "result": [
        {
            "id": 46484,
            "size": 1454,
            "mimeType": "text/plain",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/websites.png",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images - deverly"
            },
            "name": "websites.png",
            "description": "This is a test file.",
            "createdAt": "2015-05-06T20:15:58Z+0000",
            "updatedAt": "2015-06-22T02:12:36Z+0000"
        },
        {
            "id": 46486,
            "size": 4169,
            "mimeType": "image/png",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/mobile.png",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images - deverly"
            },
            "name": "mobile.png",
            "description": null,
            "createdAt": "2015-05-06T22:13:33Z+0000",
            "updatedAt": "2015-05-06T22:13:33Z+0000"
        },
        {
            "id": 46488,
            "size": 13987,
            "mimeType": "image/png",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/foo.png",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images - deverly"
            },
            "name": "foo.png",
            "description": "This is a test file.",
            "createdAt": "2015-05-06T22:16:58Z+0000",
            "updatedAt": "2015-05-06T22:19:29Z+0000"
        }
    ]
}
```

## 作成と更新

`multipart/form-data` リクエストを使用して、[ ファイルを作成](https://developer.adobe.com/marketo-apis/api/asset#tag/Files/operation/createFileUsingPOST)します。 `name`、`folder`および`file` パラメーターが必要です。 `description`および`insertOnly` パラメーターはオプションです。 trueの場合、`insertOnly`は、同じ名前の既存のファイルを更新するリクエストを禁止します。

`file` パラメーターの場合、`Content-Disposition` ヘッダーに`filename`を含めます。 ファイルの`Content-Type` ヘッダーも含めます。 Marketoは、ファイルを提供する際にこのMIME タイプを使用します。

```http
POST /rest/asset/v1/files.json
```

```html
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="file"; filename="marketo.html"
Content-Type: text/html
<html>
<body>
<h1>Test Page - marketo.html</h1>
</body>
</html>
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="name"
marketo.html
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="folder"
{"id":436,"type":"Folder"}
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="description"
This is a test file
------WebKitFormBoundary2VyWOacQSupl4gUL—
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "278d#14e23316f63",
    "result": [
        {
            "id": 46960,
            "size": 69,
            "mimeType": "text/html",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/marketo.html",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images - deverly"
            },
            "name": "marketo.html",
            "description": "This is a test file",
            "createdAt": "2015-06-24T01:31:59Z+0000",
            "updatedAt": "2015-06-24T01:31:59Z+0000"
        }
    ]
}
```

[ ファイルを更新](https://developer.adobe.com/marketo-apis/api/asset#tag/File-Contents/operation/updateContentUsingPOST)するには、そのIDを指定します。 `file` パラメーターの要件は、ファイルの作成と同じです。

```http
POST /rest/asset/v1/file/{id}/content.json
```

```html
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="file"; filename="marketo.html"
Content-Type: text/html
<html>
<body>
<h1>Test Page - marketo.html</h1>
</body>
</html>
------WebKitFormBoundary2VyWOacQSupl4gUL--
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": null,
    "result": [
        {
            "id": 67,
            "size": 512000,
            "mimeType": "image/png",
            "url": "http://pages.devlocal.marketo.com/rs/test/assets/aLZiwCkXor",
            "folder": {
                "type": "Email",
                "id": 10391
            },
            "name": "aLZiwCkXor",
            "description": null,
            "createdAt": "2014-12-18T09:03:43Z+0000",
            "updatedAt": "2015-01-07T04:40:20Z+0000"
        }
    ]
}
```
