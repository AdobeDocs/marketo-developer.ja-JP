---
title: '[!DNL Ionic]'
feature: Mobile Marketing
description: モバイルデバイス向けMarketoの使用  [!DNL Ionic]  使用
exl-id: 204e5fb4-c9d6-43a6-9d77-0b2a67ddbed3
source-git-commit: 6fc45ff98998217923e2a5b02d00d1522fe3272c
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 73%

---

# イオン

ここでは、Marketo Cordova プラグインの統合方法を説明します。 [!DNL Ionic] コンデンサは現在サポートされていません。

## 前提条件

1. [Marketo Admin でのアプリケーションの追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID を取得します）。
1. プッシュ通知の設定（[iOS](push-notifications.md) | [Android](push-notifications.md)）。
1. [[!DNL Ionic]](https://ionicframework.com/getting-started/) および [Cordova CLI](https://cordova.apache.org/docs/en/latest/guide/cli/) をインストールします。

## インストール手順

### Marketo [!DNL Ionic] プラグインの設定

1. Cordova CLI がインストールされている場合は、[!DNL Ionic] アプリケーションディレクトリに移動し、次のコマンドを実行してMarketo プラグインをアプリケーションに追加します。

   `$ ionic plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

1. プラグインがアプリケーションに追加されたことを確認するには、次のコマンドを実行します。

   `$ ionic plugin list com.marketo.plugin 0.X.0 "MarketoPlugin"`

### 新しいバージョンに移行（オプション）

1. 既存のプラグインを削除するには、次のコマンドを実行します。

   `$ ionic plugin remove com.marketo.plugin`

1. プラグインを読み込むには、次のコマンドを実行します。

   `$ ionic plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

### xCode でのプッシュ通知の有効化

1. xCode プロジェクトでプッシュ通知機能をオンにします。![ 通知機能 ](assets/notification-capability.png)

### プッシュ通知のトラッキング

次のコードをに貼り付けます。 `application:didFinishLaunchingWithOptions:` 関数。

>[!BEGINTABS]

>[!TAB 目標 C]

```
Marketo *sharedInstance = [Marketo sharedInstance];

[sharedInstance trackPushNotification:launchOptions];
```

>[!TAB Swift]

```
let sharedInstance: Marketo = Marketo.sharedInstance()

sharedInstance.trackPushNotfication(launchOptions)
```

>[!ENDTABS]

### Marketo フレームワークの初期化

Marketo フレームワークがアプリの起動時に確実に開始されるようにするには、以下のコードをアプリの `onDeviceReady` メイン JavaScript ファイルで機能します。

[!DNL Ionic] Cordova アプリのフレームワークタイプとして `ionicCordova` を渡す必要があります。

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

- Success Callback :Marketo フレームワークが正常に初期化された場合に実行する関数。
- Failure Callback :Marketo フレームワークを初期化できない場合に実行する関数
- MUNCHKIN ID：登録時にMarketoから受信した Munchkin ID。
- 秘密鍵：登録時にMarketoから受信した秘密鍵。

### Marketo プッシュ通知の初期化

Marketoのプッシュ通知が確実に開始されるようにするには、メインのJavaScript ファイル内の初期化された関数の後に次のコードを追加します。

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

- Success Callback :Marketo プッシュ通知が正常に初期化された場合に実行する関数。
- Failure Callback :Marketoのプッシュ通知が初期化に失敗した場合に実行する関数
- GCM_PROJECT_ID :GCM プロジェクト ID が見つかりました [Google開発者コンソール](https://accounts.google.com/ServiceLogin?service=cloudconsole&amp;passive=1209600&amp;osid=1&amp;continue=https://console.cloud.google.com/apis/dashboard&amp;followup=https://console.cloud.google.com/apis/dashboard) アプリの作成後。

トークンは、ログアウト時に登録解除することもできます。

```javascript
marketo.uninitializeMarketoPush(
  function() { console.log("Marketo push successfully uninitialized."); } ,
  function(error) { console.log("an error occurred:" + error); }
);
```

## リードの関連付け

associateLead 関数を呼び出すことで、Marketo リードを作成できます。

### 構文

```javascript
marketo.associateLead(
  function(){ console.log("MarketoSDK : Lead Added"); },
  function(error){ console.log("an error occurred:" + error); },
  'Lead_Data_JSON_String'
);
```

### パラメーター

- Success Callback :Marketo Framework がリードを正常に関連付けたときに実行する関数。
- Failure Callback :Marketo フレームワークがリードを関連付けられなかった場合に実行する関数
- リードデータ :JSON 文字列形式のリードデータ。

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

ユーザーがアクションを実行した場合は、 `reportaction` 関数。

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

- Success Callback :Marketo フレームワークがアクションを正常にレポートした場合に実行する関数。
- Failure Callback :Marketo フレームワークがアクションのレポートに失敗した場合に実行する関数。
- アクション名：アクション名。
- アクションデータ :JSON 文字列形式のアクションデータ。

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

次に示すように、「一時停止」および「再開」イベントタイプをバインドして、開始イベントと停止イベントをレポートします。 これは、モバイルアプリケーションで費やした時間を追跡するために使用されます。 メモ：これは Android で必要です。

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

新しく作成されたリードは、使用する方法に応じて、異なるトリガーとフィルターで認識されます。 MME SDK または REST API を使用して作成されたリードは、「リードが作成されました」のトリガーおよびフィルターに表示されます。 フォーム送信によって作成されたリードは、「フォームに記入」トリガーとフィルターに表示されます。

ベストプラクティスは、リードを作成する際に Web アプリで使用される方法との一貫性を維持することです。 リードを作成するメカニズムとしてフォーム送信を使用する web アプリが既にある場合は、ハイブリッドアプリでリードを作成する際に同じメカニズムを使用します。 リードを作成するメカニズムとして REST API を使用する web アプリが既にある場合は、ハイブリッドアプリでリードを作成する際に同じメカニズムを使用します。 Web アプリでリードを作成するメカニズムとしてフォーム送信も REST API も使用していない場合は、MME SDK を使用してMarketoでリードを作成することを検討できます。
