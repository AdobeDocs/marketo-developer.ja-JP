---
title: スニペット
feature: REST API, Snippets
description: Marketo Asset REST APIのスニペット用。ID別のクエリとステータス付きの参照、コンテンツの取得、HTML、テキスト、動的コンテンツの作成と更新が可能です。
exl-id: 87901c29-ee59-4224-848d-3bd6a6c52718
TQID: https://experienceleague.adobe.com/1UpwX-ZzXTzkTRheu8exBDIoIvAGgoZgpA851PuL8sI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 386
ht-degree: 11%

---

# スニペット

[スニペットエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset#tag/Snippets)

スニペットは、電子メールやランディングページに埋め込むことができる、再利用可能なHTMLコンポーネントです。 動的コンテンツ用にスニペットをセグメント化することができます。 スニペットはテンプレートを使用せず、他のMarketo アセット内で作成およびデプロイできます。

## クエリ

ID[&#128279;](https://developer.adobe.com/marketo-apis/api/asset#tag/Snippets/operation/getSnippetByIdUsingGET)または[閲覧](https://developer.adobe.com/marketo-apis/api/asset#tag/Snippets/operation/getSnippetUsingGET)によって スニペットをクエリします。 APIは名前によるクエリのメソッドを提供しません。 両方のエンドポイントは、承認済みまたはドラフトのバージョンを取得するために`status` フィールドを受け入れます。

### ID 別

```http
GET /rest/asset/v1/snippet/{id}.json?status=approved
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"fa0f#14b04375f0a",
   "result":[
      {
         "id":83,
         "name":"BYkHVJEedl",
         "description":"yzSLvNFyrmeVmyLzqryUfGlDOJTnvyyfsQTXPDCGdCwcWUlfoCNApUqYgwZGElrUFoxBHJcMdXdqTKvtjtfsmPgokyRgVLeHyJCw",
         "createdAt":"2015-01-19T22:01:52Z+0000",
         "updatedAt":"2015-01-19T22:01:52Z+0000",
         "folder":{
            "type":"Folder",
            "value":662
         },
         "status":"approved",
         "workspace":"Default"
      }
   ]
}
```

### 参照

```http
GET /rest/asset/v1/snippets.json?maxReturn=3
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"f9cc#14b04376181",
   "result":[
      {
         "id":23,
         "name":"ADJvMLBMpS",
         "description":"XkzFUVLXVHrojLGLJVLPpwguOXuDvhAqaaSkBUVzgHrgDhqqRzyXlULIXSHJvfBHjCSaMwjyEdrdxcjFCRoNFVvdBBTDfSrUJzaR",
         "createdAt":"2015-01-15T20:10:39Z+0000",
         "updatedAt":"2015-01-15T20:10:39Z+0000",
         "url": null,
         "folder":{
            "type":"Folder",
            "value":620,
            "folderName": "Snippets"
         },
         "status":"draft",
         "workspace":"Default"
      },
      {
         "id":46,
         "name":"Biswa Snippet",
         "description":"",
         "createdAt":"2015-01-16T05:18:55Z+0000",
         "updatedAt":"2015-01-16T05:19:27Z+0000",
         "url": null,
         "folder":{
            "type":"Folder",
            "value":630,
            "folderName": "Snippets"
         },
         "status":"draft",
         "workspace":"Default"
      },
      {
         "id":12,
         "name":"dJJQkKbUYq",
         "description":"VXuHkYMREHrhxUSgYbKfaNeLisdFxOromCXQNrgmModvkuoyZdQjtAbXxDUbBvoDVCZmAVbasiHyWoWfTwgrGxnzpKepGrAUvfen",
         "createdAt":"2015-01-15T05:12:33Z+0000",
         "updatedAt":"2015-01-15T05:12:33Z+0000",
         "url": null,
         "folder":{
            "type":"Folder",
            "value":615,
            "folderName": "Snippets"
         },
         "status":"draft",
         "workspace":"Default"
      }
   ]
}
```

## クエリコンテンツ

スニペット IDでスニペット コンテンツを取得します。

```http
GET /rest/asset/v1/snippet/{id}/content.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"5c50#14b04376159",
   "result":[
      {
         "type":"HTML",
         "content":"draft testUpdateSnippetContent1 HTML Content"
      },
      {
         "type":"Text",
         "content":"draft testUpdateSnippetContent1 Text Content"
      }
   ]
}
```

応答には、タイプ `HTML`または`DynamicContent`のセクションが含まれています。 `Text`型のセクションを含めることもできます。

## 作成と更新

スニペットアセットとそのコンテンツを別々に作成します。 まず、[create snippet](https://developer.adobe.com/marketo-apis/api/asset#tag/Snippets/operation/createSnippetUsingPOST) エンドポイントを呼び出します。 説明はオプションです。 データをJSONではなく`x-www-form-urlencoded`として渡します。

```http
POST /rest/asset/v1/snippets.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=Test Snippet 09 - deverly&folder={"id":395,"type":"Folder"}&description=This is a test snippet
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "bd57#14e231ee3a1",
    "result": [
        {
            "id": 13,
            "name": "Test Snippet 09 - deverly",
            "description": "This is a test snippet",
            "createdAt": "2015-06-24T01:11:43Z+0000",
            "updatedAt": "2015-06-24T01:11:43Z+0000",
            "url": "https://app-abm.marketo.com/#SN13B2ZN395",
            "folder": {
                "type": "Folder",
                "value": 395,
                "folderName": "Snippets"
            },
            "status": "draft",
            "workspace": "Default"
        }
    ]
}
```

スニペットコンテンツをIDで追加または置換します。 コンテンツの種類は`Text`、`HTML`、または`DynamicContent`です。

- `Text`の場合、`content` パラメーターにプレーンテキストを渡します。
- `HTML`の場合、`content` パラメーターにマークアップを渡します。
- `DynamicContent`の場合、`content`をスニペットに関連付けられたセグメントのIDに設定します。

```http
POST /rest/asset/v1/snippet/{id}/content.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
type=HTML&content=draft testUpdateSnippetContent1 HTML Content
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"73d9#14b04376139",
   "result":[
      {
         "id":82
      }
   ]
}
```

[&#x200B; メタデータを更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Snippets/operation/updateSnippetUsingPOST)するには、スニペット IDを指定します。 更新できるのは、名前と説明のみです。

```http
POST /rest/asset/v1/snippet/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=Test Snippet&description=New Description
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"9ad0#14b043762b1",
   "result":[
      {
         "id":82,
         "name":"Test Snippet",
         "description":"New Description",
         "createdAt":"2015-01-19T22:01:52Z+0000",
         "updatedAt":"2015-01-19T22:01:53Z+0000",
         "url": "https://app-abm.marketo.com/#SN3B2ZN395",
         "folder":{
            "type":"Folder",
            "value":662,
            "folderName": "Snippets"
         },
         "status":"draft",
         "workspace":"Default"
      }
   ]
}
```

## 動的コンテンツ

スニペットは、1つの完全なコンテンツセクションを表し、1つの動的セクションのみを含めることができます。 このセクションには、関連するセグメント内の各セグメントの内部セクションを含めることができます。

スニペットには1つの動的セクションしか含めることができないので、スニペット IDでその動的コンテンツをクエリします。

```http
GET /rest/asset/v1/snippet/{id}/dynamicContent.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "ae3#14c2b499111",
    "result": [
        {
            "createdAt": "2015-03-13T06:24:35Z+0000",
            "updatedAt": "2015-03-17T20:29:42Z+0000",
            "id": 70,
            "segmentation": 1001,
            "content": [
                {
                    "id": "Nzk*",
                    "segmentId": 1001,
                    "segmentName": "Area",
                    "content": "Sample HTML for Area",
                    "type": "HTML"
                },
                {
                    "id": "Nzk*",
                    "segmentId": 1001,
                    "segmentName": "Area",
                    "content": "Sample Text for Area",
                    "type": "Text"
                },
                {
                    "id": "Nzk*",
                    "segmentId": 1002,
                    "segmentName": "Default",
                    "content": "Sample HTML for Default",
                    "type": "HTML"
                },
                {
                    "id": "Nzk*",
                    "segmentId": 1002,
                    "segmentName": "Default",
                    "content": "Sample Text for Default",
                    "type": "Text"
                }
            ]
        }
    ]
}
```

## 承認

スニペットは、承認、承認の削除、ドラフトの破棄のためのエンドポイントを提供します。 スニペットは承認前にドラフトステータスである必要があります。

### 承認

```http
POST /rest/asset/v1/snippet/{id}/approveDraft.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "11903#14db1af2f6c",
    "result": [
        {
            "id": 3,
            "name": "Test Snippet 02 - deverly",
            "description": "hey this is a test snippet!",
            "createdAt": "2015-06-02T00:32:37Z+0000",
            "updatedAt": "2015-06-02T00:32:37Z+0000",
            "url": "https://app-abm.marketo.com/#SN3B2ZN395",
            "folder": {
                "type": "Folder",
                "value": 395,
                "folderName": "Snippets"
            },
            "status": "approved",
            "workspace": "Default"
        }
    ]
}
```

### 未承認

`unapprove` エンドポイントは、承認済みスニペットに対してのみ使用できます。

```http
POST /rest/asset/v1/snippet/{id}/unapprove.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "7d20#14db1c7a2a9",
    "result": [
        {
            "id": 89,
            "name": "Test Snippet 01 - deverly",
            "description": "",
            "createdAt": "2015-05-15T19:01:22Z+0000",
            "updatedAt": "2015-05-15T19:07:07Z+0000",
            "url": "https://app-abm.marketo.com/#SN1B2ZN395",
            "folder": {
                "type": "Folder",
                "value": 395,
                "folderName": "Snippets"
            },
            "status": "draft",
            "workspace": "Default"
        }
    ]
}
```

### 下書きを破棄

スニペットを破棄するには、メールがドラフトステータスである必要があります。  承認済みスニペットは破棄できません。

```http
POST /rest/asset/v1/snippet/{id}/discardDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"674c#14b043760de",
   "result":[
      {
         "id":88
      }
   ]
}
```

## 複製

スニペット [&#128279;](https://developer.adobe.com/marketo-apis/api/asset#tag/Snippets/operation/cloneSnippetUsingPOST)を複製するには、名前、ソーススニペット ID、フォルダーを指定します。 説明はオプションです。 ソースに承認済みのバージョンがない場合、エンドポイントはドラフトを複製します。

```http
POST /rest/asset/v1/snippet/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=Test Snippet Clone 3 - deverly&folder={"id":395,"type":"Folder"}&description=This is a test snippet
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "21c9#14e2327e33d",
    "result": [
        {
            "id": 14,
            "name": "Test Snippet Clone 3 - deverly",
            "description": "This is a test snippet",
            "createdAt": "2015-06-24T01:21:33Z+0000",
            "updatedAt": "2015-06-24T01:21:33Z+0000",
            "url": "https://app-abm.marketo.com/#SN14B2ZN395",
            "folder": {
                "type": "Folder",
                "value": 395,
                "folderName": "Snippets"
            },
            "status": "draft",
            "workspace": "Default"
        }
    ]
}
```
