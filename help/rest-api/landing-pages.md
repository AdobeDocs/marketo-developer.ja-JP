---
title: ランディングページ
feature: REST API, Landing Pages
description: Marketoのランディングページをクエリします。
exl-id: 2f986fb0-0a6b-469f-b199-1c526cd5a882
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 2%

---

# ランディングページ

[ ランディングページのエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages)

ランディングページは、Marketoがホストする web ページです。

## クエリ

他のほとんどのアセットと同様に、ランディングページのクエリ [ 名前別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/getLandingPageByNameUsingGET)、[ID 別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/getLandingPageByIdUsingGET)、[ 参照別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/browseLandingPagesUsingGET) が可能です。 これらのクエリはメタデータのみを返します。ランディングページのコンテンツセクションのリストは、ランディングページの ID によって個別にクエリする必要があります。

ランディングページのコンテンツをクエリすると、ランディングページで使用可能なコンテンツセクションのリストが返されます。 コンテンツを更新するには、ページのコンテンツリストにセクションが存在する必要があります。

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

ガイド付きランディングページには、派生元のテンプレートによって定義された一連のセクションが含まれるのに対して、フリーフォームページには事前定義済みのセクションが含まれておらず、編集する前にそのコンテンツを追加する必要があるので、結果はガイド付きフォームテンプレートとフリーフォームテンプレートで異なります。  「content」属性の形式は、「type」属性によって、またフィールドが静的か動的かによって異なる場合があります。

## 作成と更新

[ ランディングページは ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/createLandingPageUsingPOST) テンプレートを参照することで作成されます。 作成に必要なフィールドは、名前、テンプレート（テンプレートの ID）、ページを配置するフォルダーのみです。 入力できるその他のメタデータについては、エンドポイントのリファレンスを参照してください。

[ ランディングページコンテンツ ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content) エンドポイントとして有効なコンテンツタイプは、richText、HTML、フォーム、画像、長方形、スニペットです。

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

ランディングページのメタデータは、[ ランディングページメタデータの更新エンドポイント ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/updateLandingPageUsingPOST) で更新できます。

## 承認

ランディングページは、標準のドラフト承認済みモデルに従います。ドラフトバージョンや承認済みバージョンを指定できます。 ページに更新が適用されるたびに、常に最初にドラフトバージョンに適用され、ページが承認された場合にのみライブで表示されます。

## 削除

ランディングページを削除するには、まずそのページが使用されておらず、他のMarketo アセットから参照されていないこと、また承認されていないことが必要です。 ページは、「[ ランディングページを削除 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/deleteLandingPageByIdUsingPOST)」エンドポイントを使用して個別に削除されます。 ソーシャルボタンが埋め込まれたランディングページは、この API からは削除できません。 

## 複製

Marketoでは、ランディングページのクローンを作成する簡単な方法を提供しています。 これは、application/x-www-url-formencodedPOSTリクエストです。

`id` path パラメーターは、複製するソースランディングページの ID を指定します。

`name` パラメーターは、新しいランディングページの名前を指定するために使用されます。

`folder` パラメーターは、新しいランディングページが作成される親フォルダーを指定するために使用されます。 これは、`id` と `type` を含む埋め込み JSON オブジェクトの形式です。

`template` パラメーターは、ソースのランディングページテンプレート ID を指定するために使用されます。

オプションの `description` パラメーターは、新しいランディングページを記述するために使用されます。

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

## コンテンツ管理セクション

コンテンツセクションはインデックスプロパティ別に並べ替えられ、最終的には、クライアントで表示するときに適用される CSS ルールに従ってレイアウトされます。 コンテンツセクションは、対応する [ 追加 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/addLandingPageContentUsingPOST)、[ 更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST)、[ 削除 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/removeLandingPageContentUsingPOST) ランディングページコンテンツセクションのエンドポイントに含まれて管理され、[ ランディングページコンテンツを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/getLandingPageContentUsingGET) を使用してクエリできます。 各セクションには、type パラメーターと value パラメーターがあります。 型は、値に設定する対象を決定します。  これらのエンドポイントの場合、データは JSON ではなく、POST x-www-form-urlencoded として渡されます。

**断面タイプ**

| タイプ | 値 |
|--- |--- |
| DynamicContent | セグメント化の ID。 |
| フォーム | フォームの ID。 |
| HTML | テキストHTMLのコンテンツ。 |
| 画像 | 画像アセットの id。 |
| 長方形 | 空です。 |
| RichText | テキストHTMLのコンテンツ。  リッチテキスト要素のみを含めることができます。 |
| スニペット | スニペットの ID。 |
| SocialButton | の ID  「ソーシャル」ボタン。 |
| 動画 | ビデオの ID。 |

フリーフォームページの場合、必要なすべてのコンテンツセクションを追加する必要があります。これは、ID `mktoContent` の div 要素に埋め込まれます。 ガイド付きページの場合、事前定義済みの要素のリストが、[ ランディングページコンテンツを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/getLandingPageContentUsingGET) エンドポイントからのリストに表示されることがあります。 さらに追加したり、それぞれのエンドポイントを介して [ コンテンツを更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST) したりできます。

### 動的コンテンツ

動的コンテンツセクションを作成するには、そのセクションがランディングページのコンテンツリストに既に存在している必要があります。 次に、[ ランディングページコンテンツを更新セクション ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST) エンドポイントを使用して、タイプを「DynamicContent」に設定する必要があります。 セクションを動的コンテンツに設定すると、コンテンツセクション内に基づく動的セクションが作成され、すべてのセクションが変換後の要素のベースタイプを継承します。 また、各動的セクションは、変換後のセクションのコンテンツも継承します。

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

個々のセグメントの [ コンテンツの更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageDynamicContentUsingPOST) は、セグメント ID に基づいて行われます。

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

ガイド付きランディングページに導入された機能の 1 つは、編集可能な変数です。  変数には、ランディングページの要素の値が含まれます。  以下に示すように、ランディングページエディターを使用して、変数を簡単に変更できます。

![ ランディングページ変数 ](assets/landing-page-variables.png)

変数は、ガイド付きモードのランディングページテンプレート `<head>` 要素内のメタタグとして定義されます。 使用できる変数には、文字列、カラー、ブール値の 3 種類があります。  次に、3 つの変数定義の例を示します。

```html
<head>
  <meta charset="utf-8">
  <meta class="mktoString" mktoName="My String Variable" id="stringVar" default="Hello World!">
  <meta class="mktoColor" mktoName="My Color Variable" id="colorVar" default="#ffffff">
  <meta class="mktoBoolean" mktoName="My Boolean Variable" id="boolVar" default="true">
</head>
```

詳しくは、「ガイド付きランディングページテンプレートの作成 [ ドキュメントの「編集可能な変数」の節を参照し ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-guided-landing-page-template) ください。

### クエリ

ランディングページ ID を渡してランディングページ変数を取得エンドポイントにより、ガイド付きランディングページの変数を取得します。

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

対象：  この例では、ガイド付きランディングページには、stringVar、colorVar、boolVar の 3 つの変数が含まれています。

### 更新

ランディングページ ID、変数 ID および変数値を「ランディングページ変数を更新」エンドポイントに渡すことにより、ガイド付きランディングページの変数を更新します。

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

## ランディングページをプレビュー

Marketoは、ランディングページのライブプレビューをブラウザーでレンダリングされるとおりに取得するための [ ランディングページの完全なコンテンツを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/getLandingPageFullContentUsingGET) エンドポイントを提供します。 必須パラメーターが 1 つあります。`id` パスパラメーターは、プレビューするランディングページの ID です。 その他に 2 つのオプションのクエリパラメーターがあります。

- segmentation:segmentationId 属性と segmentId 属性を含む JSON オブジェクトの配列を受け入れます。 設定すると、ランディングページが、これらのセグメントに一致するリードであるかのようにプレビューされます。
- leadId:  リードの整数 ID を受け入れます。 設定すると、指定されたリードがランディングページを表示したかのようにプレビューされます。

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
