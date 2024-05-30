---
title: "インストール"
feature: "Mobile Marketing"
description: 「Mobile Marketo用 SDK のインストール方法」
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# インストール

Marketo Mobile SDK のインストール手順。 プッシュ通知やアプリ内メッセージを送信するには、次の手順が必要です。

## iOSへのMarketo SDK のインストール

### 前提条件

1. [Marketo Admin でのアプリケーションの追加](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID の取得）
1. [プッシュ通知の設定](push-notifications.md) （オプション）

### CocoaPods を介したフレームワークのインストール

1. CocoaPods をインストールします。 `$ sudo gem install cocoapods`
1. ディレクトリをプロジェクトディレクトリに変更し、スマートデフォルトを使用してプロファイルを作成します。 `$ pod init`
1. Podfile を開きます。 `$ open -a Xcode Podfile`
1. Podfile に次の行を追加します。 `$ pod 'Marketo-iOS-SDK'`
1. Podfile を保存して閉じます。
1. Marketo iOS SDK をダウンロードしてインストールします。 `$ pod install`
1. Xcode でワークスペースを開きます。 `$ open App.xcworkspace`

### Swift パッケージマネージャーを使用したフレームワークのインストール

1. プロジェクトナビゲーターからプロジェクトを選択し、「パッケージの依存関係を追加」の下で「+」をクリックします（下図を参照）。

   ![依存関係の追加](assets/dependency-manager-add.png)

1. このリポジトリからMarketo パッケージを追加します。 このリポジトリの URL を追加します：https://github.com/Marketo/ios-sdk。

   ![リポジトリ URL](assets/dependency-manager-url.png)

1. 次に示すように、リソースバンドルを追加します。を見つけます。 `MarketoFramework.XCframework` プロジェクトナビゲーターで、Finder で開きます。 ドラッグ&amp;ドロップ `MKTResources.bundle` バンドルリソースをコピーする

### Swift ブリッジング ヘッダーの設定

1. ファイル/新規/ファイルに移動し、「ヘッダーファイル」を選択します。

   ![「ヘッダーファイル」を選択します](assets/choose-header-file.png)

1. ファイル名に「&lt;_ProjectName_>-Bridging-Header」と表示されます。

1. プロジェクト / Target / ビルドフェーズ / Swift コンパイラー/ コード生成に移動します。 Objective-Bridging ヘッダーに次のパスを追加します。

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

   ![ビルドフェーズ](assets/build-phases.png)

## SDK の初期化

Marketo iOS SDK を使用する前に、Munchkin アカウント ID とアプリ秘密鍵を使用して初期化する必要があります。 これらはそれぞれ、「モバイルアプリとデバイス」の下の「Marketo管理者」領域にあります。

1. AppDelegate.m ファイル （Objective-C）または Bridging ファイル （Swift）を開き、Marketo.h ヘッダーファイルを読み込みます。

   ```
   #import <MarketoFramework/MarketoFramework.h>
   ```

1. 次のコードをに貼り付けます。 `application:didFinishLaunchingWithOptions`：関数。

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

1. 置換 `munkinAccountId` および `secretKey` 上記では、Marketoにある「Munchkin アカウント ID」と「秘密鍵」を使用します。 **[!UICONTROL Admin]** > **[!UICONTROL モバイルアプリとデバイス]** セクション。

## iOS テストデバイス

1. Project/Target/情報/URL タイプを選択します。
1. 識別子を追加：${PRODUCT_NAME}
1. URL スキームの設定： `mkto-<Secret Key_>`
1. アプリケーションを含める:openURL:sourceApplication:annotation: to AppDelegate.m ファイル （Objective-C）

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

## Android にMarketo SDK をインストールする方法

### 前提条件

1. [Marketo Admin でのアプリケーションの追加](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID の取得）
1. [プッシュ通知の設定](push-notifications.md#android_setup_push) （オプション）
1. [Android 用Marketo SDK のダウンロード](https://codeload.github.com/Marketo/android-sdk/zip/refs/heads/master)

### Gradle を使用した Android SDK セットアップ

1. アプリケーションレベルの build.gradle ファイルの依存関係セクションの下で、次を追加します。

`implementation 'com.marketo:MarketoSDK:0.8.9'`

1. ルート `build.gradle` ファイルに含める必要がある

   ```
   buildscript {
       repositories {
           google()
           mavenCentral()
       }
   ```

1. プロジェクトと Gradle ファイルの同期

### 権限の設定

開く `AndroidManifest.xml` および次の権限を追加します。 アプリは、「インターネット」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリがこれらの権限を既にリクエストしている場合は、この手順をスキップします。

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

   アプリに ProGuard を使用している場合は、に次の行を追加します `proguard.cfg` ファイル。 ファイルは、プロジェクト フォルダ内にあります。 このコードを追加すると、Marketo SDK が不明化プロセスから除外されます。

   ```
   -dontwarn com.marketo.*
   -dontnote com.marketo.*
   -keep class com.marketo.`{ *; }
   ```

## Android テストデバイス

「MarketoActivity」をに追加 `AndroidManifest.xml` ファイルはアプリケーションタグ内にあります。

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

Android 向け MME ソフトウェア開発キット （SDK）が、より柔軟性が高く、Android アプリ開発者向けの新しいエンジニアリング機能を含む、より現代的で、安定した、スケーラブルなフレームワークに更新されました。

Android アプリの開発者は、Googleを直接使用できるようになりました [Firebase Cloud Messages](https://firebase.google.com/docs/cloud-messaging/) （FCM）と、この SDK。

### アプリケーションへの FCM の追加

1. 最新のMarketo Android SDK を Android アプリに統合します。  手順は、次の場所から利用できます [GitHub](https://github.com/Marketo/android-sdk).
1. Firebase コンソールで Firebase アプリを設定します。
   1. でのプロジェクトの作成/追加 [](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)Firebase コンソール。
      1. が含まれる [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)を選択 `Add Project`.
      1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択して、を選択します。 `Add Firebase`.
      1. Firebase のようこそ画面で、次を選択します。 `Add Firebase to your Android App`.
      1. パッケージ名と SHA-1 を指定し、を選択します。 `Add App`. 新品 `google-services.json` firebase アプリのファイルがダウンロードされます。
      1. を選択 `Continue` Android Studio でGoogle サービスプラグインを追加する手順の詳細に従います。

   1. プロジェクトの概要の「プロジェクト設定」に移動する
      1. 「一般」タブをクリックします。 「google-services.json」ファイルをダウンロードします。
      1. 「Cloud Messaging」タブをクリックします。 「サーバーキー」と「送信者 ID」をコピーします。 これらの「サーバーキー」と「送信者 ID」をMarketoに指定します。
   1. Android アプリでの FCM の変更
      1. Android Studio のプロジェクトビューに切り替えて、プロジェクトのルートディレクトリを表示します
         1. ダウンロードした「google-services.json」ファイルを Android アプリモジュールのルートディレクトリに移動します
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
