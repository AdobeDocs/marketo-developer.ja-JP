---
title: 「ランディングページのリダイレクトルール」
feature: REST API, Landing Pages
description: 「API を使用したランディングページのリダイレクトルールの設定」
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 3%

---


# ランディングページのリダイレクトルール

[ランディングページリダイレクトルールエンドポイントのリファレンス](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules)

Marketoは、ランディングページのリダイレクト URL で CRUD 操作を実行するための一連の REST API を提供します。 これらの API は、クエリ、作成、更新、削除のオプションを提供するアセット API の標準インターフェイスパターンに従います。

ランディングページのリダイレクトルールは、ランディングページの URL を別のページの URL にリダイレクトする機能を提供します。 Marketoのランディングページ、Marketo以外のランディングページまたはそれらの組み合わせをリダイレクトできます。 リダイレクトランディングページルールに関する追加情報は、次のとおりです [こちら](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ja).

## クエリ

ランディングページのリダイレクトルールのクエリは、のアセットの標準のクエリタイプに従います [id 別](#by_id)、および [ブラウジング](#browse).

### Id 別

この [Id によるランディングページのリダイレクトルールの取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRuleByIdUsingGET) エンドポイントは、単一のランディングページルールリダイレクトを使用します `id` パスパラメーターで、単一のランディングページリダイレクトルールレコードを返します。

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

この [ランディングページのリダイレクトルールの取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRulesUsingGET) エンドポイントは、ランディングページリダイレクトルールレコードのリストを返します。

結果をフィルタリングするためのオプションのクエリパラメーターがいくつか渡されています。

この `offset` パラメーターは、返されるエントリの最大数を指定する整数です（デフォルトは 20）。 最大値は 200 です。 この `maxReturn` パラメータは、エントリの取得を開始する場所を指定する整数です。 offset と組み合わせて使用できます（デフォルトは 0）。

この `hostname` パラメーターを使用して、ランディングページのホスト名をフィルタリングできます。

この `redirectToLandingPageId` は、リダイレクト先のランディングページの ID に基づいてフィルタリングするために使用できる整数です。 この `redirectToPath` リダイレクト先のランディングページのパスに基づいてフィルタリングするために使用できます。

この `earliestUpdatedAt` および `latestUpdatedAt` パラメーターを使用すると、指定された範囲内で更新または最初に作成されたランディングページリダイレクトルールを返すための日時下限と上限の透かしを設定できます。

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

この [ランディングページのリダイレクトルールの作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/createLandingPageRedirectRuleUsingPOST) エンドポイントは、次の 3 つの必須パラメーターを持つ application/x-www-form-urlencoded POSTで実行されます。

この `hostname` パラメーターは、ランディングページのホスト名を指定します。 これは、ブランディングドメインまたはエイリアスに属している必要があります。 最大長は 255 文字です。

この `redirectFrom` パラメーターは、ソースランディングページを指定します。 これは、ソースがMarketo ランディングページかMarketo以外のランディングページかを判断するタイプと値のペアを含む JSON オブジェクトです。 この `type` 属性は、「landingPageId」または「path」のいずれかです。

| パラメーター | オプション/必須 | タイプ | 説明 |
|---|---|---|---|
| &#39;get&#39; | 必須 | 文字列 | メソッドのアクション。 |
| &#39;訪問者&#39; | 必須 | 文字列 | メソッド名。 |
| callback | 必須 | 機能 | 返されるキャンペーンごとにトリガーされるコールバック関数。 |


この `redirectTo` パラメーターは、ターゲットランディングページを指定します。 これは、ソースがMarketo ランディングページかMarketo以外のランディングページかを判断するタイプと値のペアを含む JSON オブジェクトです。 この `type` 属性は、「landingPageId」または「url」のいずれかです。

| ランディングページのタイプ | redirectTo タイプ | 例 |
|---|---|---|
| Marketo | landingPageId | {&quot;type&quot;:&quot;landingPageId&quot;,&quot;value&quot;:&quot;1774&quot;} |
| 非Marketo | URL | {&quot;type&quot;:&quot;url&quot;,&quot;value&quot;:&quot;www.contactLogs.com&quot;} |

ランディングページのリダイレクトルールの作成について詳しくは、こちらを参照してください [こちら](https://experienceleague.adobe.com/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-actions/redirect-a-marketo-landing-page-to-another-page.html).

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

この [ランディングページのリダイレクトルールを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/updateLandingPageRedirectRuleUsingPOST) エンドポイントは、単一のランディングページリダイレクトルールを使用 `id` パスパラメーター。 このエンドポイントは、application/x-www-form-urlencoded POSTで実行されます。

前述の create 呼び出しと同様に、次の 1 つ以上のクエリパラメーターが渡され、ルールの更新する属性が指定されます。 `hostname`, `redirectFrom`, `redirectTo`.

更新されたランディングページのリダイレクトルールレコードが応答で返されます。

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

この [Id によるランディングページリダイレクトルールの削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/deleteLandingPageRedirectRuleUsingPOST) エンドポイントは、単一のランディングページルールリダイレクトを使用します `id` パスパラメーター。

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

## ランディングページドメインの参照

この [ランディングページのドメインを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageDomainsUsingGET) エンドポイントは、ランディングページドメインレコードのリストを返します。

結果をフィルタリングするためのオプションのクエリパラメーターが 2 つあります。

この `offset` パラメーターは、返されるエントリの最大数を指定する整数です（デフォルトは 20、最大は 200）。

この `maxReturn` パラメータは、エントリの取得を開始する場所を指定する整数です。 と組み合わせて使用できます `offset` （デフォルトは 0）。

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
