---
title: プログラムメンバーの一括読み込み
feature: REST API
description: 「メンバーデータのバッチインポート」
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---


# プログラムメンバーの一括読み込み

[プログラムメンバーの一括読み込みエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members)

大量のプログラムメンバーレコードの場合、プログラムメンバーは [一括 API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members). これにより、区切り文字（コンマ、タブ、またはセミコロン）を含むフラットファイルを使用して、レコードのリストをMarketoにインポートできます。 ファイルには任意の数のレコードを含めることができます（ファイルの合計サイズが 10 MB 未満である場合）。 レコード操作は、「挿入または更新」のみです。

## 処理制限

制限を持つ複数の一括読み込みリクエストを送信できます。 各リクエストは、処理される FIFO キューにジョブとして追加されます。 最大 2 つのジョブが同時に処理されます。 任意の時点でキューに入れられるジョブの数は最大 10 個です（現在処理中の 2 個を含む）。 ジョブの最大数 10 を超えると、「1016, Too many imports」エラーが返されます。

## ファイルのインポート

ファイルの最初の行は、対応する REST API 名を、各行の値をマッピングするフィールドとしてリストするヘッダーである必要があります。 REST API 名は、を使用して取得できます [リードの説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) および/または [プログラムメンバーの説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeProgramMemberUsingGET) エンドポイント。 レコードには、リードフィールド、カスタムリードフィールド、カスタムプログラムメンバーフィールドを含めることができます。

一般的なファイルの形式は、次のような基本的なパターンになります。

```
email,firstName,lastName
test@example.com,John,Doe
```

呼び出しそのものは、 `multipart/form-data` content-type。

このリクエストタイプは実装が困難な場合があるので、既存のライブラリ実装を使用することを強くお勧めします。

## ジョブの作成

この [プログラムメンバーのインポート](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/importProgramMemberUsingPOST) エンドポイントは、プログラムメンバーレコードを含むファイルを読み取り、特定のステータスのプログラムに追加します。 このレコードには、リードフィールドとプログラムメンバーカスタムフィールドの両方を含めることができます。 すべてのレコードには、重複排除に使用される「メール」フィールドを含める必要があります。

この `programId` path パラメーターは、メンバーを追加するプログラムを指定します。

必須のクエリパラメーターは 3 つあります。 この `format` パラメーターは、読み込みファイルの形式（CSV、TSV または SSV）を指定し、 `programMemberStatus` パラメーターは、プログラムに追加されるメンバーのプログラムステータスを指定します。 `file` パラメーターには、プログラムメンバーレコードを含むインポートファイルの名前が含まれています。

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

呼び出しに対する応答で、が存在することに注意します。 `batchId` および `status` 結果の配列内のレコードのフィールド。 このエンドポイントは非同期なので、ステータスが Queued、Importing または Failed を返す場合があります。 を保持する必要があります `batchId` 読み込みジョブのステータスを取得し、完了時に失敗や警告を取得できます。 この `batchId` は 7 日間有効です。

上記の例を使用すると、エンドポイントを呼び出す簡単な方法は、コマンドラインから cURL を使用することです。

```bash
curl -i -F format='csv' -F programMemberStatus='On List' -F file='@Lead-House-Lannister.csv' -F access_token='<Access Token>' <REST API Endpoint Base URL>/bulk/v1/program/{programId}/members/import.json
```

読み込みファイル「Lead-House-Lanister.csv」には、次のファイルが含まれています。

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

インポートジョブを作成したら、そのステータスを問い合わせる必要があります。 インポートジョブは 5～30 秒ごとにポーリングすることをお勧めします。 これを行うには、 `batchId` へのパスパラメーター [インポート プログラム メンバーステータスの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) エンドポイント。

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

この応答は、完了した読み込みを示しています。 ステータスは、完了、キュー内、インポート、失敗のいずれかです。

ジョブが完了すると、処理された行数、失敗した行数、警告を含む行数のリストが表示されます。 ステータスが失敗の場合は、メッセージパラメーターで失敗メッセージが表示される場合もあります。

## 失敗

失敗は、によって示されます `numOfRowsFailed` 属性： [インポート プログラム メンバーステータスの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) 応答。 numOfRowsFailed が 0 より大きい場合、その値は発生したエラーの数を示します。

の使用 [インポート プログラム メンバーの取得エラー](http://TODO) レコードおよび失敗した行の原因を取得するエンドポイント （を渡すことにより） `batchId` パスパラメーター。

```
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

エンドポイントは、失敗した行を示すファイルと、レコードが失敗した理由を示すメッセージを返します。 ファイルの形式はで指定した形式と同じです。 `format` ジョブ作成中のパラメーター。 各レコードには、失敗の説明が追加のフィールドが追加されます。

例えば、無効なリードスコアを含む次のファイルを読み込んだとします。

```
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD
```

ジョブステータスを確認すると、次のように表示されます `numOfRowsFailed` は 1 で、エラーが発生したことを示します。

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

次に、失敗ファイルを取得して、失敗に関する追加の詳細を確認します。

```
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

```
firstName,lastName,email,title,company,leadScore,Import Failure Reason
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD,Invalid data type in field Lead Score
```

## 警告

警告は、 `numOfRowsWithWarning` 属性： [インポート プログラム メンバーステータスの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) 応答。 次の場合 `numOfRowsWithWarning` が 0 より大きい場合、その値は発生した警告の数を示します。

の使用 [インポート プログラム メンバーの警告の取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberWarningsUsingGET) レコードを取得するエンドポイント、および `batchId` パスパラメーター。

```
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

エンドポイントには、警告が発生した行を示すファイルと、レコードで警告が発生した理由を示すメッセージが応答されます。 ファイルの形式はで指定した形式と同じです。 `format` ジョブ作成中のパラメーター。 各レコードに、警告の説明を含むフィールドが 1 つ追加されます。

例えば、無効なメールアドレスを使用して次のファイルを読み込むとします。

```
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0
```

ジョブステータスを確認すると、次のように表示されます `numOfRowsWithWarning` は 1 で、警告が発生したことを示します。

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

その後、警告ファイルを取得して、警告に関する追加の詳細を確認します。

```
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

```
firstName,lastName,email,title,company,leadScore,Import Warning Reason
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0,Invalid email address
```
