---
title: ランディングページのテンプレート
feature: REST API, Landing Pages
description: REST API エンドポイントを使用して、フリーフォームとガイド付きタイプのMarketoランディングページテンプレートを管理し、IDまたは名前によるクエリを実行して、HTMLを作成、更新し、複製、Munchkinを実行できます。
exl-id: f9d1255e-ec13-4b75-96d5-b4cc9457a51b
TQID: https://experienceleague.adobe.com/U9K1MG-q2gIgJMgfM3lt1S4olETt8ln9seOIKZUncBY
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 519
ht-degree: 20%

---

# ランディングページのテンプレート

[ランディングページテンプレートのエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates)

ランディングページテンプレートは、Marketo ランディングページの親リソースです。 各ランディングページは、親テンプレートから初期コンテンツ構造を導き出します。

## テンプレートタイプ

Marketoには、フリーフォームとガイド付きのランディングページテンプレートが用意されています。 自由形式テンプレートを使用すると、緩やかに構造化された編集体験を提供できます。 ガイド付きテンプレートを使用すると、テンプレートレベルでエレメントの種類と場所を制限できます。

詳細な比較については、[&#x200B; フリーフォームとガイド付きランディングページについて](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/understanding-landing-pages/understanding-free-form-vs-guided-landing-pages)を参照してください。

## クエリ

ランディングページテンプレート [をID](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/getLandingPageTemplateByIdUsingGET)で、[を名前](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/getLandingPageTemplateByNameUsingGET)で、または[閲覧](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/getLandingPageTemplatesUsingGET)でクエリします。 これらのエンドポイントは、テンプレートメタデータを返します。 IDでテンプレートごとにHTML コンテンツを個別に取得します。

## 作成と更新

テンプレートは、メタデータを含む空のアセットとして作成されます。 `name`および`folder` パラメーターが必要です。 `description`、`templateType`および`enableMunchkin` パラメーターはオプションです。

`templateType`の値は`freeform`または`guided`で、デフォルトは`freeForm`です。 `enableMunchkin`の値はデフォルトで`false`です。 有効にすると、テンプレートの子ランディングページでMunchkin トラッキングが実行されなくなります。

```http
POST /rest/asset/v1/landingPageTemplates.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=New LPT - PHP&folder={"id":12,"type":"Folder"}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "11b7#14dfe1e3bcf",
    "result": [
        {
            "id": 286,
            "name": "assetAPITest",
            "description": "test",
            "createdAt": "2015-06-16T20:45:03Z+0000",
            "updatedAt": "2015-06-16T20:45:03Z+0000",
            "url": "https://app-devlocal1.marketo.com/#LT286B2ZN12",
            "folder": {
                "type": "Folder",
                "value": 12,
                "folderName": "Templates"
            },
            "status": "draft",
            "workspace": "Default"
        }
    ]
}
```

[&#x200B; ランディングページテンプレートコンテンツの更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/updateLandingPageTemplateContentUsingPOST) エンドポイントを使用して、テンプレートコンテンツを個別に追加します。

### メタデータの更新

[&#x200B; ランディングページテンプレートのメタデータを更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/updateLpTemplateUsingPOST) エンドポイントを使用して、名前、説明または`enableMunchkin`設定を変更します。

### コンテンツの更新

テンプレートコンテンツを更新すると、既存のすべてのHTML コンテンツが置き換えられます。 `content` パラメーターに`multipart/form-data`として置換を渡します。

```http
POST /rest/asset/v1/landingPageTemplate/286/content.json
```

```html
content-type: multipart/form-data; boundary=--------------------------435851813185237176536801
----------------------------435851813185237176536801
Content-Disposition: form-data; name="content"; filename="content.txt"
Content-Type: text/plain

<html>
<head>
</head>
<body>
<div>Placeholder Content</div>
</body>
</html>
----------------------------435851813185237176536801--
```

```json
 {
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "7516#14e0dc60bbc",
  "result": [
    {
      "id": 286
    }
  ]
}
```

## 複製

`application/x-www-url-formencoded` POST リクエストを使用してランディングページテンプレートを複製します。

`id` パス パラメーターは、ソース ランディングページ テンプレートを指定します。

`name` パラメーターは、新しいランディングページテンプレートの名前を指定します。

`folder` パラメーターは、新しいテンプレートの親フォルダーを指定します。 `id`と`type`を含む埋め込みJSON オブジェクトとして渡します。

オプションの`description` パラメーターは、新しいテンプレートを説明します。

```http
POST /rest/asset/v1/landingPageTemplate/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=Standard Template Clone&folder={"type": "Folder", "id": 732}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "dee6#1683e9fd410",
    "warnings": [],
    "result": [
        {
            "id": 61,
            "name": "Standard Template Clone",
            "createdAt": "2019-01-11T20:34:48Z+0000",
            "updatedAt": "2019-01-11T20:34:48Z+0000",
            "url": "https://app-abm.marketo.com/#LT61B2ZN732",
            "folder": {
                "type": "Folder",
                "value": 732,
                "folderName": "Test LP Template Clone"
            },
            "status": "draft",
            "workspace": "Default",
            "templateType": "freeForm",
            "enableMunchkin": true
        }
    ]
}
```

## 承認

ランディングページテンプレートでは、標準のドラフトと承認済みモデルを使用します。 更新は最初にドラフトに適用され、テンプレートが承認された後にのみ公開されます。

承認する前に、テンプレートは、ガイド付き形式または自由形式の形式の要件を満たしている必要があります。 次のリソースを参照してください。

- [フリーフォームのランディングページテンプレート](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-free-form-landing-page-template)
- [ガイド付きランディングページテンプレート](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-guided-landing-page-template)
- [ガイド付きテンプレート例](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/guided-landing-page-template-list)

## 削除

テンプレートを削除するには、テンプレートが承認されておらず、子ランディングページがテンプレートを参照していないことを確認します。 このAPIを使用して、ソーシャルボタンが埋め込まれたランディングページテンプレートを削除することはできません。
