---
title: JavaScript API
description: Marketo JavaScript APIをMunchkin リードトラッキング、Forms 2.0、Web Personalization、予測コンテンツの埋め込みコードと共に使用する方法について説明します。
feature: Munchkin Tracking Code, Forms, Web Personalization, Predictive Content, Social, Javascript
exl-id: 6129a467-be44-44bd-9e02-62009070c318
TQID: https://experienceleague.adobe.com/R9kIFBiH6jc64ay85QkumV7jCsFnj9J0t5G4IJKEsJM
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: e2290edd-b061-4880-9d79-dee306cf5aa9id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 00118a89f25a23b931fac671130932bb0e0e4e4e
workflow-type: tm+mt
source-wordcount: 311
ht-degree: 85%

---

# JavaScript API

次に、Marketo のクライアントサイド JavaScript 統合機能の概要を示します。 これらの機能を利用するには、Marketo アカウントが必要です。 通常、実装では単に web プロパティに「埋め込みコード」を追加するだけです。 埋め込みコードによって公開される JavaScript 関数を呼び出すことで、追加の機能を使用することもできます。 これらの関数について詳しくは、こちらを参照してください。

埋め込みコードにはアカウント識別子が含まれているので、Marketo インスタンスごとに一意です。 Marketo ユーザインターフェイス内の適切なパネルに移動して埋め込みコードを取得し、クリップボードにコピーして、web ページに貼り付けます。

## リードトラッキング（Munchkin）

Marketo の [Munchkin JavaScript トラッキングコード](lead-tracking.md)は、Marketo の機能の鍵です。 Web サイトへの訪問からリードを生成できます。 さらに、まだ個人情報を提供していない訪問者を追跡し、ユーザの IP アドレスやその他の情報を含む匿名のリードを作成します。 Munchkin の設定は、Marketo の管理領域にある Munchkin ページで行います。

## Forms 2.0

[Forms 2.0](forms-api-reference.md) を使用すると、マーケターは、プログラミングの知識がなくても、美しく安定した柔軟な web フォームを作成できます。 Forms は、Marketo のランディングページにあり、web サイトの任意のページに埋め込むことができます。 Marketo web フォームのコア機能は、Forms 2.0 JavaScript API を使用して拡張できます。

## Web パーソナライゼーション

[Marketo web パーソナライゼーション](web-personalization.md)は、ターゲティングとパーソナライズ機能を実現するプラットフォームです。Web サイトを訪問する何千人もの見込み客に対し、その人物と行動に基づいてリアルタイムで引き付けることができます。

## 予測コンテンツ

[Marketo Predictive Content](predictive-content.md)を使用すると、マシンラーニングと予測分析を利用して、web訪問者に最も関連性の高いコンテンツを提供できます。 テキストの説明や画像を使用してコンテンツを強化し、web サイトに複数のコンテンツレコメンデーションを埋め込みます。

