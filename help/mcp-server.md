---
title: Marketo Engage MCP Server
description: Marketo Engage MCP サーバーを使用して、AI アシスタントをMarketoに接続する方法を説明します。 Marketoの資格情報を使用して、Claude Desktop、Cursor、Claude Code、またはVS Codeを設定します。
badgeBeta: label="限定提供" type="informative" tooltip="この機能は、現在、限定ベータ版リリース中です"
exl-id: ab446e56-6250-4af5-b03e-162991d09a5c
autotag-review: '2026-06-02T13:31:15.329Z'
TQID: 'https://experienceleague.adobe.com/PJJm7yv8HmbwMB2fsnfDCXs8zprDJK5Q5z2uiiCJRZI'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
  - id: c2dbad80-0f5c-4d96-a798-2a65f93b8721
  - id: dca84292-69e9-4116-a575-667d31fa060d
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
source-git-commit: bef569a714bfb797bcf8bb82a406ca6df26facb0
workflow-type: tm+mt
source-wordcount: 1433
ht-degree: 1%

---

# [!DNL Marketo Engage] MCP サーバー

>[!AVAILABILITY]
>
> この機能は限定的に利用できます。 アクセスをリクエストするには、[このフォーム &#x200B;](https://forms.cloud.microsoft/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4Y-uSf63sAxCmWyqMJg8eMFUMVZSVExSNDA3T0I4SEcwRDFSVTBGWU01Uy4u&origin=QRCode){target="_blank"}に入力してください。 サブスクリプションのMunchkin IDの準備が整っていることを確認します。

モデルコンテキストプロトコル（MCP）は、AI ツールが外部サービスと通信できるようにするオープンスタンダードです。 [!DNL Marketo] MCP サーバーは、AI アシスタントと[!DNL Marketo]の間のブリッジとして機能します。 フォーム、プログラム、スマートキャンペーン、リード、メール、スニペット、リスト、フォルダーなど、100以上の業務を網羅しています。

AI ツールがMCP サーバーを呼び出すと、サーバーは各リクエストで指定した資格情報を使用して、対応するREST API呼び出しを代わりに実行します。 サーバーサイドソフトウェアをインストールしたり、デプロイしたり、実行したりする必要はありません。

>[!IMPORTANT]
>
>Model Context Protocol （MCP）は新しいオープンソースの標準であり、セキュリティや信頼性に関するリスクが生じる可能性があります。Adobe MCP サーバーの統合と関連ドキュメントは、いかなる保証も受けることなく、「現状のまま」提供されます。
>MCP クライアントまたはサーバーをAdobe製品に接続することは、お客様が選択した設定であり、お客様はMCP統合のセキュリティと適合性を評価する責任があります。Adobeは、設定ミス、MCPの誤用、サードパーティ実装の脆弱性、またはMCP対応ワークフローを通じて実行された意図しないアクションから生じる問題については責任を負いません。
> リスクを軽減するために、Adobeでは、実稼働的に使用する前にサンドボックス環境で統合をテストし、MCPが開始するすべてのアクションと応答を慎重にレビューおよび検証してから、確認または依存することを推奨しています。

## MCPの基本

>MCPは、AI アプリケーションのUSB-C ポートのようなものだと考えてください。 USB-Cがデバイスをさまざまな周辺機器やアクセサリに接続するための標準化された方法を提供するのと同様に、MCPはAI モデルをさまざまなデータソースやツールに接続するための標準化された方法を提供します。 — [&#x200B; モデル コンテキスト プロトコル &#x200B;](https://modelcontextprotocol.io/docs/getting-started/intro){target="_blank"}

MCPでは、AI ツールを複数の外部サービスに同時に接続できます。 例えば、AI アシスタントは次のような能力を備えています。

* ワードプロセッサーに接続して、AIを活用したドキュメント生成を実現
* Blenderなどの3D モデリングアプリに接続してアニメーションを作成する
* After Effectsに接続してビデオを編集

MCPとは、任意のアプリケーションがデータとアクションをAI ツールに公開するために実装できるオープンスタンダードである通信プロトコルです。

## [!DNL Marketo Engage] MCPの機能と機能なし

MCPの範囲を把握することで、AI ツールを導入する前に期待値を設定することができます。

**MCP実行：**

* 標準のREST APIを使用して、[!DNL Marketo]個のデータと機能へのアクセスを提供します
* 各リクエストで指定した資格情報を使用して、API呼び出しを実行します
* 複数の同時ユーザーをサポートし、それぞれが独自の資格情報で接続されています
* OAuth トークンの更新を自動的に処理する – トークンの有効期限を管理する必要はありません
* テナントが分離された環境内で運用できるため、データが他のユーザーのセッションと競合することはありません

**MCPが次の操作を行っていません：**

* AIまたはマシンラーニングモデルを使用、ホスティング、実行します。AI処理はすべて、MCPではなくAI ツールで行われます
* 顧客データを含むあらゆるデータを活用する、または学習する
* 予測、推奨事項、意思決定の生成：意思決定は、AI ツールやユーザーの責任です
* リクエスト間で、資格情報、リクエストデータ、またはセッション状態を保存または保持する
* サーバーサイドソフトウェアのインストール、デプロイ、管理が必要

MCPは、APIの使用状況に応じて、機密性の高いフィールドを含むデータを送信できますが、B2B データは顧客ビジネスデータを含み、PII データは含まれません。

## 前提条件

* REST API アクセスが有効になっている[!DNL Marketo] インスタンス
* [!DNL Marketo] LaunchPointでAPI資格情報を作成するための管理者アクセス
* 次のいずれかのAI ツール：Claude Desktop、Cursor、Claude Code （CLI）、またはVS Code with GitHub Copilot
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

各AI ツールは、異なる場所からMCP サーバー設定を読み取ります。 以下のツールを見つけ、手順に従って[!DNL Marketo] MCP サーバーを追加します。

>[!TIP]
>
>複数の[!DNL Marketo] インスタンスに接続するには、MCP設定内で、対応する資格情報を持つ一意の名前（例：`marketo-prod`と`marketo-staging`）を持つ個別のエントリを個別に追加します。

### Claude Desktop

設定ファイルは`claude_desktop_config.json`です。 次のいずれかの場所から開きます。

* **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
* **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

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

**[!UICONTROL Ctrl+Shift+P]** （またはmacOSの&#x200B;**[!UICONTROL Cmd+Shift+P]**）を押し、**[!UICONTROL MCP: Open User Configuration]**&#x200B;と入力してEnter キーを押します。 `mcp.json`が開きます。 `servers` オブジェクト内の`marketo` エントリを追加します。

```json
{
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
```

>[!NOTE]
>
>セキュリティ上の理由から、資格情報を直接貼り付ける代わりに、環境変数の補間を設定ファイルで使用します。 `${MARKETO_CLIENT_SECRET}`のような構文を使用して変数を参照し、環境に設定できます。 これにより、バージョン管理にコミットされる可能性のあるファイルに、資格情報がプレーンテキストで保存されるのを防ぎます。

## 使用可能な操作

接続が完了したら、AI アシスタントに次のカテゴリにわたる操作を実行するように依頼できます。 API参照でサポートされている操作の一覧については、[&#x200B; サポートされているMCP操作](mcp-server-operations.md)を参照してください。

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

メールアドレスでリードを検索し、リードレコードを作成または更新して、静的リストのメンバーシップを管理できます。

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

フォルダー、チャネル、タグタイプおよびアクティビティタイプを参照して、[!DNL Marketo]設定を理解します。

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
| 「Marketo資格情報が提供されていません」 | `X-Marketo-Client-Id`、`X-Marketo-Client-Secret`または`X-Marketo-Munchkin-Id`のうち1つ以上が見つかりません。 | 4つのヘッダーがすべて設定に存在することを確認します。 |
| 「認証エラー」 | 資格情報が無効または期限切れです。 | **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**&#x200B;でクライアント IDとクライアント シークレットを再確認します。 |
| 「403禁止」 | Munchkin IDがサーバー許可リストにありません。 | Munchkin IDを追加するには、[!DNL Marketo] MCP管理者にお問い合わせください。 |
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
* **資格情報をバージョン管理から除外します。** AI ツールでサポートされている場合は、環境変数の補間（`${MARKETO_CLIENT_SECRET}`）を使用します。そのため、資格情報はリポジトリにコミットされたファイル内のプレーンテキストに保存されません。
