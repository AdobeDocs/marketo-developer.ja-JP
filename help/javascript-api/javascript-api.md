---
title: JavaScript API
description: JavaScript API
feature: Munchkin Tracking Code, Forms, Web Personalization, Predictive Content, Social, Javascript
exl-id: 6129a467-be44-44bd-9e02-62009070c318
source-git-commit: e63db409981d10cfea6206cf91340428e5d0b17f
workflow-type: ht
source-wordcount: '337'
ht-degree: 100%

---

# JavaScript API

次に、Marketo のクライアントサイド JavaScript 統合機能の概要を示します。これらの機能を利用するには、Marketo アカウントが必要です。通常、実装では単に web プロパティに「埋め込みコード」を追加するだけです。埋め込みコードによって公開される JavaScript 関数を呼び出すことで、追加の機能を使用することもできます。これらの関数について詳しくは、こちらを参照してください。

埋め込みコードにはアカウント識別子が含まれているので、Marketo インスタンスごとに一意です。Marketo ユーザインターフェイス内の適切なパネルに移動して埋め込みコードを取得し、クリップボードにコピーして、web ページに貼り付けます。

## リードトラッキング（Munchkin）

Marketo の [Munchkin JavaScript トラッキングコード](lead-tracking.md)は、Marketo の機能の鍵です。Web サイトへの訪問からリードを生成できます。さらに、まだ個人情報を提供していない訪問者を追跡し、ユーザの IP アドレスやその他の情報を含む匿名のリードを作成します。Munchkin の設定は、Marketo の管理領域にある Munchkin ページで行います。

## Forms 2.0

[Forms 2.0](forms-api-reference.md) を使用すると、マーケターは、プログラミングの知識がなくても、美しく安定した柔軟な web フォームを作成できます。Forms は、Marketo のランディングページにあり、web サイトの任意のページに埋め込むことができます。Marketo web フォームのコア機能は、Forms 2.0 JavaScript API を使用して拡張できます。

## Web パーソナライゼーション

[Marketo web パーソナライゼーション](web-personalization.md)は、ターゲット設定とパーソナライズ機能を実現するプラットフォームです。Web サイトを訪問する何千人もの見込み客に対し、その人物と行動に基づいてリアルタイムで引き付けることができます。

## 予測コンテンツ

[Marketo 予測コンテンツ](predictive-content.md)は、機械学習と予測分析を利用して、最も関連性の高いコンテンツで web 訪問者を引きつける機能です。テキストの説明や画像を使用してコンテンツを強化し、web サイトに複数のコンテンツレコメンデーションを埋め込みます。

## ソーシャルマーケティング

[Marketo ソーシャルマーケティング](social.md)では、マーケターは web サイトやランディングページにソーシャルウィジェットを埋め込むことができます。ソーシャルウィジェットには、投票、ソーシャル共有ボタン、ビデオ、懸賞、紹介オファーなどのプロモーションが含まれます。これらのウィジェットの表示はカスタマイズ可能であり、独自のユーザーエクスペリエンスを作成するのに取り込んだイベントもカスタマイズできます。
