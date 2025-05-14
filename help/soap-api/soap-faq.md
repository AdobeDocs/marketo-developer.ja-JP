---
title: SOAP に関するよくある質問
feature: SOAP
description: SOAP に関するよくある質問
exl-id: a2d8f144-cd5f-41bc-8231-29c42af935b8
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '333'
ht-degree: 100%

---

# SOAP に関するよくある質問

**Q：** Marketo 内のすべてのプログラムのリストと、このメタデータを取得するにはどうすればよいですか？

**A：**&#x200B;すべてのプログラムのリストを取得するには、[getMObjects](./getmobjects.md) を使用して、型を「Program」に渡し、includeDetails を true に設定します。

**Q：** getMultipleLeads のパフォーマンスを高速化する方法はありますか？

**A：** getMultipleLeads 呼び出しのパフォーマンスを高速化するオプションがいくつかあります。1 番目は、各呼び出しでリクエストする batchSize を減らすことです。推奨されるバッチサイズは 200 です。2 番目のオプションは、includeAttributes フィルターを使用して、興味のあるフィールドを指定することです。これにより、クエリが高速化され、受け取る応答のペイロードが削減されます。最後のアプローチは、LastUpdateAtSelector を使用して、oldestUpdatedAt とlatestUpdatedAt を指定することです。異なる日付範囲を指定して、複数のリクエストを同時にスレッド化できます。スレッド化したアプローチを使用する場合は、SOAP／WSDL クライアントが[永続的な接続](https://www.w3.org/Protocols/rfc2616/rfc2616-sec8.html)をサポートしていることを確認します。

**Q：** SalesForce や Microsoft Dynamics などの CRM と統合されていない場合、SOAP API 経由で商談を作成するにはどうすればよいですか？

**A：** SOAP API を使用して、[syncMObjects](syncmobjects.md) 呼び出しで、OpportunityPersonRole および Opportunity [MObject](marketo-objects.md) タイプに書き込みを行うことで商談を作成できます。

**Q：** Marketo からプログラムでメールを送信できますか？その場合、各メール受信者にカスタムコンテンツを送信するにはどうすればよいですか？

**A：**&#x200B;もちろんできます。[requestCampaign](requestcampaign.md)、または [importToList](importtolist.md) と [scheduleCampaign](schedulecampaign.md) SOAP API の組み合わせのいずれかを使用して、Marketo からメールを送信するようにリクエストできます。1 人以上の人物にすぐにメールを送信するには、[requestCampaign](requestcampaign.md) を使用します。指定した日時にメールを送信するようにスケジュールする場合は、[importToList](importtolist.md) を使用してメールの受信者を指定し、[scheduleCampaign](schedulecampaign.md) を使用してこれらの受信者にメールを送信するタイミングを指定します。

各メール受信者のコンテンツをカスタマイズする場合は、メールテンプレート内に設定されている[プログラムトークン](../rest-api/tokens.md)の値を上書きしてカスタマイズできます。
