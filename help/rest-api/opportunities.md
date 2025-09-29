---
title: 商談
feature: REST API
description: Marketo REST API でオポチュニティ、重複排除および検索可能なフィールド、制限、SFDCまたは Dynamics sync による読み取り専用動作を記述、クエリ、作成および更新できます。
exl-id: 46451285-4125-4857-890a-575069a68288
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 96%

---

# 商談

[商談エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities)

Marketo は、商談レコードの読み取り、書き込み、作成、更新の API を公開します。Marketo では、商談レコードは中間の商談ロールオブジェクトを通じてリードレコードと取引先責任者レコードにリンクされるので、商談は多数の個別のリードにリンクされる場合があります。これらのオブジェクトタイプは、両方とも API を通じて公開され、ほとんどのリードデータベースオブジェクトタイプと同様に、どちらにも対応する Describe 呼び出しがあり、オブジェクトタイプに関するメタデータを返します。

Opportunity API は、[SFDC 同期](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=ja)または [Microsoft Dynamics 同期](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=ja)が有効になっているサブスクリプションに対して読み取り専用アクセスです。

## 説明

商談レコードの説明は、リードデータベースオブジェクトの標準パターンに従います。

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

この応答タイプで最も重要なフィールドは、`idField`、`dedupeFields` および `searchableFields` です。idField は、商談のプライマリキーである marketoGUID を示します。これは、システムによって生成された一意のキーで、読み取りと更新の操作に使用できますが、システムで管理されているので、挿入には使用できません。dedupeFields 配列は、挿入操作の有効なキーであるフィールドを示します。商談の場合、これは externalOpportunityId のみです。searchableFields 配列は、クエリの実行に有効なフィールドのセットの externalOpportunityId および marketoGUID を提供します。

## クエリ

[商談のクエリ実行](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunitiesUsingGET)のパターンは、リード API のパターンに密接に従いますが、`filterType` パラメーターが `searchableFields` 配列や対応する説明呼び出しまたは dedupeFields にリストされているフィールドを受け入れるという追加の制限があります。カスタム商談フィールドを使用している場合、searchableFields 配列には文字列または整数タイプのカスタム商談フィールドのみがリストされます。

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

また、追加の商談フィールドを返すオプションのクエリパラメーター `fields` や、バッチサイズ `batchSize`（デフォルトは 300、最大値は 300）より大きいセットをページングする `nextPageToken` を含めることもできます。`fields` のリストをリクエストする際に、特定のフィールドがリクエストされたが返されない場合、その値は null であると見なされます。

## 作成と更新

商談は、リード API パターンに密接に従っていますが、いくつかの制限があります。`action` に使用できる値は、createOnly、createOrUpdate、updateOnly です。createOnly または createOrUpdate モードを使用する場合は、各レコードに externalOpportunityId フィールドを含める必要があります。updateOnly モードの場合、marketoGUID または externalOpportunityId のいずれかを使用できます。指定しない場合、モードはデフォルトで createOrUpdate です。

リード API の `lookupField` パラメーターは使用できず、アクションが updateOnly の場合にのみ有効な dedupeBy パラメーターに置き換えられます。dedupeBy に使用できる値は、&quot;dedupeFields&quot; または &quot;idField&quot; のいずれかで、describe 呼び出しによってそれぞれ externalOpportunityId と marketoGUID として指定されます。dedupeBy を指定しない場合、デフォルトで dedupeFields モードになります。「name」フィールドは null にしないでください。

一度に最大 300 個のレコードを送信できます。

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

API は、各レコードの `marketoGUID` と、各レコードの個別の成功または失敗を示す「`status`」フィールド、送信したレコードを応答順序の関連付け使用される「`seq`」フィールドで応答します。フィールドの数値は、リクエストで送信したレコードのインデックスです。

### フィールド

会社オブジェクトには、一連のフィールドが含まれています。各フィールド定義は、フィールドを説明する属性のセットで構成されます。属性の例としては、表示名、API 名、dataType があります。これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、会社オブジェクトのフィールドに対してクエリを実行できます。これらの API では、所有する API ユーザに、`Read-Write Schema Standard Field` 権限または `Read-Write Schema Custom Field` 権限のいずれかまたは両方を含むロールを用意する必要があります。

### クエリフィールド

商談フィールドのクエリの実行は簡単です。API 名で単一の会社フィールドに対してクエリを実行することも、すべての会社フィールドのセットに対してクエリを実行することもできます。

#### 名前別

[名前による商談フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunityFieldByNameUsingGET)エンドポイントでは、会社オブジェクトの単一フィールドのメタデータを取得します。必須の `fieldApiName` パスパラメーターは、フィールドの API 名を指定します。応答は「商談を説明」エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す `isCustom` 属性などの追加のメタデータが含まれます。

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

[商談フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunityFieldsUsingGET)エンドポイントでは、会社オブジェクトのすべてのフィールドのメタデータを取得します。デフォルトでは、最大 300 個のレコードが返されます。`batchSize` クエリパラメーターを使用して、この数を減らすことができます。`moreResult` 属性が true の場合、さらに多くの結果が使用可能です。moreResult 属性が false を返すまで、つまり使用可能な結果が存在しなくなるまで、このエンドポイントを引き続き呼び出します。この API から返される `nextPageToken` は、この呼び出しの次の反復で常に再利用する必要があります。

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

商談は、重複排除フィールドまたは ID フィールドで削除できます。dedupeFields または idField のいずれかの値を持つ `deleteBy` パラメーターを使用して指定します。指定しない場合、デフォルトは dedupeFields です。リクエスト本文には、削除する商談の `input` 配列が含まれます。1 回の呼び出しにつき最大 300 個の商談が許可されます。

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

- 「商談」エンドポイントは、以下に記載されていない限り、タイムアウトが 30 秒になります。
   - 同期の機会：60 秒
   - 商談を削除：60 秒
