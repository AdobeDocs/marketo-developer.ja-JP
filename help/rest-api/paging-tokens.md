---
title: ページングトークン
feature: REST API
description: Marketo REST API ページングトークンを使用して、アクティビティとリードを取得します。これには、日付ベースおよび位置ベースのトークン、日時からのISO 8601、414 エラーが含まれます。
exl-id: 63fbbf03-8daf-4add-85b0-a8546c825e5b
TQID: https://experienceleague.adobe.com/Ut05n-Y-qPJnvcNRs9liwE3NVBMbJlvaGyv-nExRsek
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 387
ht-degree: 5%

---

# ページングトークン

Marketoには、結果を確認したり、特定の日付に関連して更新されたデータを取得したりするためのページングトークンが用意されています。

一部の応答では、長いページングトークン文字列が返されるため、HTTP 414 エラーが発生する可能性があります。 これらの[ エラー](error-codes.md)の処理に関する情報を参照してください。

[Paging Token API](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getActivitiesPagingTokenUsingGET) ドキュメントを参照してください。

## トークンのタイプ

Marketoには、関連する2種類のページングトークンがありますが、異なる種類があります。

- 日付ベースのトークンは、指定された日時の後に発生したレコードを取得します。
- ポジションベースのトークンは、結果セット内のレコードをトラバースします。

## 日付ベース

日付ベースのページングトークンは、日時を表します。 このデータを使用して、アクティビティ、データ値の変更、およびその日付以降に発生した削除されたリードを取得します。

日時を含む[ ページングトークンを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getActivitiesPagingTokenUsingGET) エンドポイントを呼び出して、日付ベースのトークンを生成します。

```http
GET /rest/v1/activities/pagingtoken.json?sinceDatetime=2014-10-06T13:22:17-08:00
```

```json
{
    "requestId": "1607c#14884f3e74e",
    "success": true,
    "nextPageToken": "GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ"
}
```

`sinceDateTime` パラメーターでは、[ISO 8601](https://ja.wikipedia.org/wiki/ISO_8601)の標準日付表記法を使用する必要があります。 最良の結果を得るには、タイムゾーンを含む完全な日時を指定します。

タイムゾーンをGMTからのオフセットとして次の形式で表します。

`yyyy-mm-ddThh:mm:ss+|-hh:mm`

または、大文字の「Z」を使用してUTCを表します。

`yyyy-mm-ddThh:mm:ssZ`

例：

`2016-09-15T15:53:00+05:00`

`2016-09-15T10:53:00Z`

`sinceDateTime`はクエリパラメーターであるため、その値をURL エンコードします。

返された`nextPageToken`文字列を[ リード活動の取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadActivitiesUsingGET)、[ リード変更の取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadChangesUsingGET)または[削除されたリードの取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getDeletedLeadsUsingGET)呼び出しに渡します。 呼び出しは、Get Paging Token APIに指定された日時の後に発生するレコードを取得します。

```http
GET /rest/v1/activities.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ&activityTypeIds=1&activityTypeIds=12
```

## 位置ベース

ポジションベースのページングトークンは、リードデータベース APIに対する任意のバッチ取得呼び出しによって返すことができます。 トークンはデータベースカーソルのように機能し、レコードのトラバーサルを可能にします。

例えば、「フィルタータイプ別にリードを取得」呼び出しは、要求されたバッチサイズよりも大きい結果セットを返すことができます。通常、最大値とデフォルト値は300です。 より多くの結果が得られると、応答はmoreResult フィールドをtrueに設定し、`nextPageToken`を返します。

次のページを取得するには、別の呼び出しを行い、前の応答から`nextPageToken`値を渡します。 応答は、結果セット内の次のページを返します。
