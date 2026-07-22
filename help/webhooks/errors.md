---
title: エラー
feature: Webhooks
description: MarketoのWebhook エラーコード、リードフィールドの更新に2xx応答が必要な理由、Webhookでエラーを検出して処理する方法を説明します。
exl-id: adce40c3-87b1-4f31-8995-eb64e8a72b55
TQID: https://experienceleague.adobe.com/N2jNA4EUMMTUFL9uJHZhOor6Tlz4-EXWciwoXrPml48
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 213
ht-degree: 22%

---

# エラー

このページでは、Marketo Webhookのエラー応答コードについて説明し、Webhook エラーの処理方法について説明します。

Marketoは、エラーコード 1000と1001を生成します。 Marketo Webhookによって呼び出されるシステムは、2xxから5xxの応答コードを返します。

Marketoは、web サービスが2xxの応答コードを返す場合にのみ、応答値をフィールドにマッピングします。 Webhook応答がMarketo リードレコードの値を変更することを意図している場合、他のすべての応答コードにより、フィールド更新の応答がMarketoで無視されます。

| 応答コード | 説明 |
| --- | --- |
| 1000 | これは、「Webhook を呼び出し」フローアクションがバッチキャンペーン内に格納されていることを示します。 Webhook はトリガーキャンペーンからのみ起動できます。 |
| 1001 | これは、web サービスが空の応答本文を送信したことを示します。 |

## Webhook エラーのキャッチ

**[!UICONTROL Webhook is Called]** トリガーを使用して、Webhook エラーを検出および処理します。

![Webhook 呼び出し](assets/webhook-called.png)

* **Response** - リクエストで受信したリテラル応答ペイロード。
* **エラーの種類** - HTTP ステータス メッセージの理由フレーズ。

これらの値を使用して、予測可能なエラーと例外に対応します。 統合サービスに応じて、一部のエラークラスから自動的に回復し、予期しないエラーに対するアラートを作成できます。
