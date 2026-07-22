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
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 131
ht-degree: 22%

---

# パフォーマンス

このページのパフォーマンスオプションを使用して、統合の効率を向上させます。

## HTTP 圧縮

Marketo REST APIは、HTTP 1.1仕様で定義されているHTTP response-body圧縮をサポートしています。 圧縮を有効にして、帯域幅の使用とデータ検索時間を短縮します。

>[!NOTE]
>
>1024 バイト未満のペイロードは圧縮されず、一括 API は圧縮をサポートしません。

圧縮を有効にするには、リクエストに次の HTTP ヘッダーを含めます。

```html
Accept-Encoding: gzip
```

Marketo REST APIは、レスポンス本文を圧縮し、次のヘッダーを含みます。

```html
Content-Encoding: gzip
```

次のcURLの例では、[&#x200B; フィルターの種類](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/getLeadsByFilterUsingGET)でリードを取得エンドポイントを呼び出して、5つのリードを取得します。

```bash
curl -H 'Accept-Encoding: gzip' 'https://123-ABC-456.mktorest.com/rest/v1/leads.json?filterType=id&filterValues=4,5,7,12,13'
```
