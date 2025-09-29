---
title: Forms API リファレンス
description: Marketo Forms 2.0 API の包括的なリファレンスで、フォームの読み込みとレンダリングのための MktoForms2 およびフォームメソッド、パラメーター、コールバック、戻り値の詳細を説明します。
feature: Forms, Javascript
exl-id: 0f8d242f-0b27-4087-b080-3d41ebaa25b3
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 98%

---

# Forms API リファレンス

Forms 2.0 API を使用して操作する主なオブジェクトは 2 つあります。`MktoForms2` オブジェクトと `Form` オブジェクトです。`MktoForms2` オブジェクトは、Forms2 機能の上位レベルの公開名前空間であり、Form オブジェクトを作成、読み込み、取得するための関数が含まれています。

## MktoForms2 メソッド

<table>
  <tbody>
    <tr valign="top">
      <td><strong>メソッド</strong></td>
      <td><strong>説明</strong></td>
      <td><strong>パラメーター</strong></td>
      <td><strong>戻り値</strong></td>
    </tr>
    <tr valign="top">
      <td>.loadForm(baseUrl, munchkinId, formId, callback)</td>
      <td>Marketo サーバーからフォーム記述子を読み込み、新しい Form オブジェクトを作成します。</td>
      <td> baseUrl（文字列） - サブスクリプションの Marketo サーバーインスタンスへの URL</td>
      <td>未定義</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>munchkinId（文字列）- サブスクリプションのMunchkin ID</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>formId（文字列または数値）- 読み込むフォームのフォームバージョン ID（Vid）</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>callback（オプション）（関数）- 構築された Form オブジェクトが読み込まれ、初期化されたら渡すコールバック関数。</td>
      <td></td>
    </tr>
    <tr valign="top">
      <td>.lightbox(form, opts)</td>
      <td>Form オブジェクトを含むライトボックススタイルのモーダルダイアログをレンダリングします。</td>
      <td>form（Form オブジェクト）- ライトボックスにレンダリングする Form オブジェクトのインスタンス。</td>
      <td>.show() および .hide() メソッドを備えたライトボックスオブジェクト。</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>opts（オプション）（オブジェクト）- ライトボックスオブジェクトに渡されるオプションのオブジェクト</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>onSuccess（関数） - フォームを送信した際にトリガーされるコールバック。</td>
      <td></td>
    </tr>
    <tr>
          <td></td>
      <td></td>
      <td>closeBtn（ブーリアン） デフォルト true - ライトボックスダイアログに閉じるボタン（X）を表示するかどうかを制御します。</td>
      <td></td>
    </tr>
    <tr valign="top">
      <td>.newForm(formData, callback)</td>
      <td>フォーム記述子 JS オブジェクトから新しい Form オブジェクトを作成します。すべてのスタイルシートと既知のリード情報が取得され、Form オブジェクトが作成された後に呼び出されるコールバック関数を追加します。</td>
      <td>formData（フォーム記述子オブジェクト） - Marketo Forms V2 エディターで作成されたフォーム記述子オブジェクト</td>
      <td>未定義</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>callback（オプション）（関数）- このコールバックは、Form オブジェクトの新しく作成されたインスタンスである単一の引数で呼び出されます。</td>
      <td></td>
    </tr>
    <tr valign="top">
      <td>.getForm(formId)</td>
      <td>フォーム識別子で以前に作成された Form オブジェクトを取得します</td>
      <td> formId（数値または文字列）- Form Vid の識別子。</td>
      <td>Form オブジェクト</td>
    </tr>
    <tr valign="top">
      <td>.allForms()</td>
      <td>ページ上で以前に作成されたすべての Form オブジェクトの配列を取得します。</td>
      <td>該当なし</td>
      <td>Form オブジェクトの配列</td>
    </tr>
    <tr valign="top">
      <td>.getPageFields()</td>
      <td>トラッキング目的で関心がある場合のある URL とリファラーからのデータを含む JS オブジェクトを取得します。</td>
      <td>該当なし</td>
      <td>オブジェクト</td>
    </tr>
    <tr valign="top">
      <td>.whenReady(callback)</td>
      <td>「準備完了」になるページ上の各フォームに対して 1 回だけ呼び出されるコールバックを追加します。準備完了とは、つまり、フォームが存在し、最初にレンダリングされ、最初のコールバックが呼び出されたことです。この関数が呼び出された時点で既に準備が整っているフォームがある場合は、渡されたコールバックがすぐに呼び出されます。</td>
      <td>callback（関数） - コールバックには、Form オブジェクトという単一の引数が渡されます。</td>
      <td>MktoForms2 オブジェクト</td>
    </tr>
    <tr valign="top">
      <td>.onFormRender(callback)</td>
      <td>ページ上のフォームをレンダリングするたびに呼び出されるコールバックを追加します。フォームは最初に作成した際にレンダリングされ、その後、表示ルールによってフォームの構造が変更されるたびに再度レンダリングされます。</td>
      <td>callback（関数）- コールバックには、レンダリングしたフォームの Form オブジェクトという単一の引数が渡されます。</td>
      <td>MktoForms2 オブジェクト</td>
    </tr>
    <tr valign="top">
      <td>.whenRendered(callback)</td>
      <td>onFormRender と同様に、フォームをレンダリングするたびに呼び出されるコールバックを追加します。さらに、既にレンダリングしているすべてのフォームに対して、コールバックをすぐに呼び出します。</td>
      <td>callback（関数） - コールバックには、レンダリングしたフォームの Form オブジェクトという単一の引数が渡されます。</td>
      <td></td>
    </tr>
</table>

## Form メソッド

<table>
  <tbody>
    <tr valign="top">
      <td><strong>メソッド</strong></td>
      <td><strong>説明</strong></td>
      <td><strong>パラメーター</strong></td>
      <td><strong>戻り値</strong></td>
    </tr>
    <tr valign="top">
      <td>.render(formElem)</td>
      <td>Form オブジェクトをレンダリングし、フォームを含むフォーム要素を囲む jQuery オブジェクトを返します。formElem が渡された場合は、それがフォーム要素として使用され、それ以外の場合は新しい要素が作成されます。</td>
      <td>formElem（オプション）- レンダリング先の jQuery オブジェクトで囲まれたフォーム要素。</td>
      <td> レンダリングされたフォームを含む、jQuery オブジェクトで囲まれたフォーム要素。</td>
    </tr>
    <tr valign="top">
      <td>.getId()</td>
      <td>フォームの ID を取得します。</td>
      <td>該当なし</td>
      <td>数値 - このフォームが表すフォームオブジェクトの ID</td>
    </tr>
    <tr valign="top">
      <td>.getFormElem()</td>
      <td>レンダリングされたフォームの、jQuery で囲まれたフォーム要素を取得します。</td>
      <td>該当なし</td>
      <td>jQuery オブジェクトで囲まれたフォーム要素、またはフォームが render() メソッドでまだレンダリングされていない場合は null です。</td>
    </tr>
    <tr valign="top">
      <td>.validate()</td>
      <td>フォームを強制的に検証し、存在する可能性のあるエラーをハイライト表示して結果を返します。フォームを送信しません。</td>
      <td>該当なし</td>
      <td>ブーリアン - フォーム上のすべての検証に合格した場合は true を返し、それ以外の場合は false を返します。</td>
    </tr>
    <tr valign="top">
      <td>.onValidate(callback)</td>
      <td>検証がトリガーされるたびに呼び出される検証コールバックを追加します。</td>
      <td>callback（関数） - 検証が発生するたびにトリガーされるコールバック。コールバックには、検証が成功したかどうかを示すブール値である 1 つのパラメーターが渡されます。</td>
      <td>Form オブジェクト - 連鎖の目的で、メソッドが呼び出されたのと同じ Form オブジェクト。</td>
    </tr>
    <tr valign="top">
      <td>.submit()</td>
      <td>フォームの送信イベントをトリガーします。これにより、送信からフローが開始され、検証が実行されると、onSubmit イベントが発生します。フォームが送信され、フォームの送信が成功した場合は onSuccess イベントが発生します。</td>
      <td>該当なし</td>
      <td>Form オブジェクト - 連鎖の目的で、メソッドが呼び出されたのと同じ Form オブジェクト。</td>
    </tr>
    <tr valign="top">
      <td>.onSubmit(callback)</td>
      <td>フォームを送信した際に呼び出されるコールバックを追加します。これは、リクエストの成功／失敗がわかる前に、送信を開始した際に発生します。</td>
      <td>callback - フォームを送信した際に呼び出される関数。このコールバックには、この Form オブジェクトという 1 つの引数が渡されます。</td>
      <td>Form オブジェクト - 連鎖の目的で、メソッドが呼び出されたのと同じ Form オブジェクト。</td>
    </tr>
    <tr valign="top">
      <td>.onSuccess(callback)</td>
      <td>フォームを正常に送信したが、リードがフォローアップページに転送される前に呼び出されるコールバックを追加します。送信が成功した後にリードがフォローアップページに転送されるのを防ぐために使用できます。</td>
      <td>callback - フォームを正常に送信した際に呼び出される関数。このコールバックには、2 つの引数が渡されます。送信した値と、ユーザの転送先となるフォローアップページの文字列 URL を含む JS オブジェクト。フォローアップページを設定していない場合は null または空の文字列になります。特別な動作：このコールバックが「false」（=== を使用して測定）を返す場合、訪問者はフォローアップページに転送されず、ページはリロードされません。これにより、実装者はフォローアップ URL に対して追加の処理を実行したり、ページを離れる代わりに JavaScript を使用してページでアクションを実行したりできます。</td>
      <td>Form オブジェクト - 連鎖の目的で、メソッドが呼び出されたのと同じ Form オブジェクト。</td>
    </tr>
    <tr valign="top">
      <td>.submittable(canSubmit) <em>次のように使用することも可能：</em><em>.submitable(canSubmit)</em></td>
      <td>フォームを送信できるかどうかを取得または設定します。引数を指定せずに呼び出した場合は値を取得し、1 つの引数を指定して呼び出した場合は値を設定します。これを使用すると、通常のフォーム以外の条件を満たす必要がある場合にフォームが送信されないようにすることができます。</td>
      <td>canSubmit（オプション）（ブール値）- フォームを送信可能または送信不可能に設定します。</td>
      <td>ブール値または Form オブジェクト - 引数を指定せずに呼び出した場合、フォームが送信可能かどうかを示すブール値を返します。1 つの引数を指定して呼び出した場合、この Form オブジェクトを連鎖的に返します。 </td>
    </tr>
    <tr valign="top">
      <td>.allFieldsFilled()</td>
      <td>フォームのすべてのフィールドに空白以外の値を設定した場合、true を返します。</td>
      <td>該当なし</td>
      <td>ブール値 - すべてのフィールドが空白／空／未設定／null 以外の値の場合は true、それ以外の場合は false。</td>
    </tr>
    <tr valign="top">
      <td>.setValues(vals)</td>
      <td>フォーム内の 1 つ以上のフィールドに値を設定します。</td>
      <td>vals - JS オブジェクト。オブジェクト内の各キーと値のペアに対して、キーという名前のフォームフィールドに値が設定されます。</td>
      <td>未定義</td>
    </tr>
    <tr valign="top">
      <td>.getValues()</td>
      <td>フォーム内のすべてのフィールドのすべての値を取得します。</td>
      <td>該当なし</td>
      <td>オブジェクト - フォーム内のフィールドの名前と値を表すキーと値のペアを含む JS オブジェクト。</td>
    </tr>
    <tr valign="top">
      <td>.addHiddenFields(values)</td>
      <td>フォームに input type=hidden フィールドを追加します。</td>
      <td>values - フォームに追加する非表示フィールドの名前と値を表すキーと値のペアを含む JS オブジェクト。</td>
      <td>未定義</td>
    </tr>
    <tr valign="top">
      <td>.vals(values)</td>
      <td>jQuery スタイルの .vals() セッター／ゲッター。引数を指定せずに呼び出した場合、getValues() の呼び出しと同じになります。1 つの引数を指定して呼び出した場合、setValues() の呼び出しと同じになります</td>
      <td>values（オプション）- オブジェクト</td>
      <td>未定義</td>
    </tr>
    <tr valign="top">
      <td>.showErrorMessage(msg, elem)</td>
      <td>elem を指すエラーメッセージを表示します。</td>
      <td>msg（HTML の文字列）- 表示するエラーのテキストを含む文字列。</td>
            <td>Form オブジェクト - 連鎖用の Form オブジェクト。</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>elem（オプション）（jQuery オブジェクト）- エラーが指す要素。未設定の場合は、フォームの送信ボタンが使用されます。</td>
<td></td>
    </tr>
  </tbody>
</table>
