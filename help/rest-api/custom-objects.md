---
title: カスタムオブジェクト
feature: REST API, Custom Objects
description: カスタム Marketo オブジェクトを作成および操作します。
exl-id: 88e8829b-f8f1-46d7-a753-5aa6e20e2c40
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '2909'
ht-degree: 99%

---

# カスタムオブジェクト

[**カスタムオブジェクトエンドポイント参照**](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects) Marketo では、ユーザは Marketo 標準オブジェクト（リード、会社）またはその他の Marketo カスタムオブジェクトに関連する Marketo カスタムオブジェクトを定義できます。Marketo カスタムオブジェクトは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects)の説明に従って Marketo UI を使用して作成することや、以下の説明に従って Custom Object Metadata API を使用して作成することができます。

Custom Object Metadata API にアクセスするには、適切な Marketo サブスクリプションタイプが必要です。詳しくは、CSM にお問い合わせください。

## リスト

リードデータベースオブジェクトで使用できる標準の説明、クエリ、更新、削除呼び出しに加えて、カスタムオブジェクトでは[リスト呼び出し](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectsUsingGET)も使用できます。このエンドポイントを呼び出すと、宛先インスタンスで使用可能なカスタムオブジェクトのリストと、オブジェクトに関する追加のメタデータを含む応答が返されます。

```
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

応答には、各オブジェクトに存在する関係のリストが提供されます。関係には、リンク値を保持するオブジェクトのフィールドを示す `field` メンバー、関係が親タイプオブジェクトか子タイプオブジェクトかを示す `type` メンバー、関連オブジェクトの名前とそのオブジェクトのリンクフィールドを示す `relatedTo` オブジェクトが含まれます。

## 説明

カスタム オブジェクトの[説明呼び出し](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1)は、商談および会社の場合と同じパターンに従いますが、応答に `relationships` 配列が追加され、説明するカスタムオブジェクトタイプの API 名を取得する URI の `apiName` パスパラメーターが追加されます。リスト呼び出しと同様に、これにより、このカスタムオブジェクトタイプで使用可能なすべての関係が一覧表示されます。

```
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

[カスタムオブジェクトのクエリ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectsUsingGET)は、他のLead Database API とは少し異なり、describe と同様に `apiName` パスパラメーターを取ります。通常の filterType パラメーターの場合、クエリは他のタイプのレコードのクエリと同様にシンプルな GET で、`filterType` と `filterValues` が必要です。オプションで、`**fields**`、`batchSize`、`nextPageToken` パラメーターを受け取ります。フィールドのリストをリクエストする際に、特定のフィールドがリクエストされたが返されない場合、その値は null であると見なされます。

```
GET /rest/v1/customobjects/{apiName}.json?filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa,dff23271-f996-47d7-984f-f2676861b5fb
```

```
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

または、複合キーを使用してクエリを実行する際、API は Opportunity Roles API のように動作し、JSON 本文を含む POST を受け取ります。JSON 本文には、`filterValues` を除いて、GET クエリと同じメンバーが含まれる場合があります。フィルター値の代わりに、各オブジェクトタイプの `dedupeFields` の名前が付けられたメンバーを含むオブジェクトを受け取る `input` 配列があります。

```
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

[カスタムオブジェクトを同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST)エンドポイントを使用して、カスタムオブジェクトを作成または更新し、`action` パラメーターを使用して操作を指定できます。1 回の呼び出しで最大 300 個のレコードを作成または更新できます。`input` 配列で使用される値は、主に[カスタムオブジェクトを説明](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/endpoint-reference#!/Custom_Objects/describeUsingGET_1)エンドポイントによって返される情報に基づいています。 例えば、car オブジェクトには、重複排除フィールド `vin` が 1 つだけあります。dedupeFields モードを使用する際にレコードを更新または作成するには、入力配列の各レコードに 1 つ以上の `vin` フィールドを含める必要があります。

```
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

`idField` モードを通じて更新を実行する場合、`idField` は常に `marketoGUID` になるので、各レコードには常に `marketoGUID` フィールドが必要になります。`idField` は常にシステムで管理されるので、updateOnly アクションタイプに対してのみ有効です。応答には、結果配列内の各レコードの&#x200B;**ステータス**&#x200B;と、個々のレコードに対する操作が成功したかどうかに応じて `marketoGUID` または `reasons` 配列のいずれかが含まれます。

## 削除

[レコードの削除](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST)は非常に簡単です。`deleteBy` モード（`idField` または `dedupeFields`）を選択し、`input` 配列の各レコードの対応するフィールドを含めるだけです。1 回の呼び出しあたり最大 300 個のレコードが許可されます。

```
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

更新の場合と同様に、結果には各レコードのステータスと、削除が成功したかどうかに応じて `marketoGUID` または `reasons` 配列が含まれます。

## カスタムオブジェクトタイプ

Custom Object Metadata API を使用すると、カスタムオブジェクトスキーマをリモートで管理できます。この API を使用すると、新しいカスタムオブジェクトタイプを作成したり、既存のカスタムオブジェクトタイプを変更したりできます。カスタムオブジェクトタイプを作成または変更したら、使用するために承認を受ける必要があります。カスタムオブジェクトについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/home)にある製品ドキュメントを参照してください。

* API で作成したカスタムオブジェクトタイプは、Marketo UI を使用して変更できません
* 許可されるカスタムオブジェクトタイプの最大数は 10 です
* 許可されるカスタムオブジェクトフィールドの最大数はタイプあたり 50 です
* カスタムオブジェクトタイプの API 名と表示名には、英数字とアンダースコア「_」を含めることができます。

### クエリタイプ

カスタムオブジェクトタイプのメタデータを取得する方法は 2 つあります。「カスタムオブジェクトタイプを説明」は、単一のカスタムオブジェクトタイプのレコードを返す機能で、承認状態によるフィルタリングが可能です。「カスタムオブジェクトタイプをリスト」は、サブスクリプション内のすべてのカスタムオブジェクトタイプのリストを返す機能で、名前と承認状態によるフィルタリングが可能です。

### 説明タイプ

[カスタムオブジェクトタイプを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1)エンドポイントは、単一のカスタムオブジェクトタイプのメタデータを返します。必須の `apiName` パスパラメーターは、説明するカスタムオブジェクトタイプの API 名です。承認済みバージョンが存在する場合は、それが返されます。それ以外の場合は、ドラフトバージョンが返されます。オプションの `state` パラメーターは、返されるバージョン（`draft`、`approved`、`approvedWithDraft`）を指定するために使用されます。

```
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

ここでは、次の属性を確認できます。

* メタデータ：state、displayName、description、apiName、idField、createdAt、updatedAt、dedupeFields、searchableFields、relationships
* 標準フィールド：marketoGUID、createdAt、updatedAt
* カスタムフィールド：leadId、vin、make、model、year

### リストタイプ

[カスタムオブジェクトタイプをリスト](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/listCustomObjectTypesUsingGET)エンドポイントは、宛先インスタンスで使用可能なすべてのカスタムオブジェクトタイプのメタデータを返します。このエンドポイントは、[カスタムオブジェクトをリスト](https://experienceleague.adobe.com/docs/marketo-developer/marketo/soap/custom-objects/custom-objects.html?lang=ja)に似ていますが、より包括的で、状態、関係、フィールドなどの追加のメタデータが含まれています。承認済みバージョンが存在する場合は、それが返されます。それ以外の場合は、ドラフトバージョンが返されます。オプションの **state** パラメーターは、返されるカスタムオブジェクトタイプのバージョン（**draft**、**approved**、**approvedWithDraft**）を指定するために使用されます。オプションの **names** パラメーターは、返されるカスタムオブジェクトタイプの特定の名前を指定するために使用されます。これは、API 名のコンマ区切りリストとして構造化されています。

```
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
            "description": "No really, it's a car!",
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

[カスタムオブジェクトタイプを同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST)エンドポイントは、カスタムオブジェクトタイプを作成または更新するために使用されます。実行するレコード操作は、**createOnly**、**createOrUpdate** または **updateOnly** に指定できるオプションの **action** 属性によって制御されます。デフォルト設定は createOrUpdate です。アクションとして updateOnly を使用する場合を除き、**displayName** 属性と **apiName** 属性は必須です。お客様がプロビジョニングしたタイプとの競合を避けるために、両方とも一意である必要があります。Launchpoint パートナーの場合は、これらの名前の前に代表的な名前空間を追加する必要があります。apiName の場合、規則では、他のテキスト文字列を区別しやすくするために、小文字または camelCase を使用します。オプションの **pluralName** 属性は、displayName の複数形を指定します。オプションの **description** 属性は、カスタムオブジェクトタイプを説明するために使用されます。オプションの **showInLeadDetail** ブール値属性は、Marketo UI のリードデータベースページ内でカスタムオブジェクトデータを表示できるようにするために使用されます。デフォルト設定は false です。

カスタムオブジェクトに名前を付ける場合は注意してください。新しいカスタムオブジェクトを作成する際は、名前の前に会社名を示す文字列（英数字またはアンダースコアが使用可能）を付けることをお勧めします。これにより、カスタムオブジェクトを MLM UI で簡単に検索でき、名前が一意であることも確認できます。

API 名「transaction」を使用して新しいカスタムオブジェクトタイプを作成する例を以下に示します。

```
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

新しく作成されたタイプを説明する後続の呼び出しを以下に示します。

```
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

ここでは、次のカスタムオブジェクト関連データを確認できます。

* メタデータ：state、displayName、description、apiName、idField、createdAt、updatedAt、dedupeFields、searchableFields、relationships
* 標準フィールド：marketoGUID、createdAt、updatedAt

#### タイプの更新

API 名が「transaction」である既存のタイプの説明を更新する例を以下に示します。**apiName** 属性は必須です。ここでは、タイプが既に存在すると想定し、オプションの **action** 属性に updateOnly を使用します。**apiName** とは別に、作成に使用できる属性は更新される場合があります。

```
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

カスタムオブジェクトタイプは、使用する前に承認する必要があります。[カスタムオブジェクトタイプを同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectTypeUsingPOST)エンドポイントを使用して新しいカスタムオブジェクトタイプを作成すると、ドラフトバージョンとして作成されます。カスタムフィールドの追加が完了したら、ドラフトバージョンを承認する必要があります。これにより、承認済みバージョンが作成され、ドラフトバージョンが削除されます。「カスタムオブジェクトタイプを同期」エンドポイントを使用するか、「カスタムオブジェクトタイプフィールドを追加／更新／削除」エンドポイントのいずれかを使用して既存のカスタムオブジェクトタイプを変更すると、ドラフトバージョンが作成されます。タイプまたはそのフィールドに対するすべての変更は、ドラフトバージョンにのみ影響します。変更が完了したら、ドラフトバージョンを承認する必要があります。これにより、承認済みバージョンがドラフトバージョンに置き換えられ、ドラフトバージョンが削除されます。カスタムオブジェクトの承認について詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object)にある製品ドキュメントを参照してください。

カスタムオブジェクトタイプを承認すると、次の操作は実行できなくなります。

* `displayName` または `apiName` を更新
* リンクフィールドを追加または削除
* 重複排除フィールドを追加または削除

これらの理由から、使用する予定のスキーマと命名規則を慎重に検討することが重要です。

### タイプの承認

[カスタムオブジェクトタイプを承認](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/approveCustomObjectTypeUsingPOST)エンドポイントを使用して、ドラフトバージョンを新しい承認済みバージョンとして公開します。**apiName** は、パスパラメーターとして唯一の必須パラメーターです。タイプは、ドラフト状態で、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object)で説明する一連の検証ルールを満たしていない限り、承認できません。

```
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

[カスタムオブジェクトタイプのドラフトを破棄](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/discardCustomObjectTypeUsingPOST)エンドポイントを使用して、ドラフトバージョンを削除します。`apiName` は、パスパラメーターとして唯一の必須パラメーターです。タイプを破棄するには、ドラフト状態である必要があります。つまり、承認済みのタイプは破棄できません。

```
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

[カスタムオブジェクトタイプを削除](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST)エンドポイントを使用して、承認済みバージョンを削除します。`apiName` は、パスパラメーターとして必要な唯一のパラメーターです。これは破壊的な操作であり、元に戻すことはできません。タイプは、トリガーやフィルターなどのアセットから使用が解除されていない限り削除できません。「カスタムオブジェクト依存アセットを取得」エンドポイントは、特定のタイプの依存アセットのリストを取得するために使用できます。

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

* Marketo GUID - カスタムオブジェクトタイプの一意の ID
* 作成日時 - カスタムオブジェクトタイプを作成した日時
* 更新日時 - カスタムオブジェクトタイプを最後に更新した日時

以下に説明するエンドポイントを使用して、カスタムフィールドを自由に追加、変更、削除できます。

* 許可されるフィールドの最大数は 50 です
* カスタムオブジェクトを承認した後、カスタムオブジェクトに最大 20 個の追加フィールドを追加できます
* 1 つ以上の重複排除フィールドが必要です。最大 3 つまで許可されます。
* フィールドの API 名と表示名には、英数字とアンダースコア「_」を含めることができます。

カスタムオブジェクトフィールドについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)にある製品ドキュメントを参照してください。

### フィールドの追加

[カスタムオブジェクトタイプフィールドを追加](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/addCustomObjectTypeFieldsUsingPOST)エンドポイントを使用すると、カスタムオブジェクトに 1 つ以上のフィールドを追加できます。リクエスト本体には、1 つ以上の要素を含む `input` 配列が含まれます。各要素は、フィールドを説明する属性を持つ JSON オブジェクトです。必須の `name` 属性はフィールドの API 名で、カスタムオブジェクトに対して一意である必要があります。規則では、他のテキスト文字列を区別しやすくするために、すべて小文字または camelCase を使用します。必須の `displayName` 属性は、人間が読み取り可能なフィールドの名前で、カスタムオブジェクトに対して一意である必要があります。必須の `dataType` 属性は、フィールドのデータタイプです。許可されるデータタイプのリストは、[カスタムオブジェクトタイプフィールドデータタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET)エンドポイントを呼び出すことによって取得できます。カスタムオブジェクトには、データタイプが &quot;link&quot; のフィールドを含めることができます。リンクフィールドは、カスタムオブジェクトとシステム内の他のオブジェクトタイプ（例：リード、会社）間の関係を確立するために使用されます。リンクフィールドについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)を参照してください。オプションの `description` 属性は、フィールドの説明です。オプションの `isDedupeField` ブール値属性は、カスタムオブジェクトの更新操作中にフィールドが重複排除に使用されるかどうかを指定します。デフォルト設定は false です。1 対多の関係の場合、重複排除フィールドは必須です。オプションの `relatedTo` オブジェクト属性は、リンクフィールドを指定します。1 対多の関係の場合、このオブジェクトには、リンク先の「リンクオブジェクト」または親オブジェクトである `name` 属性と、キー属性として使用する親オブジェクト内の「リンクフィールド」または `field` 属性が含まれます。許可されるリンクオブジェクトのリストを取得するには、[カスタムオブジェクトリンク可能オブジェクトを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET)エンドポイントを呼び出します。リンクフィールドについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)にある製品ドキュメントを参照してください。カスタムオブジェクトは、既存のリンクフィールドを持つ別のカスタムオブジェクトにはリンクできません。

### 1 対多の関係

1 対多のカスタムオブジェクト構造の場合は、カスタムオブジェクトのリンクフィールドを使用して、標準オブジェクト（リードまたは会社）に接続します。[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure)のMarketo 製品ドキュメントの自動車所有者の例を使用して、リードに接続する自動車関連情報を含むカスタムオブジェクトを作成します。

1. **Car** オブジェクトを作成します
1. **Car** オブジェクトにフィールドを追加します。**VIN** で重複を削除し、**Lead**&#x200B;***/Lead ID** にリンクします
1. **Car** オブジェクトを承認します

最初に、自動車固有の情報を含めるカスタムオブジェクトタイプを作成します。

```
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

次に、Car カスタムオブジェクトタイプにフィールドを追加します。リンクフィールドを使用して、接続するオブジェクトとフィールドの両方を指定します。この場合、リンクオブジェクトはリードで、リンクフィールドは ID です。重複排除（VIN）には文字列フィールドを使用します。追加の自動車属性（メーカー、モデル、年式）を保存するために、さらに 3 つのフィールドを追加します。

```
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

```
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

多対多の関係は、リードや会社などの標準カスタムオブジェクトと「エッジ」カスタムオブジェクトの間にある「ブリッジ」または中間カスタムオブジェクトを使用して表されます。エッジオブジェクトは、説明的な属性（フィールド）を含むプライマリエンティティです。ブリッジオブジェクトには、2 つのリンクフィールドを使用してオブジェクトの関係を解決するためのデータが含まれています。1 つのリンクフィールドは、1 対多の関係設定と同様に、親の標準オブジェクトを指します。もう一方のリンクフィールドは、リンクのないカスタムオブジェクトであるエッジオブジェクトを指します。ブリッジオブジェクトには、説明的な属性（フィールド）も含まれる場合があります。[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure)にある Marketo 製品ドキュメントの大学コース登録の例を使用して、コース関連情報を含むエッジカスタムオブジェクトと、コースとリードを接続するために使用される登録ブリッジオブジェクトを作成します。手順は次の通りです。

1. **コース**&#x200B;エッジオブジェクトを作成します
1. **コース**&#x200B;にフィールドを追加します。**コース ID** で重複排除します
1. **コース**&#x200B;を承認します
1. **登録**&#x200B;ブリッジオブジェクトを作成します
1. **登録**&#x200B;にフィールドを追加します。**登録 ID**、**コース**&#x200B;**/コース ID** フィールドへのリンク、**リード**&#x200B;**/リード ID** へのリンクで重複削除します
1. **登録**&#x200B;を承認します

最初に、コース固有の情報を含めるエッジオブジェクトタイプを作成します。

```
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

次に、エッジオブジェクトタイプにカスタムフィールドを追加します。この例では、大学のコースをモデル化するために、コース ID、コースインストラクター、コースの場所、コース名の 4 つのカスタムフィールドを追加します。1 つ以上の重複排除フィールドが必須なので、コース ID を重複排除フィールドとして指定します。

```
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

```
{
    "requestId": "cc36#16895b82a41",
    "result": [],
    "success": true
}
```

ここで、後でブリッジオブジェクトタイプにリンクする際に参照できるように、エッジオブジェクトタイプを承認する必要があります。カスタムオブジェクトタイプは、リンクオブジェクトとして選択できるように承認する必要があります。

```
POST /rest/v1/customobjects/schema/course/approve.json
```

```json
{
    "requestId": "460b#16896055fa3",
    "result": [],
    "success": true
}
```

エッジオブジェクトが完成しました。次に、登録固有の情報を含むブリッジオブジェクトタイプの作成に進みます。

```
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

ブリッジオブジェクトタイプにカスタムフィールドを追加するには、2 つのリンクフィールドを追加します。1 つはリードオブジェクトにリンクし、もう 1 つは先ほど作成したコースオブジェクトにリンクします。リードオブジェクトにリンクするには、「リード ID」フィールドを使用します。コースオブジェクトにリンクするには、「コース ID」フィールドを使用します。次に、1 つ以上の重複排除フィールドが必要なので、重複排除フィールドとして登録 ID の一意の ID を追加します。最後に、学生の成績を追跡するための「成績」フィールドを追加します。

```
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

```
POST /rest/v1/customobjects/schema/enrollment/approve.json
```

```json
{
    "requestId": "9a76#16897b0e84b",
    "result": [],
    "success": true
}
```

[カスタムオブジェクトを同期](#create_and_update)または[カスタムオブジェクトの一括読み込み](https://experienceleague.adobe.com/docs/marketo-developer/marketo/rest/bulk-import/bulk-custom-object-import.html?lang=ja)を使用して、カスタムオブジェクトレコードをプログラムで入力できます。または、Marketo UI 機能の[カスタムオブジェクトデータを読み込み](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/import-custom-object-data)を使用することもできます。

## フィールドの更新

[カスタムオブジェクトタイプフィールドを更新](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/updateCustomObjectTypeFieldUsingPOST)エンドポイントを使用すると、ドラフトのカスタムオブジェクトのフィールドを更新できます。必須のパスパラメーター `apiName` は、カスタムオブジェクトタイプの API 名です。必須のパスパラメーター `fieldAPIName` は、カスタムオブジェクトタイプフィールドの API 名です。リクエスト本文には、更新するフィールド属性を指定するキーと値のペアを含む JSON オブジェクトが含まれます。

```
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

[カスタムオブジェクトタイプフィールドを削除](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectTypeFieldsUsingPOST)エンドポイントを使用すると、カスタムオブジェクトから 1 つ以上のフィールドを削除できます。必須のパスパラメーター `apiName` は、カスタムオブジェクトタイプの API 名です。リクエスト本体には、1 つ以上の要素を含む `input` 配列を持つ JSON オブジェクトが含まれます。各要素は、削除するフィールドの API 名を指定する `name` 属性を持つ JSON オブジェクトです。

```
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

[カスタムオブジェクトタイプフィールドデータタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET)エンドポイントは、許可されるすべてのフィールドデータタイプのリストを返します。これは、カスタムオブジェクトタイプをモデル化して、サポートされているカスタムフィールドデータタイプを識別する際に役立ちます。

```
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

[カスタムオブジェクトリンク可能オブジェクトを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET)エンドポイントは、許可されているすべてのリンクオブジェクトとそのリンクフィールドのリストを返します。リストには、標準オブジェクト（リード、会社）と、インスタンスで作成されたカスタムオブジェクトが含まれます。

```
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

[カスタムオブジェクト依存アセットを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeDependentAssetsUsingGET)エンドポイントは、インスタンス内の場所を含む、カスタムオブジェクトタイプの依存アセットのリストを返します。これは、統合を削除し、カスタムオブジェクトタイプが使用されているすべての場所を識別する必要がある際に役立ちます。

```
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

* 「カスタムオブジェクト」エンドポイントは、以下に記載されていない限り、30 秒でタイムアウトします
   * カスタムオブジェクトを同期：120 秒 
   * カスタムオブジェクトを削除：60 秒
