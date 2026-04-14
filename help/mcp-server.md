---
title: MCP サーバー
description: MCP サーバーを使用してAI アシスタントをMarketoに接続する方法を説明します。 Marketoの資格情報を使用して、Claude Desktop、Cursor、Claude Code、またはVS Codeを設定します。
hidefromtoc: true
source-git-commit: a9946d79bfc4cabd27fe33d95f25ee99d777fb1b
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 1%

---


# [!DNL Marketo] MCP サーバー

モデルコンテキストプロトコル（MCP）は、AI ツールが外部サービスと通信できるようにするオープンスタンダードです。 [!DNL Marketo] MCP サーバーは、AI アシスタントと[!DNL Marketo]の間のブリッジとして機能します。 フォーム、プログラム、スマートキャンペーン、リード、メール、スニペット、リスト、フォルダーなど、100以上の業務を網羅しています。

AI ツールがMCP サーバーを呼び出すと、サーバーは各リクエストで指定した資格情報を使用して、対応するREST API呼び出しを代わりに実行します。 サーバーサイドソフトウェアをインストールしたり、デプロイしたり、実行したりする必要はありません。

## 前提条件

- REST API アクセスが有効になっている[!DNL Marketo] インスタンス
- [!DNL Marketo] LaunchPointでAPI資格情報を作成するための管理者アクセス
- 次のいずれかのAI ツール：Claude Desktop、Cursor、Claude Code （CLI）、またはVS Code with GitHub Copilot
- MCP サーバーURLへのネットワーク アクセス：`https://marketo-mcp.adobe.io/mcp`

## Marketo資格情報の取得

[!DNL Marketo] インスタンスには次の値が必要です。

- **クライアント ID**
- **クライアント秘密鍵**
- **Munchkin アカウント ID**
- **REST API エンドポイント**

既に使用している場合は、[AI ツールの設定](#configure-your-ai-tool)にスキップします。

### クライアント IDとクライアント秘密鍵

1. **[!UICONTROL 管理者]** > **[!UICONTROL LaunchPoint]**&#x200B;に移動します。
1. API サービスをクリックします。 お持ちでない場合は、**[!UICONTROL New]** > **[!UICONTROL New Service]**&#x200B;を選択し、サービスタイプとして&#x200B;**[!UICONTROL Custom]**&#x200B;を選択して、専用のAPI ユーザーを割り当てます。
1. 「**[!UICONTROL 詳細を表示]**」をクリックし、**[!UICONTROL クライアント ID]**&#x200B;と&#x200B;**[!UICONTROL クライアントシークレット]**&#x200B;の値をコピーします。

### Munchkin アカウント ID

1. **[!UICONTROL 管理者]** > **[!UICONTROL Munchkin]**&#x200B;に移動します。
1. **[!UICONTROL Munchkin アカウント ID]**&#x200B;をコピーします。 形式は`XXX-XXX-XXX`で、インスタンス URLのプレフィックスと一致します。

### REST API エンドポイント

1. **[!UICONTROL 管理者]** > **[!UICONTROL Web サービス]**&#x200B;に移動します。
1. **[!UICONTROL REST API]**&#x200B;で、**[!UICONTROL エンドポイント]**&#x200B;のURLをコピーします。 形式は`https://XXX-XXX-XXX.mktorest.com`です。

## AI ツールの設定

各AI ツールは、異なる場所からMCP サーバー設定を読み取ります。 以下のツールを見つけ、手順に従って[!DNL Marketo] MCP サーバーを追加します。

### Claude Desktop

設定ファイルは`claude_desktop_config.json`です。 次のいずれかの場所から開きます。

- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

ファイルに他のMCP サーバーが既に含まれている場合は、`mcpServers`の下に`marketo` エントリを追加します。 次の例は、完全な`mcpServers` ブロックを示しています。

```json
{
  "mcpServers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
        "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
        "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID",
        "X-Marketo-Endpoint": "YOUR-REST-API-ENDPOINT"
      }
    }
  }
}
```

ファイルを保存し、Claude Desktopを終了して再度開きます。

### カーソル

カーソル MCP設定に既に他のサーバーが含まれている場合は、`mcpServers`の下に`marketo` エントリを追加します。 次の例は、プロジェクトディレクトリの&#x200B;**[!UICONTROL Settings]** > **[!UICONTROL MCP]**&#x200B;または`.cursor/mcp.json`の完全な`mcpServers` ブロックを示しています。

```json
{
  "mcpServers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
        "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
        "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID",
        "X-Marketo-Endpoint": "YOUR-REST-API-ENDPOINT"
      }
    }
  }
}
```

カーソルを再起動します。

### Claude Code （CLI）

ターミナルで次のコマンドを実行し、資格情報を代入します。

```bash
claude mcp add --transport http marketo \
  https://marketo-mcp.adobe.io/mcp \
  --header "X-Marketo-Client-Id: YOUR-CLIENT-ID" \
  --header "X-Marketo-Client-Secret: YOUR-CLIENT-SECRET" \
  --header "X-Marketo-Munchkin-Id: YOUR-MUNCHKIN-ID" \
  --header "X-Marketo-Endpoint: YOUR-REST-API-ENDPOINT"
```

### VS CodeとGitHub Copilot

MacOSで&#x200B;**[!UICONTROL Ctrl+Shift+P]**&#x200B;または&#x200B;**[!UICONTROL Cmd+Shift+P]**&#x200B;を押し、**[!UICONTROL Preferences: Open User Settings （JSON）]**&#x200B;を選択して、VS Code `settings.json`を開きます。 次の例を追加します。

```json
{
  "mcp": {
    "servers": {
      "marketo": {
        "type": "http",
        "url": "https://marketo-mcp.adobe.io/mcp",
        "headers": {
          "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
          "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
          "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID",
          "X-Marketo-Endpoint": "YOUR-REST-API-ENDPOINT"
        }
      }
    }
  }
}
```

**[!UICONTROL Ctrl+Shift+P]** （またはmacOSの&#x200B;**[!UICONTROL Cmd+Shift+P]**）を押し、**[!UICONTROL ウィンドウをリロード]**&#x200B;と入力してEnter キーを押します。

>[!NOTE]
>
>セキュリティ上の理由から、資格情報を直接貼り付ける代わりに、環境変数の補間を設定ファイルで使用します。 `${MARKETO_CLIENT_SECRET}`のような構文を使用して変数を参照し、環境に設定できます。 これにより、バージョン管理にコミットされる可能性のあるファイルに、資格情報がプレーンテキストで保存されるのを防ぎます。

## 使用可能な操作

接続が完了したら、AI アシスタントに次のカテゴリにわたる操作を実行するように依頼できます。

### フォーム

フォームの参照、作成、複製、承認ができます。 フィールドの追加または削除、フィールドの表示ルールの設定、フォームの埋め込み先の特定を行います。

プロンプトの例：

- 「承認済みのすべてのフォームを表示」
- 「問い合わせフォームをQ2 キャンペーンフォルダーに複製」
- 「デモリクエストフォームに会社フィールドを追加」

### スマートキャンペーン

スマートキャンペーンの作成、スマートリストフィルターの設定、フローステップの追加、キャンペーンのアクティブ化または非アクティブ化を行うことができます。

プロンプトの例：

- 「現在アクティブなスマートキャンペーンはどれですか？」
- 「操作フォルダーのリードスコアリングアップデートと呼ばれる新しいスマートキャンペーンの作成」
- 「ウェルカムメールキャンペーンのフローステップを表示する」

### リードとリスト

メールアドレスでリードを検索し、リードレコードを作成または更新して、静的リストのメンバーシップを管理できます。

プロンプトの例：

- 「電子メールでリードを探すjane@example.com」
- 「第2四半期MQL リストにリード ID12345を追加」
- 「サマーイベント参加者」という新しい静的リストの作成

### プログラム

プログラムの作成、複製、タグ付けをおこなえます。 タイプ、チャネル、日付範囲ごとにプログラムを参照できます。

プロンプトの例：

- 「Q4 ウェビナープログラムを2026年イベントフォルダーに複製」
- 「Campaigns フォルダーのサマーセールという新しいメールプログラムを作成する」
- 「ウェビナーとしてタグ付けされたすべてのプログラムを表示する」

### メールとスニペット

メールの閲覧、テンプレートからのメール作成、コンテンツセクションの更新、再利用可能なスニペットの管理などをおこなえます。

プロンプトの例：

- 「すべての下書きメールを表示」
- 「ウェルカムメールのヘッダーセクションの更新」
- 「どのようなアセットがホリデープロモーションスニペットを使用しますか？」

### インスタンス構造

フォルダー、チャネル、タグタイプおよびアクティビティタイプを参照して、[!DNL Marketo]設定を理解します。

プロンプトの例：

- 「Marketoのすべてのフォルダーを一覧表示」
- 「使用可能なすべてのチャネルを表示」
- 「設定されているタグタイプは何ですか？」

### 一括操作

リードデータを一括エクスポートし、ジョブステータスのインポートまたはエクスポートをチェックします。

プロンプトの例：

- 「過去30日間に作成されたリードの一括書き出しを作成」
- 「書き出しジョブ xxのステータスを確認」

## トラブルシューティング

| エラー | 原因 | 修正 |
| ------- | ------- | ----- |
| 「Marketo エンドポイントが提供されていません」 | 設定に`X-Marketo-Endpoint` ヘッダーがありません。 | MCP設定を再確認し、4つのヘッダーがすべて存在することを確認します。 |
| 「Marketo資格情報が提供されていません」 | `X-Marketo-Client-Id`、`X-Marketo-Client-Secret`または`X-Marketo-Munchkin-Id`のうち1つ以上が見つかりません。 | 4つのヘッダーがすべて設定に存在することを確認します。 |
| 「認証エラー」 | 資格情報が無効または期限切れです。 | **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**&#x200B;でクライアント IDとクライアント シークレットを再確認します。 |
| 「403禁止」 | Munchkin IDがサーバー許可リストにありません。 | Munchkin IDを追加するには、[!DNL Marketo] MCP管理者にお問い合わせください。 |
| 接続がタイムアウトしたか、拒否されました | MCP サーバーにネットワークからアクセスできません。 | お使いの環境からサーバーのURLにアクセスできることを確認します。 該当する場合は、VPNの要件を確認します。 |
| ツール呼び出しは空の結果を返します | API ユーザーには、リクエストされたアセットタイプに対する権限がありません。 | [!DNL Marketo]管理者にAPI ユーザーの役割と権限の確認を依頼します。 |

## よくある質問

### 自分のデータは安全か？

認証情報は、個々のリクエストごとにHTTP ヘッダーで送信されます。 サーバーはセッション間で資格情報を保存またはキャッシュせず、各リクエストは完全に分離されます。

### 複数の人が同時に使用できますか？

はい。 サーバーはマルチテナントです。 各ユーザーは自分の資格情報に接続し、リクエストは互いに分離されます。

### アクセストークンの有効期限が切れた場合はどうなりますか？

クライアント IDとクライアントシークレットを使用して認証を行うと、サーバーはトークンの更新を自動的に処理します。 アクションを起こす必要はありません。

### 何かをインストールまたは実行する必要がありますか？

いいえ、できません。 MCP サーバーはAdobeによってホストされます。 AI ツールを接続するために設定するだけです。

### API ユーザーに必要な[!DNL Marketo]権限は何ですか？

API ユーザーは、管理するアセットタイプにアクセスする必要があります。 少なくとも、閲覧操作には読み取り専用の役割を割り当て、アセットの作成または変更には読み取り/書き込み役割を割り当てます。 [!DNL Marketo]管理者と協力して、適切な権限を割り当てます。

### レートの制限は何ですか？

MCP サーバーは、Marketo インスタンスのAPI レート制限を継承します。 専用のAPI ユーザーを使用して、クォータ消費を追跡、管理します。

### サポートされているAI ツールは何ですか？

Claude Desktop、Cursor、Claude Code （CLI）、VS CodeとGitHub Copilotの連携。 HTTP経由でモデルコンテキストプロトコルをサポートするすべてのAI ツールが機能する必要があります。

### 複数の[!DNL Marketo] インスタンスに接続できますか？

はい。 AI ツールのMCP設定に、それぞれ一意の名前と対応するインスタンスの資格情報を持つ複数のエントリを追加します。 例えば、`marketo-prod`と`marketo-staging`を個別のサーバーとして設定できます。

## セキュリティに関する検討事項

>[!IMPORTANT]
>
>作業に必要な権限のみを持つ[!DNL Marketo]の専用API ユーザーを使用してください。 API アクセスに管理者資格情報を再利用しないでください。

- **リクエストごとの資格情報。** クライアント ID、クライアントシークレット、Munchkin ID、およびREST API エンドポイントは、各リクエストでHTTP ヘッダーで送信されます。 サーバーはそれらを保存またはキャッシュしません。
- **マルチテナント分離。** 各リクエストは、独自の資格情報セットを使用します。 このデータは、他のユーザーのセッションと相互作用しません。
- **Munchkin IDが許可リストに加えるしました。** サーバーは、承認済みの[!DNL Marketo] インスタンスに対するリクエストのみを受け付けます。 権限のないMunchkin IDを使用したリクエストは、403 エラーで拒否されます。
- **資格情報をバージョン管理から除外します。** AI ツールでサポートされている場合は、環境変数の補間（`${MARKETO_CLIENT_SECRET}`）を使用します。そのため、資格情報はリポジトリにコミットされたファイル内のプレーンテキストに保存されません。
