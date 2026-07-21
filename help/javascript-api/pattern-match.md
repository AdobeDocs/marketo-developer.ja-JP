---
title: パターン一致
description: RTP rtp.checkPattern ユーティリティを使用して、パーセントのワイルドカードを使用して文字列パターンをテストします。同期の制限、使用とURLの例、必要なRTP タグ設定を参照してください。
feature: Javascript
exl-id: 4ebd13e3-375b-449b-850f-3b18f570ca75
TQID: https://experienceleague.adobe.com/-HopUg6-2EchL9kJrPDbz62mRlrqYaXYdufILjkvP1Y
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
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 188
ht-degree: 31%

---

# パターン一致

RTPは、パターンが文字列と一致するかどうかをチェックするユーティリティ関数を提供します。 ユーティリティは一致した結果を同期して返し、非同期で使用することはできません。

User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。

## 使用方法

> rtp.checkPattern(check_against, pattern);

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| check_against | 必須 | 文字列 | 現在のページ URLや製品名など、パターンと一致する文字列。 |
| パターン | 必須 | 文字列 | 一致させるパターン。 文字列の開始、終了、または内容に一致するワイルドカードとして`%`を追加します。 完全一致の場合は`%`を省略します。 |

## 例

次の使用例は、現在のページ URLが「productA」で終わる場合、インデックス 1にカスタム変数を設定します。

```javascript
if (rtp.checkPattern(window.location.href, '%productA')) {
    rtp('set', 'custom1', 'productA');
}
```

次の例では、現在のURL パスは「/products/productB」です。 次の使用例は、パスに「products」が含まれているかどうかを確認し、カスタム変数を設定します。

```javascript
var currentURLPath = '/products/productB';
if (rtp.checkPattern(currentURLPath, '%products%')) {
    rtp('set', 'custom1', 'products');
}
```
