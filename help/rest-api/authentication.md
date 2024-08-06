---
title: 認証
feature: REST API
description: API を使用するためのMarketo ユーザーの認証。
exl-id: f89a8389-b50c-4e86-a9e4-6f6acfa98e7e
source-git-commit: e0fc654efe4501f734ab5158ce0bfd3ed08896ce
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---

# 認証

Marketoの REST API は、2-legged OAuth 2.0 で認証されます。クライアント ID とクライアント秘密鍵は、定義したカスタムサービスによって提供されます。 各カスタムサービスは、特定のアクションを実行するようにサービスを承認する一連の役割と権限を持つ API 専用ユーザーが所有しています。 アクセストークンは、1 つのカスタムサービスに関連付けられます。 アクセストークンの有効期限は、インスタンスに存在する他のカスタムサービスに関連付けられたトークンとは独立しています。

## アクセストークンの作成

`Client ID` と `Client Secret` は、**[!UICONTROL Admin]**/**[!UICONTROL Integration]**/**[!UICONTROL LaunchPoint]** メニューでカスタムサービスを選択し、「**[!UICONTROL 詳細を表示]**」をクリックします。

![REST サービスの詳細の取得 ](assets/authentication-service-view-details.png)

![ ランチポイント資格情報 ](assets/admin-launchpoint-credentials.png)

この `Identity URL` は、「REST API」セクションの **[!UICONTROL 管理者]**/**[!UICONTROL 統合]**/**[!UICONTROL web サービス]** メニューにあります。

次のように、HTTP GET（またはPOST）リクエストを使用してアクセストークンを作成します。

```
GET <Identity URL>/oauth/token?grant_type=client_credentials&client_id=<Client Id>&client_secret=<Client Secret>
```

リクエストが有効な場合は、次のような JSON 応答が返されます。

```json
{
    "access_token": "cdf01657-110d-4155-99a7-f986b2ff13a0:int",
    "token_type": "bearer",
    "expires_in": 3599,
    "scope": "apis@acmeinc.com"
}
```

応答定義

- `access_token` – その後の呼び出しで渡して、ターゲットインスタンスで認証するトークン。
- `token_type` - OAuth 認証方法。
- `expires_in` – 現在のトークンの残り存続期間（秒単位）（この時間を超えると無効になります）。 アクセストークンが最初に作成されたときの有効期間は 3600 秒または 1 時間です。
- `scope` – 認証に使用されたカスタムサービスの所有ユーザー。

## アクセストークンの使用

REST API メソッドを呼び出す場合は、呼び出しを正常に実行するために、すべての呼び出しにアクセストークンを含める必要があります。

呼び出しにトークンを含める方法、HTTP ヘッダーとして含める方法およびクエリ文字列パラメーターとして含める方法は 2 つあります。

1. HTTP ヘッダー

   `Authorization: Bearer cdf01657-110d-4155-99a7-f986b2ff13a0:int`

1. クエリパラメーター

   `access_token=cdf01657-110d-4155-99a7-f986b2ff13a0:int`

   >[!IMPORTANT]
   >
   >**access_token** クエリパラメーターを使用した認証のサポートは、今後のリリースで削除される予定です。 プロジェクトでクエリパラメーターを使用してアクセストークンを渡す場合は、できるだけ早く **Authorization** ヘッダーを使用するように更新する必要があります。 新しい開発では、**Authorization** ヘッダーのみを使用する必要があります。

## ヒントとベストプラクティス

アクセストークンの有効期限の管理は、統合がスムーズに動作し、通常の操作中に予期しない認証エラーが発生するのを防ぐために重要です。 統合の認証を設計する場合は、ID 応答に含まれるトークンと有効期限を必ず保存してください。

REST 呼び出しを行う前に、残りの存続期間に基づいてトークンの有効性を確認する必要があります。 トークンの有効期限が切れている場合は、[Identity](https://developer.adobe.com/marketo-apis/api/identity/#tag/Identity/operation/identityUsingGET)endpoint を呼び出して更新します。 これにより、トークンの有効期限が切れていることが原因で REST 呼び出しが失敗することがなくなります。 これにより、予測可能な方法で REST 呼び出しの待ち時間を管理できます。これは、エンドユーザーに接続するアプリケーションにとって重要です。

期限切れトークンを使用して REST 呼び出しを認証すると、REST 呼び出しは失敗し、602 エラーコードが返されます。 REST 呼び出しの認証に無効なトークンが使用されている場合は、601 エラーコードが返されます。 これらのコードのいずれかが受信された場合、クライアントは ID エンドポイントを呼び出してトークンを更新する必要があります。

トークンの有効期限が切れる前に ID エンドポイントを呼び出した場合、同じトークンと残りの存続期間が応答で返されます。

アクセストークンは、ユーザーベースではなく、カスタムサービスごとに所有されることに注意してください。 2 つの ID 応答が同じユーザーに対してスコープされている場合でも、2 つの異なるサービスの資格情報で作成されたアクセストークンと有効期限は互いに独立しています。 同じアプリケーションに複数の資格情報セットがある場合は、このことに注意してください。クライアント ID は、それらを個別に管理するための便利なキーです。
