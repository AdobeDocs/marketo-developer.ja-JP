---
title: カスタムオブジェクト
feature: SOAP
description: Marketoのカスタムオブジェクトを使用して、1つのリードを多くのレコードにリンクする方法を説明します。取得、同期、削除、スマートリストおよびメールの使用に対するSOAP API呼び出しの構造、制限を含みます。
exl-id: 29d65841-4b44-4d94-b14e-c583d433d015
TQID: https://experienceleague.adobe.com/Fy3h8qfKs8gizeakXkhoj5mJhib-QA2kYOu41YMIEZs
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 286
ht-degree: 78%

---

# カスタムオブジェクト

Marketo カスタムオブジェクトを使用すると、Marketo リードとカスタムオブジェクトレコードの間に 1 対多の関係を作成できます。 例えば、リードが参加したすべてのロードショーを追跡する必要がある場合、 リードは（複数年にわたって）多数のロードショーに参加する場合があるので、この情報を保存するにはカスタムオブジェクトの方が適しています。

カスタムオブジェクトは、Spark を除くすべての Marketo エディションでサポートされています。 Marketo カスタムオブジェクトがアカウントに正常にプロビジョニングされると、次の操作を実行できます

- Marketo SOAP API 経由でカスタムオブジェクトのレコードを作成／読み取り／更新／削除
- カスタムオブジェクトに新しいレコードが追加された際にスマートリストトリガーを使用
- カスタムオブジェクトデータをスマートリストのフィルターとして使用
- Marketo メールスクリプトを使用してメールでカスタムオブジェクトデータを使用

## カスタムオブジェクトの構造

カスタムオブジェクトは、次で構成されます。

- すべてのカスタムオブジェクトに共通する固定属性の小さなセット
   - オブジェクト名（オブジェクトタイプ名とも呼ばれる）
   - オブジェクトの詳細
   - カスタムオブジェクトから Marketo リードへのリンクフィールド名 - カスタムオブジェクトが参照するリード（ユーザ）オブジェクトのフィールドです
   - オブジェクトキーフィールド名 - オブジェクトで使用されるプライマリキー
- 1 つ以上のオブジェクト固有フィールド（最大 50 個のフィールドをサポート）

## カスタムオブジェクト操作

次の呼び出しを使用して、CO とやり取りできます。

- [getCustomObjects](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectsUsingGET)
- [syncCustomObjects](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST)
- [deleteCustomObjects](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST)
