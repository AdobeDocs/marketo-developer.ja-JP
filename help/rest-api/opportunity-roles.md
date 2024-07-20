---
title: オポチュニティの役割
feature: REST API
description: Marketoでのオポチュニティの役割の処理。
exl-id: 2ba84f4d-82d0-4368-94e8-1fc6d17b69ed
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 2%

---

# オポチュニティの役割

[ 商談の役割のエンドポイントリファレンス ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunityRolesUsingGET)

リードは、中間 `opportunityRole` オブジェクトを介して商談にリンクされています。

商談役割 API は、ネイティブの CRM 同期が有効になっていない購読に対してのみ公開されます。

## 説明

オポチュニティと同様に、説明の電話および CRUD 操作がオポチュニティの役割に公開されます。

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

`dedupeFields` と `searchableFields` はどちらも商談とは少し異なります。 `dedupeFields` は実際に、`externalOpportunityId`、`leadId`、`role` の 3 つすべてが必要な複合キーを提供します。 レコードの作成を成功させるには、ID フィールド別のオポチュニティとリードリンクの両方が宛先インスタンスに存在する必要があります。 `searchableFields`、`marketoGUID`、`leadId`、`externalOpportunityId` はすべて、独自のクエリに有効で、Opportunities と同じパターンを使用しますが、複合キーを使用してクエリを実行するには、追加のクエリパラメーター `_method=GET` を使用したPOST経由で JSON オブジェクトを送信する必要があります。

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

これにより、標準のGETクエリと同じタイプの応答が生成されます。リクエストを行うための異なるインターフェイスが用意されているだけです。

## 作成と更新

商談役割には、商談としてレコードを作成および更新するための同じインターフェイスが用意されています。

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

重複の除外フィールドまたは ID フィールドを使用して、オポチュニティの役割を削除できます。 値が dedupeFields または idField の deleteBy パラメーターを使用して指定します。 指定しない場合、デフォルトは dedupeFields です。 リクエスト本文には、削除するオポチュニティの役割の入力配列が含まれます。 1 回の呼び出しで許可されるオポチュニティの役割は、最大 300 個です。

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

- 以下に示さない限り、商談の役割エンドポイントのタイムアウトは 30 秒です
   - 商談ロールの同期：60s 
   - 商談ロールの削除：60s
