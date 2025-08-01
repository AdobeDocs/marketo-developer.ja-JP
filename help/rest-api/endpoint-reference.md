---
title: エンドポイント参照
feature: REST API
description: Marketo API エンドポイント参照
exl-id: 27d16b6f-865a-4e40-ab9c-cbabe2927472
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '4448'
ht-degree: 76%

---

# エンドポイント参照

Marketo REST API 参照へのリンクを以下に示します。

- [アセット](https://developer.adobe.com/marketo-apis/api/asset/)
- [ID](https://developer.adobe.com/marketo-apis/api/identity/)
- [リードデータベース](https://developer.adobe.com/marketo-apis/api/mapi/)
- [ユーザー管理](https://developer.adobe.com/marketo-apis/api/user/)

## エンドポイントリスト {#endpoint_list}

REST API エンドポイントの包括的なリストを以下に示します。

| 名前 | グループ | メソッド | URI | 必須の権限 |
|---|---|---|---|---|
| カスタムアクティビティの追加 | アクティビティ | POST | /rest/v1/activities/external.json | 読み取り／書き込みアクティビティ |
| カスタムアクティビティタイプを承認 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/approve.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプの属性を作成 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/attributes/create.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプを作成 | アクティビティ | POST | /rest/v1/activities/external/type.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプを削除 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/delete.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプの属性を削除 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/attributes/delete.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプを説明 | アクティビティ | GET | /rest/v1/activities/external/type/{apiName}/describe.json | 読み取り専用アクティビティメタデータ |
| カスタムアクティビティタイプのドラフトを破棄 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/discardDraft.json | 読み取り／書き込みアクティビティメタデータ |
| アクティビティタイプの取得 | アクティビティ | GET | /rest/v1/activities/types.json | 読み取り専用アクティビティ |
| カスタムアクティビティタイプを取得 | アクティビティ | GET | /rest/v1/activities/external/types.json | 読み取り専用アクティビティメタデータ |
| 削除済みリードの取得 | アクティビティ | GET | /rest/v1/activities/deletedleads.json | 読み取り専用アクティビティ |
| リードアクティビティの取得 | アクティビティ | GET | /rest/v1/activities.json | 読み取り専用アクティビティ |
| リードの変更の取得 | アクティビティ | GET | /rest/v1/activities/leadchanges.json | 読み取り専用アクティビティ |
| ページトークンの取得 | アクティビティ | GET | /rest/v1/activities/pagingtoken.json | 読み取り専用アクティビティ |
| カスタムアクティビティタイプを更新 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}.json | 読み取り／書き込みアクティビティメタデータ |
| カスタムアクティビティタイプの属性を更新 | アクティビティ | POST | /rest/v1/activities/external/type/{apiName}/attributes/update.json | 読み取り／書き込みアクティビティメタデータ |
| ID | 認証 | GET または POST | /identity/oauth/token | None |
| アクティビティを書き出しジョブをキャンセル | アクティビティを一括書き出し | POST | /bulk/v1/activities/export/{exportid}/cancel.json | 読み取り専用アクティビティ |
| アクティビティを書き出しジョブを作成 | アクティビティを一括書き出し | POST | /bulk/v1/activities/export/create.json | 読み取り専用アクティビティ |
| アクティビティを書き出しジョブをキューに入れる | アクティビティを一括書き出し | POST | /bulk/v1/activities/export/{exportid}/enqueue.json | 読み取り専用アクティビティ |
| アクティビティを書き出しファイルを取得 | アクティビティを一括書き出し | GET | /bulk/v1/activities/export/{exportid}/file.json | 読み取り専用アクティビティ |
| アクティビティを書き出しジョブステータスを取得 | アクティビティを一括書き出し | GET | /bulk/v1/activities/export/{exportid}/status.json | 読み取り専用アクティビティ |
| アクティビティを書き出しジョブを取得 | アクティビティを一括書き出し | GET | /bulk/v1/activities/export.json | 読み取り専用アクティビティ |
| カスタムオブジェクトを書き出しジョブをキャンセル | カスタムオブジェクトを一括書き出し | POST | /bulk/v1/customobjects/export/{exportid}/cancel.json | 読み取り専用カスタムオブジェクト |
| カスタムオブジェクトを書き出しジョブを作成 | カスタムオブジェクトを一括書き出し | POST | /bulk/v1/customobjects/export/create.json | 読み取り専用カスタムオブジェクト |
| カスタムオブジェクトを書き出しジョブをキューに入れる | カスタムオブジェクトを一括書き出し | POST | /bulk/v1/customobjects/export/{exportid}/enqueue.json | 読み取り専用カスタムオブジェクト |
| カスタムオブジェクトを書き出しファイルを取得 | カスタムオブジェクトを一括書き出し | GET | /bulk/v1/customobjects/export/{exportid}/file.json | 読み取り専用カスタムオブジェクト |
| カスタムオブジェクトを書き出しジョブステータスを取得 | カスタムオブジェクトを一括書き出し | GET | /bulk/v1/customobjects/export/{exportid}/status.json | 読み取り専用カスタムオブジェクト |
| カスタムオブジェクトを書き出しジョブを取得 | カスタムオブジェクトを一括書き出し | GET | /bulk/v1/customobjects/export.json | 読み取り専用カスタムオブジェクト |
| リードを書き出しジョブをキャンセル | リードを一括書き出し | POST | /bulk/v1/leads/export/{exportid}/cancel.json | 読み取り専用リード |
| リードを書き出しジョブを作成 | リードを一括書き出し | POST | /bulk/v1/leads/export/create.json | 読み取り専用リード |
| リードを書き出しジョブをキューに入れる | リードを一括書き出し | POST | /bulk/v1/leads/export/{exportid}/enqueue.json | 読み取り専用リード |
| リードを書き出しファイルを取得 | リードを一括書き出し | GET | /bulk/v1/leads/export/{exportid}/file.json | 読み取り専用リード |
| リードを書き出しジョブステータスを取得 | リードを一括書き出し | GET | /bulk/v1/leads/export/{exportid}/status.json | 読み取り専用リード |
| リードを書き出しジョブを取得 | リードを一括書き出し | GET | /bulk/v1/leads/export.json | 読み取り専用リード |
| プログラムメンバーを書き出しジョブをキャンセル | プログラムメンバーを一括書き出し | POST | /bulk/v1/program/members/export/{exportid}/cancel.json | 読み取り専用リード |
| プログラムメンバーを書き出しジョブを作成 | プログラムメンバーを一括書き出し | POST | /bulk/v1/program/members/export/create.json | 読み取り専用リード |
| プログラムメンバーを書き出しジョブをキューに入れる | プログラムメンバーを一括書き出し | POST | /bulk/v1/program/members/export/{exportid}/enqueue.json | 読み取り専用リード |
| プログラムメンバーを書き出しファイルを取得 | プログラムメンバーを一括書き出し | GET | /bulk/v1/program/members/export/{exportid}/file.json | 読み取り専用リード |
| プログラムメンバーを書き出しジョブステータスを取得 | プログラムメンバーを一括書き出し | GET | /bulk/v1/program/members/export/{exportid}/status.json | 読み取り専用リード |
| プログラムメンバーを書き出しジョブを取得 | プログラムメンバーを一括書き出し | GET | /bulk/v1/program/members/export.json | 読み取り専用リード |
| カスタムオブジェクトを読み込み失敗を取得 | カスタムオブジェクトを一括読み込み | GET | /bulk/v1/customobjects/import/{id}/failures.json | 読み取り／書き込みカスタムオブジェクト |
| カスタムオブジェクトを読み込みステータスを取得 | カスタムオブジェクトを一括読み込み | GET | /bulk/v1/customobjects/import/{id}/status.json | 読み取り／書き込みカスタムオブジェクト |
| カスタムオブジェクトを読み込み警告を取得 | カスタムオブジェクトを一括読み込み | GET | /bulk/v1/customobjects/import/{id}/warnings.json | 読み取り／書き込みカスタムオブジェクト |
| カスタムオブジェクトを読み込み | カスタムオブジェクトを一括読み込み | POST | /bulk/v1/customobjects/{apiName}/import.json | 読み取り／書き込みカスタムオブジェクト |
| リードを読み込み失敗を取得 | リードを一括読み込み | GET | /bulk/v1/leads/batch/{id}/failures.json | 読み取り／書き込みリード |
| リードを読み込みステータスを取得 | リードを一括読み込み | GET | /bulk/v1/leads/batch/{id}.json | 読み取り／書き込みリード |
| リードを読み込み警告を取得 | リードを一括読み込み | GET | /bulk/v1/leads/batch/{id}/warnings.json | 読み取り／書き込みリード |
| リードを読み込み | リードを一括読み込み | POST | /bulk/v1/leads.json | 読み取り／書き込みリード |
| プログラムメンバーを読み込み失敗を取得 | プログラムメンバーを一括読み込み | GET | /bulk/v1/program/members/import/{id}/failures.json | 読み取り／書き込みリード |
| プログラムメンバーを読み込みステータスを取得 | プログラムメンバーを一括読み込み | GET | /bulk/v1/program/members/import/{id}/status.json | 読み取り／書き込みリード |
| プログラムメンバーを読み込み警告を取得 | プログラムメンバーを一括読み込み | GET | /bulk/v1/program/members/import/{id}/warnings.json | 読み取り／書き込みリード |
| プログラムメンバーを読み込み | プログラムメンバーを一括読み込み | POST | /bulk/v1/program/{programId}/members/import.json | 読み取り／書き込みリード |
| ID によるキャンペーンを取得 | キャンペーン | GET | /rest/v1/campaigns/{id}.json | 読み取り専用キャンペーン |
| キャンペーンを取得 | キャンペーン | GET | /rest/v1/campaigns.json | 読み取り専用キャンペーン |
| キャンペーンをリクエスト | キャンペーン | POST | /rest/v1/campaigns/{id}/trigger.json | 読み取り／書き込みキャンペーン |
| キャンペーンをスケジュール | キャンペーン | POST | /rest/v1/campaigns/{id}/schedule.json | 読み取り／書き込みキャンペーン |
| 名前によるチャネルを取得 | チャネル | GET | /rest/asset/v1/channel/byName.json | 読み取り専用アセット |
| チャネルを取得 | チャネル | GET | /rest/asset/v1/channels.json | 読み取り専用アセット |
| 会社を削除 | 会社 | POST | /rest/v1/companies/delete.json | 読み取り／書き込み会社 |
| 会社を説明 | 会社 | GET | /rest/v1/companies/describe.json | 読み取り専用会社 |
| 会社を取得 | 会社 | GET | /rest/v1/companies.json | 読み取り専用会社 |
| 会社を同期 | 会社 | POST | /rest/v1/companies.json | 読み取り／書き込み会社 |
| 名前による会社フィールドを取得 | 会社 | GET | /rest/v1/companies/schema/fields/{fieldApiName}.json | 読み取り／書き込みスキーマカスタムフィールド |
| 会社フィールドを取得 | 会社 | GET | /rest/v1/companies/schema/fields.json | 読み取り／書き込みスキーマカスタムフィールド |
| カスタムオブジェクトタイプフィールドを追加 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/addField.json | 読み取り／書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトタイプを承認 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/approve.json | 読み取り／書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトを削除 | カスタムオブジェクト | POST | /rest/v1/customobjects/{name}/delete.json | 読み取り／書き込みカスタムオブジェクト |
| カスタムオブジェクトタイプを削除 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/delete.json | 読み取り／書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトタイプフィールドを削除 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/deleteField.json | 読み取り／書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトを説明 | カスタムオブジェクト | GET | /rest/v1/customobjects/{name}/describe.json | 読み取り専用カスタムオブジェクト |
| カスタムオブジェクトタイプを説明 | カスタムオブジェクト | GET | /rest/v1/customobjects/schema/{apiName}/describe.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタムオブジェクトタイプのドラフトを破棄 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/discardDraft.json | 読み取り／書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトを取得 | カスタムオブジェクト | GET | /rest/v1/customobjects/{name}.json | 読み取り専用カスタムオブジェクト |
| カスタムオブジェクトリンク可能オブジェクトを取得 | カスタムオブジェクト | GET | /rest/v1/customobjects/schema/linkableObjects.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタムオブジェクト依存アセットを取得 | カスタムオブジェクト | GET | /rest/v1/customobjects/schema/{apiName}/dependentAssets.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタムオブジェクトタイプフィールドデータタイプを取得 | カスタムオブジェクト | GET | /rest/v1/customobjects/schema/fieldDataTypes.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタムオブジェクトのリスト | カスタムオブジェクト | GET | /rest/v1/customobjects.json | 読み取り専用カスタムオブジェクト |
| カスタムオブジェクトタイプのリスト | カスタムオブジェクト | GET | /rest/v1/customobjects/schema.json | 読み取り専用カスタムオブジェクトタイプ |
| カスタムオブジェクトを同期 | カスタムオブジェクト | POST | /rest/v1/customobjects/{name}.json | 読み取り／書き込みカスタムオブジェクト |
| カスタムオブジェクトタイプを同期 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema.json | 読み取り／書き込みカスタムオブジェクトタイプ |
| カスタムオブジェクトタイプフィールドを更新 | カスタムオブジェクト | POST | /rest/v1/customobjects/schema/{apiName}/updateField.json | 読み取り／書き込みカスタムオブジェクトタイプ |
| メールテンプレートのドラフトを承認 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/approveDraft.json | 読み取り／書き込みアセット |
| メールテンプレートの複製 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/clone.json | 読み取り／書き込みアセット |
| メールテンプレートを作成 | メールテンプレート | POST | /rest/asset/v1/emailTemplates.json | 読み取り／書き込みアセット |
| メールテンプレートの削除 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/delete.json | 読み取り／書き込みアセット |
| メールテンプレートのドラフトを破棄 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/discardDraft.json | 読み取り／書き込みアセット |
| ID によるメールテンプレートを取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplate/{id}.json | 読み取り専用アセット |
| 名前によるメールテンプレートを取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplate/byName.json | 読み取り専用アセット |
| ID によるメールテンプレートコンテンツを取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplate/{id}/content.json | 読み取り専用アセット |
| 使用されるメールテンプレートを取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplates/{id}/usedBy.json | 読み取り専用アセット |
| メールテンプレートを取得 | メールテンプレート | GET | /rest/asset/v1/emailTemplates.json | 読み取り専用アセット |
| メールテンプレートのドラフトを未承認 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/unapprove.json | 読み取り／書き込みアセット |
| メールテンプレートコンテンツを更新 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}/content.json | 読み取り／書き込みアセット |
| メールテンプレートメタデータを更新 | メールテンプレート | POST | /rest/asset/v1/emailTemplate/{id}.json | 読み取り／書き込みアセット |
| メールモジュールを追加 | メール | POST | /rest/asset/v1/email/{id}/content/{moduleId}/add.json | 読み取り／書き込みアセット |
| メールのドラフトを承認 | メール | POST | /rest/asset/v1/email/{id}/approveDraft.json | 読み取り／書き込みアセット |
| メールの複製 | メール | POST | /rest/asset/v1/email/{id}/clone.json | 読み取り／書き込みアセット |
| メールを作成 | メール | POST | /rest/asset/v1/emails.json | 読み取り／書き込みアセット |
| メールの削除 | メール | POST | /rest/asset/v1/email/{id}/delete.json | 読み取り／書き込みアセット |
| モジュールを削除 | メール | POST | /rest/asset/v1/email/{id}/content/{moduleId}/delete.json | 読み取り／書き込みアセット |
| メールのドラフトを破棄 | メール | POST | /rest/asset/v1/email/{id}/discardDraft.json | 読み取り／書き込みアセット |
| メールモジュールを複製 | メール | POST | /rest/asset/v1/email/{id}/content/{moduleId}/duplicate.json | 読み取り／書き込みアセット |
| ID によるメールを取得 | メール | GET | /rest/asset/v1/email/{id}.json | 読み取り専用アセット |
| 名前によるメールを取得 | メール | GET | /rest/asset/v1/email/byName.json | 読み取り専用アセット |
| メールコンテンツを取得 | メール | GET | /rest/asset/v1/email/{id}/content.json | 読み取り専用アセット |
| メール動的コンテンツを取得 | メール | GET | /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json | 読み取り専用アセット |
| メールの完全なコンテンツを取得 | メール | GET | /rest/asset/v1/email/{id}/fullContent.json | 読み取り専用アセット |
| メール変数を取得 | メール | GET | /rest/asset/v1/email/{id}/variables.json | 読み取り専用アセット |
| メール CC フィールドを取得 | メール | GET | /rest/asset/v1/email/ccFields.json | 読み取り専用アセット |
| メールを取得 | メール | GET | /rest/asset/v1/emails.json | 読み取り専用アセット |
| メールモジュールを並べ替え | メール | POST | /rest/asset/v1/email/{id}/content/rearrange.json | 読み取り／書き込みアセット |
| メールモジュールを名前変更 | メール | POST | /rest/asset/v1/email/{id}/content/{moduleId}/rename.json | 読み取り／書き込みアセット |
| サンプルメールを送信 | メール | POST | /rest/asset/v1/email/{id}/sendSample.json | 読み取り／書き込みアセット |
| メールを未承認 | メール | POST | /rest/asset/v1/email/{id}/unapprove.json | 読み取り／書き込みアセット |
| メールコンテンツを更新 | メール | POST | /rest/asset/v1/email/{id}/content.json | 読み取り／書き込みアセット |
| メールコンテンツセクションを更新 | メール | POST | /rest/asset/v1/email/{id}/content/{htmlId}.json | 読み取り／書き込みアセット |
| メール動的コンテンツセクションを更新 | メール | POST | /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json | 読み取り／書き込みアセット |
| メールの完全なコンテンツを更新 | メール | POST | /rest/asset/v1/emails/{id}/fullContent.json | 読み取り／書き込みアセット |
| メールメタデータを更新 | メール | POST | /rest/asset/v1/email/{id}.json | 読み取り／書き込みアセット |
| メール変数を更新 | メール | POST | /rest/asset/v1/email/{id}/variable/{name}.json | 読み取り／書き込みアセット |
| ファイルを作成 | ファイル | POST | /rest/asset/v1/files.json | 読み取り／書き込みアセット |
| ID によるファイルを取得 | ファイル | GET | /rest/asset/v1/file/{id}.json | 読み取り専用アセット |
| 名前によるファイルを取得 | ファイル | GET | /rest/asset/v1/file/byName.json | 読み取り専用アセット |
| ファイルを取得 | ファイル | GET | /rest/asset/v1/files.json | 読み取り専用アセット |
| ファイルコンテンツを更新 | ファイル | POST | /rest/asset/v1/file/{id}/content.json | 読み取り／書き込みアセット |
| フォルダーを作成 | フォルダー | POST | /rest/asset/v1/folders.json | 読み取り／書き込みアセット |
| フォルダーを削除 | フォルダー | POST | /rest/asset/v1/folder/{id}/delete.json | 読み取り／書き込みアセット |
| ID によるフォルダーを取得 | フォルダー | GET | /rest/asset/v1/folder/{id}.json | 読み取り専用アセット |
| 名前によるフォルダーを取得 | フォルダー | GET | /rest/asset/v1/folder/byName.json | 読み取り専用アセット |
| フォルダーコンテンツを取得 | フォルダー | GET | /rest/asset/v1/folder/{id}/content.json | 読み取り専用アセット |
| フォルダーを取得 | フォルダー | GET | /rest/asset/v1/folders.json | 読み取り専用アセット |
| フォルダーメタデータを更新 | フォルダー | POST | /rest/asset/v1/folder/{id}.json | 読み取り／書き込みアセット |
| フォームにフィールドを追加 | フォームフィールド | POST | /rest/asset/v1/form/{id}/fields.json | 読み取り／書き込みアセット |
| フォームにフィールドセットを追加 | フォームフィールド | POST | /rest/asset/v1/form/{id}/fieldSet.json | 読み取り／書き込みアセット |
| フォームフィールド表示ルールを追加 | フォームフィールド | POST | /rest/asset/v1/form/{formId}/field/{fieldId}/visibility.json | 読み取り／書き込みアセット |
| リッチテキストフィールドを追加 | フォームフィールド | POST | /rest/asset/v1/form/{id}/richText.json | 読み取り／書き込みアセット |
| フィールドセットからフィールドを削除 | フォームフィールド | POST | /rest/asset/v1/form/{id}/fieldSet/{fieldSetId}/field/{fieldId}/delete.json | 読み取り／書き込みアセット |
| フォームフィールドを削除 | フォームフィールド | POST | /rest/asset/v1/form/{id}/field/{fieldId}/delete.json | 読み取り／書き込みアセット |
| 使用可能なフォームフィールドを取得 | フォームフィールド | GET | /rest/asset/v1/form/fields.json | 読み取り専用アセット |
| 使用可能なフォームプログラムメンバーフィールドを取得 | フォームフィールド | GET | /rest/asset/v1/form/programMemberFields.json | 読み取り専用アセット |
| フォームのフィールドを取得 | フォームフィールド | GET | /rest/asset/v1/form/{id}/fields.json | 読み取り専用アセット |
| フィールド位置を更新 | フォームフィールド | POST | /rest/asset/v1/form/{id}/reArrange.json | 読み取り／書き込みアセット |
| フォームフィールドを更新 | フォームフィールド | POST | /rest/asset/v1/form/{id}/field/{fieldId}.json | 読み取り／書き込みアセット |
| フォームのドラフトを承認 | フォーム | POST | /rest/asset/v1/form/{id}/approveDraft.json | 読み取り／書き込みアセット |
| フォームを複製 | フォーム | POST | /rest/asset/v1/form/{id}/clone.json | 読み取り／書き込みアセット |
| フォームを作成 | フォーム | POST | /rest/asset/v1/forms.json | 読み取り／書き込みアセット |
| 使用されるフォームを取得 | フォーム | GET | /rest/asset/v1/form/{id}/usedBy.json | 読み取り／書き込みアセット |
| フォームを削除 | フォーム | POST | /rest/asset/v1/form/{id}/delete.json | 読み取り／書き込みアセット |
| フォームのドラフトを破棄 | フォーム | POST | /rest/asset/v1/form/{id}/discardDraft.json | 読み取り／書き込みアセット |
| ID によるフォームを取得 | フォーム | GET | /rest/asset/v1/form/{id}.json | 読み取り専用アセット |
| 名前によるフォームを取得 | フォーム | GET | /rest/asset/v1/form/byName.json | 読み取り専用アセット |
| フォームを取得 | フォーム | GET | /rest/asset/v1/forms.json | 読み取り専用アセット |
| フォーム ID によるサンキューページを取得 | フォーム | GET | /rest/asset/v1/form/{id}/thankYouPage.json | 読み取り専用アセット |
| フォームメタデータを更新 | フォーム | POST | /rest/asset/v1/form/{id}.json | 読み取り／書き込みアセット |
| 送信ボタンを更新 | フォーム | POST | /rest/asset/v1/{id}/submitButton.json | 読み取り／書き込みアセット |
| サンキューページを更新 | フォーム | POST | /rest/asset/v1/form/{id}/thankYouPage.json | 読み取り／書き込みアセット |
| ランディングページコンテンツセクションを追加 | ランディングページコンテンツ | POST | /rest/asset/v1/landingPage/{id}/content.json | 読み取り／書き込みアセット |
| ランディングページコンテンツセクションを削除 | ランディングページコンテンツ | POST | /rest/asset/v1/landingPage/{id}/content/{contentId}/delete.json | 読み取り／書き込みアセット |
| ランディングページコンテンツを取得 | ランディングページコンテンツ | GET | /rest/asset/v1/landingPage/{id}/content.json | 読み取り専用アセット |
| ランディングページ動的コンテンツを取得 | ランディングページコンテンツ | GET | /rest/asset/v1/landingPage/{id}/dynamicContent/{dynamicContentId}.json | 読み取り専用アセット |
| ランディングページコンテンツセクションを更新 | ランディングページコンテンツ | POST | /rest/asset/v1/landingPage/{id}/content/{contentId}.json | 読み取り／書き込みアセット |
| ランディングページ動的コンテンツセクションを更新 | ランディングページコンテンツ | POST | /rest/asset/v1/landingPage/{id}/dynamicContent/{dynamicContentId}.json | 読み取り／書き込みアセット |
| ランディングページテンプレートのドラフトを承認 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/approveDraft.json | 読み取り／書き込みアセット |
| ランディングページテンプレートを複製 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/clone.json | 読み取り／書き込みアセット |
| ランディングページテンプレートを作成 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate.json | 読み取り／書き込みアセット |
| ランディングページテンプレートを削除 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/delete.json | 読み取り／書き込みアセット |
| ランディングページテンプレートのドラフトを破棄 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/discardDraft.json | 読み取り／書き込みアセット |
| ID によるランディングページテンプレートを取得 | ランディングページのテンプレート | GET | /rest/asset/v1/landingPageTemplate/{id}.json | 読み取り専用アセット |
| 名前によるランディングページテンプレートを取得 | ランディングページのテンプレート | GET | /rest/asset/v1/landingPageTemplates/byName.json | 読み取り専用アセット |
| ランディングページテンプレートコンテンツを取得 | ランディングページのテンプレート | GET | /rest/asset/v1/landingPageTemplate/{id}/content.json | 読み取り専用アセット |
| ランディングページテンプレートを取得 | ランディングページのテンプレート | GET | /rest/asset/v1/landingPageTemplates.json | 読み取り専用アセット |
| ランディングページテンプレートを承認取消 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/unapprove.json | 読み取り／書き込みアセット |
| ランディングページテンプレートコンテンツを更新 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}/content.json | 読み取り／書き込みアセット |
| ランディングページテンプレートメタデータを更新 | ランディングページのテンプレート | POST | /rest/asset/v1/landingPageTemplate/{id}.json | 読み取り／書き込みアセット |
| ランディングページのドラフトを承認 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/approveDraft.json | 読み取り／書き込みアセット |
| ランディングページを複製 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/clone.json | 読み取り／書き込みアセット |
| ランディングページを作成 | ランディングページ | POST | /rest/asset/v1/landingPages.json | 読み取り／書き込みアセット |
| ランディングページを削除 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/delete.json | 読み取り／書き込みアセット |
| ランディングページのドラフトを破棄 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/discardDraft.json | 読み取り／書き込みアセット |
| ID によるランディングページを取得 | ランディングページ | GET | /rest/asset/v1/landingPage/{id}.json | 読み取り専用アセット |
| 名前によるランディングページを取得 | ランディングページ | GET | /rest/asset/v1/landingPage/byName.json | 読み取り専用アセット |
| ランディングページ変数を取得 | ランディングページ | GET | /rest/asset/v1/landingPage/{id}/variables.json | 読み取り専用アセット |
| ランディングページを取得 | ランディングページ | GET | /rest/asset/v1/landingPages.json | 読み取り専用アセット |
| ランディングページのプレビュー | ランディングページ | GET | /rest/asset/v1/landingPage/{id}/preview.json | 読み取り専用アセット |
| ランディングページを承認取消 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/unapprove.json | 読み取り／書き込みアセット |
| ランディングページメタデータを更新 | ランディングページ | POST | /rest/asset/v1/{id}.json | 読み取り／書き込みアセット |
| ランディングページ変数を更新 | ランディングページ | POST | /rest/asset/v1/landingPage/{id}/variable/{variableId}.json | 読み取り／書き込みアセット |
| ランディングページのリダイレクトルールを作成 | ランディングページ | POST | /rest/asset/v1/redirectRules.json | 読み取り／書き込みリダイレクトルール |
| ランディングページのリダイレクトルールを削除 | ランディングページ | POST | /rest/asset/v1/redirectRule/{id}/delete.json | 読み取り／書き込みリダイレクトルール |
| ランディングページのリダイレクトルールを取得 | ランディングページ | GET | /rest/asset/v1/redirectRules.json | 読み取り専用リダイレクトルール |
| ID によるランディングページのリダイレクトルールを取得 | ランディングページ | GET | /rest/asset/v1/redirectRule/{id}.json | 読み取り専用リダイレクトルール |
| ランディングページのリダイレクトルールを更新 | ランディングページ | POST | /rest/asset/v1/redirectRule/{id}.json | 読み取り／書き込みリダイレクトルール |
| ランディングページのドメインを取得 | ランディングページ | GET | /rest/asset/v1/landingPageDomains.json | 読み取り専用リダイレクトルール |
| リードを関連付け | リード | POST | /rest/v1/leads/{id}/associate.json | 読み取り／書き込みリード |
| リードのプログラムステータスを変更 | リード | POST | /rest/v1/leads/programs/{programId}/status.json | 読み取り／書き込みリード |
| リードを削除 | リード | POST | /rest/v1/leads.json | 読み取り／書き込みリード |
| リードを説明 | リード | GET | /rest/v1/leads/describe.json | 読み取り専用リード |
| リード 2 を説明 | リード | GET | /rest/v1/leads/describe2.json | 読み取り専用リード |
| プログラムメンバーを説明 | リード | GET | /rest/v1/program/members/describe.json | 読み取り専用リード |
| ID によるリードを取得 | リード | GET | /rest/v1/lead/{id}.json | 読み取り専用リード |
| リードパーティションを取得 | リード | GET | /rest/v1/leads/partitions.json | 読み取り専用リード |
| フィルタータイプによるリードを取得 | リード | GET | /rest/v1/leads.json | 読み取り専用リード |
| プログラム ID でリードを取得 | リード | GET | /rest/v1/leads/programs/{programId}.json | 読み取り専用リード |
| リードを結合 | リード | POST | /rest/v1/leads/{id}/merge.json | 読み取り／書き込みリード |
| リード ID によるリストを取得 | リード | GET | /rest/v1/leads/{leadId}.json | 読み取り専用アセット |
| リード ID によるプログラムを取得 | リード | GET | /rest/v1/leads/{leadId}programMembership.json | 読み取り専用アセット |
| リード ID によるスマートキャンペーンを取得 | リード | GET | /rest/v1/leads/{leadId}/smartCampaignMembership.json | 読み取り専用アセット |
| Marketo にリードをプッシュ | リード | POST | /rest/v1/leads/partitions.json | 読み取り／書き込みリード |
| フォームを送信 | リード | POST | /rest/v1/leads/submitForm.json | 読み取り／書き込みリード |
| リードを同期 | リード | POST | /rest/v1/leads.json | 読み取り／書き込みリード |
| リードパーティションを更新 | リード | POST | /rest/v1/leads/partitions.json | 読み取り／書き込みリード |
| 名前によるリードフィールドを取得 | リード | GET | /rest/v1/leads/schema/fields/{fieldApiName}.json | 読み取り／書き込みスキーマカスタムフィールド |
| リードフィールドを取得 | リード | GET | /rest/v1/leads/schema/fields.json | 読み取り／書き込みスキーマカスタムフィールド |
| リードフィールドを作成 | リード | POST | /rest/v1/leads/schema/fields.json | 読み取り／書き込みスキーマカスタムフィールド |
| リードフィールドを更新 | リード | POST | /rest/v1/leads/schema/fields/{fieldApiName}.json | 読み取り／書き込みスキーマカスタムフィールド |
| 名前付きアカウントリストメンバーを追加 | 重点顧客リスト | POST | /rest/v1/namedaccountlist/{id}/namedaccounts.json | 読み取り／書き込み名前付きアカウント |
| 名前付きアカウントリストを削除 | 重点顧客リスト | POST | /rest/v1/namedaccountlists/delete.json | 読み取り／書き込み名前付きアカウントリスト |
| 名前付きアカウントリストメンバーを取得 | 重点顧客リスト | GET | /rest/v1/namedaccountlist/{id}/namedaccounts.json | 読み取り専用名前付きアカウント |
| 名前付きアカウントリストを取得 | 重点顧客リスト | GET | /rest/v1/namedaccountlists.json | 読み取り専用名前付きアカウントリスト |
| 名前付きアカウントリストメンバーを削除 | 重点顧客リスト | POST | /rest/v1/namedaccountlist/{id}/namedaccounts/remove.json | 読み取り／書き込み名前付きアカウント |
| 名前付きアカウントリストを同期 | 重点顧客リスト | POST | /rest/v1/namedaccountlists.json | 読み取り／書き込み名前付きアカウントリスト |
| 名前付きアカウントを削除 | 重点顧客 | POST | /rest/v1/namedaccounts/delete.json | 読み取り／書き込み名前付きアカウント |
| 名前付きアカウントを説明 | 重点顧客 | GET | /rest/v1/namedaccounts/describe.json | 読み取り専用名前付きアカウント |
| 名前付きアカウントを取得 | 重点顧客 | GET | /rest/v1/namedaccounts.json | 読み取り専用名前付きアカウント |
| 名前付きアカウントを同期 | 重点顧客 | POST | /rest/v1/namedaccounts.json | 読み取り／書き込み名前付きアカウント |
| 名前による名前付きアカウントフィールドを取得 | 重点顧客 | GET | /rest/v1/namedaccounts/schema/fields/{fieldApiName}.json | 読み取り／書き込みスキーマカスタムフィールド |
| 名前付きアカウントフィールドを取得 | 重点顧客 | GET | /rest/v1/namedaccounts/schema/fields.json | 読み取り／書き込みスキーマカスタムフィールド |
| 商談を削除 | 商談 | POST | /rest/v1/opportunities/delete.json | 読み取り／書き込み商談 |
| 商談ロールを削除 | 商談 | POST | /rest/v1/opportunities/roles/delete.json | 読み取り／書き込み商談 |
| 商談を説明 | 商談 | GET | /rest/v1/opportunities/describe.json | 読み取り専用商談 |
| 商談ロールを説明 | 商談 | GET | /rest/v1/opportunities/roles/describe.json | 読み取り専用商談 |
| 商談を取得 | 商談 | GET | /rest/v1/opportunities.json | 読み取り専用商談 |
| 商談ロールを取得 | 商談 | GET | /rest/v1/opportunities/roles.json | 読み取り専用商談 |
| 商談を同期 | 商談 | POST | /rest/v1/opportunities.json | 読み取り／書き込み商談 |
| 商談ロールを同期 | 商談 | POST | /rest/v1/opportunities/roles.json | 読み取り／書き込み商談 |
| 名前による商談フィールドを取得 | 商談 | GET | /rest/v1/opportunities/schema/fields/{fieldApiName}.json | 読み取り／書き込みスキーマカスタムフィールド |
| 商談フィールドを取得 | 商談 | GET | /rest/v1/opportunities/schema/fields.json | 読み取り／書き込みスキーマカスタムフィールド |
| プログラムメンバーを削除 | プログラムメンバー | POST | /rest/v1/programs/{programId}/members/delete.json | 読み取り／書き込みリード |
| プログラムメンバーを説明 | プログラムメンバー | GET | /rest/v1/programs/members/describe.json | 読み取り専用リード |
| プログラムメンバーを取得 | プログラムメンバー | GET | /rest/v1/programs/{programId}/members.json | 読み取り専用リード |
| プログラムメンバーデータを同期 | プログラムメンバー | POST | /rest/v1/programs/{programId}/members.json | 読み取り／書き込みリード |
| プログラムメンバーステータスを同期 | プログラムメンバー | POST | /rest/v1/programs/{programId}/members/status.json | 読み取り／書き込みリード |
| 名前によるプログラムメンバーフィールドを取得 | プログラムメンバー | GET | /rest/v1/programs/members/schema/fields/{fieldApiName}.json | 読み取り／書き込みスキーマカスタムフィールド |
| プログラムメンバーフィールドを取得 | プログラムメンバー | GET | /rest/v1/programs/members/schema/fields.json | 読み取り／書き込みスキーマカスタムフィールド |
| プログラムメンバーフィールドを作成 | プログラムメンバー | POST | /rest/v1/programs/members/schema/fields.json | 読み取り／書き込みスキーマカスタムフィールド |
| プログラムメンバーフィールドを更新 | プログラムメンバー | POST | /rest/v1/programs/members/schema/fields/{fieldApiName}.json | 読み取り／書き込みスキーマカスタムフィールド |
| プログラムを承認 | プログラム | POST | /rest/asset/v1/program/{id}/approve.json | 読み取り／書き込みアセット |
| プログラムを複製 | プログラム | POST | /rest/asset/v1/program/{id}/clone.json | 読み取り／書き込みアセット |
| プログラムを作成 | プログラム | POST | /rest/asset/v1/programs.json | 読み取り／書き込みアセット |
| プログラムの削除 | プログラム | POST | /rest/asset/v1/program/{id}/delete.json | 読み取り／書き込みアセット |
| ID によるプログラムを取得 | プログラム | GET | /rest/asset/v1/program/{id}.json | 読み取り専用アセット |
| 名前によるプログラムを取得 | プログラム | GET | /rest/asset/v1/program/byName.json | 読み取り専用アセット |
| プログラムを取得 | プログラム | GET | /rest/asset/v1/programs.json | 読み取り専用アセット |
| タグによるプログラムを取得 | プログラム | GET | /rest/asset/v1/program/byTag.json | 読み取り専用アセット |
| プログラム ID によるスマートリストを取得 | プログラム | GET | /rest/asset/v1/program/{id}/smartList.json | 読み取り専用アセット |
| プログラムを承認取消 | プログラム | POST | /rest/asset/v1/program/{id}/unapprove.json | 読み取り／書き込みアセット |
| プログラムメタデータを更新 | プログラム | POST | /rest/asset/v1/program/{id}.json | 読み取り／書き込みアセット |
| プログラムタグを更新 | プログラム | POST | /rest/asset/v1/program/{id}/tag/{tagType}.json | 読み取り／書き込みアセット |
| プログラムタグを削除 | プログラム | POST | /rest/asset/v1/program/{id}/tag/{tagType}/delete.json | 読み取り／書き込みアセット |
| セールス担当者を削除 | セールス担当者 | POST | /rest/v1/salespersons/delete.json | 読み取り／書き込みセールス担当者 |
| セールス担当者を説明 | セールス担当者 | GET | /rest/v1/salespersons/describe.json | 読み取り専用セールス担当者 |
| セールス担当者を取得 | セールス担当者 | GET | /rest/v1/salespersons.json | 読み取り専用セールス担当者 |
| セールス担当者を同期 | セールス担当者 | POST | /rest/v1/salespersons.json | 読み取り／書き込みセールス担当者 |
| セグメント化を取得 | セグメント | GET | /rest/asset/v1/segmentation.json | 読み取り専用アセット |
| セグメント化のセグメントを取得 | セグメント | GET | /rest/asset/v1/segmentation/{id}/segments.json | 読み取り専用アセット |
| スマートキャンペーンをアクティブ化 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}/activate.json | キャンペーンをアクティブ化 |
| スマートキャンペーンを複製 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}/clone.json | 読み取り／書き込みアセット |
| スマートキャンペーンを作成 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaigns.json | 読み取り／書き込みアセット |
| スマートキャンペーンを非アクティブ化 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}/deactivate.json | キャンペーンを非アクティブ化 |
| スマートキャンペーンを削除 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}/delete.json | 読み取り／書き込みアセット |
| スマートキャンペーンを取得 | スマートキャンペーン | GET | /rest/asset/v1/smartCampaigns.json | 読み取り専用アセット |
| ID によるスマートキャンペーンを取得 | スマートキャンペーン | GET | /rest/asset/v1/smartCampaign/{id}.json | 読み取り専用アセット |
| 名前によるスマートキャンペーンを取得 | スマートキャンペーン | GET | /rest/asset/v1/smartCampaign/byName.json | 読み取り専用アセット |
| スマートキャンペーン ID によるスマートリストを取得 | スマートキャンペーン | GET | /rest/asset/v1/smartCampaign/{id}/smartList.json | 読み取り専用アセット |
| スマートキャンペーンを更新 | スマートキャンペーン | POST | /rest/asset/v1/smartCampaign/{id}.json | 読み取り／書き込みアセット |
| スマートリストを複製 | スマートリスト | POST | /rest/asset/v1/smartList/{id}/clone.json | 読み取り／書き込みアセット |
| スマートリストを削除 | スマートリスト | POST | /rest/asset/v1/smartList/{id}/delete.json | 読み取り／書き込みアセット |
| ID によるスマートリストを取得 | スマートリスト | GET | /rest/asset/v1/smartList/{id}.json | 読み取り専用アセット |
| 名前によるスマートリストを取得 | スマートリスト | GET | /rest/asset/v1/smartList/byName.json | 読み取り専用アセット |
| スマートリストを取得 | スマートリスト | GET | /rest/asset/v1/smartLists.json | 読み取り専用アセット |
| スニペットのドラフトを承認 | スニペット | POST | /rest/asset/v1/snippet/{id}/approveDraft.json | 読み取り／書き込みアセット |
| スニペットを複製 | スニペット | POST | /rest/asset/v1/snippet/{id}/clone.json | 読み取り／書き込みアセット |
| スニペットを作成 | スニペット | POST | /rest/asset/v1/snippets.json | 読み取り／書き込みアセット |
| スニペットを削除 | スニペット | POST | /rest/asset/v1/snippet/{id}/delete.json | 読み取り／書き込みアセット |
| スニペットのドラフトを破棄 | スニペット | POST | /rest/asset/v1/snippet/{id}/discardDraft.json | 読み取り／書き込みアセット |
| 動的コンテンツを取得 | スニペット | GET | /rest/asset/v1/snippet/{id}/dynamicContent.json | 読み取り専用アセット |
| ID によるスニペットを取得 | スニペット | GET | /rest/asset/v1/snippet/{id}.json | 読み取り専用アセット |
| スニペットコンテンツを取得 | スニペット | GET | /rest/asset/v1/snippet/{id}/content.json | 読み取り専用アセット |
| スニペットを取得 | スニペット | GET | /rest/asset/v1/snippets.json | 読み取り専用アセット |
| スニペットを承認取消 | スニペット | POST | /rest/asset/v1/snippet/{id}/unapprove.json | 読み取り／書き込みアセット |
| スニペットコンテンツを更新 | スニペット | POST | /rest/asset/v1/snippet/{id}/content.json | 読み取り／書き込みアセット |
| スニペット動的コンテンツを更新 | スニペット | POST | /rest/asset/v1/snippet/{id}/dynamicContent/{segmentId}.json | 読み取り／書き込みアセット |
| スニペットメタデータを更新 | スニペット | POST | /rest/asset/v1/snippet/{id}.json | 読み取り／書き込みアセット |
| リストに追加 | 静的リスト | POST | /rest/v1/lists/{listId}/leads.json | 読み取り／書き込みリード |
| 静的リストを作成 | 静的リスト | POST | /asset/v1/staticLists.json | 読み取り／書き込みアセット |
| 静的リストを削除 | 静的リスト | POST | /asset/v1/staticList/{id}/delete.json | 読み取り／書き込みアセット |
| リスト ID によるリードを取得 | 静的リスト | GET | /rest/v1/lists/{listId}/leads.json | 読み取り専用リード |
| ID によるリストを取得 | 静的リスト | GET | /rest/v1/lists/{id}.json | 読み取り専用リード |
| リストを取得 | 静的リスト | GET | /rest/v1/lists.json | 読み取り専用リード |
| ID による静的リストを取得 | 静的リスト | GET | /asset/v1/staticList/{id}.json | 読み取り専用アセット |
| 名前による静的リストを取得 | 静的リスト | GET | /asset/v1/staticList/byName.json | 読み取り専用アセット |
| 静的リストを取得 | 静的リスト | GET | /asset/v1/staticLists.json | 読み取り専用アセット |
| リストのメンバー | 静的リスト | GET | /rest/v1/lists/{listId}/leads/ismember.json | 読み取り専用リード |
| リストから削除 | 静的リスト | DELETE | /rest/v1/lists/{listId}/leads.json | 読み取り／書き込みリード |
| 静的リストメタデータを更新 | 静的リスト | POST | /asset/v1/staticList/{id}.json | 読み取り／書き込みアセット |
| 名前によるタグを取得 | タグ | GET | /rest/asset/v1/tagType/byName.json | 読み取り専用アセット |
| タグタイプを取得 | タグ | GET | /rest/asset/v1/tagTypes.json | 読み取り専用アセット |
| トークンを作成 | トークン | POST | /rest/asset/v1/folder/{id}/tokens.json | 読み取り／書き込みアセット |
| 名前によるトークンを削除 | トークン | POST | /rest/asset/v1/folder/{id}/tokens/delete.json | 読み取り／書き込みアセット |
| フォルダー ID によるトークンを取得 | トークン | GET | /rest/asset/v1/folder/{id}/tokens.json | 読み取り専用アセット |
| ロールの追加 | ユーザ管理 | POST | /userservice/management/v1/users/{userid}/roles/create.json | User Management API にアクセス |
| 招待されたユーザの削除 | ユーザ管理 | POST | /userservice/management/v1/users/{userId}/invite/delete.json | User Management API にアクセス |
| ロールの削除 | ユーザ管理 | POST | /userservice/management/v1/users/{userid}/roles/delete.json | User Management API にアクセス |
| ユーザの削除 | ユーザ管理 | POST | /userservice/management/v1/users/{userId}/delete.json | User Management API にアクセス |
| ID による招待されたユーザを取得 | ユーザ管理 | GET | /userservice/management/v1/users/{userid}/invite.json | User Management API にアクセス |
| ロールを取得 | ユーザ管理 | GET | /userservice/management/v1/users/roles.json | User Management API にアクセス |
| ID によるロールとワークスペースを取得 | ユーザ管理 | GET | /userservice/management/v1/users/{userid}/roles.json | User Management API にアクセス |
| ユーザを取得 | ユーザ管理 | GET | /userservice/management/v1/users/allusers.json | User Management API にアクセス |
| ID によるユーザを取得 | ユーザ管理 | GET | /userservice/management/v1/users/{userid}/user.json | User Management API にアクセス |
| ワークスペースを取得 | ユーザ管理 | GET | /userservice/management/v1/users/workspaces.json | User Management API にアクセス |
| ユーザの招待 | ユーザ管理 | POST | /userservice/management/v1/users/invite.json | User Management API にアクセス |
| ユーザ属性の更新 | ユーザ管理 | POST | /userservice/management/v1/users/{userId}/update.json | User Management API にアクセス |
