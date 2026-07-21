---
title: カスタムオブジェクト
feature: REST API, Custom Objects
description: エンドポイント、メタデータ、リレーションシップ、フィールド、クエリなど、REST APIを使用してMarketo カスタムオブジェクトを作成および管理する方法について説明します。
exl-id: 88e8829b-f8f1-46d7-a753-5aa6e20e2c40
TQID: https://experienceleague.adobe.com/NWm9CjFVqQdVDJRrnE4nA299-Lg53-JR7xvY-82dUqY
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
subfeature_v2:
  - id: ea4e3ff5-e7b9-4b4c-a5a0-dc27cc3f4275
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 2938
ht-degree: 13%

---

# カスタムオブジェクト

[**カスタムオブジェクトエンドポイント参照**](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects)

Marketo カスタムオブジェクトは、リードや会社などのMarketo標準オブジェクトや、その他のMarketo カスタムオブジェクトに関連付けることができます。 [Marketo UI](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects)で、または本ドキュメントに記載されているカスタムオブジェクトメタデータ APIを使用して、Marketo カスタムオブジェクトを作成します。

カスタムオブジェクトメタデータ APIにアクセスするには、適切なMarketo サブスクリプションタイプが必要です。 詳細については、CSMにお問い合わせください。

## リスト

リードデータベースオブジェクトに対する標準の説明、クエリ、更新、削除の呼び出しに加えて、カスタムオブジェクトは[&#x200B; リスト呼び出しを提供します](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectsUsingGET)。 エンドポイントは、宛先インスタンスで使用可能なカスタムオブジェクトと、各オブジェクトに関するメタデータを返します。

```http
GET /rest/v1/customobjects.json
```

```json
{
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[
      {
         "name":"Car",
         "displayName":"Car",
         "description":"Car owner",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"marketoGUID",
         "dedupeFields":["vin"],
         "searchableFields":[
            ["vin"],
            ["marketoGUID"],
            ["siebelId"]
         ],
         "relationships":[
            {
               "field":"siebelId",
               "type":"parent",
               "relatedTo":{
                  "name":"Lead",
                  "field":"siebelId"
               }
            }
         ]
      }
   ]
}
```

応答には、各オブジェクトの関係が一覧表示されます。 各関係には次のものが含まれます。

- `field`: リンク値を保持するオブジェクトのフィールド。
- `type`：関連オブジェクトが親オブジェクトか子オブジェクトかのどちらかです。
- `relatedTo`：関連するオブジェクトの名前とそのリンクフィールド。

## 説明

カスタムオブジェクトの[Describe呼び出し](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/describeUsingGET_1)は、商談と企業と同じパターンに従い、次の2つの追加が含まれています。

- `apiName` path パラメーターは、記述するカスタムオブジェクトタイプのAPI名を指定します。
- 応答には、カスタムオブジェクトタイプで使用可能な関係をリストする`relationships`配列が含まれています。

```http
GET /rest/v1/customobjects/{apiName}/describe.json
```

```json
{
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[
      {
         "name":"Car",
         "displayName":"Car",
         "description":"Car owner",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"marketoGUID",
         "dedupeFields":["vin"],
         "searchableFields":[
            ["vin"],
            ["marketoGUID"],
            ["siebelId"]
         ],
         "relationships":[
            {
               "field":"siebelId",
               "type":"parent",
               "object":{
                  "name":"Lead",
                  "field":"siebelId"
               }
            }
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
               "name":"vin",
               "displayName":"VIN",
               "description":"Vehicle Identification Number",
               "dataType":"string",
               "length":36,
               "updateable":false
            },
            {
               "name":"siebelId",
               "displayName":"External Id",
               "description":"External Id",
               "dataType":"string",
               "length":36,
               "updateable":true
            },
            {
               "name":"make",
               "displayName":"Make",
               "dataType":"string",
               "length":36,
               "updateable":true
            },
            {
               "name":"model",
               "displayName":"Model",
               "description":"Vehicle Model",
               "dataType":"string",
               "length":255,
               "updateable":true
            },
            {
               "name":"year",
               "displayName":"Year",
               "dataType":"integer",
               "updateable":true
            },
            {
               "name":"color",
               "displayName":"Color",
               "description":"Vehicle color",
               "dataType":"String",
               "length": 255,
               "updateable":true
            }
         ]
      }
   ]
}
```

## クエリ

[&#x200B; カスタムオブジェクトのクエリ &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectsUsingGET)は、他のリードデータベースオブジェクトのクエリとは若干異なります。 説明と同様に、リクエストは`apiName` パスパラメーターを使用します。

通常のfilterTypeの場合は、必要な`filterType`および`filterValues` パラメーターを指定してGET リクエストを送信します。 オプションの`**fields**`、`batchSize`および`nextPageToken` パラメーターを含めることもできます。

フィールドのリストをリクエストする場合、返されないリクエストされたフィールドの暗黙的な値はnullになります。

```http
GET /rest/v1/customobjects/{apiName}.json?filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa,dff23271-f996-47d7-984f-f2676861b5fb
```

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fa",
         "vin":"19UYA31581L000000",
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      },
      {
         "seq":1,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "vin":"29UYA31581L000000",
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      },
   ]
}
```

複合キーを使用してクエリを実行すると、APIは商談ロール APIと同様に動作し、JSON本文を使用してPOST リクエストを受け入れます。 本文には、`filterValues`を除くGET クエリと同じメンバーを含めることができます。

フィルター値の代わりに、`input`個のオブジェクト配列を指定します。 各オブジェクトには、オブジェクトタイプの`dedupeFields`の各フィールドのメンバーが含まれます。

```http
POST /rest/v1/customobjects/{apiName}.json?_method=GET
```

```json
{
   "filterType":"dedupeFields",
   "fields":[
      "marketoGuid",
      "Bedrooms",
      "yearBuilt"
   ],
   "input":[
      {
         "mlsNum":"1962352",
         "houseOwnerId":"42645756"
      },
      {
         "mlsNum":"2962352",
         "houseOwnerId":"52645756"
      },
      {
         "mlsNum":"3962352",
         "houseOwnerId":"62645756"
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
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fa",
         "Bedrooms":3,
         "yearBuilt":1948,
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      },
      {
         "seq":1,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "Bedrooms":4,
         "yearBuilt":1956,
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      },
      {
         "seq":2,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fc",
         "Bedrooms":3,
         "yearBuilt":2001,
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      }
   ]
}
```

## 作成と更新

カスタムオブジェクトを作成または更新するには、[&#x200B; カスタムオブジェクトを同期](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) エンドポイントを使用します。 操作を`action` パラメーターで指定します。 各呼び出しは、最大300件のレコードを作成または更新できます。

`input`配列の値は、[&#x200B; カスタムオブジェクトの記述](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/endpoint-reference#!/Custom_Objects/describeUsingGET_1) エンドポイントによって返される情報に基づきます。 例のcar オブジェクトでは、重複排除フィールドは`vin`のみです。 dedupeFields モードを使用してレコードを作成または更新する場合は、入力配列内の各オブジェクトに少なくとも`vin` フィールドを含めます。

```http
POST /rest/v1/customobjects/{apiName}.json
```

```json
{
   "action":"updateOnly",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "vin":"19UYA31581L000000",
         "siebelId":"f2676861b5fb",
         "make":"BMW",
         "model":"3-Series 330i",
         "year":2003
      },
      {
         "vin":"29UYA31581L000000",
         "siebelId":"f2676861b5fc",
         "make":"BMW",
         "model":"3-Series 330i",
         "year":2003
      },
      {
         "vin":"39UYA31581L000000",
         "siebelId":"f2676861b5fd",
         "make":"BMW",
         "model":"3-Series 330i",
         "year":2003
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
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq":1,
         "status": "created",
         "marketoGUID":"cff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq":2,
         "status": "skipped"
         "reasons":[
            {
               "code":"1004",
               "message":"Lead not found"
            }
         ]
      }
   ]
}
```

`idField` モードでレコードを更新すると、`idField`は常に`marketoGUID`になります。 すべてのレコードに`marketoGUID` フィールドを含めます。

このフィールドはシステムで管理されているため、`idField`はupdateOnly アクションタイプに対してのみ有効です。 結果の配列には、各レコードの&#x200B;**status**&#x200B;が含まれます。 また、正常な操作の`marketoGUID`または失敗した操作の`reasons`配列も含まれます。

## 削除

[&#x200B; レコードを削除](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST)するには、`idField`または`dedupeFields`のいずれかの`deleteBy` モードを選択します。 `input`配列の各レコードに対応するフィールドを含めます。 各呼び出しでは、最大300件のレコードを使用できます。

```http
POST /rest/v1/customobjects/{apiName}/delete.json
```

```json
{
   "deleteBy":"dedupeFields",
   "input":[
      {
         "vin":"19UYA31581L000000"
      },
      {
         "vin":"29UYA31581L000000"
      },
      {
         "vin":"39UYA31581L000000"
      }
   ]
}

{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "status": "deleted"
      },
      {
         "seq":1,
         "marketoGUID":"da42707c-4dc4-4fc1-9fef-f30a3017240a",
         "status": "deleted"
      },
      {
         "seq":2,
         "status": "skipped"
         "reasons":[
            {
               "code":"1013",
               "message":"Object not found"
            }
         ]
      }
   ]
}
```

更新と同様に、結果には各レコードのステータスが含まれます。 また、削除が成功した場合は`marketoGUID`、削除が失敗した場合は`reasons`配列が含まれます。

## カスタムオブジェクトタイプ

カスタムオブジェクトメタデータ APIを使用すると、カスタムオブジェクトスキーマをリモートで管理できます。 カスタムオブジェクトタイプを作成したり、既存のオブジェクトタイプを変更したりするのに使用します。 タイプを作成または変更した後、使用する前にタイプを承認します。

詳しくは、[&#x200B; カスタムオブジェクト製品ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/home)を参照してください。

- APIで作成したカスタムオブジェクトタイプをMarketo UIで変更することはできません。
- カスタムオブジェクトタイプの最大数は10です。
- カスタムオブジェクトフィールドの最大数は、タイプごとに50です。
- カスタムオブジェクトタイプ API名と表示名には、英数字とアンダースコア文字「_」を含めることができます。

### クエリタイプ

次のいずれかの方法で、カスタムオブジェクトタイプのメタデータを取得します。

- 「カスタムオブジェクトタイプを記述」は、1つのカスタムオブジェクトタイプレコードを返し、承認状態によるフィルタリングをサポートします。
- カスタムオブジェクトタイプのリストは、サブスクリプション内のすべてのカスタムオブジェクトタイプを返し、名前と承認状態によるフィルタリングをサポートします。

### 説明タイプ

[&#x200B; カスタムオブジェクトタイプの説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/describeUsingGET_1) エンドポイントは、1つのカスタムオブジェクトタイプのメタデータを返します。 必須の`apiName` パス パラメーターは、記述するタイプのAPI名を指定します。

承認されたバージョンが存在する場合、エンドポイントはそれを返します。 それ以外の場合は、ドラフトバージョンを返します。 オプションの`state` パラメーターを使用して、`draft`、`approved`、または`approvedWithDraft`をリクエストします。

```http
GET /rest/v1/customobjects/schema/{apiName}/describe.json?state=approved
```

```json
{
    "requestId": "d9bf#16876fa84b9",
    "result": [
        {
            "state": "approved",
            "version": "approved",
            "displayName": "Car",
            "description": "Automobile owned",
            "apiName": "car",
            "idField": "marketoGUID",
            "createdAt": "2019-01-22T19:12:18Z",
            "updatedAt": "2019-01-22T19:12:18Z",
            "dedupeFields": [
                "vin"
            ],
            "searchableFields": [
                [
                    "vin"
                ],
                [
                    "marketoGUID"
                ],
                [
                    "leadID"
                ]
            ],
            "relationships": [
                {
                    "field": "leadID",
                    "type": "child",
                    "relatedTo": {
                        "name": "Lead",
                        "field": "id"
                    }
                }
            ],
            "fields": [
                {
                    "name": "createdAt",
                    "displayName": "Created At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "Updated At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "leadID",
                    "displayName": "Lead ID",
                    "dataType": "integer",
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "make",
                    "displayName": "Make",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "model",
                    "displayName": "Model",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "vin",
                    "displayName": "VIN",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "year",
                    "displayName": "Year",
                    "dataType": "integer",
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

応答には次が含まれます。

- メタデータ：状態、displayName、説明、apiName、idField、createdAt、updatedAt、dedupeFields、searchableFields、relationships。
- 標準フィールド：marketoGUID、createdAt、updatedAt
- カスタムフィールド：leadId、vin、make、model、year

### リストタイプ

[カスタムオブジェクトタイプをリスト](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/listCustomObjectTypesUsingGET)エンドポイントは、宛先インスタンスで使用可能なすべてのカスタムオブジェクトタイプのメタデータを返します。 [&#x200B; カスタムオブジェクトのリスト &#x200B;](https://experienceleague.adobe.com/docs/marketo-developer/marketo/soap/custom-objects/custom-objects.html?lang=ja)と似ていますが、状態、関係、フィールドなどの追加のメタデータが含まれます。

承認されたバージョンが存在する場合、エンドポイントはそれを返します。 それ以外の場合は、ドラフトバージョンを返します。

オプションのパラメーターは次のとおりです。

- **状態**：返すバージョンを指定します。 有効な値は&#x200B;**draft**、**approved**、**approvedWithDraft**&#x200B;です。
- **names**: API名のコンマ区切りリストとして返すカスタムオブジェクトタイプを指定します。

```http
GET /rest/v1/customobjects/schema.json?names=purchaseHistory
```

```json
{
    "requestId": "a181#167ebe94703",
    "result": [
        {
            "state": "approved",
            "displayName": "Purchases",
            "description": "Purchase data",
            "apiName": "purchaseHistory",
            "idField": "marketoGUID",
            "createdAt": "2014-09-12T16:13:37Z",
            "updatedAt": "2014-09-12T16:13:42Z",
            "dedupeFields": [
                "lead_id",
                "product_name"
            ],
            "searchableFields": [
                [
                    "lead_id",
                    "product_name"
                ],
                [
                    "marketoGUID"
                ],
                [
                    "lead_id"
                ]
            ],
            "relationships": [
                {
                    "field": "lead_id",
                    "type": "child",
                    "relatedTo": {
                        "name": "Lead",
                        "field": "lead_id"
                    }
                }
            ],
            "fields": [
                {
                    "name": "marketoGUID",
                    "displayName": "marketoGUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "amount",
                    "displayName": "Amount",
                    "dataType": "float",
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "lead_id",
                    "displayName": "lead_id",
                    "dataType": "integer",
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "product_name",
                    "displayName": "Product Name",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "purchase_date",
                    "displayName": "Transaction Date",
                    "dataType": "datetime",
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        },
        {
            "state": "approved",
            "version": "approved",
            "displayName": "Car",
            "description": "No really, it is a car!",
            "apiName": "car_c",
            "idField": "marketoGUID",
            "createdAt": "2017-02-22T19:55:51Z",
            "updatedAt": "2018-12-11T23:52:56Z",
            "dedupeFields": [
                "vin"
            ],
            "searchableFields": [
                [
                    "vin"
                ],
                [
                    "marketoGUID"
                ]
            ],
            "relationships": [],
            "fields": [
                {
                    "name": "createdAt",
                    "displayName": "Created At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "Updated At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "color",
                    "displayName": "Color",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "make",
                    "displayName": "Make",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "model",
                    "displayName": "Model",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "vin",
                    "displayName": "VIN",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "year",
                    "displayName": "Year",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

### タイプの作成と更新

#### タイプの作成

カスタムオブジェクトタイプを作成または更新するには、[&#x200B; カスタムオブジェクトタイプを同期](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) エンドポイントを使用します。

属性は次のとおりです。

- **action**: レコード操作を制御するオプションの属性。 有効な値は&#x200B;**createOnly**、**createOrUpdate**、**updateOnly**&#x200B;です。 デフォルトはcreateOrUpdateです。
- **displayName**&#x200B;および&#x200B;**apiName**: アクションがupdateOnlyでない限り必須です。 お客様がプロビジョニングしたタイプとの競合を避けるために、両方とも一意である必要があります。 LaunchPoint パートナーは、代表的な名前空間を先頭に追加する必要があります。 apiNameの場合、小文字またはcamelCaseを使用して、他のテキスト文字列と区別します。
- **pluralName**: displayNameの複数形を指定するオプションの属性。
- **description**: カスタムオブジェクトタイプを説明するオプションの属性。
- **showInLeadDetail**: Marketo UIのリードデータベースページでカスタムオブジェクトデータを有効にする、オプションのBoolean属性。 デフォルトはfalseです。

カスタムオブジェクト名は慎重に選択してください。 新しいカスタムオブジェクト名の前には、会社を識別する文字列を付けます。 接頭辞には、英数字またはアンダースコアを含めることができます。 この規則により、オブジェクトはMLM UIで見つけやすくなり、名前が一意であることを確認するのに役立ちます。

次の例では、「transaction」というAPI名でカスタムオブジェクトタイプを作成します。

```http
POST /rest/v1/customobjects/schema.json
```

```json
{
  "action":"createOnly",
  "displayName": "Transaction",
  "apiName": "transaction",
  "description": "Commerce happens"
}
```

```json
{
    "requestId": "fb9d#167f2879557",
    "result": [],
    "success": true
}
```

次のリクエストは、新しく作成されたタイプを説明します。

```http
GET /rest/v1/customobjects/schema/transaction/describe.json
```

```json
{
    "requestId": "cf9b#167f28db0a9",
    "result": [
        {
            "state": "draft",
            "displayName": "Transaction",
            "description": "Commerce happens",
            "apiName": "transaction",
            "idField": null,
            "createdAt": null,
            "updatedAt": null,
            "dedupeFields": [],
            "searchableFields": [
                []
            ],
            "relationships": [],
            "fields": [
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "createdAt",
                    "displayName": "Created At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "Updated At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

応答には次が含まれます。

- メタデータ：状態、displayName、説明、apiName、idField、createdAt、updatedAt、dedupeFields、searchableFields、relationships。
- 標準フィールド：marketoGUID、createdAt、updatedAt

#### タイプの更新

次の例では、API名が「transaction」の既存のタイプの説明を更新します。 **apiName** 属性は必須です。 タイプは既に存在するため、リクエストではオプションの&#x200B;**action**&#x200B;属性にupdateOnlyが使用されます。

**apiName**&#x200B;以外にも、作成中に使用可能な属性を更新できます。

```http
POST /rest/v1/customobjects/schema.json
```

```json
{
  "action":"updateOnly",
  "apiName": "transaction",
  "description":"No really, commerce happens!"
}
```

```json
{
    "requestId": "103c3#167f2223fd7",
    "result": [],
    "success": true
}
```

## タイプの承認

カスタムオブジェクトタイプを使用する前に承認します。 [Sync Custom Object Type](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/syncCustomObjectTypeUsingPOST) エンドポイントを使用して型を作成すると、Marketoは下書き版を作成します。 カスタムフィールドを追加したら、ドラフトを承認します。 承認により、承認済みバージョンが作成され、ドラフトが削除されます。

カスタムオブジェクトタイプを同期またはカスタムオブジェクトタイプフィールドエンドポイントの追加/更新/削除を使用して既存のタイプを変更すると、Marketoはドラフトを作成します。 タイプまたはそのフィールドの変更は、ドラフトバージョンにのみ影響します。 変更を加えたら、ドラフトを承認します。 承認は、承認されたバージョンをドラフトに置き換え、ドラフトを削除します。

詳しくは、[&#x200B; カスタムオブジェクトの承認に関するドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object)を参照してください。

カスタムオブジェクトタイプを承認すると、次の操作は実行できなくなります。

- `displayName`または`apiName`を更新します。
- リンクフィールドを追加または削除します。
- 重複排除フィールドの追加または削除。

タイプを承認する前に、スキーマと命名規則を慎重に計画してください。

### タイプの承認

[&#x200B; カスタムオブジェクトタイプを承認](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/approveCustomObjectTypeUsingPOST) エンドポイントを使用して、ドラフトを新しい承認済みバージョンとして公開します。 必須パラメーターは&#x200B;**apiName** パスパラメーターのみです。

タイプは、ドラフト状態で、文書化された[検証ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object)を満たす場合にのみ承認できます。

```http
POST /rest/v1/customobjects/schema/{apiName}/approve.json
```

```json
{
    "requestId": "11d86#1685304a983",
    "result": [],
    "success": true
}
```

### タイプの破棄

[カスタムオブジェクトタイプのドラフトを破棄](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/discardCustomObjectTypeUsingPOST)エンドポイントを使用して、ドラフトバージョンを削除します。 必須パラメーターは`apiName` パス パラメーターのみです。

ドラフト状態では、タイプのみを破棄できます。 承認済みタイプは破棄できません。

```http
POST /rest/v1/customobjects/schema/{apiName}/discardDraft.json
```

```json
{
    "requestId": "5228#1684edde793",
    "result": [],
    "success": true
}
```

### タイプの削除

[カスタムオブジェクトタイプを削除](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST)エンドポイントを使用して、承認済みバージョンを削除します。 必須パラメーターは`apiName` パス パラメーターのみです。

この操作は破壊的であり、元に戻すことはできません。 タイプを削除する前に、トリガーやフィルターなどのアセットからタイプの使用を削除します。 カスタムオブジェクト依存Assets エンドポイントを取得を使用して、タイプの依存アセットを取得します。

POST /rest/v1/customobjects/schema/{apiName}/delete.json

```json
{
    "requestId": "14e36#1684efc4227",
    "result": [],
    "success": true
}
```

## カスタムオブジェクトフィールド

デフォルトでは、すべてのカスタムオブジェクトタイプに次の標準フィールドが含まれます。

- Marketo GUID: カスタムオブジェクトタイプの一意のID。
- 作成日時：カスタムオブジェクトタイプが作成された日時。
- 更新日時：カスタムオブジェクトタイプが最後に更新された日時。

カスタムフィールドを追加、変更、削除するには、次のエンドポイントを使用します。

- フィールドの最大数は50です。
- カスタムオブジェクトを承認した後、最大20個のフィールドを追加できます。
- 少なくとも1つの重複排除フィールドが必要です。 最大3つの重複排除フィールドが許可されます。
- フィールド API名と表示名には、英数字とアンダースコア文字「_」を含めることができます。

詳しくは、[&#x200B; カスタムオブジェクトフィールドのドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)を参照してください。

### フィールドの追加

カスタムオブジェクトに1つ以上のフィールドを追加するには、[&#x200B; カスタムオブジェクトタイプフィールドを追加](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/addCustomObjectTypeFieldsUsingPOST) エンドポイントを使用します。 リクエスト本体には、1 つ以上の要素を含む `input` 配列が含まれます。 各要素は、フィールドを説明する属性を持つ JSON オブジェクトです。

フィールド属性は次のとおりです。

- `name`：必須。 フィールドのAPI名。カスタムオブジェクトに固有である必要があります。 名前を他のテキスト文字列と区別するには、小文字またはキャメルケースを使用します。
- `displayName`：必須。 人間が判読可能なフィールド名。カスタムオブジェクトに固有である必要があります。
- `dataType`：必須。 フィールドのデータタイプ。 [&#x200B; カスタムオブジェクトタイプフィールドデータタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET) エンドポイントを使用して、許可されたデータタイプを取得します。
- `description`：オプション。 フィールドの説明。
- `isDedupeField`: カスタムオブジェクトの更新操作中にフィールドを重複排除に使用するかどうかを指定するオプションのブール値です。 デフォルトはfalseです。 1対多の関係には重複排除フィールドが必要です。
- `relatedTo`: リンクフィールドを指定するオプションのオブジェクト。 1対多の関係の場合、`name`は「リンクオブジェクト」または親オブジェクトを識別し、`field`は親オブジェクトの「リンクフィールド」またはキーフィールドを識別します。

カスタムオブジェクトには、データタイプ「リンク」のフィールドを含めることができます。 リンクフィールドは、カスタムオブジェクトと、リードや会社などの他のオブジェクトタイプとの関係を確立します。 リンクフィールドについて詳しくは、[&#x200B; カスタムオブジェクトフィールドのドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)を参照してください。 許可されたリンクオブジェクトを取得するには、[&#x200B; カスタムオブジェクトのリンク可能オブジェクトを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET) エンドポイントを使用します。

カスタムオブジェクトは、既存のリンクフィールドを持つ別のカスタムオブジェクトにはリンクできません。 詳しくは、[&#x200B; リンクフィールドのドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)を参照してください。

### 1 対多の関係

1対多のカスタムオブジェクト構造の場合は、リンクフィールドを使用して、カスタムオブジェクトを標準のリードオブジェクトまたは会社オブジェクトに接続します。 次のワークフローでは、[自動車所有者の例](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure)を使用して、自動車情報を保存し、リードに接続するカスタムオブジェクトを作成します。

1. **Car** オブジェクトを作成します。
1. **Car** オブジェクトにフィールドを追加します：**VIN**&#x200B;に重複排除し、**リード**&#x200B;**/リード ID**&#x200B;にリンクします。
1. **Car** オブジェクトを承認します。

まず、自動車固有の情報を含むカスタムオブジェクトタイプを作成します。

```http
POST /rest/v1/customobjects/schema.json
```

```json
{
    "action":"createOnly",
    "displayName": "Car",
    "pluralName": "Cars"
    "apiName": "car",
    "description": "Automobile owned",
    "showInLeadDetail": true
}
```

```json
{
    "requestId": "cbaa#16876dd3da6",
    "result": [],
    "success": true
}
```

次に、Car カスタムオブジェクトタイプにフィールドを追加します。 リンクフィールドを使用して、接続するオブジェクトとフィールドの両方を指定します。 この例では、リンクオブジェクトはリードで、リンクフィールドはIDです。

重複排除（VIN）には文字列フィールドを使用します。 さらに3つのフィールドを追加して、Make、Model、Year属性を保存します。

```http
POST /rest/v1/customobjects/schema/car/addField.json
```

```json
{
  "input": [
    {
      "displayName": "Lead ID",
      "description": "Link field to Lead object",
      "name": "leadID",
      "dataType": "link",
      "relatedTo": {
        "field": "id",
        "name": "lead"
      }
    },
    {
      "displayName": "VIN",
      "description": "Vehicle ID number",
      "name": "vin",
      "dataType": "string",
      "isDedupeField": true
    },
    {
      "displayName": "Make",
      "description": "Vehicle make",
      "name": "make",
      "dataType": "string"
    },
    {
      "displayName": "Model",
      "description": "Vehicle model",
      "name": "model",
      "dataType": "string"
    },
    {
      "displayName": "Year",
      "description": "Vehicle year",
      "name": "year",
      "dataType": "integer"
    }
  ]
}

{
    "requestId": "b359#16876f17996",
    "result": [],
    "success": true
}
```

最後に、カスタムオブジェクトタイプを承認します。

```http
POST /rest/v1/customobjects/schema/course/approve.json
```

```json
{
    "requestId": "460b#16896055fa3",
    "result": [],
    "success": true
}
```

### 多対多の関係

多対多の関係では、リードや会社などの標準オブジェクトと「エッジ」カスタムオブジェクトの間に「ブリッジ」カスタムオブジェクトを使用します。 エッジオブジェクトはプライマリエンティティであり、説明フィールドを含みます。

ブリッジオブジェクトは、2つのリンクフィールドとの関係を解決します。 1つのフィールドは、1対多の関係と同様に、親の標準オブジェクトを指します。 もう1つは、リンクのないカスタムオブジェクトであるエッジオブジェクトを指しています。 ブリッジオブジェクトには記述的なフィールドを含めることもできます。

次のワークフローでは、[大学コース登録例](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure)を使用しています。 コース エッジ オブジェクトと、コースとリードを接続する登録ブリッジ オブジェクトが作成されます。

1. **コース** エッジ オブジェクトを作成します。
1. **コース ID**&#x200B;で&#x200B;**コース：**&#x200B;の重複排除にフィールドを追加します。
1. **コース**&#x200B;を承認します。
1. **登録** ブリッジオブジェクトを作成します。
1. **登録：**&#x200B;にフィールドを追加して、**登録ID**&#x200B;に重複排除し、**コース**&#x200B;**/コース ID** フィールドにリンクし、**&#x200B; リード &#x200B;**&#x200B;**/リード ID**&#x200B;にリンクします。
1. **登録**&#x200B;を承認します。

最初に、コース固有の情報を含むエッジオブジェクトタイプを作成します。

```http
POST /rest/v1/customobjects/schema.json
```

```json
{
    "action":"createOnly",
    "displayName": "Course",
    "pluralName": "Courses",
    "apiName": "course",
    "description": "Modeling a college course, an edge object in Marketo",
    "showInLeadDetail": true
}
```

```json
{
    "requestId": "4aec#168879ede00",
    "result": [],
    "success": true
}
```

次に、大学コースをモデル化する4つのカスタムフィールド（コース ID、コースインストラクター、コースの場所、コース名）を追加します。 少なくとも1つの重複排除フィールドが必要なため、「コース ID」を「重複排除」フィールドとして指定します。

```http
POST /rest/v1/customobjects/schema/course/addField.json
```

```json
{
    "input": [
        {
            "displayName": "Course ID",
            "name": "courseID",
            "dataType": "string",
            "isDedupeField": true
        },
        {
            "displayName": "Course Instructor",
            "name": "courseInstructor",
            "dataType": "string"
        },
        {
            "displayName": "Course Location",
            "name": "courseLocation",
            "dataType": "string"
        },
        {
            "displayName": "Course Name",
            "name": "courseName",
            "dataType": "string"
        }
    ]
}
```

```json
{
    "requestId": "cc36#16895b82a41",
    "result": [],
    "success": true
}
```

エッジ オブジェクト タイプを承認して、ブリッジ オブジェクト タイプにリンクするときに参照できるようにします。 カスタムオブジェクトタイプは、リンクオブジェクトとして選択する前に承認する必要があります。

```http
POST /rest/v1/customobjects/schema/course/approve.json
```

```json
{
    "requestId": "460b#16896055fa3",
    "result": [],
    "success": true
}
```

エッジオブジェクトが完了したら、登録固有の情報を含むブリッジオブジェクトタイプを作成します。

```http
POST /rest/v1/customobjects/schema.json
```

```json
{
    "action": "createOnly",
    "displayName": "Enrollment",
    "pluralName": "Enrollments",
    "apiName": "enrollment",
    "description": "Bridge object for Course custom object",
    "showInLeadDetail": true
}
```

```json
{
    "requestId": "8fbb#168960f671b",
    "result": [],
    "success": true
}
```

2つのリンクフィールドをブリッジオブジェクトタイプに追加します。1つはリードオブジェクトにリンクし、もう1つはコースオブジェクトにリンクします。 「リード ID」フィールドを使用してリードにリンクし、「コース ID」フィールドを使用してコースにリンクします。

少なくとも1つの重複排除フィールドが必要なため、重複排除フィールドとして登録IDを追加します。 次に、「成績」フィールドを追加して、学生のパフォーマンスを追跡します。

```http
POST /rest/v1/customobjects/schema/enrollment/addField.json
```

```json
{
    "input": [
        {
            "displayName": "Lead ID",
            "description": "Link field to Lead object",
            "name": "leadID",
            "dataType": "link",
            "relatedTo": {
                "field": "id",
                "name": "lead"
            }
        },
        {
            "displayName": "Course ID",
            "description": "Link field to Course object",
            "name": "courseID",
            "dataType": "link",
            "relatedTo": {
                "field": "courseID",
                "name": "course"
            }
        },
        {
            "displayName": "Enrollment ID",
            "description": "Unique ID for deduplication",
            "name": "enrollmentID",
            "dataType": "string",
            "isDedupeField": true
        },
        {
            "displayName": "Grade",
            "description": "Grade for the course",
            "name": "grade",
            "dataType": "string"
        }
    ]
}
```

```json
{
    "requestId": "7be5#168973f5052",
    "result": [],
    "success": true
}
```

最後に、ブリッジオブジェクトを承認します。

```http
POST /rest/v1/customobjects/schema/enrollment/approve.json
```

```json
{
    "requestId": "9a76#16897b0e84b",
    "result": [],
    "success": true
}
```

[&#x200B; カスタムオブジェクトの同期](#create_and_update)または[&#x200B; カスタムオブジェクトの一括読み込み](https://experienceleague.adobe.com/docs/marketo-developer/marketo/rest/bulk-import/bulk-custom-object-import.html?lang=ja)を使用して、カスタムオブジェクトレコードをプログラムで入力します。 または、Marketo UIで[&#x200B; カスタムオブジェクトデータの読み込み](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/import-custom-object-data)を使用します。

## フィールドの更新

ドラフトカスタムオブジェクトのフィールドを更新するには、[&#x200B; カスタムオブジェクトタイプフィールドを更新](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/updateCustomObjectTypeFieldUsingPOST) エンドポイントを使用します。

必要なパスパラメーターは次のとおりです。

- `apiName`: カスタムオブジェクトタイプのAPI名。
- `fieldAPIName`: カスタムオブジェクトタイプフィールドのAPI名。

リクエスト本文には、更新するフィールド属性を指定するキーと値のペアを持つJSON オブジェクトが含まれています。

```http
POST /rest/v1/customobjects/schema/{apiName}/{fieldApiName}/updateField.json
```

```json
{
  "displayName": "Very Long Title",
  "dataType": "text"
}
```

```json
{
    "requestId": "d523#1684f355db9",
    "result": [],
    "success": true
}
```

## フィールドの削除

カスタムオブジェクトから1つ以上のフィールドを削除するには、[&#x200B; カスタムオブジェクトタイプフィールドを削除](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/deleteCustomObjectTypeFieldsUsingPOST) エンドポイントを使用します。 必須の`apiName` パスパラメーターは、カスタムオブジェクトタイプのAPI名を指定します。

リクエスト本文には、1つ以上の要素の`input`配列を持つJSON オブジェクトが含まれています。 各要素は、`name`属性で削除するフィールドのAPI名を指定するJSON オブジェクトです。

```http
POST /rest/v1/customobjects/schema/{apiName}/deleteField.json
```

```json
{
    "input":
    [
        {
            "name": "title"
        },
        {
            "name": "author"
        }
    ]
}
```

```json
{
"requestId": "b359#19934f17996",
"result": [],
"success": true
}
```

## フィールドデータタイプのリスト

[&#x200B; カスタムオブジェクトタイプフィールドデータタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET) エンドポイントは、許可されているすべてのフィールドデータタイプを返します。 このエンドポイントを使用して、カスタムオブジェクトタイプをモデル化する際に使用できるカスタムフィールドデータタイプを特定します。

```http
GET /rest/v1/customobjects/schema/fieldDataTypes.json
```

```json
{
    "requestId": "c405#167ed49e866",
    "result": [
        "string",
        "boolean",
        "integer",
        "float",
        "link",
        "email",
        "currency",
        "date",
        "datetime",
        "phone",
        "text"
    ],
    "success": true
}
```

## リンク可能なカスタムオブジェクトのリスト

[&#x200B; カスタムオブジェクトの取得リンク可能オブジェクト &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET) エンドポイントは、許可されているすべてのリンクオブジェクトとそのリンクフィールドを返します。 応答には、リードや会社などの標準オブジェクトと、インスタンスで作成されたカスタムオブジェクトが含まれます。

```http
GET /rest/v1/customobjects/schema/linkableObjects.json
```

```json
{
    "requestId": "11e62#167f1160e4e",
    "result": [
        {
            "name": "lead",
            "displayName": "Lead",
            "fields": [
                {
                    "name": "Account Balance",
                    "displayName": "Account Balance",
                    "dataType": "integer"
                },
                {
                    "name": "Email Address",
                    "displayName": "Email Address",
                    "dataType": "email"
                },
                {
                    "name": "Id",
                    "displayName": "Id",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Facebook Display Name",
                    "displayName": "Marketo Social Facebook Display Name",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Facebook Id",
                    "displayName": "Marketo Social Facebook Id",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Facebook Photo URL",
                    "displayName": "Marketo Social Facebook Photo URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Facebook Profile URL",
                    "displayName": "Marketo Social Facebook Profile URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Facebook Reach",
                    "displayName": "Marketo Social Facebook Reach",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Facebook Referred Enrollments",
                    "displayName": "Marketo Social Facebook Referred Enrollments",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Facebook Referred Visits",
                    "displayName": "Marketo Social Facebook Referred Visits",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Gender",
                    "displayName": "Marketo Social Gender",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Display Name",
                    "displayName": "Marketo Social LinkedIn Display Name",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Id",
                    "displayName": "Marketo Social LinkedIn Id",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Photo URL",
                    "displayName": "Marketo Social LinkedIn Photo URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Profile URL",
                    "displayName": "Marketo Social LinkedIn Profile URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Reach",
                    "displayName": "Marketo Social LinkedIn Reach",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social LinkedIn Referred Enrollments",
                    "displayName": "Marketo Social LinkedIn Referred Enrollments",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social LinkedIn Referred Visits",
                    "displayName": "Marketo Social LinkedIn Referred Visits",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Syndication Id",
                    "displayName": "Marketo Social Syndication Id",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Total Referred Enrollments",
                    "displayName": "Marketo Social Total Referred Enrollments",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Total Referred Visits",
                    "displayName": "Marketo Social Total Referred Visits",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Twitter Display Name",
                    "displayName": "Marketo Social Twitter Display Name",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Twitter Id",
                    "displayName": "Marketo Social Twitter Id",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Twitter Photo URL",
                    "displayName": "Marketo Social Twitter Photo URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Twitter Profile URL",
                    "displayName": "Marketo Social Twitter Profile URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Twitter Reach",
                    "displayName": "Marketo Social Twitter Reach",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Twitter Referred Enrollments",
                    "displayName": "Marketo Social Twitter Referred Enrollments",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Twitter Referred Visits",
                    "displayName": "Marketo Social Twitter Referred Visits",
                    "dataType": "integer"
                }
            ]
        },
        {
            "name": "company",
            "displayName": "Company",
            "fields": [
                {
                    "name": "Id",
                    "displayName": "Id",
                    "dataType": "integer"
                }
            ]
        },
        {
            "name": "car_c",
            "displayName": "Car",
            "fields": [
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string"
                },
                {
                    "name": "vin",
                    "displayName": "VIN",
                    "dataType": "string"
                }
            ]
        }
    ],
    "success": true
}
```

## カスタムオブジェクト依存アセットを取得

[&#x200B; カスタムオブジェクト依存Assetsを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeDependentAssetsUsingGET) エンドポイントは、カスタムオブジェクトタイプとそのインスタンス内の場所の依存アセットを返します。 統合を削除する際に、カスタムオブジェクトタイプが使用されているすべての場所を識別するために使用します。

```http
GET /rest/v1/customobjects/schema/{apiName}/dependentAssets.json
```

```json
{
    "requestId": "71cf#16a21f30ed6",
    "result": [
        {
            "assetType": "Smart Campaign",
            "assetId": 3773,
            "assetName": "CarTest.HasCar (Smart List)"
        },
        {
            "assetType": "Smart Campaign",
            "assetId": 3773,
            "assetName": "CarTest.HasCar (Smart List)",
            "usedFields": [
                "leadID",
                "make",
                "model",
                "vin",
                "year"
            ]
        }
    ],
    "success": true
}
```

## タイムアウト

- 特に明記されていない限り、カスタムオブジェクトエンドポイントのタイムアウトは30秒です。
- カスタムオブジェクトの同期のタイムアウトは120秒です。
- カスタムオブジェクトの削除のタイムアウトは60秒です。
