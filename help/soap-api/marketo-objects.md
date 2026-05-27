---
title: Marketo オブジェクト
feature: SOAP
description: Marketo オブジェクトの概要（種類、属性、外部キーの動作、商談、プログラム、関連レコードのサポートされているSOAP APIなど）。
exl-id: 99b9aed4-94e8-46e8-84d9-2cc5215b0c13
TQID: https://experienceleague.adobe.com/-G3BW9oFhPZL68yBUy-aNYycmgADhQCo8OclQAierrU
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 83%

---

# Marketo オブジェクト

Marketo は、Marketo オブジェクト（MObject）を使用して、Program、Opportunity、OpportunityPersonRole などの様々なクラスを表します。

## MObject の構造

MObject には、標準、カスタム、仮想の 3 つのタイプのいずれかを指定できます。 標準およびカスタム MObject は、Lead や Company などの個別のエンティティを表しますが、LeadRecord などの仮想オブジェクトは、1 つ以上のオブジェクトのフィールドで構成されます。 仮想オブジェクトは、API 内で使用される便利なオブジェクトですが、Marketo アプリケーション内には存在しません。

MObject は、次で構成されます。

- すべての MObject に共通する固定属性の小さなセット
   - 必須タイプ
   - オプションの externalKey
   - 読み取り専用 ID、createdAt、updatedAt
- 名前と値のペアとして 1 つ以上のオブジェクト固有の属性のリスト。一部の属性は必須になる場合があります。 例：Opportunity での名前。
- 関連するオブジェクト参照のリスト。オブジェクト名と、次のいずれかが含まれます。
   - Marketo ID または
   - 属性名／属性値のペアとしての外部キー。

### 外部キー

外部キーは、Lead や Opportunity などの Marketo オブジェクトで定義されたカスタムフィールドです。 名前はフィールド名で、値は外部システムで生成されたフィールド値です。 **Marketoはこれらの値に一意の制約を適用しません。** 値が一意であることを確認するのは、API ユーザーの責任です。 重複が発生した場合、Marketo では最後に追加されたオブジェクトを使用します。 これは、「メールアドレス」標準フィールドの動作に似ています。

### 使用可能な API

| API | 次で操作可能 |
| --- | --- |
| describeMObject | ActivityRecord、LeadRecord、Opportunity、OpportunityPersonRole |
| getMObjects | Opportunity、OpportunityPersonRole、Program |
| syncMObjects | Opportunity、OpportunityPersonRole、Program |
| deleteMObjects | Opportunity、OpportunityPersonRole |
| listMObjects | ActivityRecord、LeadRecord、Opportunity、OpportunityPersonRole |
