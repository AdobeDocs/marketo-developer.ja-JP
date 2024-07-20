---
title: Marketo Mobile Extension for [!DNL Adobe Launch]
feature: Mobile Marketing
description: Marketo Mobile Extension for [!DNL Adobe Launch] overview
exl-id: 2f8691ff-0442-45a5-aeba-c91c3af5c711
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# [!DNL Adobe Launch] 用Marketo Mobile 拡張機能

[!DNL Adobe Launch] のMarketo Mobile SDK 拡張機能のインストール手順。 プッシュ通知やアプリ内メッセージを送信するには、次の手順が必要です。

## 前提条件

- [Marketo管理者でアプリケーションを追加 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID を取得）
- [!DNL Adobe Launch] ポータルに記載されている手順に従ってインストールします
- [ プッシュ通知の設定 ](push-notifications.md) （オプション）

## iOS

### Swift ブリッジング ヘッダーの設定

1. ファイル/新規/ファイルに移動し、「ヘッダーファイル」を選択します。
1. ファイルに「&lt;_ProjectName_>-Bridging-Header」という名前を付けます。
1. プロジェクト / Target / ビルドフェーズ / Swift コンパイラー/ コード生成に移動します。 Objective-Bridging ヘッダーに次のパスを追加します。

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

Swift ユーザーの場合：上記の手順でブリッジヘッダーが追加されるので、次の import 文を削除します。

`import Marketo/ALMarketo`

### iOS テストデバイス

[iOS テストデバイスの追加 ](installation.md#ios_test_devices) の手順に従います

### AppDelegate でのカスタム Url タイプの処理

手順に従う [ こちら ](installation.md#ios_test_devices)

### iOSでのプッシュ通知の設定

手順 [ こちら ](push-notifications.md) に従い、「Marketo」ではなく「ALMarketo」というクラス名を使用します

## Android

### 権限の設定

`AndroidManifest.xml` を開いて、次の権限を追加します。 アプリは、「インターネット」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリがこれらの権限を既にリクエストしている場合は、この手順をスキップします。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### ProGuard 構成（オプション）

アプリに ProGuard を使用している場合は、`proguard.cfg` ファイルに次の行を追加します。 ファイルは、プロジェクト フォルダ内にあります。 このコードを追加すると、Marketo SDK が不明化プロセスから除外されます。

```
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

### Android テストデバイス

手順に従う [ こちら ](installation.md#android_test_devices)

## Androidでのプッシュ通知の設定

手順 [ こちら ](installation.md#android_firebase_cloud_messaging_support) に従い、「Marketo」ではなく「ALMarketo」というクラス名を使用します

ユーザープロファイルの設定は手順 [ こちら ](user-profiles.md) に従い、カスタムアクションの設定は手順 [ こちら ](custom-actions.md#android_custom_action) に従います。 以下の手順では、「Marketo」ではなく「ALMarketo」というクラス名を使用します
