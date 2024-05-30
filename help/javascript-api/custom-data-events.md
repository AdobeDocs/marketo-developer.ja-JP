---
title: 「カスタムデータイベント」
description: 「Custom Data Events API」
feature: Javascript
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 4%

---


# カスタムデータイベント

このメソッドは、トラッキングとリアルタイムパーソナライゼーション用のカスタムイベントを送信します。 これを使用して、サードパーティデータを送信したり、訪問者行動に基づいて独自のカスタムイベントをトリガーしたりできます。 カスタムデータイベントは、訪問者のセッション内で 1 回カウントされます。

Web パーソナライゼーションの顧客になり、次を持っている必要があります [RTP タグが展開されました](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) User Context API を使用する前に、サイトで次の操作を行います。

| パラメーター | オプション/必須 | タイプ | 説明 |
|---|---|---|---|
| `send` | 必須 | 文字列 | メソッドのアクション。 |
| `event` | 必須 | 文字列 | メソッド名。 |
| `customData` | 必須 | 文字列または配列 | カスタムデータ。 |

## 例

### カスタムデータに文字列を使用してイベントを送信

```javascript
var customData = {value: 'MyEvent'};
rtp('send', 'event', customData);
```

### カスタムデータの文字列の配列を使用してイベントを送信

カスタムデータ配列には、最大 4 つの要素を含めることができます。  4 つ以上の要素を送信する必要がある場合は、すべての項目が送信されるまで Send Event API を繰り返し（最大 4 つの項目）呼び出します。

```javascript
var customData = {value: ['MyEvent', 'download - example whitepaper']};
rtp('send', 'event', customData);
```

### ボタンのクリックに基づいてイベントを送信

Marketoは、特定のホワイトペーパーをダウンロードした web 訪問者に対して、web サイト上のコンテンツをパーソナライズします。 これを行うには、訪問者がホワイトペーパーのダウンロードボタンをクリックする様子をキャプチャし、カスタムデータイベントを送信します。 RTP は、「ホワイトペーパーのダウンロード」ボタンをクリックしたすべての訪問者をリアルタイムでセグメント化し、各訪問者にパーソナライズされたキャンペーンを表示することで、後で 2 回のクリックを提供します。 これは、ダウンロードされたホワイトペーパーに関連する別のコンテンツを表示することで実現されます。

```html
<button id="download-whitepaper" onclick="rtp('send', 'event', {value :'download - example whitepaper'})">Download</button>
```
