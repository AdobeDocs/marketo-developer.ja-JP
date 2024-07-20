---
title: プログラム
feature: REST API, Programs
description: プログラム情報を作成および編集します。
exl-id: 30700de2-8f4a-4580-92f2-7036905deb80
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 2%

---

# プログラム

[ プログラムエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs)

プログラムは、Marketo マーケティングアクティビティの中心組織コンポーネントです。 ほとんどのタイプのアセットの親となることができ、個々のマーケティング施策の中で、メンバーシップの追跡やリードの成功を可能にします。 プログラムは、LP、電子メールテンプレート、およびファイルを除くすべての種類のレコードの親にすることができます。

## プログラムタイプ

Marketoには 5 つの主要なタイプのプログラムがあります。

- デフォルト
- イベント
- オンライン セミナのあるイベント
- エンゲージメント
- メール

エンゲージメントプログラムは、他のタイプのプログラムの親になることができますが、デフォルト、ウェビナー付きイベントおよびイベントは、メールプログラムの親でしかありません。

プログラムには常にチャネルがあり、プログラムが作成されたチャネルから、可能なセットアッププログラムメンバーステータスを派生します。これは Get Channels API で取得できます。 プログラムには、一連のタグが関連付けられている場合もあります。 タグはカスタマイズ可能なフィールドで、任意の種類のプログラムに対してオプションまたは必須に設定できます。このフィールドの値は、Marketo管理で設定されたリストから選択されます。

## クエリ

プログラムは、タグタイプと値でクエリする追加のオプションを備えた、アセットクエリの標準のパターンに従います。 使用可能なタグと値は、[ タグタイプを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tags/operation/getTagTypesUsingGET) で取得できます。

### Id 別

[ID によるプログラムの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) エンドポイントには、`id` のパス パラメーターが必要です。

プログラム ID は、UI のプログラムの URL から取得できます（URL は `https://app-\*\*\*.marketo.com/#PG1001A1` のようになります）。 この URL の `id` は 1001 です。 URL の最初の文字セットと 2 番目の文字セットの間に必ず入ります。

```
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

[ 名前によるプログラムの取得 ](https://developer.adobe.com/marketo-apis/api/asset/) エンドポイントには、`name` のクエリパラメーターが必要です。 オプションのブール型クエリパラメーターは `includeTags` と `includeCosts` で、それぞれプログラムタグとプログラムコストを返すために使用されます。

```
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

[ プログラムの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) エンドポイントを使用すると、プログラムを参照できます。

オプションの `status` パラメーターを使用すると、プログラムステータスをフィルタリングできます。 このパラメーターは、エンゲージメントおよびメールプログラムにのみ適用されます。 使用可能な値は、エンゲージメントプログラムの場合は「オン」と「オフ」、メールプログラムの場合は「ロック解除」です。

オプションの `maxReturn` パラメーターは、返されるプログラムの数を制御します（最大は 200、デフォルトは 20）。 結果のページングに使用するオプションの `offset` パラメーター（デフォルトは 0）。

プログラムに関連付けられたタグは、このエンドポイントでは返されないことに注意してください。 プログラムタグは、[ プログラムを ID で取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByIdUsingGET) または [ プログラムを名前で取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByNameUsingGET) を使用して取得できます。

```
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

[ プログラムを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) エンドポイントの `earliestUpdatedAt` パラメーターと `latestUpdatedAt` パラメーターを使用すると、指定された範囲内に更新または最初に作成されたプログラムを返すために、日時の下限と上限を設定できます。

```
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

[ タグによるプログラムの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramListByTagUsingGET) エンドポイントは、提供されたタグタイプとタグ値に一致するプログラムのリストを取得します。

必須パラメーターは 2 つあります。`tagType` れはフィルタリング対象のタグのタイプで、`tagValue` れはフィルタリング対象のタグの値です。  返すプログラムの数を制御するオプションの整数 `maxReturn` パラメーター（最大は 200、デフォルトは 20）、および結果のページングに使用するオプションの整数 `offset` パラメーター（デフォルトは 0）があります。  結果はランダムな順序で返されます。

```
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

[]https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/createProgramUsingPOST）および [ 更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/updateProgramUsingPOST) プログラムは標準のアセットパターンに従い、必須パラメーターとして `folder`、`name`、`type` および `channel` を持ちます。`description`、`costs` および `tags` はオプションです。 チャネルとタイプは、プログラムの作成時にのみ設定できます。 作成後に更新できるのは、説明、名前、`tags` および `costs` のみで、追加の `costsDestructiveUpdate` パラメーターを使用できます。 `costsDestructiveUpdate` を true に渡すと、既存のコストがすべてクリアされ、呼び出しに含まれるコストに置き換えられます。 一部の購読では、一部のプログラムタイプにタグが必要になる場合があることに注意してください。ただし、これは設定に依存し、最初に「タグを取得」を使用して、インスタンス固有の要件があるかどうかを確認する必要があります。

メールプログラムを作成または更新する際に、`startDate` と `endDate` が渡される場合もあります。

### 作成

```
POST /rest/asset/v1/programs.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

プログラムコストを更新する場合、新しいコストを追加するには、`costs` 配列に追加するだけです。 破壊的な更新を実行するには、新しいコストを、パラメーター `costsDestructiveUpdate` を `true` に設定して渡します。 プログラムからすべてのコストをクリアするには、`costs` パラメーターを渡さず、設定 `costsDestructiveUpdate` を `true` に渡します。

```
POST /rest/asset/v1/program/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

メールプログラムは、リモートで承認または未承認になる場合があります。これにより、プログラムは指定された startDate に実行され、指定された endDate に終了します。 これらは両方とも、プログラムを承認するように設定し、UI から有効で承認されたメールとスマートリストを設定する必要があります。

### 承認

```
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

### 承認取消

```
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

[ プログラムのクローン作成 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/cloneProgramUsingPOST) は、新しい名前とフォルダーを必須パラメーターとして指定し、オプションで説明を付けた、標準のアセットパターンに従います。  `name` パラメーターは、グローバルに一意であり、255 文字を超えることはできません。  `folder` パラメーターは親フォルダーです。  `folder` パラメータータイプ属性は「フォルダー」に設定し、ターゲットフォルダーは、複製されるプログラムと同じワークスペースにある必要があります。

プッシュ通知、アプリ内メッセージ、レポート、ソーシャルAssetsなど、特定の種類のアセットを含んだプログラムは、この API を使用してクローンすることはできません。 アプリ内プログラムは、この API を使用して複製することはできません。

```
POST /rest/asset/v1/program/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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
