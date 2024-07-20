---
title: ディープリンクの有効化
feature: Mobile Marketing
description: ディープリンクを有効にする手順
exl-id: c3647416-d81d-4f15-b660-bcb3e54cb9bc
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
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

iOSについては、「アプリのカスタム URL スキームの定義 [ に関するApple ドキュメントを参照してください ](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app)。

Androidについては、Googleのドキュメント [ アプリコンテンツのディープリンクの有効化 ](https://developer.android.com/training/app-links/deep-linking) を参照してください。

PhoneGap アプリの場合、ディープリンクはネイティブのiOSやAndroid アプリほど簡単ではありませんが、ハイブリッドアプリがiOSとAndroidの両方でディープリンクカスタム URL スキームやユニバーサル/アプリリンクに対応できるようにするプラグインがあります。 [ これらのプラグイン ](https://cordova.apache.org/plugins/?q=deeplink) を検討してください。

アプリでディープリンクを有効にした場合は、Marketo ユーザーとカスタム URI を共有すると、プッシュメッセージのタップアクションにユーザーが URI を挿入できるようになります。

Marketoでは、テストデバイスを設定する際に、事前定義済みの URI 構造を使用します。 詳細については、「インストール ガイド [ の「デバイスのテスト」セクションを参照し ](installation.md) ください。

## URI 構造を定義するためのベストプラクティス

ブランドに既存のモバイルサイトがある場合、ベストプラクティスは、その URL 構造に従ってディープリンク URI も設定することです。 例えば、問題の製品の web サイトアドレスが `https://myappname.com/products/purple-shirt` の場合、アプリ `myappname://products/purple-shirt` 使用するディープリンク URI 構造として適しています。

一般に、スキームはブランドに固有にする必要があります。 現在、スキームを世界的に一意にするための規制はありませんが、スキームが一意であることを確認する 1 つの方法は、ドメイン名を逆にすることです（例：`org.companyname`）。
