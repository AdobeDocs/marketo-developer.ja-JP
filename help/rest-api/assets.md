---
title: アセット
feature: REST API
description: Marketo アセットを操作する API。
exl-id: 4273a5b1-1904-46e8-b583-fc6f46b388d2
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '876'
ht-degree: 100%

---

# アセット

Marketo には、Marketo 内のほとんどのマーケティングアセットおよび組織アセットとやり取りする API が用意されています。

## アセット

Marketo アセットには、次のものが含まれます。

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

パラメーターやモデリング情報を含む Asset API エンドポイントの完全なリストについて詳しくは、[Asset API エンドポイント参照](endpoint-reference.md)を参照してください。

## クエリ

アセットは通常、ID 別、名前別、参照別の 3 つのパターンで取得できます。ID 別と名前別の両方で、指定したパラメーターの単一のアセットを取得しますが、参照では、このタイプのアセットのリスト全体を返してページングできます。個々のタイプのアセットにはフィルタリングに使用できる様々なパラメーターがあるので、詳しくは、個々のドキュメントを参照してください。

場合によっては、一部のアセットタイプの参照エンドポイントでは、タグの許容値などの子アセットを返さないので、メタデータの完全なセットを返すには、名前別エンドポイントまたは ID 別エンドポイントを使用して個別に取得する必要があります。その他のアセットタイプには、フォームフィールドなどの依存オブジェクトを取得するエンドポイントがまったく別に存在する場合があります。

### ID 別

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

技術的な理由により、Asset API はコンマ（,）を含むアセット名を検索できません。命名規則では、すべてのアセットタイプに対してコンマを除外することをお勧めします。

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

アセットの参照では、常に次の 2 つのクエリパラメーターが許可されます。

- offset - 結果を返す整数のオフセット。
- maxReturn - 返されるレコードの数を制限します。未設定の場合のデフォルト値は 20 で、最大値は 200 です。

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

フォルダー、トークン、ファイルなどのシンプルなアセットタイプの場合、通常は作成用のエンドポイントは 1 つだけで、ID 別のレコードの更新用に追加のエンドポイントがあります。アセットは、常に必要な名前で作成し、その後、メタデータと ID が作成または更新応答によって返されます。

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

他のアセットは、構造がより複雑で、追加のサブセクションや子オブジェクトの更新が必要であり、最終的には承認を受けて初めて使用できます。これらのアセットタイプには、フォーム、メール、メールテンプレート、ランディングページ、ランディングページテンプレートが含まれます。これらにはそれぞれ、レコードを作成する単一のエンドポイントがあり、次にメタデータ、コンテンツ、コンテンツセクションを更新する追加のエンドポイントがあります。

例えば、ランディングページを作成するには、テンプレート ID を使用して作成エンドポイントを呼び出し、コンテンツセクションを取得し、各セクションを個別に更新してコンテンツを追加してから、承認してライブでデプロイできるようにする必要があります。

### 複雑な作成

ランディングページでは、最初に親テンプレートを使用して、ランディングページアセットを作成する必要があります。これにより、各コンテンツセクションのテンプレートのデフォルトコンテンツを含む新しいランディングページが作成されます。

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

#### セクションの取得

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

メール、ランディングページ、スニペット、フォームおよび対応するテンプレートを含む多くのアセットタイプには、関連するドラフトおよび承認システムがあります。アセットを承認しようとすると、特定の検証ルールのセットに対してアセットが評価され、承認済み状態に設定される、失敗の理由が返されます。これらのタイプのアセットの場合、特定のアセットのコンテンツを更新するたびに、アセットのドラフトに変更が行われ、承認済みバージョンには影響しません。これにより、アセットのライブバージョンに影響を与えることなく、コンテンツを安全に変更できます。その後、変更を、承認エンドポイントを使用してライブバージョンに適用できます。また、これにより、追加の更新が適用されるまで、アセットのドラフト状態もクリアされます。

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

承認が成功すると、以前のライブバージョンが更新されたバージョンに置き換えられます。

また、ドラフトの破棄は、有効なアセットタイプごとにエンドポイントを通じても実行できます。承認済みでドラフト状態のアセットにこれを使用すると、現在のドラフトと保留中の変更がすべて破棄されます。現在承認済みのバージョンがないアセットに対してこれを使用しても、何も実行されず、エラーが返されます。ドラフトのみのアセットは削除できますが、破棄できません。

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

また、アセットが承認のみされている状態では、承認されていない状態になることもあります。これにより、アセットのライブバージョンがすべて削除され、アセットがドラフトのみの状態に戻され、関連するドラフトも破棄されます。このアクションは、アセットが Marketo 内のどこにも使用されていない場合にのみ、ほとんどのアセットに対して実行できます（例：メールが「メールを送信」フローステップで参照されていたり、スニペットがメールに埋め込まれていたりしない）。

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

フォームを除き、承認およびドラフト状態のアセットは、承認されている間は削除できません。削除する前に未承認にする必要があります。削除は通常、アセットの場合は未承認で使用されておらず、フォルダーの場合はアセットが空の場合にのみ実行できます。注目すべき例外の 1 つはプログラムです。プログラムは、プログラムとそのコンテンツがプログラムの範囲外で使用されていない限り、すべての子コンテンツと共に削除できます。

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
