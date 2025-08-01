---
title: メールスクリプト
feature: Email Programs
description: メールスクリプトの概要
exl-id: ff396f8b-80c2-4c87-959e-fb8783c391bf
source-git-commit: 9012135dc7a295c2462574dad1aca2d06a9077ea
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 100%

---

# メールスクリプト

メモ：Velocity テンプレート言語の動作について詳しくは、[Velocity ユーザガイド](https://velocity.apache.org/engine/devel/user-guide.html)を参照することを強くお勧めします。

[Apache Velocity](https://velocity.apache.org/) は、HTML コンテンツのテンプレートとスクリプトのために設計された、Java で作成された言語です。Marketo では、スクリプトトークンを使用することで、メールのコンテキストで使用できます。これにより、商談オブジェクトとカスタムオブジェクトに保存されているデータにアクセスして、メールで動的コンテンツを作成できます。Velocity では、if/else、for、for each を使用した標準的な高レベルの制御フローを提供し、コンテンツの条件付き反復操作を可能にします。正しい敬称を含む挨拶を印刷する簡単な例を以下に示します。

```java
##check if the lead is male
#if(${lead.MarketoSocialGender} == "Male")
    ##if the lead is male, use the salutation 'Mr.'
    #set($greeting = "Dear Mr. ${lead.LastName},")
##check is the lead is female
#elseif(${lead.MarketoSocialGender} == "Female")
    ##if female, use the salutation 'Ms.'
    #set($greeting = "Dear Ms. ${lead.LastName},")
#else
    ##otherwise, use the first name
    #set($greeting = "Dear ${lead.FirstName},")
#end
##print the greeting and some content
${greeting}

    Lorem ipsum dolor sit amet...
```

## 変数

変数には常に「$」というプレフィックスが付き、#set を使用して設定および更新します。

```
#set($variable = "value")
```

値は、動作が異なる複数の様々な参照タイプを通じて取得できます。

```
$variable ##outputs 'value'
$variablename ##outputs '$variablename'
${variable}name ##outputs 'valuename'
```

また、`$` の後に `!` が含まれるクワイエット参照表記もあります。通常、velocity で未定義の参照が検出されると、その参照を表す文字列はそのままになります。クワイエット参照表記では、未定義の参照が検出されても、値は出力されません。

```
##Defined Reference

#set($foo = "bar")
$foo ##outputs "bar"

##Undefined Reference

##normal
$baz ##outputs "$baz"

##quiet
$!baz ##outputs nothing
```

変数の参照方法について詳しくは、[Apache ユーザガイド](https://velocity.apache.org/engine/devel/user-guide.html#formal-reference-notation)を参照してください。

## Velocity ツール

Apache Velocity プロジェクトでは、[Velocity ツール](https://velocity.apache.org/tools/devel/apidocs/overview-summary.html)の使用を通じて機能を使用できます。これらは、単に Java オブジェクトのラッパーで、すべてのスクリプトで使用できるグローバル変数を通じてメソッドを公開します。

- [AlternatorTool](https://velocity.apache.org/tools/devel/apidocs/org/apache/velocity/tools/generic/AlternatorTool.html)
- [ComparisonDateTool](https://velocity.apache.org/tools/devel/apidocs/org/apache/velocity/tools/generic/ComparisonDateTool.html)
- [ConversionTool](https://velocity.apache.org/tools/devel/apidocs/org/apache/velocity/tools/generic/ConversionTool.html)
- [DateTool](https://velocity.apache.org/tools/devel/apidocs/org/apache/velocity/tools/generic/DateTool.html)
- [DisplayTool](https://velocity.apache.org/tools/devel/apidocs/org/apache/velocity/tools/generic/DisplayTool.html)
- [MathTool](https://velocity.apache.org/tools/devel/apidocs/org/apache/velocity/tools/generic/MathTool.html)
- [NumberTool](https://velocity.apache.org/tools/devel/apidocs/org/apache/velocity/tools/generic/NumberTool.html)
- [EscapeTool](https://velocity.apache.org/tools/devel/apidocs/org/apache/velocity/tools/generic/EscapeTool.html)
- [LoopTool](https://velocity.apache.org/tools/devel/apidocs/org/apache/velocity/tools/generic/LoopTool.html)

例えば、`ComparisonDateTool` からのメソッドを使用するには、スクリプトトークンの `$date` 変数からアクセスします。

```
#set($birthday = $convert.parseDate("2015-08-07","yyyy-MM-dd"))
##use whenIs to determine how many days away it is
$date.whenIs($birthday).days ##outputs 1
```

## スクリプトトークンの作成

Velocity スクリプトは、メールスクリプトトークンを使用してメールに組み込まれます。これらは、マーケティングフォルダーまたはプログラムのいずれかのマーケティングアクティビティで作成できます。トークンをメール内で使用するには、そのメールが、トークンを所有しているか、マーケティングフォルダーからトークンを継承しているプログラムの子である必要があります。トークンを作成するには、フォルダーまたはプログラムに移動し、「[!UICONTROL マイトークン]」タブを選択します。右側のメニューから、「メールスクリプト」オプションをトークンリストにドラッグします

![スクリプトトークン](assets/script-token.png)

ここから、トークンの名前を編集し、「[!UICONTROL クリックして編集]」オプションでエディターを開くことができます。

![スクリプトを編集](assets/script-edit.png)

エディターを開くと、スクリプトでアクセス可能なオブジェクト内のすべての変数にアクセスするスクリプトを作成できます。オブジェクトからフィールド参照を取得するには、右側のツリーからスクリプトにドラッグします。

![スクリプトトークンを編集](assets/edit-script-token.png)

## スクリプトの埋め込みとテスト

プログラムマイトークン内でスクリプトを定義したら、Marketo メールエディターを使用して特定のメール内で参照できます。

![メールスクリプト](assets/email-script-marketo-email.png)

Marketo のメールデザイナー内の[!UICONTROL サンプルメールを送信]メールアクションを使用して、スクリプトをテストできます。スクリプトを正しく処理するには、「[!UICONTROL リード]」フィールドで既存のリードを選択し、そのユーザとして実行するする必要があります。`$TriggerObject` を使用してテストする場合は、[!UICONTROL Trigger] パラメーターを使用してトリガーオブジェクトを選択できます。これにより、そのタイプの最後に更新したオブジェクトのデータが `$TriggerObject` 変数として使用されます。

![メールスクリプトをテスト](assets/velocity-test.png)

また、[!UICONTROL メールプレビュー]を使用してスクリプトをテストすることもできます。これを行うには、「**[!UICONTROL 表示形式：リード詳細]**」を選択し、使用可能な静的リストからリードを選択する必要があります。これには、スクリプト実行中に発生した例外を出力するという追加のメリットがあります。

![メールの表示形式](assets/view-as.png)

## 役に立つヒント

特定のメール内のすべてのメールスクリプトトークンの組み合わせた長さは、100,000 バイトを超えることはできません。この制限は、トークン文字列自体の合計長に適用されます（トークンを展開した後の合計長ではありません）。

- メールスクリプトで参照される変数は、スクリプトに使用できる Marketo 内のオブジェクトの 1 つに存在している必要があります。
- ネイティブに統合された CRM から生成され、リードまたは取引先責任者に直接接続された第 1 レベルおよび第 2 レベルのカスタムオブジェクトは参照できますが、第 3 レベルのカスタムオブジェクトは参照できません。カスタムオブジェクトは、リードまたは会社の親にすることはできません
- Marketo カスタムオブジェクトの場合、親子関係を持つ第 2 レベルのカスタムオブジェクトを参照できます。例：`Lead <- Parent <- Child`。エッジ-ブリッジ関係を持つ第 2 レベルのカスタムオブジェクトを参照することはできません。例：`Lead <- Bridge -> Edge`
- リード、取引先責任者またはアカウントに接続されたカスタムオブジェクトは参照できますが、複数のオブジェクトは参照できません。
- カスタムオブジェクトは、単一の接続、リード、取引先責任者またはアカウントを通じてのみ参照できます
- 使用しているフィールドのスクリプトエディターのチェックボックスをオンにする必要があります。オンにしない場合、処理されません
- 各カスタムオブジェクトに対して、ユーザ／取引先責任者ごとの最近更新された 10 個のレコードが実行時に使用可能であり、最新の更新（0 番目）から最も古い更新（9 番目）まで順番に並べられます。[手順に従う](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/email-setup/change-custom-object-retrieval-limits-in-velocity-scripting)ことで、使用可能なレコードの数を増やすことができます。
- メール内に複数のメールスクリプトを含める場合、スクリプトは上から下に向かって実行されます。最初に実行するスクリプトで定義された変数のスコープは、後続のスクリプトでも使用できます。
- ツール参照：[https://velocity.apache.org/tools/2.0/index.html](https://velocity.apache.org/tools/2.0/index.html)
- 改行文字「\n」または「\r\n」を含むトークンに関するメモ。「サンプルを送信」またはバッチキャンペーン経由でメールを送信すると、トークン内の改行文字はスペースに置き換えられます。トリガーキャンペーン経由でメールを送信すると、改行文字はそのままになります。
- URL を適切に解析するには、パス全体を変数として設定してから出力する必要があります。また、変数は URL 参照内に出力しないでください。プロトコル（http://またはhttps://）を含める必要があり、URL の残りの部分とは区別する必要があります。また、URL は、完全な形式のアンカー (<a>) タグの一部にする必要があります。リンクを追跡するためには、スクリプトは完全な形式のアンカータグを出力する必要があります。リンクは、for ループまたは foreach ループ内から出力される場合、追跡されません。

```html
<!-- Correct -->
#set($url = "www.example.com/${object.id}")
<a href="http://${url}">Link Text</a>

<!-- Correct -->
<a href="http://www.example.com/${object.id}">Link Text</a>

<!-- Incorrect -->
<a href="${url}">Link Text</a>

<!-- Incorrect -->
<a href="{{my.link}}">Link Text</a>

<!-- Incorrect -->
<a href="http://{{my.link}}">Link Text</a>
```
