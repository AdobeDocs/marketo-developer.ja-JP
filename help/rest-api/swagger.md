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

Marketo Engageの Swagger/OpenAPI 定義を使用するには、 `host` 各ドキュメントのフィールドは、Marketo Engageインスタンスの REST API ホスト名に一致するように更新する必要があります。

まず、使用する OpenAPI 定義をダウンロードします。

* [アセット](assets/swagger-asset.json)
* [リード](assets/swagger-mapi.json)
* [ID](assets/swagger-identity.json)
* [ユーザ管理](assets/swagger-user.json)

次に、Marketo管理者から REST API ホスト名を取得します。 に移動します _Admin_-> _Web サービス_ Marketo Engageのメニューで、エンドポイント フィールドからホスト名をコピーします。 この `hostname` は、プロトコルの間の文字列です。 `https://`、および `/rest`。次のようになります `AAA-999-AAA.mktorest.com`

OpenAPI ファイルをテキストエディターで開き、 `host` 「」フィールドに入力し、その値を REST API ホスト名に変更します。 `"host":"localhost:8080"` 対象： `"host":"AAA-999-AAA.mktorest.com"`.

保存したら、Swagger UI インスタンスまたはその他の OpenAPI ソフトウェアで定義ファイルを実行できます。
