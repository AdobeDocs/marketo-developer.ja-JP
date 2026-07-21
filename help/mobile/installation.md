---
title: インストール
feature: Mobile Marketing
description: CocoaPods、Swift Package Manager、またはGradleを使用して、iOSとAndroidにMarketo Mobile SDKをインストールし、初期化し、プッシュおよびアプリ内メッセージを有効にする方法を説明します。
exl-id: e0b79d85-3509-46d2-a77d-cee211c5ec7f
TQID: https://experienceleague.adobe.com/zYNoGPwJTQnqmP6CH0NDbmb-b8vAKRScMmms6vy0Sb4
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45id: e2290edd-b061-4880-9d79-dee306cf5aa9id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 772
ht-degree: 49%

---

# インストール

Marketo Mobile SDKをインストールして初期化し、プッシュ通知、アプリ内メッセージ、またはその両方を送信します。

## iOS への Marketo SDK のインストール

### 前提条件

1. [Marketo Admin](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)でアプリケーションを追加し、アプリケーションの秘密鍵とMunchkin IDを取得します。
1. オプション：[ プッシュ通知を設定](push-notifications.md)。

### CocoaPods 経由のフレームワークのインストール

1. CocoaPods をインストールします。`$ sudo gem install cocoapods`
1. ディレクトリをプロジェクトディレクトリに変更し、スマートデフォルトを使用して Podfile を作成します。`$ pod init`
1. Podfile を開きます。`$ open -a Xcode Podfile`
1. Podfile に次の行を追加します。`$ pod 'Marketo-iOS-SDK'`
1. Podfile を保存して閉じます。
1. Marketo iOS SDK をダウンロードしてインストールします。`$ pod install`
1. Xcodeでワークスペースを開きます。`$ open App.xcworkspace`

### Swift パッケージマネージャーを使用したフレームワークのインストール

1. プロジェクトナビゲーターでプロジェクトを選択します。 「パッケージ依存関係を追加」で、「+」を選択します。

   ![依存関係の追加](assets/dependency-manager-add.png)

1. <https://github.com/Marketo/ios-sdk>からMarketo パッケージを追加します。

   ![リポジトリ URL](assets/dependency-manager-url.png)

1. リソースバンドルを追加します。 プロジェクトナビゲーターで`MarketoFramework.XCframework`を見つけ、Finderで開きます。 `MKTResources.bundle`をドラッグしてバンドルリソースをコピーします。

### Swift ブリッジングヘッダーの設定

1. ファイル/新規/ファイルに移動し、「ヘッダーファイル」を選択します。

   ![「ヘッダーファイル」の選択](assets/choose-header-file.png)

1. ファイルに「&lt;_ProjectName_>-Bridging-Header」という名前を付けます。

1. プロジェクト／ターゲット／ビルドフェーズ／Swift コンパイラー／コード生成に移動します。 Objective-Bridging ヘッダーに次のパスを追加します。

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

   ![ビルドフェーズ](assets/build-phases.png)

## SDK の初期化

Munchkin アカウント IDとアプリ秘密鍵を使用して、Marketo iOS SDKを初期化します。 Marketo Adminの「Mobile Apps and Devices」で両方の値を検索します。

1. Objective-Cの場合はAppDelegate.m ファイル、Swiftの場合はBridging ファイルを開きます。 Marketo.h ヘッダーファイルを読み込みます。

   ```
   #import <MarketoFramework/MarketoFramework.h>
   ```

1. 次のコードを `application:didFinishLaunchingWithOptions`: 関数内にペーストします。

   ネイティブアプリのフレームワークタイプとして「ネイティブ」を渡します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
Marketo *sharedInstance = [Marketo sharedInstance];

[sharedInstance initializeWithMunchkinID:@"munchkinAccountId" appSecret:@"secretKey" mobileFrameworkType:@"native" launchOptions:launchOptions];
```

>[!TAB Swift]

```swift
let sharedInstance: Marketo = Marketo.sharedInstance()

sharedInstance.initialize(withMunchkinID: "munchkinAccountId", appSecret: "secretKey", mobileFrameworkType: "native", launchOptions: launchOptions)
```

>[!ENDTABS]

1. `munkinAccountId`と`secretKey`をMarketo **[!UICONTROL 管理者]** > **[!UICONTROL モバイルアプリとデバイス]**&#x200B;の「Munchkin アカウント ID」と「秘密鍵」に置き換えます。

## iOS テストデバイス

1. プロジェクト／ターゲット／情報／URL タイプを選択します。
1. 識別子${PRODUCT_NAME}を追加します。
1. URL スキームを`mkto-<Secret Key_>`に設定します。
1. Application:openURL:sourceApplication:annotation:をObjective-C用のAppDelegate.m ファイルに追加します。

## AppDelegate でカスタム URL タイプを処理する

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
- (BOOL)application:(UIApplication *)app
            openURL:(NSURL *)url
            options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options{

    return [[Marketo sharedInstance] application:app
                                         openURL:url
                                         options:options];
}
```

>[!TAB Swift]

```swift
private func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool
    {
        return Marketo.sharedInstance().application(app, open: url, options: options)
    }
```

>[!ENDTABS]

## Android に Marketo SDK をインストールする方法

### 前提条件

1. [Marketo Admin](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)でアプリケーションを追加し、アプリケーションの秘密鍵とMunchkin IDを取得します。
1. オプション：[ プッシュ通知を設定](push-notifications.md#android_setup_push)。
1. [Android用Marketo SDKのダウンロード](https://codeload.github.com/Marketo/android-sdk/zip/refs/heads/master)

### Gradle を使用した Android SDK の設定

1. アプリケーションレベルのbuild.gradle ファイルで、「依存関係」セクションの下に依存関係を追加します。

   `implementation 'com.marketo:MarketoSDK:0.8.9'`

1. ルート `build.gradle` ファイルに次の設定を追加します。

   ```
   buildscript {
       repositories {
           google()
           mavenCentral()
       }
   ```

1. プロジェクトをGradle ファイルと同期します。

### 権限の設定

`AndroidManifest.xml`を開き、次の権限を追加します。 アプリでは、「INTERNET」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリが既にリクエストしている場合は、この手順をスキップします。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### SDK の初期化

1. Application クラスまたはActivity クラスを開きます。 setContentViewの前またはアプリケーションコンテキストで、Marketo SDKをアクティビティに読み込みます。

   ```java
   // Initialize Marketo
   Marketo marketoSdk = Marketo.getInstance(getApplicationContext());
   marketoSdk.initializeSDK("native","munchkinAccountId","secretKey");
   ```

1. ProGuard 構成（オプション）

   アプリでProGuardを使用している場合は、プロジェクトフォルダーの`proguard.cfg` ファイルに次の行を追加します。 この設定により、Marketo SDKは難読化から除外されます。

   ```
   -dontwarn com.marketo.*
   -dontnote com.marketo.*
   -keep class com.marketo.`{ *; }
   ```

## Android テストデバイス

アプリケーションタグ内の `AndroidManifest.xml` に「MarketoActivity」を追加します。

```xml
<activity android:name="com.marketo.MarketoActivity"  android:configChanges="orientation|screenSize" >
    <intent-filter android:label="MarketoActivity" >
        <action  android:name="android.intent.action.VIEW"/>
        <category  android:name="android.intent.category.DEFAULT"/>
        <category  android:name="android.intent.category.BROWSABLE"/>
        <data android:host="add_test_device" android:scheme="mkto" />
    </intent-filter>
</activity>
```

## Firebase Cloud Messaging サポート

MME SDK for Androidは、Googleの[Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/) （FCM）の直接使用をサポートしています。

### アプリケーションへの FCM の追加

1. 最新のMarketo Android SDKをAndroid アプリに統合します。 [GitHub](https://github.com/Marketo/android-sdk)の手順を参照してください。
1. Firebase ConsoleでFirebase アプリを設定します。
   1. でのプロジェクトの作成/追加 [](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)Firebase コンソール。
      1. [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)で、`Add Project` を選択します。
      1. 既存の Google Cloud プロジェクトのリストから GCM プロジェクトを選択し、`Add Firebase` を選択します。
      1. Firebase のスタートアップスクリーンで、`Add Firebase to your Android App` を選択します。
      1. パッケージ名と SHA-1 を入力し、`Add App` を選択します。 Firebase アプリの新しい `google-services.json` ファイルがダウンロードされます。
      1. `Continue` を選択し、Android Studio に Google サービスプラグインを追加する詳細な手順に従います。

   1. プロジェクトの概要の「プロジェクト設定」に移動
      1. 「一般」タブをクリックします。 「google-services.json」ファイルをダウンロードします。
      1. 「Cloud Messaging」タブをクリックします。 「サーバーキー」と「送信者 ID」をコピーします。 これらの「サーバーキー」と「送信者 ID」を Marketo に指定します。
   1. Android アプリでFCMを設定します。
      1. Android Studio のプロジェクトビューに切り替えて、プロジェクトのルートディレクトリを確認します
         1. ダウンロードした「google-services.json」ファイルを Android アプリモジュールのルートディレクトリに移動します。
         1. プロジェクトレベルの build.gradle に次を追加します。

            ```
            buildscript {
              dependencies {
                classpath 'com.google.gms:google-services:4.0.0'
              }
            }
            ```

         1. アプリレベルの build.gradle に以下を追加します。

            ```
            dependencies {
              compile 'com.google.firebase:firebase-core:17.4.0'
            }
            // Add to the bottom of the file
            apply plugin: 'com.google.gms.google-services'
            ```

         1. 最後に、IDに表示されるバーで「**[!UICONTROL 今すぐ同期]**」を選択します
   1. アプリマニフェストを編集します。 FCM SDKは、必要な権限と受信者の機能を自動的に追加します。 メッセージの重複を引き起こす可能性のある、次の古い要素を削除します。

      ```xml
      <uses-permission android:name="android.permission.WAKE_LOCK" />
      <permission android:name="<your-package-name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
      <uses-permission android:name="<your-package-name>.permission.C2D_MESSAGE" />
      
      ...
      
      <receiver>
        android:name="com.google.android.gms.gcm.GcmReceiver"
        android:exported="true"
        android:permission="com.google.android.c2dm.permission.SEND"
        <intent-filter>
          <action android:name="com.google.android.c2dm.intent.RECEIVE" />
          <category android:name="<your-package-name> />
        </intent-filter>
      </receiver>
      ```
