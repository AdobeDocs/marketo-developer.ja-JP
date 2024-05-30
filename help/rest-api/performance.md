---
title: "パフォーマンス"
feature: REST API
description: 「Marketo API を使用する際のパフォーマンスヒント」
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# パフォーマンス

このページには、統合のパフォーマンスを向上させるために使用できるパフォーマンス関連のトピックのリストが含まれています。

## HTTP 圧縮

Marketo REST API は、HTTP 1.1 仕様で定義された標準を使用して、応答本文の HTTP 圧縮をサポートしています。  圧縮を有効にすることをお勧めします。これにより、帯域幅の使用量と、データの取得に費やす時間が削減されるからです。

**注意：**  1024 バイト未満のペイロードは圧縮されません。

圧縮を有効にするには、リクエストに次の HTTP ヘッダーを含めます。

```html
Accept-Encoding: gzip
```

Marketo REST API は応答本文を圧縮し、次のヘッダーを含めます。

```html
Content-Encoding: gzip
```

Curl を使用してを呼び出す例を次に示します [フィルタータイプ別のリードの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET) 5 つのリードを取得するエンドポイント：

```bash
$ curl -H 'Accept-Encoding: gzip' 'https://123-ABC-456.mktorest.com/rest/v1/leads.json?filterType=id&filterValues=4,5,7,12,13'
```
