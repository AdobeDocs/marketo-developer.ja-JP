---
title: カスタムオブジェクト
feature: REST API, Custom Objects
description: カスタム Marketo オブジェクトを作成および操作します。
source-git-commit: f1c9c5ba07013c2fdccb9f799b5c0077eb789a4b
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 0%

---


# カスタムオブジェクト

[**カスタムオブジェクトエンドポイントリファレンス**](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects) Marketoを使用すると、Marketo標準オブジェクト（リード、会社）または他のMarketo カスタムオブジェクトに関連するMarketo カスタムオブジェクトを定義できます。  Marketoのカスタムオブジェクトは、Marketo UI を使用して [ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects) で説明されているように作成することも、以下で説明するようにカスタムオブジェクトメタデータ API を使用して作成することもできます。

カスタムオブジェクトメタデータ API にアクセスするには、適切なMarketo購読タイプが必要です。  詳しくは、CSM に問い合わせてください。

## リスト

リードデータベースオブジェクトで使用できる標準の記述、クエリ、更新、削除の呼び出しに加えて、カスタムオブジェクトでは [ リスト呼び出し ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectsUsingGET) を使用できます。  このエンドポイントを呼び出すと、宛先インスタンスで使用可能なカスタムオブジェクトのリストと、オブジェクトに関する追加のメタデータを含む応答が返されます。

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

応答には、各オブジェクトに存在する関係のリストが表示されます。  リレーションシップには、リンク値を保持するオブジェクト上のフィールドを示す `field` メンバ、リレーションシップが親と子のどちらのものかを示す `type` メンバ、および関連オブジェクトの名前、およびそのオブジェクト上のリンク フィールドを示す `relatedTo` オブジェクトが含まれます。

## 説明

カスタムオブジェクトの [describe 呼び出し ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1) は、Opportunity や Companies と同じパターンに従います。さらに、応答に `relationships` 配列を追加し、説明するカスタムオブジェクトタイプの API 名を取る URI に `apiName` パスパラメーターを追加します。  リスト呼び出しと同様に、このカスタムオブジェクトタイプで使用可能な関係がリストされます。

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

[ カスタムオブジェクトのクエリ ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectsUsingGET) は、他のリードデータベース API とは少し異なり、describe のようなパスパラメーター `apiName` 取ります。  通常の filterType パラメーターの場合、クエリは、他の種類のレコードのクエリと同様の単純なGETであり、`filterType` と `filterValues` が必要です。  オプションで、`**fields**`、`batchSize`、`nextPageToken` のパラメーターを受け入れます。  フィールドのリストをリクエストするときに、特定のフィールドがリクエストされても返されなかった場合、値は null であることが暗示されます。

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

または、複合キーでクエリを実行する場合、API は Opportunity Roles API と同様に動作し、JSON 本文を含むPOSTを受け入れます。  JSON 本文は、`filterValues` を除き、GETクエリと同じメンバーを持つ場合があります。  フィルター値の代わりに、オブジェクトを受け取る `input` 配列があります。このオブジェクトには、オブジェクトタイプの `dedupeFields` ごとに名前が付けられたメンバーが含まれています。

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

[ カスタムオブジェクトを同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) エンドポイントを使用して、カスタムオブジェクトを作成または更新すると、`action` パラメーターを使用して操作を指定できます。  1 回の呼び出しで最大 300 個のレコードを作成または更新できます。  `input` 配列で使用される値は、主に [ カスタムオブジェクトを記述 ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/endpoint-reference#!/Custom_Objects/describeUsingGET_1) エンドポイントから返される情報に基づいています。 例えば、car オブジェクトには、重複排除フィールド `vin` が 1 つだけ存在します。  dedupeFields モードを使用する場合にレコードを更新または作成するには、入力配列内の各レコードに少なくとも `vin` フィールドを含める必要があります。

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

`idField` モードを使用して更新を実行する場合、`idField` は常に `marketoGUID` なので、各レコードには常に `marketoGUID` フィールドが必要です。  `idField` のフィールドは常にシステム管理なので、updateOnly アクションタイプに対してのみ有効です。  応答には、結果配列内の個々のレコードの **ステータス** が含まれます。また、個々のレコードに対して操作が成功したかどうかに応じて、`marketoGUID` または `reasons` の配列が含まれます。

## 削除

[ レコードの削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST) は非常に簡単です。  `deleteBy` モード（`idField` または `dedupeFields`）を選択し、`input` 配列の各レコードに対応するフィールドを含めるだけです。 1 回の呼び出しにつき最大 300 レコードまで許可されます。

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

更新と同様に、結果には、個々のレコードのステータスと、削除が成功したかどうかに応じて `marketoGUID` または `reasons` 配列が含まれます。

## カスタムオブジェクトタイプ

Custom Object Metadata API を使用すると、カスタムオブジェクトスキーマをリモートで管理できます。  API を使用すると、新しいカスタムオブジェクトタイプを作成したり、既存のカスタムオブジェクトタイプを変更したりできます。  カスタムオブジェクトタイプを作成または変更したら、使用を承認する必要があります。  カスタムオブジェクトについて詳しくは、製品ドキュメント [ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/home) を参照してください。

* API で作成されたカスタムオブジェクトタイプは、Marketo UI を使用して変更することはできません
* 許可されるカスタムオブジェクトタイプの最大数は 10 です
* タイプごとに許可されるカスタムオブジェクトフィールドの最大数は 50 です
* カスタムオブジェクトタイプの API 名および表示名には、英数字およびアンダースコア「_」を含めることができます

### クエリタイプ

カスタムオブジェクトタイプのメタデータを取得する方法は 2 つあります。カスタムオブジェクトタイプを記述すると、が返されます  1 つのカスタムオブジェクトタイプのレコードで、承認状態でフィルタリング可能です。List Custom Object Types は、サブスクリプション内のすべてのカスタムオブジェクトタイプのリストを返し、名前および承認状態でフィルタリングできます。

### 説明タイプ

[ カスタムオブジェクトタイプを記述 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1) エンドポイントは、単一のカスタムオブジェクトタイプのメタデータを返します。 必須の `apiName` パスパラメーターは、説明されているカスタムオブジェクトタイプの API 名です。  承認済みバージョンが存在する場合は、返されます。  それ以外の場合は、ドラフトバージョンが返されます。  オプションの `state` パラメーターを使用して、返されるバージョン（`draft`、`approved`、`approvedWithDraft`）を指定します。

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

* メタデータ：state、displayName、description、apiName、idField、createdAt、updatedAt、dedupeFields、searchableFields、relationship
* 標準フィールド：marketoGUID、createdAt、updatedAt
* カスタムフィールド leadId、vin、make、  モデル、年

### リストタイプ

[ カスタムオブジェクトタイプのリスト ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/listCustomObjectTypesUsingGET) エンドポイントは、宛先インスタンスで使用可能なすべてのカスタムオブジェクトタイプのメタデータを返します。  このエンドポイントは [ カスタムオブジェクトをリスト ](https://experienceleague.adobe.com/docs/marketo-developer/marketo/soap/custom-objects/custom-objects.html?lang=ja) に似ていますが、より包括的で、状態、関係、フィールドなどの追加のメタデータが含まれています。 承認済みバージョンが存在する場合は、返されます。  それ以外の場合は、ドラフトバージョンが返されます。  オプションの **state** パラメーターを使用して、返されるカスタムオブジェクトタイプのバージョン（**draft**、**approved**、または **approvedWithDraft**）を指定します。  オプションの **names** パラメーターは、返されるカスタムオブジェクトタイプの特定の名前を指定するために使用されます。これは、API 名のコンマ区切りリストとして構造化されています。

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

### タイプを作成および更新

#### タイプを作成

[ カスタムオブジェクトタイプを同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) エンドポイントは、カスタムオブジェクトタイプの作成または更新に使用されます。  実行するレコード操作は、オプションの **action** 属性によって制御されます。この属性は、**createOnly**、**createOrUpdate** または **updateOnly** のいずれかになります。  デフォルト設定は createOrUpdate です。 updateOnly をアクションとして使用する場合を除き、**displayName** 属性と **apiName** 属性は必須です。   顧客がプロビジョニングしたタイプとの競合を避けるために、どちらも一意である必要があります。  LaunchPoint パートナーの場合は、それらの名前に代表的な名前空間を付加する必要があります。  apiName の規則では、他のテキスト文字列を区別するために小文字またはキャメルケースを使用します。 オプションの **pluralName** 属性は、displayName の複数形式を指定します。  オプションの **description** 属性は、カスタムオブジェクトタイプを記述するために使用されます。  オプションの **showInLeadDetail** ブール値の属性を使用すると、Marketo UI のリードデータベースページ内でカスタムオブジェクトデータを表示できます。  デフォルト設定は false です。

カスタムオブジェクトの名前には注意が必要です。 新しいカスタムオブジェクトを作成する際は、名前の前に、会社名を示す文字列（英数字またはアンダースコアを使用できます）を付けることをお勧めします。 これにより、MLM UI 内でカスタムオブジェクトを簡単に検索できるようになり、名前が一意であることも確信できるようになります。

以下は、API を使用して新しいカスタムオブジェクトタイプを作成する例です  名前「transaction」です。

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

次に、新しく作成されたタイプを記述する呼び出しを示します。

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

ここには、次のカスタムオブジェクト関連データが表示されます。

* メタデータ：state、displayName、description、apiName、idField、createdAt、updatedAt、dedupeFields、searchableFields、relationship
* 標準フィールド：marketoGUID、createdAt、updatedAt

#### 更新の種類

API 名が「transaction」である既存タイプの説明を更新する例を次に示します。  **apiName** 属性は必須です。  ここでは、タイプが既に存在し、オプションの **action** 属性に updateOnly を使用するとします。  **apiName** とは別に、作成に使用できる属性が更新される場合があります。

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

カスタムオブジェクトタイプは、使用する前に承認する必要があります。 [ カスタムオブジェクトタイプを同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectTypeUsingPOST) エンドポイントを使用して新しいカスタムオブジェクトタイプを作成すると、ドラフトバージョンとして作成されます。 カスタムフィールドの追加が完了したら、ドラフトバージョンを承認する必要があります。 これにより、承認済みバージョンが作成され、ドラフトバージョンが削除されます。 既存のカスタムオブジェクトタイプが、「カスタムオブジェクトタイプを同期」エンドポイントを使用して、またはカスタムオブジェクトタイプのフィールドの「追加」、「更新」、「削除」のいずれかのエンドポイントを使用して変更されると、ドラフトバージョンが作成されます。 タイプまたはそのフィールドに対するすべての変更は、ドラフトバージョンにのみ影響します。 変更が完了したら、ドラフトバージョンを承認する必要があります。 これにより、承認済みバージョンがドラフトバージョンに置き換えられ、ドラフトバージョンが削除されます。 カスタムオブジェクトの承認について詳しくは、製品ドキュメント [ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object) を参照してください。

カスタムオブジェクトタイプが承認されると、次の操作はできなくなります。

* `displayName` または `apiName` の更新
* リンクフィールドの追加または削除
* 重複排除フィールドの追加または削除

これらの理由から、使用するスキーマと命名規則を慎重に検討することが重要です。

### 承認タイプ

[ カスタムオブジェクトタイプを承認 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/approveCustomObjectTypeUsingPOST) エンドポイントを使用して、ドラフトバージョンを新しい承認済みバージョンとして公開します。  **apiName** は、パスパラメーターとして必要な唯一のパラメーターです。  タイプは、ドラフト状態でない限り承認できません。また、タイプが [ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object) で説明されている一連の検証ルールを満たしている必要があります。

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

### 破棄タイプ

[ カスタムオブジェクトタイプのドラフトを破棄 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/discardCustomObjectTypeUsingPOST) エンドポイントを使用して、ドラフトバージョンを削除します。 パスパラメーターとして必須のパラメーターは `apiName` のみです。 タイプを破棄するには、タイプがドラフト状態である必要があります。つまり、承認済みタイプは破棄できません。

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

### タイプを削除

[ カスタムオブジェクトタイプを削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST) エンドポイントを使用して、承認済みバージョンを削除します。  パスパラメーターとして必須のパラメーターは `apiName` のみです。  これは破壊的な操作であり、元に戻すことはできません。  タイプは、トリガーやフィルターなどのアセットで使用から削除されていない限り、削除できません。  「カスタムオブジェクトの依存Assetsを取得」エンドポイントは、特定のタイプの依存アセットのリストを取得するために使用できます。

POST /rest/v1/customobjects/schema/{apiName}/delete.json

```json
{
    "requestId": "14e36#1684efc4227",
    "result": [],
    "success": true
}
```

## カスタムオブジェクトフィールド

デフォルトでは、すべてのカスタムオブジェクトタイプには、次の標準フィールドが含まれています。

* Marketo GUID - カスタムオブジェクトタイプの一意の ID
* 作成日時 – カスタムオブジェクトタイプが作成された日時
* 更新日時 – カスタムオブジェクトタイプが最後に更新された日時

以下に説明するエンドポイントを使用して、カスタムフィールドを自由に追加、変更、削除できます。

* 許可されるフィールドの最大数は 50 です
* カスタムオブジェクトが承認された後、このカスタムオブジェクトに最大 20 個のフィールドを追加できます
* 少なくとも 1 つの重複排除フィールドが必要です。最大 3 つまで指定できます
* フィールド API 名および表示名には、英数字およびアンダースコア「_」を含めることができます

カスタムオブジェクトフィールドについて詳しくは、製品ドキュメント [ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) を参照してください。

### フィールドを追加

[ カスタムオブジェクトタイプフィールドを追加 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/addCustomObjectTypeFieldsUsingPOST) エンドポイントを使用すると、1 つ以上のフィールドをカスタムオブジェクトに追加できます。  リクエスト本文には、1 つ以上の要素を持つ `input` 配列が含まれます。  各要素は、フィールドを記述する属性を持つ JSON オブジェクトです。 必須の `name` 属性はフィールドの API 名で、カスタムオブジェクトに対して一意である必要があります。   規則では、他のテキスト文字列を区別するために小文字または camelCase を使用します。 必須の `displayName` 属性は、人間が判読できるフィールドの名前であり、カスタムオブジェクトに対して一意である必要があります。 必須の `dataType` 属性は、フィールドのデータタイプです。  A  許可されるデータタイプのリストは、[ カスタムオブジェクトタイプフィールドのデータタイプを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET) エンドポイントを呼び出すことで取得できます。  カスタムオブジェクトには、データタイプが「リンク」のフィールドを含めることができます。  リンクフィールドは、カスタムオブジェクトとシステム内の他のオブジェクトタイプ（リード、会社など）との関係を確立するために使用されます。  リンクフィールドについて詳しくは、[ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) を参照してください。 オプションの `description` 属性は、フィールドの説明です。 オプションの `isDedupeField` boolean 属性は、カスタムオブジェクト更新操作中の重複排除にフィールドを使用するかどうかを指定します。  デフォルト設定は false です。  1 対多の関係の場合、重複排除フィールドは必須です。 オプションの `relatedTo` オブジェクト属性は、リンクフィールドを指定します。  1 対多の関係の場合、このオブジェクトには、「リンクオブジェクト」またはリンク先の親オブジェクトである `name` 属性と、「リンクフィールド」である `field` 属性が含まれます。  または、親オブジェクト内のフィールドをキー属性として使用します。  [ カスタムオブジェクトのリンク可能オブジェクトを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET) エンドポイントを呼び出して、許可されるリンクオブジェクトのリストを取得します。  リンクフィールドについて詳しくは、製品ドキュメント [ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) を参照してください。 カスタムオブジェクトは、既存のリンクフィールドを持つ別のカスタムオブジェクトにリンクすることはできません。

### 1 対多の関係

1 対多のカスタムオブジェクト構造の場合、カスタムオブジェクトのリンクフィールドを使用して、標準オブジェクト（リードまたは会社）に接続します。 Marketo製品ドキュメント [ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure) にある自動車オーナーの例を使用して、リードと結び付ける自動車関連情報を含むカスタムオブジェクトを作成します。

1. **Car** オブジェクトを作成する
1. **Car** オブジェクトにフィールドを追加：**VIN** での重複排除、**リード**&#x200B;**/リード ID**&#x200B;へのリンク
1. **Car** オブジェクトを承認

まず、自動車固有の情報を格納するカスタム オブジェクト タイプを作成します。

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

次に、Car カスタムオブジェクトタイプにフィールドを追加します。 リンクフィールドを使用して、オブジェクトと接続先のフィールドの両方を指定します。 この場合、リンクオブジェクトはリードで、リンクフィールドは ID です。 重複排除（VIN）には文字列フィールドを使用します。  追加の車属性（車種、モデル、年）を保存するために、さらに 3 つのフィールドを追加します。

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

### 多対多関係

多対多の関係は、リードや会社などの標準カスタムオブジェクトと「エッジ」カスタムオブジェクトの間の「ブリッジ」（仲介者）カスタムオブジェクトを使用して表されます。 エッジオブジェクトは、説明属性（フィールド）を含むプライマリエンティティです。 ブリッジ オブジェクトには、2 つのリンク フィールドを使用してオブジェクトの関係を解決するためのデータが含まれています。  1 つのリンク フィールドは、  1 対多の関係設定。  もう 1 つのリンクフィールドは、リンクのないカスタムオブジェクトであるエッジオブジェクトを指しています。  ブリッジオブジェクトには、記述属性（フィールド）を含めることもできます。 Marketoの製品ドキュメント [ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure) にある大学コースの登録例を使用して、コース関連情報を含むエッジカスタムオブジェクトと、コースとリードを結び付けるために使用される登録ブリッジオブジェクトを作成します。 手順は次の通りです。

1. **コース** エッジオブジェクトの作成
1. にフィールドを追加 **コース :** コース ID **で重複排除**
1. 承認 **コース**
1. **登録** ブリッジオブジェクトの作成
1. **登録：** のフィールドを **登録 ID** に重複排除、**コース**&#x200B;**/コース ID**&#x200B;フィールドにリンク、**リード**&#x200B;**/リード ID**&#x200B;にリンクを追加
1. 承認 **登録**

まず、コース固有の情報を含むエッジオブジェクトタイプを作成します。

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

次に、エッジオブジェクトタイプにカスタムフィールドを追加します。  この例では、次の 4 つのカスタムフィールドを追加して、カレッジのコースをモデル化します（コース ID、コースインストラクター、コースの場所、コース名）。  少なくとも 1 つの重複排除フィールドが必要なので、コース ID を重複排除フィールドとして指定しています。

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

次に、ブリッジ オブジェクト タイプにリンクするときに後で参照できるように、エッジ オブジェクト タイプを承認する必要があります。  リンクオブジェクトとして選択できるようにするには、カスタムオブジェクトタイプを承認する必要があります。

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

エッジ オブジェクトが完成しました。  次に、登録固有の情報を含むブリッジ オブジェクト タイプを作成します。

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

カスタムフィールドをブリッジオブジェクトタイプに追加するには、2 つのリンクフィールドを追加します。1 つはリードオブジェクトにリンクし、もう 1 つは先ほど作成したコースオブジェクトにリンクします。 リードオブジェクトにリンクするには、「リード ID」フィールドを使用します。 コースオブジェクトにリンクするには、「コース ID」フィールドを使用します。  次に、少なくとも 1 つの重複除外フィールドが必要なため、登録 ID の一意の ID を重複除外フィールドとして追加します。 最後に、成績フィールドを追加して、生徒の成績を追跡します。

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

最後に、ブリッジ オブジェクトを承認します。

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

[ カスタムオブジェクトを同期 ](#create_and_update) または [ カスタムオブジェクトの一括読み込み ](https://experienceleague.adobe.com/docs/marketo-developer/marketo/rest/bulk-import/bulk-custom-object-import.html?lang=ja) を使用して、カスタムオブジェクトレコードをプログラムで入力できます。 または、Marketo UI 機能 [ カスタムオブジェクトデータを読み込む ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/import-custom-object-data) を使用できます。

## フィールドを更新

[ カスタムオブジェクトタイプフィールドを更新 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/updateCustomObjectTypeFieldUsingPOST) エンドポイントを使用すると、ドラフトカスタムオブジェクトのフィールドを更新できます。  必須のパスパラメーター `apiName` は、カスタムオブジェクトタイプの API 名です。  必須パスパラメーター `fieldAPIName` は、カスタムオブジェクトタイプフィールドの API 名です。  リクエスト本文には、更新するフィールド属性を指定するキーと値のペアを含む JSON オブジェクトが含まれています。

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

## フィールドを削除

[ カスタムオブジェクトタイプフィールドを削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectTypeFieldsUsingPOST) エンドポイントを使用すると、カスタムオブジェクトから 1 つ以上のフィールドを削除できます。  必須のパスパラメーター `apiName` は、カスタムオブジェクトタイプの API 名です。  リクエスト本文には、1 つ以上の要素を持つ `input` 配列を持つ JSON オブジェクトが含まれます。  各要素は、削除するフィールドの API 名を指定する `name` 属性を持つ JSON オブジェクトです。

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

## リストフィールドのデータタイプ

[ カスタムオブジェクトタイプフィールドのデータタイプを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET) エンドポイントは、許可されるすべてのフィールドデータタイプのリストを返します。 これは、カスタムオブジェクトタイプをモデリングして、サポートされているカスタムフィールドデータタイプを識別する際に役立ちます。

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

[ カスタムオブジェクトのリンク可能なオブジェクトを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET) エンドポイントは、許可されるすべてのリンクオブジェクトとそのリンクフィールドのリストを返します。  このリストには、標準オブジェクト （リード、会社）と、インスタンスで作成されたカスタムオブジェクトが含まれます。

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

## カスタムオブジェクト依存Assetsを取得

[ カスタムオブジェクト依存のAssetsを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeDependentAssetsUsingGET) エンドポイントは、カスタムオブジェクトタイプの依存アセットのリストを、インスタンス内の場所を含めて返します。  これは、統合を削除し、カスタムオブジェクトタイプが使用されているすべての場所を識別する必要がある場合に役立ちます。

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

* 以下に示さない限り、カスタムオブジェクトのエンドポイントのタイムアウトは 30 秒になります
   * カスタム オブジェクトの同期：120 秒 
   * カスタム オブジェクトの削除：60 秒
