---
title: リードの一括読み込み
feature: REST API
description: CSV TSV または SSV を使用して、Marketoでの非同期の一括リード読み込みを作成および監視します。
exl-id: 615f158b-35f9-425a-b568-0a7041262504
source-git-commit: c1b9763835b25584f0c085274766b68ddf5c7ae2
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 77%

---

# リードの一括読み込み

[リードの一括読み込みエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads)

大量のリードレコードの場合は、[一括 API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/importLeadUsingPOST) を使用してリードを非同期的に読み込めます。これにより、区切り文字（コンマ、タブ、またはセミコロン）を含むフラットファイルを使用して、レコードのリストを Marketo に読み込めます。ファイルの合計サイズが 10 MB 未満であれば、ファイルには任意の数のレコードを含めることができます。レコード操作は、「挿入または更新」のみです。

## 処理制限

制限付きで、複数の一括読み込みリクエストを送信できます。各リクエストは、ジョブとして FIFO キューに追加され、処理されます。最大 2 つのジョブが同時に処理されます。任意の時点でキュー内に許可されるジョブの数は最大 10 です（現在処理中の 2 つのジョブを含む）。 ジョブの最大数が 10 を超えると、`1016, Too many imports` のエラーが返されます。

## ファイルの読み込み

ファイルの最初の行は、各行の値のマッピング先に対応する REST API フィールドをリストするヘッダーにする必要があります。一般的なファイルは、次の基本パターンに従います。

```csv
email,firstName,lastName
test@example.com,John,Doe
```

`externalCompanyId` フィールドを使用すると、リードレコードを会社レコードにリンクできます。`externalSalesPersonId` フィールドを使用すると、リードレコードをセールス担当者レコードにリンクできます。

呼び出し自体は、`multipart/form-data` コンテンツタイプを使用して行われます。

このリクエストタイプは実装が難しい場合があるので、既存のライブラリ実装を使用することを強くお勧めします。

## ジョブの作成

一括読み込みリクエストを行うには、content-type ヘッダーを `multipart/form-data` に設定し、少なくともファイルコンテンツを指定する `file` パラメーターと、ファイル形式を示す値 `format`、`csv`、`tsv` を指定する `ssv` パラメーターを含める必要があります。

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

firstName,lastName,email,company
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

このエンドポイントは、[コンテンツタイプとして multipart/form-data](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html) を使用します。正しく使用するために、選択した言語に HTTP サポートライブラリを使用することをお勧めします。 次の例は、コマンドラインから cURL を使用してこれを行う簡単な方法です。

```
curl -i -F format=csv -F file=@lead_data.csv -F access_token=<Access Token> <REST API Endpoint Base URL>/bulk/v1/leads.json
```

読み込みファイル `lead_data.csv` には、次の内容が含まれます。

```
firstName,lastName,email,company
Able,Baker,ablebaker@marketo.com,Marketo
Charlie,Dog,charliedog@marketo.com,Marketo
Easy,Fox,easyfox@marketo.com,Marketo
```

オプションで、リクエストに `lookupField`、`listId`、`partitionName` パラメーターを含めることもできます。`lookupField` を使用すると、「リードを同期」と同様に重複排除する特定のフィールドを選択でき、デフォルトはメールになります。「更新のみ」の操作を示すために、`id` を `lookupField` として指定できます。`listId` を使用すると、リードのリストを読み込む静的リストを選択できます。これにより、読み込みによって作成されたリードや更新に加えて、リスト内のリードがこの静的リストのメンバーになります。`partitionName` は、読み込み先の特定のパーティションを選択します。詳しくは、「ワークスペースとパーティション」の節を参照してください。

呼び出しに対する応答では、「リードを同期」のように成功または失敗のリストは表示されませんが、結果配列にはレコードの batchId とステータスフィールドが表示されます。これは、この API が非同期で、ステータスとして &quot;Queued&quot;、&quot;Importing&quot;、または &quot;Failed&quot; が返される可能性があるからです。読み込みジョブのステータスを取得し、完了時に失敗や警告を取得するには、batchId を保持する必要があります。batchId は 7 日間有効です。

## ジョブステータスのポーリング

読み込みジョブのステータスを確認するには、必要な待ち時間と API 呼び出しの制限に応じて、5～30 秒ごとにジョブをポーリングするのがベストプラクティスです。これを行うには、Get Import Lead Status API を使用します。

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

この応答は、完了した読み込みを示しますが、ステータスは次のいずれかになります。

- Complete
- 待機中
- 読み込み
- 失敗

ジョブが完了したら、処理された行数、失敗した行数、警告のあった行数のリストが表示されます。ステータスが失敗の場合、メッセージパラメーターによって失敗メッセージも返されることがあります。

## 失敗

失敗は、「インポートリードステータスの取得」応答の `numOfRowsFailed` 属性で示されます。 `numOfRowsFailed` がゼロより大きい場合、この値は発生した失敗の数を示します。

失敗したローのレコードと原因を取得するには、失敗ファイルを取得する必要があります。

```
GET /bulk/v1/leads/batch/{id}/failures.json
```

API は、失敗した行を示すファイルと、レコードが失敗した理由を示すメッセージで応答します。 ファイルの形式は、ジョブ作成時に `format` パラメーターで指定されたものと同じです。各レコードに、失敗の説明を含む追加フィールドが追加されます。

## 警告

警告は、「インポートリードのステータスを取得」応答の `numOfRowsWithWarning` 属性で示されます。 `numOfRowsWithWarning` が 0 より大きい場合、その値は発生した警告の数を示します。

警告の行のレコードと原因を取得するには、警告ファイルを取得します。

```
GET /bulk/v1/leads/batch/{id}/warnings.json
```

API は、警告が発生した行を示すファイルと、レコードが失敗した理由を示すメッセージで応答します。ファイルの形式は、ジョブ作成時に `format` パラメーターで指定されたものと同じです。各レコードに、警告の説明を含む追加フィールドが追加されます。
