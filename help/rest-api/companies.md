---
title: 会社
feature: REST API
description: Marketo Companies REST APIを使用して、会社レコードの記述、クエリ、同期、フィールドの管理、externalCompanyIdによる重複排除、CRM同期の読み取り専用へのメモ作成を行います。
exl-id: 80e514a2-1c86-46a7-82bc-e4db702189b0
TQID: https://experienceleague.adobe.com/LdJYN4lx9JfcE-02zTz8ktfYXm4EdPtxMYOx9gGR0sg
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 582
ht-degree: 14%

---

# 会社

[会社エンドポイントリファレンス](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies)

企業は、リードレコードが属する組織を表します。 会社にリードを追加するには、[ リードの同期](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/syncLeadUsingPOST)または[ リードの一括読み込み](bulk-lead-import.md) エンドポイントを使用して、その`externalCompanyId` フィールドに入力します。

別の会社にリードを追加しない限り、会社からリードを削除することはできません。 会社レコードにリンクされたリードは、そのレコードから値を継承し、その値がリードレコードに存在するかのように処理します。

企業APIは、[Microsoft Dynamics Sync](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=ja)または[SFDC Sync](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=ja)が有効になっているサブスクリプションに対して、読み取り専用アクセスを提供します。

## 説明

会社レコードを操作するために必要な情報を取得する会社オブジェクトを記述します。

```http
GET /rest/v1/companies/describe.json
```

```json
{
   "success":true,
   "requestId":"5847#14d44113ad7",
   "result":[
      {
         "name":"Company",
         "description":"Company object",
         "createdAt":"2015-05-11T17:11:32Z",
         "updatedAt":"2015-05-11T17:11:32Z",
         "idField":"id",
         "dedupeFields":[
            "externalCompanyId"
         ],
         "searchableFields":[
            [
               "externalCompanyId"
            ],
            [
               "id"
            ],
            [
               "company"
            ]
         ],
         "fields":[
            {
               "name":"createdAt",
               "displayName":"Created At",
               "dataType":"datetime",
               "updateable":false
            },
            {
               "name":"externalCompanyId",
               "displayName":"External Company Id",
               "dataType":"string",
               "length":100,
               "updateable":false
            },
            {
               "name":"id",
               "displayName":"Id",
               "dataType":"integer",
               "updateable":false
            },
            {
               "name":"updatedAt",
               "displayName":"Updated At",
               "dataType":"datetime",
               "updateable":false
            },
            {
               "name":"annualRevenue",
               "displayName":"Annual Revenue",
               "dataType":"currency",
               "updateable":true
            }
            {
               "name":"company",
               "displayName":"Company Name",
               "dataType":"string",
               "length":255,
               "updateable":true
            }
         ]
      }
   ]
}
```

## クエリ

[企業](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/getCompaniesUsingGET)のクエリのパターンは、リード APIに密接に従っています。 ただし、`filterType` パラメーターは、Describe Companies レスポンスまたはdedupeFieldsのsearchableFields配列にリストされているフィールドのみを受け入れます。

クエリパラメーターは次のとおりです。

- `filterType`と`filterValues`：必須パラメーター。
- `fields`、`nextPageToken`、および`batchSize`: リードと商談APIの対応するパラメーターと同様に機能するオプションのパラメーター。

`fields`のリストをリクエストする場合、返されないリクエストされたフィールドの暗黙的な値はnullです。

fields パラメーターを省略すると、応答はデフォルトで次のフィールドを返します。

- id
- dedupeFields
- updatedAt
- createdAt

```http
GET /rest/v1/companies.json?filterType=id&filterValues=3433,5345
```

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "id":3433,
         "externalCompanyId":"19UYA31581L000000",
         "company":"Google"
      },
      {
         "seq":1,
         "id":5345,
         "externalCompanyId":"29UYA31581L000000",
         "company":"Yahoo"
      }
   ]
}
```

## 作成と更新

[Sync Companies](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/syncCompaniesUsingPOST) エンドポイントは、会社オブジェクトの配列を含む必須の`input` パラメーターを受け入れます。

商談と同様に、エンドポイントは3つの作成モードと更新モード（createOnly、updateOnly、createOrUpdate）をサポートしています。 リクエストの`action` パラメーターでモードを指定します。

`dedupeBy`および`action` パラメーターはオプションです。 デフォルトでは、それぞれdedupeFieldsとcreateOrUpdateです。

```http
POST /rest/v1/companies.json
```

```text
Content-Type: application/json
```

```json
{
   "action":"createOrUpdate",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "externalCompanyId":"19UYA31581L000000",
         "company":"Google"
      },
      {
         "externalCompanyId":"29UYA31581L000000",
         "company":"Yahoo"
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
         "id":1232
      },
      {
         "seq":1,
         "status":"created",
         "id":1323
      }
   ]
}
```

### フィールド

company オブジェクトには、表示名、API名、dataTypeなどの属性で定義されたフィールドが含まれます。 これらの属性をメタデータと呼びます。

次のエンドポイントは、会社オブジェクトのフィールドをクエリします。 API ユーザーには、`Read-Write Schema Standard Field`権限、`Read-Write Schema Custom Field`権限、またはその両方を持つ役割が必要です。

### クエリフィールド

API名で1つの会社フィールドをクエリするか、すべての会社フィールドを取得します。

#### 名前別

[名前で会社フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/getCompanyFieldByNameUsingGET) エンドポイントは、会社オブジェクトの1つのフィールドのメタデータを取得します。 必須の`fieldApiName` パスパラメーターは、フィールドのAPI名を指定します。

応答はDescribe Company応答に似ていますが、追加のメタデータが含まれています。 例えば、`isCustom`属性は、フィールドがカスタムかどうかを示します。

```http
GET /rest/v1/companies/schema/fields/industry.json
```

```json
{
    "requestId": "88f6#17e976d6ab4",
    "result": [
        {
            "displayName": "Industry",
            "name": "industry",
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
    "success": true
}
```

#### 参照

[会社フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/getCompanyFieldsUsingGET)エンドポイントでは、会社オブジェクトのすべてのフィールドのメタデータを取得します。 デフォルトでは、最大300件のレコードが返されます。 この数を減らすには、`batchSize` クエリパラメーターを使用します。

`moreResult` 属性が true の場合、さらに多くの結果が使用可能です。 `moreResult`がfalseになるまで、返された`nextPageToken`でエンドポイントの呼び出しを続行します。

```http
GET /rest/v1/companies/schema/fields.json?batchSize=5
```

```json
{
    "requestId": "b50e#17e995c2d35",
    "result": [
        {
            "displayName": "Company Name",
            "name": "company",
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
            "displayName": "Site",
            "name": "site",
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
            "displayName": "Website",
            "name": "website",
            "description": null,
            "dataType": "url",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Main Phone",
            "name": "mainPhone",
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
            "displayName": "Annual Revenue",
            "name": "annualRevenue",
            "description": null,
            "dataType": "currency",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true,
    "nextPageToken": "L7XD3EFJ3OLFZKXKJBWYULOTRA======",
    "moreResult": true
}
```

### 削除

削除条件を`input`配列内の検索値のリストとして指定します。 `deleteBy` パラメーターで削除方法を指定します。

許可される値はdedupeFieldsとidFieldです。 デフォルトはdedupeFieldsです。

```text
Content-Type: application/json
```

```http
POST /rest/v1/companies/delete.json
```

```json
{
   "deleteBy":"dedupeFields",
   "input":[
      {
         "externalCompanyId":"19UYA31581L000000"
      },
      {
         "externalCompanyId":"29UYA31581L000000"
      },
      {
         "externalCompanyId":"39UYA31581L000000"
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
         "id":1234,
         "status":"deleted"
      },
      {
         "seq":1,
         "id":56456,
         "status":"deleted"
      },
      {
         "seq":2,
         "status":"skipped",
         "reasons":[
            {
               "code":"1013",
               "message":"Record not found"
            }
         ]
      }
   ]
}
```

## タイムアウト

- 特に明記されていない限り、企業エンドポイントのタイムアウトは30秒です。
- Sync Companiesのタイムアウトは60秒です。
- Delete Companiesのタイムアウトは60秒です。
