---
title: 「ページングトークン」
feature: REST API
description: 「ページング・トークン・データの表示」
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# ページングトークン

Marketoでは、結果をページスルーしたり、特定のデータに関連して更新されたデータを取得したりするために、ページングトークンを使用できます。

場合によっては、長いページングトークン文字列が返されることがあります。 これにより、HTTP 414 エラーコードが発生する場合があります。 これらの処理方法について詳しくは、こちらを参照してください [エラー](error-codes.md).

## トークンのタイプ

Marketoが提供する、関連する異なる 2 種類のページングトークンがあります。

- 日付ベース
- 位置ベース

## 日付ベース

1 つ目は、日付を表すページングトークンです。 これらは、ページングトークンで表された日付以降に発生したアクティビティ、データ値の変更および削除されたリードを取得するために使用されます。 このタイプのページングトークンは、 [ページングトークンの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getActivitiesPagingTokenUsingGET) エンドポイントと（日時を含む）。

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

の形式 `sinceDateTime` パラメーターはに準拠する必要があります [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 標準の日付表記。 最適な結果を得るには、タイムゾーンを含む完全な日時を使用します。 タイムゾーンは、次の形式を使用して GMT からのオフセットとして表すことができます。

`yyyy-mm-ddThh:mm:ss+|-hh:mm`

または、大文字「Z」を略記法として使用して、UTC を次のように表します。

`yyyy-mm-ddThh:mm:ssZ`

例

`2016-09-15T15:53:00+05:00`

`2016-09-15T10:53:00Z`

なぜなら `sinceDateTime` はクエリパラメーターで、URL エンコードする必要があります。

この `nextPageToken` 次に、文字列がに提供されます [リードアクティビティの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET), [リードの変更を取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadChangesUsingGET)、または [削除されたリードの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET) 呼び出しとアクティビティは、Get Paging Token API に提供された日時の後からから取得されます。

```
GET /rest/v1/activities.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ&activityTypeIds=1&activityTypeIds=12
```

## 位置ベース

2 つ目のタイプのページングトークンは、リードデータベース API に対する任意のバッチ取得呼び出しによって返される場合があります。 このタイプのページングトークンは、レコードのトラバーサルを可能にするデータベースカーソルと、概念が似ています。 例えば、フィルタータイプによるリードの取得呼び出しは、指定されたバッチサイズを超えるセット（通常は最大およびデフォルトの 300）を表す場合があります。 より多くの結果がある場合、応答の moreResult フィールドは true になり、 `nextPageToken` が返されます。 結果セットに追加のレコードを取得するには、以下のような追加の呼び出しを実行します `nextPageToken` と、新しい呼び出しでの前の応答から受信した値。 結果の応答は、結果セットの次のページを返します。
