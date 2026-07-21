---
title: 訪問者データを取得
description: パラメーター、コールバック例、セグメント、ABM、位置情報のサンプル応答を含むRTP ユーザーコンテキスト APIを使用して、リアルタイムの訪問者を特定します。
feature: Javascript
exl-id: 39a2446d-8a31-461e-bbe6-a7edf24b4d52
TQID: https://experienceleague.adobe.com/B-JMACtMs3aRVsb1eJKaRoQGgVKB6MTbd0KBoZ7Ay6k
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: e2290edd-b061-4880-9d79-dee306cf5aa9id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 214
ht-degree: 48%

---

# 訪問者データを取得

この方法を使用して、訪問者識別データをリアルタイムで取得します。

- User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。
- RTP は、アカウントベースマーケティングの重点顧客リストをサポートしていません。 ABM リストとコードは、RTP 内で管理されるアップロード済みアカウントリスト（CSV ファイル）にのみ関連しています。

エラーが発生した場合、応答JSONにはエラーメッセージが含まれます。 APIが500 コードを返す場合は、サポートに連絡して、エラーの原因となったリクエストを提供してください。

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| `get` | 必須 | 文字列 | メソッドアクション。 |
| `visitor` | 必須 | 文字列 | メソッド名。 |
| `callback` | 必須 | 関数 | 返されるキャンペーンごとにトリガーされるコールバック関数。 |

## 例

次の例では、訪問者識別データを取得します。

```javascript
function callbackFunction() {
    console.log('RTP is awesome!');
}
rtp('get', 'visitor', callbackFunction);
```

セグメント一致を含む応答：

次の応答には、`matchedSegments`が含まれます。これは、訪問者がGet Visitor Data API呼び出しの前にリアルタイムセグメントと一致したためです。

```json
{
    "status": 200,
    "results": {
        "matchedSegments": [
            {
                "name": "first click",
                "id": 177
            }
        ],
        "abm": [
            {
                "code": 4,
                "name": "abm_saleforce_customers"
            },
            {
                "code": 5,
                "name": "abm_top_customers"
            }
        ],
        "org": "Marketo",
        "location": {
            "country": "United States",
            "city": "San Mateo",
            "state": "CA"
        },
        "industries": [
            "Software & Internet"
        ],
        "isp": false
    }
}
```

セグメント一致なしの応答：

次の応答には`matchedSegments`が含まれていません。これは、訪問者がGet Visitor Data API呼び出しの前にリアルタイム セグメントに一致しなかったためです。

```json
{
    "status": 200,
    "results": {
        "abm": [
            {
                "code": 4,
                "name": "abm_saleforce_customers"
            },
            {
                "code": 5,
                "name": "abm_top_customers"
            }
        ],
        "org": "Marketo",
        "location": {
            "country": "United States",
            "city": "San Mateo",
            "state": "CA"
        },
        "industries": [
            "Software & Internet"
        ],
        "isp": false
    }
}
```
