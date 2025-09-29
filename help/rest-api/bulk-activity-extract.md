---
title: アクティビティの一括抽出
feature: REST API
description: Marketo Bulk Activity Extract REST API :31 日間の日付範囲、ETL および CRM のアクティビティおよびプライマリ属性フィルターを使用して、大量のアクティビティデータを書き出します。
exl-id: 6bdfa78e-bc5b-4eea-bcb0-e26e36cf6e19
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 94%

---

# アクティビティの一括抽出

[アクティビティの一括抽出エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/)

REST API のアクティビティ一括抽出のセットには、Marketo から大量のアクティビティデータを取得するプログラムインターフェイスが用意されています。低遅延を必要とせず、CRM 統合、ETL、データウェアハウジング、データのアーカイブなど、大量のアクティビティデータを Marketo から転送する必要があるケースの場合。

## 権限

Bulk Activity Extract API では、API ユーザに「読み取り専用アクティビティ」または「読み取り／書き込みアクティビティ」の権限が必要です。

## フィルター

| フィルタータイプ | データタイプ | 必須 | メモ |
| --- | --- | --- | --- |
| createdAt | 日付範囲 | はい | メンバー `startAt` と `endAt` を持つ JSON オブジェクトを受け入れます。`startAt` は透かし（低）を表す日時を受け入れ、`endAt` は透かし（高）を表す日時を受け入れます。範囲は 31日以内にする必要があります。 このフィルタータイプのジョブは、日付範囲内で作成されたアクセス可能なすべてのレコードを返します。日時形式は、ミリ秒を含まない ISO-8601 形式にする必要があります。 |
| activityTypeIds | 配列\[整数\] | いいえ | 1 つのメンバー `activityTypeIds` を持つ JSON オブジェクトを受け入れます。値は、目的のアクティビティタイプに対応する整数の配列にする必要があります。「リードを削除」アクティビティはサポートされていません（代わりに[削除されたリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET)エンドポイントを使用）。[アクティビティタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getAllActivityTypesUsingGET)エンドポイントを使用して、アクティビティタイプ ID を取得します。 |
| [primaryAttributeValueIds](#primaryattributevalueids-options) | 配列\[整数\] | いいえ | 1 つのメンバー `primaryAttributeValueIds` を持つ JSON オブジェクトを受け入れます。値は、フィルタリングするプライマリ属性を指定する ID の配列です。最大 50 個の ID を指定できます。ID は、リードフィールドまたはアセットの一意の ID で、適切な REST API エンドポイントを呼び出すことで取得できます。例えば、「フォームに入力」アクティビティの特定のフォームをフィルタリングするには、フォーム名を[名前によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET)エンドポイントに渡してフォーム ID を取得します。プライマリ属性のフィルタリングがサポートされているアクティビティタイプののリストを以下に示します。 |
| [primaryAttributeValues](#primaryattributevalues-options) | 配列\[文字列\] | いいえ | 1 つのメンバー `primaryAttributeValues` を持つ JSON オブジェクトを受け入れます。値は、フィルタリングするプライマリ属性を指定する名前の配列です。最大 50 個の名前を指定できます。名前は、リードフィールドまたはアセットの一意の ID で、適切な REST API エンドポイントを呼び出すことで取得できます。例えば、「フォームに入力」アクティビティの特定のフォームをフィルタリングするには、フォーム ID を [ID によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5)エンドポイントに渡してフォーム名を取得します。プライマリ属性のフィルタリングがサポートされているアクティビティタイプののリストを以下に示します。 |

### primaryAttributeValueIds オプション {#primaryattributevalueids-options}

| アクティビティのタイプ | プライマリ属性値 ID | 取得エンドポイント | アセットグループ |
| --- | --- | --- | --- |
| データ値を変更 | リードフィールド ID | [リードを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| スコアを変更 | リードフィールド ID | [リードを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| 進行状況のステータスを変更 | プログラム ID | [名前によるプログラムを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByNameUsingGET) | マーケティングプログラム |
| リストに追加 | 静的リスト ID | [名前による静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 静的リスト |
| リストから削除 | 静的リスト ID | [名前による静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 静的リスト |
| フォームに入力 | フォーム ID | [名前によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET) | Web フォーム |

`primaryAttributeValueIds` を使用する際は、`activityTypeIds` フィルターが存在し、対応するアセットグループに一致するアクティビティ ID のみを含める必要があります。例えば、web フォームアセットをフィルタリングする際、`activityTypeIds` では「フォームに入力」アクティビティタイプ ID のみが許可されます。

リクエスト本文の例：

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
| データ値を変更 | リードフィールド displayName | [リードを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| スコアを変更 | リードフィールド displayName | [リードを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| 進行状況のステータスを変更 | プログラム名 | [ID によるプログラムを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByIdUsingGET) | マーケティングプログラム |
| リストに追加 | 静的リスト名 | [ID による静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 静的リスト |
| リストから削除 | 静的リスト名 | [ID による静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 静的リスト |
| フォームに入力 | フォーム名 | [ID によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) | Web フォーム |

「&lt;<em>program</em>>.&lt;<em>asset</em>>」表記を使用して、マーケティングプログラム、静的リスト、web フォームなどのアセットグループの名前を指定する必要があります。例えば、「GL_OP_ALL_2021」という名前のプログラムの下にある「MPS Outbound」という名前のフォームは、「GL_OP_ALL_2021.MPS Outbound」と指定します。

リクエスト本文の例：

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

`primaryAttributeValues` を使用する際は、`activityTypeIds` フィルターが存在し、対応するアセットグループに一致するアクティビティ ID のみを含める必要があります。例えば、web フォームアセットをフィルタリングする際、`activityTypeIds` では「フォームに入力」アクティビティタイプ ID のみが許可されます。`primaryAttributeValues` と `primaryAttributeValueIds` は併用できません。

## オプション

| パラメーター | データタイプ | 必須 | メモ |
|---|---|---|---|
| filter | 配列[オブジェクト] | はい | フィルターの配列を受け入れます。配列には、`createdAt` フィルターを 1 つのみ含める必要があります。オプションの `activityTypeIds` フィルターを含めることができます。アクセス可能なアクティビティセットにフィルターが適用され、結果として得られるアクティビティセットが書き出しジョブによって返されます。 |
| format | 文字列 | いいえ | CSV、TSV、SSV のいずれかを受け入れます。書き出されたファイルは、設定済みの場合、それぞれコンマ区切り値、タブ区切り値、またはスペース区切り値のファイルとしてレンダリングされます。未設定の場合は、デフォルトで CSV に設定されます。 |
| columnHeaderNames | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。キーは、書き出しジョブに含まれるフィールドの名前にする必要があります。値は、このフィールドの書き出された列ヘッダーの名前です。 |
| フィールド | 配列[文字列] | いいえ | フィールド値を含む文字列のオプションの配列。リストされたフィールドは、書き出されたファイルに含まれます。デフォルトでは、次のフィールドが返されます。 <ul><li>`marketoGUIDleadId`</li><li> `activityDate` </li><li>`activityTypeId` </li><li>`campaignId`</li><li> `primaryAttributeValueId` </li><li>`primaryAttributeValue`</li><li> `attributes`</li></ul>.このパラメーターは、上記のリストからサブセットを指定することで、返されるフィールドの数を減らすために使用できます。`"fields": ["leadId", "activityDate", "activityTypeId"]` 追加のフィールド `actionResult` を指定して、アクティビティ アクション `("succeeded", "skipped", or "failed")` を含めることができます。 |

## ジョブの作成

レコードを書き出すには、最初にジョブと、取得するレコードのセットを定義する必要があります。[アクティビティを書き出しジョブを作成](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/createExportActivitiesUsingPOST)エンドポイントを使用してジョブを作成します。アクティビティを書き出す際は、常に必須の `createdAt` とオプションの `activityTypeIds` という 2 つの主なフィルターを適用できます。`createdAt` フィルターは、`startAt` パラメーターと `endAt` パラメーターを使用してアクティビティを作成した日付範囲を定義するのに使用されます。これらのパラメーターは、両方とも日時フィールドで、それぞれ許可される最も早い作成日と最も遅い作成日を表します。また、オプションで、`activityTypeIds` フィルターを使用して、特定のタイプのアクティビティのみをフィルタリングすることもできます。これは、ユースケースに関連しない結果を削除するのに役立ちます。

```
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

ジョブのステータスは「作成済み」になりましたが、まだ処理キューには入っていません。処理を開始できるようにキューに入れるには、作成ステータス応答の exportId を使用して、[アクティビティを書き出しジョブをキューに入れる](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/enqueueExportActivitiesUsingPOST)エンドポイントを呼び出します。

```
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

現在、ステータスはジョブがキューに入れられたことを報告しています。このジョブでワーカーが使用可能になると、ステータスが「処理中」に切り替わり、ジョブは Marketo からのレコードの集計を開始します。

## ジョブステータスのポーリング

ジョブステータスを取得できるのは、同じ API ユーザによって作成されたジョブのみです。

Marketo のアクティビティの一括抽出は非同期エンドポイントなので、ジョブがいつ完了したかを判断するには、ジョブステータスをポーリングする必要があります。次のように、[アクティビティを書き出しジョブのステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesStatusUsingGET)エンドポイントを使用してポーリングします。

```
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

ステータスフィールドは、次のいずれかの値で応答する場合があります。

- 作成済み
- 待機中
- 処理中
- キャンセル済み
- 完了
- 失敗

## データの取得

ジョブが完了したら、[アクティビティを書き出しファイルを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesFileUsingGET)エンドポイントを使用してデータを取得します。

```
GET /bulk/v1/activities/export/{exportId}/file.json
```

応答には、ジョブの設定方法に従って書式設定されたファイルが含まれます。エンドポイントは、ファイルのコンテンツを使用して応答します。

リクエストされたリードフィールドが空（データが含まれていない）の場合、書き出しファイル内の対応するフィールドに `then null` が配置されます。  次の例では、返されるアクティビティの `campaignId` フィールドが空です。

```json
marketoGUID,leadId,activityDate,activityTypeId,campaignId,primaryAttributeValueId,primaryAttributeValue,attributes
783957693,5414087,2022-02-13T14:06:20Z,104,8497,1670,MembershipTest1,"{""Reason"":""Changed by Smart Campaign MembershipTestCampaignStepChoice.MembershipTestCampaignStepChoiceSetUp action Change Data Value"",""Program Member ID"":3240303,""Acquired By"":true,""Old Status"":""Not in Program"",""New Status ID"":21,""Success"":false,""New Status"":""On List"",""Old Status ID"":20}"
783958220,5414094,2022-02-13T14:08:50Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":6,""Success"":true,""New Status"":""Attended"",""Old Status ID"":1}"
783958306,5414094,2022-02-13T14:09:16Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Attended"",""New Status ID"":6,""Success"":false,""New Status"":""Attended"",""Old Status ID"":6}"
783961924,5316669,2022-02-13T14:27:21Z,104,11614,2333,Nurture Automation,"{""Program Member ID"":3240306,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":27,""Success"":false,""New Status"":""Member"",""Old Status ID"":26}"
```

抽出されたデータの部分的で再開にわかりやすい取得をサポートするのに、ファイルエンドポイントは、オプションで `bytes` タイプの HTTP ヘッダー `Range` をサポートします。ヘッダーが設定されていない場合は、コンテンツ全体が返されます。Marketo [一括抽出](bulk-extract.md)で範囲ヘッダーを使用する方法について詳しくは、こちらを参照してください。

## ジョブのキャンセル

ジョブが誤って設定されたり、不要になったりした場合は、[アクティビティを書き出しジョブをキャンセル](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/cancelExportActivitiesUsingPOST)エンドポイントを使用して簡単にキャンセルできます。

```
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

この応答には、ジョブがキャンセルされたことを示すステータスがあります。
