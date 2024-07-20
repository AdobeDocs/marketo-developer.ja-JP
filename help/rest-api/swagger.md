---
title: Swagger 定義のダウンロード
feature: REST API, Programs
description: ローカルで使用するための Swagger 定義ファイルをダウンロードします。
source-git-commit: 85062243d57a3fc6d15251163e926495858edf2a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 2%

---

# Swagger 定義のダウンロード

[Swagger](https://swagger.io/) または [OpenAPI](https://www.openapis.org/) 定義は、REST API のすべてのメソッドとパラメーターを記述したデータファイルです。 これらのデータファイルをダウンロードし、個人用 API リファレンスとしてローカルに使用できます。

Marketo Engageの Swagger/OpenAPI 定義を使用するには、各ドキュメントの `host` フィールドを更新して、Marketo Engageインスタンスの REST API ホスト名と一致させる必要があります。

まず、使用する OpenAPI 定義をダウンロードします。

* [アセット](assets/swagger-asset.json)
* [リード](assets/swagger-mapi.json)
* [ID](assets/swagger-identity.json)
* [ユーザ管理](assets/swagger-user.json)

次に、Marketo管理者から REST API ホスト名を取得します。 エンドポイントで _管理者_/_web サービス_ メニューに移動し、Marketo Engage フィールドからホスト名をコピーします。 `hostname` は、プロトコル、`https://`、`/rest` の間の文字列で、`AAA-999-AAA.mktorest.com` のようになります

OpenAPI ファイルをテキストエディターで開き、JSON 内の `host` フィールドを見つけて、その値を REST API ホスト名に変更します：`"host":"localhost:8080"` を `"host":"AAA-999-AAA.mktorest.com"` に変更します。

保存したら、Swagger UI インスタンスまたはその他の OpenAPI ソフトウェアで定義ファイルを実行できます。
