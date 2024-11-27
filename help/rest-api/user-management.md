---
title: ユーザ管理
feature: REST API
description: ユーザーレコードに対して CRUD 操作を実行します。
exl-id: 2a58f496-0fe6-4f7e-98ef-e9e5a017c2de
source-git-commit: b89a22e136a7b81a5cd1af9ba7b0caa41c619ff4
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 1%

---

# ユーザ管理

[User Management エンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/user/)

Marketoには、Marketo内のユーザーレコードに対して CRUD 操作を実行できる一連の User Management エンドポイントが用意されています。 ユーザーを作成するには、招待をユーザーに送信します。ユーザーはパスワードを設定し、初めてMarketoにアクセスできるようになります。

他のMarketo REST API とは異なり、User Management API を使用する場合は、次の点に注意してください。

- 認証するアクセストークンを送信するには、HTTP ヘッダーメソッドを使用する必要があります。 アクセストークンをクエリ文字列パラメーターとして渡すことはできません。 認証の詳細については、[ こちら ](authentication.md) を参照してください。
- REST API 用の [ カスタムサービス ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api) のユーザーの役割を作成する場合は、2 つの異なるグループから役割の権限を選択する必要があります。
   1. 「管理者にアクセス ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions) グループからの「ユーザーにアクセス [ 権限
   1. [Access API](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions) グループの「User Management Api へのアクセス」
- 応答本文には、呼び出しの成功または失敗を示す「success」ブール値属性が含まれていません。 代わりに、HTTP 応答ステータスコードを評価する必要があります。 呼び出しが成功した場合は、200 ステータスコードが返されます。 呼び出しが失敗した場合は、200 レベル以外のステータスコードが返され、応答本文には、エラーコードと説明的なエラーメッセージを含む標準の「エラー」配列が含まれます。
- 日時文字列の形式は `yyyyMMdd'T'HH:mm:ss.SSS't'+|-hhmm` です。 これは、属性 `createdAt`、`updatedAt`、`expiresAt` に適用されます。
- User Management API エンドポイントには、他のエンドポイントのようにプレフィックス「/rest」が付きません。

## クエリ

ユーザー管理のクエリサポートには、すべてのユーザー、役割、ワークスペースを取得する機能が含まれます。 また、ユーザー ID によって 1 つのユーザーレコードを取得したり、ユーザー ID によって役割/ワークスペースレコードを取得したりできます。

### ユーザー（ID 別）

[ID によるユーザーの取得 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUserUsingGET) エンドポイントは、単一の `userid` パスパラメーターを受け取り、招待を承諾したユーザーに関する単一のユーザーレコードを返します。

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

### 招待ユーザー（Id 別）

[ID で招待ユーザーを取得 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getInvitedUserUsingGET) エンドポイントは、単一の `userid` パスパラメーターを受け取り、「保留中」のユーザー（まだ招待を受け入れていない）に対して単一のユーザーレコードを返します。

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

### 役割とワークスペース （Id 別）

[ID による役割とワークスペースの取得 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUserRolesAndWorkspacesUsingGET) エンドポイントは、単一の `userid` パスパラメーターを受け取り、ユーザーの役割とワークスペースのレコードのリストを返します。 応答には、指定したユーザーの役割、ワークスペース ID および名前を含む 1 つのオブジェクトを持つ配列が含まれています。

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

### ユーザーの参照

[ ユーザーを取得 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUsersUsingGET) エンドポイントは、すべてのユーザーレコードのリストを返します。 オプションの `pageSize` パラメーターは、返されるエントリの最大数を指定する整数です。 デフォルトは 20 です。 最大値は 200 です。 オプションの `pageOffset` パラメーターは、エントリの取得を開始する場所を指定する整数です。 `pageSize` と併用できます。 初期設定は 0 です。

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
>上記のコードサンプルでは、Adobe IMSに移行されたお客様の `userid` が表示されます。 移行されていないお客様には、`userid` フィールドに通常のメールアドレスが表示されます。

### 役割の参照

[ 役割を取得 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getRolesUsingGET) エンドポイントは、すべての役割レコードのリストを返します。

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

[ ワークスペースを取得 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getWorkspacesUsingGET) エンドポイントは、すべてのワークスペースレコードのリストを返します。

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

## ユーザーの招待

[Adobe IMS統合サブスクリプション ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview) では、このエンドポイントは [API のみのユーザー ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user) の招待のみをサポートします。 [ 標準ユーザー ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users) を招待するには、代わりに [AdobeUser Management API](https://developer.adobe.com/umapi/) を使用します。

[ ユーザーを招待 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/inviteUserUsingPOST) エンドポイントは、「Marketoへようこそ」という E メール招待状を新規ユーザーに送信します。 メール本文には、ユーザーが初めてMarketoにアクセスできる「Marketoにログイン」リンクが含まれています。 招待を受け入れるために、メール受信者が「Marketoにログイン」リンクをクリックし、パスワードを作成して、Marketoにアクセスできます。 受け入れプロセスが完了するまで、招待は「保留中」となり、ユーザーレコードは編集できません。 保留中の招待は、送信されてから 7 日後に有効期限が切れます。 ユーザー管理の詳細については、[ こちら ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users) を参照してください。

パラメーターは、リクエスト本文で `application/json` 形式で渡されます。

次のパラメーターが必要です。  `emailAddress`、`firstName`、`lastName, userRoleWorkspaces`。 `userRoleWorkspaces` パラメーターは、`accessRoleId` および `workspaceId` 属性を含むオブジェクトの配列です。

`userid` パラメーターは、ユーザーログイン目的で使用される一意のユーザー識別子文字列値で、メールアドレスの形式にする必要があります。 リクエストに値が指定されていない場合、`userid` のデフォルト値はパラメーターに指定された値 `emailAddress` なります。

ブール値 `apiOnly` パラメーターは、ユーザーが [API のみのユーザー ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user) かどうかを指定します。 `expiresAt` パラメーターは、ユーザーログインの有効期限を指定し、W3C ISO-8601 形式（ミリ秒単位なし）で書式設定します。 リクエストで指定されていない場合、ユーザーの有効期限はありません。 `reason` パラメーターは、ユーザー招待の理由を説明する文字列です。

エンドポイントは、成功した場合は「true」の値を返し、失敗した場合はエラーメッセージを返します。

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

以下は、新しいユーザーに送信される「Marketoへようこそ」というメール招待の例です。 メールの件名は「Marketo Login Information」で、送信者は [REST API カスタムサービス ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api) に関連付けられている API 専用ユーザーのメールアドレスで、受信者は firstName、lastName、emailAddress パラメーターで指定されています。

![Invite User Email](assets/invite-user-email.png)

ユーザーは、パスワードを 2 回入力し、「パスワードを作成」ボタンをクリックして、電子メールの招待を受け入れます。 その後、Marketoへのアクセス権が初めて付与されます。

## ユーザーの更新

ユーザーの更新サポートには、ユーザー属性を更新する機能や、ユーザーを削除する機能が含まれます。 更新できるのは、招待を承諾したユーザーのみです。 属性は、パラメーターとしてリクエスト本文に application/json 形式で渡されます。

### ユーザー属性の更新

[Adobe IMS統合サブスクリプション ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview) では、このエンドポイントは [API のみのユーザー ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user) の属性の更新のみをサポートしています。 [ 標準ユーザー ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users) の属性を更新するには、代わりに [AdobeUser Management API](https://developer.adobe.com/umapi/) を使用します。

[ ユーザー属性を更新 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/updateUserAttributeUsingPOST) エンドポイントは、単一の `userid` パスパラメーターを受け取り、単一のユーザーレコードを返します。 リクエスト本文には、更新する 1 つ以上のユーザー属性（`emailAddress`、`firstName`、`lastName`、`expiresAt`）が含まれます。

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

[Adobe IMS統合サブスクリプション ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview) では、このエンドポイントは [API のみのユーザー ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user) の削除のみをサポートします。 [ 標準ユーザー ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users) を削除するには、代わりに [AdobeUser Management API](https://developer.adobe.com/umapi/) を使用します。

[ ユーザーを削除 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteUserUsingPOST) エンドポイントは、1 つの `userid` パスパラメーターを受け取り、対応するユーザーをインスタンスから削除します。 これは破壊的な削除であり、元に戻すことはできません。 成功した場合は 200 ステータスコードが返され、失敗した場合はエラーメッセージが返されます。

```
POST /userservice/management/v1/users/{userid}/delete.json
```

#### 招待ユーザーの削除

[ 招待ユーザーを削除 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteInvitedUserUsingPOST) エンドポイントは、単一の `userid` パスパラメーターを受け取り、対応する「保留中」ユーザーをインスタンスから削除します（ユーザーはまだ招待を受け入れていません）。 これは破壊的な削除であり、元に戻すことはできません。 成功した場合は 200 ステータスコードが返され、失敗した場合はエラーメッセージが返されます。

```
POST /userservice/management/v1/users/{userid}/invite/delete.json
```

## 役割の更新

役割の更新サポートには、役割を追加および削除する機能が含まれます。 属性は、パラメーターとしてリクエスト本文に application/json 形式で渡されます。

## 役割の追加

[ 役割を追加 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/addRolesUsingPOST) エンドポイントは、単一の `userid` パスパラメーターを受け取り、1 つ以上のユーザーの役割を対応するユーザーに追加します。 リクエスト本文には、1 つ以上のオブジェクトのリストが含まれ、各オブジェクトには以下の情報が含まれます。  `accessRoleId` と `workspaceId` 属性。 成功した場合は、指定したユーザーの `accessRoleId/workspaceId` ペアのリスト全体が返されます。

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

## 役割の削除

[ 役割を削除 ](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteRolesUsingPOST) エンドポイントは、単一の `userid` パスパラメーターを受け取り、対応するユーザーから 1 つ以上のユーザーの役割を削除します。 リクエスト本文には、1 つ以上のオブジェクトのリストが含まれ、各オブジェクトには以下の情報が含まれます。  `accessRoleId` と `workspaceId` 属性。 成功すると、指定したユーザーの accessRoleId と workspaceId のペアの残りのリストが返されます。

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
