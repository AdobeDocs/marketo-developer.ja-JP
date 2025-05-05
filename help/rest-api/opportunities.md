---
title: 商談
feature: REST API
description: 'Marketo API を使用してオポチュニティを設定します。'
exl-id: 46451285-4125-4857-890a-575069a68288
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# 商談

[ 商談エンドポイントの参照 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities)

Marketoは、商談レコードの読み取り、書き込み、作成、更新のための API を公開しています。 Marketoでは、商談レコードは中間の商談ロールオブジェクトを通じてリードおよび連絡先レコードにリンクされるので、1 つの商談が多数の個々のリードにリンクされることがあります。  これらのオブジェクトタイプは両方とも API を通じて公開され、ほとんどのリードデータベースオブジェクトタイプと同様に、両方とも対応する Describe 呼び出しを持ち、オブジェクトタイプに関するメタデータを返します。

商談 API は、{SFDC 同期 [ または ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=en)2}Microsoft Dynamics 同期 &rbrace; が有効になっている購読の読み取り専用アクセ [&#128279;](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=en) です。

## 説明

商談レコードの記述は、リードデータベースオブジェクトの標準パターンに従います。

```
GET /rest/v1/opportunities/describe.json
```

```json
{  
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[  
      {  
         "name":"opportunity",
         "displayName":"Opportunity",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"marketoGUID",
         "dedupeFields":[  
            "externalOpportunityId"
         ],
         "searchableFields":[  
            [  
               "externalOpportunityId"
            ],
            [  
               "marketoGUID"
            ]
         ],
         "fields":[  
            {  
               "name":"marketoGUID",
               "displayName":"Marketo GUID",
               "dataType":"string",
               "length":36,
               "updateable":false
            },
            {  
               "name":"createdAt",
               "displayName":"Created At",
               "dataType":"datetime",
               "updateable":false
            },
            {  
               "name":"updatedAt",
               "displayName":"Updated At",
               "dataType":"datetime",
               "updateable":false
            },
            {  
               "name":"externalOpportunityId",
               "displayName":"External Opportunity Id",
               "dataType":"string",
               "length":50,
               "updateable":false
            }
         ]
      }
   ]
}
```

この応答タイプで最も重要なフィールドは、`idField`、`dedupeFields` および `searchableFields` です。  idField 商談のプライマリキー、marketoGUID を示します。  これは、システムで生成された一意のキーで、読み取りと更新の操作に使用できますが、システムで管理されているので、挿入には使用できません。  dedupeFields 配列は、挿入操作に有効なキーであるフィールドを示します。商談の場合、これは externalOpportunityId のみです。  searchableFields 配列は、クエリ、externalOpportunityId および marketoGUID に有効なフィールドのセットを提供します。

## クエリ

[ オポチュニティのクエリ ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunitiesUsingGET) のパターンは、リード API のパターンに密接に続いており、`filterType` パラメーターが、`searchableFields` 配列にリストされたフィールド、対応する describe 呼び出し、または dedupeFields を受け入れることを制限が追加されています。  カスタムの商談フィールドを使用している場合、文字列または整数タイプのカスタム商談フィールドのみが searchableFields 配列に一覧表示されます。

```
GET /rest/v1/opportunities.json?filterType=marketoGUID&filterValues=dff23271-f996-47d7-984f-f2676861b5fa&dff23271-f996-47d7-984f-f2676861b5fc,dff23271-f996-47d7-984f-f2676861b5fb
```

```json
{  
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[  
      {  
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fa ",
         "externalOpportunityId":"19UYA31581L000000",
         "name":"Chairs",
         "description":"Chairs",
         "amount":"1604.47",
         "source":"Inbound Sales Call/Email"
      },
      {  
         "seq":1,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fc ",
         "externalOpportunityId":"29UYA31581L000000",
         "name":"Big Dog Day Care-Phase12",
         "description":"Big Dog Day Care-Phase12",
         "amount":"1604.47",
         "source":"Email"
      }
   ]
}
```

オプションのクエリパラメーター `fields` を含めることもできます。これは、追加の商談フィールドを返す場合、`nextPageToken`、バッチサイズより大きいセットをページングする場合に使用できます。バッチサイズは `batchSize` で、デフォルトは最大 300 です。  `fields` のリストをリクエストするときに、特定のフィールドがリクエストされても返されなかった場合、値は null であることが暗示されます。

## 作成と更新

オポチュニティは、いくつかの制限を除き、リード API パターンに厳密に従います。  `action` に使用できる値は、createOnly、createOrUpdate、updateOnly です。  createOnly または createOrUpdate モードを使用する場合は、各レコードに externalOpportunityId フィールドを含める必要があります。  updateOnly モードの場合は、marketoGUID または externalOpportunityId を使用できます。  未指定の場合、モードのデフォルト値は createOrUpdate です。

リード API の `lookupField` パラメーターは使用できず、dedupeBy パラメーターに置き換えられます。このパラメーターは、action が updateOnly の場合にのみ有効です。  dedupeBy に使用できる値は、「dedupeFields」または「idField」です。これらは、それぞれ describe 呼び出しで externalOpportunityId および marketoGUID として指定します。  dedupeBy を指定しない場合は、デフォルトで dedupeFields モードになります。  「名前」フィールドは null にしないでください。

一度に最大 300 件のレコードを送信できます。

```
POST /rest/v1/opportunities.json
```

```json
{  
   "action":"createOrUpdate",
   "dedupeBy":"dedupeFields",
   "input":[  
      {  
         "externalOpportunityId":"19UYA31581L000000",
         "name":"Chairs",
         "description":"Chairs",
         "amount":"1604.47",
         "source":"Inbound Sales Call/Email"
      },
      {  
         "externalOpportunityId":"29UYA31581L000000",
         "name":"Big Dog Day Care-Phase12",
         "description":"Big Dog Day Care-Phase12",
         "amount":"1604.47",
         "source":"Email"
      }
   ]
}
```

```json
{  
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[  
      {  
         "seq":0,
         "status":"updated",
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {  
         "seq":1,
         "status":"created",
         "marketoGUID":"cff23271-f996-47d7-984f-f2676861b5fb"
      }
   ]
}
```

API は、各レコードの `marketoGUID`、各レコードの個々の成功または失敗を示す `status` フィールド、送信されたレコードを応答の順序に関連付けるために使用される `seq` フィールドを使用して応答します。  フィールドの数値は、リクエストで送信されたレコードのインデックスです。

### フィールド

company オブジェクトには、一連のフィールドが含まれています。  各フィールド定義は、フィールドを記述する一連の属性で構成されます。  属性の例としては、表示名、API 名、データタイプがあります。  これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、company オブジェクトのフィールドに対してクエリを実行できます。 これらの API では、所有している API ユーザーが、`Read-Write Schema Standard Field` の権限または `Read-Write Schema Custom Field` の権限の一方または両方の役割を持っている必要があります。

### クエリフィールド

商談フィールドのクエリは簡単です。  API 名で 1 つの会社フィールドに対してクエリを実行したり、すべての会社フィールドのセットに対してクエリを実行したりできます。

#### 名前別

[ 名前による商談フィールドの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunityFieldByNameUsingGET) エンドポイントは、会社オブジェクト上の 1 つのフィールドのメタデータを取得します。  必須の `fieldApiName` パスパラメーターは、フィールドの API 名を指定します。  この応答は商談の説明エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す `isCustom` 属性などの追加メタデータが含まれています。

```
GET /rest/v1/opportunities/schema/fields/externalOpportunityId.json
```

```json
{
    "requestId": "12331#17e9779cb4b",
    "result": [
        {
            "displayName": "SFDC Oppty Id",
            "name": "externalOpportunityId",
            "description": null,
            "dataType": "string",
            "length": 50,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true
}
```

#### 参照

[ 商談フィールドを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunityFieldsUsingGET) エンドポイントは、会社オブジェクト上のすべてのフィールドのメタデータを取得します。  デフォルトでは、最大 300 件のレコードが返されます。  `batchSize` クエリパラメーターを使用して、この数を減らすことができます。  `moreResult` 属性が true の場合は、より多くの結果が利用可能であることを意味します。  moreResult 属性が false を返す（使用できる結果がないことを意味する）まで、このエンドポイントの呼び出しを続行します。  この API から返された `nextPageToken` は、この呼び出しの次のイテレーションでは常に再利用する必要があります。

```
GET /rest/v1/opportunities/schema/fields.json?batchSize=5
```

```json
{
    "requestId": "b4a#17e995b31da",
    "result": [
        {
            "displayName": "SFDC Oppty Id",
            "name": "externalOpportunityId",
            "description": null,
            "dataType": "string",
            "length": 50,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Name",
            "name": "name",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Description",
            "name": "description",
            "description": null,
            "dataType": "string",
            "length": 2000,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Type",
            "name": "type",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Stage",
            "name": "stage",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true,
    "nextPageToken": "E5ZONGE4SAHALYYW6FS25KB5BM======",
    "moreResult": true
}
```

#### 削除

商談は、重複排除フィールドまたは ID フィールドで削除できます。 値が dedupeFields または idField の `deleteBy` パラメーターを使用して指定します。 指定しない場合、デフォルトは dedupeFields です。 リクエスト本文には、削除するオポチュニティの `input` 配列が含まれます。 1 回の呼び出しにつき最大 300 の機会が許可されます。

```
POST /rest/v1/opportunities/delete.json
```

```json
{ 
   "deleteBy":"dedupeFields",
   "input":[ 
      { 
         "externalOpportunityId":"19UYA31581L000000"
      },
      { 
         "externalOpportunityId":"29UYA31581L000000"
      }
   ]
}
```

```json
{ 
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[ 
      { 
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "status":"deleted"
      },
      { 
         "seq":1,
         "marketoGUID":"cff23271-f996-47d7-984f-f2676861b5fb",
         "status":"deleted"
      }
   ]
}
```

## タイムアウト

- 以下に示さない限り、商談エンドポイントのタイムアウトは 30 秒です
   - 同期の機会：60 秒 
   - 商談を削除：60s
