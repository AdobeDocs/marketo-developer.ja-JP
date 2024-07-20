---
title: JAVASCRIPT API
description: Javascript API
feature: Munchkin Tracking Code, Javascript
exl-id: 6129a467-be44-44bd-9e02-62009070c318
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 2%

---

# JavaScript アプリ

Marketoのクライアントサイド JavaScript統合機能の概要を次に示します。 これらの機能を利用するには、Marketo アカウントが必要です。 通常、実装では単に web プロパティに「埋め込みコード」を追加するだけです。 埋め込みコードによって公開されるJavaScript関数を呼び出すことで、追加の機能を使用することもできます。 これらの関数については、こちらを参照してください。

はアカウント ID を含んでいるので、埋め込みコードはMarketo インスタンスに固有です。 Marketo ユーザーインターフェイス内の適切なパネルに移動して埋め込みコードを取得し、クリップボードにコピーして、web ページに貼り付けます。

## リードトラッキング （Munchkin）

Marketo [Munchkin JavaScript トラッキングコード ](lead-tracking.md) は、Marketoの機能の鍵です。 Web サイトへの訪問からリードを生成できます。 さらに、まだ個人情報を提供していない訪問者を追跡し、ユーザーの IP アドレスやその他の情報を含む匿名のリードを作成します。 Munchkin は、Marketoの管理領域にある Munchkin ページで設定します。

## Forms 2.0

[Forms 2.0](forms-api-reference.md) を使用すると、マーケターは、プログラミングの知識がなくても、美しく安定した柔軟な web フォームを作成できます。 Formsは、Marketoのランディングページにあり、web サイトの任意のページに埋め込むことができます。 Marketo web フォームのコア機能は、Forms 2.0 JavaScript API を使用して拡張できます。

## Web パーソナライズ

[Marketo Web Personalization](web-personalization.md) は、ターゲット設定とPersonalizationを実現するプラットフォームです。Web サイトを訪問する何千人もの見込み客に対し、その人物と行動に基づいてリアルタイムでエンゲージできるよう支援します。

## 予測  コンテンツ

[Marketo予測コンテンツ ](predictive-content.md) を使用すると、機械学習と予測分析を活用して、最も関連性の高いコンテンツで web 訪問者を引き付けることができます。 テキストの説明や画像を使用してコンテンツを強化し、web サイトに複数のコンテンツレコメンデーションを埋め込みます。

## ソーシャルマーケティング

[Marketo ソーシャルマーケティング ](social.md) を使用すると、マーケターは web サイトやランディングページにソーシャルウィジェットを埋め込むことができます。 ソーシャルウィジェットには、投票、ソーシャル共有ボタン、ビデオ、キャンペーン、紹介オファーなどのプロモーションが含まれます。 これらのウィジェットの表示はカスタマイズでき、独自のユーザーエクスペリエンスを作成するために取り込んだイベントもカスタマイズできます。
