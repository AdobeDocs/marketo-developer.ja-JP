---
title: エラー
feature: Webhooks
description: MarketoのWebhook エラーコード、リードフィールドの更新に2xx応答が必要な理由、Webhookでエラーを検出して処理する方法を説明します。
exl-id: adce40c3-87b1-4f31-8995-eb64e8a72b55
TQID: https://experienceleague.adobe.com/N2jNA4EUMMTUFL9uJHZhOor6Tlz4-EXWciwoXrPml48
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 255
ht-degree: 72%

---

# エラー

このページには、Marketo の webhook エラー応答コードがリストされています。

1000 と 1001 は Marketo によって生成され、2xx ～ 5xx は Marketo webhook が呼び出しているシステムから返されるエラーです。

Marketoが値をフィールドにマッピングし直すには、Webhook応答コードが2xxのバリエーションである必要があります。 Webhook の目的が、応答を通じて Marketo リードレコードの値を変更することである場合、呼び出される web サービスは 2xx を返す必要があります。その他のすべての応答コードでは、リードレコードの値を更新する目的で webhook は無視されます。

| 応答コード | 説明 |
| --- | --- |
| 1000 | これは、「Webhook を呼び出し」フローアクションがバッチキャンペーン内に格納されていることを示します。 Webhook はトリガーキャンペーンからのみ起動できます。 |
| 1001 | これは、web サービスが空の応答本文を送信したことを示します。 |

## Webhook エラーのキャッチ

Webhook からのエラーは、**[!UICONTROL Webhook 呼び出し]**&#x200B;トリガーによってキャッチおよび処理されます。

![Webhook 呼び出し](assets/webhook-called.png)

* **応答** – 応答は、リクエストによって受信されたリテラル応答ペイロードです。
* **エラーの種類** – これは、HTTP ステータス メッセージのReason-Phraseに対応します。

これらは、予測可能なエラーや例外を処理し、対応するために使用できます。 統合するサービスによっては、特定のクラスのエラーを自動的に復元できる場合があり、予期しないエラーをユーザに通知するアラートを作成することもできます。
