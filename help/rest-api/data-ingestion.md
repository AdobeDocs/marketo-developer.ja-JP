---
title: データ取り込み
feature: REST API, Dynamic Content
description: Marketo API でのデータの使用。
source-git-commit: 1595aa6df0b0404c7cda2c246c9249018fe87e77
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 12%

---

# データ取得 API

Data Ingestion API は、大量の人物および人物関連データの取り込みを効率的かつ最小限の遅延で処理するように設計された、大容量、低遅延、高可用性のサービスです。

非同期で実行されるリクエストを送信することで、データが取り込まれます。 リクエストのステータスは、[Marketo Observability Data Stream](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-observability-data-stream-setup/) からイベントを登録することで取得できます&#x200B;

インターフェイスは、人物、カスタムオブジェクトの 2 つのオブジェクトタイプで提供されます。 レコード操作は、「挿入または更新」のみです。

データ取り込み API は現在、プライベートベータ版です。  招待者には、[Marketo Engageパフォーマンス層 ](https://nation.marketo.com/t5/product-documents/marketo-engage-performance-tiers/ta-p/328835) パッケージの使用権限が必要です。

## 認証

Data Ingestion API では、Marketo REST API と同じ OAuth 2.0 認証方式を使用してアクセストークンを生成しますが、アクセストークンは HTTP ヘッダー `X-Mkto-User-Token` を使用して渡す必要があります。 クエリパラメーターを使用してアクセストークンを渡すことはできません。

ヘッダーを介したアクセストークンの例：

`X-Mkto-User-Token: 11606815-aa7a-405a-80a1-f9683efa528b:ab`

## 権限

データ取り込みでは、Marketo REST API と同じ権限モデルを使用し、使用するために特別な権限は必要ありませんが、各エンドポイントには特定の権限が必要です。

| エンドポイント | 権限 |
|-|-|
| ユーザー | リード読み取り/書き込み可 |
| カスタムオブジェクト | 読み取り／書き込みカスタムオブジェクト |

## ヘッダー

データ取り込みは、次のカスタム HTTP ヘッダーを利用します。

### リクエスト

| キー | 値 | 必須 | 説明 |
| - | - | - | - |
| X-Correlation-Id | 任意の文字列（最大 255 文字）。 | いいえ | システムを介したリクエストのトレースに使用できます。  Marketo Observability Data Stream を参照してください。 |
| X-Request-Source | 任意の文字列（最大 50 文字）。 | いいえ | システム経由でのリクエストのソースのトレースに使用できます。  Marketo Observability Data Stream を参照してください。 |

### 応答

| キー | 値 | 必須 |
| - | - | - |
| X-Request-Id | 一意のリクエスト ID。 | はい |

## リクエスト

HTTPPOST方式を使用して、サーバーにデータを送信します。

データ表現は、application/json としてリクエスト本文に含まれます。

ドメイン名：`mkto-ingestion-api.adobe.io`

パスは `/subscriptions/MunchkinId` で始まり、MunchkinId はMarketo インスタンスに固有です。 Munchkin ID は、Marketo EngageUI の **管理者**/**マイアカウント**/**サポート情報** で確認できます。  パスの残りの部分は、対象のリソースを指定するために使用されます。

人物の URL の例：

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/persons`

カスタムオブジェクトの URL の例：

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/customobjects/purchases`

### 回答

すべての応答は、`X-Request-Id` ヘッダーを介して一意のリクエスト ID を返します。

ヘッダーを介したリクエスト ID の例：

`X-Request-Id: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### 成功

呼び出しが成功すると、202 ステータスが返されます。  応答本文は返されません。

成功応答の例：

```
HTTP/1.1 202 Accepted
X-Request-Id: e3d92152-0fb1-444a-8f8f-29d5a2338598
Content-Length: 0
Date: Wed, 18 Oct 2023 18:56:49 GMT
```

### エラー

呼び出しでエラーが発生した場合は、202 以外のステータスと、エラーの詳細が追加された応答本文が返されます。  応答本文は application/json で、メンバーが error_code および message の単一のオブジェクトが含まれます。

以下は、Adobe Developer Gateway から再利用されたエラーコードです。

| HTTP ステータスコード | error_code | メッセージ |
| - | - | - |
| 401 | 401013 | Oauth トークンが無効です |
| 403 | 403010 | OAuth トークンがありません |
| 404 | 404040 | リソースが見つかりません |
| 429 | 429001 | サービスの使用制限に達しました |

次に、データ取り込み API に固有の、3 つのセグメントで構成されるエラーコードを示します。  最初の 3 桁はステータス（Adobe Developer Gateway によって返される）で、その後に 0 （ゼロ）が続き、その後に 3 桁が続きます。

| HTTP ステータスコード | error_code | メッセージ |
| - | - | - |
| 400 | 4000801 | リクエストが正しくありません |
| 400 | 4000802 | 無効なデータ |
| 403 | 4030801 | 未認証 |
| 429 | 4290801 | 毎日の割り当てに達しました |
| 500 | 5000801 | 内部サーバーエラー |

## 再試行

一時的なエラーが検出されると、サービスは操作を 3 回再試行します。  最初の再試行は 5 分待ち期間の後に行われ、2 回目は 30 分後に行われ、3 回目は 30 分後に行われます。  再試行は様々な理由で発生します。主に、依存サービスがタイムアウトしたり、一時的に利用できなくなったりした場合です。

## エンドポイント

取り込みエンドポイントは、人物およびカスタムオブジェクトで使用できます。

### ユーザー

人物レコードのアップサートに使用されるエンドポイント。

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
| priority | 文字列 | いいえ | リクエストの優先度：標準または高 | 標準 |
| partitionName | 文字列 | いいえ | ユーザーパーティションの名前 | デフォルト |
| dedupeFields | オブジェクト | いいえ | 重複排除する属性。 1 つまたは 2 つの属性名を使用できます。 <br/> 2 つの属性が AND 操作で使用されます。 例えば、`email` と `firstName` の両方を指定した場合、AND 操作を使用して人物を検索するために両方を使用します。 <br/> サポートされる属性は、`id`、`email`、`sfdcAccountId`、`sfdcContactId`、`sfdcLeadId` `sfdcLeadOwnerId`、カスタム属性（「string」タイプと「integer」タイプのみ）、`email` です。 |
| 人物 | オブジェクトの配列 | はい | 人物の属性名と値のペアのリスト | - |

必要な権限は `Read-Write Lead` です。

### 人物の例

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

カスタムオブジェクトレコードのアップサートに使用するエンドポイント

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
| priority | 文字列 | いいえ | リクエストの優先度：標準、高 | 標準 |
| dedupeBy | 文字列 | いいえ | 重複排除する属性：dedupeFields、marketoGUID | dedupeFields |
| customObjects | オブジェクトの配列 | はい | オブジェクトの属性名と値のペアのリスト。 | - |

必要な権限は `Read-Write Custom Object` です。

リクエストでユーザーへのリンクフィールドが指定されていて、そのユーザーが存在しない場合、再試行が数回行われます。 再試行期間中にそのユーザーが追加された場合（65 分）、更新は成功します。 例えば、リンクフィールドがユーザーのメールであり、ユーザーが存在しない場合、再試行が発生します。

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

* リクエストの最大サイズ : 1 MB
* オブジェクトタイプごとのリクエストあたりの最大オブジェクト数：1,000
* クライアント ID あたりの 1 秒あたりの最大要求数：5,000
* 1 日あたりの最大オブジェクト数：10,000,000

## データ取得 API と REST API の比較

データ取得 API と他のMarketo REST API の違いを以下に示します。

* これは完全な CRUD インターフェイスではなく、アップサートのみをサポートします
* 認証するには、`X-Mkto-User-Token` ヘッダーを使用してアクセストークンを渡す必要があります
* URL ドメイン名は `mkto-ingestion-api.adobe.io` です
* URL パスは `/subscriptions/MunchkinId` で始まります。
* クエリパラメーターがありません
* 呼び出しが成功した場合、202 ステータスが返され、応答本文は空です
* 呼び出しが失敗した場合、202 以外のステータスが返され、応答本文には `{ "error_code" : "Error Code", "message" : "Message" }` が含まれます
* リクエスト ID はヘッダーを介して返 `X-Request-Id` れます
