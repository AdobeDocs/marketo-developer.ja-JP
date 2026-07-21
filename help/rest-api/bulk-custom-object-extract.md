---
title: カスタムオブジェクトの一括抽出
feature: REST API, Custom Objects
description: Marketo Bulk カスタムオブジェクトのガイド UpdateAtおよびリストフィルター、選択したフィールドおよびリードリンクされたカスタムオブジェクトを書き出すためのREST APIを抽出します…
exl-id: 86cf02b0-90a3-4ec6-8abd-b4423cdd94eb
TQID: https://experienceleague.adobe.com/KAT-vab2uZq8FrRbZLy30PCJNfq01znDDuSSWuIu7WE
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1231
ht-degree: 31%

---

# カスタムオブジェクトの一括抽出

[一括カスタムオブジェクト抽出エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Custom-Objects)

Bulk Custom Object Extract REST APIは、Marketoから大規模なカスタムオブジェクトレコードのセットを取得します。 これらのAPIを使用すると、Marketoと外部システム、ETL、データウェアハウス、アーカイブ間で継続的にデータをやり取りできます。

このAPIは、リードに直接リンクされたファーストレベルのMarketo カスタムオブジェクトレコードを書き出します。 カスタムオブジェクト名とリンクされたリードのリストを指定します。 各リードについて、APIは一致するリンクされたカスタムオブジェクトレコードをエクスポートファイルの行として書き込みます。

カスタムオブジェクトデータは、Marketo UI[&#128279;](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/understanding-marketo-custom-objects)のリードの詳細ページの「 カスタムオブジェクト」タブで確認できます。

## 権限

API ユーザーには、読み取り専用カスタムオブジェクト権限、読み取り/書き込みカスタムオブジェクト権限、またはその両方を持つ役割が必要です。

## フィルター

カスタムオブジェクト抽出フィルターは、カスタムオブジェクトにリンクされたリードのリストを指定します。 リストされたリードが指定されたカスタムオブジェクト名に一致するレコードにリンクされている場合、APIはそれらのレコードをエクスポートファイルに書き込みます。

書き出しジョブごとに1つのフィルタータイプのみを指定します。

| フィルタータイプ | データタイプ | メモ |
| --- | --- | --- |
| `updatedAt` | 日付範囲 | メンバー`startAt`および`endAt` &amp;nbspを含むJSON オブジェクトを受け入れます。;`startAt`は低い透かしを表す日時を受け入れ、`endAt`は高い透かしを表す日時を受け入れます。 範囲は 31日以内にする必要があります。 このフィルタータイプのジョブは、日付範囲内で更新されたアクセス可能なすべてのレコードを返します。 日時形式は、ミリ秒を含まない ISO-8601 形式にする必要があります。 |
| `staticListName` | 文字列 | 静的リストの名前を受け取ります。 このフィルタータイプのジョブは、ジョブの処理開始時点で静的リストのメンバーであるアクセス可能なすべてのレコードを返します。 「リストを取得」エンドポイントを使用して静的リスト名を取得します。 |
| `staticListId` | 整数 | 静的リストの ID を受け取ります。 このフィルタータイプのジョブは、ジョブの処理開始時点で静的リストのメンバーであるアクセス可能なすべてのレコードを返します。 「リストを取得」エンドポイントを使用して静的リスト ID を取得します。 |
| `smartListName`* | 文字列 | スマートリストの名前を受け取ります。 このフィルタータイプのジョブは、ジョブの処理開始時点でスマートリストのメンバーであるアクセス可能なすべてのレコードを返します。 「スマートリストを取得」エンドポイントを使用してスマートリスト名を取得します。 |
| `smartListId`* | 整数 | スマートリストの ID を受け取ります。 このフィルタータイプのジョブは、ジョブの処理開始時点でスマートリストのメンバーであるアクセス可能なすべてのレコードを返します。 「スマートリストを取得」エンドポイントを使用してスマートリスト ID を取得します。 |

一部のサブスクリプションはこのフィルタータイプをサポートしていません。 使用できない場合は、「リードジョブを書き出し作成」エンドポイントは`1035, Unsupported filter type for target subscription`を返します。 Marketo サポートに連絡して、サブスクリプションにこの機能をリクエストしてください。

## オプション

[&#x200B; カスタムオブジェクトの書き出し作成ジョブ &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Custom-Objects/operation/createExportCustomObjectsUsingPOST) エンドポイントには、次のオプションがあります。

- 書き出しファイルに含めるフィールドを指定します。
- 書き出した列ヘッダーの名前を変更します。
- 書き出しファイル形式を指定します。

| パラメーター | データタイプ | 必須 | メモ |
| --- | --- | --- | --- |
| `fields` | 配列[文字列] | はい | 「カスタムオブジェクトを説明」エンドポイントによって返されるカスタムオブジェクト属性名の値を含む文字列の配列。 リストされたフィールドは、書き出されたファイルに含まれます。 |
| `columnHeaderNames` | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。 キーは、書き出しジョブに含まれるフィールドの名前にする必要があります。 値は、このフィールドの書き出された列ヘッダーの名前です。 |
| `format` | 文字列 | いいえ | CSV、TSV、SSV のいずれかを受け入れます。 書き出されたファイルは、設定した場合、それぞれコンマ区切り値、タブ区切り値、またはスペース区切り値のファイルとしてレンダリングされます。 未設定の場合は、デフォルトで CSV に設定されます。 |

## ジョブの作成

[&#x200B; カスタムオブジェクトジョブの作成](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Custom-Objects/operation/createExportCustomObjectsUsingPOST) エンドポイントを使用して、書き出しジョブを定義します。

リクエストでは、次のパラメーターを使用します。

- `apiName`：必須のパス パラメーター。 [&#x200B; カスタムオブジェクトの説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/describeUsingGET_1) エンドポイントから返された名前を使用して、書き出すMarketo カスタムオブジェクトを指定します。 CRM カスタムオブジェクトは許可されていません。
- `filter`：必須。 静的リストまたはスマートリストを参照して、リンクされたリードを指定します。
- `fields`：必須。 書き出しファイルに含めるカスタムオブジェクト属性のAPI名を指定します。
- `format`：オプション。 書き出しファイル形式を指定します。
- `columnHeaderNames`：オプション。 置換する列ヘッダー名を指定します。

この例では、`Color`、`Make`、`Model`、`VIN`のフィールドを持つ`Car` カスタムオブジェクトを使用しています。 リンクフィールドはリード ID で、重複排除フィールドは VIN です。

カスタムオブジェクトの定義

![カスタムオブジェクト](assets/custom-object-car.png)

カスタムオブジェクトフィールド

![カスタムオブジェクトフィールド](assets/custom-object-car-fields.png)

カスタムオブジェクトを記述[呼び出して](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/describeUsingGET_1) カスタムオブジェクト属性をプログラムで調べます。 応答は`fields`の属性を返します。

```http
GET /rest/v1/customobjects/car_c/describe.json
```

```json
{
    "requestId": "148ef#1793e00f64f",
    "result": [
        {
            "name": "car_c",
            "displayName": "Car",
            "description": "It's a car.",
            "createdAt": "2021-05-05T16:14:41Z",
            "updatedAt": "2021-05-05T16:14:42Z",
            "idField": "marketoGUID",
            "dedupeFields": [
                "vIN"
            ],
            "searchableFields": [
                [
                    "vIN"
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
                        "field": "Id"
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
                    "name": "color",
                    "displayName": "Color",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
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
                    "name": "vIN",
                    "displayName": "VIN",
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

カスタムオブジェクトレコードを作成し、各レコードをリードにリンクするには、[&#x200B; カスタムオブジェクトの同期](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) エンドポイントを使用します。 1つのリードを複数のカスタムオブジェクトレコードにリンクして、1対多の関係を作成できます。

```http
POST /rest/v1/customobjects/car_c.json
```

```json
{
   "action":"createOrUpdate",
   "input":[
       {
           "leadId": 11,
           "color": "Pearl White",
           "make": "Tesla",
           "model": "Model S",
           "vIN": "5YJSA1E41FF156789"
       },
       {
           "leadId": 12,
           "color": "Midnight Silver Metallic",
           "make": "Tesla",
           "model": "Model X",
           "vIN": "LRWXB2B41FF198765"
       },
       {
           "leadId": 13,
           "color": "Fusion Red",
           "make": "Tesla",
           "model": "Roadster",
           "vIN": "SFGRC3C41FF154321"
       }
    ]
}
```

```json
{
    "requestId": "50d9#1793e066088",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "d911eaa1-fd0b-4a99-9b71-c6a7233c782c",
            "status": "created"
        },
        {
            "seq": 1,
            "marketoGUID": "20d04ffb-51f0-4336-924c-c783b9bb4215",
            "status": "created"
        },
        {
            "seq": 2,
            "marketoGUID": "e7da4331-8e7a-473b-85c8-047638eb6c7f",
            "status": "created"
        }
    ],
    "success": true
}
```

この例の3つのリードは、`Car Buyers`の静的リストに属しており、1081の`id`があります。 リスト ID [&#128279;](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/getLeadsByListIdUsingGET_1) エンドポイントでGet リードを呼び出して、リスト メンバーを取得します。

```http
GET /rest/v1/lists/1081/leads.json
```

```json
{
    "requestId": "d023#1793e1e982b",
    "result": [
        {
            "id": 11,
            "firstName": "Hanna",
            "lastName": "Crawford",
            "email": "208161Hanna.Crawford@pookmail.com",
            "updatedAt": "2020-01-16T02:38:22Z",
            "createdAt": "2017-07-27T01:38:42Z"
        },
        {
            "id": 12,
            "firstName": "Bertha",
            "lastName": "Fulton",
            "email": "208160Bertha.Fulton@trashymail.com",
            "updatedAt": "2020-01-16T02:38:22Z",
            "createdAt": "2017-07-27T01:38:42Z"
        },
        {
            "id": 13,
            "firstName": "Faith",
            "lastName": "England",
            "email": "208159Faith.England@dodgit.com",
            "updatedAt": "2020-01-16T02:38:22Z",
            "createdAt": "2017-07-27T01:38:42Z"
        }
    ],
    "success": true
}
```

これらのレコードを取得するには、[&#x200B; カスタムオブジェクトジョブの作成](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Custom-Objects/operation/createExportCustomObjectsUsingPOST) エンドポイントを呼び出します。 `fields`のカスタムオブジェクト属性と`filter`の静的リスト IDを指定します。

```http
POST /bulk/v1/customobjects/car_c/export/create.json
```

```json
{
    "fields": [
        "leadId",
        "color",
        "make",
        "model",
        "vIN"
    ],
    "filter": {
        "staticListId": 1081
    }
}
```

```json
{
    "requestId": "8d2f#1793e289e87",
    "result": [
        {
            "exportId": "f2c03f1d-226f-47c1-a557-357af8c2b32a",
            "format": "CSV",
            "status": "Created",
            "createdAt": "2021-05-05T20:12:01Z"
        }
    ],
    "success": true
}
```

応答は、ジョブが作成されたことを確認しますが、書き出しは自動的に開始されません。 `apiName`と返された`exportId`を[Enqueue カスタムオブジェクト書き出しジョブ &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Custom-Objects/operation/enqueueExportCustomObjectsUsingPOST) エンドポイントに渡して、ジョブを開始します。

```http
POST /bulk/v1/customobjects/car_c/export/f2c03f1d-226f-47c1-a557-357af8c2b32a/enqueue.json
```

```json
{
    "requestId": "cfaf#1793e2a0762",
    "result": [
        {
            "exportId": "f2c03f1d-226f-47c1-a557-357af8c2b32a",
            "format": "CSV",
            "status": "Queued",
            "createdAt": "2021-05-05T20:12:01Z",
            "queuedAt": "2021-05-05T20:13:32Z"
        }
    ],
    "success": true
}
```

エンキュー応答は、最初に`Queued` ステータスを返します。 書き出しスロットが使用可能になると、ステータスが`Processing`に変わります。

## ジョブステータスのポーリング

同じAPI ユーザーが作成したジョブに対してのみ、ステータスを取得できます。

書き出しは非同期で実行されるので、[&#x200B; カスタムオブジェクトジョブステータスの書き出しを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Custom-Objects/operation/getExportCustomObjectsStatusUsingGET) エンドポイントを使用して、進行状況を調査します。 ステータスは60秒ごとに1回しか更新されないので、より頻繁にポーリングしないでください。

ステータスは`Created`、`Queued`、`Processing`、`Canceled`、`Completed`または`Failed`です。

```http
GET /bulk/v1/customobjects/{apiName}/export/{exportId}/status.json
```

```json
{
    "requestId": "14daa#1793e2cf9de",
    "result": [
        {
            "exportId": "f2c03f1d-226f-47c1-a557-357af8c2b32a",
            "format": "CSV",
            "status": "Processing",
            "createdAt": "2021-05-05T20:12:01Z",
            "queuedAt": "2021-05-05T20:13:32Z",
            "startedAt": "2021-05-05T20:14:15Z"
        }
    ],
    "success": true
}
```

この応答は、ジョブがまだ処理中であるため、ファイルが利用できないことを示します。 ジョブのステータスが`Completed`に変更されると、ファイルをダウンロードする準備が整います。

```json
{
    "requestId": "14daa#1793e2cf9de",
    "result": [
        {
            "exportId": "f2c03f1d-226f-47c1-a557-357af8c2b32a",
            "format": "CSV",
            "status": "Completed",
            "createdAt": "2021-05-05T20:12:01Z",
            "queuedAt": "2021-05-05T20:13:32Z",
            "startedAt": "2021-05-05T20:14:15Z",
            "finishedAt": "2021-05-05T20:14:28Z",
            "numberOfRecords": 3,
            "fileSize": 182,
            "fileChecksum": "sha256:fac0cabc2352229c12e18b2fde03d1f24178bc71e9e926f520ae8d61bbe98c01"
        }
    ],
    "success": true
}
```

## データの取得

完了したカスタムオブジェクトの書き出しを取得するには、`apiName`と`exportId`を[&#x200B; カスタムオブジェクトファイルの書き出しの取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Custom-Objects/operation/getExportCustomObjectsFileUsingGET) エンドポイントに渡します。

エンドポイントは、ジョブ用に設定された形式でファイルを返します。 要求されたカスタムオブジェクト属性にデータが含まれていない場合、対応する書き出しフィールドには`null`が含まれます。

```http
GET /bulk/v1/customobjects/car_c/export/f2c03f1d-226f-47c1-a557-357af8c2b32a/file.json
```

```csv
leadId,color,make,model,vIN
11,Pearl White,Tesla,Model S,5YJSA1E41FF156789
12,Midnight Silver Metallic,Tesla,Model X,LRWXB2B41FF198765
13,Fusion Red,Tesla,Roadster,SFGRC3C41FF154321
```

部分的または再開可能な取得の場合、ファイルエンドポイントは、範囲タイプが`bytes`のオプションのHTTP `Range` ヘッダーをサポートします。 ヘッダーを設定しない場合、エンドポイントはファイル全体を返します。 詳しくは、[一括抽出](bulk-extract.md)を参照してください。

## ジョブのキャンセル

正しく設定されていないか、不要になったジョブをキャンセルするには、[&#x200B; カスタムオブジェクトジョブの書き出しをキャンセル &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Custom-Objects/operation/getExportCustomObjectsFileUsingPOST) エンドポイントを呼び出します。 応答ステータスは、ジョブがキャンセルされたことを示します。

```http
POST /bulk/v1/customobjects/car_c/export/f2c03f1d-226f-47c1-a557-357af8c2b32a/cancel.json
```

```json
{
    "requestId": "e5f9#179391286a7",
    "result": [
        {
            "exportId": "4a8cdd80-0d16-4dd6-9923-6ec97e30e91b",
            "format": "CSV",
            "status": "Cancelled",
            "createdAt": "2021-05-04T20:24:33Z"
        }
    ],
    "success": true
}
```
