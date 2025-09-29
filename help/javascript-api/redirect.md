---
title: リダイレクト
description: RTP リダイレクト API を実装して、ABM、組織、場所、セグメントなどのフィールドと、例やヒントを使用して、セグメント化された訪問者をターゲット URL に送信します。
feature: Javascript
exl-id: bbf91245-42e5-47ae-a561-e522cc65ff49
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 79%

---

# リダイレクト

RTP Redirect API を使用すると、セグメント化されたオーディエンスをターゲット URL にリダイレクトできます。

- User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。
- RTP は、アカウントベースマーケティングの重点顧客リストをサポートしていません。ABM リストとコードは、RTP 内で管理されるアップロード済みアカウントリスト（CSV ファイル）にのみ関連しています。

## 使用方法

`rtp('send' , 'redirect' , 'field_name' , [ 'values_array' , '...' , '...' ] , 'www.redirect_url.com' , true/false )`

| パラメーター | オプション／必須 | タイプ | 説明 |
|---------------------------|-------------------|---------|-----------------------------|
| &#39;send&#39; | 必須 | 文字列 | メソッドアクション。 |
| &#39;redirect&#39; | 必須 | 文字列 | メソッド名。 |
| field_name | 必須 | 文字列 | 照合対象のフィールド名。例：&#39;abm.name&#39;（以下を参照）。 |
| values_array | 必須 | 配列 | 照合対象フィールドと一致する値のリスト（大文字と小文字は区別されません）。 |
| redirect_url | 必須 | 文字列 | 条件に一致した訪問者をリダイレクトするターゲット URL。 |
| redirect_matched_visitors | オプション | ブール値 | true の場合、条件に一致した訪問者がリダイレクトされます。false の場合、条件に一致しない訪問者がリダイレクトされます。デフォルト：true。 |

組織、業界、ABM リスト、場所、ISP、一致したセグメント

| 条件 | データ階層 | 例 |
|-------------------------------------------------|----------------------|------------------------------------------------------------------------------------------------------------------|
| 一致したセグメント（最初のクリック後にのみ機能） | matchedSegments.name | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;matchedSegments.name&#39; , [&#39;Fortune 1,000&#39; , &#39;Enterprise&#39;] , &#39;<http://www.marketo.com>&#39;）; |
| 一致したセグメント（最初のクリック後にのみ機能） | matchedSegments.id | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;matchedSegments.id&#39; , [106 , 107 , 190] , &#39;<http://www.marketo.com>&#39;）; |
| ABM リスト | abm.name | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;abm.name&#39; , [&#39;top_key_accounts&#39;, &#39;active_customers&#39;] , &#39;<http://www.marketo.com>&#39;）; |
| ABM リスト | abm.code | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;abm.code&#39; , [13 , 15] , &#39;<http://www.marketo.com>&#39;）; |
| 組織 | org | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;org&#39;, [&#39;ebay&#39;], &#39;<http://www.marketo.com>&#39;）; |
| 場所 | location.country | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;location.country&#39; , [&#39;米国&#39;], &#39;<http://www.marketo.com>&#39;）; |
| 場所 | location.state | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;location.state&#39;, [&#39;ca&#39;], &#39;<http://www.marketo.com>&#39;）; |
| 場所 | location.city | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;location.city&#39;, [&#39;San Mateo&#39;], &#39;<http://www.marketo.com>&#39;）; |
| 業界 | industries | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;industries&#39; , [&#39;Education&#39;], &#39;<http://www.marketo.com>&#39;）; |
| ISP | isp | rtp （&#39;send&#39;, &#39;redirect&#39; , isp , [&#39;False&#39;], &#39;<http://www.marketo.com>&#39;）; |

## メモ

- リダイレクトルール／条件が企業特性（会社、業界、場所）に基づいている場合は、待ち時間を短縮するために、rtp(‘send’, ‘view’) および rtp(‘get’,‘campaign’) の前にリダイレクトコードを挿入できます。
- JavaScript 経由のリダイレクトは、ブラウザー側のリダイレクトで、最大速度に到達するには web サイトの読み込みと最適化に依存します。
- ベストプラクティスは、リダイレクトコードを rtp タグの直後に設定し、ヘッダーに配置することです。
- セルフリダイレクトを実行していないことを確認します（rtp には、サイクリックリダイレクト呼び出しをブロックするセーフティネットがあります）。

```html
<!DOCTYPE html>
<html lang="en-US">
<head>
<!-- RTP tag -->
<script type='text/javascript'>

// This tag needs to be replaced with your account tag
(function(c,h,a,f,i){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
c[a].a=i;var g=h.createElement("script");g.async=true;g.type="text/javascript";
g.src=f+'?rh='+c.location.hostname+'&aid='+i;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b);
})(window,document,"rtp","//xyz.marketo.com/rtp-api/v1/rtp.js","xyz");

// START REDIRECT EXAMPLE
//   - Using a helper redirect function
//   - Redirect based on named account
rtp('send','redirect','org', ['microsoft'],'http://www.marketo.com');

// Redirect based on named account list (ABM)
rtp('send','redirect','abm.name', {
    // Redirect visitors that match 'first_abm' list to www.marketo.com
    'http://www.marketo.com' : ['first_abm'],
    // Redirect visitors that match 'second_abm' list to blog.marketo.com
    'http://blog.marketo.com' : ['second_abm']
});
// END REDIRECT EXAMPLE
rtp('send','view');
rtp('get','campaign');
</script>
<!-- End of RTP tag -->
```

## 追跡された訪問者のリダイレクト方法

1. ターゲット URL の末尾にパラメーターを追加します。例：&lt;www.marketo.com?rtp=redirect>
1. 「RTP でリダイレクト」というセグメントを作成します
1. 「特定のページ」パラメーターを使用して、以下に示すパラメーターを持つページを閲覧している訪問者をターゲットにします。

![リダイレクトされた訪問者のトラッキング](assets/tracking-redirected-vistors.png)

## 異なるターゲット URL で複数の条件を定義する方法

リダイレクト呼び出しは、複数の呼び出しをサポートします。これにより、複数のフィールドでリダイレクトし、異なる URL と値を持つ複雑な条件を作成できます。

### 使用方法

`rtp('send', 'redirect', field_name, url_values_map);`

| パラメーター | オプション／必須 | タイプ | 説明 |
|---|---|---|---|
| &#39;send&#39; | 必須 | 文字列 | メソッドアクション。 |
| &#39;redirect&#39; | 必須 | 文字列 | メソッド名。 |
| field_name | 必須 | 文字列 | 照合対象のフィールド名。例：&#39;abm.name&#39;（上記を参照）。 |
| url_values_map | 必須 | オブジェクト | リダイレクト URL と値のリスト間でマッピングします。例：{&#39;<http://marketo.com>&#39; : [&#39;first_abm&#39;, &#39;second_abm&#39;]} |

#### 例

```javascript
rtp('send','redirect','abm.name', {
    // Redirect visitors that match 'first_abm' list to www.marketo.com
    'http://www.marketo.com' : ['first_abm'],
    // Redirect visitors that match 'second_abm' list to blog.marketo.com
    'http://blog.marketo.com' : ['second_abm']
});
rtp('send','redirect','org', {
    // Redirect visitors from 'Microsoft' to www.marketo.com/enterprise
    'http://www.marketo.com/enterprise' : ['microsoft']
});
```
