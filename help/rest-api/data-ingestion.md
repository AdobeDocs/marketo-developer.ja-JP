---
title: データ取り込み
feature: REST API, Dynamic Content, Static Lists
description: Marketo Data Ingestion APIを使用すると、ユーザー、カスタムオブジェクト、企業、プログラムメンバー、リストの大量かつ低遅延の取り込みが可能になります。
exl-id: 1d501916-53ac-42d8-a804-abb4ab01c7e8
TQID: https://experienceleague.adobe.com/xby7hs-CSLrVzy-FXEBi1FeU1-ca7vI4kB85BYJ9snk
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 2151
ht-degree: 33%

---

# Data Ingestion API

Data Ingestion APIは、大量、低遅延、高可用性のサービスです。 最小限の遅延で膨大な個人および人関連データを取り込むことができます。

データ収集リクエストは非同期で実行されます。 リクエストのステータスを取得するには、[Marketo Observability Data Stream](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-observability-data-stream-setup)からイベントを購読します。

APIには、次の5つのオブジェクトタイプのインターフェイスが用意されています。

- 個人、カスタムオブジェクト、および会社は、「挿入または更新」操作をサポートしています。
- プログラムメンバーは、「挿入または更新」および削除操作をサポートしています。
- リスト（静的リスト）は、操作の追加と削除をサポートしています。

[Data Ingestion API ドキュメント &#x200B;](https://developer.adobe.com/marketo-apis/api/data-ingestion)を参照してください。

>[!NOTE]
>
>Data Ingestion APIにアクセスするには、[Marketo Engage Performance Tier](https://nation.marketo.com/t5/product-documents/marketo-engage-performance-tiers/ta-p/328835) パッケージの使用権限が必要です。

## 認証

Data Ingestion APIは、Marketo REST APIと同じOAuth 2.0認証方法を使用してアクセストークンを生成します。 `X-Mkto-User-Token` HTTP ヘッダーにアクセストークンを渡します。 クエリパラメーターとして渡すことはできません。

次の例では、ヘッダーにアクセストークンを渡します。

`X-Mkto-User-Token: 11606815-aa7a-405a-80a1-f9683efa528b:ab`

## 権限

Data Ingestionは、Marketo REST API権限モデルを使用します。追加の権限は必要ありません。 次の表に示すように、各エンドポイントには特定の既存の権限が必要です。

| エンドポイント | 権限 |
| --- | --- |
| ユーザ | 読み取り／書き込みリード |
| カスタムオブジェクト | 読み取り／書き込みカスタムオブジェクト |
| 会社 | 読み取り／書き込み企業 |
| プログラムメンバー | 読み取り／書き込みリード |
| リスト | 読み取り／書き込みリード |

## サポートされているオブジェクトタイプ

| オブジェクトのタイプ | サポートされる操作 |
| --- | --- |
| ユーザ | Upsert （挿入または更新） |
| カスタムオブジェクト | Upsert （挿入または更新） |
| 会社 | 同期（`createOnly`、`updateOnly`、`createOrUpdate`） |
| プログラムメンバー | 同期（アップセルステータス）、削除（プログラムから削除） |
| リスト | リストに追加、リストから削除 |

## ヘッダー

データ取り込みは、次のカスタム HTTP ヘッダーをサポートしています。

### リクエスト

| キー | 値 | 必須 | 説明 |
| --- | --- | --- | --- |
| `X-Correlation-Id` | 任意の文字列（最大長 255 文字）。 | いいえ | システムを通じてリクエストを追跡するために使用できます。 「Marketo Observability Data Stream」を参照してください |
| `X-Request-Source` | 任意の文字列（最大長 50 文字）。 | いいえ | システムを通じてリクエストのソースを追跡するために使用できます。 「Marketo Observability Data Stream」を参照してください |

### 応答

| キー | 値 | 必須 |
| --- | --- | --- |
| `X-Request-Id` | 一意のリクエスト ID。 | はい |

## リクエスト

HTTP POST メソッドを使用してサーバーにデータを送信します。

リクエスト本文にapplication/jsonとしてデータを含めます。

ドメイン `mkto-ingestion-api.adobe.io`を使用します。

パスは`/subscriptions/MunchkinId`で始まり、MunchkinIdはMarketo インスタンスに固有です。 Munchkin IDは、Marketo Engage UIの&#x200B;**管理者**/**マイアカウント**/**サポート情報**&#x200B;で確認できます。 パスの残りの部分でリソースを指定します。

ユーザの URL の例：

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/persons`

カスタムオブジェクトの URL の例：

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/customobjects/purchases`

企業のURLの例：

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/companies`

プログラムメンバーのURLの例：

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/programmembers`

リストのURLの例：

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/lists`

### 応答

すべての応答は、`X-Request-Id` ヘッダー内の一意のリクエスト IDを返します。

ヘッダー経由のリクエスト ID の例：

`X-Request-Id: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### 成功

呼び出しが成功すると、ステータス 202が返され、応答本文は返されません。

成功応答の例：

```http
HTTP/1.1 202 Accepted
X-Request-Id: e3d92152-0fb1-444a-8f8f-29d5a2338598
Content-Length: 0
Date: Wed, 18 Oct 2023 18:56:49 GMT
```

### エラー

呼び出しが失敗すると、202以外のステータスと、エラーの詳細が記載された応答本文が返されます。 `application/json`応答本文には、`error_code`および`message`人のメンバーを持つ1つのオブジェクトが含まれています。

次のエラーコードは、Adobe Developer Gatewayから再利用されます。

| HTTP ステータスコード | エラーコード | メッセージ |
| --- | --- | --- |
| 401 | 401013 | OAuth トークンが無効です |
| 403 | 403010 | OAuth トークンがありません |
| 404 | 404040 | リソースが見つかりません |
| 429 | 429001 | サービス使用制限に達しました |

Data Ingestion API固有のエラーコードには、Adobe Developer Gatewayから返される3桁のステータス、ゼロの「0」、および3桁の追加の数字の3つのセグメントが含まれています。

| HTTP ステータスコード | エラーコード | メッセージ |
| --- | --- | --- |
| 400 | 4000801 | リクエストが正しくありません |
| 400 | 4000802 | 無効なデータ |
| 403 | 4030801 | 未認証 |
| 429 | 4290801 | 毎日の割り当て量に達しました |
| 500 | 5000801 | 内部サーバーエラー |

## 再試行

サービスが一時的なエラーを検出すると、操作を再試行します。 再試行は、主に依存サービスがタイムアウトするか、一時的に利用できない場合に発生します。

サービスは、次の再試行間隔を使用します。

- 最初の再試行までの初期操作：5分
- 最初の再試行から2回目の再試行：15分
- 2回目の再試行から3回目の再試行：20分
- 3回目から4回目の再試行：20分
- 4回目から5回目の再試行：2時間
- 5回目の再試行後：3時間

## エンドポイント

取り込みエンドポイントは、個人、カスタムオブジェクト、会社、プログラムメンバーおよびリストに対して使用できます。 各エンドポイントセクションでは、リクエストを定義し、例を示します。

### ユーザ

このエンドポイントを使用して、個人レコードをアップサートします。

| メソッド | パス |
| --- | --- |
| POST | /subscriptions/{munchkinId}/persons |

#### ヘッダー

| キー | 値 |
| --- | --- |
| `Content-Type` | application/json |
| `X-Mkto-User-Token` | {accessToken} |

#### リクエスト本文

| キー | データタイプ | 必須 | 値 | デフォルト値 |
| --- | --- | --- | --- | --- |
| `priority` | 文字列 | いいえ | リクエストの優先度：通常または高 | 通常 |
| `partitionName` | 文字列 | いいえ | 顧客パーティションの名前 | デフォルト |
| `dedupeFields` | オブジェクト | いいえ | 重複排除する属性。 1つまたは2つの属性名を使用できます。<br/> AND 操作では、2 つの属性が使用されます。 例えば、`email` と `firstName` の両方が指定されている場合、AND 操作を使用してユーザを検索するために両方が使用されます。 <br/> サポートされる属性：`id`、`email`、`sfdcAccountId`、`sfdcContactId`、`sfdcLeadId`、`sfdcLeadOwnerId`、カスタム属性（「文字列」および「整数」タイプのみ）、`email` |  |
| `persons` | オブジェクトの配列 | はい | ユーザの属性名と値のペアのリスト | - |

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
         "lastName": "Parker",
         "company": "Karnv"
      },
      {
         "email": "johnny.neal@yvu30.com",
         "firstName": "Johnny",
         "lastName": "Neal",
         "company": "Acme Inc"
      }
   ]
}
```

#### 応答

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### カスタムオブジェクト

このエンドポイントを使用して、カスタムオブジェクトレコードをアップサートします。

| メソッド | パス |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/customobjects/{customObjectAPIName}` |

#### ヘッダー

| キー | 値 |
| --- | --- |
| `Content-Type` | application/json |
| `X-Mkto-User-Token` | {accessToken} |

#### リクエスト本文

| キー | データタイプ | 必須 | 値 | デフォルト値 |
| --- | --- | --- | --- | --- |
| `priority` | 文字列 | いいえ | リクエストの優先度：通常、高 | 通常 |
| `dedupeBy` | 文字列 | いいえ | 重複排除する属性：dedupeFields、marketoGUID | dedupeFields |
| `customObjects` | オブジェクトの配列 | はい | オブジェクトの属性名と値のペアのリスト。 | - |

必須の権限は `Read-Write Custom Object` です。

リクエストでユーザへのリンクフィールドが指定され、そのユーザが存在しない場合は、複数回の再試行が行われます。 再試行ウィンドウ（65 分）内にそのユーザが追加された場合、更新は成功します。 例えば、リンクフィールドがユーザの `email` であり、ユーザが存在しない場合は再試行が行われます。

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

### 会社

このエンドポイントを使用して、会社レコードを同期します。 外部の会社IDまたはMarketoの内部IDによる重複排除を使用して、作成、更新、アップサート操作をサポートします。

| メソッド | パス |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/companies` |

#### ヘッダー

| キー | 値 | 必須 |
| --- | --- | --- |
| `Content-Type` | application/json | ○ |
| `X-Mkto-User-Token` | {accessToken} | はい |
| `X-Correlation-Id` | 任意の文字列（最大長255文字） | いいえ |
| `X-Request-Source` | 任意の文字列（最大長50文字） | いいえ |

#### リクエスト本文

| キー | データタイプ | 必須 | 値 | デフォルト値 |
| --- | --- | --- | --- | --- |
| `action` | 文字列 | いいえ | 同期アクション：`createOnly`、`updateOnly`または`createOrUpdate` | `createOrUpdate` |
| `dedupeBy` | 文字列 | いいえ | 次の場所で重複を除外するフィールド：`dedupeFields`または`idField` （大文字と小文字を区別しない）。 `createOnly`および`createOrUpdate`の場合、`dedupeFields`のみが許可されます。 `updateOnly`の場合、両方が許可されます。 | `dedupeFields` |
| `input` | オブジェクトの配列 | はい | 企業属性の名前と値のペアのリスト。 JSON キー`input`または`companies`を受け入れます。 | - |

`input`配列内の各会社オブジェクトは、次のフィールドをサポートしています。

| キー | データタイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `externalCompanyId` | 文字列 | 条件 | 外部企業ID。 `dedupeBy`が`dedupeFields`の場合は必須です。 `dedupeBy`が`idField`の場合は許可されていません。 |
| `id` | Long | 条件 | Marketoの社内企業ID。 `dedupeBy`が`idField`で`action`が`updateOnly`の場合は必須です。 `dedupeBy`が`dedupeFields`の場合は許可されていません。 |
| `company` | 文字列 | いいえ | 企業名。 |
| （任意のフィールド） | 任意 | いいえ | [会社の説明](companies.md)で定義されている追加の標準またはカスタム会社フィールド。 フィールド名では大文字と小文字が区別されません。 |

必須の権限は `Read-Write Company` です。

### 企業の例

#### リクエスト

`POST /subscriptions/{munchkinId}/companies`

#### ヘッダー

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 本文

```json
{
   "action": "createOrUpdate",
   "dedupeBy": "dedupeFields",
   "input": [
      {
         "externalCompanyId": "ext-company-001",
         "company": "Acme Corporation",
         "industry": "Technology",
         "numberOfEmployees": 5000,
         "annualRevenue": 100000000
      },
      {
         "externalCompanyId": "ext-company-002",
         "company": "Globex Industries",
         "industry": "Manufacturing",
         "numberOfEmployees": 1200
      }
   ]
}
```

#### 応答

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### 企業のIDによる更新の例

```json
{
   "action": "updateOnly",
   "dedupeBy": "idField",
   "input": [
      {
         "id": 12345,
         "company": "Acme Corporation (Renamed)",
         "numberOfEmployees": 5500
      }
   ]
}
```

### 会社の検証ルール

| ルール | 詳細 |
| --- | --- |
| アクション | `createOnly`、`updateOnly`、`createOrUpdate`のいずれかである必要があります。 大文字と小文字を区別。 |
| dedupeBy | `dedupeFields`または`idField`である必要があります（大文字と小文字を区別しません）。 デフォルト値は `dedupeFields` です。 |
| dedupeBy + action | `createOnly`と`createOrUpdate`は`dedupeFields`のみを許可します。 `updateOnly`では、`dedupeFields`と`idField`の両方を使用できます。 |
| `dedupeBy=dedupeFields`の場合 | 各会社には`externalCompanyId`が必要です。 フィールド `id`は存在できません。 |
| `dedupeBy=idField`の場合 | 各会社には`id`が必要です。 フィールド `externalCompanyId`は存在できません。 |
| `input` / `companies` | nullまたは空にすることはできません。 |
| リクエストあたりの最大オブジェクト数 | 1,000 |

### プログラムメンバー（同期）

プログラムメンバーのステータスを同期したり、リードをプログラムに追加したり、プログラムステータスを更新したりするために使用されるエンドポイント。

| メソッド | パス |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/programmembers` |

#### ヘッダー

| キー | 値 | 必須 |
| --- | --- | --- |
| Content-Type | application/json | ○ |
| X-Mkto-User-Token | {accessToken} | ○ |
| X-Correlation-Id | 任意の文字列（最大長255文字） | いいえ |
| X-Request-Source | 任意の文字列（最大長50文字） | いいえ |

#### リクエスト本文

| キー | データタイプ | 必須 | 値 | デフォルト値 |
| --- | --- | --- | --- | --- |
| プログラム | オブジェクトの配列 | はい | プログラム操作のリスト。 それぞれ、プログラム、ターゲットステータス、リードの同期を指定します。 | - |

`programs`配列内の各オブジェクトには、次のものが含まれます。

| キー | データタイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| programId | Long | はい | Marketo プログラム ID。 正の整数にする必要があります。 |
| status | 文字列 | ○ | 設定するプログラム メンバーの状態（例：`"Member"`または`"Influenced"`）。 JSON キー`statusName`または`status`を受け入れます。 値を`"Not in Program"`にすることはできません。代わりに削除エンドポイントを使用してください。 |
| メンバー | オブジェクトの配列 | はい | プログラムに追加または更新するリード参照のリスト。 JSON キー`input`または`members`を受け入れます。 |

`members`配列内の各オブジェクトには、次のものが含まれます。

| キー | データタイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| leadId | Long | はい | Marketoのリード ID。 |
| （任意のフィールド） | 任意 | いいえ | 追加のカスタムプログラムメンバーフィールド。 フィールド名では大文字と小文字が区別されません。 |

必須の権限は `Read-Write Lead` です。

### プログラムメンバーの同期例

#### リクエスト

`POST /subscriptions/{munchkinId}/programmembers`

#### ヘッダー

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 本文

```json
{
   "programs": [
      {
         "programId": 1001,
         "status": "Member",
         "members": [
            {
               "leadId": 10001
            },
            {
               "leadId": 10002
            }
         ]
      },
      {
         "programId": 1002,
         "status": "Influenced",
         "members": [
            {
               "leadId": 10003
            }
         ]
      }
   ]
}
```

#### 応答

`HTTP/1.1 202`
`X-Request-ID: e3d92152-0fb1-444a-8f8f-29d5a2338598`

### プログラムメンバーの同期検証ルール

| ルール | 詳細 |
| --- | --- |
| プログラム | nullまたは空にすることはできません。 |
| programId | 必須。 正の整数にする必要があります。 |
| status | 必須。 空白にすることはできません。 `"Not in Program"`にすることはできません（大文字と小文字を区別しません）。 代わりに、削除エンドポイントを使用してください。 |
| メンバー | nullまたは空にすることはできません。 |
| leadId | 入力配列内の各メンバーに対して必要です。 |
| リクエストあたりの最大リード数 | すべてのプログラムで1,000人のメンバーを獲得。 |

### プログラムメンバー（削除）

プログラムからリードを削除するために使用されるエンドポイント。 これにより、リードのメンバーシップ ステータスが`"Not in Program"`に設定され、そのプログラムからメンバーが削除されます。

>[!NOTE]
>
>このエンドポイントは、リクエストには構造化データを含むJSON本文が必要なため、DELETEではなくPOSTを使用します。

| メソッド | パス |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/programmembers/delete` |

#### ヘッダー

| キー | 値 | 必須 |
| --- | --- | --- |
| Content-Type | application/json | ○ |
| X-Mkto-User-Token | {accessToken} | ○ |
| X-Correlation-Id | 任意の文字列（最大長255文字） | いいえ |
| X-Request-Source | 任意の文字列（最大長50文字） | いいえ |

#### リクエスト本文

| キー | データタイプ | 必須 | 値 | デフォルト値 |
| --- | --- | --- | --- | --- |
| プログラム | オブジェクトの配列 | はい | プログラム削除操作のリスト。 それぞれがプログラムと削除するリードを指定します。 | - |

`programs`配列内の各オブジェクトには、次のものが含まれます。

| キー | データタイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| programId | Long | はい | Marketo プログラム ID。 正の整数にする必要があります。 |
| メンバー | オブジェクトの配列 | はい | プログラムから削除するリード参照のリスト。 JSON キー`input`または`members`を受け入れます。 |

`members`配列内の各オブジェクトには、次のものが含まれます。

| キー | データタイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| leadId | Long | はい | Marketoのリード ID。 |

必須の権限は `Read-Write Lead` です。

### プログラムメンバーの削除例

#### リクエスト

`POST /subscriptions/{munchkinId}/programmembers/delete`

#### ヘッダー

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 本文

```json
{
   "programs": [
      {
         "programId": 1001,
         "members": [
            {
               "leadId": 10001
            },
            {
               "leadId": 10002
            }
         ]
      },
      {
         "programId": 1002,
         "members": [
            {
               "leadId": 10003
            }
         ]
      }
   ]
}
```

#### 応答

`HTTP/1.1 202`
`X-Request-ID: a1b2c3d4-e5f6-7890-abcd-ef1234567890`

### プログラムメンバーが検証ルールを削除

| ルール | 詳細 |
| --- | --- |
| プログラム | nullまたは空にすることはできません。 |
| programId | 必須。 正の整数にする必要があります。 |
| メンバー | nullまたは空にすることはできません。 |
| leadId | 入力配列内の各メンバーに対して必要です。 |
| リクエストあたりの最大リード数 | すべてのプログラムで1,000人のメンバーを獲得。 |

### リスト （リストに追加）

静的リストにリードを追加するために使用されるエンドポイント。 リードは、Marketoのリード IDで識別されます。

| メソッド | パス |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/lists` |

#### ヘッダー

| キー | 値 | 必須 |
| --- | --- | --- |
| `Content-Type` | application/json | ○ |
| `X-Mkto-User-Token` | {accessToken} | はい |
| `X-Correlation-Id` | 任意の文字列（最大長255文字） | いいえ |
| `X-Request-Source` | 任意の文字列（最大長50文字） | いいえ |

#### リクエスト本文

| キー | データタイプ | 必須 | 値 | デフォルト値 |
| --- | --- | --- | --- | --- |
| `listId` | Long | はい | Marketo静的リスト ID。 正の整数にする必要があります。 | - |
| `leads` | オブジェクトの配列 | はい | リストに追加するリード参照のリスト。 JSON キー`input`または`leads`を受け入れます。 | - |

入力配列内の各オブジェクトには、次のものが含まれます。

| キー | データタイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `leadId` | Long | はい | Marketoのリード ID。 JSON キー`leadId`または`id`を受け入れます。 |

必須の権限は `Read-Write Lead` です。

### リストに追加する例

#### リクエスト

`POST /subscriptions/{munchkinId}/lists`

#### ヘッダー

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 本文

```json
{
   "listId": 1001,
   "leads": [
      {
         "leadId": 10001
      },
      {
         "leadId": 10002
      },
      {
         "leadId": 10003
      }
   ]
}
```

#### 応答

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### リストに追加するリストの検証ルール

| ルール | 詳細 |
| --- | --- |
| listId | 必須。 正の整数（> 0）である必要があります。 |
| リード | 必須。 nullまたは空にすることはできません。 |
| leadId | 入力配列内の各リードに必要です。 |
| リクエストあたりの最大リード数 | 1,000件のリードを取得できました。 |

### リスト （リストから削除）

静的リストからリードを削除するために使用されるエンドポイント。 リードは、Marketoのリード IDで識別されます。

>[!NOTE]
>
>このエンドポイントは、リクエストには構造化データを含むJSON本文が必要なため、DELETEではなくPOSTを使用します。

| メソッド | パス |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/lists/remove` |

#### ヘッダー

| キー | 値 | 必須 |
| --- | --- | --- |
| `Content-Type` | application/json | ○ |
| `X-Mkto-User-Token` | {accessToken} | はい |
| `X-Correlation-Id` | 任意の文字列（最大長255文字） | いいえ |
| `X-Request-Source` | 任意の文字列（最大長50文字） | いいえ |

#### リクエスト本文

| キー | データタイプ | 必須 | 値 | デフォルト値 |
| --- | --- | --- | --- | --- |
| `listId` | Long | はい | Marketo静的リスト ID。 正の整数にする必要があります。 | - |
| `leads` | オブジェクトの配列 | はい | リストから削除するリード参照のリスト。 JSON キー`input`または`leads`を受け入れます。 | - |

入力配列内の各オブジェクトには、次のものが含まれます。

| キー | データタイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `leadId` | Long | はい | Marketoのリード ID。 JSON キー`leadId`または`id`を受け入れます。 |

必須の権限は `Read-Write Lead` です。

### リストから削除する例

#### リクエスト

`POST /subscriptions/{munchkinId}/lists/remove`

#### ヘッダー

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 本文

```json
{
   "listId": 1001,
   "leads": [
      {
         "leadId": 10001
      },
      {
         "leadId": 10002
      }
   ]
}
```

#### 応答

`HTTP/1.1 202`
`X-Request-ID: e3d92152-0fb1-444a-8f8f-29d5a2338598`

### リストの検証ルールからリストを削除

| ルール | 詳細 |
| --- | --- |
| listId | 必須。 正の整数（> 0）である必要があります。 |
| リード | 必須。 nullまたは空にすることはできません。 |
| leadId | 入力配列内の各リードに必要です。 |
| リクエストあたりの最大リード数 | 1,000件のリードを取得できました。 |

## 制限

Data Ingestion APIには、次のガードレールがあります。

- 最大リクエストサイズ：1 MB
- 各オブジェクトタイプのリクエストあたりの最大オブジェクト数：1,000
- 各クライアント IDの1秒あたりの最大リクエスト数：5,000
- 1 日あたりの最大オブジェクト数：10,000,000

これらの制限は、個人、カスタムオブジェクト、会社、プログラムメンバー、およびリストに対して一様に適用されます。 プログラムメンバーの場合、「リクエストごとのオブジェクト」は、1回のリクエスト内のすべてのプログラムにわたるリード参照の合計数です。 リストの場合、「リクエストごとのオブジェクト」は、入力配列内のリード参照の数です。

## Data Ingestion API と REST API

Data Ingestion APIは、次の点で他のMarketo REST APIとは異なります。

- `X-Mkto-User-Token` ヘッダーにアクセストークンを渡します。
- `mkto-ingestion-api.adobe.io` ドメインを使用します。
- URL パスを`/subscriptions/MunchkinId`で開始します。
- クエリパラメーターは使用しないでください。
- 呼び出しが成功すると、ステータス 202と空の応答本文が返されます。
- 失敗した呼び出しは、202以外のステータスと`{ "error_code" : "Error Code", "message" : "Message" }`を含む応答本文を返します。
- `X-Request-Id` ヘッダーはリクエスト IDを返します。
