---
title: 認証
feature: REST API
description: API の使用に関して Marketo ユーザを認証します。
exl-id: f89a8389-b50c-4e86-a9e4-6f6acfa98e7e
source-git-commit: 206724e5177eb9040fa36202d91b2ed9daa734c3
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 80%

---

# 認証

Marketo の REST API は、2-legged OAuth 2.0 で認証されます。クライアント ID とクライアント秘密鍵は、定義したカスタムサービスによって提供されます。各カスタムサービスは、サービスが特定のアクションを実行することを許可するロールと権限のセットを持つ API 専用ユーザによって所有されます。アクセストークンは、単一のカスタムサービスに関連付けられます。アクセストークンの有効期限は、インスタンス内に存在する場合がある他のカスタムサービスに関連付けられたトークンとは独立しています。

## アクセストークンの生成

`Client ID` と `Client Secret` は、カスタムサービスを選択し、「**[!UICONTROL 詳細を表示]**」をクリックすると、**[!UICONTROL 管理]**／**[!UICONTROL 統合]**／**[!UICONTROL Launchpoint]** メニューに表示されます。

![REST サービスの詳細を取得](assets/authentication-service-view-details.png)

![Launchpoint 資格情報](assets/admin-launchpoint-credentials.png)

`Identity URL` は、**[!UICONTROL 管理]**／**[!UICONTROL 統合]**／**[!UICONTROL Web サービス]**&#x200B;メニューの「REST API」セクションに表示されます。

次のように、HTTP GET（または POST）リクエストを使用してアクセストークンを作成します。

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

応答の定義

- `access_token` - ターゲットインスタンスで認証するのに後続の呼び出しで渡すトークン。
- `token_type` - OAuth 認証方法。
- `expires_in` - 秒単位での現在のトークンの残り有効期間（これを超えると無効になります）。アクセストークンを最初に作成した際の有効期間は 3600 秒または 1 時間です。
- `scope` - 認証に使用されたカスタムサービスの所有ユーザ。

## アクセストークンの使用

REST API メソッドを呼び出す場合は、呼び出しを正常に実行するために、すべての呼び出しにアクセストークンを含める必要があります。
アクセストークンは、HTTP ヘッダーとして送信する必要があります。

>[!IMPORTANT]
>
>`access_token` クエリパラメーターを使用した認証のサポートは、2025 年 10 月 31 日（PT）に削除されます。 プロジェクトでクエリパラメーターを使用してアクセストークンを渡す場合は、[Authorization ヘッダー ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/authentication#using-an-access-token) を使用するように直ちに更新する必要があります。 新規開発では、`Authorization` ヘッダーのみを使用する必要があります。

### 認証ヘッダーへの切り替え


`access_token` クエリパラメーターの使用から認証ヘッダーの使用に切り替えるには、小規模なコード変更が必要です。

例えば CURL を使用する場合、このコードでは `access_token` の値をフォームパラメーター（– F フラグ）として送信します。

```bash
curl ...  -F access_token=<Access Token> <REST API Endpoint Base URL>/bulk/v1/apiCall.json
```

このコードは、`Authorization: Bearer` http ヘッダー（– H フラグ）と同じ値を送信します。

```bash
curl ... -H 'Authorization: Bearer <Access Token>' <REST API Endpoint Base URL>/bulk/v1/apiCall.json
```

## ヒントとベストプラクティス

アクセストークンの有効期限を管理することは、統合がスムーズに機能し、通常の操作中に予期しない認証エラーが発生するのを防ぐために重要です。統合の認証を設計する際は、ID 応答に含まれるトークンと有効期限を保存します。

REST 呼び出しを行う前に、トークンの残りの有効期間に基づいてトークンの有効性を確認する必要があります。トークンの有効期限が切れている場合は、[ID](https://developer.adobe.com/marketo-apis/api/identity/#tag/Identity/operation/identityUsingGET) エンドポイントを呼び出して更新します。これにより、トークンの有効期限が切れていることが原因で REST 呼び出しが失敗することがなくなります。これは、エンドユーザ向けアプリケーションにとって重要な、予測可能な方法で REST 呼び出しの待ち時間を管理するのに役立ちます。

有効期限が切れているトークンを使用して REST 呼び出しを認証すると、REST 呼び出しは失敗し、602 エラーコードが返されます。無効なトークンを使用して REST 呼び出しを認証すると、601 エラーコードが返されます。これらのコードのいずれかを受信すると、クライアントは ID エンドポイントを呼び出してトークンを更新する必要があります。

トークンの有効期限が切れる前に ID エンドポイントを呼び出すと、同じトークンと残りの有効期間が応答で返されます。

アクセストークンは、ユーザベースではなく、カスタムサービスベースで所有されます。2 つの ID 応答のスコープが同じユーザに設定されている場合でも、2 つの異なるサービスからの資格情報を使用して作成された場合、アクセストークンと有効期限は互いに独立しています。同じアプリケーションに複数の資格情報のセットがある場合は、クライアント ID が個別に管理する便利なキーになります。
