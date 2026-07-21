---
title: リダイレクト
description: RTP リダイレクト APIを実装して、ABM、組織、場所、セグメントなどのフィールドを使用して、ターゲット URLにセグメント化された訪問者を送信します。例とヒントを説明します。
feature: Javascript
exl-id: bbf91245-42e5-47ae-a561-e522cc65ff49
TQID: https://experienceleague.adobe.com/frvGjN7DBJ1RJ3QFvWxo1qGiTNFmvyxi3H6FeynJHLU
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: e2290edd-b061-4880-9d79-dee306cf5aa9id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 473
ht-degree: 52%

---

# リダイレクト

RTP リダイレクト APIを使用して、セグメント化されたオーディエンスをターゲット URLに送信します。

- User Context API を使用する前に、web パーソナライゼーションの顧客になり、サイトに [RTP タグをデプロイ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)する必要があります。
- RTP は、アカウントベースマーケティングの重点顧客リストをサポートしていません。 ABM リストとコードは、RTP 内で管理されるアップロード済みアカウントリスト（CSV ファイル）にのみ関連しています。

## 使用方法

`rtp('send' , 'redirect' , 'field_name' , [ 'values_array' , '...' , '...' ] , 'www.redirect_url.com' , true/false )`

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| &#39;send&#39; | 必須 | 文字列 | メソッドアクション。 |
| &#39;redirect&#39; | 必須 | 文字列 | メソッド名。 |
| field_name | 必須 | 文字列 | 照合対象のフィールド名。 例：&#39;abm.name&#39;（以下を参照）。 |
| values_array | 必須 | 配列 | 照合対象フィールドと一致する値のリスト（大文字と小文字は区別されません）。 |
| redirect_url | 必須 | 文字列 | 条件に一致した訪問者をリダイレクトするターゲット URL。 |
| redirect_matched_visitors | オプション | ブール値 | true の場合、条件に一致した訪問者がリダイレクトされます。 false の場合、条件に一致しない訪問者がリダイレクトされます。 デフォルト：true。 |

リダイレクト条件では、組織、業界、ABM リスト、所在地、ISP、または一致するセグメントを使用できます。

| 条件 | データ階層 | 例 |
| --- | --- | --- |
| 一致したセグメント（最初のクリック後にのみ機能） | matchedSegments.name | rtp （&#39;send&#39;, &#39;redirect&#39;, &#39;matchedSegments.name&#39;, [&#39;Fortune 1,000&#39;, &#39;Enterprise&#39;], &#39;<https://www.example.com>&#39;）; |
| 一致したセグメント（最初のクリック後にのみ機能） | matchedSegments.id | rtp （&#39;send&#39;, &#39;redirect&#39;, &#39;matchedSegments.id&#39;, [106 , 107 , 190] , &#39;<https://www.example.com>&#39;）; |
| ABM リスト | abm.name | rtp （&#39;send&#39;, &#39;redirect&#39;, &#39;abm.name&#39;, [&#39;top_key_accounts&#39;, &#39;active_customers&#39;], &#39;<https://www.example.com>&#39;）; |
| ABM リスト | abm.code | rtp （&#39;send&#39;, &#39;redirect&#39;, &#39;abm.code&#39;, [13 , 15] , &#39;<https://www.example.com>&#39;）; |
| 組織 | org | rtp （&#39;send&#39;, &#39;redirect&#39;, &#39;org&#39;, [&#39;ebay&#39;], &#39;<https://www.example.com>&#39;）; |
| 場所 | location.country | rtp （&#39;send&#39;, &#39;redirect&#39;, &#39;location.country&#39;, [&#39;United States&#39;], &#39;<https://www.example.com>&#39;）; |
| 場所 | location.state | rtp （&#39;send&#39;, &#39;redirect&#39;, &#39;location.state&#39;, [&#39;ca&#39;], &#39;<https://www.example.com>&#39;）; |
| 場所 | location.city | rtp （&#39;send&#39;, &#39;redirect&#39;, &#39;location.city&#39;, [&#39;San Mateo&#39;], &#39;<https://www.example.com>&#39;）; |
| 業界 | industries | rtp （&#39;send&#39;, &#39;redirect&#39;, &#39;industries&#39;, [&#39;Education&#39;], &#39;<https://www.example.com>&#39;）; |
| ISP | isp | rtp （&#39;send&#39;, &#39;redirect&#39; , isp , [&#39;False&#39;], &#39;<https://www.example.com>&#39;）; |

## メモ

- 会社、業界、場所などの企業特性に基づくリダイレクトの遅延を減らすには、rtp （&#39;send&#39;, &#39;view&#39;）およびrtp （&#39;get&#39;, &#39;campaign&#39;）の前にリダイレクトコードを挿入します。
- ページヘッダーのrtp タグの直後にリダイレクトコードを配置します。
- Web サイトの読み込みを最適化して、ブラウザー側のJavaScript リダイレクトの速度を向上させます。
- セルフリダイレクトを避ける： rtpには、サイクリックリダイレクト呼び出しをブロックするセーフガードが含まれています。

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

1. パラメーターをターゲット URLに追加します（例：&lt;www.marketo.com?rtp=redirect>）。
1. 「RTPでリダイレクト」という名前のセグメントを作成します。
1. 「特定ページ」パラメーターを使用して、パラメーターを含むページを表示する訪問者をターゲットにします。

![リダイレクトされた訪問者のトラッキング](assets/tracking-redirected-vistors.png)

## 異なるターゲット URL で複数の条件を定義する方法

リダイレクト呼び出しは、複数の呼び出しをサポートします。 複数の呼び出しを使用してフィールドを組み合わせ、異なるURLと値を持つ条件を作成します。

### 使用方法

`rtp('send', 'redirect', field_name, url_values_map);`

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| &#39;send&#39; | 必須 | 文字列 | メソッドアクション。 |
| &#39;redirect&#39; | 必須 | 文字列 | メソッド名。 |
| field_name | 必須 | 文字列 | 照合対象のフィールド名。 例：&#39;abm.name&#39;（上記を参照）。 |
| url_values_map | 必須 | オブジェクト | リダイレクト URL と値のリスト間でマッピングします。 例：{&#39;<https://www.example.com>&#39; : [&#39;first_abm&#39;, &#39;second_abm&#39;]} |

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
