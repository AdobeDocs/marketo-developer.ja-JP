---
title: 動的コンテンツ
feature: REST API, Dynamic Content
description: セグメント化を使用してメール、ランディングページ、エンドポイントと例を含むスニペットをパーソナライズし、REST API を介してセクションレベルのMarketo動的コンテンツを設定します
exl-id: 8ab97624-5fb5-4a41-911f-ec8616dd43c9
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 95%

---

# 動的コンテンツ

Marketo は、複数のアセットタイプでのリードのセグメント化を通じて動的コンテンツの使用を容易にします。

- メール
- ランディングページ
- スニペット

## 概要

動的コンテンツはセクションレベルで実装され、セグメント内で選択されたセグメント内のリードの資格に応じて、セクションの特定のバリエーションをリードに配信するように指定されます。コンテンツが特定のセグメント化に基づいて動的コンテンツを配信するように設定されている場合、そのコンテンツを表示するリードには、該当するセグメントに属するコンテンツのバリエーションが配信されます。セグメントに該当しないリードには、デフォルトコンテンツが配信されます。

## 例

これを説明するために、地域（米国）のセグメントがあり、カリフォルニア州、ネバダ州、ユタ州、コロラド州、アリゾナ州、ニューメキシコ州のリードを含む南西部セグメントに該当するリードに対してのみイベントプロモーションを表示するメールの例を見てみましょう。これを実行するには、ID「Q1-promotion-banner」を持つメール内の編集可能なセクションを DynamicContent セクションに作成します。そのため、メールの[メールコンテンツセクションを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailComponentContentUsingPOST)エンドポイントを使用する必要があります。`value` パラメーターは、セグメントの ID を指定するために使用されます。

メモ：メールとランディングページの両方が、このパターンに従います。スニペットには異なるパターンがあります。詳しくは、Snippets API のドキュメントを参照してください。

次の例では、セクションを動的コンテンツセクションに設定し、セグメント 1001 でセグメント化しています。

```
POST /rest/asset/v1/email/{id}/content/Q1-promotion-banner.json
```

```
type=DynamicContent&value=1001
```

```json
{
  "success": true,
  "errors": [],
  "requestId": "891b#1729b34b9a5",
  "warnings": [],
  "result": [
    {
      "id": 1909
    }
  ]
}
```

個々のセグメントにコンテンツを追加するには、特定のセクションの[メール動的コンテンツセクションを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailDynamicContentUsingPOST)エンドポイントを呼び出す必要があります。

次の例では、デフォルトではなく、南西部セグメントのリードに対して特別なバナー画像を表示するようにセクションを設定します。より多くのセグメントに対してより多くのバリエーションを作成する場合は、各セグメントとセクションに対してこのエンドポイントを再度呼び出します。

```
POST /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json
```

```
segment=Southwest&type=HTML&value=<img src='//www.example.com/SuperSpecialBannerForAmericanSouthwestLeads.jpg'/>
```

```json
{
  "success": true,
  "errors": [],
  "requestId": "891b#1729b34b9a5",
  "warnings": [],
  "result": [
    {
      "id": 1637
    }
  ]
}
```

## セグメント化

セグメント化は、Marketo 動的コンテンツの核心です。セグメント化は、リードデータベース全体に対して上から下まで評価される個別のルールセットのユーザ定義リストです。リードは、各セグメント化で 1 つのセグメントにのみ所属でき、各セグメントで最初に選定されるメンバーです。セグメントに該当しない場合は、デフォルトセグメントのメンバーとなり、そのセグメントを使用する動的コンテンツの特定の部分に対してデフォルトコンテンツを受け取ります。

### リスト

セグメント化には、使用可能なセグメント化のリストを含む応答を返すリストエンドポイントがあります。

```
GET /rest/asset/v1/segmentation.json
```

```json
{
  "success": true,
  "warnings": [ ],
  "errors": [ ],
  "requestId": "78eb#14e9de95868",
  "result": [
    {
      "id": 1001,
      "name": "My Industry Segmentation",
      "description": "",
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:10Z+0000",
      "url": "https://app-abm.marketo.com/#SG1001A1",
      "folder": {
        "type": "Program",
        "value": 396,
        "folderName": null
      },
      "status": "approved",
      "workspace": "Default"
    },
    {
      "id": 1002,
      "name": "My Country Segmentation",
      "description": "",
      "createdAt": "2015-04-06T18:28:23Z+0000",
      "updatedAt": "2015-04-06T18:37:18Z+0000",
      "url": "https://app-abm.marketo.com/#SG1002A1",
      "folder": {
        "type": "Program",
        "value": 396,
        "folderName": null
      },
      "status": "approved",
      "workspace": "Default"
    }
  ]
}
```

また、セグメント化には、親セグメントからのセグメントのリストを含む応答を返すエンドポイントもあります。

```
GET /rest/asset/v1/segmentation/1001/segments.json
```

```json
{
  "success": true,
  "warnings": [ ],
  "errors": [ ],
  "requestId": "2031#14e9df08796",
  "result": [
    {
      "id": 1001,
      "name": "Manufacturing",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "status": "approved",
      "segmentationId": 1001
    },
    {
      "id": 1002,
      "name": "Healthcare",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "url": "https://app-abm.marketo.com/#SL769688A1",
      "status": "approved",
      "segmentationId": 1001
    },
    {
      "id": 1003,
      "name": "Financial",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "url": "https://app-abm.marketo.com/#SL769690A1",
      "status": "approved",
      "segmentationId": 1001
    },
    {
      "id": 1004,
      "name": "Technology",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "url": "https://app-abm.marketo.com/#SL769692A1",
      "status": "approved",
      "segmentationId": 1001
    },
    {
      "id": 1005,
      "name": "Default",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "url": "https://app-abm.marketo.com/#SL769694A1",
      "status": "approved",
      "segmentationId": 1001
    }
  ]
}
```
