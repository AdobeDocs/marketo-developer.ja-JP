---
title: 「リードの一括読み込み」
feature: REST API
description: リードデータのバッチインポート。
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---


# リードの一括読み込み

[リードの一括インポートエンドポイントのリファレンス](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads)

大量のリードレコードの場合、リードはと非同期でインポートできます [一括 API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/importLeadUsingPOST). これにより、区切り文字（コンマ、タブ、またはセミコロン）を含むフラットファイルを使用して、レコードのリストをMarketoにインポートできます。 ファイルには任意の数のレコードを含めることができます（ファイルの合計サイズが 10 MB 未満である場合）。 レコード操作は、「挿入または更新」のみです。

## 処理制限

制限を持つ複数の一括読み込みリクエストを送信できます。 各リクエストは、処理される FIFO キューにジョブとして追加されます。 最大 2 つのジョブが同時に処理されます。 任意の時点でキューに入れられるジョブの数は最大 10 個です（現在処理中の 2 個を含む）。 ジョブの最大数 10 を超えると、「1016, Too many imports」エラーが返されます。

## ファイルのインポート

ファイルの最初の行は、各行の値をマッピングするために対応する REST API フィールドをリストするヘッダーである必要があります。 一般的なファイルの形式は、次のような基本的なパターンになります。

```
email,firstName,lastName
test@example.com,John,Doe
```

この `externalCompanyId` フィールドを使用して、リードレコードを会社レコードにリンクできます。 この `externalSalesPersonId` フィールドを使用して、潜在顧客レコードを販売担当者レコードにリンクできます。

呼び出しそのものは、 `multipart/form-data` content-type。

このリクエストタイプは実装が困難な場合があるので、既存のライブラリ実装を使用することを強くお勧めします。

## ジョブの作成

一括読み込みリクエストを行うには、content-type ヘッダーを「multipart/form-data」に設定し、少なくともファイルコンテンツを含むファイルパラメーターと、ファイル形式を示す値「csv」、「tsv」、「ssv」を持つ形式パラメーターを含める必要があります。

```
POST /bulk/v1/leads.json?format=csv
```

```
Content-Type: multipart/form-data; boundary=------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Length: 311
Host: <munchkinId>.mktorest.com
```

```
------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Disposition: form-data; name="file"; filename="leads.csv"
Content-Type: text/csv

FirstName,LastName,Email,Company
Able,Baker,ablebaker@marketo.com,Marketo
Charlie,Dog,charliedog@marketo.com,Marketo
Easy,Fox,easyfox@marketo.com,Marketo
------WebKitFormBoundaryBQACkJZyaiIAXogC--
```

```json
{
    "requestId": "d01f#15d672f8560",
    "result": [
        {
            "batchId": 3404,
            "importId": "3404",
            "status": "Queued"
        }
    ],
    "success": true
}
```

このエンドポイントはを使用します [content-type として multipart/form-data](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html). 正しく設定するまでには時間がかかるので、ベストプラクティスは HTTP サポートライブラリを使用して目的の言語を選択することです。 コマンドラインから cURL を使用してこれを行う簡単な方法は、次のようになります。

```
curl -i -F format=csv -F file=@lead_data.csv -F access_token=<Access Token> <REST API Endpoint Base URL>/bulk/v1/leads.json
```

読み込みファイル「lead_data.csv」には次の内容が含まれています。

```
FirstName,LastName,Email,Company
Able,Baker,ablebaker@marketo.com,Marketo
Charlie,Dog,charliedog@marketo.com,Marketo
Easy,Fox,easyfox@marketo.com,Marketo
```

オプションで、を含めることもできます `lookupField`, `listId`、および `partitionName` リクエストのパラメーター。 `lookupField` リードを同期と同様に、重複排除する特定のフィールドを選択でき、デフォルトはメールです。 以下を指定できます `id` as `lookupField` 「更新のみ」の操作を示します。 `listId` 静的リストを選択して、リードのリストを読み込むことができます。これにより、読み込みによる作成や更新に加えて、リスト内のリードがこの静的リストのメンバーになります。 `partitionName` インポート先の特定のパーティションを選択します。 詳しくは、ワークスペースとパーティションの節を参照してください。

呼び出しへの応答では、同期リードの場合のように成功または失敗のリストはなく、結果の配列のレコードの batchId と status フィールドがあることに注意してください。 これは、この API が非同期で、ステータスが Queued、Importing または Failed を返す場合があるためです。 インポートジョブのステータスを取得したり、完了時に失敗や警告を取得したりするには、batchId を保持する必要があります。 batchId は 7 日間有効です。

## ジョブステータスのポーリング

必要な待ち時間と API 呼び出しの制限に応じて、5～30 秒ごとにジョブをポーリングして、インポートジョブのステータスを確認することをお勧めします。 これを行うには、Get Import Lead Status API を使用します。

```
GET /bulk/v1/leads/batch/{id}.json
```

```json
{
   "requestId":"8136#146daebc2ed",
   "success":true,
   "result":[
      {
         "batchId":1022,
         "status":"Complete",
         "numOfLeadsProcessed":2,
         "numOfRowsFailed":1,
         "numOfRowsWithWarning":0,
         "message":"Import completed with errors, 2 records imported (2 members), 1 failed"
      }
   ]
}
```

この応答は、完了した読み込みを示していますが、ステータスは次のいずれかになります。

- 完了
- キュー
- インポート
- 失敗

ジョブが完了した場合は、警告が発生したジョブで処理され、失敗した行の数のリストが表示されます。 ステータスが失敗の場合は、メッセージパラメーターで失敗メッセージが表示される場合もあります。

## 失敗

失敗は、「リードのステータスを読み込む」応答の「numOfRowsFailed」属性で示されます。 「numOfRowsFailed」が 0 より大きい場合、その値は発生したエラーの数を示します。

失敗した行のレコードと原因を取得するには、失敗ファイルを取得する必要があります。

```
GET /bulk/v1/leads/batch/{id}/failures.json
```

API が、失敗した行を示すファイルと、レコードが失敗した理由を示すメッセージを返します。 ファイルの形式は、ジョブ作成時に「format」パラメーターで指定した形式と同じです。 各レコードには、失敗の説明が追加のフィールドが追加されます。

## 警告

警告は、「リードのステータスのインポートの取得」応答の「numOfRowsWithWarning」属性で示されます。 「numOfRowsWithWarning」が 0 より大きい場合、その値は発生した警告の数を示します。

警告ローのレコードと原因を取得するには、警告ファイルを取得します。

```
GET /bulk/v1/leads/batch/{id}/warnings.json
```

API は、警告が発生した行を示すファイルと、レコードの失敗の理由を示すメッセージを返します。 ファイルの形式は、ジョブ作成時に「format」パラメーターで指定した形式と同じです。 各レコードに、警告の説明を含むフィールドが 1 つ追加されます。
