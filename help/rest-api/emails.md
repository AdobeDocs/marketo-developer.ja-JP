---
title: メール
feature: REST API
description: メールアセットを操作するための API。
exl-id: 6875730d-c74a-42cf-a3d2-dad7a3ac535d
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 2%

---

# メール

[ メールエンドポイントの参照 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails) メールアセットの操作に使用できる REST エンドポイントの完全なセットが提供されています。

注意：[Marketo予測コンテンツ ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/predictive-content/working-with-predictive-content/understanding-predictive-content) を使用している場合、予測コンテンツを含むメールを参照しているエンドポイント [ メールコンテンツの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET)、[ メールコンテンツの更新セクション ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailComponentContentUsingPOST)、[ メールドラフトの承認 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/approveDraftUsingPOST) は失敗します。 この呼び出しは、709 エラーコードと、対応するエラーメッセージを返します。

## クエリ

メールのクエリパターンはテンプレートのクエリパターンと同じであり、クエリ [ID 別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByIdUsingGET)、[ 名前別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByNameUsingGET) および [ 閲覧別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailUsingGET) が可能なほか、参照 API と名前別 API を使用してフォルダーに基づいてフィルタリングできます。

メモ：メールが [A/B テスト ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/email-programs/email-program-actions/email-test-a-b-test/add-an-a-b-test) を使用するメールプログラムに含まれている場合、そのメールは、[ID でメールを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByIdUsingGET)、[ 名前でメールを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByNameUsingGET)、[ メールを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailUsingGET) のエンドポイントを使用したクエリでは使用できません。 呼び出しは成功を示しますが、「指定された検索条件でアセットが見つかりませんでした」という警告が含まれます。

### ID 別

```
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

「」という名前を使用して、オプションで、そのフォルダー内のみを検索するフォルダーを渡すことができます。

```
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

フォルダーの参照は、他の Asset API 参照エンドポイントと同様に機能し、`status`、`folder`、`earliestUpdatedAt`/`latestUpdatedAt`、`maxReturn` および `offset` に対するオプションのフィルタリングを可能にします。 `status` は承認済みまたはドラフトです。 `folder` は、`id` と `type` を含む JSON オブジェクトです。 `maxReturn` は結果の数を制限する整数（デフォルトは 20、最大は 200）、`offset` は大きな結果セットを読み取るために `maxReturn` で使用できる整数（デフォルトは 0）です。

```
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

## コンテンツのクエリ

メールのコンテンツをクエリして、そのメールで [ 使用可能な編集可能なセクションを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET) できます。また、オプションでステータスをフィルタリングして、承認済みまたはドラフトのバージョンのセクションを取得できます。

```
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

セクションは、dynamicContent タイプを持つものとして返される場合があります。 詳しくは、[ 動的コンテンツ ](dynamic-content.md) の節を参照してください。

## CC フィールドのクエリ

[ メール CC フィールドを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailCCFieldsUsingGET) エンドポイントを呼び出して、ターゲットインスタンスで「メール CC」が有効な一連のフィールドを取得できます。

```
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

[ メールは ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/createEmailUsingPOST) ソーステンプレートをベースにして作成され、「mktEditable」クラスと一意の id プロパティを持つ、そのテンプレート内の個別のHTML要素から派生した編集可能セクションのリストを持ちます。 API でメールを作成すると、テンプレートに基づいたレコードと、渡された追加のメタデータが作成されます。 作成メールを正常に呼び出すには、名前、テンプレート、フォルダーのパラメーターが必要です。

作成する場合は、`subject`、`fromName`、`fromEmail`、`replyEmail`、`operational`、`isOpenTrackingDisabled` のパラメーターはオプションです。 設定を解除すると、`subject` は空、`fromName`、`fromEmail` になり、`replyEmail` はインスタンスのデフォルトに設定され、`operational` と `isOpenTrackingDisabled` は false になります。 送信時に、開封トラッキングピクセルをメールに含めるかどうかを `isOpenTrackingDisabled` 定します。

```
POST /rest/asset/v1/emails.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

[ メールの更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailContentUsingPOST) レコードは ID で作成できます。 これにより、メールの説明または名前を更新できます。

```
POST /rest/asset/v1/email/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

### Content Section, Type, and Update

メールの各セクションのコンテンツは、件名、fromName、fromEmail、replyEmail とは別に、個別に更新する必要があります。件名は、「[ メールコンテンツの更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailContentUsingPOST) エンドポイントを使用して更新されます。 このエンドポイントを使用する場合、静的コンテンツではなく動的コンテンツを使用するようにこれらの値を設定することもできます。 各パラメーターは、タイプ/値の JSON オブジェクトです。タイプは「Text」または「DynamicContent」で、値は、適切なテキスト値または動的コンテンツに使用するセグメント化の ID です。 データは、JSON としてではなく、POST x-www-form-urlencoded として渡されます。  isOpenTrackingDisabled は Update Email Content で設定できます。

```
POST /rest/asset/v1/email/{id}/content.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

動的コンテンツを使用するようにセクションを設定する場合、セクション ID はメールコンテンツの取得呼び出しを使用して取得する必要があります。

### 編集可能セクションを更新

編集可能セクションは、個々の htmlId で更新されます。 パスパラメーターとしては、メールの ID とセクションの htmlId のみが必須で、type、value および textValue はオプションです。 タイプは、「テキスト」、「ダイナミックコンテンツ」、「スニペット」のいずれかであり、値に渡されるものに影響を与えます。 タイプがテキストの場合、値はセクションのHTMLコンテンツを含む文字列になります。 DynamicContent の場合は、3 つのメンバーを持つ JSON ブロックです。type は「DynamicContent」、segmentation は、コンテンツに使用するセグメント化の ID、default は、セクションのデフォルトのHTMLコンテンツを含む文字列です。 オプションの textValue パラメーターは、セクションのテキストバージョンを含む文字列です。 データは、JSON としてではなく、POST x-www-form-urlencoded として渡されます。

```
POST /rest/asset/v1/email/{id}/content/{htmlId}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

注意：メールに埋め込まれたスニペットに対して「テキストに自動コピー」が無効になっている場合、スニペットのHTMLの値が更新され、その後メール内の別のセクションのテキストバージョンが更新されると、メールのテキストバージョンには、自動コピーが無効になっている場合に期待される以前のバージョンではなく、スニペットのHTMLの更新された値を反映したテキストが表示されます。

## モジュール

メールエディター 1.0 のモジュールは、テンプレートで定義されたメールのセクションです。モジュールには、要素、変数、その他のHTMLコンテンツを任意に組み合わせて含めることができます。詳しくは、[ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Modules) を参照してください。 Marketoは、メール内のモジュールを管理するための一連の API を提供します。 HTTP POST方式を必要とするモジュール関連のエンドポイントの場合、本文は（JSON ではなく）「application/x-www-form-urlencoded」としてフォーマットされます。

モジュール関連のエンドポイントのほとんどは、パスパラメーターとして「moduleId」を必要とします。 これは、モジュールを説明する文字列です。 moduleId は、[ メールコンテンツを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET) エンドポイントによって「htmlId」属性として返されます（以下の [ クエリ ](#modules_query) の節を参照）。

### クエリ

モジュールを操作するには、モジュールを一意に識別する moduleId パラメーターを指定する必要があります。 また、モジュールインデックスパラメーターを指定する必要もあります。このパラメーターは、メール内のモジュールの順序を説明する整数です。

メール ID をパスパラメーターとして指定して、[moduleIds とそのインデックスを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET) します。

次の例では、テンプレートピッカー UI の「スターターテンプレート」セクションにある「スケルトン」テンプレートに基づいて 1.0 メールをクエリします。

```
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
          "value": "<p style=\"text-align: center;\"><span style=\"color: #333333;\"><strong>Acme, Inc<\/strong><\/span><\/p> \n<div style=\"text-align: center;\">\n  You received this because you've subscribed to our newsletter. Click \n <a href=\"{{system.unsubscribeLink}}\" target=\"_blank\" class=\"mktNoTrack\">here<\/a> to unsubscribe. \n <br> \n<\/div>"
        },
        {
          "type": "Text",
          "value": "Acme, Inc \n You received this because you've subscribed to our newsletter. Click here <{{system.unsubscribeLink}}> to unsubscribe."
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

結果の配列には、モジュールとHTML要素の両方を混在させて記述する要素が含まれます。 モジュール要素には、「contentType」:「Module」属性と「index」属性が含まれます。 moduleId は、「htmlId」属性に保存されます。

上記の「スケルトン」の例を続けると、次の表に、moduleIds の概要と、メールに含まれる対応するインデックスが示されます。

| moduleId （htmlId とも呼ばれます） | インデックス |
|---|---|
| spacer | 0 |
| 自由画像 | 1 |
| ビデオ | 2 |
| フリーテキスト | 3 |
| CTA | 4 |
| 時間 | 5 |
| 2 つの記事 | 6 |
| フッター | 7 |

#### 追加

使用中のメールテンプレートに含まれる既存のモジュールの 1 つを選択して、メールに [ モジュールを追加 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/addModuleUsingPOST) します。 これを行うには、メール ID と moduleId をパスパラメーターとして指定します。 インデックスクエリパラメーターは必須で、メール内のモジュールの順序を決定します。 インデックス値が既存の最大インデックス値を超えると、モジュールがメールに追加されます。

```
POST /rest/asset/v1/email/{id}/content/{moduleId}/add.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
index=10
```

```
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

メール ID と moduleId をパスパラメーターとして指定して、[ モジュールを削除 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/deleteModuleUsingPOST) します。

```
POST /rest/asset/v1/email/{id}/content/{moduleId}/delete.json
```

```
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

メール ID と moduleId をパスパラメーターとして指定して [ モジュールを複製 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/duplicateModuleUsingPOST) します。 この呼び出しではモジュールが複製され、元のモジュールの下に配置されて、他のモジュールを下に押し下げます。

```
POST /rest/asset/v1/email/{id}/content/{moduleId}/duplicate.json
```

```
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

[ すべてのモジュールと、それぞれのメール内の目的の位置を含むモジュール ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/rearrangeModulesUsingPOST) 配列を並べ替えます。 各配列要素には、次の形式の JSON オブジェクトが含まれます。  { &quot;index&quot;: &lt;_index_>, &quot;moduleId&quot;: &quot;&lt;_moduleId_>&quot; }。&lt;_index_> は 0 から始まるモジュールのオーダー番号、&lt;_moduleId_> はモジュール ID です。

```
POST /rest/asset/v1/email/{id}/content/rearrange.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
positions=[ {"index": 0, "moduleId": "free-image"}, {"index": 1, "moduleId": "title"}, {"index": 2, "moduleId": "mkvideo"}, {"index": 3, moduleId": "free-text"}, {"index": 4, "moduleId": "blankSpace"}, {"index": 5, "moduleId": "Separator"}, {"index": 6, "moduleId": "callToAction"}, {"index": 7, "moduleId": "blankSpace2"}, {"index": 8, "moduleId": "blankSpace3"} ]
```

```
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

name パラメーターを使用して新しい名前を渡すことにより、メールの [ モジュール名を変更 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/renameUsingPOST) します。 メール ID と moduleId （既存の名前）をパスパラメーターとして指定します。

```
POST /rest/asset/v1/email/{id}/content/{moduleId}/rename.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=MarketoVideo
```

```
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

メールエディター 1.0 では、変数を使用してメール内の要素の値が格納されます。 各変数は、（こちら [ の説明に従って、Marketo固有の構文をHTMLに追加することで定義され ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Variables) す。 Marketoは、メール内の変数を管理するための一連の API を提供します。

### クエリ

メール ID をパスパラメーターとして指定して、メールの [ 変数を取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailVariablesUsingGET) します。

次の例では、テンプレートピッカー UI の「スターターテンプレート」セクションにある「スケルトン」テンプレートに基づいて 1.0 メールをクエリします。

```
GET /rest/asset/v1/email/{id}/variables.json
```

```
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

結果の配列には、要素ごとに 1 つの変数を記述する要素が含まれます。

変数は、メール全体に対してグローバルにスコープ設定することも、特定のモジュールに対してローカルにスコープ設定することもできます。 どちらのスコープの変数にも、「name」、「value」、および「moduleScope」属性が含まれています。 「moduleScope」属性はブール値です。false はグローバル、true はローカルを示します。 ローカル変数には、変数が関連付けられているモジュールを指定する追加の「moduleId」属性が含まれています。

#### 更新

値パラメーターを使用して新しい目的の値を渡すことにより、メール内で [ 変数を更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateVariableUsingPOST) します。 メール ID と変数名をパスパラメーターとして指定します。 モジュール変数を更新する場合、moduleId パラメーターを渡して、変数が関連付けられているモジュールを指定する必要もあります。

次の例では、「hrBorderSize」という名前のグローバル変数を値 1 に更新します。

```
POST /rest/asset/v1/email/{id}/variable/{name}.json
```

```
Content-Type: application/x-www-form-urlencoded; charset=utf-8
```

```
value=2
```

```
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

次の例では、「ctaLinkText」という名前のローカル変数を「Click this button!」という値に更新します。 モジュール ID 「CTA」内。

```
POST /rest/asset/v1/email/1032/variable/ctaLinkText.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

メールは、アセットレコードの承認の標準パターンに従います。 ドラフトの承認、承認バージョンの未承認、メールの既存のドラフトの破棄を、それぞれのエンドポイントで行うことができます。

### 承認

承認エンドポイントを呼び出すと、メールがMarketo メールのルールに対して検証されます。 メールを承認するには、`from name`、`from email`、`reply to email`、`subject` を入力する必要があります。

```
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

#### 承認取消

`unapprove` の操作は、承認された E メールに対してのみ実行できます。

```
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

破棄するには、メールがドラフトステータスである必要があります。 承認済みのメールは破棄できません。

```
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

```
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

## クローン作成

Marketoには、メールの簡単なクローン作成方法が用意されています。 このタイプのリクエストは、application/x-www-url-urlencoded POSTーで行われ、2 つの必須パラメーター（名前、フォルダー）、id および type を持つ埋め込み JSON オブジェクトを受け取ります。 説明はオプションのパラメーターでもあります。 承認済みバージョンが存在しない場合は、ドラフトバージョンのクローンが作成されます。

```
POST /rest/asset/v1/email/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

api を介してサンプルメールをトリガーし、emailAddress クエリパラメーターに送信できます。 オプションで、データベースの特定のリードとして実行する leadId パラメーターや、メールのテキストバージョンのみを送信する textOnly パラメーターを追加することもできます。

```
POST /rest/asset/v1/email/{id}/sendSample.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

Marketoは [ メールの完全なコンテンツを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailFullContentUsingGET) エンドポイントを提供して、受信者に送信されるメールのライブプレビューを取得します。 このエンドポイントは、バージョン 1.0 のメールでのみ使用できます。 必須パラメーターが 1 つあります。id パスパラメーターは、プレビューするメールアセットの ID です。 オプションのクエリパラメーターがさらに 3 つあります。

- ステータス：値「ドラフト」または「承認済み」を受け入れます。この値はデフォルトで、承認済みのバージョン、承認済みの場合、ドラフト （未承認の場合）に設定されます。
- type:「テキスト」または「HTML」を使用できます。デフォルトはHTMLです。
- leadId:. リードの整数 ID を受け入れます。 設定すると、指定されたリードが受信したかのようにメールがプレビューされます

```
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

Marketoには、メールアセットのコンテンツ全体を置き換える [ メールの完全なコンテンツを更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/createEmailFullContentUsingPOST) エンドポイントが用意されています。 このエンドポイントは、UI の「コードを編集」機能が使用され、親テンプレートとの関係が壊れているバージョン 1.0 のメールでのみ使用できます。 この API は主に、プログラムの一部として複製されたアセットで使用することを目的としており、標準のコンテンツエンドポイントでは変更できません。 動的コンテンツを含むメールはサポートされていません。 また、関係が損なわれていないメールのHTMLを置き換えようとすると、エラーが返されます。

このエンドポイントでは、パスに id パラメーター、メールの ID および本文に 1 つのパラメーターを持つマルチパート/フォームデータで、コンテンツタイプが「text/html」の完全なHTMLメールドキュメントとしてコンテンツが想定されます。 形式が正しくないHTMLドキュメントでは警告が表示されますが、承認できない場合があります。その一方で、ドキュメントにJavaScriptや `<script>` タグを含めると、呼び出しが失敗し、エラーが表示されます。

```
POST /rest/asset/v1/email/{id}/fullContent.json
```

```
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
