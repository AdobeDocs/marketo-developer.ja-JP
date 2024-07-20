---
title: カスタムオブジェクトの一括抽出
feature: REST API, Custom Objects
description: カスタム Marketo オブジェクトのバッチ処理。
exl-id: 86cf02b0-90a3-4ec6-8abd-b4423cdd94eb
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 1%

---

# カスタムオブジェクトの一括抽出

[ カスタムオブジェクト抽出エンドポイントの一括参照 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects)

REST API の一括カスタムオブジェクト抽出セットは、Marketoから大きなカスタムオブジェクトレコードセットを取得するためのプログラムによるインターフェイスを提供します。 ETL、データウェアハウスおよびアーカイブの目的で、Marketoと 1 つ以上の外部システムとの間でデータを継続的にやり取りする必要があるユースケースでは、このインターフェイスをお勧めします。

この API は、リードに直接リンクされた第 1 レベルのMarketo カスタムオブジェクトレコードの書き出しをサポートします。 カスタムオブジェクトの名前と、オブジェクトのリンク先となるリードのリストを渡します。 リストのリードごとに、指定したカスタムオブジェクト名に一致するリンクされたカスタムオブジェクトレコードが行としてエクスポートファイルに書き込まれます。 カスタムオブジェクトデータは、[Marketo UI のリードの詳細ページの「カスタムオブジェクト」タブ ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/understanding-marketo-custom-objects) で表示できます。

## 権限

一括カスタムオブジェクト抽出 API では、API ユーザーが「読み取り専用カスタムオブジェクト」または「読み取り/書き込みカスタムオブジェクト」の権限の一方または両方の役割を持っている必要があります。

## フィルター

カスタムオブジェクト抽出は、カスタムオブジェクトにリンクされたリードのリストを指定するために使用される、複数のフィルターオプションをサポートしています。 リスト内のリードが特定のカスタムオブジェクト名に一致するカスタムオブジェクトレコードにリンクされている場合、レコードはエクスポートファイルに書き込まれます。 エクスポートジョブごとに指定できるフィルタータイプは 1 つだけです。

| フィルタータイプ | データタイプ | 注意 |
|---|---|---|
| `updatedAt` | 日付範囲 | メンバーが `startAt` および&amp;nbsp の JSON オブジェクト `endAt` 受け入れます。;`startAt` にはローウォーターマークを表す日時、`endAt` にはハイウォーターマークを表す日時を指定できます。 範囲は 31 日以内にする必要があります。 このフィルタータイプを持つジョブは、日付範囲内に更新されたすべてのアクセス可能なレコードを返します。 日時は、ミリ秒なしの ISO-8601 形式である必要があります。 |
| `staticListName` | 文字列 | 静的リストの名前を受け入れます。 このフィルタータイプを持つジョブは、ジョブの処理開始時に静的リストのメンバーであるすべてのアクセス可能なレコードを返します。 Get Lists エンドポイントを使用して静的リスト名を取得します。 |
| `staticListId` | 整数 | 静的リストの ID を受け入れます。 このフィルタータイプを持つジョブは、ジョブの処理開始時に静的リストのメンバーであるすべてのアクセス可能なレコードを返します。 リストの取得エンドポイントを使用して、静的リスト ID を取得します。 |
| `smartListName`* | 文字列 | スマートリストの名前を受け入れます。 このフィルタ・タイプを持つジョブは、ジョブの処理開始時にスマート・リストのメンバーであるアクセス可能なすべてのレコードを返します。 「スマート・リストの取得」エンドポイントを使用してスマート・リスト名を取得します。 |
| `smartListId`* | 整数 | スマートリストの ID を受け入れます。 このフィルタ・タイプを持つジョブは、ジョブの処理開始時にスマート・リストのメンバーであるアクセス可能なすべてのレコードを返します。 「スマート・リストの取得」エンドポイントを使用してスマート・リスト ID を取得します。 |

一部のサブスクリプションでは、フィルタータイプを使用できません。 サブスクリプションで利用できない場合は、リードの書き出しジョブを作成エンドポイントを呼び出すとエラーが発生します（「1035, ターゲットのサブスクリプションでサポートされていないフィルタータイプ」）。 お客様は、Marketo サポートに連絡して、この機能をサブスクリプションで有効にすることができます。

## オプション

[ カスタムオブジェクトの書き出しを作成ジョブ ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/createExportCustomObjectsUsingPOST) エンドポイントには、複数の書式設定オプションが用意されています。 これらのオプションを使用すると、ユーザーは次のことができます。

- 書き出されたファイルに含めるフィールドを指定
- これらのフィールドの列ヘッダーの名前を変更
- 書き出すファイルの形式を指定

| パラメーター | データタイプ | 必須 | 注意 |
|---|---|---|---|
| `fields` | 配列 [ 文字列 ] | はい | Describe Custom Object エンドポイントによって返されるカスタムオブジェクト属性名の値を含む文字列の配列。 リストされたフィールドは、書き出されたファイルに含まれます。 |
| `columnHeaderNames` | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。 キーは、エクスポートジョブに含まれるフィールドの名前である必要があります。 値は、そのフィールドの書き出された列ヘッダーの名前です。 |
| `format` | 文字列 | いいえ | CSV、TSV、SSV のいずれかを使用できます。 書き出されたファイルは、コンマ区切り値、タブ区切り値、スペース区切り値の各ファイル（設定されている場合）としてレンダリングされます。 未設定の場合のデフォルト値は CSV です。 |


## ジョブの作成

ジョブのパラメーターは、[ 書き出しカスタムオブジェクトジョブを作成 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/createExportCustomObjectsUsingPOST) エンドポイントを使用して書き出しを開始する前に定義されます。

必須の `apiName` パスパラメーターは、[ カスタムオブジェクトを記述 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1) エンドポイントによって返されるカスタムオブジェクト名です。 書き出すMarketo カスタムオブジェクトを指定します。 CRM カスタムオブジェクトは許可されていません。 必須の `filter` パラメーターには、カスタムオブジェクトにリンクされているリードのリストが含まれています。 これは、静的リストまたはスマートリストを参照できます。 必須の `fields` パラメーターには、書き出しファイルに含めるカスタムオブジェクト属性の API 名が含まれています。 オプションで、ファイルの `format` と `columnHeaderNames` を定義できます。

例えば、「Color」、「Make」、「Model」、「VIN」のフィールドを持つ「Car」というカスタムオブジェクトを作成したとします。 リンクフィールドはリード ID で、重複排除フィールドは VIN です。

カスタムオブジェクト定義

![ カスタム オブジェクト ](assets/custom-object-car.png)


カスタムオブジェクトフィールド

![ カスタムオブジェクトフィールド ](assets/custom-object-car-fields.png)

[ カスタムオブジェクトを記述 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1) を呼び出して、応答の `fields` 属性に表示されるカスタムオブジェクト属性をプログラムで調べることができます。

```
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

複数のカスタムオブジェクトレコードを作成し、[ カスタムオブジェクトを同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) エンドポイントを使用してそれぞれを別のリードにリンクします。 1 つのリードを複数のカスタムオブジェクトレコードにリンクすることができます。 これは、「1 対多」関係と呼ばれます。

```
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

上記の 3 つのリードはそれぞれ、「リスト ID でリードを取得 [ エンドポイントを呼び出すことで示されるように、`id` が 1081 である「自動車バイヤー」という名前の静的リストに属し ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/getLeadsByListIdUsingGET_1) す。

```
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

次に、これらのレコードを取得するエクスポートジョブを作成します。 [ 書き出しカスタムオブジェクトジョブを作成 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/createExportCustomObjectsUsingPOST) エンドポイントを使用して、カスタムオブジェクト属性を `fields` パラメーターで、静的リスト ID を `filter` パラメーターで指定します。

```
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

これは、ジョブが作成されたことを示すステータスを応答で返します。 ジョブは定義され作成されましたが、まだ開始されていません。 これを行うには、`apiName` と、作成ステータス応答の `exportId` を使用して、[ カスタムオブジェクトジョブのエンキュー ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/enqueueExportCustomObjectsUsingPOST) エンドポイントを呼び出す必要があります。

```
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

これにより、使用可能な書き出しスロットがある場合、初期 `status` は「待機中」になり、「処理中」に設定されます。

## ジョブステータスのポーリング

ステータスは、同じ API ユーザーによって作成されたジョブについてのみ取得できます。

これは非同期エンドポイントなので、ジョブを作成した後、そのステータスをポーリングして、進行状況を判断する必要があります。 [ カスタム オブジェクト ジョブの状態のエクスポートの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/getExportCustomObjectsStatusUsingGET) エンドポイントを使用してポーリングします。 ステータスは 60 秒に 1 回だけ更新されるので、これよりも低いポーリング頻度は推奨されず、ほとんどすべての場合で過剰です。 ステータスフィールドの応答は、作成済み、待機中、処理中、キャンセル済み、完了または失敗のいずれかです。

```
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

ステータスエンドポイントは、ジョブがまだ処理中であることを示す応答なので、ファイルはまだ取得できません。 ジョブ `status` が「完了」に変わると、ダウンロードできるようになります。

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

完了したカスタムオブジェクト書き出しのファイルを取得するには、`apiName` と `exportId` を指定して [ 書き出しカスタムオブジェクトファイルを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/getExportCustomObjectsFileUsingGET) エンドポイントを呼び出すだけです。

応答には、ジョブの設定方法に従ってフォーマットされたファイルが含まれています。 エンドポイントは、ファイルのコンテンツを使用して応答します。 リクエストされたカスタムオブジェクト属性が空（データが含まれていない）の場合、`null` はエクスポートファイルの対応するフィールドに配置されます。

```
GET /bulk/v1/customobjects/car_c/export/f2c03f1d-226f-47c1-a557-357af8c2b32a/file.json
```

```csv
leadId,color,make,model,vIN
11,Pearl White,Tesla,Model S,5YJSA1E41FF156789
12,Midnight Silver Metallic,Tesla,Model X,LRWXB2B41FF198765
13,Fusion Red,Tesla,Roadster,SFGRC3C41FF154321
```

抽出されたデータの部分的で再開にわかりやすい取得をサポートするために、ファイルエンドポイントはオプションでバイト型の HTTP ヘッダー範囲をサポートします。 ヘッダーが設定されていない場合は、コンテンツ全体が返されます。 範囲ヘッダーの使用について詳しくは、Marketo[ 一括抽出 ](bulk-extract.md) を参照してください。

## ジョブのキャンセル

ジョブが誤って設定された場合、または不要になった場合は、[ カスタムオブジェクトジョブの書き出しをキャンセル ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/getExportCustomObjectsFileUsingPOST) エンドポイントを使用すると、簡単にキャンセルできます。 ジョブがキャンセルされたことを示す `status` が返されます。

```
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
