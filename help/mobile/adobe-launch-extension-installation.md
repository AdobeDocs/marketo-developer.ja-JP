---
title: '[!DNL Adobe Launch] 拡張機能のインストール'
feature: Mobile Marketing
description: '[!DNL Adobe Launch] 拡張機能のインストールの概要'
exl-id: d71b7cd7-309b-4882-9bba-7daaaa5ef32d
source-git-commit: 6fc45ff98998217923e2a5b02d00d1522fe3272c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 10%

---

# [!DNL Adobe Launch] 拡張機能のインストール

Marketo拡張機能 [!DNL Adobe Launch] インストール手順。 プッシュ通知やアプリ内メッセージを送信するには、次の手順が必要です。

## 前提条件

1. [Marketo管理者でアプリケーションを追加 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID を取得）
1. [ ポータル内でのプロパティ  [!DNL Adobe Launch]  設定 ](https://experience.adobe.com/#/@amc/data-collection/home)
1. [!DNL Adobe Launch] ポータルのプロパティにアプリケーション秘密鍵と Munchkin ID を設定する
1. [ プッシュ通知の設定 ](push-notifications.md) （オプション）

## iOSにMarketo拡張機能をインストールする方法

### Swift ブリッジング ヘッダーの設定

1. [!UICONTROL &#x200B; ファイル &#x200B;]/[!UICONTROL &#x200B; 新規 &#x200B;]/[!UICONTROL &#x200B; ファイル &#x200B;] に移動し、「**[!UICONTROL ヘッダーファイル]**」を選択します。

1. ファイルに「&lt;_ProjectName_>-Bridging-Header」という名前を付けます。

1. [!UICONTROL &#x200B; プロジェクト &#x200B;]/[!UICONTROL &#x200B; ターゲット &#x200B;]/[!UICONTROL &#x200B; ビルド設定 &#x200B;]/[!UICONTROL Swift コンパイラ &#x200B;]/[!UICONTROL &#x200B; コード生成 &#x200B;] に移動します。 「Objective-Bridging」ヘッダーに次のパスを追加します。

`$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

## 拡張機能の初期化

>[!BEGINTABS]

>[!TAB 目標 C]

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

1. **[!UICONTROL プロジェクト]**/**[!UICONTROL ターゲット]**/**[!UICONTROL 情報]**/**[!UICONTROL URL タイプ]** を選択します。
1. 識別子の追加：${PRODUCT_NAME}
1. URL スキームを設定：mkto-&lt;S_ecret Key_>
1. `application:openURL:sourceApplication:annotation:` ～ `AppDelegate.m file` を含める（Objective-C）

### AppDelegate でのカスタム Url タイプの処理

>[!BEGINTABS]

>[!TAB 目標 C]

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

## AndroidにMarketo SDK をインストールする方法

### Android拡張機能の設定

[!DNL Adobe Launch] portal の手順に従う

### 権限の設定

`AndroidManifest.xml` を開いて、次の権限を追加します。 アプリは、「インターネット」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリがこれらの権限を既にリクエストしている場合は、この手順をスキップします。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

## 拡張機能の初期化

ProGuard 構成（オプション）

アプリに ProGuard を使用している場合は、`proguard.cfg` ファイルに次の行を追加します。 ファイルは、`project` フォルダー内にあります。 このコードを追加すると、Marketo SDK が不明化プロセスから除外されます。

```
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

## Android  テスト  デバイス

「MarketoActivity」をアプリケーションタグ内に追加 `AndroidManifest.xml` ます。

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
   1. でのプロジェクトの作成/追加 [&#128279;](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)Firebase コンソール。
      1. が含まれる [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)を選択 **[!UICONTROL プロジェクトを追加]**.
      1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択して、を選択します。 **[!UICONTROL Firebase の追加]**.
      1. Firebase のようこそ画面で、「**[!UICONTROL Android アプリに Firebase を追加]**」を選択します。
      1. パッケージ名と SHA-1 を指定し、を選択します。 **[!UICONTROL アプリを追加]**. 新品 `google-services.json` firebase アプリのファイルがダウンロードされます。
      1. 「**[!UICONTROL 続行]**」を選択し、Android Studio にGoogle Services プラグインを追加する手順の詳細に従います。

   1. **[!UICONTROL プロジェクトの概要]** の [!UICONTROL &#x200B; プロジェクト設定 &#x200B;] に移動します
      1. **[!UICONTROL 一般]** タブをクリックします。 `google-services.json` ファイルをダウンロードします。
      1. 「**[!UICONTROL クラウドメッセージング]**」タブをクリックします。 [!UICONTROL &#x200B; サーバーキー &#x200B;] と [!UICONTROL &#x200B; 送信者 ID] をコピーします。 これらの [!UICONTROL &#x200B; サーバーキー &#x200B;] と [!UICONTROL &#x200B; 送信者 ID] をMarketoに提供します。
   1. Android アプリでの FCM の変更
      1. Android Studio のプロジェクトビューに切り替えて、プロジェクトのルートディレクトリを表示します
         1. ダウンロードした `google-services.json` ファイルをAndroid アプリモジュールのルートディレクトリに移動します。
         1. プロジェクトレベルの `build.gradle` で、以下を追加します。

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

         1. 最後に、ID に表示されるバーの **[!UICONTROL 今すぐ同期]**」をクリックします
   1. アプリのマニフェストの編集 FCM SDK は、必要なすべての権限と必要なレシーバー機能を自動的に追加します。 次の古い（有害な可能性がある）要素は、アプリのマニフェストから削除してください。

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

Firebase Cloud Messaging のサポートに関するよくある質問です。

**Q:MME SDK の最新バージョンにアップデートする手順はどこで確認できますか？** の手順については、Marketo開発者サイト [ こちら ](installation.md) を参照してください。

**Q:SDK の最新バージョンにアップデートするには、Android アプリケーションの更新バージョンを既存のユーザーに公開する必要がありますか？** No.

**Q:Marketo Android SDK と統合されたAndroid アプリを公開している既存の MME のお客様には、どのような影響がありますか？** 次のように、Androidの既存の GCM クライアントアプリを Firebase Cloud Messaging （FCM）に移行できます。

1. [Firebase コンソール ](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/) で、「**[!UICONTROL プロジェクトを追加]**」を選択します。
1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択し、「**[!UICONTROL Firebase を追加]**」を選択します。
1. Firebase のようこそ画面で、「**[!UICONTROL Android アプリに Firebase を追加]**」を選択します。
1. パッケージ名と SHA-1 を指定し、「**[!UICONTROL アプリを追加]**」を選択します。 新しい google-services.json ファイル
1. Firebase アプリがダウンロードされます。
1. 「**[!UICONTROL 続行]**」を選択し、Android Studio にGoogle Services プラグインを追加する手順の詳細に従います。

**Q:GCM アプリを使用した古いMarketo SDK を使用して作成されたリードをターゲットにすることはできますか？** はい。 Marketo SDK を使用して作成されたすべてのリードは、プッシュ通知の送信対象にすることができます。
