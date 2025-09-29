---
title: カスタムオブジェクトの一括読み込み
feature: Custom Objects
description: CSV、TSV、SSV の各ファイルを使用し、REST 経由でMarketoのカスタムオブジェクトを一括読み込みする方法について説明します。
exl-id: e795476c-14bc-4e8c-b611-1f0941a65825
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 98%

---

# カスタムオブジェクトの一括読み込み

[カスタムオブジェクトの一括読み込みエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects)

読み込むカスタムオブジェクトレコードが多数ある場合は、一括 API を使用して非同期的に読み込むのがベストプラクティスです。これを実行するには、（コンマ、タブ、またはセミコロンで）区切られたレコードを含むフラットファイルを読み込みます。ファイルのサイズが 10 MB 未満であれば、任意の数のレコードを含めることができます（それ以外の場合は、HTTP 413 ステータスコードが返されます）。ファイルのコンテンツは、カスタムオブジェクトの定義によって異なります。最初の行には常に、各行の値をマッピングするフィールドをリストするヘッダーが含まれます。ヘッダー内のすべてのフィールド名は、API 名と一致する必要があります（以下で説明）。残りの行には、読み込むデータが行ごとに 1 つのレコードとして含まれます。レコード操作は、「挿入または更新」のみです。

## 処理制限

制限付きで、複数の一括読み込みリクエストを送信できます。各リクエストは、ジョブとして FIFO キューに追加され、処理されます。最大 2 つのジョブが同時に処理されます。任意の時点でキューに入れることができるジョブの数は最大 10 個です（現在処理中の 2 個を含む）。ジョブの最大数が 10 を超えると、「1016、読み込みが多すぎます」というエラーが返されます。

## カスタムオブジェクトの例

一括 API を使用する前に、最初に Marketo Admin UI を使用して[カスタムオブジェクトを作成](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects)する必要があります。例えば、&quot;Car&quot; カスタムオブジェクトを作成し、&quot;Color&quot;、&quot;Make&quot;、&quot;Model&quot;、および &quot;VIN&quot; フィールドをそこに含めるとします。カスタムオブジェクトを表示する管理 UI 画面を以下に示します。重複排除に VIN フィールドを使用したことが分かります。API 名は、一括 API 関連のエンドポイントを呼び出す際に使用する必要があるので、ハイライト表示されています。

![カスタムオブジェクトを挿入](assets/bulk-insert-co-car-1.png)

管理 UI に表示されるカスタムオブジェクトフィールドを以下に示します。

![カスタムオブジェクトフィールドを挿入](assets/bulk-insert-co-car-fields.png)

### API 名

カスタム オブジェクトの API 名を[カスタムオブジェクトを説明](#describe)エンドポイントに渡すことで、プログラムで API 名を取得できます。

```
/rest/v1/customobjects/{apiName}/describe.json
```

```json
{
    "requestId": "46ff#15a686e66de",
    "result": [
        {
            "name": "car_c",
            "displayName": "Car",
            "description": "It's a car.",
            "createdAt": "2017-02-22T19:55:51Z",
            "updatedAt": "2017-02-22T19:55:51Z",
            "idField": "marketoGUID",
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
            "fields": [
                {
                    "name": "createdAt",
                    "displayName": "Created At",
                    "dataType": "datetime",
                    "updateable": false
                },
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "Updated At",
                    "dataType": "datetime",
                    "updateable": false
                },
                {
                    "name": "color",
                    "displayName": "Color",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true
                },
                {
                    "name": "make",
                    "displayName": "Make",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true
                },
                {
                    "name": "model",
                    "displayName": "Model",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true
                },
                {
                    "name": "vin",
                    "displayName": "VIN",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true
                }
            ]
        }
    ],
    "success": true
}
```

### ファイルの読み込み

次に、3 つの &quot;Car&quot; カスタムオブジェクトレコードを読み込むとします。コンマ区切り形式（CSV）を使用した場合、ファイルは次のようになります。

```
color,make,model,vin
red,bmw,2002,WBA4R7C55HK895912
yellow,bmw,320i,WBA4R7C30HK896061
blue,bmw,325i,WBS3U9C52HP970604
```

行 1 はヘッダー、行 2～4 はカスタムオブジェクトデータレコードです。

## ジョブの作成

一括読み込みリクエストを行うには、[カスタムオブジェクトを読み込み](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Identity/operation/identityUsingPOST)エンドポイントへのパスにカスタムオブジェクトの API 名を含める必要があります。また、読み込みファイルの名前を参照する &quot;file&quot; パラメーターと、読み込み ファイルの区切り方法（「csv」、「tsv」または「ssv」）を指定する &quot;format&quot; パラメーターも含める必要があります。

```
POST /bulk/v1/customobjects/{apiName}/import.json?format=csv
```

```
Transfer-Encoding: chunked
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryXjWP6BP8Ciq6bPeo
Content-Length: 290
Host: <munchkinId>.mktorest.com
```

```
------WebKitFormBoundaryXjWP6BP8Ciq6bPeo
Content-Disposition: form-data; name="file"; filename="custom_object_import.csv"
Content-Type: text/csv

color,make,model,vin
red,bmw,2002,WBA4R7C55HK895912
yellow,bmw,320i,WBA4R7C30HK896061
blue,bmw,325i,WBS3U9C52HP970604
------WebKitFormBoundaryXjWP6BP8Ciq6bPeo--
```

```json
{
    "requestId": "c015#15a68a23418",
    "result": [
        {
            "batchId": 1013,
            "status": "Queued",
            "objectApiName": "car_c"
        }
    ],
    "success": true
}
```

この例では、「csv」形式を指定し、読み込みファイルに「custom_object_import.csv」という名前を付けました。

呼び出しに対する応答では、「カスタムオブジェクトを同期」エンドポイントから返されるような成功または失敗のリストは表示されません。代わりに、`batchId` を受信します。これは、呼び出しが非同期で行われ、`status` として &quot;Queued&quot;、&quot;Importing&quot;、または &quot;Failed&quot; が返される可能性があるからです。読み込みジョブのステータスを取得したり、完了時に失敗や警告を取得したりできるように、batchId を保持する必要があります。batchId は 7 日間有効です。

一括読み込みリクエストを複製する簡単な方法は、コマンドラインから curl を使用することです。

```
curl -X POST -i -F format='csv' -F file='@custom_object_import.csv' -F access_token='<Access Token>' <REST API Endpoint URL>/bulk/v1/customobjects/car_c/import.json
```

読み込みファイル「custom_object_import.csv」には次の内容が含まれます。

```
color,make,model,vin
red,bmw,2002,WBA4R7C55HK895912
yellow,bmw,320i,WBA4R7C30HK896061
blue,bmw,325i,WBS3U9C52HP970604
```

## ジョブステータスのポーリング

読み込みジョブを作成したら、このステータスのクエリを実行する必要があります。インポートジョブを 5～30 秒ごとにポーリングするのがベストプラクティスです。これを行うには、カスタムオブジェクトの API 名とパス内の `batchId` を[カスタムオブジェクトを読み込みステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectStatusUsingGET)エンドポイントに渡します。

```
GET /bulk/v1/customobjects/{apiName}/import/{batchId}/status.json
```

```json
{
    "requestId": "2a5#15a68dd9be1",
    "result": [
        {
            "batchId": 1013,
            "operation": "import",
            "status": "Complete",
            "objectApiName": "car_c",
            "numOfObjectsProcessed": 3,
            "numOfRowsFailed": 0,
            "numOfRowsWithWarning": 0,
            "importTime": "2 second(s)",
            "message": "Import succeeded, 3 records imported (3 members)"
        }
    ],
    "success": true
}
```

この応答は、完了した読み込みを示しますが、`status` は完了、キュー済み、読み込み中、失敗のいずれかになります。ジョブが完了したら、処理された行数、失敗した行数、警告のあった行数のリストが表示されます。また、メッセージ属性は、追加のジョブ情報を探すのにも適しています。

## 失敗

失敗は、[カスタムオブジェクトを読み込みステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectStatusUsingGET)応答の `numOfRowsFailed` 属性によって示されます。numOfRowsFailed がゼロより大きい場合、この値は発生した失敗の数を示します。失敗の詳細を含むファイルを取得するには、[カスタムオブジェクトを読み込み失敗を取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectFailuresUsingGET)エンドポイントを呼び出します。ここでも、パスにカスタムオブジェクトの API 名と `batchId` を渡す必要があります。失敗ファイルが存在しない場合は、HTTP 404 ステータスコードが返されます。

例を続けると、ヘッダーを変更して「vin」を「 vin」（コンマと「vin」の間にスペースを追加）に変更することで、強制的に失敗させることができます。

```
color,make,model, vin
```

再読み込みしてステータスを確認すると、`numRowsFailed`: 3 の応答が表示されます。これは 3 つの失敗を示します。

```
GET /bulk/v1/customobjects/car_c/import/{batchId}/status.json
```

```json
{
    "requestId": "12260#15a68f491ed",
    "result": [
        {
            "batchId": 1016,
            "operation": "import",
            "status": "Complete",
            "objectApiName": "car_c",
            "numOfObjectsProcessed": 0,
            "numOfRowsFailed": 3,
            "numOfRowsWithWarning": 0,
            "importTime": "1 second(s)",
            "message": "Import completed with errors, 0 records imported (0 members), 3 failed"
        }
    ],
    "success": true
}
```

ここで、「カスタムオブジェクトを読み込み失敗を取得」エンドポイント呼び出しを実行して、追加の失敗の詳細を取得します。

```
GET /bulk/v1/customobjects/car_c/import/{batchId}/failures.json
```

```
color,make,model, vin,Import Failure Reason
red,bmw,2002,WBA4R7C55HK895912,missing.dedupe.fields
yellow,bmw,320i,WBA4R7C30HK896061,missing.dedupe.fields
blue,bmw,325i,WBS3U9C52HP970604,missing.dedupe.fields
```

また、重複排除フィールド `vin` が欠落していることが分かります。

## 警告

警告は、「カスタムオブジェクトを読み込みステータスを取得」応答の `numOfRowsWithWarning` 属性によって示されます。numOfRowsWithWarning がゼロより大きい場合、この値は発生した警告の数を示します。警告の詳細を含むファイルを取得するには、[カスタムオブジェクトを読み込み警告を取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectWarningsUsingGET)エンドポイントを呼び出します。ここでも、パスにカスタムオブジェクトの API 名と `batchId` を渡す必要があります。警告ファイルが存在しない場合は、HTTP 404 ステータスコードが返されます。

```
GET /bulk/v1/customobjects/car_c/import/{batchId}/warnings.json
```
