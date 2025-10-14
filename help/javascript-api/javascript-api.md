---
title: JavaScript API
description: Marketo JavaScript API を埋め込みコードと共に使用して、Munchkin リードトラッキング、Forms 2.0、web Personalizationおよび予測コンテンツを処理する方法について説明します。
feature: Munchkin Tracking Code, Forms, Web Personalization, Predictive Content, Social, Javascript
exl-id: 6129a467-be44-44bd-9e02-62009070c318
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 85%

---

# JavaScript API

次に、Marketo のクライアントサイド JavaScript 統合機能の概要を示します。これらの機能を利用するには、Marketo アカウントが必要です。通常、実装では単に web プロパティに「埋め込みコード」を追加するだけです。埋め込みコードによって公開される JavaScript 関数を呼び出すことで、追加の機能を使用することもできます。これらの関数について詳しくは、こちらを参照してください。

埋め込みコードにはアカウント識別子が含まれているので、Marketo インスタンスごとに一意です。Marketo ユーザインターフェイス内の適切なパネルに移動して埋め込みコードを取得し、クリップボードにコピーして、web ページに貼り付けます。

## リードトラッキング（Munchkin）

Marketo の [Munchkin JavaScript トラッキングコード](lead-tracking.md)は、Marketo の機能の鍵です。Web サイトへの訪問からリードを生成できます。さらに、まだ個人情報を提供していない訪問者を追跡し、ユーザの IP アドレスやその他の情報を含む匿名のリードを作成します。Munchkin の設定は、Marketo の管理領域にある Munchkin ページで行います。

## Forms 2.0

[Forms 2.0](forms-api-reference.md) を使用すると、マーケターは、プログラミングの知識がなくても、美しく安定した柔軟な web フォームを作成できます。Forms は、Marketo のランディングページにあり、web サイトの任意のページに埋め込むことができます。Marketo web フォームのコア機能は、Forms 2.0 JavaScript API を使用して拡張できます。

## Web パーソナライゼーション

[Marketo web パーソナライゼーション](web-personalization.md)は、ターゲティングとパーソナライズ機能を実現するプラットフォームです。Web サイトを訪問する何千人もの見込み客に対し、その人物と行動に基づいてリアルタイムで引き付けることができます。

## 予測コンテンツ

[Marketo予測コンテンツ &#x200B;](predictive-content.md) を使用すると、機械学習と予測分析を活用して、最も関連性の高いコンテンツで web 訪問者を引き付けることができます。 テキストの説明や画像を使用してコンテンツを強化し、web サイトに複数のコンテンツレコメンデーションを埋め込みます。

