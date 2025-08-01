---
title: 重点顧客リスト
feature: REST API
description: 重点顧客リストを設定します。
exl-id: 98f42780-8329-42fb-9cd8-58e5dbea3809
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 100%

---

# 重点顧客リスト

[重点顧客リストエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Account-Lists)

Marketo の[重点顧客リスト](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/target-account-management/target/account-lists)は、重点顧客のコレクションを表します。分類、データエンリッチメント、スマートキャンペーンフィルタリングなど、様々なケースに使用できます。Named Account List API を使用すると、これらのリストアセットとそのメンバーシップをリモートで管理できます。
`Content`

## 権限

重点顧客リストのクエリを実行するには、重点顧客リストの読み取り専用権限、または重点顧客リストの読み取り／書き込み権限が必要です。リストを作成、更新または削除するには、重点顧客リストの読み取り／書き込み権限が必要です。リストメンバーシップのクエリを実行するには、重点顧客の読み取り専用権限、または重点顧客の読み取り／書き込み権限が必要です。一方、メンバーシップを管理するには、重点顧客の読み取り／書き込み権限が必要です。

## モデル

重点顧客リストでは、標準フィールドの数が制限され、カスタムフィールドで拡張できません。
`Named Account List Field`

| 名前 | データタイプ | 更新可能 | メモ |
|---|---|---|---|
| marketoGUID | 文字列 | False | 重点顧客リストの一意の文字列識別子。このフィールドは、システムで管理され、レコードを作成する際にフィールドとして使用できません。作成または更新の実行時に &quot;dedupeBy&quot;:&quot;idField&quot; によって使用されるフィールド。 |
| name | 文字列 | True | リストの名前。作成または更新の実行時に &quot;dedupeBy&quot;:&quot;dedupeFields&quot; によって使用されるフィールド。 |
| createdAt | 日時 | False | リストの作成日時。このフィールドは、システムで管理され、レコードを作成または更新する際にフィールドとして使用できません。 |
| updatedAt | 日時 | False | リストの最新の更新日時。このフィールドは、システムで管理され、レコードを作成または更新する際にフィールドとして使用できません。 |
| タイプ | 文字列 | False | リストのタイプ。&quot;default&quot; または &quot;external&quot;のいずれかの値を指定できます。外部リストは、CRM アカウントビューで作成されたリストです。 |


## クエリ

アカウントリストのクエリの実行はシンプルで簡単です。現在、重点顧客リストのクエリを実行するための有効な filterTypes は、&quot;dedupeFields&quot; と &quot;idField&quot; の 2 つだけです。フィルタリングするフィールドは、クエリの `filterType` パラメーターで設定され、値はコンマ区切りのリストとして `filterValues as` に設定されます。また、`nextPageToken` フィルターおよび `batchSize` フィルターもオプションのパラメーターです。

```
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

重点顧客リストレコードの作成と更新は、他のリードデータベースの作成および更新操作の確立されたパターンに従います。重点顧客リストには、更新可能なフィールドの `name` が 1 つだけあります。

エンドポイントでは、&quot;createOnly&quot; と &quot;updateOnly&quot; の 2 つの標準アクションタイプを指定できます。`action defaults` は &quot;createOnly&quot; です。

アクションが `updateOnly` の場合、オプションの `dedupeBy parameter` パラメーターを指定できます。指定可能な値は、&quot;dedupeFields&quot;（&quot;name&quot; に対応）または idField&quot;（&quot;marketoGUID&quot; に対応）です。`createOnly` モードでは、`dedupeBy` フィールドとして &quot;name&quot; のみが指定できます。一度に最大 300 個のレコードを送信できます。

```
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

重点顧客リストの削除は簡単で、リストの `name` または `marketoGUID` に基づいて実行できます。使用するキーを選択するには、リクエストの `deleteB` メンバーで、名前に &quot;dedupeFields&quot; を渡すか、marketoGUID に &quot;idField&quot; を渡します。未設定の場合、デフォルトは dedupeFields になります。一度に最大 300 個のレコードを削除できます。

```
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

特定のキーのレコードが見つからない場合、対応する結果項目の `status` は &quot;skipped&quot; になり、上記の例に示すように、失敗を説明するコードとメッセージを含む理由が表示されます。

## メンバーシップの管理

### クエリメンバーシップ

重点顧客リストのメンバーシップのクエリの実行は簡単で、アカウントリストの `i` のみが必要です。オプションのパラメーターは次のとおりです。

-`field` - 応答レコードに含めるフィールドのコンマ区切りのリスト
-`nextPageToke` - 結果セットのページング用
-`batchSiz` - 返すレコード数の指定用

`field` が未設定の場合は、`marketoGUI`、`nam`、`createdA`、`updatedA` が返されます。 `batchSiz` の最大値とデフォルト値は 300 です。

```
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

重点顧客は、重点顧客リストに簡単に追加できます。アカウントは、marketoGUID を使用してのみ追加できます。一度に最大 300 個のレコードを追加できます。

```
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

アカウントリストからレコードを削除するには、パスは異なりますが、インターフェイスは同じで、削除するレコードごとに `marketoGUI` が必要です。一度に最大 300 個のレコードを削除できます。

```
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

- 「重点顧客リスト」エンドポイントは、以下に記載されていない限り、タイムアウトが 30 秒になります
   - 重点顧客リストを同期：60 秒
   - 重点顧客リストを削除：60 秒
   - 重点顧客リストを取得：60 秒
   - 重点顧客リストメンバーを追加：60 秒
   - 重点顧客リストメンバーを削除：60 秒
   - 重点顧客リストメンバーを取得：60 秒
