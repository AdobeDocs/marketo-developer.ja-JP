---
title: Marketo オブジェクト
feature: Email Programs
description: リード、オポチュニティ、カスタムオブジェクトでMarketo Velocityを使用する方法、フィールドの読み込み、上位10件のリストアクセス、SFDCのリレーションシップ、$TriggerObjectの順に説明します。
exl-id: 88c63d72-7aa5-4550-9e1a-887a479872e1
TQID: https://experienceleague.adobe.com/PvLJb-AOk6DKaNINycpzk5ojZiL8UNcanRg3vXmsGCI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 2%

---

# Marketo オブジェクト

Marketo Velocityの導入では、次のMarketo ソースからのデータを使用できます。

- リード
- 商談
- カスタムオブジェクト
- モバイルアプリ
- モバイルアプリのインストール

## フィールドをロードしています

スクリプト内のフィールドを使用するには、スクリプトトークンエディターの対応するリストの下にあるフィールドを選択します。

スクリプトが読み込まれていないフィールドを参照する場合、スクリプトは実行時に失敗します。 フィールドメニューからスクリプトにフィールドをドラッグして読み込み、カーソルに参照を追加します。

## 商談およびカスタムオブジェクトリスト

商談とカスタムオブジェクトの場合、Marketoは各タイプの最新に更新された10個のオブジェクトのみを読み込みます。 ここで説明する手順に従って、使用可能なカスタムオブジェクトの数を増やすことができます。

Marketoは、`<objectName>List`という名前のリスト内のオブジェクトを提供し、最新に更新されたレコードから最新に更新されたレコードに順序付けします。 最新に更新された商談から「金額」フィールドにアクセスするには、次を使用します。

`${OpportunityList.get(0).Amount}`

次の使用例は、OpportunityList オブジェクトを参照し、get メソッドを使用してインデックス 0のレコードにアクセスし、そのレコードからAmount プロパティを取得します。

商談フィールドまたはカスタムオブジェクトフィールドをエディターにドラッグすると、Marketoはインデックス 0のレコードからフィールドを自動的に取得します。

## SFDC カスタムオブジェクトの関連付け

SFDC カスタムオブジェクトを使用するには、オブジェクトにMarketo リードとのリレーションシップが1つだけ必要です。 一般的に、オブジェクトは連絡先とアカウントの両方を通じてリンクされます。 リード/取引先責任者の関係が有効になっているオブジェクトのみを同期します。

## トリガーオブジェクト

キャンペーンで「商談に追加」、「商談が更新されました」、「`<Custom Object Name>`」トリガーを使用すると、トリガーキャンペーンで実行されるスクリプトトークンに`$TriggerObject`変数を使用できます。 この変数は、`<Custom Object Name>`は更新済みトリガーではサポートされていません。

この変数は、キャンペーンをトリガーしたオブジェクトを参照します。 別の変数名を使用してオブジェクトにアクセスする際に使用できる同じレコードデータが含まれています。

バッチキャンペーンで`$TriggerObject`を参照するトークンは使用しないでください。 オブジェクトはバッチキャンペーンでは使用できず、メール送信が失敗します。

例えば、商品の注文のカスタムオブジェクトがキャンペーンをトリガーする場合、`$TriggerObject`変数はリードが追加された注文を公開します。

次の例は、注文フォローアップメールのスクリプトを示しています。

```html
<div>
<strong>Your order information:</strong>
##pull information from the Triggering Order and format it in a list
<ul>
<li>Product Ordered: $!{TriggerObject.ProductName}</li>
<li>Product Quantity: $!{TriggerObject.Quanitity}</li>
<li>Shipping Address: $!{TriggerObject.ShippingAddress}</li>
<li>Billing Address: $!{TriggerObject.BillingAddress}</li>
<li>Order Total: $!{TriggerObject.Amount}</li>
</ul>
<p><a href="$!{TriggerObject.OrderURL}">View Your Order Online</a></p>
</div>
```

トリガーアクションによってオブジェクトが決まります。 使用可能なオブジェクトにローカルデータが含まれているかを判断するために、追加のコードは必要ありません。 参照するオブジェクトを明示的に識別するため、使用可能で適切な場合は`$TriggerObject`を使用します。

注意：`$TriggerObject`を使用する場合は、編集ペインでオブジェクトのフィールドを選択して、スクリプトで使用できるようにします。

注2: `$TriggerObject`は、「追加された」トリガーでのみ機能し、「更新された」トリガーでは機能しません。
