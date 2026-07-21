---
title: カスタムデータイベント
description: Web Personalization用のRTP JavaScript APIを使用して、パラメーター、最大4つのアイテムの文字列または配列データ、クリックベースのトリガーーを含むカスタムイベントを送信します。
feature: Javascript
exl-id: ef7cab9c-3bd0-450e-9247-9324b1e6f9ab
TQID: https://experienceleague.adobe.com/oWDmtMF94xG5HYXeTwkx5zF9PWo98bpwoVB6kAKLYDo
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: e2290edd-b061-4880-9d79-dee306cf5aa9id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 241
ht-degree: 36%

---

# カスタムデータイベント

この方法を使用して、トラッキングとリアルタイムのパーソナライゼーション用にカスタムイベントを送信します。 訪問者の行動にもとづいて、サードパーティデータやトリガーにカスタムイベントを送信できます。

各カスタムデータイベントは、訪問者のセッション中に1回カウントされます。

User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| `send` | 必須 | 文字列 | メソッドアクション。 |
| `event` | 必須 | 文字列 | メソッド名。 |
| `customData` | 必須 | 文字列または配列 | カスタムデータ。 |

## 例

### カスタムデータの文字列を使用してイベントを送信する

```javascript
var customData = {value: 'MyEvent'};
rtp('send', 'event', customData);
```

### カスタムデータの文字列の配列を使用してイベントを送信する

カスタムデータ配列には、最大4つの要素を含めることができます。 4つ以上の要素を送信するには、Send Event APIを繰り返し呼び出し、1回の呼び出しごとに4つ以下の項目を使用します。

```javascript
var customData = {value: ['MyEvent', 'download - example whitepaper']};
rtp('send', 'event', customData);
```

### ボタンのクリックに基づいてイベントを送信する

次の使用例は、訪問者がボタンを選択して特定のホワイトペーパーをダウンロードしたときに、カスタム データ イベントを送信します。 RTPは、イベントを使用して、これらの訪問者をリアルタイムでセグメント化できます。

web サイトでは、さらに2回クリックするだけでパーソナライズされたキャンペーンを表示できます。 例えば、ダウンロードしたホワイトペーパーに関連する別のコンテンツをキャンペーンに表示できます。

```html
<button id="download-whitepaper" onclick="rtp('send', 'event', {value :'download - example whitepaper'})">Download</button>
```
