---
title: 商談ロール
feature: REST API
description: REST API を使用してMarketoのオポチュニティの役割を管理します。これには、説明、複合重複排除フィールドを使用したクエリ、作成更新削除、タイムアウト、CRM 同期なしが含まれます。
exl-id: 2ba84f4d-82d0-4368-94e8-1fc6d17b69ed
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 90%

---

# 商談ロール

[商談ロールエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunityRolesUsingGET)

リードは、中間の `opportunityRole` オブジェクトを通じて商談にリンクされます。

Opportunity Role API は、ネイティブ CRM 同期が有効になっていないサブスクリプションに対してのみ公開されます。

## 説明

商談と同様に、商談ロールに対して説明呼び出しと CRUD 操作が公開されます。

```
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

`dedupeFields` と `searchableFields` は、両方とも商談とは少し異なります。`dedupeFields` は、実際には複合キーを提供しますが、`externalOpportunityId`、`leadId`、`role` の 3 つすべてが必要です。レコードの作成を成功させるには、ID フィールド別の商談リンクとリードリンクの両方が宛先インスタンスに存在する必要があります。`searchableFields` の場合、`marketoGUID`、`leadId`、`externalOpportunityId` は、すべて独自のクエリに有効で、商談と同じパターンを使用しますが、複合キーを使用してクエリを実行する追加オプションがあり、追加のクエリパラメーター `_method=GET` を使用して、JSON オブジェクトを POST 経由で送信する必要があります。

```
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

これにより、標準の GET クエリと同じタイプの応答が生成されますが、リクエストを行うインターフェイスが異なるだけです。

## 作成と更新

商談ロールには、レコードの作成および更新用の、商談と同じインターフェイスが用意されています。

```
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

商談ロールは、重複排除フィールドまたは ID フィールドで削除できます。dedupeFields または idField のいずれかの値を持つ deleteBy パラメーターを使用して指定します。指定しない場合、デフォルトは dedupeFields です。リクエスト本体には、削除する商談ロールの入力配列が含まれます。1 回の呼び出しにつき最大 300 個の商談ロールが許可されます。

```
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

- 「商談ロール」エンドポイントは、以下に記載されていない限り、タイムアウトが 30 秒になります。
   - 商談ロールの同期：60s
   - 商談ロールを削除：60 秒
