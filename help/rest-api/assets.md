---
title: アセット
feature: REST API
description: Marketo Assets を操作するための API。
exl-id: 4273a5b1-1904-46e8-b583-fc6f46b388d2
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 2%

---

# アセット

Marketoは、Marketo内のほとんどのマーケティングアセットや組織的なアセットとやり取りするための API を提供します。

## アセット

Marketo アセットには次のものが含まれます。

- フォルダー
- プログラム
- メール
- メールテンプレート
- ランディングページ
- ランディングページのテンプレート
- スニペット
- フォーム
- トークン
- ファイル

## API

パラメーターやモデリング情報を含む、Asset API エンドポイントの完全なリストについては、[Asset API エンドポイントのリファレンス ](endpoint-reference.md) を参照してください。

## クエリ

Assetsには通常、id、名前、参照の 3 つのパターンがあり、それによって取得できます。  ID と名前の両方で、特定のパラメーターに対して 1 つのアセットを取得し、ブラウジングは、そのタイプのアセットのリスト全体を返してページングを許可します。  個々のタイプのアセットには、フィルタリングできる様々なパラメーターがあるので、詳しくは、個々のドキュメントを参照してください。

場合によっては、タグの許容値など、一部のアセットタイプの参照エンドポイントが子アセットを返さないので、メタデータの完全なセットを返すには、名前別または ID 別のエンドポイントを使用して個別に取得する必要があります。  また、フォームフィールドなどの依存オブジェクトを取得するために、完全に別個のエンドポイントを持つ場合もあります。

### Id 別

```
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

技術的な理由により、Asset API はコンマ（,）を含むアセット名を検索できません。  すべてのアセットタイプについて、命名規則でコンマを除外することをお勧めします。

```
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

アセットを参照すると、常に 2 つのクエリパラメーターが許可されます。

- offset – 結果を返す整数のオフセット。
- maxReturn – 返されるレコードの数を制限します。  未設定の場合のデフォルト値は 20 で、最大値は 200 です。

```
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

フォルダー、トークン、ファイルなどのシンプルなアセットタイプの場合、通常、作成するエンドポイントは 1 つだけで、レコードを ID で更新するエンドポイントは 1 つ追加です。  Assetsは、常に必須の名前で作成され、メタデータと ID が create または update 応答から返されます。

例えば、トークンの作成方法を次に示します。

```
POST /rest/asset/v1/folder/{id}/tokens.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

フォルダーを更新するには、次の操作を実行します。

```
POST /rest/asset/v1/folder/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

他のアセットの構造はより複雑で、追加のサブセクションや子オブジェクトを更新する必要があるので、最終的に承認してから使用する必要があります。  これらのアセットタイプには、Forms、メール、メールテンプレート、ランディングページおよびランディングページテンプレートが含まれます。  これらにはそれぞれ、レコードを作成するためのエンドポイントと、メタデータ、コンテンツおよびコンテンツセクションを更新するための追加のエンドポイントが含まれます。

例えば、ランディングページを作成するには、その作成エンドポイントをテンプレート ID を使用して呼び出した後、そのコンテンツセクションを取得し、各セクションを個別に更新してコンテンツを追加してから、承認してライブでデプロイできるようにする必要があります。

### 複雑な作成

ランディングページでは、まず親テンプレートを使用してランディングページアセットを作成する必要があります。  これにより、各コンテンツセクションのテンプレートのデフォルトコンテンツを含む新しいランディングページが作成されます。

```
POST rest/asset/v1/landingPages.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

#### セクションを取得

ランディングページのコンテンツを入力するには、コンテンツセクションのリストを取得し、テンプレートから外れたセクションに対して個別に更新を実行する必要があります。

```
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

```
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

多くのアセットタイプには、関連するドラフトおよび承認システムがあります。これには、メール、ランディングページ、スニペット、Formsおよび対応するテンプレートが含まれます。  アセットを承認しようとすると、特定の検証ルールセットに対してアセットが評価され、その後、アセットが承認済みの状態に設定されるか、エラー理由が返されます。  このタイプのアセットの場合、特定のアセットのコンテンツに更新が加えられるたびに、アセットのドラフトに変更が加えられますが、これは承認されたバージョンには影響しません。  これにより、アセットのライブバージョンに影響を与えることなく、コンテンツに対する変更を安全に行うことができます。  その後、承認エンドポイントを使用して、変更内容をライブバージョンに適用できます。  また、追加の更新が適用されるまで、アセットのドラフト状態がクリアされます。

```
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

正常に承認されると、以前のライブバージョンが更新されたバージョンに置き換えられます。

ドラフトの破棄は、有効な各アセットタイプのエンドポイントを通じて利用することもできます。  ドラフトで承認済み状態のアセットでこれを使用すると、現在のドラフトと、保留中の変更がすべて破棄されます。  現在承認されたバージョンがないアセットでこれを使用しても、何も実行されず、エラーが返されます。  ドラフトのみのアセットは削除できますが、破棄することはできません。

```
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

また、Assetsが承認専用状態の場合は、承認を取り消すこともできます。  これにより、アセットのライブバージョンがすべて削除され、アセットがドラフトのみの状態に戻ると同時に、関連するドラフトも破棄されます。  このアクションは、メール送信フローステップで参照されるメールや、メールに埋め込まれるスニペットなど、Marketoで使用されていない場合にのみ、ほとんどのアセットで実行できます。

```
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

承認を含むAssetsおよび下書きの状態（フォームを除く）は、承認中は削除できません。また、削除する前に承認を取り消す必要があります。  削除は通常、アセットが未承認で未使用の場合、およびフォルダーが空の場合にのみ実行できます。  顕著な例外はプログラムです。プログラムとその内容がプログラムの範囲外で使用されていない限り、プログラムはその子コンテンツと共に削除できます。

```
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

Asset API のタイムアウトは 300 秒です
