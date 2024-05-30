---
title: 「SOAP に関する FAQ」
feature: SOAP
description: 「SOAP に関する FAQ」
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# SOAP に関する FAQ

**Q:** Marketo内のすべてのプログラムとそのメタデータのリストを取得するにはどうすればよいですか？

**回答：** すべてのプログラムのリストを取得するには、次を使用します [getMObjects](./getmobjects.md) 「Program」に等しいタイプを渡し、includeDetails を true に設定します。

**Q:** getMultipleLeads のパフォーマンスを高速化する方法はありますか？

**回答：** getMultipleLeads 呼び出しのパフォーマンスを高速化するには、いくつかのオプションがあります。 1 つ目は、各呼び出しで要求する batchSize を減らすことです。 推奨されるバッチサイズは 200 です。 2 つ目のオプションは、includeAttributes フィルターを使用して、目的のフィールドを指定することです。 これにより、クエリが高速化され、受信する応答のペイロードが減少します。 最後のアプローチは、LastUpdateAtSelector を使用し、oldestUpdatedAt と latestUpdatedAt を指定することです。 異なる日付範囲を指定してから、複数のリクエストを同時にスレッド化できます。 スレッドアプローチを使用する場合、SOAP/WSDL クライアントがサポートしていることを確認します [永続的な接続](https://www.w3.org/Protocols/rfc2616/rfc2616-sec8.html).

**Q:** SalesForce やMicrosoft Dynamics などの CRM と統合されていない場合、SOAP API を使用して商談を作成するにはどうすればよいですか？

**回答：** 次を使用して、SOAP API を使用して商談を作成できます [syncMObjects](syncmobjects.md) opportunityPersonRole および Opportunity への書面の呼び出し [オブジェクト](marketo-objects.md) タイプ。

**Q:** Marketoからプログラムでメールを送信できますか？ その場合、各メール受信者にカスタムコンテンツを送信するにはどうすればよいですか？

**回答：** 絶対。 Marketoから送信されるメールをリクエストするには、 [requestPaign](requestcampaign.md) または組み合わせ [importToList](importtolist.md) および [scheduleCampaign](schedulecampaign.md) SOAP API。 1 人または複数のユーザーにメールをすぐに送信するには、次を使用します。 [requestPaign](requestcampaign.md). 指定した日時にメールを送信するようにスケジュールする場合は、次を使用します [importToList](importtolist.md) メールの受信者を指定する手順は、次のとおりです。 [scheduleCampaign](schedulecampaign.md) これらの受信者に電子メールを送信するタイミングを指定します。

各メール受信者のコンテンツをカスタマイズする場合は、の値を上書きすることによって行うことができます。 [プログラムトークン](../rest-api/tokens.md) これは、メールテンプレート内で設定されます。
