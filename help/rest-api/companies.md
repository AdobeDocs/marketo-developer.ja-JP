---
title: 企業
feature: REST API
description: Marketo API を使用して会社データを設定します。
exl-id: 80e514a2-1c86-46a7-82bc-e4db702189b0
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 1%

---

# 企業

[ 会社エンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies)

会社は、リードレコードが属する組織を表します。 リードは、「リードを同期」または「リードを一括で読み込み [ エンドポイントを使用して、対応する `externalCompanyId` フィールドに値を入力す ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST)[ ことで、会社に追加さ ](bulk-lead-import.md) ます。 リードを会社に追加した後は、その会社からリードを削除することはできません（リードを別の会社に追加する場合を除く）。 会社レコードにリンクされたリードは、値がリード自身のレコードに存在していたかのように、会社レコードから値を直接継承します。

会社 API は、{SFDC 同期 [ または ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=en)2}Microsoft Dynamics 同期 } が有効になっている購読の読み取り専用アクセス ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=en) す。[

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

[ 会社のクエリ ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompaniesUsingGET) のパターンは、Describe Companies 呼び出し（dedupeFields）の searchableFields 配列にリストされているフィールドを `filterType` パラメーターが受け入れる制限が追加されたリード API のパターンによく似ています。

`filterType` と `filterValues` は必須のクエリパラメーターです。  `fields`、`nextPageToken`、`batchSize` はオプションのパラメーターです。  パラメーターは、Leads API と Opportunity API の対応するパラメーターと同様に機能します。 `fields` のリストをリクエストするときに、特定のフィールドがリクエストされても返されなかった場合、値は null であることが暗示されます。

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

[ 会社の同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST) エンドポイントは、会社オブジェクトの配列を含む必須の `input` パラメーターを受け入れます。 商談と同様に、会社を作成および更新するモードには、createOnly、updateOnly、createOrUpdate の 3 つがあります。  モードは、リクエストの `action` パラメーターで指定します。 `dedupeBy` パラメーターと `action` パラメーターは両方ともオプションで、デフォルトではそれぞれ dedupeFields モードと createOrUpdate モードになっています。

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

次のエンドポイントを使用すると、company オブジェクトのフィールドに対してクエリを実行できます。 これらの API では、所有している API ユーザーが、`Read-Write Schema Standard Field` の権限または `Read-Write Schema Custom Field` の権限の一方または両方の役割を持っている必要があります。

### クエリフィールド

会社フィールドのクエリは簡単です。 API 名で 1 つの会社フィールドに対してクエリを実行したり、すべての会社フィールドのセットに対してクエリを実行したりできます。

#### 名前別

[ 名前による会社フィールドの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompanyFieldByNameUsingGET) エンドポイントは、会社オブジェクト上の 1 つのフィールドのメタデータを取得します。 必須の `fieldApiName` パスパラメーターは、フィールドの API 名を指定します。 応答は、Describe Company エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す `isCustom` 属性などの追加メタデータが含まれています。

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

[ 会社フィールドを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompanyFieldsUsingGET) エンドポイントは、会社オブジェクト上のすべてのフィールドのメタデータを取得します。 デフォルトでは、最大 300 件のレコードが返されます。 `batchSize` クエリパラメーターを使用して、この数を減らすことができます。 `moreResult` 属性が true の場合は、より多くの結果が利用可能であることを意味します。 moreResult 属性が false を返す（使用できる結果がないことを意味する）まで、このエンドポイントの呼び出しを続行します。 この API から返された `nextPageToken` は、この呼び出しの次のイテレーションでは常に再利用する必要があります。

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

削除条件は、検索値のリストを含む `input` 配列で指定します。  削除方法は、`deleteBy` パラメーターで指定します。  指定できる値は、dedupeFields、idField です。  デフォルトは dedupeFields です。

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
