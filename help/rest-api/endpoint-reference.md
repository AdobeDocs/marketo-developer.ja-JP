---
title: 「エンドポイントリファレンス」
feature: REST API
description: 「Marketo API エンドポイントのリファレンス」
source-git-commit: 2454f126dc4275697ef6773420453ad8853eae73
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---


# エンドポイントの参照

- [アセット](https://developer.adobe.com/marketo-apis/api/asset/)
- [ID](https://developer.adobe.com/marketo-apis/api/identity/)
- [リードデータベース](https://developer.adobe.com/marketo-apis/api/mapi/)
- [ユーザー管理](https://developer.adobe.com/marketo-apis/api/user/)

## エンドポイントの参照

Marketoは、Swagger を使用して、REST API のパブリックインターフェイスの正式な定義を提供します。 Swagger は、URL 構造、リクエストモデル、応答モデルの豊富な定義モデルを提供し、API インタラクション、テスト、クライアント生成で使用するツールの開発されたエコシステムを備えています。

エンドポイント参照では、を使用します [Swagger-UI](https://swagger.io/tools/swagger-ui/) クライアントサイドで参照ページを生成する JavaScript パッケージ。 各パブリックエンドポイントが一覧表示され、応答モデルの構造、必要なリクエストパラメーター、および必要に応じてリクエストモデルが提供されます。

## Marketoの Swagger 定義の使用

Swagger 標準では、ホストを指定するか、ホストをファイルを提供するホストが生成する必要があります。 Marketoは定義を含んだ空のホストパラメーターを提供するので、既存のツールを使用する前に定義でホストを修正することが重要です。 各Marketo インスタンスの REST API ホストは一意で、次のパターンに従います。

`{Munchkin ID}.mktorest.com`

## アセットAPI

Marketo Asset API では、 `application/x-www-url-formencoded` POSTメソッドを必要とするエンドポイントのリクエストのスタイルパラメーター。 ただし、フォルダーパラメーターなど、場合によっては、パラメーターの値が JSON 配列またはオブジェクトになることがあります。 これらのパラメーターは、エンドポイントのリファレンスに記載されています。
