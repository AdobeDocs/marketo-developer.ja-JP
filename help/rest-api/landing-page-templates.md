---
title: 「ランディングページテンプレート」
feature: REST API, Landing Pages
description: ランディングページテンプレートの作成と編集。
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 1%

---


# ランディングページのテンプレート

[ランディングページテンプレートエンドポイントのリファレンス](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates)

ランディングページテンプレートは、個々のMarketo ランディングページの親リソースおよび依存関係です。 ランディングページは、親テンプレートからコンテンツのスケルトンを派生させます。

## テンプレートタイプ

Marketoには、自由形式とガイド付きの 2 種類のランディングページテンプレートがあります。 自由形式のランディングページテンプレートは、そのテンプレートから派生したページに対して、大まかに構造化された編集エクスペリエンスを提供します。 ガイド付きテンプレートは、要素のタイプと場所をテンプレートレベルで制限できる、高度に構造化されたエクスペリエンスを提供します。 違いについて詳しくは、 [このドキュメント](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/demand-generation/landing-pages/understanding-landing-pages/understanding-free-form-vs-guided-landing-pages).

## クエリ

ランディングページテンプレートは、のアセットに対する標準のクエリタイプをサポートしています。 [id 別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/getLandingPageTemplateByIdUsingGET), [名前別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/getLandingPageTemplateByNameUsingGET)、および [ブラウジング](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/getLandingPageTemplatesUsingGET). これらのエンドポイントは、テンプレートのメタデータを返します。 テンプレートのHTMLコンテンツの取得は、その ID を使用して、テンプレートごとに行う必要があります。

## 作成と更新

テンプレートは、関連するメタデータを持つ空のアセットとして作成されます。 テンプレートを作成するときは、名前とフォルダーを、オプションの説明、templateType および enableMunchkin パラメーターと共に含める必要があります。 templateType は、フリーフォームまたはガイド型のいずれかであり、デフォルトは freeForm です。 タイプの違いについては、ガイド付きフォームとフリーフォームの節を参照してください。 enableMunchkin はデフォルトで false に設定されています。これを有効にすると、テンプレートの子ランディングページで Munchkin のトラッキングが実行されなくなります。

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

テンプレートのコンテンツは、 [ランディングページテンプレートコンテンツを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/updateLandingPageTemplateContentUsingPOST) エンドポイント。

### メタデータを更新

ランディングページテンプレートのメタデータは、 [ランディングページテンプレートメタデータの更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/updateLpTemplateUsingPOST) エンドポイント。 名前、説明、enableMunchkin 設定は、この方法で更新できます。

### コンテンツを更新

ランディングページテンプレートのコンテンツは、破壊的なアップデートとしてHTMLコンテンツ全体に対して行われます。 コンテンツは、multipart/form-data として渡し、唯一のパラメーターに content という名前を付ける必要があります。

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

Marketoでは、ランディングページテンプレートのクローンを簡単に作成できます。 これは、application/x-www-url-formencodedPOSTリクエストです。

この `id` path パラメーターは、複製するソースランディングページテンプレートの ID を指定します。

この `name` パラメーターは、新しいランディングページテンプレートの名前を指定するために使用されます。

この `folder` パラメーターは、新しいランディングページテンプレートが存在する親フォルダーを指定するために使用されます。 これは、を含む埋め込み JSON オブジェクトの形式です。  `id` および `type`.

オプション `description` パラメーターは、新しいランディングページテンプレートを記述するために使用されます。

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

ランディングページテンプレートは、標準のドラフト承認済みモデルに従います。ここでは、ドラフトバージョンや承認済みバージョンを使用できます。 テンプレートに更新が適用されるたびに、常に最初にドラフトバージョンに適用され、テンプレートが承認された場合にのみライブで表示されます。

テンプレートが承認されるには、そのタイプのルール（自由形式のガイド付き）に従う必要があります。 それぞれのタイプのテンプレートを作成および承認するための要件について詳しくは、それぞれの作成ドキュメントを参照してください。

- [自由形式のランディングページテンプレート](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-free-form-landing-page-template)
- [ガイド付きランディングページテンプレート](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-guided-landing-page-template)
- [ガイドテンプレートの例](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/guided-landing-page-template-list)

## 削除

テンプレートを削除するには、そのテンプレートが未使用かつ未承認である必要があります。つまり、子ランディングページが参照することはできません。  ソーシャルボタンが埋め込まれたランディングページテンプレートは、この API では削除できません。
