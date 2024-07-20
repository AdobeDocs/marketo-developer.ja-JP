---
title: 訪問者データの取得
description: 訪問者データの取得
feature: Javascript
exl-id: 39a2446d-8a31-461e-bbe6-a7edf24b4d52
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 10%

---

# 訪問者データの取得

このメソッドを使用すると、リアルタイムの訪問者識別データを取得できます。

- User Context API を使用する前に、web Personalizationのユーザーになり、サイトに [RTP タグをデプロイ ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) しておく必要があります。
- RTP では、アカウントベースのマーケティングの名前付きアカウントリストをサポートしていません。 ABM のリストとコードは、RTP で管理されるアップロード済みアカウントリスト（CSV ファイル）にのみ関連しています。

エラーが発生した場合、応答 JSON の一部としてエラーメッセージが表示されます。 500 コードが返された場合は、そのリクエストをサポートにお問い合わせください。

| パラメーター | オプション/必須 | タイプ | 説明 |
|---|---|---|---|
| `get` | 必須 | 文字列 | メソッドのアクション。 |
| `visitor` | 必須 | 文字列 | メソッド名。 |
| `callback` | 必須 | 機能 | 返されるキャンペーンごとにトリガーされるコールバック関数。 |

## 例

訪問者識別データの取得：

```javascript
function callbackFunction() {
    console.log('RTP is awesome!');
}
rtp('get', 'visitor', callbackFunction);
```

セグメント一致を含む応答：

Get Visitor Data API 呼び出しの前に訪問者がリアルタイムセグメントと一致した場合に返される応答の例を以下に示します。

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

以下は、訪問者データの取得 API 呼び出し前に訪問者がリアルタイムセグメントと一致しなかった場合に返される応答の例です。

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
