---
title: チャネル
feature: REST API
description: Asset REST API を使用してMarketo チャネルをクエリする方法、ページネーションを使用して参照する方法または名前で取得する方法、進捗ステータスを表示する方法およびプログラムタイプルールを理解する方法について説明します。
exl-id: ec6c279f-a7b4-4a7c-b980-1a68045f37ce
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 82%

---

# チャネル

[チャネルエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Channels)

チャネルは、すべてのプログラムタイプに標準の必須フィールドです。各タイプのチャネルは、指定された `applicableProgramType` タイプでのみ使用でき、各プログラムのプログラムメンバーに有効な使用可能なプログラムステータスのリストを提供します。プログラムの作成後にチャネルのプログラムステータスを変更した場合、リードが変更される可能性のあるプログラムステータスのリストは、その時点でチャネルによって提供されたリストと一致しますが、既存のプログラムメンバーシップレコードのプログラムステータスが遡及的に変更されることはありません。

## クエリ

チャネルは、標準アセットとしてクエリを実行できますが、ID でチャネルを取得するエンドポイントはありません。

### 参照

```
GET /rest/asset/v1/channels.json?offset=10
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "651#1504ebbbfcf",
    "result": [
        {
            "id": 3,
            "name": "Blog",
            "applicableProgramType": "program",
            "progressionStatuses": [
                {
                    "name": "Not in Program",
                    "step": 0,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Invited",
                    "step": 10,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Visited Booth",
                    "step": 20,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Influenced",
                    "step": 30,
                    "description": null,
                    "hidden": false,
                    "success": true
                }
            ],
            "createdAt": "2015-07-15T11:40:57Z+0000",
            "updatedAt": "2015-07-15T11:40:57Z+0000"
        },
        {
            "id": 4,
            "name": "Online Advertising",
            "applicableProgramType": "program",
            "progressionStatuses": [
                {
                    "name": "Not in Program",
                    "step": 0,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Invited",
                    "step": 10,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Registered",
                    "step": 20,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "No Show",
                    "step": 30,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Attended",
                    "step": 40,
                    "description": null,
                    "hidden": false,
                    "success": true
                }
            ],
            "createdAt": "2015-07-15T11:40:58Z+0000",
            "updatedAt": "2015-07-15T11:40:58Z+0000"
        }
    ]
}
```

### 名前別

```
GET /rest/asset/v1/channel/byName.json?name=Online Advertising
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "394c#1504eb476ed",
    "result": [
        {
            "id": 4,
            "name": "Online Advertising",
            "applicableProgramType": "program",
            "progressionStatuses": [
                {
                    "name": "Not in Program",
                    "step": 0,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Invited",
                    "step": 10,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Registered",
                    "step": 20,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "No Show",
                    "step": 30,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Attended",
                    "step": 40,
                    "description": null,
                    "hidden": false,
                    "success": true
                }
            ],
            "createdAt": "2015-07-15T11:40:58Z+0000",
            "updatedAt": "2015-07-15T11:40:58Z+0000"
        }
    ]
}
```
