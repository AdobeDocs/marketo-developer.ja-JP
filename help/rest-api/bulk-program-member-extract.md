---
title: プログラムメンバーの一括抽出
feature: REST API
description: Marketo Bulk Program Member Extract REST APIを使用すると、権限やフィールドメタデータを使用して、ETL、データウェアハウス、アーカイブ用の大規模なメンバーレコードをエクスポートできます。
exl-id: 6e0a6bab-2807-429d-9c91-245076a34680
TQID: https://experienceleague.adobe.com/w4qaVTKSe0EORaSiURB6WbJXi29JUdEgfkb2dnfuVFw
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1024
ht-degree: 30%

---

# プログラムメンバーの一括抽出

[一括プログラムメンバー抽出エンドポイントリファレンス](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members)

Bulk プログラムメンバーExtract REST APIは、Marketoから大規模なプログラムメンバーレコードのセットを取得します。 これらのAPIを使用すると、Marketoと外部システム、ETL、データウェアハウス、アーカイブ間で継続的にデータをやり取りできます。

## 権限

API ユーザーには、読み取り専用リード権限、読み取り/書き込みリード権限、またはその両方を持つ役割が必要です。

## 説明

[&#x200B; プログラムメンバーの説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2)を使用して、使用可能なフィールドを決定し、そのメタデータを取得します。 `name`属性にREST API フィールド名が含まれています。

```http
GET /rest/v1/programs/members/describe.json
```

```json
{
    "requestId": "f813#1791563c7cc",
    "result": [
        {
            "name": "API Program Membership",
            "description": "Map for API program membership fields",
            "createdAt": "2021-03-20T01:30:05Z",
            "updatedAt": "2021-03-20T01:30:05Z",
            "dedupeFields": [
                "leadId",
                "programId"
            ],
            "searchableFields": [
                [
                    "leadId"
                ],
                [
                    "myCustomField"
                ],
                [
                    "reachedSuccess"
                ],
                [
                    "statusName"
                ]
            ],
            "fields": [
                {
                    "name": "acquiredBy",
                    "displayName": "acquiredBy",
                    "dataType": "boolean",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "attendanceLikelihood",
                    "displayName": "attendanceLikelihood",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "createdAt",
                    "displayName": "createdAt",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "isExhausted",
                    "displayName": "isExhausted",
                    "dataType": "boolean",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "leadId",
                    "displayName": "leadId",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "membershipDate",
                    "displayName": "membershipDate",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "nurtureCadence",
                    "displayName": "nurtureCadence",
                    "dataType": "string",
                    "length": 4,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "program",
                    "displayName": "program",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "programId",
                    "displayName": "programId",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "reachedSuccess",
                    "displayName": "reachedSuccess",
                    "dataType": "boolean",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "reachedSuccessDate",
                    "displayName": "reachedSuccessDate",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "registrationLikelihood",
                    "displayName": "registrationLikelihood",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "statusName",
                    "displayName": "statusName",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "statusReason",
                    "displayName": "statusReason",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "trackName",
                    "displayName": "trackName",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "updatedAt",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "waitlistPriority",
                    "displayName": "waitlistPriority",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "myCustomField",
                    "displayName": "myCustomField",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "registrationCode",
                    "displayName": "registrationCode",
                    "dataType": "string",
                    "length": 100,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "webinarUrl",
                    "displayName": "webinarUrl",
                    "dataType": "string",
                    "length": 2000,
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

## フィルター

プログラムメンバーの書き出しは、複数のフィルターオプションをサポートしています。 ジョブが複数のフィルタータイプを指定する場合、APIはそれらをAND操作と組み合わせます。

各ジョブは`programId`または`programIds`のいずれかを指定する必要があります。 その他のフィルターはすべてオプションです。 `updatedAt` フィルターには、すべてのサブスクリプションで利用できないインフラストラクチャが必要です。

<table>
  <tbody>
    <tr>
      <td>フィルタータイプ</td>
      <td>データタイプ</td>
      <td>メモ</td>
    </tr>
    <tr>
      <td>programId</td>
      <td>整数</td>
      <td>プログラムの ID を受け入れます。 ジョブは、ジョブが処理を開始する時点でプログラムのメンバーであるすべてのアクセス可能なレコードを返します。<a href="https://developer.adobe.com/marketo-apis/api/asset#tag/Programs"> プログラムを取得</a> エンドポイントを使用してプログラム IDを取得します。programIds フィルターでは使用できません。</td>
    </tr>
    <tr>
      <td>programIds</td>
      <td>配列[整数]</td>
      <td>最大 10 個のプログラム ID の配列を受け入れます。 ジョブは、ジョブが処理を開始する時点でプログラムのメンバーであるすべてのアクセス可能なレコードを返します。追加のフィールド「programId」が、最初のフィールドとしてエクスポートファイルに追加されます。 このフィールドは、プログラムメンバーシップレコードが抽出されたプログラムを識別します。<a href="https://developer.adobe.com/marketo-apis/api/asset#tag/Programs"> プログラムを取得</a> エンドポイントを使用してプログラム IDを取得します。programId フィルターでは使用できません。</td>
    </tr>
    <tr>
      <td>isExhausted</td>
      <td>ブール値</td>
      <td><a href="https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/drip-nurturing/using-engagement-programs/people-who-have-exhausted-content">コンテンツ消費済みの人物</a>のプログラムメンバーシップレコードをフィルタリングするために使用されるブール値を受け入れます。</td>
    </tr>
    <tr>
      <td>nurtureCadence</td>
      <td>文字列</td>
      <td>特定の育成ケイデンスのプログラムメンバーシップレコードをフィルタリングするために使用される文字列を受け入れます。許容値は次のとおりです。
        <ul>
          <li>一時停止 - ケイデンスが一時停止されます</li>
          <li>通常 - ケイデンスは通常です</li>
        </ul></td>
    </tr>
    <tr>
      <td>statusNames</td>
      <td>配列[文字列]</td>
      <td>プログラムメンバーのステータス名の配列を受け入れます。複数のステータス名がOR結合されます。このフィルタータイプを持つジョブは、指定されたステータス名のいずれかにプログラムメンバーのステータスが一致する、アクセス可能なすべてのレコードを返します。デフォルト名とユーザー定義のステータス名の両方を使用できます。statusNames フィルターを「programIds」フィルターと共に使用する場合、各プログラムでステータスがステータス名のいずれかに一致するメンバーシップレコードがチェックされます。いずれかのプログラムでステータス名が見つからない場合は、「1003、無効なデータ」エラーが返されます。
        <table>
          <tbody>
            <tr>
              <td>出席</td>
              <td>オンデマンドで出席</td>
              <td>バウンス</td>
            </tr>
            <tr>
              <td>クリック済み</td>
              <td>問い合わせ済み</td>
              <td>コンバージョン済み</td>
            </tr>
            <tr>
              <td>エンゲージ済み</td>
              <td>入力済みフォーム</td>
              <td>影響</td>
            </tr>
            <tr>
              <td>招待済み</td>
              <td>メンバー</td>
              <td>無断欠席</td>
            </tr>
            <tr>
              <td>プログラム対象外</td>
              <td>リスト掲載あり</td>
              <td>開封済み</td>
            </tr>
            <tr>
              <td>登録済み</td>
              <td>登録中</td>
              <td>登録エラー</td>
            </tr>
            <tr>
              <td>送信済み</td>
              <td>登録済み</td>
              <td>配信停止完了</td>
            </tr>
            <tr>
              <td>表示済み</td>
              <td>訪問済み</td>
              <td>訪問済みのブース</td>
            </tr>
            <tr>
              <td>待機リスト登録済み</td>
              <td>Web コンテンツ</td>
              <td></td>
            </tr>
          </tbody>
        </table></td>
    </tr>
    <tr>
      <td>updatedAt*</td>
      <td>日付範囲</td>
      <td>メンバー startAt と endAt のプロパティを持つ JSON オブジェクトを受け入れます。 startAt は、透かし（低）を表す日時を受け取ります。endAt は、透かし（高）を表す日時を受け取ります。 範囲は 31日以内にする必要があります。 日時形式は、ミリ秒を含まない ISO-8601 形式にする必要があります。このフィルタータイプのジョブは、日付範囲内で最近更新されたアクセス可能なすべてのレコードを返します。</td>
    </tr>
  </tbody>
</table>

一部のサブスクリプションはこのフィルタータイプをサポートしていません。 使用できない場合は、プログラム メンバーの作成ジョブ エンドポイントは`1035, Unsupported filter type for target subscription`を返します。 Marketo サポートに連絡して、サブスクリプションにこの機能をリクエストしてください。

## オプション

「プログラム・メンバーの作成」ジョブ・エンドポイントには、次のオプションがあります。

- 書き出しファイルに含めるフィールドを指定します。
- 書き出した列ヘッダーの名前を変更します。
- 書き出しファイル形式を指定します。

| パラメーター | データタイプ | 必須 | メモ |
| --- | --- | --- | --- |
| フィールド | 配列[文字列] | はい | fields パラメーターは、文字列の JSON 配列を受け入れます。 リストされたフィールドは、書き出されたファイルに含まれます。 フィールドタイプ `LeadCustom`、`LeadProgram`、MemberCustom、`ProgramMember` を書き出すことができます。 それを使用してフィールドを指定するREST API名は、Describe Lead2やDescribe Program Member エンドポイントを使用して取得できます。 |
| columnHeaderNames | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。 キーは、書き出しジョブに含まれるフィールドの名前にする必要があります。 値は、このフィールドの書き出された列ヘッダーの名前です。 |
| format | 文字列 | いいえ | CSV、TSV、SSV のいずれかを受け入れます。 書き出されたファイルは、設定した場合、それぞれコンマ区切り値、タブ区切り値、またはスペース区切り値のファイルとしてレンダリングされます。 未設定の場合は、デフォルトで CSV に設定されます。 |

## ジョブの作成

[書き出しプログラムメンバージョブの作成](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members/operation/createExportProgramMembersUsingPOST) エンドポイントを使用して、書き出しジョブを定義します。 書き出すプログラム IDと`fields`を含む`filter`を指定します。 `format`と`columnHeaderNames`を指定することもできます。

```http
POST /bulk/v1/program/members/export/create.json
```

```json
{
   "format": "CSV",
   "fields": [
        "firstName",
        "lastName",
        "email",
        "membershipDate",
        "program",
        "statusName",
        "leadId",
        "reachedSuccess",
        "leadCustomField01",
        "leadCustomField02",
        "pMCustomField01",
        "pMCustomField02"
   ],
   "filter": {
      "programId":1044
   }
}
```

```json
{
    "requestId": "4d44#16f92734f6e",
    "result": [
        {
            "exportId": "b5ca52a9-5ecb-4966-b5a9-11659a8b4c2b",
            "format": "CSV",
            "status": "Created",
            "createdAt": "2020-01-11T02:33:48Z"
        }
    ],
    "success": true
}
```

応答は、ジョブが作成されたことを確認しますが、書き出しは自動的に開始されません。 返された`exportId`を[Enqueue Export Program Member Job](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members/operation/enqueueExportProgramMembersUsingPOST) エンドポイントに渡して、ジョブを開始します。

```http
POST /bulk/v1/program/members/export/{exportId}/enqueue.json
```

```json
{
    "requestId": "d70b#16f9273ae32",
    "result": [
        {
            "exportId": "b5ca52a9-5ecb-4966-b5a9-11659a8b4c2b",
            "format": "CSV",
            "status": "Queued",
            "createdAt": "2020-01-11T02:33:48Z",
            "queuedAt": "2020-01-11T02:34:13Z"
        }
    ],
    "success": true
}
```

エンキュー応答は、最初に`Queued` ステータスを返します。 書き出しスロットが使用可能になると、ステータスが`Processing`に変わります。

## ジョブステータスのポーリング

同じAPI ユーザーが作成したジョブに対してのみ、ステータスを取得できます。

書き出しは非同期で実行されるので、[書き出しプログラムメンバーのジョブステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET) エンドポイントを使用して、進行状況を調査します。 ステータスは60秒ごとに1回しか更新されないので、より頻繁にポーリングしないでください。

ステータスは`Created`、`Queued`、`Processing`、`Canceled`、`Completed`または`Failed`です。

```http
GET /bulk/v1/program/members/export/{exportId}/status.json
```

```json
{
    "requestId": "9a40#16f9274d250",
    "result": [
        {
            "exportId": "b5ca52a9-5ecb-4966-b5a9-11659a8b4c2b",
            "format": "CSV",
            "status": "Processing",
            "createdAt": "2020-01-11T02:33:48Z",
            "queuedAt": "2020-01-11T02:34:13Z",
            "startedAt": "2020-01-11T02:35:19Z"
        }
    ],
    "success": true
}
```

この応答は、ジョブがまだ処理中であるため、ファイルが利用できないことを示します。 ジョブのステータスが`Completed`に変更されると、ファイルをダウンロードする準備が整います。

```json
{
    "requestId": "11ad1#16f9ff6da23",
    "result": [
        {
            "exportId": "1118dc83-273b-4d44-becb-4d212fece550",
            "format": "CSV",
            "status": "Completed",
            "createdAt": "2020-01-11T02:33:48Z",
            "queuedAt": "2020-01-11T02:34:13Z",
            "startedAt": "2020-01-11T02:35:19Z"
            "finishedAt": "2020-01-11T02:36:12Z",
            "numberOfRecords": 13,
            "fileSize": 1752,
            "fileChecksum": "sha256:b3c8e70e6e501cf1025e345a66b409d4fd07364c7da773cfa68a2b68ce1a7212"
        }
    ],
    "success": true
}
```

## データの取得

完了したプログラムメンバーの書き出しを取得するには、`exportId`を[書き出しプログラムメンバーファイルを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members/operation/getExportProgramMembersFileUsingGET) エンドポイントに渡します。

エンドポイントは、ジョブ用に設定された形式でファイルを返します。 要求されたプログラムメンバーフィールドにデータが含まれていない場合、対応するエクスポートフィールドには`null`が含まれます。

```http
GET /bulk/v1/program/members/export/{exportId}/file.json
```

```text
firstName,lastName,email,Member Date,Program,Status,Lead Id,Success,leadCustomField01,leadCustomField02,pMCustomField01,pMCustomField02
Meera,Reed,mree@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1789,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Jon,Umber,jumb@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1790,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Lyanna,Mormont,lmor@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1791,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Rickon,Stark,rsta@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1792,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Hodor,null,hodor@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1793,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Osha,null,osha@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1794,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Jojen,Reed,Jree@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1795,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Rickard,Karstark,rkar@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1796,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Maester,Luwin,mluw@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1797,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Rodrik,Cassel,rcas@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1798,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Jory,Cassel,jcas@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1799,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Septa,Mordane,smor@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1800,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
```

部分的または再開可能な取得の場合、ファイルエンドポイントは、範囲タイプが`bytes`のオプションのHTTP `Range` ヘッダーをサポートします。 ヘッダーを設定しない場合、エンドポイントはファイル全体を返します。 詳しくは、[一括抽出](bulk-extract.md)を参照してください。

## ジョブのキャンセル

正しく設定されていないジョブや不要になったジョブをキャンセルするには、[&#x200B; プログラム メンバーのエクスポート ジョブをキャンセル &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members/operation/cancelExportProgramMembersUsingPOST) エンドポイントを呼び出します。

```http
POST /bulk/v1/program/members/export/{exportId}/cancel.json
```

```json
{
    "requestId": "bb4f#16f86727f89",
    "result": [
        {
            "exportId": "f0d3520c-3a60-4568-9e71-2e619d3805a4",
            "format": "CSV",
            "status": "Cancelled",
            "createdAt": "2020-01-07T21:47:35Z"
        }
    ],
    "success": true
}
```

応答ステータスは、ジョブがキャンセルされたことを示します。
