---
title: PhoneGap
feature: Mobile Marketing
description: CordovaでMarketo PhoneGap プラグインを設定し、Firebase Cloud Messagingを設定し、iOSとAndroidのプッシュを有効にし、通知をトラッキングし、SDKを初期化します。
exl-id: 99f14c76-9438-4942-9309-643bca434d07
TQID: https://experienceleague.adobe.com/eFAwR7r5IE6vKigsEWrJdCmC3VrfB-nl0h8x7Vgt1VY
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: ea90ebee-5c84-42d9-8b21-006bdabc95a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 775
ht-degree: 27%

---

# PhoneGap

Marketo PhoneGap PluginをCordova アプリと統合します。

## 前提条件

1. [Marketo Admin](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)でアプリケーションを追加し、アプリケーションの秘密鍵とMunchkin IDを取得します。
1. [Android](push-notifications.md)または[iOS](push-notifications.md)のプッシュ通知を設定します。
1. [PhoneGap/Cordova CLI のインストール](https://cordova.apache.org/docs/en/latest/guide/cli/).

## インストール手順

1. Marketo PhoneGap Pluginを設定します。

   PhoneGap アプリケーションディレクトリに移動し、次のコマンドを実行してMarketo プラグインを追加します。

   `$ cordova plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

1. FCM プラグインをインストールします。

   `$ cordova plugin add cordova-plugin-fcm`

   次のコマンドを実行して、プラグインが追加されたことを確認します。

   `$ cordova plugin ls com.marketo.plugin 0.X.0 "MarketoPlugin" cordova-plugin-fcm 2.1.2 "FCMPlugin"`

**新しいバージョンに移行（オプション）**

既存のプラグインを削除するには、次のコマンドを実行します。

`$ cordova plugin remove com.marketo.plugin`

プラグインを再度追加するには、次のコマンドを実行します。

`$ cordova plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

**Cordova バージョン 8.0.0 （Cordova@Android7.0.0）以降**

Cordova Android プラットフォームを構築した後、Android Studioでアプリを開きます。 `com.marketo.plugin` フォルダーの`Marketo.gradle` ファイルの`dirs`値を更新します。

```groovy
repositories{
  jcenter()
  flatDir{
      dirs '../app/src/main/aar'
   }
}
```

アプリのターゲットプラットフォームを追加：`$cordova platform add android` `$ cordova platform add ios`

追加されたプラットフォームを確認してください：`$cordova platform ls`

1. Firebase Cloud Messaging サポート

1. Firebase ConsoleでFirebase アプリを設定します。
   1. [](https://console.firebase.google.com/)Firebase コンソールでプロジェクトを作成または追加します。
      1. が含まれる [Firebase コンソール](https://console.firebase.google.com/)を選択 **[!UICONTROL プロジェクトを追加]**.
      1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択して、を選択します。 **[!UICONTROL Firebase の追加]**.
      1. Firebase のスタートアップスクリーンで、「Android アプリに Firebase を追加」を選択します。
      1. パッケージ名と SHA-1 を指定し、を選択します。 **[!UICONTROL アプリを追加]**. 新品 `google-services.json` firebase アプリのファイルがダウンロードされます。
   1. [!UICONTROL  プロジェクト概要]の&#x200B;**[!UICONTROL プロジェクト設定]**&#x200B;に移動します。
      1. 「**[!UICONTROL 一般]**」タブを選択し、「google-services.json」ファイルをダウンロードします。
      1. 「**[!UICONTROL クラウドメッセージ]**」タブを選択します。 [!UICONTROL  サーバーキー]と[!UICONTROL 送信者ID]をコピーし、Marketoに提供します。
   1. PhoneGap アプリでFCMを設定します。
      1. ダウンロードした「google-services.json」ファイルをPhoneGap アプリモジュールのルートディレクトリに移動します。
      1. の場所からファイル「MyFirebaseInstanceIDService」を削除します `platforms/android/app/src/main/java/com/gae/scaffolder/plugin` （非推奨）
      1. の場所にあるファイル「MyFirebaseMessagingService」を `platforms/android/app/src/main/java/com/gae/scaffolder/plugin` 次のように設定します。

         ```
         import com.marketo.Marketo;
         
         public class MyFirebaseMessagingService extends FirebaseMessagingService{
         
         @Override
         public void onNewToken(String s){
           super.onNewToken(s);
           MarketoExtension.setPushNotificaitonTokens(s);
           //Add your code here
         }
         
         @Override
         public void onMessageReceived(RemoteMessage remoteMessage) {
           MarketoExtension.showPushNotificaiton(remoteMessage);
           //Add your code here
         }
         }
         ```

         1. plugins/cordova-plugin-fcm/scripts にあるファイル「fcm_config_files_process.js」を次のように変更します

            ```
            //change
            var strings = fs.readFileSync("platforms/android/res/values/strings.xml").toString();
            //to
            var strings = fs.readFileSync("platforms/android/app/src/main/res/values/strings.xml").toString();
            
            //AND change
            fs.writeFileSync("platforms/android/res/values/strings.xml", strings);
            //to
            fs.writeFileSync("platforms/android/app/src/main/res/values/strings.xml", strings);
            ```

### &#x200B;3. xCode でのプッシュ通知の有効化

xCode プロジェクトのプッシュ通知機能をオンにします。

### &#x200B;4. プッシュ通知のトラッキング

次のコードをに貼り付けます。 `application:didFinishLaunchingWithOptions:` 関数。

>[!BEGINTABS]

>[!TAB Objective C]

次のように`applicationDidBecomeActive` メソッドを更新します。

```objectivec
Marketo *sharedInstance = [Marketo sharedInstance];

[sharedInstance trackPushNotification:launchOptions];
```

>[!TAB Swift]

次のように`applicationDidBecomeActive` メソッドを更新します。

```swift
let sharedInstance: Marketo = Marketo.sharedInstance()

sharedInstance.trackPushNotification(launchOptions)
```

>[!ENDTABS]

### &#x200B;5. Marketo フレームワークの初期化

アプリの起動時にMarketo フレームワークを初期化するには、メインのJavaScript ファイルの`onDeviceReady`関数に次のコードを追加します。

`phonegap`をPhoneGap アプリのフレームワークタイプとして渡します。

### 構文

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

### パラメーター

- Success Callback: Marketo フレームワークが正常に初期化された場合に実行する関数。
- Failure Callback: Marketo フレームワークが初期化に失敗した場合に実行する関数。
- MUNCHKIN ID：登録時にMarketoから受信したMunchkin ID。
- 秘密鍵：登録時にMarketoから秘密鍵を受信しました。

### &#x200B;6. Marketo プッシュ通知の初期化

Marketo プッシュ通知を初期化するには、メインのJavaScript ファイルのinitialize関数の後に次のコードを追加します。

### 構文

```javascript
// This function will Enable user notifications (prompts the user to accept push notifications in iOS)
marketo.initializeMarketoPush(
    function() { console.log("Marketo push successfully initialized."); },
    function(error) { console.log("an error occurred:" + error); },
    'YOUR_GCM_PROJECT_ID' // This is required for Android and will be ignored in iOS
);
```

### パラメーター

- Success Callback: Marketo プッシュ通知が正常に初期化された場合に実行する関数。
- Failure Callback: Marketo プッシュ通知が初期化に失敗した場合に実行する関数。
- GCM_PROJECT_ID: アプリの作成後、[Google Developers Console](https://console.developers.google.com/)にGCM プロジェクト IDが見つかりました。

ログアウト時にトークンを登録解除することもできます。

```javascript
marketo. uninitializeMarketoPush(
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
lead[marketo.KEY_FIRST_NAME] = "Phone";
lead[marketo.KEY_LAST_NAME] = "Gap";
lead[marketo.KEY_EMAIL] = email;
lead[marketo.KEY_ADDRESS] = "demo address";
lead[marketo.KEY_CITY] = "city";
lead[marketo.KEY_STATE] = "state";
lead[marketo.KEY_COUNTRY] = "country";
lead[marketo.KEY_POSTAL_CODE] = "postalCode";
lead[marketo.KEY_GENDER] = "gender";
// To use lead custom field, use the REST API NAME as key
lead["REST API NAME"] = "value";

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
