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
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 724
ht-degree: 81%

---

# Web フック

Marketo では、web フックを使用してサードパーティの web サービスと通信できます。 Web フックは、特定の URL からデータをプッシュまたは取得する GET または POST HTTP 動詞の使用をサポートします。 アプリケーション内での web フックの作成とスマートキャンペーンへの追加方法の手順について詳しくは、次の記事を参照してください。

- [Webhook の作成](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/additional-integrations/create-a-webhook)
- [Web フックの呼び出し](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/call-webhook)
- [スマートキャンペーンでの web フックの使用](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/use-a-webhook-in-a-smart-campaign)

個々の web フックには、次のプロパティがあります。

- **[!UICONTROL URL]** - Web サービスに対するリクエストの送信に使用する URL を入力します。
- **[!UICONTROL リクエストタイプ]** - HTTP メソッド。
- **[!UICONTROL ペイロードテンプレート]** - POST の本文で情報を送信する場合は、テンプレートを入力します。 XML、JSON、SOAP など、HTTP POST をサポートする任意のデータ形式を使用します。 シリアル化形式では、文字列を二重引用符で囲むことができる必要があります。 テンプレートにトークンを挿入するには、**[!UICONTROL トークンを挿入]**&#x200B;を選択します。 文字列タイプのトークンは、自動的に二重引用符で囲まれます。
- **[!UICONTROL リクエストトークンのエンコード]** - トークンの値に特殊文字（アンパサンド「&amp;」など）が含まれる場合は、リクエストの形式（JSON またはフォーム／URL）を指定します。 Web フックが web サービスと正しく通信するには、本文に正しいエンコードを選択する必要があります。
- **[!UICONTROL 応答タイプ]** - サービスから受け取る応答の形式（JSON または XML）を選択します。 レスポンスのプロパティをMarketoのリードフィールドにマッピングするには、正しいレスポンスのタイプを選択する必要があります。
- **[!UICONTROL カスタムヘッダー]** - **[!UICONTROL Webhook アクション]**/**[!UICONTROL カスタムヘッダーを設定]**&#x200B;経由でアクセスすると、このメニューでは、任意の数のカスタムキーと値のペアをHTTP ヘッダーとして追加できます。

[応答マッピング ](response-mappings.md)を使用して、web サービスの応答からリードにデータを書き戻すことができます。

## トークン

Web フック内のすべての送信フィールド（URL、テンプレート、カスタムヘッダー）には、フローステップの同じコンテキストでトークンのコンテンツを入力します。 つまり、リードトークンとシステムトークンは常に使用できますが、トリガートークン、キャンペーントークン、プログラムトークンはそれぞれのスコープ内で使用できます。 詳しくは、次のトークンに関する記事を参照してください。

- [トークンの概要](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/personalizing-landing-pages/tokens-overview)
- [システムトークンの用語集](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/using-tokens/system-tokens-glossary)
- [注目のアクションのトークン](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/marketo-sales-insight/msi-for-salesforce/features/tabs-in-the-msi-panel/interesting-moments/trigger-tokens-for-interesting-moments)

一般的なケースは、プログラムまたはキャンペーンがサードパーティのリソースに明示的にマッピングされる場合です。 ID は、プログラムレベルで `My Token` として設定でき、その後トークンとして Web フックリクエストに渡すことができます。

## カスタムヘッダー

Web フックを使用すると、送信リクエストと共に任意の数のカスタムヘッダーフィールドを送信できます。 これらは、**[!UICONTROL web フックアクション]**／**[!UICONTROL カスタムヘッダーを設定]**&#x200B;を通じて追加できます。 各ヘッダーは、シンプルなキーと値のペアとして記録されます。 この領域ではトークンを使用できます。

![カスタムヘッダー](assets/custom-headers.png)

## ヒント

- Web フックを呼び出しフローステップは、トリガーキャンペーンでのみ有効です。
- 応答マッピングを通じた更新は、web サービスが 2xx HTTP 応答コードで応答した場合にのみ発生します。 その他のタイプのコードでは、レコードは更新されません。
- Web サービスを使用して、内部または外部のサービスからカスタムデータのエンリッチメント、検証または正規化を実行できます。
- Web フックの実行時間は、使用しているサービスの応答時間に左右され、キャンペーンの実行が長時間遅延する場合があります。 サービスの実行に 50 ミリ秒しかかからないとしても、100,000 回実行すると 1.5 時間かかります。
- Marketoは、特定のサービスコールに対して最大30秒待ってから、呼び出しを終了します（タイムアウトとも呼ばれます）。
- URL フィールドに埋め込まれた文字は書き込み通りに渡されます。例：&#39;&amp;&#39;は&#39;&amp;&#39;として送信され、&#39;%26&#39;は&#39;%26&#39;として送信されます
   - 受信者サーバーで受信時に文字をパーセントでエンコードする必要がある場合は、その文字を表す文字列として明示的に渡す必要があります。
