---
title: アプリ内メッセージ
feature: Mobile Marketing
description: Marketoと Mobile SDKの連携によるアプリ内メッセージの設定、カスタムイベントトリガーの設定、タップアクティビティの追跡、アプリが最初に開く際の初期化の問題の修正を行います。
exl-id: 73c9f862-d154-4b37-94ce-92311aa756e8
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 92%

---

# アプリ内メッセージ

Marketo のアプリ内メッセージ機能を使用するには、次の手順を実行する必要があります。

1. [モバイルのインストール](installation.md)の説明に従って、Marketo Mobile SDK をインストールします。
1. [モバイルアプリの追加](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)の説明に従って、モバイルアプリを Marketo に追加します。
1. オプションで、モバイルアプリにコードを追加して、[カスタムアクション](custom-actions.md)を取得します。

Marketo Mobile SDK をインストールし、Marketo へのアプリの追加を完了すると、ユーザがアプリを開いた際に表示されるアプリ内メッセージを送信する準備が整います。

デフォルトでは、アプリを開いたときにアプリ内メッセージがトリガーされます。特定のページが閲覧された際や特定のボタンが押された際など、他のイベントに対してアプリ内メッセージをトリガーする場合は、コードにカスタムアクションを追加する必要があります。このコードサンプルについて詳しくは、[カスタムアクション](custom-actions.md)の節を参照してください。

## トラブルシューティング

**アプリ内メッセージが表示されない**

Marketo は、Marketo Mobile SDK を Marketo Platform で初期化した後にのみ、アプリからのトリガーに応答します。初期化プロセスは、アプリを初めてインストールして開いた際に発生します。初期化は最初のアプリを開いた後に行われるので、アプリを 2 回目に開くまで「アプリを開く」イベントはトリガーされません。アプリを閉じて再度開くと、アプリを開くことによってトリガーされたメッセージがデバイスに表示されます。

カスタムイベントは、アプリが開いた後のユーザインタラクションによってトリガーされます。カスタムイベントは、最初のセッション中に Marketo によって認識されます。

**アプリ内タップアクティビティのトラッキング**

タップアクティビティを追跡し、タップ回数に基づいて基本表示頻度を使用するには、プライマリボタンまたはセカンダリボタンのいずれかに「閉じる」以外のアクションを割り当てます。

詳しくは、製品ドキュメントの[アプリ内メッセージ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/in-app-messages/creating-in-app-messages/create-an-in-app-message)の節を参照してください。
