---
title: リード APIの更新を取得
feature: REST API
description: リード活動の取得とリード変更のエンドポイントの制限の変更について説明します。
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# リード APIの更新を取得

2026年9月30日以降、ターゲットリストに10,000人以上のリードが含まれる場合、`listId` パラメーターを含む[&#x200B; リードアクティビティを取得](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadActivitiesUsingGET)または[&#x200B; リード変更を取得](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadChangesUsingGET) エンドポイントへの呼び出しは失敗します。 エンドポイントは、ターゲットの静的リストにレコードが多すぎることを示す1003 エラーコードを返します。

1つ以上の最近のAPI呼び出しは、この変更の影響を受けます。 サービスの中断を回避するには、2026年9月30日（PT）までにアプリケーションとMarketoの統合方法を更新する必要があります。

こうしたクエリでは、検索結果が表示されない場合や、検索結果が見つかる前にタイムアウトする場合がよくあります。 設定サイズを制限することで、クエリの応答性が向上し、タイムリーに検索を完了できるようになります。

## 自分が影響を受けているかどうかはどのように判断できますか？

この変更は、少数のMarketo Engage インスタンスにのみ影響します。 影響を受けるサブスクリプションの管理者は、変更が適用される前に、アプリケーション内通知を受け取ります。

## どうすればよいですか？

このドキュメントを、Marketo Engage統合の担当者またはチームと共有します。

ユースケースに応じて、次のいずれかの移行オプションを使用します。

* アクティビティ抽出に使用する静的リストの数を10,000人に制限します。 既存のリストをより小さなリストに分割し、アクティビティに対して同じオーディエンスを引き続きポーリングします。
* 一括アクティビティ抽出またはデータストリームを使用して、アクティビティを抽出するか、データ値の変更を抽出します。 [getLeadByListId](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadsByListIdUsingGET_1)または[Bulk リード抽出](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/bulk-extract/bulk-lead-extract)を使用して、結果を静的リスト メンバーシップに結合します。

## 何もしないとどうなるの。

多数のメンバーを持つ静的リストからアクティビティをクエリする際に、API統合が処理されないエラーによって中断される可能性があります。
