---
title: 重点顧客リスト
feature: REST API
description: クエリ、作成、更新、削除する権限、フィールド、フィルタリング、エンドポイントなど、REST APIを使用してMarketoの名前付きアカウントリストを管理する方法について説明します。
exl-id: 98f42780-8329-42fb-9cd8-58e5dbea3809
TQID: https://experienceleague.adobe.com/18lMhheW21Gz1-3TMHwleHhmLTOqJsZSQ5aqkbbchhM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 686
ht-degree: 36%

---

# 重点顧客リスト

[名前付きアカウントリストのエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi#tag/Named-Account-Lists)

[名前付きアカウントリスト &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/target-account-management/target/account-lists)は、Marketoの名前付きアカウントのコレクションです。 分類、データエンリッチメント、スマートキャンペーンのフィルタリングに使用できます。

名前付きアカウントリスト APIを使用すると、リストアセットとそのメンバーシップをリモートで管理できます。
`Content`

## 権限

必要な権限は、操作によって異なります。

- 名前付きアカウントリストのクエリ：読み取り専用の名前付きアカウントリストまたは読み取り/書き込みの名前付きアカウントリスト。
- リストの作成、更新、または削除：名前付きアカウントリストの読み取りと書き込み。
- クエリリストメンバーシップ：読み取り専用の名前付きアカウントまたは読み取り/書き込み可能な名前付きアカウント。
- リスト メンバーシップの管理：読み取り/書き込み指定アカウント。

## モデル

名前付きアカウントリストには、標準フィールドのセットが限られており、カスタムフィールドはサポートされていません。
`Named Account List Field`

| 名前 | データタイプ | 更新可能 | メモ |
| --- | --- | --- | --- |
| marketoGUID | 文字列 | False | 重点顧客リストの一意の文字列識別子。 このフィールドは、システムで管理され、レコードを作成する際にフィールドとして使用できません。 作成または更新の実行時に &quot;dedupeBy&quot;:&quot;idField&quot; によって使用されるフィールド。 |
| name | 文字列 | True | リストの名前。 作成または更新の実行時に &quot;dedupeBy&quot;:&quot;dedupeFields&quot; によって使用されるフィールド。 |
| createdAt | 日時 | False | リストの作成日時。 このフィールドは、システムで管理され、レコードを作成または更新する際にフィールドとして使用できません。 |
| updatedAt | 日時 | False | リストの最新の更新日時。 このフィールドは、システムで管理され、レコードを作成または更新する際にフィールドとして使用できません。 |
| タイプ | 文字列 | False | リストのタイプ。 &quot;default&quot; または &quot;external&quot;のいずれかの値を指定できます。 外部リストは、CRM アカウントビューで作成されたリストです。 |

## クエリ

名前付きアカウントリストクエリは、「dedupeFields」と「idField」の2つのfilterTypeをサポートしています。 `filterType` クエリパラメーターのフィールドを設定し、`filterValues as`の値をコンマ区切りのリストとして指定します。

`nextPageToken`および`batchSize` フィルターはオプションです。

```http
GET /rest/v1/namedAccountLists.json?filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fb,dff23271-f996-47d7-984f-f2676861b5fc
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "seq": 0,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
         "name": "Saas List",
         "createdAt": "xxxxxxxx",
         "updatedAt": "xxxxxxxx",
         "type": "default",
         "updateable": true
      },
      {
         "seq": 1,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fc",
         "name": "My Account List",
         "createdAt": "xxxxxxxx",
         "updatedAt": "xxxxxxxx",
         "type": "default",
         "updateable": true
      }
   ]
}
```

## 作成と更新

標準のリードデータベースパターンを使用して、名前付きアカウントリストレコードを作成および更新します。 名前付きアカウントリストには、更新可能なフィールドが1つしかありません：`name`。

エンドポイントは、「createOnly」と「updateOnly」の2つの標準アクションタイプをサポートしています。 `action defaults` は &quot;createOnly&quot; です。

アクションが`updateOnly`の場合、オプションの`dedupeBy parameter`を指定できます。 許可される値は、「dedupeFields」で、「name」に対応し、「idField」で、「marketoGUID」に対応します。

`createOnly` モードでは、`dedupeBy` フィールドとして &quot;name&quot; のみが指定できます。 一度に最大 300 個のレコードを送信できます。

```http
POST /rest/v1/namedAccountLists.json
```

```json
{
   "action": "createOnly",
   "dedupeBy": "dedupeFields",
   "input": [
      {
         "name": "SAAS List"
      },
      {
         "name": "Manufacturing (Domestic)"
      }
   ]
}
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "seq": 0,
         "status": "created",
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq": 1,
         "status": "created",
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fc"
      }
   ]
}
```

## 削除

リストの`name`または`marketoGUID`のいずれかを使用して、名前付きアカウントリストを削除します。 キーを選択するには、リクエストの`deleteB` メンバーのnameに「dedupeFields」を、marketoGUIDに「idField」を渡します。

unsetの場合、値はデフォルトでdedupeFieldsになります。 一度に最大 300 個のレコードを削除できます。

```http
POST /rest/v1/namedAccountLists/delete.json
```

```json
{
   "deleteBy": "dedupeFields",
   "input": [
      {
         "name": "Saas List"
      },
      {
         "name": "B2C List"
      },
      {
         "name": "Launchpoint Partner List"
      }
   ]
}
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "seq": 0,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
         "status": "deleted"
      },
      {
         "seq": 1,
         "id": "dff23271-f996-47d7-984f-f2676861b5fc",
         "status": "deleted"
      },
      {
         "seq": 2,
         "status": "skipped",
         "reasons": [
            {
               "code": "1013",
               "message": "Record not found"
            }
         ]
      }
   ]
}
```

キーのレコードが見つからない場合、対応する結果項目には「スキップ」の`status`があります。 また、失敗を説明するコードとメッセージを含む理由も含まれます。

## メンバーシップの管理

### クエリメンバーシップ

アカウントリストの`i`を指定して、名前付きアカウントリストメンバーシップをクエリします。 オプションのパラメーターは次のとおりです。

- `field` – 応答レコードに含めるフィールドのコンマ区切りリスト
- `nextPageToke` – 結果セットをページングする場合
- `batchSiz` – 返すレコードの数を指定します

`field` が未設定の場合は、`marketoGUI`、`nam`、`createdA`、`updatedA` が返されます。 `batchSiz` の最大値とデフォルト値は 300 です。

```http
GET /rest/v1/namedAccountList/{id}/namedAccounts.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "seq": 0,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
         "name": "Saas List",
         "createdAt": "2017-02-01T00:00:00Z",
         "updatedAt": "2017-03-05T17:21:15Z"
      },
      {
         "seq": 1,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fc",
         "name": "My Account List",
         "createdAt": "2017-02-01T00:00:00Z",
         "updatedAt": "2017-03-05T17:21:15Z"
      }
   ]
}
```

### メンバーの追加

MarketoGUIDを使用して、名前付きアカウントリストに名前付きアカウントを追加します。 一度に最大 300 個のレコードを追加できます。

```http
POST /rest/v1/namedAccountList/{id}/namedAccounts.json
```

```json
{
    "input": [
        {
             "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
        },
        {
             "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
        }
    ]
}
```

```json
{
    "requestId": "string",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
            "status": "added"
        },
        {
            "seq": 1,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
            "status": "added"
        }
    ],
    "success": true,
}
```

### メンバーの削除

アカウントリストからレコードを削除するには、別のパスを使用しますが、同じインターフェイスを使用します。 削除する各レコードに`marketoGUI`を指定します。 一度に最大 300 個のレコードを削除できます。

```http
POST /rest/v1/namedAccountList/{id}/namedAccounts/remove.json
```

```json
{
    "input": [
        {
             "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
        },
        {
             "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
        }
    ]
}
```

```json
{
    "requestId": "string",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
            "status": "added"
        },
        {
            "seq": 1,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
            "status": "added"
        }
    ],
    "success": true
}
```

## タイムアウト

- 名前付きアカウントリストエンドポイントのタイムアウトは、特に明記されていない限り30秒です。
- 名前付きアカウントリストの同期のタイムアウトは60秒です。
- 名前付きアカウントリストの削除のタイムアウトは60秒です。
- 名前付きアカウントリストを取得のタイムアウトは60秒です。
- 名前付きアカウントリストメンバーの追加のタイムアウトは60秒です。
- 名前付きアカウントリストメンバーの削除のタイムアウトは60秒です。
- 名前付きアカウントリストのメンバーを取得のタイムアウトは60秒です。
