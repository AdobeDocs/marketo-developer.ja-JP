---
title: Marketo オブジェクト
feature: Email Programs
description: リード、商談、カスタムオブジェクト、フィールドの読み込み、上位 10 件のリストアクセス、Marketoの関係、$TriggerObject とSFDC Velocity の使用に関するガイドです。
exl-id: 88c63d72-7aa5-4550-9e1a-887a479872e1
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 1%

---

# Marketo オブジェクト

Marketoの Velocity 実装は、リード、オポチュニティ、カスタムオブジェクト、モバイルアプリ、モバイルアプリのインストールなど、Marketo内の複数のソースからのデータに対して動作できます。

## フィールドをロードしています

スクリプトで使用するフィールドを読み込むには、スクリプトトークンエディターの対応するリストでそのフィールドをオンにする必要があります。

フィールドがスクリプト内で参照されている場合にフィールドを読み込まないと、スクリプトの実行が実行時に失敗します。 フィールドメニューからスクリプトにフィールドをドラッグ&amp;ドロップできます。 これにより、フィールドを読み込むことができ、カーソル位置のフィールドへの参照が追加されます。

## 商談とカスタムオブジェクトリスト

商談またはカスタムオブジェクトから取得する場合、タイプの最近更新された 10 個のオブジェクトのみが読み込まれます。 使用可能なカスタムオブジェクトの数は、ここで説明する手順に従って増やすことができます。 これらは、`<objectName>List` という名前のリストとして提供され、最も新しいレコードから順に並べられます。 したがって、最近更新されたオポチュニティから「金額」フィールドにアクセスするには、次を使用します。

`${OpportunityList.get(0).Amount}`

次の使用例では、OpportunityList オブジェクトを参照し、get メソッドを使用して 0 でインデックスが設定されたレコードにアクセスし、返されたオブジェクトから Amount プロパティを取得します。 商談またはカスタムオブジェクトからエディターにフィールドをドラッグすると、0 でインデックス付けされたレコードからフィールドが自動的に取得されます。

## SFDCのカスタムオブジェクトの関係

SFDC カスタムオブジェクトを使用するには、Marketo リードとの関係が 1 つだけである必要があります。 多くの場合、オブジェクトは連絡先とアカウントの両方を通じてリンクされるので、リードと連絡先の関係を有効にしてオブジェクトをMarketoにのみ同期することが重要です。

## トリガーオブジェクト

「Added to Opportunity」、「Opportunity is Updated」、または「Added to `<Custom Object Name>`」トリガーでキャンペーンがトリガーされると、トリガーキャンペーンのコンテキスト内で実行されるスクリプトトークンで、特別な変数が使用できるようになります。`$TriggerObject ` （`<Custom Object Name>` is Updatedトリガーではサポートされていません）。  `$TriggerObject` 参照を使用するトークンをバッチキャンペーンで使用すると、このオブジェクトはどの種類のバッチキャンペーンでも使用できないので、メール送信は失敗します。  これは、キャンペーンをトリガーしたオブジェクトへの参照です。 オブジェクトには、別の変数名でアクセスされた場合にレコードに含まれているすべてのデータが含まれています。

例えば、製品オーダーのカスタムオブジェクトを介してキャンペーンがトリガーされた場合、リードが追加されたオーダーは `$TriggerObject` 変数で公開されます。

注文のフォローアップ メールのサンプルスクリプトを次に示します。

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

`$TriggerObject` 変数を使用する利点は、ローカルデータを取り込む使用可能なオブジェクトを決定するためにコードを捧げる必要がないことです。  オブジェクトは、トリガーするアクションによって決定されます。 これは、参照するオブジェクトを選択する最も明確な方法であり、利用可能かつ適切な場合はいつでも使用する必要があります。

注意：`$TriggerObject` を使用する場合、スクリプトでオブジェクトを使用可能にするには、編集ペインでフィールドを選択する必要があります。

メモ 2：この `$TriggerObject` は、「追加された」トリガーに対してのみ機能し、「更新された」トリガーに対しては機能しません。
