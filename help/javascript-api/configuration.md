---
title: 設定
description: JavaScript APIを使用してMarketo Munchkinを設定します。 altId、anonymizeIP、asyncOnly、cookie life、domainLevel、Beacon APIなどのMunchkin.initの設定を学びます。
feature: Munchkin Tracking Code, Javascript
exl-id: 4700ce7b-f624-4f27-871e-9a050f203973
TQID: https://experienceleague.adobe.com/ip2cCGgoa83v8m9GYLYXe132veYxS1C6UWX1iLB6X5Q
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45id: ea90ebee-5c84-42d9-8b21-006bdabc95a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 541
ht-degree: 43%

---

# 設定

Munchkinでは、ビヘイビアーをカスタマイズする設定を受け付けています。 設定を[Munchkin.init （） ](api-reference.md#munchkin_init)の2番目のパラメーターにJavaScript オブジェクトのプロパティとして渡します。

```json
Munchkin.init("AAA-BBB-CCC", {
        "configName":"configValue",
        "configName2":"configValue2"
    }
);
```

構成設定オブジェクトには、次の表の任意の数のプロパティを含めることができます。

## プロパティ

| 名前 | データタイプ | 説明 |
| --- | --- | --- |
| altIds | 配列 | Munchkin ID 文字列の配列を受け入れます。 これを有効にすると、すべてのweb アクティビティが、Munchkin IDで識別されたサブスクリプションに複製されます。 |
| anonymizeIP | ブール値 | 新規訪問者の Marketo に記録された IP アドレスを匿名化します。 |
| apiOnly | ブール値 | true に設定すると、`Munchkin.Init()` 関数は `visitsWebPage` を呼び出しません。 これは、すべての `visitsWebPage` イベントに対して完全に制御する必要がある単一ページの web アプリケーションに役立ちます。 |
| asyncOnly | ブール値 | trueに設定すると、XMLHttpRequestsが非同期で送信されます。 デフォルトは false です。 |
| clickTime | 整数 | クリック後にブロックする時間をミリ秒単位で設定し、クリックトラッキングリクエストを完了できるようにします。 この値を小さくすると、クリックトラッキングの精度が低下します。 デフォルトは 350 ミリ秒です。 |
| cookieAnon | ブール値 | falseに設定すると、新しい匿名リードのトラッキングとCookieの作成が防止されます。 リードはCookieを受け取り、Marketoフォームを送信するか、Marketoのメールをクリックした後に追跡されます。 デフォルトは true です。 |
| cookieLifeDays | 整数 | 新しく作成された Munchkin トラッキング cookie の有効期限を、この日数後に設定します。 デフォルトは 730 日（2 年）です。 |
| customName | 文字列 | カスタムページ名。 システムのみで使用します。 |
| <a name="domainlevel"></a>domainLevel | 整数 | Cookieのdomain属性に使用するページドメインの部分の数を設定します。<br><br>www.example.comの場合、`domainLevel: 2`はcookie ドメインを&quot;.example.com&quot;に設定し、`domainLevel: 3`は&quot;.www.example.com&quot;に設定します。<br><br> デフォルトでは、最上位ドメインに3文字がある場合、Munchkinは2つの部分を使用します。 例えば、「www.example.com」は「.example.com」を使用します。<br><br>2文字の国コード（「.jp」、「.us」、「.cn」、「.uk」など）の場合、Munchkinは3つの部分を使用します。 例えば、「www.example.co.jp」は「.example.co.jp」を使用します。<br><br> ドメインパターンで異なる動作が必要な場合は、`domainLevel` パラメーターを使用します。 |
| domainSelectorV2 | ブール値 | true に設定すると、cookie ドメイン属性を設定する方法を決定するために改善した方法が利用されます。 |
| httpsOnly | ブール値 | デフォルトは false です。 true に設定すると、追跡したページが https 経由で提供された際に、セキュア設定を使用する cookie が設定されます。 |
| useBeaconAPI | ブール値 | デフォルトは false です。 true に設定すると、[XMLHttpRequest](https://developer.mozilla.org/ja/docs/Web/API/XMLHttpRequest) の代わりに、[Beacon API](https://developer.mozilla.org/ja/docs/Web/API/Beacon_API) を使用して、ブロック以外のリクエストを送信します。 ブラウザーがBeacon APIをサポートしていない場合、MunchkinはXMLHttpRequestを使用します。 |
| wsInfo | 文字列 | ワークスペースをターゲットにします。 管理者/統合/Munchkin メニューでワークスペースを選択して、ワークスペース IDを取得します。<br><br>この設定は、匿名のリード レコードが最初に作成された場合にのみ適用されます。 そのリードレコードに対してMunchkin cookie値を設定した後、wsInfo パラメーターはそのパーティションを変更できません。<br><br>この設定は匿名リードにのみ影響するため、Web レポートのパーティション固有の[匿名訪問者](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/reporting/basic-reporting/report-activity/display-people-or-anonymous-visitors-in-web-reports)にのみ関連します。 |

## 例

### 複数のサブスクリプションへのアクティビティの送信

この例では、すべての web アクティビティを Munchkin ID「AAA-BBB-CCC」および「XXX-YYY-ZZZ」を含むインスタンスに送信します。

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      // Add configuration settings to the init method
      Munchkin.init('AAA-BBB-CCCC', { 'altIds': ['XXX-YYY-ZZZ'] });
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin.js';
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName('head')[0].appendChild(s);
})();
</script>
```

### 非同期へのトラッキングの設定

次の使用例は、すべてのXMLHttpRequestをメイン スレッドから非同期的に送信します。

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      // Add configuration settings to the init method
      Munchkin.init('AAA-BBB-CCC', { 'asyncOnly': true });
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin-beta.js';
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName('head')[0].appendChild(s);
})();
</script>
```
