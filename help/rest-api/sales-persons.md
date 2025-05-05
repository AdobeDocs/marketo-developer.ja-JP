---
title: 販売担当者
feature: REST API
description: 営業担当者に関するデータを読み取ります。
exl-id: f8ed5aa5-63c1-4c5b-8683-bf47eed1ea18
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---

# 販売担当者

[ 販売担当者エンドポイントの参照 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Sales-Persons)

営業担当者 API は、[SFDC 同期 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync) または [Microsoft Dynamics 同期 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync) が有効になっている購読に対する読み取り専用アクセスです。 営業担当者は、引合レコードの販売所有者である個人レコードのタイプです。 これらは、各リードレコードの externalSalesPersonId フィールドによってリードレコードに関連付けられています。 設定された externalSalesPersonId フィールドによってリードが販売担当者に関連付けられると、対応するリードオーナー検索フィールドにMarketoのそのリードレコードが設定され、対応するフィルターおよびトークンを使用できるようになります。

販売担当者は、[ 同期リード ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST) エンドポイントを使用し、externalSalesPersonId 属性を渡すことで、リードレコードに関連付けられます。

営業担当者は、[ 商談の同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/syncOpportunitiesUsingPOST) エンドポイントを使用し、externalSalesPersonId 属性を渡すことで、商談レコードに関連しています。

販売担当者は、[ 会社の同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST) エンドポイントを使用し、externalSalesPersonId 属性を渡すことで、会社レコードに関連付けられます。

販売担当者レコードは、API からのみ編集できます。

## 説明

営業担当者レコードの記述は、引合データベース・オブジェクトの標準パターンに従います。

```
GET /rest/v1/salespersons/describe.json
```

```json
{  
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[  
      {  
         "name":"SalesPerson",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"id",
         "dedupeFields":[  
            "externalSalesPersonId"
         ],
         "searchableFields":[  
            [  
               "email"
            ],
            [  
               "id"
            ],
            [
               "externalSalesPersonId"
            ]
         ],
         "fields":[  
            {  
               "name":"id",
               "displayName":"Marketo Id",
               "dataType":"integer",
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
               "name":"email",
               "displayName":"Email",
               "dataType":"string",
               "length":255,
               "updateable":false
            },
            {  
               "name":"externalSalesPersonId",
               "displayName":"External Sales Person Id",
               "dataType":"string",
               "length":255,
               "updateable":false
            }
         ]
      }
   ]
}
```

デフォルトでは、販売担当者の `idField` は「id」で、`dedupeFields` は単に「externalSalesPersonId」です。

## クエリ

シンプルなキーに対する標準的なクエリパターンを使用する販売担当者。 次の例では、ユーザーのメールを externalSalesPersonId として使用しています。 デフォルトでは、クエリは、返されたレコードに対して入力されたすべてのフィールドを返します。

```
GET /rest/v1/salespersons.json?filterType=dedupeFields&filterValues=david@test.com,sam@test.com
```

```json
 {  
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[  
      {  
         "seq":0,
         "id":53453,
         "externalSalesPersonId":"sam@test.com",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:23Z"
      },
      {  
         "seq":1,
         "id":53454,
         "externalSalesPersonId":"david@test.com",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:23Z"
      }
   ]
}
```

## 作成と更新

更新のパターンは標準です。

```
POST /rest/v1/salespersons.json
```

```json
{
   "action":"createOrUpdate",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "externalSalesPersonId":"sam@test.com",
         "email":"sam@test.com",
         "firstName":"Sam",
         "lastName":"Sanosin"
      },
      {
         "externalSalesPersonId":"david@test.com",
         "email":"david@test.com",
         "firstName":"David",
         "lastName":"Aulassak"
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
         "status": "updated",
         "id":45232
      },
      {
         "seq":1,
         "status": "created",
         "id":45236
      }
   ]
}
```

## 削除

削除のパターンは標準です。

「使用中」の場合、販売担当者の削除は許可されません。 この場合、販売担当者はスキップされます。 例:

- 販売担当者がアクティブなリードに関連付けられている場合
- 販売担当者が削除された会社に関連付けられている場合

```
POST /rest/v1/salespersons/delete.json
```

```json
{  
   "deleteBy":"dedupeFields",
   "input":[  
      {  
         "externalSalesPersonId":"sam@test.com"
      },
      {  
         "externalSalesPersonId":"david@test.com"
      },
      {  
         "externalSalesPersonId":"raj@test.com"
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
         "id":56343,
         "status": "deleted"
      },
      {
         "seq":1,
         "id":53453,
         "status": "deleted"
      },
      {
         "seq":2,
         "status": "skipped"
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

- 販売担当者エンドポイントのタイムアウトは、以下に記載されていない限り 30 秒です
   - 営業担当者の同期：60s
   - 営業担当者の削除：60s
