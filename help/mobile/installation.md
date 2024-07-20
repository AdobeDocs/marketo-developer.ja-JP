---
title: インストール
feature: Mobile Marketing
description: Mobile Marketo用 SDK のインストール方法
exl-id: e0b79d85-3509-46d2-a77d-cee211c5ec7f
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 7%

---

# インストール

Marketo Mobile SDK のインストール手順。 プッシュ通知やアプリ内メッセージを送信するには、次の手順が必要です。

## iOSへのMarketo SDK のインストール

### 前提条件

1. [Marketo管理者でアプリケーションを追加 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID を取得）
1. [ プッシュ通知の設定 ](push-notifications.md) （オプション）

### CocoaPods を介したフレームワークのインストール

1. CocoaPods をインストールします。`$ sudo gem install cocoapods`
1. ディレクトリをプロジェクトディレクトリに変更し、スマートデフォルトを使用してプロファイルを作成します。`$ pod init`
1. Podfile を開きます。`$ open -a Xcode Podfile`
1. Podfile に次の行を追加します。`$ pod 'Marketo-iOS-SDK'`
1. Podfile を保存して閉じます。
1. Marketo iOS SDK をダウンロードしてインストールします。`$ pod install`
1. Xcode でワークスペースを開きます。`$ open App.xcworkspace`

### Swift パッケージマネージャーを使用したフレームワークのインストール

1. プロジェクトナビゲーターからプロジェクトを選択し、「パッケージの依存関係を追加」の下で「+」をクリックします（下図を参照）。

   ![ 依存関係の追加 ](assets/dependency-manager-add.png)

1. このリポジトリからMarketo パッケージを追加します。 このリポジトリの URL を追加します：https://github.com/Marketo/ios-sdk。

   ![ リポジトリ URL](assets/dependency-manager-url.png)

1. 次に示すように、リソースバンドルを追加します。プロジェクトナビゲーターで `MarketoFramework.XCframework` を見つけて、Finder で開きます。 `MKTResources.bundle` をドラッグ&amp;ドロップして、バンドルリソースをコピーします。

### Swift ブリッジング ヘッダーの設定

1. ファイル/新規/ファイルに移動し、「ヘッダーファイル」を選択します。

   ![ 「ヘッダーファイル」を選択する ](assets/choose-header-file.png)

1. ファイルに「&lt;_ProjectName_>-Bridging-Header」という名前を付けます。

1. プロジェクト / Target / ビルドフェーズ / Swift コンパイラー/ コード生成に移動します。 Objective-Bridging ヘッダーに次のパスを追加します。

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

   ![ ビルドフェーズ ](assets/build-phases.png)

## SDK の初期化

Marketo iOS SDK を使用する前に、Munchkin アカウント ID とアプリ秘密鍵を使用して初期化する必要があります。 これらはそれぞれ、「モバイルアプリとデバイス」の下の「Marketo管理者」領域にあります。

1. AppDelegate.m ファイル （Objective-C）または Bridging ファイル （Swift）を開き、Marketo.h ヘッダーファイルを読み込みます。

   ```
   #import <MarketoFramework/MarketoFramework.h>
   ```

1. 次のコードを `application:didFinishLaunchingWithOptions`：関数内に貼り付けます。

   なお、「native」をネイティブアプリのフレームワークタイプとして渡す必要があります。

>[!BEGINTABS]

>[!TAB 目標 C]

```
Marketo *sharedInstance = [Marketo sharedInstance];

[sharedInstance initializeWithMunchkinID:@"munchkinAccountId" appSecret:@"secretKey" mobileFrameworkType:@"native" launchOptions:launchOptions];
```

>[!TAB Swift]

```
let sharedInstance: Marketo = Marketo.sharedInstance()

sharedInstance.initialize(withMunchkinID: "munchkinAccountId", appSecret: "secretKey", mobileFrameworkType: "native", launchOptions: launchOptions)
```

>[!ENDTABS]

1. 「Munchkin アカウント ID」と「秘密鍵」を使用して、上記 `munkinAccountId` と `secretKey` を置き換えます。これらはMarketo **[!UICONTROL 管理者]**/**[!UICONTROL モバイルアプリとデバイス]** セクションにあります。

## iOS テストデバイス

1. Project/Target/情報/URL タイプを選択します。
1. 識別子の追加：${PRODUCT_NAME}
1. URL スキームの設定：`mkto-<Secret Key_>`
1. application:openURL:sourceApplication:annotation: を AppDelegate.m ファイルに含める（Objective-C）

## AppDelegate でのカスタム Url タイプの処理

>[!BEGINTABS]

>[!TAB 目標 C]

```
- (BOOL)application:(UIApplication *)app
            openURL:(NSURL *)url
            options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options{
   
    return [[Marketo sharedInstance] application:app
                                         openURL:url
                                         options:options];    
}
```

>[!TAB Swift]

```
private func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool
    {
        return Marketo.sharedInstance().application(app, open: url, options: options)
    }
```

>[!ENDTABS]

## AndroidにMarketo SDK をインストールする方法

### 前提条件

1. [Marketo管理者でアプリケーションを追加 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID を取得）
1. [ プッシュ通知の設定 ](push-notifications.md#android_setup_push) （オプション）
1. [Android用Marketo SDK のダウンロード ](https://codeload.github.com/Marketo/android-sdk/zip/refs/heads/master)

### Gradle を使用したAndroid SDK のセットアップ

1. アプリケーションレベルの build.gradle ファイルの依存関係セクションの下で、次を追加します。

`implementation 'com.marketo:MarketoSDK:0.8.9'`

1. ルートの `build.gradle` ファイルには、

   ```
   buildscript {
       repositories {
           google()
           mavenCentral()
       }
   ```

1. プロジェクトと Gradle ファイルの同期

### 権限の設定

`AndroidManifest.xml` を開いて、次の権限を追加します。 アプリは、「インターネット」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリがこれらの権限を既にリクエストしている場合は、この手順をスキップします。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### SDK の初期化

1. アプリで Application クラスまたは Activity クラスを開き、Marketo SDK をアクティビティに読み込んでから、setContentView または Application Context に設定します。

   ```java
   // Initialize Marketo
   Marketo marketoSdk = Marketo.getInstance(getApplicationContext());
   marketoSdk.initializeSDK("native","munchkinAccountId","secretKey");
   ```

1. ProGuard 構成（オプション）

   アプリに ProGuard を使用している場合は、`proguard.cfg` ファイルに次の行を追加します。 ファイルは、プロジェクト フォルダ内にあります。 このコードを追加すると、Marketo SDK が不明化プロセスから除外されます。

   ```
   -dontwarn com.marketo.*
   -dontnote com.marketo.*
   -keep class com.marketo.`{ *; }
   ```

## Android テストデバイス

アプリケーションタグ内のファイルに「MarketoActivity」 `AndroidManifest.xml` 追加します。

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

Android用 MME Software Development Kit （SDK）が、より柔軟で安定した、拡張性の高いフレームワークに更新されました。このフレームワークには、Android アプリ開発者向けの新しいエンジニアリング機能が備わっています。

Android アプリ開発者は、この SDK でGoogle[Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/) （FCM）を直接使用できるようになりました。

### アプリケーションへの FCM の追加

1. Android アプリに最新のMarketo Android SDK を統合します。  手順は、[GitHub](https://github.com/Marketo/android-sdk) で確認できます。
1. Firebase コンソールで Firebase アプリを設定します。
   1. でのプロジェクトの作成/追加 [](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)Firebase コンソール。
      1. [Firebase コンソール ](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/) で、「`Add Project`」を選択します。
      1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択し、「`Add Firebase`」を選択します。
      1. Firebase のスタートアップスクリーンで、「`Add Firebase to your Android App`」を選択します。
      1. パッケージ名と SHA-1 を指定し、「`Add App`」を選択します。 新品 `google-services.json` firebase アプリのファイルがダウンロードされます。
      1. `Continue` を選択し、Android Studio にGoogle Services プラグインを追加するための詳細な手順に従います。

   1. プロジェクトの概要の「プロジェクト設定」に移動する
      1. 「一般」タブをクリックします。 「google-services.json」ファイルをダウンロードします。
      1. 「Cloud Messaging」タブをクリックします。 「サーバーキー」と「送信者 ID」をコピーします。 これらの「サーバーキー」と「送信者 ID」をMarketoに指定します。
   1. Android アプリでの FCM の変更
      1. Android Studio のプロジェクトビューに切り替えて、プロジェクトのルートディレクトリを表示します
         1. ダウンロードした「google-services.json」ファイルをAndroid アプリモジュールのルートディレクトリに移動します
         1. プロジェクトレベルの build.gradle で、以下を追加します。

            ```
            buildscript {
              dependencies {
                classpath 'com.google.gms:google-services:4.0.0'
              }
            }
            ```

         1. App-level build.gradle で、以下を追加します。

            ```
            dependencies {
              compile 'com.google.firebase:firebase-core:17.4.0'
            } 
            // Add to the bottom of the file 
            apply plugin: 'com.google.gms.google-services'
            ```

         1. 最後に、ID に表示されるバーの「Sync now」をクリックします
   1. アプリのマニフェストの編集 FCM SDK は、必要なすべての権限と必要なレシーバー機能を自動的に追加します。 次の古い（有害な可能性がある）要素は、アプリのマニフェストから削除してください。

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
