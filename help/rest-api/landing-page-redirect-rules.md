---
title: ランディングページのリダイレクトルール
feature: REST API, Landing Pages
description: Marketo Asset REST API を使用して、フィルター、ページネーション、ホスト名オプション、Marketo以外のターゲットを含むランディングページのリダイレクトルールを作成、クエリ、更新および削除します。
exl-id: f63aa5ef-5872-4401-be75-6fb9b2977734
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 96%

---

# ランディングページのリダイレクトルール

[ランディングページのリダイレクトルールエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules)

Marketo は、ランディングページのリダイレクト URL で CRUD 操作を実行する一連の REST API を備えています。これらの API は、クエリ、作成、更新、削除のオプションを提供するアセット API の標準インターフェイスパターンに従います。

ランディングページのリダイレクトルールは、ランディングページ URL を別のページ URL にリダイレクトする機能を提供します。Marketo ランディングページ、Marketo 以外のランディングページ、そしてこれらの組み合わせをリダイレクトできます。ランディングページのリダイレクトルールに関する情報について詳しくは、[こちら](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ja)を参照してください。

## クエリ

ランディングページのリダイレクトルールのクエリは、[ID 別](#by_id)および[参照](#browse)のアセットに対する標準のクエリタイプに従います。

### ID 別

[ID によるランディングページのリダイレクトルールを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRuleByIdUsingGET)エンドポイントは、単一のランディングページルールのリダイレクト `id` パスパラメーターを受け取り、単一のランディングページのリダイレクトルールレコードを返します。

```
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

[ランディングページのリダイレクトルールを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRulesUsingGET)エンドポイントは、ランディングページのリダイレクトルールレコードのリストを返します。

結果をフィルタリングするために渡すことができるオプションのクエリパラメーターがいくつかあります。

`offset` パラメーターは、返されるエントリの最大数を指定する整数です（デフォルトは 20）。最大値は 200 です。`maxReturn` パラメーターは、エントリの取得を開始する場所を指定する整数です。offset と併用できます（デフォルトは 0）。

`hostname` パラメーターを使用すると、ランディングページのホスト名をフィルタリングできます。

`redirectToLandingPageId` は、リダイレクト先のランディングページの ID をフィルタリングするために使用できる整数です。`redirectToPath` を使用すると、リダイレクト先のランディングページのパスに基づいてフィルタリングできます。

`earliestUpdatedAt` および `latestUpdatedAt` パラメーターを使用すると、指定した範囲内で更新されたか最初に作成されたランディングページのリダイレクトルールを返すための低および高の日時透かしを設定できます。

```
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

[ランディングページのリダイレクトルールを作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/createLandingPageRedirectRuleUsingPOST)エンドポイントは、次の 3 つの必須パラメーターを持つ application/x-www-form-urlencoded POST で実行されます。

`hostname` パラメーターは、ランディングページのホスト名を指定します。これは、ブランディングドメインまたはエイリアスに属している必要があります。最大長は 255 文字です。

`redirectFrom` パラメーターは、ソースランディングページを指定します。これは、ソースが Marketo ランディングページであるか、Marketo 以外のランディングページであるかを決定するタイプおよび値のペアを含む JSON オブジェクトです。`type` 属性は &quot;landingPageId&quot; または &quot;path&quot; のいずれかを指定できます。

| パラメーター | オプション／必須 | タイプ | 説明 |
|---|---|---|---|
| &#39;get&#39; | 必須 | 文字列 | メソッドアクション。 |
| &#39;visitor&#39; | 必須 | 文字列 | メソッド名。 |
| callback | 必須 | 関数 | 返されるキャンペーンごとにトリガーされるコールバック関数。 |

`redirectTo` パラメーターは、ターゲットランディングページを指定します。これは、ソースが Marketo ランディングページであるか、Marketo 以外のランディングページであるかを決定するタイプおよび値のペアを含む JSON オブジェクトです。`type` 属性は「landingPageId」または「url」のいずれかを指定できます。

| ランディングページのタイプ | redirectTo タイプ | 例 |
|---|---|---|
| Marketo | landingPageId | {&quot;type&quot;:&quot;landingPageId&quot;,&quot;value&quot;:&quot;1774&quot;} |
| Marketo 以外 | URL | {&quot;type&quot;:&quot;url&quot;,&quot;value&quot;:&quot;www.contactLogs.com&quot;} |

ランディングページのリダイレクトルールの作成について詳しくは、[こちら](https://experienceleague.adobe.com/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-actions/redirect-a-marketo-landing-page-to-another-page.html?lang=ja)を参照してください。

```
POST /rest/asset/v1/redirectRules.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

## 更新

[ランディングページのリダイレクトルールを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/updateLandingPageRedirectRuleUsingPOST)エンドポイントは、単一のランディングページのリダイレクトルール `id` パスパラメーターを受け取ります。このエンドポイントは、application/x-www-form-urlencoded POST で実行されます。

上記の作成呼び出しと同様に、更新するルールの属性を指定するのに、`hostname`、`redirectFrom`、`redirectTo` の 1 つ以上のクエリパラメーターが渡されます。

更新したランディングページのリダイレクトルールレコードが応答で返されます。

```
POST /rest/asset/v1/redirectRule/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

[ID によるランディングページのリダイレクトルールを削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/deleteLandingPageRedirectRuleUsingPOST)エンドポイントは、単一のランディングページのルールリダイレクト `id` パスパラメーターを受け取ります。

```
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

[ランディングページのドメインを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageDomainsUsingGET)エンドポイントは、ランディングページのドメインレコードのリストを返します。

結果をフィルタリングするのに渡すことができるオプションのクエリパラメーターが 2 つあります。

`offset` パラメーターは、返されるエントリの最大数を指定する整数です（デフォルトは 20、最大は 200）。

`maxReturn` パラメーターは、エントリの取得を開始する場所を指定する整数です。`offset` と併用できます（デフォルトは 0）。

```
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
