---
title: フォルダー
feature: REST API
description: Marketo API を使用したフォルダーの操作。
exl-id: 4b55c256-ef0a-42b4-9548-ff8a4106f064
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 1%

---

# フォルダー

[ フォルダーエンドポイントの参照 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders)

フォルダーはMarketoの中核的な組織資産であり、その他のすべてのタイプのアセットには少なくとも 1 つのフォルダーが親として含まれています。 この親フォルダーは、純粋に組織的なフォルダー、または他のアセットタイプとの機能上の関係を持ち、他のアセットの親でもあるプログラムの場合があります。 API を使用して、フォルダーの作成、クエリ、更新、削除を行うことができます。また、フォルダーのコンテンツのリストを取得することもできます。 プログラムは Folders API に対するクエリを通じて返すことができますが、プログラムの作成、更新、削除はプログラム API を通じて実行する必要があります。

## クエリ

フォルダーのクエリは、[by id](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByIdUsingGET)、[by name](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByNameUsingGET) および [browsing](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderUsingGET) のアセットに対する、標準のクエリタイプに従います。

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

type パラメーターは必須で、&quot;Folder&quot;または&quot;Program&quot;のいずれかである必要があります。  タイプは、フォルダーへの参照をフォルダー ID とプログラム ID のどちらに対して行うかを指定します。 このエンドポイントの場合、結果の配列で返されるレコードは 1 つだけです。 応答に folderType パラメーターがあります。 これは、様々な種類のフォルダーを示す場合があります。 Marketo アクティビティフォルダーにはタイプが「マーケティングフォルダー」または「プログラム」のどちらかがあり、様々なタイプのアセットを格納できます。一方、Design Studio フォルダーには、保持できるアセットタイプに対応するタイプがあります。 例えば、folderType が「Email」のフォルダーには、Emails または他のサブフォルダーのみが含まれ、folderType が Email または Email テンプレートである場合があります。 タイプには以下が含まれます。

- メール
- メールテンプレート
- ランディングページ
- ランディングページテンプレート
- スニペット
- ファイル

### 名前別

[ 名前によるクエリ ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByNameUsingGET) も使用できます。 名前によるクエリのエンドポイントには、必須パラメーターとして名前のみが指定されています。 Name：インスタンス内のフォルダーの名前フィールドに対して完全に一致する文字列を実行し、その名前に一致する各フォルダーの結果を返します。 また、「type」というオプションのクエリパラメーターも含まれています。これは、フォルダーまたはプログラム、「root」（検索するフォルダーの ID）、または「workspace」（検索するワークスペースの名前）にすることができます。 ルートパラメーターを設定する場合は、type パラメーターも設定する必要があります。

```
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

名前で検索する場合、マーケティングアクティビティと Design Studio はどちらも独自のルートフォルダーであることに注意してください。そのため、名前で検索することができ、宛先インスタンスの残りのフォルダー階層を移動するために使用できます。

### 参照

フォルダーは [ 一括で取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderUsingGET) することもできます。 「root」パラメーターは、クエリが実行される親フォルダーを指定するために使用でき、クエリパラメーターの値として埋め込まれる JSON オブジェクトとしてフォーマットされます。 ルートには次の 2 つのメンバーがあります。

1. id - フォルダーまたはプログラムの id。
1. タイプ – ブラウザーへのルートフォルダーのタイプに応じて、フォルダーまたはプログラム。

ルートフォルダーが不明な場合や、特定のエリア内のすべてのフォルダーを取得する場合は、ルートを「マーケティングアクティビティ」、「Design Studio」または「リードデータベース」エリアとして指定できます。 これらの各 ID は、[ 名前でフォルダーを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByNameUsingGET) API を使用して、目的の領域の名前を指定することで取得できます。

他の一括アセット取得エンドポイントと同様に、offset と maxReturn はページングのオプションのパラメーターです。   その他のオプションパラメーターは次のとおりです。

- workSpace - フィルタリング先のワークスペースの名前。
- maxDepth - フォルダー階層内をトラバースするレベルの最大数。 0 に設定した場合は、root で指定したフォルダーのみが返されます。 指定しない場合、デフォルト値は 2 です。

```
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

フォルダー応答構造の多くは自明ですが、いくつかのフィールドは個別に注目する価値があります。 `folderId` および親フィールドは、フォルダー自体の明示的な ID とタイプを含む JSON オブジェクトです。 このタイプは、API によってクエリ、ルート、親パラメーターで使用され、フォルダーのタイプとプログラムタイプのフォルダー間で適切に区別されるようにします。 `folderType` は、フォルダーの使用状況を反映します。これは「マーケティングフォルダー」、「プログラム」、「電子メール」、「電子メールテンプレート」、「ランディングページ」、「ランディングページテンプレート」、「スニペット」、「画像」、「ゾーン」、「ファイル」のいずれかです。  マーケティングフォルダーおよびプログラムのタイプは、これらがマーケティングアクティビティに存在し、複数のタイプのアセットを含むことができることを示します。 その他のタイプのフォルダーには、そのアセットタイプ、サブフォルダーおよびそのタイプのテンプレートバージョン（該当する場合）のみを含めることができます。 ゾーン タイプは、マーケティングアクティビティにあるルートレベルのフォルダーを表します。

フォルダーのパスは、Unix スタイルのパスと同様に、フォルダーツリーに階層を表示します。 パスの最初のエントリは、常にマーケティングアクティビティまたは Design Studio です。 ターゲットインスタンスにワークスペースがある場合、パスの 2 番目のエントリは、所有しているワークスペースの名前になります。 `url` フィールドには、指定したインスタンス内のアセットの明示的な URL が表示されます。 これはユニバーサルリンクではないので、正しく機能するにはユーザーとして認証される必要があります。 `isSystem` は、フォルダーがシステムフォルダーであるかどうかを示します。 これが true に設定されている場合、フォルダー自体は読み取り専用ですが、フォルダーはその子として作成できます。

## 作成と更新

[ フォルダーの作成 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/createFolderUsingPOST) は簡単で、フォルダーを作成するための 2 つの必須パラメーター（name、string、parent）を持つ application/x-www-form-urlencoded POSTで実行されます。このパラメーターは、フォルダーのタイプに応じて、id と type の 2 つのメンバーを持つ埋め込み JSON オブジェクトです。 オプションで、「説明」という文字列を含めることもできます（最大文字数は 2000 文字まで可能）。

```
POST /rest/asset/v1/folders.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

フォルダーの更新は別のエンドポイントで行われ、説明、名前、`isArchive` は更新用のオプションのパラメーターです。 更新によって `isArchive` が変更された場合、Marketo UI では、フォルダーが true に変更された場合はアーカイブされ、false に変更された場合はアーカイブ解除されます。 この API ではプログラムを更新できません。

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

### 削除

削除は、空の場合、つまりアセットやサブフォルダーが含まれていない場合は、単一のフォルダーに対して実行できます。 フォルダーのタイプがプログラムの場合、または isSystem フィールドが true に設定されている場合、この API では削除できません。

```
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
