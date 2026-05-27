---
title: フィールド
feature: REST API, Field Management
description: RESTとSOAPのリードフィールドの命名規則、REST Describe Leadによるフィールドのリスト、機能マッピング、sfdcIdがnullである理由、およびsfdcLeadIdまたはsfdcContactIdの使用について説明します。
exl-id: 9033f32a-c7cb-4bbf-abcf-38ca4112139f
TQID: https://experienceleague.adobe.com/H2Bvhy-67U8JJ1V3JwYJ0O0vj4i11fwUCyYQtjxm8u0
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 213
ht-degree: 88%

---

# フィールド

REST API と SOAP API では、リードフィールドに異なる命名規則を使用します。

## フィールド名のリストの取得

REST「リードを説明」エンドポイントを使用して、リードレコードで使用可能なすべてのサポートされているフィールド名のリストを取得します。

## 使用するフィールド名タイプ

特定の統合関連機能を活用する際、どのフィールド名タイプを使用する必要があるのか、把握するのが困難な場合があります。 REST または SOAP フィールド名タイプを使用する機能のクイック参照を以下に示します。

| 機能 | 使用するフィールド名タイプ |
| --- | --- |
| Lead Tracking API（Munchkin） | SOAP |
| Forms 2.0 API | SOAP |
| リストの読み込み（UI） | SOAP |
| リストの読み込み（REST API） | REST |
| Web フック応答マッピング | SOAP |
| メールスクリプト（Velocity） | SOAP |
| SOAP API | SOAP |
| REST API | REST |

### REST API フィールド sfdcId が常に null 値を返す理由

フィールド `sfdcId` は、REST API の元のフィールドマップに誤って含まれていた数式フィールドです。 REST API を通じて取得されたレコードは数式フィールドの値を計算しないので、値は常に null になります。 実際の SFDC ID を取得するには、`sfdcLeadId` および `sfdcContactId` というフィールドを使用する必要があります。
