---
title: 「ディープリンクの有効化」
feature: "Mobile Marketing"
description: 「ディープリンクを有効にする手順」
source-git-commit: cb000968c78e062b3c17be7d0faa6236c73e7358
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# ディープリンクの有効化

ディープリンクを使用すると、アプリ内の特定のコンテンツ（リソース）にユーザーをリダイレクトできます。 例えば、紫色の T シャツを広告するモバイルプッシュメッセージをユーザーがクリックした場合、そのアプリは（ホームページではなく）紫色の T シャツコンテンツに直接移動します。

プロセスは次のように動作します。

1. Marketo ユーザーは、プッシュメッセージのタップアクションにカスタム URI を配置します。
1. デバイス上でプッシュメッセージをタップすると、Marketo MME SDK は、カスタム URI でイベントをトリガーします。
1. その後、アプリはイベントを処理し、アプリ内の適切なコンテンツにユーザーをリダイレクトします。

それには、アプリのカスタム URI 構造を定義し、アプリのマニフェスト内でスキームを登録し、ディープリンクイベントを処理してアプリの適切な場所にルーティングするコードを追加する必要があります。

iOSについては、次のApple ドキュメントを参照してください。 [アプリのカスタム URL スキームの定義](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app).

Android の場合は、のGoogle ドキュメントを参照してください。 [アプリコンテンツのディープリンクの有効化](https://developer.android.com/training/app-links/deep-linking).

PhoneGap アプリの場合、ディープリンクはネイティブのiOSや Android アプリほど簡単ではありませんが、ハイブリッドアプリがiOSと Android の両方でディープリンクのカスタム URL スキームやユニバーサル/アプリリンクに対応できるようにするプラグインがあります。 考慮 [これらのプラグイン](https://cordova.apache.org/plugins/?q=deeplink).

アプリでディープリンクを有効にした場合は、Marketo ユーザーとカスタム URI を共有すると、プッシュメッセージのタップアクションにユーザーが URI を挿入できるようになります。

Marketoでは、テストデバイスを設定する際に、事前定義済みの URI 構造を使用します。 の「テストデバイス」の節を参照してください [インストールガイド](installation.md) を参照してください。

## URI 構造を定義するためのベストプラクティス

ブランドに既存のモバイルサイトがある場合、ベストプラクティスは、その URL 構造に従ってディープリンク URI も設定することです。 例えば、 `https://myappname.com/products/purple-shirt` は、該当する製品の web サイトアドレスで、次の条件を満たす必要があります `myappname://products/purple-shirt` は、アプリで使用するディープリンク URI 構造として適しています。

一般に、スキームはブランドに固有にする必要があります。 現在、スキームを世界的に一意にするための規制はありませんが、スキームが一意であることを確認する 1 つの方法は、ドメイン名を逆にすることです（例： `org.companyname`）に設定します。