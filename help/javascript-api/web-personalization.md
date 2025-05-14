---
title: Web パーソナライゼーション
description: Web パーソナライゼーション
feature: Web Personalization, Javascript
exl-id: b2c26b28-e9bf-4faf-8b6e-c102f41aeaa1
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '401'
ht-degree: 100%

---

# Web パーソナライゼーション

Web Personalization JavaScript API は、プラットフォームの Automated Personalization 機能を拡張します。これにより、web ページのイベントトラッキングと動的なカスタマイズが可能です。その他の機能：[カスタムデータイベント](custom-data-events.md)、[動的コンテンツ](web-personalization.md)、[訪問者データを取得](get-visitor-data.md)、[特定のボットのタグを除外](#exclude_tag_for_specific_bots)。

- User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。
- RTP は、アカウントベースマーケティングの重点顧客リストをサポートしていません。ABM リストとコードは、RTP 内で管理されるアップロード済みアカウントリスト（CSV ファイル）にのみ関連しています。

## タグ設定

RTP タグは、パーソナライズされたページのヘッダーに挿入する必要があります。

```javascript
<!-- RTP tag --> 
<script type='text/javascript'>
(function(c,h,a,f,e,i){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
c[a].p=e;c[a].a=i;var g=h.createElement("script");g.async=true;g.type="text/javascript";
g.src=f;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b)})
(window,document,"rtp","[rtp-js-cdn-url]","[pod-url]","[accountId]");
</script>
<!-- End of RTP tag -->
```

## アカウント設定

このメソッドは、関連するアカウント ID を設定するタグレベルで自動的に呼び出されます。異なるドメイン間で分割する際は、アカウント ID を設定できます。

| パラメーター | オプション／必須 | タイプ | 説明 |
|--------------|-------------------|--------|--------------|
| &#39;setAccount&#39; | 必須 | 文字列 | メソッド名。 |
| accountId | 必須 | 文字列 | アカウント ID。 |


```javascript
var accountId = '561-HYG-937';
rtp('setAccount', accountId);
```

## イベント送信関数

このメソッドは、ページトラッキングに使用されるビューイベントを送信します。次の例では、現在のページ URL を訪問者ページビューとして追跡します。

このメソッドでオプションの「page」パラメーターを渡すと、現在のページを上書きできます。

| パラメーター | オプション／必須 | タイプ | 説明 |
|-----------|-------------------|--------|---------------------------------|
| &#39;send&#39; | 必須 | 文字列 | メソッドアクション。 |
| &#39;view&#39; | 必須 | 文字列 | メソッド名。 |
| ページ | オプション | 文字列 | 相対パスまたは完全なページの URL。 |


```javascript
// Example for Default Page
rtp('send', 'view');

// Example for Overriding Default Page
var page = 'my-page?param=1';
rtp('send', 'view', page);
```

## 特定のボットのタグを除外（ユーザエージェント）

Web パーソナライゼーションプラットフォームにデータを送信する特定のブラウザーを除外するには（ボットが識別された場合）、次の IF ステートメントをタグスクリプトに追加します。

以下のコード例では、Web パーソナライゼーションアクティビティから除外するボットの例として「Googlebot|msnbot」が使用されています。

```javascript
<!-- RTP tag --> 
<script type='text/javascript'>
if(navigator.userAgent.match(/.(Googlebot|msnbot)./gi) == null){
    (function(c,h,a,f,i){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
    c[a].a=i;var g=h.createElement("script");g.async=true;g.type="text/javascript";
    g.src=f+'?rh='+c.location.hostname+'&aid='+i;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b);
})(window,document,"rtp","//[cdn-pod-X-url]/rtp-api/v1/rtp.js","[accountId]");

    rtp('send','view');
    rtp('get', 'campaign', true);
}
</script>
<!-- End of RTP tag -->
```

## JavaScript 呼び出しの説明

Web パーソナライゼーションおよび予測コンテンツを使用する際に web サイトに追加される JavaScript の説明です。

### コア／依存 JavaScript

| 名前 | 説明 | コントロール |
|---------------------------|-------------|--------------------------------------------------------|
| rtp.js | - | Marketo によって制御されます |
| jquery.min.js | v1.8.3 | Marketo カスタマーサポートに連絡して無効にすることができます |
| jquery-custom-ui-min.js | v1.9.2 | Marketo カスタマーサポートに連絡して無効にすることができます |
| query-ui-1.8.17-dialog.js | v1.9.2* | Marketo カスタマーサポートに連絡して無効にすることができます |


*jQuery UI にダイアログがない場合にのみ使用されます

### オンデマンド JavaScript

| 名前 | 説明 | コントロール |
|-------------------------|-----------------------------------------------------------------------|-----------------------|
| ga-integration-2.0.1.js | Google Analytics／Facebook／SiteCatalyst 統合が有効な場合に使用されます | Marketo によって制御されます |
| insightera-bar-2.1.js | 予測コンテンツレコメンデーションバーが有効な場合に使用されます | Marketo によって制御されます |
| froogaloop2.min.js | コンテンツトラッキングが有効で、Vimeo プレーヤーがページ上に存在する場合に使用されます | - |
| iframe-api-v1.js | コンテンツトラッキングが有効で、YouTube プレーヤーがページ上に存在する場合に使用されます | - |
