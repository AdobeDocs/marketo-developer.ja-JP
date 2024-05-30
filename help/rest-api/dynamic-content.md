---
title: 「動的コンテンツ」
feature: REST API, Dynamic Content
description: 「Marketo API を使用した動的コンテンツの設定」
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 2%

---


# 動的コンテンツ

Marketoは、複数のアセットタイプでのリードのセグメント化を通じて、動的コンテンツの使用を容易にします。

- メール
- ランディングページ
- スニペット

## 概要

動的コンテンツは、選択されたセグメント化内のセグメントにおける選定に基づいて、リードに提供されるセクションの特定のバリエーションを指定することにより、セクションレベルで実装される。 コンテンツの一部が特定のセグメント化に基づいて動的コンテンツを提供するように設定されている場合、そのコンテンツが、該当するセグメントに一致するコンテンツバリエーションを提供するようしたリード、またはセグメントに適合しない場合はデフォルトコンテンツを提供します。

## 例

これを示すために、地域（米国）のセグメント化があるメールの例で、南西セグメントに分類されるリード（カリフォルニア、ネバダ、ユタ、コロラド、アリゾナ、ニューメキシコのリードを含む）にのみイベントプロモーションを表示する場合を見てみましょう。 これを行うには、ID が「Q1-promotion-banner」の編集可能なセクションを DynamicContent セクションに作成します。 これを行うには、 [「メールコンテンツの更新」セクション](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailComponentContentUsingPOST) メールのエンドポイント。 この `value` パラメーターは、セグメント化の ID を指定するために使用されます。

注意：メールとランディングページはどちらも、このパターンに従います。 スニペットには異なるパターンがあります。詳しくは、スニペット API のドキュメントを参照してください。

次の例では、セクションを、セグメント化 1001 でセグメント化された動的コンテンツセクションに設定します。

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

個々のセグメントのコンテンツを追加するには、を呼び出す必要があります [「メール動的コンテンツの更新」セクション](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailDynamicContentUsingPOST) 特定のセクションのエンドポイント。

次の例では、セクションを設定して、デフォルトの代わりに南西セグメントのリードに対して特別なバナー画像を表示させます。 より多くのセグメントに対してさらにバリエーションを作成する場合は、セグメントおよびセクションごとに、このエンドポイントを再度呼び出します。

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

セグメント化は、Marketo動的コンテンツの中核です。 セグメント化は、リードデータベース全体に対して上から下に評価される個々のルールセットのユーザー定義リストです。 リードは、各セグメントで 1 つのセグメントのメンバーでしかなく、各セグメントで最初に選定されたセグメントのメンバーになることはできません。 セグメントに適合しない場合、セグメントはデフォルトセグメントのメンバーになり、そのセグメント化を使用する特定の動的コンテンツのデフォルトコンテンツを受け取ります。

### リスト

セグメントには、使用可能なセグメントのリストを含む応答を返すリストエンドポイントがあります。

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

セグメント化には、親セグメント化からのセグメントのリストを含んだ応答を返すエンドポイントもあります。

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
