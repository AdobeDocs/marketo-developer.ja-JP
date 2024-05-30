---
title: "ユーザーコンテキスト"
feature: REST API
description: 「ユーザーコンテキストの概要と API の説明」
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 5%

---


# ユーザーコンテキスト

User Context JavaScript API は、複数のセッションをまたいでユーザーおよび訪問者レベルのデータを公開し、過去のユーザー行動とデータを使用して高度なパーソナライゼーション機能を有効にします。 この API は、データの読み取りを超え、高度なセグメント化とパーソナライゼーションの目的で意味のあるデータとイベントを RTP バックエンドにプッシュできるカスタム変数を公開します。 追加機能： [トリガー](../javascript-api/triggers.md), [パターン一致](../javascript-api/pattern-match.md).

- Web パーソナライゼーションの顧客になり、次を持っている必要があります [RTP タグが展開されました](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) User Context API を使用する前に、サイトで次の操作を行います。
- User Context API は、Marketo サポートがリクエストに応じて有効にする必要がある機能です。 この API が有効な場合、RTP グローバルオブジェクトの下の userContext オブジェクトが公開されます。

## ユーザーコンテキスト属性

| 名前 | タイプ | 説明 |
|------------------|-------------|------|
| customVar[1-5] | 文字列 | ユーザーコンテキストに保存されたカスタムデータ。 |
| viewedCampaigns | キャンペーン ID をコンマ区切り文字列で表したもの | 現在または以前の訪問でキャンペーンを表示。 |
| clickedCampaign | キャンペーン ID をコンマ区切り文字列で表したもの | 現在または以前の訪問でキャンペーンをクリック済み。 |

## カスタム変数の設定

ユーザーコンテキストへのカスタムデータの追加

### 使用方法

`rtp('set', 'customVar'[1-5], my_custom_value);`

| パラメーター | オプション/必須 | タイプ | 説明 |
|-----------------|-------------------|--------|-----------------|
| &#39;設定&#39; | 必須 | 文字列 | メソッドのアクション。 |
| customVar | 必須 | 文字列 | カスタム変数名。 |
| my_custom_value | 必須 | 文字列 | インデックス 1 ～ 5 のカスタム変数に保存するカスタム値。 |

メモ：カスタム変数はビュー呼び出し時にのみ RTP に送信されるので、ビューが呼び出される前にカスタム変数を設定することをお勧めします。 それ以外の場合は、次のビュー呼び出しでのみ送信されます。

カスタム変数の制限

- カスタム変数の長さは 100 文字以下にする必要があります。
- キャンペーンデータは最後の 10 回の訪問に制限され、1 訪問あたり 10 回のキャンペーンが含まれます。

### 使用方法

`rtp('set', 'customVar', 'A');`

```javascript
// Set and get customVars
rtp('set', 'customVar1', 'foo');
 
// Read location 
if (rtp.userContext.location.state == 'CA')  {
    // Do something
}
 
// Check if user viewed campaign id 45:
// The campaign id is exposed in the RTP UI when hovering over a campaign name.
if (rtp.userContext.viewedCampaign('45')) {
    // Do something
}
```
