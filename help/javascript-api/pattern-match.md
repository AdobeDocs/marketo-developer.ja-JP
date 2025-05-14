---
title: パターン一致
description: パターン一致
feature: Javascript
exl-id: 4ebd13e3-375b-449b-850f-3b18f570ca75
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '134'
ht-degree: 100%

---

# パターン一致

RTP は、パターンが特定の文字列と一致するかどうかを確認するユーティリティ関数を公開します。このユーティリティは、一致があるかどうかの指示を返すので、非同期では使用できません。

User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。

## 使用方法

> rtp.checkPattern(check_against, pattern);

| パラメーター | オプション／必須 | タイプ | 説明 |
|---|---|---|---|
| check_against | 必須 | 文字列 | パターンと一致させる文字列。例：現在のページの URL、製品名。 |
| パターン | 必須 | 文字列 | ワイルドカードには % を追加します。パターンは、start with／end with／contains／full match のようになります。 |


## 例

現在のページ URL が「productA」で終わる場合は、インデックス 1 にカスタム変数を設定します。

```javascript
if (rtp.checkPattern(window.location.href, '%productA')) {
    rtp('set', 'custom1', 'productA');
}
```

現在の URL パスは「/products/productB」です。この例では、パスに「products」が含まれているかどうかを確認し、カスタム変数を設定します。

```javascript
var currentURLPath = '/products/productB';
if (rtp.checkPattern(currentURLPath, '%products%')) {
    rtp('set', 'custom1', 'products');
}
```
