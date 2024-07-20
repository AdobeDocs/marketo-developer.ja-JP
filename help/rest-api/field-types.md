---
title: フィールドのタイプ
feature: REST API
description: Marketoのフィールドタイプのリスト
exl-id: a0ba9e02-ed42-4be3-9cdd-a97fee9a726e
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 9%

---

# フィールドのタイプ

Marketoのフィールドタイプの説明を以下に示します。 フィールドタイプに関する追加情報は、[ こちら ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/custom-field-type-glossary) を参照してください。 フィールドタイプの制限に関する追加情報は、[ こちら ](https://nation.marketo.com/t5/knowledgebase/tkb-p/support_solutions-documents) を参照してください。

| フィールドのタイプ | 説明 | 例 |
| --- | --- | --- |
| 日時 | 日付と時刻の入力に使用します。 [W3C 形式 ](https://www.w3.org/TR/NOTE-datetime) （ISO 8601）に従います。 ベストプラクティスは、常にタイムゾーンオフセットを含めることです。 完了日+時間および分：YYYY-MM-DDThh:mm:ssTZD （TZD は「+hh:mm」または「– hh:mm」）注意：一部のアセット API では、updatedAt および createdAt に対して「Z+0000」が TZD として返されます。 | 2010-05-07T15:41:32-05:00 |
| メール | メールアドレスを受け入れる文字列フィールド | example@example.com |
| 浮動 | 実数を含み、小数点以下の桁数を使用できる数値フィールド。 | 10.4 |
| 整数 | 整数 | 10 |
| 数式 | リードレコード上に存在する他のフィールドのデータを操作することによって値が生成されるフィールド。 これらはエクスポートされず、スマートキャンペーンでは使用できません。 | この [ 記事 ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/create-and-use-a-concatenated-string-formula-field) を参照してください。 |
| パーセント | 整数で表された割合 | 30 |
| URL | 入力を URL のプロトコルを含む URL に制限するテキストフィールド。 | http://example.com/ |
| 電話 | 電話番号 | 111-111-1111 |
| テキスト領域 | 長いテキスト。 | 最大 30,000 バイトをサポートします。 標準の ASCII 文字は、1 文字あたり 1 バイトを使用します（最大 30,000 文字まで可能）。 Unicode 文字は、1 文字あたり最大 4 バイトを使用できます（以下の値を減らします）  文字数は 30,000 文字未満にする必要があります）。 |
| 文字列 | 短いテキスト （最大 255 文字） | Lorem ipsum dolor sit amet |
| Score | スコアの変更フローステップで操作できる整数フィールド | 10 |
| Boolean （以前のチェックボックス） | ユーザーが True （オン）または False （オフ）の値を選択できるようにします。 | True |
| 通貨 | Marketo配信登録用に選択されたデフォルトの通貨タイプを表す浮動小数フィールド | 10.40 |
| 日付 | 日付に使用されます。 W3C 形式に従います。 | 2010-05-07 |
| 参照 | 別のレコードへのキー（外部キー）を含む文字列フィールド。 | 企業に連絡 |
