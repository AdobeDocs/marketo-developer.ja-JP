---
title: データ取り込み
feature: REST API, Dynamic Content
description: Marketo API を使用してデータを消費します。
exl-id: 1d501916-53ac-42d8-a804-abb4ab01c7e8
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 99%

---

# Data Ingestion API

Data Ingestion API は、大量のユーザおよびユーザ関連データの取り込みを効率的で最小限の遅延で処理するように設計された、大容量、低遅延、高可用性のサービスです。

データは、非同期で実行されるリクエストを送信することで取り込まれます。リクエストのステータスは、[Marketo Observability Data Stream](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-observability-data-stream-setup) からのイベントをサブスクライブすることで取得できます。

インターフェイスは、ユーザとカスタムオブジェクトの 2 つのオブジェクトタイプに対して提供されます。レコード操作は、「挿入または更新」のみです。

Data Ingestion API は現在プライベートベータ版です。招待者には、[Marketo Engage パフォーマンス階層](https://nation.marketo.com/t5/product-documents/marketo-engage-performance-tiers/ta-p/328835)パッケージの資格が必要です。

## 認証

Data Ingestion API は、Marketo REST API と同じ OAuth 2.0 認証方法を使用してアクセストークンを生成しますが、アクセストークンは HTTP ヘッダー `X-Mkto-User-Token` 経由で渡す必要があります。クエリパラメーター経由でアクセストークンを渡すことはできません。

ヘッダー経由のアクセストークンの例：

`X-Mkto-User-Token: 11606815-aa7a-405a-80a1-f9683efa528b:ab`

## 権限

データ取り込みでは、Marketo REST API と同じ権限モデルが使用され、使用するために追加の特別な権限は必要ありませんが、各エンドポイントには特定の権限が必要です。

| エンドポイント | 権限 |
|-|-|
| ユーザ | 読み取り／書き込みリード |
| カスタムオブジェクト | 読み取り／書き込みカスタムオブジェクト |

## ヘッダー

データ取り込みでは、次のカスタム HTTP ヘッダーが使用されます。

### リクエスト

| キー | 値 | 必須 | 説明 |
| - | - | - | - |
| X-Correlation-Id | 任意の文字列（最大長 255 文字）。 | いいえ | システムを通じてリクエストを追跡するために使用できます。「Marketo Observability Data Stream」を参照してください |
| X-Request-Source | 任意の文字列（最大長 50 文字）。 | いいえ | システムを通じてリクエストのソースを追跡するために使用できます。「Marketo Observability Data Stream」を参照してください |

### 応答

| キー | 値 | 必須 |
| - | - | - |
| X-Request-Id | 一意のリクエスト ID。 | はい |

## リクエスト

HTTP POST メソッドを使用して、データをサーバーに送信します。

データ表現は、リクエスト本文に application/json として含まれます。

ドメイン名：`mkto-ingestion-api.adobe.io`

パスは `/subscriptions/MunchkinId` で始まります。MunchkinId は Marketo インスタンスに固有です。Munchkin ID は、Marketo Engage UI の&#x200B;**管理**／**マイアカウント**／**サポート情報**&#x200B;で確認できます。パスの残りの部分は、対象のリソースを指定するために使用されます。

ユーザの URL の例：

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/persons`

カスタムオブジェクトの URL の例：

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/customobjects/purchases`

### 応答

すべての応答は、`X-Request-Id` ヘッダー経由で一意のリクエスト ID を返します。

ヘッダー経由のリクエスト ID の例：

`X-Request-Id: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### 成功

呼び出しが成功すると、202 ステータスが返されます。応答本文は返されません。

成功応答の例：

```
HTTP/1.1 202 Accepted
X-Request-Id: e3d92152-0fb1-444a-8f8f-29d5a2338598
Content-Length: 0
Date: Wed, 18 Oct 2023 18:56:49 GMT
```

### エラー

呼び出しでエラーが発生した場合、追加のエラー詳細を含む応答本文と共に 202 以外のステータスが返されます。応答本文は application/json で、メンバー error_code と message を持つ単一のオブジェクトが含まれます。

Adobe Developer Gateway から再利用されたエラーコードを以下に示します。

| HTTP ステータスコード | エラーコード | メッセージ |
| - | - | - |
| 401 | 401013 | OAuth トークンが無効です |
| 403 | 403010 | OAuth トークンがありません |
| 404 | 404040 | リソースが見つかりません |
| 429 | 429001 | サービス使用制限に達しました |

Data Ingestion API に一意の、3 つのセグメントで構成されるエラーコードを以下に示します。最初の 3 桁は、ステータス（Adobe Developer Gateway によって返される）で、その後にゼロ「0」が続き、その後に 3 桁の数字が続きます。

| HTTP ステータスコード | エラーコード | メッセージ |
| - | - | - |
| 400 | 4000801 | リクエストが正しくありません |
| 400 | 4000802 | 無効なデータ |
| 403 | 4030801 | 未認証 |
| 429 | 4290801 | 毎日の割り当て量に達しました |
| 500 | 5000801 | 内部サーバーエラー |

## 再試行

一時的なエラーが検出されると、サービスは操作を 3 回再試行します。最初の再試行は 5 分間の待機期間後に行われ、2 回目はさらに 30 分後に行われ、最後に 3 回目はさらに 30 分後に行われます。再試行は様々な理由で発生しますが、主に依存するサービスがタイムアウトになった場合や、一時的に使用できない場合に発生します。

## エンドポイント

取り込みエンドポイントは、ユーザとカスタムオブジェクトに使用できます。

### ユーザ

ユーザレコードのアップサートに使用されるエンドポイント。

| メソッド | パス |
| - | - |
| POST | /subscriptions/{munchkinId}/persons |

#### ヘッダー

| キー | 値 |
| - | - |
| Content-Type | application/json |
| X-Mkto-User-Token | {accessToken} |

#### リクエスト本文

| キー | データタイプ | 必須 | 値 | デフォルト値 |
| - | - | - | - | - |
| priority | 文字列 | いいえ | リクエストの優先度：通常または高 | 通常 |
| partitionName | 文字列 | いいえ | 顧客パーティションの名前 | デフォルト |
| dedupeFields | オブジェクト | いいえ | 重複排除する属性。1 つまたは 2 つの属性名が許可されます。<br/>AND 操作では、2 つの属性が使用されます。例えば、`email` と `firstName` の両方が指定されている場合、AND 操作を使用してユーザを検索するために両方が使用されます。<br/>サポートされている属性：`id`、`email`、`sfdcAccountId`、`sfdcContactId`、`sfdcLeadId` `sfdcLeadOwnerId`、カスタム属性（「文字列」と「整数」タイプのみ）、`email` |
| persons | オブジェクトの配列 | はい | ユーザの属性名と値のペアのリスト | - |

必須の権限は `Read-Write Lead` です。

### ユーザの例

#### リクエスト

`POST /subscriptions/{munchkinId}/persons`

#### ヘッダー

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 本文

```json
{
   "priority": "high",
   "partitionName": "EMEA",
   "dedupeFields": {
      "field1": "email",
      "field2": "firstName"
   },
   "persons":[
      {
         "email": "brooklyn.parker@karnv.com",
         "firstName": "Brooklyn",
         "lastName": "Parker"
      },
      {
         "email": "johnny.neal@yvu30.com",
         "firstName": "Johnny",
         "lastName": "Neal"
      }
   ]
}
```

#### 応答

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### カスタムオブジェクト

カスタムオブジェクトレコードのアップサートに使用されるエンドポイント

| メソッド | パス |
| - | - |
| POST | `/subscriptions/{munchkinId}/customobjects/{customObjectAPIName}` |

#### ヘッダー

| キー | 値 |
| - | - |
| Content-Type | application/json |
| X-Mkto-User-Token | {accessToken} |

#### リクエスト本文

| キー | データタイプ | 必須 | 値 | デフォルト値 |
| - |- | - | - | - |
| priority | 文字列 | いいえ | リクエストの優先度：通常、高 | 通常 |
| dedupeBy | 文字列 | いいえ | 重複排除する属性：dedupeFields、marketoGUID | dedupeFields |
| customObjects | オブジェクトの配列 | はい | オブジェクトの属性名と値のペアのリスト。 | - |

必須の権限は `Read-Write Custom Object` です。

リクエストでユーザへのリンクフィールドが指定され、そのユーザが存在しない場合は、複数回の再試行が行われます。再試行ウィンドウ（65 分）内にそのユーザが追加された場合、更新は成功します。例えば、リンクフィールドがユーザのメールであり、ユーザが存在しない場合は再試行が行われます。

### カスタムオブジェクトの例

#### リクエスト

`POST /subscriptions/{munchkinId}/customobjects/{customObjectAPIName}`

#### ヘッダー

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 本文

```json
{
   "dedupeBy": "dedupeFields",
   "priority": "high",
   "customObjects": [
      {
         "email": "brooklyn.parker@karnv.com",
         "vin": "20UYA31581L000000",
         "make": "BMW",
         "model": "3-Series 330i",
         "year": 2003
      },
      {
         "email": "johnny.neal@yvu30.com",
         "vin": "19UYA31581L000000",
         "make": "BMW",
         "model": "3-Series 325i",
         "year": 1989
      }
   ]
}
```

#### 応答

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

## 制限

ガードレールの使用方法のリストを以下に示します。

* リクエストの最大サイズ：1 MB
* オブジェクトタイプごとのリクエストあたりの最大オブジェクト数：1,000
* クライアント ID ごとの 1 秒あたりの最大リクエスト数：5,000
* 1 日あたりの最大オブジェクト数：10,000,000

## Data Ingestion API と REST API

Data Ingestion API と他の Marketo REST API の違いのリストを以下に示します。

* これは完全な CRUD インターフェイスではなく、アップサートのみをサポートします
* 認証するには、`X-Mkto-User-Token` ヘッダーを使用してアクセストークンを渡す必要があります
* URL ドメイン名は `mkto-ingestion-api.adobe.io`
* URL パスは `/subscriptions/MunchkinId` で始まる
* クエリパラメーターがない
* 呼び出しが成功した場合、202 ステータスが返され、応答本文は空です
* 呼び出しが失敗した場合、202 以外のステータスが返され、応答本文には `{ "error_code" : "Error Code", "message" : "Message" }` が含まれます
* リクエスト ID は `X-Request-Id` ヘッダー経由で返されます
