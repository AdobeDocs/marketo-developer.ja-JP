---
title: ディープリンクの有効化
feature: Mobile Marketing
description: IOS、Android、PhoneGapのガイダンスとベストプラクティスを使用して、カスタム URI スキームを使用したMarketo プッシュメッセージのアプリでディープリンクを有効にする方法について説明します。
exl-id: c3647416-d81d-4f15-b660-bcb3e54cb9bc
TQID: https://experienceleague.adobe.com/UswOvHXGlfTrTUqr4Gsf3j2Z7Xpv2FF2luXeygT4qE0
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 363
ht-degree: 28%

---

# ディープリンクの有効化

ディープリンクを利用すれば、アプリ内の特定のコンテンツにオーディエンスを誘導できます。 例えば、オーディエンスが紫のT シャツを広告するモバイルプッシュメッセージを選択すると、ホームページの代わりに紫のT シャツコンテンツをアプリで開くことができます。

プロセスは次のように機能します。

1. Marketo ユーザーは、プッシュメッセージのタップアクションにカスタム URIを配置します。
1. ユーザがデバイス上でプッシュメッセージをタップすると、Marketo MME SDK はカスタム URI を使用してイベントをトリガーします。
1. アプリがイベントを処理し、そのユーザーを対応するコンテンツに誘導します。

このプロセスを有効にするには：

1. アプリのカスタム URI構造を定義します。
1. アプリマニフェストにスキームを登録します。
1. ディープリンクイベントを処理し、ユーザーを対応するコンテンツにルーティングするコードを追加します。

IOSについては、[&#x200B; アプリのカスタム URL スキームの定義](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app)に関するAppleのドキュメントを参照してください。

Androidについては、[&#x200B; アプリ コンテンツのディープリンクの有効化](https://developer.android.com/training/app-links/deep-linking)に関するGoogleのドキュメントを参照してください。

PhoneGap アプリの場合は、プラグインを使用して、iOSとAndroidのカスタム URL スキームとユニバーサル/アプリリンクに対応するハイブリッド アプリを有効にします。 使用可能な[&#x200B; ディープリンクプラグイン &#x200B;](https://cordova.apache.org/plugins/?q=deeplink)を参照してください。

アプリでディープリンクを有効にした際は、カスタム URI を Marketo ユーザと共有して、プッシュメッセージのタップアクションに挿入できます。

Marketo では、テストデバイスを設定する際に、事前定義済みの URI 構造を使用します。 詳しくは、[&#x200B; インストールガイド &#x200B;](installation.md)の「デバイスのテスト」を参照してください。

## URI 構造を定義するベストプラクティス

ブランドにモバイルサイトがある場合は、ディープリンク URIを定義するときに、そのURL構造に従います。 例えば、製品URLが`https://myappname.com/products/purple-shirt`の場合、対応するディープリンク URIとして`myappname://products/purple-shirt`を使用します。

自社ブランドに固有のスキームを使用します。 スキームをグローバルに一意にする必要はありませんが、`org.companyname`のようにドメイン名を逆転させることで、一意のスキームを作成できます。
