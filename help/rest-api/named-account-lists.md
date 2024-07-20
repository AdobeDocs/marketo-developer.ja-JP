---
title: 重点顧客の一覧
feature: REST API
description: 名前付きアカウント リストを構成します。
exl-id: 98f42780-8329-42fb-9cd8-58e5dbea3809
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# 重点顧客の一覧

[ 指定顧客リストのエンドポイントリファレンス ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Account-Lists)

Marketoの [ 名前付きアカウントリスト ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/target-account-management/target/account-lists) は、名前付きアカウントのコレクションを表します。 カテゴリ化、データ強化、スマートキャンペーンフィルタリングなど、様々なケースで使用できます。 指定アカウントリスト API を使用すると、これらのリストアセットとそのメンバーシップをリモートで管理できます。
`Content`

## 権限

名前付きアカウント リストを照会するには、読み取り専用の名前付きアカウント リストまたは読み取り/書き込みの名前付きアカウント リスト権限が必要です。 リストを作成、更新または削除するには、読み取り/書き込み可能な名前付きアカウントリスト権限が必要です。 リスト メンバーシップのクエリには、読み取り専用の名前付きアカウントまたは読み取り/書き込みの名前付きアカウントのアクセス許可が必要ですが、メンバーシップの管理には、読み取り/書き込みの名前付きアカウントのアクセス許可が必要です。

## モデル

名前付きアカウントリストには限られた数の標準フィールドがあり、カスタムフィールドを使用して拡張することはできません。
`Named Account List Field`

| 名前 | データタイプ | 更新可能 | 注意 |
|---|---|---|---|
| marketoGUID | 文字列 | False | 指定されたアカウントリストを表す一意の文字列識別子。 このフィールドはシステム管理であり、レコードの作成時にフィールドとして使用することはできません。 作成または更新の実行時に「dedupeBy」:「idField」によって使用されるフィールド。 |
| 名前 | 文字列 | True | リストの名前。 作成または更新の実行時に「dedupeBy」:「dedupeFields」によって使用されるフィールド。 |
| createdAt | 日時 | False | リストの作成日時。 このフィールドはシステムによって管理され、レコードの作成または更新時にはフィールドとして許可されません。 |
| updatedAt | 日時 | False | リストの最新の更新の日時。 このフィールドはシステムによって管理され、レコードの作成または更新時にはフィールドとして許可されません。 |
| タイプ | 文字列 | False | リストのタイプ。 「default」または「external」のいずれかの値を持つことができます。 外部リストは、CRM アカウント ビューで作成されたリストです。 |


## クエリ

アカウントリストのクエリはシンプルで簡単です。 現在、名前付きアカウントリストをクエリするための有効な filterType は、「dedupeFields」と「idField」の 2 つのみです。 フィルターするフィールドはクエリの `filterType` パラメーターで設定し、値はコンマ区切りリスト `filterValues as` 設定します。 `nextPageToken` フィルターと `batchSize` フィルターもオプションのパラメーターです。

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

名前付きアカウントリストレコードの作成および更新は、他のリードデータベースの作成および更新操作で確立されたパターンに従います。 名前付きアカウントリストには、更新可能なフィールド `name` が 1 つだけあることに注意してください。

エンドポイントでは、「createOnly」と「updateOnly」の 2 つの標準のアクションタイプが許可されています。  「createOnly」の `action defaults`。

アクションが `updateOnly` の場合は、オプションの `dedupeBy parameter` を指定できます。  指定できる値は、「dedupeFields」（「name」に対応）または「idField」（「marketoGUID」に対応）です。  `createOnly` モードでは、「名前」のみが `dedupeBy` フィールドとして許可されます。 一度に最大 300 件のレコードを送信できます。

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

名前付きアカウントリストの削除は簡単で、リストの `name` または `marketoGUID` に基づいて実行できます。 使用するキーを選択するには、リクエストの `deleteB` メンバーで、名前に「dedupeFields」を渡すか、marketoGUID に「idField」を渡します。 未設定の場合、デフォルトで dedupeFields になります。 一度に最大 300 件のレコードを削除できます。

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

指定されたキーのレコードが見つからない場合、対応する結果項目には「スキップ」の `status` と、上記の例に示すように、失敗を説明するコードとメッセージを含む理由が含まれます。

## メンバーシップの管理

### クエリメンバーシップ

名前付きアカウントリストのメンバーシップのクエリは簡単で、アカウントリストの `i` のみが必要です。 オプションのパラメーターは次のとおりです。

-`field` – 応答レコードに含めるフィールドのコンマ区切りのリスト
-`nextPageToke` – 結果セットをページングする
-`batchSiz` – 返すレコード数を指定します。

`field` が未設定の場合は、`marketoGUI`,`nam`、`createdA` および `updatedA` が返されます。 `batchSiz` の最大値とデフォルト値は 300 です。

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

名前付きアカウントは、名前付きアカウント リストに簡単に追加できます。 アカウントは、marketoGUID を使用してのみ追加できます。 一度に最大 300 件のレコードを追加できます。

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

アカウントリストからレコードを削除すると、パスは異なりますが、削除するレコードごとに `marketoGUI` が必要な同じインターフェイスになります。 一度に最大 300 件のレコードを削除できます。

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

- 以下に示さない限り、名前付きアカウントリストのエンドポイントのタイムアウトは 30 秒です
   - 名前付きアカウント リストの同期：60s 
   - 重点顧客リストの削除：60s 
   - 名前付きアカウント リストの取得：60s 
   - 指定アカウント・リスト・メンバーの追加：60s 
   - 名前付きアカウント リスト メンバの削除：60s 
   - 指定されたアカウント リスト メンバの取得：60s
