---
title: REST API への移行
feature: SOAP
description: SOAP から REST API への移行
exl-id: c2956db3-defe-4163-99f3-58654ce8ee2b
source-git-commit: 8a785b0719e08544ed1a87772faf90bd9dda3077
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 99%

---

# REST API への移行

Marketo Engage SOAP API は、2025年10月31日（PT）以降に廃止される予定です。サービスの中断を回避するために、SOAP API を使用したすべての既存の統合は、この日付までに廃止するか、[Marketo Engage REST API](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/rest-api) に移行する必要があります。

## 移行

SOAP API は、[REST API](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/rest-api) と比較して、サポートされるユースケースの範囲が制限されます。ユースケースをマッピングするエンドポイントを決定する際は、[Marketo 統合ベストプラクティス](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/marketo-integration-best-practices)に従う必要があります

[CRM 同期](https://experienceleague.adobe.com/docs/marketo-developer/assets/sync-architecture-whitepaper.pdf?lang=ja)および[データウェアハウスの書き出し](https://experienceleague.adobe.com/docs/marketo-developer/assets/reference_architecture.pdf?lang=ja)のユースケースでは、[参照アーキテクチャ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/reference-architectures)が使用できます。

## 認証

[認証ドキュメント](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/authentication)

Marketo REST API では、クライアント資格情報付与タイプを使用した OAuth 2.0 ベースの認証を使用します。アクセストークンの有効期間は、作成後 1 時間です。

## リード

[リード API ドキュメント](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/lead-database/leads)

SOAP API では、リードデータの同期、[Munchkin cookie の関連付け](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/javascriptapi/leadtracking/lead-tracking)、およびリードの結合をサポートしています。アプリケーションが SOAP syncLead メソッドを呼び出して `marketoCookie` パラメーターを設定する場合は、次のいずれかの方法で移行できます。

1. [リードを同期](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) RESTメソッドを使用し、その後に[関連付けられたリード](https://developer.adobe.com/marketo-apis/api/mapi/#operation/associateLeadUsingPOST)を使用
2. [フォームを送信](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/lead-database/leads)を呼び出すことができますが、これにはマーケティングアセットの設定と [Forms API](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/assets/forms) とのインタラクションが必要です

`foreignSysPersonId` キータイプを使用するアプリケーションでは、この外部識別子を表すカスタムリードフィールドを使用するように移行し、[リードを同期](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/lead-database/leads#create-and-update)または[リードの一括読み込み](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/bulk-import/bulk-lead-import) REST メソッドのいずれかを使用する必要があります。

| SOAP メソッド | REST メソッド |
| --- | --- |
| [getLead](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/leads/getlead) | [ID によるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)、[フィルタータイプによるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) |
| [getMultipleLeads](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/leads/getmultipleleads) | [ID によるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)、[フィルタータイプによるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)、[プログラム ID によるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByProgramIdUsingGET)、[リスト ID によるリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByListIdUsingGET)、[リードの一括書き出し](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads) |
| [mergeLeads](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/leads/mergeleads) | [リードを結合](https://developer.adobe.com/marketo-apis/api/mapi/#operation/mergeLeadsUsingPOST) |
| [syncLead](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/leads/synclead) | [リードを同期](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) [フォームを送信](https://developer.adobe.com/marketo-apis/api/mapi/#operation/SubmitFormUsingPOST) [リードを関連付け](https://developer.adobe.com/marketo-apis/api/mapi/#operation/associateLeadUsingPOST) |
| [syncMultipleLeads](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/leads/syncmultipleleads) | [リードを同期](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) [一括読み込み](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) |

## M オブジェクト

M オブジェクトは、外部分析用の商談属性データの書き出しをサポートする包括的な概念で、商談、商談ロール、プログラムという 3 つのオブジェクトタイプで機能しました。

REST ドキュメント：

- [商談](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/lead-database/opportunities)
- [ロール](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/lead-database/opportunity-roles)
- [プログラム](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/assets/programs)

| SOAP メソッド | REST メソッド |
| --- | --- |
| [deleteMObjects](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/marketo-objects/deletemobjects) | [商談を削除](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteOpportunitiesUsingPOST)、[商談ロールを削除](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteOpportunityRolesUsingPOST) |
| [describeMObjects](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/marketo-objects/describemobject) | [商談を説明](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeUsingGET_4)、[商談ロールを説明](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeOpportunityRoleUsingGET) |
| [getMObjects](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/marketo-objects/getmobjects) | [商談を取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getOpportunitiesUsingGET)、[商談ロールを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeOpportunityRoleUsingGET) |
| [listMObjects](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/marketo-objects/listmobjects) | 該当なし |
| [syncMObjects](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/marketo-objects/syncmobjects) | [商談を同期](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncOpportunitiesUsingPOST)、[商談ロールを同期](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncOpportunityRolesUsingPOST) |
| [getChannels](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/programs/getchannels) | [チャネルを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getAllChannelsUsingGET) |
| [getTags](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/programs/gettags) | [タグタイプを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getTagTypesUsingGET)、[名前でタグを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getTagByNameUsingGET) |

## 静的リスト

SOAP API での静的リストのユースケースは、メンバーシップとリードデータの取り込み、および[リストに追加](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addLeadsToListUsingPOST)、[リードを一括読み込み](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/bulk-import/bulk-lead-import)、または[リストから削除](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE)の REST メソッドを使用して実行できるメンバーシップの削除に制限されています。

| SOAP メソッド | REST メソッド |
| --- | --- |
| [getImportToListStatus](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/static-lists/getimporttoliststatus) | [リードを一括読み込み](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) |
| [importToList](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/static-lists/importtolist) | [リストに追加](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addLeadsToListUsingPOST) [リードを一括読み込み](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) |
| [listOperation](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/static-lists/listoperation) | [リストから削除](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE) |

## アクティビティ

SOAP API では、アクティビティの取得のみをサポートしています。

REST ドキュメント：

- [同期アクティビティ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/lead-database/activities)
- [アクティビティの一括抽出](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/bulk-extract/bulk-activity-extract)

| SOAP メソッド | REST メソッド |
| --- | --- |
| [getLeadActivity](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/activities/getleadactivity) | [一括書き出しアクティビティ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities) [リードを取得アクティビティ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET) |
| [getLeadChanges](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/activities/getleadchanges) | [一括書き出しアクティビティ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities) [リードを取得の変更](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadChangesUsingGET) |

## キャンペーン

REST ドキュメント：

- [スマートキャンペーン](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/assets/smart-campaigns)

SOAP API では、[リクエスト可能なスマートキャンペーンを選定するためのリードのトリガー](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/assets/smart-campaigns#trigger)、リクエスト可能なキャンペーンの取得、および[スマートキャンペーンの今後の実行のスケジュール](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/assets/smart-campaigns#schedule)のスマートキャンペーンの 3 つのユースケースのみをサポートしています。

| SOAP メソッド | REST メソッド |
| --- | --- |
| [getCampaignsForSource](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/campaigns/getcampaignsforsource) | [スマートキャンペーンを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getAllSmartCampaignsGET) |
| [requestCampaign](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/campaigns/requestcampaign) | [キャンペーンをリクエスト](https://developer.adobe.com/marketo-apis/api/mapi/#operation/triggerCampaignUsingPOST) |
| [scheduleCampaign](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/campaigns/schedulecampaign) | [キャンペーンをスケジュール](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST) |

## カスタムオブジェクト

REST ドキュメント：

- [カスタムオブジェクト](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/custom-objects)

SOAP API では、カスタムオブジェクトの CRUD 操作のみをサポートしていました。

| SOAP メソッド | REST メソッド |
| --- | --- |
| [deleteCustomObjects](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/custom-objects/deletecustomobjects) | [カスタムオブジェクトを削除](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteCustomObjectsUsingPOST) |
| [getCustomObjects](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/custom-objects/getcustomobjects) | [カスタムオブジェクトを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCustomObjectsUsingGET) |
| [syncCustomObjects](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/custom-objects/synccustomobjects) | [カスタムオブジェクトを同期](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncCustomObjectsUsingPOST) [カスタムオブジェクトを一括読み込み](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/bulk-import/bulk-custom-object-import) |
