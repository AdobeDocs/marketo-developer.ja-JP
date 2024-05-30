---
title: 「一括読み込み」
feature: REST API
description: 「人物データのバッチインポート」
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---


# 一括読み込み

Marketoには、一括読み込みと呼ばれる、人物および人物に関連する大量のデータを挿入するためのインターフェイスが用意されています。 現在、インターフェイスは次の 3 つのオブジェクトタイプで提供されています。

- リード （人物）
- カスタムオブジェクト
- プログラムメンバー

一括読み込みは、ジョブを作成したあと、ジョブがファイルの読み取りを完了するのを待つことによって実行されます。 これらのジョブは非同期で実行され、ポーリングすることでインポートのステータスを取得できます。 ファイルは、RFC 2399 に従って、HTTP マルチパート/フォームデータを使用してアップロードされます。

Bulk API エンドポイントには、他のエンドポイントのようにプレフィックス「/rest」が付きません。

## 認証

一括読み込み API は、他のMarketo REST API と同じ OAuth 2.0 認証方式を使用します。  これには、有効なアクセストークンをクエリ文字列パラメーターとして埋め込む必要があります `access_token={_AccessToken_}`、または HTTP ヘッダーとして `Authorization: Bearer {_AccessToken_}`.

## 制限

- 最大の同時読み込みジョブ数：2
- 最大キュー内インポートジョブ数（現在のインポートジョブを含む）: 10
- インポート ファイルの最大サイズ：10 MB

## 権限

一括読み込みではMarketo REST API と同じ権限モデルを使用し、使用するために特別な権限は必要ありませんが、エンドポイントのセットごとに特別な権限が必要になります。

## レコード操作

一括読み込みは、「挿入または更新」レコード操作です。 一致するレコードがデータベース内で見つかった場合は、そのレコードが更新されます。 それ以外の場合は、新しいレコードが作成されます。 一括読み込み応答は、特定のレコードが更新されたか挿入されたかを示しません。

## ジョブの作成

Marketoの一括読み込み API では、データの読み込みを実行するジョブの概念を使用します。 を使用したシンプルなリードインポートジョブの作成を見てみましょう。 [リードを読み込み](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/importLeadUsingPOST) エンドポイント。  このエンドポイントはを使用します。 [content-type として multipart/form-data](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html). 正しく設定するまでには時間がかかるので、ベストプラクティスは HTTP サポートライブラリを使用して目的の言語を選択することです。  足を濡らすだけなら、を使用することをお勧めします [curl](https://curl.se/).

```
POST /bulk/v1/leads.json?format=csv
```

```
Content-Type: multipart/form-data; boundary=--------------------------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Length: 311
Host: <munchkinId>.mktorest.com
```

```
------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Disposition: form-data; name="file"; filename="leads.csv"
Content-Type: text/csv

firstName,lastName,email
Able,Baker,ablebaker@marketo.com
Charlie,Dog,charliedog@marketo.com
Easy,Fox,easyfox@marketo.com
------WebKitFormBoundaryBQACkJZyaiIAXogC--
```

このリクエストでは、「leads.csv」という名前の CSV ファイルに含まれる値を読み込むジョブを作成し、列ヘッダーを「FirstName」、「LastName」、「Email」、「Company」とします。

```json
{
    "requestId": "d01f#15d672f8560",
    "result": [
        {
            "batchId": 3404,
            "importId": "3404",
            "status": "Queued"
        }
    ],
    "success": true
}
```

ジョブを送信すると batchId が返され、そのステータスを確認するために使用できます。

### 共通パラメーター

各ジョブ作成エンドポイントは、一括抽出ジョブのファイル形式、フィールド名、フィルターを設定するための一般的なパラメーターをいくつか共有しています。  抽出ジョブの各サブタイプには、追加のパラメーターを指定できます。

| パラメーター | データタイプ | 注意 |
|---|---|---|
| 形式 | 文字列 | 読み込むデータのファイル形式を、コンマ区切り値、タブ区切り値、セミコロン区切り値のオプションと共に決定します。 CSV、SSV、TSV のいずれかを使用できます。 形式のデフォルトは CSV です。 |
| ファイル | 文字列 | データは、ファイル内のマルチパートフォームデータを通じて指定されます。 |


## ジョブステータスのポーリング

ジョブのステータスを判断するには、 [リードのインポートステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/getImportLeadStatusUsingGET) エンドポイント。

```
GET /bulk/v1/leads/batch/{batchId}.json
```

```json
{
    "requestId": "1f63#15d6738fd15",
    "result": [
        {
            "batchId": 3404,
            "importId": "3404",
            "status": "Complete",
            "numOfLeadsProcessed": 3,
            "numOfRowsFailed": 0,
            "numOfRowsWithWarning": 0,
            "message": "Import succeeded, 3 records imported (3 members)"
        }
    ],
    "success": true
}
```

インナー `status` メンバーは、ジョブの進行状況を示します。値は Queued、Importing、Complete、Failed のいずれかになります。 この場合、ジョブが完了したので、ポーリングを停止できます。

## 失敗

失敗は、によって示されます `numOfRowsFailed` リードステータス取得応答の属性。 次の場合 `numOfRowsFailed` が 0 より大きい場合、その値は発生したエラーの数を示します。

失敗した行のレコードと原因を取得するには、次を使用して失敗ファイルを取得する必要があります [リードの読み込みエラーを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/getImportLeadFailuresUsingGET) エンドポイント。

```
GET /bulk/v1/leads/batch/{batchId}/failures.json
```

このファイルには、失敗した行と、レコードが失敗した理由を示すメッセージが示されます。
