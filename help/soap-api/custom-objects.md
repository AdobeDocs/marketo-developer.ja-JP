---
title: 「カスタムオブジェクト」
feature: SOAP
description: 「カスタムオブジェクトの作成」
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---


# カスタムオブジェクト

Marketo カスタムオブジェクトを使用すると、Marketo リードとカスタムオブジェクトレコードの間に 1 対多の関係を作成できます。 例えば、リードが参加しているすべてのロードショーをトラッキングする必要がある場合があります。 リードは（数年間にわたって）多数のロードショーに参加する可能性があるので、カスタムオブジェクトは、この情報の保存に適しています。

カスタムオブジェクトは、Spark を除くすべてのMarketo エディションでサポートされています。 Marketo カスタムオブジェクトがアカウントに正常にプロビジョニングされると、次のことが可能になります

- Marketo SOAP API を使用したカスタムオブジェクト内のレコードの作成/読み取り/更新/削除
- 新しいレコードがカスタム・オブジェクトに追加された場合にスマート・リスト・トリガーを使用します
- カスタム・オブジェクト・データをスマート・リストのフィルタとして使用
- Marketoのメールスクリプティングを使用したメールでのカスタムオブジェクトデータの使用

## カスタムオブジェクトの構造

カスタムオブジェクトは、次の要素で構成されます。

- すべてのカスタムオブジェクトに共通の固定属性の小さなセットです。
   - オブジェクト名（オブジェクトタイプ名）
   - オブジェクトの詳細
   - Marketo リードリンクフィールド名へのカスタムオブジェクト – カスタムオブジェクトが参照するリード（人物）オブジェクト上のフィールドです
   - オブジェクトキーフィールド名 – オブジェクトで使用されるプライマリキー
- 1 つ以上のオブジェクト固有フィールド（最大 50 個のフィールドをサポート）

## カスタムオブジェクト操作

次の呼び出しを使用して、CO とやり取りできます。

- [getCustomObjects](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectsUsingGET)
- [syncCustomObjects](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST)
- [deleteCustomObjects](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST)
