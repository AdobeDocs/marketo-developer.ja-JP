---
title: ランディングページ
feature: REST API, Landing Pages
description: Marketo のランディングページのクエリを実行します。
exl-id: 2f986fb0-0a6b-469f-b199-1c526cd5a882
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '1000'
ht-degree: 100%

---

# ランディングページ

[ランディングページエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages)

ランディングページは、Marketo がホストする web ページです。

## クエリ

他のほとんどのアセットと同様に、ランディングページは[名前別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/getLandingPageByNameUsingGET)、[ID 別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/getLandingPageByIdUsingGET)および[参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/browseLandingPagesUsingGET)別にクエリを実行できます。これらのクエリは、メタデータのみを返します。ランディングページのコンテンツセクションのリストは、ランディングページの ID 別に個別にクエリを実行する必要があります。

ランディングページのコンテンツのクエリを実行すると、ランディングページで使用可能なコンテンツセクションのリストが返されます。コンテンツを更新するには、ページのコンテンツリストにセクションが存在している必要があります。

```
GET /rest/asset/v1/landingPage/{id}/content.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "6307#154ea1689d7",
    "result": [
        {
            "id": "67",
            "type": "Form",
            "index": 1,
            "content": {
                "content": "189",
                "contentType": "Form",
                "contentUrl": "https://app-devlocal1.marketo.com/#FO189A1ZN13LA1"
            },
            "formattingOptions": {
                "zIndex": 15,
                "left": "359px",
                "top": "122px"
            }
        }
    ]
}
```

ガイド付きランディングページには、派生元のテンプレートによって定義された一連のセクションが含まれていますが、フリーフォームページには事前定義済みのセクションが含まれておらず、編集前にコンテンツを追加する必要があるので、結果はガイド付きテンプレートとフリーフォームテンプレートで異なります。&quot;content&quot; 属性の形式は、&quot;content&quot; 属性と、フィールドが静的か動的かによって異なります。

## 作成と更新

[ランディングページ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/createLandingPageUsingPOST)は、テンプレートを参照して作成されます。作成に必要なフィールドは、名前、テンプレート（テンプレートの ID）およびページを配置するフォルダーのみです。入力できる追加のメタデーターについて詳しくは、エンドポイント参照を参照してください。

[ランディングページのコンテンツ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content)エンドポイントの有効なコンテンツタイプは、richText、HTML、Form、Image、Rectangle、Snippet です。

```
POST rest/asset/v1/landingPages.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=createLandingPage&folder={"type": "Folder", "id": 11}&template=1&description=this is a test&workspace=default&title=test create&keywords=awesome&formPrefill=false
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "7a39#154cf7922c6",
    "result": [
        {
            "id": 27,
            "name": "createLandingPage",
            "description": "this is a test",
            "createdAt": "2016-05-20T18:41:43Z+0000",
            "updatedAt": "2016-05-20T18:41:43Z+0000",
            "folder": {
                "type": "Folder",
                "value": 11,
                "folderName": "Landing Pages"
            },
            "workspace": "Default",
            "status": "draft",
            "template": 1,
            "title": "test create",
            "keywords": "awesome",
            "robots": "index, nofollow",
            "formPrefill": false,
            "mobileEnabled": false,
            "URL": "https://app-devlocal1.marketo.com/lp/622-LME-718/createLandingPage.html",
            "computedUrl": "https://app-devlocal1.marketo.com/#LP27B2"
        }
    ]
}
```

ランディングページのメタデータは、[「ランディングページのメタデータを更新」エンドポイント](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/updateLandingPageUsingPOST)を使用して更新できます。

## 承認

ランディングページは、ドラフトバージョンや承認済みバージョンを指定できる標準のドラフト承認済みモデルに従います。ページに更新を適用するたびに、常に最初にドラフトバージョンに適用され、ページが承認された場合にのみライブで表示されます。

## 削除

ランディングページを削除するには、まずそのページが使用されておらず、他の Marketo アセットによって参照されておらず、未承認である必要があります。ページは、[ランディングページを削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/deleteLandingPageByIdUsingPOST)エンドポイントを使用して個別に削除されます。ソーシャルボタンが埋め込まれたランディングページは、この API を通じて削除できません。

## 複製

Marketo には、ランディングページを複製するための簡単な方法が用意されています。これは、application/x-www-url-formencoded POST リクエストです。

`id` パスパラメーターは、複製するソースランディングページの ID を指定します。

`name` パラメーターは、新しいランディングページの名前を指定するために使用されます。

`folder` パラメーターは、新しいランディングページが作成される親フォルダーを指定するために使用されます。これは、`id` と `type` を含む埋め込み JSON オブジェクトの形式です。

`template` パラメーターは、ソースランディングページのテンプレート ID を指定するために使用されます。

オプションの `description` パラメーターは、新しいランディングページを説明するために使用されます。

```
POST /rest/asset/v1/landingPage/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=MyNewLandingPage&folder={"type":"Program","id":1119}&template=57
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "1078d#1683e4881c6",
    "warnings": [],
    "result": [
        {
            "id": 3291,
            "name": "MyNewLandingPage",
            "createdAt": "2019-01-11T18:59:25Z+0000",
            "updatedAt": "2019-01-11T18:59:25Z+0000",
            "folder": {
                "type": "Program",
                "value": 1119,
                "folderName": "DefaultProgramWithGuidedLP"
            },
            "workspace": "Default",
            "status": "draft",
            "template": 57,
            "robots": "index, nofollow",
            "formPrefill": false,
            "mobileEnabled": false,
            "URL": "http://na-abm.marketo.com/lp/284-RPR-133/DefaultProgramWithGuidedLPPerkutoTestLP-Clone-1.html",
            "computedUrl": "https://app-abm.marketo.com/#LP3291A1LA1"
        }
    ]
}
```

## コンテンツセクションの管理

コンテンツセクションはインデックスプロパティによって順序付けられ、最終的にはクライアントに表示される際に適用される CSS ルールに従ってレイアウトされます。コンテンツセクションは、対応する「ランディングページのコンテンツセクションの「[追加](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/addLandingPageContentUsingPOST)、[更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST)および[削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/removeLandingPageContentUsingPOST)」エンドポイントに含まれ、管理されており、[ランディングページのコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/getLandingPageContentUsingGET)を使用してクエリを実行できます。各セクションには、タイプと値のパラメーターがあります。タイプによって、値に何を入れる必要があるかが決まります。これらのエンドポイントの場合、データは、JSON ではなく、POST x-www-form-urlencoded として渡されます。

**セクションタイプ**

| タイプ | 値 |
|--- |--- |
| DynamicContent | セグメント化の ID。 |
| Form | フォームの ID。 |
| HTML | テキスト HTML コンテンツ。 |
| Image | 画像アセットの ID。 |
| Rectangle | 空。 |
| RichText | テキスト HTML コンテンツ。 リッチテキスト要素のみを含めることができます。 |
| スニペット | スニペットの ID。 |
| SocialButton | ソーシャルボタンの ID。 |
| Video | ビデオの ID。 |

フリーフォームページの場合、必要なすべてのコンテンツセクションを追加する必要があり、`mktoContent` という ID を持つ div 要素に埋め込まれます。 ガイド付きページの場合、[ランディングページのコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/getLandingPageContentUsingGET)エンドポイントからのリストに、事前定義済みの要素のリストが存在する場合があります。それぞれのエンドポイントを通じて、さらに追加したり、[コンテンツを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST)したりできます。

### 動的コンテンツ

動的コンテンツセクションを作成するには、このセクションがランディングページのコンテンツリストに既に存在している必要があります。次に、[ランディングページのコンテンツセクションを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST)エンドポイントを使用して、タイプを「DynamicContent」に設定する必要があります。セクションを動的コンテンツに設定すると、コンテンツセクション内に基になる動的セクションが作成され、これらのセクションはすべて変換元の要素の基本タイプを継承します。 また、各動的セクションは、変換されたセクションのコンテンツも継承します。

```
GET /rest/asset/v1/landingPage/{id}/dynamicContent/RVMtNDg=.json
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "46e#1560fa169d9",
  "result": [
    {
      "createdAt": "2016-07-21",
      "updatedAt": "2016-07-21",
      "segmentation": 1007,
      "segments": [
        {
          "segmentId": 1018,
          "segmentName": "Default",
          "type": "RichText",
          "content": "\n\t\t\t\t\t\t\tAlice was beginning to get very tired of sitting by her sister on the bank, and having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it.\n\t\t\t\t\t\t"
        },
        {
          "segmentId": 1017,
          "segmentName": "New Segment",
          "type": "RichText",
          "content": "\n\t\t\t\t\t\t\tAlice was beginning to get very tired of sitting by her sister on the bank, and having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it.\n\t\t\t\t\t\t"
        }
      ]
    }
  ]
}
```

個々のセグメントの[コンテンツの更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageDynamicContentUsingPOST)は、セグメント ID に基づいて行われます。

```
POST /rest/asset/v1/landingPage/{id}/dynamicContent/{dynamicContentId}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
segment=New Segment&value=New Content
```

```json
 {
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "7516#14e08fe7cbbc",
  "result": [
    {
      "id": 1012
    }
  ]
}
```

## 変数

ガイド付きランディングページに導入された機能の 1 つは、編集可能な変数です。変数には、ランディングページ上の要素の値が含まれます。変数は、以下に示すようにランディングページエディターを使用して簡単に変更できます。

![ランディングページの変数](assets/landing-page-variables.png)

変数は、ガイド付きモードのランディングページテンプレートの `<head>` 要素内のメタタグとして定義されます。使用できる変数には、文字列、色、ブール値の 3 つのタイプがあります。次に、3 つの変数定義の例を示します。

```html
<head>
  <meta charset="utf-8">
  <meta class="mktoString" mktoName="My String Variable" id="stringVar" default="Hello World!">
  <meta class="mktoColor" mktoName="My Color Variable" id="colorVar" default="#ffffff">
  <meta class="mktoBoolean" mktoName="My Boolean Variable" id="boolVar" default="true">
</head>
```

詳しくは、[ガイド付きランディングページテンプレートの作成](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-guided-landing-page-template)ドキュメントの「編集可能な変数」の節を参照してください。

### クエリ

ランディングページ ID を「ランディングページの変数を取得」エンドポイントに渡して、ガイド付きランディングページの変数を取得します。

```
GET /rest/asset/v1/landingPage/{id}/variables.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "10843#15a6d7e5fa1",
    "result": [
        {
            "id": "stringVar",
            "value": "Hello World!",
            "type": "string"
        },
        {
            "id": "colorVar",
            "value": "#FFFFFF",
            "type": "color"
        },
        {
            "id": "boolVar",
            "value": "true",
            "type": "boolean"
        }
    ]
}
```

この例では、ガイド付きランディングページに stringVar、colorVar、boolVar の 3 つの変数が含まれています。

### 更新

ランディングページ ID、変数 ID、変数値を「ランディングページの変数を更新」エンドポイントに渡して、ガイド付きランディングページの変数を更新します。

```
POST /rest/asset/v1/landingPage/{id}/variable/{variableId}.json?value={newValue}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "2b07#15a6db77da3",
    "result": [
        {
            "id": "stringVar",
            "value": "Hello Brave New World!",
            "type": "String"
        }
    ]
}
```

## ランディングページのプレビュー

Marketo には、ブラウザーでレンダリングされるランディングページのライブプレビューを取得するための[ランディングページの完全なコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/getLandingPageFullContentUsingGET)エンドポイントが用意されています。必須パラメーターが 1 つあります。プレビューするランディングページの ID である `id` パスパラメーターです。オプションのクエリパラメーターがさらに 2 つあります。

- segmentation：segmentationId 属性と segmentId 属性を含む JSON オブジェクトの配列を受け入れます。設定すると、これらのセグメントに一致するリードとしてランディングページをプレビューします。
- leadId：リードの整数 ID を受け入れます。設定すると、指定されたリードが表示したかのようにランディングページがプレビューされます。

```
GET /rest/asset/v1/landingPage/{id}/fullContent.json?leadId=1001&segmentation=[{"segmentationId":1030,"segmentId":1103}]
```

```json
{
  "success": true,
  "errors": [],
  "requestId": "119ab#17692849f1e",
  "warnings": [],
  "result": [
    {
      "id": 1023,
      "content": "<!DOCTYPE html>\n<html>\n <head>\n <meta charset=\"utf-8\">\n \n \n <meta name=\"robots\" content=\"index, nofollow\">\n <title></title>\n <style>\n body {background:#FFFFFF} \n #myConditionalDisplayArea {\n display: true;\n }\n </style>\n <link rel=\"shortcut icon\" href=\"/favicon.ico\" type=\"image/x-icon\" >\n<link rel=\"icon\" href=\"/favicon.ico\" type=\"image/x-icon\" >\n\n\n<style>.mktoGen.mktoImg {display:inline-block; line-height:0;}</style>\n </head>\n <body id=\"bodyId\">\n \n Hello Brave New World!\n <div class=\"mktoText\" id=\"exampleText\"><div>This is an example editable text area.</div>\n<div>Lead Full Name = Hanna Crawford</div>\n<div><br /></div>\n <script type=\"text/javascript\" src=\"//munchkin.marketo.net//munchkin.js\"></script><script>Munchkin.init('123-ABC-456', {customName: 'Test-Landing-Page-APIs_Guided-Landing-Page---deverly', PURL_VISIT_TOKEN, wsInfo: 'j1RR'});</script>\n<div id=\"mktoClickBlockingDiv\"></div>\n </body>\n</html>\n"
    }
  ]
}
```
