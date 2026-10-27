---
title: Marketo Engage MCPの操作
description: AI アシスタントで使用できるMarketo Engage MCPの操作について説明します。
autotag-review: '2026-06-02T13:31:42.084Z'
TQID: 'https://experienceleague.adobe.com/qvrWbHOCsCCHctduNDxMhkE8JAKxZk8FCYfKvzxfcYA'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
    internal-label: Smart Campaigns
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
    internal-label: Forms
  - id: dca84292-69e9-4116-a575-667d31fa060d
    internal-label: APIs
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
    internal-label: Programs
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
source-git-commit: 1cdb28422994b772a0fa430e213facaf26817952
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%
---

# [!DNL Marketo Engage]個のMCP操作

[!DNL Marketo Engage] MCP サーバーは、アセット管理、リードデータ、およびキャンペーンの自動化全体で182の操作をサポートしています。



## サポートされる操作

コネクテッド AI アシスタントを通じて、利用可能な操作を確認できます。

接続で検出ツールが表示される場合は、次のプロンプトを使用します。

* 「Marketo MCP `list_tool_categories` ツールを使用して、使用可能な操作カテゴリを一覧表示します。」
* 「Marketo MCP `search_tools` ツールを使用して、スマートキャンペーンを管理するためのオペレーションを検索します。」

2番目のプロンプトのタスクを必要な操作に置き換えます。 検出ツールが公開されていない場合は、AI アシスタントに、[!DNL Marketo] MCP サーバーから使用可能なツールのリストを表示するように依頼します。

結果には、接続の権限と機能の可用性が反映されます。 これらは、利用可能なMCP ツールを記述するもので、完全な[!DNL Marketo] REST APIではありません。

[!DNL Marketo] クライアント資格情報を使用する接続では、次の機能はサポートされていません。

* SMS ツール
* プッシュ通知ツール
* アプリ内メッセージとアプリ内プログラムツール
* `schedule_smart_campaign`を使用したスマートキャンペーンのスケジュール設定
* ユーザー管理ツールとバルクサービスツール

`schedule_campaign`操作は、クライアントと資格情報の接続でサポートされています。

利用できる操作は、API ユーザーの権限、[!DNL Marketo] インスタンスで有効になっている機能、およびMCP クライアントの制限によって異なります。 データを変更または削除する操作の中には、確認と追加アクセスが必要なものもあります。 カテゴリのサポートは、すべてのREST エンドポイントへのアクセスを意味するものではありません。

接続手順とプロンプトの例については、[MCP サーバー](mcp-server.md#available-operations) ページを参照してください。 [!DNL Marketo] AIおよび[!DNL Marketo Engage] MCP サーバーでのデータの処理方法について詳しくは、[&#x200B; データ情報](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/marketo-ai/data-information) ページを参照してください。