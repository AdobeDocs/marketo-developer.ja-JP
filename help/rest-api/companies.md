---
title: 会社
feature: REST API
description: Marketo会社 REST API を使用して、会社レコードの記述、クエリ、同期、フィールドの管理および externalCompanyId による重複排除を行い、CRM 同期を読み取り専用でメモします。
exl-id: 80e514a2-1c86-46a7-82bc-e4db702189b0
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 95%

---

# 会社

[会社エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies)

会社は、リードレコードが属する組織を表します。リードは、[リードを同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST)エンドポイントまたは[リードの一括読み込み](bulk-lead-import.md)エンドポイントを使用して、対応する「`externalCompanyId`」フィールドに入力することで会社に追加されます。リードを会社に追加すると、この会社からリードを削除できません（リードを別の会社に追加しない限り）。会社レコードにリンクされたリードは、リード自身のレコードに値が存在するかのように、会社レコードから値を直接継承します。

Company API は、[SFDC 同期](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=ja)または [Microsoft Dynamics 同期](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=ja)が有効になっているサブスクリプションに対して読み取り専用アクセスです。

## 説明

会社オブジェクトを説明すると、そのオブジェクトとやり取りするのに必要なすべての情報が得られます。

```
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

[会社のクエリ実行](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompaniesUsingGET)のパターンは、リード API のパターンに密接に従いますが、`filterType` パラメーターが「会社を説明」呼び出しの searchableFields 配列にリストされているフィールドや、dedupeFields を受け入れるという追加の制限があります。

`filterType` と `filterValues` は、必須のクエリパラメーターです。`fields`、`nextPageToken`、`batchSize` は、オプションのパラメーターです。パラメーターは、Leads API と Opportunity API の対応するパラメーターと同様に機能します。`fields` のリストをリクエストする際に、特定のフィールドがリクエストされたが返されない場合、その値は null であると見なされます。

fields パラメーターを省略した場合、返されるフィールドのデフォルトセットは次のようになります。

- id
- dedupeFields
- updatedAt
- createdAt

```
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

[会社を同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST)エンドポイントでは、会社オブジェクトの配列を含む必須の `input` パラメーターを受け入れます。商談と同様に、会社を作成および更新するモードには、createOnly、updateOnly、createOrUpdate の 3 つがあります。モードは、リクエストの `action` パラメーターで指定されます。`dedupeBy` パラメーターと `action` パラメーターは両方ともオプションで、デフォルトはそれぞれ dedupeFields モードと createOrUpdate モードになります。

```
POST /rest/v1/companies.json
```

```
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

会社オブジェクトには、一連のフィールドが含まれています。各フィールド定義は、フィールドを説明する属性のセットで構成されます。属性の例としては、表示名、API 名、dataType があります。これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、会社オブジェクトのフィールドに対してクエリを実行できます。これらの API では、所有する API ユーザに、`Read-Write Schema Standard Field` 権限または `Read-Write Schema Custom Field` 権限のいずれかまたは両方を含むロールを用意する必要があります。

### クエリフィールド

会社フィールドのクエリの実行は簡単です。API 名で単一の会社フィールドに対してクエリを実行することも、すべての会社フィールドのセットに対してクエリを実行することもできます。

#### 名前別

[名前による会社フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompanyFieldByNameUsingGET)エンドポイントでは、会社オブジェクトの単一フィールドのメタデータを取得します。必須の `fieldApiName` パスパラメーターは、フィールドの API 名を指定します。応答は「会社を説明」エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す `isCustom` 属性などの追加のメタデータが含まれます。

```
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

[会社フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompanyFieldsUsingGET)エンドポイントでは、会社オブジェクトのすべてのフィールドのメタデータを取得します。デフォルトでは、最大 300 個のレコードが返されます。`batchSize` クエリパラメーターを使用して、この数を減らすことができます。`moreResult` 属性が true の場合、さらに多くの結果が使用可能です。moreResult 属性が false を返すまで、つまり使用可能な結果が存在しなくなるまで、このエンドポイントを引き続き呼び出します。この API から返される `nextPageToken` は、この呼び出しの次の反復で常に再利用する必要があります。

```
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

削除条件は、検索値のリストを含む `input` 配列で指定します。削除メソッドは、`deleteBy` パラメーターで指定されます。指定できる値は、dedupeFields、idField です。デフォルトは dedupeFields です。

```
Content-Type: application/json
```

```
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

- 会社エンドポイントは、以下に記載されていない限り、タイムアウトが 30 秒になります。
   - 同期会社：60s
   - 会社を削除：60 秒
