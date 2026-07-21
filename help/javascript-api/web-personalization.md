---
title: Web パーソナライゼーション
description: Web Personalization JavaScript APIおよびRTP タグのガイド、ページビューイベント、アカウント設定、ボットの除外、コアおよびオンデマンドのスクリプトについて説明します
feature: Web Personalization, Javascript
exl-id: b2c26b28-e9bf-4faf-8b6e-c102f41aeaa1
TQID: https://experienceleague.adobe.com/yplunKmgjOJ7gJTA2TDc9cfJXyXbrVWuM-NdVbDMN4A
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: e2290edd-b061-4880-9d79-dee306cf5aa9id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
subfeature_v2: id: cdd4e0f6-e87e-453f-88ee-2ee54a7de272
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 435
ht-degree: 54%

---

# Web パーソナライゼーション

Web Personalization JavaScript APIは、イベントを追跡し、web ページを動的にカスタマイズします。 プラットフォームの自動パーソナライゼーション機能を拡張します。

関連する機能には、[ カスタムデータイベント ](custom-data-events.md)、[動的コンテンツ ](web-personalization.md)、[訪問者データを取得](get-visitor-data.md)、および[特定のボットのタグを除外](#exclude_tag_for_specific_bots)が含まれます。

- User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。
- RTP は、アカウントベースマーケティングの重点顧客リストをサポートしていません。 ABM リストとコードは、RTP 内で管理されるアップロード済みアカウントリスト（CSV ファイル）にのみ関連しています。

## タグ設定

パーソナライズされた各ページのヘッダーにRTP タグを挿入します。

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

タグは、このメソッドを自動的に呼び出して、関連するアカウント IDを設定します。 異なるドメインに異なるアカウントを使用する場合は、アカウント IDを明示的に設定します。

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| &#39;setAccount&#39; | 必須 | 文字列 | メソッド名。 |
| accountId | 必須 | 文字列 | アカウント ID。 |

```javascript
var accountId = '561-HYG-937';
rtp('setAccount', accountId);
```

## イベント送信関数

このメソッドは、ページトラッキング用のビューイベントを送信します。 次の例の最初の呼び出しは、現在のページ URLを訪問者ページビューとして追跡します。

オプションの「page」パラメーターを渡して、2回目の呼び出しに示すように、現在のページを上書きします。

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
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

識別されたボットがWeb Personalization プラットフォームにデータを送信しないようにするには、タグスクリプトに次の`if` ステートメントを追加します。

この例では、「Googlebot|msnbot」ユーザーエージェントをWeb Personalization アクティビティから除外しています。

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

次の表は、Web Personalizationと予測コンテンツを使用するweb サイトに追加されたJavaScriptを示しています。

### コア／依存 JavaScript

| 名前 | 説明 | コントロール |
| --- | --- | --- |
| rtp.js | - | Marketo によって制御されます |
| jquery.min.js | v1.8.3 | Marketo カスタマーサポートに連絡して無効にすることができます |
| jquery-custom-ui-min.js | v1.9.2 | Marketo カスタマーサポートに連絡して無効にすることができます |
| query-ui-1.8.17-dialog.js | v1.9.2* | Marketo カスタマーサポートに連絡して無効にすることができます |

*jQuery UI ダイアログが表示されない場合にのみ使用します。

### オンデマンド JavaScript

| 名前 | 説明 | コントロール |
| --- | --- | --- |
| ga-integration-2.0.1.js | Google Analytics／Facebook／SiteCatalyst 統合が有効な場合に使用されます | Marketo によって制御されます |
| insightera-bar-2.1.js | 予測コンテンツレコメンデーションバーが有効な場合に使用されます | Marketo によって制御されます |
| froogaloop2.min.js | コンテンツトラッキングが有効で、Vimeo プレーヤーがページ上に存在する場合に使用されます | - |
| iframe-api-v1.js | コンテンツトラッキングが有効で、YouTube プレーヤーがページ上に存在する場合に使用されます | - |
