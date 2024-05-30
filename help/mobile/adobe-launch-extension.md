---
title: '"Marketo Mobile 拡張機能 [!DNL Adobe Launch]“'
feature: Mobile Marketing
description: "Marketo Mobile 拡張機能 [!DNL Adobe Launch] 概要"
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---


# のMarketo Mobile 拡張機能 [!DNL Adobe Launch]

のMarketo Mobile SDK 拡張機能のインストール手順 [!DNL Adobe Launch]. プッシュ通知やアプリ内メッセージを送信するには、次の手順が必要です。

## 前提条件

- [Marketo Admin でのアプリケーションの追加](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID の取得）
- に記載されている手順に従います [!DNL Adobe Launch] インストール用ポータル
- [プッシュ通知の設定](push-notifications.md) （オプション）

## iOS

### Swift ブリッジング ヘッダーの設定

1. ファイル/新規/ファイルに移動し、「ヘッダーファイル」を選択します。
1. ファイル名に「&lt;_ProjectName_>-Bridging-Header」と表示されます。
1. プロジェクト / Target / ビルドフェーズ / Swift コンパイラー/ コード生成に移動します。 Objective-Bridging ヘッダーに次のパスを追加します。

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

Swift ユーザーの場合：上記の手順でブリッジヘッダーが追加されるので、次の import 文を削除します。

`import Marketo/ALMarketo`

### iOS テストデバイス

の手順に従う [iOS テストデバイスの追加](installation.md#ios_test_devices)

### AppDelegate でのカスタム Url タイプの処理

手順に従う [こちら](installation.md#ios_test_devices)

### iOSでのプッシュ通知の設定

手順に従う [こちら](push-notifications.md) また、「Marketo」ではなく「ALMarketo」というクラス名を使用します。

## Android

### 権限の設定

開く `AndroidManifest.xml` および次の権限を追加します。 アプリは、「インターネット」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリがこれらの権限を既にリクエストしている場合は、この手順をスキップします。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### ProGuard 構成（オプション）

アプリに ProGuard を使用している場合は、に次の行を追加します `proguard.cfg` ファイル。 ファイルは、プロジェクト フォルダ内にあります。 このコードを追加すると、Marketo SDK が不明化プロセスから除外されます。

```
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

### Android テストデバイス

手順に従う [こちら](installation.md#android_test_devices)

## Android でのプッシュ通知の設定

手順に従う [こちら](installation.md#android_firebase_cloud_messaging_support) また、「Marketo」ではなく「ALMarketo」というクラス名を使用します。

ユーザープロファイルの設定については、手順に従ってください [こちら](user-profiles.md) カスタムアクションの場合は、の手順に従います [こちら](custom-actions.md#android_custom_action). 以下の手順では、「Marketo」ではなく「ALMarketo」というクラス名を使用します
