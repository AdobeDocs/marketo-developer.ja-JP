---
title: プログラムメンバーの一括読み込み
feature: REST API
description: 10MB 未満の CSV TSV または SSV ファイル、キューの制限、必要なパラメーター、ポーリングジョブステータスを使用して、Marketo REST API を介してプログラムメンバーを一括で読み込む方法について説明します。
exl-id: b0e1039a-fe9b-4fb7-9aa6-9980a06da673
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 94%

---

# プログラムメンバーの一括読み込み

[プログラムメンバーの一括読み込みエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members)

大量のプログラムメンバーレコードの場合は、[一括 API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members) を使用してプログラムメンバーを非同期的に読み込めます。これにより、区切り文字（コンマ、タブ、またはセミコロン）を含むフラットファイルを使用して、レコードのリストを Marketo に読み込めます。ファイルの合計サイズが 10 MB 未満であれば、ファイルには任意の数のレコードを含めることができます。レコード操作は、「挿入または更新」のみです。

## 処理制限

制限付きで、複数の一括読み込みリクエストを送信できます。各リクエストは、ジョブとして FIFO キューに追加され、処理されます。最大 2 つのジョブが同時に処理されます。任意の時点でキューに入れることができるジョブの数は最大 10 個です（現在処理中の 2 個を含む）。ジョブの最大数が 10 を超えると、「1016、読み込みが多すぎます」というエラーが返されます。

## ファイルの読み込み

ファイルの最初の行は、各行の値をマッピングするフィールドとして対応する REST API 名をリストするヘッダーにする必要があります。REST API 名は、[リードを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2)エンドポイントや[プログラムメンバーを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeProgramMemberUsingGET)エンドポイントを使用して取得できます。レコードには、リードフィールド、カスタムリードフィールド、カスタムプログラムメンバーフィールドを含めることができます。

一般的なファイルは、次の基本パターンに従います。

```
email,firstName,lastName
test@example.com,John,Doe
```

呼び出し自体は、`multipart/form-data` コンテンツタイプを使用して行われます。

このリクエストタイプは実装が難しい場合があるので、既存のライブラリ実装を使用することを強くお勧めします。

## ジョブの作成

[プログラムメンバーを読み込み](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/importProgramMemberUsingPOST)エンドポイントでは、プログラムメンバーレコードを含むファイルを読み取り、指定したステータスでプログラムに追加します。レコードには、リードフィールドとプログラムメンバーのカスタムフィールドの両方を含めることができます。すべてのレコードには、重複排除に使用されるメールフィールドを含める必要があります。

`programId` パスパラメーターは、メンバーを追加するプログラムを指定します。

必須のクエリパラメーターは 3 つあります。`format` パラメーターは読み込みファイルの形式（CSV、TSV または SSV）を指定し、`programMemberStatus` パラメーターはプログラムに追加されるメンバーのプログラムステータスを指定し、`file` パラメーターにはプログラムメンバーレコードを含む読み込みファイルの名前が含まれます。

```
POST /bulk/v1/program/{programId}/members/import.json?format=csv&programMemberStatus=On List
```

```
Content-Type: multipart/form-data; boundary=--------------------------118046853683028616211319
Content-Length: 772
Host: <munchkinId>.mktorest.com
```

```
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

呼び出しに対する応答では、結果配列のレコードの `batchId` と `status` フィールドが表示されます。このエンドポイントは非同期なので、キュー済み、読み込み中、または失敗のステータスを返すことができます。読み込みジョブのステータスを取得し、完了時に失敗や警告を取得するには、`batchId` を保持する必要があります。`batchId` は 7 日間有効です。

上記の例を使用すると、エンドポイントを呼び出す簡単な方法は、コマンドラインから cURL を使用することです。

```bash
curl -i -F format='csv' -F programMemberStatus='On List' -F file='@Lead-House-Lannister.csv' -F access_token='<Access Token>' <REST API Endpoint Base URL>/bulk/v1/program/{programId}/members/import.json
```

読み込みファイル「Lead-House-Lannister.csv」には次の内容が含まれます。

```
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

読み込みジョブを作成したら、このステータスのクエリを実行する必要があります。インポートジョブを 5～30 秒ごとにポーリングするのがベストプラクティスです。これを行うには、`batchId` パスパラメーターを[プログラムメンバーを読み込みステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET)エンドポイントに渡します。

```
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

この応答は、完了した読み込みを示しています。ステータスは、完了、キュー済み、読み込み中、失敗のいずれかです。

ジョブが完了したら、処理された行数、失敗した行数、警告のあった行数のリストが表示されます。ステータスが失敗の場合、メッセージパラメーターによって失敗メッセージも返されることがあります。

## 失敗

失敗は、[プログラムメンバーを読み込みステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET)応答の `numOfRowsFailed` 属性によって示されます。numOfRowsFailed がゼロより大きい場合、この値は発生した失敗の数を示します。

「読み込みプログラムメンバーのエラーの取得」エンドポイントを使用して、`batchId` パスパラメーターを渡すことにより、失敗した行のレコードと原因を取得します。

```
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

エンドポイントは、失敗した行を示すファイルと、レコードが失敗した理由を示すメッセージで応答します。ファイルの形式は、ジョブ作成時に `format` パラメーターで指定されたものと同じです。各レコードに、失敗の説明を含む追加フィールドが追加されます。

例えば、無効なリードスコアを含む次のファイルを読み込むとします。

```
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD
```

ジョブのステータスを確認すると、`numOfRowsFailed` が 1 になっており、失敗が発生したことが示されています。

```
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

次に、失敗に関する追加の詳細を確認するのに、失敗ファイルを取得します。

```
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

```
firstName,lastName,email,title,company,leadScore,Import Failure Reason
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD,Invalid data type in field Lead Score
```

## 警告

警告は、[プログラムメンバーを読み込みステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET)応答の `numOfRowsWithWarning` 属性によって示されます。`numOfRowsWithWarning` がゼロより大きい場合、この値は発生した警告の数を示します。

[プログラムメンバーを読み込み警告を取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberWarningsUsingGET)エンドポイントを使用して、`batchId` パスパラメーターを渡すことで、警告した行のレコードと原因を取得します。

```
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

エンドポイントは、警告が発生した行を示すファイルと、レコードが警告を生成した理由を示すメッセージで応答します。ファイルの形式は、ジョブ作成時に `format` パラメーターで指定されたものと同じです。各レコードに、警告の説明を含む追加フィールドが追加されます。

例えば、無効なメールアドレスを含む次のファイルを読み込むとします。

```
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0
```

ジョブのステータスを確認すると、`numOfRowsWithWarning` が 1 になっており、警告が発生したことが示されています。

```
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

次に、警告に関する追加の詳細を確認する警告ファイルを取得します。

```
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

```
firstName,lastName,email,title,company,leadScore,Import Warning Reason
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0,Invalid email address
```
