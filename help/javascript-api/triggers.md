---
title: トリガー
description: Web PersonalizationでRTP トリガーを使用して、構文、パラメーター、場所の例を含むuserContextReadyなどのrtp ステートで関数を実行します。
feature: Javascript
exl-id: 588836fa-1e4d-41f3-aec5-5cd17eb16071
TQID: https://experienceleague.adobe.com/yTz9i4bnD4I0PDAmpnjdD1okYJzd40wriA-2ZzO5OMM
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: e2290edd-b061-4880-9d79-dee306cf5aa9id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 117
ht-degree: 52%

---

# トリガー

グローバル `rtp` オブジェクトが指定されたステートに達すると、トリガーが関数を実行します。

User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。

## 使用方法

`rtp('triggerName', function_to_trigger);`

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| &#39;triggerName&#39; | 必須 | 文字列 | メソッド名。 |
| function_to_trigger | 必須 | 関数 | トリガーする関数。 |

### ユーザコンテキスト準備完了トリガー

グローバル `rtpUserContext` オブジェクトの準備ができたら、`userContextReady` トリガーが関数を呼び出します。 次の例では、ユーザーの場所に基づいてカスタム変数を設定します。

```javascript
rtp('userContextReady', function() {
    if (rtpUserContext.location.state == 'CA') {
        rtp('set', 'custom1', 'productA');
    }
});
```
