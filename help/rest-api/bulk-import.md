---
title: 一括読み込み
feature: REST API
description: Marketoの一括読み込み：マルチパートアップロードによるリード、カスタムオブジェクト、プログラムメンバーの読み込み、非同期ジョブの作成、ポーリングステータス、エラーの処理を行います。
exl-id: f7922fd2-8408-4d04-8955-0f8f58914d24
TQID: https://experienceleague.adobe.com/lr9dyX-fY-oJ2LM5P0zE1m24HtFYKQYYbxMkVe--PkE
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 538
ht-degree: 30%

---

# 一括読み込み

一括読み込みは、個人および人物関連の大規模なデータセットを挿入するためのインターフェイスを提供します。 3つのオブジェクトタイプを読み込むことができます。

- リード（ユーザ）
- カスタムオブジェクト
- プログラムメンバー

一括読み込みを実行するには、アップロードしたファイルを読み込むジョブを作成します。 ジョブは非同期で実行されるので、ポーリングしてインポートステータスを取得します。

RFC 2399ごとにHTTP `multipart/form-data`を使用してファイルをアップロードします。

他のエンドポイントとは異なり、Bulk API エンドポイントには`/rest`というプレフィックスはありません。

## 認証

一括読み込み API は、他の Marketo REST API と同じ OAuth 2.0 認証方法を使用します。 `Authorization: Bearer {_AccessToken_}` HTTP ヘッダーに有効なアクセストークンを送信します。

>[!IMPORTANT]
>
>**access_token** クエリパラメーターを使用した認証のサポートは、2025年6月30日（PT）に削除されます。 プロジェクトでアクセストークンを渡すのにクエリパラメーターを使用している場合は、できるだけ早く **Authorization** ヘッダーを使用するように更新する必要があります。 新規開発では、**Authorization** ヘッダーのみを使用する必要があります。

## 制限

- 最大同時読み込みジョブ数：2
- 現在インポート中のジョブを含む、キューに入れられた最大インポートジョブ数：10
- 最大インポートファイルサイズ：10 MB

## 権限

一括読み込みでは、Marketo REST APIと同じ権限モデルを使用します。 追加の権限は必要ありませんが、各エンドポイントのセットには特定の権限が必要です。

## レコード操作

一括読み込みは、レコードの「挿入または更新」操作です。 データベースに一致するレコードが含まれている場合、操作はそのレコードを更新します。 それ以外の場合、操作はレコードを作成します。

一括読み込み応答は、個々のレコードが更新または挿入されたかどうかを示すものではありません。

## ジョブの作成

[ リードの読み込み](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads/operation/importLeadUsingPOST) エンドポイントを呼び出して、リード読み込みジョブを作成します。 このエンドポイントは、[コンテンツタイプとして multipart/form-data](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html) を使用します。

任意の言語のHTTP サポートライブラリを使用して、マルチパートリクエストを作成します。 [curl](https://curl.se/)を使用して開始することもできます。

```http
POST /bulk/v1/leads.json?format=csv
```

```text
Content-Type: multipart/form-data; boundary=--------------------------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Length: 311
Host: <munchkinId>.mktorest.com
```

```text
------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Disposition: form-data; name="file"; filename="leads.csv"
Content-Type: text/csv

firstName,lastName,email
Able,Baker,ablebaker@marketo.com
Charlie,Dog,charliedog@marketo.com
Easy,Fox,easyfox@marketo.com
------WebKitFormBoundaryBQACkJZyaiIAXogC--
```

このリクエストは、`leads.csv`という名前のCSV ファイルから値をインポートするジョブを作成します。

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

応答は`batchId`を返します。 この値を使用して、ジョブのステータスを確認します。

### 一般的なパラメーター

各ジョブ作成エンドポイントは、インポートファイルを設定するためのパラメーターを共有します。 インポートサブタイプは、追加のパラメーターをサポートすることもできます。

| パラメーター | データタイプ | メモ |
| --- | --- | --- |
| format | 文字列 | コンマ区切り値、タブ区切り値、セミコロン区切り値のオプションを使用して、読み込まれたデータのファイル形式を決定します。 CSV、SSV、TSV のいずれかを受け入れます。 形式のデフォルトは CSV です。 |
| ファイル | 文字列 | データは、ファイル内の multipart フォームデータを通じて指定されます。 |

## ジョブステータスのポーリング

`batchId`を[読み込みリードステータスの取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads/operation/getImportLeadStatusUsingGET) エンドポイントに渡して、ジョブのステータスを取得します。

```http
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

`status` メンバーは、ジョブの進行状況を示します。 値は`Queued`、`Importing`、`Complete`または`Failed`です。

この例では、ジョブが完了したので、ポーリングを停止できます。

## 失敗

Get Import Lead Status応答の`numOfRowsFailed`属性は、失敗した行の数を示します。 0より大きい値は、エラーが発生したことを意味します。

失敗したレコードとその原因を取得するには、[読み込み失敗の取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads/operation/getImportLeadFailuresUsingGET) エンドポイントを使用します。

```http
GET /bulk/v1/leads/batch/{batchId}/failures.json
```

失敗ファイルは、失敗した各行を識別し、レコードが失敗した理由を説明します。
