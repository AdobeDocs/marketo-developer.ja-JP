---
title: 「[!DNLAdobe Launch] 拡張機能のインストール」
feature: "Mobile Marketing"
description: “[!DNL Adobe Launch] 拡張機能のインストールの概要」
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# [!DNL Adobe Launch] 拡張機能のインストール

のインストール手順 [!DNL Adobe Launch] Marketo拡張機能。 プッシュ通知やアプリ内メッセージを送信するには、次の手順が必要です。

## 前提条件

1. [Marketo Admin でのアプリケーションの追加](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID の取得）
1. [のプロパティを設定します [!DNL Adobe Launch] ポータル](https://experience.adobe.com/#/@amc/data-collection/home)
1. のプロパティのアプリケーション秘密鍵と Munchkin ID を設定します。 [!DNL Adobe Launch] ポータル
1. [プッシュ通知の設定](push-notifications.md) （オプション）

## iOSにMarketo拡張機能をインストールする方法

### Swift ブリッジング ヘッダーの設定

1. ファイル/新規/ファイルに移動し、「ヘッダーファイル」を選択します。

1. ファイル名に「&lt;_ProjectName_>-Bridging-Header」と表示されます。

1. プロジェクト / Target / ビルド設定/ Swift コンパイラー/ コード生成に移動します。 「Objective-Bridging」ヘッダーに次のパスを追加します。

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

1. を選択 [!UICONTROL プロジェクト] > [!UICONTROL ターゲット] > [!UICONTROL 情報] > URL タイプ。
1. 識別子を追加：${PRODUCT_NAME}
1. URL スキームの設定：mkto-&lt;s_ecret key_=&quot;&quot;>
1. 次を含める `application:openURL:sourceApplication:annotation:` 対象： `AppDelegate.m file` （Objective-C）

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

## Android にMarketo SDK をインストールする方法

### Android 拡張機能のセットアップ

の手順に従います。 [!DNL Adobe Launch] ポータル

### 権限の設定

開く `AndroidManifest.xml` および次の権限を追加します。 アプリは、「インターネット」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリがこれらの権限を既にリクエストしている場合は、この手順をスキップします。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

## 拡張機能の初期化

ProGuard 構成（オプション）

アプリに ProGuard を使用している場合は、に次の行を追加します `proguard.cfg` ファイル。 ファイルは以下の場所にあります。 `project` フォルダー。 このコードを追加すると、Marketo SDK が不明化プロセスから除外されます。

```
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

## Android テストデバイス

「MarketoActivity」をに追加 `AndroidManifest.xml` アプリケーションタグの内部。

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
      1. が含まれる [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)を選択 [!UICONTROL プロジェクトを追加].
      1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択して、を選択します。 [!UICONTROL Firebase の追加].
      1. Firebase のスタートアップスクリーンで、「Android アプリに Firebase を追加」を選択します。
      1. パッケージ名と SHA-1 を指定し、を選択します。 [!UICONTROL アプリを追加]. 新品 `google-services.json` firebase アプリのファイルがダウンロードされます。
      1. を選択 [!UICONTROL 続行] Android Studio でGoogle サービスプラグインを追加する手順の詳細に従います。

   1. プロジェクトの概要の「プロジェクト設定」に移動する
      1. 「一般」タブをクリックします。 をダウンロード `google-services.json` ファイル。
      1. 「Cloud Messaging」タブをクリックします。 「サーバーキー」と「送信者 ID」をコピーします。 これらの「サーバーキー」と「送信者 ID」をMarketoに指定します。
   1. Android アプリでの FCM の変更
      1. Android Studio のプロジェクトビューに切り替えて、プロジェクトのルートディレクトリを表示します
         1. ダウンロードしたを移動 `google-services.json` ファイルを Android アプリモジュールのルートディレクトリに追加します
         1. プロジェクトレベルで `build.gradle` 以下を追加します。

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

         1. 最後に、「[!UICONTROL 今すぐ同期]」と表示されます。
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

**Q:MME SDK の最新バージョンにアップデートする方法を教えてください。** 手順については、Marketo開発者サイトを参照してください [こちら](installation.md).

**Q:SDK の最新バージョンに更新するには、Android アプリケーションの更新バージョンを既存のユーザーに公開する必要がありますか？** いいえ。

**Q:Marketo Android SDK と統合された Android アプリを公開している既存の MME のお客様には、どのような影響がありますか？** Android 上の既存の GCM クライアントアプリを Firebase Cloud Messaging （FCM）に移行するには、次の手順を実行します。

1. が含まれる [Firebase コンソール](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)を選択 [!UICONTROL プロジェクトを追加].
1. 既存のGoogle Cloud プロジェクトのリストから GCM プロジェクトを選択して、を選択します。 **[!UICONTROL Firebase の追加]**.
1. Firebase のようこそ画面で、次を選択します。 **[!UICONTROL Android アプリへの Firebase の追加]**.
1. パッケージ名と SHA-1 を指定し、を選択します。 **[!UICONTROL アプリを追加]**. 新しい google-services.json ファイル
1. Firebase アプリがダウンロードされます。
1. を選択 **[!UICONTROL 続行]** Android Studio でGoogle サービスプラグインを追加する手順の詳細に従います。

**Q:GCM アプリを使用した古いMarketo SDK を使用して作成されたリードをターゲットにすることはできますか？** はい。 Marketo SDK を使用して作成されたすべてのリードは、プッシュ通知の送信対象にすることができます。
