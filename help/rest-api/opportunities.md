---
title: 商談
feature: REST API
description: Marketo REST APIを使用して、SFDCまたはDynamics syncで商談の記述、クエリ、作成、更新、重複排除および検索可能なフィールド、制限、読み取り専用の動作を実行できます。
exl-id: 46451285-4125-4857-890a-575069a68288
TQID: https://experienceleague.adobe.com/rBDJcXWQrN5qyKRWHyzVC-sc9BH2mQFLm7fKUk-NUn8
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 708
ht-degree: 16%

---

# 商談

[商談エンドポイントの参照](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities)

Marketoには、商談レコードの読み取り、書き込み、作成、更新のためのAPIが用意されています。 Marketoでは、中間のOpportunity Role オブジェクトは、商談レコードをリードおよび連絡先レコードにリンクします。 商談は、多くの個々のリードにリンクできます。

APIは両方のオブジェクトタイプを公開します。 ほとんどのリードデータベースオブジェクトタイプと同様に、各オブジェクトタイプには、オブジェクトメタデータを返す対応するDescribe呼び出しがあります。

商談APIは、[Microsoft Dynamics Sync](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=ja)または[SFDC Sync](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=ja)が有効になっているサブスクリプションに対して、読み取り専用アクセスを提供します。

## 説明

リード データベース オブジェクトの標準パターンを使用して、商談レコードを記述します。

```http
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

キー応答フィールドは次のとおりです。

- `idField`：商談のプライマリキーであるmarketoGUIDを特定します。 このシステム生成キーは、読み取りと更新の操作をサポートしていますが、挿入はサポートしていません。
- `dedupeFields`：挿入操作の有効なキーを特定します。 商談の場合、唯一のキーはexternalOpportunityIdです。
- `searchableFields`: クエリに有効なフィールドを特定します。 これらのフィールドはexternalOpportunityIdおよびmarketoGUIDです。

## クエリ

[商談のクエリ ](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities/operation/getOpportunitiesUsingGET)のパターンは、リード APIに密接に従っています。 ただし、`filterType` パラメーターは、対応するDescribe応答またはdedupeFieldsの`searchableFields`配列にリストされているフィールドのみを受け入れます。

カスタム商談フィールドの場合、検索可能なFields配列に表示されるのは、String型またはInteger型のフィールドのみです。

```http
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

次のオプションのクエリパラメーターを含めることができます。

- `fields`：追加の商談フィールドを返します。
- `nextPageToken`: バッチサイズよりも大きい結果セットをページ化します。
- `batchSize`: バッチサイズを指定します。 デフォルト値と最大値は300です。

`fields`のリストをリクエストする場合、返されないリクエストされたフィールドの暗黙的な値はnullです。

## 作成と更新

オポチュニティは、リード API パターンに従い、いくつかの制限があります。 `action`の値は、createOnly、createOrUpdate、およびupdateOnlyです。

- createOnly モードまたはcreateOrUpdate モードの場合は、各レコードにexternalOpportunityId フィールドを含めます。
- updateOnly モードには、marketoGUIDまたはexternalOpportunityIdのいずれかを使用します。
- 指定しない場合、モードはデフォルトでcreateOrUpdateになります。

リード APIの`lookupField` パラメーターは使用できません。 dedupeBy パラメーターは、アクションがupdateOnlyの場合にのみ有効です。

dedupeByの値は「dedupeFields」と「idField」で、Describeの応答はそれぞれexternalOpportunityIdとmarketoGUIDとして識別されます。 dedupeBy を指定しない場合、デフォルトで dedupeFields モードになります。 「name」フィールドは null にしないでください。

一度に最大 300 個のレコードを送信できます。

```http
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

応答には、各レコードに次の値が含まれます。

- `marketoGUID`: レコード ID。
- `status`：個々のレコードの成功または失敗。
- `seq`：送信されたレコードのインデックス。リクエスト レコードと応答順序を関連付けます。

### フィールド

company オブジェクトには、表示名、API名、dataTypeなどの属性で定義されたフィールドが含まれます。 これらの属性をメタデータと呼びます。

次のエンドポイントは、会社オブジェクトのフィールドをクエリします。 API ユーザーには、`Read-Write Schema Standard Field`権限、`Read-Write Schema Custom Field`権限、またはその両方を持つ役割が必要です。

### クエリフィールド

API名で1つの会社フィールドをクエリするか、すべての会社フィールドを取得します。

#### 名前別

[名前で商談フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities/operation/getOpportunityFieldByNameUsingGET) エンドポイントは、会社オブジェクトの1つのフィールドのメタデータを取得します。 必須の`fieldApiName` パスパラメーターは、フィールドのAPI名を指定します。

応答はDescribe Opportunity応答に似ていますが、追加のメタデータが含まれています。 例えば、`isCustom`属性は、フィールドがカスタムかどうかを示します。

```http
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

[商談フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities/operation/getOpportunityFieldsUsingGET)エンドポイントでは、会社オブジェクトのすべてのフィールドのメタデータを取得します。 デフォルトでは、最大300件のレコードが返されます。 この数を減らすには、`batchSize` クエリパラメーターを使用します。

`moreResult` 属性が true の場合、さらに多くの結果が使用可能です。 返された`nextPageToken`でエンドポイントの呼び出しを続行し、moreResultがfalseになるまで呼び出します。

```http
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

重複排除フィールドまたはID フィールドで商談を削除します。 `deleteBy` パラメーターをdedupeFieldsまたはidFieldのいずれかに設定します。 デフォルトはdedupeFieldsです。

リクエスト本文には、削除する商談の `input` 配列が含まれます。 1回の呼び出しごとに最大300件の商談を許可します。

```http
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

- 特に明記されていない限り、商談エンドポイントのタイムアウトは30秒です。
- Sync Opportunitiesのタイムアウトは60秒です。
- Delete Opportunitiesのタイムアウトは60秒です。
