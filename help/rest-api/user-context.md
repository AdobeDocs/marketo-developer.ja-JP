---
title: ユーザコンテキスト
feature: REST API
description: Marketo RTP User Context APIを有効にして使用する方法を説明します。カスタム変数の設定、訪問時のユーザーデータの読み取り、表示およびクリックされたキャンペーンのトラッキングを行います。
exl-id: b8daace2-07a5-4621-aa3a-03fa9f66ea73
TQID: https://experienceleague.adobe.com/Ph0Tw-C9jzWaR4bYyUIXyzzoa2yjHQk2gt6tNA8H2mA
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
subfeature_v2:
  - id: a1d50dda-6d94-4e16-8c30-5eb7181c4650
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 273
ht-degree: 34%

---

# ユーザコンテキスト

ユーザーコンテキスト JavaScript APIは、複数のセッションにわたってユーザーレベルおよび訪問者レベルのデータを公開します。 過去の行動やデータを利用して、高度なパーソナライゼーションを実現。

このAPIは、セグメント化とパーソナライゼーションのために、データとイベントをRTP バックエンドに送信するためのカスタム変数も提供します。 関連する[トリガー](../javascript-api/triggers.md)および[&#x200B; パターンマッチ &#x200B;](../javascript-api/pattern-match.md)機能を参照してください。

- Web Personalizationのお客様で、サイトに[RTP タグがデプロイされている](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)必要があります。
- Marketo サポートにユーザーコンテキスト APIを有効にするように依頼する必要があります。 イネーブルメントの後、userContext オブジェクトがRTP グローバルオブジェクトの下に表示されます。

## ユーザコンテキスト属性

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| `customVar[1-5]` | 文字列 | ユーザコンテキストに保存されたカスタムデータ。 |
| `viewedCampaigns` | コンマ区切り文字列としてのキャンペーン ID | 現在または以前の訪問で閲覧したキャンペーン。 |
| `clickedCampaigns` | コンマ区切り文字列としてのキャンペーン ID | 現在または以前の訪問でクリックスルーされたキャンペーン。 |

## カスタム変数の設定

ユーザーのコンテキストにデータを追加するカスタム変数を設定します。

### 使用方法

`rtp('set', 'customVar'[1-5], my_custom_value);`

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| `'set'` | 必須 | 文字列 | メソッドアクション。 |
| `customVar` | 必須 | 文字列 | カスタム変数名。 |
| `my_custom_value` | 必須 | 文字列 | インデックス 1～5 のカスタム変数に保存するカスタム値。 |

カスタム変数は、ビュー呼び出しでのみRTPに送信されます。 ビュー呼び出しの前にカスタム変数を設定します。 それ以外の場合、変数は次のビュー呼び出しで送信されます。

カスタム変数には、次の制限があります。

- カスタム変数は100文字以内にする必要があります。
- キャンペーンデータは、1 回の訪問あたり 10 個のキャンペーンが含まれる過去 10 回の訪問に制限されます。

### 使用方法

`rtp('set', 'customVar', 'A');`

```javascript
// Set and get customVars
rtp('set', 'customVar1', 'foo');

// Read location
if (rtp.userContext.location.state == 'CA')  {
    // Do something
}

// Check if user viewed campaign id 45:
// The campaign id is exposed in the RTP UI when hovering over a campaign name.
if (rtp.userContext.viewedCampaign('45')) {
    // Do something
}
```
