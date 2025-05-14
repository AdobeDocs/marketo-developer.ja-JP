---
title: リードトラッキング
description: Lead Tracking API
feature: Munchkin Tracking Code, Javascript
exl-id: 7ece5133-9d32-4be3-a940-4ac0310c4d8b
source-git-commit: 8ad3e3f0958ea705375651b1c8a75967d807ca80
workflow-type: ht
source-wordcount: '766'
ht-degree: 100%

---

# Lead Tracking API

Marketo の Munchkin JavaScript を使用すると、エンドユーザのページ訪問と Marketo ランディングページおよび外部 web ページへのクリックを追跡できます。これらは、Marketo に「web ページを訪問」アクティビティと「web ページのリンクのクリック」アクティビティとして記録され、スマートキャンペーンとスマートリストのトリガーおよびフィルターで使用できます。

## コードの埋め込み

Marketo インスタンスでは、コードを外部ページに埋め込むための、事前設定済みのトラッキングコードスニペットを自動的に提供し、Marketo インスタンスまでアクティビティを追跡します。埋め込みコードの使用は、この[ライセンス契約](../munchkin-license.pdf)の規定に従います。

使用可能なトラッキングコードのタイプは次の 3 つです。

1. シンプル - 同期的に読み込みます
1. 非同期 - 非同期的に読み込みます
1. 非同期 jQuery - 非同期的に読み込み、事前に jQuery を読み込む必要があります

外部ページに Munchkin を埋め込む場合は、非同期トラッキングコードを使用することを強くお勧めします。実行の成功率を最大限に高めるには、各ページの `<head>` に非同期トラッキングコードを埋め込みます。

一部のコンテンツ管理システムでは、任意のスクリプトを埋め込む際に特定の方法や制限が適用される場合があります。

参照用に、最終ページでは HTML ドキュメントの `<head>` に次のようなコードを含める必要があります。

```html
<head>
    <script type="text/javascript">
    (function() {
        var didInit = false;
        function initMunchkin() {
            if(didInit === false) {
                didInit = true;
                Munchkin.init('CHANGE-ME');
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
    ...
</head>
```

## Munchkin の動作

Marketo Munchkin のデフォルトの動作は、ページの読み込み時に次の操作を実行することです。

1. 現在のブラウザーに Munchkin cookie があるかどうかを確認し、ない場合は作成します。
1. 現在のページとブラウザーの情報を使用して、指定された Marketo インスタンスに「web ページを訪問」イベントを送信します。これにより、Marketo の対応するレコードにアクティビティが記録されます。
1. リンク上で発生したユーザクリックごとに、「web ページのリンクをクリック」イベントを送信します。

Munchkin の動作は、Munchkin [設定](configuration.md)を使用して変更できます。例えば、`cookieAnon` 設定を使用してページを訪問した際にすべてのリードに対して cookie を作成するかどうか、`clickTime` 設定を使用してクリック遅延を変更するかどうかなどです。apiOnly 設定を true に設定し、訪問アクティビティの送信を無効にすることができます。バージョン 162（2022年8月）時点では、`http/s` リンクに加えて、`tel` リンクと `mailto` リンクのクリックも追跡されます。

## 既知および匿名のリード

リードがドメイン上のページに初めて訪問すると、Marketo に新しい匿名リードレコードが作成されます。このレコードのプライマリキーは、ユーザのブラウザーで作成される Munchkin cookie（`_mkto_trk`）です。そのブラウザーでの後続のすべての web アクティビティは、この匿名レコードに対して記録されます。 Marketo の既知のレコードに関連付けるには、次のいずれかの条件を満たす必要があります。

- リードは、トラッキング対象の Marketo メールリンクからクエリ文字列に `mkt_tok` パラメーターを含む Munchkin トラッキング対象ページを訪問する必要があります。
- リードは、Marketo フォームに入力する必要があります。
- REST の[リードを関連付け](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/associateLeadUsingPOST)呼び出しを送信する必要があります。

これらの条件のいずれかが満たされると、cookie と関連するすべての web アクティビティが既知のリードに関連付けられます。

個々のブラウザーごとに新しい匿名の web アクティビティレコードが作成されるので、リードが新しいコンピューターやブラウザーを使用して初めてドメインを訪問する場合は、この関連付けを再度実行する必要があります。

## ドメイン

Munchkin はドメインごとに個々の cookie を作成して追跡するので、ドメイン間で既知のリードトラッキングを行うには、各ドメインでリード関連付けイベントが発生する必要があります。例えば、`marketo.com` と `example.com` という 2 つのドメインを管理していて、リードが `marketo.com` でフォームに入力し、その後 `example.com` に移動した場合、`marketo.com` でのアクティビティは既知のリードレコードで追跡されますが、`example.com` でのアクティビティは匿名になります。ただし、既知のリードはサブドメイン間で保持されるので、`www.example.com` の既知のリードは `info.example.com` でも既知のリードになります。

上位レベルのドメインが `.co.uk` のように 2 つの部分で構成されている場合は、コードが正しく追跡されるように、Munchkin スニペットに domainLevel パラメーターを追加します。詳しくは、[こちら](configuration.md#domainlevel)を参照してください。

## cookie

Munchkin cookie はキー `_mkto_trk` を使用し、次のパターンに従う値があります。

`id:561\-HYG\-937&token:_mch\-marketo.com\-1374552656411\-90718`

または

`id:561\-HYG\-937&token:_mch\-marketo.com\-97bf4361ef4433921a6da262e8df45a`

Munchkin cookie は、第 2 レベルドメイン（`example.com`）ごとに固有です。cookie のデフォルトの有効期間は 2 年（730 日）です。

## ベータ版

ランディングページで Munchkin ベータ版チャネルにオプトインするには、[管理／アイデアスペース](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features)メニューに移動し、「ランディングページでの Munchkin ベータ版」設定を有効にします。これにより、**[!UICONTROL 管理]**／**[!UICONTROL Munchkin]** メニューに新しいコードスニペットが提供され、外部サイトでベータ版を使用できます。

## オプトアウト

訪問者は、ブラウザーの URL に `querystring` パラメーター「marketo_opt_out=true」を追加すれば、Munchkin のトラッキングを完全にオプトアウトできます。Munchkin JavaScript は、この設定を検出すると、値が `true` の新しい cookie「mkto_opt_out」を設定しようとします。この設定が検出されると、他のすべての Marketo トラッキング cookie は削除され、新しい cookie は設定されず、Munchkin によって HTTP リクエストは行われません。
