---
title: ランディングページのリダイレクトルール
feature: REST API, Landing Pages
description: API を使用したランディングページのリダイレクトルールの設定。
exl-id: f63aa5ef-5872-4401-be75-6fb9b2977734
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 4%

---

# ランディングページのリダイレクトルール

[ ランディングページリダイレクトルールエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules)

Marketoは、ランディングページのリダイレクト URL で CRUD 操作を実行するための一連の REST API を提供します。 これらの API は、クエリ、作成、更新、削除のオプションを提供するアセット API の標準インターフェイスパターンに従います。

ランディングページのリダイレクトルールは、ランディングページの URL を別のページの URL にリダイレクトする機能を提供します。 Marketoのランディングページ、Marketo以外のランディングページまたはそれらの組み合わせをリダイレクトできます。 リダイレクトランディングページルールに関する追加情報は、[ こちら ](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ja) を参照してください。

## クエリ

ランディングページのリダイレクトルールのクエリは、[id 別 ](#by_id) および [ 参照 ](#browse) のアセットの標準のクエリタイプに従います。

### Id 別

[ID によるランディングページリダイレクトルールの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRuleByIdUsingGET) エンドポイントは、パスパラメーター `id` とに 1 つのランディングページルールのリダイレクトを受け取り、1 つのランディングページリダイレクトルールレコードを返します。

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

[ ランディングページのリダイレクトルールの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRulesUsingGET) エンドポイントは、ランディングページのリダイレクトルールレコードのリストを返します。

結果をフィルタリングするためのオプションのクエリパラメーターがいくつか渡されています。

`offset` パラメーターは、返されるエントリの最大数を指定する整数です（デフォルトは 20）。 最大値は 200 です。 `maxReturn` パラメーターは、エントリの取得を開始する場所を指定する整数です。 offset と組み合わせて使用できます（デフォルトは 0）。

`hostname` パラメーターは、ランディングページのホスト名でフィルタリングするために使用できます。

`redirectToLandingPageId` は整数で、リダイレクト先のランディングページの ID に基づいてをフィルタリングするために使用できます。 この `redirectToPath` を使用して、リダイレクト先のランディングページのパスに基づいてフィルタリングできます。

`earliestUpdatedAt` パラメーターと `latestUpdatedAt` パラメーターを使用すると、指定された範囲内に更新または最初に作成されたランディングページリダイレクトルールを返すための低日時透かしと高日時透かしを設定できます。

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

[ ランディングページリダイレクトルールの作成 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/createLandingPageRedirectRuleUsingPOST) エンドポイントは、次の 3 つの必須パラメーターを持つ application/x-www-form-urlencoded POSTで実行されます。

`hostname` パラメーターは、ランディングページのホスト名を指定します。 これは、ブランディングドメインまたはエイリアスに属している必要があります。 最大長は 255 文字です。

`redirectFrom` パラメーターは、ソースランディングページを指定します。 これは、ソースがMarketo ランディングページかMarketo以外のランディングページかを判断するタイプと値のペアを含む JSON オブジェクトです。 `type` 属性は、「landingPageId」または「path」のいずれかです。

| パラメーター | オプション/必須 | タイプ | 説明 |
|---|---|---|---|
| &#39;get&#39; | 必須 | 文字列 | メソッドのアクション。 |
| &#39;訪問者&#39; | 必須 | 文字列 | メソッド名。 |
| callback | 必須 | 機能 | 返されるキャンペーンごとにトリガーされるコールバック関数。 |


`redirectTo` パラメーターは、ターゲットランディングページを指定します。 これは、ソースがMarketo ランディングページかMarketo以外のランディングページかを判断するタイプと値のペアを含む JSON オブジェクトです。 `type` 属性は、「landingPageId」または「url」のいずれかです。

| ランディングページのタイプ | redirectTo タイプ | 例 |
|---|---|---|
| Marketo | landingPageId | {&quot;type&quot;:&quot;landingPageId&quot;,&quot;value&quot;:&quot;1774&quot;} |
| 非Marketo | URL | {&quot;type&quot;:&quot;url&quot;,&quot;value&quot;:&quot;www.contactLogs.com&quot;} |

ランディングページのリダイレクトルールの作成について詳しくは [ こちら ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-actions/redirect-a-marketo-landing-page-to-another-page.html) を参照してください。

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

[ ランディングページのリダイレクトルールを更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/updateLandingPageRedirectRuleUsingPOST) エンドポイントは、パスパラメーターとして単一のランディングページのリダイレクトルール `id` 受け取ります。 このエンドポイントは、application/x-www-form-urlencoded POSTで実行されます。

前述の create 呼び出しと同様に、更新するルールの属性を指定する 1 つ以上のクエリパラメーター（`hostname`、`redirectFrom`、`redirectTo`）が渡されます。

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

[ID によるランディングページリダイレクトルールを削除 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/deleteLandingPageRedirectRuleUsingPOST) エンドポイントは、パスパラメーターを使用して 1 つのランディングページルール `id` リダイレクトを受け取ります。

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

[ ランディングページドメインを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageDomainsUsingGET) エンドポイントは、ランディングページドメインレコードのリストを返します。

結果をフィルタリングするためのオプションのクエリパラメーターが 2 つあります。

`offset` パラメーターは、返されるエントリの最大数を指定する整数です（デフォルトは 20、最大は 200）。

`maxReturn` パラメーターは、エントリの取得を開始する場所を指定する整数です。 `offset` と組み合わせて使用できます（デフォルトは 0）。

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
