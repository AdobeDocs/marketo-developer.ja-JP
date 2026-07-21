---
title: リードの一括読み込み
feature: REST API
description: CSV TSVまたはSSVを使用して、Marketoで非同期の一括リードインポートを作成および監視します。
exl-id: 615f158b-35f9-425a-b568-0a7041262504
TQID: https://experienceleague.adobe.com/UamXYWis5J1ERqnp5lAnfUf3pFcgfSOLfKRXRB-Yg4I
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 623
ht-degree: 9%

---

# リードの一括読み込み

[リードの一括読み込みエンドポイントの参照](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads)

[bulk API](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads/operation/importLeadUsingPOST)を使用して、多数のリードレコードを非同期で読み込みます。 10 MB未満のコンマ、タブ、またはセミコロンで区切られたフラットファイルでレコードを指定します。

リードの一括読み込みは、「挿入または更新」レコード操作のみをサポートします。

## 処理制限

各一括読み込みリクエストは、ジョブとしてFIFO （先入れ先出し）キューに追加されます。 次の制限が適用されます。

- 最大2つのジョブを同時に処理できます。
- 処理中の2つのジョブを含め、最大10個のジョブをキューに入れることができます。

10 ジョブの最大値を超えると、APIは`1016, Too many imports` エラーを返します。

## ファイルの読み込み

ファイルの最初の行は、各行の値がマップされるREST API フィールドをリストするヘッダーである必要があります。 一般的なファイルは、次のパターンに従います。

```csv
email,firstName,lastName
test@example.com,John,Doe
```

`externalCompanyId`を使用して、リード レコードを会社レコードにリンクします。 `externalSalesPersonId`を使用して、リード レコードを営業担当者レコードにリンクします。

`multipart/form-data` コンテンツタイプを使用してリクエストを送信します。 既存のライブラリ実装を使用して、マルチパートリクエストを作成します。

## ジョブの作成

一括読み込みジョブを作成するには、コンテンツタイプを`multipart/form-data`に設定し、次のパラメーターを含めます。

- `file`: インポートファイルのコンテンツ。
- `format`: ファイル形式。 有効な値は`csv`、`tsv`、`ssv`です。

```http
POST /bulk/v1/leads.json?format=csv
```

```text
Content-Type: multipart/form-data; boundary=------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Length: 311
Host: <munchkinId>.mktorest.com
```

```text
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

このエンドポイントは、[コンテンツタイプとして multipart/form-data](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html) を使用します。 HTTP サポートライブラリを使用して、リクエストを正しく構築します。 次の例では、コマンドラインからcURLを使用します。

```bash
curl -i -F format=csv -F file=@lead_data.csv -F access_token=<Access Token> <REST API Endpoint Base URL>/bulk/v1/leads.json
```

この例では、`lead_data.csv`読み込みファイルに次のデータが含まれています。

```text
firstName,lastName,email,company
Able,Baker,ablebaker@marketo.com,Marketo
Charlie,Dog,charliedog@marketo.com,Marketo
Easy,Fox,easyfox@marketo.com,Marketo
```

次のオプションのパラメーターも含めることができます。

- `lookupField`：重複排除に使用されるフィールドを選択し、デフォルトは`email`です。 「更新専用」操作を実行するには、`id`を指定します。
- `listId`：静的リストを選択します。 インポートしたリードは、インポートで作成または更新されたレコードに加えて、このリストのメンバーになります。
- `partitionName`: インポート先のパーティションを選択します。 詳しくは、「ワークスペースとパーティション」の節を参照してください。

APIは非同期なので、応答には個々の成功と失敗ではなく`batchId`と`status`のフィールドが含まれます。 ステータスは`Queued`、`Importing`、または`Failed`です。

ジョブの状態を確認し、完了後にエラーまたは警告を取得するには、`batchId`を保持します。 `batchId` は 7 日間有効です。

## ジョブステータスのポーリング

Get Import Lead Status APIを使用して、待ち時間の要件とAPI呼び出しの制限に応じて、5～30秒ごとにジョブをポーリングします。

```http
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

この応答は、完了した読み込みを示しています。 ステータスは、次のいずれかの値にすることができます。

- Complete
- 待機中
- 読み込み
- 失敗

ジョブが完了すると、応答には、処理された行、失敗した行、および警告を伴って処理された行の数が一覧表示されます。 `message` パラメーターは、ステータスが`Failed`の場合にエラーのメッセージを提供することもできます。

## 失敗

Get Import Lead Status応答の`numOfRowsFailed`属性は、失敗した行の数を示します。 0より大きい値は、エラーが発生したことを意味します。

失敗したレコードとその原因を取得するには、失敗ファイルをリクエストします。

```http
GET /bulk/v1/leads/batch/{id}/failures.json
```

APIは、失敗した各行を識別し、レコードが失敗した理由を説明するファイルを返します。 このファイルは、ジョブ作成時に`format` パラメーターで指定された形式を使用します。 各レコードの追加フィールドは、失敗を説明します。

## 警告

Get Import Lead Status応答の`numOfRowsWithWarning`属性は、警告を含む行数を示します。 0より大きい値は、警告が発生したことを意味します。

影響を受けるレコードとその原因を取得するには、警告ファイルをリクエストします。

```http
GET /bulk/v1/leads/batch/{id}/warnings.json
```

APIは、警告を含む各行を識別し、警告が発生した理由を説明するファイルを返します。 このファイルは、ジョブ作成時に`format` パラメーターで指定された形式を使用します。 各レコードの追加フィールドは、警告を表します。
