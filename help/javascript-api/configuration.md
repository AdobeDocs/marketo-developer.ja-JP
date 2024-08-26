---
title: 設定
description: Munchkin を使用する場合は、設定 JavaScript API を使用して設定値を設定します。
feature: Javascript
exl-id: 4700ce7b-f624-4f27-871e-9a050f203973
source-git-commit: e609f9d5d58f656298412acef5e2106a19765396
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 3%

---

# 設定

Munchkin は、様々な設定を受け入れて、動作をカスタマイズできます。 設定は、[Munchkin.init （）を呼び出す際に 2 番目のパラメーターとして渡されるJavaScript オブジェクトのプロパティ ](lead-tracking.md#munchkin-behavior) す。

```json
Munchkin.init("AAA-BBB-CCC", {
        "configName":"configValue",
        "configName2":"configValue2"
    }
);
```

構成設定オブジェクトには、以下の表に示す任意の数のプロパティを含めることができます。

## プロパティ

| 名前 | データタイプ | 説明 |
|---|---|---|
| altIds | 配列 | Munchkin ID 文字列の配列を受け入れます。 有効にすると、すべての web アクティビティが、Munchkin ID に基づいてターゲットのサブスクリプションに複製されます。 |
| anonymizeIP | ブール値 | Marketoに記録された新規訪問者向けの IP アドレスを匿名化します。`{Munchkin-Id}.mktoresp.com` ドメインに `192.28.144.124` アドレスまたは `103.237.104.82` アドレスがあるかどうかを確認することで、Munchkin V2 でサブスクリプションがプロビジョニングされているかどうかを判断でき `134.213.193.62` す。アドレス `192.28.147.68` アドレス。 または、Unix シェルから次のスクリプトを実行できます。nslookup {munchkin-id}.mktoresp.com | grep -E -c -e ```（192.28.144.124,134.213.193.62,192.28.147.68,103.237.104.82）``` コマンドで「0」と出力された場合、サブスクリプションは Munchkin V2 でプロビジョニングされていません。1 以上が出力された場合、プロビジョニングされます。 |
| apiOnly | ブール値 | true に設定すると、関数は `Munchkin.Init()` を呼び出 `visitsWebPage` ません。 これは、すべての `visitsWebPage` イベントに対して完全な制御を必要とする単一ページ web アプリケーションで役立ちます。 |
| asyncOnly | ブール値 | true に設定した場合、XMLHttpRequest のを非同期で送信します。 デフォルトは false です。 |
| clickTime | 整数 | クリック追跡要求を許可するために、クリック後にブロックする時間をミリ秒単位で設定します。 これを減らすと、クリックの追跡の精度が低下します。 デフォルトは 350 ms です。 |
| cookieAnon | ブール値 | false に設定すると、新しい匿名リードのトラッキングと cookie の作成を防ぎます。 リードには cookie が含まれており、Marketo フォームに入力した後、またはMarketoのメールからクリックスルーして追跡されます。 デフォルトは true です。 |
| cookieLifeDays | 整数 | 新しく作成された Munchkin トラッキング cookie の有効期限を何日後もこの値に設定します。 デフォルトは 730 日（2 年）です。 |
| customName | 文字列 | カスタムページ名。 システムのみで使用します。 |
| domainLevel | 整数 | ページのドメインから、cookie のドメイン属性を設定する際に使用する部分の数を設定します。例えば、現在のページドメインが「www.example.com」。domainLevel:2 が cookie ドメイン属性を「.example.com」に設定する場合、domainLevel:3 が cookie ドメイン属性を「。www.example.com」に設定する場合、Background:Munchkin は特定の 2 文字のトップレベルドメインを自動的に管理します。 最上位ドメインが 3 文字の場合、通常は 2 つの部分がデフォルトで選択されます。 例えば、「www.example.com」の場合、右端の 2 つの部分を使用して Cookie を設定します。「.jp」、「.us」、「.cn」、「.uk」などの 2 つの文字の国コードの場合、コードはデフォルトで 3 つの部分に設定されます。 例えば、「www.example.co.jp」は、右端の 3 つのドメイン部分「.example.co.jp」を使用します。ドメインパターンに別の動作が必要な場合は、`domainLevel` パラメーターを使用してこれを指定する必要があります。 |
| domainSelectorV2 | ブール値 | true に設定した場合、は改善された方法を利用して、cookie ドメイン属性の設定方法を決定します。 |
| httpsOnly | ブール値 | デフォルトは false です。 true に設定した場合、トラッキングするページが https で提供された際に、cookie がセキュア設定を使用するように設定します。 |
| useBeaconAPI | ブール値 | デフォルトは false です。 true に設定すると、は、XMLHttpRequest の代わりにビーコン API を使用して非ブロックリクエストを送信します。 ブラウザーがこの API をサポートしていない場合、Munchkin は XMLHttpRequest の使用にフォールバックします。 |
| wsInfo | 文字列 | ワークスペースをターゲットにする文字列を取得します。 このワークスペース ID は、管理者/統合/Munchkin メニューのWorkspaceを選択することで取得されます。 この設定は、匿名リードレコードの初期作成にのみ適用されます。 そのリードレコードの Munchkin Cookie 値が設定されると、wsInfo パラメーターを使用してパーティションを変更できなくなります。 この設定は匿名リードにのみ影響するので、web レポートのパーティション固有の匿名訪問者にのみ関連します。 |

## 例

### 複数のサブスクリプションへのアクティビティの送信

この例では、すべての web アクティビティを、Munchkin ID が「AAA-BBB-CCC」および「XXX-YYY-ZZZ」のインスタンスに送信します。

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

### トラッキングを非同期に設定

この例では、すべての XMLHttpRequest をメインスレッドから非同期で送信します。

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
