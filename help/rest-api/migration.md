---
title: リード APIの更新を取得
feature: REST API
description: リード活動の取得とリード変更のエンドポイントの制限の変更について説明します。
source-git-commit: e71bcf289229867bc969345d79c8f014761aaaf9
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# リード APIの更新を取得

2026年9月30日から、[&#x200B; リードアクティビティの取得](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadActivitiesUsingGET)または[&#x200B; リード変更の取得](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadChangesUsingGET) エンドポイントへの呼び出しが開始されます。このエンドポイントに`listId` パラメーターが含まれていると、ターゲットリストに10,000個以上のリードが含まれ、ターゲットスタティックリストにレコードが多すぎることを示すエラーコードが1003件ある場合、失敗します。 この変更の影響を受ける1つ以上のAPI呼び出しが最近行われました。 サービスの中断を回避するには、2026年9月30日（PT）までにアプリケーションとMarketoの統合方法を更新する必要があります。

これらのタイプのクエリは、多くの場合、結果が出ない可能性のある検索や、結果が見つかる前にタイムアウトする検索を作成します。 セットのサイズを制限すると、これらのタイプのクエリの応答性が向上し、データセットの検索をタイムリーに完了できるようになります。

## 自分が影響を受けているかどうかはどのように判断できますか？

この変更は、少数のMarketo Engage インスタンスにのみ影響します。 影響を受けるサブスクリプションの管理者には、変更が適用される前にアプリケーション内で通知されます。

## どうすればよいですか？

このドキュメントは、Marketo Engage統合の担当者またはチームと共有する必要があります。

ユースケースに応じて、アプリケーションを移行するには、次の2つの基本的なオプションがあります。

* アクティビティを抽出する静的リストは、最大10,000人のメンバーに制限します。 既存のリストのいずれかを小さなリストに分割して、アクティビティに対して同じオーディエンスを引き続きポーリングできます。
* アクティビティの一括抽出またはデータストリームを使用してアクティビティまたはデータ値の変更を抽出し、その結果を[getLeadByListId](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadsByListIdUsingGET_1)または[Bulk リード抽出](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/bulk-extract/bulk-lead-extract)の静的リストメンバーシップに結合します

## 何もしないとどうなるの。

多数のメンバーを持つ静的リストからアクティビティをクエリする際に、処理できないエラーが発生し、API統合の機能が中断される場合があります。
