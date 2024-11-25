---
title: リードトラッキング
description: Lead Tracking API
feature: Munchkin Tracking Code, Javascript
exl-id: 7ece5133-9d32-4be3-a940-4ac0310c4d8b
source-git-commit: 1ad2d793832d882bb32ebf7ef1ecd4148a6ef8d5
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Lead Tracking API

MarketoのMunchkin JavaScriptを使用すると、Marketo ランディングページや外部 web ページへのエンドユーザーページの訪問およびクリックをトラッキングできます。 これらの指標は、Marketoで「Web ページに訪問」アクティビティと「Web ページ上のクリックされたリンク」アクティビティとして記録され、スマートキャンペーンやスマートリストのトリガーおよびフィルターで使用できるようになります。

## コードの埋め込み

Marketo インスタンスは、外部ページにコードを埋め込むための事前設定済みのトラッキングコードスニペットを自動的に提供します。このコードは、アクティビティを追跡してMarketo インスタンスに返します。 埋め込みコードの使用は、この [ 使用許諾契約 ](../munchkin-license.pdf) の規定に従います。

使用できるトラッキングコードタイプは 3 つあります。

1. シンプル – 同期的に読み込む
1. 非同期 – 非同期で読み込みます
1. 非同期 jQuery – 非同期で読み込みます。事前に jQuery を読み込んでおく必要があります

外部ページへのMunchkinの埋め込みには、非同期トラッキングコードを使用することを強くお勧めします。 実行の成功率を可能な限り高くするには、各ページの `<head>` に非同期トラッキングコードを埋め込みます。

一部のコンテンツ管理システムでは、任意のスクリプトを埋め込む際に、特定のメソッドや制限が存在する場合があります。

参照用に、最終ページのHTMLドキュメントの `<head>` に次のようなコードを含める必要があります。

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

## Munchkin動作

Marketo Munchkinのデフォルトの動作は、ページの読み込み時に次のとおりです。

1. 現在のブラウザーにMunchkin Cookie があるかどうかを確認し、ない場合は作成します。
1. 現在のページとブラウザーの情報を使用して、指定されたMarketo インスタンスに「Web ページに訪問」イベントを送信します。 これにより、Marketo内の対応するレコードにアクティビティが記録されます。
1. リンクで発生するユーザークリックに対して「Web ページ上のクリックされたリンク」イベントを送信します。

Munchkinの動作は、Munchkin[ 設定 ](configuration.md) を使用して変更できます。例えば、`cookieAnon` 設定を使用してページにアクセスしたすべてのリードに対して cookie が作成されるかどうか、または `clickTime` 設定を使用してクリックの遅延を変更するかどうかなどです。 apiOnly を true に設定すると、訪問アクティビティの送信が無効になる場合があります。 バージョン 162 （2022 年 8 月）の時点では、`http/s` のリンクに加えて、クリック数 `tel` と `mailto` のリンクも追跡されています。

## 既知のリードと匿名リード

ドメイン上のページにリードが初めて訪問すると、新しい匿名リードレコードがMarketoに作成されます。 このレコードのプライマリキーはMunchkin Cookie （`_mkto_trk`）で、ユーザーのブラウザー内で作成されます。 そのブラウザーでの後続のすべての web アクティビティは、この匿名レコードに対して記録されます。 Marketoの既知のレコードに関連付けるには、次のいずれかの操作を行う必要があります。

- リードは、トラッキング対象のMunchkin メールリンクから、クエリ文字列に `mkt_tok` パラメーターを含んだMarketoでトラッキングされるページにアクセスする必要があります。
- リードはMarketo フォームに入力する必要があります。
- SOAP [syncLead](../soap-api/leads.md) または REST [Associate Lead](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/associateLeadUsingPOST) 呼び出しを送信する必要があります。

これらの条件の 1 つが満たされると、Cookie と関連するすべての web アクティビティが既知のリードに関連付けられます。

個々のブラウザーごとに新しい匿名 web アクティビティレコードが作成されるので、リードが新しいコンピューターやブラウザーを使用して初めてドメインを訪問した場合、この関連付けは再度行われる必要があります。

## ドメイン

Munchkinはドメインごとに個々の cookie を作成および追跡します。このため、複数のドメインをまたいで既知のリードトラッキングが行われる場合、ドメインごとにリードの関連付けイベントが発生する必要があります。 例えば、`marketo.com` と `example.com` の 2 つのドメインを制御しており、あるリードが `marketo.com` でフォームに入力してから、後で `example.com` に移動した場合、`marketo.com` でのアクティビティは既知のリードレコードで追跡されますが、`example.com` でのアクティビティは匿名となります。 ただし、既知のリードはサブドメイン間で保持されるので、`www.example.com` での既知のリードは `info.example.com` での既知のリードでもあります。

`.co.uk` のようにトップレベルドメインが 2 つの部分で構成されている場合は、コードが正しく追跡されるように domainLevel パラメーターをMunchkin スニペットに追加します。 詳しくは [ こちら ](configuration.md#domainlevel) を参照してください。

## Cookie

Munchkin Cookie はキー `_mkto_trk` を使用し、値はこのパターンに従います。

`id:561\-HYG\-937&token:_mch\-marketo.com\-1374552656411\-90718`

または

`id:561\-HYG\-937&token:_mch\-marketo.com\-97bf4361ef4433921a6da262e8df45a`

Munchkin cookie は、第 2 レベルドメイン（`example.com`）ごとに固有です。 Cookie のデフォルトの有効期間は 2 年（730 日）です。

## ベータ版

ランディングページのMunchkin ベータ版チャネルをオプトインするには、[ 管理者/宝箱 ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features) メニューに移動し、「ランディングページのMunchkin Beta」設定を有効にします。 これにより、**[!UICONTROL 管理者]** -> に新しいコードスニペットが提供されます。  **[!UICONTROL Munchkin]** メニューを使用すると、外部サイトでベータ版を使用できます。

## オプトアウト

訪問者は、ブラウザーの URL に `querystring` パラメーター「marketo_opt_out=true」を追加することで、Munchkinのトラッキングを完全にオプトアウトできます。 Munchkin JavaScriptはこの設定を検出すると、値が `true` の新しい cookie 「mkto_opt_out」の設定を試みます。 この設定が検出された場合、他のすべてのMarketo トラッキング cookie は削除され、新しい cookie は設定されず、Munchkinによる HTTP リクエストも行われません。
