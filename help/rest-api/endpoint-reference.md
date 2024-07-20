---
title: エンドポイントの参照
feature: REST API
description: Marketo API エンドポイントのリファレンス
exl-id: 27d16b6f-865a-4e40-ab9c-cbabe2927472
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 4%

---

# エンドポイントの参照

- [ アセット ](https://developer.adobe.com/marketo-apis/api/asset/)
- [ID](https://developer.adobe.com/marketo-apis/api/identity/)
- [ リードデータベース ](https://developer.adobe.com/marketo-apis/api/mapi/)
- [ ユーザー管理 ](https://developer.adobe.com/marketo-apis/api/user/)

## エンドポイントの参照

Marketoは、Swagger を使用して、REST API のパブリックインターフェイスの正式な定義を提供します。 Swagger は、URL 構造、リクエストモデル、応答モデルの豊富な定義モデルを提供し、API インタラクション、テスト、クライアント生成で使用するツールの開発されたエコシステムを備えています。

エンドポイント参照は、[Swagger-UI](https://swagger.io/tools/swagger-ui/) JavaScript パッケージを使用して、クライアントサイドで参照ページを生成します。 各パブリックエンドポイントが一覧表示され、応答モデルの構造、必要なリクエストパラメーター、および必要に応じてリクエストモデルが提供されます。

## Marketoの Swagger 定義の使用

Swagger 標準では、ホストを指定するか、ホストをファイルを提供するホストが生成する必要があります。 Marketoは定義を含んだ空のホストパラメーターを提供するので、既存のツールを使用する前に定義でホストを修正することが重要です。 各Marketo インスタンスの REST API ホストは一意で、次のパターンに従います。

`{Munchkin ID}.mktorest.com`

## アセットAPI

Marketo Asset API では、POST方式が必要なエンドポイントのリクエストで `application/x-www-url-formencoded` スタイルパラメーターを使用します。 ただし、フォルダーパラメーターなど、場合によっては、パラメーターの値が JSON 配列またはオブジェクトになることがあります。 これらのパラメーターは、エンドポイントのリファレンスに記載されています。
