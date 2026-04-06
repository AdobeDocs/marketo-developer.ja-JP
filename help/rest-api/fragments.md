---
title: フラグメント
feature: REST API
description: Marketo Asset REST APIを使用して、フラグメントの依存関係をクエリ、作成、更新、複製、削除、承認、検査します。
exl-id: 9dd532d1-1dd7-4581-86dd-1943fab66cbb
source-git-commit: 0e0a3e5a08e81f349044cbc327d1aba963ab30e4
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 11%

---

# フラグメント

フラグメントは、電子メールなどの他のアセットで参照できる、再利用可能なコンテンツアセットです。

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

アセット IDまたはフィルターエンドポイントを使用して、フラグメントメタデータを取得できます。

### ID 別

#### リクエスト

```text
GET /rest/asset/v2/fragment/{id}
```

#### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "fa0f#1900ab15001",
  "result": [
    {
      "id": "83",
      "name": "Hero Banner Fragment",
      "description": "Reusable hero block",
      "status": "approved"
    }
  ]
}
```

### フィルター

フィルターエンドポイントは、ワークスペース内での検索と、追加のクエリパラメーターによる結果の絞り込みをサポートします。 `workspaceId`が必要です。

todo：これをテーブルにする
サポートされているフィルターには、`folderId`、繰り返し`folderIds`、繰り返し`status`、`pageIndex`、`pageSize`、`createdBy`、`createdAtStart`、`createdAtEnd`、`modifiedBy`、`modifiedAtStart`、`modifiedAtEnd`、`name`、`fragmentType`、`sortKey`、`sortOrder`、`isCreatedByMe`、`isModifiedByMe`、`scriptEngine`、`isValueNonNullable`および`includeArchived`が含まれます。

#### リクエスト

```text
GET /rest/asset/v2/fragment/filter?workspaceId=1001&fragmentType=email&pageIndex=0&pageSize=20
```

#### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "f9cc#1900ab1504a",
  "result": [
    {
      "id": "83",
      "name": "Hero Banner Fragment",
      "status": "approved"
    }
  ]
}
```

名前でフラグメントを検索する必要がある場合は、`name` パラメーターを使用します。

## 作成

JSON ペイロードを送信してフラグメントを作成します。 `name`、`appData`および`settings`が必要です。 `settings`には`fragmentType`と`supportedChannels`を含める必要があります。

### リクエスト

```text
POST /rest/asset/v2/fragment
Content-Type: application/json
```

```json
{
  "name": "Hero Banner Fragment",
  "description": "Reusable hero block",
  "appData": {
    "workspaceId": "1001",
    "folderId": "395",
    "editorType": "fragment"
  },
  "settings": {
    "fragmentType": "email",
    "fragmentSubType": "html",
    "supportedChannels": [
      "email"
    ]
  }
}
```

### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "bd57#1900ab1509d",
  "result": [
    {
      "id": "13",
      "name": "Hero Banner Fragment",
      "status": "draft"
    }
  ]
}
```

リクエスト本文には、`data`、`editorContext`、`themeId`、`appType`および`status`も含めることができます。

### フィールドの作成

* `appData`は、フラグメントの保存場所と編集方法を識別します。
* `settings.fragmentType`は、電子メールフラグメントなどのフラグメントカテゴリを識別します。
* `settings.fragmentSubType`を使用して、フラグメント形式をさらに定義できます。
* `settings.supportedChannels`には、フラグメントを使用できるチャネルが一覧表示されます。

## 更新

アセット IDでフラグメントを更新します。

### リクエスト

```text
POST /rest/asset/v2/fragment/{id}/update
Content-Type: application/json
```

```json
{
  "name": "Hero Banner Fragment v2",
  "description": "Updated reusable hero block",
  "settings": {
    "fragmentSubType": "html",
    "supportedChannels": [
      "email"
    ]
  }
}
```

### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "73d9#1900ab150f0",
  "result": [
    {
      "id": "13"
    }
  ]
}
```

## 状態を管理

フラグメントでは、ドラフトと承認されたライフサイクルを使用します。 状態遷移エンドポイントを使用して、フラグメントの承認、承認の取り消し、ドラフトの破棄、または新しいドラフトの作成を行います。

有効な`action`値は次のとおりです。

* `approve`
* `unapprove`
* `discard`
* `create_draft`

### リクエスト

```text
POST /rest/asset/v2/fragment/state/transition
Content-Type: application/json
```

### 応答

```json
{
  "contentId": "13",
  "action": "approve"
}
```

## 複製

コピーエンドポイントを使用して、既存のフラグメントのコピーを作成します。

### リクエスト

```text
POST /rest/asset/v2/fragment/clone
Content-Type: application/json
```

### 応答

```json
{
  "assetId": "13",
  "newAsset": {
    "name": "Hero Banner Fragment Copy",
    "description": "Cloned fragment"
  }
}
```

## 削除

アセット IDでフラグメントを削除します。

### リクエスト

```text
POST /rest/asset/v2/fragment/{id}/delete
Content-Type: application/json
```

このエンドポイントは、パス内のフラグメント IDを取得し、リクエスト本文を定義しません。

## 使用者

`usedby` エンドポイントを使用して、特定のフラグメントを参照するアセットを取得します。

### リクエスト

```text
POST /rest/asset/v2/fragment/usedby
Content-Type: application/json
```

### 応答

```json
{
  "assetId": "13",
  "pageIndex": 0,
  "pageSize": 20,
  "type": "all"
}
```
