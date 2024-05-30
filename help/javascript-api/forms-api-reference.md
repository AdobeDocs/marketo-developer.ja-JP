---
title: 「Forms API リファレンス」
description: 「Forms API リファレンス」
feature: Forms, Javascript
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 2%

---


# Forms API リファレンス

Forms 2.0 API を使用してやり取りする主なオブジェクトは 2 つあります。 この `MktoForms2` オブジェクトと `Form` オブジェクト。 この `MktoForms2` オブジェクトは、Forms2 機能の最上位の公開されている名前空間で、フォームオブジェクトを作成、読み込み、取得する関数が含まれています。

## MktoForms2 メソッド

<table>
  <tbody>
    <tr valign="top">
      <td><strong>方法</strong></td>
      <td><strong>説明</strong></td>
      <td><strong>パラメーター</strong></td>
      <td><strong>戻り値</strong></td>
    </tr>
    <tr valign="top">
      <td>.loadForm （baseUrl, munchkinId, formId, callback）</td>
      <td>Marketo サーバーからフォーム記述子を読み込み、新しいフォームオブジェクトを作成します。</td>
      <td> baseUrl （String） – 購読用のMarketo サーバーインスタンスの URL</td>
      <td>未定義</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>munchkinId （String） – 購読の Munchkin ID</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>formId （文字列または数値） – 読み込むフォームのフォームバージョン ID （Vid）</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>callback （オプション） （Function） – 構築されたフォームオブジェクトが読み込まれて初期化された後に、そのオブジェクトを渡すコールバック関数。</td>
      <td></td>
    </tr>
    <tr valign="top">
      <td>.lightbox （フォーム、オプション）</td>
      <td>フォームオブジェクトを含んだライトボックススタイルのモーダルダイアログをレンダリングします。</td>
      <td>フォーム（フォームオブジェクト） – ライトボックスでレンダリングするフォームオブジェクトのインスタンス。</td>
      <td>.show （） メソッドと.hide （） メソッドを持つ Lightbox オブジェクト</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>opts （optional）（Object） - Lightbox オブジェクトに渡すオプションのオブジェクト</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>onSuccess （Function） – フォームが送信されたときにトリガーされるコールバック。</td>
      <td></td>
    </tr>
    <tr>
          <td></td>
      <td></td>
      <td>closeBtn （Boolean） default true - ライトボックスダイアログに閉じるボタン（X）を表示するかどうかを制御します。</td>
      <td></td>
    </tr>
    <tr valign="top">
      <td>.newForm （formData, callback）</td>
      <td>フォーム記述子 JS オブジェクトから新しいフォームオブジェクトを作成します。 すべてのスタイルシートと既知のリード情報を取得し、フォームオブジェクトを作成したら呼び出されるコールバック関数を追加します。</td>
      <td>formData （フォーム記述子オブジェクト） - Marketo Forms V2 エディターで作成されるフォーム記述子オブジェクト</td>
      <td>未定義</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>callback （オプション）（Function） – このコールバックは、1 つの引数（フォームオブジェクトの新しく作成されたインスタンス）で呼び出されます。</td>
      <td></td>
    </tr>
    <tr valign="top">
      <td>.getForm （formId）</td>
      <td>フォーム識別子から作成済みのフォームオブジェクトを取得します</td>
      <td> formId （数値または文字列） - Form Vid の識別子。</td>
      <td>フォームオブジェクト</td>
    </tr>
    <tr valign="top">
      <td>.allForms （）</td>
      <td>ページ上で以前に作成されたすべてのフォームオブジェクトの配列を取得します。</td>
      <td>該当なし</td>
      <td>フォームオブジェクトの配列</td>
    </tr>
    <tr valign="top">
      <td>.getPageFields （）</td>
      <td>トラッキング目的で関心がある可能性のある URL およびリファラーからのデータを含む JS オブジェクトを取得します。</td>
      <td>該当なし</td>
      <td>オブジェクト</td>
    </tr>
    <tr valign="top">
      <td>.whenReady （callback）</td>
      <td>「準備完了」になるページ上の各フォームに対して 1 回だけ呼び出されるコールバックを追加します。 準備とは、フォームが存在し、最初にレンダリングされ、最初のコールバックが呼び出されたことを意味します。 この関数が呼び出される時点で準備が整っているフォームが既にある場合、渡されたコールバックが直ちに呼び出されます。</td>
      <td>callback （Function） – コールバックには、1 つの引数であるフォームオブジェクトが渡されます。</td>
      <td>MktoForms2 オブジェクト</td>
    </tr>
    <tr valign="top">
      <td>.onFormRender （callback）</td>
      <td>ページ上のフォームがレンダリングされるたびに呼び出されるコールバックを追加します。 Formsは最初に作成されたときに、その表示ルールによってフォームの構造が変わるたびに再びレンダリングされます。</td>
      <td>callback （関数） – コールバックには、レンダリングされたフォームのフォームオブジェクトである単一の引数が渡されます。</td>
      <td>MktoForms2 オブジェクト</td>
    </tr>
    <tr valign="top">
      <td>.whenRendered （callback）</td>
      <td>onFormRender と同様に、フォームがレンダリングされるたびに呼び出されるコールバックを追加します。 さらに、既にレンダリングされたすべてのフォームに対して、すぐにコールバックが呼び出されます。</td>
      <td>callback （Function） – コールバックには、レンダリングされたフォームのフォームオブジェクトである単一の引数が渡されます。</td>
      <td></td>
    </tr>
</table>


## フォームメソッド

<table>
  <tbody>
    <tr valign="top">
      <td><strong>方法</strong></td>
      <td><strong>説明</strong></td>
      <td><strong>パラメーター</strong></td>
      <td><strong>戻り値</strong></td>
    </tr>
    <tr valign="top">
      <td>.render （formElem）</td>
      <td>フォームオブジェクトをレンダリングし、フォームを含むフォーム要素をラップする jQuery オブジェクトを返します。 formElem が渡された場合は、それをフォーム要素として使用します。それ以外の場合は、新しく作成します。</td>
      <td>formElem （オプション） – レンダリング先の jQuery オブジェクトでラップされたフォーム要素。</td>
      <td> レンダリングされたフォームを含む、jQuery オブジェクトラップされたフォーム要素。</td>
    </tr>
    <tr valign="top">
      <td>.getId （）</td>
      <td>フォームの ID を取得します。</td>
      <td>該当なし</td>
      <td>数値 – このフォームが表すフォームオブジェクトの ID</td>
    </tr>
    <tr valign="top">
      <td>.getFormElem （）</td>
      <td>レンダリングされたフォームの jQuery でラップされたフォーム要素を取得します。</td>
      <td>該当なし</td>
      <td>jQuery オブジェクトラップされたフォーム要素、またはフォームがまだ render （） メソッドでレンダリングされていない場合は null。</td>
    </tr>
    <tr valign="top">
      <td>.validate （）</td>
      <td>フォームの検証を強制し、存在する可能性のあるエラーをハイライト表示して結果を返します。 フォームを送信しません。</td>
      <td>該当なし</td>
      <td>ブール値 – フォーム上のすべてのバリデータが渡された場合は true を返し、それ以外の場合は false を返します。</td>
    </tr>
    <tr valign="top">
      <td>.onValidate （callback）</td>
      <td>検証がトリガーされるたびに呼び出される検証コールバックを追加します。</td>
      <td>callback （Function） – 検証が発生するたびにトリガーされるコールバック。 コールバックには、1 つのパラメーター（検証が成功したかどうかを示すブール値）が渡されます。</td>
      <td>フォームオブジェクト – メソッドが呼び出されたのと同じフォームオブジェクト（連鎖の目的）。</td>
    </tr>
    <tr valign="top">
      <td>.submit （）</td>
      <td>フォームの送信イベントをトリガーします。 これは、送信フローから開始し、検証を実行し、onSubmit イベントを発生させ、フォームを送信し、フォームの送信が成功した場合に onSuccess イベントを発生させます。</td>
      <td>該当なし</td>
      <td>フォームオブジェクト – メソッドが呼び出されたのと同じフォームオブジェクト（連鎖の目的）。</td>
    </tr>
    <tr valign="top">
      <td>.onSubmit （callback）</td>
      <td>フォームが送信されたときに呼び出されるコールバックを追加します。 これは、リクエストの成功/失敗がわかる前に、送信が開始されると実行されます。</td>
      <td>callback - フォームが送信されたときに呼び出される関数。 このコールバックには、このフォームオブジェクトという 1 つの引数が渡されます。</td>
      <td>フォームオブジェクト – メソッドが呼び出されたのと同じフォームオブジェクト（連鎖の目的）。</td>
    </tr>
    <tr valign="top">
      <td>.onSuccess （callback）</td>
      <td>フォームが正常に送信された後、リードがフォローアップページに転送される前に呼び出されるコールバックを追加します。 送信に成功した後に、リードがフォローアップページに転送されるのを防ぐために使用できます。</td>
      <td>callback - フォームが正常に送信されたときに呼び出される関数。 このコールバックには 2 つの引数が渡されます。 送信された値と、ユーザーの転送先となるフォローアップページの文字列 URL を含む JS オブジェクト。設定されたフォローアップページがない場合は null または空の文字列。 特別な動作：このコールバックが（===を使用して測定された）「false」を返した場合、訪問者はフォローアップページに転送されず、ページは再読み込みされません。 これにより、実装者は、フォローアップ URL に対して追加の処理を行ったり、ページを離れることなく JavaScript を使用してページに対するアクションを実行したりできます。</td>
      <td>フォームオブジェクト – メソッドが呼び出されたのと同じフォームオブジェクト（連鎖の目的）。</td>
    </tr>
    <tr valign="top">
      <td>.submittable （canSubmit） <em>次の URL も利用できます。</em> <em>.submitable （canSubmit）</em></td>
      <td>フォームを送信できるかどうかを取得または設定します。 引数を指定せずに呼び出した場合はその値を取得し、1 つの引数を指定して呼び出した場合はその値を設定します。これを使用すると、通常のフォーム以外の条件を満たす必要がある場合に、フォームが送信されないようにすることができます。</td>
      <td>canSubmit （optional）（Boolean） – フォームを送信可能または送信不可能に設定します。</td>
      <td>ブール値またはフォームオブジェクト – 引数を指定せずに呼び出した場合、フォームが送信可能かどうかを示すブール値を返します。 1 つの引数を指定して呼び出された場合は、このフォームオブジェクトが連鎖的に返されます。 </td>
    </tr>
    <tr valign="top">
      <td>.allFieldsFilled （）</td>
      <td>フォームのすべてのフィールドに空白以外の値が設定されている場合、true を返します。</td>
      <td>該当なし</td>
      <td>ブール値 – すべてのフィールドに空白以外の値または空の値または未設定の値または null 値がある場合は true、そうでない場合は false を返します。</td>
    </tr>
    <tr valign="top">
      <td>.setValues （vals）</td>
      <td>フォーム内の 1 つ以上のフィールドに値を設定します。</td>
      <td>vals - JS オブジェクト。 オブジェクト内のキーと値のペアごとに、key という名前のフォームフィールドが value に設定されます。</td>
      <td>未定義</td>
    </tr>
    <tr valign="top">
      <td>.getValues （）</td>
      <td>フォーム内のすべてのフィールドのすべての値を取得します。</td>
      <td>該当なし</td>
      <td>オブジェクト – フォーム内のフィールドの名前と値を表すキーと値のペアを含む JS オブジェクト。</td>
    </tr>
    <tr valign="top">
      <td>.addHiddenFields （values）</td>
      <td>input type=hidden フィールドをフォームに追加します。</td>
      <td>values - フォームに追加する非表示フィールドの名前と値を表すキーと値のペアを含む JS オブジェクト。</td>
      <td>未定義</td>
    </tr>
    <tr valign="top">
      <td>.vals （values）</td>
      <td>jQuery スタイル .vals （）の設定/取得 引数を指定せずに呼び出した場合、getValues （）の呼び出しと同じになります。 1 つの引数を指定して呼び出した場合、setValues （）の呼び出しと同じになります</td>
      <td>values （optional） – オブジェクト</td>
      <td>未定義</td>
    </tr>
    <tr valign="top">
      <td>.showErrorMessage （msg, elem）</td>
      <td>要素を指すエラーメッセージを表示します。</td>
      <td>msg （HTMLの文字列） – 表示するエラーのテキストを含む文字列。</td>
            <td>フォームオブジェクト – このフォームオブジェクトは、チェーン用です。</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>elem （オプション）（jQuery オブジェクト） – エラーの参照先の要素。 未設定の場合は、フォームの送信ボタンが使用されます。</td>
<td></td>
    </tr>
  </tbody>
</table>
