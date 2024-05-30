---
title: 「一括アクティビティ抽出」
feature: REST API
description: 「Marketoからのアクティビティデータのバッチ処理」
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 7%

---


# 一括アクティビティ抽出

[一括アクティビティ抽出エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/)

REST API の一括アクティビティ抽出セットは、Marketoから大量のアクティビティデータを取得するためのプログラムによるインターフェイスを提供します。  低遅延を必要とせず、CRM 統合、ETL、データウェアハウジング、データアーカイブなど、大量のアクティビティデータをMarketoから転送する必要がある場合。

## 権限

一括アクティビティ抽出 API では、API ユーザーが「読み取り専用アクティビティ」または「読み取り/書き込みアクティビティ」権限を持っている必要があります。

## フィルター

<table>
  <tbody>
    <tr>
      <td>フィルタータイプ</td>
      <td>データタイプ</td>
      <td>必須</td>
      <td>注意</td>
    </tr>
    <tr>
      <td>createdAt</td>
      <td>日付範囲</td>
      <td>はい</td>
      <td>startAt および endAt メンバーを持つ JSON オブジェクトを受け入れます。 startAt には透かし（低）を表す日時を指定し、endAt には透かし（高）を表す日時を指定します。 範囲は 31 日以内である必要があります。このフィルタータイプを使用するジョブは、日付範囲内に作成されたすべてのアクセス可能なレコードを返します。日時はミリ秒なしの ISO-8601 形式である必要があります。</td>
    </tr>
    <tr>
      <td>activityTypeIds</td>
      <td>Array[Integer]</td>
      <td>いいえ</td>
      <td>1 つのメンバー activityTypeIds を持つ JSON オブジェクトを受け入れます。 値は、目的のアクティビティタイプに対応する整数の配列である必要があります。「リードを削除」アクティビティはサポートされていません（ <a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET">削除されたリードの取得</a>代わりに、エンドポイントを使用します）。次を使用して、アクティビティタイプ ID を取得します<a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getActivitiesPagingTokenUsingGET">アクティビティタイプの取得</a>エンドポイント。</td>
    </tr>
    <tr>
      <td>primaryAttributeValueIds</td>
      <td>Array[Integer]</td>
      <td>いいえ</td>
      <td>1 つのメンバーを持つ JSON オブジェクト、primaryAttributeValueIds を受け入れます。 値は、フィルタリングするプライマリ属性を指定する id の配列です。 最大 50 個の ID を指定できます。ID はリードフィールドまたはアセットの一意の ID であり、適切な REST API エンドポイントを呼び出すことで取得できます。 例えば、特定のフォームを「フォームに入力」アクティビティ用にフィルタリングするには、フォーム名をに渡します <a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET">名前によるフォームの取得</a> フォーム ID を取得するエンドポイント。プライマリ属性フィルタリングがサポートされているアクティビティタイプのリストを以下に示します。
        <table>
          <tbody>
            <tr>
              <td>アクティビティのタイプ</td>
              <td>プライマリ属性値 Id</td>
              <td>取得エンドポイント</td>
              <td>アセットグループ</td>
            </tr>
            <tr>
              <td>データ値の変更</td>
              <td>リードフィールド ID</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2">リードの説明</a></td>
              <td>属性名</td>
            </tr>
            <tr>
              <td>スコアの変更</td>
              <td>リードフィールド ID</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2">リードの説明</a></td>
              <td>属性名</td>
            </tr>
            <tr>
              <td>進行状況のステータスの変更</td>
              <td>プログラム ID</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByNameUsingGET">名前によるプログラムの取得</a></td>
              <td>マーケティング プログラム</td>
            </tr>
            <tr>
              <td>リストに追加</td>
              <td>静的リスト ID</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET">名前による静的リストの取得</a></td>
              <td>静的リスト</td>
            </tr>
            <tr>
              <td>リストから削除</td>
              <td>静的リスト ID</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET">名前による静的リストの取得</a></td>
              <td>静的リスト</td>
            </tr>
            <tr>
              <td>フォームの入力</td>
              <td>フォーム ID</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET">名前によるフォームの取得</a></td>
              <td>ウェブフォーム</td>
            </tr>
          </tbody>
        </table>
        primaryAttributeValueIds を使用する場合、activityTypeIds フィルターが存在し、対応するアセットグループに一致するアクティビティ ID のみを含める必要があります。例：web フォームアセットでフィルタリングしている場合、activityTypeIds では「フォームに入力」アクティビティタイプ ID のみを使用できます。例：リクエスト本文：{"filter":{"createdAt":{"startAt": "2021-07-01T2:59:59-00:00","endAt": "2021-07-02T23:59:59-00:00"},"activityTypeIds":[2],"primaryAttributeValueIds" : [16,102,95,8]}}primaryAttributeValueIds と primaryAttributeValues を一緒に使用することはできません。</td>
    </tr>
    <tr>
      <td>primaryAttributeValues</td>
      <td>配列 [ 文字列 ]</td>
      <td>いいえ</td>
      <td>1 つのメンバーを持つ JSON オブジェクト、primaryAttributeValues を受け入れます。 値は、フィルタリングするプライマリ属性を指定する名前の配列です。 最大 50 個の名前を指定できます。名前はリードフィールドまたはアセットの一意の ID であり、適切な REST API エンドポイントを呼び出すことで取得できます。 例えば、特定のフォームを「フォームに入力」アクティビティ用にフィルタリングするには、フォーム ID をに渡します <a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5">Id でフォームを取得</a> フォーム名を取得するエンドポイント。プライマリ属性フィルタリングがサポートされているアクティビティタイプのリストを以下に示します。
        <table>
          <tbody>
            <tr>
              <td>アクティビティのタイプ</td>
              <td>プライマリ属性値</td>
              <td>取得エンドポイント</td>
              <td>アセットグループ</td>
            </tr>
            <tr>
              <td>データ値の変更</td>
              <td>リードフィールド displayName</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2">リードの説明</a></td>
              <td>属性名</td>
            </tr>
            <tr>
              <td>スコアの変更</td>
              <td>リードフィールド displayName</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2">リードの説明</a></td>
              <td>属性名</td>
            </tr>
            <tr>
              <td>進行状況のステータスの変更</td>
              <td>プログラム名</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByIdUsingGET">Id でプログラムを取得</a></td>
              <td>マーケティング プログラム</td>
            </tr>
            <tr>
              <td>リストに追加</td>
              <td>静的リスト名</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET">Id による静的リストの取得</a></td>
              <td>静的リスト</td>
            </tr>
            <tr>
              <td>リストから削除</td>
              <td>静的リスト名</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET">Id による静的リストの取得</a></td>
              <td>静的リスト</td>
            </tr>
            <tr>
              <td>フォームの入力</td>
              <td>フォーム名</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5">Id でフォームを取得</a></td>
              <td>ウェブフォーム</td>
            </tr>
          </tbody>
        </table>
        「&lt;」を使用する必要があります<em>プログラム</em>&gt;.&lt;<em>資産</em>次のアセットグループの名前を一意に指定する &gt;」表記：マーケティングプログラム、静的リスト、web フォーム。例：例：「GL_OP_ALL_2021」という名前のプログラムの下にある「MPS Outbound」という名前のフォームは、「GL_OP_ALL_2021.MPS Outbound」と指定されます。例：リクエスト本文：{"filter":{"createdAt": "202221-07-0 1T23:59:59-00:00","endAt": "2021-07-02T23:59:59-00:00"},"activityTypeIds":[2],"primaryAttributeValues":["GL_OP_ALL_2021.MPS Outbound"]}}primaryAttributeValues を使用する場合、activityTypeIds フィルターが存在し、対応するアセットグループに一致するアクティビティ ID のみを含んでいる必要があります。 例えば、web フォームのアセットをフィルタリングしている場合、activityTypeIds.primaryAttributeValues と primaryAttributeValueIds を一緒に使用することはできません。使用できるアクティビティタイプ ID は「フォームに入力」のみです。</td>
    </tr>
  </tbody>
</table>

## オプション

| パラメーター | データタイプ | 必須 | 注意 |
|---|---|---|---|
| フィルター | 配列[オブジェクト] | はい | フィルターの配列を受け入れます。 配列には、createdAt フィルターを 1 つだけ含める必要があります。 オプションの activityTypeIds フィルターを含めることができます。フィルターはアクセス可能なアクティビティセットに適用され、結果のアクティビティセットはエクスポートジョブによって返されます。 |
| 形式 | 文字列 | いいえ | CSV、TSV、SSV のいずれかを受け入れます。書き出されたファイルは、設定されている場合、それぞれコンマ区切り値、タブ区切り値、スペース区切り値のファイルとしてレンダリングされます。設定されていない場合、デフォルトは CSV です。 |
| columnHeaderNames | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。 キーは、エクスポートジョブに含まれるフィールドの名前である必要があります。 値は、そのフィールドの書き出された列ヘッダーの名前です。 |
| フィールド | 配列[文字列] | いいえ | オプションのフィールド値を含む文字列の配列。 リストに表示されたフィールドは、書き出されたファイルに含まれます。デフォルトでは、次のフィールドが返されます。 `marketoGUIDleadId` `activityDate` `activityTypeId` `campaignId` `primaryAttributeValueId` `primaryAttributeValueattributes`、このパラメーターを使用すると、上記のリストからサブセットを指定することで、返されるフィールドの数を減らすことができます。例：&quot;fields&quot;: [&quot;leadId&quot;, &quot;activityDate&quot;, &quot;activityTypeId&quot;]追加のフィールド「actionResult」を指定して、アクティビティアクション（「succeeded」、「skipped」、「failed」）を含めることができます。 |


## ジョブの作成

レコードを書き出すには、まず取得するジョブとレコードのセットを定義する必要があります。  を使用したジョブの作成 [エクスポートアクティビティジョブを作成](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/createExportActivitiesUsingPOST) エンドポイント。  アクティビティを書き出す場合、2 つの主要なフィルターを適用できます。 `createdAt`（常に必須）、 `activityTypeIds`（オプション）。  createdAt フィルターは、 `startAt` および `endAt` パラメーターは、いずれも datetime フィールドで、許可される最も早い作成日と許可される最も遅い作成日をそれぞれ表します。  オプションで、を使用して、特定のタイプのアクティビティのみをフィルタリングすることもできます `activityTypeIds` フィルター。  これは、ユースケースとは関係のない結果を削除する場合に役立ちます。

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

ジョブのステータスは「作成済み」になりましたが、まだ処理キューにありません。  処理を開始できるようにキューに入れるには、を呼び出す必要があります。 [書き出しアクティビティジョブをエンキュー](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/enqueueExportActivitiesUsingPOST) 作成ステータス応答から exportId を使用しているエンドポイント。

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

これで、ステータスは、ジョブがキューに入れられたことをレポートしています。  このジョブでワーカーが使用可能になると、ステータスが「処理中」に切り替わり、ジョブはMarketoからのレコードの集計を開始します。

## ジョブステータスのポーリング

ジョブステータスは、同じ API ユーザーによって作成されたジョブに対してのみ取得できます。

Marketoの一括アクティビティ抽出は非同期エンドポイントなので、ジョブのステータスをポーリングして、ジョブがいつ完了するかを判断する必要があります。  を使用したポーリング [エクスポートアクティビティジョブステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesStatusUsingGET) エンドポイントを次に示します。

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

ジョブが完了したら、 [書き出しアクティビティファイルを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesFileUsingGET) エンドポイント。

```
GET /bulk/v1/activities/export/{exportId}/file.json
```

応答には、ジョブの設定方法に従ってフォーマットされたファイルが含まれています。 エンドポイントは、ファイルのコンテンツを使用して応答します。

リクエストされたリードフィールドが空（データが含まれていない）の場合、 `then null` がエクスポートファイル内の対応するフィールドに配置されます。  次の例では、返されるアクティビティの campaignId フィールドが空です。

```json
marketoGUID,leadId,activityDate,activityTypeId,campaignId,primaryAttributeValueId,primaryAttributeValue,attributes
783957693,5414087,2022-02-13T14:06:20Z,104,8497,1670,MembershipTest1,"{""Reason"":""Changed by Smart Campaign MembershipTestCampaignStepChoice.MembershipTestCampaignStepChoiceSetUp action Change Data Value"",""Program Member ID"":3240303,""Acquired By"":true,""Old Status"":""Not in Program"",""New Status ID"":21,""Success"":false,""New Status"":""On List"",""Old Status ID"":20}"
783958220,5414094,2022-02-13T14:08:50Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":6,""Success"":true,""New Status"":""Attended"",""Old Status ID"":1}"
783958306,5414094,2022-02-13T14:09:16Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Attended"",""New Status ID"":6,""Success"":false,""New Status"":""Attended"",""Old Status ID"":6}"
783961924,5316669,2022-02-13T14:27:21Z,104,11614,2333,Nurture Automation,"{""Program Member ID"":3240306,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":27,""Success"":false,""New Status"":""Member"",""Old Status ID"":26}"
```

抽出したデータの部分的で再開に適した取得をサポートするために、ファイルエンドポイントではオプションで HTTP ヘッダーをサポートしています `Range` タイプの `bytes`.  ヘッダーが設定されていない場合は、コンテンツ全体が返されます。  Marketoでの範囲ヘッダーの使用について詳しくは、こちらを参照してください [一括抽出](bulk-extract.md).

## ジョブのキャンセル

ジョブが正しく設定されなかった場合や不要になった場合は、を使用して簡単にキャンセルできます。 [書き出しアクティビティジョブをキャンセル](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/cancelExportActivitiesUsingPOST) エンドポイント：

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
