---
title: 重点顧客
feature: REST API
description: API を通じて重点顧客を操作します。
exl-id: 2aa1d2a0-9e54-4a9a-abb1-0d0479ed3558
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 100%

---

# 重点顧客

[重点顧客エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Accounts)

Marketo は、Marketo ABM で使用する重点顧客に対して CRUD 操作を実行する一連の API を備えています。これらの API は、説明、作成／更新、削除、クエリのオプションを提供するリードデータベース API の標準インターフェイスパターンに従います。

現在、Marketo の API 経由で使用できる ABM 関連機能は、重点顧客の CRUD 操作のみです。リードは、任意の API 経由で重点顧客にリンクできません。

## 説明

重点顧客を説明すると、クエリの実行時に有効で検索可能なフィールドのリストや、API の使用状況に対して使用できるすべてのフィールドのリストなど、Marketo の API 経由で重点顧客の使用状況に関連するメタデータが返されます。重点顧客の `idField` は常に `marketoGUID` で、作成に使用できる唯一の `dedupeField` およびキーは、オブジェクトの `name` フィールドです。

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

重点顧客のクエリは、filterType と、最大 300 個のコンマ区切りの filterValues のセットの使用状況に基づいています。`filterType` は、重点顧客の説明結果の `searchableFields` メンバーで返される任意の単一フィールドである場合がありますが、filterValues は、フィールドのデータタイプの有効な入力である場合があります。特定のフィールドセットを返すには、fields パラメーターを渡す必要があります。値は、応答で返されるフィールドのコンマ区切りリストです。他のクエリオプションと同様に、単一のクエリページのレコードの最大数は 300 で、セット内の追加のレコードは、呼び出しによって返される nextPageToken を使用してリクエストする必要があります。

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

重点顧客の作成と更新は、標準のリードデータベースパターンに従います。レコードは、POST リクエストの JSON 本文の入力メンバーに渡す必要があります。`input` は唯一の必須メンバーで、`action` と `dedupeBy` はオプションのメンバーです。入力には、最大 300 個のレコードを含めることができます。アクションは、createOnly、updateOnly、createOrUpdate のいずれかです。指定しない場合、アクションはデフォルトで createOrUpdate です。dedupeBy は、アクションが updateOnly の場合にのみ指定でき、それぞれ name フィールドと marketoGUID フィールドに対応する dedupeFields または idField のいずれか 1 つだけを受け入れます。

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

重点顧客オブジェクトには、一連のフィールドが含まれています。各フィールド定義は、フィールドを説明する属性のセットで構成されます。属性の例としては、表示名、API 名、dataType があります。これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、会社オブジェクトのフィールドに対してクエリを実行できます。これらの API では、所有する API ユーザに、「読み取り／書き込みスキーマ標準フィールド」権限または「読み取り／書き込みスキーマカスタムフィールド」権限のいずれかまたは両方を含むロールを用意する必要があります。

### クエリフィールド

重点顧客フィールドのクエリの実行は簡単です。API 名で単一の重点顧客フィールドに対してクエリを実行することも、すべての会社フィールドのセットに対してクエリを実行することもできます。

#### 名前別

[名前による重点顧客フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET)エンドポイントでは、重点顧客オブジェクトの単一フィールドのメタデータを取得します。必須の fieldApiName パスパラメーターは、フィールドの API 名を指定します。応答は「重点顧客を説明」エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す isCustom 属性などの追加のメタデータが含まれます。

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

[重点顧客フィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET)エンドポイントでは、重点顧客オブジェクトのすべてのフィールドのメタデータを取得します。デフォルトでは、最大 300 個のレコードが返されます。batchSize クエリパラメーターを使用して、この数を減らすことができます。moreResult 属性が true の場合、さらに多くの結果が使用可能です。moreResult 属性が false を返すまで、つまり使用可能な結果が存在しなくなるまで、このエンドポイントを引き続き呼び出します。この API から返される nextPageToken は、この呼び出しの次の反復で常に再利用する必要があります。

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

削除は JSON POST リクエストを通じて実行され、必須の input メンバーとオプションの deleteBy メンバーがあります。deleteBy は、それぞれ name または marketoGUID に対応する「dedupeFields」または「idField」のいずれかで、設定されていない場合はデフォルトで dedupeFields になります。input メンバーは、deleteBy の設定に応じて、name または marketoGUID のいずれか 1 つのメンバーを含む最大 300 個のレコードの配列を受け入れます。

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

- 「重点顧客」エンドポイントは、以下に記載されていない限り、タイムアウトが 30 秒になります
   - 重点顧客を同期：120 秒
   - 重点顧客を削除：60 秒
