---
title: Web フック
feature: Webhooks
description: MarketoのWebhookを設定して、サードパーティサービスの呼び出し、ペイロードテンプレート、エンコーディング、レスポンスマッピング、トークン、カスタムヘッダー、ヒントを設定する方法を説明します。
exl-id: fd283c66-05a1-4aa4-8412-0d41b8d1e3c8
TQID: https://experienceleague.adobe.com/r-GpAqhYPKvlDtMw5l23jeJWzlSqycP65eYJPA3m9EM
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: a7170d27-32ab-462b-a333-269abc654483id: b13bd2ad-8e65-49e5-9691-2a0d31067b35id: d1d0a9cd-295d-4976-8c39-ddae266f240eid: f82558ea-6af5-44eb-a424-5b3389abb0a3
subfeature_v2: id: ad89fb33-8541-4339-afe7-bb13d1633714id: fc9b09fe-b844-4544-887b-e420c3b82065
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 614
ht-degree: 30%

---

# Web フック

MarketoのWebhookは、サードパーティのweb サービスと通信します。 Webhookは、GETまたはPOST HTTP動詞を使用して、特定のURLにデータを送信したり、特定のURLからデータを取得したりします。

Webhookを作成してスマートキャンペーンに追加する手順については、次を参照してください。

- [Webhook の作成](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/additional-integrations/create-a-webhook)
- [Web フックの呼び出し](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/call-webhook)
- [スマートキャンペーンでの web フックの使用](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/use-a-webhook-in-a-smart-campaign)

各Webhookに次のプロパティを設定します。

- **[!UICONTROL URL]** - web サービスリクエストを送信するURL。
- **[!UICONTROL リクエストタイプ]** - HTTP メソッド。
- **[!UICONTROL ペイロードテンプレート]** - POST本文で送信される情報のテンプレート。 XML、JSON、SOAP など、HTTP POST をサポートする任意のデータ形式を使用します。 シリアル化形式では、文字列を二重引用符で囲むことができる必要があります。 トークンを挿入するには、**[!UICONTROL トークンを挿入]**&#x200B;を選択します。 Marketoでは、文字列タイプトークンが二重引用符で囲まれます。
- **[!UICONTROL 要求トークンエンコーディング]** - アンパサンドや「&amp;」などの特殊文字を含むトークン値をエンコードするために使用される、JSONまたはForm/Urlのリクエスト形式。 WebhookがWeb サービスと正しく通信するように、正しいボディエンコーディングを選択します。
- **[!UICONTROL 応答タイプ]** – 応答の形式（JSONまたはXML）。 Marketoのリードフィールドに応答プロパティをマッピングする正しいタイプを選択します。
- **[!UICONTROL カスタムヘッダー]** - キーと値のペアが&#x200B;**[!UICONTROL Webhook アクション]** > **[!UICONTROL カスタムヘッダーを設定]**&#x200B;を通じてHTTP ヘッダーとして追加されました。 任意の数のカスタムヘッダーを追加できます。

[応答マッピング ](response-mappings.md)を使用して、web サービス応答からリードにデータを書き込みます。

## トークン

URL、テンプレート、カスタムヘッダーを含むすべての送信Webhook フィールドは、フローステップと同じコンテキストでトークンコンテンツを入力します。

リードトークンとシステムトークンはいつでも利用できます。 トリガー、Campaign、およびプログラムトークンは、それぞれのスコープで使用できます。 詳しくは、次を参照してください。

- [トークンの概要](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/personalizing-landing-pages/tokens-overview)
- [システムトークンの用語集](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/using-tokens/system-tokens-glossary)
- [注目のアクションのトークン](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/marketo-sales-insight/msi-for-salesforce/features/tabs-in-the-msi-panel/interesting-moments/trigger-tokens-for-interesting-moments)

例えば、プログラムまたはCampaignがサードパーティリソースにマッピングされる場合、プログラムレベルのIDを`My Token`に設定します。 その後、IDをトークンとしてWebhook リクエストに渡します。

## カスタムヘッダー

Webhookは、送信リクエストを含む任意の数のカスタムヘッダーフィールドを送信できます。 **[!UICONTROL Webhook アクション]**/**[!UICONTROL カスタムヘッダーを設定]**&#x200B;でヘッダーを追加します。

各ヘッダーはキーと値のペアで、トークンを含めることができます。

![カスタムヘッダー](assets/custom-headers.png)

## ヒント

- トリガーキャンペーンでのみ、「Webhookを呼び出し」フローステップを使用します。
- レスポンスマッピングは、web サービスが2xx HTTP レスポンスコードを返すときにのみレコードを更新します。
- Web サービスを使用して、内部または外部のサービスからカスタムデータのエンリッチメント、検証または正規化を実行できます。
- Webhook実行時間は、サービスの応答時間に依存し、キャンペーン実行の遅延が長くなる可能性があります。 サービスの実行に50 ミリ秒しかかからない場合でも、10万回の実行には1.5時間かかります。
- Marketoは、特定のサービスコールに対して最大30秒待ってから、呼び出しを終了します（タイムアウトとも呼ばれます）。
- Marketoは、書き込まれたURL フィールドの文字を渡します。 例えば、「&amp;」は「&amp;」として送信され、「%26」は「%26」として送信されます。
  - パーセントでエンコードされた文字を受信者サーバーに送信するには、その文字を表す文字列を明示的に渡します。
