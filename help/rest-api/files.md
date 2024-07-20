---
title: ファイル
feature: REST API
description: Marketo ファイルの保存と操作。
exl-id: 17361cdc-2309-442c-803c-34ce187aee1a
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 1%

---

# ファイル

[ ファイルエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files)

Marketoのサブスクリプションを使用すると、画像、スクリプト、ドキュメント、スタイルシートなど、任意のファイルを保存できます。 これらはすべて、REST API を使用してリモートで操作できます。 Marketoのサブスクリプションで利用できるストレージは、帯域幅を集中的に消費するアプリケーション向けに最適化されていないので、適切なオーディオおよびビデオストリーミングアプリケーションには代替手段を使用する必要があります。

## クエリ

ファイルのクエリは単純で、（ID 別 [、（名前 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files/operation/getFileByIdUsingGET)、ブラウジング [ の各アセットの標準のクエリタイプ ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files/operation/getFileByNameUsingGET) に従い [ す ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files/operation/getFilesUsingGET)。

### Id 別

```
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

必要な `name` パラメーターを使用してファイルの名前を指定します。

```
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

オプションのパラメーターは 3 つあります。

- フォルダー – 「id」属性と「type」属性を含む JSON ブロックとして指定された親フォルダー
- offset - エントリの取得を開始する場所を指定する整数（デフォルトは 0）。maxReturn パラメーターと共に使用できます
- maxReturn – 返されるエントリの最大数を指定する整数（デフォルトは 20、最大は 200）

```
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

[ ファイルの作成 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files/operation/createFileUsingPOST) は、マルチパート/フォームデータタイプのリクエストで行われます。 最小限の場合、リクエストには名前、フォルダー、ファイルが必要です。オプションの説明と insertOnly フラグが追加されています。これにより、作成呼び出しで既存のファイルが同じ名前で更新されなくなります。 file パラメーターの場合、name パラメーターに加えて、Content-Disposition ヘッダーに「filename」が必要です。 また、ファイルの Content-Type ヘッダーを渡す必要があります。このヘッダーは、Marketoがファイルを提供するために使用する MIME タイプです。

```
POST /rest/asset/v1/files.json
```

```
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

[ ファイルの更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/File-Contents/operation/updateContentUsingPOST) は、ID に基づいて実行できます。 唯一のパラメーターは、作成と同じ要件を持つファイルパラメーターです。

```
POST /rest/asset/v1/file/{id}/content.json
```

```
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
