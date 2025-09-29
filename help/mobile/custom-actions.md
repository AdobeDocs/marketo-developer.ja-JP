---
title: カスタムアクション
feature: Mobile Marketing
description: iOSおよびAndroid用のMarketo Mobile SDKを使用してカスタムアクションを送信およびレポートする方法、オフラインでキューに入れる方法、スマートキャンペーンをトリガーで配信する方法、20 文字を満たす方法について説明します。
exl-id: 8c2698ce-4e39-4b2b-9d36-0864c55be17a
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 92%

---

# カスタムアクション

カスタムアクションを送信することで、ユーザインタラクションを追跡できます。モバイルアプリが Marketo SDK を呼び出してカスタムアクションを送信すると、カスタムアクションは最初にデバイスに保存されます。次に、Marketo SDK では、カスタムアクションを送信する前に、適切なインターネット接続があるかどうかを確認します。その結果、カスタムアクションが送信されてから Marketo で受信されるまでの間に遅延が生じる場合があります。

カスタムアクションは、スマートキャンペーンのトリガーおよびフィルターとして使用できます。詳しくは、[モバイルアプリのアクティビティ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/triggers-and-filters-for-mobile-smart-campaigns)を参照してください。

## iOS でのカスタムアクションの送信

カスタムアクションを送信します。

>[!BEGINTABS]

>[!TAB Objective C]

```
Marketo *sharedInstance = [Marketo sharedInstance];
[sharedInstance reportAction:@"Login" withMetaData:nil];
```

>[!TAB Swift]

```
sharedInstance.reportAction("Login", withMetaData:nil);
```

>[!ENDTABS]

メタデータを含むカスタムアクションを送信します。

>[!BEGINTABS]

>[!TAB Objective C]

```
MarketoActionMetaData *meta = [[MarketoActionMetaData alloc] init];
[meta setType:@"Shopping"];
[meta setDetails:@"RedShirt"];
[meta setLength:20];
[meta setMetric:30];

[sharedInstance reportAction:@"Bought Shirt" withMetaData:meta];
```

>[!TAB Swift]

```
let meta = MarketoActionMetaData()
meta.setType("Shopping");
meta.setDetails("RedShirt");
meta.setLength(20);
meta.setMetric(30);

sharedInstance.reportAction("Bought Shirt", withMetaData:meta);
```

>[!ENDTABS]

すべてのアクションをすぐに報告します（保存されているすべてのアクションを送信します）。

>[!BEGINTABS]

>[!TAB 目標 C]

```
[sharedInstance reportAll];
```

>[!TAB Swift]

```
sharedInstance.reportAll();
```

>[!ENDTABS]

## Android でのカスタムアクションの送信

1. カスタムアクションを送信します。

   ```
   Marketo.reportAction("Login", null);
   ```

1. メタデータを含むカスタムアクションを送信します。

   ```
   MarketoActionMetaData meta = new MarketoActionMetaData();
   meta.setActionType("Shopping");
   meta.setActionDetails("RedShirt");
   meta.setActionLength("20");
   meta.setActionMetric("30");
   
   Marketo.reportAction("Bought Shirt", meta);
   ```

1. すべてのカスタムアクションをすぐに報告します（保存されているすべてのアクションを送信します）。

   ```
   Marketo.reportAll();
   ```

## カスタムアクションのトラブルシューティング

モバイルカスタムアクションの設定は簡単ですが、Mobile SDK から Marketo に送信できる文字数には制限があります。Mobile SDK を通じて Marketo に報告するカスタムアクションはすべて 20 文字未満であることを確認します。

**共有デバイスでの複数ユーザのユースケースに関するメモ：**&#x200B;ユーザが Marketo SDK と統合されたモバイルアプリにログインすると、リードとアプリのインストールを関連付ける最初の呼び出しが行われます。この呼び出しが正常に完了すると、アプリ内の後続のユーザアクティビティがリードのアクティビティログに表示されます。これは非同期呼び出しなので、ログイン直後にカスタムアクションが記録された場合、関連付け呼び出しが成功するまで、以前にログインしていたユーザに関連付けられる場合があります。
