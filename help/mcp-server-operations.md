---
title: Marketo Engage MCPの操作
description: AI アシスタントで使用できるMarketo Engage MCPの操作について説明します。
autotag-review: '2026-06-02T13:31:42.084Z'
TQID: 'https://experienceleague.adobe.com/qvrWbHOCsCCHctduNDxMhkE8JAKxZk8FCYfKvzxfcYA'
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: a7170d27-32ab-462b-a333-269abc654483id: b0bb9048-d951-48d8-8232-45cf248a7e27id: dca84292-69e9-4116-a575-667d31fa060did: e64968b2-4ee5-47f9-8cae-0588f184b9eb
topic_v2: id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
source-git-commit: c631b7c3d571f29083673f9b97d22230d109abfc
workflow-type: tm+mt
source-wordcount: 1228
ht-degree: 50%

---


# [!DNL Marketo Engage]個のMCP操作

次の操作は、[!DNL Marketo Engage] MCP サーバーを通じて使用できます。 サーバーは、読み取り専用または非破壊的なエンドポイントを提供します。 AI システムは`Delete`またはその他の破壊的な操作を使用できません。

>[!NOTE]
>
>スマートリストとスマートキャンペーン `create`および`update` ツールは、2026年9月のリリースを対象としています。

Marketo AIおよびMarketo Engage MCP サーバーでのデータの処理方法について詳しくは、[Data Information](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/marketo-ai/data-information) ページを参照してください。

## 一括書き出し

[一括書き出しAPI リファレンス](https://developer.adobe.com/marketo-apis/api/mapi){target="_blank"}

- `bulk_export_create`
- `bulk_export_enqueue`
- `bulk_export_file`
- `bulk_export_status`
- `get_import_status`

## チャネルとタグ

[ チャネル API リファレンス ](https://developer.adobe.com/marketo-apis/api/asset#tag/Channels){target="_blank"} | [ タグ API リファレンス ](https://developer.adobe.com/marketo-apis/api/asset#tag/Tags){target="_blank"}

- `browse_channels`
- `browse_tag_types`
- `get_channel_by_name`
- `get_tag_type_by_name`

## メール

[メール API リファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails){target="_blank"}

- `approve_email`
- `browse_emails`
- `create_email`
- `get_email_by_id`
- `get_email_by_name`
- `get_email_content`
- `update_email_content`

## フォルダー

[Folders API リファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders){target="_blank"}

- `browse_folders`
- `create_folder`
- `delete_folder`
- `get_folder_by_id`
- `get_folder_by_name`
- `get_folder_content`
- `update_folder`

## フォーム

[Forms API リファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms){target="_blank"}

- `add_field_set`
- `add_field_to_form`
- `add_field_visibility_rule`
- `add_rich_text_field`
- `approve_form`
- `browse_forms`
- `clone_form`
- `create_form`
- `delete_field_from_fieldset`
- `delete_form`
- `delete_form_field`
- `discard_form_draft`
- `get_form_by_id`
- `get_form_by_name`
- `get_form_field_metadata`
- `get_form_fields`
- `get_forms_used_by`
- `get_program_member_fields`
- `get_thank_you_page`
- `set_field_autofill`
- `update_field_positions`
- `update_form`
- `update_form_field`

## リード

[リード API リファレンス](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads){target="_blank"}

- `add_leads_to_list`
- `describe_lead`
- `get_activity_types`
- `get_lead_activities`
- `get_leads_by_filter`
- `get_leads_by_smart_list`
- `get_paging_token`

## プログラム

[プログラム API リファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs){target="_blank"}

- `approve_program`
- `browse_email_batch_programs`
- `browse_nurture_programs`
- `browse_program_details`
- `browse_program_events`
- `browse_programs`
- `browse_scheduled_programs`
- `clone_program`
- `create_program`
- `delete_program_tag`
- `get_program_by_id`
- `get_program_by_name`
- `get_program_creation_options`
- `get_program_smart_list`
- `get_programs_by_tag`
- `unapprove_program`
- `update_program`
- `update_program_tag`

## スマートキャンペーン

[スマートキャンペーン API リファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns){target="_blank"}

- `activate_smart_campaign`
- `add_flow_step`
- `browse_smart_campaigns`
- `create_smart_campaign`
- `facet_smart_campaigns`
- `get_smart_campaign_auto_suggest`
- `get_smart_campaign_by_id`
- `get_smart_campaign_by_name`
- `get_smart_campaign_flow_step_by_name`
- `get_smart_campaign_flow_step_type_by_name`
- `get_smart_campaign_flow_step_types`
- `get_smart_campaign_flow_steps`
- `get_smart_campaign_rule_by_name`
- `get_smart_campaign_rules`
- `get_smart_campaign_scheduled_runs`
- `get_smart_campaign_used_by`
- `get_smart_list_by_campaign_id`
- `schedule_campaign`
- `trigger_campaign`
- `update_flow_step_choice`
- `update_smart_campaign`

## スマートリスト

[スマートリスト API リファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Lists){target="_blank"}

- `add_smart_list_rule`
- `browse_smart_lists`
- `clone_smart_list`
- `create_smart_list`
- `delete_all_smart_list_rules`
- `get_smart_list_auto_suggest`
- `get_smart_list_by_id`
- `get_smart_list_by_name`
- `get_smart_list_rule_by_name`
- `get_smart_list_rules`
- `get_smart_list_used_by`
- `remove_smart_list_rule_constraint`
- `reorder_smart_list_rules`
- `update_smart_list_filter_logic`
- `update_smart_list_rule`

## スニペット

[スニペット API リファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Snippets){target="_blank"}

- `approve_snippet`
- `browse_snippets`
- `clone_snippet`
- `create_snippet`
- `delete_snippet`
- `discard_snippet_draft`
- `facet_snippets`
- `get_snippet_by_id`
- `get_snippet_content`
- `get_snippet_dynamic_content`
- `unapprove_snippet`
- `update_snippet`
- `update_snippet_content`
- `update_snippet_dynamic_content`

## 静的リスト

[静的リスト API リファレンス](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists){target="_blank"}

- `browse_lists`
- `create_list`
- `get_list_by_id`
- `get_list_by_name`
- `get_list_members`
- `remove_from_list`
- `update_list`

## トークン

[トークン API リファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens){target="_blank"}

- `create_calendar_token`
- `create_token`
- `delete_token`
- `get_calendar_tokens`
- `get_tokens_by_folder`

## MCP フローステップツールが有効

<table style="table-layout:auto">
<tr>
<th>フローステップ</th>
<th>トリガー</th>
<th>フィルター（アクティビティ）</th>
<th>フィルター（属性）</th>
</tr>
<tr>
<td valign="top"><ul><li>フィールドセットに追加</li><li>リストに追加</li><li>Microsoft キャンペーンに追加</li><li>育成に追加</li><li>SFDC キャンペーンに追加​</li><li>Web フックの呼び出し</li><li>データ値の変更</li><li>リードのパーティションを変更</li><li>育成ケイデンスを変更</li><li>育成トラックを変更</li><li>所有者を変更</li><li>Microsoft の所有者の変更</li><li>プログラムデータの変更</li><li>プログラムメンバーのデータの変更</li><li>売上高ステージの変更</li><li>スコアの変更</li><li>セグメントの変更</li><li>進行状況のステータスを変更</li><li>SFDC キャンペーンのステータスを変更</li><li>リードを変換</li><li>タスクの作成</li><li>Microsoft でタスクを作成</li><li>リードの削除</li><li>Microsoftからリードを削除</li><li>SFDC からリードを削除</li><li>キャンペーンの実行</li><li>注目のアクション</li><li>フィールドセットから削除</li><li>フローから削除</li><li>リストから削除</li><li>Microsoft キャンペーンから削除</li><li>SFDC キャンペーンから削除</li><li>キャンペーンのリクエスト</li><li>アラートの送信</li><li>メールの送信</li><li>リードをMicrosoftに同期</li><li>リードを SFDC に同期</li><li>待機</li></ul></td>
<td valign="top"><ul><li>アクティビティの記録</li><li>アクティビティの更新</li><li>リストに追加</li><li>Microsoft Campaignに追加しました</li><li>ナーチャリングに追加しました</li><li>商談に追加</li><li>商談（アカウント）に追加</li><li>商談（連絡先）に追加</li><li>SFDC キャンペーンに追加</li><li>イベント中に質問する</li><li>イベントへの参加</li><li>キャンペーンをリクエスト</li><li>リンクをクリック</li><li>メール内リンクのクリック</li><li>セールスメール内のリンクをクリック</li><li>SMS メッセージのリンクをクリック</li><li>リンクのクリック数</li><li>データ値変更</li><li>アセットをダウンロード</li><li>バウンスメール</li><li>ソフトバウンスメール</li><li>メール配信完了</li><li>対話型フローでエンゲージ</li><li>ダイアログを使用する</li><li>会話フローでエージェントとエンゲージ</li><li>ダイアログでエージェントとエンゲージ</li><li>フォームの入力</li><li>注目のアクションあり</li><li>対話型フローでのドキュメントの操作</li><li>ダイアログでのドキュメントの操作</li><li>セールスメール送信</li><li>リードがコンバージョン済み</li><li>リードが作成されました</li><li>Microsoftからリードが削除されました</li><li>SFDCからリードが削除されました</li><li>リードはMarketoにプッシュされます</li><li>リードはMicrosoftに同期されます</li><li>リードはSFDCに同期されます</li><li>リードパーティションの変更</li><li>手動ステージの変更</li><li>ケイデンスの変更の育成</li><li>ナーチャリングトラックの変更</li><li>メールを開く</li><li>セールスメールを開く</li><li>商談（アカウント）が更新されました</li><li>商談（連絡先）が更新されました</li><li>商談更新</li><li>所有者の変更</li><li>Microsoftでのオーナーの変更</li><li>プログラムメンバーデータが変更されました</li><li>進捗ステータスが変更されました</li><li>ダイアログの目標を達成</li><li>対話型フローで目標を達成</li><li>転送メール（友達宛て）を受信</li><li>リストから削除</li><li>Microsoft キャンペーンから削除</li><li>商談から削除</li><li>商談（アカウント）から削除されました</li><li>商談（連絡先）から削除されました</li><li>SFDC キャンペーンから削除</li><li>営業用メールへの返信</li><li>アンケートへの回答</li><li>アンケートへの回答</li><li>収益ステージの変更</li><li>セールスメールのバウンス</li><li>セールスメールの受信</li><li>対話型フローでスケジュール会議を開催</li><li>ダイアログでのスケジュールミーティング</li><li>スコア変更</li><li>セグメント変更</li><li>アラート送信</li><li>転送メール（友達宛て）を送信</li><li>SMS メッセージバウンス</li><li>SMS メッセージが配信される</li><li>SFDC キャンペーンでステータスが変更された</li><li>メール配信停止</li><li>Web ページにアクセス</li><li>ウェブフックの呼び出し中</li></ul></td>
<td valign="top"><ul><li>活動が記録済み</li><li>活動が更新済み</li><li>アラートを送信済み</li><li>キャンペーンが実行されました</li><li>キャンペーンをリクエスト済み</li><li>リンクをクリック</li><li>メール内リンクをクリック済み</li><li>セールスメール内のリンクをクリック済み</li><li>SMS メッセージのクリックリンク</li><li>リンクをクリックしました</li><li>データ値変更済み</li><li>アセットをダウンロード済み</li><li>バウンスしたメール</li><li>ソフトバウンスしたメール</li><li>会話フローにエンゲージ済み</li><li>ダイアログでエンゲージ済み</li><li>対話型フローでエージェントとエンゲージ</li><li>ダイアログでエージェントとエンゲージ済み</li><li>フォーム入力完了</li><li>過去に注目のアクションあり</li><li>イベント中に質問済み</li><li>イベントに参加済み</li><li>対話型フローでのドキュメントの操作</li><li>ダイアログでドキュメントを操作済み</li><li>変更されたリード パーティション</li><li>リードがコンバージョンしました</li><li>リードが作成されました</li><li>Microsoftからリードが削除されました</li><li>SFDCからリードが削除されました</li><li>リードはMarketoにプッシュされました</li><li>リードがMicrosoftに同期されました</li><li>リードがSFDCに同期されました</li><li>ナーチャリングの頻度が変更されました</li><li>ナーチャリングトラックが変更されました</li><li>メール開封済み</li><li>セールスメール開封済み</li><li>商談（アカウント）が更新されました</li><li>商談（連絡先）が更新されました</li><li>商談は更新済み</li><li>所有者が変更済み</li><li>Microsoftでオーナーが変更されました</li><li>プログラムメンバーデータが変更されました</li><li>進捗ステータスが変更されました</li><li>ダイアログの目標達成済み</li><li>対話型フローで目標を達成</li><li>転送メール（友達宛て）を受信</li><li>セールスメールに返信</li><li>アンケートへの回答</li><li>アンケートへの回答</li><li>収益ステージを変更済み</li><li>セールスメールバウンス</li><li>セールスメール受信済み</li><li>対話型フローでスケジュールされたミーティング</li><li>ダイアログでミーティングをスケジュール</li><li>スコアを変更済み</li><li>セグメント変更済み</li><li>転送メール（友達宛て）を送信</li><li>SMS メッセージのバウンス</li><li>メール購読解除済み</li><li>ウェブページにアクセス済み</li><li>リストに追加済み</li><li>ナーチャリングに追加されました</li><li>商談に追加済み</li><li>さんが商談（アカウント）に追加されました</li><li>さんが商談（連絡先）に追加されました</li><li>メール配信済み</li><li>SMS メッセージが配信されました</li><li>リストから削除済み</li><li>商談から削除済み</li><li>商談（アカウント）から削除されました</li><li>が商談（連絡先）から削除されました</li><li>メールを送信済み</li><li>セールスメールを送信済み</li><li>ウェブフックの呼び出し中</li></ul></td>
<td valign="top"><ul><li>アカウント所有者のメール</li><li>アカウント所有者の名</li><li>アカウント所有者の姓</li><li>取得日</li><li>新規顧客獲得プログラム</li><li>新規顧客獲得プログラム名</li><li>住所</li><li>年間収益</li><li>匿名 IP</li><li>請求先住所</li><li>請求先住所（市区町村）</li><li>請求先住所 (国)</li><li>請求先住所（郵便番号）</li><li>請求先住所（都道府県）</li><li>ブロックリストに登録済み</li><li>市区町村</li><li>企業の Microsoft のタイプ</li><li>企業名</li><li>国</li><li>作成日時</li><li>生年月日</li><li>部門</li><li>電話連絡拒否</li><li>電話連絡拒否の理由</li><li>重複フィールド</li><li>メールアドレス</li><li>メール無効</li><li>メール無効の理由</li><li>メールの中断</li><li>メールの中断時刻</li><li>メールの中断原因</li><li>ファックス番号</li><li>名前（名）</li><li>氏名</li><li>商談あり</li><li>業種</li><li>推測される市区町村</li><li>推測される企業</li><li>推測される国</li><li>推測される都市圏</li><li>推測される市外局番</li><li>推測される郵便番号</li><li>推測される都道府県／地域</li><li>顧客</li><li>パートナー</li><li>役職</li><li>名前（姓）</li><li>リード所有者のメールアドレス</li><li>リード所有者の名（名）</li><li>リード所有者の役職名</li><li>リード所有者の姓</li><li>リード所有者の電話番号</li><li>リード パーティション名</li><li>リード評価</li><li>リードのスコア</li><li>リードのソース</li><li>リードのステータス</li><li>代表電話</li><li>マーケティングを中断したリード</li><li>フィールドセットのメンバー</li><li>リストのメンバー</li><li>Nurtureのメンバー</li><li>プログラムのメンバー</li><li>収益モデルのメンバー</li><li>収益ステージのメンバー</li><li>SFDC キャンペーンのメンバー</li><li>スマートキャンペーンのメンバー</li><li>スマートリストのメンバー</li><li>Microsoft アカウント番号</li><li>Microsoft による作成日</li><li>Microsoft 削除済み</li><li>Microsoft のタイプ</li><li>ミドルネーム</li><li>携帯電話番号</li><li>メモ</li><li>従業員数</li><li>商談数</li><li>訪問者の参照元</li><li>参照元検索エンジン</li><li>参照元検索フレーズ</li><li>参照元のソース情報</li><li>参照元のソースのタイプ</li><li>親会社名</li><li>顧客のタイムゾーン</li><li>電話番号</li><li>郵便番号</li><li>ランダム サンプル</li><li>登録ソース情報</li><li>登録ソースのタイプ</li><li>ロール</li><li>敬称</li><li>SFDC アカウント番号</li><li>SFDC 作成日</li><li>SFDC 削除済み</li><li>SFDC のタイプ</li><li>SIC コード</li><li>サイト</li><li>ステート</li><li>合計商談数</li><li>商談の合計収益予測</li><li>配信停止完了</li><li>登録解除の理由</li><li>更新時刻</li><li>Web サイト</li></ul></td>
</tr>
</table>
