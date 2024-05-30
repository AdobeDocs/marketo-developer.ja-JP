---
title: 「フィールドタイプ」
feature: REST API
description: 「Marketo フィールドタイプのリスト」
source-git-commit: fd75f60adbc4d38e4743db5447d15cf90f025e22
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 9%

---


# フィールドのタイプ

Marketoのフィールドタイプの説明を以下に示します。 フィールドタイプに関する追加情報は、こちらを参照してください [こちら](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/custom-field-type-glossary). フィールドタイプの上限に関する追加情報は、こちらを参照してください [こちら](https://nation.marketo.com/t5/knowledgebase/tkb-p/support_solutions-documents).

| フィールドのタイプ | 説明 | 例 |
| --- | --- | --- |
| 日時 | 日付と時刻の入力に使用します。 フォロー [W3C 形式](https://www.w3.org/TR/NOTE-datetime) （ISO 8601）。 ベストプラクティスは、常にタイムゾーンオフセットを含めることです。 完了日+時間および分：YYYY-MM-DDThh:mm:TZD が「+hh:mm」または「– hh:mm」である場合の ssTZD 注：一部の Asset API は、updatedAt と createdAt に対して「Z+0000」を TZD として返します。 | 2010-05-07T15:41:32-05:00 |
| メール | メールアドレスを受け入れる文字列フィールド | example@example.com |
| 浮動 | 実数を含み、小数点以下の桁数を使用できる数値フィールド。 | 10.4 |
| 整数 | 整数 | 10 |
| 数式 | リードレコード上に存在する他のフィールドのデータを操作することによって値が生成されるフィールド。 これらはエクスポートされず、スマートキャンペーンでは使用できません。 | これを表示 [記事](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/create-and-use-a-concatenated-string-formula-field) |
| パーセント | 整数で表された割合 | 30 |
| URL | 入力を URL のプロトコルを含む URL に制限するテキストフィールド。 | http://example.com/ |
| 電話 | 電話番号 | 111-111-1111 |
| テキスト領域 | 長いテキスト。 | 最大 30,000 バイトをサポートします。 標準の ASCII 文字は、1 文字あたり 1 バイトを使用します（最大 30,000 文字まで可能）。 Unicode 文字は、1 文字あたり最大 4 バイトを使用できます（許可される文字数を 30,000 文字未満に減らします）。 |
| 文字列 | 短いテキスト （最大 255 文字） | Lorem ipsum dolor sit amet |
| Score | スコアの変更フローステップで操作できる整数フィールド | 10 |
| Boolean （以前のチェックボックス） | ユーザーが True （オン）または False （オフ）の値を選択できるようにします。 | True |
| 通貨 | Marketo配信登録用に選択されたデフォルトの通貨タイプを表す浮動小数フィールド | 10.40 |
| 日付 | 日付に使用されます。 W3C 形式に従います。 | 2010-05-07 |
| 参照 | 別のレコードへのキー（外部キー）を含む文字列フィールド。 | 企業に連絡 |
