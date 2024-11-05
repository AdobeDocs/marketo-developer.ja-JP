---
title: ページングトークン
feature: REST API
description: ページング・トークン・データの表示。
exl-id: 63fbbf03-8daf-4add-85b0-a8546c825e5b
source-git-commit: a00583f367c2da36d9d1d6e0b05bfd4216573fbb
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 2%

---

# ページングトークン

Marketoでは、結果をページスルーしたり、特定のデータに関連して更新されたデータを取得したりするために、ページングトークンを使用できます。

場合によっては、長いページングトークン文字列が返されることがあります。 これにより、HTTP 414 エラーコードが発生する場合があります。 これらの [ エラー ](error-codes.md) の処理方法の詳細を確認できます。

[ ページングトークン API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getActivitiesPagingTokenUsingGET) ドキュメントを参照してください。

## トークンのタイプ

Marketoが提供する、関連する異なる 2 種類のページングトークンがあります。

- 日付ベース
- 位置ベース

## 日付ベース

1 つ目は、日付を表すページングトークンです。 これらは、ページングトークンで表された日付以降に発生したアクティビティ、データ値の変更および削除されたリードを取得するために使用されます。 このタイプのページングトークンは、[ ページングトークンの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getActivitiesPagingTokenUsingGET) エンドポイントを呼び出し、日時を含めることで生成されます。

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

`sinceDateTime` パラメーターの形式は、[ISO 8601](https://ja.wikipedia.org/wiki/ISO_8601) 標準の日付表記に準拠する必要があります。 最適な結果を得るには、タイムゾーンを含む完全な日時を使用します。 タイムゾーンは、次の形式を使用して GMT からのオフセットとして表すことができます。

`yyyy-mm-ddThh:mm:ss+|-hh:mm`

または、大文字「Z」を略記法として使用して、UTC を次のように表します。

`yyyy-mm-ddThh:mm:ssZ`

例

`2016-09-15T15:53:00+05:00`

`2016-09-15T10:53:00Z`

`sinceDateTime` はクエリパラメーターなので、URL エンコードする必要があります。

次に、`nextPageToken` 文字列が [ リードアクティビティを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET)、[ リード変更を取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadChangesUsingGET) または [ 削除されたリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET) 呼び出しに提供され、アクティビティは Get Paging Token API に提供された日時の後から取得されます。

```
GET /rest/v1/activities.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ&activityTypeIds=1&activityTypeIds=12
```

## 位置ベース

2 つ目のタイプのページングトークンは、リードデータベース API に対する任意のバッチ取得呼び出しによって返される場合があります。 このタイプのページングトークンは、レコードのトラバーサルを可能にするデータベースカーソルと、概念が似ています。 例えば、フィルタータイプによるリードの取得呼び出しは、指定されたバッチサイズを超えるセット（通常は最大およびデフォルトの 300）を表す場合があります。 より多くの結果がある場合、応答で moreResult フィールドが true になり、`nextPageToken` が返されます。 結果セット内の追加のレコードを取得するには、新しい呼び出しの前の応答から受け取った値を持つ `nextPageToken` を含む、追加の呼び出しを実行します。 結果の応答は、結果セットの次のページを返します。
