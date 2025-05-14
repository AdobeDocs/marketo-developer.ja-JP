---
title: プログラムメンバーの一括抽出
feature: REST API
description: メンバーデータ抽出のバッチ処理。
exl-id: 6e0a6bab-2807-429d-9c91-245076a34680
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '1142'
ht-degree: 100%

---

# プログラムメンバーの一括抽出

[プログラムメンバーの一括抽出エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members)

REST API のプログラムメンバーの一括抽出のセットには、Marketo から大量のプログラムメンバーレコードを取得するためのプログラムインターフェイスが用意されています。このインターフェイスは、ETL、データウェアハウス、アーカイブの目的で、Marketo と 1 つ以上の外部システム間で継続的にデータを交換する必要があるユースケースに推奨されます。

## 権限

Bulk Program Member Extract API では、所有する API ユーザに、「読み取り専用リード」権限または「読み取り／書き込みリード」権限のいずれかまたは両方を含むロールを用意する必要があります。

## 説明

「[プログラムメンバーを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2)」は、フィールドが使用可能かどうか、およびこれらのフィールドに関するメタデータに対する、信頼できるプライマリソースです。`name` 属性には REST API 名が含まれます。

```
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

プログラムメンバーは、様々なフィルターオプションをサポートしています。ジョブには複数のフィルタータイプを指定できます。この場合、フィルタータイプは AND 結合されます。`programId` フィルターまたは `programIds` フィルターのいずれかを指定する必要があります。その他のフィルターはすべてオプションです。`updatedAt` フィルターには、まだすべてのサブスクリプションにロールアウトされていない追加のインフラストラクチャコンポーネントが必要です。

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
      <td>プログラムの ID を受け入れます。ジョブは、ジョブの処理開始時点でプログラムのメンバーであるアクセス可能なすべてのレコードを返します。<a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs">プログラムを取得</a>エンドポイントを使用してプログラム ID を取得します。programIds フィルターでは使用できません。</td>
    </tr>
    <tr>
      <td>programIds</td>
      <td>配列[整数]</td>
      <td>最大 10 個のプログラム ID の配列を受け入れます。ジョブは、ジョブの処理開始時点でプログラムのメンバーであるアクセス可能なすべてのレコードを返します。追加フィールド「programId」が最初のフィールドとして書き出しファイルに追加されます。このフィールドは、プログラムメンバーシップレコードが抽出されたプログラムを識別します。<a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs">プログラムを取得</a>エンドポイントを使用してプログラム ID を取得します。programId フィルターでは使用できません。</td>
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
      <td>プログラムメンバーのステータス名の配列を受け入れます。複数のステータス名が OR 結合されます。このフィルタータイプを含むジョブは、プログラムメンバーステータスが指定されたステータス名のいずれかと一致するアクセス可能なすべてのレコードを返します。デフォルトのステータス名とユーザ定義のステータス名の両方を使用できます。statusNames フィルターを「programIds」フィルターと共に使用すると、各プログラムで、ステータスがいずれかのステータス名と一致するメンバーシップレコードが確認されます。いずれのプログラムにもステータス名が見つからない場合は、「1003、無効なデータ」エラーが返されます。
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
              <td>登録解除済み</td>
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
      <td>メンバー startAt と endAt のプロパティを持つ JSON オブジェクトを受け入れます。startAt は、透かし（低）を表す日時を受け取ります。endAt は、透かし（高）を表す日時を受け取ります。範囲は 31日以内にする必要があります。 日時形式は、ミリ秒を含まない ISO-8601 形式にする必要があります。このフィルタータイプのジョブは、日付範囲内で最近更新されたアクセス可能なすべてのレコードを返します。</td>
    </tr>
  </tbody>
</table>

一部のサブスクリプションでは、フィルタータイプは使用できません。サブスクリプションで使用できない場合は、「プログラムメンバー書き出しジョブの作成」エンドポイントを呼び出す際にエラーが発生します（「1035、ターゲットサブスクリプションでサポートされていないフィルタータイプ」）。顧客は、Marketo サポートに連絡して、サブスクリプションでこの機能を有効にすることができます。

## オプション

「プログラムメンバーの書き出しジョブの作成」エンドポイントには、複数の書式設定オプションが用意されています。これらのオプションにより、ユーザは次の操作を実行できます。

- 書き出されたファイル内に含めるフィールドの指定
- これらのフィールドの列ヘッダーの名前の変更
- 書き出すファイルの形式の指定

| パラメーター | データタイプ | 必須 | メモ |
|---|---|---|---|
| フィールド | 配列[文字列] | はい | fields パラメーターは、文字列の JSON 配列を受け入れます。リストされたフィールドは、書き出されたファイルに含まれます。フィールドタイプ `LeadCustom`、`LeadProgram`、MemberCustom、`ProgramMember` を書き出すことができます。「リード 2 を説明」エンドポイントや「プログラムメンバーを説明」エンドポイントを使用して取得できる REST API 名を使用してフィールドを指定します。 |
| columnHeaderNames | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。キーは、書き出しジョブに含まれるフィールドの名前にする必要があります。値は、このフィールドの書き出された列ヘッダーの名前です。 |
| format | 文字列 | いいえ | CSV、TSV、SSV のいずれかを受け入れます。書き出されたファイルは、設定した場合、それぞれコンマ区切り値、タブ区切り値、またはスペース区切り値のファイルとしてレンダリングされます。未設定の場合は、デフォルトで CSV に設定されます。 |


## ジョブの作成

ジョブのパラメーターは、[プログラムメンバーの書き出しジョブを作成](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/createExportProgramMembersUsingPOST)エンドポイントを使用して書き出しを開始する前に定義されます。プログラム ID を含む `filter` と、書き出しに必要な `fields` を定義する必要があります。オプションで、ファイルの `format` と、`columnHeaderNames` を定義できます。

```
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

これにより、ジョブが作成されたことを示すステータス応答が返されます。ジョブは定義および作成されましたが、まだ開始されていません。これを行うには、作成ステータス応答の `exportId` を使用して、[プログラムメンバーの書き出しジョブをキューに入れる](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/enqueueExportProgramMembersUsingPOST)エンドポイントを呼び出す必要があります。

```
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

これは、最初の `status` の &quot;Queued&quot; で応答し、その後、使用可能な書き出しスロットがある場合に &quot;Processing&quot; に設定されます。

## ジョブステータスのポーリング

メモ：ステータスを取得できるのは、同じ API ユーザによって作成されたジョブのみです。

これは非同期エンドポイントなので、ジョブを作成した後、その進行状況を判断するためにこのステータスをポーリングする必要があります。[プログラムメンバーの書き出しジョブのステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET)エンドポイントを使用してポーリングします。ステータスは 60 秒ごとに 1 回しか更新されないので、これより低いポーリング頻度はお勧めしません。ほとんどの場合、それでも過剰です。ステータスフィールドには、作成済み、待機中、処理中、キャンセル済み、完了、失敗のいずれかが返されます。

```
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

ステータスエンドポイントは、ジョブがまだ処理中なので、ファイルはまだ取得できないことを示す応答を返します。ジョブの `status` が「完了」に変更されると、ダウンロードできます。

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

完了したプログラムメンバーの書き出しのファイルを取得するには、`exportId` を使用して[プログラムメンバーの書き出しファイルを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/getExportProgramMembersFileUsingGET)エンドポイントを呼び出すだけです。

応答には、ジョブの設定方法に従って書式設定されたファイルが含まれます。エンドポイントは、ファイルのコンテンツを使用して応答します。リクエストされたプログラムメンバーフィールドが空（データが含まれていない）の場合、書き出しファイル内の対応するフィールドに `null` が配置されます。

```
GET /bulk/v1/program/members/export/{exportId}/file.json
```

```
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

抽出されたデータの部分的で再開にわかりやすい取得をサポートするために、ファイルエンドポイントは、オプションで bytes タイプの HTTP ヘッダー範囲をサポートします。ヘッダーが設定されていない場合は、コンテンツ全体が返されます。Marketo 一括抽出で範囲ヘッダーを使用する方法について詳しくは、[こちら](bulk-extract.md)を参照してください。

## ジョブのキャンセル

ジョブが誤って設定されたり、不要になったりした場合は、[プログラムメンバーの書き出しジョブをキャンセル](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/cancelExportProgramMembersUsingPOST)エンドポイントを使用して簡単にキャンセルできます。

```
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

これは、ジョブがキャンセルされたことを示す `status` で応答します。
