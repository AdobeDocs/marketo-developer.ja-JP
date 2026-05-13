---
title: アプリ内メッセージ
feature: Mobile Marketing
description: Mobile SDKでMarketo アプリ内メッセージを設定し、カスタムイベントトリガーを設定し、タップアクティビティを追跡し、最初に開いたアプリの初期化の問題を修正します。
exl-id: 73c9f862-d154-4b37-94ce-92311aa756e8
TQID: https://experienceleague.adobe.com/RVkEUBaFb-PHd0gE9ngzYc5zOojINwSI7ic2TmcU7-8
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 357
ht-degree: 93%

---

# アプリ内メッセージ

Marketo のアプリ内メッセージ機能を使用するには、次の手順を実行する必要があります。

1. [モバイルのインストール](installation.md)の説明に従って、Marketo Mobile SDK をインストールします。
1. [モバイルアプリの追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)の説明に従って、モバイルアプリを Marketo に追加します。
1. オプションで、モバイルアプリにコードを追加して、[カスタムアクション](custom-actions.md)を取得します。

Marketo Mobile SDK をインストールし、Marketo へのアプリの追加を完了すると、ユーザがアプリを開いた際に表示されるアプリ内メッセージを送信する準備が整います。

デフォルトでは、アプリを開いたときにアプリ内メッセージがトリガーされます。 特定のページが閲覧された際や特定のボタンが押された際など、他のイベントに対してアプリ内メッセージをトリガーする場合は、コードにカスタムアクションを追加する必要があります。 このコードサンプルについて詳しくは、[カスタムアクション](custom-actions.md)の節を参照してください。

## トラブルシューティング

**アプリ内メッセージが表示されない**

Marketo は、Marketo Mobile SDK を Marketo Platform で初期化した後にのみ、アプリからのトリガーに応答します。 初期化プロセスは、アプリを初めてインストールして開いた際に発生します。 初期化は最初のアプリを開いた後に行われるので、アプリを 2 回目に開くまで「アプリを開く」イベントはトリガーされません。 アプリを閉じて再度開くと、アプリを開くことによってトリガーされたメッセージがデバイスに表示されます。

カスタムイベントは、アプリが開いた後のユーザインタラクションによってトリガーされます。 カスタムイベントは、最初のセッション中に Marketo によって認識されます。

**アプリ内タップアクティビティのトラッキング**

タップアクティビティを追跡し、タップ回数に基づいて基本表示頻度を使用するには、プライマリボタンまたはセカンダリボタンのいずれかに「閉じる」以外のアクションを割り当てます。

詳しくは、製品ドキュメントの[アプリ内メッセージ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/in-app-messages/creating-in-app-messages/create-an-in-app-message)の節を参照してください。
