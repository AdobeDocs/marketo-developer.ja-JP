---
title: 重点顧客
feature: REST API
description: 記述分析、クエリ分析、更新例の作成、検索可能なフィールド、重複排除ルール、リードリンクのないABM名前付きアカウントを活用したCRUDに関するMarketo REST ガイド。
exl-id: 2aa1d2a0-9e54-4a9a-abb1-0d0479ed3558
TQID: https://experienceleague.adobe.com/iY3UYVelm3aKuuDBCTxaVCbkXfwnJzDjV3Kvn9rcNbA
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 590
ht-degree: 5%

---

# 重点顧客

[名前付きアカウントエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi#tag/Named-Accounts)

Marketoには、Marketo ABMで使用する名前付きアカウントに対してCRUD操作を実行するためのAPIが用意されています。 これらのAPIは、標準のリードデータベースのインターフェイスパターンに従い、「説明」、「作成/更新」、「削除」、「クエリ」オプションを提供します。

現在、Marketo APIでは、名前付きアカウントに対するCRUD操作のみがサポートされています。 APIを介してリードを名前付きアカウントにリンクすることはできません。

## 説明

Describe Named Accountsは、Marketo APIを介して名前付きアカウントを使用するためのメタデータを返します。 応答には、有効な検索可能なフィールドと、APIで使用可能なすべてのフィールドが含まれます。

名前付きアカウントの`idField`は常に`marketoGUID`です。 オブジェクトの`name` フィールドは、使用可能な唯一の`dedupeField`および作成キーです。

```http
GET /rest/v1/namedaccounts/describe.json
```

```json
{
   "requestId":"d65e#156c27ac57d",
   "result":[
      {
         "name":"Named Account",
         "description":"Marketo standard account attribute map",
         "createdAt":"2016-08-18T20:16:41Z",
         "updatedAt":"2016-08-18T20:16:41Z",
         "idField":"marketoGUID",
         "dedupeFields":[
            "name"
         ],
         "searchableFields":[
            [
               "marketoGUID",
            ],
            [
               "annualRevenue"
            ],
            [
               "city"
            ],
            [
               "country"
            ],
            [
               "domainName"
            ],
            [
               "industry"
            ],
            [
               "logoUrl"
            ],
            [
               "membershipCount"
            ],
            [
               "name"
            ],
            [
               "numberOfEmployees"
            ],
            [
               "opptyAmount"
            ],
            [
               "opptyCount"
            ],
            [
               "score1"
            ],
            [
               "score2"
            ],
            [
               "score3"
            ],
            [
               "score4"
            ],
            [
               "score5"
            ],
            [
               "sicCode"
            ],
            [
               "state"
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
               "name":"annualRevenue",
               "displayName":"annualRevenue",
               "dataType":"currency",
               "updateable":true
            },
            {
               "name":"city",
               "displayName":"city",
               "dataType":"string",
               "length":255,
               "updateable":true
            },
            {
               "name":"country",
               "displayName":"country",
               "dataType":"string",
               "length":255,
               "updateable":true
            }
         ]
      }
   ],
   "success":true
}
```

### クエリ

filterTypeと最大300個のコンマ区切りのfilterValuesを使用して、名前付きアカウントをクエリします。 filterTypeは、Describe応答の`searchableFields` メンバーで返される任意の単一フィールドにすることができます。 各filterValues エントリは、フィールドのデータタイプに対して有効な値である必要があります。

特定のフィールドを返すには、fields パラメーターにフィールドのコンマ区切りリストを渡します。 クエリページには、最大300件のレコードが含まれます。 追加のレコードを取得するには、呼び出しによって返されるnextPageTokenを使用します。

```http
GET /rest/v1/namedaccounts.json?filterType=name&filterValues=Google,Yahoo
```

```json
{
    "requestId": "6dac#157d4ddc9d7",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "16efafdd-0148-4ea7-8782-f451d7c6345d",
            "createdAt": "2016-10-17T22:49:04Z",
            "name": "Google",
            "updatedAt": "2016-10-17T22:49:04Z"
        },
        {
            "seq": 1,
            "marketoGUID": "44d62353-7f9d-4d43-b9cc-7ef0f7a09137",
            "createdAt": "2016-10-17T22:49:04Z",
            "name": "Yahoo",
            "updatedAt": "2016-10-17T22:49:04Z"
        }
    ],
    "success": true
}
```

### 作成と更新

標準のリードデータベースパターンを使用して、名前付きアカウントを作成および更新します。 POST リクエストのJSON本文の入力メンバーにレコードを渡します。 最大300件のレコードを含めることができます。

リクエストメンバーは次のとおりです。

- `input`：必要なメンバーは1人だけです。
- `action`: createOnly、updateOnly、またはcreateOrUpdateを受け入れるオプションのメンバー。 デフォルトはcreateOrUpdateです。
- `dedupeBy`: アクションがupdateOnlyの場合にのみ使用できるオプションのメンバー。 名前フィールドとmarketoGUID フィールドにそれぞれ対応するdedupeFieldsまたはidFieldを使用できます。

```http
POST /rest/v1/namedaccounts.json
```

```text
Content-Type: application/json
```

```json
{
   "action":"updateOnly",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "name":"Google",
         "domainName":"www.google.com"
      },
      {
         "name":"Yahoo",
         "domainName":"www.yahoo.com"
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
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fc"
      }
   ]
}
```

### フィールド

名前付きアカウントオブジェクトには、表示名、API名、dataTypeなどの属性で定義されたフィールドが含まれます。 これらの属性をメタデータと呼びます。

次のエンドポイントは、会社オブジェクトのフィールドをクエリします。 API ユーザーには、読み取り/書き込みスキーマ標準フィールド権限、読み取り/書き込みスキーマカスタムフィールド権限、またはその両方を持つ役割が必要です。

### クエリフィールド

API名で1つの名前付きアカウントフィールドをクエリするか、すべての会社フィールドを取得します。

#### 名前別

[名前付きアカウントフィールドを名前付きアカウントオブジェクトで取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET) エンドポイントは、名前付きアカウントオブジェクトの1つのフィールドのメタデータを取得します。 必須のfieldApiName パスパラメーターは、フィールドのAPI名を指定します。

応答は、「名前付きアカウントを説明」応答に似ていますが、追加のメタデータが含まれています。 例えば、isCustom属性は、フィールドがカスタムかどうかを示します。

```http
GET /rest/v1/namedaccounts/schema/fields/annualRevenue.json
```

```json
{
    "requestId": "371c#17e979c5d1f",
    "result": [
        {
            "displayName": "Annual Revenue",
            "name": "annualRevenue",
            "description": null,
            "dataType": "currency",
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

[重点顧客フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET)エンドポイントでは、重点顧客オブジェクトのすべてのフィールドのメタデータを取得します。 デフォルトでは、最大300件のレコードが返されます。 この数を減らすには、batchSize クエリパラメーターを使用します。

moreResult属性がtrueの場合、より多くの結果を使用できます。 返されたnextPageTokenでエンドポイントの呼び出しを続行し、moreResultがfalseになるまで呼び出します。

```http
GET /rest/v1/namedaccounts/schema/fields.json?batchSize=5
```

```json
{
    "requestId": "f287#17e995bd0c5",
    "result": [
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
            "displayName": "Domain Name",
            "name": "domainName",
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
        },
        {
            "displayName": "SIC Code",
            "name": "sicCode",
            "description": null,
            "dataType": "string",
            "length": 40,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "City",
            "name": "city",
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
    "nextPageToken": "N42LHXWEULHZ3N2I77DKOJUVOY======",
    "moreResult": true
}
```

### 削除

JSON本文を使用してPOST リクエストを送信し、名前付きアカウントを削除します。 リクエストには、必須の入力メンバーとオプションのdeleteBy メンバーが含まれます。

deleteBy メンバーは、それぞれnameおよびmarketoGUIDに対応する「dedupeFields」または「idField」を受け入れます。 未設定の場合、デフォルトでは重複排除フィールドになります。 入力メンバーは、最大300件のレコードを受け入れます。 各レコードには、deleteBy設定に応じて、名前またはmarketoGUIDが含まれます。

```http
POST /rest/v1/namedaccounts/delete.json
```

```text
Content-Type: application/json
```

```json
{
   "deleteBy":"dedupeFields",
   "input":[
      {
         "name":"Google"
      },
      {
         "name":"Yahoo"
      },
      {
         "name":"Marketo"
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
         "id":"dff23271-f996-47d7-984f-f2676861b5fc",
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

- 名前付きアカウントエンドポイントのタイムアウトは、特に明記されていない限り30秒です。
- 名前付きアカウントの同期のタイムアウトは120秒です。
- 名前付きアカウントの削除のタイムアウトは60秒です。
