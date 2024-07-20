---
title: ソーシャル
description: ソーシャル
feature: Social, Javascript
exl-id: 82d2b86f-5efe-4434-b617-d27f76515a79
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 4%

---

# ソーシャル

[Marketo ソーシャルマーケティング ](https://business.adobe.com/products/marketo/social-marketing.html) を使用すると、マーケターは web サイトやランディングページにソーシャルウィジェットを埋め込むことができます。 ソーシャルウィジェットには、投票、ソーシャル共有ボタン、ビデオ、キャンペーン、紹介オファーなどのプロモーションが含まれます。

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

ソーシャルウィジェットをカスタマイズする基本的な方法は 2 つあります。

1. 製品の通常の UI を使用し、UI で特定のアクションが発生した場合に通知されるイベントリスナーを付加して、追加のビジネスロジックを実行する。
1. 製品の通常の UI をカスタム UI に置き換え、必要に応じて UI のポップアップ「ステージ」をアクティブ化する。

## 通常の UI へのイベントの添付

CF JavaScript ライブラリでイベントを登録するには、グローバルに登録する方法と、1 つのウィジェットで登録する方法の 2 つがあります。 イベントは、イベントテーブルの以下に記載されています。

### グローバルイベント購読

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

### ウィジェットごとのイベント購読

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

この例では、「referral_SignUp」という名前のウィジェットのオファー登録を完了した後、ID が「signedUp」の以前に非表示にされた要素を示しています。

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
| share_sent | 共有リクエストが処理のためにサーバーに送信されるたびに呼び出されます | 共有機能を持つすべてのウィジェット | 1.&quot;share_sent&quot;（String） <br>2. 送信されたパラメーター（オブジェクト） |
| share_success | 共有要求が正常に処理されたときに発生します。 | 共有機能を持つすべてのウィジェット。 | 1.&quot;share_success&quot;（String） <br>2. 送信されたメッセージと短縮 URL を含む、応答オブジェクトを共有します（オブジェクト） |
| vote_success | ユーザーが投票に成功したときに発生します。 | ポーリング、VS、投票ウィジェット | 1. &quot;vote_success&quot; （String） <br>2. タイトル、説明、エンティティ識別子（オブジェクト）など、投票された項目 |
| offer_enrolled | ユーザーがオファーへの登録に成功したときに呼び出されます | すべてのオファーウィジェット | 1.&quot;offer_enrolled&quot;（文字列） <br>2. ユーザープロパティ（オブジェクト）、<br>3 を変更しました。 変更されたユーザー属性（オブジェクト） |
| profile_saved | ユーザーがプロファイル キャプチャからプロファイルを更新したときに発生します。 | プロファイルキャプチャが有効になっているすべての非オファーウィジェット | 1.&quot;profile_saved&quot;（String） <br>2. ユーザープロパティ （オブジェクト） <br>3 を変更しました。 変更されたユーザー属性（オブジェクト） |
| video_loaded | 埋め込みビデオが完全に読み込まれて初期化されたときに呼び出されます。 | VideoShare ウィジェット | 1. video_loaded （文字列） 2. ビデオを保持する「.cf_videoshare_wrap」要素（jQuery オブジェクト） |

## UI のカスタム UI への置き換え

UI をカスタム UI に置き換えるには、まず通常の UI をオフにする必要があります。これを行うには、オプション _popupUIOnly_ を _true_ に設定します。 このオプションを設定すると、標準 UI はページの読み込み時にレンダリングされず、代わりにウィジェットがデータを取得し、_CF.widget.activate_ 関数を呼び出してポップアップステージの 1 つを開始するのを待ち、実行するオプションを提供します。

以下の例は、_referral_SignUp_ という名前のリファラルオファーウィジェットに対してリファラルオファーのサインアップフローを開始するカスタムボタンを作成する例です。

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

クリックハンドラーの追加は一般的なので、クリックハンドラーを追加するためのショートカットメソッドがあります。 次の例は、機能的には前の例と同じです。

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

## ウィジェット UI データを代替の UI に入力する方法

置き換える UI を描画するためにウィジェットに関するデータが必要な場合は、特別なイベント _ui_data_ からデータを取得できます。 通常の `CF.widget.listen` 関数を使用してこのイベントをリッスンできますが、そうすると、ウィジェットが既に the_ui_data_ イベントを発生させた後にイベントリスナーが追加され、データを受信できなくなる競合状態が発生する可能性があります。 この競合を避けるために、`CF.widget.uiData_ method instead, which will give you the most recent available _ui_data_, and listen for all future updates as well. The _ui_data` イベントは、`popupUIOnly` のオプションでその UI を無効にした場合でも、ウィジェットの標準 UI を再描画する原因となったアクションが実行されるたびに使用されます。

`uiData` の関数を使用して、ウィジェット名が _sweaps_Sweepstakes_ の Sweepstakes に対するユーザーのエントリ数を表示する例を示します。

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

## 参照オファーのサインアップ UI データ参照

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| 日 | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| リッチテキスト | HTML文字列 |
| スコア | 符号付き 32 ビット整数 |
| sfdc キャンペーン | Salesforce キャンペーン管理統合で使用 |
| テキスト | テキスト文字列 |

## 参照オファーの TrackProgress UI データ参照

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| 日 | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| リッチテキスト | HTML文字列 |
| スコア | 符号付き 32 ビット整数 |
| sfdc キャンペーン | Salesforce キャンペーン管理統合で使用 |
| テキスト | テキスト文字列 |

## 広告キャンペーン UI データ参照（LM 広告ではなくソーシャルキャンペーン広告）

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| 日 | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| リッチテキスト | HTML文字列 |
| スコア | 符号付き 32 ビット整数 |
| sfdc キャンペーン | Salesforce キャンペーン管理統合で使用 |
| テキスト | テキスト文字列 |

## ソーシャルサインオン（フォーム入力ウィジェット）データ参照

| タイプ | 説明 |
|---------------|----------------------------------------------------|
| 日 | 「yyyy-MM-dd」形式の日付値 |
| number | 整数または浮動小数点数 |
| リッチテキスト | HTML文字列 |
| スコア | 符号付き 32 ビット整数 |
| sfdc キャンペーン | Salesforce キャンペーン管理統合で使用 |
| テキスト | テキスト文字列 |

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
