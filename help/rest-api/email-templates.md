---
title: メールテンプレート
feature: REST API
description: Marketo API を使用してメールテンプレートを作成します。
exl-id: 0ecf4da6-eb7e-43c1-8d5c-0517c43b47c8
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 2%

---

# メールテンプレート

[ メールテンプレートエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates)

メールテンプレートは、Marketoで新しいメールを作成するたびに使用されます。  HTMLの置き換えを通じてメールをテンプレートからリンク解除することもできますが、メールは最初にテンプレートをベースとして作成する必要があります。  テンプレートは、名前や説明などのメタデータを含む、純粋なHTMLドキュメントとしてMarketoで作成されます。  コンテンツに関する制限はほとんどありませんが、テンプレートのHTMLが有効で、要件（ここでは概要 [ に従った編集可能なセクションが少なくとも 1 つ含まれている必要があ ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/add-editable-sections-to-email-templates-v1-0) ます。

## クエリ

メールテンプレートのクエリは、アセットの標準のパターンに従い、特定のフォルダーに対して [id 別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/getTemplateByIdUsingGET)、[ 名前別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/getTemplateByNameUsingGET) および [ 参照別 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/getEmailTemplatesUsingGET) クエリを実行できます。

### Id 別

```
GET /rest/asset/v1/emailTemplate/{id}.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "14f9e#14a12955df1",
    "result": [
        {
            "id": 19,
            "name": "aFgSxuZrBI",
            "description": "fUMhVfIyVkhHzRolYzjGyWouTMfjXCPIAZxHMAEmszAjguVKDtbznEeqbqiDuNBzQoHwBJFdXiMzYiMlGUwtuklUhjGfJlDbhaTL",
            "createdAt": "2014-11-14T02:41:26Z+0000",
            "updatedAt": "2014-11-14T02:41:26Z+0000",
            "folder": {
                "type": "Folder",
                "value": 15
            },
            "status": "Draft",
            "workspace": "Default"
        }
    ]
}
```

#### 名前別

```
GET /rest/asset/v1/emailTemplate/byName.json?name=Test Template
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "14f9e#14a12955df1",
    "result": [
        {
            "id": 19,
            "name": "aFgSxuZrBI",
            "description": "fUMhVfIyVkhHzRolYzjGyWouTMfjXCPIAZxHMAEmszAjguVKDtbznEeqbqiDuNBzQoHwBJFdXiMzYiMlGUwtuklUhjGfJlDbhaTL",
            "createdAt": "2014-11-14T02:41:26Z+0000",
            "updatedAt": "2014-11-14T02:41:26Z+0000",
            "folder": {
                "type": "Folder",
                "value": 15
            },
            "status": "Draft",
            "workspace": "Default"
        }
    ]
}
```

#### 参照

```
GET /rest/asset/v1/emailTemplates.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"33c4#14a1832b4a8",
   "result":[
      {
         "id":18,
         "name":"AAA0unit3CreateTestEmailTemplateName.2314673e-7bc2-47da-a1e8-66dfdd8a1f1d",
         "description":"AssetAPI: getTemplates test",
         "createdAt":"2014-11-03T19:52:58Z+0000",
         "updatedAt":"2014-11-03T19:52:58Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":177,
         "name":"ABfRGutnwN",
         "description":"HMmHkdTRrGaRpPakdgGKICxfMunCEWDUWiThgAbInfaBXxGxSFfjKQIwerngCHRlGTnAJhKPmwlXLcsjGPtWEiILGyeIJTNVHoHg",
         "createdAt":"2014-11-20T19:31:06Z+0000",
         "updatedAt":"2014-11-20T19:31:06Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":148,
         "name":"ADVHJBQLyw",
         "description":null,
         "createdAt":"2014-11-20T06:42:57Z+0000",
         "updatedAt":"2014-11-20T06:42:57Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":201,
         "name":"AIpwuwiaqb",
         "description":null,
         "createdAt":"2014-11-25T20:49:06Z+0000",
         "updatedAt":"2014-11-25T20:49:06Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":240,
         "name":"aqZGoAskEF",
         "description":"uOMEhLpXOEWkwdZxkpcdDjTjKfokxuHEYHPVIVsADFIUEUobzIEaDiqFFxezwfovGfwjuPTJRxUmuHmGpyIklJdDdVosPJdyOVom",
         "createdAt":"2014-11-26T21:11:56Z+0000",
         "updatedAt":"2014-11-26T21:11:56Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":199,
         "name":"BAxnkVfLGi",
         "description":"TzUMQKzKXdgukNCCcaiJHUWASceqlZswhCqDQFDFZULqzYkEiyKcwtQRzKERynReqtMHOhqjnhExCsZopyfzglmXAOjEJdxNURCX",
         "createdAt":"2014-11-25T20:49:06Z+0000",
         "updatedAt":"2014-11-25T20:49:06Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":278,
         "name":"bcBNCUIHrL",
         "description":"UJEPYBRGTSYosZRnMnahMyVtdyxjRpzJMSXyncATKwcLlDAqDnSCFezGVsDZFpZwPzQvBlvaOZzOzBIsIAtqIerZhJFfpqMogoiB",
         "createdAt":"2014-11-30T11:30:07Z+0000",
         "updatedAt":"2014-11-30T11:30:07Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      }
   ]
}
```

レコード自体に対してクエリを実行すると、レコードに関するメタデータのみが返されます。 コンテンツを取得するには、#content の節を参照してください。

## 作成と更新

テンプレートの [ 作成 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/createEmailTemplateUsingPOST) または [ 更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/updateEmailTemplateContentUsingPOST) はかなり簡単です。 各テンプレートのコンテンツはHTMLドキュメントとして保存され、マルチパート/フォームデータタイプのPOSTを使用してMarketoに渡す必要があります。 [multipart](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html) および [multipart/form-data](https://www.ietf.org/rfc/rfc2388.txt) の RFC で説明されているように、境界を含む適切な Content-Type ヘッダーを渡す必要があります。

テンプレートを作成するには、名前、フォルダー、コンテンツの 3 つのパラメーターを含める必要があります。 オプションの説明パラメーターを含めることができます。  HTMLドキュメントは、コンテンツパラメーターで渡されます。このパラメーターには、従来の filename パラメーターも Content-Disposition ヘッダーの一部として含める必要があります。

```
POST /rest/asset/v1/emailTemplates.json
```

```
Content-Type: multipart/form-data; boundary=mktoBoundary1480963323998
```

```html
--mktoBoundary1480963323998
Content-Disposition: form-data; name="name"

Sample Email Template
--mktoBoundary1480963323998
Content-Disposition: form-data; name="folder"

{"id":15,"type":"Folder"}
--mktoBoundary1480963323998
Content-Disposition: form-data; name="content"; filename="testHTML.html"
Content-Type: text/html

<html>
<body>
<h1>TEST HTML</h1>
</body>
</html>

--mktoBoundary1480963323998
Content-Disposition: form-data; name="description"

Create email template using API
--mktoBoundary1480963323998--
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "a99f#14e22b2b85e",
    "result": [
        {
            "id": 1022,
            "name": "Sample Email Template",
            "description": "Create email template using API",
            "createdAt": "2015-06-23T23:13:34Z+0000",
            "updatedAt": "2015-06-23T23:13:34Z+0000",
            "url": "https://app-abm.marketo.com/#ET1022B2ZN12",
            "folder": {
                "type": "Folder",
                "value": 15,
                "folderName": "Templates"
            },
            "status": "draft",
            "workspace": "Default",
            "version": 1
        }
    ]
}
```

コンテンツの更新は、メールテンプレートの ID が必要な [ 個別のエンドポイント ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/updateEmailTemplateContentUsingPOST) を使用して行われます。 このエンドポイントでは、本文のコンテンツパラメーターの送信のみが許可されます。 更新を行うと、コンテンツパラメーターで渡される内容が、承認済みバージョンを更新する場合は新しいドラフトでメールの既存のコンテンツを完全に置き換え、アセットがドラフトのみの状態の場合は現在のドラフトを置き換えます。

```
POST /rest/asset/v1/emailTemplate/{id}/content.json
```

```
Content-Type: multipart/form-data; boundary=mktoBoundaryEiJFFFPFKK2WovsT
```

```html
--mktoBoundaryEiJFFFPFKK2WovsT
Content-Disposition: form-data; name="content"; filename="testHTML2.html"
Content-Type: text/html

<html>
<body>
<h1>TEST HTML WITH UPDATE</h1>
<div class="mktEditable"></div>
</body>
</html>
--mktoBoundaryEiJFFFPFKK2WovsT--
```

```json
{
   "success": true,
   "warnings": [ ],
   "errors": [ ],
   "requestId": "f8e2#158d0ae24f8",
   "result":[
      {
         "id":1022,
         "status":"Draft",
         "content":"<html>\n<body>\n<h1>TEST HTML WITH UPDATE</h1>\n<div class="mktEditable"></div>\n</body>\n</html>"
      }
   ]
}
```

## メタデータを更新

[ テンプレートのメタデータ、名前、説明を更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/updateEmailTemplateUsingPOST) するには、コンテンツを更新する場合と同じエンドポイントを使用できますが、代わりに、名前と説明のパラメーターを使用して application/x-www-url-formencoded POSTーを渡します。

```
POST /rest/asset/v1/emailTemplate/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
description=Updated description&name=New Name
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "17ca5#14a12ab900a",
    "result": [
        {
            "id": 19,
            "name": "New Name",
            "description": "Updated description",
            "createdAt": "2014-11-14T02:41:26Z+0000",
            "updatedAt": "2014-11-14T02:41:26Z+0000",
            "folder": {
                "type": "Folder",
                "value": 15
            },
            "status": "Draft",
            "workspace": "Default"
        }
    ]
}
```

## 承認

メールテンプレートは、アセットレコードの承認の標準パターンに従います。 ドラフトの承認、承認バージョンの未承認、メールテンプレートの既存のドラフトの破棄は、それぞれのエンドポイントで行うことができます。

### 承認

承認エンドポイントを呼び出すと、メールがMarketo メールのルールに対して検証されます。 メールを承認する前に、送信者名、送信元メール、返信先メール、件名を入力する必要があります。

```
POST /rest/asset/v1/emailTemplate/{id}/approveDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"abe2#14a1832a97d",
   "result":[
      {
         "id":338,
         "name":"lvAVYMZqPS",
         "description":"fZLJQSJRvnYbjGTUpIHHqDOuQgQzXQcWIXoOUPwrVLdMHKcbRqwLoSLkWZTUmaMiCIJSfQiufnnrgITUIqjuAPBLpmliiKuIUFYG",
         "createdAt":"2014-12-05T02:06:21Z+0000",
         "updatedAt":"2014-12-05T02:06:21Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Approved",
         "workspace":"Default"
      }
   ]
}
```

### 承認取消

未承認のエンドポイントは、承認済みテンプレートでのみ使用できます。

```
POST /rest/asset/v1/emailTemplate/{id}/unapprove.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"17bfa#14a1832b3c4",
   "result":[
      {
         "id":344,
         "name":"LkilkvKrkp",
"description":"yAyUEXuWMtdhpODUmnCkGjpBcyEKnYucxaSoTyYeQzyNbYanxCXWPOzwiIWmeXPUwjfGAUmgnxlhgOPluVqwNittuvxJmNTaHxYM",
         "createdAt":"2014-12-05T02:06:23Z+0000",
         "updatedAt":"2014-12-05T02:06:23Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      }
   ]
}
```

### 破棄

承認済みのメールが更新されると、テンプレートのドラフトバージョンが作成されます。

```
POST /rest/asset/v1/emailTemplate/{id}/discardDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"17bfa#14a1832b3c4",
   "result":[
      {
         "id":344,
         "name":"LkilkvKrkp",
         "description":"yAyUEXuWMtdhpODUmnCkGjpBcyEKnYucxaSoTyYeQzyNbYanxCXWPOzwiIWmeXPUwjfGAUmgnxlhgOPluVqwNittuvxJmNTaHxYM",
         "createdAt":"2014-12-05T02:06:23Z+0000",
         "updatedAt":"2014-12-05T02:06:23Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      }
   ]
}
```

### 削除

```
POST /rest/asset/v1/emailTemplate/{id}/delete.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"15cef#149d3de83db",
   "result":[
      {
         "id":12
      }
   ]
}
```

## クローン作成

Marketoには、（メールテンプレートのクローン [ を作成するための簡単な方法が用意されて ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/cloneTemplateUsingPOST) ます。 creating とは異なり、この種のリクエストは application/x-www-url-formencoded POSTから行われ、id と type を持つ埋め込み JSON オブジェクトである、名前とフォルダーの 2 つの必須パラメーターを受け取ります。  説明はオプションのパラメーターでもあります。

```
POST /rest/asset/v1/emailTemplate/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Sample Template 01 - deverly&folder={"id":12,"type":"Folder"}&description=This is a sample template
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "905e#14e22c693f8",
    "result": [
        {
            "id": 1024,
            "name": "Sample Template 01 - deverly",
            "description": "This is a sample template",
            "createdAt": "2015-06-23T23:35:16Z+0000",
            "updatedAt": "2015-06-23T23:35:16Z+0000",
            "url": "https://app-abm.marketo.com/#ET1024B2ZN12",
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

## メールの依存関係のクエリ

[ 使用されているメールテンプレートを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/getEmailTemplateUsedByUsingGET) エンドポイントを使用して、特定のメールテンプレートに依存するメールのリストを取得します。  `id` path パラメーターは、親メールテンプレートを指定します。

オプションのパラメーターが 2 つあります。 `maxReturn`  は結果の数を制限する整数（デフォルトは 20、最大は 200）、`offset` は大きな結果セットを読み取るために `maxReturn` で使用できる整数（デフォルトは 0）です。

```
GET /rest/asset/v1/emailTemplates/{id}/usedBy.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "18b0#16fa3344169",
    "warnings": [],
    "result": [
        {
            "id": 1022,
            "name": "EmailPr.Email2",
            "type": "Email",
            "status": "approved",
            "updatedAt": "2019-12-02T00:42:21Z+0000"
        },
        {
            "id": 1023,
            "name": "Default.Email1.email1",
            "type": "Email",
            "status": "approved",
            "updatedAt": "2019-12-02T00:42:21Z+0000"
        },
        {
            "id": 1025,
            "name": "Defa.E1",
            "type": "Email",
            "status": "draft",
            "updatedAt": "2019-12-02T00:42:21Z+0000"
        },
        {
            "id": 1052,
            "name": "Email v1 Program.Email v1 Email",
            "type": "Email",
            "status": "draft",
            "updatedAt": "2019-06-07T20:07:16Z+0000"
        }
    ]
}
```
