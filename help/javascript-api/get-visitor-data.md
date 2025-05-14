---
title: 訪問者データを取得
description: 訪問者データを取得
feature: Javascript
exl-id: 39a2446d-8a31-461e-bbe6-a7edf24b4d52
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '184'
ht-degree: 100%

---

# 訪問者データを取得

このメソッドは、リアルタイムの訪問者識別データを取得するのに使用されます。

- User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。
- RTP は、アカウントベースマーケティングの重点顧客リストをサポートしていません。ABM リストとコードは、RTP 内で管理されるアップロード済みアカウントリスト（CSV ファイル）にのみ関連しています。

エラーが発生した場合、応答 JSON の一部としてエラーメッセージが表示されます。500 コードが返された場合は、リクエストをサポートにお問い合わせしてください。

| パラメーター | オプション／必須 | タイプ | 説明 |
|---|---|---|---|
| `get` | 必須 | 文字列 | メソッドアクション。 |
| `visitor` | 必須 | 文字列 | メソッド名。 |
| `callback` | 必須 | 関数 | 返されるキャンペーンごとにトリガーされるコールバック関数。 |

## 例

訪問者識別データの取得：

```javascript
function callbackFunction() {
    console.log('RTP is awesome!');
}
rtp('get', 'visitor', callbackFunction);
```

セグメント一致を含む応答：

Get Visitor Data API 呼び出しの前に訪問者がリアルタイムセグメントに一致した場合に返される応答の例を以下に示します。

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

Get Visitor Data API 呼び出しの前に訪問者がリアルタイムセグメントに一致しなかった場合に返される応答の例を以下に示します。

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
