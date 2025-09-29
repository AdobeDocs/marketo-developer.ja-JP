---
title: パターン一致
description: RTP rtp.checkPattern ユーティリティを使用して、パーセント ワイルドカードを使用した文字列パターンのテスト、同期の制限事項、使用例、URL の例、および必要な RTP タグのセットアップを参照してください。
feature: Javascript
exl-id: 4ebd13e3-375b-449b-850f-3b18f570ca75
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 80%

---

# パターン一致

RTP は、パターンが特定の文字列と一致するかどうかを確認するユーティリティ関数を公開します。このユーティリティは、一致があるかどうかの指示を返すので、非同期では使用できません。

User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。

## 使用方法

> rtp.checkPattern(check_against, pattern);

| パラメーター | オプション／必須 | タイプ | 説明 |
|---|---|---|---|
| check_against | 必須 | 文字列 | パターンと一致させる文字列。例：現在のページの URL、製品名。 |
| パターン | 必須 | 文字列 | ワイルドカードには % を追加します。このパターンは :startcontainsfull のマッチで終わる |

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
