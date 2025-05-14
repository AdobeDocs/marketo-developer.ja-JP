---
title: ソーシャル
description: ソーシャル
feature: Social, Javascript
exl-id: 82d2b86f-5efe-4434-b617-d27f76515a79
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '776'
ht-degree: 100%

---

# ソーシャル

[Marketo ソーシャルマーケティング](https://business.adobe.com/products/marketo/social-marketing.html)では、マーケターは web サイトやランディングページにソーシャルウィジェットを埋め込むことができます。ソーシャルウィジェットには、投票、ソーシャル共有ボタン、ビデオ、懸賞、紹介オファーなどのプロモーションが含まれます。

## 埋め込み共有ウィジェットのサンプル

```html
<!-- Marketo Widget Loader Script --> 

<script type="text/javascript" src="//b2c-mlm.marketo.com/jsloader/271d8232-1500-4305-b7ed-05d451b9ee0c/loader.php.js">
</script>

 <!-- The Location of the Social Widget --> 

<divclass='cf_widgetloader cf_w_245d8f3c0955454cbd26abc39d0d874c'="" options="{&quot;outerHeight&quot;:400, &quot;outerWidth&quot;:600}">
</divclass='cf_widgetloader'>
```

![social-share-widget](assets/social-share-widget.png)

ソーシャルウィジェットのカスタマイズには、2 つの基本的な方法があります。

1. 製品の通常の UI を使用し、イベントリスナーを添付して、UI で特定のアクションが発生した際に通知を受け取り、追加のビジネスロジックを実行する。
1. 製品の通常の UI をカスタム UI に置き換え、必要に応じて UI のポップアップ「ステージ」をアクティブ化する。

## 通常の UI へのイベントの添付

CF JavaScript ライブラリ内のイベントをサブスクライブする方法は、グローバルにサブスクライブする方法と、単一のウィジェットに対してサブスクライブする方法の 2 つがあります。イベントは、以下のイベントテーブルに記載されています。

### グローバルイベントサブスクリプション

```html
<script>
cf_scripts.afterload(function(){
    CF.events.listen("event_name_here",
        function(event, arg1){
            //Your code to do something on the event goes here.
            //It will be fired whenever ANY widget fires the event "event_name_here".
        }
    );
});
</script>
```

### ウィジェットごとのイベントサブスクリプション

```html
<script>
cf_scripts.afterload(function(){
    CF.widget.listen("widget_name_here", "event_name_here",
        function(event, arg1){
            //Your code to do something on the event goes here.
            //It will be fired whenever the widget named "widget_name_here" fires the event "event_name_here".
        }
    );
});
</script>
```

## 例

この例では、ユーザが「referral_SignUp」というウィジェットのオファー登録を完了した後、以前は非表示だった ID「signedUp」の要素が表示されています。

```html
<div id='signedUp'style='display:none; color:green;'>This is a custom message to let you know that you signed up!</div>
<div class='cf_widgetLoader cf_w_referral_SignUp'></div>

<script>
    cf_scripts.afterload(function(){
        CF.widget.listen("referral_SignUp", "offer_enrolled", function(){
        cf_jq("#signedUp").show();
    });
});
</script>
```

## 基本イベントテーブル

| イベント名 | 説明 | このイベントを使用するウィジェット | サポートされる引数（イベントコールバック関数に渡される） |
| --- | --- | --- | --- | 
| share_sent | 共有リクエストが処理にサーバーに送信されるたびに発生します。 | 共有する機能を持つすべてのウィジェット。 | 1.&quot;share_sent&quot;（文字列）<br>2.送信されたパラメーター（オブジェクト） |
| share_success | 共有リクエストが正常に処理された際に発生します。 | 共有する機能を持つすべてのウィジェット。 | 1.&quot;share_success&quot;（文字列）<br>2.送信されたメッセージと短縮 URL を含む共有応答オブジェクト（オブジェクト） |
| vote_success | ユーザが調査に正常に投票した際に発生します。 | 調査と投票ウィジェット | 1.&quot;vote_success&quot;（文字列）<br>2.タイトル、説明、エンティティ識別子など、投票された項目（オブジェクト） |
| offer_enrolled | ユーザがオファーに正常に登録した際に発生します。 | すべてのオファーウィジェット。 | 1.&quot;offer_enrolled&quot;（文字列）<br>2.変更されたユーザプロパティ（オブジェクト）、<br>3.変更されたユーザ属性（オブジェクト） |
| profile_saved | ユーザがプロファイル取得からプロファイルを更新した際に発生します。 | プロファイル取得が有効になっているすべてのオファー以外のウィジェット | 1.&quot;profile_saved&quot;（文字列）<br>2.変更されたユーザプロパティ（オブジェクト）<br>3.変更されたユーザ属性（オブジェクト） |
| video_loaded | 埋め込みビデオが完全に読み込まれ、初期化された際に発生します。 | VideoShare ウィジェット | 1.&quot;video_loaded&quot;（文字列）2.“.cf_videoshare_wrap” ビデオを保持する要素（jQuery オブジェクト） |

## UI のカスタム UI への置き換え

UI をカスタム UI に置き換えるには、まず通常の UI をオフにする必要があります。これを行うには、オプション _popupUIOnly_ を _true_ に設定します。このオプションを設定すると、ページの読み込み時に標準 UI はレンダリングされず、代わりにウィジェットがデータを取得し、_CF.widget.activate_ 関数を呼び出して、実行するオプションを指定して、ポップアップステージの 1 つを開始するまで待機します。

_referral_SignUp_ という名前のリファラルオファーウィジェットのリファラルオファー新規登録フローを起動するカスタムボタンの作成例を以下に示します。

```html
<button id="myNewSignUpButton">My newSign Up button</button>

<!-- Turn off the defaultreferral offer UI by setting popupUIOnly to true-->
<div class="cf_widgetLoader cf_w_referral_SignUp" options="{popupUIOnly:true}"></div>

<script>
cf_scripts.afterload(function($, CF){
    // After the cf script library has loaded, find the button with
    // id="myNewSignUpButton", and attach a click listener to it.
    $("#myNewSignUpButton").click(function(){
        // When it is clicked, activate the popup widget flow for the referral,
        // asking it to point to the clicked button.
        CF.widget.activate("referral_SignUp", {pointTo:$(this)});
    });
});
</script>
```

クリックハンドラーの追加は一般的なので、追加するショートカットメソッドがあります。次の例は、機能的には前の例と同じです。

```html
<button id="myNewSignUpButton">My newSign Up button</button>
<div class="cf_widgetLoader cf_w_referral_SignUp" options="{popupUIOnly:true}"></div>

<script>
cf_scripts.afterload(function($, CF){
    // Use the addClickActivate convenience method, which will
    // automatically make the popup point at the clicked item with id myNewSignUpButton.
    CF.widget.addClickActivate("#myNewSignUpButton", "referral_SignUp", {});
});
</script>
```

## 置換 UI に組み込むウィジェット UI データの取得

置換 UI を描画するのにウィジェットに関するデータが必要な場合は、特別なイベント _ui_data_ からデータを取得できます。通常の `CF.widget.listen` 関数を使用してこのイベントをリッスンできますが、これを行うと、ウィジェットが the_ui_data_ イベントを既に発生させた後にイベントリスナーが追加され、データが受信されないという潜在的な競合状態が発生する場合があります。この競合を回避するには、`popupUIOnly` オプションで UI を無効にしている場合でも、ウィジェットの標準 UI の再描画を引き起こすアクションが発生するたびに `CF.widget.uiData_ method instead, which will give you the most recent available _ui_data_, and listen for all future updates as well. The _ui_data` イベントが発生するようにします。

`uiData` 関数を使用して、ウィジェット名 _sweeps_Sweepstakes_ の懸賞に対するユーザのエントリ数を表示する例。

```html
<span>You have <span id="entryCount">?</span> entries.</span>

<div class="cf_widgetLoader cf_w_sweeps_Sweepstakes"></div>

<button id='myNewSweepsButton'>New Sweeps Up Button!</button>

<script>
cf_scripts.afterload(function($, CF){
    CF.widget.uiData("sweeps_Sweepstakes", function(uiData){
        if(uiData.user && uiData.userStatus && uiData.userEntries){
            $("entryCount").html(""+ uiData.userEntries);
        }
        else{
            $("entryCount").html("0");
        }
    });
});
</script>
```

## リファラルオファー SignUp UI データ参照

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| date | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| rich text | HTML 文字列 |
| score | 符号付き 32 ビット整数 |
| sfdc campaign | Salesforce キャンペーン管理の統合で使用 |
| text | テキスト文字列 |

## リファラルオファー TrackProgress UI データ参照

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| date | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| rich text | HTML 文字列 |
| score | 符号付き 32 ビット整数 |
| sfdc campaign | Salesforce キャンペーン管理の統合で使用 |
| text | テキスト文字列 |

## 懸賞 UI データ参照（LM 懸賞ではなくソーシャルキャンペーン懸賞）

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| date | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| rich text | HTML 文字列 |
| score | 符号付き 32 ビット整数 |
| sfdc campaign | Salesforce キャンペーン管理の統合で使用 |
| text | テキスト文字列 |

## ソーシャルサインオン（フォーム入力ウィジェット）データ参照

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| date | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| rich text | HTML 文字列 |
| score | 符号付き 32 ビット整数 |
| sfdc campaign | Salesforce キャンペーン管理の統合で使用 |
| text | テキスト文字列 |

```javascript
{
"alt_id": "http://www.facebook.com/profile.php?id=1526228678",
"provider_name": "facebook",
"default_photo_url": "https://graph.facebook.com/1526228678/picture?type=large",
"email": "ian.b.taylor@gmail.com",
"verified_email": "ian.b.taylor@gmail.com",
"gender": "male",
"preferred_user_name": "IanTaylor",
"display_name": "Ian Taylor",
"birth_date": 343954800000,
"first_name": "Ian",
"last_name": "Taylor",
"city": null,
"state": null,
"region": null,
"postal_code": null,
"country": null,
"time_zone": null,
"connection_count": 0,
"credentials": {
"uid": "1526228678",
"scopes": "publish_actions",
"expires": "1371994082",
"accessToken": "BAAGFJ0KUFpcBABuNMptmYY...",
"type": "Facebook"
},
"about_me": null,
"cur_pos_title": "Senior Staff Engineer",
"phone_number": null,
"company": "Marketo",
"cur_pos_start_date": 1333231200000,
"cur_pos_summary": null
}
```
