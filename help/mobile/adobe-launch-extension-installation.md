---
title: '[!DNL Adobe Launch] 拡張機能のインストール'
feature: Mobile Marketing
description: モバイル用Adobe Launch Marketo拡張機能をインストールします。 プッシュとアプリ内では、iOSとAndroidの設定、テストデバイス、権限、FCM の手順に従います。
exl-id: d71b7cd7-309b-4882-9bba-7daaaa5ef32d
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 96%

---

# [!DNL Adobe Launch] 拡張機能のインストール

[!DNL Adobe Launch] Marketo 拡張機能のインストール手順です。プッシュ通知やアプリ内メッセージを送信するには、以下の手順が必要です。

## 前提条件

1. [Marketo Admin でアプリケーションを追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)（アプリケーションの秘密鍵と Munchkin ID を取得します）
1. [ [!DNL Adobe Launch]  ポータルでプロパティを設定](https://experience.adobe.com/#/@amc/data-collection/home)
1. [!DNL Adobe Launch] ポータルでプロパティのアプリケーション秘密鍵と Munchkin ID を設定
1. [プッシュ通知を設定](push-notifications.md)（オプション）

## iOS に Marketo 拡張機能をインストールする方法

### Swift ブリッジングヘッダーの設定

1. [!UICONTROL ファイル]／[!UICONTROL 新規]／[!UICONTROL ファイル]に移動し、「**[!UICONTROL ヘッダーファイル]**」を選択します。

1. ファイルに「&lt;_ProjectName_>-Bridging-Header」という名前を付けます。

1. [!UICONTROL プロジェクト]／[!UICONTROL ターゲット]／[!UICONTROL ビルド設定]／[!UICONTROL Swift コンパイラー]／[!UICONTROL コード生成]に移動します。「Objective-Bridging」ヘッダーに次のパスを追加します。

`$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

## 拡張機能の初期化

>[!BEGINTABS]

>[!TAB Objective C]

を更新 `applicationDidBecomeActive` 次のようなメソッド

```
(void)applicationDidBecomeActive:(UIApplication*) application
{
 [[ALMarketo sharedInstance] initializeMarketo:nil];
}
```

>[!TAB Swift]

を更新 `applicationDidBecomeActive` 次のようなメソッド

```
func applicationDidBecomeActive(_ application: UIApplication)
{
 ALMarketo.sharedInstance().initializeMarketo(nil)
}
```

>[!ENDTABS]

## iOS テストデバイス

1. **[!UICONTROL プロジェクト]**／**[!UICONTROL ターゲット]**／**[!UICONTROL 情報]**／**[!UICONTROL URL タイプ]**&#x200B;を選択します。
1. 識別子を追加：${PRODUCT_NAME}
1. URL スキーム mkto-&lt;S_ecret Key_> を設定します。
1. `AppDelegate.m file`（Objective-C）に `application:openURL:sourceApplication:annotation:` を含めます。

### AppDelegate でカスタム URL タイプを処理する

>[!BEGINTABS]

>[!TAB Objective C]

```
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

```
func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    return ALMarketo.sharedInstance().application(application, open: url, sourceApplication: nil, annotation: nil)
}
```

>[!ENDTABS]

## Android に Marketo SDK をインストールする方法

### Android 拡張機能の設定

[!DNL Adobe Launch] ポータルの手順に従ってください。

### 権限の設定

`AndroidManifest.xml` を開き、次の権限を追加します。アプリでは、「INTERNET」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。アプリで既にこれらの権限をリクエストしている場合は、この手順をスキップしてください。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

## 拡張機能の初期化

ProGuard 構成（オプション）

アプリに ProGuard を使用している場合は、`proguard.cfg` ファイルに次の行を追加します。ファイルは、`project` フォルダー内にあります。このコードを追加すると、Marketo SDK が不明化プロセスから除外されます。

```
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

Android 向け MME Software Development Kit（SDK）は、Android アプリデベロッパー向けの柔軟性と新しいエンジニアリング機能を備えた、より最新で安定したスケーラブルなフレームワークに更新されました。

この SDK では、Android アプリデベロッパーが Google の [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/)（FCM）を直接使用できるようになりました。

### アプリケーションへの FCM の追加

1. 最新の Marketo Android SDK を Android アプリに統合します。手順は [GitHub](https://github.com/Marketo/android-sdk) で確認できます。
1. Firebase コンソールで Firebase アプリを設定します。
   1. でのプロジェクトの作成/追加 [&#128279;](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)Firebase コンソール。
      1. が含まれる [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)を選択 **[!UICONTROL プロジェクトを追加]**.
      1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択して、を選択します。 **[!UICONTROL Firebase の追加]**.
      1. Firebase のスタートアップスクリーンで、「**[!UICONTROL Android アプリに Firebase を追加]**」を選択します。
      1. パッケージ名と SHA-1 を指定し、を選択します。 **[!UICONTROL アプリを追加]**. 新品 `google-services.json` firebase アプリのファイルがダウンロードされます。
      1. 「**[!UICONTROL 続行]**」を選択し、Android Studio に Google サービスプラグインを追加する詳細な手順に従います。

   1. 「[!UICONTROL プロジェクトの概要」]」の「**[!UICONTROL プロジェクトの設定]**」に移動します
      1. 「**[!UICONTROL 全般]**」タブをクリックします。`google-services.json` ファイルをダウンロードします。
      1. 「**[!UICONTROL Cloud Messaging]**」タブをクリックします。 [!UICONTROL サーバーキー]と[!UICONTROL 送信者 ID] をコピーします。 これらの[!UICONTROL サーバーキー]と[!UICONTROL 送信者 ID] を Marketo に指定します。
   1. Android アプリで FCM 変更を設定します
      1. Android Studio のプロジェクトビューに切り替えて、プロジェクトのルートディレクトリを確認します
         1. ダウンロードした `google-services.json` ファイルを Android アプリモジュールのルートディレクトリに移動します
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

         1. 最後に、IDに表示されるバーの「**[!UICONTROL 今すぐ同期]**」をクリックします。
   1. アプリのマニフェストを編集します。FCM SDK では、必要なすべての権限と必要な受信者機能が自動的に追加されます。アプリのマニフェストから次の古い（メッセージの重複を引き起こす可能性があるので、潜在的に有害な）要素を削除します

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

Firebase Cloud Messaging サポートに関するよくある質問です。

**Q：MME SDK を最新バージョンに更新する手順はどこにありますか？**&#x200B;手順について詳しくは、Marketo デベロッパーサイトの[こちら](installation.md)を参照してください。

**Q：SDK を最新バージョンに更新するには、Android アプリケーションの更新バージョンを既存のユーザに公開する必要がありますか？**&#x200B;いいえ。

**Q：Marketo Android SDK と統合された Android アプリを公開している既存の MME 顧客にはどのような影響がありますか？**&#x200B;次のように、Android 上の既存の GCM クライアントアプリを Firebase Cloud Messaging（FCM）に移行できます。

1. [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)で、「**[!UICONTROL プロジェクトを追加]**」を選択します。
1. 既存の Google Cloud プロジェクトのリストから GCM プロジェクトを選択し、「**[!UICONTROL Firebase を追加]**」を選択します。
1. Firebase のスタートアップスクリーンで、「**[!UICONTROL Android アプリに Firebase を追加]**」を選択します。
1. パッケージ名と SHA-1 を入力し、「**[!UICONTROL アプリを追加]**」を選択します。新しい google-services.json ファイル
1. （Firebase アプリ用）がダウンロードされます。
1. 「**[!UICONTROL 続行]**」を選択し、Android Studio に Google サービスプラグインを追加する詳細な手順に従います。

**Q：GCM アプリを使用した古い Marketo SDK を使用して作成されたリードをターゲットにできますか？**&#x200B;はい。Marketo SDK を使用して作成されたすべてのリードは、プッシュ通知の送信先にすることができます。
