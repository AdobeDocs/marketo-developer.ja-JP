---
title: "リッチメディアのレコメンデーション"
description: "リッチメディアのレコメンデーション"
feature: Javascript
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 4%

---


# リッチメディアレコメンデーション

リッチメディアレコメンデーションテンプレートを表示するページで、次のタグと API 呼び出しを設定する必要があります。

1. ページヘッダー内
   1. RTP タグをインストールする
   1. GET呼び出しをページに追加し、レコメンデーションに入力します
   1. SET 呼び出しを追加してテンプレートを設定します
1. ページ本文内
   1. テンプレートを表示する場所にテンプレートタグ（div クラス）を配置します

詳しくは、こちらを参照してください [こちら](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/predictive-content/enabling-predictive-content/enable-predictive-content-for-web-rich-media).

## テンプレートタグ

| 属性 | オプション/必須 | 説明 |
|---|---|---|
| クラス | 必須 | この divHTML要素が RTP 推奨 div であることを指定します。 |
| data-rtp-template-id | 必須 | テンプレート ID。 これにより、レコメンデーションの整合性が決定されます。 水平方向の整列には「template1」、垂直方向の整列には「template2」、タイトルと説明のみを含む垂直方向の整列には「template3」を使用します。 スクリプトは、このに一致するテンプレートを挿入します `div.Permissible` 値：template1、template2、template3 |

### 例

レコメンデーションを水平方向に揃えて表示するには、「template1」を使用します。

```html
<div class="RTP_RCMD2" data-rtp-template-id="template1"></div>
```

レコメンデーションを垂直方向に揃えて表示するには、「template2」を使用します。

```html
<div class="RTP_RCMD2" data-rtp-template-id="template2"></div>
```

レコメンデーションをタイトルと説明のみで垂直方向に揃えて表示するには、「template3」を使用します。

```html
<div class="RTP_RCMD2" data-rtp-template-id="template3"></div>
```

テンプレート配置のスクリーンショットを参照 [こちら](#example_of_rich_media_recommendation_template_1).

## レコメンデーションの入力

このメソッドは、すべてのリッチメディアに入力されます `<divs>` お勧めのページで。

### 使用方法

`rtp('get', 'rcmd', 'richmedia');`

| パラメーター | オプション/必須 | タイプ | 説明 |
|---|---|---|---|
| &#39;get&#39; | 必須 | 文字列 | メソッドのアクション。 |
| &#39;rcmd&#39; | 必須 | 文字列 | メソッド名。 |
| 『リッチメディア 』 | 必須 | 文字列 | サブメソッド名。 |


## テンプレート設定の変更

この方法では、テンプレートのデフォルト設定が変更されます。

注意：このメソッドを使用する場合は、rtp （&#39;get&#39;,&#39;rcmd&#39;, &#39;richmedia&#39;）を呼び出す前に呼び出す必要があります。

### 使用方法

`rtp('set', 'rcmd', 'richmedia', 'template_id', conf_obj);`

| パラメーター | オプション/必須 | タイプ | 説明 |
|---|---|---|---|
| &#39;設定&#39; | 必須 | 文字列 | メソッドのアクション。 |
| &#39;rcmd&#39; | 必須 | 文字列 | メソッド名。 |
| 『リッチメディア 』 | 必須 | 文字列 | サブメソッド名。 |
| template_id | オプション | 文字列 | 設定変更のテンプレート ID。 を使用して、1 つのテンプレートのみの設定変更を指定します。 |
| conf_obj | 必須 | オブジェクト | 新しい設定。 オブジェクトは、すべての設定をキーと値のペアとして保持します。 |


### 例

このコードスニペットはテンプレートのタイトルテキストを変更します。

```javascript
rtp("set", "rcmd", "richmedia","template1",
    {
        "rcmd.title.text": "RECOMMENDED CONTENT"
    }
);
```

このコードスニペットは、1 つのテンプレートに対して複数の設定を持つ設定カテゴリを示しています。

```javascript
rtp("set", "rcmd", "richmedia",
    {
        "template1": 
        {
            "rcmd.title.text": "RECOMMENDED CONTENT",
            "rcmd.general.font.family": "arial",
            "category":
            [
                "webinar",
                "blog posts",
                "pricing_page_category",
                "product_a_category"
            ]
        }
    }
);
```

メモ：予測コンテンツレコメンデーションの結果に表示されるコンテンツをフィルタリングするには、「カテゴリ」を使用します。 有効なすべてのコンテンツ部分に予測コンテンツを適用するには、「カテゴリ」を空のままにします。 リッチメディアテンプレートの出力に特定のコンテンツのみをレコメンデーションする場合は、コンテンツを設定ページでコンテンツのカテゴリを追加し、そのカテゴリをレコメンデーションテンプレートコード内で関連付けます。 Web サイトのセクション（製品またはソリューション）に従って関連コンテンツを分類します。

このコードスニペットは、1 つのテンプレートに対して複数のテンプレート設定を指定する様子を示しています。

```javascript
rtp("set", "rcmd", "richmedia",
    {
        "template1":
        {
            "rcmd.title.text": "RECOMMENDED CONTENT",
            "rcmd.general.font.family": "arial"
        }
    }
);
```

#### 設定プロパティ

| 設定 | 例 | 説明 |
|---|---|---|
| rcmd.general.font.family | &quot;rcmd.general.font.family&quot; : &quot;arial&quot; | テンプレート内のすべてのテキストのフォントファミリーを変更します。 このプロパティは、ブラウザータイプ別のすべての CSS 値をサポートします。 ページに存在する場合は、カスタムフォントファミリーを使用できます。 |
| rcmd.content.background.color | &quot;rcmd.content.background.color&quot; : &quot;black&quot; | テンプレートの内部ボックスの背景色を変更します。 このプロパティは、ブラウザータイプ別のすべての CSS 値をサポートします。 |
| rcmd.title.text | &quot;rcmd.title.text&quot; :&quot;推奨コンテンツ&quot; | テンプレートのタイトルを変更します。 |
| rcmd.title.background.color | &quot;rcmd.title.background.color&quot; : &quot;blue&quot; | タイトルボックスの背景色を変更します。 このプロパティは、すべての css カラー値（カラー名、rgb など）をサポートします。 |
| rcmd.title.font.size | &quot;rcmd.title.font.size&quot; : &quot;26px&quot; | タイトルのフォントサイズを変更します。 このプロパティは、使用可能なすべてのフォントサイズの CSS 値（px、em など）をサポートします。 |
| rcmd.title.font.color | &quot;rcmd.title.font.color&quot; : &quot;white&quot; | タイトルのフォントカラーを変更します。 このプロパティは、すべてのフォントカラー値（rgb、16 進数など）をサポートします |
| rcmd.description.font.color | &quot;rcmd.description.font.color&quot; : &quot;white&quot; | 説明のフォントカラーを変更します。 このプロパティは、すべてのフォントカラー値（rgb、16 進数など）をサポートします |
| rcmd.cta.background.color | &quot;rcmd.cta.background.color&quot; : &quot;green&quot; | ボタンの背景色を変更します。 このプロパティは、すべての css カラー値（カラー名、rgb など）をサポートします。 |
| rcmd.cta.font.color | &quot;rcmd.cta.font.color&quot; : &quot;rgb （90, 84, 164）&quot; | ボタンのフォントカラーを変更します。 このプロパティは、すべてのフォントカラー値（rgb、16 進数など）をサポートします |
| rcmd.cta.text | &quot;rcmd.cta.text&quot; :&quot;プッシュ&quot; | ボタンのテキストを変更します。 テキストは、すべてのボタンで同じです。 |
| カテゴリー | &quot;category&quot; : [「1 つのカテゴリ」] | このテンプレートがサポートする推奨カテゴリを変更します。 テンプレートには、この設定で設定されたカテゴリの 1 つを持つレコメンデーションのみが表示されます。 |


メモ：設定のサポートはテンプレートごとに変わることがあります。

#### 基本的な例

この例には、3 つのレコメンデーションを含む 1 つのテンプレートがあります。 この例をHTMLページにコピーしてから、RTP タグを自分のタグに置き換えます。

```html
<!DOCTYPE>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>RTP recommendation</title>
<!-- RTP tag --> 
<script type='text/javascript'>

// This tag needs to be replaced with your account tag
(function(c,h,a,f,i,e){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
c[a].a=i;c[a].e=e;var g=h.createElement("script");g.async=true;g.type="text/javascript";
g.src=f+'?aid='+i;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b);
})(window,document,"rtp","//example.rtp.com/rtp-api/v1/rtp.js","account_id");

// Send page view (required by  the recommendation)
rtp('send','view');
// Populate recommendation
rtp('get','rcmd', 'richmedia');
</script>
<!-- End of RTP tag -->
</head>
<body>
<div class="RTP_RCMD2" data-rtp-template-id="template1"></div>
</body>
</html>
```

#### 高度な例

この例には、3 つのレコメンデーションを含む 1 つのテンプレートがあります。 テンプレートのタイトルは「RECOMMENDED CONTENT」、ボタンのテキストは「Read More」になります。 この例をHTMLページにコピーしてから、RTP タグを自分のタグに置き換えます。

```html
<!DOCTYPE>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>RTP recommendation</title>
<!-- RTP tag --> 
<script type='text/javascript'>

// This tag needs to be replaced with your account tag
(function(c,h,a,f,i,e){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
c[a].a=i;c[a].e=e;var g=h.createElement("script");g.async=true;g.type="text/javascript";
g.src=f+'?aid='+i;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b);
})(window,document,"rtp","//example.rtp.com/rtp-api/v1/rtp.js","account_id");

// Send page view (required by  the recommendation)
rtp('send','view');
// Populate the recommendation zone
rtp('get', 'campaign',true);
// Change template configuration
rtp('set', 'rcmd', 'richmedia',
    {
        template1 :
        {
            "rcmd.title.text" : "RECOMMENDED CONTENT",
            "rcmd.cta.text" : "Read More"
        }
    }
);
// Populate recommendation
rtp('get','rcmd', 'richmedia');
</script>
<!-- End of RTP tag -->
</head>
<body>
<div class="RTP_RCMD2" data-rtp-template-id="template1"></div>
</body>
</html>
```

#### リッチメディアレコメンデーションテンプレート#1 の例

**名前**: template1 **説明**：画像、タイトル、説明、誘い文句（CTA：コールトゥアクション）ボタンなどの横長コンテンツ。

![リッチメディアテンプレート](assets/rich-media-template1.png)

#### リッチメディアレコメンデーションテンプレート#2 の例

**名前**:template2 **説明**：画像、タイトル、説明、誘い文句（CTA：コールトゥアクション）ボタンなどの垂直方向のコンテンツ。

![リッチメディアテンプレート](assets/rich-media-template2.png)

#### リッチメディアレコメンデーションテンプレート#3 の例

**名前**:template3 **説明**：タイトルと説明のみを含む垂直コンテンツ。 マウスポインターを置くと、ヘッダーの色が変更され、コンテンツ URL にハイパーリンクされます。 説明は、色を変更せずにコンテンツにリンクすることもできます。 ![リッチメディアテンプレート](assets/rich-media-template3.png)
