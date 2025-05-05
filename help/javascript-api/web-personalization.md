---
title: Web パーソナライズ
description: Web パーソナライズ
feature: Web Personalization, Javascript
exl-id: b2c26b28-e9bf-4faf-8b6e-c102f41aeaa1
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 6%

---

# Web パーソナライズ

Web Personalization JavaScript API は、プラットフォームの Automated Personalization 機能を拡張します。 これにより、イベントの追跡や、web ページの動的なカスタマイズが可能になります。 その他の機能：[ カスタムデータイベント ](custom-data-events.md)、[ 動的コンテンツ ](web-personalization.md)、[ 訪問者データの取得 ](get-visitor-data.md)、[ 特定のボットのタグを除外 ](#exclude_tag_for_specific_bots)。

- User Context API を使用する前に、web Personalizationのユーザーになり、サイトに [RTP タグをデプロイ ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) しておく必要があります。
- RTP では、アカウントベースのマーケティングの名前付きアカウントリストをサポートしていません。 ABM のリストとコードは、RTP で管理されるアップロード済みアカウントリスト（CSV ファイル）にのみ関連しています。

## タグ設定

RTP タグは、パーソナライズされたページのヘッダーに挿入してください。

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

このメソッドは、タグレベルで自動的に呼び出され、関連するアカウント ID が設定されます。 異なるドメイン間で分割する場合は、アカウント ID を設定できます。

| パラメーター | オプション/必須 | タイプ | 説明 |
|--------------|-------------------|--------|--------------|
| &#39;setAccount&#39; | 必須 | 文字列 | メソッド名。 |
| accountId | 必須 | 文字列 | アカウント Id。 |


```javascript
var accountId = '561-HYG-937';
rtp('setAccount', accountId);
```

## イベント送信関数

このメソッドは、ページトラッキングに使用されるビューイベントを送信します。 次の例では、現在のページ URL を訪問者ページビューとして追跡します。

このメソッドでオプションの「page」パラメーターを渡すと、現在のページを上書きできます。

| パラメーター | オプション/必須 | タイプ | 説明 |
|-----------|-------------------|--------|---------------------------------|
| &#39;送信&#39; | 必須 | 文字列 | メソッドのアクション。 |
| &#39;表示&#39; | 必須 | 文字列 | メソッド名。 |
| ページ | オプション | 文字列 | 相対パスまたは完全ページの URL。 |


```javascript
// Example for Default Page
rtp('send', 'view');

// Example for Overriding Default Page
var page = 'my-page?param=1';
rtp('send', 'view', page);
```

## 特定のボットのタグを除外（ユーザーエージェント）

特定のブラウザーから Web Personalization プラットフォームにデータが送信されないようにするには（ボットが識別されている場合）、タグスクリプトに次の IF 文を追加します。

以下のコード例では、「Googlebot|msnbot」をボットの例として使用して、web Personalization アクティビティから除外します。

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

## JavaScript呼び出しの説明

Web JavaScriptと予測コンテンツを使用する際に web サイトに追加されるPersonalizationの説明。

### コア /依存JavaScript

| 名前 | 説明 | 制御 |
|---------------------------|-------------|--------------------------------------------------------|
| rtp.js | - | Marketoによって制御 |
| jquery.min.js | v1.8.3 | Marketo カスタマーサポートに連絡して無効にすることができます |
| jquery-custom-ui-min.js | v1.9.2 | Marketo カスタマーサポートに連絡して無効にすることができます |
| query-ui-1.8.17-dialog.js | v1.9.2* | Marketo カスタマーサポートに連絡して無効にすることができます |


*jQuery UI にダイアログがない場合にのみ使用されます

### オンデマンドJavaScript

| 名前 | 説明 | 制御 |
|-------------------------|-----------------------------------------------------------------------|-----------------------|
| ga-integration-2.0.1.js | Google Analytics/Facebook/SiteCatalyst統合が有効な場合に使用されます | Marketoによって制御 |
| insightera-bar-2.1.js | 予測コンテンツレコメンデーションバーが有効な場合に使用されます | Marketoによって制御 |
| froogaloop2.min.js | コンテンツ追跡が有効で、Vimeo プレーヤーがページ上に存在する場合に使用されます | - |
| iframe-api-v1.js | コンテンツトラッキングが有効になっていて、YouTube Player がページに存在する場合に使用されます | - |
