---
title: JavaScript API
description: Marketo JavaScript APIをMunchkin リードトラッキング、Forms 2.0、Web Personalization、予測コンテンツの埋め込みコードと共に使用する方法について説明します。
feature: Munchkin Tracking Code, Forms, Web Personalization, Predictive Content, Social, Javascript
exl-id: 6129a467-be44-44bd-9e02-62009070c318
TQID: https://experienceleague.adobe.com/R9kIFBiH6jc64ay85QkumV7jCsFnj9J0t5G4IJKEsJM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 4%

---

# JavaScript API

MarketoのクライアントサイドのJavaScriptとの統合により、リードトラッキング、フォーム、web パーソナライゼーション、予測コンテンツなどの機能を利用できます。 これらの機能を使用するには、Marketo アカウントが必要です。

通常、実装には、web プロパティに埋め込みコードを追加する必要があります。 埋め込みコードによって公開されるJavaScript関数を呼び出して、機能を追加することもできます。

埋め込みコードは、アカウント IDが含まれているため、Marketo インスタンスに固有です。 Marketoのユーザーインターフェイスで、適切なパネルに移動し、埋め込みコードをクリップボードにコピーして、web ページに貼り付けます。

## リードトラッキング（Munchkin）

Marketoの[Munchkin JavaScript トラッキングコード &#x200B;](lead-tracking.md)は、web サイトへの訪問からリードを生成します。 また、個人情報を提供していない訪問者を追跡し、ユーザーのIP アドレスやその他の情報を含む匿名リードを作成します。

Marketoの管理画面にあるMunchkin ページでMunchkinを設定します。

## Forms 2.0

[Forms 2.0](forms-api-reference.md)を使用すると、マーケターはプログラミングの知識がなくてもweb フォームを作成できます。 Formsは、Marketoのランディングページだけでなく、web サイトのどのページにも埋め込むことができます。

Forms 2.0 JavaScript APIを使用して、Marketo web フォームのコア機能を拡張します。

## Web パーソナライゼーション

[Marketo Web Personalization](web-personalization.md)を使用すると、Web サイト上の見込客の身元と行動に基づいて、リアルタイムでエンゲージできます。

## 予測コンテンツ

[Marketo Predictive Content](predictive-content.md)は、機械学習と予測分析を使用して、web訪問者に関連するコンテンツを表示します。 コンテンツにテキストの説明や画像を追加したり、web サイトに複数のコンテンツレコメンデーションを埋め込んだりできます。
