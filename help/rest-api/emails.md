---
title: メール
feature: REST API
description: メールアセットを操作するための API。
exl-id: 6875730d-c74a-42cf-a3d2-dad7a3ac535d
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '1946'
ht-degree: 100%

---

# メール

[メールエンドポイントの参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails) メールアセットを操作するための REST エンドポイントの完全なセットが提供されています。

メモ：[Marketo 予測コンテンツ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/predictive-content/working-with-predictive-content/understanding-predictive-content)を使用している場合、予測コンテンツを含むメールを参照すると、「[メールコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET)」、「[メールコンテンツセクションを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailComponentContentUsingPOST)」、「[メールのドラフトを承認](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/approveDraftUsingPOST)」のエンドポイントは失敗します。この呼び出しでは、709 エラーコードと、対応するエラーメッセージが返されます。

## クエリ

メールのクエリパターンは、テンプレートのパターンと同じで、[ID 別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByIdUsingGET)、[名前別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByNameUsingGET)、[参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailUsingGET)にクエリを実行したり、参照 API と名前 API を使用してフォルダーに基づいてフィルタリングしたりできます。

メモ：メールが [A/B テスト](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/email-programs/email-program-actions/email-test-a-b-test/add-an-a-b-test)を使用しているメールプログラムの一部である場合、このメールは、「[ID でメールを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByIdUsingGET)」、「[名前でメールを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByNameUsingGET)」、「[メールを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailUsingGET)」などのエンドポイントを使用したクエリには使用できません。呼び出しは成功を示しますが、「指定された検索条件のアセットが見つかりません」という警告が含まれます。

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

名前別では、オプションでフォルダーを渡して、このフォルダー内のみを検索できます。

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

フォルダーの参照では、他の Asset API 参照エンドポイントと同様に機能し、`status`、`folder`、`earliestUpdatedAt`／`latestUpdatedAt`、`maxReturn`、`offset` でのオプションのフィルタリングが可能です。`status` は、承認済みまたはドラフトのいずれかです。`folder` は、`id` と `type` を含む JSON オブジェクトです。`maxReturn` は結果の数を制限する整数（デフォルトは 20、最大は 200）で、`offset` は大きな結果セットを読み取るために `maxReturn` と併用できる整数（デフォルトは 0）です。

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

## クエリコンテンツ

メールのコンテンツのクエリを実行して、[編集可能なセクションを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET)できます。また、オプションでステータスをフィルタリングして、承認済みバージョンまたはドラフトバージョンのセクションを取得できます。

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

セクションは dynamicContent のタイプとして返される場合があります。詳しくは、[動的コンテンツ](dynamic-content.md)の節を参照してください。

## CC フィールドのクエリ

[メール CC フィールドを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailCCFieldsUsingGET)エンドポイントを呼び出すことで、ターゲットインスタンスでメール CC に対して有効になっているフィールドのセットを取得できます。

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

[メール](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/createEmailUsingPOST)はソーステンプレートに基づいて作成され、このテンプレート内の各 HTML 要素から派生した編集可能なセクションのリストが、「mktEditable」クラスと一意の ID プロパティと共に保持されます。API を使用してメールを作成すると、渡された追加のメタデータと共にテンプレートに基づいたレコードが作成されます。「メールを作成」呼び出しを正常に実行するには、名前、テンプレート、フォルダーのパラメーターが必須です。

`subject`、`fromName`、`fromEmail`、`replyEmail`、`operational`、`isOpenTrackingDisabled` のパラメーターは作成時ではオプションです。設定していない場合、`subject` は空になり、`fromName`、`fromEmail`、`replyEmail` はインスタンスのデフォルトに設定され、`operational` と `isOpenTrackingDisabled` は false になります。`isOpenTrackingDisabled` は、送信時にメールに開封トラッキングピクセルが含まれるかどうかを決定します。

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

[メールの更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailContentUsingPOST)レコードは、ID で実行できます。これにより、メールの説明または名前を更新できます。

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

### コンテンツセクション、タイプ、更新

メールの各セクションのコンテンツは、件名、fromName、fromEmail、replyEmail を除き、個別に更新する必要があります。これらは、[メールコンテンツを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailContentUsingPOST)エンドポイントを使用して更新されます。このエンドポイントを使用する際、これらの値を設定すると、静的コンテンツの代わりに動的コンテンツを使用することもできます。各パラメーターは、タイプ／値の JSON オブジェクトです。タイプは「Text」または「DynamicContent」のいずれかであり、値は適切なテキスト値、または動的コンテンツに使用するセグメント化の ID のいずれかです。データは、JSON ではなく、POST x-www-form-urlencoded として渡されます。isOpenTrackingDisabled は、「メールコンテンツを更新」で設定できます

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

セクションを設定して動的コンテンツを使用する場合は、「メールコンテンツを取得」呼び出し経由でセクション ID を取得する必要があります。

### 編集可能なセクションの更新

編集可能なセクションは、個々の htmlId で更新されます。パスパラメーターとして必須なのは、メールの ID とセクションの htmlId のみで、type、value および textValue はオプションです。タイプは、&quot;Text&quot;、&quot;DynamicContent&quot;、または &quot;Snippet&quot; のいずれかであり、値で渡される内容に影響を与えます。タイプが Text の場合、値はセクションの HTML コンテンツを含む文字列になります。DynamicContent の場合、type（「DynamicContent」）、segmentation（コンテンツに使用するセグメント化の ID）、default（セクションのデフォルトの HTML コンテンツを含む文字列）の 3 つのメンバーを持つ JSON ブロックです。オプションの textValue パラメーターは、セクションのテキストバージョンを含む文字列です。データは、JSON ではなく、POST x-www-form-urlencoded として渡されます。

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

メモ：メールに埋め込まれたスニペットのテキストへの自動コピーが無効になっている場合、スニペットの HTML 値が更新され、次にメール内の別のセクションのテキストバージョンが更新されると、メールのテキストバージョンには、自動コピーが無効になっている場合に予想される以前のバージョンではなく、スニペット HTML の更新された値を反映したテキストが含まれます。

## モジュール

メールエディター 1.0 のモジュールは、テンプレートで定義されたメールのセクションです。モジュールには、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Modules)の説明に従って、要素、変数、その他の HTML コンテンツの任意の組み合わせを含めることができます。Marketo は、メール内のモジュールを管理するための一連の API を備えています。HTTP POST メソッドを必要とするモジュール関連のエンドポイントの場合、本文は「application/x-www-form-urlencoded」（JSON ではない）として書式設定されます。

モジュール関連のエンドポイントのほとんどは、パスパラメーターとして「moduleId」を必要とします。これは、モジュールを説明する文字列です。moduleIds は、[メールコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET)エンドポイントによって &quot;htmlId&quot; 属性として返されます（以下の[クエリ](#modules_query)の節を参照）。

### クエリ

モジュールを操作するには、モジュールを一意に識別する moduleId パラメーターを指定する必要があります。また、モジュールインデックスパラメーターを指定する必要もあります。これは、メール内のモジュールの順序を説明する整数です。

[moduleIds とこのインデックスを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET)するには、パスパラメーターとしてメール ID を指定します。

次の例では、テンプレートピッカー UI の「スターターテンプレート」セクションにある「スケルトン」テンプレートに基づいて 1.0 メールに対してクエリを実行します。

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

結果配列には、モジュールと HTML 要素の両方を説明する要素が混在して含まれています。モジュール要素には、&quot;contentType&quot;: &quot;Module&quot; 属性と &quot;index&quot; 属性が含まれます。moduleId は &quot;htmlId&quot; 属性に格納されます。

上記の「スケルトン」の例を続けます。次の表に、メールに含まれる moduleIds とこれに対応するインデックスの概要を示します。

| moduleId（htmlId とも呼ばれる） | インデックス |
|---|---|
| spacer | 0 |
| free-image | 1 |
| video | 2 |
| free-text | 3 |
| CTA | 4 |
| hr | 5 |
| two-articles | 6 |
| footer | 7 |

#### 追加

使用中のメールテンプレートに含まれる既存のモジュールの 1 つを選択して、メールに[モジュールを追加](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/addModuleUsingPOST)します。これを行うには、メール ID と、パスパラメーターとして moduleId を指定します。インデックスクエリパラメーターは必須で、メール内のモジュールの順序を決定します。インデックス値が既存の最大のインデックス値を超える場合、モジュールはメールに追加されます。

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

メール ID と、パスパラメーターとして moduleId を指定して[モジュールを削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/deleteModuleUsingPOST)します。

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

メール ID と、パスパラメーターとして moduleId を指定して[モジュールを複製](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/duplicateModuleUsingPOST)します。この呼び出しにより、モジュールが複製され、元のモジュールの下に配置され、他のモジュールが下に押し下げられます。

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

すべてのモジュールと、それぞれのメール内での目的の位置を含む配列の[モジュールを並べ替え](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/rearrangeModulesUsingPOST)ます。各配列要素には、{ “index”: &lt;_index_>, “moduleId”: “&lt;_moduleId_>” } の形式の JSON オブジェクトが含まれます。ここで、&lt;_index_> はゼロベースのモジュール順序番号、&lt;_moduleId_> は moduleId です。

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

name パラメーター経由で新しい名前を渡して、メールの[モジュールを名前変更](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/renameUsingPOST)します。メール ID と、パスパラメーターとして moduleId（既存の名前）を指定します。

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

メールエディター 1.0 では、変数を使用してメール内の要素の値を格納します。各変数は、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Variables)の説明に従って、Marketo 固有の構文を HTML に追加することで定義されます。Marketo は、メール内の変数を管理するための一連の API を備えています。

### クエリ

メールの[変数を取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailVariablesUsingGET)するには、パスパラメーターとしてメール ID を指定します。

次の例では、テンプレートピッカー UI の「スターターテンプレート」セクションにある「スケルトン」テンプレートに基づいて 1.0 メールに対してクエリを実行します。

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

結果配列には、要素ごとに 1 つの変数を含む、変数を説明する要素が含まれています。

変数は、メール全体に対してグローバルにスコープすることも、特定のモジュールに対してローカルにスコープすることもできます。どちらのスコープの変数にも、&quot;name&quot;、&quot;value&quot;、および &quot;moduleScope&quot; 属性が含まれています。&quot;moduleScope&quot; 属性はブーリアンで、false はグローバル、true はローカルを示します。ローカル変数には、変数が関連付けられているモジュールを指定する追加の &quot;moduleId&quot; 属性が含まれています。

#### 更新

値パラメーター経由で新しい目的の値を渡して、メールの[変数を更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateVariableUsingPOST)します。メール ID と、パスパラメーターとして変数名を指定します。モジュール変数を更新する場合は、変数が関連付けられているモジュールを指定するために moduleId パラメーターも渡す必要があります。

次の例では、&quot;hrBorderSize&quot; という名前のグローバル変数の値を 1 に更新します。

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

次の例では、moduleId &quot;CTA&quot; の&quot;ctaLinkText&quot; というローカル変数を &quot;Click this button!&quot; という値に更新します。

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

メールは、アセットレコードの承認の標準パターンに従います。それぞれのエンドポイントを通じて、メールのドラフトを承認したり、承認済みバージョンを未承認にしたり、既存のドラフトを破棄したりできます。

### 承認

承認エンドポイントを呼び出すと、メールは Marketo メールのルールに対して検証されます。メールを承認する前に、`from name`、`from email`、`reply to email`、`subject` を入力する必要があります。

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

#### 未承認

`unapprove` 操作は、承認済みメールに対してのみ実行できます。

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

メールを破棄するには、メールがドラフトステータスである必要があります。承認済みメールは破棄できません。

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

## 複製

Marketo には、メールを複製するための簡単な方法が用意されています。このタイプのリクエストは、application/x-www-url-urlencoded POST を使用して行われ、name とfolder の 2 つの必須パラメーターおよび ID とタイプを含む埋め込み JSON オブジェクトを受け取ります。description もオプションのパラメーターです。承認済みバージョンが存在しない場合は、ドラフトバージョンが複製されます。

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

API 経由でサンプルメールをトリガーし、emailAddress クエリパラメーターに送信できます。また、オプションで、leadId パラメーターを追加してデータベースから特定のリードを別のユーザとして実行したり、textOnly パラメーターを追加してメールのテキストバージョンのみを送信したりすることもできます。

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

Marketo には、受信者に送信されるメールのライブプレビューを取得するための[メールの完全なコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailFullContentUsingGET)エンドポイントが用意されています。このエンドポイントは、バージョン 1.0 のメールでのみ使用できます。必須パラメーターが 1 つあり、プレビューするメールアセットの ID である id パスパラメーターです。オプションのクエリパラメーターがさらに 3 つあります。

- status：&quot;draft&quot; または &quot;approved&quot; の値を使用できます。承認済みの場合は、承認済みバージョンがデフォルトになり、未承認の場合はドラフトになります。
- type：&quot;Text&quot; または &quot;HTML&quot; を使用でき、デフォルトは HTML になります
- leadId：リードの整数 ID を使用できます。設定すると、指定されたリードが受信したかのようにメールがプレビューされます

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

Marketo には、メールアセットのコンテンツ全体を置き換えるための[メールの完全なコンテンツを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/createEmailFullContentUsingPOST)エンドポイントが用意されています。このエンドポイントでは、UI の「コードを編集」機能が使用され、親テンプレートとの関係が破損しているバージョン 1.0 のメールでのみ使用できます。この API は主に、プログラムの一部として複製されたアセットで使用することを目的としており、標準のコンテンツエンドポイントでは変更できません。動的コンテンツを含むメールはサポートされていません。また、関係が維持されているメールの HTML を置き換えようとすると、エラーが返されます。

このエンドポイントは、Content-Type: multipart/form-data を想定しており、パスには id パラメーター、メールの ID、本文には 1 つのパラメーター、Content-Type「text/html」を持つ完全な HTML メールドキュメントとしてのコンテンツが必要です。形式が正しくない HTML ドキュメントでは警告が表示されますが、承認を許可しない場合があります。一方、ドキュメントに JavaScript や `<script>` タグが含まれていると、呼び出しが失敗し、エラーが表示されます。

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
