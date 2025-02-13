---
title: エンドポイントの参照
feature: REST API
description: Marketo API エンドポイントのリファレンス
exl-id: 27d16b6f-865a-4e40-ab9c-cbabe2927472
source-git-commit: 3632d2b713d97a2c895c65f144c07e62e1d369cb
workflow-type: tm+mt
source-wordcount: '4676'
ht-degree: 28%

---

# エンドポイントの参照

以下は、Marketo REST API リファレンスへのリンクです。

- [ アセット ](https://developer.adobe.com/marketo-apis/api/asset/)
- [ID](https://developer.adobe.com/marketo-apis/api/identity/)
- [ リードデータベース ](https://developer.adobe.com/marketo-apis/api/mapi/)
- [ユーザー管理](https://developer.adobe.com/marketo-apis/api/user/)

## エンドポイントリスト {#endpoint_list}

REST API エンドポイントの一覧を次に示します。

| 名前 | グループ | メソッド | URI | 必要な権限 |
|---|---|---|---|---|
| カスタムアクティビティの追加 | アクティビティ | POST | /rest/v1/activities/external.json | 読み取り／書き込みアクティビティ |
| カスタムアクティビティタイプの承認 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/approve.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプ属性の作成 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/attributes/create.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプの作成 | アクティビティ | POST | /rest/v1/activities/external/type.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプを削除 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/delete.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプ属性の削除 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/attributes/delete.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプの説明 | アクティビティ | GET | /rest/v1/activities/external/type/{apiName}/describe.json | 読み取り専用アクティビティメタデータ |
| カスタムアクティビティタイプのドラフトを破棄 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/discardDraft.json | 読み取り／書き込みアクティビティメタデータ |
| アクティビティタイプの取得 | アクティビティ | GET | /rest/v1/activities/types.json | 読み取り専用アクティビティ |
| カスタムアクティビティタイプの取得 | アクティビティ | GET | /rest/v1/activities/external/types.json | 読み取り専用アクティビティメタデータ |
| 削除済みリードの取得 | アクティビティ | GET | /rest/v1/activities/deletedleads.json | 読み取り専用アクティビティ |
| リードアクティビティの取得 | アクティビティ | GET | /rest/v1/activities.json | 読み取り専用アクティビティ |
| リードの変更の取得 | アクティビティ | GET | /rest/v1/activities/leadchanges.json | 読み取り専用アクティビティ |
| ページトークンの取得 | アクティビティ | GET | /rest/v1/activities/pagingtoken.json | 読み取り専用アクティビティ |
| カスタムアクティビティタイプを更新 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプ属性の更新 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/attributes/update.json | 読み取り／書き込みアクティビティメタデータ |
| ID | 認証 | GETまたは POST | /identity/oauth/token | None |
| 書き出しアクティビティジョブをキャンセル | 一括書き出しアクティビティ | POST | /bulk/v1/activities/export/{exportid}/cancel.json | 読み取り専用アクティビティ |
| エクスポートアクティビティジョブを作成 | 一括書き出しアクティビティ | POST | /bulk/v1/activities/export/create.json | 読み取り専用アクティビティ |
| 書き出しアクティビティジョブをエンキュー | 一括書き出しアクティビティ | POST | /bulk/v1/activities/export/{exportid}/enqueue.json | 読み取り専用アクティビティ |
| 書き出しアクティビティファイルを取得 | 一括書き出しアクティビティ | GET | /bulk/v1/activities/export/{exportid}/file.json | 読み取り専用アクティビティ |
| エクスポートアクティビティジョブステータスを取得 | 一括書き出しアクティビティ | GET | /bulk/v1/activities/export/{exportid}/status.json | 読み取り専用アクティビティ |
| エクスポートアクティビティジョブを取得 | 一括書き出しアクティビティ | GET | /bulk/v1/activities/export.json | 読み取り専用アクティビティ |
| カスタム オブジェクトの書き出しジョブのキャンセル | カスタムオブジェクトの一括書き出し | POST | /bulk/v1/customobjects/export/{exportid}/cancel.json | カスタムオブジェクト読み取り可 |
| カスタム オブジェクト書き出しジョブの作成 | カスタムオブジェクトの一括書き出し | POST | /bulk/v1/customobjects/export/create.json | カスタムオブジェクト読み取り可 |
| カスタム オブジェクト書き出しジョブをキューに入れる | カスタムオブジェクトの一括書き出し | POST | /bulk/v1/customobjects/export/{exportid}/enqueue.json | カスタムオブジェクト読み取り可 |
| カスタム オブジェクト ファイルのエクスポートを取得 | カスタムオブジェクトの一括書き出し | GET | /bulk/v1/customobjects/export/{exportid}/file.json | カスタムオブジェクト読み取り可 |
| カスタムオブジェクトジョブステータスの書き出しを取得 | カスタムオブジェクトの一括書き出し | GET | /bulk/v1/customobjects/export/{exportid}/status.json | カスタムオブジェクト読み取り可 |
| カスタム オブジェクト ジョブのエクスポートを取得 | カスタムオブジェクトの一括書き出し | GET | /bulk/v1/customobjects/export.json | カスタムオブジェクト読み取り可 |
| リードジョブの書き出しをキャンセル | リードを一括書き出し | POST | /bulk/v1/leads/export/{exportid}/cancel.json | リード読み取り可 |
| リードエクスポートジョブの作成 | リードを一括書き出し | POST | /bulk/v1/leads/export/create.json | リード読み取り可 |
| リード書き出しジョブをキューに入れる | リードを一括書き出し | POST | /bulk/v1/leads/export/{exportid}/enqueue.json | リード読み取り可 |
| リードファイルのエクスポートを取得 | リードを一括書き出し | GET | /bulk/v1/leads/export/{exportid}/file.json | リード読み取り可 |
| リード書き出しジョブステータスの取得 | リードを一括書き出し | GET | /bulk/v1/leads/export/{exportid}/status.json | リード読み取り可 |
| リードジョブのエクスポートの取得 | リードを一括書き出し | GET | /bulk/v1/leads/export.json | リード読み取り可 |
| プログラムメンバージョブのエクスポートをキャンセル | プログラムメンバーの一括書き出し | POST | /bulk/v1/program/members/export/{exportid}/cancel.json | リード読み取り可 |
| プログラム メンバージョブのエクスポートの作成 | プログラムメンバーの一括書き出し | POST | /bulk/v1/program/members/export/create.json | リード読み取り可 |
| プログラム メンバージョブのエクスポートをキューに入れる | プログラムメンバーの一括書き出し | POST | /bulk/v1/program/members/export/{exportid}/enqueue.json | リード読み取り可 |
| プログラム メンバ ファイルのエクスポートの取得 | プログラムメンバーの一括書き出し | GET | /bulk/v1/program/members/export/{exportid}/file.json | リード読み取り可 |
| プログラム メンバージョブの状態のエクスポートの取得 | プログラムメンバーの一括書き出し | GET | /bulk/v1/program/members/export/{exportid}/status.json | リード読み取り可 |
| プログラム メンバージョブのエクスポートの取得 | プログラムメンバーの一括書き出し | GET | /bulk/v1/program/members/export.json | リード読み取り可 |
| カスタムオブジェクトの読み込みの取得に失敗しました | カスタムオブジェクトの一括読み込み | GET | /bulk/v1/customobjects/import/{id}/failures.json | 読み取り／書き込みカスタムオブジェクト |
| 読み込みのカスタムオブジェクトステータスを取得 | カスタムオブジェクトの一括読み込み | GET | /bulk/v1/customobjects/import/{id}/status.json | 読み取り／書き込みカスタムオブジェクト |
| カスタムオブジェクトの読み込みの警告の取得 | カスタムオブジェクトの一括読み込み | GET | /bulk/v1/customobjects/import/{id}/warnings.json | 読み取り／書き込みカスタムオブジェクト |
| カスタムオブジェクトを読み込み | カスタムオブジェクトの一括読み込み | POST | /bulk/v1/customobjects/{apiName}/import.json | 読み取り／書き込みカスタムオブジェクト |
| リードの読み込みエラーを取得 | リードを一括読み込み | GET | /bulk/v1/leads/batch/{id}/failures.json | リード読み取り/書き込み可 |
| リードのインポートステータスを取得 | リードを一括読み込み | GET | /bulk/v1/leads/batch/{id}.json | リード読み取り/書き込み可 |
| リード警告のインポートの取得 | リードを一括読み込み | GET | /bulk/v1/leads/batch/{id}/warnings.json | リード読み取り/書き込み可 |
| リードを読み込み | リードを一括読み込み | POST | /bulk/v1/leads.json | リード読み取り/書き込み可 |
| インポート プログラム メンバーの取得エラー | プログラムメンバーの一括読み込み | GET | /bulk/v1/program/members/import/{id}/failures.json | リード読み取り/書き込み可 |
| インポート プログラム メンバーステータスの取得 | プログラムメンバーの一括読み込み | GET | /bulk/v1/program/members/import/{id}/status.json | リード読み取り/書き込み可 |
| インポート プログラム メンバーの警告の取得 | プログラムメンバーの一括読み込み | GET | /bulk/v1/program/members/import/{id}/warnings.json | リード読み取り/書き込み可 |
| プログラムメンバーのインポート | プログラムメンバーの一括読み込み | POST | /bulk/v1/program/{programId}/members/import.json | リード読み取り/書き込み可 |
| ID でキャンペーンを取得 | キャンペーン | GET | /rest/v1/campaigns/{id}.json | 読み取り専用キャンペーン |
| キャンペーンを取得 | キャンペーン | GET | /rest/v1/campaigns.json | 読み取り専用キャンペーン |
| キャンペーンのリクエスト | キャンペーン | POST | /rest/v1/campaigns/{id}/trigger.json | 読み取り/書き込みキャンペーン |
| キャンペーンのスケジュール | キャンペーン | POST | /rest/v1/campaigns/{id}/schedule.json | 読み取り/書き込みキャンペーン |
| 名前によるチャネルの取得 | チャネル | GET | /rest/asset/v1/channel/byName.json | 読み取り専用資産 |
| チャネルを取得 | チャネル | GET | /rest/asset/v1/channels.json | 読み取り専用資産 |
| 会社の削除 | 企業 | POST | /rest/v1/companies/delete.json | 読み取り／書き込み企業 |
| 会社の説明 | 企業 | GET | /rest/v1/companies/describe.json | 企業読み取り可 |
| 会社の取得 | 企業 | GET | /rest/v1/companies.json | 企業読み取り可 |
| 会社の同期 | 企業 | POST | /rest/v1/companies.json | 読み取り／書き込み企業 |
| 名前による会社フィールドの取得 | 企業 | GET | /rest/v1/companies/schema/fields/{fieldApiName}.json | 読み取り/書き込みスキーマカスタムフィールド |
| 会社フィールドを取得 | 企業 | GET | /rest/v1/companies/schema/fields.json | 読み取り/書き込みスキーマカスタムフィールド |
| カスタムオブジェクトタイプフィールドの追加 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/addField.json | 読み取り/書き込みカスタムオブジェクトタイプ |
| カスタム オブジェクト タイプの承認 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/approve.json | 読み取り/書き込みカスタムオブジェクトタイプ |
| カスタム オブジェクトの削除 | カスタムオブジェクト | POST | /rest/v1/customobjects/{name}/delete.json | 読み取り／書き込みカスタムオブジェクト |
| カスタム オブジェクト タイプの削除 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/delete.json | 読み取り/書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトタイプフィールドの削除 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/deleteField.json | 読み取り/書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトの説明 | カスタムオブジェクト | GET | /rest/v1/customobjects/{name}/describe.json | カスタムオブジェクト読み取り可 |
| カスタムオブジェクトタイプの説明 | カスタムオブジェクト | GET | /rest/v1/customobjects/schema/{apiName}/describe.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタム オブジェクト タイプの下書きを破棄 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/discardDraft.json | 読み取り/書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトを取得 | カスタムオブジェクト | GET | /rest/v1/customobjects/{name}.json | カスタムオブジェクト読み取り可 |
| カスタムオブジェクトのリンク可能オブジェクトを取得 | カスタムオブジェクト | GET | /rest/v1/customobjects/schema/linkableObjects.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタムオブジェクト依存Assetsを取得 | カスタムオブジェクト | GET | /rest/v1/customobjects/schema/{apiName}/dependentAssets.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタムオブジェクトタイプの取得フィールドのデータタイプ | カスタムオブジェクト | GET | /rest/v1/customobjects/schema/fieldDataTypes.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタムオブジェクトのリスト | カスタムオブジェクト | GET | /rest/v1/customobjects.json | カスタムオブジェクト読み取り可 |
| カスタムオブジェクトタイプのリスト | カスタムオブジェクト | GET | /rest/v1/customobjects/schema.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタム オブジェクトの同期 | カスタムオブジェクト | POST | /rest/v1/customobjects/{name}.json | 読み取り／書き込みカスタムオブジェクト |
| カスタム オブジェクト タイプの同期 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema.json | 読み取り/書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトタイプフィールドを更新 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/updateField.json | 読み取り/書き込みカスタムオブジェクトタイプ |
| メールテンプレートドラフトを承認 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/approveDraft.json | 読み取り/書き込みアセット |
| メールテンプレートの複製 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/clone.json | 読み取り/書き込みアセット |
| メールテンプレートを作成 | メールテンプレート | POST | /rest/asset/v1/emailTemplates.json | 読み取り/書き込みアセット |
| メールテンプレートの削除 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/delete.json | 読み取り/書き込みアセット |
| メールテンプレートのドラフトを破棄 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/discardDraft.json | 読み取り/書き込みアセット |
| ID によるメールテンプレートの取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplate/{id}.json | 読み取り専用資産 |
| 名前によるメールテンプレートの取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplate/byName.json | 読み取り専用資産 |
| ID によるメールテンプレートコンテンツの取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplate/{id}/content.json | 読み取り専用資産 |
| が使用する電子メールテンプレートを取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplates/{id}/usedBy.json | 読み取り専用資産 |
| メールテンプレートの取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplates.json | 読み取り専用資産 |
| メールテンプレートドラフトを未承認 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/unapprove.json | 読み取り/書き込みアセット |
| メールテンプレートコンテンツの更新 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/content.json | 読み取り/書き込みアセット |
| メールテンプレートメタデータの更新 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}.json | 読み取り/書き込みアセット |
| メールモジュールを追加 | メール | POST | /rest/asset/v1/email/{id}/content/{moduleId}/add.json | 読み取り/書き込みアセット |
| メールのドラフトを承認 | メール | POST | /rest/asset/v1/email/{id}/approveDraft.json | 読み取り/書き込みアセット |
| メールの複製 | メール | POST | /rest/asset/v1/email/{id}/clone.json | 読み取り/書き込みアセット |
| メールを作成 | メール | POST | /rest/asset/v1/emails.json | 読み取り/書き込みアセット |
| メールの削除 | メール | POST | /rest/asset/v1/email/{id}/delete.json | 読み取り/書き込みアセット |
| モジュールの削除 | メール | POST | /rest/asset/v1/email/{id}/content/{moduleId}/delete.json | 読み取り/書き込みアセット |
| メールのドラフトを破棄 | メール | POST | /rest/asset/v1/email/{id}/discardDraft.json | 読み取り/書き込みアセット |
| 電子メールモジュールを複製 | メール | POST | /rest/asset/v1/email/{id}/content/{moduleId}/duplicate.json | 読み取り/書き込みアセット |
| ID で電子メールを取得 | メール | GET | /rest/asset/v1/email/{id}.json | 読み取り専用資産 |
| 名前によるメールの取得 | メール | GET | /rest/asset/v1/email/byName.json | 読み取り専用資産 |
| メールコンテンツを取得 | メール | GET | /rest/asset/v1/email/{id}/content.json | 読み取り専用資産 |
| メールの動的コンテンツの取得 | メール | GET | /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json | 読み取り専用資産 |
| メールの完全なコンテンツを取得 | メール | GET | /rest/asset/v1/email/{id}/fullContent.json | 読み取り専用資産 |
| メール変数の取得 | メール | GET | /rest/asset/v1/email/{id}/variables.json | 読み取り専用資産 |
| メール CC フィールドを取得 | メール | GET | /rest/asset/v1/email/ccFields.json | 読み取り専用資産 |
| メールを取得 | メール | GET | /rest/asset/v1/emails.json | 読み取り専用資産 |
| メールモジュールの並べ替え | メール | POST | /rest/asset/v1/email/{id}/content/rearrange.json | 読み取り/書き込みアセット |
| メールモジュール名を変更 | メール | POST | /rest/asset/v1/email/{id}/content/{moduleId}/rename.json | 読み取り/書き込みアセット |
| サンプル メールの送信 | メール | POST | /rest/asset/v1/email/{id}/sendSample.json | 読み取り/書き込みアセット |
| メールを未承認 | メール | POST | /rest/asset/v1/email/{id}/unapprove.json | 読み取り/書き込みアセット |
| メールコンテンツを更新 | メール | POST | /rest/asset/v1/email/{id}/content.json | 読み取り/書き込みアセット |
| 「メールコンテンツの更新」セクション | メール | POST | /rest/asset/v1/email/{id}/content/{htmlId}.json | 読み取り/書き込みアセット |
| 「メール動的コンテンツの更新」セクション | メール | POST | /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json | 読み取り/書き込みアセット |
| メールの完全なコンテンツを更新 | メール | POST | /rest/asset/v1/emails/{id}/fullContent.json | 読み取り/書き込みアセット |
| メールメタデータの更新 | メール | POST | /rest/asset/v1/email/{id}.json | 読み取り/書き込みアセット |
| メール変数を更新 | メール | POST | /rest/asset/v1/email/{id}/variable/{name}.json | 読み取り/書き込みアセット |
| ファイルを作成 | ファイル | POST | /rest/asset/v1/files.json | 読み取り/書き込みアセット |
| ID によるファイルの取得 | ファイル | GET | /rest/asset/v1/file/{id}.json | 読み取り専用資産 |
| ファイルを名前で取得 | ファイル | GET | /rest/asset/v1/file/byName.json | 読み取り専用資産 |
| ファイルを取得 | ファイル | GET | /rest/asset/v1/files.json | 読み取り専用資産 |
| ファイルコンテンツを更新 | ファイル | POST | /rest/asset/v1/file/{id}/content.json | 読み取り/書き込みアセット |
| フォルダの作成 | フォルダー | POST | /rest/asset/v1/folders.json | 読み取り/書き込みアセット |
| フォルダーの削除 | フォルダー | POST | /rest/asset/v1/folder/{id}/delete.json | 読み取り/書き込みアセット |
| ID によるフォルダーの取得 | フォルダー | GET | /rest/asset/v1/folder/{id}.json | 読み取り専用資産 |
| 名前によるフォルダーの取得 | フォルダー | GET | /rest/asset/v1/folder/byName.json | 読み取り専用資産 |
| フォルダーのコンテンツを取得 | フォルダー | GET | /rest/asset/v1/folder/{id}/content.json | 読み取り専用資産 |
| フォルダーを取得 | フォルダー | GET | /rest/asset/v1/folders.json | 読み取り専用資産 |
| フォルダーメタデータの更新 | フォルダー | POST | /rest/asset/v1/folder/{id}.json | 読み取り/書き込みアセット |
| フォームにフィールドを追加 | フォームフィールド | POST | /rest/asset/v1/form/{id}/fields.json | 読み取り/書き込みアセット |
| フォームにフィールドセットを追加 | フォームフィールド | POST | /rest/asset/v1/form/{id}/fieldSet.json | 読み取り/書き込みアセット |
| フォームフィールド表示ルールの追加 | フォームフィールド | POST | /rest/asset/v1/form/{formId}/field/{fieldId}/visibility.json | 読み取り/書き込みアセット |
| リッチテキストフィールドを追加 | フォームフィールド | POST | /rest/asset/v1/form/{id}/richText.json | 読み取り/書き込みアセット |
| フィールドセットからフィールドを削除 | フォームフィールド | POST | /rest/asset/v1/form/{id}/fieldSet/{fieldSetId}/field/{fieldId}/delete.json | 読み取り/書き込みアセット |
| フォームフィールドを削除 | フォームフィールド | POST | /rest/asset/v1/form/{id}/field/{fieldId}/delete.json | 読み取り/書き込みアセット |
| 使用可能なフォームフィールドを取得 | フォームフィールド | GET | /rest/asset/v1/form/fields.json | 読み取り専用資産 |
| 利用可能なフォームプログラムメンバーフィールドを取得する | フォームフィールド | GET | /rest/asset/v1/form/programMemberFields.json | 読み取り専用資産 |
| フォームのフィールドの取得 | フォームフィールド | GET | /rest/asset/v1/form/{id}/fields.json | 読み取り専用資産 |
| フィールド位置の更新 | フォームフィールド | POST | /rest/asset/v1/form/{id}/reArrange.json | 読み取り/書き込みアセット |
| フォームフィールドを更新 | フォームフィールド | POST | /rest/asset/v1/form/{id}/field/{fieldId}.json | 読み取り/書き込みアセット |
| フォームドラフトを承認 | フォーム | POST | /rest/asset/v1/form/{id}/approveDraft.json | 読み取り/書き込みアセット |
| フォームのクローン作成 | フォーム | POST | /rest/asset/v1/form/{id}/clone.json | 読み取り/書き込みアセット |
| フォームを作成 | フォーム | POST | /rest/asset/v1/forms.json | 読み取り/書き込みアセット |
| フォームの取得者 | フォーム | GET | /rest/asset/v1/form/{id}/usedBy.json | 読み取り/書き込みアセット |
| フォームの削除 | フォーム | POST | /rest/asset/v1/form/{id}/delete.json | 読み取り/書き込みアセット |
| フォームの下書きを破棄する | フォーム | POST | /rest/asset/v1/form/{id}/discardDraft.json | 読み取り/書き込みアセット |
| ID でフォームを取得 | フォーム | GET | /rest/asset/v1/form/{id}.json | 読み取り専用資産 |
| 名前によるフォームの取得 | フォーム | GET | /rest/asset/v1/form/byName.json | 読み取り専用資産 |
| Formsの取得 | フォーム | GET | /rest/asset/v1/forms.json | 読み取り専用資産 |
| フォーム ID から「ありがとうございます」ページを取得 | フォーム | GET | /rest/asset/v1/form/{id}/thankYouPage.json | 読み取り専用資産 |
| フォームメタデータの更新 | フォーム | POST | /rest/asset/v1/form/{id}.json | 読み取り/書き込みアセット |
| 送信ボタンを更新 | フォーム | POST | /rest/asset/v1/{id}/submitButton.json | 読み取り/書き込みアセット |
| ありがとうページの更新 | フォーム | POST | /rest/asset/v1/form/{id}/thankYouPage.json | 読み取り/書き込みアセット |
| ランディングページコンテンツセクションを追加 | ランディングページコンテンツ | POST | /rest/asset/v1/landingPage/{id}/content.json | 読み取り/書き込みアセット |
| ランディングページコンテンツセクションを削除 | ランディングページコンテンツ | POST | /rest/asset/v1/landingPage/{id}/content/{contentId}/delete.json | 読み取り/書き込みアセット |
| ランディングページのコンテンツを取得 | ランディングページコンテンツ | GET | /rest/asset/v1/landingPage/{id}/content.json | 読み取り専用資産 |
| ランディングページの動的コンテンツを取得 | ランディングページコンテンツ | GET | /rest/asset/v1/landingPage/{id}/dynamicContent/{dynamicContentId}.json | 読み取り専用資産 |
| ランディングページコンテンツの更新セクション | ランディングページコンテンツ | POST | /rest/asset/v1/landingPage/{id}/content/{contentId}.json | 読み取り/書き込みアセット |
| ランディングページの動的コンテンツの節を更新 | ランディングページコンテンツ | POST | /rest/asset/v1/landingPage/{id}/dynamicContent/{dynamicContentId}.json | 読み取り/書き込みアセット |
| ランディングページテンプレートのドラフトを承認 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/approveDraft.json | 読み取り/書き込みアセット |
| ランディングページ テンプレートの複製 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/clone.json | 読み取り/書き込みアセット |
| ランディングページテンプレートの作成 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate.json | 読み取り/書き込みアセット |
| ランディングページテンプレートの削除 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/delete.json | 読み取り/書き込みアセット |
| ランディングページテンプレートのドラフトを破棄 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/discardDraft.json | 読み取り/書き込みアセット |
| ID によるランディングページテンプレートの取得 | ランディングページのテンプレート | GET | /rest/asset/v1/landingPageTemplate/{id}.json | 読み取り専用資産 |
| 名前によるランディングページテンプレートの取得 | ランディングページのテンプレート | GET | /rest/asset/v1/landingPageTemplates/byName.json | 読み取り専用資産 |
| ランディングページのテンプレートコンテンツを取得 | ランディングページのテンプレート | GET | /rest/asset/v1/landingPageTemplate/{id}/content.json | 読み取り専用資産 |
| ランディングページテンプレートの取得 | ランディングページのテンプレート | GET | /rest/asset/v1/landingPageTemplates.json | 読み取り専用資産 |
| ランディングページテンプレートの承認取消 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/unapprove.json | 読み取り/書き込みアセット |
| ランディングページテンプレートコンテンツを更新 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/content.json | 読み取り/書き込みアセット |
| ランディングページテンプレートメタデータの更新 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}.json | 読み取り/書き込みアセット |
| ランディングページのドラフトを承認 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/approveDraft.json | 読み取り/書き込みアセット |
| ランディングページのクローン作成 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/clone.json | 読み取り/書き込みアセット |
| ランディングページの作成 | ランディングページ | POST | /rest/asset/v1/landingPages.json | 読み取り/書き込みアセット |
| ランディングページの削除 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/delete.json | 読み取り/書き込みアセット |
| ランディングページのドラフトを破棄 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/discardDraft.json | 読み取り/書き込みアセット |
| ID によるランディングページの取得 | ランディングページ | GET | /rest/asset/v1/landingPage/{id}.json | 読み取り専用資産 |
| 名前によるランディングページの取得 | ランディングページ | GET | /rest/asset/v1/landingPage/byName.json | 読み取り専用資産 |
| ランディングページ変数を取得 | ランディングページ | GET | /rest/asset/v1/landingPage/{id}/variables.json | 読み取り専用資産 |
| ランディングページの取得 | ランディングページ | GET | /rest/asset/v1/landingPages.json | 読み取り専用資産 |
| ランディングページをプレビュー | ランディングページ | GET | /rest/asset/v1/landingPage/{id}/preview.json | 読み取り専用資産 |
| ランディングページの承認取消 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/unapprove.json | 読み取り/書き込みアセット |
| ランディングページのメタデータを更新 | ランディングページ | POST | /rest/asset/v1/{id}.json | 読み取り/書き込みアセット |
| ランディングページ変数を更新 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/variable/{variableId}.json | 読み取り/書き込みアセット |
| ランディングページのリダイレクトルールの作成 | ランディングページ | POST | /rest/asset/v1/redirectRules.json | 読み取り/書き込みリダイレクトルール |
| ランディングページのリダイレクトルールの削除 | ランディングページ | POST | /rest/asset/v1/redirectRule/{id}/delete.json | 読み取り/書き込みリダイレクトルール |
| ランディングページのリダイレクトルールの取得 | ランディングページ | GET | /rest/asset/v1/redirectRules.json | 読み取り専用リダイレクトルール |
| ID によるランディングページのリダイレクトルールの取得 | ランディングページ | GET | /rest/asset/v1/redirectRule/{id}.json | 読み取り専用リダイレクトルール |
| ランディングページのリダイレクトルールを更新 | ランディングページ | POST | /rest/asset/v1/redirectRule/{id}.json | 読み取り/書き込みリダイレクトルール |
| ランディングページのドメインを取得 | ランディングページ | GET | /rest/asset/v1/landingPageDomains.json | 読み取り専用リダイレクトルール |
| リードの関連付け | リード | POST | /rest/v1/leads/{id}/associate.json | リード読み取り/書き込み可 |
| リードプログラムのステータスの変更 | リード | POST | /rest/v1/leads/programs/{programId}/status.json | リード読み取り/書き込み可 |
| リードを削除 | リード | POST | /rest/v1/leads.json | リード読み取り/書き込み可 |
| リードの説明 | リード | GET | /rest/v1/leads/describe.json | リード読み取り可 |
| リード 2 の説明 | リード | GET | /rest/v1/leads/describe2.json | リード読み取り可 |
| プログラムメンバーの説明 | リード | GET | /rest/v1/program/members/describe.json | リード読み取り可 |
| リードを ID で取得 | リード | GET | /rest/v1/lead/{id}.json | リード読み取り可 |
| リード区分の取得 | リード | GET | /rest/v1/leads/partitions.json | リード読み取り可 |
| フィルタータイプ別のリードの取得 | リード | GET | /rest/v1/leads.json | リード読み取り可 |
| プログラム ID でリードを取得 | リード | GET | /rest/v1/leads/programs/{programId}.json | リード読み取り可 |
| リードのマージ | リード | POST | /rest/v1/leads/{id}/merge.json | リード読み取り/書き込み可 |
| リード ID 別にリストを取得 | リード | GET | /rest/v1/leads/{leadId}.json | 読み取り専用資産 |
| リード ID によるプログラムの取得 | リード | GET | /rest/v1/leads/{leadId}programMembership.json | 読み取り専用資産 |
| リード ID でスマートキャンペーンを取得 | リード | GET | /rest/v1/leads/{leadId}/smartCampaignMembership.json | 読み取り専用資産 |
| Marketo にリードをプッシュ | リード | POST | /rest/v1/leads/partitions.json | リード読み取り/書き込み可 |
| 送信フォーム | リード | POST | /rest/v1/leads/submitForm.json | リード読み取り/書き込み可 |
| リードを同期 | リード | POST | /rest/v1/leads.json | リード読み取り/書き込み可 |
| リードパーティションの更新 | リード | POST | /rest/v1/leads/partitions.json | リード読み取り/書き込み可 |
| 名前によるリードフィールドの取得 | リード | GET | /rest/v1/leads/schema/fields/{fieldApiName}.json | 読み取り/書き込みスキーマカスタムフィールド |
| リードフィールドを取得 | リード | GET | /rest/v1/leads/schema/fields.json | 読み取り/書き込みスキーマカスタムフィールド |
| リードフィールドを作成 | リード | POST | /rest/v1/leads/schema/fields.json | 読み取り/書き込みスキーマカスタムフィールド |
| リードフィールドを更新 | リード | POST | /rest/v1/leads/schema/fields/{fieldApiName}.json | 読み取り/書き込みスキーマカスタムフィールド |
| 指定顧客リストのメンバーの追加 | 重点顧客の一覧 | POST | /rest/v1/namedaccountlist/{id}/namedaccounts.json | 読み取り／書き込み重点顧客 |
| 指定顧客リストの削除 | 重点顧客の一覧 | POST | /rest/v1/namedaccountlists/delete.json | 読み出し/書き込み重要顧客リスト |
| 指定されたアカウント リストのメンバーの取得 | 重点顧客の一覧 | GET | /rest/v1/namedaccountlist/{id}/namedaccounts.json | 読み取り専用重点顧客 |
| 指定顧客リストの取得 | 重点顧客の一覧 | GET | /rest/v1/namedaccountlists.json | 読み出し専用重要顧客リスト |
| 指定顧客リストのメンバーの削除 | 重点顧客の一覧 | POST | /rest/v1/namedaccountlist/{id}/namedaccounts/remove.json | 読み取り／書き込み重点顧客 |
| 名前付きアカウント リストの同期 | 重点顧客の一覧 | POST | /rest/v1/namedaccountlists.json | 読み出し/書き込み重要顧客リスト |
| 特定アカウントを削除 | 重点顧客 | POST | /rest/v1/namedaccounts/delete.json | 読み取り／書き込み重点顧客 |
| 指定顧客の説明 | 重点顧客 | GET | /rest/v1/namedaccounts/describe.json | 読み取り専用重点顧客 |
| 重点顧客の取得 | 重点顧客 | GET | /rest/v1/namedaccounts.json | 読み取り専用重点顧客 |
| 指定アカウントの同期 | 重点顧客 | POST | /rest/v1/namedaccounts.json | 読み取り／書き込み重点顧客 |
| 名前による名前付きアカウントフィールドの取得 | 重点顧客 | GET | /rest/v1/namedaccounts/schema/fields/{fieldApiName}.json | 読み取り/書き込みスキーマカスタムフィールド |
| 指定顧客フィールドの取得 | 重点顧客 | GET | /rest/v1/namedaccounts/schema/fields.json | 読み取り/書き込みスキーマカスタムフィールド |
| 商談の削除 | 商談 | POST | /rest/v1/opportunities/delete.json | 読み取り／書き込み商談 |
| 商談ロールの削除 | 商談 | POST | /rest/v1/opportunities/roles/delete.json | 読み取り／書き込み商談 |
| オポチュニティの説明 | 商談 | GET | /rest/v1/opportunities/describe.json | 商談読み取り可 |
| オポチュニティの役割の説明 | 商談 | GET | /rest/v1/opportunities/roles/describe.json | 商談読み取り可 |
| 商談の取得 | 商談 | GET | /rest/v1/opportunities.json | 商談読み取り可 |
| オポチュニティの役割を取得 | 商談 | GET | /rest/v1/opportunities/roles.json | 商談読み取り可 |
| 商談を同期 | 商談 | POST | /rest/v1/opportunities.json | 読み取り／書き込み商談 |
| オポチュニティの役割を同期 | 商談 | POST | /rest/v1/opportunities/roles.json | 読み取り／書き込み商談 |
| 商談フィールドを名前で取得 | 商談 | GET | /rest/v1/opportunities/schema/fields/{fieldApiName}.json | 読み取り/書き込みスキーマカスタムフィールド |
| 商談フィールドを取得 | 商談 | GET | /rest/v1/opportunities/schema/fields.json | 読み取り/書き込みスキーマカスタムフィールド |
| プログラムメンバーの削除 | プログラムメンバー | POST | /rest/v1/programs/{programId}/members/delete.json | リード読み取り/書き込み可 |
| プログラムメンバーの説明 | プログラムメンバー | GET | /rest/v1/programs/members/describe.json | リード読み取り可 |
| プログラムメンバーの取得 | プログラムメンバー | GET | /rest/v1/programs/{programId}/members.json | リード読み取り可 |
| プログラムメンバーデータの同期 | プログラムメンバー | POST | /rest/v1/programs/{programId}/members.json | リード読み取り/書き込み可 |
| プログラムメンバーステータスを同期 | プログラムメンバー | POST | /rest/v1/programs/{programId}/members/status.json | リード読み取り/書き込み可 |
| 名前によるプログラムメンバーフィールドの取得 | プログラムメンバー | GET | /rest/v1/programs/members/schema/fields/{fieldApiName}.json | 読み取り/書き込みスキーマカスタムフィールド |
| プログラムメンバーフィールドを取得 | プログラムメンバー | GET | /rest/v1/programs/members/schema/fields.json | 読み取り/書き込みスキーマカスタムフィールド |
| プログラムメンバーフィールドの作成 | プログラムメンバー | POST | /rest/v1/programs/members/schema/fields.json | 読み取り/書き込みスキーマカスタムフィールド |
| プログラムメンバーフィールドを更新 | プログラムメンバー | POST | /rest/v1/programs/members/schema/fields/{fieldApiName}.json | 読み取り/書き込みスキーマカスタムフィールド |
| プログラムの承認 | プログラム | POST | /rest/asset/v1/program/{id}/approve.json | 読み取り/書き込みアセット |
| プログラムの複製 | プログラム | POST | /rest/asset/v1/program/{id}/clone.json | 読み取り/書き込みアセット |
| プログラムの作成 | プログラム | POST | /rest/asset/v1/programs.json | 読み取り/書き込みアセット |
| プログラムの削除 | プログラム | POST | /rest/asset/v1/program/{id}/delete.json | 読み取り/書き込みアセット |
| プログラムを ID で取得 | プログラム | GET | /rest/asset/v1/program/{id}.json | 読み取り専用資産 |
| 名前によるプログラムの取得 | プログラム | GET | /rest/asset/v1/program/byName.json | 読み取り専用資産 |
| プログラムの取得 | プログラム | GET | /rest/asset/v1/programs.json | 読み取り専用資産 |
| タグ別プログラムの取得 | プログラム | GET | /rest/asset/v1/program/byTag.json | 読み取り専用資産 |
| プログラム ID によるスマートリストの取得 | プログラム | GET | /rest/asset/v1/program/{id}/smartList.json | 読み取り専用資産 |
| プログラムの承認取消 | プログラム | POST | /rest/asset/v1/program/{id}/unapprove.json | 読み取り/書き込みアセット |
| プログラムメタデータの更新 | プログラム | POST | /rest/asset/v1/program/{id}.json | 読み取り/書き込みアセット |
| プログラム タグの更新 | プログラム | POST | /rest/asset/v1/program/{id}/tag/{tagType}.json | 読み取り/書き込みアセット |
| プログラム タグの削除 | プログラム | POST | /rest/asset/v1/program/{id}/tag/{tagType}/delete.json | 読み取り/書き込みアセット |
| 販売担当者の削除 | 販売担当者 | POST | /rest/v1/salespersons/delete.json | 読み取り／書き込みセールス担当者 |
| 営業担当者の説明 | 販売担当者 | GET | /rest/v1/salespersons/describe.json | セールス担当者読み取り可 |
| 販売担当者の取得 | 販売担当者 | GET | /rest/v1/salespersons.json | セールス担当者読み取り可 |
| 営業担当者の同期 | 販売担当者 | POST | /rest/v1/salespersons.json | 読み取り／書き込みセールス担当者 |
| セグメント化を取得 | セグメント | GET | /rest/asset/v1/segmentation.json | 読み取り専用資産 |
| セグメント化するセグメントの取得 | セグメント | GET | /rest/asset/v1/segmentation/{id}/segments.json | 読み取り専用資産 |
| スマート キャンペーンの有効化 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}/activate.json | キャンペーンを有効化 |
| スマート キャンペーンの複製 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}/clone.json | 読み取り/書き込みアセット |
| スマートキャンペーンの作成 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaigns.json | 読み取り/書き込みアセット |
| スマートキャンペーンを非アクティブ化 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}/deactivate.json | キャンペーンを無効化 |
| スマートキャンペーンの削除 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}/delete.json | 読み取り/書き込みアセット |
| スマートキャンペーンの取得 | スマートキャンペーン | GET | /rest/asset/v1/smartCampaigns.json | 読み取り専用資産 |
| ID によるスマートキャンペーンの取得 | スマートキャンペーン | GET | /rest/asset/v1/smartCampaign/{id}.json | 読み取り専用資産 |
| 名前によるスマートキャンペーンの取得 | スマートキャンペーン | GET | /rest/asset/v1/smartCampaign/byName.json | 読み取り専用資産 |
| スマートキャンペーン ID によるスマートリストの取得 | スマートキャンペーン | GET | /rest/asset/v1/smartCampaign/{id}/smartList.json | 読み取り専用資産 |
| スマートキャンペーンを更新 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}.json | 読み取り/書き込みアセット |
| スマート リストの複製 | スマートリスト | POST | /rest/asset/v1/smartList/{id}/clone.json | 読み取り/書き込みアセット |
| スマート リストの削除 | スマートリスト | POST | /rest/asset/v1/smartList/{id}/delete.json | 読み取り/書き込みアセット |
| ID によるスマートリストの取得 | スマートリスト | GET | /rest/asset/v1/smartList/{id}.json | 読み取り専用資産 |
| 名前によるスマート・リストの取得 | スマートリスト | GET | /rest/asset/v1/smartList/byName.json | 読み取り専用資産 |
| スマート・リストの取得 | スマートリスト | GET | /rest/asset/v1/smartLists.json | 読み取り専用資産 |
| スニペットドラフトを承認 | スニペット | POST | /rest/asset/v1/snippet/{id}/approveDraft.json | 読み取り/書き込みアセット |
| スニペットの複製 | スニペット | POST | /rest/asset/v1/snippet/{id}/clone.json | 読み取り/書き込みアセット |
| スニペットを作成 | スニペット | POST | /rest/asset/v1/snippets.json | 読み取り/書き込みアセット |
| スニペットの削除 | スニペット | POST | /rest/asset/v1/snippet/{id}/delete.json | 読み取り/書き込みアセット |
| スニペットドラフトの破棄 | スニペット | POST | /rest/asset/v1/snippet/{id}/discardDraft.json | 読み取り/書き込みアセット |
| 動的コンテンツの取得 | スニペット | GET | /rest/asset/v1/snippet/{id}/dynamicContent.json | 読み取り専用資産 |
| ID によるスニペットの取得 | スニペット | GET | /rest/asset/v1/snippet/{id}.json | 読み取り専用資産 |
| スニペットコンテンツの取得 | スニペット | GET | /rest/asset/v1/snippet/{id}/content.json | 読み取り専用資産 |
| スニペットの取得 | スニペット | GET | /rest/asset/v1/snippets.json | 読み取り専用資産 |
| スニペットの承認取消 | スニペット | POST | /rest/asset/v1/snippet/{id}/unapprove.json | 読み取り/書き込みアセット |
| スニペットコンテンツの更新 | スニペット | POST | /rest/asset/v1/snippet/{id}/content.json | 読み取り/書き込みアセット |
| スニペットの動的コンテンツの更新 | スニペット | POST | /rest/asset/v1/snippet/{id}/dynamicContent/{segmentId}.json | 読み取り/書き込みアセット |
| スニペットメタデータの更新 | スニペット | POST | /rest/asset/v1/snippet/{id}.json | 読み取り/書き込みアセット |
| リストに追加 | 静的リスト | POST | /rest/v1/lists/{listId}/leads.json | リード読み取り/書き込み可 |
| 静的リストの作成 | 静的リスト | POST | /asset/v1/staticLists.json | 読み取り/書き込みアセット |
| 静的リストの削除 | 静的リスト | POST | /asset/v1/staticList/{id}/delete.json | 読み取り/書き込みアセット |
| リスト ID 別のリードの取得 | 静的リスト | GET | /rest/v1/lists/{listId}/leads.json | リード読み取り可 |
| ID によるリストの取得 | 静的リスト | GET | /rest/v1/lists/{id}.json | リード読み取り可 |
| リストの取得 | 静的リスト | GET | /rest/v1/lists.json | リード読み取り可 |
| ID による静的リストの取得 | 静的リスト | GET | /asset/v1/staticList/{id}.json | 読み取り専用資産 |
| 名前による静的リストの取得 | 静的リスト | GET | /asset/v1/staticList/byName.json | 読み取り専用資産 |
| 静的リストの取得 | 静的リスト | GET | /asset/v1/staticLists.json | 読み取り専用資産 |
| リストのメンバー | 静的リスト | GET | /rest/v1/lists/{listId}/leads/ismember.json | リード読み取り可 |
| リストから削除 | 静的リスト | DELETE | /rest/v1/lists/{listId}/leads.json | リード読み取り/書き込み可 |
| 静的リストメタデータの更新 | 静的リスト | POST | /asset/v1/staticList/{id}.json | 読み取り/書き込みアセット |
| 名前でタグを取得 | タグ | GET | /rest/asset/v1/tagType/byName.json | 読み取り専用資産 |
| タグのタイプの取得 | タグ | GET | /rest/asset/v1/tagTypes.json | 読み取り専用資産 |
| トークンを作成 | トークン | POST | /rest/asset/v1/folder/{id}/tokens.json | 読み取り/書き込みアセット |
| 名前によるトークンの削除 | トークン | POST | /rest/asset/v1/folder/{id}/tokens/delete.json | 読み取り/書き込みアセット |
| フォルダー ID によるトークンの取得 | トークン | GET | /rest/asset/v1/folder/{id}/tokens.json | 読み取り専用資産 |
| 役割の追加 | ユーザ管理 | POST | /userservice/management/v1/users/{userid}/roles/create.json | ユーザー管理 API にアクセス |
| 招待ユーザーの削除 | ユーザ管理 | POST | /userservice/management/v1/users/{userId}/invite/delete.json | ユーザー管理 API にアクセス |
| 役割の削除 | ユーザ管理 | POST | /userservice/management/v1/users/{userid}/roles/delete.json | ユーザー管理 API にアクセス |
| ユーザの削除 | ユーザ管理 | POST | /userservice/management/v1/users/{userId}/delete.json | ユーザー管理 API にアクセス |
| Id で招待ユーザーを取得 | ユーザ管理 | GET | /userservice/management/v1/users/{userid}/invite.json | ユーザー管理 API にアクセス |
| 役割の取得 | ユーザ管理 | GET | /userservice/management/v1/users/roles.json | ユーザー管理 API にアクセス |
| Id による役割とワークスペースの取得 | ユーザ管理 | GET | /userservice/management/v1/users/{userid}/roles.json | ユーザー管理 API にアクセス |
| ユーザーの取得 | ユーザ管理 | GET | /userservice/management/v1/users/allusers.json | ユーザー管理 API にアクセス |
| Id によるユーザーの取得 | ユーザ管理 | GET | /userservice/management/v1/users/{userid}/user.json | ユーザー管理 API にアクセス |
| ワークスペースを取得 | ユーザ管理 | GET | /userservice/management/v1/users/workspaces.json | ユーザー管理 API にアクセス |
| ユーザーの招待 | ユーザ管理 | POST | /userservice/management/v1/users/invite.json | ユーザー管理 API にアクセス |
| ユーザー属性の更新 | ユーザ管理 | POST | /userservice/management/v1/users/{userId}/update.json | ユーザー管理 API にアクセス |