---
title: メールテンプレート
feature: REST API
description: Marketo Asset REST APIを使用して、メールテンプレートの依存関係をクエリ、作成、更新、複製、削除、承認、検査します。
exl-id: 50bb0047-d6ea-4c94-a900-18c37b17a147
source-git-commit: 0e0a3e5a08e81f349044cbc327d1aba963ab30e4
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 14%

---

# メールテンプレート

[メールテンプレートエンドポイントの参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates)

メールテンプレートは、メール作成時に使用される構造と再利用可能なレイアウトを定義します。

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

アセット IDまたはフィルターエンドポイントを使用して、メールテンプレートのメタデータを取得できます。

### ID 別

#### リクエスト

```text
GET /rest/asset/v2/emailtemplate/{id}
```

#### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "14f9e#1900ab14001",
  "result": [
    {
      "id": "19",
      "name": "Base Newsletter Template",
      "description": "Core responsive template",
      "status": "draft"
    }
  ]
}
```

### フィルター

フィルターエンドポイントは、ワークスペース内での検索と、追加のクエリパラメーターによる結果の絞り込みをサポートします。 `workspaceId`が必要です。

サポートされているフィルターには、`folderId`、繰り返し`folderIds`、繰り返し`status`、`pageIndex`、`pageSize`、`createdBy`、`createdAtStart`、`createdAtEnd`、`modifiedBy`、`modifiedAtStart`、`modifiedAtEnd`、`name`、`sortKey`、`sortOrder`、`isCreatedByMe`、`isModifiedByMe`、`scriptEngine`、`isValueNonNullable`、および`includeArchived`が含まれます。

#### リクエスト

```text
GET /rest/asset/v2/emailtemplate/filter?workspaceId=1001&name=Newsletter&pageIndex=0&pageSize=20
```

#### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "33c4#1900ab1402f",
  "result": [
    {
      "id": "19",
      "name": "Base Newsletter Template",
      "status": "draft"
    }
  ]
}
```

名前でテンプレートを検索する必要がある場合は、`name` パラメーターを使用します。

## 作成

JSON ペイロードを送信して、メールテンプレートを作成します。 `name`と`appData`が必要です。 `appData`には少なくとも`folderId`または`workspaceId`を含める必要があります。

### リクエスト

```text
POST /rest/asset/v2/emailtemplate
Content-Type: application/json
```

```json
{
  "name": "Base Newsletter Template",
  "description": "Core responsive template",
  "appData": {
    "workspaceId": "1001",
    "folderId": "15",
    "editorType": "emailTemplate"
  },
  "themeId": "42"
}
```

### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "a99f#1900ab1407e",
  "result": [
    {
      "id": "1022",
      "name": "Base Newsletter Template",
      "status": "draft"
    }
  ]
}
```

リクエスト本文には、`data`、`editorContext`、`appType`、`status`も含めることができます。

### フィールドの作成

`appData`は、テンプレートの保存場所と編集方法を特定します。

`themeId`を使用して、該当する場合にテーマをテンプレートに関連付けることができます。

## 更新

アセット IDでテンプレートを更新します。

### リクエスト

```text
POST /rest/asset/v2/emailtemplate/{id}/update
Content-Type: application/json
```

```json
{
  "name": "Base Newsletter Template v2",
  "description": "Updated responsive template",
  "appData": {
    "folderId": "15"
  }
}
```

### 応答

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "cf10#1900ab140b3",
  "result": [
    {
      "id": "1022"
    }
  ]
}
```

## 状態を管理

メールテンプレートでは、ドラフトと承認されたライフサイクルを使用します。 状態遷移エンドポイントを使用して、テンプレートの承認、承認の取り消し、ドラフトの破棄、または新しいドラフトの作成を行います。

有効な`action`値は次のとおりです。

- `approve`
- `unapprove`
- `discard`
- `create_draft`

### リクエスト

```text
POST /rest/asset/v2/emailtemplate/state/transition
Content-Type: application/json
```

### 応答

```json
{
  "contentId": "1022",
  "action": "approve"
}
```

## 複製

コピーエンドポイントを使用して、既存のテンプレートのコピーを作成します。

### リクエスト

```text
POST /rest/asset/v2/emailtemplate/clone
Content-Type: application/json
```

### 応答

```json
{
  "assetId": "1022",
  "newAsset": {
    "name": "Base Newsletter Template Copy",
    "description": "Cloned template"
  }
}
```

## 削除

アセット IDでテンプレートを削除します。

### リクエスト

```text
POST /rest/asset/v2/emailtemplate/{id}/delete
Content-Type: application/json
```

このエンドポイントは、パス内のテンプレート IDを取得し、リクエスト本文を定義しません。

## 使用者

`usedby` エンドポイントを使用して、特定のテンプレートを参照するアセットを取得します。

### リクエスト

```text
POST /rest/asset/v2/emailtemplate/usedby
Content-Type: application/json
```

### 応答

```json
{
  "assetId": "1022",
  "pageIndex": 0,
  "pageSize": 20,
  "type": "all"
}
```

## メモ

クエリエンドポイントは、アセットのメタデータを返します。 完全な応答スキーマと環境固有のプロパティに対しては、エンドポイントリファレンスを使用します。
