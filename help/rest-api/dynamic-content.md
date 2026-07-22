---
title: 動的コンテンツ
feature: REST API, Dynamic Content
description: セグメンテーションを使用して、REST APIを介してセクションレベルのMarketo動的コンテンツを設定し、エンドポイントや例を使用してメール、ランディングページ、スニペットをパーソナライズします
exl-id: 8ab97624-5fb5-4a41-911f-ec8616dd43c9
TQID: https://experienceleague.adobe.com/MwfPxu74qk0bPZMr6yuxQi--e3gMvP1tXQZ5iMil02o
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 329
ht-degree: 8%

---

# 動的コンテンツ

リードセグメンテーションを利用して、次のようなアセットタイプのコンテンツを動的に提供できます。

- メール
- ランディングページ
- スニペット

## 概要

動的コンテンツはセクションレベルで動作します。 各セクションには、選択したセグメント内のセグメントのバリエーションを表示できます。

リードがアセットを閲覧すると、Marketoにはリードのセグメントのバリエーションが表示されます。 リードがセグメントに適格でない場合、Marketoにはデフォルトのコンテンツが表示されます。

## 例

この例では、地域（米国）セグメントを使用して、南西セグメントのリードにイベントプロモーションを表示します。 このセグメントには、カリフォルニア州、ネバダ州、ユタ州、コロラド州、アリゾナ州、ニューメキシコ州のリードが含まれます。

[電子メールコンテンツセクションを更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailComponentContentUsingPOST) エンドポイントを使用して、ID `Q1-promotion-banner`の編集可能セクションを`DynamicContent` セクションに変更します。 `value` パラメーターは、セグメント IDを指定します。

電子メールやランディングページは、このパターンに従っています。 スニペットでは、スニペット API ドキュメントに記載されている様々なパターンを使用します。

次の例では、セクションを動的コンテンツセクションに設定し、セグメント 1001 でセグメント化しています。

```http
POST /rest/asset/v1/email/{id}/content/Q1-promotion-banner.json
```

```text
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

[&#x200B; メール動的コンテンツの更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailDynamicContentUsingPOST) エンドポイントを呼び出して、特定のセクションのセグメントにコンテンツを追加します。

次のリクエストでは、南西セグメントのリードのデフォルトコンテンツではなく、特別なバナーが表示されます。 さらにバリエーションを作成するには、各セグメントとセクションのエンドポイントを呼び出します。

```http
POST /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json
```

```text
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

セグメンテーションとは、Marketoがリードデータベースに対して上下を評価する、ユーザー定義のルールセットのリストです。 リードは、各セグメント内の1つのセグメントにのみ属することができます。 リードは、最初に選定されたセグメントに属します。

リードが別のセグメントに適格でない場合は、デフォルトセグメントに結合され、セグメントのデフォルトコンテンツを受け取ります。

### リスト

リストエンドポイントを使用して、使用可能なセグメントを取得します。

```http
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

セグメント エンドポイントを使用して、親セグメント内のセグメントを取得します。

```http
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
