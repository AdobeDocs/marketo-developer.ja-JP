---
title: ユーザ管理
feature: REST API
description: ユーザー、ヘッダーベースの認証、ロールとワークスペース、ステータスコードの処理、日付時形式、クエリエンドポイントに関するCRUD用Marketo User Management APIのガイドです。
exl-id: 2a58f496-0fe6-4f7e-98ef-e9e5a017c2de
TQID: https://experienceleague.adobe.com/V1NzpIl-peHBi9rqy8YwdJDh3O-dViIdF0cBsDSI-w8
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b13bd2ad-8e65-49e5-9691-2a0d31067b35id: d1d0a9cd-295d-4976-8c39-ddae266f240eid: d65b4a73-87a3-4d56-b638-74e74d9939ce
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1440
ht-degree: 61%

---

# ユーザ管理

[ユーザー管理エンドポイントリファレンス](https://developer.adobe.com/marketo-apis/api/user/)

Marketo User Management エンドポイントは、ユーザーレコードに対してCRUD操作を実行します。 ユーザーを作成するには、招待状を送信します。 その後、ユーザーはパスワードを設定し、初めてMarketoにアクセスします。

User Management API を使用する際、他の Marketo REST API とは次の点が異なります。

- HTTP ヘッダーにアクセストークンを送信します。 アクセストークンをクエリ文字列パラメーターとして渡すことはできません。 [認証ガイド ](authentication.md)を参照してください。
- REST API [ カスタムサービス ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api)のユーザーロールを作成する際に、次の各グループから権限を選択します。
  1. [管理にアクセス](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions)グループの「ユーザにアクセス」権限
  1. [Access API](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions) グループの「Access User Management API」
- 応答本文に「success」ブール属性が含まれていないため、HTTP応答ステータスコードを評価します。 呼び出しが成功すると、ステータスコード 200が返されます。 失敗した呼び出しは、200以外のステータスコードと、エラーコードと説明メッセージを含む標準の「errors」配列を返します。
- 日時の文字列を`yyyyMMdd'T'HH:mm:ss.SSS't'+|-hhmm`として書式設定します。 この形式は、`createdAt`、`updatedAt`、`expiresAt`に適用されます。
- User Management API エンドポイントのプレフィックスに「/rest」を付けないでください。

## クエリ

ユーザー管理クエリは、すべてのユーザー、役割、ワークスペースを取得できます。 また、1人のユーザー、またはユーザーID別に関連する役割とワークスペースレコードを取得することもできます。

### ID 別のユーザ

[ID によるユーザの取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUserUsingGET)エンドポイントは、単一の `userid` パスパラメーターを受け取り、招待を受け入れたユーザの単一のユーザレコードを返します。

```http
GET /userservice/management/v1/users/{userid}/user.json
```

```json
{
  "userid": "jamie@houselannister.com",
  "firstName": "Jamie",
  "lastName": "Lannister",
  "emailAddress": "jamie@lannister.com",
  "optedIn": false,
  "failedLogins": 0,
  "failedDeviceCode": 0,
  "isLocked": false,
  "lockedReason": null,
  "id": 0,
  "apiOnly": false,
  "userRoleWorkspaces": [
    {
      "accessRoleId": 1,
      "accessRoleName": "Admin",
      "workspaceId": 0,
      "workspaceName": "AllZones"
    },
    {
      "accessRoleId": 2,
      "accessRoleName":
      "Standard User",
      "workspaceId": 1008,
      "workspaceName": "World"
    }
  ],
  "expiresAt": "2020-12-31T08:00:00.000t+0000",
  "lastLoginAt": "2020-02-05T01:02:23.000t+0000"
}
```

### ID 別の招待ユーザ

[ID により招待されたユーザの取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getInvitedUserUsingGET)エンドポイントは、単一の `userid` パスパラメーターを受け取り、「保留中」のユーザ（まだ招待を受け入れていないユーザ）の単一のユーザレコードを返します。

```http
GET /userservice/management/v1/users/{userid}/invite.json
```

```json
{
    "id": 25112,
    "firstName": "Jamie",
    "lastName": "Lannister",
    "emailAddress": "jamie@lannister.com",
    "userId": "jamie@lannister.com",
    "subscriptionId": 3381,
    "status": "pending",
    "expiresAt": "20200807T20:49:54.0t+0000",
    "createdAt": "20200731T20:49:54.0t+0000",
    "updatedAt": "20200731T20:49:54.0t+0000"
}
```

### ID 別のロールとワークスペース

Id](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUserRolesAndWorkspacesUsingGET)による役割とワークスペースの取得エンドポイントは、1つの`userid` パスパラメーターを取り、ユーザーの役割とワークスペースレコードを返します。 [応答配列内の各オブジェクトには、役割とワークスペース IDおよび名前が含まれます。

```http
GET /userservice/management/v1/users/{userid}/roles.json
```

```json
[
  {
    "accessRoleId": 1,
    "accessRoleName": "Admin",
    "workspaceId": 0,
    "workspaceName": "AllZones"
  },
  {
    "accessRoleId": 2,
    "accessRoleName": "Standard User",
    "workspaceId": 1008,
    "workspaceName": "World"
  }
]
```

### ユーザの参照

[Get Users](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUsersUsingGET) エンドポイントは、すべてのユーザーレコードを返します。 次のオプションの整数パラメーターをサポートしています。

- `pageSize`は、返すエントリの最大数を指定します。 デフォルトは20、最大は200です。
- `pageOffset`は、エントリの取得を開始する場所を指定します。 デフォルトは0で、`pageSize`と一緒に使用できます。

```http
GET /userservice/management/v1/users/allusers.json
```

```json
[
  {
    "userid": "jamie@lannister.com",
    "firstName": "Jamie",
    "lastName": "Lannister",
    "emailAddress": "jamie@houselannister.com",
    "id": 6785,
    "apiOnly": false
  },
  {
    "userid": "jeoffery@housebaratheon.com",
    "firstName": "Jeoffery",
    "lastName": "Baratheon",
    "emailAddress": "jeoffery@housebaratheon.com",
    "id": 7718,
    "apiOnly": false
  },
  {
    "userid": "rickon@housestark.com",
    "firstName": "Rickon",
    "lastName": "Stark",
    "emailAddress": "rickon@housestark.com",
    "id": 8612,
    "apiOnly": false
  }
]
```

>[!NOTE]
>
>上記のコードサンプルでは、表示される`userid` は、Adobe IMS に移行されたお客様の ID です。 まだ移行していないお客様には、`userid` フィールドに通常のメールアドレスが表示されます。

### ロールの参照

[ロールを取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getRolesUsingGET)エンドポイントは、すべてのロールレコードのリストを返します。

```http
GET /userservice/management/v1/users/roles.json
```

```json
[
    {
        "id": 1,
        "name": "Admin",
        "description": "All permissions",
        "type": "system",
        "hidden": false,
        "onlyAllZones": true,
        "createdAt": "20100327T18:27:42.0t+0000",
        "updatedAt": "20100327T18:27:42.0t+0000"
    },
    {
        "id": 2,
        "name": "Standard User",
        "description": "All permissions except Admin",
        "type": "system",
        "hidden": false,
        "onlyAllZones": false,
        "createdAt": "20100327T18:27:42.0t+0000",
        "updatedAt": "20180423T02:33:29.0t+0000"
    },
    {
        "id": 24,
        "name": "RTP Launcher",
        "description": "Role required for launcher in RTP",
        "type": "system",
        "hidden": false,
        "onlyAllZones": false,
        "createdAt": "20151024T01:45:40.0t+0000",
        "updatedAt": "20171024T23:41:24.0t+0000"
    },
    {
        "id": 25,
        "name": "RTP Editor",
        "description": "Role required for editor in RTP",
        "type": "system",
        "hidden": false,
        "onlyAllZones": false,
        "createdAt": "20151024T01:45:40.0t+0000",
        "updatedAt": "20171024T23:41:24.0t+0000"
    },
    {
        "id": 101,
        "name": "Analytics User",
        "description": "Has access to Analytics",
        "type": "custom",
        "hidden": false,
        "onlyAllZones": false,
        "createdAt": "20100327T18:27:42.0t+0000",
        "updatedAt": "20180423T02:33:29.0t+0000"
    },
    {
        "id": 102,
        "name": "Marketing User",
        "description": "All permissions except Admin",
        "type": "custom",
        "hidden": false,
        "onlyAllZones": false,
        "createdAt": "20100327T18:27:42.0t+0000",
        "updatedAt": "20100327T18:27:42.0t+0000"
    },
    {
        "id": 103,
        "name": "Web Designer",
        "description": "Has access to Design Studio except approval permission",
        "type": "custom",
        "hidden": false,
        "onlyAllZones": false,
        "createdAt": "20100327T18:27:42.0t+0000",
        "updatedAt": "20180423T02:33:29.0t+0000"
    }
]
```

### ワークスペースの参照

[ワークスペースを取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getWorkspacesUsingGET)エンドポイントは、すべてのワークスペースレコードのリストを返します。

```http
GET /userservice/management/v1/users/workspaces.json
```

```json
[
  {
    "id": 1,
    "name": "Default",
    "description": "Initial workspace for Marketing Activities, Design Studio, and so on.",
    "globalViz": 0,
    "status": "active",
    "currencyInfo": null,
    "createdAt": "20160910T23:08:05.0t+0000",
    "updatedAt": "20160910T23:08:05.0t+0000"
  },
  {
    "id": 1008,
    "name": "World",
    "description": "",
    "globalViz": 0,
    "status": "active",
    "currencyInfo": null,
    "createdAt": "20181119T21:59:36.0t+0000",
    "updatedAt": "20181119T21:59:36.0t+0000"
  },
  {
    "id": 1009,
    "name": "Reproduction - US English - All Leads",
    "description": "A Workspace for recreating customer-reported problems.",
    "globalViz": 1,
    "status": "active",
    "currencyInfo": null,
    "createdAt": "20190129T23:36:37.0t+0000",
    "updatedAt": "20190129T23:36:37.0t+0000"
  },
  {
    "id": 1010,
    "name": "US",
    "description": "United States - Qualified Leads",
    "globalViz": 0,
    "status": "active",
    "currencyInfo": null,
    "createdAt": "20190322T15:55:40.0t+0000",
    "updatedAt": "20190322T15:55:40.0t+0000"
  }
]
```

## ユーザの招待

[Adobe IMS 統合サブスクリプション](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)では、このエンドポイントは [API 専用ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user)の招待のみをサポートします。 [標準ユーザ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)を招待するには、代わりに [Adobe User Management API](https://developer.adobe.com/umapi/) を使用します。

[Invite User](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/inviteUserUsingPOST) エンドポイントは、新しいユーザーに「Welcome to Marketo」のメール招待状を送信します。 このメールには、「Marketoにログイン」リンクが含まれています。 受信者はリンクを選択し、パスワードを作成してMarketoにアクセスできます。

受信者が招待を受け入れるまで、そのステータスは「保留中」であり、ユーザーレコードを編集することはできません。 保留中の招待状は、送信されてから7日後に有効期限が切れます。 詳しくは、[Marketo ユーザー管理ドキュメント ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)を参照してください。

リクエスト本文にパラメーターを`application/json`形式で渡します。

必要なパラメーターは`emailAddress`、`firstName`、`lastName`、および`userRoleWorkspaces`です。 `userRoleWorkspaces` パラメーターは、`accessRoleId`および`workspaceId`属性を含むオブジェクトの配列です。

`userid` パラメーターは、ログインに使用される一意のユーザーIDであり、電子メールアドレスとしてフォーマットする必要があります。 リクエストが`userid`を省略した場合、その値はデフォルトで`emailAddress`の値になります。

ブール値の `apiOnly` パラメーターは、ユーザが [API 専用ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user)であるかどうかを指定します。 `expiresAt` パラメーターは、ユーザーログインの有効期限を指定し、ミリ秒単位でW3C ISO-8601形式を使用します。 リクエストが`expiresAt`を省略した場合、ユーザーは期限切れになりません。 `reason` パラメーターは、招待の理由を説明します。

招待が成功すると、エンドポイントは「true」を返します。 それ以外の場合は、エラーメッセージが返されます。

```http
POST /userservice/management/v1/users/invite.json
```

```text
Content-Type: application/json
```

```json
{
  "emailAddress": "daenerys@housetargaryen.com",
  "firstName": "Daenerys",
  "lastName": "Targaryen",
  "expiresAt": "2020-12-31T23:59:59-05:00",
  "reason": "Keeper of dragons",
  "userRoleWorkspaces": [
    {
      "accessRoleId": 1,
      "workspaceId": 0
    }
  ]
}
```

```text
true
```

次の図は、新規ユーザーに送信された「Marketoへようこそ」電子メールを示しています。 件名は「Marketo Login Information」です。 送信者は、[REST API カスタムサービス ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api)に関連付けられたAPI専用ユーザーの電子メールアドレスです。 firstName、lastName、emailAddressの各パラメーターで受信者を指定します。

![ユーザ招待メール](assets/invite-user-email.png)

ユーザーは、パスワードを2回入力し、「パスワードを作成」ボタンを選択して、招待を受け入れます。 その後、利用者はMarketoへのアクセス権を取得します。

## ユーザの更新

ユーザーが招待を受け入れた後、ユーザー属性を更新したり、ユーザーを削除したりできます。 属性をリクエスト本文のパラメーターとしてapplication/json形式で渡します。

### ユーザ属性の更新

[Adobe IMS 統合サブスクリプション](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)では、このエンドポイントは [API 専用ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user)の属性の更新のみをサポートします。 [標準ユーザ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)の属性を更新するには、代わりに [Adobe User Management API](https://developer.adobe.com/umapi/) を使用します。

[ユーザ属性を更新](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/updateUserAttributeUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、単一のユーザレコードを返します。 リクエスト本文には、更新する 1 つ以上のユーザ属性（`emailAddress`、`firstName`、`lastName`、`expiresAt`）が含まれます。

```http
POST /userservice/management/v1/users/{userid}/update.json
```

```text
Content-Type: application/json
```

```json
{
  "firstName": "JAMIE",
  "lastName": "LANISTER",
  "expiresAt": "20211231T08:00:00.000t+0000"
}
```

```json
{
  "userid": "jamie@houselannister.com",
  "firstName": "JAMIE",
  "lastName": "LANISTER",
  "emailAddress": "jamie@houselannister.com",
  "optedIn": false,
  "failedLogins": 0,
  "failedDeviceCode": 0,
  "isLocked": false,
  "lockedReason": null,
  "id": 0,
  "apiOnly": false,
  "userRoleWorkspaces": [
    {
      "accessRoleId": 1,
      "accessRoleName": "Admin",
      "workspaceId": 0,
      "workspaceName": "AllZones"
    },
    {
      "accessRoleId": 2,
      "accessRoleName":
      "Standard User",
      "workspaceId": 1008,
      "workspaceName": "World"
    }
  ],
  "expiresAt": "2021-12-31T08:00:00.000t+0000"
  "lastLoginAt": "2020-02-05T01:02:23.000t+0000"
}
```

#### ユーザの削除

[Adobe IMS 統合サブスクリプション](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)では、このエンドポイントは [API 専用ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user)の削除のみをサポートします。 [標準ユーザ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)を削除するには、代わりに [Adobe User Management API](https://developer.adobe.com/umapi/) を使用します。

[ユーザを削除](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteUserUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、インスタンスから対応するユーザを削除します。 これは、破壊的な削除であり、元に戻すことはできません。 成功した場合は 200 ステータスコードが返され、それ以外の場合はエラーメッセージが返されます。

```http
POST /userservice/management/v1/users/{userid}/delete.json
```

#### 招待されたユーザの削除

[招待されたユーザを削除](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteInvitedUserUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、対応する「保留中」のユーザ（まだ招待を受け入れていないユーザ）をインスタンスから削除します。 これは、破壊的な削除であり、元に戻すことはできません。 成功した場合は 200 ステータスコードが返され、それ以外の場合はエラーメッセージが返されます。

```http
POST /userservice/management/v1/users/{userid}/invite/delete.json
```

## ロールの更新

役割は追加または削除できます。 属性をリクエスト本文のパラメーターとしてapplication/json形式で渡します。

## ロールの追加

[ロールを追加](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/addRolesUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、対応するユーザに 1 つ以上のユーザロールを追加します。 リクエスト本文には、それぞれ `accessRoleId` 属性と `workspaceId` 属性を含む 1 つ以上のオブジェクトのリストが含まれます。 成功した場合、指定したユーザの `accessRoleId/workspaceId` ペアのリスト全体が返されます。

```http
POST /userservice/management/v1/users/{userid}/roles/create.json
```

```text
Content-Type: application/json
```

```json
[
  {
    "accessRoleId": 2,
    "workspaceId": 1008
  }
]
```

```json
[
  {
    "accessRoleId": 1,
    "accessRoleName": "Admin",
    "workspaceId": 0,
    "workspaceName": "AllZones"
  },
  {
    "accessRoleId": 2,
    "accessRoleName": "Standard User",
    "workspaceId": 1008,
    "workspaceName": "World"
  }
]
```

## ロールの削除

[ロールを削除](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteRolesUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、対応するユーザから 1 つ以上のユーザロールを削除します。 リクエスト本文には、それぞれ `accessRoleId` 属性と `workspaceId` 属性を含む 1 つ以上のオブジェクトのリストが含まれます。 成功した場合、指定したユーザの accessRoleId/workspaceId ペアの残りのリストが返されます。

```http
POST /userservice/management/v1/users/{userid}/roles/delete.json
```

```text
Content-Type: application/json
```

```json
[
  {
    "accessRoleId": 2,
    "workspaceId": 1008
  }
]
```

```json
[
  {
    "accessRoleId": 1,
    "accessRoleName": "Admin",
    "workspaceId": 0,
    "workspaceName": "AllZones"
  }
]
```
