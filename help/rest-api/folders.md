---
title: フォルダー
feature: REST API
description: Marketo API を使用したフォルダーの操作。
exl-id: 4b55c256-ef0a-42b4-9548-ff8a4106f064
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '1008'
ht-degree: 100%

---

# フォルダー

[フォルダーエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders)

フォルダーは、Marketo のコア組織のアセットです。他のすべてのタイプのアセットには親として 1 つ以上のフォルダーがあります。この親フォルダーは、純粋に組織的なフォルダーや、他のアセットタイプと機能的な関係があり、他のアセットの親になることもできるプログラムのいずれかになる場合があります。フォルダーは、API を通じて作成、クエリ、更新、削除を実行でき、またフォルダーのコンテンツのリストを取得することもできます。プログラムは、Folders API に対するクエリを通じて返すことができますが、プログラムの作成、更新、削除は、Programs API を通じて実行する必要があります。

## クエリ

フォルダーのクエリは、[ID 別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByIdUsingGET)、[名前別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByNameUsingGET)および[参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderUsingGET)のアセットに対する標準のクエリタイプに従います。

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

type パラメーターは必須で、&quot;Folder&quot; 　または &quot;Program&quot; のいずれかにする必要があります。タイプによって、フォルダーへの参照がフォルダー ID に対して実行されるか、プログラム ID に対して実行されるかが指定されます。このエンドポイントの場合、結果の配列には 1 つのレコードのみが返されます。応答には、folderType パラメーターがあります。このパラメーターは、様々なタイプのフォルダーを示すことができます。Marketo アクティビティフォルダーには、マーケティングフォルダーまたはプログラムのいずれかのタイプがあり、様々なタイプのアセットを含めることができます。一方、デザインスタジオフォルダーには、保持できるアセットタイプに対応するタイプがあります。例えば、folderType が &quot;Email&quot; のフォルダーには、メールのみが含まれる場合もあれば、folderType がメールまたはメールテンプレートである可能性があるその他のサブフォルダーが含まれる場合もあります。タイプには、以下を含めることができます。

- メール
- メールテンプレート
- ランディングページ
- ランディングページテンプレート
- スニペット
- ファイル

### 名前別

[名前別クエリ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByNameUsingGET)も許可されます。名前別クエリエンドポイントでは、name が唯一の必須パラメーターです。name は、インスタンス内のフォルダーの名前フィールドに対して正確な文字列一致を実行し、その名前に一致する各フォルダーの結果を返します。また、オプションのクエリパラメーターとして、「フォルダー」または「プログラム」にすることができる「type」、検索するフォルダーの ID である「root」、または検索するワークスペースの名前である「workspace」があります。root パラメーターが設定されている場合は、type パラメーターも設定する必要があります。

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

名前別で検索する場合、マーケティングアクティビティとデザインスタジオはどちらも独自のルートフォルダーなので、名前別で取得して、宛先インスタンスの残りのフォルダー階層をトラバースするために使用できます。

### 参照

フォルダーは、[一括で取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderUsingGET)することもできます。「root」パラメーターは、クエリが実行される親フォルダーを指定するために使用でき、クエリパラメーターの値として埋め込まれた JSON オブジェクトとして書式設定されます。ルートには次の 2 つのメンバーがあります。

1. id - フォルダーまたはプログラムの ID。
1. type - ブラウザーのルートフォルダーのタイプに応じて、フォルダーまたはプログラムのいずれか。

ルートフォルダーが不明な場合や、特定の領域内のすべてのフォルダーを取得することが目的である場合は、ルートを「マーケティングアクティビティ」、「デザインスタジオ」、または「リードデータベース」領域として指定できます。それぞれの ID は、[Get Folder By Name](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByNameUsingGET) API を使用して、目的の領域の名前を指定して取得できます。

他のアセットの一括取得エンドポイントと同様に、 offset と maxReturn はページングのオプションパラメーターです。他のオプションのパラメーターは次のとおりです。

- workSpace - フィルタリング先のワークスペースの名前。
- maxDepth - フォルダー階層内をトラバースするレベルの最大数。0 に設定すると、ルートで指定したフォルダーのみが返されます。指定しない場合、デフォルト値は 2 です。

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

フォルダー応答構造の多くは自明ですが、いくつかのフィールドは個別に注目する価値があります。`folderId` フィールドと parent フィールドは、フォルダー自体の明示的な ID とタイプを含む JSON オブジェクトです。このタイプは、フォルダーのフォルダータイプとプログラムタイプ間の適切な区別を確保するために、API によってクエリ、ルート、親パラメーターで使用されるタイプです。`folderType` は、フォルダーの使用状況を反映し、「マーケティングフォルダー」、「プログラム」、「メール」、「メールテンプレート」、「ランディングページ」、「ランディングページテンプレート」、「スニペット」、「画像」、「ゾーン」、「ファイル」のいずれかに指定できます。マーケティングフォルダーとプログラムのタイプは、マーケティングアクティビティ内に存在し、複数のタイプのアセットを含めることができることを示します。他のタイプは、該当する場合はそのタイプのアセット、サブフォルダーおよびこのタイプのテンプレートバージョンのみを含めることができることを示します。「ゾーン」タイプは、マーケティングアクティビティにあるルートレベルのフォルダーを表します。

フォルダーのパスは、Unix スタイルのパスと同様に、フォルダーツリー内の階層を表示します。パスの最初のエントリは、常にマーケティングアクティビティまたはデザインスタジオになります。ターゲットインスタンスにワークスペースがある場合、パスの 2 番目のエントリは所有ワークスペースの名前になります。`url` フィールドには、指定したインスタンス内のアセットの明示的な URL が表示されます。これはユニバーサルリンクではないので、正しく機能するにはユーザとして認証される必要があります。`isSystem` は、フォルダーがシステムフォルダーであるかどうかを示します。これを true に設定すると、フォルダー自体は読み取り専用になりますが、その子としてフォルダーを作成できます。

## 作成と更新

[フォルダーの作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/createFolderUsingPOST)は簡単で、application/x-www-form-urlencoded POST で実行されます。この POST には、文字列の「name」とフォルダーを作成する親の「parent」という 2 つの必須パラメーターがあります。parent idは、id と type の 2 つのメンバーを持つ埋め込み JSON オブジェクトです。type は、対象フォルダのタイプに応じて Folder または Program のいずれかになります。オプションで、「description」という文字列も含めることができ、最大 2000 文字まで指定できます。

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

フォルダーの更新は別のエンドポイントを通じて行われ、description、name および `isArchive` は更新用のオプションパラメーターです。`isArchive` が更新によって変更された場合、Marketo UI でフォルダーがアーカイブされる（true に変更された場合）か、アーカイブ解除される（false に変更された場合）ことになります。この API ではプログラムを更新できません。

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

フォルダーが空の場合、つまりアセットやサブフォルダーが含まれていない場合、単一のフォルダーに対して削除を行うことができます。フォルダーのタイプがプログラムの場合や、isSystem フィールドが true に設定されている場合、この API ではフォルダーを削除できません。

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
