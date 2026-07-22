---
title: '[!DNL Ionic]'
feature: Mobile Marketing
description: Marketo Cordova PluginとIonicを統合するステップバイステップガイド、プッシュ通知を有効にする、SDKを初期化する、セッションをトラッキングする、リードを関連付ける。
exl-id: 204e5fb4-c9d6-43a6-9d77-0b2a67ddbed3
TQID: https://experienceleague.adobe.com/UTNWd69NliR896RcO-XM2GG35liuLeNNhTXo9GRtB4o
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: ea90ebee-5c84-42d9-8b21-006bdabc95a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 581
ht-degree: 22%

---

# Ionic

Marketo Cordova プラグインを[!DNL Ionic] アプリと統合します。[!DNL Ionic] Capacitorは現在サポートされていません。

## 前提条件

1. [Marketo Admin](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)でアプリケーションを追加し、アプリケーションの秘密鍵とMunchkin IDを取得します。
1. [Android](push-notifications.md)または[iOS](push-notifications.md)のプッシュ通知を設定します。
1. [[!DNL Ionic]](https://ionicframework.com/getting-started/)と[Cordova CLI](https://cordova.apache.org/docs/en/latest/guide/cli/)をインストールします。

## インストール手順

### Marketo [!DNL Ionic] プラグインの設定

1. [!DNL Ionic] アプリケーションディレクトリに移動し、次のコマンドを実行してMarketo プラグインを追加します。

   `$ ionic plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

1. 次のコマンドを実行して、プラグインが追加されたことを確認します。

   `$ ionic plugin list com.marketo.plugin 0.X.0 "MarketoPlugin"`

### 新しいバージョンへの移行（オプション）

1. 既存のプラグインを削除するには、次のコマンドを実行します。

   `$ ionic plugin remove com.marketo.plugin`

1. プラグインを再度追加するには、次のコマンドを実行します。

   `$ ionic plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

### xCode でのプッシュ通知の有効化

1. xCode プロジェクトのプッシュ通知機能をオンにします。![通知機能](assets/notification-capability.png)

### プッシュ通知のトラッキング

次のコードをに貼り付けます。 `application:didFinishLaunchingWithOptions:` 関数。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
Marketo *sharedInstance = [Marketo sharedInstance];

[sharedInstance trackPushNotification:launchOptions];
```

>[!TAB Swift]

```swift
let sharedInstance: Marketo = Marketo.sharedInstance()

sharedInstance.trackPushNotfication(launchOptions)
```

>[!ENDTABS]

### Marketo フレームワークの初期化

アプリの起動時にMarketo フレームワークを初期化するには、メインのJavaScript ファイルの`onDeviceReady`関数に次のコードを追加します。

`ionicCordova`を[!DNL Ionic]個のCordova アプリのフレームワークタイプとして渡します。

#### 構文

```javascript
// This method will Initialize the Marketo Framework using Your MunchkinId and Secret Key
marketo.initialize(
  function() { console.log("MarketoSDK Init done."); },
  function(error) { console.log("an error occurred:" + error); },
  'YOUR_MUNCHKIN_ID',
  'YOUR_SECRET_KEY',
  'FRAMEWORK_TYPE'
);

// For session tracking, add following.
marketo.onStart(
  function(){ console.log("onStart."); },
  function(error){ console.log("Failed to report onStart." + error); }
);
```

#### パラメーター

- Success Callback: Marketo フレームワークが正常に初期化された場合に実行する関数。
- Failure Callback: Marketo フレームワークが初期化に失敗した場合に実行する関数。
- MUNCHKIN ID：登録時にMarketoから受信したMunchkin ID。
- 秘密鍵：登録時にMarketoから秘密鍵を受信しました。

### Marketo プッシュ通知の初期化

Marketo プッシュ通知を初期化するには、メインのJavaScript ファイルのinitialize関数の後に次のコードを追加します。

#### 構文

```javascript
// This function will Enable user notifications (prompts the user to accept push notifications in iOS)
marketo.initializeMarketoPush(
    function() { console.log("Marketo push successfully initialized."); },
    function(error) { console.log("an error occurred:" + error); },
    'YOUR_GCM_PROJECT_ID' // This is required for Android and will be ignored in iOS
);
```

#### パラメーター

- Success Callback: Marketo プッシュ通知が正常に初期化された場合に実行する関数。
- Failure Callback: Marketo プッシュ通知が初期化に失敗した場合に実行する関数。
- GCM_PROJECT_ID: アプリの作成後、[Google Developers Console](https://accounts.google.com/ServiceLogin?service=cloudconsole&passive=1209600&osid=1&continue=https://console.cloud.google.com/apis/dashboard&followup=https://console.cloud.google.com/apis/dashboard)にGCM プロジェクト IDが見つかりました。

ログアウト時にトークンを登録解除することもできます。

```javascript
marketo.uninitializeMarketoPush(
  function() { console.log("Marketo push successfully uninitialized."); } ,
  function(error) { console.log("an error occurred:" + error); }
);
```

## リードの関連付け

associateLead関数を呼び出して、Marketo リードを作成します。

### 構文

```javascript
marketo.associateLead(
  function(){ console.log("MarketoSDK : Lead Added"); },
  function(error){ console.log("an error occurred:" + error); },
  'Lead_Data_JSON_String'
);
```

### パラメーター

- Success Callback: Marketo フレームワークがリードを正常に関連付ける場合に実行する関数。
- 失敗コールバック：Marketo フレームワークがリードの関連付けに失敗した場合に実行する関数。
- リードデータ：JSON文字列形式のリードデータ。

### 例

```javascript
// First create a lead as shown below
var lead = {};
lead[marketo.KEY_FIRST_NAME] = "Ionic";
lead[marketo.KEY_LAST_NAME] = "App";
lead[marketo.KEY_EMAIL] = email;
lead[marketo.KEY_ADDRESS] = "demo address";
lead[marketo.KEY_CITY] = "city";
lead[marketo.KEY_STATE] = "state";
lead[marketo.KEY_COUNTRY] = "country";
lead[marketo.KEY_POSTAL_CODE] = "postalCode";
lead[marketo.KEY_GENDER] = "gender";

// Use associateLead function to associate it.
marketo.associateLead(
  function() { console.log("MarketoSDK : Lead Associated"); },
  function(error) { console.log("an error occurred:" + error); },
  JSON.stringify(lead)
);
```

## 報告書アクション

`reportaction`関数を呼び出して、ユーザーアクションを報告します。

### 構文

```javascript
marketo.reportaction(
  function(){ console.log("MarketoSDK : New event sent "); },
  function(error){ console.log("an error occurred:" + error); },
  'Action_Name',
  'Action_Data_JSON_String'
);
```

### パラメーター

- Success Callback: Marketo フレームワークがアクションを正常に報告した場合に実行する関数。
- Failure Callback: Marketo フレームワークがアクションのレポートに失敗した場合に実行する関数。
- アクション名：アクション名。
- アクションデータ：JSON文字列形式のアクションデータ。

### 例

```javascript
// First create an event as below
var event = {
    "Action Type":"Add To Cart",
    "Action Details":"Adding Product in cart",
    "Action Metric":"10",
    "Action Length":"1"
}

marketo.reportaction(
    function(){ console.log("Reported action successfully."); },
    function(error){ console.log("Failed to report action." + error); },
    "Add To Cart",
    JSON.stringify(event)
);
```

## セッションレポート

「一時停止」および「再開」イベントタイプをバインドして、開始イベントと停止イベントを報告します。 これらのイベントは、モバイルアプリケーションで費やした時間を追跡し、Androidで必要です。

```javascript
//Add the following code in your www/js/index.js

bindEvents: function() {
   document.addEventListener('pause', this.onStop, false);
   document.addEventListener('resume', this.onStart, false);
},
onStop: function() {
   marketo.onStop(
       function(){ console.log("onStop"); },
       function(error){ console.log("Failed to report onStop." + error); }
   );
},
onStart: function() {
   marketo.onStart(
       function(){ console.log("onStart."); },
       function(error){console.log( "Failed to report onStart." + error); }
   );
},
```

## リードの作成

ハイブリッドアプリからリードを作成する方法は 3 つあります。

1. MARKETO MME SDK
1. MARKETO REST API
1. フォーム送信

新しいリードを識別するトリガーとフィルターは、作成方法によって異なります。

- MME SDKまたはREST APIで作成されたリードは、「作成されたリード」トリガーおよびフィルターに表示されます。
- フォーム送信によって作成されたリードは、「フォームに入力」トリガーとフィルターに表示されます。

ハイブリッドアプリとweb アプリでも、同様のリード作成方法を使用できます。 Web アプリでフォーム送信またはREST APIを使用する場合は、ハイブリッドアプリでそのメソッドを使用します。 Web アプリでどちらのメソッドも使用しない場合は、MME SDKを使用してMarketoでリードを作成することを検討してください。
