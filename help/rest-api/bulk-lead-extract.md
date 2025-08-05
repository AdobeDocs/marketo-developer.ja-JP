---
title: リードの一括抽出
feature: REST API
description: リードデータのバッチ抽出。
exl-id: 42796e89-5468-463e-9b67-cce7e798677b
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 100%

---

# リードの一括抽出

[リードの一括抽出エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads)

REST API のリードの一括抽出のセットには、Marketo から大量のリード／ユーザレコードを取得するためのプログラムインターフェイスが用意されています。また、レコードの作成日、最新の更新、静的リストのメンバーシップまたはスマートリストのメンバーシップに基づいて、リードを増分的に取得するためにも使用できます。ETL、データウェアハウス、アーカイブの目的で、Marketo と 1 つ以上の外部システム間で継続的にデータを交換する必要があるユースケースに推奨されるインターフェイスです。

## 権限

Bulk Lead Extract API では、所有する API ユーザが、「読み取り専用リード」権限または「読み取り／書き込みリード」権限のいずれかまたは両方を含むロールを有している必要があります。

## フィルター

リードは、様々なフィルターオプションをサポートしています。`updatedAt`、`smartListName`、`smartListId` を含む特定のフィルターには、すべてのサブスクリプションにはロールアウトされていない追加のインフラストラクチャコンポーネントが必要です。書き出しジョブごとに指定できるフィルタータイプは 1 つだけです。

| フィルタータイプ | データタイプ | メモ |
|---|---|---|
| createdAt | 日付範囲 | メンバー `startAt` と `endAt` を持つ JSON オブジェクトを受け入れます。`startAt` は透かし（低）を表す日時を受け入れ、`endAt` は透かし（高）を表す日時を受け入れます。範囲は 31日以内にする必要があります。 日時形式は、ミリ秒を含まない ISO-8601 形式にする必要があります。このフィルタータイプのジョブは、日付範囲内で作成されたアクセス可能なすべてのレコードを返します。 |
| updatedAt* | 日付範囲 | メンバー `startAt` と `endAt` を持つ JSON オブジェクトを受け入れます。`startAt` は透かし（低）を表す日時を受け入れ、`endAt` は透かし（高）を表す日時を受け入れます。範囲は 31日以内にする必要があります。 日時形式は、ミリ秒を含まない ISO-8601 形式にする必要があります。メモ：このフィルターは、標準フィールドへの更新のみを反映する、表示可能な「updatedAt」フィールドはフィルタリングしません。このフィルターは、リードレコードに対して最新のフィールド更新が行われた日時に基づいてフィルタリングしますこのフィルタータイプのジョブは、日付範囲内で最近更新されたアクセス可能なすべてのレコードを返します。 |
| staticListName | 文字列 | 静的リストの名前を受け取ります。このフィルタータイプのジョブは、ジョブの処理開始時点で静的リストのメンバーであるアクセス可能なすべてのレコードを返します。「リストを取得」エンドポイントを使用して静的リスト名を取得します。 |
| staticListId | 整数 | 静的リストの ID を受け取ります。このフィルタータイプのジョブは、ジョブの処理開始時点で静的リストのメンバーであるアクセス可能なすべてのレコードを返します。「リストを取得」エンドポイントを使用して静的リスト ID を取得します。 |
| smartListName* | 文字列 | スマートリストの名前を受け取ります。このフィルタータイプのジョブは、ジョブの処理開始時点でスマートリストのメンバーであるアクセス可能なすべてのレコードを返します。「スマートリストを取得」エンドポイントを使用してスマートリスト名を取得します。 |
| smartListId* | 整数 | スマートリストの ID を受け取ります。このフィルタータイプのジョブは、ジョブの処理開始時点でスマートリストのメンバーであるアクセス可能なすべてのレコードを返します。「スマートリストを取得」エンドポイントを使用してスマートリスト ID を取得します。 |

一部のサブスクリプションでは、フィルタータイプは使用できません。サブスクリプションで使用できない場合は、「リードを書き出しジョブを作成」エンドポイントを呼び出す際にエラーが発生します（「1035、ターゲットサブスクリプションでサポートされていないフィルタータイプ」）。顧客は、Marketo サポートに連絡して、サブスクリプションでこの機能を有効にすることができます。

## オプション

「リードを書き出しジョブを作成」エンドポイントには、いくつかの書式設定オプションが用意されており、ユーザは書き出されたファイル内に特定のフィールドを含めたり、これらのフィールドの列ヘッダーの名前を変更したり、書き出されたファイルの形式を変更したりできます。

| パラメーター | データタイプ | 必須 | メモ |
|---|---|---|---|
| フィールド | 配列[文字列] | はい | fields パラメーターは、文字列の JSON 配列を受け入れます。各文字列は、Marketo リードフィールドの REST API 名にする必要があります。リストされたフィールドは、書き出されたファイルに含まれます。各フィールドの列ヘッダーは、columnHeader で上書きしない限り、各フィールドの REST API 名になります。メモ：[!DNL Adobe Experience Cloud Audience Sharing] 機能を有効にすると、[!DNL Adobe Experience Cloud] ID（ECID）を Marketo リードに関連付ける cookie 同期プロセスが実行されます。「ecids」フィールドを指定して、書き出しファイルに ECID を含めることができます。 |
| columnHeaderNames | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。キーは、書き出しジョブに含まれるフィールドの名前にする必要があります。これは、「リードを説明」を呼び出すことによって取得できるフィールドの API 名です。値は、このフィールドの書き出された列ヘッダーの名前です。 |
| format | 文字列 | いいえ | CSV、TSV、SSV のいずれかを受け入れます。書き出されたファイルは、設定した場合、それぞれコンマ区切り値、タブ区切り値、またはスペース区切り値のファイルとしてレンダリングされます。未設定の場合は、デフォルトで CSV に設定されます。 |

## ジョブの作成

ジョブのパラメーターは、[リードを書き出しジョブを作成](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/createExportLeadsUsingPOST)エンドポイントを使用して書き出しを開始する前に定義されます。書き出しに必要な `fields`、`filter` のパラメーターのタイプ、ファイルの `format`、列ヘッダー名（存在する場合）を定義する必要があります。

```
POST /bulk/v1/leads/export/create.json
```

```json
{
   "fields": [
      "firstName",
      "lastName",
      "id",
      "email"
   ],
   "format": "CSV",
   "columnHeaderNames": {
      "firstName": "First Name",
      "lastName": "Last Name",
      "id": "Marketo Id",
      "email": "Email Address"
   },
   "filter": {
      "createdAt": {
         "startAt": "2017-01-01T00:00:00Z",
         "`endAt`": "2017-01-31T00:00:00Z"
      }
   }
}
```

このリクエストでは、対応する `firstName`、`lastName`、`id` および `email` フィールドの値を含む、2017年1月1日（PT）から 2017年1月31日（PT）の間に作成した一連のリードの書き出しが開始されます。

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Created",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "format": "CSV"
      }
   ]
}
```

これにより、ジョブが作成されたことを示すステータス応答が返されます。ジョブは定義および作成されましたが、まだ開始されていません。これを行うには、作成ステータス応答の exportId を使用して、[リードを書き出しジョブをキューに入れる](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/enqueueExportLeadsUsingPOST)エンドポイントを呼び出す必要があります。

```
POST /bulk/v1/leads/export/{exportId}/enqueue.json
```

```json
{
    "requestId": "147e4#16b24d9b913",
    "result": [
        {
            "exportId": "fad2cd1b-e822-4025-be1e-9caa9cf1d4b8",
            "format": "CSV",
            "status": "Queued",
            "createdAt": "2019-06-04T23:35:43Z",
            "queuedAt": "2019-06-04T23:36:17Z"
        }
    ],
    "success": true
}
```

これは、「キュー済み」の `status` で応答し、その後、使用可能な書き出しスロットがある場合に「処理中」に設定されます。

## ジョブステータスのポーリング

`Note:` ステータスを取得できるのは、同じ API ユーザによって作成されたジョブのみです。

これは非同期エンドポイントなので、ジョブを作成した後、その進行状況を判断するためにこのステータスをポーリングする必要があります。[リードを書き出しジョブのステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET)エンドポイントを使用してポーリングします。ステータスは 60 秒ごとに 1 回しか更新されないので、これより低いポーリング頻度はお勧めしません。ほとんどの場合、それでも過剰です。ポーリングについて簡単に見てみましょう。

```
GET /bulk/v1/leads/export/{exportId}/status.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Processing",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "format": "CSV"
      }
   ]
}
```

ステータスエンドポイントは、ジョブがまだ処理中なので、ファイルはまだ取得できないことを示す応答を返します。ジョブのステータスが「完了」に変わったら、ダウンロードの準備をします。

ステータスフィールドは、次のいずれかで応答します。

- 作成済み
- 待機中
- 処理中
- キャンセル済み
- 完了
- 失敗

## データの取得

リードの書き出しが完了したファイルを取得するには、`exportId` を使用して[リードを書き出しファイルを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/getExportLeadsFileUsingGET)エンドポイントを呼び出すだけです。

```
GET /bulk/v1/leads/export/{exportId}/file.json
```

応答には、ジョブの設定方法に従って書式設定されたファイルが含まれます。エンドポイントは、ファイルのコンテンツを使用して応答します。


リクエストされたリードフィールドが空（データが含まれていない）の場合、書き出しファイル内の対応するフィールドに `null` が配置されます。以下の例では、返されたリードの email フィールドは空です。

```csv
firstName,lastName,email,cookies
Russell,Wilson,null,_mch-localhost-1536605780000-12105
```

抽出されたデータの部分的で再開にわかりやすい取得をサポートするために、ファイルエンドポイントは、オプションで bytes タイプの HTTP ヘッダー範囲をサポートします。ヘッダーが設定されていない場合は、コンテンツ全体が返されます。Marketo [一括抽出](bulk-extract.md)で範囲ヘッダーを使用する詳しい方法について参照してください。

## ジョブのキャンセル

ジョブを誤って設定したり、不要になった場合は、[リードを書き出しジョブをキャンセル](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/cancelExportLeadsUsingPOST)エンドポイントを使用して簡単にキャンセルできます。

```
POST /bulk/v1/leads/export/{exportId}/cancel.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Cancelled",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "format": "CSV"
      }
   ]
}
```

これは、ジョブがキャンセルされたことを示すステータスで応答します。
