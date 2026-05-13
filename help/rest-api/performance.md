---
title: パフォーマンス
feature: REST API
description: HTTP圧縮でMarketo REST APIのパフォーマンスを向上。 Gzipを有効にして帯域幅をカットします。一括APIはサポートされておらず、1024 バイト未満のバイトは圧縮されません。
exl-id: 173a398a-9d36-4e8d-9dd3-7d0d375b085a
TQID: https://experienceleague.adobe.com/foJCTd890HZtL-UzWx2cjRXwTxqgW56A79sB7FPEWis
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 146
ht-degree: 78%

---

# パフォーマンス

このページには、統合のパフォーマンスを向上させるために使用できるパフォーマンス関連のトピックのリストが含まれています。

## HTTP 圧縮

Marketo REST API は、HTTP 1.1 仕様で定義された標準を使用して、応答本文の HTTP 圧縮をサポートしています。 帯域幅の使用量と、データの取得にかかる時間が削減されるので、圧縮を有効にすることをお勧めします。

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

Curl を使用して[フィルタータイプによるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/getLeadsByFilterUsingGET)エンドポイントを呼び出し、5 個のリードを取得する例を以下に示します。

```bash
curl -H 'Accept-Encoding: gzip' 'https://123-ABC-456.mktorest.com/rest/v1/leads.json?filterType=id&filterValues=4,5,7,12,13'
```
