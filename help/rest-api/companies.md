---
title: 「会社」
feature: REST API
description: Marketo API を使用して会社データを設定します。
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 1%

---


# 企業

[会社エンドポイントのリファレンス](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies)

会社は、リードレコードが属する組織を表します。 リードは、対応するリードに入力することで会社に追加されます `externalCompanyId` を使用したフィールド [リードを同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST) または [リードの一括読み込み](bulk-lead-import.md) エンドポイント。 リードを会社に追加した後は、その会社からリードを削除することはできません（リードを別の会社に追加する場合を除く）。 会社レコードにリンクされたリードは、値がリード自身のレコードに存在していたかのように、会社レコードから値を直接継承します。

会社 API は、次の情報を持つサブスクリプションに対する読み取り専用アクセスです [SFDC 同期](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=en) または [Microsoft Dynamics Sync](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=en) が有効になっています。

## 説明

会社オブジェクトを記述すると、それらとやり取りする必要があるすべての情報を取得できます。

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

パターン [会社のクエリ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompaniesUsingGET) は、リード API のそれに厳密に従いますが、制限が追加されています。 `filterType` パラメーターには、Describe Companies 呼び出しまたは dedupeFields の searchableFields 配列にリストされているフィールドを使用できます。

`filterType` および `filterValues` は必須のクエリパラメーターです。  `fields`, `nextPageToken`、および `batchSize` はオプションのパラメーターです。  パラメーターは、Leads API と Opportunity API の対応するパラメーターと同様に機能します。 次のリストをリクエストする場合： `fields`の場合、特定のフィールドがリクエストされても返されなかった場合、値は null であることが暗示されます。

fields パラメーターを省略した場合、返されるフィールドのデフォルトセットは次のようになります。

- ID
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

この [会社の同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST) エンドポイントは必要なを受け入れます `input` company オブジェクトの配列を含むパラメーター。 商談と同様に、会社を作成および更新するモードには、createOnly、updateOnly、createOrUpdate の 3 つがあります。  モードは `action` リクエストのパラメーター。 両方 `dedupeBy` および `action` パラメーターはオプションで、デフォルトではそれぞれ dedupeFields モードと createOrUpdate モードになっています。

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

company オブジェクトには、一連のフィールドが含まれています。 各フィールド定義は、フィールドを説明する一連の属性で構成されます。 属性の例としては、表示名、API 名、データタイプがあります。 これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、company オブジェクトのフィールドに対してクエリを実行できます。 これらの API では、所有している API ユーザーが、の一方または両方の役割を持っている必要があります `Read-Write Schema Standard Field` または `Read-Write Schema Custom Field` 権限。

### クエリフィールド

会社フィールドのクエリは簡単です。 API 名で 1 つの会社フィールドに対してクエリを実行したり、すべての会社フィールドのセットに対してクエリを実行したりできます。

#### 名前別

この [名前による会社フィールドの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompanyFieldByNameUsingGET) エンドポイントは、company オブジェクトの 1 つのフィールドのメタデータを取得します。 必須 `fieldApiName` パスパラメーターは、フィールドの API 名を指定します。 応答は Describe Company エンドポイントに似ていますが、次のような追加のメタデータが含まれています `isCustom` フィールドがカスタムフィールドであるかどうかを示す属性。

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

この [会社フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompanyFieldsUsingGET) エンドポイントは、company オブジェクトのすべてのフィールドのメタデータを取得します。 デフォルトでは、最大 300 件のレコードが返されます。 を使用できます `batchSize` この数を減らすには、パラメーターをクエリします。 次の場合 `moreResult` 属性が true の場合、より多くの結果が利用可能であることを意味します。 moreResult 属性が false を返す（使用できる結果がないことを意味する）まで、このエンドポイントの呼び出しを続行します。 この `nextPageToken` この API から返された値は、この呼び出しの次の反復で常に再利用する必要があります。

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

削除条件はで指定します。 `input` 検索値のリストを含む配列。  削除方法は、で指定します。 `deleteBy` パラメーター。  指定できる値は、dedupeFields、idField です。  デフォルトは dedupeFields です。

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

- 企業エンドポイントのタイムアウトは、以下に記載されていない限り 30 秒です
   - 同期会社：60s 
   - 会社の削除：60s
