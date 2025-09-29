---
title: セールス担当者
feature: REST API
description: externalSalesPersonId を使用してリードに関連付け、クエリ、アップサート、削除を実行する、SFDCまたは Dynamics 同期を使用した営業担当者レコードに関するMarketo REST API ガイド。
exl-id: f8ed5aa5-63c1-4c5b-8683-bf47eed1ea18
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 92%

---

# セールス担当者

[セールス担当者エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Sales-Persons)

Sales Person API は、[SFDC 同期](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync)または [Microsoft Dynamics 同期](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync)が有効になっているサブスクリプションに対する読み取り専用アクセスです。セールス担当者は、リードレコードのセールス所有者であるユーザレコードのタイプです。各リードレコードの externalSalesPersonId フィールドによってリードレコードに関連付けられます。リードが、入力した externalSalesPersonId フィールドでセールス担当者に関連付けられると、Marketo のそのリードレコードに対応するリード所有者ルックアップフィールドが入力され、対応するフィルターとトークンの使用が可能になります。

セールス担当者は、[リードを同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST)エンドポイントを使用して externalSalesPersonId 属性を渡すことによってリードレコードに関連付けられます。

セールス担当者は、[商談を同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/syncOpportunitiesUsingPOST)エンドポイントを使用して externalSalesPersonId 属性を渡すことによって商談レコードに関連付けられます。

セールス担当者は、[会社を同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST)エンドポイントを使用して externalSalesPersonId 属性を渡すことによって会社レコードに関連付けられます。

セールス担当者レコードは、API 経由でのみ編集可能です。

## 説明

セールス担当者レコードの説明は、リードデータベースオブジェクトの標準パターンに従います。

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

デフォルトでは、セールス担当者の `idField` は「id」で、`dedupeFields` は「externalSalesPersonId」です。

## クエリ

シンプルなキーの標準クエリパターンを使用するセールス担当者。この例では、ユーザのメールは externalSalesPersonId として使用されています。デフォルトでは、クエリは、返されたレコードに対して入力されているすべてのフィールドを返します。

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

セールス担当者は、「使用中」の場合は削除できません。この場合、セールス担当者はスキップされます。例:

- セールス担当者がアクティブなリードに関連付けられている場合
- セールス担当者が削除された会社に関連付けられている場合

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

- 「セールス担当者」エンドポイントは、以下では、30 秒でタイムアウトします。
   - セールス担当者を同期：60 秒
   - セールス担当者を削除：60 秒
