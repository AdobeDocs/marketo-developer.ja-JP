---
title: ディープリンクの有効化
feature: Mobile Marketing
description: カスタム URI スキームを使用し、iOS、Android、PhoneGap のガイダンスとベストプラクティスに基づいて、Marketo プッシュメッセージに対してアプリでディープリンクを有効にする方法を説明します。
exl-id: c3647416-d81d-4f15-b660-bcb3e54cb9bc
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 93%

---

# ディープリンクの有効化

ディープリンクを使用すると、アプリ内の特定のコンテンツ（リソース）に人物をリダイレクトできます。例えば、ユーザが紫色の T シャツを広告するモバイルプッシュメッセージをクリックすると、アプリを開いて（ホームページではなく）紫色の T シャツのコンテンツを直接表示できます。

プロセスは次のように機能します。

1. Marketo ユーザは、プッシュメッセージのタップアクションにカスタム URI を配置します。
1. ユーザがデバイス上でプッシュメッセージをタップすると、Marketo MME SDK はカスタム URI を使用してイベントをトリガーします。
1. その後、アプリはイベントを処理し、ユーザをアプリ内の適切なコンテンツにリダイレクトします。

これには、アプリのカスタム URI 構造を定義し、アプリのマニフェスト内にスキームを登録し、ディープリンクイベントを処理してアプリ内の適切な場所にルーティングするコードを追加する必要があります。

iOS の場合は、[アプリのカスタム URL スキームの定義](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app)に関する Apple ドキュメントを参照してください。

Android の場合は、[アプリコンテンツのディープリンクの有効化](https://developer.android.com/training/app-links/deep-linking)に関する Google ドキュメントを参照してください。

PhoneGap アプリの場合、ディープリンクはネイティブ iOS または Android アプリほど簡単ではありませんが、ハイブリッドアプリが iOS と Android の両方でディープリンクのカスタム URL スキームとユニバーサル／アプリリンクに応答できるようにするプラグインがあります。[これらのプラグイン](https://cordova.apache.org/plugins/?q=deeplink)を考慮してください。

アプリでディープリンクを有効にした際は、カスタム URI を Marketo ユーザと共有して、プッシュメッセージのタップアクションに挿入できます。

Marketo では、テストデバイスを設定する際に、事前定義済みの URI 構造を使用します。詳しくは、インストールガイドの[テストデバイス](installation.md)の節を参照してください。

## URI 構造を定義するベストプラクティス

ブランドに既存のモバイルサイトがある場合は、ディープリンク URI に対してもこの URL 構造に従うのがベストプラクティスです。例えば、`https://myappname.com/products/purple-shirt` が対象製品の web サイトアドレスである場合、`myappname://products/purple-shirt` はアプリで使用するのに適したディープリンク URI 構造になります。

一般に、スキームはブランドに一意である必要があります。現在、スキームを世界中で一意にする規制はありませんが、スキームが一意であることを確保する 1 つの方法は、ドメイン名を逆にすることです（例：`org.companyname`）。
