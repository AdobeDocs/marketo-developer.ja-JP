---
title: ' [!DNL Adobe Launch] 用 Marketo Mobile 拡張機能'
feature: Mobile Marketing
description: プッシュ通知やアプリ内メッセージの設定など、iOSおよびAndroid用のAdobe LaunchにMarketo Mobile SDK拡張機能をインストールして設定します。
exl-id: 2f8691ff-0442-45a5-aeba-c91c3af5c711
TQID: https://experienceleague.adobe.com/Bk5GTnQjm6NDosl5Iw6TS-NRjH8owNRUKoE0mZ-H3pY
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 305
ht-degree: 92%

---

# [!DNL Adobe Launch] 用 Marketo Mobile 拡張機能

[!DNL Adobe Launch] での Marketo Mobile SDK 拡張機能のインストール手順です。 プッシュ通知やアプリ内メッセージを送信するには、以下の手順が必要です。

## 前提条件

- [Marketo Admin でアプリケーションを追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)（アプリケーションの秘密鍵と Munchkin ID を取得します）
- [!DNL Adobe Launch] ポータルに記載されている手順に従ってインストール
- [プッシュ通知を設定](push-notifications.md)（オプション）

## iOS

### Swift ブリッジングヘッダーの設定

1. ファイル／新規／ファイルに移動し、「ヘッダーファイル」を選択します。
1. ファイルに「&lt;_ProjectName_>-Bridging-Header」という名前を付けます。
1. プロジェクト／ターゲット／ビルドフェーズ／Swift コンパイラー／コード生成に移動します。 Objective-Bridging ヘッダーに次のパスを追加します。

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

Swift ユーザの場合：上記の手順でブリッジングヘッダーが追加されるので、次の読み込みステートメントを削除します。

`import Marketo/ALMarketo`

### iOS テストデバイス

[iOS テストデバイスの追加](installation.md#ios_test_devices)の手順に従ってください

### AppDelegate でカスタム URL タイプを処理する

[こちら](installation.md#ios_test_devices)の手順に従ってください

### iOS でのプッシュ通知の設定

[こちら](push-notifications.md)の手順に従って、&quot;Marketo&quot; の代わりに &quot;ALMarketo&quot; というクラス名を使用してください

## Android

### 権限の設定

`AndroidManifest.xml` を開き、次の権限を追加します。 アプリでは、「INTERNET」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリで既にこれらの権限をリクエストしている場合は、この手順をスキップしてください。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### ProGuard 構成（オプション）

アプリに ProGuard を使用している場合は、`proguard.cfg` ファイルに次の行を追加します。 ファイルは、プロジェクトフォルダー内にあります。 このコードを追加すると、Marketo SDK が不明化プロセスから除外されます。

```text
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

### Android テストデバイス

[こちら](installation.md#android_test_devices)の手順に従ってください

## Android でのプッシュ通知の設定

[こちら](installation.md#android_firebase_cloud_messaging_support)の手順に従い、クラス名に「Marketo」の代わりに「ALMarketo」を使用します

ユーザプロファイルを設定するには、[こちら](user-profiles.md)の手順に従ってください。カスタムアクションを設定するには、[こちら](custom-actions.md#android_custom_action)の手順に従ってください。 次の手順では、&quot;Marketo&quot; の代わりに &quot;ALMarketo&quot; というクラス名を使用します
