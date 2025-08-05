---
title: 一括読み込み
feature: REST API
description: ユーザデータのバッチ読み込み。
exl-id: f7922fd2-8408-4d04-8955-0f8f58914d24
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 100%

---

# 一括読み込み

Marketo には、一括読み込みと呼ばれる、ユーザおよびユーザ関連のデータの大規模なセットを挿入するインターフェイスが用意されています。現在、次の 3 つのオブジェクトタイプに対してインターフェイスが提供されています。

- リード（ユーザ）
- カスタムオブジェクト
- プログラムメンバー

一括読み込みを実行するには、ジョブを作成し、このジョブがファイルの読み取りを完了するまで待機します。これらのジョブは非同期で実行され、ポーリングして読み込みのステータスを取得できます。ファイルは、RFC 2399 に準拠した HTTP multipart/form-data を使用してアップロードされます。

Bulk API エンドポイントには、他のエンドポイントのように「/rest」というプレフィックスは付きません。

## 認証

一括読み込み API は、他の Marketo REST API と同じ OAuth 2.0 認証方法を使用します。これには、有効なアクセストークンを HTTP ヘッダー `Authorization: Bearer {_AccessToken_}` として送信する必要があります。

>[!IMPORTANT]
>
>**access_token** クエリパラメーターを使用した認証のサポートは、2025年6月30日（PT）に削除されます。プロジェクトでアクセストークンを渡すのにクエリパラメーターを使用している場合は、できるだけ早く **Authorization** ヘッダーを使用するように更新する必要があります。新規開発では、**Authorization** ヘッダーのみを使用する必要があります。

## 制限

- 同時読み込みジョブの最大数：2
- キューに入れられた読み込みジョブの最大数（現在読み込み中のジョブを含む）：10
- 読み込みファイルの最大サイズ：10 MB

## 権限

一括読み込みでは、Marketo REST API と同じ権限モデルが使用され、使用する追加の特別な権限は必要ありませんが、各エンドポイントのセットには特定の権限が必要です。

## レコード操作

一括読み込みは、レコードの「挿入または更新」操作です。データベース内に一致するレコードが見つかった場合は、更新されます。それ以外の場合は、新しいレコードが作成されます。一括読み込み応答では、特定のレコードが更新されたか挿入されたかは示されません。

## ジョブの作成

Marketo の一括読み込み API では、データ読み込みを実行するジョブの概念を使用します。[リードを読み込み](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/importLeadUsingPOST)エンドポイントを使用して、シンプルなリード読み込みジョブを作成する方法を見てみましょう。このエンドポイントは、[コンテンツタイプとして multipart/form-data](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html) を使用します。これを正しく行うのは難しい場合があるので、選択した言語の HTTP サポートライブラリを使用するのがベストプラクティスです。初めて使用する場合は、[curl](https://curl.se/) を使用することをお勧めします。

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

このリクエストでは、「FirstName」、「LastName」、「Email」、「Company」という列ヘッダーを持つ「leads.csv」という名前の CSV ファイルに含まれる値を読み込むジョブを構築します。

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

ジョブを送信すると batchId が返され、これを使用してジョブのステータスを確認できます。

### 一般的なパラメーター

各ジョブ作成エンドポイントでは、一括抽出ジョブのファイル形式、フィールド名、フィルターを設定する一般的なパラメーターをいくつか共有しています。抽出ジョブの各サブタイプには、追加のパラメーターを指定できます。

| パラメーター | データタイプ | メモ |
|---|---|---|
| format | 文字列 | コンマ区切り値、タブ区切り値、セミコロン区切り値のオプションを使用して、読み込まれたデータのファイル形式を決定します。CSV、SSV、TSV のいずれかを受け入れます。形式のデフォルトは CSV です。 |
| ファイル | 文字列 | データは、ファイル内の multipart フォームデータを通じて指定されます。 |

## ジョブステータスのポーリング

[リードを読み込みステータスを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/getImportLeadStatusUsingGET)エンドポイントを使用すると、ジョブのステータスを簡単に確認できます。

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

内部 `status` メンバーはジョブの進行状況を示し、キュー済み、読み込み中、完了、失敗のいずれかの値になります。この場合、ジョブは完了しているので、ポーリングを停止できます。

## 失敗

失敗は、リードを読み込みステータスを取得の応答の `numOfRowsFailed` 属性によって示されます。`numOfRowsFailed` がゼロより大きい場合、この値は発生した失敗の数を示します。

失敗した行のレコードと原因を取得するには、[リードを読み込み失敗を取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/getImportLeadFailuresUsingGET)エンドポイントを使用して、失敗ファイルを取得する必要があります。

```
GET /bulk/v1/leads/batch/{batchId}/failures.json
```

ファイルには、失敗した行と、レコードが失敗した理由を示すメッセージが示されます。
