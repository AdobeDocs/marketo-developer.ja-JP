---
title: プログラム
feature: REST API, Programs
description: IDまたは名前で取得し、参照し、ステータスでフィルタリングする種類、チャネル、タグ、メンバーステータス、エンドポイントについて説明する、Asset REST API用のMarketo プログラムガイド。
exl-id: 30700de2-8f4a-4580-92f2-7036905deb80
TQID: https://experienceleague.adobe.com/5ILyahSn3Pp-lF6YPogVnkXjXP-QLtEmyLm7iKMIgo0
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: a7170d27-32ab-462b-a333-269abc654483id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45id: e64968b2-4ee5-47f9-8cae-0588f184b9ebid: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 741
ht-degree: 12%

---

# プログラム

[プログラムエンドポイントリファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs)

プログラムは、Marketoのマーケティングアクティビティを整理し、個々のマーケティング施策のリードメンバーシップと成功を追跡します。 プログラムには、ランディングページ、メールテンプレート、ファイル以外のほとんどのアセットタイプを含めることができます。

## プログラムタイプ

Marketo には、5 つのコアとなるプログラムタイプがあります。

- デフォルト
- イベント
- オンライン セミナのあるイベント
- エンゲージメント
- メール

エンゲージメントプログラムには、他のあらゆるプログラムタイプを含めることができます。 ウェビナープログラムのデフォルト、イベント、イベントには、メールプログラムのみを含めることができます。

どんなプログラムにもチャネルがあります。 このチャネルは、使用可能なプログラムメンバーのステータスを定義し、Get Channels APIを使用して取得できます。

プログラムにはタグを付けることもできます。 タグは、プログラムタイプに応じてオプションまたは必須にできる、カスタマイズ可能なフィールドです。 各タグは、Marketo Adminで設定されたリストの値を使用します。

## クエリ

ID、名前、ブラウジング、またはタグの種類と値でプログラムをクエリします。 [ タグの種類を取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Tags/operation/getTagTypesUsingGET)して、使用可能なタグと値を取得します。

### ID 別

[ID によるプログラムを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5)エンドポイントには、`id` パスパラメーターが必要です。

プログラム IDは、`https://app-\*\*\*.marketo.com/#PG1001A1`などのUI URLから取得できます。 この例では、最初と2番目の文字セットの間のIDは`1001`です。

```http
GET /rest/asset/v1/program/{id}.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "948f#14db037ec71",
    "result": [
        {
            "id": 1107,
            "name": "AAA2QueryProgramName",
            "description": "AssetAPI: getProgram tests",
            "createdAt": "2015-05-21T22:45:13Z+0000",
            "updatedAt": "2015-05-21T22:45:13Z+0000",
            "url": "https://app-devlocal1.marketo.com/#PG1107A1",
            "type": "Default",
            "channel": "Online Advertising",
            "folder": {
                "type": "Folder",
                "value": 1910,
                "folderName": "ProgramQueryTestFolder"
            },
            "status": "",
            "workspace": "Default",
            "tags": [
                {
                    "tagType": "AAA1 Required Tag Type",
                    "tagValue": "AAA1 RT1"
                }
            ],
            "costs": null,
            "headStart": false
        }
    ]
}
```

### 名前別

[名前によるプログラムを取得](https://developer.adobe.com/marketo-apis/api/asset)エンドポイントには、`name` クエリパラメーターが必要です。 タグとコストをそれぞれ返すために、オプションのブール値パラメーター`includeTags`と`includeCosts`を設定します。

```http
GET /rest/asset/v1/program/byName.json?name=TestProgramName&includeTags=true
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "16026#14db03e070c",
    "result": [
        {
            "id": 1107,
            "name": "AAA2QueryProgramName",
            "description": "AssetAPI: getProgram tests",
            "createdAt": "2015-05-21T22:45:13Z+0000",
            "updatedAt": "2015-05-21T22:45:13Z+0000",
            "url": "https://app-devlocal1.marketo.com/#PG1107A1",
            "type": "Default",
            "channel": "Online Advertising",
            "folder": {
                "type": "Folder",
                "value": 1910,
                "folderName": "ProgramQueryTestFolder"
            },
            "status": "",
            "workspace": "Default",
            "tags": [
                {
                    "tagType": "AAA1 Required Tag Type",
                    "tagValue": "AAA1 RT1"
                }
            ],
            "costs": null,
            "headStart": false
        }
    ]
}
```

### 参照

プログラムを参照するには、[ プログラムを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5) エンドポイントを使用します。

オプションの`status` パラメーターは、エンゲージメントおよびメールプログラムをステータス別にフィルタリングします。 有効な値は、エンゲージメントプログラムでは`on`と`off`、メールプログラムでは`unlocked`です。

オプションの`maxReturn` パラメーターは、返されるプログラムの数を制御します。 デフォルトは20、最大は200です。 ページネーションにはオプションの`offset` パラメーターを使用します。デフォルトは0です。

このエンドポイントはプログラムタグを返しません。 ID](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramByIdUsingGET)または[名前](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramByNameUsingGET)でプログラムを取得[ プログラムを取得する タグを取得します。

```http
GET /rest/asset/v1/programs.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "7a39#1511bf8a41c",
    "result": [
        {
            "id": 1035,
            "name": "clone it",
            "description": "",
            "createdAt": "2015-11-18T15:25:35Z+0000",
            "updatedAt": "2015-11-18T15:25:46Z+0000",
            "url": "https://app-devlocal1.marketo.com/#NP1035A1",
            "type": "Engagement",
            "channel": "Nurture",
            "folder": {
                "type": "Folder",
                "value": 28,
                "folderName": "Nurturing"
            },
            "status": "on",
            "workspace": "Default",
            "headStart": false
        },
        {
            "id": 1032,
            "name": "email prog",
            "description": "",
            "createdAt": "2015-11-18T14:56:28Z+0000",
            "updatedAt": "2015-11-18T14:56:28Z+0000",
            "url": "https://app-devlocal1.marketo.com/#EBP1032A1",
            "type": "Email",
            "channel": "Email Send",
            "folder": {
                "type": "Folder",
                "value": 26,
                "folderName": "Data Management"
            },
            "status": "unlocked",
            "workspace": "Default",
            "headStart": false
        }
    ]
}
```

### 日付範囲別

`earliestUpdatedAt`および`latestUpdatedAt` パラメーターと[ プログラムの取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5)を使用して、低い日時と高い日時の境界を設定します。 エンドポイントは、範囲内で作成または更新されたプログラムを返します。

```http
GET /rest/asset/v1/programs.json?earliestUpdatedAt=2017-01-01T00:00:00-05:00&latestUpdatedAt=2017-01-30T00:00:00-05:00
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "1225a#15f82a83875",
    "warnings": [],
    "result": [
        {
            "id": 1070,
            "name": "Bulk Import - Test",
            "description": "",
            "createdAt": "2017-01-13T19:34:17Z+0000",
            "updatedAt": "2017-01-13T19:34:18Z+0000",
            "url": "https://app-abm.marketo.com/#PG1070A1",
            "type": "Default",
            "channel": "Content",
            "folder": {
                "type": "Folder",
                "value": 637,
                "folderName": "Avention"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
        },
        {
            "id": 1069,
            "name": "Program With Email",
            "description": "",
            "createdAt": "2017-01-03T22:53:14Z+0000",
            "updatedAt": "2017-01-03T22:53:15Z+0000",
            "url": "https://app-abm.marketo.com/#EBP1069A1",
            "type": "Email",
            "channel": "Email Send",
            "folder": {
                "type": "Folder",
                "value": 621,
                "folderName": "Smartling"
            },
            "status": "unlocked",
            "workspace": "Default",
            "headStart": false
        },
        {
            "id": 1071,
            "name": "Program with Guided Landing Page Template",
            "description": "",
            "createdAt": "2017-01-24T22:59:21Z+0000",
            "updatedAt": "2017-01-24T22:59:22Z+0000",
            "url": "https://app-abm.marketo.com/#PG1071A1",
            "type": "Default",
            "channel": "Content",
            "folder": {
                "type": "Folder",
                "value": 621,
                "folderName": "Smartling"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
        },
        {
            "id": 1047,
            "name": "ReachForce List Update",
            "description": "",
            "createdAt": "2016-05-24T19:38:35Z+0000",
            "updatedAt": "2017-01-13T19:28:09Z+0000",
            "url": "https://app-abm.marketo.com/#PG1047A1",
            "type": "Default",
            "channel": "Content",
            "folder": {
                "type": "Folder",
                "value": 407,
                "folderName": "Everly Tests"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
        }
    ]
}
```

### タグタイプ別

タグ別[ プログラムを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramListByTagUsingGET) エンドポイントは、指定されたタグの種類と値に一致するプログラムを返します。

`tagType`および`tagValue` パラメーターが必要です。 オプションの整数`maxReturn`は、返されるプログラムの数を制御します。デフォルトは20、最大値は200です。 ページネーションにはオプションの整数`offset`を使用します。デフォルトは0です。 結果はランダムな順序で返されます。

```http
GET /rest/asset/v1/program/byTag.json?tagType=Presenter&tagValue=Dennis
```

```json
{
    "success" : true,
    "warnings" : [],
    "errors" : [],
    "requestId" : "13b6d#152b38d5be4",
    "result" : [{
            "id" : 1004,
            "name" : "It's a Program",
            "description" : "",
            "createdAt" : "2013-02-26T00:37:37Z+0000",
            "updatedAt" : "2013-03-11T15:32:02Z+0000",
            "url" : "https://app-sjst.marketo.com/#PG1004A1",
            "type" : "Default",
            "channel" : "Email Blast",
            "folder" : {
                "type" : "Folder",
                "value" : 38,
                "folderName" : "Test"
            },
            "status" : "",
            "workspace" : "Default",
            "tags" : [{
                    "tagType" : "Presenter",
                    "tagValue" : "Dennis"
                }
            ],
                        "headStart": false
    ]
}
```

## 作成と更新

[ プログラムを](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/createProgramUsingPOST)作成するには、`folder`、`name`、`type`および`channel`が必要です。 オプションのパラメーターは`description`、`costs`および`tags`です。 一部のサブスクリプションでは、特定のプログラムタイプにタグが必要です。 Get Tagsを使用して、インスタンスの要件を確認します。

[更新中](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/updateProgramUsingPOST)に変更できるのは、説明、名前、`tags`および`costs`のみです。 チャネルとタイプは、作成時にのみ設定できます。 `costsDestructiveUpdate`を`true`に設定すると、既存のコストがすべてクリアされ、リクエストに含まれるコストに置き換えられます。

メールプログラムを作成または更新する際に、`startDate` と `endDate` を UTC 日時として渡すこともできます。

`"startDate": "2022-10-19T15:00:00.000Z"`
`"endDate": "2022-10-19T15:00:00.000Z"`

### 作成

```http
POST /rest/asset/v1/programs.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=API Test Program&folder={"id":1035,"type":"Folder"}&description=Sample API Program&type=Default&channel=Email Blast&costs=[{"startDate":"2015-01-01","cost":2000}]
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "d505#14d9bd96352",
    "result": [
        {
            "id": 1207,
            "name": "newProgram",
            "description": "This is a test",
            "createdAt": "2015-05-28T18:47:15Z+0000",
            "updatedAt": "2015-05-28T18:47:15Z+0000",
            "url": "https://app-devlocal1.marketo.com/#ME1207A1",
            "type": "Event",
            "channel": "channelOne",
            "folder": {
                "type": "Folder",
                "value": 59,
                "folderName": "blah blah"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
            "tags": null,
            "costs": [
                {
                    "startDate":"2015-01-01",
                    "cost":2000
                }
            ]
        }
    ]
}
```

### 更新

プログラムのコストを追加するには、それらを`costs`配列に追加します。 既存のコストを置き換えるには、新しいコストを渡し、`costsDestructiveUpdate`を`true`に設定します。 すべてのコストをクリアするには、`costs`を省略し、`costsDestructiveUpdate`を`true`に設定します。

```http
POST /rest/asset/v1/program/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
description=This is an updated description&name=Updated Program Name&costs=[{"startDate":"2016-01-01","cost":200,"note":"Google Adwords"}]
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "5c37#14db05608aa",
    "result": [
        {
            "id": 1110,
            "name": "Updated Program Name",
            "description": "This is a updated description",
            "createdAt": "2015-05-21T22:45:14Z+0000",
            "updatedAt": "2015-06-01T18:13:58Z+0000",
            "url": "https://app-devlocal1.marketo.com/#NP1110A1",
            "type": "Engagement",
            "channel": "Nurture",
            "folder": {
                "type": "Folder",
                "value": 1910,
                "folderName": "ProgramQueryTestFolder"
            },
            "status": "on",
            "workspace": "Default",
            "headStart": false,
            "tags": [
                {
                    "tagType": "AAA1 Required Tag Type",
                    "tagValue": "AAA1 RT1"
                },
                {
                    "tagType": "tagTypeOne",
                    "tagValue": "tagTypeValue1"
                }
            ],
            "costs": [
                {
                    "startDate": "2016-01-01",
                    "cost": 200,
                    "note": "Google Adwords"
                }
            ]
        }
    ]
}
```

## 承認

メールプログラムをリモートで承認または未承認にすることができます。 承認されたプログラムは`startDate`で実行され、`endDate`で終了します。

承認前に、日付を設定し、UIで有効で承認済みの電子メールとスマートリストを設定します。

### 承認

```http
POST /rest/asset/v1/program/{id}/approve.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "16026#150b5bf7692",
    "result": [
        {
            "id": 11062
        }
    ]
}
```

### 未承認

```http
POST /rest/asset/v1/program/{id}/unapprove.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "16026#150b5bf7692",
    "result": [
        {
            "id": 11062
        }
    ]
}
```

## 複製

[ プログラムの複製](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/cloneProgramUsingPOST)には、新しい名前と親フォルダーが必要です。 説明はオプションです。 `name`はグローバルに一意である必要があり、255文字を超えることはできません。

`folder` パラメーターのtype属性を`Folder`に設定します。 ターゲットフォルダーは、ソースプログラムと同じワークスペースにある必要があります。

このAPIを使用して、プッシュ通知、アプリ内メッセージ、レポート、ソーシャルアセットを含むアプリ内プログラムまたはプログラムを複製することはできません。

```http
POST /rest/asset/v1/program/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=Cloned Program - PHP&folder={"id":5562,"type":"Folder"}&description=Description
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "3a7f#14db06990cc",
    "result": [
        {
            "id": 1221,
            "name": "cloneProgram",
            "description": "This is a description for the cloned program",
            "createdAt": "2015-06-01T18:36:57Z+0000",
            "updatedAt": "2015-06-01T18:36:57Z+0000",
            "url": "https://app-devlocal1.marketo.com/#PG1221A1",
            "type": "Default",
            "channel": "Blog",
            "folder": {
                "type": "Folder",
                "value": 59,
                "folderName": "blah blah"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
            "tags": null,
            "costs": null
        }
    ]
}
```

## プログラムの削除

プログラムの削除は、標準のアセット削除パターンに従います。

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
