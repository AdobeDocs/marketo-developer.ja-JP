---
title: アセット
feature: REST API
description: IDまたは名前によるクエリ、ページングによる参照、フォルダー、電子メール、フォーム、テンプレート、ファイル、トークンの作成または更新を行うためのMarketo Asset REST APIの概要。
exl-id: 4273a5b1-1904-46e8-b583-fc6f46b388d2
TQID: https://experienceleague.adobe.com/gRhXvFtG1FHtGJ4tFQxOyGMkEiOX0K1S0VpjcB6s6xM
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: d65b4a73-87a3-4d56-b638-74e74d9939ceid: e64968b2-4ee5-47f9-8cae-0588f184b9ebid: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 631
ht-degree: 11%

---

# アセット

Marketo Asset REST APIを使用して、マーケティングアセットや組織アセットをクエリおよび管理できます。

## アセット

Marketo アセットには、次のものが含まれます。

- フォルダー
- プログラム
- メール
- メールテンプレート
- フラグメント
- ランディングページ
- ランディングページのテンプレート
- スニペット
- フォーム
- トークン
- ファイル

## API

パラメーターやモデリング情報を含む Asset API エンドポイントの完全なリストについて詳しくは、[Asset API エンドポイント参照](endpoint-reference.md)を参照してください。

## クエリ

アセット APIは通常、ID、名前、ブラウジングの3つの取得パターンをサポートしています。 IDまたは名前によるクエリは、指定したパラメーターに対して1つのアセットを取得します。 参照エンドポイントは、そのタイプのアセットのページ分割されたリストを返します。

フィルタリングパラメーターは、アセットの種類によって異なります。 サポートされているフィルターについては、各アセットタイプのドキュメントを参照してください。

参照エンドポイントの中には、タグに許可されている値など、子アセットを返さないものもあります。 これらのアセットを名前またはIDで個別に取得し、完全なメタデータを取得します。 その他のアセットタイプでは、フォームフィールドなどの依存オブジェクトに対して個別のエンドポイントを提供します。

### ID 別

```http
GET /rest/asset/v1/folder/{id}.json?type=Folder
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "1241b#14e21ca814a",
    "result": [
        {
            "name": "Social Media",
            "description": null,
            "createdAt": "2011-03-04T17:01:32Z+0000",
            "updatedAt": "2011-03-04T17:01:32Z+0000",
            "url": null,
            "folderId": {
                "id": 341,
                "type": "Folder"
            },
            "folderType": "Email",
            "parent": {
                "id": 11,
                "type": "Folder"
            },
            "path": "/Design Studio/Default/Emails/Social Media",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 341
        }
    ]
}
```

### 名前別

アセット APIでは、コンマを含むアセット名を検索できません。 アセット名からコンマを除外します。

```http
GET /rest/asset/v1/file/byName.json?name=My File
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":null,
   "result":[
      {
         "id":148,
         "size":270313,
         "mimeType":"image/jpeg",
         "url":"http://mlm.devlocal.marketo.com/rs/test/assets/piKLbhVFvW",
         "folder":{
            "type":"Email",
            "id":10614
         },
         "name":"My File",
         "description":null,
         "createdAt":"2014-12-09T22:33:57Z+0000",
         "updatedAt":"2014-12-09T22:33:57Z+0000"
      }
   ]
}
```

### 参照

アセット参照エンドポイントは、次のクエリパラメーターをサポートしています。

- `offset` – 結果の返しを開始する整数オフセット。
- `maxReturn` – 返されるレコードの最大数。 デフォルトは20、最大は200です。

```http
GET /rest/asset/v1/emailTemplates.json?offset=10&maxReturn=50
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"33c4#14a1832b4a8",
   "result":[
      {
         "id":18,
         "name":"AAA0unit3CreateTestEmailTemplateName.2314673e-7bc2-47da-a1e8-66dfdd8a1f1d",
         "description":"AssetAPI: getTemplates test",
         "createdAt":"2014-11-03T19:52:58Z+0000",
         "updatedAt":"2014-11-03T19:52:58Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":177,
         "name":"ABfRGutnwN",
         "description":"HMmHkdTRrGaRpPakdgGKICxfMunCEWDUWiThgAbInfaBXxGxSFfjKQIwerngCHRlGTnAJhKPmwlXLcsjGPtWEiILGyeIJTNVHoHg",
         "createdAt":"2014-11-20T19:31:06Z+0000",
         "updatedAt":"2014-11-20T19:31:06Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":148,
         "name":"ADVHJBQLyw",
         "description":null,
         "createdAt":"2014-11-20T06:42:57Z+0000",
         "updatedAt":"2014-11-20T06:42:57Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      }
   ]
}
```

## 作成と更新

フォルダー、トークン、ファイルなどのシンプルなアセットタイプは、通常、作成するエンドポイントとIDで更新するエンドポイントを提供します。 アセットを作成する際には、名前が必要です。 「作成」または「更新」応答は、アセットのメタデータとIDを返します。

次のリクエストはトークンを作成します。

```http
POST /rest/asset/v1/folder/{id}/tokens.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=April Fools&value=2015-04-01&type=date&folderType=Folder
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

次のリクエストは、フォルダーを更新します。

```http
POST /rest/asset/v1/folder/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```sql
type=Folder&description=This is a test (update 01)
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "c5b2#14e1f3954bf",
    "result": [
        {
            "name": "Learning - deverly",
            "description": "This is a test (update 01)",
            "createdAt": "2015-03-17T00:17:02Z+0000",
            "updatedAt": "2015-06-23T07:02:07Z+0000",
            "url": "https://app-abm.marketo.com/#MF1044A1",
            "folderId": {
                "id": 407,
                "type": "FOLDER"
            },
            "folderType": "Marketing Folder",
            "parent": {
                "id": 15,
                "type": "FOLDER"
            },
            "path": "/Marketing Activities/Default/Learning - deverly",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 407
        }
    ]
}
```

Formsの電子メール、メールテンプレート、ランディングページ、ランディングページテンプレートは、より複雑な構造になっています。 各タイプには、アセットを作成するための1つのエンドポイントと、メタデータ、コンテンツ、およびコンテンツセクションを更新するための追加のエンドポイントが用意されています。

これらのアセットは、使用前に承認する必要があります。 たとえば、テンプレート IDを使用してランディングページを作成し、そのコンテンツセクションを取得して、必要な各セクションを更新し、展開のためにページを承認します。

### 複雑な作成

親テンプレートからランディングページを作成します。 新しいランディングページには、各セクションのテンプレートのデフォルトコンテンツが含まれます。

```http
POST rest/asset/v1/landingPages.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=createLandingPage&folder={"type": "Folder", "id": 11}&template=1&description=this is a test&workspace=default&title=test create&keywords=awesome&formPrefill=false
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "7a39#154cf7922c6",
    "result": [
        {
            "id": 27,
            "name": "createLandingPage",
            "description": "this is a test",
            "createdAt": "2016-05-20T18:41:43Z+0000",
            "updatedAt": "2016-05-20T18:41:43Z+0000",
            "folder": {
                "type": "Folder",
                "value": 11,
                "folderName": "Landing Pages"
            },
            "workspace": "Default",
            "status": "draft",
            "template": 1,
            "title": "test create",
            "keywords": "awesome",
            "robots": "index, nofollow",
            "formPrefill": false,
            "mobileEnabled": false,
            "URL": "https://app-devlocal1.marketo.com/lp/622-LME-718/createLandingPage.html",
            "computedUrl": "https://app-devlocal1.marketo.com/#LP27B2"
        }
    ]
}
```

#### セクションの取得

ランディングページのコンテンツセクションを取得します。 テンプレートと異なる必要がある各セクションを更新します。

```http
GET /rest/asset/v1/landingPage/{id}/content.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "6307#154ea1689d7",
    "result": [
        {
            "id": "67",
            "type": "Form",
            "index": 1,
            "content": {
                "content": "189",
                "contentType": "Form",
                "contentUrl": "https://app-devlocal1.marketo.com/#FO189A1ZN13LA1"
            },
            "formattingOptions": {
                "zIndex": 15,
                "left": "359px",
                "top": "122px"
            }
        }
    ]
}
```

#### セクションの更新

```http
POST /rest/asset/v1/landingPage/{id}/content/{contentId}.json?type=Form&value=1
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "5c37#154ea32cf11",
    "result": [
        {
            "id": 174
        }
    ]
}
```

## 承認

電子メール、ランディングページ、スニペット、フォーム、そのテンプレートでは、ドラフトと承認のシステムが使用されています。 コンテンツの更新は、承認されたライブバージョンに影響を与えることなく、ドラフトを変更します。

承認エンドポイントは、ドラフトを検証します。 検証が成功すると、ドラフトがライブバージョンに置き換わり、ドラフトの状態がクリアされます。 検証が失敗した場合、エンドポイントは理由を返します。

```http
POST /rest/asset/v1/emailTemplate/{id}/approveDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"abe2#14a1832a97d",
   "result":[
      {
         "id":338,
         "name":"lvAVYMZqPS",
         "description":"fZLJQSJRvnYbjGTUpIHHqDOuQgQzXQcWIXoOUPwrVLdMHKcbRqwLoSLkWZTUmaMiCIJSfQiufnnrgITUIqjuAPBLpmliiKuIUFYG",
         "createdAt":"2014-12-05T02:06:21Z+0000",
         "updatedAt":"2014-12-05T02:06:21Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Approved",
         "workspace":"Default"
      }
   ]
}
```

承認が成功すると、以前のライブバージョンが更新されたバージョンに置き換えられます。

サポートされている各アセットタイプは、ドラフトを破棄するためのエンドポイントを提供します。 ドラフトを持つ承認済みアセットの場合、このエンドポイントはドラフトとその保留中の変更を破棄します。

アセットに承認済みのバージョンがない場合、エンドポイントはエラーを返します。 ドラフトのみのアセットは削除できますが、ドラフトを破棄することはできません。

```http
POST /rest/asset/v1/emailTemplate/{id}/discardDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"17bfa#14a1832b3c4",
   "result":[
      {
         "id":344,
         "name":"LkilkvKrkp",
         "description":"yAyUEXuWMtdhpODUmnCkGjpBcyEKnYucxaSoTyYeQzyNbYanxCXWPOzwiIWmeXPUwjfGAUmgnxlhgOPluVqwNittuvxJmNTaHxYM",
         "createdAt":"2014-12-05T02:06:23Z+0000",
         "updatedAt":"2014-12-05T02:06:23Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      }
   ]
}
```

承認済みのみの状態にあるアセットは、承認を取り消すことができます。 承認を取り消すと、ライブバージョンが削除され、アセットはドラフトのみの状態に戻され、関連するドラフトはすべて破棄されます。

ほとんどのアセットタイプでは、アセットを使用中にすることはできません。 例えば、メールを送信フローステップで参照されるメールや、メールに埋め込まれたスニペットを承認しないようにすることはできません。

```http
POST /rest/asset/v1/email/{id}/unapprove.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"3514#14a1832b0fa",
   "result":[
      {
         "id":1364
      }
   ]
}
```

## 削除

フォームを除き、承認とドラフトの状態を持つアセットは、削除前に未承認にする必要があります。 一般的に、アセットも未使用である必要があります。 フォルダーは空である必要があります。

プログラムは例外です。 プログラムとそのコンテンツがプログラム外で使用されていない場合は、プログラムとその子コンテンツを削除できます。

```http
POST /rest/asset/v1/program/{id}/delete.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "16501#14db042c6b7",
    "result": [
        {
            "id": 1109
        }
    ]
}
```

## タイムアウト

アセット APIのタイムアウトは300秒です。
