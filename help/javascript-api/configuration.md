---
title: 設定
description: JavaScript API を使用してMarketo Munchkinを設定します。 altIds、anonymizeIP、asyncOnly、cookie life、domainLevel、Beacon API などのMunchkin.init 設定について説明します。
feature: Munchkin Tracking Code, Javascript
exl-id: 4700ce7b-f624-4f27-871e-9a050f203973
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 87%

---

# 設定

Munchkin は、動作をカスタマイズする様々な設定を受け入れることができます。設定は、[Munchkin.init()](api-reference.md#munchkin_init) を呼び出す際に 2 番目のパラメーターとして渡される JavaScript オブジェクトのプロパティです。

```json
Munchkin.init("AAA-BBB-CCC", {
        "configName":"configValue",
        "configName2":"configValue2"
    }
);
```

設定オブジェクトには、次の表に示す任意の数のプロパティを含めることができます。

## プロパティ

| 名前 | データタイプ | 説明 |
|---|---|---|
| altIds | 配列 | Munchkin ID 文字列の配列を受け入れます。有効にすると、Munchkin ID に基づいて、すべての web アクティビティがターゲットのサブスクリプションに複製されます。 |
| anonymizeIP | ブール値 | 新規訪問者の Marketo に記録された IP アドレスを匿名化します。 |
| apiOnly | ブール値 | true に設定すると、`Munchkin.Init()` 関数は `visitsWebPage` を呼び出しません。これは、すべての `visitsWebPage` イベントに対して完全に制御する必要がある単一ページの web アプリケーションに役立ちます。 |
| asyncOnly | ブール値 | true に設定すると、XMLHttpRequest が非同期で送信されます。デフォルトは false です。 |
| clickTime | 整数 | クリックの追跡リクエストを許可するのに、クリック後にブロックする時間を設定します（ミリ秒単位）。これを減らすと、クリックの追跡の精度が低下します。デフォルトは 350 ミリ秒です。 |
| cookieAnon | ブール値 | false に設定すると、新しい匿名リードのトラッキングと cookie の作成が防止されます。リードには cookie があり、Marketo フォームに入力した後や、Marketo メールからクリックスルーすることで追跡されます。デフォルトは true です。 |
| cookieLifeDays | 整数 | 新しく作成された Munchkin トラッキング cookie の有効期限を、この日数後に設定します。デフォルトは 730 日（2 年）です。 |
| customName | 文字列 | カスタムページ名。システムのみで使用します。 |
| <a name="domainlevel"></a>domainLevel | 整数 | ページのドメインから、cookie のドメイン属性を設定する際に使用する部分の数を設定します。例えば、現在のページドメインが「www.example.com」であるとします。domainLevel:2 は cookie ドメイン属性を「.example.com」に設定します。domainLevel:3 は cookie ドメイン属性を「。www.example.com」に設定します。Background:Munchkin は特定の 2 文字のトップレベルドメインを自動的に管理します。 通常、上位レベルドメインが 3 文字の場合、これはデフォルトで 2 つの部分になります。例えば、「www.example.com」の場合、右端の 2 つの部分「.example.com」が cookie の設定に使用されます。「.jp」、「.us」、「.cn」、「.uk」などの 2 文字の国コードの場合、コードはデフォルトで 3 つの部分になります。例えば、「www.example.co.jp」は、右端の 3 つのドメイン部分「.example.co.jp」を使用します。ドメインパターンで異なる動作が必要な場合は、`domainLevel` パラメーターを使用してこれを指定する必要があります。 |
| domainSelectorV2 | ブール値 | true に設定すると、cookie ドメイン属性を設定する方法を決定するために改善した方法が利用されます。 |
| httpsOnly | ブール値 | デフォルトは false です。true に設定すると、追跡したページが https 経由で提供された際に、セキュア設定を使用する cookie が設定されます。 |
| useBeaconAPI | ブール値 | デフォルトは false です。true に設定すると、[XMLHttpRequest](https://developer.mozilla.org/ja/docs/Web/API/XMLHttpRequest) の代わりに、[Beacon API](https://developer.mozilla.org/ja/docs/Web/API/Beacon_API) を使用して、ブロック以外のリクエストを送信します。ブラウザーがこの API をサポートしていない場合、Munchkin は XMLHttpRequest の使用にフォールバックします。 |
| wsInfo | 文字列 | ワークスペースをターゲットにする文字列を受け取ります。このワークスペース ID は、管理／統合／Munchkin メニューでワークスペースを選択することで取得されます。この設定は、匿名リードレコードの初期作成にのみ適用されます。リードレコードに対して Munchkin cookie 値が確立されると、wsInfo パラメーターを使用してこのパーティションを変更できません。この設定は、匿名リードにのみ影響するので、パーティション固有の [web レポートの匿名訪問者](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/reporting/basic-reporting/report-activity/display-people-or-anonymous-visitors-in-web-reports)にのみ関連します。 |

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

この例では、メインスレッドから非同期的に送信する、すべての XMLHttpRequest を適用します。

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
