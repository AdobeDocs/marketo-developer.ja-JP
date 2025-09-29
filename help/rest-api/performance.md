---
title: パフォーマンス
feature: REST API
description: HTTP 圧縮によるMarketo REST API のパフォーマンスの向上。 gzip を有効にして帯域幅を削減。Bulk API はサポートされておらず、1024 バイト未満は圧縮されていません。
exl-id: 173a398a-9d36-4e8d-9dd3-7d0d375b085a
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 83%

---

# パフォーマンス

このページには、統合のパフォーマンスを向上させるために使用できるパフォーマンス関連のトピックのリストが含まれています。

## HTTP 圧縮

Marketo REST API は、HTTP 1.1 仕様で定義された標準を使用して、応答本文の HTTP 圧縮をサポートしています。帯域幅の使用量と、データの取得にかかる時間が削減されるので、圧縮を有効にすることをお勧めします。

>[!NOTE]
>
>1024 バイト未満のペイロードは圧縮されず、一括 API は圧縮をサポートしません。

圧縮を有効にするには、リクエストに次の HTTP ヘッダーを含めます。

```html
Accept-Encoding: gzip
```

Marketo REST API は、応答本文を圧縮し、次のヘッダーを含めます。

```html
Content-Encoding: gzip
```

Curl を使用して[フィルタータイプによるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET)エンドポイントを呼び出し、5 個のリードを取得する例を以下に示します。

```bash
curl -H 'Accept-Encoding: gzip' 'https://123-ABC-456.mktorest.com/rest/v1/leads.json?filterType=id&filterValues=4,5,7,12,13'
```
