---
title: "フィールド"
feature: REST API, Field Management
description: 「サポートされているフィールド名のリスト。」
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 6%

---


# フィールド

REST API と SOAP API では、リードフィールドに異なる命名規則を使用します。

## フィールド名のリストの取得

REST 「リードを説明」エンドポイントを使用して、リードレコードで使用可能なすべてのサポートされているフィールド名のリストを取得します。

## 使用するフィールド名タイプ

特定の統合関連機能を活用する際に、使用する必要があるフィールド名タイプを把握するのが難しい場合があります。 以下は、REST または SOAP フィールド名タイプを使用する機能のクイックリファレンスです。

| 機能 | 使用するフィールド名タイプ |
|--- |--- |
| リードトラッキング API （Munchkin） | SOAP |
| Forms 2.0 API | SOAP |
| リストの読み込み（UI） | SOAP |
| リストの読み込み（REST API） | REST |
| Webhook 応答マッピング | SOAP |
| メールスクリプティング（Velocity） | SOAP |
| SOAP API | SOAP |
| REST API | REST |

### REST API フィールド sfdcId が常に null の値を返すのはなぜですか？

フィールド `sfdcId` は、REST API の元のフィールドマップに誤って含まれた式フィールドです。 REST API を介して取得されたレコードは、式フィールドの値を計算しないので、値は常に null になります。 実際の SFDC ID を取得するには、というフィールドを使用する必要があります。 `sfdcLeadId` および `sfdcContactId`.
