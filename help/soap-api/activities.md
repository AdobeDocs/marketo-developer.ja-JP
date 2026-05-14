---
title: アクティビティ
feature: SOAP
description: SOAPを使用してアクティビティを操作する方法、リードアクティビティを取得する方法、getLeadActivitiesおよびgetLeadChangesを使用してリードの変更を追跡する方法について説明します
exl-id: fd695ab6-e7be-4ced-89c9-c4cd2d4c2ab0
TQID: https://experienceleague.adobe.com/6zUkvoDCqlRmblFDPWzLjdwITsyWxcXrJBKbLux76WI
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: e71bcf289229867bc969345d79c8f014761aaaf9
workflow-type: tm+mt
source-wordcount: 79
ht-degree: 18%

---

# アクティビティ

次の SOAP 呼び出しを使用して、アクティビティとやり取りできます。

- [getLeadActivities](getleadactivity.md)
- [getLeadChanges](getleadchanges.md)

>[!CAUTION]
>
>2026-12-30以降、ターゲットリストに10,000人以上のリードが含まれる場合、`listId` パラメーターを含む`Get Lead Activities`および`Get Lead Changes` エンドポイントへの呼び出しは失敗します（エラーコード 1003）。 サービスの中断を回避するには、この制限を回避するために、呼び出しが適切にスコープ設定されていることを確認します。 [移行ガイド ](migration.md)を参照してください。
