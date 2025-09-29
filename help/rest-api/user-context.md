---
title: ユーザコンテキスト
feature: REST API
description: Marketo RTP User Context API を有効にして使用することで、カスタム変数を設定し、複数の訪問をまたいでユーザーデータを読み取り、閲覧済みおよびクリック済みキャンペーンを追跡できる方法を説明します。
exl-id: b8daace2-07a5-4621-aa3a-03fa9f66ea73
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 90%

---

# ユーザコンテキスト

User Context JavaScript API は、複数のセッションをまたいでユーザおよび訪問者レベルのデータを公開し、過去のユーザの行動とデータを使用して高度なパーソナライゼーション機能を有効にします。この API は、データの読み取りにとどまらず、高度なセグメント化とパーソナライゼーションの目的で、意味のあるデータとイベントを RTP バックエンドにプッシュできるカスタム変数を公開します。その他の機能：[トリガー](../javascript-api/triggers.md)、[パターン一致](../javascript-api/pattern-match.md)。

- User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。
- User Context API は、リクエストに応じて Marketo サポートが有効にする必要がある機能です。この API が有効な場合、RTP グローバルオブジェクトの下にある userContext オブジェクトが公開されます。

## ユーザコンテキスト属性

| 名前 | タイプ | 説明 |
|------------------|-------------|------|
| customVar[1-5] | 文字列 | ユーザコンテキストに保存されたカスタムデータ。 |
| viewedCampaigns | コンマ区切りの文字列としてのキャンペーン ID | 現在または以前の訪問で閲覧したキャンペーン。 |
| clickedCampaigns | コンマ区切りの文字列としてのキャンペーン ID | 現在または以前の訪問でクリックスルーされたキャンペーン。 |

## カスタム変数の設定

ユーザコンテキストにカスタムデータを追加します。

### 使用方法

`rtp('set', 'customVar'[1-5], my_custom_value);`

| パラメーター | オプション／必須 | タイプ | 説明 |
|-----------------|-------------------|--------|-----------------|
| ‘set’ | 必須 | 文字列 | メソッドアクション。 |
| customVar | 必須 | 文字列 | カスタム変数名。 |
| my_custom_value | 必須 | 文字列 | インデックス 1～5 のカスタム変数に保存するカスタム値。 |

メモ：カスタム変数は、ビュー呼び出しでのみ RTP に送信されるので、ビューが呼び出される前にカスタム変数を設定することをお勧めします。それ以外の場合は、次のビュー呼び出しでのみ送信されます。

カスタム Var の制限

- カスタム変数の長さは 100 文字を超えることはできません。
- キャンペーンデータは、1 回の訪問あたり 10 個のキャンペーンが含まれる過去 10 回の訪問に制限されます。

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
