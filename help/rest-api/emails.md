---
title: メール
feature: REST API
description: Marketo Asset REST APIを使用して、ID、名前、フォルダー参照ごとにメールアセットをクエリおよび管理する方法と、予測コンテンツとA/B テストの制限に関するメモを確認する方法について説明します。
exl-id: 6875730d-c74a-42cf-a3d2-dad7a3ac535d
TQID: https://experienceleague.adobe.com/t2FyPbwS836MvOe5rL0rVS7ibtzzZMmXwmgHBDZEr8Q
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399id: e64968b2-4ee5-47f9-8cae-0588f184b9ebid: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1813
ht-degree: 9%

---

# メール

[メールエンドポイントの参照](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails)

メール REST エンドポイントを使用して、メールアセットをクエリおよび管理します。

メールに[Marketo Predictive Content](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/predictive-content/working-with-predictive-content/understanding-predictive-content)が含まれている場合、次のエンドポイントはエラーコード 709と対応するエラーメッセージで失敗します。

- [メールコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailContentByIdUsingGET)
- [メールコンテンツセクションを更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailComponentContentUsingPOST)
- [メールのドラフトを承認](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/approveDraftUsingPOST)

## クエリ

メールでは、テンプレートと同じクエリパターンがサポートされています。例：[ID](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailByIdUsingGET)、[名前](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailByNameUsingGET)、および[閲覧](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailUsingGET)。 名前指定エンドポイントと参照エンドポイントは、フォルダーフィルタリングもサポートしています。

メールが[A/B テスト ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/email-programs/email-program-actions/email-test-a-b-test/add-an-a-b-test)を使用するメールプログラムに属している場合、次のエンドポイントはそのメールを返しません。

- [IDでメールを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailByIdUsingGET)
- [名前によるメールを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailByNameUsingGET)
- [メールを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailUsingGET)

呼び出しは成功を示しますが、警告`No assets found for the given search criteria.`が含まれています

### ID 別

```http
GET /rest/asset/v1/email/1351.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"9ad0#14a1832af8c",
   "result":[
      {
         "id":1356,
         "name":"sakZxhxkwV",
         "description":"sample description",
         "createdAt":"2014-12-05T02:06:21Z+0000",
         "updatedAt":"2014-12-05T02:06:21Z+0000",
         "subject":{
            "type":"Text",
            "value":"sample subject"
         },
         "fromName":{
            "type":"Text",
            "value":"RBxEtmdQZz"
         },
         "fromEmail":null,
         "replyEmail":{
            "type":"Text",
            "value":"Qlikf@testmail.com"
         },
         "folder":{
            "type":"folder",
            "value":10421
         },
         "operational":false,
         "textOnly":false,
         "publishToMSI":false,
         "webView":false,
         "status":false,
         "template":338,
         "workspace":"Default",
         "isOpenTrackingDisabled": false,
         "version": 2,
         "autoCopyToText": true,
         "ccFields": [
            {
              "attributeId": "157",
              "objectName": "lead",
              "displayName": "Lead Owner Email Address",
              "apiName": null
            }
          ],
         "preHeader": "My awesome preheader!"
      }
   ]
}
```

### 名前別

名前でクエリする場合は、オプションでフォルダーを渡して、そのフォルダーに検索を制限します。

```http
GET /rest/asset/v1/email/byName.json?name=My Email&folder={"id":1056,"type"="Folder"}
```

```json
{
   "success":true,
   "warnings":[
   ],
   "errors":[
   ],
   "requestId":"3a7f#14c484de875",
   "result":[
      {
         "id":1032,
         "name":"My Email",
         "description":"eCjxjIHmYPLtecoSphkvIXlrygOBDLhgyQKnsKMpiKWgSCKhkPMUFvFPUvEylmFiLjQGnffXGaiNLxAwiFOmIDvxEINoaSYascJw",
         "createdAt":"2015-03-23T20:23:25Z+0000",
         "updatedAt":"2015-03-23T20:23:25Z+0000",
         "subject":{
            "type":"Text",
            "value":"ezyKBmDcyCcUIrXASrLSvRuWQgWpRZxQstJoStgMSLEBASGKMpAnVeWrgJsaVFoFJUEXhEIPpDAWpzajzingUruFpiMcRRwtoBzU"
         },
         "fromName":{
            "type":"Text",
            "value":"dAiqRNJOdY"
         },
         "fromEmail":{
            "type":"Text",
            "value":"ilZxG@testmail.com"
         },
         "replyEmail":{
            "type":"Text",
            "value":"VYsCS@testmail.com"
         },
         "folder":{
            "type":"folder",
            "value":1056
         },
         "operational":false,
         "textOnly":false,
         "publishToMSI":false,
         "webView":false,
         "status":"draft",
         "template":32,
         "workspace":"Default",
         "isOpenTrackingDisabled": false,
        "version": 2,
         "autoCopyToText": true,
         "ccFields": [
            {
              "attributeId": "157",
              "objectName": "lead",
              "displayName": "Lead Owner Email Address",
              "apiName": null
            }
          ],
         "preHeader": "My awesome preheader!"
      }
   ]
}
```

### 参照

メールのブラウジングは、標準のAsset API パターンに従い、次のオプションのフィルターをサポートしています。

- `status`: `Approved`または`Draft`のいずれか。
- `folder`: `id`と`type`を含むJSON オブジェクト。
- `earliestUpdatedAt`と`latestUpdatedAt`：更新時間範囲。
- `maxReturn`：返される結果の数。 デフォルトは20、最大は200です。
- `offset`: `maxReturn`と連携して、大きな結果セットをページ表示できます。 デフォルトは0です。

```http
GET /rest/asset/v1/emails.json?maxReturn=3&folder={"id":341,"type":"Folder"}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "17576#14e22eb29cb",
    "result": [
        {
            "id": 2137,
            "name": "Social Sharing in Email",
            "description": "",
            "createdAt": "2011-03-04T17:12:42Z+0000",
            "updatedAt": "2011-03-04T19:04:36Z+0000",
            "url": null,
            "subject": {
                "type": "Text",
                "value": "Republish this content to your favorite social site!"
            },
            "fromName": {
                "type": "Text",
                "value": "Demo Master Marketo"
            },
            "fromEmail": {
                "type": "Text",
                "value": "demomaster@marketo.com"
            },
            "replyEmail": {
                "type": "Text",
                "value": "demomaster@marketo.com"
            },
            "folder": {
                "type": "Folder",
                "value": 341,
                "folderName": "Social Media"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": true,
            "status": "approved",
            "template": null,
            "workspace": "Default",
            "isOpenTrackingDisabled": false,
            "version": 2,
            "autoCopyToText": true,
            "ccFields": [
               {
                 "attributeId": "157",
                 "objectName": "lead",
                 "displayName": "Lead Owner Email Address",
                 "apiName": null
               }
             ],
            "preHeader": "My awesome preheader!"
        }
    ]
}
```

## クエリコンテンツ

[ メールの編集可能なセクションを取得するには](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailContentByIdUsingGET)、そのコンテンツをクエリします。 オプションでステータスでフィルタリングして、承認済みバージョンまたはドラフトバージョンからセクションを返します。

```http
GET /rest/asset/v1/email/1356/content.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"8a44#14c484de8c8",
   "result":[
      {
         "htmlId":"edit_text_3",
         "value":[
            {
               "type":"HTML",
               "value":"Content from testCreateEmailTemplate2"
            },
            {
               "type":"Text",
               "value":"Content from testCreateEmailTemplate2"
            }
         ],
         "contentType":"Text"
      }
   ]
}
```

セクションのタイプは`dynamicContent`です。 詳しくは、[動的コンテンツ ](dynamic-content.md)を参照してください。

## CC フィールドのクエリ

[電子メール CC フィールドを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailCCFieldsUsingGET) エンドポイントを呼び出して、ターゲットインスタンスで電子メール CCに対して有効なフィールドを取得します。

```http
GET /rest/asset/v1/email/ccFields.json
```

```json
{
   "success":true,
   "errors":[ ],
   "requestId":"e54b#16796fdbd4e",
   "warnings":[ ],
   "result":[
      {
         "attributeId":"157",
         "objectName":"lead",
         "displayName":"Lead Owner Email Address",
         "apiName":"leadOwnerEmailAddress"
      },
      {
         "attributeId":"396",
         "objectName":"company",
         "displayName":"Account Owner Email Address",
         "apiName":"accountOwnderEmailAddress"
      }
   ]
}
```

## 作成と更新

[ ソーステンプレートからメール ](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/createEmailUsingPOST)を作成します。 メールの編集可能なセクションは、`mktEditable` クラスと一意の`id` プロパティを持つテンプレートのHTML要素から取得されます。

メールを作成の呼び出しには、次のパラメーターが必要です。

- `name`: メール名。
- `template`: ソーステンプレート。
- `folder`：親フォルダー。

オプションの作成パラメーターは`subject`、`fromName`、`fromEmail`、`replyEmail`、`operational`および`isOpenTrackingDisabled`です。 これらのパラメーターを省略すると、次のデフォルトが適用されます。

- `subject`は空です。
- `fromName`、`fromEmail`および`replyEmail`は、インスタンスのデフォルトを使用します。
- `operational`と`isOpenTrackingDisabled`は`false`です。

`isOpenTrackingDisabled` パラメーターは、送信された電子メールにオープントラッキングピクセルが含まれているかどうかを判断します。

```http
POST /rest/asset/v1/emails.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=My New Email 02 - deverly&folder={"id":1017,"type":"Program"}&template=24&description=This is a test email&subject=Hey There&fromName=SomeBody&fromEmail=somebody@marketo.com&replyEmail=somebody@marketo.com
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "f557#14e22db88d9",
    "result": [
        {
            "id": 2212,
            "name": "My New Email 02 - deverly",
            "description": "This is a test email",
            "createdAt": "2015-06-23T23:58:09Z+0000",
            "updatedAt": "2015-06-23T23:58:09Z+0000",
            "url": "https://app-abm.marketo.com/#EM2212A1LA1",
            "subject": {
                "type": "Text",
                "value": "Hey There"
            },
            "fromName": {
                "type": "Text",
                "value": "SomeBody"
            },
            "fromEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "replyEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "folder": {
                "type": "Program",
                "value": 1017,
                "folderName": "Landing Page - promotion"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": false,
            "status": "draft",
            "template": 24,
            "workspace": "Default",
            "isOpenTrackingDisabled": false,
            "version": 2,
            "autoCopyToText": false,
            "ccFields": null,
            "preHeader": null
        }
    ]
}
```

[ メールを更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailContentUsingPOST)するには、そのIDを渡して、メールの説明または名前を更新します。

```http
POST /rest/asset/v1/email/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
description=This is an Email&name=Updated Email
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "f557#14e22db88d9",
    "result": [
        {
            "id": 2212,
            "name": "Updated Email",
            "description": "This is an Email",
            "createdAt": "2015-06-23T23:58:09Z+0000",
            "updatedAt": "2015-06-23T23:58:09Z+0000",
            "url": "https://app-abm.marketo.com/#EM2212A1LA1",
            "subject": {
                "type": "Text",
                "value": "Hey There"
            },
            "fromName": {
                "type": "Text",
                "value": "SomeBody"
            },
            "fromEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "replyEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "folder": {
                "type": "Program",
                "value": 1017,
                "folderName": "Landing Page - promotion"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": false,
            "status": "draft",
            "template": 24,
            "workspace": "Default",
            "isOpenTrackingDisabled": false,
            "version": 2,
            "autoCopyToText": false,
            "ccFields": null,
            "preHeader": null
        }
    ]
}
```

### コンテンツセクション、タイプ、更新

各メールコンテンツセクションを個別に更新します。 [ メールコンテンツの更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailContentUsingPOST) エンドポイントを使用して、`subject`、`fromName`、`fromEmail`および`replyEmail`を更新します。 このエンドポイントでは、これらの値を設定して、静的コンテンツの代わりに動的コンテンツを使用することもできます。

各パラメーターは、型/値のJSON オブジェクトです。 型は`Text`または`DynamicContent`です。 値は、対応するテキストまたは動的コンテンツに使用されるセグメント化のIDです。 データをJSONではなく`application/x-www-form-urlencoded`を使用したPOSTとして送信します。 `isOpenTrackingDisabled`をメール コンテンツの更新で設定することもできます。

```http
POST /rest/asset/v1/email/{id}/content.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
subject={"type":"Text","value":"Gettysburg Address"}&fromEmail={"type":"Text","value":"abe@testmail.com"}&fromName={"type":"Text","value":"Abe Lincoln"}&replyTO={"type":"Text","value":"replies@testmail.com"}
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"c865#14a1832afac",
   "result":[
      {
         "id":1356
      }
   ]
}
```

動的コンテンツを使用するようにセクションを設定するには、まずメールコンテンツを取得でセクション IDを取得します。

### 編集可能なセクションの更新

編集可能セクションを`htmlId`で更新します。 電子メール `id`とセクション `htmlId`は必須のパス パラメーターです。 `type`、`value`および`textValue` パラメーターはオプションです。

`type`が`value`の内容を決定します：

- `Text`: `value`は、セクションのHTML コンテンツを含む文字列です。
- `DynamicContent`: `value`は、`type`が`DynamicContent`に設定され、`segmentation`がセグメント IDに設定され、`default`がデフォルトのHTML コンテンツに設定されているJSON オブジェクトです。
- `Snippet`：サポートされているセクションタイプ。

オプションの`textValue` パラメーターには、セクションのテキストバージョンが含まれています。 データをJSONではなく`application/x-www-form-urlencoded`を使用したPOSTとして送信します。

```http
POST /rest/asset/v1/email/{id}/content/{htmlId}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
type=Text&value=<h1>Hello World!</h1>&textValue=Hello World!
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "155ac#14d58dfa9ad",
    "result": [
        {
            "id": 2179
        }
    ]
}
```

埋め込みスニペットで「テキストに自動コピー」が無効になっている場合、スニペットのHTMLを更新してから別のセクションのテキストバージョンを更新すると、更新されたスニペットのHTMLがメールテキストバージョンに反映されます。 自動コピーが無効になっている場合、以前のスニペットテキストは想定どおりに保持されません。

## モジュール

メールエディター1.0では、モジュールはテンプレートで定義されたメールセクションです。 モジュールには、[電子メールテンプレートの構文](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Modules)で説明されているように、エレメント、変数、およびその他のHTML コンテンツを含めることができます。

モジュール APIを使用して、メール内のモジュールを管理します。 HTTP POSTを使用するモジュールエンドポイントの場合、リクエスト本文をJSONではなく`application/x-www-form-urlencoded`としてフォーマットします。

ほとんどのモジュールエンドポイントでは、パスパラメーターとして`moduleId`が必要です。 [電子メールコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailContentByIdUsingGET) エンドポイントは、`htmlId`属性のモジュール IDを返します。 [ クエリ ](#modules_query)を参照してください。

### クエリ

モジュールを操作するには、モジュールを一意に識別する`moduleId`を指定します。 また、メール内のモジュールの順序を説明する整数モジュールインデックスが必要になる場合もあります。

[ モジュール IDとそのインデックス ](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailContentByIdUsingGET)を取得するには、電子メール IDをパスパラメーターとして指定します。

次の例では、テンプレートピッカーUIの「スターターテンプレート」セクションの`Skeleton` テンプレートに基づいて1.0 メールをクエリします。

```http
GET /rest/asset/v1/email/{moduleId}/content.json
```

```json
{
  "success": true,
  "warnings": [ ],
  "errors": [ ],
  "requestId": "3d79#158da6492bd",
  "result": [
    {
      "htmlId": "free-image",
      "contentType": "Module",
      "index": 1,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "single",
      "value": {
        "width": "600",
        "altText": "",
        "style": "-ms-interpolation-mode: bicubic; outline: none; border-right-width: 0; border-bottom-width: 0; border-left-width: 0; text-decoration: none; border-top-width: 0; display: block; max-width: 100%; line-height: 100%; height: auto; width: 600px"
      },
      "contentType": "Image",
      "parentHtmlId": "free-image",
      "isLocked": false
    },
    {
      "htmlId": "video",
      "contentType": "Module",
      "index": 2,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "video2",
      "value": {

      },
      "contentType": "Video",
      "parentHtmlId": "video",
      "isLocked": false
    },
    {
      "htmlId": "free-text",
      "contentType": "Module",
      "index": 3,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "text",
      "value": [
        {
          "type": "HTML",
          "value": "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Harum officiis dolorum, nulla, mollitia ducimus iure modi perferendis tenetur ea illum veniam aut sapiente deserunt repellendus. Excepturi illo numquam sint harum."
        },
        {
          "type": "Text",
          "value": "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Harum officiis dolorum, nulla, mollitia ducimus iure modi perferendis tenetur ea illum veniam aut sapiente deserunt repellendus. Excepturi illo numquam sint harum."
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "free-text",
      "isLocked": false
    },
    {
      "htmlId": "two-articles",
      "contentType": "Module",
      "index": 6,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "article3",
      "value": {
        "height": "auto",
        "width": "270",
        "style": "-ms-interpolation-mode: bicubic; outline: none; border-right-width: 0; border-bottom-width: 0; border-left-width: 0; text-decoration: none; border-top-width: 0; display: block; max-width: 100%; line-height: 100%; height: auto; width: 270px"
      },
      "contentType": "Image",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "articleTitle",
      "value": [
        {
          "type": "HTML",
          "value": "LOREM IPSUM DOLOR SIT AMET"
        },
        {
          "type": "Text",
          "value": "LOREM IPSUM DOLOR SIT AMET"
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "text2",
      "value": [
        {
          "type": "HTML",
          "value": "Gumbo beet greens corn soko endive gumbo gourd. shallot courgette tatsoi pea sprouts fava bean collard greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini."
        },
        {
          "type": "Text",
          "value": "Gumbo beet greens corn soko endive gumbo gourd. shallot courgette tatsoi pea sprouts fava bean collard greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini."
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "article4",
      "value": {
        "height": "auto",
        "width": "270",
        "style": "-ms-interpolation-mode: bicubic; outline: none; border-right-width: 0; border-bottom-width: 0; border-left-width: 0; text-decoration: none; border-top-width: 0; display: block; max-width: 100%; line-height: 100%; height: auto; width: 270px"
      },
      "contentType": "Image",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "articleTitle2",
      "value": [
        {
          "type": "HTML",
          "value": "LOREM IPSUM DOLOR SIT AMET"
        },
        {
          "type": "Text",
          "value": "LOREM IPSUM DOLOR SIT AMET"
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "text3",
      "value": [
        {
          "type": "HTML",
          "value": "Gumbo beet greens corn soko endive gumbo gourd. shallot courgette tatsoi pea sprouts fava bean collard greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini."
        },
        {
          "type": "Text",
          "value": "Gumbo beet greens corn soko endive gumbo gourd. shallot courgette tatsoi pea sprouts fava bean collard greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini."
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "footer",
      "contentType": "Module",
      "index": 7,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "footerText",
      "value": [
        {
          "type": "HTML",
          "value": "<p style=\"text-align: center;\"><span style=\"color: #333333;\"><strong>Acme, Inc<\/strong><\/span><\/p> \n<div style=\"text-align: center;\">\n  You received this because you have subscribed to our newsletter. Click \n <a href=\"{{system.unsubscribeLink}}\" target=\"_blank\" class=\"mktNoTrack\">here<\/a> to unsubscribe. \n <br> \n<\/div>"
        },
        {
          "type": "Text",
          "value": "Acme, Inc \n You received this because you have subscribed to our newsletter. Click here <{{system.unsubscribeLink}}> to unsubscribe."
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "footer",
      "isLocked": false
    },
    {
      "htmlId": "spacer",
      "contentType": "Module",
      "index": 0,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "CTA",
      "contentType": "Module",
      "index": 4,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "hr",
      "contentType": "Module",
      "index": 5,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    }
  ]
}
```

結果の配列には、モジュールとHTMLの両方のエレメントの説明が含まれます。 モジュール要素には`contentType`/`Module`があり、`index`が含まれています。 `htmlId`属性に`moduleId`が含まれています。

`Skeleton`の例では、次の表は、各`moduleId`をメール内のインデックスにマッピングします。

| moduleId（htmlId とも呼ばれる） | インデックス |
| --- | --- |
| spacer | 0 |
| free-image | 1 |
| video | 2 |
| free-text | 3 |
| CTA | 4 |
| hr | 5 |
| two-articles | 6 |
| footer | 7 |

#### 追加

モジュール ](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/addModuleUsingPOST)を[追加するには、メールのテンプレートから既存のモジュールを選択します。 電子メール IDと`moduleId`をパスパラメーターとして指定します。 必須の`index` クエリパラメーターによって、モジュールの位置が決まります。 `index`が既存の最大インデックスを超える場合、APIはモジュールをメールに追加します。

```http
POST /rest/asset/v1/email/{id}/content/{moduleId}/add.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
index=10
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "1063e#158d6ad2c3f",
    "result": [
        {
            "id": 1028
        }
    ]
}
```

#### 削除

モジュール ](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/deleteModuleUsingPOST)を[削除するには、電子メール IDと`moduleId`をパスパラメーターとして指定します。

```http
POST /rest/asset/v1/email/{id}/content/{moduleId}/delete.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "2356#158d6f6104a",
    "result": [
        {
            "id":1028
        }
    ]
}
```

#### 複製

モジュール ](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/duplicateModuleUsingPOST)を[複製するには、電子メール IDと`moduleId`をパスパラメーターとして指定します。 APIは、複製を元のモジュールの下に配置し、残りのモジュールを下に移動します。

```http
POST /rest/asset/v1/email/{id}/content/{moduleId}/duplicate.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "e740#158d705d967",
    "result": [
        {
            "id":1028
        }
    ]
}
```

#### 並べ替え

[ モジュールを並べ替え](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/rearrangeModulesUsingPOST)するには、すべてのモジュールとその目的の位置を含む配列を送信します。 各配列要素は、フォーム `{ "index": <_index_>, "moduleId": "<_moduleId_>" }`のJSON オブジェクトです。`<_index_>`はゼロ ベースのモジュール位置で、`<_moduleId_>`はモジュール IDです。

```http
POST /rest/asset/v1/email/{id}/content/rearrange.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
positions=[ {"index": 0, "moduleId": "free-image"}, {"index": 1, "moduleId": "title"}, {"index": 2, "moduleId": "mkvideo"}, {"index": 3, moduleId": "free-text"}, {"index": 4, "moduleId": "blankSpace"}, {"index": 5, "moduleId": "Separator"}, {"index": 6, "moduleId": "callToAction"}, {"index": 7, "moduleId": "blankSpace2"}, {"index": 8, "moduleId": "blankSpace3"} ]
```

```json
{
    "success": true,
    "warnings":[ ],
    "errors":[ ],
    "requestId": "e67a#158d72d1cde",
    "result":[
        {
            "id": 1030
        }
    ]
}
```

#### 名前変更

モジュール ](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/renameUsingPOST)の名前を[変更するには、`name` パラメーターに新しい名前を渡します。 電子メール IDと既存の`moduleId`をパスパラメーターとして指定します。

```http
POST /rest/asset/v1/email/{id}/content/{moduleId}/rename.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=MarketoVideo
```

```json
{
    "success": true,
    "warnings":[ ],
    "errors": [ ],
    "requestId":"11521#158d740abc0",
    "result": [
        {
            "id": 1030
        }
    ]
}
```

## 変数

メールエディター1.0では、変数はメール要素の値を保存します。 [電子メールテンプレートの構文](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Variables)の説明に従って、HTMLにMarketo固有の構文を追加して、各変数を定義します。 変数APIを使用して、メール内の変数を管理します。

### クエリ

[変数を取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailVariablesUsingGET)するには、電子メール IDをパスパラメーターとして指定します。

次の例では、テンプレートピッカーUIの「スターターテンプレート」セクションの`Skeleton` テンプレートに基づいて1.0 メールをクエリします。

```http
GET /rest/asset/v1/email/{id}/variables.json
```

```json
{
  "success": true,
  "warnings": [ ],
  "errors": [  ],
  "requestId": "756#158dade55e8",
  "result": [
    {
      "name": "twoArticlesSpacer5",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer6",
      "value": "15",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "footerSpacer2",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer7",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "twoArticlesLinkText2",
      "value": "CALL TO ACTION",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer8",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "twoArticlesLinkText",
      "value": "CALL TO ACTION",
      "moduleScope": false
    },
    {
      "name": "freeTextSpacer",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "freeTextSpacer2",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "ctaSpacer2",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "hrBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "freeTextBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "spacerBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "twoArticlesLink2",
      "value": "http:\/\/mylink",
      "moduleScope": false
    },
    {
      "name": "hrBorderColor",
      "value": "#e6e6e6",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBorderSize",
      "value": "1",
      "moduleScope": false
    },
    {
      "name": "ctaLink",
      "value": "http:\/\/mylink",
      "moduleScope": false
    },
    {
      "name": "freeImageBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "spacerSpacer",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "footerSpacer",
      "value": "10",
      "moduleScope": false
    },
    {
      "name": "ctaLinkText",
      "value": "CALL TO ACTION",
      "moduleScope": false
    },
    {
      "name": "twoArticlesButtonBackgroundColor2",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "ctaBorderSize",
      "value": "1",
      "moduleScope": false
    },
    {
      "name": "ctaBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "footerBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "twoArticlesLink",
      "value": "http:\/\/mylink",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBorderColor",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "ctaBorderColor",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBorderColor2",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "hrBorderSize",
      "value": "1",
      "moduleScope": false
    },
    {
      "name": "twoArticlesButtonBackgroundColor",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBorderSize2",
      "value": "1",
      "moduleScope": false
    },
    {
      "name": "ctaButtonBackgroundColor",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer4",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer3",
      "value": "15",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer2",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "ctaSpacer",
      "value": "20",
      "moduleScope": false
    }
  ]
}
```

結果配列内の各要素は、1つの変数を記述します。

変数には、メール全体のグローバルスコープまたはモジュールのローカルスコープを設定できます。 各変数には、`name`、`value`および`moduleScope`属性が含まれます。 ブール値`moduleScope`属性は、グローバル変数の場合は`false`、ローカル変数の場合は`true`です。 ローカル変数には、関連するモジュールの`moduleId`も含まれます。

#### アップデート

変数](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateVariableUsingPOST)を[更新するには、`value` パラメーターに新しい値を渡します。 電子メール IDと変数名をパスパラメーターとして指定します。 モジュール変数を更新する場合は、`moduleId`を渡して、関連するモジュールを識別します。

次の例は、グローバル変数`hrBorderSize`を更新します。

```http
POST /rest/asset/v1/email/{id}/variable/{name}.json
```

```text
Content-Type: application/x-www-form-urlencoded; charset=utf-8
```

```text
value=2
```

```json
{
    "success":true,
    "warnings":[ ],
    "errors":[ ],
    "requestId":"feb5#158db4be57e",
    "result": [
        {
            "name":"hrBorderSize",
            "value":"2",
            "moduleScope":false
        }
    ]
}
```

次の例では、モジュール `CTA`のローカル変数`ctaLinkText`を`Click this button!`に更新します。

```http
POST /rest/asset/v1/email/1032/variable/ctaLinkText.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
value=Click this button!&moduleId=CTA
```

```json
{
    "success": true,
    "warnings":[ ],
    "errors":[ ],
    "requestId": "7f34#158dc28d2f7",
    "result": [
        {
            "name":"ctaLinkText",
            "value":"Click this button!",
            "moduleScope":true,
            "moduleId":"CTA"
        }
    ]
}
```

## 承認

電子メールは、標準的なアセット承認ライフサイクルに従っています。 個別のエンドポイントを使用して、ドラフトを承認したり、承認されたバージョンを未承認にしたり、既存のドラフトを破棄したりできます。

### 承認

承認エンドポイントは、Marketoのメールルールに照らし合わせてメールを検証します。 `from name`、`from email`、`reply to email`および`subject`は、承認の前に入力する必要があります。

```http
POST /rest/asset/v1/email/{id}/approveDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"15dbf#14a1832ae86",
   "result":[
      {
         "id":1362
      }
   ]
}
```

#### 承認を取消

承認済み電子メールでのみ`unapprove`操作を使用します。

```http
POST /rest/asset/v1/email/{id}/unapprove.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"3514#14a1832b0fa",
   "result":[
      {
         "id":1364
      }
   ]
}
```

#### 破棄

下書きステータスでは、メールのみを破棄できます。 承認された電子メールは破棄できません。

```http
POST /rest/asset/v1/email/{id}/discardDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"182c0#14a1832af4f",
   "result":[
      {
         "id":1362
      }
   ]
}
```

#### 削除

```http
POST /rest/asset/v1/email/{id}/delete.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"169cd#14a1832adba",
   "result":[
      {
         "id":1361
      }
   ]
}
```

## 複製

電子メールを複製するには、次のパラメーターを使用して`application/x-www-form-urlencoded` POST リクエストを送信します。

- `name`：必須。 複製されたメール名。
- `folder`：必須。 `id`と`type`を含む埋め込みJSON オブジェクト。
- `description`：オプション。 複製されたメールの説明。

ソースメールに承認済みのバージョンがない場合、エンドポイントはドラフトバージョンを複製します。

```http
POST /rest/asset/v1/email/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=Clone of Social Sharing in Email&folder={"id":239,"type":"Folder"}&description=This is a test of clone email
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "bd49#15706f43d96",
    "result": [
        {
            "id": 2250,
            "name": "Clone of Social Sharing in Email",
            "description": "This is a test of clone email",
            "createdAt": "2016-09-07T23:20:52Z+0000",
            "updatedAt": "2016-09-07T23:20:52Z+0000",
            "url": "https://app-abm.marketo.com/#EM2250B2",
            "subject": {
                "type": "Text",
                "value": "Hey There"
            },
            "fromName": {
                "type": "Text",
                "value": "SomeBody"
            },
            "fromEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "replyEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "folder": {
                "type": "Folder",
                "value": 239,
                "folderName": "Tradeshows and Events"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": false,
            "status": "draft",
            "template": 24,
            "workspace": "Default",
            "isOpenTrackingDisabled": false
        }
    ]
}
```

## サンプルの送信

サンプルメールを送信するには、`emailAddress` クエリパラメーターで受信者を指定します。 次のオプションのパラメーターも含めることができます。

- `leadId`: データベースから特定のリードを偽装します。
- `textOnly`：電子メールのテキストバージョンのみを送信します。

```http
POST /rest/asset/v1/email/{id}/sendSample.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
emailAddress=abe@testmail.com&textOnly=true
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "360b#14cce7d2708",
    "result": [
        {
            "id": 2179
        }
    ]
}
```

## メールのプレビュー

[電子メールの完全なコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailFullContentUsingGET) エンドポイントを使用して、受信者が受信する電子メールのライブプレビューを取得します。 このエンドポイントは、バージョン 1.0のメールのみをサポートします。

必須の`id` パス パラメーターは、プレビューする電子メールを識別します。 エンドポイントは、次の3つのオプションのクエリパラメーターも受け入れます。

- `status`: `draft`または`approved`を受け入れます。 デフォルトは、承認済み電子メールの承認済みバージョンまたは未承認の電子メールのドラフトバージョンです。
- `type`: `Text`または`HTML`を受け入れます。 デフォルトは `HTML` です。
- `leadId`: リードの整数IDを受け入れ、そのリードが受け取ったかのようにメールをプレビューします。

```http
GET /rest/asset/v1/email/{id}/fullContent.json
```

```json
{
   "success": true,
   "warnings": [ ],
   "errors": [ ],
   "requestId": null,
   "result": [
      {
         "id": 339,
         "status": "draft",
         "content": "<!DOCTYPE HTML PUBLIC \"-//W3C//DTD HTML 1.01 Transitional//EN\" \"http://www.w1.org/TR/html4/loose.dtd\">\n<html>\n  <head>\n    <meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\"/>\n    <title></title>\n  </head>\n  <body>\n      <div style=\"font: 14px tahoma; width: 100%\" class=\"mktEditable\" id=\"edit_text_3\">\n        Content from testCreateEmailTemplate2\n    </div>\n  </body>\n</html>"
      }
   ]
}
```

## HTML の置換

[ メールの完全コンテンツの更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/createEmailFullContentUsingPOST) エンドポイントを使用して、メールアセット内のすべてのコンテンツを置き換えます。 このエンドポイントは、UIでコードを編集する機能を使用し、親テンプレートにリンクされなくなったバージョン 1.0の電子メールのみをサポートします。

エンドポイントは、主に、標準コンテンツエンドポイントで変更できないプログラムの一部として複製されたアセットを対象としています。 動的コンテンツを含むメールはサポートされていません。 メールがまだテンプレートにリンクされている場合、エンドポイントはエラーを返します。

パスにメール `id`を含む`multipart/form-data` リクエストを送信します。 リクエスト本文には、完全なHTML電子メールドキュメントとコンテンツタイプ `text/html`を含む1つの`content` パラメーターが含まれている必要があります。

形式が正しくないHTML ドキュメントは警告を生成し、承認を妨げる可能性があります。 JavaScriptまたは`<script>` タグを含めると、呼び出しが失敗し、エラーが発生します。

```http
POST /rest/asset/v1/email/{id}/fullContent.json
```

```text
content-type: multipart/form-data; boundary=--------------------------116301888604800085728247
content-length: 599
```

```html
----------------------------116301888604800085728247
Content-Disposition: form-data; name="content"; filename="email_content.html"
Content-Type: text/html

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 1.01 Transitional//EN" "http://www.w1.org/TR/html4/loose.dtd">
 <html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
 <title></title>
 </head>
 <body>
 <div style="font: 14px tahoma; width: 100%" class="mktEditable" id="edit_text_3">
 EMAIL TEST CONTENT
 </div>
 </body>
 </html>
----------------------------116301888604800085728247--
```

```json
{
   "success": true,
   "warnings": [ ],
   "errors": [ ],
   "requestId": "15dbf#14a1832ae86",
   "result": [
      {
         "id": 1001
      }
   ]
}
```
