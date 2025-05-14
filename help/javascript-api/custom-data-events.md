---
title: カスタムデータイベント
description: 一意のイベントのトラッキングには、Custom Data Events Javascript API を使用します。
feature: Javascript
exl-id: ef7cab9c-3bd0-450e-9247-9324b1e6f9ab
source-git-commit: e609f9d5d58f656298412acef5e2106a19765396
workflow-type: ht
source-wordcount: '231'
ht-degree: 100%

---

# カスタムデータイベント

このメソッドは、トラッキングとリアルタイムのパーソナライゼーション用のカスタムイベントを送信します。これを使用すると、サードパーティのデータを送信したり、訪問者の行動に基づいて独自のカスタムイベントをトリガーしたりできます。カスタムデータイベントは、1 人の訪問者のセッションで 1 回カウントされます。

User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。

| パラメーター | オプション／必須 | タイプ | 説明 |
|---|---|---|---|
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

カスタムデータ配列には、最大 4 つの要素を含めることができます。4 つ以上の要素を送信する必要がある場合は、すべての項目が送信されるまで Send Event API を繰り返し呼び出します（最大 4 項目）。

```javascript
var customData = {value: ['MyEvent', 'download - example whitepaper']};
rtp('send', 'event', customData);
```

### ボタンのクリックに基づいてイベントを送信する

Marketo では、特定のホワイトペーパーをダウンロードした web 訪問者に対して、web サイトのコンテンツをパーソナライズします。これを行うには、訪問者によるホワイトペーパーのダウンロードボタンのクリックをキャプチャして、カスタムデータイベントを送信します。RTP では、ホワイトペーパーのダウンロードボタンをクリックしたすべての訪問者をリアルタイムでセグメント化し、各訪問者に対して、2 回クリックした後で、パーソナライズされたキャンペーンオファーを表示します。これは、ダウンロードしたホワイトペーパーに関連する別のコンテンツを表示することによって実現されます。

```html
<button id="download-whitepaper" onclick="rtp('send', 'event', {value :'download - example whitepaper'})">Download</button>
```
