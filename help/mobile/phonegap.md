---
title: PhoneGap
feature: Mobile Marketing
description: Cordova を使用したMarketo PhoneGap プラグインの設定、Firebase Cloud Messaging の設定、iOSとAndroidのプッシュの有効化、通知のトラッキング、SDKの初期化を行います。
exl-id: 99f14c76-9438-4942-9309-643bca434d07
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 97%

---

# PhoneGap

Marketo PhoneGap プラグインの統合

## 前提条件

1. [Marketo Admin でのアプリケーションの追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID を取得します）。
1. プッシュ通知を設定（[iOS](push-notifications.md) | [Android](push-notifications.md)）に設定します。
1. [PhoneGap/Cordova CLI のインストール](https://cordova.apache.org/docs/en/latest/guide/cli/).

## インストール手順

1. Marketo PhoneGap プラグインの設定

   Cordova CLI がインストールされている場合は、PhoneGap アプリケーションディレクトリに移動し、次のコマンドを実行してMarketo プラグインをアプリケーションに追加します。

   `$ cordova plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

1. FCM プラグインのインストール

   `$ cordova plugin add cordova-plugin-fcm`

   プラグインがアプリケーションに追加されたことを確認するには、次のコマンドを実行し、

   `$ cordova plugin ls com.marketo.plugin 0.X.0 "MarketoPlugin" cordova-plugin-fcm 2.1.2 "FCMPlugin"`

**新しいバージョンに移行（オプション）**

既存のプラグインを削除するには、次のコマンドを実行します。

`$ cordova plugin remove com.marketo.plugin`

プラグインを再追加するには、次のコマンドを実行します。

`$ cordova plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

**Cordova バージョン 8.0.0 （Cordova@Android7.0.0）以降**

Cordova Android プラットフォームをビルドしたら、Android Studio でアプリを開き、 `dirs` 値 `Marketo.gradle` でファイルが見つかりました `com.marketo.plugin` フォルダー。

```
repositories{
  jcenter()
  flatDir{
      dirs '../app/src/main/aar'
   }
}
```

アプリのターゲットにするプラットフォームの追加 `$cordova platform add android` `$ cordova platform add ios`

追加されたプラットフォームのリストを確認します `$cordova platform ls`

1. Firebase Cloud Messaging サポート

1. Firebase コンソールで Firebase アプリを設定します。
   1. でのプロジェクトの作成/追加 [&#128279;](https://console.firebase.google.com/)Firebase コンソール。
      1. が含まれる [Firebase コンソール](https://console.firebase.google.com/)を選択 **[!UICONTROL プロジェクトを追加]**.
      1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択して、を選択します。 **[!UICONTROL Firebase の追加]**.
      1. Firebase のスタートアップスクリーンで、「Android アプリに Firebase を追加」を選択します。
      1. パッケージ名と SHA-1 を指定し、を選択します。 **[!UICONTROL アプリを追加]**. 新品 `google-services.json` firebase アプリのファイルがダウンロードされます。
   1. [!UICONTROL プロジェクトの概要]の&#x200B;**[!UICONTROL プロジェクト設定]**&#x200B;に移動します
      1. 「**[!UICONTROL 一般]**」タブをクリックします。「google-services.json」ファイルをダウンロードします。
      1. 「**[!UICONTROL Cloud Messaging]**」タブをクリックします。[!UICONTROL サーバーキー]と[!UICONTROL 送信者 ID] をコピーします。 これらの[!UICONTROL サーバーキー]と[!UICONTROL 送信者 ID] を Marketo に指定します。
   1. Phonegap アプリでの FCM 変更の設定
      1. ダウンロードした「google-services.json」ファイルを Phonegap アプリモジュールのルートディレクトリに移動します
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

### &#x200B;3. xCode でプッシュ通知を有効にする

xCode プロジェクトでプッシュ通知機能をオンにします。

### &#x200B;4. プッシュ通知のトラッキング

次のコードをに貼り付けます。 `application:didFinishLaunchingWithOptions:` 関数。

>[!BEGINTABS]

>[!TAB Objective C]

を更新 `applicationDidBecomeActive` 次のようなメソッド

```
Marketo *sharedInstance = [Marketo sharedInstance];

[sharedInstance trackPushNotification:launchOptions];
```

>[!TAB Swift]

を更新 `applicationDidBecomeActive` 次のようなメソッド

```
let sharedInstance: Marketo = Marketo.sharedInstance()

sharedInstance.trackPushNotification(launchOptions)
```

>[!ENDTABS]

### &#x200B;5. Marketo フレームワークの初期化

Marketo フレームワークがアプリの起動時に確実に開始されるようにするには、以下のコードをアプリの `onDeviceReady` メイン JavaScript ファイルで機能します。

我々は合格しなければならないことに注意してください `phonegap` PhoneGap アプリのフレームワークタイプとして。

### 構文

```
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

- Success Callback :Marketo フレームワークが正常に初期化された場合に実行する関数。
- Failure Callback :Marketo フレームワークを初期化できない場合に実行する関数
- MUNCHKIN ID：登録時にMarketoから受信した Munchkin ID。
- 秘密鍵：登録時にMarketoから受信した秘密鍵。

### &#x200B;6. Marketo プッシュ通知の初期化

Marketoのプッシュ通知が開始されるようにするには、メインの JavaScript ファイルの initialize 関数の後に次のコードを追加します。

### 構文

```
// This function will Enable user notifications (prompts the user to accept push notifications in iOS)
marketo.initializeMarketoPush(
    function() { console.log("Marketo push successfully initialized."); },
    function(error) { console.log("an error occurred:" + error); },
    'YOUR_GCM_PROJECT_ID' // This is required for Android and will be ignored in iOS
);
```

### パラメーター

- Success Callback :Marketo プッシュ通知が正常に初期化された場合に実行する関数。
- Failure Callback :Marketoのプッシュ通知が初期化に失敗した場合に実行する関数
- GCM_PROJECT_ID :GCM プロジェクト ID が見つかりました [Google開発者コンソール](https://console.developers.google.com/) アプリの作成後。

トークンは、ログアウト時に登録解除することもできます。

```
marketo. uninitializeMarketoPush(
  function() { console.log("Marketo push successfully uninitialized."); } ,
  function(error) { console.log("an error occurred:" + error); }
);
```

## リードを関連付け

associateLead 関数を呼び出すことで、Marketo リードを作成できます。

### 構文

```
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

```
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

ユーザーがアクションを実行した場合は、 `reportaction` 関数。

### 構文

```
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

```
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

次に示すように、「一時停止」および「再開」イベントタイプをバインドして、開始イベントと停止イベントをレポートします。  これは、モバイルアプリケーションで費やした時間を追跡するために使用されます。 メモ：これは Android で必要です。

```
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
