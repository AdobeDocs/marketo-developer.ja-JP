---
title: Swagger 定義のダウンロード
feature: REST API, Programs
description: ローカルで使用するための Swagger 定義ファイルをダウンロードします。
exl-id: c2bed094-36f9-47e7-a6d5-c237e425966a
source-git-commit: fb95ac67e7fbabe772341d78af7c5cbf3721f66d
workflow-type: ht
source-wordcount: '170'
ht-degree: 100%

---

# Swagger 定義のダウンロード

[Swagger](https://swagger.io/) または [OpenAPI](https://www.openapis.org/) 定義は、REST API のすべてのメソッドとパラメーターを説明するデータファイルです。これらのデータファイルをローカルにダウンロードして、個人用 API 参照として使用できます。

Marketo Engage Swagger／OpenAPI 定義を使用するには、各ドキュメントの `host` フィールドを、Marketo Engage インスタンスの REST API ホスト名と一致するように更新する必要があります。

最初に、使用する OpenAPI 定義をダウンロードします。

* [アセット](assets/swagger-asset.json)
* [リード](assets/swagger-mapi.json)
* [ID](assets/swagger-identity.json)
* [ユーザ管理](assets/swagger-user.json)

次に、Marketo Admin から REST API ホスト名を取得します。Marketo Engage の&#x200B;_管理_／_Web サービス_&#x200B;メニューに移動し、「エンドポイント」フィールドからホスト名をコピーします。`hostname` は、プロトコル `https://` と `/rest` の間の文字列で、`AAA-999-AAA.mktorest.com` のようになります

テキストエディターで OpenAPI ファイルを開き、JSON の `host` フィールドを見つけて、その値（`"host":"localhost:8080"`）を REST API ホスト名（`"host":"AAA-999-AAA.mktorest.com"`）に変更します。

保存したら、Swagger UI インスタンスまたはその他の OpenAPI ソフトウェアで定義ファイルを実行できます。
