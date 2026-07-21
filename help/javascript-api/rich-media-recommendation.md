---
title: リッチメディアレコメンデーション
description: Marketoの予測コンテンツ RTP タグ、template1 template2 template3のdiv、GETを使用した入力、SETを使用したリッチメディアのレコメンデーションを設定してカテゴリを設定します。
feature: Javascript
exl-id: ee92e46d-e529-40a2-a0d0-ee233916f004
TQID: https://experienceleague.adobe.com/ygm5h1FJZZW4mC318-fRR3VAcO6j1sitcAeqIUjDTbI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 814
ht-degree: 48%

---

# リッチメディアレコメンデーション

リッチメディアのレコメンデーションテンプレートを表示するには、必要なタグとAPI呼び出しをページに追加します。

1. ページヘッダーで次の操作を行います。
   1. RTP タグをインストールします。
   1. レコメンデーションを入力するGET呼び出しを追加します。
   1. テンプレートを設定するSET呼び出しを追加します。
1. ページ本文：
   1. テンプレートを表示する場所にテンプレートタグ（div クラス）を配置します。

詳しくは、[Web リッチメディアの予測コンテンツを有効にする](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/predictive-content/enabling-predictive-content/enable-predictive-content-for-web-rich-media)を参照してください。

## テンプレートタグ

| 属性 | オプション／必須 | 説明 |
| --- | --- | --- |
| クラス | 必須 | div HTML要素をRTP レコメンデーション divとして識別します。 |
| data-rtp-template-id | 必須 | レコメンデーションの整合性を決定します。 水平方向の整列には「template1」、垂直方向の整列には「template2」、タイトルと説明のみを含む垂直方向の整列には「template3」を使用します。 スクリプトは、一致するテンプレートをこの`div`に挿入します。 使用可能な値：template1、template2、template3。 |

### 例

「template1」を使用して、レコメンデーションを水平方向に表示します。

```html
<div class="RTP_RCMD2" data-rtp-template-id="template1"></div>
```

レコメンデーションを垂直方向に表示するには、「template2」を使用します。

```html
<div class="RTP_RCMD2" data-rtp-template-id="template2"></div>
```

「template3」を使用すると、タイトルと説明のみでレコメンデーションを垂直方向に表示できます。

```html
<div class="RTP_RCMD2" data-rtp-template-id="template3"></div>
```

[&#x200B; テンプレートの整列の例](#example_of_rich_media_recommendation_template_1)を参照してください。

## レコメンデーションの入力

このメソッドは、ページ上のすべてのリッチメディア `<divs>`にレコメンデーションを入力します。

### 使用方法

`rtp('get', 'rcmd', 'richmedia');`

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| &#39;get&#39; | 必須 | 文字列 | メソッドアクション。 |
| &#39;rcmd&#39; | 必須 | 文字列 | メソッド名。 |
| &#39;richmedia&#39; | 必須 | 文字列 | サブメソッド名。 |

## テンプレート設定の変更

このメソッドは、デフォルトのテンプレート設定を変更します。

rtp （&#39;get&#39;,&#39;rcmd&#39;, &#39;richmedia&#39;）を呼び出す前に、このメソッドを呼び出してください。

### 使用方法

`rtp('set', 'rcmd', 'richmedia', 'template_id', conf_obj);`

| パラメーター | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| ‘set’ | 必須 | 文字列 | メソッドアクション。 |
| &#39;rcmd&#39; | 必須 | 文字列 | メソッド名。 |
| &#39;richmedia&#39; | 必須 | 文字列 | サブメソッド名。 |
| template_id | オプション | 文字列 | 設定変更のテンプレート ID。 1 つのテンプレートのみの設定変更を指定するのに使用します。 |
| conf_obj | 必須 | オブジェクト | 新しい設定。 オブジェクトは、すべての設定をキーと値のペアとして保持します。 |

### 例

次の使用例は、テンプレートのタイトル テキストを変更します。

```javascript
rtp("set", "rcmd", "richmedia","template1",
    {
        "rcmd.title.text": "RECOMMENDED CONTENT"
    }
);
```

次の使用例は、テンプレートのカテゴリと複数の設定プロパティを設定します。

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

予測コンテンツレコメンデーションに表示されるコンテンツをフィルタリングするには、「カテゴリ」を使用します。 有効なすべてのコンテンツに予測コンテンツを使用するには、「カテゴリ」を空のままにします。

リッチメディアテンプレート内の特定のコンテンツのみをレコメンデーションするには、コンテンツの設定ページでコンテンツのカテゴリを追加します。 その後、そのカテゴリをレコメンデーションテンプレートコードに関連付けます。 たとえば、web サイトの製品セクションやソリューションセクションごとに、関連コンテンツを分類します。

次の使用例は、テンプレートに複数の設定プロパティを設定します。

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
| --- | --- | --- |
| rcmd.general.font.family | &quot;rcmd.general.font.family&quot; : &quot;arial&quot; | テンプレート内のすべてのテキストのフォントファミリーを変更します。 このプロパティは、ブラウザータイプ別のすべての CSS 値をサポートします。 ページに存在する場合は、カスタムフォントファミリーを使用できます。 |
| rcmd.content.background.color | &quot;rcmd.content.background.color&quot; : &quot;black&quot; | テンプレートの内部ボックスの背景色を変更します。 このプロパティは、ブラウザータイプ別のすべての CSS 値をサポートします。 |
| rcmd.title.text | &quot;rcmd.title.text&quot; : &quot;RECOMMENDED CONTENT&quot; | テンプレートのタイトルを変更します。 |
| rcmd.title.background.color | &quot;rcmd.title.background.color&quot; : &quot;blue&quot; | タイトルボックスの背景色を変更します。 このプロパティは、すべての css カラー値（color name、rgb など）をサポートします。 |
| rcmd.title.font.size | &quot;rcmd.title.font.size&quot; : &quot;26px&quot; | タイトルのフォントサイズを変更します。 このプロパティは、使用可能なすべてのフォントサイズの CSS 値（px、em など）をサポートします。 |
| rcmd.title.font.color | &quot;rcmd.title.font.color&quot; : &quot;white&quot; | タイトルのフォントカラーを変更します。 このプロパティは、すべてのフォントカラー値（rgb、hex など）をサポートします |
| rcmd.description.font.color | &quot;rcmd.description.font.color&quot; : &quot;white&quot; | 説明のフォントカラーを変更します。 このプロパティは、すべてのフォントカラー値（rgb、hex など）をサポートします |
| rcmd.cta.background.color | &quot;rcmd.cta.background.color&quot; : &quot;green&quot; | ボタンの背景色を変更します。 このプロパティは、すべての css カラー値（color name、rgb など）をサポートします。 |
| rcmd.cta.font.color | &quot;rcmd.cta.font.color&quot; : &quot;rgb(90, 84, 164)&quot; | ボタンのフォントカラーを変更します。 このプロパティは、すべてのフォントカラー値（rgb、hex など）をサポートします |
| rcmd.cta.text | &quot;rcmd.cta.text&quot; : &quot;Push&quot; | ボタンのテキストを変更します。 テキストは、すべてのボタンで同じです。 |
| カテゴリ | &quot;category&quot; : [&quot;one category&quot;] | このテンプレートがサポートするレコメンデーションカテゴリを変更します。 テンプレートには、この設定で指定されたカテゴリの 1 つを持つレコメンデーションのみが表示されます。 |

設定のサポートはテンプレートによって異なります。

#### 基本的な例

次の使用例は、1つのテンプレートに3つの推奨事項を表示します。 この例をHTML ページにコピーし、RTP タグをタグに置き換えます。

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

次の使用例は、1つのテンプレートに3つの推奨事項を表示します。 テンプレートタイトルは「おすすめコンテンツ」、ボタンテキストは「続きを読む」です。 この例をHTML ページにコピーし、RTP タグをタグに置き換えます。

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

#### リッチメディアレコメンデーションテンプレート #1 の例

**名前**: template1

**説明**：画像、タイトル、説明、call-to-action ボタンを含む横方向のコンテンツ。

![リッチメディアテンプレート](assets/rich-media-template1.png)

#### リッチメディアレコメンデーションテンプレート #2 の例

**名前**: template2

**説明**：画像、タイトル、説明、call-to-action ボタンを含む縦方向のコンテンツ。

![リッチメディアテンプレート](assets/rich-media-template2.png)

#### リッチメディアレコメンデーションテンプレート #3 の例

**名前**: template3

**説明**: タイトルと説明のみを含む垂直方向のコンテンツ。 マウスカーソルを合わせると、ヘッダーの色が変わり、コンテンツ URLへのリンクが表示されます。 また、説明は色を変更せずにコンテンツにリンクされます。

![リッチメディアテンプレート](assets/rich-media-template3.png)
