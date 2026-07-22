---
title: ランディングページのリダイレクトルール
feature: REST API, Landing Pages
description: Marketo Asset REST APIを使用して、フィルター、ページネーション、ホスト名オプション、Marketo以外のターゲットを含むランディングページリダイレクトルールを作成、クエリ、更新、削除します。
exl-id: f63aa5ef-5872-4401-be75-6fb9b2977734
TQID: https://experienceleague.adobe.com/2gePbKA3xeoRdnL8mNnObN-GPTX00Ii4-zcM0lBjs-o
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 626
ht-degree: 28%

---

# ランディングページのリダイレクトルール

[ランディングページリダイレクトルールエンドポイントの参照](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules)

ランディングページリダイレクトルール REST APIを使用して、ランディングページリダイレクト URLのクエリ、作成、更新、削除を行います。

リダイレクトルールは、あるランディングページのURLを別のページのURLに送信します。 ソースと宛先は、MarketoまたはMarketo以外のページにすることができます。 関連製品ドキュメントについては、[Marketo Engage ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ja)を参照してください。

## クエリ

ランディングページのリダイレクトルール [をID](#by_id)または[閲覧](#browse)でクエリします。

### ID 別

ID[&#128279;](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRuleByIdUsingGET)による ランディングページ取得リダイレクトルール エンドポイントは、1つのリダイレクトルール `id` パスパラメーターを取り、一致するレコードを返します。

```http
GET /rest/asset/v1/redirectRule/{id}.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "3d0#1707b2521e4",
    "warnings": [],
    "result": [
        {
            "id": 20,
            "redirectFromUrl": "https://calqeauto.com/DefDelPro1_LandingPage1.html",
            "hostname": "calqeauto.com",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5483
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5559
            },
            "redirectToUrl": "https://calqeauto.com/DefDelPro1_LandingPage2.html",
            "createdAt": "2020-02-25T06:56:44Z+0000",
            "updatedAt": "2020-02-25T06:56:44Z+0000"
        }
    ]
}
```

### 参照

[&#x200B; ランディングページリダイレクトルールを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRulesUsingGET) エンドポイントは、ランディングページリダイレクトルールレコードを返します。

オプションのクエリパラメーターを使用して、結果をフィルタリングします。

`offset` パラメーターは、返されるエントリの最大数を指定する整数です（デフォルトは 20）。 最大値は 200 です。 `maxReturn` パラメーターは、エントリの取得を開始する場所を指定する整数です。 offset と併用できます（デフォルトは 0）。

`hostname` パラメーターは、ランディングページのホスト名でフィルタリングされます。

宛先ランディングページ IDによる`redirectToLandingPageId`整数フィルター。 `redirectToPath` パラメーターは、宛先ランディングページのパスでフィルタリングされます。

`earliestUpdatedAt`と`latestUpdatedAt`のパラメーターは、低い日時と高い日時の境界を設定します。 エンドポイントは、範囲内で作成または更新されたルールを返します。

```http
GET /rest/asset/v1/redirectRules.json&maxReturn=3
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "12213#1707b27efb5",
    "warnings": [],
    "result": [
        {
            "id": 5,
            "redirectFromUrl": "https://www.kirtideep.contact/LandingPage2.html",
            "hostname": "www.kirtideep.contact",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5406
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5404
            },
            "redirectToUrl": "https://www.kirtideep.contact/www.showLogs.com.html",
            "createdAt": "2019-11-14T06:26:29Z+0000",
            "updatedAt": "2019-11-14T06:26:29Z+0000"
        },
        {
            "id": 6,
            "redirectFromUrl": "https://www.kirtideep.contact/www.showLogs.com.html",
            "hostname": "www.kirtideep.contact",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5404
            },
            "redirectTo": {
                "type": "url",
                "value": "www.contactLogs.com"
            },
            "redirectToUrl": "www.contactLogs.com",
            "createdAt": "2019-11-14T06:27:10Z+0000",
            "updatedAt": "2019-11-14T06:27:10Z+0000"
        },
        {
            "id": 7,
            "redirectFromUrl": "https://www.kirtideep.contact/contact/log/check",
            "hostname": "www.kirtideep.contact",
            "redirectFrom": {
                "type": "path",
                "value": "/contact/log/check"
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5404
            },
            "redirectToUrl": "https://www.kirtideep.contact/www.showLogs.com.html",
            "createdAt": "2019-11-14T06:27:49Z+0000",
            "updatedAt": "2019-11-14T06:27:49Z+0000"
        }
    ]
}
```

## 作成

`application/x-www-form-urlencoded` POST リクエストを使用して、[&#x200B; ランディングページリダイレクトルールの作成](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/createLandingPageRedirectRuleUsingPOST) エンドポイントを呼び出します。 リクエストには3つの必須パラメーターがあります。

`hostname` パラメーターは、ランディングページのホスト名を指定します。 ブランディングドメインまたはエイリアスに属している必要があり、255文字を超えることはできません。

`redirectFrom` パラメーターは、ソース ランディングページを型と値のペアを持つJSON オブジェクトとして指定します。 `type`属性は、Marketo ランディングページの`landingPageId`またはMarketo以外のページの`path`にすることができます。

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| &#39;get&#39; | 必須 | 文字列 | メソッドアクション。 |
| &#39;visitor&#39; | 必須 | 文字列 | メソッド名。 |
| callback | 必須 | 関数 | 返されるキャンペーンごとにトリガーされるコールバック関数。 |

`redirectTo` パラメーターは、宛先を型と値のペアを持つJSON オブジェクトとして指定します。 `type`属性は、Marketo ランディングページの`landingPageId`またはMarketo以外のページの`url`にすることができます。

| ランディングページのタイプ | redirectTo タイプ | 例 |
| --- | --- | --- |
| Marketo | landingPageId | {&quot;type&quot;:&quot;landingPageId&quot;,&quot;value&quot;:&quot;1774&quot;} |
| Marketo 以外 | URL | {&quot;type&quot;:&quot;url&quot;,&quot;value&quot;:&quot;www.contactLogs.com&quot;} |

詳しくは、[Marketo ランディングページを別のページにリダイレクトする](https://experienceleague.adobe.com/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-actions/redirect-a-marketo-landing-page-to-another-page.html?lang=ja)を参照してください。

```http
POST /rest/asset/v1/redirectRules.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
hostname=calqeauto.com&redirectFrom={"type":"landingPageId", "value":"5483"}&redirectTo={"type":"landingPageId", "value":"5559"}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "d7c6#1707b223522",
    "warnings": [],
    "result": [
        {
            "id": 20,
            "redirectFromUrl": "https://calqeauto.com/DefDelPro1_LandingPage1.html",
            "hostname": "calqeauto.com",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5483
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5559
            },
            "redirectToUrl": "https://calqeauto.com/DefDelPro1_LandingPage2.html",
            "createdAt": "2020-02-25T06:56:44Z+0000",
            "updatedAt": "2020-02-25T06:56:44Z+0000"
        }
    ]
}
```

## アップデート

[&#x200B; ランディングページリダイレクトルールの更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/updateLandingPageRedirectRuleUsingPOST) エンドポイントは、1つのリダイレクトルール `id` パスパラメーターを取ります。 更新を`application/x-www-form-urlencoded` POST リクエストとして送信します。

更新する属性を選択するには、次の1つ以上のパラメーターを渡します：`hostname`、`redirectFrom`または`redirectTo`。

応答は、更新されたリダイレクトルールレコードを返します。

```http
POST /rest/asset/v1/redirectRule/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
redirectTo={"type":"landingPageId", "value":"5561"}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "57b2#1707b3852d7",
    "warnings": [],
    "result": [
        {
            "id": 20,
            "redirectFromUrl": "https://calqeauto.com/DefDelPro1_LandingPage1.html",
            "hostname": "calqeauto.com",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5483
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5561
            },
            "redirectToUrl": "https://calqeauto.com/DefDelPro1_LandingPage3.html",
            "createdAt": "2020-02-25T06:56:44Z+0000",
            "updatedAt": "2020-02-25T07:20:53Z+0000"
        }
    ]
}
```

## 削除

ID[&#128279;](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/deleteLandingPageRedirectRuleUsingPOST)による ランディングページリダイレクトルールの削除エンドポイントは、1つのリダイレクトルール `id` パスパラメーターを取ります。

```http
POST /rest/asset/v1/redirectRule/{id}/delete.json
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "d505#154d01c8364",
  "result": [
    {
      "id": 2
    }
  ]
}
```

## ランディングページのドメインの参照

[&#x200B; ランディングページドメインを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/getLandingPageDomainsUsingGET) エンドポイントは、ランディングページドメインレコードを返します。

2つのオプションのクエリパラメーターを使用して結果をフィルタリングします。

`offset` パラメーターは、返されるエントリの最大数を指定する整数です（デフォルトは 20、最大は 200）。

`maxReturn` パラメーターは、エントリの取得を開始する場所を指定する整数です。 `offset` と併用できます（デフォルトは 0）。

```http
POST /rest/asset/v1/landingPageDomains.json?maxReturn=3
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6eb8#1707b43d3cb",
    "warnings": [],
    "result": [
        {
            "hostname": "calqeauto.com",
            "type": "domain"
        },
        {
            "hostname": "www.google.com",
            "type": "domain-alias"
        },
        {
            "hostname": "www.kirti.com",
            "type": "domain-alias"
        }
    ]
}
```
