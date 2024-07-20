---
title: ベース URL
feature: REST API
description: Marketoの URL を使用する方法について説明します。
exl-id: 6c3f122c-3ace-4ed3-bed0-a6b89cedc99a
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 2%

---

# ベース URL

各 API 呼び出しの [ エンドポイントリファレンス ](endpoint-reference.md) ドキュメントには、リクエストを形成するためにベース URL に追加する必要がある REST メソッド、パス、リソース、パラメーターが示されています。

次に、整形式の REST URL の例を示します。

`https://284-RPR-133.mktorest.com/rest/v1/lead/318581.json?fields=email,firstName,lastName`

これは、次の部分で構成されます。

- ベース URL: `https://284-RPR-133.mktorest.com/rest`
- パス：`/v1/lead/`
- リソース：`318582.json`
- クエリパラメーター：`fields=email,firstName,lastName`

ベース URL にはアカウント ID （Munchkin ID とも呼ばれます）が含まれているので、Marketoのサブスクリプションごとに一意になります。 ベース URL を見つけるには、Marketoにログインし、**[!UICONTROL 管理者]**/**[!UICONTROL 統合]**/**[!UICONTROL Web サービス]** メニューに移動します。 次のスクリーンショットに示すように、「REST API」セクションの下には「エンドポイント：」というラベルが付いています。

![Web サービスベース URL エンドポイント ](assets/rest-api-base-url-web-services.png)

ベース URL が見つかったら、それをコピーして、REST API のいずれかを呼び出す際に使用する URL に含めます。
