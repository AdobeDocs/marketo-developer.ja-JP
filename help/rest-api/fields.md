---
title: フィールド
feature: REST API, Field Management
description: RESTとSOAPのリードフィールドの命名規則、REST Describe Leadによるフィールドのリスト、機能マッピング、sfdcIdがnullである理由、およびsfdcLeadIdまたはsfdcContactIdの使用について説明します。
exl-id: 9033f32a-c7cb-4bbf-abcf-38ca4112139f
TQID: https://experienceleague.adobe.com/H2Bvhy-67U8JJ1V3JwYJ0O0vj4i11fwUCyYQtjxm8u0
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 194
ht-degree: 40%

---

# フィールド

REST API と SOAP API では、リードフィールドに異なる命名規則を使用します。 各統合機能で必要なフィールド名規則を使用します。

## フィールド名のリストの取得

RESTの「リードの記述」エンドポイントを使用して、リードレコードでサポートされているすべてのフィールド名を取得します。

## 使用するフィールド名タイプ

必須のフィールド名タイプは、統合機能によって異なります。 次の表は、各機能でRESTまたはSOAPのフィールド名を使用するかどうかを示しています。

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

`sfdcId` フィールドは、REST APIの元のフィールドマップに含まれた数式フィールドです。 REST APIを介して取得されたレコードは数式フィールド値を計算しないため、`sfdcId`は常にnullを返します。

SFDC IDを取得するには、`sfdcLeadId`および`sfdcContactId` フィールドを使用します。
