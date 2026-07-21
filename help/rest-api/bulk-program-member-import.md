---
title: プログラムメンバーの一括読み込み
feature: REST API
description: 10 MB未満のCSV TSVまたはSSV ファイル、キューの制限、必須パラメーター、およびポーリングジョブステータスを使用して、Marketo REST APIを介してプログラムメンバーを一括で読み込む方法について説明します。
exl-id: b0e1039a-fe9b-4fb7-9aa6-9980a06da673
TQID: https://experienceleague.adobe.com/T1PAzLN1mnp38kJ0jwh6kPv6r1Uvxc7-o9zeTHetIV0
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
source-wordcount: 771
ht-degree: 11%

---

# プログラムメンバーの一括読み込み

[一括プログラムメンバー読み込みエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members)

[bulk API](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members)を使用して、多数のプログラムメンバーレコードを非同期で読み込みます。 10 MB未満のコンマ、タブ、またはセミコロンで区切られたフラットファイルでレコードを指定します。

プログラムメンバーの一括読み込みは、「挿入または更新」レコード操作のみをサポートします。

## 処理制限

各一括読み込みリクエストは、ジョブとしてFIFO （先入れ先出し）キューに追加されます。 次の制限が適用されます。

- 最大2つのジョブを同時に処理できます。
- 処理中の2つのジョブを含め、最大10個のジョブをキューに入れることができます。

10 ジョブの最大値を超えると、APIは`1016, Too many imports` エラーを返します。

## ファイルの読み込み

ファイルの最初の行は、各行の値がマップされるREST API フィールド名をリストするヘッダーである必要があります。 これらの名前は、[&#x200B; リードの説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2)および[&#x200B; プログラムメンバーの説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeProgramMemberUsingGET) エンドポイントを使用して取得します。

レコードには、リードフィールド、カスタムリードフィールド、カスタムプログラムメンバーフィールドを含めることができます。

一般的なファイルは、次のパターンに従います。

```text
email,firstName,lastName
test@example.com,John,Doe
```

`multipart/form-data` コンテンツタイプを使用してリクエストを送信します。 既存のライブラリ実装を使用して、マルチパートリクエストを作成します。

## ジョブの作成

[&#x200B; プログラムメンバーの読み込み](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/importProgramMemberUsingPOST) エンドポイントは、ファイルからプログラムメンバーレコードを読み取り、指定されたステータスのプログラムに追加します。 レコードには、リードフィールドとカスタムプログラムメンバーフィールドを含めることができます。

すべてのレコードには、重複排除に使用されるメールフィールドを含める必要があります。

`programId` パスパラメーターは、メンバーを追加するプログラムを指定します。

リクエストには、次の3つのクエリパラメーターが必要です。

- `format`: インポート ファイル形式（`CSV`、`TSV`、または`SSV`）。
- `programMemberStatus`：読み込まれたメンバーに割り当てられたプログラムのステータス。
- `file`: プログラムメンバーレコードを含むファイルの名前。

```http
POST /bulk/v1/program/{programId}/members/import.json?format=csv&programMemberStatus=On List
```

```text
Content-Type: multipart/form-data; boundary=--------------------------118046853683028616211319
Content-Length: 772
Host: <munchkinId>.mktorest.com
```

```text
----------------------------118046853683028616211319
Content-Disposition: form-data; name="file"; filename="Lead-House-Lannister.csv"
Content-Type: text/csv

firstName,lastName,email,title,company,leadScore
Joanna,Lannister,Joanna@Lannister.com,Lannister,House Lannister,0
Tywin,Lannister,Tywin@Lannister.com,Lannister,House Lannister,0
Cersei,Lannister,Cersei@Lannister.com,Lannister,House Lannister,0
Jamie,Lannister,Jamie@Lannister.com,Lannister,House Lannister,0
Tyrion,Lannister,Tyrion@Lannister.com,Lannister,House Lannister,0
Kevan,Lannister,Kevan@Lannister.com,Lannister,House Lannister,0
Dorna,Lannister,Dorna@Lannister.com,Lannister,House Lannister,0
Lancel,Lannister,Lancel@Lannister.com,Lannister,House Lannister,0

----------------------------118046853683028616211319--
```

```json
{
    "requestId": "17f4a#16f87f87325",
    "result": [
        {
            "batchId": 1040,
            "importId": "1040",
            "status": "Queued"
        }
    ],
    "success": true
}
```

エンドポイントは非同期なので、応答には`batchId`と`status`のフィールドが含まれます。 ステータスは`Queued`、`Importing`、または`Failed`です。

`batchId`を保持して、読み込みステータスを確認し、完了後にエラーまたは警告を取得します。 `batchId` は 7 日間有効です。

次のコマンドライン cURL リクエストは、ジョブの例を送信します。

```bash
curl -i -F format='csv' -F programMemberStatus='On List' -F file='@Lead-House-Lannister.csv' -F access_token='<Access Token>' <REST API Endpoint Base URL>/bulk/v1/program/{programId}/members/import.json
```

この例では、`Lead-House-Lannister.csv`読み込みファイルに次のデータが含まれています。

```text
firstName,lastName,email,title,company,leadScore
Joanna,Lannister,Joanna@Lannister.com,Lannister,House Lannister,0
Tywin,Lannister,Tywin@Lannister.com,Lannister,House Lannister,0
Cersei,Lannister,Cersei@Lannister.com,Lannister,House Lannister,0
Jamie,Lannister,Jamie@Lannister.com,Lannister,House Lannister,0
Tyrion,Lannister,Tyrion@Lannister.com,Lannister,House Lannister,0
Kevan,Lannister,Kevan@Lannister.com,Lannister,House Lannister,0
Dorna,Lannister,Dorna@Lannister.com,Lannister,House Lannister,0
Lancel,Lannister,Lancel@Lannister.com,Lannister,House Lannister,0
```

## ジョブステータスのポーリング

インポートジョブを作成したら、5～30秒ごとにポーリングします。 `batchId` パス パラメーターを[読み込みプログラム メンバーのステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) エンドポイントに渡します。

```http
GET /bulk/v1/program/members/import/{batchId}/status.json
```

```json
{
    "requestId": "e0cb#16f87f8b177",
    "result": [
        {
            "batchId": 1040,
            "importId": "1040",
            "status": "Complete",
            "numOfLeadsProcessed": 8,
            "numOfRowsFailed": 0,
            "numOfRowsWithWarning": 0,
            "message": "Import succeeded, 8 records imported (8 members)"
        }
    ],
    "success": true
}
```

この応答は、完了した読み込みを示しています。 ステータスは`Complete`、`Queued`、`Importing`、または`Failed`です。

ジョブが完了すると、応答には、処理された行、失敗した行、および警告を伴って処理された行の数が一覧表示されます。 `message` パラメーターは、ステータスが`Failed`の場合にエラーのメッセージを提供することもできます。

## 失敗

[Get Import Program Member Status](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET)応答の`numOfRowsFailed`属性は、失敗した行の数を示します。 0より大きい値は、エラーが発生したことを意味します。

`batchId` パス パラメーターをGet Import Program Member Failures エンドポイントに渡して、失敗したレコードとその原因を取得します。

```http
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

エンドポイントは、失敗した各行を識別し、レコードが失敗した理由を説明するファイルを返します。 このファイルは、ジョブ作成時に`format` パラメーターで指定された形式を使用します。 各レコードの追加フィールドは、失敗を説明します。

例えば、無効なリードスコアを含む次のファイルを読み込むとします。

```text
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD
```

ジョブのステータスは`numOfRowsFailed`を1として返し、エラーが発生したことを示します。

```http
GET /bulk/v1/program/members/import/{batchId}/status.json
```

```json
{
    "requestId": "4c2d#16f8b32c8ef",
    "result": [
        {
            "batchId": 1046,
            "importId": "1046",
            "status": "Complete",
            "numOfLeadsProcessed": 0,
            "numOfRowsFailed": 1,
            "numOfRowsWithWarning": 0,
            "message": "Import completed with errors, 0 records imported (0 members), 1 failed"
        }
    ],
    "success": true
}
```

詳細については、障害ファイルを取得します。

```http
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

```text
firstName,lastName,email,title,company,leadScore,Import Failure Reason
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD,Invalid data type in field Lead Score
```

## 警告

[読み込みプログラムメンバーのステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET)応答の`numOfRowsWithWarning`属性は、警告が発生した行数を示します。 0より大きい値は、警告が発生したことを意味します。

`batchId` パス パラメーターを[読み込みプログラムメンバーの警告を取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberWarningsUsingGET) エンドポイントに渡して、影響を受けるレコードとその原因を取得します。

```http
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

エンドポイントは、警告を含む各行を識別し、警告が発生した理由を説明するファイルを返します。 このファイルは、ジョブ作成時に`format` パラメーターで指定された形式を使用します。 各レコードの追加フィールドは、警告を表します。

例えば、無効なメールアドレスを含む次のファイルを読み込むとします。

```text
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0
```

ジョブのステータスは`numOfRowsWithWarning`を1として返し、警告が発生したことを示します。

```http
GET /bulk/v1/program/members/import/{batchId}/status.json
```

```json
{
   "requestId":"4ca1#16f883c2003",
   "result":[
      {
         "batchId":1041,
         "importId":"1041",
         "status":"Complete",
         "numOfLeadsProcessed":1,
         "numOfRowsFailed":0,
         "numOfRowsWithWarning":1,
         "message":"Import succeeded, 1 records imported (1 members), 1 warning."
      }
   ],
   "success":true
}
```

詳細については、警告ファイルを取得します。

```http
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

```text
firstName,lastName,email,title,company,leadScore,Import Warning Reason
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0,Invalid email address
```
