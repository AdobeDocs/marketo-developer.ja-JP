---
title: EXL プレビューテスト
description: 拡張機能のプレビューをテストするためのAdobe EXL マークダウン構文の例。
source-git-commit: 87d2584ed0ef2c1fa219f2a3ad120c91dc5491e0
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 13%

---


# EXL プレビューテスト

## アラートブロック

>[!NOTE]
>
>これはメモです。 読者が認識すべき補足情報については、メモを使用してください。

>[!TIP]
>
>これはヒントです。 オプションだが役に立つ情報についてはヒントを使う。

>[!IMPORTANT]
>
>これは重要な警告です。 読者が見落としてはいけない情報に使用してください。

>[!WARNING]
>
>これは警告です。 潜在的な問題に関する情報を使用します。

>[!CAUTION]
>
>これは注意すべき点です。 潜在的なリスクに関する情報の活用：

>[!ADMIN]
>
>これは管理者アラートです。 管理者のみのコンテンツ。

>[!AVAILABILITY]
>
>これは可用性に関するメモです。 機能の可用性の詳細。

>[!PREREQUISITES]
>
>これは前提条件のブロックです。 始める前に読者が必要としているものをリストします。

## シェードボックス

>[!BEGINSHADEBOX &quot;オプションのタイトル&quot;]

このコンテンツは灰色の背景で表示されます。 シェードボックスを使用して、関連コンテンツを視覚的にグループ化します。

リストを含めることができます。

- 項目1
- 2つ目
- 3つ目

>[!ENDSHADEBOX]

>[!BEGINSHADEBOX]

タイトルのないシェードボックス。

>[!ENDSHADEBOX]

## 折りたたみ可能なセクション

+++クリックして展開：基本的な例

このコンテンツは、ユーザーがタイトルを選択するまで非表示になります。

コードブロックを含め、任意のコンテンツをここに含めることができます。

```javascript
const example = 'hello world';
console.log(example);
```

+++

+++高度な設定

オプションまたは詳細なコンテンツには、折りたたみ可能なセクションを使用します。このセクションを使用しないと、メインフローが混乱します。

| 設定 | 値 | 説明 |
| --- | --- | --- |
| timeout | 30 | リクエストがタイムアウトするまでの秒数 |
| 再試行 | 3 | 再試行回数 |

{style="table-layout:auto"}

+++

## コンテキストヘルプ

コンテキストヘルプはプレビューから非表示になっています。 見て！
>[!CONTEXTUALHELP]
>id="models_insights_undefinedchannels"
>title="未定義のチャネル"
>abstract="未定義のチャネルが含まれますが、起因するコンバージョンはありません。"

## 埋め込みビデオ

>[!VIDEO](https://video.tv.adobe.com/v/3427028/?quality=12&learn=on)

## ローカリゼーションマクロ

製品名がローカライズされないように、[!DNL Marketo]を使用して製品名を折り返します。

UI要素ラベルには、**[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**&#x200B;を使用します。

組み合わせた例：[!DNL Adobe Analytics]で、**[!UICONTROL Workspace]** > **[!UICONTROL プロジェクトを作成]**&#x200B;を選択します。

## バッジ

[!BADGE Beta]{type=Informative}

[!BADGE 一般提供]{type=Positive}

[!BADGE 非推奨（廃止予定）]{type=Negative}

[!BADGE 実験]{type=Caution}

## タブ

>[!BEGINTABS]

>[!TAB 要件]

>[!IMPORTANT]
>
>このタスクを完了するには、管理者権限が必要です。

必須フィールド：

| フィールド | タイプ | 必須 |
| --- | --- | --- |
| 名前 | 文字列 | ○ |
| メール | 文字列 | ○ |
| 役割 | 列挙 | いいえ |

>[!TAB 手順]

1. Admin Consoleを開きます。
1. **[!UICONTROL Users]** > **[!UICONTROL Add user]**&#x200B;を選択します。
1. 必須のフィールドに入力します。
1. 「**[!UICONTROL 保存]**」を選択します。

>[!NOTE]
>
>変更はすぐに有効になります。

>[!TAB 結果]

新規ユーザーには、パスワードを設定するためのリンク付きのウェルカムメールが届きます。

- リンクは24時間後に有効期限が切れます。
- ユーザーは、ログインページから新しいリンクをリクエストできます。

>[!ENDTABS]

## コードブロック

```json
{
  "name": "example",
  "version": "1.0.0",
  "enabled": true
}
```

```javascript
function greet(name) {
  return `Hello, ${name}!`;
}
```

## テーブル

| 列1 | 列2 | コラム 3 |
| --- | --- | --- |
| [!UICONTROL 行1]、セル 1 | 行1、セル 2 | [!DNL Row 1, cell 3] |
| 行2、セル 1 | 行2、セル 2 | 行2、セル 3 |

