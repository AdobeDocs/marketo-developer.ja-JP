---
title: リードトラッキング
description: Marketo Munchkin JavaScriptを埋め込む方法、訪問とクリックを追跡する方法、既知のリードと匿名のリードを管理する方法、クロスドメイン Cookie、スマートキャンペーンをオプトアウトする方法について説明します。
feature: Munchkin Tracking Code, Javascript
exl-id: 7ece5133-9d32-4be3-a940-4ac0310c4d8b
TQID: https://experienceleague.adobe.com/nGUcLLgL9X7PBKf2E5IzppDj8e-SyEtxmkQaESd90mE
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
subfeature_v2:
  - id: d0251300-e25f-466f-9856-7e11ce8fa7aa
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 720
ht-degree: 14%

---

# Lead Tracking API

MarketoとMunchkin JavaScriptを使用すれば、Marketoのランディングページと外部web ページにおけるページ訪問とリンククリックを追跡できます。 Marketoは、これらのインタラクションを「Web ページにアクセス」および「Web ページ上のクリック済みリンク」アクティビティとして記録します。

スマートキャンペーンとスマートリストのトリガーとフィルターでアクティビティを使用します。

## コードの埋め込み

Marketo インスタンスには、外部ページのアクティビティをトラッキングするための事前設定済みのコードスニペットが用意されています。 埋め込みコードの使用は、この[ライセンス契約](../munchkin-license.pdf)の規定に従います。

使用可能なトラッキングコードのタイプは次の 3 つです。

1. シンプル – 同期して読み込みます。
1. 非同期：非同期で読み込みます。
1. 非同期jQuery：非同期で読み込み、最初に読み込むにはjQueryが必要です。

非同期トラッキングコードを使用して、外部ページにMunchkinを埋め込みます。 可能な限り高い実行成功率を得るには、各ページの`<head>`要素にコードを配置します。

一部のコンテンツ管理システムでは、任意のスクリプトを埋め込む際に特定の方法や制限が適用される場合があります。

最後のページでは、HTML ドキュメントの`<head>`要素に次のようなコードを含める必要があります。

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

デフォルトでは、ページが読み込まれると、Marketo Munchkinは次のアクションを実行します。

1. 現在のブラウザーにMunchkin Cookieがあるかどうかを確認し、必要に応じてCookieを作成します。
1. 現在のページとブラウザーの情報を使用して、指定されたMarketo インスタンスに「Web ページにアクセス」イベントを送信します。 このイベントは、対応するMarketo レコードにアクティビティを記録します。
1. ユーザーがリンクを選択すると、「Web ページでクリックしたリンク」イベントを送信します。

Munchkin [Configuration settings](configuration.md)を使用して、この動作を変更します。 例えば、`cookieAnon`を使用して、ページにアクセスするすべてのリードに対してMunchkinがCookieを作成するかどうかを制御するか、`clickTime`を使用してクリック遅延を変更します。

訪問アクティビティを無効にするには、`apiOnly`をtrueに設定します。 バージョン 162 （2022年8月）時点で、Munchkinは`http/s`個のリンクに加えて`tel`個と`mailto`個のリンクのクリックを追跡します。

## 既知および匿名のリード

リードが最初にドメインのページにアクセスすると、Marketoは匿名のリードレコードを作成します。 このレコードの主キーは、ユーザーのブラウザーで作成されたMunchkin Cookie （`_mkto_trk`）です。

Marketoは、そのブラウザーのその後のweb アクティビティを匿名レコードに記録します。 アクティビティを既知のMarketo レコードに関連付けるには、次のいずれかのイベントが発生する必要があります。

- リードは、トラッキング対象の Marketo メールリンクからクエリ文字列に `mkt_tok` パラメーターを含む Munchkin トラッキング対象ページを訪問する必要があります。
- リードは、Marketo フォームに入力する必要があります。
- REST の[リードを関連付け](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/associateLeadUsingPOST)呼び出しを送信する必要があります。

これらのイベントのいずれかが発生すると、MarketoはCookieとすべての関連するweb アクティビティを既知のリードに関連付けます。

Marketoは、ブラウザーごとに匿名のweb アクティビティレコードを作成します。 リードが新しいコンピューターまたはブラウザーからドメインにアクセスした場合、関連付けを再度行う必要があります。

## ドメイン

Munchkinは、ドメインごとにCookieを作成および追跡します。 ドメイン間で既知のリードを追跡するには、各ドメインでリードの関連付けイベントが発生する必要があります。

例えば、`marketo.com`と`example.com`を制御するとします。 リードは`marketo.com`にフォームを送信し、後で`example.com`に送信します。 `marketo.com`のアクティビティは既知のリードに関連付けられていますが、`example.com`のアクティビティは匿名です。

既知のリードはサブドメイン間で保持されます。 `www.example.com`の既知のリードは`info.example.com`の既知のリードでもあります。

トップレベルドメインに`.co.uk`などの2つの部分がある場合は、`domainLevel` パラメーターをMunchkin スニペットに追加します。 詳しくは、[設定](configuration.md#domainlevel)を参照してください。

## cookie

Munchkin Cookieは、キー`_mkto_trk`と、次のいずれかのパターンに従う値を使用します。

`id:561-HYG-937&token:_mch-marketo.com-1374552656411-90718`

Or

`id:561-HYG-937&token:_mch-marketo.com-97bf4361ef4433921a6da262e8df45a`

MunchkinのCookieは、`example.com`などの各セカンドレベルのドメインに固有です。 デフォルトのCookieの有効期間は2年（730日）です。

## ベータ版

ランディングページのMunchkin ベータ版チャネルにオプトインするには、[管理者/ トレジャーチェスト &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features)に移動し、「ランディングページでMunchkin Beta」設定を有効にします。

この設定により、**[!UICONTROL 管理者]** -> **[!UICONTROL Munchkin]** メニューにコードスニペットが追加されます。 これらのスニペットを使用して、外部サイトでベータ版を実行します。

## オプトアウト

訪問者は、ブラウザーのURLに`querystring` パラメーター「marketo_opt_out=true」を追加することで、Munchkin トラッキングをオプトアウトできます。 Munchkin JavaScriptがこの設定を検出すると、値`true`の新しい「mkto_opt_out」 Cookieを設定しようとします。

その後、Munchkinは他のすべてのMarketo トラッキング Cookieを削除し、新しいCookieを設定せず、HTTP リクエストも行いません。
