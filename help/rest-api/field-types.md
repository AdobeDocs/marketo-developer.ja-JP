---
title: フィールドのタイプ
feature: REST API
description: ISO 8601の日時、テキスト領域の制限、通貨、ブール値などの定義、例、およびフォーマットを含むMarketoのフィールドタイプの包括的なリスト。
exl-id: a0ba9e02-ed42-4be3-9cdd-a97fee9a726e
TQID: https://experienceleague.adobe.com/Q-L1NCCS1caYip-niSrBAkp6k37ErzmsLCFvn7fRJW0
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
subfeature_v2:
  - id: ad89fb33-8541-4339-afe7-bb13d1633714
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 371
ht-degree: 76%

---

# フィールドのタイプ

次の表に、Marketoで使用可能なフィールドタイプを示します。 詳しくは、[&#x200B; カスタムフィールドタイプ用語集](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/field-management/custom-field-type-glossary)および[&#x200B; フィールドタイプ別のMarketo フィールドの制限](https://nation.marketo.com/t5/knowledgebase/marketo-field-limits-by-field-type/ta-p/251613)を参照してください。

| フィールドのタイプ | 説明 | 例 |
| --- | --- | --- |
| 日時 | 日付と時刻の入力に使用します。 [W3C 形式](https://www.w3.org/TR/NOTE-datetime)（ISO 8601）に従います。 ベストプラクティスは、タイムゾーンオフセットを含めることです。 完了日と時間と分：YYYY-MM-DDThh:mm:ssTZD （TZDが「+hh:mm」または「 – hh:mm」の場合）注意：一部のAsset APIでは、`updatedAt`および`createdAt`の場合、「Z+0000」がTZDとして返されます。 | 2010-05-07T15:41:32-05:00 |
| メール | メールアドレスを受け入れる文字列フィールド | <example@example.com> |
| 浮動 | 実数を含め小数点以下の桁を使用できる数値フィールド。 | 10.4 |
| 整数 | 整数 | 10 |
| 数式 | リードレコードに存在する他のフィールドのデータを操作することによって値が生成されるフィールド。 これらは書き出されず、スマートキャンペーンでは使用できません。 | この[記事](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/field-management/create-and-use-a-concatenated-string-formula-field)を参照してください |
| パーセント | 整数で表されるパーセント | 30 |
| URL | URL のプロトコルを含む、入力を URL に制限するテキストフィールド。 | <http://example.com/> |
| 電話 | 電話番号 | 111-111-1111 |
| テキストエリア | 長いテキスト。 | 最大 30,000 バイトをサポートします。 標準 ASCII 文字は、1 文字あたり 1 バイトを使用します（最大 30,000 文字まで可能）。 Unicode 文字は、1 文字あたり最大 4 バイトを使用できます（使用可能な文字数は 30,000 文字未満に制限されます）。 |
| 文字列 | 短いテキスト | 最大255文字のテキスト |
| スコア | 「スコアを変更」フローステップで操作できる整数フィールド | 10 |
| ブール値（以前のチェックボックス） | ユーザが True（オン）または False（オフ）の値を選択できます。 | True |
| 通貨 | Marketo サブスクリプションで選択されたデフォルトの通貨タイプを表す浮動小数フィールド | 10.40 |
| 日付 | 日付に使用されます。 W3C 形式に従います。 | 2010-05-07 |
| 参照 | 別のレコードへのキー（外部キー）を含む文字列フィールド。 | 会社連絡先 |
