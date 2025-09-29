---
title: ランディングページのテンプレート
feature: REST API, Landing Pages
description: 自由形式およびガイド付きタイプの REST API エンドポイントを使用したMarketo ランディングページテンプレートの管理、ID または名前によるクエリ、HTMLの作成、更新、クローン、Munchkin。
exl-id: f9d1255e-ec13-4b75-96d5-b4cc9457a51b
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 95%

---

# ランディングページのテンプレート

[ランディングページのテンプレートエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates)

ランディングページのテンプレートは、個々の Marketo ランディングページの親リソースおよび依存関係です。ランディングページは、親テンプレートからコンテンツのスケルトンを派生します。

## テンプレートタイプ

Marketo には、フリーフォームとガイド付きの 2 つのタイプのランディングページのテンプレートがあります。フリーフォームのランディングページのテンプレートは、そのテンプレートから派生したページに対して大まかに構造化された編集エクスペリエンスを提供します。ガイド付きテンプレートは、要素のタイプと場所をテンプレートレベルで制限できる、高度に構造化されたエクスペリエンスを提供します。違いについて詳しくは、[このドキュメント](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/understanding-landing-pages/understanding-free-form-vs-guided-landing-pages)を参照してください。

## クエリ

ランディングページのテンプレートは、[ID 別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/getLandingPageTemplateByIdUsingGET)、[名前別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/getLandingPageTemplateByNameUsingGET)、[参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/getLandingPageTemplatesUsingGET)のアセットに対する標準クエリタイプをサポートします。これらのエンドポイントは、テンプレートのメタデータを返します。テンプレートの HTML コンテンツの取得は、テンプレートごとに ID を通じて実行する必要があります。

## 作成と更新

テンプレートは、関連付けられたメタデータを持つ空のアセットとして作成されます。テンプレートを作成する際は、名前とフォルダーに加えて、オプションの説明、templateType パラメーター、enableMunchkin パラメーターも含める必要があります。templateType は、freeform または guided のいずれかで、デフォルトは freeForm です。タイプ間の違いについては、「ガイド付きフォームとフリーフォーム」の節を参照してください。enableMunchkin のデフォルトは false です。有効にすると、テンプレートの子ランディングページで Munchkin トラッキングが実行されなくなります。

```
POST /rest/asset/v1/landingPageTemplates.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

テンプレートのコンテンツは、「[ランディングページのテンプレートコンテンツを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/updateLandingPageTemplateContentUsingPOST)」エンドポイント経由で個別に入力する必要があります。

### メタデータの更新

ランディングページのテンプレートのメタデータは、「[ランディングページのテンプレートメタデータを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/updateLpTemplateUsingPOST)」エンドポイント経由で更新できます。名前、説明、enableMunchkin 設定は、この方法で更新できます。

### コンテンツの更新

ランディングページのテンプレートのコンテンツは、HTML コンテンツ全体に対する破壊的な更新として作成されます。コンテンツは multipart/form-data として渡す必要があり、パラメーターは content という名前だけになります。

```
POST /rest/asset/v1/landingPageTemplate/286/content.json
```

```
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

```
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

Marketo には、ランディングページのテンプレートを複製するための簡単な方法が用意されています。これは、application/x-www-url-formencoded POST リクエストです。

`id` パスパラメーターは、複製するソースランディングページのテンプレートの ID を指定します。

`name` パラメーターは、新しいランディングページのテンプレートの名前を指定するために使用されます。

`folder` パラメーターは、新しいランディングページのテンプレートが存在する親フォルダーを指定するために使用されます。これは、`id` と `type` を含む埋め込み JSON オブジェクトの形式です。

オプションの `description` パラメーターは、新しいランディングページのテンプレートを説明するために使用されます。

```
POST /rest/asset/v1/landingPageTemplate/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

ランディングページのテンプレートは、ドラフトバージョンや承認済みバージョンを指定できる標準のドラフト承認済みモデルに従います。テンプレートに更新を適用するたびに、常に最初にドラフトバージョンに適用され、テンプレートが承認された場合にのみライブで表示されます。

テンプレートが承認されるには、ガイド付きまたはフリーフォームのいずれかのタイプのルールに準拠している必要があります。それぞれのタイプのテンプレートの作成と承認の要件について詳しくは、次のそれぞれの作成ドキュメントを参照してください。

- [フリーフォームランディングページのテンプレート](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-free-form-landing-page-template)
- [ガイド付きランディングページのテンプレート](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-guided-landing-page-template)
- [ガイド付きテンプレートの例](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/guided-landing-page-template-list)

## 削除

テンプレートを削除するには、そのテンプレートが未使用かつ未承認である必要があります。つまり、子ランディングページでそのテンプレートを参照できません。ソーシャルボタンが埋め込まれたランディングページのテンプレートは、この API では削除できません。
