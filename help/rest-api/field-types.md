---
title: フィールドのタイプ
feature: REST API
description: Marketo フィールドタイプのリスト
exl-id: a0ba9e02-ed42-4be3-9cdd-a97fee9a726e
source-git-commit: fc9b9037986a35036dbd909339f59bd33aa67e71
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 94%

---

# フィールドのタイプ

Marketo のフィールドタイプの説明を以下に示します。フィールドタイプに関する追加情報について詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/field-management/custom-field-type-glossary)を参照してください。フィールドタイプの制限に関する追加情報について詳しくは、[こちら](https://nation.marketo.com/t5/knowledgebase/marketo-field-limits-by-field-type/ta-p/251613)を参照してください。

| フィールドのタイプ | 説明 | 例 |
| --- | --- | --- |
| 日時 | 日付と時刻の入力に使用します。[W3C 形式](https://www.w3.org/TR/NOTE-datetime)（ISO 8601）に従います。ベストプラクティスは、タイムゾーンオフセットを含めることです。 完全な日付と時間と分：YYYY-MM-DDThh:mm:ssTZD（TZD は「+hh:mm」または「-hh:mm」）メモ：一部の Asset API では、`updatedAt` および `createdAt` の TZD として「Z+0000」を返します。 | 2010-05-07T15:41:32-05:00 |
| メール | メールアドレスを受け入れる文字列フィールド | example@example.com |
| 浮動 | 実数を含め小数点以下の桁を使用できる数値フィールド。 | 10.4 |
| 整数 | 整数 | 10 |
| 数式 | リードレコードに存在する他のフィールドのデータを操作することによって値が生成されるフィールド。これらは書き出されず、スマートキャンペーンでは使用できません。 | この[記事](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/field-management/create-and-use-a-concatenated-string-formula-field)を参照してください |
| パーセント | 整数で表されるパーセント | 30 |
| URL | URL のプロトコルを含む、入力を URL に制限するテキストフィールド。 | http://example.com/ |
| 電話 | 電話番号 | 111-111-1111 |
| テキストエリア | 長いテキスト。 | 最大 30,000 バイトをサポートします。標準 ASCII 文字は、1 文字あたり 1 バイトを使用します（最大 30,000 文字まで可能）。Unicode 文字は、1 文字あたり最大 4 バイトを使用できます（使用可能な文字数は 30,000 文字未満に制限されます）。 |
| 文字列 | 短いテキスト | 255 文字までのテキスト |
| スコア | 「スコアを変更」フローステップで操作できる整数フィールド | 10 |
| ブール値（以前のチェックボックス） | ユーザが True（オン）または False（オフ）の値を選択できます。 | True |
| 通貨 | Marketo サブスクリプションで選択されたデフォルトの通貨タイプを表す浮動小数フィールド | 10.40 |
| 日付 | 日付に使用されます。W3C 形式に従います。 | 2010-05-07 |
| 参照 | 別のレコードへのキー（外部キー）を含む文字列フィールド。 | 会社連絡先 |
