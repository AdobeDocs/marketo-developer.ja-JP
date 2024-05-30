---
title: 「アプリ内メッセージ」
feature: "Mobile Marketing"
description: 「アプリ内メッセージの概要」
source-git-commit: e8bb45a7b3bee71c3d0ab6117296a75c8959d72e
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---


# アプリ内メッセージ

Marketoのアプリ内メッセージ機能を使用するには、次の手順を実行する必要があります。

1. の説明に従って、Marketo Mobile SDK をインストールします。 [モバイルのインストール](installation.md).
1. の説明に従って、Marketoにモバイル アプリを追加します [モバイルアプリを追加](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app).
1. オプションで、キャプチャするコードをモバイルアプリに追加します [カスタムアクション](custom-actions.md).

Marketo Mobile SDK をインストールし、Marketoでのアプリの追加が完了したら、ユーザーがアプリを開くと表示されるアプリ内メッセージを送信する準備が整います。

デフォルトでは、アプリを開いたときにアプリ内メッセージがトリガーされます。特定のページが表示されたとき、または特定のボタンが押されたときなど、他のイベントのアプリ内メッセージをトリガーにする場合は、コードにカスタムアクションを追加する必要があります。 参照： [カスタムアクション](custom-actions.md) こののコードサンプルについては、を参照してください。

## トラブルシューティング

**アプリ内メッセージが表示されない**

Marketoは、Marketo Mobile SDK がMarketo Platform で初期化された後にのみ、アプリからのトリガーに応答します。 初期化プロセスは、アプリを初めてインストールして開いたときに行われます。 初期化は最初のアプリを開いた後に行われるので、「アプリを開く」イベントはアプリを 2 回目に開くまでトリガーされません。 アプリを閉じて再度開くと、アプリを開くことによってトリガーされたメッセージがデバイスに表示されます。

カスタムイベントは、アプリが開かれた後のユーザーインタラクションによってトリガーされます。 カスタムイベントは、最初のセッション中にMarketoによって認識されます。

**アプリ内タップアクティビティのトラッキング**

タップのアクティビティを追跡したり、タップ数に基づいてベース表示頻度を使用したりするには、必ず「解除」以外のアクションをプライマリボタンまたはセカンダリボタンのいずれかに割り当ててください。

詳しくは、を参照してください [アプリ内メッセージ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/in-app-messages/creating-in-app-messages/create-an-in-app-message) の節を参照してください。
