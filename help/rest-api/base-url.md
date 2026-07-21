---
title: ベース URL
feature: REST API
description: Marketo REST API リクエストを作成する方法、ベース URL パスのリソースとパラメーターについて理解する方法、一意のベース URLを見つける方法について説明します。
exl-id: 6c3f122c-3ace-4ed3-bed0-a6b89cedc99a
TQID: https://experienceleague.adobe.com/NZisV6V-FMPi0RHpdaFrc1kZc3nb15YomwRgohaQmEE
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 146
ht-degree: 14%

---

# ベース URL

[&#x200B; エンドポイント参照](endpoint-reference.md)の各API呼び出しは、REST メソッド、パス、リソース、およびパラメーターを指定します。 これらのコンポーネントをベース URLに追加して、リクエストを形成します。

適切に形成された REST URL の例を次に示します。

`https://284-RPR-133.mktorest.com/rest/v1/lead/318581.json?fields=email,firstName,lastName`

この例には、次のコンポーネントが含まれています。

- **ベース URL:** `https://284-RPR-133.mktorest.com/rest`
- **パス：** `/v1/lead/`
- **リソース：** `318582.json`
- **クエリパラメーター：** `fields=email,firstName,lastName`

ベース URLには、Marketo IDとも呼ばれるアカウント IDが含まれており、各Munchkin サブスクリプションに固有です。

ベース URLを見つけるには、Marketoにログインし、**[!UICONTROL Admin]** > **[!UICONTROL Integration]** > **[!UICONTROL Web Services]**&#x200B;に移動します。 ベース URLは、次の画像に示すように、「REST API」セクションで「Endpoint:」というラベルが付けられます。

![Web サービスのベース URL エンドポイント](assets/rest-api-base-url-web-services.png)

ベース URLをコピーし、REST API呼び出しごとにURLに含めます。
