---
title: '[!DNL Adobe Launch] 拡張機能のインストール'
feature: Mobile Marketing
description: Adobe Launch Marketoのモバイル向け拡張機能をインストールします。 IOSとAndroidの設定に従い、プッシュおよびアプリ内のデバイス、権限、FCMの手順をテストします。
exl-id: d71b7cd7-309b-4882-9bba-7daaaa5ef32d
TQID: https://experienceleague.adobe.com/UZRHaRBISIZsE6E25Ee7CnnYwyZwi6w2YgOQJ-JL00U
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 753
ht-degree: 43%

---

# [!DNL Adobe Launch] 拡張機能のインストール

[!DNL Adobe Launch] Marketo拡張機能をインストールして、プッシュ通知、アプリ内メッセージ、またはその両方を送信します。

## 前提条件

1. [Marketo Admin](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)でアプリケーションを追加し、アプリケーションの秘密鍵とMunchkin IDを取得します。
1. [ ポータル  [!DNL Adobe Launch] でプロパティを設定します](https://experience.adobe.com/#/@amc/data-collection/home)。
1. [!DNL Adobe Launch] ポータルのプロパティのアプリケーション秘密鍵とMunchkin IDを設定します。
1. オプション：[ プッシュ通知を設定](push-notifications.md)。

## iOS に Marketo 拡張機能をインストールする方法

### Swift ブリッジングヘッダーの設定

1. [!UICONTROL  ファイル ] > [!UICONTROL 新規] > [!UICONTROL  ファイル ]に移動し、**[!UICONTROL ヘッダーファイル]**&#x200B;を選択します。

1. ファイルに「&lt;_ProjectName_>-Bridging-Header」という名前を付けます。

1. [!UICONTROL プロジェクト]／[!UICONTROL ターゲット]／[!UICONTROL ビルド設定]／[!UICONTROL Swift コンパイラー]／[!UICONTROL コード生成]に移動します。
1. 「Objective-Bridging」ヘッダーに次のパスを追加します。

`$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

## 拡張機能の初期化

>[!BEGINTABS]

>[!TAB Objective C]

次のように`applicationDidBecomeActive` メソッドを更新します。

```objectivec
(void)applicationDidBecomeActive:(UIApplication*) application
{
 [[ALMarketo sharedInstance] initializeMarketo:nil];
}
```

>[!TAB Swift]

次のように`applicationDidBecomeActive` メソッドを更新します。

```objectivec
func applicationDidBecomeActive(_ application: UIApplication)
{
 ALMarketo.sharedInstance().initializeMarketo(nil)
}
```

>[!ENDTABS]

## iOS テストデバイス

1. **[!UICONTROL プロジェクト]**／**[!UICONTROL ターゲット]**／**[!UICONTROL 情報]**／**[!UICONTROL URL タイプ]**&#x200B;を選択します。
1. 識別子${PRODUCT_NAME}を追加します。
1. URL スキームをmkto-&lt;S_ecret Key_>に設定します。
1. Objective-Cの`application:openURL:sourceApplication:annotation:`を`AppDelegate.m file`に追加します。

### AppDelegate でカスタム URL タイプを処理する

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
#ifdef __IPHONE_10_0
-(BOOL)application:(UIApplication *)application
           openURL:(NSURL *)url
           options:(NSDictionary *)options{
    return [[ALMarketo sharedInstance] application:application
                                         openURL:url
                               sourceApplication:nil
                                      annotation:nil];
}
#endif

- (BOOL)application:(UIApplication *)application
            openURL:(NSURL *)url
  sourceApplication:(NSString *)sourceApplication
         annotation:(id)annotation {
    return [[ALMarketo sharedInstance] application:application
                                         openURL:url
                               sourceApplication:nil
                                      annotation:nil];
}
```

>[!TAB Swift]

```objectivec
func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    return ALMarketo.sharedInstance().application(application, open: url, sourceApplication: nil, annotation: nil)
}
```

>[!ENDTABS]

## Android に Marketo SDK をインストールする方法

### Android 拡張機能の設定

[!DNL Adobe Launch] ポータルの指示に従います。

### 権限の設定

`AndroidManifest.xml`を開き、次の権限を追加します。 アプリでは、「INTERNET」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリが既にリクエストしている場合は、この手順をスキップします。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

## 拡張機能の初期化

ProGuard 構成（オプション）

アプリでProGuardを使用している場合は、`project` フォルダーの`proguard.cfg` ファイルに次の行を追加します。 この設定により、Marketo SDKは難読化から除外されます。

```text
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
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
   1. [](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)Firebase コンソールでプロジェクトを作成または追加します。
      1. が含まれる [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)を選択 **[!UICONTROL プロジェクトを追加]**.
      1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択して、を選択します。 **[!UICONTROL Firebase の追加]**.
      1. Firebase のスタートアップスクリーンで、「**[!UICONTROL Android アプリに Firebase を追加]**」を選択します。
      1. パッケージ名と SHA-1 を指定し、を選択します。 **[!UICONTROL アプリを追加]**. 新品 `google-services.json` firebase アプリのファイルがダウンロードされます。
      1. 「**[!UICONTROL 続行]**」を選択し、Android Studio に Google サービスプラグインを追加する詳細な手順に従います。

   1. [!UICONTROL  プロジェクト概要]の&#x200B;**[!UICONTROL プロジェクト設定]**&#x200B;に移動します。
      1. 「**[!UICONTROL 一般]**」タブを選択し、`google-services.json`をダウンロードします。
      1. 「**[!UICONTROL クラウドメッセージ]**」タブを選択します。 [!UICONTROL  サーバーキー]と[!UICONTROL 送信者ID]をコピーし、Marketoに提供します。
   1. Android アプリでFCMを設定します。
      1. Android Studioのプロジェクトビューに切り替えて、プロジェクトのルートディレクトリを表示します。
         1. ダウンロードした`google-services.json` ファイルをAndroid アプリモジュールのルートディレクトリに移動します。
         1. プロジェクトレベルの `build.gradle` に以下を追加します。

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

         1. IDEに表示されるバーで「**[!UICONTROL 今すぐ同期]**」を選択します。
   1. アプリマニフェストを編集します。 FCM SDKは、必要な権限と受信者の機能を自動的に追加します。 メッセージの重複を引き起こす可能性のある、次の古い要素を削除します。

      ```xml
      <uses-permission android:name="android.permission.WAKE_LOCK" />
      <permission android:name="<your-package-name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
      <uses-permission android:name="<your-package-name>.permission.C2D_MESSAGE" />
      
      ...
      
      <receiver>
        android:name="com.google.android.gms.gcm.GcmReceiver"
        android:exported="true"
        android:permission="com.google.android.c2dm.permission.SEND">
        <intent-filter>
          <action android:name="com.google.android.c2dm.intent.RECEIVE" />
          <category android:name="<your-package-name> />
        </intent-filter>
      </receiver>
      ```

### FCM に関するよくある質問

これらの質問では、Firebase Cloud Messagingのサポートについて説明します。

**Q: MME SDKの最新バージョンに更新する手順はどこで確認できますか？** Marketo Developer サイトの[ インストール手順](installation.md)を参照してください。

**Q：最新バージョンのSDKにアップデートする場合、既存のユーザーに対してAndroid アプリケーションの更新バージョンを公開する必要がありますか？** いいえ、できません。

**Q: Marketo Android SDKを使用する公開済みAndroid アプリを使用している既存のMMEのお客様にどのような影響がありますか？** 既存のAndroid GCM クライアント アプリをFirebase Cloud Messaging （FCM）に次のように移行します。

1. [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)で、「**[!UICONTROL プロジェクトを追加]**」を選択します。
1. 既存の Google Cloud プロジェクトのリストから GCM プロジェクトを選択し、「**[!UICONTROL Firebase を追加]**」を選択します。
1. Firebase のスタートアップスクリーンで、「**[!UICONTROL Android アプリに Firebase を追加]**」を選択します。
1. パッケージ名と SHA-1 を入力し、「**[!UICONTROL アプリを追加]**」を選択します。 Firebase アプリ用の新しいgoogle-services.json ファイルがダウンロードされます。
1. 「**[!UICONTROL 続行]**」を選択し、Android Studio に Google サービスプラグインを追加する詳細な手順に従います。

**Q: GCM アプリを使用した古いMarketo SDKで作成されたリードをターゲットにできますか？** はい。 Marketo SDKで作成したすべてのリードを、プッシュ通知の対象にすることができます。
