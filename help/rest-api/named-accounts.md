---
title: 重点顧客
feature: REST API
description: API を使用して名前付きアカウントを操作します。
exl-id: 2aa1d2a0-9e54-4a9a-abb1-0d0479ed3558
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---

# 重点顧客

[ 重点顧客エンドポイントリファレンス ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Accounts)

Marketoは、Marketo ABM で使用する名前付きアカウントに対して CRUD 操作を実行するための一連の API を提供します。 これらの API は、リードデータベース API の標準インターフェイスパターンに従い、説明、作成/更新、削除、クエリの各オプションを提供します。

現在、Marketoの API で使用できる ABM 関連の機能は、指定されたアカウントの CRUD 操作のみです。リードを指定されたアカウントに API を使用してリンクすることはできません。

## 説明

指定されたアカウントを記述すると、Marketo API による指定されたアカウントの使用に関するメタデータが返されます。これには、クエリ時に検索できる有効なフィールドのリスト、API で使用可能なすべてのフィールドのリストが含まれます。 名前付きアカウントの `idField` は常に `marketoGUID` であり、作成に使用できる `dedupeField` とキーはオブジェクトの `name` フィールドのみです。

```
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

名前付きアカウントのクエリは、filterType の使用方法と、最大 300 個のコンマ区切り filterValues のセットに基づいています。 `filterType` は、名前付き勘定科目の記述結果の `searchableFields` メンバーで返される任意の単一フィールドです。一方、filterValues は、フィールドのデータ型に対する任意の有効な入力です。 から特定のフィールドのセットを返すには、fields パラメーターを渡す必要があります。この値は、応答で返されるフィールドのコンマ区切りリストです。 他のクエリオプションと同様に、1 つのクエリページの最大レコード数は 300 で、セット内の追加のレコードをリクエストするには、呼び出しによって返される nextPageToken を使用する必要があります。

```
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

指定顧客の作成と更新は、標準のリードデータベースパターンに従います。 レコードは、POSTリクエストの JSON 本文の入力メンバーで渡す必要があります。 必須のメンバーは `input` のみです。`action` と `dedupeBy` は省略可能なメンバーです。 入力には、最大 300 件のレコードを含めることができます。 Action は、createOnly、updateOnly、createOrUpdate のいずれかです。 指定しない場合、アクションはデフォルトで createOrUpdate になります。 dedupeBy は、action が updateOnly の場合にのみ指定でき、それぞれ name フィールドおよび marketoGUID フィールドに対応する dedupeFields または idField のいずれか 1 つのみを受け入れます。

```
POST /rest/v1/namedaccounts.json
```

```
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

名前付きアカウントオブジェクトには、一連のフィールドが含まれています。 各フィールド定義は、フィールドを説明する一連の属性で構成されます。 属性の例としては、表示名、API 名、データタイプがあります。 これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、company オブジェクトのフィールドに対してクエリを実行できます。 これらの API では、所有している API ユーザーが、読み取り/書き込みスキーマ標準フィールドまたは読み取り/書き込みスキーマカスタムフィールドの権限の一方または両方の役割を持っている必要があります。

### クエリフィールド

名前付きアカウントフィールドのクエリは簡単です。 API 名で 1 つの名前付きアカウントフィールドに対してクエリを実行したり、すべての会社フィールドのセットに対してクエリを実行したりできます。

#### 名前別

[ 名前による名前付きアカウント フィールドの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET) エンドポイントは、名前付きアカウント オブジェクトの 1 つのフィールドのメタデータを取得します。 必須の fieldApiName パスパラメーターは、フィールドの API 名を指定します。 この応答は、Describe Named Account エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す isCustom 属性などの追加メタデータが含まれています。

```
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

[ 名前付きアカウント フィールドの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET) エンドポイントは、名前付きアカウント オブジェクトのすべてのフィールドのメタデータを取得します。 デフォルトでは、最大 300 件のレコードが返されます。 batchSize クエリパラメーターを使用して、この数を減らすことができます。 moreResult 属性が true の場合は、使用可能な結果が多いことを意味します。 moreResult 属性が false を返す（使用できる結果がないことを意味する）まで、このエンドポイントの呼び出しを続行します。 この API から返された nextPageToken は、常にこの呼び出しの次のイテレーションで再利用する必要があります。

```
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

削除は JSON POSTリクエストを介して実行され、必須の入力メンバーとオプションの deleteBy メンバーが含まれています。 deleteBy は、それぞれ name または marketoGUID に対応する「dedupeFields」または「idField」のいずれかであり、設定されていない場合はデフォルトで dedupeFields に設定されます。 入力メンバーは、最大 300 個のレコードの配列を受け入れます。この配列には、deleteBy の設定に応じて、name または marketoGUID のいずれかのメンバーがそれぞれ 1 つ含まれます。

```
POST /rest/v1/namedaccounts/delete.json
```

```
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

- 以下に示さない限り、名前付きアカウント エンドポイントのタイムアウトは 30 秒です
   - 指定したアカウントを同期：120s 
   - 重点顧客の削除：60s
