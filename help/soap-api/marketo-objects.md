---
title: "Marketo オブジェクト"
feature: SOAP
description: 「Marketo オブジェクトの概要」
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Marketo オブジェクト

Marketoは、Marketo オブジェクト（MObjects）を使用して、Program、Opportunity、OpportunityPersonRole などの様々なクラスを表します。

## MObjects の構造

MObjects には、標準、カスタム、仮想の 3 つのタイプがあります。 標準オブジェクトとカスタムオブジェクトは、リードや会社などの個別のエンティティを表しますが、LeadRecord などの仮想オブジェクトは、1 つ以上のオブジェクトのフィールドで構成されます。 仮想オブジェクトは、API 内で使用される便利なオブジェクトですが、Marketo アプリケーション内には存在しません。

オブジェクトは、次の要素で構成されます。

- すべてのオブジェクトに共通の固定属性の小さなセット
   - 必須タイプ
   - オプションの externalKey
   - 読み取り専用 ID、createdAt、updatedAt
- 1 つ以上のオブジェクト固有の属性（名前と値のペア）のリスト。一部は必須になる場合があります。 例えば、オポチュニティに名前を付けます。
- 関連するオブジェクト参照のリスト（オブジェクト名プラス）
   - Marketo ID または
   - 属性名/属性値ペアとしての外部キー。

### 外部キー

外部キーは、リードやオポチュニティなど、Marketo オブジェクトで定義されたカスタムフィールドです。 name はフィールド名で、value は外部システムで生成されたフィールド値です。 **Marketoは、これらの値に対して一意性制約を適用しません。** 値が一意であることを確認するのは、API ユーザーの責任です。 重複が発生した場合、Marketoは最後に追加されたオブジェクトを使用します。 これは、「メールアドレスの標準」フィールドの動作と似ています。

### 使用可能な API

| API | 操作可能 |
|---|---|
| describeMObject | ActivityRecord, LeadRecord, Opportunity, OpportunityPersonRole |
| getMObjects | 商談，OpportunityPersonRole, プログラム |
| syncMObjects | 商談，OpportunityPersonRole, プログラム |
| deleteMObjects | 商談，OpportunityPersonRole |
| listMObjects | ActivityRecord, LeadRecord, Opportunity, OpportunityPersonRole |
