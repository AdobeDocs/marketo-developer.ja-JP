---
title: 一括アクティビティ抽出
feature: REST API
description: Marketoからのアクティビティデータをバッチ処理します。
exl-id: 6bdfa78e-bc5b-4eea-bcb0-e26e36cf6e19
source-git-commit: a5b855691e7fb9e628e2d68fd14a8a6c689d6750
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 7%

---

# 一括アクティビティ抽出

[ 一括アクティビティ抽出エンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/mapi/)

REST API の一括アクティビティ抽出セットは、Marketoから大量のアクティビティデータを取得するためのプログラムによるインターフェイスを提供します。  低遅延を必要とせず、CRM 統合、ETL、データウェアハウジング、データアーカイブなど、大量のアクティビティデータをMarketoから転送する必要がある場合。

## 権限

一括アクティビティ抽出 API では、API ユーザーが「読み取り専用アクティビティ」または「読み取り/書き込みアクティビティ」権限を持っている必要があります。

## フィルター

| フィルタータイプ | データタイプ | 必須 | 注意 |
| --- | --- | --- | --- |
| createdAt | 日付範囲 | はい | `startAt` および `endAt` メンバーを持つ JSON オブジェクトを受け入れます。 `startAt` にはローウォーターマークを表す日時を指定し、`endAt` にはハイウォーターマークを表す日時を指定します。 範囲は 31 日以内にする必要があります。 このフィルタータイプを持つジョブは、日付範囲内に作成されたアクセス可能なすべてのレコードを返します。 日時は、ミリ秒なしの ISO-8601 形式である必要があります。 |
| activityTypeIds | 配列\[Integer\] | いいえ | 1 つのメンバー `activityTypeIds` を持つ JSON オブジェクトを受け入れます。 値は、目的のアクティビティタイプに対応する整数の配列である必要があります。 「リードを削除」アクティビティはサポートされていません（代わりに [ 削除されたリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET) エンドポイントを使用します）。 [Get アクティビティタイプ エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getAllActivityTypesUsingGET) を使用して、アクティビティタイプ ID を取得します。 |
| [primaryAttributeValueIds](#primaryattributevalueids-options) | 配列\[Integer\] | いいえ | 1 つのメンバー `primaryAttributeValueIds` を持つ JSON オブジェクトを受け入れます。 値は、フィルタリングするプライマリ属性を指定する id の配列です。 最大 50 個の ID を指定できます。 ID は、リードフィールドまたはアセットの一意の ID で、適切な REST API エンドポイントを呼び出すことで取得できます。 例えば、特定のフォームを「フォームに入力」アクティビティ用にフィルタリングするには、フォーム名を [ 名前によるフォームを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET) エンドポイントに渡して、フォーム ID を取得します。 プライマリ属性のフィルタリングがサポートされているアクティビティタイプのリストを以下に示します。 |
| [primaryAttributeValues](#primaryattributevalues-options) | 配列\[ 文字列\] | いいえ | 1 つのメンバー `primaryAttributeValues` を持つ JSON オブジェクトを受け入れます。 値は、フィルタリングするプライマリ属性を指定する名前の配列です。 最大 50 個の名前を指定できます。 この名前は、リードフィールドまたはアセットの一意の ID で、適切な REST API エンドポイントを呼び出すことで取得できます。 例えば、特定のフォームを「フォームに入力」アクティビティ用にフィルタリングするには、フォーム ID を [ID でフォームを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) エンドポイントに渡して、フォーム名を取得します。 プライマリ属性のフィルタリングがサポートされているアクティビティタイプのリストを以下に示します。 |

### primaryAttributeValueIds オプション {#primaryattributevalueids-options}

| アクティビティのタイプ | プライマリ属性値 Id | 取得エンドポイント | アセットグループ |
| --- | --- | --- | --- |
| データ値の変更 | リードフィールド ID | [ リードの説明 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| スコアの変更 | リードフィールド ID | [ リードの説明 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| 進行状況のステータスの変更 | プログラム ID | [ 名前によるプログラムの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByNameUsingGET) | マーケティング プログラム |
| リストに追加 | 静的リスト ID | [ 名前による静的リストの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 静的リスト |
| リストから削除 | 静的リスト ID | [ 名前による静的リストの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 静的リスト |
| フォームの入力 | フォーム ID | [ 名前によるフォームの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET) | ウェブフォーム |

`primaryAttributeValueIds` を使用する場合、`activityTypeIds` フィルターが存在し、対応するアセットグループに一致するアクティビティ ID のみを含んでいる必要があります。 例えば、web フォームアセットをフィルタリングしている場合、「フォームに入力」アクティビティタイプ ID のみ `activityTypeIds` で許可されます。

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
| データ値の変更 | リードフィールド displayName | [ リードの説明 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| スコアの変更 | リードフィールド displayName | [ リードの説明 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 属性名 |
| 進行状況のステータスの変更 | プログラム名 | [Id によるプログラムの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByIdUsingGET) | マーケティング プログラム |
| リストに追加 | 静的リスト名 | [Id による静的リストの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 静的リスト |
| リストから削除 | 静的リスト名 | [Id による静的リストの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 静的リスト |
| フォームの入力 | フォーム名 | [Id でフォームを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) | ウェブフォーム |

「&lt;<em>program</em>> を使用する必要があります。マーケティングプログラム、静的リスト、web フォームの &lt;<em>asset</em>>」表記で、アセットグループの名前を指定します。 例えば、「GL_OP_ALL_2021」という名前のプログラムの下にある「MPS Outbound」という名前のフォームは、「GL_OP_ALL_2021.MPS Outbound」と指定されます。

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

`primaryAttributeValues` を使用する場合、`activityTypeIds` フィルターが存在し、対応するアセットグループに一致するアクティビティ ID のみを含んでいる必要があります。 例えば、web フォームのアセットをフィルターしている場合、「フォームに入力」アクティビティタイプ ID のみ `activityTypeIds` で許可されます。 `primaryAttributeValues` と `primaryAttributeValueIds` は併用できません。

## オプション

| パラメーター | データタイプ | 必須 | 注意 |
|---|---|---|---|
| filter | Array[Object] | はい | フィルターの配列を受け入れます。 配列には、1 つの `createdAt` フィルターのみを含める必要があります。 オプションの `activityTypeIds` フィルターを含めることができます。 フィルターはアクセス可能なアクティビティセットに適用され、結果のアクティビティセットはエクスポートジョブによって返されます。 |
| format | 文字列 | いいえ | CSV、TSV、SSV のいずれかを受け入れます。書き出されたファイルは、コンマ区切り値、タブ区切り値、スペース区切り値のファイルとしてレンダリングされます（設定されている場合）。 未設定の場合のデフォルト値は CSV です。 |
| columnHeaderNames | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。 キーは、エクスポートジョブに含まれるフィールドの名前である必要があります。 値は、そのフィールドの書き出された列ヘッダーの名前です。 |
| フィールド | 配列 [ 文字列 ] | いいえ | オプションのフィールド値を含む文字列の配列。 リストされたフィールドは、書き出されたファイルに含まれます。 デフォルトでは、次のフィールドが返されます。 <ul><li>`marketoGUIDleadId`</li><li> `activityDate` </li><li>`activityTypeId` </li><li>`campaignId`</li><li> `primaryAttributeValueId` </li><li>`primaryAttributeValue`</li><li> `attributes`</li></ul>.このパラメーターは、上記のリストからサブセットを指定することで、返されるフィールドの数を減らすために使用できます。`"fields": ["leadId", "activityDate", "activityTypeId"]` 追加のフィールド `actionResult` を指定して、アクティビティ アクション `("succeeded", "skipped", or "failed")` を含めることができます。 |


## ジョブの作成

レコードを書き出すには、まず取得するジョブとレコードのセットを定義する必要があります。  [ エクスポートアクティビティジョブを作成 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/createExportActivitiesUsingPOST) エンドポイントを使用してジョブを作成します。  アクティビティを書き出す場合、適用できる主なフィルターは、常に必須の `createdAt` とオプションの `activityTypeIds` の 2 つです。  `createdAt` フィルターを使用して、アクティビティが作成された日付範囲を定義します。`startAt` パラメーターと `endAt` パラメーターは両方とも datetime フィールドであり、許可される最も早い作成日と許可される最も遅い作成日をそれぞれ表します。  また、オプションで、`activityTypeIds` フィルターを使用して、特定のタイプのアクティビティのみをフィルタリングすることもできます。  これは、ユースケースに関係のない結果を削除する場合に役立ちます。

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

ジョブのステータスは「作成済み」になりましたが、まだ処理キューにありません。  処理を開始できるようにキューに入れるには、作成ステータス応答の exportId を使用して [ エンキューエクスポートアクティビティジョブ ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/enqueueExportActivitiesUsingPOST) エンドポイントを呼び出します。

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

これで、ステータスは、ジョブがキューに入れられたことをレポートしています。  このジョブでワーカーが使用可能になると、ステータスが「処理中」に切り替わり、ジョブがMarketoからのレコードの集計を開始します。

## ジョブステータスのポーリング

ジョブステータスは、同じ API ユーザーによって作成されたジョブに対してのみ取得できます。

Marketoの一括アクティビティ抽出は非同期エンドポイントなので、ジョブのステータスをポーリングして、ジョブがいつ完了するかを判断する必要があります。  [ 書き出しアクティビティのジョブステータスを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesStatusUsingGET) エンドポイントを使用して、次のようにポーリングします。

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

- 作成日
- キュー
- 処理中
- キャンセル済み
- 完了
- 失敗

## データの取得

ジョブが完了したら、[ 書き出しアクティビティファイルを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesFileUsingGET) エンドポイントを使用してデータを取得します。

```
GET /bulk/v1/activities/export/{exportId}/file.json
```

応答には、ジョブの設定方法に従ってフォーマットされたファイルが含まれています。 エンドポイントは、ファイルのコンテンツを使用して応答します。

リクエストされたリードフィールドが空（データを含まない）の場合、`then null` はエクスポートファイルの対応するフィールドに配置されます。  次の例では、返されるアクティビティの `campaignId` フィールドが空です。

```json
marketoGUID,leadId,activityDate,activityTypeId,campaignId,primaryAttributeValueId,primaryAttributeValue,attributes
783957693,5414087,2022-02-13T14:06:20Z,104,8497,1670,MembershipTest1,"{""Reason"":""Changed by Smart Campaign MembershipTestCampaignStepChoice.MembershipTestCampaignStepChoiceSetUp action Change Data Value"",""Program Member ID"":3240303,""Acquired By"":true,""Old Status"":""Not in Program"",""New Status ID"":21,""Success"":false,""New Status"":""On List"",""Old Status ID"":20}"
783958220,5414094,2022-02-13T14:08:50Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":6,""Success"":true,""New Status"":""Attended"",""Old Status ID"":1}"
783958306,5414094,2022-02-13T14:09:16Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Attended"",""New Status ID"":6,""Success"":false,""New Status"":""Attended"",""Old Status ID"":6}"
783961924,5316669,2022-02-13T14:27:21Z,104,11614,2333,Nurture Automation,"{""Program Member ID"":3240306,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":27,""Success"":false,""New Status"":""Member"",""Old Status ID"":26}"
```

抽出されたデータの部分的で再開にわかりやすい取得をサポートするために、ファイルエンドポイントはオプションで `bytes` タイプの HTTP ヘッダー `Range` をサポートします。  ヘッダーが設定されていない場合は、コンテンツ全体が返されます。  Marketoでの範囲ヘッダーの使用について詳しくは、[ 一括抽出 ](bulk-extract.md) を参照してください。

## ジョブのキャンセル

ジョブが正しく設定されなかった場合や、不要になった場合は、[ エクスポートアクティビティジョブをキャンセル ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/cancelExportActivitiesUsingPOST) エンドポイントを使用すると簡単にキャンセルできます。

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
