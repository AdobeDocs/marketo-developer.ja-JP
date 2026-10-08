---
title: アプリ内メッセージ
feature: Mobile Marketing
description: Mobile SDKでMarketo アプリ内メッセージを設定し、カスタムイベントトリガーを設定し、タップアクティビティを追跡し、最初に開いたアプリの初期化の問題を修正します。
exl-id: 73c9f862-d154-4b37-94ce-92311aa756e8
TQID: 'https://experienceleague.adobe.com/RVkEUBaFb-PHd0gE9ngzYc5zOojINwSI7ic2TmcU7-8'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: 44b89f75-c1af-5353-8094-79b278102d46
    internal-label: Mobile Marketing
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: 5620f050ba834be3f6648650b5cc7d781ea394bf
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 31%
---
# アプリ内メッセージ

Marketoのアプリ内メッセージを使用するには、次の手順を実行します。

1. [モバイルのインストール](installation.md)の説明に従って、Marketo Mobile SDK をインストールします。
1. [モバイルアプリの追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)の説明に従って、モバイルアプリを Marketo に追加します。
1. オプション：モバイルアプリにコードを追加して、[ カスタムアクション ](custom-actions.md)をキャプチャします。

Marketo Mobile SDKをインストールしてアプリをMarketoに追加すると、ユーザーがアプリを開いたときに表示されるアプリ内メッセージを送信できます。

デフォルトでは、アプリが開いたときにアプリ内メッセージがトリガーされます。 特定のページの表示や特定のボタンのトリガーなど、別のイベントのメッセージを選択するには、コードにカスタムアクションを追加します。 コードサンプルについては、[ カスタムアクション ](custom-actions.md)を参照してください。

## トラブルシューティング

**アプリ内メッセージが表示されない**

Marketoは、Marketo PlatformでMarketo Mobile SDKが初期化された後にのみアプリトリガーに応答します。 初期化は、アプリを初めてインストールして開いたときに発生します。

初期化は最初のアプリを開いた後に行われるため、「アプリを開く」イベントは、アプリを2回開くまでトリガーされません。 アプリを閉じて再度開きます。 App Openによってトリガーされるメッセージがデバイスに表示されます。

カスタムイベントは、アプリが開いた後のユーザーインタラクションによってトリガーされます。 カスタムイベントは、最初のセッション中に Marketo によって認識されます。

**アプリ内タップアクティビティのトラッキング**

タップアクティビティを追跡し、タップ数に基づいて表示頻度を設定するには、「却下」以外のアクションをプライマリボタンまたはセカンダリボタンに割り当てます。

詳しくは、製品ドキュメントの[ アプリ内メッセージ ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/in-app-messages/creating-in-app-messages/create-an-in-app-message)を参照してください。
