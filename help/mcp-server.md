---
title: MCP Server
description: Learn how to connect an AI assistant to Marketo using the MCP server. Configure Claude Desktop, Cursor, Claude Code, or VS Code with your Marketo credentials.
badgeBeta: label="ベータ版" type="informative" tooltip="This feature is currently in a closed beta release"
exl-id: ab446e56-6250-4af5-b03e-162991d09a5c
source-git-commit: 74f277aa200fa54bc386c067ec3302d144ec250a
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 1%

---

# [!DNL Marketo] MCP Server

>[!NOTE]
>
>The MCP server is currently in a closed beta release. It is not available to all users at this time.

The Model Context Protocol (MCP) is an open standard that enables AI tools to communicate with external services. The [!DNL Marketo] MCP server acts as a bridge between your AI assistant and [!DNL Marketo]. It exposes more than 100 operations across forms, programs, smart campaigns, leads, emails, snippets, lists, and folders.

When your AI tool calls the MCP server, the server executes the corresponding REST API call on your behalf, using the credentials you provide in each request. You do not need to install, deploy, or run any server-side software.

>[!IMPORTANT]
>
>Model Context Protocol （MCP）は新しいオープンソースの標準であり、セキュリティや信頼性に関するリスクが生じる可能性があります。 Adobe MCP サーバーの統合と関連ドキュメントは、いかなる保証も受けることなく、「現状のまま」提供されます。
>Connecting MCP clients or servers to Adobe products is a customer-elected configuration, and customers are responsible for evaluating the security and suitability of any MCP integration. Adobeは、設定ミス、MCPの誤用、サードパーティ実装の脆弱性、またはMCP対応ワークフローを通じて実行された意図しないアクションから生じる問題については責任を負いません。
>To reduce risk, Adobe encourages testing integrations in a sandbox environment prior to productive use and carefully reviewing and validating all MCP-initiated actions and responses before confirming or relying on them.

## 前提条件

- A [!DNL Marketo] instance with REST API access enabled
- Admin access to create API credentials in [!DNL Marketo] LaunchPoint
- One of the following AI tools: Claude Desktop, Cursor, Claude Code (CLI), or VS Code with GitHub Copilot
- Network access to the MCP server URL: `https://marketo-mcp.adobe.io/mcp`

## Get Marketo credentials

You need the following values from your [!DNL Marketo] instance:

- **クライアント ID**
- **クライアント秘密鍵**
- **Munchkin Account ID**

If you already have them, skip to [Configure your AI tool](#configure-your-ai-tool).

### クライアント IDとクライアント秘密鍵

1. **[!UICONTROL 管理者]** > **[!UICONTROL LaunchPoint]**&#x200B;に移動します。
1. API サービスをクリックします。 お持ちでない場合は、**[!UICONTROL New]** > **[!UICONTROL New Service]**&#x200B;を選択し、サービスタイプとして&#x200B;**[!UICONTROL Custom]**&#x200B;を選択して、専用のAPI ユーザーを割り当てます。
1. 「**[!UICONTROL 詳細を表示]**」をクリックし、**[!UICONTROL クライアント ID]**&#x200B;と&#x200B;**[!UICONTROL クライアントシークレット]**&#x200B;の値をコピーします。

### Munchkin アカウント ID

1. **[!UICONTROL 管理者]** > **[!UICONTROL Munchkin]**&#x200B;に移動します。
1. **[!UICONTROL Munchkin アカウント ID]**&#x200B;をコピーします。 形式は`XXX-XXX-XXX`で、インスタンス URLのプレフィックスと一致します。

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
        "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
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
        "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
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
  --header "X-Marketo-Munchkin-Id: YOUR-MUNCHKIN-ID"
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
          "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
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
| &quot;Marketo credentials not provided&quot; | One or more of `X-Marketo-Client-Id`, `X-Marketo-Client-Secret`, or `X-Marketo-Munchkin-Id` is missing. | Verify all four headers are present in your configuration. |
| &quot;Authentication Error&quot; | Your credentials are invalid or expired. | Re-check your Client ID and Client Secret in **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**. |
| &quot;403 Forbidden&quot; | Your Munchkin ID is not on the server allowlist. | Contact your [!DNL Marketo] MCP administrator to add your Munchkin ID. |
| Connection timeout or refused | The MCP server is unreachable from your network. | Confirm you can reach the server URL from your environment. Check VPN requirements if applicable. |
| Tool calls return empty results | The API user lacks permissions for the requested asset type. | Ask your [!DNL Marketo] admin to review the API user role and permissions. |

## よくある質問

+++Is my data secure?

Credentials are transmitted in HTTP headers with each individual request. The server does not store or cache credentials between sessions, and each request is fully isolated.

+++

+++Can multiple people use this at the same time?

はい。 The server is multi-tenant. Each user connects with their own credentials, and requests are isolated from one another.

+++

+++What happens if my access token expires?

When you authenticate using Client ID and Client Secret, the server handles token refresh automatically. You do not need to take any action.

+++

+++何かをインストールまたは実行する必要がありますか？

いいえ、できません。 MCP サーバーはAdobeによってホストされます。 AI ツールを接続するために設定するだけです。

+++

+++API ユーザーに必要な[!DNL Marketo]権限は何ですか？

API ユーザーは、管理するアセットタイプにアクセスする必要があります。 少なくとも、閲覧操作には読み取り専用の役割を割り当て、アセットの作成または変更には読み取り/書き込み役割を割り当てます。 [!DNL Marketo]管理者と協力して、適切な権限を割り当てます。

+++

+++レートの制限は何ですか？

MCP サーバーは、[!DNL Marketo] インスタンスのAPI レート制限を継承します。 専用のAPI ユーザーを使用して、クォータ消費を追跡、管理します。

+++

+++サポートされているAI ツールは何ですか？

Claude Desktop、Cursor、Claude Code （CLI）、VS CodeとGitHub Copilotの連携。 HTTP経由でモデルコンテキストプロトコルをサポートするすべてのAI ツールが機能する必要があります。

+++

+++複数の[!DNL Marketo] インスタンスに接続できますか？

はい。 AI ツールのMCP設定に、それぞれ一意の名前と対応するインスタンスの資格情報を持つ複数のエントリを追加します。 例えば、`marketo-prod`と`marketo-staging`を個別のサーバーとして設定できます。

+++

## セキュリティに関する検討事項

>[!IMPORTANT]
>
>作業に必要な権限のみを持つ[!DNL Marketo]の専用API ユーザーを使用してください。 API アクセスに管理者資格情報を再利用しないでください。

- **リクエストごとの資格情報。** クライアント ID、クライアントシークレット、Munchkin ID、およびREST API エンドポイントは、各リクエストでHTTP ヘッダーで送信されます。 サーバーはそれらを保存またはキャッシュしません。
- **マルチテナント分離。** 各リクエストは、独自の資格情報セットを使用します。 このデータは、他のユーザーのセッションと相互作用しません。
- **Munchkin IDが許可リストに加えるしました。** サーバーは、承認済みの[!DNL Marketo] インスタンスに対するリクエストのみを受け付けます。 権限のないMunchkin IDを使用したリクエストは、403 エラーで拒否されます。
- **資格情報をバージョン管理から除外します。** AI ツールでサポートされている場合は、環境変数の補間（`${MARKETO_CLIENT_SECRET}`）を使用します。そのため、資格情報はリポジトリにコミットされたファイル内のプレーンテキストに保存されません。
