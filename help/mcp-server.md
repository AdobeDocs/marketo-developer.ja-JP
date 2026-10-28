---
title: Marketo Engage MCP サーバー
description: Marketo Engage MCP サーバーを使用して、AI アシスタントをMarketoに接続する方法を説明します。 Marketoの資格情報を使用して、Claude Desktop、Cursor、Claude Code、またはVS Codeを設定します。
exl-id: ab446e56-6250-4af5-b03e-162991d09a5c
autotag-review: '2026-06-02T13:31:15.329Z'
TQID: 'https://experienceleague.adobe.com/PJJm7yv8HmbwMB2fsnfDCXs8zprDJK5Q5z2uiiCJRZI'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
    internal-label: Smart Campaigns
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
    internal-label: Forms
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
    internal-label: Integrations
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
    internal-label: Configuration
  - id: c2dbad80-0f5c-4d96-a798-2a65f93b8721
    internal-label: Assets
  - id: dca84292-69e9-4116-a575-667d31fa060d
    internal-label: APIs
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
    internal-label: Implementation
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
    internal-label: Programs
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
    internal-label: Templates
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
source-git-commit: 1cdb28422994b772a0fa430e213facaf26817952
workflow-type: tm+mt
source-wordcount: '2620'
ht-degree: 3%
---

# [!DNL Marketo Engage] MCP サーバー

モデルコンテキストプロトコル（MCP）は、AI ツールを外部サービスに接続するオープンスタンダードです。 [!DNL Marketo] MCP サーバーは、AI アシスタントを[!DNL Marketo]に接続します。 アセット管理、リードデータ、キャンペーンの自動化など、あらゆる業務をサポートします。 例外と可用性の要件については、[&#x200B; サポートされているMCP操作](mcp-server-operations.md)を参照してください。

AI ツールがMCP サーバーを呼び出すと、サーバーはそのリクエストの資格情報を使用して、対応するREST API呼び出しを実行します。 サーバーサイドソフトウェアをインストール、デプロイ、または実行する必要はありません。

Marketo AIとMarketo Engage MCP サーバーでのデータの処理方法について詳しくは、[Data Information](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/marketo-ai/data-information) ページを参照してください。

>[!IMPORTANT]
>
>Model Context Protocol（MCP）は、新しいオープンソースの標準であり、セキュリティや信頼性に関するリスクが発生する場合があります。 Adobe MCP サーバーの統合および関連ドキュメントは、「現状のまま」でいかなる保証もなく提供されません。
>MCP クライアントまたはサーバーをAdobe製品に接続することは、お客様が選択した設定であり、お客様はMCP統合のセキュリティと適合性を評価する責任があります。 アドビは、設定ミス、MCP の誤用、サードパーティ実装の脆弱性、または MCP 対応ワークフローを通じて実行された意図しないアクションから発生する問題について、一切の責任を負いません。
>リスクを軽減するために、Adobeでは、本番稼働前にサンドボックス環境で統合をテストし、MCPで開始されるすべてのアクションと応答を慎重にレビューおよび検証してから、確認または依存することを推奨しています。

## MCPの基本

>MCPは、AI アプリケーションのUSB-C ポートのようなものだと考えてください。 USB-Cは、デバイスをさまざまな周辺機器やアクセサリーに接続するための標準化された方法を提供し、MCPは、AI モデルをデータソースやツールに接続するための標準化された方法を提供します。 — [&#x200B; モデル コンテキスト プロトコル &#x200B;](https://modelcontextprotocol.io/docs/getting-started/intro){target="_blank"}

MCPでは、AI ツールを複数の外部サービスに同時に接続することができます。 例えば、AI アシスタントは次のことが可能です。

* ワードプロセッサーに接続して、AIを活用したドキュメント生成を実現
* Blenderなどのアニメーションツールに接続して、ビルドのビジュアライゼーションを行います
* Adobe After Effectsに接続してビデオを編集

あらゆるアプリケーションがMCPを実装し、データとアクションをAI ツールに公開できます。

## [!DNL Marketo Engage] MCPの機能と機能なし

MCPの範囲を把握することで、AI ツールを導入する前に期待値を設定することができます。

**MCP実行：**

* 標準のREST APIを使用して、[!DNL Marketo]個のデータと機能へのアクセスを提供します
* 各リクエストで指定した資格情報を使用して、API呼び出しを実行します
* 複数の同時ユーザーをサポートし、それぞれが独自の資格情報で接続されています
* OAuth トークンの自動更新を処理します。 トークンの有効期限を管理する必要はありません
* テナントが分離された環境内で運用できるため、データが他のユーザーのセッションと競合することはありません

**MCPが次の操作を行っていません：**

* AIまたはマシンラーニングモデルを使用、ホスト、実行します。 AIの処理はすべて、MCPではなくAI ツールで行われます
* 顧客データを含むあらゆるデータを活用する、または学習する
* 予測、提案、意思決定の促進： 意思決定は、下流のAI ツールやユーザーの責任です
* リクエスト間で、資格情報、リクエストデータ、またはセッション状態を保存または保持する
* サーバーサイドソフトウェアのインストール、デプロイ、管理が必要

MCPは、APIの使用状況に応じて、機密性の高いフィールドを含むデータを送信できますが、B2B データは顧客ビジネスデータを含み、PII データは含まれません。

## 前提条件

* REST API アクセスが有効になっている[!DNL Marketo] インスタンス
* [!DNL Marketo] LaunchPointでAPI資格情報を作成するための管理者アクセス
* MCP サーバーURLへのネットワーク アクセス：`https://marketo-mcp.adobe.io/mcp`

## Marketo資格情報の取得

[!DNL Marketo] インスタンスには次の値が必要です。

* **クライアント ID**
* **クライアント秘密鍵**
* **Munchkin アカウント ID**

既に使用している場合は、[AI ツールの設定](#configure-your-ai-tool)にスキップします。

### クライアント IDとクライアント秘密鍵

1. **[!UICONTROL 管理者]** > **[!UICONTROL LaunchPoint]**&#x200B;に移動します。
1. API サービスを選択します。 お持ちでない場合は、**[!UICONTROL New]** > **[!UICONTROL New Service]**&#x200B;を選択し、サービスタイプとして&#x200B;**[!UICONTROL Custom]**&#x200B;を選択して、専用のAPI ユーザーを割り当てます。
1. **[!UICONTROL 詳細を表示]**&#x200B;を選択し、**[!UICONTROL クライアント ID]**&#x200B;および&#x200B;**[!UICONTROL クライアント秘密鍵]**&#x200B;の値をコピーします。

### Munchkin アカウント ID

1. **[!UICONTROL 管理者]** > **[!UICONTROL Munchkin]**&#x200B;に移動します。
1. **[!UICONTROL Munchkin アカウント ID]**&#x200B;をコピーします。 形式は`XXX-XXX-XXX`で、インスタンス URLのプレフィックスと一致します。

## AI ツールの設定

ツールによって設定が少し異なります。 この節では、一般的なツールの接続例を示します。

>[!TIP]
>
>複数の[!DNL Marketo] インスタンスに接続するには、MCP設定に一意の名前`marketo-prod`と`marketo-staging`を持つ個別のエントリを追加し、それぞれに対応する資格情報を付けます。

>[!BEGINTABS]

>[!TAB  クラウド デスクトップ ]

### Claude Desktop {#claude-desktop}

Claude Desktopに接続するには、[marketo-mcp-bridge.zip](assets/marketo-mcp-bridge.zip)をダウンロードして解凍します。 `marketo-mcp-bridge.mjs`を既知の場所に配置し、以下の設定でその絶対パスを使用します。

また、サポートされているLTS バージョンのNode.jsがコンピューターにインストールされている必要があります。 ブリッジには追加のnpm パッケージは必要ありません。

1. Claude Desktopを開きます。
1. `claude_desktop_config.json`を開きます。 MacOSでは、ファイルは`~/Library/Application Support/Claude/`にあります。 Windowsでは、`%APPDATA%\Claude\`にあります。 開発者設定メニューのバージョンで、**[!UICONTROL 設定]** > **[!UICONTROL 開発者]** > **[!UICONTROL 設定を編集]**&#x200B;を選択して開きます。
1. 次のエントリを`mcpServers`の下に追加し、既存の設定を保持します。 パスと資格情報のプレースホルダーを値に置き換えます。

```json
{
  "mcpServers": {
    "marketo-mcp": {
      "command": "node",
      "args": ["/path/to/marketo-bridge/marketo-mcp-bridge.mjs"],
      "env": {
        "MARKETO_MCP_PROD_CLIENT_ID": "<your-client-id>",
        "MARKETO_MCP_PROD_CLIENT_SECRET": "<your-client-secret>",
        "MARKETO_MCP_PROD_MUNCHKIN_ID": "<your-munchkin-id>"
      }
    }
  }
}
```

1. Claude Desktopを再起動します。

Claude DesktopでNode.jsが見つからない場合は、`command`の`node`をNode.js実行可能ファイルへの絶対パスに置き換えます。 詳しくは、[&#x200B; ローカル MCP サーバーへの接続](https://modelcontextprotocol.io/docs/develop/connect-local-servers){target="_blank"}を参照してください。

>[!TAB  カーソル ]

### カーソル {#cursor}

ユーザーアカウントの`~/.cursor/mcp.json`の`mcpServers`またはプロジェクトディレクトリの`.cursor/mcp.json`の`marketo` エントリを追加します。 既存のサーバーを保持し、資格情報のプレースホルダーを値に置き換えます。

```json
{
  "mcpServers": {
    "marketo": {
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

カーソルで&#x200B;**[!UICONTROL カスタマイズ]**&#x200B;を開き、サーバーがオンになっていることを確認します。 詳しくは、[&#x200B; カーソル MCP設定](https://cursor.com/docs/context/mcp){target="_blank"}を参照してください。

>[!TAB Claude Code CLI]

### Claude Code （CLI） {#claude-code}

ターミナルで次のコマンドを実行し、資格情報を代入します。

```bash
claude mcp add --transport http marketo \
  https://marketo-mcp.adobe.io/mcp \
  --header "X-Marketo-Client-Id: YOUR-CLIENT-ID" \
  --header "X-Marketo-Client-Secret: YOUR-CLIENT-SECRET" \
  --header "X-Marketo-Munchkin-Id: YOUR-MUNCHKIN-ID"
```

このコマンドは、現在のプロジェクトのサーバーとユーザーアカウントを追加します。 プロジェクト全体で使用できるようにするには、`--scope user`を追加します。 Claude Codeで、`/mcp`を実行して接続を確認します。 詳しくは、[Claude Code MCP configuration](https://code.claude.com/docs/en/mcp){target="_blank"}を参照してください。

>[!TAB OpenAI Codex]

### OpenAI Codex {#codex}

次の項目を`~/.codex/config.toml`に追加し、既存の設定を保持します。

```toml
[mcp_servers.marketo]
url = "https://marketo-mcp.adobe.io/mcp"

[mcp_servers.marketo.env_http_headers]
X-Marketo-Client-Id = "MARKETO_CLIENT_ID"
X-Marketo-Client-Secret = "MARKETO_CLIENT_SECRET"
X-Marketo-Munchkin-Id = "MARKETO_MUNCHKIN_ID"
```

Codexを実行するプロセスの環境で`MARKETO_CLIENT_ID`、`MARKETO_CLIENT_SECRET`および`MARKETO_MUNCHKIN_ID`を設定します。 `env_http_headers`の値は環境変数名で、資格情報ではありません。

新しいCodex セッションを開始し、`/mcp`を実行して接続を確認します。 詳しくは、[Codex MCP設定](https://developers.openai.com/codex/mcp){target="_blank"}を参照してください。

>[!TAB Gemini CLI]

### Gemini CLI

Gemini CLIに[!DNL Marketo Engage] MCP サーバーを追加するには、次の`mcpServers` エントリをプロジェクトディレクトリの`.gemini/settings.json`に追加するか、ユーザーアカウントの`~/.gemini/settings.json`に追加します。 既存の設定を保持し、資格情報のプレースホルダーを値に置き換えます。

```json
{
  "mcpServers": {
    "marketo": {
      "httpUrl": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
        "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
        "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
      }
    }
  }
}
```

または、シェル環境で`MARKETO_CLIENT_ID`、`MARKETO_CLIENT_SECRET`、`MARKETO_MUNCHKIN_ID`を設定し、次のコマンドを実行します。 シェルは、CLIがユーザー設定にヘッダー値を保存する前に変数を展開します。

```bash
gemini mcp add --transport http -s user marketo https://marketo-mcp.adobe.io/mcp \
  -H "X-Marketo-Client-Id: $MARKETO_CLIENT_ID" \
  -H "X-Marketo-Client-Secret: $MARKETO_CLIENT_SECRET" \
  -H "X-Marketo-Munchkin-Id: $MARKETO_MUNCHKIN_ID"
```

セッションを再起動し、`/mcp`を実行して接続を確認します。 詳しくは、[Gemini CLI MCP設定](https://geminicli.com/docs/tools/mcp-server/){target="_blank"}を参照してください。

>[!TAB VS Code with GitHub Copilot]

### VS CodeとGitHub Copilot {#vscode}

最新バージョンのVS Codeには、ポータブルコパイロット設定を使用します。 `~/.copilot/mcp-config.json`の`mcpServers`の下に次のエントリを追加するか、`COPILOT_HOME`を設定した場合は`$COPILOT_HOME/mcp-config.json`を追加します。 既存のサーバーを保存します。

```json
{
  "mcpServers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "X-Marketo-Client-Id": "${MARKETO_CLIENT_ID}",
        "X-Marketo-Client-Secret": "${MARKETO_CLIENT_SECRET}",
        "X-Marketo-Munchkin-Id": "${MARKETO_MUNCHKIN_ID}"
      }
    }
  }
}
```

VS Codeを実行する環境またはサーバーに接続するリモートホストで3つの環境変数を設定します。 新しいCopilot セッションを開始し、サーバーの信頼プロンプトを確認します。

代わりにガイド付き設定を使用するには、**[!UICONTROL MCP: Add Server]**&#x200B;を実行し、**[!UICONTROL HTTP （HTTPまたはServer-Sent Events）]**&#x200B;を選択し、サーバーURLを入力して、**[!UICONTROL Global]** > **[!UICONTROL Copilot Global]**&#x200B;を選択します。 次に、保存した設定にヘッダーを追加します。

古いバージョンでは、**[!UICONTROL MCP: Open User Configuration]**&#x200B;または`.vscode/mcp.json`もサポートされています。 これらのファイルでは、環境変数に`mcpServers`および`${env:MARKETO_CLIENT_ID}`構文ではなく`servers`を使用します。 2つの形式を混在させないでください。 詳細については、[VS Code MCP設定](https://code.visualstudio.com/docs/agents/reference/mcp-configuration){target="_blank"}を参照してください。

>[!TAB  コパイロット スタジオ ]

### Copilot Studio

MCP ツールを追加する前に、エージェントの生成オーケストレーションをオンにします。 カスタムコネクタを使用して、必要な3つの[!DNL Marketo] ヘッダーをすべて定義します。

エージェントの&#x200B;**[!UICONTROL ツール]** ページで、**[!UICONTROL ツールの追加]** > **[!UICONTROL 新しいツール]** > **[!UICONTROL カスタムコネクタ]**&#x200B;を選択します。 Power Appsで、カスタムコネクタを作成し、**[!UICONTROL Swagger エディター]**&#x200B;を使用して次の定義を入力します。

```yaml
swagger: '2.0'
info:
  title: Marketo MCP Server
  description: Connect to the Marketo MCP server.
  version: 1.0.0
host: marketo-mcp.adobe.io
basePath: /
schemes:
  - https
paths:
  /mcp:
    post:
      summary: Marketo MCP Server
      description: Invoke the Marketo MCP server.
      operationId: InvokeServer
      x-ms-agentic-protocol: mcp-streamable-1.0
      parameters:
        - name: X-Marketo-Client-Id
          in: header
          description: Client ID.
          type: string
          required: true
        - name: X-Marketo-Client-Secret
          in: header
          description: Client secret.
          type: string
          required: true
        - name: X-Marketo-Munchkin-Id
          in: header
          description: Munchkin ID.
          type: string
          required: true
      responses:
        '200':
          description: Immediate Response
securityDefinitions: {}
security: []
```

コネクタを保存または更新し、Copilot Studioに戻ってエージェントに追加します。 接続を作成し、プロンプトが表示されたら3つのヘッダー値を入力します。 資格情報をOpenAPI定義およびエージェントの命令から除外します。 詳しくは、[既存のMCP サーバーへのエージェントの接続](https://learn.microsoft.com/en-us/microsoft-copilot-studio/mcp-add-existing-server-to-agent){target="_blank"}を参照してください。

>[!TAB  グリアン ]

### Glean {#glean}

Gleanを[!DNL Marketo Engage] MCP サーバーに接続するには、[Gleanのリモート MCP設定手順](https://docs.glean.com/administration/tools/connect-remote-mcp-servers-to-glean){target="_blank"}に従って`https://marketo-mcp.adobe.io/mcp`を追加します。 最初に&#x200B;**[!UICONTROL コネクタ]** カタログを確認してください。 カスタムサーバーまたは非公開サーバーの場合は、**[!UICONTROL Admin Console]** > **[!UICONTROL Platform]** > **[!UICONTROL ツール]** > **[!UICONTROL MCP サーバーからツールを読み込む]**&#x200B;を使用します。

[Glean サポートチームは、以下のカスタムヘッダー](https://docs.glean.com/administration/tools/mcp-custom-headers){target="_blank"}を設定する必要があります。 サポートリクエストにサーバー名、URL、必要なヘッダー名を含め、資格情報の値の安全な処理を調整します。 標準のAPI キー接続だけでは、3つのヘッダーすべてを提供することはできません。

| ヘッダー | 値 |
| ------ | ----- |
| `X-Marketo-Client-Id` | クライアント ID |
| `X-Marketo-Client-Secret` | クライアント秘密鍵 |
| `X-Marketo-Munchkin-Id` | Munchkin アカウント ID |

Gleanがヘッダーがアクティブであることを確認したら、他のユーザーがツールを使用できるようにする前に、読み取り専用リクエストで接続をテストします。

>[!TAB その他のツール ]

### 他社製品 {#other-tools}

Adobeは[!DNL Marketo] MCP サーバーをホストし、パブリック URLで公開します。 ストリーミング可能なHTTP トランスポート経由でリモートサーバーをサポートするMCP クライアントは、接続できます。
直接リモート HTTP接続をサポートするクライアントには、ブリッジやローカルにインストールされたサーバーソフトウェアは必要ありません。 お使いのツールが上記に記載されていない場合は、以下の接続の詳細を使用して手動で設定します。

**接続の詳細：**

| 設定 | 値 |
| ------- | ----- |
| 運輸 | HTTP （ストリーミング可能なHTTP） |
| サーバーURL | `https://marketo-mcp.adobe.io/mcp` |

**認証ヘッダー：**

各リクエストで3つのヘッダーをすべて送信します。 サーバーのURLとヘッダーを入力する場所は、ツールによって異なりますので、そのMCP ドキュメントを参照してください。

| ヘッダー | 値 |
| ------ | ----- |
| `X-Marketo-Client-Id` | クライアント ID |
| `X-Marketo-Client-Secret` | クライアント秘密鍵 |
| `X-Marketo-Munchkin-Id` | Munchkin アカウント ID |

ツールがJSON設定を受け入れる場合は、[&#x200B; カーソル &#x200B;](#cursor)または[VS コード &#x200B;](#vscode)の例から始め、ツールのスキーマに合わせてキーと環境変数の構文を調整します。

>[!ENDTABS]

接続後、AI アシスタントに[!DNL Marketo] MCP サーバーを使用して、データを変更することなく利用可能なチャネルを一覧表示するように依頼します。 ツール呼び出しとその応答を調べて、リクエストが意図したサーバーを使用し、接続または認証エラーなしでデータを返すことを確認します。

## 使用可能な操作

接続が完了したら、AI アシスタントに次のカテゴリにわたる操作を実行するように依頼できます。 例外と可用性の要件については、[&#x200B; サポートされているMCP操作](mcp-server-operations.md)を参照してください。

### フォーム

フォームの参照、作成、複製、承認ができます。 フィールドの追加または削除、フィールドの表示ルールの設定、フォームの埋め込み先の特定を行います。

プロンプトの例：

* 「承認済みのすべてのフォームを表示」
* 「問い合わせフォームをQ2 キャンペーンフォルダーに複製」
* 「デモリクエストフォームに会社フィールドを追加」

### スマートキャンペーン

スマートキャンペーンの作成、スマートリストフィルターの設定、フローステップの追加、キャンペーンのアクティブ化または非アクティブ化を行うことができます。

プロンプトの例：

* 「現在アクティブなスマートキャンペーンはどれですか？」
* 「操作フォルダーのリードスコアリングアップデートと呼ばれる新しいスマートキャンペーンの作成」
* 「ウェルカムメールキャンペーンのフローステップを表示する」

### リードとリスト

メールアドレスでリードを検索し、リードレコードを作成し、静的リストのメンバーシップを管理します。

プロンプトの例：

* 「電子メールでリードを探すjane@example.com」
* 「第2四半期MQL リストにリード ID12345を追加」
* 「サマーイベント参加者」という新しい静的リストの作成

### プログラム

プログラムの作成、複製、タグ付けをおこなえます。 タイプ、チャネル、日付範囲ごとにプログラムを参照できます。

プロンプトの例：

* 「Q4 ウェビナープログラムを2026年イベントフォルダーに複製」
* 「Campaigns フォルダーのサマーセールという新しいメールプログラムを作成する」
* 「ウェビナーとしてタグ付けされたすべてのプログラムを表示する」

### メールとスニペット

メールの閲覧、テンプレートからのメール作成、コンテンツセクションの更新、再利用可能なスニペットの管理などをおこなえます。

プロンプトの例：

* 「すべての下書きメールを表示」
* 「ウェルカムメールのヘッダーセクションの更新」
* 「どのようなアセットがホリデープロモーションスニペットを使用しますか？」

### インスタンス構造

[!DNL Marketo]の設定を理解するには、フォルダー、チャネル、タグタイプ、アクティビティタイプを参照します。

プロンプトの例：

* 「Marketoのすべてのフォルダーを一覧表示」
* 「使用可能なすべてのチャネルを表示」
* 「設定されているタグタイプは何ですか？」

### 一括操作

リードデータを一括エクスポートし、ジョブステータスのインポートまたはエクスポートをチェックします。

プロンプトの例：

* 「過去30日間に作成されたリードの一括書き出しを作成」
* 「書き出しジョブ xxのステータスを確認」

## トラブルシューティング

| エラー | 原因 | 修正 |
| ------- | ------- | ----- |
| 「Marketo資格情報が提供されていません」 | `X-Marketo-Client-Id`、`X-Marketo-Client-Secret`または`X-Marketo-Munchkin-Id`のうち1つ以上が見つかりません。 | すべてのMarketo クライアント資格情報ヘッダーが設定に存在することを確認します。 |
| 「401 Unauthorized」 | 資格情報が見つからないか、無効であるか、有効期限が切れています。 Marketo クライアント資格情報を使用すると、クライアント IDまたはクライアントシークレットが正しくありません。 IMS トークンを使用すると、トークンが無効または期限切れになります。 | 認証方法の資格情報を確認します。 クライアント資格情報については、**[!UICONTROL 管理者]** > **[!UICONTROL LaunchPoint]**&#x200B;の&#x200B;**[!UICONTROL クライアント ID]**&#x200B;と&#x200B;**[!UICONTROL クライアントシークレット]**&#x200B;を再確認してください。 IMS トークンの場合は、新しいトークンを生成し、`Authorization` ヘッダーを更新します。 |
| 「403禁止」 | 資格情報は有効ですが、[!DNL Marketo] インスタンスでMCP アクセスが有効になっていません。 | Munchkin アカウント IDのMCP アクセスを有効にするには、[!DNL Marketo] MCP管理者にお問い合わせください。 |
| 「リクエストが多すぎます」（レート制限） | 短時間に送信したリクエストが多すぎるか、同時に送信したリクエストが多すぎるため、[!DNL Marketo] インスタンスのAPI制限に達しました。 | 一度に送信するリクエストの数と頻度を減らし、再試行するまでに少し待ちます。 専用のAPI ユーザーを使用して、割り当て量を追跡、管理します。 |
| 接続がタイムアウトしたか、拒否されました | MCP サーバーにネットワークからアクセスできません。 | お使いの環境からサーバーのURLにアクセスできることを確認します。 該当する場合は、VPNの要件を確認します。 |
| ツール呼び出しは空の結果を返します | API ユーザーには、リクエストされたアセットタイプに対する権限がありません。 | [!DNL Marketo]管理者にAPI ユーザーの役割と権限の確認を依頼します。 |

## セキュリティに関する検討事項

>[!IMPORTANT]
>
>作業に必要な権限のみを持つ[!DNL Marketo]の専用API ユーザーを使用してください。 API アクセスに管理者資格情報を再利用しないでください。

* **リクエストごとの資格情報。** クライアント ID、クライアントシークレット、Munchkin ID、およびREST API エンドポイントは、各リクエストでHTTP ヘッダーで送信されます。 サーバーはそれらを保存またはキャッシュしません。
* **マルチテナント分離。** 各リクエストは、独自の資格情報セットを使用します。 このデータは、他のユーザーのセッションと相互作用しません。
* **Munchkin IDが許可リストに加えるしました。** サーバーは、承認済みの[!DNL Marketo] インスタンスに対するリクエストのみを受け付けます。 権限のないMunchkin IDを使用したリクエストは、403 エラーで拒否されます。
* **API レート制限。** MCP サーバーは、[!DNL Marketo] インスタンスのAPI レート制限を継承します。 専用のAPI ユーザーを使用して、クォータ消費を追跡、管理します。
* **資格情報をバージョン管理から除外します。** AI ツールでサポートされている場合は、環境変数の補間（`${MARKETO_CLIENT_SECRET}`）を使用します。そのため、資格情報はリポジトリーファイルのプレーンテキストに保存されません。

## ガバナンスとデータ保持

### 資格情報の処理

* 顧客資格情報はサーバーサイドで永続化されず、リクエストごとにクライアントから提供されるため、サービス内での資格情報公開を制限するのに役立ちます。

### API インタラクションモデル

* エージェントの使用：エージェントは、サポートされているMarketo APIを呼び出すためにMCP Serverを使用できます。
* 認証モデルの調整：サービスは、Marketo APIに関して文書化されているのと同じ外部API認証モデルを使用します。

### 認証と認証

* 最小権限：効果的な権限は、お客様のLaunchPoint サービスに割り当てられたMarketo APIのみのユーザーから継承され、お客様のMarketo設定内で最小権限の管理が可能になります。
* サーバーサイドトークンの永続性なし：サービスは、引き続き、顧客資格情報またはトークンのサーバーサイドの保存を回避します。  

### ログと監視

* セキュリティログ：構造化されたJSON ログは、コンプライアンス要件をサポートする機密データマスキングと追加のフィルタリングを使用して、Fluent Bitを介してSplunkにルーティングされます。
* 監査サポート：これらの制御は、サービスの可用性、セキュリティ関連イベント、運用品質の継続的な監視をサポートします。
* サーバーサイドの秘密鍵ストレージなし：お客様の資格情報はMCP デプロイメントによって保存されないため、リクエストごとにクライアントから提供する必要があります。
* トークンの処理：アクセストークンは短期間有効で、トークン応答はストアなしでマークされ、トークンはクエリ文字列送信ではなく標準的な認証メカニズムを通じて受け入れられます。
* ロールベースの運用アクセス：管理デプロイメントアクセスは、Adobe インフラストラクチャのロールとグループベースの制御によって管理されますが、データプレーンの権限はお客様のMarketo API ユーザー設定から継承されます。
* 監査とオブザーバビリティ：セキュリティログ、マスキング、モニタリング、アラート機能が有効になっており、調査、サービスの健全性の追跡、運用上の監視に対応できます。
