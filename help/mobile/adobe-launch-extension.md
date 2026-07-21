---
title: ' [!DNL Adobe Launch] 用 Marketo Mobile 拡張機能'
feature: Mobile Marketing
description: プッシュ通知やアプリ内メッセージの設定など、iOSおよびAndroid用のAdobe LaunchにMarketo Mobile SDK拡張機能をインストールして設定します。
exl-id: 2f8691ff-0442-45a5-aeba-c91c3af5c711
TQID: https://experienceleague.adobe.com/Bk5GTnQjm6NDosl5Iw6TS-NRjH8owNRUKoE0mZ-H3pY
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 303
ht-degree: 30%

---

# [!DNL Adobe Launch] 用 Marketo Mobile 拡張機能

[!DNL Adobe Launch]にMarketo Mobile SDK拡張機能をインストールして、プッシュ通知、アプリ内メッセージ、またはその両方を送信します。

## 前提条件

- [Marketo Admin](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)でアプリケーションを追加し、アプリケーションの秘密鍵とMunchkin IDを取得します。
- [!DNL Adobe Launch] ポータルのインストール手順に従います。
- オプション：[ プッシュ通知を設定](push-notifications.md)。

## iOS

### Swift ブリッジングヘッダーの設定

1. ファイル/新規/ファイルに移動し、「ヘッダーファイル」を選択します。
1. ファイルに「&lt;_ProjectName_>-Bridging-Header」という名前を付けます。
1. プロジェクト／ターゲット／ビルドフェーズ／Swift コンパイラー／コード生成に移動します。
1. Objective-Bridging ヘッダーに次のパスを追加します。

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

Swiftの場合、前の手順でブリッジングヘッダーが追加されるので、次の読み込みステートメントを削除します。

`import Marketo/ALMarketo`

### iOS テストデバイス

[iOS テストデバイスの追加](installation.md#ios_test_devices)の手順に従います。

### AppDelegate でカスタム URL タイプを処理する

[ カスタム URLの手順](installation.md#ios_test_devices)に従います。

### iOS でのプッシュ通知の設定

[ プッシュ通知の手順](push-notifications.md)に従います。 「Marketo」の代わりに「ALMarketo」というクラス名を使用します。

## Android

### 権限の設定

`AndroidManifest.xml`を開き、次の権限を追加します。 アプリでは、「INTERNET」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリが既にリクエストしている場合は、この手順をスキップします。

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### ProGuard 構成（オプション）

アプリでProGuardを使用している場合は、プロジェクトフォルダーの`proguard.cfg` ファイルに次の行を追加します。 この設定により、Marketo SDKは難読化から除外されます。

```text
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

### Android テストデバイス

[Android Test Devices](installation.md#android_test_devices)の手順に従います。

## Android でのプッシュ通知の設定

[Android Firebase Cloud Messagingの手順](installation.md#android_firebase_cloud_messaging_support)に従います。 「Marketo」の代わりに「ALMarketo」というクラス名を使用します。

ユーザープロファイルを設定するには、[ ユーザープロファイルの手順](user-profiles.md)に従います。 カスタムアクションを設定するには、[ カスタムアクションの手順](custom-actions.md#android_custom_action)に従います。 両方の手順で、「Marketo」の代わりに「ALMarketo」というクラス名を使用します。
