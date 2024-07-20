---
title: SOAPに関する FAQ
feature: SOAP
description: SOAPに関する FAQ
exl-id: a2d8f144-cd5f-41bc-8231-29c42af935b8
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---

# SOAPに関する FAQ

**Q:** Marketo内のすべてのプログラムとそのメタデータのリストを取得するにはどうすればよいですか？

**A:** すべてのプログラムのリストを取得するには、[getMObjects](./getmobjects.md) を使用して、「Program」と等しいタイプを渡し、includeDetails を true に設定します。

**Q:** getMultipleLeads のパフォーマンスを高速化する方法はありますか？

**A:** getMultipleLeads 呼び出しのパフォーマンスを高速化するには、いくつかのオプションがあります。 1 つ目は、各呼び出しで要求する batchSize を減らすことです。 推奨されるバッチサイズは 200 です。 2 つ目のオプションは、includeAttributes フィルターを使用して、目的のフィールドを指定することです。 これにより、クエリが高速化され、受信する応答のペイロードが減少します。 最後のアプローチは、LastUpdateAtSelector を使用し、oldestUpdatedAt と latestUpdatedAt を指定することです。 異なる日付範囲を指定してから、複数のリクエストを同時にスレッド化できます。 スレッドアプローチを使用する場合は、SOAP/WSDL クライアントが [ 永続的な接続 ](https://www.w3.org/Protocols/rfc2616/rfc2616-sec8.html) をサポートしていることを確認します。

**Q:** SalesForce やMicrosoft Dynamics などの CRM と統合されていない場合、SOAP API を使用してオポチュニティを作成するにはどうすればよいですか？

**A:** OpportunityPersonRole タイプおよび Opportunity [MObject](syncmobjects.md) タイプへの [syncMObjects](marketo-objects.md) 呼び出し書き込みを使用し、SOAP API を使用して商談を作成できます。

**Q:** Marketoからプログラムでメールを送信することはできますか？ その場合、各メール受信者にカスタムコンテンツを送信するにはどうすればよいですか？

**A：絶対**。 [requestCampaign](requestcampaign.md) または [importToList](importtolist.md) と [scheduleCampaign](schedulecampaign.md) SOAP API の組み合わせを使用して、Marketoから送信されるメールをリクエストできます。 1 人または複数のユーザーにメールをすぐに送信するには、[requestCampaign](requestcampaign.md) を使用します。 メールが指定の日時に送信されるようにスケジュールする場合は、[importToList](importtolist.md) を使用してメールの受信者を指定し、[scheduleCampaign](schedulecampaign.md) を使用して、これらの受信者にメールが送信される日時を指定します。

各メール受信者のコンテンツをカスタマイズする場合は、メールテンプレート内で設定されている [ プログラムトークン ](../rest-api/tokens.md) の値を上書きします。
