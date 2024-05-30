---
title: "トリガー"
description: "トリガー"
feature: Javascript
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 11%

---


# トリガー

グローバル rtp オブジェクトの特定のステートに対してトリガー関数を追加します。

Web パーソナライゼーションの顧客であり、次を持っている必要があります [RTP タグが展開されました](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) User Context API を使用する前に、サイトで次の操作を行います。

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
