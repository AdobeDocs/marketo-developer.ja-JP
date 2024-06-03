---
title: 「リードの一括抽出」
feature: REST API
description: 「リードデータのバッチ抽出。」
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 2%

---


# リードの一括抽出

[バルクリード抽出エンドポイントのリファレンス](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads)

REST API の一括リード抽出セットは、Marketoからリード/人物レコードの大きなセットを取得するためのプログラム的なインターフェイスを提供します。 また、レコードの作成日、最新の更新、静的リストメンバーシップまたはスマートリストメンバーシップに基づいて、リードを増分的に取得するためにも使用できます。 ETL、データウェアハウスおよびアーカイブの目的で、Marketoと 1 つ以上の外部システムとの間でデータを継続的にやり取りする必要があるユースケースに推奨されるインターフェイス。

## 権限

バルクリード抽出 API では、所有している API ユーザーが、読み取り専用リードまたは読み取り/書き込みリードの権限の一方または両方を持つ役割を持っている必要があります。

## フィルター

リードは、様々なフィルターオプションをサポートします。 特定のフィルター（など） `updatedAt`, `smartListName`、および `smartListId` すべてのサブスクリプションにまだロールアウトされていない、追加のインフラストラクチャコンポーネントが必要です。 エクスポートジョブごとに指定できるフィルタータイプは 1 つだけです。

| フィルタータイプ | データタイプ | 注意 |
|---|---|---|
| createdAt | 日付範囲 | メンバーを含む JSON オブジェクトを受け入れます `startAt` および `endAt`. `startAt` ローウォーターマークを表す日時を受け入れる `endAt` ハイウォーターマークを表す日時を受け入れます。 範囲は 31 日以内にする必要があります。 日時は、ミリ秒なしの ISO-8601 形式である必要があります。 このフィルタータイプを持つジョブは、日付範囲内に作成されたすべてのアクセス可能なレコードを返します。 |
| updatedAt* | 日付範囲 | メンバーを含む JSON オブジェクトを受け入れます `startAt` および `endAt`. `startAt` ローウォーターマークを表す日時を受け入れる `endAt` ハイウォーターマークを表す日時を受け入れます。 範囲は 31 日以内にする必要があります。 日時は、ミリ秒なしの ISO-8601 形式である必要があります。 メモ：このフィルターは、標準フィールドの更新のみを反映する、表示されている「updatedAt」フィールドをフィルタリングしません。 このフィルタータイプは、リードのレコードが最新のフィールド更新をいつ行ったかに基づいてフィルタリングします。Jobs このフィルタータイプを使用すると、日付範囲内で最近更新されたアクセス可能なすべてのレコードが返されます。 |
| staticListName | 文字列 | 静的リストの名前を受け入れます。 このフィルタータイプを持つジョブは、ジョブの処理開始時に静的リストのメンバーであるすべてのアクセス可能なレコードを返します。 Get Lists エンドポイントを使用して静的リスト名を取得します。 |
| staticListId | 整数 | 静的リストの ID を受け入れます。 このフィルタータイプを持つジョブは、ジョブの処理開始時に静的リストのメンバーであるすべてのアクセス可能なレコードを返します。 リストの取得エンドポイントを使用して、静的リスト ID を取得します。 |
| smartListName* | 文字列 | スマートリストの名前を受け入れます。 このフィルタ・タイプを持つジョブは、ジョブの処理開始時にスマート・リストのメンバーであるアクセス可能なすべてのレコードを返します。 スマート・リストの取得エンドポイントを使用してスマート・リスト名を取得します。 |
| smartListId* | 整数 | スマートリストの ID を受け入れます。 このフィルタ・タイプを持つジョブは、ジョブの処理開始時にスマート・リストのメンバーであるアクセス可能なすべてのレコードを返します。 「スマート・リストの取得」エンドポイントを使用してスマート・リスト ID を取得します。 |


一部のサブスクリプションでは、フィルタータイプを使用できません。 サブスクリプションで利用できない場合は、リードの書き出しジョブを作成エンドポイントを呼び出すとエラーが発生します（「1035, ターゲットのサブスクリプションでサポートされていないフィルタータイプ」）。 お客様は、Marketo サポートに連絡して、この機能をサブスクリプションで有効にすることができます。

## オプション

書き出しリードジョブの作成エンドポイントには、いくつかの書式設定オプションがあります。ユーザーは、書き出されたファイルに特定のフィールドを含めたり、これらのフィールドの列ヘッダーの名前を変更したり、書き出されたファイルの形式を変更したりできます。

| パラメーター | データタイプ | 必須 | 注意 |
|---|---|---|---|
| フィールド | 配列[文字列] | はい | この fields パラメーターには、文字列の JSON 配列を指定できます。 各文字列は、Marketo リードフィールドの REST API 名である必要があります。 リストされたフィールドは、書き出されたファイルに含まれます。 columnHeader で上書きしない限り、各フィールドの列ヘッダーは各フィールドの REST API 名になります。 メモ：条件 [!DNL Adobe Experience Cloud Audience Sharing] 機能が有効になっている場合は、に関連付けられた cookie 同期プロセスが発生します [!DNL Adobe Experience Cloud] Marketo リード付き ID （ECID）。 「ecid」フィールドを指定して、エクスポートファイルに ECID を含めることができます。 |
| columnHeaderNames | オブジェクト | いいえ | フィールド名と列ヘッダー名のキーと値のペアを含む JSON オブジェクト。 キーは、エクスポートジョブに含まれるフィールドの名前である必要があります。 これは、Describe Lead を呼び出して取得できるフィールドの API 名です。 値は、そのフィールドの書き出された列ヘッダーの名前です。 |
| 形式 | 文字列 | いいえ | CSV、TSV、SSV のいずれかを使用できます。 書き出されたファイルは、コンマ区切り値、タブ区切り値、スペース区切り値の各ファイル（設定されている場合）としてレンダリングされます。 未設定の場合のデフォルト値は CSV です。 |


## ジョブの作成

ジョブのパラメーターは、を使用してエクスポートを開始する前に定義されます [リードエクスポートジョブの作成](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/createExportLeadsUsingPOST) エンドポイント。 を定義する必要があります `fields` 書き出しに必要なパラメーターのタイプ。 `filter`, `format` （ファイル名と列ヘッダー名がある場合）。

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

このリクエストでは、2017 年 1 月 1 日～ 2017 年 1 月 31 日の間に作成された一連のリードのエクスポートが開始され、対応するからの値が含まれます `firstName`, `lastName`, `id`、および `email` フィールド。

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

ジョブが作成されたことを示すステータス応答を返します。 ジョブは定義され作成されましたが、まだ開始されていません。 そのためには、 [リード書き出しジョブをキューに入れる](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/enqueueExportLeadsUsingPOST) エンドポイントは、作成ステータス応答から exportId を使用して呼び出す必要があります。

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

これは、次のように応答します `status` （使用可能なエクスポートスロットがある場合、待機中の場合）は、待機中に設定されます。

## ジョブステータスのポーリング

`Note:` ステータスは、同じ API ユーザーによって作成されたジョブについてのみ取得できます。

これは非同期エンドポイントなので、ジョブを作成した後、そのステータスをポーリングして、進行状況を判断する必要があります。 を使用したポーリング [リード書き出しジョブステータスの取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET) エンドポイント。 ステータスは 60 秒に 1 回だけ更新されるので、これよりも低いポーリング頻度は推奨されず、ほとんどすべての場合で過剰です。 ポーリングについて簡単に見てみましょう。

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

ステータスエンドポイントは、ジョブがまだ処理中であることを示す応答なので、ファイルはまだ取得できません。 ジョブのステータスが「完了」に変わったら、ダウンロードの準備をします。

ステータスフィールドは、次のいずれかの応答を返すことができます。

- 作成日
- キュー
- 処理中
- キャンセル済み
- 完了
- 失敗

## データの取得

完了したリードエクスポートのファイルを取得するには、を呼び出すだけです [リードファイルのエクスポートを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/getExportLeadsFileUsingGET) エンドポイントと `exportId`.

```
GET /bulk/v1/leads/export/{exportId}/file.json
```

応答には、ジョブの設定方法に従ってフォーマットされたファイルが含まれています。 エンドポイントは、ファイルのコンテンツを使用して応答します。

リクエストされたリードフィールドが空（データが含まれていない）の場合、 `null` がエクスポートファイル内の対応するフィールドに配置されます。 次の例では、返されたリードのメールフィールドが空です。

```csv
firstName,lastName,email,cookies
Russell,Wilson,null,_mch-localhost-1536605780000-12105
```

抽出されたデータの部分的で再開にわかりやすい取得をサポートするために、ファイルエンドポイントはオプションでバイト型の HTTP ヘッダー範囲をサポートします。 ヘッダーが設定されていない場合は、コンテンツ全体が返されます。 詳しくは、Marketoでの範囲ヘッダーの使用を参照してください [一括抽出](bulk-extract.md).

## ジョブのキャンセル

ジョブが正しく設定されなかった場合や不要になった場合は、を使用して簡単にキャンセルできます。 [リードジョブの書き出しをキャンセル](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/cancelExportLeadsUsingPOST) エンドポイント：

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

ジョブがキャンセルされたことを示すステータスで応答します。