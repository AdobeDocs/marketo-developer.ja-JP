---
title: カスタムアクション
feature: Mobile Marketing
description: カスタムアクションの概要
exl-id: 8c2698ce-4e39-4b2b-9d36-0864c55be17a
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 4%

---

# カスタムアクション

カスタムアクションを送信することで、ユーザーインタラクションを追跡できます。 モバイルアプリがMarketo SDK を呼び出してカスタムアクションを送信すると、カスタムアクションは最初にデバイスに保存されます。 次に、Marketo SDK は、カスタムアクションを送信する前に、適切なインターネット接続があるかどうかを確認します。 その結果、カスタムアクションが送信されてからMarketoが受信されるまでの間に遅延が生じる可能性があります。

カスタムアクションは、スマートキャンペーンのトリガーおよびフィルターとして使用できます。 詳しくは、[ モバイルアプリのアクティビティ ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/triggers-and-filters-for-mobile-smart-campaigns) を参照してください。

## iOSでのカスタムアクションの送信

カスタムアクションを送信します。

>[!BEGINTABS]

>[!TAB 目標 C]

```
Marketo *sharedInstance = [Marketo sharedInstance];
[sharedInstance reportAction:@"Login" withMetaData:nil];
```

>[!TAB Swift]

```
sharedInstance.reportAction("Login", withMetaData:nil);
```

>[!ENDTABS]

カスタムアクションとメタデータの送信

>[!BEGINTABS]

>[!TAB 目標 C]

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

すべてのアクションを直ちにレポート （保存されているすべてのアクションを送信）。

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

## Androidでのカスタムアクションの送信

1. カスタムアクションを送信します。

   ```
   Marketo.reportAction("Login", null);
   ```

1. カスタムアクションとメタデータの送信

   ```
   MarketoActionMetaData meta = new MarketoActionMetaData();
   meta.setActionType("Shopping");
   meta.setActionDetails("RedShirt");
   meta.setActionLength("20");
   meta.setActionMetric("30");
   
   Marketo.reportAction("Bought Shirt", meta);
   ```

1. すべてのカスタムアクションを直ちに報告（保存されたすべてのアクションを送信）。

   ```
   Marketo.reportAll();
   ```

## カスタムアクションのトラブルシューティング

モバイルカスタムアクションの設定は簡単ですが、Mobile SDK からMarketoに送信できる文字数には制限があります。 Mobile SDK を通じてMarketoにレポートするすべてのカスタムアクションの長さが、20 文字未満であることを確認します。

**共有デバイスでのマルチユーザーの使用例に関する注意：** ユーザーが、Marketo SDK と統合されたモバイルアプリにログインすると、最初の呼び出しでリードとアプリのインストールが関連付けられます。 この呼び出しが正常に完了すると、アプリ内の後続のユーザーアクティビティがリードのアクティビティログに表示されます。 ログイン直後にカスタムアクションがログに記録された場合、これは非同期呼び出しであるため、関連付け呼び出しが成功するまで、以前にログインしたユーザーに関連付けられる可能性があります。
