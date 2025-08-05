---
title: トリガー
description: トリガー
feature: Javascript
exl-id: 588836fa-1e4d-41f3-aec5-5cd17eb16071
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 100%

---

# トリガー

グローバル RTP オブジェクトの特定の状態で関数をトリガーする機能を追加します。

User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。

## 使用方法

`rtp('triggerName', function_to_trigger);`

| パラメーター | オプション／必須 | タイプ | 説明 |
|---------------------|-------------------|----------|----------------------|
| &#39;triggerName&#39; | 必須 | 文字列 | メソッド名。 |
| function_to_trigger | 必須 | 関数 | トリガーする関数。 |

### ユーザコンテキスト準備完了トリガー

ユーザの場所に基づいてカスタム変数を設定します。この関数は、&quot;rtpUserContext&quot; グローバルオブジェクトの準備が整った際に呼び出されます。

```javascript
rtp('userContextReady', function() {
    if (rtpUserContext.location.state == 'CA') {
        rtp('set', 'custom1', 'productA');
    }
});
```
