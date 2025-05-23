---
title: フィールド
feature: REST API, Field Management
description: サポートされているフィールド名のリスト。
exl-id: 9033f32a-c7cb-4bbf-abcf-38ca4112139f
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '194'
ht-degree: 100%

---

# フィールド

REST API と SOAP API では、リードフィールドに異なる命名規則を使用します。

## フィールド名のリストの取得

REST「リードを説明」エンドポイントを使用して、リードレコードで使用可能なすべてのサポートされているフィールド名のリストを取得します。

## 使用するフィールド名タイプ

特定の統合関連機能を活用する際、どのフィールド名タイプを使用する必要があるのか、把握するのが困難な場合があります。REST または SOAP フィールド名タイプを使用する機能のクイック参照を以下に示します。

| 機能 | 使用するフィールド名タイプ |
|--- |--- |
| Lead Tracking API（Munchkin） | SOAP |
| Forms 2.0 API | SOAP |
| リストの読み込み（UI） | SOAP |
| リストの読み込み（REST API） | REST |
| Web フック応答マッピング | SOAP |
| メールスクリプト（Velocity） | SOAP |
| SOAP API | SOAP |
| REST API | REST |

### REST API フィールド sfdcId が常に null 値を返す理由

フィールド `sfdcId` は、REST API の元のフィールドマップに誤って含まれていた数式フィールドです。REST API を通じて取得されたレコードは数式フィールドの値を計算しないので、値は常に null になります。実際の SFDC ID を取得するには、`sfdcLeadId` および `sfdcContactId` というフィールドを使用する必要があります。
