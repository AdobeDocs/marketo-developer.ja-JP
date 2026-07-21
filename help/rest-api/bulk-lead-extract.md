---
title: リードの一括抽出
feature: REST API
description: Marketo Bulk Lead Extract REST APIを使用して、日付、リスト、スマートリストのフィルター、カスタムフィールド、CSV/TSV形式でリードを一括エクスポートする方法を説明します。
exl-id: 42796e89-5468-463e-9b67-cce7e798677b
TQID: https://experienceleague.adobe.com/4eMJR87fHDdccrVid3wHtspvBVQmrBGHYMlIwFCSdEI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1037
ht-degree: 8%

---

# リードの一括抽出

[リード抽出の一括処理エンドポイント リファレンス](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads)

Bulk Lead Extract REST APIは、Marketoからリード/個人レコードの大規模なセットを取得します。 また、レコード作成日、最新の更新、静的リストメンバーシップ、スマートリストメンバーシップにもとづいて、リードを段階的に取得することもできます。

Bulk Lead Extractを使用すれば、ETL、データウェアハウス、アーカイブワークフローなどのMarketoと外部システムとの間で継続的にデータをやり取りできます。

## 権限

ジョブを所有するAPI ユーザーは、読み取り専用リード権限、読み取り/書き込みリード権限、またはその両方の権限を持つ役割を持っている必要があります。

## フィルター

リード書き出しジョブは、複数のフィルタータイプをサポートしています。 各エクスポートジョブで使用できるフィルタータイプは1つだけです。

`updatedAt`、`smartListName`および`smartListId`のフィルターには、すべてのサブスクリプションで利用できないインフラストラクチャが必要です。

| フィルタータイプ | データタイプ | メモ |
| --- | --- | --- |
| createdAt | 日付範囲 | `startAt`と`endAt`人のメンバーを持つJSON オブジェクト。 `startAt`は透かしの少ない日時で、`endAt`は透かしの多い日時です。 ISO-8601の日付と時刻の値をミリ秒なしで使用します。 範囲は 31日以内にする必要があります。 このジョブは、日付範囲内で作成されたすべてのアクセス可能なレコードを返します。 |
| updatedAt* | 日付範囲 | `startAt`と`endAt`人のメンバーを持つJSON オブジェクト。 `startAt`は透かしの少ない日時で、`endAt`は透かしの多い日時です。 ISO-8601の日付と時刻の値をミリ秒なしで使用します。 範囲は 31日以内にする必要があります。 このフィルターでは、標準フィールドの更新のみを反映する表示可能な`updatedAt` フィールドは使用されません。 その代わりに、最新のフィールド更新時間をリードレコードに使用します。 このジョブは、日付範囲内で最近更新されたすべてのアクセス可能なレコードを返します。 |
| staticListName | 文字列 | 静的リストの名前。 ジョブは、ジョブの処理開始時に、静的リストのメンバーであるアクセス可能なすべてのレコードを返します。 リストの取得エンドポイントを使用して、静的リスト名を取得します。 |
| staticListId | 整数 | 静的リストのID。 ジョブは、ジョブの処理開始時に、静的リストのメンバーであるアクセス可能なすべてのレコードを返します。 リストの取得エンドポイントを使用して、静的リスト IDを取得します。 |
| smartListName* | 文字列 | スマートリストの名前。 ジョブは、ジョブの処理開始時に、スマートリストのメンバーであるアクセス可能なすべてのレコードを返します。 スマートリストの取得エンドポイントを使用して、スマートリスト名を取得します。 |
| smartListId* | 整数 | スマートリストのID。 ジョブは、ジョブの処理開始時に、スマートリストのメンバーであるアクセス可能なすべてのレコードを返します。 スマートリストを取得エンドポイントを使用して、スマートリスト IDを取得します。 |

アスタリスクが付いたフィルタータイプは、一部のサブスクリプションでは使用できません。 サブスクリプションでフィルタータイプが使用できない場合、Create Export Lead Job エンドポイントは「1035, Unsupported filter type for target subscription」というエラーを返します。 Marketo サポートに連絡して、サブスクリプションでこの機能を有効にします。

## オプション

リードジョブの作成エンドポイントには、書き出されたフィールドの選択、列ヘッダーの名前変更、ファイル形式の設定を行うオプションが用意されています。

| パラメーター | データタイプ | 必須 | メモ |
| --- | --- | --- | --- |
| フィールド | 配列[文字列] | はい | 文字列のJSON配列。 各文字列は、Marketo リードフィールドの REST API 名にする必要があります。 書き出しには、リストされた各フィールドが含まれ、`columnHeaderNames`が上書きしない限り、そのREST API名が列ヘッダーとして使用されます。 [!DNL Adobe Experience Cloud Audience Sharing]機能が有効になっている場合、Cookie同期プロセスは[!DNL Adobe Experience Cloud] ID （ECID）をMarketo リードに関連付けます。 書き出しファイルにECIDを含めるには、`ecids` フィールドを指定します。 |
| columnHeaderNames | オブジェクト | いいえ | フィールドと列ヘッダーのキーと値のペアのJSON オブジェクト。 各キーは、書き出しジョブに含まれるフィールドのAPI名である必要があります。 「リードを記述」を呼び出して、API名を取得します。 各値は、そのフィールドの書き出された列ヘッダーです。 |
| format | 文字列 | いいえ | 書き出しファイル形式：コンマ区切り値の場合はCSV、タブ区切り値の場合はTSV、スペース区切り値の場合はSSV。 デフォルトはCSVです。 |

## ジョブの作成

[書き出しリードジョブの作成](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/createExportLeadsUsingPOST) エンドポイントを使用して、書き出しジョブを定義します。 書き出す`fields`、1つの`filter` タイプとそのパラメーター、ファイル `format`、および任意のカスタム列ヘッダー名を指定します。

```http
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
         "endAt": "2017-01-31T00:00:00Z"
      }
   }
}
```

このリクエストは、2017年1月1日から2017年1月31日の間に作成されたリードのエクスポートジョブを作成します。 書き出しには、`firstName`、`lastName`、`id`、および`email` フィールドの値が含まれます。

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

応答は、ジョブが作成されたが開始されていないことを確認します。 ジョブを開始するには、作成応答から`exportId`を含む[Enqueue Export Lead Job](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/enqueueExportLeadsUsingPOST) エンドポイントを呼び出します。

```http
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

エンキュー応答の値は`status`で「キューに入れました」です。 書き出しスロットが使用可能になると、ステータスは「処理中」に変わります。

## ジョブステータスのポーリング

同じAPI ユーザーが作成したジョブに対してのみ、ステータスを取得できます。

リード書き出しジョブは非同期で実行されます。 [Get Export Lead Job Status](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET) エンドポイントをポーリングして、ジョブの進行状況を追跡します。

ステータスは60秒ごとに1回だけ更新されます。 より頻繁に調査しないでください。ほとんどの場合、その間隔はまだ過剰です。

```http
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

この応答は、ジョブがまだ処理中であるため、ファイルが利用できないことを示します。 ジョブのステータスが「完了」に変わると、ファイルをダウンロードする準備が整います。

`status` フィールドは、次のいずれかの値を返すことができます。

- 作成済み
- 待機中
- 処理中
- キャンセル済み
- 完了
- 失敗

## データの取得

完了したリード書き出しを取得するには、[&#x200B; リードファイルの書き出しの取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/getExportLeadsFileUsingGET) エンドポイントに`exportId`を呼び出します。

```http
GET /bulk/v1/leads/export/{exportId}/file.json
```

応答本文には、ジョブ用に設定された形式のファイルが含まれます。

リクエストされたリードフィールドにデータが含まれていない場合、書き出しファイルの対応するフィールドに`null`が含まれます。 次の例では、返されたリードのメールフィールドが空です。

```csv
firstName,lastName,email,cookies
Russell,Wilson,null,_mch-localhost-1536605780000-12105
```

部分的または再開可能な取得の場合、ファイルエンドポイントは、`bytes` タイプのオプションのHTTP `Range` ヘッダーをサポートします。 ヘッダーを設定しない場合、エンドポイントはすべてのコンテンツを返します。 Marketo [一括抽出](bulk-extract.md)での`Range` ヘッダーの使用について詳しくは、こちらを参照してください。

## ジョブのキャンセル

正しく設定されていないジョブまたは不要なジョブをキャンセルするには、[&#x200B; リードジョブのエクスポートをキャンセル &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/cancelExportLeadsUsingPOST) エンドポイントを呼び出します。

```http
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

応答は、ジョブがキャンセルされたことを確認します。
