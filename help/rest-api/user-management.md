---
title: ユーザ管理
feature: REST API
description: ユーザレコードに対して CRUD 操作を実行します。
exl-id: 2a58f496-0fe6-4f7e-98ef-e9e5a017c2de
source-git-commit: b89a22e136a7b81a5cd1af9ba7b0caa41c619ff4
workflow-type: ht
source-wordcount: '1180'
ht-degree: 100%

---

# ユーザ管理

[ユーザ管理エンドポイント参照](https://developer.adobe.com/marketo-apis/api/user/)

Marketo には、Marketo 内のユーザレコードに対して CRUD 操作を実行できる一連のユーザ管理エンドポイントが用意されています。ユーザは、ユーザに招待状を送信することで作成され、このユーザはパスワードを設定して初めて Marketo へのアクセス権を取得できます。

User Management API を使用する際、他の Marketo REST API とは次の点が異なります。

- 認証するには、HTTP ヘッダーメソッドを使用してアクセストークンを送信する必要があります。 アクセストークンをクエリ文字列パラメーターとして渡すことはできません。認証について詳しくは、[こちら](authentication.md)を参照してください。
- REST API の[カスタムサービス](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api)のユーザロールを作成する際は、2 つの異なるグループからロール権限を選択する必要があります。
   1. [管理にアクセス](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions)グループの「ユーザにアクセス」権限
   1. [Access API](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions) グループの「Access User Management API」
- 応答本文には、呼び出しの成功または失敗を示す success ブール属性が含まれていません。代わりに、HTTP 応答ステータスコードを評価する必要があります。呼び出しが成功すると、200 ステータスコードが返されます。呼び出しが失敗すると、200 レベル以外のステータスコードが返され、応答本文にはエラーコードとエラーの説明メッセージを含む標準の「エラー」配列が含まれます。
- 日時文字列の形式は、`yyyyMMdd'T'HH:mm:ss.SSS't'+|-hhmm` です。これは、`createdAt`、`updatedAt`、`expiresAt` の属性に適用されます。
- ユーザ管理 API エンドポイントには、他のエンドポイントのように「/rest」というプレフィックスは付きません。

## クエリ

ユーザ管理のクエリサポートには、すべてのユーザ、ロール、ワークスペースを取得する機能が含まれます。また、ユーザ ID による単一のユーザレコードを取得したり、ユーザ ID でロール／ワークスペースレコードを取得したりすることもできます。

### ID 別のユーザ

[ID によるユーザの取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUserUsingGET)エンドポイントは、単一の `userid` パスパラメーターを受け取り、招待を受け入れたユーザの単一のユーザレコードを返します。

```
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

```
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

[ID によるロールとワークスペースをの取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUserRolesAndWorkspacesUsingGET)エンドポイントは、単一の `userid` パスパラメーターを受け取り、ユーザロールとワークスペースレコードのリストを返します。応答には、指定されたユーザに対応するロールとワークスペースのIDおよび名前を含むオブジェクトが 1 つ含まれた配列が含まれます。

```
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

[ユーザを取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUsersUsingGET)エンドポイントは、すべてのユーザレコードのリストを返します。オプションの `pageSize` パラメーターは、返されるエントリの最大数を指定する整数です。初期設定は 20 です。最大値は 200 です。オプションの `pageOffset` パラメーターは、エントリの取得を開始する場所を指定する整数です。`pageSize` と併用できます。初期設定は 0 です。

```
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
>上記のコードサンプルでは、表示される`userid` は、Adobe IMS に移行されたお客様の ID です。まだ移行していないお客様には、`userid` フィールドに通常のメールアドレスが表示されます。

### ロールの参照

[ロールを取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getRolesUsingGET)エンドポイントは、すべてのロールレコードのリストを返します。

```
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

```
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

[Adobe IMS 統合サブスクリプション](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)では、このエンドポイントは [API 専用ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user)の招待のみをサポートします。[標準ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)を招待するには、代わりに [Adobe User Management API](https://developer.adobe.com/umapi/) を使用します。

「Marketo へようこそ」というメール招待状を新規ユーザに送信するための[ユーザを招待](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/inviteUserUsingPOST)エンドポイントです。メール本文には、初めて Marketo にアクセスするユーザを許可する「Marketo にログイン」リンクが含まれます。メールの受信者が招待を受け入れるには、「Marketo にログイン」リンクをクリックし、パスワードを作成して、Marketo へのアクセス権を取得します。受け入れプロセスが完了するまで、招待は「保留中」となり、ユーザレコードは編集できません。保留中の招待状は、送信後 7 日で期限切れになります。ユーザの管理について詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)を参照してください。

パラメーターは、リクエスト本文で `application/json` 形式で渡されます。

`emailAddress`、`firstName`、`lastName, userRoleWorkspaces` パラメーターは必須です。`userRoleWorkspaces` パラメーターは、`accessRoleId` 属性と `workspaceId` 属性を含むオブジェクトの配列です。

`userid` パラメーターは、ユーザログインの目的で使用される一意のユーザ ID の文字列値であり、メールアドレスの形式にする必要があります。リクエストい指定されていない場合、`userid` の値はデフォルトで `emailAddress` パラメーターで指定された値になります。

ブール値の `apiOnly` パラメーターは、ユーザが [API 専用ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user)であるかどうかを指定します。`expiresAt` パラメーターは、ユーザログインの有効期限を指定し、W3C ISO-8601 形式（ミリ秒単位なし）を使用して書式設定されます。リクエストで指定されていない場合、ユーザは期限切れになりません。`reason` パラメーターは、ユーザの招待理由を説明する文字列です。

エンドポイントは、成功した場合は「true」の値を返し、それ以外の場合はエラーメッセージを返します。

```
POST /userservice/management/v1/users/invite.json
```

```
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

```
true
```

以下は、新規ユーザに送信される「Marketo へようこそ」というメール招待状の例です。メールの件名は「Marketo ログイン情報」、送信者は [REST API カスタムサービス](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api)に関連付けられた API 専用ユーザのメールアドレス、受信者は firstName、lastName、emailAddress パラメーターで指定されています。

![ユーザ招待メール](assets/invite-user-email.png)

ユーザは、パスワードを 2 回入力し、「パスワードを作成」ボタンをクリックして、メール招待状を受け入れます。その後、Marketo へのアクセス権が初めて付与されます。

## ユーザの更新

ユーザの更新サポートには、ユーザ属性を更新したり、ユーザを削除したりする機能が含まれます。招待を受け入れたユーザのみが更新できます。属性は、リクエスト本文のパラメーターとして application/json 形式で渡されます。

### ユーザ属性の更新

[Adobe IMS 統合サブスクリプション](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)では、このエンドポイントは [API 専用ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user)の属性の更新のみをサポートします。[標準ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)の属性を更新するには、代わりに [Adobe User Management API](https://developer.adobe.com/umapi/) を使用します。

[ユーザ属性を更新](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/updateUserAttributeUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、単一のユーザレコードを返します。リクエスト本文には、更新する 1 つ以上のユーザ属性（`emailAddress`、`firstName`、`lastName`、`expiresAt`）が含まれます。

```
POST /userservice/management/v1/users/{userid}/update.json
```

```
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

[Adobe IMS 統合サブスクリプション](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)では、このエンドポイントは [API 専用ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user)の削除のみをサポートします。[標準ユーザ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)を削除するには、代わりに [Adobe User Management API](https://developer.adobe.com/umapi/) を使用します。

[ユーザを削除](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteUserUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、インスタンスから対応するユーザを削除します。これは、破壊的な削除であり、元に戻すことはできません。成功した場合は 200 ステータスコードが返され、それ以外の場合はエラーメッセージが返されます。

```
POST /userservice/management/v1/users/{userid}/delete.json
```

#### 招待されたユーザの削除

[招待されたユーザを削除](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteInvitedUserUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、対応する「保留中」のユーザ（まだ招待を受け入れていないユーザ）をインスタンスから削除します。これは、破壊的な削除であり、元に戻すことはできません。成功した場合は 200 ステータスコードが返され、それ以外の場合はエラーメッセージが返されます。

```
POST /userservice/management/v1/users/{userid}/invite/delete.json
```

## ロールの更新

ロールの更新サポートには、ロールの追加と削除の機能が含まれます。属性は、リクエスト本文のパラメーターとして application/json 形式で渡されます。

## ロールの追加

[ロールを追加](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/addRolesUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、対応するユーザに 1 つ以上のユーザロールを追加します。 リクエスト本文には、それぞれ `accessRoleId` 属性と `workspaceId` 属性を含む 1 つ以上のオブジェクトのリストが含まれます。成功した場合、指定したユーザの `accessRoleId/workspaceId` ペアのリスト全体が返されます。

```
POST /userservice/management/v1/users/{userid}/roles/create.json
```

```
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

[ロールを削除](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteRolesUsingPOST)エンドポイントは、単一の `userid` パスパラメーターを受け取り、対応するユーザから 1 つ以上のユーザロールを削除します。リクエスト本文には、それぞれ `accessRoleId` 属性と `workspaceId` 属性を含む 1 つ以上のオブジェクトのリストが含まれます。成功した場合、指定したユーザの accessRoleId/workspaceId ペアの残りのリストが返されます。

```
POST /userservice/management/v1/users/{userid}/roles/delete.json
```

```
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
