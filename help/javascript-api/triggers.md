---
title: トリガー
description: トリガー
feature: Javascript
exl-id: 588836fa-1e4d-41f3-aec5-5cd17eb16071
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 13%

---

# トリガー

グローバル rtp オブジェクトの特定のステートに対してトリガー関数を追加します。

User Context API を使用する前に、Web Personalizationのユーザーであり、サイトに [RTP タグがデプロイされている ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) 必要があります。

## 使用方法

`rtp('triggerName', function_to_trigger);`

| パラメーター | オプション/必須 | タイプ | 説明 |
|---------------------|-------------------|----------|----------------------|
| &#39;triggerName&#39; | 必須 | 文字列 | メソッド名。 |
| function_to_トリガー | 必須 | 機能 | トリガーする関数。 |


### User Context Ready トリガー

ユーザーの場所に基づいてカスタム変数を設定します。 この関数は、「rtpUserContext」グローバルオブジェクトの準備が整ったときに呼び出されます。

```javascript
rtp('userContextReady', function() {
    if (rtpUserContext.location.state == 'CA') {
        rtp('set', 'custom1', 'productA');
    }
});
```
