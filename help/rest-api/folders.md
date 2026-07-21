---
title: フォルダー
feature: REST API
description: 作成、更新、削除、IDと名前によるクエリ、ルート、ワークスペース、maxDepth、ページネーションを使用した一括参照について説明するフォルダー向けのMarketo REST API ガイド。
exl-id: 4b55c256-ef0a-42b4-9548-ff8a4106f064
TQID: https://experienceleague.adobe.com/OxCNdy8qW6jwq8u57RF9mqVKPVvH99UmuiOBjFprHCM
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: c5f60233-d5ea-4453-a799-0ad258b4d399id: d65b4a73-87a3-4d56-b638-74e74d9939ceid: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 806
ht-degree: 3%

---

# フォルダー

[フォルダーエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders)

フォルダーは、Marketoの主要な組織アセットです。 他のすべてのアセットタイプには、フォルダーまたはプログラムのいずれかの親が少なくとも1つあります。 フォルダーは純粋な組織ですが、プログラムは他のアセットタイプと機能的な関係を持ち、アセットを含めることもできます。

フォルダーAPIを使用して、フォルダーを作成、クエリ、更新、削除したり、フォルダーの内容を取得したりします。 フォルダークエリはプログラムを返すことができますが、プログラム APIを使用してプログラムを作成、更新、または削除する必要があります。

## クエリ

フォルダーは、標準のアセットクエリパターンをサポートしています：[ID別](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderByIdUsingGET)、[名前別](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderByNameUsingGET)、および[閲覧別](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderUsingGET)。

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

`type` パラメーターは必須で、`Folder`または`Program`である必要があります。 エンドポイントがフォルダーIDとプログラム IDのどちらを検索するかを決定します。 エンドポイントは、結果配列内の1つのレコードを返します。

応答`folderType`は、フォルダーに含めることができる内容を識別します。 マーケティングアクティビティフォルダーには、マーケティングフォルダーまたはプログラムのタイプがあり、複数のアセットタイプを含めることができます。 Design Studio フォルダーには、含めることができるアセットに対応するタイプがあります。 例えば、メールフォルダーには、メールテンプレートのフォルダータイプを持つメールとサブフォルダーを含めることができます。

フォルダーの種類は次のとおりです。

- メール
- メールテンプレート
- ランディングページ
- ランディングページテンプレート
- スニペット
- ファイル

### 名前別

名前による[ クエリ ](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderByNameUsingGET) エンドポイントには`name`が必要です。このエンドポイントは、フォルダー名と完全に一致し、一致するすべてのフォルダーを返します。

エンドポイントは、次のオプションのパラメーターも受け入れます。

- `type`: フォルダータイプ （`Folder`または`Program`）。
- `root`：検索するフォルダーのID。 `root`を設定する場合は、`type`も設定する必要があります。
- `workspace`：検索するワークスペースの名前。

```http
GET /rest/asset/v1/folder/byName.json?name=Test%2010%20-%20deverly
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "19#14e1f2f3688",
    "result": [
        {
            "name": "Test 10 - deverly",
            "description": "This is a test",
            "createdAt": "2015-06-23T06:27:04Z+0000",
            "updatedAt": "2015-06-23T06:27:04Z+0000",
            "url": "https://app-abm.marketo.com/#MF1070A1",
            "folderId": {
                "id": 454,
                "type": "FOLDER"
            },
            "folderType": "Marketing Folder",
            "parent": {
                "id": 416,
                "type": "FOLDER"
            },
            "path": "/Marketing Activities/Default/Marketing Programs - deverly/Test 10 - deverly",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 454
        }
    ]
}
```

マーケティングアクティビティとDesign Studioはルートフォルダーです。 いずれかのルートを名前で取得し、そのルートを使用して宛先インスタンスのフォルダー階層をトラバースします。

### 参照

また、[ フォルダーを一括で取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderUsingGET)することもできます。 クエリする親フォルダーを指定するには、`root` パラメーターを使用します。 2つのメンバーを持つ埋め込みJSON オブジェクトとして`root`を渡します。

1. `id`: フォルダーまたはプログラムのID。
1. `type`: ルートフォルダーのタイプに応じて、`Folder`または`Program`のいずれかです。

ルートフォルダーがわからない場合、またはエリア内のすべてのフォルダーを取得する場合は、Marketing Activities、Design Studio、またはLead Database ルートを使用します。 エリア名を[名前でフォルダーを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderByNameUsingGET) APIに渡して、ルート IDを取得します。

他の一括アセット取得エンドポイントと同様に、ページネーションにはオプションの`offset`および`maxReturn` パラメーターを使用します。 他のオプションのパラメーターは次のとおりです。

- `workSpace`：フィルタリングするワークスペースの名前。
- `maxDepth`: フォルダー階層内でトラバースするレベルの最大数。 値0は、`root`で指定されたフォルダーのみを返します。 デフォルトは2です。

```http
GET /rest/asset/v1/folders.json?root={"id":14,"type":"Folder"}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "9bd8#14e1f49047c",
    "result": [
        {
            "name": "Marketing Activities",
            "description": "Root node for the Marketing Activities app area",
            "createdAt": "2010-03-27T18:27:45Z+0000",
            "updatedAt": "2010-03-27T18:27:45Z+0000",
            "url": null,
            "folderId": {
                "id": 14,
                "type": "Folder"
            },
            "folderType": "Zone",
            "parent": null,
            "path": "/Marketing Activities",
            "isArchive": false,
            "isSystem": true,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 14
        },
        {
            "name": "Default",
            "description": "Root node of the Marketing activities Default",
            "createdAt": "2010-03-27T18:27:45Z+0000",
            "updatedAt": "2010-03-27T18:27:45Z+0000",
            "url": null,
            "folderId": {
                "id": 15,
                "type": "Folder"
            },
            "folderType": "Zone",
            "parent": {
                "id": 14,
                "type": "Folder"
            },
            "path": "/Marketing Activities/Default",
            "isArchive": false,
            "isSystem": true,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 15
        },
        {
            "name": "Archive",
            "description": "",
            "createdAt": "2010-03-27T18:28:17Z+0000",
            "updatedAt": "2010-03-27T18:28:17Z+0000",
            "url": "https://app-abm.marketo.com/#MF157A1",
            "folderId": {
                "id": 310,
                "type": "Folder"
            },
            "folderType": "Marketing Folder",
            "parent": {
                "id": 15,
                "type": "Folder"
            },
            "path": "/Marketing Activities/Default/Archive",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 310
        }
    ]
}
```

## 応答構造

`folderId`および`parent` フィールドは、フォルダーIDとタイプを含むJSON オブジェクトです。 APIは、このタイプをクエリ、`root`、および`parent` パラメーターで使用して、フォルダーとプログラムフォルダーのタイプを区別します。

`folderType` フィールドは、フォルダーの使用方法を説明します。 その値は、マーケティングフォルダー、プログラム、電子メール、メールテンプレート、ランディングページ、ランディングページテンプレート、スニペット、画像、ゾーン、ファイルのいずれかです。 マーケティングフォルダーとプログラムはマーケティングアクティビティに存在し、複数のアセットタイプを含めることができます。 その他のフォルダータイプには、対応するアセットタイプ、サブフォルダー、および該当する場合はそのアセットタイプのテンプレートバージョンのみが含まれます。 ゾーンは、マーケティングアクティビティのルートレベルのフォルダーを表します。

フォルダー`path`は、その階層をUnix スタイルのパスとして表示します。 最初のエントリは、常に「マーケティング活動」または「デザインスタジオ」です。 インスタンスにワークスペースがある場合、2番目のエントリは所有ワークスペース名です。

`url` フィールドには、指定されたインスタンスのアセット URLが含まれています。 ユニバーサルリンクではなく、ユーザー認証が必要です。 `isSystem` フィールドは、フォルダーが読み取り専用のシステムフォルダーであるかどうかを示します。 システムフォルダーの下に子フォルダーを作成できます。

## 作成と更新

フォルダー](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/createFolderUsingPOST)を[作成するには、次のパラメーターを使用して`application/x-www-form-urlencoded` POST リクエストを送信します。

- `name`: フォルダー名を含む必要な文字列。
- `parent`: `id`と`type`を含む必須の埋め込みJSON オブジェクト。 親に応じて、タイプは`Folder`または`Program`です。
- `description`：最大2000文字のオプション文字列。

```http
POST /rest/asset/v1/folders.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
parent={"id":416,"type":"Folder"}&name=Test 10 - deverly&description=This is a test
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "111be#14e1f193e31",
    "result": [
        {
            "name": "Test 10 - deverly",
            "description": "This is a test",
            "createdAt": "2015-06-23T06:27:04Z+0000",
            "updatedAt": "2015-06-23T06:27:04Z+0000",
            "url": "https://app-abm.marketo.com/#MF1070A1",
            "folderId": {
                "id": 454,
                "type": "FOLDER"
            },
            "folderType": "Marketing Folder",
            "parent": {
                "id": 416,
                "type": "FOLDER"
            },
            "path": "/Marketing Activities/Default/Test 10 - deverly",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 454
        }
    ]
}
```

更新エンドポイントを使用して、オプションの`description`、`name`または`isArchive` パラメーターを変更します。 `isArchive`を`true`に設定すると、Marketo UIにフォルダーがアーカイブされます。 `false`に設定すると、フォルダーがアーカイブから削除されます。

このAPIを使用してプログラムを更新することはできません。

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

### 削除

1つのフォルダーを削除できるのは、アセットまたはサブフォルダーが含まれていない場合のみです。 このAPIを使用して、`isSystem` フィールドが`true`のプログラムまたはフォルダーを削除することはできません。

```http
POST /rest/asset/v1/folder/{id}/delete.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "4180#14e1f3fc017",
    "result": [
        {
            "id": 453
        }
    ]
}
```
