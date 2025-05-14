---
title: 応答マッピング
feature: Webhooks
description: Marketo の応答マッピング
exl-id: 95c6e33e-487c-464b-b920-3c67e248d84e
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '461'
ht-degree: 100%

---

# 応答マッピング

Marketo は、web フックで 2 つのコンテンツタイプから受信されたデータを変換し、これらの値を JSON と XML のリードフィールドに返すことができます。Marketo フィールドパラメーターでは常に、フィールドの [SOAP API 名](../rest-api/fields.md)を使用します。各 web フックには、無制限の数の応答マッピングを設定できます。応答マッピングは、web フックの応答マッピングパネルの「[!UICONTROL 編集]」ボタンをクリックして追加および編集できます。

![応答マッピング](assets/response-mapping.png)

応答マッピングは、「応答属性」（XML または JSON ドキュメント内の目的のプロパティへのパス）と、「Marketo フィールド」（応答属性から値が書き込まれるリードフィールドを指定する）の組み合わせを通じて作成されます。

プロパティのキーは、Marketo 応答マッピングを通じてアクセスするために、英数字、ダッシュ（-）、アンダースコア（_）、コロン（:）および空白で構成されている必要があります。

## JSON マッピング

JSON プロパティには、ドット表記と配列表記を使用してアクセスします。Marketo の配列表記では、入力として文字列を使用することはできません、整数のみを使用できます。JSON ドキュメントからデータを取得するには、応答タイプを JSON に設定する必要があります。

```json
{ "foo":"bar"}
```

応答マッピング内の `foo` プロパティにアクセスするには、プロパティの `name` を使用します。このプロパティは JSON オブジェクトの最初のレベル `foo` にあるからです。Marketo では、次のようになります。

![応答マッピング](assets/json-resp.png)

配列を使った、より複雑な例を次に示します。

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

orders 配列の最初の要素から orderDate にアクセスします。このプロパティにアクセスするには、`orders[0].orderDate` を使用します

## XML マッピング

値には、XML ドキュメント内の個々の要素からアクセスできます。これには、JSON マッピングに似たドット表記が使用されます。次の簡単な例を見てみましょう。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<example>
    <foo>bar</foo>
</example>
```

ここで foo プロパティにアクセスするには、`example.foo` を使用します

`foo` にアクセスする前に、最初に example 要素を参照する必要があります。プロパティにアクセスするには、階層内のすべての要素をマッピングで参照する必要があります。配列を含む XML ドキュメントはもう少し複雑です。次の例を使用します。

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

ドキュメントは、親配列の `elementList` と、その子である、1 つのプロパティ `foo` を含む要素で構成されます。Marketo 応答マッピングの目的で、配列は `elementList.element` として参照されるので、elementList の子には `elementList.element[i]` を通じてアクセスします。elementList の最初の子から foo の値を取得するには、`elementList.element[0].foo` の応答属性を使用します。これにより、指定したフィールドに値「baz」が返されます。一意の要素名と一意でない要素名の両方を含む要素内のプロパティにアクセスしようとすると、未定義の動作が発生します。各要素は単一のプロパティまたは配列である必要があり、タイプを混在させることはできません。

## タイプ

属性をフィールドにマッピングする際、web フック応答のタイプがターゲットフィールドと互換性があることを確認する必要があります。例えば、応答の値が文字列で、選択したフィールドが integer タイプの場合、値は書き込まれません。詳しくは、[フィールドのタイプ](../rest-api/field-types.md)を参照してください。
