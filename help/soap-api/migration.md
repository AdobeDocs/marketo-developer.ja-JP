---
title: REST API への移行
feature: SOAP
description: SOAPから REST API への移行
source-git-commit: 8ad3e3f0958ea705375651b1c8a75967d807ca80
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 3%

---


# 概要

Marketo EngageSOAP API は、2025 年 10 月 31 日（PT）以降に廃止されます。 サービスの中断を避けるために、SOAP API を使用するすべての既存の統合は、この日までに廃止するか ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/rest-api)[Marketo Engage REST API} に移行する必要があります。

## 移行

SOAP API は、[REST AP](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/rest-api)I と比較して、限られた範囲のユースケースをサポートしています。ユースケースをマッピングするエンドポイントを決定する際は、[Marketo統合のベストプラクティスに従う必要があります ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/marketo-integration-best-practices)

[ リファレンスアーキテクチャ ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/reference-architectures) は、{CRM 同期 [ および ](https://experienceleague.adobe.com/docs/marketo-developer/assets/sync-architecture-whitepaper.pdf?lang=en)4}Data Warehouseエクスポート ](https://experienceleague.adobe.com/docs/marketo-developer/assets/reference_architecture.pdf?lang=en) のユースケースで利用できます。[

## 認証

[ 認証ドキュメント ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/authentication)

Marketo REST API は、クライアント資格情報付与タイプを使用した OAuth 2.0 ベースの認証を使用します。 アクセストークンは、作成後 1 時間有効です。

## リード

[ リード API ドキュメント ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/lead-database/leads)

SOAP API は、リードデータの同期、[Munchkin cookie の関連付け ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/javascriptapi/leadtracking/lead-tracking) およびリードの結合をサポートしています。 アプリケーションがSOAP syncLead メソッドを呼び出して `marketoCookie` パラメーターを設定する場合は、次のいずれかの方法で移行できます。

1. [ リードを同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST)REST メソッドを使用し、続いて [ 関連リード ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/associateLeadUsingPOST) を使用
2. [Submit Form](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/leads&quot;%20\l%20&quot;submit-form) を呼び出すこともできますが、これには一部のマーケティングAssetsの設定と、[Forms API とのインタラクションが必要 ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/forms) す。

`foreignSysPersonId` キータイプを使用するアプリケーションは、この外部識別子を表すカスタムリードフィールドを使用してに移行し、[ リードを同期 ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/leads#create-and-update) または [ リードの一括読み込み ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/bulk-import/bulk-lead-import) のいずれかの REST メソッドを使用する必要があります。

| SOAP メソッド | REST メソッド |
| --- | --- |
| [getLead](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/getlead) | [ID でリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)、[ フィルタータイプでリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) |
| [getMultipleLeads](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/getmultipleleads) | [ID でリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)、[ フィルタータイプでリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)、[ プログラム ID でリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByProgramIdUsingGET)、[ リスト ID でリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByListIdUsingGET)、[ 一括リードエクスポート ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads) |
| [mergeLeads](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/mergeleads) | [ リードを結合 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/mergeLeadsUsingPOST) |
| [syncLead](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/synclead) | [ リードを同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST)[ フォームを送信 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/SubmitFormUsingPOST)[ リードを関連付け ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/associateLeadUsingPOST) |
| [syncMultipleLeads](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/syncmultipleleads) | [ リード ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) 一括読み込み [ 同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) |

## M オブジェクト

M オブジェクトは、外部分析用の商談アトリビューションデータのエクスポートをサポートする包括的な概念で、商談、商談の役割、プログラムの 3 つのオブジェクトタイプで作業しました。

REST ドキュメント：

- [商談](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/lead-database/opportunities)
- [ 役割 ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/opportunity-roles)
- [ プログラム ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/assets/programs)

| SOAP メソッド | REST メソッド |
| --- | --- |
| [deleteMObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/deletemobjects) | [ 商談の削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteOpportunitiesUsingPOST)、[ 商談ロールの削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteOpportunityRolesUsingPOST) |
| [describeMObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/describemobject) | [ オポチュニティの説明 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeUsingGET_4)、[ オポチュニティの役割の説明 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeOpportunityRoleUsingGET) |
| [getMObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/getmobjects) | [ オポチュニティの獲得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getOpportunitiesUsingGET)、[ オポチュニティの役割の獲得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeOpportunityRoleUsingGET) |
| [listMObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/listmobjects) | なし |
| [syncMObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/syncmobjects) | [ 商談の同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncOpportunitiesUsingPOST)、[ 商談の役割の同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncOpportunityRolesUsingPOST) |
| [getChannels](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/programs/getchannels) | [ チャネルを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getAllChannelsUsingGET) |
| [getTags](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/programs/gettags) | [ タグのタイプを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getTagTypesUsingGET)、[ 名前でタグを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getTagByNameUsingGET) |

## 静的リスト

SOAP API の静的リストのユースケースは、メンバーシップとリードデータの取り込み、およびメンバーシップの削除に制限されています。これらは、[ リストに追加 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addLeadsToListUsingPOST)、[ リードの一括読み込み ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/bulk-import/bulk-lead-import)、または [ リストから削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE) REST メソッドで実現できます。

| SOAP メソッド | REST メソッド |
| --- | --- |
| [getImportToListStatus](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/static-lists/getimporttoliststatus) | [ リードの一括読み込み ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) |
| [importToList](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/static-lists/importtolist) | [ リストに追加 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addLeadsToListUsingPOST) リード [ 一括読み込み ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) |
| [listOperation](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/static-lists/listoperation) | [ リストから削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE) |

## アクティビティ

SOAP API はアクティビティの取得のみをサポートします。

REST ドキュメント：

- [ 同期アクティビティ ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/activities)
- [ 一括アクティビティ抽出 ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/bulk-extract/bulk-activity-extract)

| SOAP メソッド | REST メソッド |
| --- | --- |
| [getLeadActivity](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/activities/getleadactivity) | [ 一括書き出しアクティビティ ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities)[ リードアクティビティの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET) |
| [getLeadChanges](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/activities/getleadchanges) | [ 一括書き出しアクティビティ ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities)[ リードの変更を取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadChangesUsingGET) |

## キャンペーン

REST ドキュメント：

- [ スマートキャンペーン ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/smart-campaigns&quot;%20\h%20HYPERLINK%20&quot;https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/smart-campaigns)

SOAP API でサポートされているスマートキャンペーンのユースケースは 3 つだけです。[ リードをトリガーしてリクエスト可能なスマートキャンペーンの対象となる ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/smart-campaigns#trigger)、それらのリクエスト可能なキャンペーンを取得、および [ スマートキャンペーンの今後の実行のスケジュール設定 ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/smart-campaigns#schedule) です。

| SOAP メソッド | REST メソッド |
| --- | --- |
| [getCampaignsForSource](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/campaigns/getcampaignsforsource) | [ スマートキャンペーンの概要 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getAllSmartCampaignsGET) |
| [requestCampaign](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/campaigns/requestcampaign) | [ キャンペーンをリクエスト ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/triggerCampaignUsingPOST) |
| [scheduleCampaign](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/campaigns/schedulecampaign) | [ キャンペーンのスケジュール設定 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST) |

## カスタムオブジェクト

REST ドキュメント：

- [ カスタムオブジェクト ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/custom-objects&quot;%20\h%20HYPERLINK%20&quot;https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/custom-objects)

SOAP API は、カスタムオブジェクトに対して CRUD 操作のみをサポートしていました。

| SOAP メソッド | REST メソッド |
| --- | --- |
| [deleteCustomObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/custom-objects/deletecustomobjects) | [ カスタム オブジェクトの削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteCustomObjectsUsingPOST) |
| [getCustomObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/custom-objects/getcustomobjects) | [ カスタムオブジェクトの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCustomObjectsUsingGET) |
| [syncCustomObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/custom-objects/synccustomobjects) | [Sync Custom Objects](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncCustomObjectsUsingPOST)[Bulk Import Custom Object](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/bulk-import/bulk-custom-object-import) |