---
title: リードトラッキング
description: Lead Tracking API
feature: Munchkin Tracking Code, Javascript
exl-id: 7ece5133-9d32-4be3-a940-4ac0310c4d8b
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---

# Lead Tracking API

Marketoの Munchkin JavaScriptを使用すると、Marketo ランディングページや外部 web ページへのエンドユーザーページの訪問およびクリック数をトラッキングできます。 これらの指標は、Marketoで「Web ページに訪問」アクティビティと「Web ページ上のクリックされたリンク」アクティビティとして記録され、スマートキャンペーンやスマートリストのトリガーおよびフィルターで使用できるようになります。

## コードの埋め込み

Marketo インスタンスは、外部ページにコードを埋め込むための事前設定済みのトラッキングコードスニペットを自動的に提供します。このコードは、アクティビティを追跡してMarketo インスタンスに返します。 埋め込みコードの使用は、この [ 使用許諾契約 ](../munchkin-license.pdf) の規定に従います。

使用できるトラッキングコードタイプは 3 つあります。

1. シンプル – 同期的に読み込む
1. 非同期 – 非同期で読み込みます
1. 非同期 jQuery – 非同期で読み込みます。事前に jQuery を読み込んでおく必要があります

外部ページに Munchkin を埋め込むために、非同期トラッキングコードを使用することを強くお勧めします。 実行の成功率を可能な限り高くするには、各ページの `<head>` に非同期トラッキングコードを埋め込みます。

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

## マンチキン行動

Marketo Munchkin のデフォルトの動作は、ページの読み込み時に次のとおりです。

1. 現在のブラウザーに Munchkin Cookie があるかどうかを確認し、ない場合は作成します。
1. 現在のページとブラウザーの情報を使用して、指定されたMarketo インスタンスに「Web ページに訪問」イベントを送信します。 これにより、Marketo内の対応するレコードにアクティビティが記録されます。
1. リンクで発生するユーザークリックに対して「Web ページ上のクリックされたリンク」イベントを送信します。

Munchkin の動作は、Munchkin [ 設定 ](lead-tracking.md#lead-tracking-api) を使用することで変更できます。例えば、`cookieAnon` 設定でページにアクセスしたときにすべてのリードに対して cookie を作成するか、`clickTime` 設定でクリック遅延を変更するかなどです。 apiOnly を true に設定すると、訪問アクティビティの送信が無効になる場合があります。 バージョン 162 （2022 年 8 月）の時点では、`http/s` のリンクに加えて、クリック数 `tel` と `mailto` のリンクも追跡されています。

## 既知のリードと匿名リード

ドメイン上のページにリードが初めて訪問すると、新しい匿名リードレコードがMarketoに作成されます。 このレコードのプライマリキーは、ユーザーのブラウザーで作成される Munchkin Cookie （`_mkto_trk`）です。 そのブラウザーでの後続のすべての web アクティビティは、この匿名レコードに対して記録されます。 Marketoの既知のレコードに関連付けるには、次のいずれかの操作を行う必要があります。

- リードは、トラッキング対象のMarketo メールリンクから、クエリ文字列に `mkt_tok` パラメーターを含んだ Munchkin でトラッキングされているページにアクセスする必要があります。
- リードはMarketo フォームに入力する必要があります。
- SOAP [syncLead](../soap-api/leads.md) または REST [Associate Lead](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/associateLeadUsingPOST) 呼び出しを送信する必要があります。

これらの条件の 1 つが満たされると、Cookie と関連するすべての web アクティビティが既知のリードに関連付けられます。

個々のブラウザーごとに新しい匿名 web アクティビティレコードが作成されるので、リードが新しいコンピューターやブラウザーを使用して初めてドメインを訪問した場合、この関連付けは再度行われる必要があります。

## ドメイン

Munchkin はドメインごとに個々の cookie を作成および追跡するので、ドメインをまたいで既知のリードトラッキングが発生するには、ドメインごとにリードの関連付けイベントが発生する必要があります。 例えば、`marketo.com` と `example.com` の 2 つのドメインを制御しており、あるリードが `marketo.com` でフォームに入力してから、後で `example.com` に移動した場合、`marketo.com` でのアクティビティは既知のリードレコードで追跡されますが、`example.com` でのアクティビティは匿名となります。 ただし、既知のリードはサブドメイン間で保持されるので、`www.example.com` での既知のリードは `info.example.com` での既知のリードでもあります。

`.co.uk` のようにトップレベルドメインが 2 つの部分で構成されている場合は、コードを正しく追跡するために、domainLevel パラメーターを Munchkin スニペットに追加します。 詳しくは [ こちら ](lead-tracking.md#domains) を参照してください。

## Cookie

Munchkin cookie はキー `_mkto_trk` を使用し、次のパターンに従った値を持ちます。

`id:561\-HYG\-937&token:_mch\-marketo.com\-1374552656411\-90718`

Munchkin cookie は、第 2 レベルドメイン（`example.com`）ごとに固有です。 Cookie のデフォルトの有効期間は 2 年（730 日）です。

## 大文字ベータ

ランディングページの Munchkin ベータ版チャンネルをオプトインするには、[ 管理者/宝箱 ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features) メニューに移動し、「ランディングページの Munchkin Beta」設定を有効にします。 これにより、**[!UICONTROL 管理者]** -> に新しいコードスニペットが提供されます。  外部サイトでベータ版を使用できる **[!UICONTROL Munchkin]** メニュー。

## オプトアウト

訪問者は、ブラウザーの URL に `querystring` パラメーター「marketo_opt_out=true」を追加することで、Munchkin のトラッキングを完全にオプトアウトできます。 Munchkin JavaScriptはこの設定を検出すると、値が `true` の新しい Cookie 「mkto_opt_out」の設定を試みます。 この設定が検出された場合、他のすべてのMarketo トラッキング cookie は削除され、新しい cookie は設定されず、Munchkin によって HTTP リクエストは行われません。
