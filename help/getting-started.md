---
title: はじめに
description: Marketo Engage API の概要
exl-id: 78c44c32-4e59-4d55-a45c-ef0d7dac814d
source-git-commit: 490411e411bed7b5b76fd9e5f41ccc9d156b2ba9
workflow-type: ht
source-wordcount: '1340'
ht-degree: 100%

---

# はじめに

Marketo Engage は、マーケターが見込み客やお客様に対してパーソナライズされたマルチチャネルプログラムやキャンペーンを管理できるようにするマーケティングオートメーションプラットフォームです。Marketo Engage プラットフォームでは、統合ポイントを使用して拡張できます。コアエンティティとその関係を以下に示します。

>[!NOTE]
>SOAP API は非推奨（廃止予定）となり、2025年10月31日（PT）以降は使用できなくなります。すべての新規開発は、Marketo [REST API](./rest-api/rest-api.md) を使用して行う必要があり、サービスの中断を回避するために、既存のサービスをその日までに移行する必要があります。SOAP API を使用するサービスがある場合、移行方法について詳しくは、SOAP API [移行ガイド](./soap-api/migration.md)を参照してください。
>

Marketo Engage インスタンスでネイティブ SFDC接続または MS Dynamics CRM 接続が有効になっている場合、会社、商談、商談ロール、セールス担当者のオブジェクトは読み取り専用です

![データモデル](assets/data_model.png)

## ユーザ（リード）

人物は、あらゆるマーケティングオートメーションプラットフォームの基盤です。Marketo 内では、セールスの観点からリード、見込み客、有望客、取引先責任者などとして指定されているかどうかに関係なく、セールス担当者以外のすべてのレコードはリードと呼ばれます。リードオブジェクトには、メール、名、姓など、一連の標準フィールドが用意されています。リードオブジェクトタイプにフィールドを追加して、システム内のレコードに関連付けられている情報のタイプを拡張できます。カスタム属性は、標準フィールドと同様に読み取りおよび書き込みが可能です。フィールドの完全なリストは、Marketo の&#x200B;**[!UICONTROL 管理]**／**[!UICONTROL フィールド管理]**&#x200B;メニューにあります。リードは、Marketo で ID フィールドによって一意に識別されます。その他の一意のキーは、システムの外部から適用する必要があります。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads)、[JavaScript](javascript-api/lead-tracking.md#lead-tracking-api)

## アクティビティ

リードは、いくつかの方法で組織とやり取りします。 リードは、会社の web サイトのページを訪問したり、展示会に参加したり、ホワイトペーパーをダウンロードしたりすることができます。これらの各アクションは Marketo 内で取り込むことができるので、マーケターはリードがどのアクティビティをいつ実行したかをより深く理解し、タイムリーで適切なコミュニケーションを調整できます。アクティビティは常に、leadId によってリードに関連付けられます。

独自のカスタムアクティビティを定義できます。カスタムアクティビティを作成して公開したら、Marketo API 経由でカスタムアクティビティを追加できます。カスタムアクティビティについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-activities/understanding-custom-activities)を参照してください。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities)、[JavaScript](javascript-api/lead-tracking.md#munchkin-behavior)

## プログラムとキャンペーン

プログラムは、マーケターが様々なタイプのマーケティング活動を 1 つの一元的な場所から整理するメカニズムです。プログラムの例として、メールの一括送信があります。リードは、特定のプログラムに関連する複数のアクション／アクティビティを実行し、そのプログラムに関連付けられます。これはリード進行と呼ばれます。メール一括配信プログラムの進行例として、リードにメールが送信された日時、リードがメールを開いた日時、リードがメール内のリンクをクリックしたかどうかなどが記録されます。

キャンペーンは、プログラム内の特定の目的と特定の目標を達成するために作成されます。キャンペーンの例として、リードのグループを絞り込んでメールを一括送信したり、リードがメール一括送信プログラム内のリンクをクリックした場合にセールス担当者にフォローアップを通知したりできます。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns)

## タグ

タグは、レポートの目的でデータをグループ化する方法です。これらの識別子により、データを分類し、プログラムの有効性と ROI を把握するためにプログラムについて報告する方法を定義できます。

Marketo Admin は、Marketo ユーザがプログラムを作成する際に選択できる必須タグタイプとオプションタグタイプを作成できます。これらの各タグタイプに可能な値は、ユーザが定義し、レポートの目的での会社がカスタムタグの使用方法を反映したものです。

例えば、複数のタグ値（北東部、南東部など）を持つカスタムの「地域」タグタイプを作成して、最も多くのリードを生成している地域を分析できます。または、例えば、「所有者」タグタイプを作成して、リードや商談の作成に最も大きな影響を与えているプログラム所有者（Maria、David、John など）を評価して理解できます。タグについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/understanding-tags)を参照してください。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/asset/)

## リスト

リストを使用すると、マーケターはリードのコレクションを整理できます。Marketo 内には、静的リストとスマートリストの 2 つのタイプのリストがあります。静的リストは、マーケターが選択して追加または削除できるリードの固定リストです。スマートリストは、指定された一連の特性に基づいたリードの動的なコレクションです。スマートリストの例として、「当社の web サイトの価格ページを訪問したすべてのリード」があります。このスマートリストは、より多くのリードが価格ページを訪問するにつれて増加し続けます。リストについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/home)を参照してください。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists)

## 商談

マーケターは、リードを商談のフォームでセールスに結びつけます。商談は、潜在的なセールス取引を表し、Marketo のリードまたは取引先責任者と組織に関連付けられます。商談ロールは、特定のリードと組織の間の共通部分です。商談ロールは、組織内のリードの機能に関連しています。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities)

## 会社

組織は、Marketo ではアカウントと呼ばれることもあり、ユーザが所属する組織を指します。Marketo または収益サイクル分析（RCA）で ROI レポートを使用する場合、適切な ROI のアトリビューションを決定できるように、人物を組織および商談に関連付けることが重要です。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies)

## アセット

アセットは、プログラム内で使用されるランディングページ、メール、フォーム、画像を指します。アセットは、特定のプログラムに対してローカルにすることも、グローバルにすることもできます。グローバルアセットは、どのプログラムでも使用できます。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/asset/)

## トークン

トークンを使用すると、マーケターはアセットを使用してメッセージをパーソナライズし、フローアクション内にロジックを追加できます。システム全体、プログラム、リード、会社用のトークンがあります。リードトークンの例は、{{lead.First Name}} です。このトークンをメール内に配置すると、リードの名を表示できます。

プログラムレベルまたはフォルダーレベルで定義されたトークンは、Marketo 内で「マイトークン」と呼ばれます。マイトークンには、ローカル、継承、上書きの 3 つのタイプのいずれかを指定できます。

特定のキャンペーンフォルダーまたはプログラム内でローカルに作成したマイトークンは、その特定のプログラムまたはキャンペーンフォルダーで使用できます（ローカル）。キャンペーンフォルダーレベルで作成したマイトークンは、そのキャンペーンフォルダー内に含まれるすべてのプログラムで使用できます（継承）。プログラムレベルでカスタム値を使用して変更したマイトークンは、プログラムフォルダーレベルのトークンの親マイトークン値を変更しません（上書き）。

マイトークンには、{{my.My Token}} という命名規則を使用し、トークン名の先頭に「my」という単語が追加されます。例えば、EventDate という名前の日付タイプのマイトークンを作成した場合、トークンの名前は {{my.EventDate}} になります。マイトークンについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/tokens/understanding-my-tokens-in-a-program)を参照してください。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens)

## カスタムオブジェクト

Marketo カスタムオブジェクトを使用すると、Marketo リードとカスタムオブジェクトレコードの間に 1 対多または多対多（エッジ-ブリッジ-エッジ）の関係を作成できます。Marketo カスタムオブジェクトを作成して公開すると、Marketo API を通じてカスタムオブジェクトに対して CRUD 操作を実行できます。カスタムオブジェクトについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/home)を参照してください。カスタムオブジェクトに新しいレコードを追加した場合は、スマートリストトリガーを使用して応答できます。また、カスタムオブジェクトデータをスマートリスト（セグメント化）のフィルターとして使用したり、[メールスクリプト](email-scripting.md)を使用してメールでフィルターとして使用したりすることもできます。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects)

## セールス担当者

ネイティブ CRM 統合が有効になっていない場合、セールス担当者のレコードとリードの関係は Marketo で管理できます。これらのレコードには、名前、メール、役職など、セールス担当者に関する基本情報が含まれています。リードがセールス担当者によって所有されている場合に、Marketo でのフィルタリングやトークンに使用できます。セールス担当者との関係は、「externalSalesPersonId」フィールドを通じてリードレベルで管理され、[Sync Leads](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST) API を通じて更新する必要があります。

関連 API：[REST](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Sales-Persons)
