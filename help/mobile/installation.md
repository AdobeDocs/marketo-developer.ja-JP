---
title: インストール
feature: Mobile Marketing
description: Mobile Marketo SDK のインストール方法
exl-id: e0b79d85-3509-46d2-a77d-cee211c5ec7f
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 99%

---

# インストール

Marketo Mobile SDK のインストール手順です。プッシュ通知やアプリ内メッセージを送信するには、以下の手順が必要です。

## iOS への Marketo SDK のインストール

### 前提条件

1. [Marketo Admin でアプリケーションを追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)（アプリケーションの秘密鍵と Munchkin ID を取得）
1. [プッシュ通知を設定](push-notifications.md)（オプション）

### CocoaPods 経由のフレームワークのインストール

1. CocoaPods をインストールします。`$ sudo gem install cocoapods`
1. ディレクトリをプロジェクトディレクトリに変更し、スマートデフォルトを使用して Podfile を作成します。`$ pod init`
1. Podfile を開きます。`$ open -a Xcode Podfile`
1. Podfile に次の行を追加します。`$ pod 'Marketo-iOS-SDK'`
1. Podfile を保存して閉じます。
1. Marketo iOS SDK をダウンロードしてインストールします。`$ pod install`
1. Xcode でワークスペースを開きます。`$ open App.xcworkspace`

### Swift パッケージマネージャーを使用したフレームワークのインストール

1. プロジェクトナビゲーターからプロジェクトを選択し、「パッケージの依存関係を追加」の下にある「+」をクリックします（以下を参照）。

   ![依存関係の追加](assets/dependency-manager-add.png)

1. このリポジトリから Marketo パッケージを追加します。このリポジトリの URL（https://github.com/Marketo/ios-sdk）を追加します。

   ![リポジトリ URL](assets/dependency-manager-url.png)

1. ここで、次のようにリソースバンドルを追加します。プロジェクトナビゲーターで `MarketoFramework.XCframework` を見つけて、Finder で開きます。`MKTResources.bundle` をドラッグ＆ドロップして、バンドルリソースをコピーします。

### Swift ブリッジングヘッダーの設定

1. ファイル／新規／ファイルに移動し、「ヘッダーファイル」を選択します。

   ![「ヘッダーファイル」の選択](assets/choose-header-file.png)

1. ファイルに「&lt;_ProjectName_>-Bridging-Header」という名前を付けます。

1. プロジェクト／ターゲット／ビルドフェーズ／Swift コンパイラー／コード生成に移動します。Objective-Bridging ヘッダーに次のパスを追加します。

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

   ![ビルドフェーズ](assets/build-phases.png)

## SDK の初期化

Marketo iOS SDK を使用する前に、Munchkin アカウント ID とアプリ秘密鍵を使用して初期化する必要があります。これらは、「モバイルアプリとデバイス」の下にある Marketo Admin 領域にあります。

1. AppDelegate.m ファイル（Objective-C）またはブリッジングファイル（Swift）を開き、Marketo.h ヘッダーファイルを読み込みます。

   ```
   #import <MarketoFramework/MarketoFramework.h>
   ```

1. 次のコードを `application:didFinishLaunchingWithOptions`: 関数内にペーストします。

   Native アプリのフレームワークタイプとして &quot;native&quot; を渡す必要があります。

>[!BEGINTABS]

>[!TAB Objective C]

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

1. 上記の `munkinAccountId` と `secretKey` を、Marketo **[!UICONTROL Admin]**／**[!UICONTROL モバイルアプリとデバイス]**&#x200B;セクションにある「Munchkin アカウント ID」と「秘密鍵」を使用して置き換えます。

## iOS テストデバイス

1. プロジェクト／ターゲット／情報／URL タイプを選択します。
1. 識別子を追加：${PRODUCT_NAME}
1. URL スキーム `mkto-<Secret Key_>` を設定します。
1. AppDelegate.m ファイルにアプリケーション :openURL:sourceApplication:annotation: を含めます（Objective-C）。

## AppDelegate でカスタム URL タイプを処理する

>[!BEGINTABS]

>[!TAB Objective C]

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

## Android に Marketo SDK をインストールする方法

### 前提条件

1. [Marketo Admin でアプリケーションを追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)（アプリケーションの秘密鍵と Munchkin ID を取得）
1. [プッシュ通知を設定](push-notifications.md#android_setup_push)（オプション）
1. [Android 用 Marketo SDK をダウンロード](https://codeload.github.com/Marketo/android-sdk/zip/refs/heads/master)

### Gradle を使用した Android SDK の設定

1.アプリケーションレベルの build.gradle ファイルの依存関係セクションに以下を追加します。

`implementation 'com.marketo:MarketoSDK:0.8.9'`

1. ルートの `build.gradle` ファイルには、次の操作を実行します。

   ```
   buildscript {
       repositories {
           google()
           mavenCentral()
       }
   ```

1. プロジェクトを Gradle ファイルと同期します。

### 権限の設定

`AndroidManifest.xml` を開き、次の権限を追加します。アプリでは、「INTERNET」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。アプリで既にこれらの権限をリクエストしている場合は、この手順をスキップしてください。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### SDK の初期化

1. アプリで Application クラスまたは Activity クラスを開き、setContentView の前またはアプリケーションコンテキスト内で Marketo SDK をアクティビティに読み込みます。

   ```java
   // Initialize Marketo
   Marketo marketoSdk = Marketo.getInstance(getApplicationContext());
   marketoSdk.initializeSDK("native","munchkinAccountId","secretKey");
   ```

1. ProGuard 構成（オプション）

   アプリに ProGuard を使用している場合は、`proguard.cfg` ファイルに次の行を追加します。ファイルは、プロジェクトフォルダー内にあります。このコードを追加すると、Marketo SDK が不明化プロセスから除外されます。

   ```
   -dontwarn com.marketo.*
   -dontnote com.marketo.*
   -keep class com.marketo.`{ *; }
   ```

## Android テストデバイス

アプリケーションタグ内の `AndroidManifest.xml` ファイルに「MarketoActivity」を追加します。

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

Android 向け MME Software Development Kit（SDK）は、Android アプリデベロッパー向けの柔軟性と新しいエンジニアリング機能を備えた、より最新で安定したスケーラブルなフレームワークに更新されました。

この SDK では、Android アプリデベロッパーが Google の [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/)（FCM）を直接使用できるようになりました。

### アプリケーションへの FCM の追加

1. 最新の Marketo Android SDK を Android アプリに統合します。手順は [GitHub](https://github.com/Marketo/android-sdk) で確認できます。
1. Firebase コンソールで Firebase アプリを設定します。
   1. でのプロジェクトの作成/追加 [&#128279;](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)Firebase コンソール。
      1. [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)で、`Add Project` を選択します。
      1. 既存の Google Cloud プロジェクトのリストから GCM プロジェクトを選択し、`Add Firebase` を選択します。
      1. Firebase のスタートアップスクリーンで、`Add Firebase to your Android App` を選択します。
      1. パッケージ名と SHA-1 を入力し、`Add App` を選択します。Firebase アプリの新しい `google-services.json` ファイルがダウンロードされます。
      1. `Continue` を選択し、Android Studio に Google サービスプラグインを追加する詳細な手順に従います。

   1. プロジェクトの概要の「プロジェクト設定」に移動
      1. 「一般」タブをクリックします。「google-services.json」ファイルをダウンロードします。
      1. 「Cloud Messaging」タブをクリックします。 「サーバーキー」と「送信者 ID」をコピーします。これらの「サーバーキー」と「送信者 ID」を Marketo に指定します。
   1. Android アプリで FCM 変更を設定します
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

         1. 最後に、ID に表示されるバーの「今すぐ同期」をクリックします。
   1. アプリのマニフェストを編集します。FCM SDK では、必要なすべての権限と必要な受信者機能が自動的に追加されます。アプリのマニフェストから次の古い（メッセージの重複を引き起こす可能性があるので、潜在的に有害な）要素を削除します

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
