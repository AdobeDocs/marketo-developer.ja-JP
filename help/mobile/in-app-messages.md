---
title: アプリ内メッセージ
feature: Mobile Marketing
description: アプリ内メッセージの概要
exl-id: 73c9f862-d154-4b37-94ce-92311aa756e8
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 5%

---

# アプリ内メッセージ

Marketoのアプリ内メッセージ機能を使用するには、次の手順を実行する必要があります。

1. [ モバイルのインストール ](installation.md) の説明に従って、Marketo Mobile SDK をインストールします。
1. [ モバイルアプリの追加 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) の説明に従って、モバイルアプリをMarketoに追加します。
1. オプションで、キャプチャするコードをモバイルアプリに追加します [ カスタムアクション ](custom-actions.md)。

Marketo Mobile SDK をインストールし、Marketoでのアプリの追加が完了したら、ユーザーがアプリを開くと表示されるアプリ内メッセージを送信する準備が整います。

デフォルトでは、アプリを開いたときにアプリ内メッセージがトリガーされます。特定のページが表示されたとき、または特定のボタンが押されたときなど、他のイベントのアプリ内メッセージをトリガーにする場合は、コードにカスタムアクションを追加する必要があります。 このコードサンプルについては、[ カスタムアクション ](custom-actions.md) の節を参照してください。

## トラブルシューティング

**アプリ内メッセージが表示されません**

Marketoは、Marketo Mobile SDK がMarketo Platform で初期化された後にのみ、アプリからのトリガーに応答します。 初期化プロセスは、アプリを初めてインストールして開いたときに行われます。 初期化は最初のアプリを開いた後に行われるので、「アプリを開く」イベントはアプリを 2 回目に開くまでトリガーされません。 アプリを閉じて再度開くと、アプリを開くことによってトリガーされたメッセージがデバイスに表示されます。

カスタムイベントは、アプリが開かれた後のユーザーインタラクションによってトリガーされます。 カスタムイベントは、最初のセッション中にMarketoによって認識されます。

**アプリ内タップアクティビティのトラッキング**

タップのアクティビティを追跡したり、タップ数に基づいてベース表示頻度を使用したりするには、必ず「解除」以外のアクションをプライマリボタンまたはセカンダリボタンのいずれかに割り当ててください。

詳しくは、製品ドキュメントの [ アプリ内メッセージ ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/in-app-messages/creating-in-app-messages/create-an-in-app-message) の節を参照してください。
