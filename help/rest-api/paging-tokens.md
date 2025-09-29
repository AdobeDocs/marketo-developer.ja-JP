---
title: ページングトークン
feature: REST API
description: Marketo REST API ページングトークンを使用してアクティビティとリードを取得し、日付ベースと位置ベースのトークン、ISO 8601 sinceDatetime、414 エラーをカバーします。
exl-id: 63fbbf03-8daf-4add-85b0-a8546c825e5b
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 94%

---

# ページングトークン

結果をページスルーしたり、特定のデータに関連して更新されたデータを取得したりするために、Marketo にはページングトークンが用意されています。

場合によっては、長いページングトークン文字列が返されることがあります。これにより、HTTP 414 エラーコードが発生する場合があります。これらのエラーの処理方法について詳しくは、[こちら](error-codes.md)を参照してください。

[Paging Token API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getActivitiesPagingTokenUsingGET) ドキュメントを参照してください。

## トークンのタイプ

Marketo が提供するページングトークンには、2 つのタイプがあります。これらは関連性はあるものの、異なるタイプです。

- 日付ベース
- 位置ベース

## 日付ベース

1 番目は、日付を表すページングトークンです。これらは、ページングトークンで表される日付以降に発生したアクティビティ、データ値の変更、および削除されたリードを取得するために使用されます。このタイプのページングトークンは、[ページングトークンを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getActivitiesPagingTokenUsingGET)エンドポイントを呼び出して日時を含めることで生成されます。

```
GET /rest/v1/activities/pagingtoken.json?sinceDatetime=2014-10-06T13:22:17-08:00
```

```json
{
    "requestId": "1607c#14884f3e74e",
    "success": true,
    "nextPageToken": "GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ"
}
```

`sinceDateTime` パラメーターの形式は、[ISO 8601](https://ja.wikipedia.org/wiki/ISO_8601) 標準の日付表記に準拠する必要があります。最適な結果を得るには、タイムゾーンを含む完全な日時を使用します。タイムゾーンは、次の形式を使用して GMT からのオフセットとして表すことができます。

`yyyy-mm-ddThh:mm:ss+|-hh:mm`

または、大文字の「Z」を省略形として使用して、次のように UTC を表します。

`yyyy-mm-ddThh:mm:ssZ`

例

`2016-09-15T15:53:00+05:00`

`2016-09-15T10:53:00Z`

`sinceDateTime` はクエリパラメーターなので、URL エンコードする必要があります。

次に、`nextPageToken` 文字列が[リードアクティビティを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET)、[リード変更を取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadChangesUsingGET)、または[削除されたリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET)呼び出しに提供され、Get Paging Token API に提供された日時以降のアクティビティが取得されます。

```
GET /rest/v1/activities.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ&activityTypeIds=1&activityTypeIds=12
```

## 位置ベース

2 番目のタイプのページングトークンは、Lead Database API へのバッチ取得呼び出しで返される場合があります。このタイプのページングトークンは、レコードのトラバーサルを可能にするデータベースカーソルと概念的に似ています。例えば、「フィルタータイプでリードを取得」呼び出しを使用すると、指定されたバッチサイズ（通常は最大値およびデフォルトの 300）を超えるセットが表示される場合があります。さらに結果がある場合、応答内の moreResult フィールドは true になり、`nextPageToken` が返されます。結果セット内の追加レコードを取得するには、新しい呼び出しで前の応答から受信した値を含む `nextPageToken` を含む追加の呼び出しを実行します。結果として得られる応答では、結果セットの次のページが返されます。
