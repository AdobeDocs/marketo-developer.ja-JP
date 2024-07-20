---
title: リダイレクト
description: リダイレクト
feature: Javascript
exl-id: bbf91245-42e5-47ae-a561-e522cc65ff49
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 8%

---

# リダイレクト

RTP リダイレクト API を使用すると、セグメント化されたオーディエンスをターゲット URL にリダイレクトできます。

- User Context API を使用する前に、web Personalizationのユーザーになり、サイトに [RTP タグをデプロイ ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) しておく必要があります。
- RTP では、アカウントベースのマーケティングの名前付きアカウントリストをサポートしていません。 ABM のリストとコードは、RTP で管理されるアップロード済みアカウントリスト（CSV ファイル）にのみ関連しています。

## 使用方法

`rtp('send' , 'redirect' , 'field_name' , [ 'values_array' , '...' , '...' ] , 'www.redirect_url.com' , true/false )`

| パラメーター | オプション/必須 | タイプ | 説明 |
|---------------------------|-------------------|---------|-----------------------------|
| &#39;送信&#39; | 必須 | 文字列 | メソッドのアクション。 |
| &#39;リダイレクト&#39; | 必須 | 文字列 | メソッド名。 |
| field_name | 必須 | 文字列 | 照合するフィールド名。 例：「abm.name」（後述）。 |
| values_array | 必須 | 配列 | フィールドと照合する値のリスト （大文字と小文字は区別されません）。 |
| redirect_url | 必須 | 文字列 | Target url は、条件に一致する訪問者をリダイレクトします。 |
| redirect_matched_visitors | オプション | ブール値 | true の場合、条件に一致した訪問者がリダイレクトされます。 false の場合、条件が一致しない訪問者はリダイレクトされます。 デフォルト：true |

組織、業界、ABM リスト、場所、ISP、一致したセグメント

| 条件 | データ階層 | 例 |
|-------------------------------------------------|----------------------|------------------------------------------------------------------------------------------------------------------|
| 一致したセグメント （最初のクリック後にのみ機能） | matchedSegments.name | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;matchedSegments.name&#39; , [&#39;Fortune 1,000&#39; , &#39;Enterprise&#39;] , &#39;http://www.marketo.com&#39;）; |
| 一致したセグメント （最初のクリック後にのみ機能） | matchedSegments.id | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;matchedSegments.id&#39; , [106 , 107 , 190] , &#39;http://www.marketo.com&#39;）; |
| ABM リスト | abm.name | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;abm.name&#39; , [&#39;top_key_accounts&#39;, &#39;active_customers&#39;] , &#39;http://www.marketo.com&#39;）; |
| ABM リスト | abm.code | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;abm.code&#39; , [13 , 15] , &#39;http://www.marketo.com&#39;）; |
| 組織 | 組織 | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;org&#39;, [&#39;ebay&#39;], &#39;http://www.marketo.com&#39;）; |
| ロケーション | location.country | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;location.country&#39; , [&#39;米国&#39;], &#39;http://www.marketo.com&#39;）; |
| ロケーション | location.state | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;location.state&#39;, [&#39;ca&#39;], &#39;http://www.marketo.com&#39;）; |
| ロケーション | location.city | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;location.city&#39;, [&#39;San Mateo&#39;], &#39;http://www.marketo.com&#39;）; |
| 業界 | 業種 | rtp （&#39;send&#39;, &#39;redirect&#39; , &#39;industries&#39; , [&#39;Education&#39;], &#39;http://www.marketo.com&#39;）; |
| ISP | isp | rtp （&#39;send&#39;, &#39;redirect&#39; , isp , [&#39;False&#39;], &#39;http://www.marketo.com&#39;）; |


## 注意

- リダイレクトルール/条件が Firmographics （会社、業界、場所）に基づいている場合は、rtp （&#39;send&#39;, &#39;view&#39;）および rtp （&#39;get&#39;,&#39;campaign&#39;）の前にリダイレクトコードを挿入して、待ち時間を短縮できます。
- JavaScriptを介したリダイレクトはブラウザーサイドのリダイレクトで、web サイトの読み込みと最適化に依存して最大速度に到達します。
- ベストプラクティスは、rtp タグの直後にリダイレクトコードを設定し、ヘッダーに配置することです。
- セルフリダイレクトを実行していないことを確認します（rtp には、サイクリックリダイレクトコールをブロックするセーフティネットがあります）。

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

## トラッキングされた訪問者のリダイレクト方法

1. ターゲット URL の末尾にパラメーターを追加します。例：www.marketo.com?rtp=redirect
1. 「RTP によってリダイレクトされる」というセグメントを作成します。
1. 「特定のページ」パラメーターを使用すると、以下に示すパラメーターで任意のページを表示する訪問者をターゲットに設定できます。

![tracking-redirected-vistors](assets/tracking-redirected-vistors.png)

## ターゲット URL が異なる複数の条件を定義する方法

リダイレクト呼び出しは、複数の呼び出しをサポートします。 これにより、複数のフィールドを使用してリダイレクトし、異なる URL と値で複雑な条件を作成できます。

### 使用方法

`rtp('send', 'redirect', field_name, url_values_map);`

| パラメーター | オプション/必須 | タイプ | 説明 |
|---|---|---|---|
| &#39;送信&#39; | 必須 | 文字列 | メソッドのアクション。 |
| &#39;リダイレクト&#39; | 必須 | 文字列 | メソッド名。 |
| field_name | 必須 | 文字列 | 照合するフィールド名。 例：「abm.name」（上記を参照）。 |
| url_values_map | 必須 | オブジェクト | リダイレクト URL と値リストの間でマッピングします。 例：{&#39;http://marketo.com&#39; : [&#39;first_abm&#39;, &#39;second_abm&#39;]} |


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
