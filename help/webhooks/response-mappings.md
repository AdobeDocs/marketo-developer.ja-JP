---
title: 「レスポンス・マッピング」
feature: Webhooks
description: 「Marketoのレスポンス・マッピング」
source-git-commit: bcc0c0c8e8209cf9fb962a85c8e7da354d95a8fe
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---


# 応答マッピング

Marketoは、Webhook で受信した 2 つのコンテンツタイプのデータを変換し、これらの値をリードフィールド（JSON および XML）に返すことができます。 Marketo フィールドのパラメーターでは、常に以下を使用します [SOAP API 名](../rest-api/fields.md) フィールドの。 各 Webhook は、応答マッピングの数に制限はありません。応答マッピングは、をクリックすることで追加および編集されます [!UICONTROL 編集] webhook の応答マッピング パネルのボタン：

![Response-Mapping](assets/response-mapping.png)

レスポンスマッピングは、「Response 属性」、XML または JSON ドキュメント内の目的のプロパティへのパス、および「Marketo フィールド」のペアで作成されます。このペアは、Response 属性から値が書き込まれたリードフィールドを指定します。

Marketoのレスポンスマッピングを使用してアクセスするには、プロパティのキーが、英数字、ダッシュ（–）、アンダースコア（_）、コロン（:）、空白で構成されている必要があります。

## JSON マッピング

JSON プロパティには、ドット表記と配列表記でアクセスします。 Marketoの配列表記は、文字列を入力として受け入れず、整数のみを受け入れます。 JSON ドキュメントからデータを取得するには、応答タイプを JSON に設定する必要があります。

```json
{ "foo":"bar"}
```

にアクセスするには `foo` 応答マッピングにおけるプロパティの使用： `name` JSON オブジェクトの最初のレベルにあるので、プロパティの `foo`. Marketoでは、次のようになります。

![応答マッピング](assets/json-resp.png)

配列を使用した、より複雑な例を次に示します。

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

orders 配列の最初の要素から orderDate にアクセスします。 このプロパティにアクセスするには、次を使用します。 `orders[0].orderDate`

## XML マッピング

値は、XML ドキュメントの個々の要素からアクセスできます。 これは、JSON マッピングと同様のドット表記を使用します。 次の簡単な例を見てみましょう。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<example>
    <foo>bar</foo>
</example>
```

ここで foo プロパティにアクセスするには、以下を使用します。 `example.foo`

にアクセスする前に、まずサンプル要素を参照する必要があります `foo`. プロパティにアクセスするには、階層内のすべての要素がマッピングで参照されている必要があります。 配列を含む XML ドキュメントはもう少し複雑です。 次の例を使用します。

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

ドキュメントは親配列で構成されます `elementList`子を持つ、次の 1 つのプロパティを含む要素： `foo`. Marketoのレスポンスマッピング用に、配列はとして参照されます `elementList.element`そのため、elementList の子には、経由でアクセスできます `elementList.element[i]`. elementList の最初の子から foo の値を取得するには、次の応答属性を使用します。 `elementList.element[0].foo` これにより、指定されたフィールドに「baz」という値が返されます。 一意の要素名と一意でない要素名の両方を含む要素内のプロパティにアクセスしようとすると、未定義の動作が発生します。 各要素は、単一のプロパティまたは配列である必要があります。型を混在させることはできません。

## タイプ

属性をフィールドにマッピングする場合は、webhook 応答のタイプがターゲットフィールドと互換性があることを確認する必要があります。 例えば、応答の値が文字列で、選択したフィールドが整数型の場合、値は書き込まれません。 詳細を読む [フィールドタイプ](../rest-api/field-types.md).
