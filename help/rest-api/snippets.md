---
title: 「スニペット」
feature: REST API, Snippets
description: 「Marketo API を使用したスニペットの管理」
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 2%

---


# スニペット

[スニペットエンドポイントの参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets)

スニペットは、メールやランディングページに埋め込み、動的コンテンツ用にセグメント化できる、再利用可能なHTMLコンポーネントです。 スニペットにはテンプレートが関連付けられていないため、Marketo内の他のアセット内で作成し、デプロイすることができます。

## クエリ

スニペットのクエリは、By Name メソッドを持たない点を除き、アセットの標準パターンに従います。 両方 [Id 別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/getSnippetByIdUsingGET) および [参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/getSnippetUsingGET) メソッドを使用すると、ステータスフィールドを使用して、スニペットの承認済みバージョンまたはドラフトバージョンを取得できます。

### Id 別

```
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

```
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

## コンテンツのクエリ

特定のスニペットのコンテンツは、スニペット ID に基づいて取得できます。

```
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

この呼び出しは、HTML型または DynamicContent 型のセクションで構成されるコンテンツセクションのリストと、オプションでテキスト型のセクションのリストを返します。

## 作成と更新

スニペットは、の呼び出しがである複雑なアセット作成パターンに従います [スニペットを作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/createSnippetUsingPOST)、およびそのコンテンツは個別に作成されるので、最初の呼び出しは、オプションの説明を含む、作成エンドポイントに対する必要があります。   データは、JSON としてではなく、x-www-form-urlencoded として渡されます。

```
POST /rest/asset/v1/snippets.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

スニペット内のコンテンツの追加や置換は、ID によって行われます。 コンテンツのタイプは、テキスト、HTML、DynamicContent のいずれかです。 type が Text の場合、コンテンツパラメーターはプレーンテキストのエンドポイントになり、HTMLの場合は、目的のマークアップテキストになります。 タイプを DynamicContent に設定した場合は、コンテンツパラメーターを、スニペットに関連付けるセグメントの ID に設定する必要があります。

```
POST /rest/asset/v1/snippet/{id}/content.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

[メタデータの更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/updateSnippetUsingPOST) は id でも実行されます。 更新できるのは名前と説明のみです：

```
POST /rest/asset/v1/snippet/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

スニペットは、動的コンテンツの標準的なパターンに従いますが、それ自体はコンテンツセクション全体を 1 つだけ表すので、各スニペットには動的セクションが 1 つだけ、オプションで使用されるセグメント内の各セグメントの内部セクションのリストが含まれる場合があります。 スニペットには動的コンテンツセクションが 1 つのみ存在する可能性があるので、動的コンテンツはスニペット ID だけでクエリできます。

```
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

スニペットには、ドラフトの承認、未承認および破棄に使用できるエンドポイントがあり、標準のアセットパターンに従っています。 スニペットを承認するには、そのスニペットがドラフトステータスになっている必要があります。

### 承認

```
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

### 承認取消

この `unapprove` エンドポイントは、承認されたスニペットでのみ使用できます。

```
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

### 下書きの破棄

破棄するには、スニペットはドラフトステータスになっている必要があります。  承認済みのスニペットは破棄できません。

```
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

[スニペットのクローン作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/cloneSnippetUsingPOST) の API はシンプルで、標準的なパターンに従います。必須の名前、元のスニペットの ID、フォルダー、オプションの説明が付きます。  承認済みバージョンが存在しない場合は、ドラフトバージョンのクローンが作成されます。

```
POST /rest/asset/v1/snippet/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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
