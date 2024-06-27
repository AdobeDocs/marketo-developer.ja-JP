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

Marketoの Munchkin JavaScript を使用すると、Marketo ランディングページや外部 web ページへのエンドユーザーページの訪問およびクリックをトラッキングできます。 これらの指標は、Marketoで「Web ページに訪問」アクティビティと「Web ページ上のクリックされたリンク」アクティビティとして記録され、スマートキャンペーンやスマートリストのトリガーおよびフィルターで使用できるようになります。

## コードの埋め込み

Marketo インスタンスは、外部ページにコードを埋め込むための事前設定済みのトラッキングコードスニペットを自動的に提供します。このコードは、アクティビティを追跡してMarketo インスタンスに返します。 埋め込みコードの使用は、次の規則に従います [使用許諾契約書](../munchkin-license.pdf).

使用できるトラッキングコードタイプは 3 つあります。

1. シンプル – 同期的に読み込む
1. 非同期 – 非同期で読み込みます
1. 非同期 jQuery – 非同期で読み込みます。事前に jQuery を読み込んでおく必要があります

外部ページに Munchkin を埋め込むために、非同期トラッキングコードを使用することを強くお勧めします。 実行の成功率を可能な限り高くするには、非同期トラッキングコードをに埋め込みます。 `<head>` （各ページ）。

一部のコンテンツ管理システムでは、任意のスクリプトを埋め込む際に、特定のメソッドや制限が存在する場合があります。

参照用に、最終ページにこれと類似したコードを含める必要があります `<head>` HTMLドキュメントについて：

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

Munchkin の動作は、Munchkin を使用して変更できます [設定](lead-tracking.md#lead-tracking-api)を使用してページにアクセスした際に、すべてのリードに対して cookie が作成されるかどうかなど、 `cookieAnon` クリック遅延の設定または変更 `clickTime` の設定値。 apiOnly を true に設定すると、訪問アクティビティの送信が無効になる場合があります。 バージョン 162 （2022 年 8 月）現在、クリック数 `tel` および `mailto` 次のリンクも追跡されます `http/s` リンク。

## 既知のリードと匿名リード

ドメイン上のページにリードが初めて訪問すると、新しい匿名リードレコードがMarketoに作成されます。 このレコードのプライマリキーは Munchkin Cookie （`_mkto_trk`）が作成されます。作成されるのは、ユーザーのブラウザーです。 そのブラウザーでの後続のすべての web アクティビティは、この匿名レコードに対して記録されます。 Marketoの既知のレコードに関連付けるには、次のいずれかの操作を行う必要があります。

- リードは、次の情報を含む Munchkin でトラッキングされたページを訪問する必要があります `mkt_tok` トラッキングされるMarketo メールリンクのクエリ文字列に含まれるパラメーター。
- リードはMarketo フォームに入力する必要があります。
- SOAP [syncLead](../soap-api/leads.md) または REST [リードを関連付け](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/associateLeadUsingPOST) 通話を送信する必要があります。

これらの条件の 1 つが満たされると、Cookie と関連するすべての web アクティビティが既知のリードに関連付けられます。

個々のブラウザーごとに新しい匿名 web アクティビティレコードが作成されるので、リードが新しいコンピューターやブラウザーを使用して初めてドメインを訪問した場合、この関連付けは再度行われる必要があります。

## ドメイン

Munchkin はドメインごとに個々の cookie を作成および追跡するので、ドメインをまたいで既知のリードトラッキングが発生するには、ドメインごとにリードの関連付けイベントが発生する必要があります。 例えば、2 つのドメインを制御している場合、 `marketo.com`、および `example.com`リードがのフォームに入力します `marketo.com`に移動した後、に移動します。 `example.com` その後、次のアクティビティ `marketo.com` は既知のリードレコードでトラッキングされますが、そのアクティビティは `example.com` 匿名 既知のリードはサブドメイン間で保持されるので、既知のリードは次の点に注意してください `www.example.com` は、に対する既知のリードでもあります。 `info.example.com`.

トップレベルドメインが次のような 2 つの部分である場合 `.co.uk`を設定してから、コードが正しく追跡できるように、domainLevel パラメーターを Munchkin スニペットに追加します。 参照： [こちら](lead-tracking.md#domains) を参照してください。

## Cookie

Munchkin cookie はキーを使用します `_mkto_trk`、およびは、このパターンに従った値を持ちます。

`id:561\-HYG\-937&token:_mch\-marketo.com\-1374552656411\-90718`

Munchkin cookie は、各第 2 レベルドメインに固有です。 `example.com`. Cookie のデフォルトの有効期間は 2 年（730 日）です。

## 大文字ベータ

ランディングページの Munchkin ベータ版チャネルをオプトインするには、 [Admin -> Treasure Chest](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features) 「ランディングページの Munchkin Beta」設定を有効にします。 これにより、に新しいコードスニペットが追加されます。 **[!UICONTROL Admin]** ->  **[!UICONTROL マンチキン]** 外部サイトでベータ版を使用できるようにするメニュー。

## オプトアウト

訪問者は、 `querystring` 「marketo_opt_out=true」パラメーターをブラウザー内の URL に設定します。 Munchkin JavaScript はこの設定を検出すると、値がの新しい Cookie 「mkto_opt_out」の設定を試みます。 `true`. この設定が検出された場合、他のすべてのMarketo トラッキング cookie は削除され、新しい cookie は設定されず、Munchkin によって HTTP リクエストは行われません。
