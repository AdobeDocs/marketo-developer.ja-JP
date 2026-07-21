---
title: アクティビティの一括抽出
feature: REST API
description: Marketo Bulk Activity ETLおよびCRM用の31日間の日付範囲、アクティビティ、主要属性フィルターを使用して、REST APIを抽出して大量のアクティビティデータを書き出します。
exl-id: 6bdfa78e-bc5b-4eea-bcb0-e26e36cf6e19
TQID: https://experienceleague.adobe.com/lIlXNjatN-F77Dv3xsVkQ3hAWwLZ4wlSW0zKNkFJFMA
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: e64968b2-4ee5-47f9-8cae-0588f184b9ebid: ea90ebee-5c84-42d9-8b21-006bdabc95a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1268
ht-degree: 23%

---

# アクティビティの一括抽出

[一括アクティビティ抽出エンドポイント リファレンス](https://developer.adobe.com/marketo-apis/api/mapi)

Bulk Activity Extract REST APIは、Marketoから大量のアクティビティデータを取得します。 CRM統合、ETL、データウェアハウス、データアーカイブなど、低遅延を必要としないプロセスに使用できます。

## 権限

API ユーザーには、「読み取り専用アクティビティ」または「読み取り/書き込みアクティビティ」権限が必要です。

## フィルター

| フィルタータイプ | データタイプ | 必須 | メモ |
| --- | --- | --- | --- |
| `createdAt` | 日付範囲 | はい | `startAt`と`endAt`を含むJSON オブジェクト。 `startAt`は透かしの少ない日時で、`endAt`は透かしの多い日時です。 範囲は 31日以内にする必要があります。 このジョブは、日付範囲内で作成されたすべてのアクセス可能なレコードを返します。 ミリ秒なしでISO-8601日時値を使用します。 |
| `activityTypeIds` | 配列\[整数\] | いいえ | リクエストされたアクティビティタイプの整数の配列。 「リードを削除」アクティビティはサポートされていません。 代わりに、[削除されたリードを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getDeletedLeadsUsingGET) エンドポイントを使用してください。 [ アクティビティタイプの取得エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getAllActivityTypesUsingGET)を使用して、アクティビティタイプ IDを取得します。 |
| [`primaryAttributeValueIds`](#primaryattributevalueids-options) | 配列\[整数\] | いいえ | プライマリ属性に対して最大50個のIDを受け入れる配列。 各IDは、リードフィールドまたはアセットを一意に識別します。 適切なREST API エンドポイントを呼び出してIDを取得します。 例えば、「フォームに入力」アクティビティの特定のフォームをフィルタリングするには、フォーム名を[名前によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByNameUsingGET)エンドポイントに渡してフォーム ID を取得します。 サポートされているアクティビティタイプについては、[primaryAttributeValueIds オプション ](#primaryattributevalueids-options)を参照してください。 |
| [`primaryAttributeValues`](#primaryattributevalues-options) | 配列\[文字列\] | いいえ | プライマリ属性の名前を50個まで指定できる配列。 各名前は、リードフィールドまたはアセットを一意に識別します。 適切なREST API エンドポイントを呼び出して、名前を取得します。 例えば、「フォームに入力」アクティビティの特定のフォームをフィルタリングするには、フォーム ID を [ID によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByIdUsingGET)エンドポイントに渡してフォーム名を取得します。 サポートされているアクティビティタイプについては、[primaryAttributeValues オプション ](#primaryattributevalues-options)を参照してください。 |

### primaryAttributeValueIds オプション {#primaryattributevalueids-options}

| アクティビティのタイプ | プライマリ属性値 ID | 取得エンドポイント | アセットグループ |
| --- | --- | --- | --- |
| データ値を変更 | リードフィールド ID | [リードを説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| スコアを変更 | リードフィールド ID | [リードを説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| 進行状況のステータスを変更 | プログラム ID | [名前によるプログラムを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramByNameUsingGET) | マーケティングプログラム |
| リストに追加 | 静的リスト ID | [名前による静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 静的リスト |
| リストから削除 | 静的リスト ID | [名前による静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 静的リスト |
| フォームに入力 | フォーム ID | [名前によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByNameUsingGET) | Web フォーム |

`primaryAttributeValueIds`を使用する場合は、`activityTypeIds` フィルターも含める必要があります。 このフィルターには、対応するアセットグループに一致するアクティビティ IDのみを含めることができます。 例えば、Web フォームアセットをフィルタリングする場合、`activityTypeIds`には「フォームに入力」アクティビティタイプ IDのみを含めることができます。

次のリクエストには、`primaryAttributeValueIds` フィルターが含まれています。

```json
{
  "filter": {
    "createdAt": {
      "startAt": "2021-07-01T23:59:59-00:00",
      "endAt": "2021-07-02T23:59:59-00:00"
    },
    "activityTypeIds": [
      2
    ],
    "primaryAttributeValueIds": [
      16,102,95,8
    ]
  }
}
```

`primaryAttributeValueIds` と `primaryAttributeValues` は併用できません。

### primaryAttributeValues オプション {#primaryattributevalues-options}

| アクティビティのタイプ | プライマリ属性値 | 取得エンドポイント | アセットグループ |
| --- | --- | --- | --- |
| データ値を変更 | リードフィールド displayName | [リードを説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| スコアを変更 | リードフィールド displayName | [リードを説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| 進行状況のステータスを変更 | プログラム名 | [ID によるプログラムを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramByIdUsingGET) | マーケティングプログラム |
| リストに追加 | 静的リスト名 | [ID による静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 静的リスト |
| リストから削除 | 静的リスト名 | [ID による静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 静的リスト |
| フォームに入力 | フォーム名 | [ID によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByIdUsingGET) | Web フォーム |

`&lt;program&gt;.&lt;asset&gt;`表記法を使用して、マーケティングプログラム、静的リスト、およびWeb フォームアセットグループの名前を指定します。 例えば、「GL_OP_ALL_2021」プログラムの「MPS Outbound」フォームを「GL_OP_ALL_2021.MPS Outbound」と指定します。

次のリクエストには、`primaryAttributeValues` フィルターが含まれています。

```json
{
  "filter": {
    "createdAt": {
      "startAt": "2021-07-01T23:59:59-00:00",
      "endAt": "2021-07-02T23:59:59-00:00"
    },
    "activityTypeIds": [
      2
    ],
    "primaryAttributeValues": [
      "GL_OP_ALL_2021.MPS Outbound"
    ]
  }
}
```

`primaryAttributeValues`を使用する場合は、`activityTypeIds` フィルターも含める必要があります。 このフィルターには、対応するアセットグループに一致するアクティビティ IDのみを含めることができます。 例えば、Web フォームアセットをフィルタリングする場合、`activityTypeIds`には「フォームに入力」アクティビティタイプ IDのみを含めることができます。

`primaryAttributeValues` と `primaryAttributeValueIds` は併用できません。

## オプション

| パラメーター | データタイプ | 必須 | メモ |
| --- | --- | --- | --- |
| `filter` | オブジェクト | はい | アクセス可能なアクティビティセットに適用されるフィルターを含むオブジェクト。 1つの`createdAt` フィルターのみを含めます。 `activityTypeIds` フィルターを含めることもできます。 書き出しジョブは、結果のアクティビティセットを返します。 |
| `format` | 文字列 | いいえ | 書き出しファイル形式は、CSV、TSV、またはSSVです。 これらの値は、それぞれコンマ区切り、タブ区切り、またはスペース区切りの値を生成します。 デフォルトはCSVです。 |
| `columnHeaderNames` | オブジェクト | いいえ | フィールドと列ヘッダーのキーと値のペアのJSON オブジェクト。 各キーには、書き出しジョブに含まれるフィールドの名前を付ける必要があります。 その値は、そのフィールドの書き出された列ヘッダーを設定します。 |
| `fields` | 配列\[文字列\] | いいえ | エクスポートファイルに含めるフィールドの配列。 デフォルトでは、応答には`marketoGUID`、`leadId`、`activityDate`、`activityTypeId`、`campaignId`、`primaryAttributeValueId`、`primaryAttributeValue`および`attributes`が含まれます。 サブセットを返すには、このリストから`"fields": ["leadId", "activityDate", "activityTypeId"]`などのフィールドを指定します。 `actionResult`を指定して、アクティビティ アクション `("succeeded", "skipped", or "failed")`を含めることもできます。 |

## ジョブの作成

取得するレコードを定義するエクスポート ジョブを作成します。 [書き出しアクティビティ ジョブの作成](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/createExportActivitiesUsingPOST) エンドポイントを使用します。

すべてのジョブには`createdAt` フィルターが必要です。 その`startAt`および`endAt`日時パラメーターは、許可されたアクティビティの作成日の最も早い日付と最も新しい日付を定義します。 関連しないアクティビティタイプを除外するには、オプションの`activityTypeIds` フィルターも含めます。

次のリクエストは、日付範囲内の選択したアクティビティタイプに対してCSV書き出しジョブを作成します。

```http
POST /bulk/v1/activities/export/create.json
```

```json
{
   "format": "CSV",
   "filter": {
      "createdAt": {
         "startAt": "2017-07-01T23:59:59-00:00",
         "endAt": "2017-07-31T23:59:59-00:00"
      },
      "activityTypeIds": [
         1,
         12,
         13
      ]
   }
}
```

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

応答は、`exportId`とステータス「作成済み」を返します。 作成されたジョブはまだ処理キューにありません。

ジョブをキューに追加するには、作成応答から`exportId`を含む[Enqueue Export Activity Job](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/enqueueExportActivitiesUsingPOST) エンドポイントを呼び出します。

```http
POST /bulk/v1/activities/export/{exportId}/enqueue.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Queued",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "format": "CSV"
      }
   ]
}
```

応答ステータスが「キューに入りました」。 ワーカーが使用可能になると、ステータスは「処理中」に変わり、ジョブはMarketoからレコードの集計を開始します。

## ジョブステータスのポーリング

ジョブステータスを取得できるのは、同じ API ユーザによって作成されたジョブのみです。

一括アクティビティ抽出では、ジョブを非同期で処理します。 [Get Export Activity Job Status](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/getExportActivitiesStatusUsingGET) エンドポイントをポーリングして、ジョブがいつ完了したかを判断します。

```http
GET /bulk/v1/activities/export/{exportId}/status.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Completed",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "startedAt": "2017-01-21T11:51:30-08:00",
         "finishedAt": "2017-01-21T12:59:30-08:00",
         "format": "CSV",
         "numberOfRecords": 15423,
         "fileSize": 12342,
         "fileChecksum": "sha256:c16514c7e80fcac5ea055dacae9617fc3c29aff5365e3743071313ce0ed2a815"
      }
   ]
}
```

`status` フィールドは、次のいずれかの値を返します。

- `Created`
- `Queued`
- `Processing`
- `Canceled`
- `Completed`
- `Failed`

## データの取得

ジョブのステータスが「完了」の場合、[書き出しアクティビティファイルを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/getExportActivitiesFileUsingGET) エンドポイントを使用して、書き出したデータを取得します。

```http
GET /bulk/v1/activities/export/{exportId}/file.json
```

応答本文には、ジョブ用に設定された形式のファイルが含まれます。

リクエストされたアクティビティフィールドにデータが含まれていない場合、`null`が対応する書き出しファイル フィールドに表示されます。 次の例は、書き出されたアクティビティデータを示しています。

```json
marketoGUID,leadId,activityDate,activityTypeId,campaignId,primaryAttributeValueId,primaryAttributeValue,attributes
783957693,5414087,2022-02-13T14:06:20Z,104,8497,1670,MembershipTest1,"{""Reason"":""Changed by Smart Campaign MembershipTestCampaignStepChoice.MembershipTestCampaignStepChoiceSetUp action Change Data Value"",""Program Member ID"":3240303,""Acquired By"":true,""Old Status"":""Not in Program"",""New Status ID"":21,""Success"":false,""New Status"":""On List"",""Old Status ID"":20}"
783958220,5414094,2022-02-13T14:08:50Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":6,""Success"":true,""New Status"":""Attended"",""Old Status ID"":1}"
783958306,5414094,2022-02-13T14:09:16Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Attended"",""New Status ID"":6,""Success"":false,""New Status"":""Attended"",""Old Status ID"":6}"
783961924,5316669,2022-02-13T14:27:21Z,104,11614,2333,Nurture Automation,"{""Program Member ID"":3240306,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":27,""Success"":false,""New Status"":""Member"",""Old Status ID"":26}"
```

部分的または再開可能な取得の場合、ファイルエンドポイントは`bytes`範囲のオプションのHTTP `Range` ヘッダーをサポートします。 このヘッダーを省略すると、エンドポイントはファイル全体を返します。 `Range` ヘッダーの使用について詳しくは、[一括抽出](bulk-extract.md)を参照してください。

## ジョブのキャンセル

正しく設定されていないジョブや不要なジョブを停止するには、[書き出しアクティビティ ジョブをキャンセル ](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/cancelExportActivitiesUsingPOST) エンドポイントを呼び出します。

```http
POST /bulk/v1/activities/export/{exportId}/cancel.json
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

応答ステータスは、ジョブがキャンセルされたことを示します。
