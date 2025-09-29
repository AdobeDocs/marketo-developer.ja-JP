---
title: Web フック
feature: Webhooks
description: サードパーティのサービスの呼び出し、ペイロードテンプレート、エンコーディング、応答マッピング、トークン、カスタムヘッダー、ヒントなどを設定するMarketo Webhook の設定方法を説明します。
exl-id: fd283c66-05a1-4aa4-8412-0d41b8d1e3c8
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 96%

---

# Web フック

Marketo では、web フックを使用してサードパーティの web サービスと通信できます。Web フックは、特定の URL からデータをプッシュまたは取得する GET または POST HTTP 動詞の使用をサポートします。アプリケーション内での web フックの作成とスマートキャンペーンへの追加方法の手順について詳しくは、次の記事を参照してください。

- [Web フックの作成](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/additional-integrations/create-a-webhook)
- [Web フックの呼び出し](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/call-webhook)
- [スマートキャンペーンでの web フックの使用](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/use-a-webhook-in-a-smart-campaign)

個々の web フックには、次のプロパティがあります。

- [!UICONTROL URL] - Web サービスに対するリクエストの送信に使用する URL を入力します。
- [!UICONTROL リクエストタイプ] - HTTP メソッド。
- [!UICONTROL ペイロードテンプレート] - POST の本文で情報を送信する場合は、テンプレートを入力します。XML、JSON、SOAP など、HTTP POST をサポートする任意のデータ形式を使用します。シリアル化形式では、文字列を二重引用符で囲むことができる必要があります。テンプレートにトークンを挿入するには、「**[!UICONTROL トークンを挿入]**」をクリックします。文字列タイプのトークンは、自動的に二重引用符で囲まれます。
- [!UICONTROL リクエストトークンのエンコード] - トークンの値に特殊文字（アンパサンド「&amp;」など）が含まれる場合は、リクエストの形式（JSON またはフォーム／URL）を指定します。Web フックが web サービスと正しく通信するには、本文に正しいエンコードを選択する必要があります。
- [!UICONTROL 応答タイプ] - サービスから受け取る応答の形式（JSON または XML）を選択します。応答のプロパティを Marketo のリードフィールドにマッピングし直すには、正しい応答タイプを選択する必要があります。
- [!UICONTROL カスタムヘッダー] - [!UICONTROL Web フックアクション]／[!UICONTROL カスタムヘッダーを設定]を通じてアクセスするこのメニューでは、任意の数のカスタムキーと値のペアを HTTP ヘッダーとして追加できます。

[応答マッピング](response-mappings.md)を使用すると、web サービス応答からリードにデータを書き戻すことができます。

## トークン

Web フック内のすべての送信フィールド（URL、テンプレート、カスタムヘッダー）には、フローステップの同じコンテキストでトークンのコンテンツを入力します。つまり、リードトークンとシステムトークンは常に使用できますが、トリガートークン、キャンペーントークン、プログラムトークンはそれぞれのスコープ内で使用できます。詳しくは、次のトークンに関する記事を参照してください。

- [トークンの概要](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/personalizing-landing-pages/tokens-overview)
- [システムトークンの用語集](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/using-tokens/system-tokens-glossary)
- [注目のアクションのトークン](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/marketo-sales-insight/msi-for-salesforce/features/tabs-in-the-msi-panel/interesting-moments/trigger-tokens-for-interesting-moments)

一般的なケースは、プログラムまたはキャンペーンがサードパーティのリソースに明示的にマッピングされる場合です。ID は、プログラムレベルで `My Token` として設定でき、その後トークンとして Web フックリクエストに渡すことができます。

## カスタムヘッダー

Web フックを使用すると、送信リクエストと共に任意の数のカスタムヘッダーフィールドを送信できます。これらは、**[!UICONTROL web フックアクション]**／**[!UICONTROL カスタムヘッダーを設定]**&#x200B;を通じて追加できます。各ヘッダーは、シンプルなキーと値のペアとして記録されます。この領域ではトークンを使用できます。

![カスタムヘッダー](assets/custom-headers.png)

## ヒント

- Web フックを呼び出しフローステップは、トリガーキャンペーンでのみ有効です。
- 応答マッピングを通じた更新は、web サービスが 2xx HTTP 応答コードで応答した場合にのみ発生します。その他のタイプのコードでは、レコードは更新されません。
- Web サービスを使用して、内部または外部のサービスからカスタムデータのエンリッチメント、検証または正規化を実行できます。
- Web フックの実行時間は、使用しているサービスの応答時間に左右され、キャンペーンの実行が長時間遅延する場合があります。サービスの実行に 50 ミリ秒しかかからないとしても、100,000 回実行すると 1.5 時間かかります。
- Marketo は、特定のサービス呼び出しを終了（タイムアウトとも呼ばれる）する前に、最大 30 秒間待機します。
- URL フィールドに埋め込まれた文字は、書き込まれたとおりに渡されます。例えば、「&amp;」は「&amp;」として送信され、「%26」は「%26」として送信されます。
   - 受信者サーバーで受信時に文字をパーセントでエンコードする必要がある場合は、その文字を表す文字列として明示的に渡す必要があります。
