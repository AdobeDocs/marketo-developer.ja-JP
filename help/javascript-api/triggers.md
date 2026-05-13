---
title: トリガー
description: Web PersonalizationでRTP トリガーを使用して、構文、パラメーター、場所の例を含むuserContextReadyなどのrtp ステートで関数を実行します。
feature: Javascript
exl-id: 588836fa-1e4d-41f3-aec5-5cd17eb16071
TQID: https://experienceleague.adobe.com/yTz9i4bnD4I0PDAmpnjdD1okYJzd40wriA-2ZzO5OMM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 116
ht-degree: 81%

---

# トリガー

グローバル RTP オブジェクトの特定の状態で関数をトリガーする機能を追加します。

User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。

## 使用方法

`rtp('triggerName', function_to_trigger);`

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| &#39;triggerName&#39; | 必須 | 文字列 | メソッド名。 |
| function_to_trigger | 必須 | 関数 | トリガーする関数。 |

### ユーザコンテキスト準備完了トリガー

ユーザの場所に基づいてカスタム変数を設定します。 この関数は、&quot;rtpUserContext&quot; グローバルオブジェクトの準備が整った際に呼び出されます。

```javascript
rtp('userContextReady', function() {
    if (rtpUserContext.location.state == 'CA') {
        rtp('set', 'custom1', 'productA');
    }
});
```
