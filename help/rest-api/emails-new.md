---
title: メール
feature: REST API
description: Marketo Asset REST APIを使用して、メールアセットのクエリ、作成、更新、複製、削除、承認、依存関係の検査を行います。
exl-id: b41a3ae5-2b25-4103-84b4-320fc2c44bd6
source-git-commit: e2606d6cb12c572603ff069617de58417e43ca63
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 6%

---

# メール

[メールエンドポイントの参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails_New)

メールは、メッセージのメタデータ、コンテンツ設定、設定、承認状態を定義するアセットレコードです。

## アクセス

この記事で説明するエンドポイントには、アクセストークンが必要です。

```text
?access_token=<access_token>
```

リクエストには`x-app-type` ヘッダーも必要です：

```text
x-app-type: <app-type>
```

## クエリ

アセット `id`またはフィルターエンドポイントを使用して、メールのメタデータを取得できます。

### ID 別

#### リクエスト

```http
GET /rest/asset/v2/email/{id}
```

#### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "7b3c#1900ab12cd3",
  "result": [
    {
      "id": "1017",
      "name": "Spring Launch Email",
      "description": "Main announcement email",
      "status": "draft"
    }
  ]
}
```

### フィルター

フィルターエンドポイントは、ワークスペース内での検索と、追加のクエリパラメーターによる結果の絞り込みをサポートします。

`workspaceId`が必要です。

サポートされるクエリパラメーター：

| パラメーター | 説明 |
| - | - |
| `workspaceId` | フィルターリクエストのスコープに使用される必須ワークスペース識別子。 |
| `folderId` | 結果を1つのフォルダーにフィルタリングします。 |
| `folderIds` | 複数のフォルダーに結果をフィルタリングする繰り返しパラメーター。 |
| `status` | 1つ以上のメールステータスでフィルタリングする繰り返しパラメーター。 |
| `pageIndex` | ページ分割された結果のゼロベースのページインデックス。 |
| `pageSize` | ページごとに返される結果の最大数。 |
| `createdBy` | 作成者によって結果をフィルタリングします。 |
| `createdAtStart` | このタイムスタンプ以降に作成されたアセットを返します。 |
| `createdAtEnd` | このタイムスタンプの前に作成されたアセットを返します。 |
| `modifiedBy` | 最後に修正したユーザーの結果をフィルタリングします。 |
| `modifiedAtStart` | このタイムスタンプ以降に変更されたアセットを返します。 |
| `modifiedAtEnd` | このタイムスタンプ以前に変更されたアセットを返します。 |
| `name` | メール名で結果をフィルタリングします。 |
| `sortKey` | 結果の並べ替えに使用するフィールドを選択します。 |
| `sortOrder` | 並べ替えの方向を設定します。 |
| `isCreatedByMe` | 現在のユーザーが作成したアセットに結果を制限します。 |
| `isModifiedByMe` | 結果を、現在のユーザーが最後に変更したアセットに制限します。 |
| `templateId` | テンプレート IDで結果をフィルタリングします。 |
| `scriptEngine` | スクリプトエンジン設定で結果をフィルタリングします。 |
| `isValueNonNullable` | 値がnull不可であるかどうかに基づいてフィルタリングします。 |
| `includeArchived` | アーカイブされたアセットが結果に含まれます。 |

#### リクエスト

```http
GET /rest/asset/v2/email/filter?workspaceId=1001&name=Spring%20Launch&status=draft&status=approved&pageIndex=0&pageSize=20
```

#### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "5dd1#1900ab13011",
  "result": [
    {
      "id": "1017",
      "name": "Spring Launch Email",
      "status": "draft"
    }
  ]
}
```

名前でメールを検索する必要がある場合は、`name` パラメーターを使用します。

## 作成

JSON ペイロードを送信してメールを作成します。 `name`、`appData`および`headers`が必要です。 `headers.subject`が必要です。`appData`には、`folderId`、`workspaceId`、または`programId`のうち少なくとも1つが含まれている必要があります。

### リクエスト

```http
POST /rest/asset/v2/email
Content-Type: application/json
```

```json
{
  "name": "Spring Launch Email",
  "description": "Main announcement email",
  "appData": {
    "workspaceId": "1001",
    "folderId": "2002",
    "editorType": "email"
  },
  "headers": {
    "subject": "Introducing the Spring Launch",
    "fromName": "Marketing Team",
    "fromEmail": "marketing@example.com",
    "replyEmail": "reply@example.com",
    "preheader": "See what changed this quarter",
    "ccEmails": [
      "owner@example.com"
    ]
  },
  "settings": {
    "isOperational": false,
    "isTextOnly": false,
    "isWebPageView": true,
    "enableUrlTracking": true
  },
  "templateId": "3003"
}
```

### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "238c#1900ab1313f",
  "result": [
    {
      "id": "1017",
      "name": "Spring Launch Email",
      "status": "draft"
    }
  ]
}
```

リクエスト本文には、`data`、`editorContext`、`themeId`、`appType`および`status`も含めることができます。

### フィールドの作成

* `appData`は、電子メールの作成場所と編集方法を特定します。
* `headers`には、件名、送信者、返信アドレス、プリヘッダー、およびオプションのCC受信者を含むメッセージヘッダーの値が含まれています。
* `settings`は、テキストのみのモード、web ページビュー、URL トラッキングなどの操作とレンダリングの動作を制御します。
* `templateId`は、電子メールの作成時に使用される電子メールテンプレートを識別します。

## 更新

アセット IDでメールを更新します。 リクエスト本文は`UpdateEmailRequest` スキーマを使用しており、すべてのプロパティはオプションであるため、変更するフィールドのみを送信できます。

### リクエスト

```http
POST /rest/asset/v2/email/{id}/update
Content-Type: application/json
```

```json
{
  "description": "Updated announcement email",
  "headers": {
    "subject": "Spring Launch Is Live",
    "preheader": "Read the latest release notes"
  },
  "settings": {
    "enableUrlTracking": true,
    "isWebPageView": true
  }
}
```

### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "9fd3#1900ab13210",
  "result": [
    {
      "id": "1017"
    }
  ]
}
```

## 状態を管理

電子メールは、ドラフトと承認されたライフサイクルを使用します。 状態遷移エンドポイントを使用して、メールの承認、承認の取り消し、ドラフトの破棄、または新しいドラフトの作成を行います。

有効な`action`値は次のとおりです。

* `approve`
* `unapprove`
* `discard`
* `create_draft`

### リクエスト

```http
POST /rest/asset/v2/email/state/transition
Content-Type: application/json
```

### 応答

```json
{
  "contentId": "1017",
  "action": "approve"
}
```

## 複製

コピーエンドポイントを使用して、既存のメールのコピーを作成します。

### リクエスト

```http
POST /rest/asset/v2/email/clone
Content-Type: application/json
```

### 応答

```json
{
  "assetId": "1017",
  "newAsset": {
    "name": "Spring Launch Email Copy",
    "description": "Cloned from Spring Launch Email"
  }
}
```

## 削除

アセット IDでメールを削除します。

### リクエスト

```http
POST /rest/asset/v2/email/{id}/delete
Content-Type: application/json
```

このエンドポイントは、パス内のアセット `id`を受け取り、リクエスト本文を定義しません。

## 使用者

`usedby` エンドポイントを使用して、特定の電子メールを参照するアセットを取得します。

### リクエスト

```http
POST /rest/asset/v2/email/usedby
Content-Type: application/json
```

### 応答

```json
{
  "assetId": "1017",
  "pageIndex": 0,
  "pageSize": 20,
  "type": "all"
}
```

## メモ

クエリエンドポイントは、アセットのメタデータを返します。 使用可能なフィールドと環境固有のプロパティの完全なスキーマに対して、エンドポイントリファレンスを使用します。
