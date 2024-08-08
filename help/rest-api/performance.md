---
title: パフォーマンス
feature: REST API
description: Marketo API を使用する際のパフォーマンスヒント
exl-id: 173a398a-9d36-4e8d-9dd3-7d0d375b085a
source-git-commit: 4e64b8a801e443471f52090b7f008b11e628012d
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---

# パフォーマンス

このページには、統合のパフォーマンスを向上させるために使用できるパフォーマンス関連のトピックのリストが含まれています。

## HTTP 圧縮

Marketo REST API は、HTTP 1.1 仕様で定義された標準を使用して、応答本文の HTTP 圧縮をサポートしています。 圧縮を有効にすることをお勧めします。これにより、帯域幅の使用量と、データの取得に費やす時間が削減されるからです。

>[!NOTE]
>
>1024 バイトに満たないペイロードは圧縮されず、Bulk API は圧縮をサポートしません。

圧縮を有効にするには、リクエストに次の HTTP ヘッダーを含めます。

```html
Accept-Encoding: gzip
```

Marketo REST API は応答本文を圧縮し、次のヘッダーを含めます。

```html
Content-Encoding: gzip
```

次に、Curl を使用して [ フィルタータイプによってリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET) エンドポイントを呼び出し、5 つのリードを取得する例を示します。

```bash
$ curl -H 'Accept-Encoding: gzip' 'https://123-ABC-456.mktorest.com/rest/v1/leads.json?filterType=id&filterValues=4,5,7,12,13'
```
