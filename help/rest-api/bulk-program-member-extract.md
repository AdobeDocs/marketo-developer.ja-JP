---
title: プログラムメンバーの一括抽出
feature: REST API
description: メンバーデータ抽出のバッチ処理。
exl-id: 6e0a6bab-2807-429d-9c91-245076a34680
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 4%

---

# プログラムメンバーの一括抽出

[ プログラムメンバー一括抽出エンドポイント参照 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members)

REST API の Bulk Program Member Extract セットは、Marketoからプログラムメンバーレコードの大きなセットを取得するためのプログラム的なインターフェイスを提供します。 ETL、データウェアハウスおよびアーカイブの目的で、Marketoと 1 つ以上の外部システムとの間でデータを継続的にやり取りする必要があるユースケースでは、このインターフェイスをお勧めします。

## 権限

プログラムメンバーの一括 Extract API では、所有している API ユーザーが、読み取り専用リードまたは読み取り/書き込みリードの権限の一方または両方を持つ役割を持っている必要があります。

## 説明

[ プログラムメンバーの説明 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) は、フィールドの使用や、フィールドに関するメタデータについての主要な情報源です。 `name` 属性には、REST API 名が格納されます。

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

プログラムメンバーは、様々なフィルターオプションをサポートしています。 1 つのジョブに対して複数のフィルタータイプを指定できます。この場合、これらは AND 結合されます。 `programId` または `programIds` フィルターのいずれかを指定する必要があります。 その他のフィルターはすべてオプションです。 `updatedAt` フィルターには、すべてのサブスクリプションにまだロールアウトされていない追加のインフラストラクチャコンポーネントが必要です。

<table>
  <tbody>
    <tr>
      <td>フィルタータイプ</td>
      <td>データタイプ</td>
      <td>注意</td>
    </tr>
    <tr>
      <td>programId</td>
      <td>整数</td>
      <td>プログラムの ID を受け入れます。 ジョブは、ジョブの処理開始時にプログラムのメンバーであった、アクセス可能なすべてのレコードを返します。<a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs"> プログラムの取得 </a> エンドポイントを使用して、プログラム ID を取得します。programIds フィルターと併用することはできません。</td>
    </tr>
    <tr>
      <td>programIds</td>
      <td>Array[Integer]</td>
      <td>最大 10 個のプログラム ID の配列を受け入れます。 ジョブは、ジョブの処理開始時にプログラムのメンバーであったすべてのアクセス可能なレコードを返します。さらに、「programId」というフィールドが、最初のフィールドとしてエクスポートファイルに追加されます。 このフィールドは、プログラム メンバーシップ レコードが抽出されたプログラムを識別します。<a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs"> プログラムの取得 </a> エンドポイントを使用して、プログラム ID を取得します。programId フィルターと共に使用することはできません。</td>
    </tr>
    <tr>
      <td>isExhausted</td>
      <td>ブール値</td>
      <td><a href="https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/drip-nurturing/using-engagement-programs/people-who-have-exhausted-content"> コンテンツを使い果たした人物 </a> のプログラムメンバーシップレコードをフィルタリングするために使用するブール値を受け入れます。</td>
    </tr>
    <tr>
      <td>nurtureCadence</td>
      <td>文字列</td>
      <td>特定の育成ケイデンスのプログラムメンバーシップレコードをフィルタリングするために使用する文字列を受け入れます。指定できる値は次のとおりです。
        <ul>
          <li>一時停止 – ケイデンスが一時停止されました。</li>
          <li>norm - ケイデンスは標準です</li>
        </ul></td>
    </tr>
    <tr>
      <td>statusNames</td>
      <td>配列 [ 文字列 ]</td>
      <td>プログラムメンバーのステータス名の配列を受け入れます。 複数のステータス名が OR で結合されています。このフィルタータイプを持つジョブは、プログラムメンバーステータスが指定されたステータス名のいずれかと一致する、アクセス可能なすべてのレコードを返します。 既定の状態名とユーザー定義の状態名の両方を使用できます。statusNames フィルターを'programIds' フィルターと併用すると、各プログラムは、状態がいずれかの状態名に一致するメンバシップ レコードをチェックします。 プログラムでステータス名が見つからない場合は、「1003, Invalid Data」エラーが返されます。
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
              <td>エンゲージ済</td>
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
              <td>配信登録済み</td>
              <td>登録解除済み</td>
            </tr>
            <tr>
              <td>表示済み</td>
              <td>訪問済み</td>
              <td>訪問済みのブース</td>
            </tr>
            <tr>
              <td>待ちリストにあります</td>
              <td>Web コンテンツ</td>
              <td></td>
            </tr>
          </tbody>
        </table></td>
    </tr>
    <tr>
      <td>updatedAt*</td>
      <td>日付範囲</td>
      <td>startAt および endAt メンバーを持つ JSON オブジェクトを受け入れます。 startAt には透かし（低）を表す日時を指定し、endAt には透かし（高）を表す日時を指定します。 範囲は 31 日以内にする必要があります。 日時は、ミリ秒を含まない ISO-8601 形式である必要があります。このフィルタータイプを使用するジョブは、日付範囲内で最近更新された、アクセス可能なすべてのレコードを返します。</td>
    </tr>
  </tbody>
</table>

一部のサブスクリプションでは、フィルタータイプを使用できません。 サブスクリプションで利用できない場合は、エクスポートプログラムメンバージョブを作成エンドポイントを呼び出すとエラーが発生します（「1035、ターゲットサブスクリプションでサポートされていないフィルタータイプ」）。 お客様は、Marketo サポートに連絡して、この機能をサブスクリプションで有効にすることができます。

## オプション

「書き出しプログラムメンバージョブの作成」エンドポイントには、複数の書式設定オプションが用意されています。 これらのオプションを使用すると、ユーザーは次のことができます。

- 書き出されたファイルに含めるフィールドを指定
- これらのフィールドの列ヘッダーの名前を変更
- 書き出すファイルの形式を指定

| パラメーター | データタイプ | 必須 | 注意 |
|---|---|---|---|
| フィールド | 配列 [ 文字列 ] | はい | この fields パラメーターには、文字列の JSON 配列を指定できます。 リストされたフィールドは、書き出されたファイルに含まれます。 次のフィールド タイプをエクスポートできます：`LeadCustom` `LeadProgram` MemberCustom `ProgramMember`。 REST API 名を使用してフィールドを指定します。この API 名は、リード 2 を説明および/またはプログラムメンバーを説明エンドポイントを使用して取得できます。 |
| columnHeaderNames | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。 キーは、エクスポートジョブに含まれるフィールドの名前である必要があります。 値は、そのフィールドの書き出された列ヘッダーの名前です。 |
| 形式 | 文字列 | いいえ | CSV、TSV、SSV のいずれかを使用できます。 書き出されたファイルは、コンマ区切り値、タブ区切り値、スペース区切り値の各ファイル（設定されている場合）としてレンダリングされます。 未設定の場合のデフォルト値は CSV です。 |


## ジョブの作成

ジョブのパラメーターは、[ エクスポートプログラムメンバージョブを作成 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/createExportProgramMembersUsingPOST) エンドポイントを使用してエクスポートを開始する前に定義されます。 プログラム ID を含む `filter` と、書き出しに必要な `fields` を定義する必要があります。 オプションで、ファイルの `format` と `columnHeaderNames` を定義できます。

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

ジョブが作成されたことを示すステータス応答を返します。 ジョブは定義され作成されましたが、まだ開始されていません。 これを行うには、作成ステータス応答の `exportId` を使用して [ エンキュー書き出しプログラムメンバージョブ ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/enqueueExportProgramMembersUsingPOST) エンドポイントを呼び出す必要があります。

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

これにより、最初の `status` が「Queued」で応答し、使用可能なエクスポートスロットがある場合は「Processing」に設定されます。

## ジョブステータスのポーリング

注意：ステータスは、同じ API ユーザーによって作成されたジョブに対してのみ取得できます。

これは非同期エンドポイントなので、ジョブを作成した後、そのステータスをポーリングして、進行状況を判断する必要があります。 [ 書き出しプログラムメンバージョブステータスの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET) エンドポイントを使用してポーリングします。 ステータスは 60 秒に 1 回だけ更新されるので、これよりも低いポーリング頻度は推奨されず、ほとんどすべての場合で過剰です。 ステータスフィールドは、作成済み、待機中、処理中、キャンセル済み、完了、失敗のいずれかの応答を返すことができます。

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

ステータスエンドポイントは、ジョブがまだ処理中であることを示す応答なので、ファイルはまだ取得できません。 ジョブ `status` が「完了」に変わると、ダウンロードできるようになります。

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

完了したプログラムメンバーエクスポートのファイルを取得するには、`exportId` で [ エクスポートプログラムメンバーファイルを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/getExportProgramMembersFileUsingGET) エンドポイントを呼び出すだけです。

応答には、ジョブの設定方法に従ってフォーマットされたファイルが含まれています。 エンドポイントは、ファイルのコンテンツを使用して応答します。 要求されたプログラムメンバーフィールドが空（データが含まれていない）の場合、`null` はエクスポートファイルの対応するフィールドに配置されます。

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

抽出されたデータの部分的で再開にわかりやすい取得をサポートするために、ファイルエンドポイントはオプションでバイト型の HTTP ヘッダー範囲をサポートします。 ヘッダーが設定されていない場合は、コンテンツ全体が返されます。 Marketoでの範囲ヘッダーの使用について詳しくは、[ 一括抽出 ](bulk-extract.md) を参照してください。

## ジョブのキャンセル

ジョブが正しく設定されなかった場合や不要になった場合は、[ 書き出しプログラムメンバージョブをキャンセル ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/cancelExportProgramMembersUsingPOST) エンドポイントを使用して簡単にキャンセルできます。

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

ジョブがキャンセルされたことを示す `status` が返されます。
