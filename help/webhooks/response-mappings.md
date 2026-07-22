---
title: 応答マッピング
feature: Webhooks
description: Marketo Webhookは、JSONおよびXMLのレスポンスマッピング、SOAP API名、ドットと配列の表記法、タイプの互換性を備えたリードフィールドに属性をマッピングします。
exl-id: 95c6e33e-487c-464b-b920-3c67e248d84e
TQID: https://experienceleague.adobe.com/-OGDeKLPS1KmWGIKj6BGq5DGXoCSj5ip-dVr7-kKDro
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 374
ht-degree: 3%

---

# 応答マッピング

Marketoは、JSONまたはXMLからWebhook データを変換し、リードフィールドに値を書き込むことができます。 Marketo Field パラメーターは、常にフィールドの[SOAP API名](../rest-api/fields.md)を使用します。

各Webhookには、無制限の数の応答マッピングを設定できます。 マッピングを追加または編集するには、Webhookの応答マッピングペインで[!UICONTROL 編集]を選択します。

![応答マッピング](assets/response-mapping.png)

応答マッピングは、次の値をペアにします。

- 「応答属性」: XMLまたはJSON ドキュメント内の目的のプロパティへのパス。
- 「Marketo フィールド」: Marketoが応答属性値を書き込むリードフィールド。

Marketo レスポンスマッピングを使用してプロパティにアクセスするには、キーに英数字、ダッシュ（ – ）、アンダースコア（_）、コロン（:）、および空白のみを含める必要があります。

## JSON マッピング

ドット表記法と配列表記法でJSON プロパティにアクセスできます。 Marketo配列表記法では、文字列ではなく整数のみを使用できます。

JSON ドキュメントからデータを取得するには、応答タイプをJSONに設定します。

```json
{ "foo":"bar"}
```

`foo` プロパティは、JSON オブジェクトの最初のレベルにあります。 応答マッピングでプロパティ `name`、`foo`を使用します。

![応答マッピング](assets/json-resp.png)

次の例には、配列が含まれています。

```json
{
    "profileId" : 1234,
    "firstName" : "Jane",
    "lastName" : "Doe",
    "orders" : [
        {
            "orderId" : 5678,
            "orderDate" : "2015-01-01",
            "orderProductId" : "4982"
        },
        {
            "orderId" : 5678,
            "orderDate" : "2014-05-07",
            "orderProductId" : "4982"
        }
    ]
}
```

orders配列の最初の要素からorderDateにアクセスするには、`orders[0].orderDate`を使用します。

## XML マッピング

JSON マッピングと同様に、ドット表記法を使用して、個々のXML要素から値にアクセスします。 次の例を考えてみましょう。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<example>
    <foo>bar</foo>
</example>
```

foo プロパティにアクセスするには、`example.foo`を使用します。

`foo`にアクセスする前に、サンプル要素を参照してください。 マッピングは、プロパティ階層内のすべての要素を参照する必要があります。

配列を含むXML ドキュメントの場合、次の例を考えてみましょう。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<elementList>
    <element>
        <foo>baz</foo>
    </element>
    <element>
        <foo>bar</foo>
    </element>
    <element>
        <foo>bar</foo>
    </element>
</elementList>
```

親配列は`elementList`です。 各子要素には、`foo` プロパティが含まれています。 Marketo応答マッピングは、配列を`elementList.element`として参照し、`elementList.element[i]`を通じてその子にアクセスします。

elementListの最初の子からfooの値を取得するには、応答属性`elementList.element[0].foo`を使用します。 このマッピングは、指定されたフィールドに「baz」という値を返します。

一意の要素名と一意でない要素名の両方を含む要素内のプロパティにアクセスすると、未定義の動作が発生します。 各要素は、単一のプロパティまたは配列のいずれかである必要があります。 種類を混ぜないでください。

## タイプ

属性をフィールドにマッピングする場合は、Webhook応答タイプがターゲットフィールドと互換性があることを確認します。 例えば、Marketoは、文字列応答値をinteger型のフィールドに書き込みません。 詳しくは、[&#x200B; フィールドタイプ &#x200B;](../rest-api/field-types.md)を参照してください。
