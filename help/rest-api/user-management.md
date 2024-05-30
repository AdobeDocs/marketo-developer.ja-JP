---
title: "ユーザー管理"
feature: REST API
description: 「ユーザーレコードに対する CRUD 操作の実行」
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---


# ユーザ管理

[User Management エンドポイントのリファレンス](https://developer.adobe.com/marketo-apis/api/user/)

Marketoには、Marketo内のユーザーレコードに対して CRUD 操作を実行できる一連の User Management エンドポイントが用意されています。 ユーザーを作成するには、招待をユーザーに送信します。ユーザーはパスワードを設定し、初めてMarketoにアクセスできるようになります。

他のMarketo REST API とは異なり、User Management API を使用する場合は、次の点に注意してください。

- 認証するアクセストークンを送信するには、HTTP ヘッダーメソッドを使用する必要があります。 アクセストークンをクエリ文字列パラメーターとして渡すことはできません。 認証に関する詳細は、です [こちら](authentication.md).
- のユーザーロールを作成する場合、2 つの異なるグループから 1 つのロール権限を選択する必要があります [カスタムサービス](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api) rest API の場合：
   1. からの「ユーザーへのアクセス」権限 [管理者にアクセス](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions) グループ
   1. から「User Management Api へのアクセス」 [アクセス API](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions) グループ
- 応答本文には、呼び出しの成功または失敗を示す「success」ブール値属性が含まれていません。 代わりに、HTTP 応答ステータスコードを評価する必要があります。 呼び出しが成功した場合は、200 ステータスコードが返されます。 呼び出しが失敗した場合は、200 レベル以外のステータスコードが返され、応答本文には、エラーコードと説明的なエラーメッセージを含む標準の「エラー」配列が含まれます。
- 日時文字列の形式は、「yyyyMMdd&#39;T&#39;HH」です:mm:ss.SSS&#39;t&#39;+|-hhmm&#39;&#39; これは、createdAt、updatedAt、expiresAt の各属性に適用されます。
- User Management API エンドポイントには、他のエンドポイントのようにプレフィックス「/rest」が付きません。

## クエリ

ユーザー管理のクエリサポートには、すべてのユーザー、役割、ワークスペースを取得する機能が含まれます。 また、ユーザー ID ごとに 1 つのユーザーレコードを取得したり、ユーザー ID ごとに役割/ワードスペースレコードを取得したりできます。

### ユーザー（ID 別）

この [Id によるユーザーの取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUserUsingGET) エンドポイントはを 1 つ取ります `userid` path パラメーターを指定し、招待を承諾したユーザーのユーザーレコードを 1 つ返します。

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

この [Id で招待ユーザーを取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getInvitedUserUsingGET) エンドポイントはを 1 つ取ります `userid` パスパラメーターを指定し、「保留中」のユーザー（まだ招待を受け入れていないユーザー）の単一のユーザーレコードを返します。

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

この [Id による役割とワークスペースの取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUserRolesAndWorkspacesUsingGET) エンドポイントはを 1 つ取ります `userid` パスパラメーターを渡し、ユーザーの役割およびワークスペースレコードのリストを返します。 応答には、指定したユーザーの役割、ワークスペース ID および名前を含む 1 つのオブジェクトを持つ配列が含まれています。

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

この [ユーザーの取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getUsersUsingGET) エンドポイントは、すべてのユーザーレコードのリストを返します。 オプション `pageSize` パラメーターは、返されるエントリの最大数を指定する整数です。 デフォルトは 20 です。 最大値は 200 です。 オプション `pageOffset` パラメータは、エントリの取得を開始する場所を指定する整数です。 と併用できます `pageSize`. デフォルトは 0 です。

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

### 役割の参照

この [役割の取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getRolesUsingGET) エンドポイントは、すべての役割レコードのリストを返します。

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

この [ワークスペースを取得](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/getWorkspacesUsingGET) エンドポイントは、すべての workspace レコードのリストを返します。

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

日付： [Adobe IMS統合サブスクリプション](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)。このエンドポイントはの招待をサポートします [API のみのユーザー](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user) のみ。 招待する [標準ユーザー](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)、を使用します [AdobeUser Management API](https://developer.adobe.com/umapi/) その代わり。

この [ユーザーを招待](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/inviteUserUsingPOST) 新規ユーザーに「Marketoへようこそ」というメール招待状を送信するためのエンドポイント。 メール本文には、ユーザーが初めてMarketoにアクセスできる「Marketoにログイン」リンクが含まれています。 招待を受け入れるために、メール受信者が「Marketoにログイン」リンクをクリックし、パスワードを作成して、Marketoにアクセスできます。 受け入れプロセスが完了するまで、招待は「保留中」となり、ユーザーレコードは編集できません。 保留中の招待は、送信されてから 7 日後に有効期限が切れます。 ユーザー管理の詳細については、こちらを参照してください [こちら](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users).

パラメーターは、リクエスト本文で application/json 形式で渡されます。

次のパラメーターが必要です。  `emailAddress`, `firstName`, `lastName, userRoleWorkspaces`. この `userRoleWorkspaces` parameter は、を含むオブジェクトの配列です。 `accessRoleId` および `workspaceId` 属性。

この `userid` パラメーターは、ユーザーログイン目的で使用される一意のユーザー識別子文字列値で、メールアドレスの形式にする必要があります。 リクエストで指定されていない場合、値 `userid` デフォルトは、に指定された値です。 `emailAddress` パラメーター。

ブール値 `apiOnly` パラメーターは、ユーザーがであるかどうかを指定します [API のみのユーザー](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user). この `expiresAt` パラメーターは、ユーザーログインの有効期限を指定し、W3C ISO-8601 形式（ミリ秒単位なし）で書式設定されます。 リクエストで指定されていない場合、ユーザーの有効期限はありません。 この `reason` パラメーターは、ユーザー招待の理由を説明する文字列です。

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

以下は、新しいユーザーに送信される「Marketoへようこそ」というメール招待の例です。 メールの件名は「Marketo Login Information」で、送信者はに関連付けられた API 専用ユーザーのメールアドレスです [REST API カスタムサービス](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api)を指定します。また、受信者は、firstName、lastName および emailAddress パラメーターで指定されたとおりに指定されます。

![Invite User Email](assets/invite-user-email.png)

ユーザーは、パスワードを 2 回入力し、「パスワードを作成」ボタンをクリックして、電子メールの招待を受け入れます。 その後、Marketoへのアクセス権が初めて付与されます。

## ユーザーの更新

ユーザーの更新サポートには、ユーザー属性を更新する機能や、ユーザーを削除する機能が含まれます。 更新できるのは、招待を承諾したユーザーのみです。 属性は、パラメーターとしてリクエスト本文に application/json 形式で渡されます。

### ユーザー属性の更新

日付： [Adobe IMS統合サブスクリプション](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)、このエンドポイントはの属性の更新をサポートしています [API のみのユーザー](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user) のみ。 の属性を更新するには [標準ユーザー](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)、を使用します [AdobeUser Management API](https://developer.adobe.com/umapi/) その代わり。

この [ユーザー属性の更新](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/updateUserAttributeUsingPOST) エンドポイントはを 1 つ取ります `userid` パスパラメーターを渡し、単一のユーザーレコードを返します。 リクエスト本文には、更新する 1 つ以上のユーザー属性が含まれます。 `emailAddress`, `firstName`, `lastName`, `expiresAt`.

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

日付： [Adobe IMS統合サブスクリプション](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)。このエンドポイントは、の削除をサポートします。 [API のみのユーザー](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/create-an-api-only-user) のみ。 削除対象 [標準ユーザー](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/managing-marketo-users)、を使用します [AdobeUser Management API](https://developer.adobe.com/umapi/) その代わり。

この [ユーザーの削除](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteUserUsingPOST) エンドポイントはを 1 つ取ります `userid` パスパラメーターを指定し、対応するユーザーをインスタンスから削除します。 これは破壊的な削除であり、元に戻すことはできません。 成功した場合は 200 ステータスコードが返され、失敗した場合はエラーメッセージが返されます。

```
POST /userservice/management/v1/users/{userid}/delete.json
```

#### 招待ユーザーの削除

この [招待ユーザーの削除](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteInvitedUserUsingPOST) エンドポイントはを 1 つ取ります `userid` パスパラメーターを使用し、対応する「保留中」のユーザーをインスタンスから削除します（ユーザーはまだ招待を受け入れていません）。 これは破壊的な削除であり、元に戻すことはできません。 成功した場合は 200 ステータスコードが返され、失敗した場合はエラーメッセージが返されます。

```
POST /userservice/management/v1/users/{userid}/invite/delete.json
```

## 役割の更新

役割の更新サポートには、役割を追加および削除する機能が含まれます。 属性は、パラメーターとしてリクエスト本文に application/json 形式で渡されます。

## 役割の追加

この [役割の追加](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/addRolesUsingPOST) エンドポイントはを 1 つ取ります `userid` パスパラメーターを使用し、1 つ以上のユーザーの役割を対応するユーザーに追加します。 リクエスト本文には、1 つ以上のオブジェクトのリストが含まれ、各オブジェクトには以下の情報が含まれます。  `accessRoleId` および `workspaceId` 属性。 成功した場合、のリスト全体 `accessRoleId/workspaceId` 指定したユーザーのペアが返されます。

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

この [役割の削除](https://developer.adobe.com/marketo-apis/api/user/#tag/User-Management/operation/deleteRolesUsingPOST) エンドポイントはを 1 つ取ります `userid` パスパラメーターを指定し、対応するユーザーから 1 つ以上のユーザーの役割を削除します。 リクエスト本文には、1 つ以上のオブジェクトのリストが含まれ、各オブジェクトには以下の情報が含まれます。  `accessRoleId` および `workspaceId` 属性。 成功すると、指定したユーザーの accessRoleId と workspaceId のペアの残りのリストが返されます。

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
