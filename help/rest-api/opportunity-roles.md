---
title: 商談ロール
feature: REST API
description: 説明、複合重複排除フィールドを含むクエリ、更新削除の作成、タイムアウト、CRM同期を含まないREST APIを介したMarketoの商談ロールの管理。
exl-id: 2ba84f4d-82d0-4368-94e8-1fc6d17b69ed
TQID: https://experienceleague.adobe.com/aE27mBhsrn-0SO41M-pV5NFjoMq--1Lp-L2TQGL7-8Y
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 254
ht-degree: 9%

---

# 商談ロール

[商談役割エンドポイントの参照](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities/operation/getOpportunityRolesUsingGET)

中間の`opportunityRole` オブジェクトは商談にリンクします。

商談役割APIは、ネイティブ CRM同期が有効になっていないサブスクリプションでのみ使用できます。

## 説明

商談と同様に、APIは商談ロールに対して記述呼び出しとCRUD操作を提供します。

```http
GET /rest/v1/opportunities/roles/describe.json
```

```json
{
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[
      {
         "name":"opportunityRole",
         "displayName":"Opportunity Role",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"marketoGUID",
         "dedupeFields":[
            "externalOpportunityId",
            "leadId",
            "role"
         ],
         "searchableFields":[
            [
               "externalOpportunityId",
               "leadId",
               "role"
            ],
            [
               "marketoGUID"
            ],
            [
               "leadId"
            ],
            [
               "externalOpportunityId"
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
               "name":"externalOpportunityId",
               "displayName":"External Opportunity Id",
               "dataType":"string",
               "length":50,
               "updateable":false
            },
            {
               "name":"leadId",
               "displayName":"Lead Id",
               "dataType":"integer",
               "updateable":false
            },
            {
               "name":"role",
               "displayName":"Role",
               "dataType":"string",
               "length":50,
               "updateable":false
            },
            {
               "name":"isPrimary",
               "displayName":"Is Primary",
               "dataType":"boolean",
               "updateable":true
            },
            {
               "name":"externalCreatedDate",
               "displayName":"External Created Date",
               "dataType":"datetime",
               "updateable":true
            }
         ]
      }
   ]
}
```

## クエリ

`dedupeFields`と`searchableFields`の値が商談と異なります。 `dedupeFields`は、`externalOpportunityId`、`leadId`および`role`を必要とする複合キーを提供します。 レコードの作成を成功させるには、ID フィールドで参照される商談とリードが宛先インスタンスに存在する必要があります。

`searchableFields`値`marketoGUID`、`leadId`および`externalOpportunityId`は、商談と同じパターンを使用する個々のクエリに対して有効です。 複合キーを使用してクエリすることもできます。 このクエリには、`_method=GET` クエリパラメーターを使用してPOSTを通じて送信されたJSON オブジェクトが必要です。

```http
POST /rest/v1/opportunities/roles.json?_method=GET
```

```json
{
   "filterType": "dedupeFields",
   "fields": [
      "marketoGuid",
      "externalOpportunityId",
      "leadId",
      "role"
   ],
   "input": [
      {
        "externalOpportunityId": "Opportunity1",
        "leadId": 1,
        "role": "Captain"
      },
      {
        "externalOpportunityId": "Opportunity2",
        "leadId": 1872,
        "role": "Commander"
      },
      {
        "externalOpportunityId": "Opportunity3",
        "leadId": 273891,
        "role": "Lieutenant Commander"
      }
   ]
}
```

このリクエストは、標準のGET クエリと同じ応答タイプを生成しますが、異なるリクエストインターフェイスを使用します。

## 作成と更新

商談と同じインターフェイスを使用して、商談の役割を作成および更新できます。

```http
POST /rest/v1/opportunities/roles.json
```

```json
{
   "action": "createOrUpdate",
   "dedupeBy": "dedupeFields",
   "input": [
      {
         "externalOpportunityId": "19UYA31581L000000",
         "leadId": 456783,
         "role": "Technical Buyer",
         "isPrimary": false
      },
      {
         "externalOpportunityId": "19UYA31581L000000",
         "leadId": 456784,
         "role": "Technical Buyer",
         "isPrimary": false
      }
   ]
}
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result":[
      {
         "seq": 0,
         "status": "updated",
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq": 1,
         "status": "created",
         "marketoGUID": "cff23271-f996-47d7-984f-f2676861b5fb"
      }
   ]
}
```

## 削除

重複排除フィールドまたはID フィールドで商談ロールを削除します。 deleteBy パラメーターをdedupeFieldsまたはidFieldのいずれかに設定します。 デフォルトはdedupeFieldsです。

リクエスト本体には、削除する商談ロールの入力配列が含まれます。 各呼び出しでは、最大300個の商談ロールを使用できます。

```http
POST /rest/v1/opportunities/roles/delete.json
```

```json
{
   "deleteBy": "dedupeFields",
   "input": [
      {
        "externalOpportunityId": "19UYA31581L000000",
        "leadId": 456783,
        "role": "Technical Buyer"
      }
   ]
}
```

```json
{
    "requestId": "10f7c#173264db42d",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
            "status": "deleted"
        }
    ]
    "success": true
}
```

## タイムアウト

- 特に明記されていない限り、商談ロールエンドポイントのタイムアウトは30秒です。
- 同期商談ロールのタイムアウトは60秒です。
- 商談ロールの削除のタイムアウトは60秒です。
