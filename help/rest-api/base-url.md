---
title: ベース URL
feature: REST API
description: Marketo REST API リクエストの作成、ベース URL パスリソースおよびパラメーターの理解、一意のベース URL の検索について説明します。
exl-id: 6c3f122c-3ace-4ed3-bed0-a6b89cedc99a
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 87%

---

# ベース URL

各 API 呼び出しの[エンドポイント参照](endpoint-reference.md)ドキュメントには、リクエストの形成にベース URL に追加する必要がある REST メソッド、パス、リソース、パラメーターが示されています。

適切に形成された REST URL の例を次に示します。

`https://284-RPR-133.mktorest.com/rest/v1/lead/318581.json?fields=email,firstName,lastName`

これは、次の部分で構成されています。

- ベース URL：`https://284-RPR-133.mktorest.com/rest`
- パス：`/v1/lead/`
- リソース：`318582.json`
- クエリパラメーター：`fields=email,firstName,lastName`

ベース URL は、アカウント ID（Munchkin ID とも呼ばれる）を含んでいるので、Marketo サブスクリプションごとに一意です。ベース URL を見つけるには、Marketo にログインし、**[!UICONTROL 管理]**／**[!UICONTROL 統合]**／**[!UICONTROL Web サービス]**&#x200B;メニューに移動します。次のスクリーンショットに示すように、「REST API」セクションの下に「エンドポイント：」というラベルが付いています。

![Web サービスのベース URL エンドポイント](assets/rest-api-base-url-web-services.png)

ベース URL を見つけたら、コピーして、いずれかの REST API を呼び出す際に使用する URL に含めます。
