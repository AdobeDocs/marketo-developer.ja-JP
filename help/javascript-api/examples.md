---
title: 「例」
description: 「Marketo コードの例」
feature: Javascript
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# 例

以下に、実証的なForms 2.0 web フォームの例のセットを示します。

## 送信成功後にフォームを非表示

この例では、訪問者をフォローアップページに移動させたり、現在のページをリロードしたりしません。

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function(form) {
    // Add an onSuccess handler
    form.onSuccess(function(values, followUpUrl) {
        // Get the form's jQuery element and hide it
        form.getFormElem().hide();
        // Return false to prevent the submission handler from taking the lead to the follow up url
        return false;
    });
});
```

## ユーザー定義 URL に訪問者を移動

この例では、訪問者を、設定済みの「ありがとうございます」ページではなく、送信に成功した後に JavaScript によって決定された URL に移動します。

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function(form) {
    //Add an onSuccess handler
    form.onSuccess(function(values, followUpUrl) {
        // Take the lead to a different page on successful submit, ignoring the form's configured followUpUrl
        location.href = "https://google.com/?q=marketo+forms+v2+examples";
        // Return false to prevent the submission handler continuing with its own processing
        return false;
    });
});
```

## フォームフィールド値の設定

次の使用例は、フォーム フィールドを設定します。

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function(form) {
    // Set the value of the Phone and Country fields
    form.vals({ "Phone":"555-555-1234", "Country":"USA"});
});
```

## フォーム送信時のフォームフィールド値の読み取り

この例では、フォーム送信時にフォームフィールドを読み取ります。

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function(form) {
    // Add an onSubmit handler
    form.onSubmit(function(){
        // Get the form field values
        var vals = form.vals();
        // You may wish to call other function calls here, for example to fire google analytics tracking or the like
        // callSomeFunction(vals);
        // We'll just alert them to show the principle
        alert("Submitted values: " + JSON.stringify(vals));
    });
}); 
```

## 非フォームクリックイベントでのフォーム送信

次の使用例では、フォームの一部ではない他の要素またはイベントのクリック イベントに基づいてフォームを送信します。

```javascript
// Load the form normally
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057);

// Find the button element that you want to attach the event to
var btn = document.getElementById("MyAlternativeSubmitButtonId");
btn.onclick = function() {
    // When the button is clicked, get the form object and submit it
    MktoForms2.whenReady(function (form) {
        form.submit();
    });
};
```

## ユーザーによるフォームの送信を防ぐ

この例では、フォームの送信ボタンを機能させるために、クリックカウンターボタンを 3 回以上クリックする必要があります。

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function (form) { 
    // Check if the form is submittable
    if (form.submittable()) {
        // Set it to be non submittable
        form.submittable(false);
    }
});

var clickCount = 0;
// Wire up the click counter button
var clickCounterBtn = document.getElementById("ClickCounter");
clickCounterBtn.onclick = function() {
    clickCount++;
    // Update the buttons's text
    clickCounterBtn.innerHTML = "Click Counter Button ("+clickCount+")";

    if (clickCount >= 3) {
        // Get the form and set it to be submittable
        MktoForms2.whenReady(function (form) {
            form.submittable(true);
        });
    }
};
```

## フォーム上の非表示フィールドに値を設定する

次の使用例は、非表示のフィールドの値を設定します。

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function (form) { 
    // Set values for the hidden fields, "userIsAwesome" and "enrollDate"
    // Note that these fields were configured in the form editor as hidden fields already
    form.vals({"userIsAwesome":"true", "enrollDate":"2014-01-01"});
});
```

## LightBox にフォームを表示

次の使用例は、URL にパラメーターが含まれている場合、Lightbox のスタイルダイアログのフォームを表示します `lightboxForm=true`.

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function (form) { 
    if (location.href.indexOf("lightboxForm=true") != -1) {
        MktoForms2.lightbox(form).show();
    }
});
```

## カスタム エラーメッセージを表示

この例では、カスタムビジネスロジックに基づいた送信に基づくカスタムエラーメッセージを示しています。

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function (form) { 
    //listen for the validate event
    form.onValidate(function() {
        // Get the values
        var vals = form.vals();
        //Check your condition
        if (vals.Country == "USA" && vals.vehicleSize != "Massive") {
            // Prevent form submission
            form.submittable(false);
            // Show error message, pointed at VehicleSize element
            var vehicleSizeElem = form.getFormElem().find("#vehicleSize");
            form.showErrorMessage("All Americans must have a massive vehicle", vehicleSizeElem);
        }
        else {
            // Enable submission for those who met the criteria
            form.submittable(true);
        }
  });
});
```
