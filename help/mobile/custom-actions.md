---
title: カスタムアクション
feature: Mobile Marketing
description: Marketo Mobile SDK iOSおよびAndroid版を使用してカスタムアクションを送信およびレポートし、オフラインでキューを作成し、スマートキャンペーンをトリガーし、20文字のユーザーに対応する方法を説明します。
exl-id: 8c2698ce-4e39-4b2b-9d36-0864c55be17a
TQID: https://experienceleague.adobe.com/yZKzdm-dH0cYPGGKE-Z-4KcbhGIwyFl0Z9vEqcv1QXI
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: a7170d27-32ab-462b-a333-269abc654483
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: c1579802-ddd4-4214-8a91-97b2066abe11id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 259
ht-degree: 25%

---

# カスタムアクション

カスタムアクション モバイルアプリでのユーザーのインタラクションを追跡します。 アプリがMarketo SDKを呼び出してカスタムアクションを送信すると、SDKはまずアクションをデバイスに保存します。 SDKが適切なインターネット接続を検出した後にアクションを送信するので、Marketoは遅延の後にアクションを受け取る可能性があります。

カスタムアクションは、スマートキャンペーンのトリガーおよびフィルターとして使用できます。 詳しくは、[モバイルアプリのアクティビティ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/triggers-and-filters-for-mobile-smart-campaigns)を参照してください。

## iOS でのカスタムアクションの送信

カスタムアクションを送信します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
Marketo *sharedInstance = [Marketo sharedInstance];
[sharedInstance reportAction:@"Login" withMetaData:nil];
```

>[!TAB Swift]

```swift
sharedInstance.reportAction("Login", withMetaData:nil);
```

>[!ENDTABS]

メタデータを使用してカスタムアクションを送信します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
MarketoActionMetaData *meta = [[MarketoActionMetaData alloc] init];
[meta setType:@"Shopping"];
[meta setDetails:@"RedShirt"];
[meta setLength:20];
[meta setMetric:30];

[sharedInstance reportAction:@"Bought Shirt" withMetaData:meta];
```

>[!TAB Swift]

```swift
let meta = MarketoActionMetaData()
meta.setType("Shopping");
meta.setDetails("RedShirt");
meta.setLength(20);
meta.setMetric(30);

sharedInstance.reportAction("Bought Shirt", withMetaData:meta);
```

>[!ENDTABS]

保存されたすべてのアクションをすぐに報告します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
[sharedInstance reportAll];
```

>[!TAB Swift]

```swift
sharedInstance.reportAll();
```

>[!ENDTABS]

## Android でのカスタムアクションの送信

1. カスタムアクションを送信します。

   ```
   Marketo.reportAction("Login", null);
   ```

1. メタデータを使用してカスタムアクションを送信します。

   ```
   MarketoActionMetaData meta = new MarketoActionMetaData();
   meta.setActionType("Shopping");
   meta.setActionDetails("RedShirt");
   meta.setActionLength("20");
   meta.setActionMetric("30");
   
   Marketo.reportAction("Bought Shirt", meta);
   ```

1. 保存されたすべてのカスタムアクションをすぐにレポートします。

   ```
   Marketo.reportAll();
   ```

## カスタムアクションのトラブルシューティング

Mobile SDKからMarketoに送信されるカスタムアクション名は、20文字未満である必要があります。

**共有デバイスでのマルチユーザーユースケース：** ユーザーがMarketo SDKを使用するモバイルアプリにログインすると、最初の呼び出しによってリードがアプリのインストールに関連付けられます。 呼び出しが成功すると、その後のユーザーアクティビティがリードのアクティビティログに表示されます。

アソシエーション呼び出しは非同期です。 ログイン直後に記録されたカスタムアクションは、呼び出しが成功するまで、以前にログインしたユーザーに関連付けられる可能性があります。
