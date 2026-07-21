---
title: プログラムメンバー
feature: REST API
description: Marketo REST APIを使用すると、プログラムメンバーの読み取り、作成、更新、削除、標準フィールドとカスタムフィールドの管理、検索可能なフィールドを使用したクエリを実行できます。
exl-id: 22f29a42-2a30-4dce-a571-d7776374cf43
TQID: https://experienceleague.adobe.com/scEHyXYq9C7cCS1kIX810wG7ahT9fsa448NwIfBmzQM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1670
ht-degree: 20%

---

# プログラムメンバー

[プログラムメンバーエンドポイントリファレンス](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members)

Marketoには、プログラムメンバーレコードの読み取り、作成、更新、削除用のAPIが用意されています。 「リード ID」フィールドは、プログラムメンバーのレコードとリードレコードを関連付けます。

各レコードには標準フィールドが含まれ、最大20個のカスタムフィールドを含めることができます。 これらのフィールドには、フォーム、フィルター、トリガー、フローアクションで使用するためのプログラム固有のメンバーデータが保存されます。 このデータは、Marketo Engage UIのプログラムの[&#x200B; メンバー](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/manage-and-view-members) タブで確認できます。

## 説明

[&#x200B; プログラム メンバーの説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2) エンドポイントは、リード データベース オブジェクトの標準パターンに従います。

- `searchableFields`配列は、クエリに有効なフィールドを識別します。
- `fields`配列には、REST API名、表示名、フィールドが更新可能かどうかなどのメタデータが含まれています。

```http
GET /rest/v1/programs/members/describe.json
```

```json
{
    "requestId": "f813#1791563c7cc",
    "result": [
        {
            "name": "API Program Membership",
            "description": "Map for API program membership fields",
            "createdAt": "2021-03-20T01:30:05Z",
            "updatedAt": "2021-03-20T01:30:05Z",
            "dedupeFields": [
                "leadId",
                "programId"
            ],
            "searchableFields": [
                [
                    "leadId"
                ],
                [
                    "myCustomField"
                ],
                [
                    "reachedSuccess"
                ],
                [
                    "statusName"
                ]
            ],
            "fields": [
                {
                    "name": "acquiredBy",
                    "displayName": "acquiredBy",
                    "dataType": "boolean",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "attendanceLikelihood",
                    "displayName": "attendanceLikelihood",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "createdAt",
                    "displayName": "createdAt",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "isExhausted",
                    "displayName": "isExhausted",
                    "dataType": "boolean",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "leadId",
                    "displayName": "leadId",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "membershipDate",
                    "displayName": "membershipDate",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "nurtureCadence",
                    "displayName": "nurtureCadence",
                    "dataType": "string",
                    "length": 4,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "program",
                    "displayName": "program",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "programId",
                    "displayName": "programId",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "reachedSuccess",
                    "displayName": "reachedSuccess",
                    "dataType": "boolean",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "reachedSuccessDate",
                    "displayName": "reachedSuccessDate",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "registrationLikelihood",
                    "displayName": "registrationLikelihood",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "statusName",
                    "displayName": "statusName",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "statusReason",
                    "displayName": "statusReason",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "trackName",
                    "displayName": "trackName",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "updatedAt",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "waitlistPriority",
                    "displayName": "waitlistPriority",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "myCustomField",
                    "displayName": "myCustomField",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "registrationCode",
                    "displayName": "registrationCode",
                    "dataType": "string",
                    "length": 100,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "webinarUrl",
                    "displayName": "webinarUrl",
                    "dataType": "string",
                    "length": 2000,
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

## クエリ

プログラムのメンバーを取得するには、[&#x200B; プログラムメンバーを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/getProgramMembersUsingGET) エンドポイントを使用します。 リクエストには、`programId` パスパラメーターと`filterType`および`filterValues` クエリパラメーターが必要です。

`programId`は、検索するプログラムを指定します。

`filterType`は、検索フィルターとして使用するフィールドを指定します。 [プログラムメンバーを説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2)エンドポイントから返される &quot;searchableFields&quot; リスト内の任意のフィールドを受け取ります。 カスタムフィールドの場合、dataTypeは「文字列」または「整数」である必要があります。

filterTypeが「leadId」でない場合、リクエストは最大100,000件のプログラムメンバーレコードを処理できます。 Marketo インスタンス設定に応じて、次のいずれかのエラーが発生します。

- プログラムメンバーの合計数が 100,000 を超えると、「1003、合計メンバーシップサイズ：100,001 は、フィルターで許可されている制限の 100,000 を超えています」というエラーが返されます。
- _フィルターに一致する_&#x200B;プログラムメンバーの合計数が 100,000 を超えると、「1003、一致するメンバーシップサイズ：100,001 は、この API で許可されている制限（100,000）を超えています」というエラーが返されます。

メンバーシップ数が制限を超えているプログラムをクエリするには、代わりに[Bulk Program Member Extract API](bulk-program-member-extract.md)を使用します。

`filterValues`は、検索する値を指定し、最大300個のコンマ区切りの値を受け入れます。 呼び出しは、プログラムメンバーフィールドが含まれているfilterValueのいずれかに一致するレコードを検索します。

または、`updatedAt`をfilterTypeとして指定し、`startAt`と`endAt`の日時パラメーターを指定して、日付範囲でフィルタリングします。 範囲は 7日以内にする必要があります。 日時の値にミリ秒以外のISO-8601形式を使用します。

オプションの`fields` クエリパラメーターは、[&#x200B; プログラムメンバー](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2) エンドポイントによって返されるフィールド API名のコンマ区切りリストを受け入れます。 含まれている場合、各応答レコードには指定されたフィールドが含まれます。 省略すると、デフォルトで`acquiredBy`、`leadId`、`membershipDate`、`programId`および`reachedSuccess`が返されます。

デフォルトでは、エンドポイントは最大300件のレコードを返します。 この数を減らすには、`batchSize` クエリパラメーターを使用します。

**moreResult**&#x200B;属性がtrueの場合、より多くの結果を使用できます。 返された`nextPageToken`でエンドポイントの呼び出しを続行し、moreResultがfalseになるまで呼び出します。

GET リクエストの合計長が8 KBを超えた場合、エンドポイントはHTTP エラー「414、URIが長すぎます」を返します。 この制限を回避するには、リクエストをGETからPOSTに変更し、`_method=GET` パラメーターを追加して、クエリ文字列をリクエスト本文に配置します。

```http
GET /rest/v1/programs/{programId}/members.json?filterType=statusName&filterValues=Influenced
```

```json
{
    "requestId": "109da#17915eec072",
    "result": [
        {
            "seq": 0,
            "leadId": 1789,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 1,
            "leadId": 1790,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 2,
            "leadId": 1791,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 3,
            "leadId": 1792,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 4,
            "leadId": 1793,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 5,
            "leadId": 1794,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 6,
            "leadId": 1795,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 7,
            "leadId": 1796,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 8,
            "leadId": 1797,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 9,
            "leadId": 1798,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 10,
            "leadId": 1799,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 11,
            "leadId": 1800,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        }
    ],
    "success": true,
    "moreResult": false
}
```

## 作成と更新

プログラムメンバーに対する作成と更新の操作をサポートする2つのエンドポイント：

- 1つのエンドポイントは、プログラムメンバーのステータスのみを更新します。
- 1つのエンドポイントは、「更新可能」としてマークされたプログラムメンバーフィールドを更新します。

各エンドポイントは、1回の呼び出しごとに最大300件のプログラムメンバーレコードを変更できます。

### プログラムメンバーステータス

[&#x200B; プログラムメンバーステータスの同期](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/syncProgramMemberStatusUsingPOST) エンドポイントを使用して、1人以上のメンバーのプログラムステータスを作成または更新します。

必要なパラメーターは次のとおりです。

- `programId`：作成または更新するメンバーを含むプログラムを指定するパスパラメーター。
- `statusName`: リードのリストに適用するプログラムのステータスを指定します。 statusName は、プログラムのチャネルで使用可能なステータスと一致する必要があります。 [&#x200B; チャネルを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Channels/operation/getAllChannelsUsingGET) エンドポイントを使用して有効なステータスを取得します。 リードのステータスが、指定されたstatusNameよりも大きいステップ値を持つ場合、リクエストはそのリードをスキップします。
- `input`: プログラムメンバーに対応する`leadId`値の配列。 呼び出しごとに、最大 300 個のリード ID を送信できます。

エンドポイントは、各レコードに対してアップサートを実行します。 leadIdがプログラムメンバーに関連付けられている場合、エンドポイントはそのメンバーシップステータスを更新します。 そうでない場合は、プログラムメンバーレコードを作成し、レコードをleadIdに関連付け、メンバーシップステータスを割り当てます。

応答には、「更新済み」、「作成済み」、または「スキップ済み」の`status`が含まれます。 スキップされた結果には、`reasons`配列も含まれます。 `seq` フィールドは、送信された各レコードと応答順序を関連付けるインデックスです。

呼び出しが成功すると、「プログラムステータスを変更」アクティビティがリードのアクティビティログに書き込まれます。

```http
POST /rest/v1/programs/{programId}/members/status.json
```

```text
Content-Type: application/json
```

```json
{
    "statusName":"Influenced",
    "input":[
        {
            "leadId": 1800
        },
        {
            "leadId": 1801
        },
        {
            "leadId": 1235
        }
    ]
}
```

```json
{
    "requestId": "14b2d#17916378ec5",
    "result": [
        {
            "seq": 0,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1037",
                    "message": "Lead skipped because it is already in or past this status"
                }
            ]
        },
        {
            "seq": 1,
            "status": "updated",
            "leadId": 1801
        },
        {
            "seq": 2,
            "status": "created",
            "leadId": 1235
        }
    ],
    "success": true
}
```

### プログラムメンバーデータ

[&#x200B; プログラムメンバーデータの同期](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/syncProgramMemberDataUsingPOST) エンドポイントを使用して、1人以上のメンバーのプログラムメンバーフィールドデータを更新します。 [&#x200B; プログラム メンバーの説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2) エンドポイントによって「更新可能」とマークされた任意のカスタム フィールドまたは任意の標準フィールドを変更できます。

必要なパラメーターは次のとおりです。

- `programId`：更新するメンバーを含むプログラムを指定するパスパラメーター。
- `input`: API名で更新する`leadId`と1つ以上のフィールドを要素に含む配列。 呼び出しごとに、最大 300 個のリード ID を送信できます。

エンドポイントは、各レコードを更新します。 leadIdはプログラムメンバーに関連付ける必要があり、各フィールドは更新可能である必要があります。

応答には、「更新」または「スキップ」の`status`が含まれます。 スキップされた結果には、`reasons`配列も含まれます。 `seq` フィールドは、送信された各レコードと応答順序を関連付けるインデックスです。

呼び出しが成功すると、「プログラムメンバーデータを変更」アクティビティがリードのアクティビティログに書き込まれます。

```http
POST /rest/v1/programs/{programId}/members.json
```

```text
Content-Type: application/json
```

```json
{
    "input":[
        {
            "leadId": 1789,
            "registrationCode": "dcff5f12-a7c7-11eb-bcbc-0242ac130002"
        },
        {
            "leadId": 1790,
            "registrationCode": "c0404b78-d3fd-47bf-82c4-d16f3852ab3a"
        },
        {
            "leadId": 1003,
            "registrationCode": "aa880c57-75b8-426b-a33a-fbf6302d7cb4"
        }
    ]
}
```

```json
{
    "requestId": "edc3#1791659b8d2",
    "result": [
        {
            "seq": 0,
            "status": "updated",
            "leadId": 1789
        },
        {
            "seq": 1,
            "status": "updated",
            "leadId": 1790
        },
        {
            "seq": 2,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1013",
                    "message": "Membership not found"
                }
            ]
        }
    ],
    "success": true
}
```

## フィールド

プログラムメンバーオブジェクトには、標準フィールドとオプションのカスタムフィールドが含まれます。 標準フィールドはMarketo Engageのサブスクリプションごとに用意されていますが、カスタムフィールドは必要に応じて作成できます。

各フィールドは、表示名、API名、dataTypeなどの属性で定義されます。 これらの属性をメタデータと呼びます。

次のエンドポイントは、プログラムメンバーオブジェクトのフィールドのクエリ、作成、更新を行います。 API ユーザーには、**読み取り/書き込みスキーマ標準フィールド**&#x200B;権限、**読み取り/書き込みスキーマカスタムフィールド**&#x200B;権限、またはその両方を持つ役割が必要です。

### クエリフィールド

API名で1つのプログラムメンバーフィールドをクエリするか、すべてのプログラムメンバーフィールドを取得します。 役割の権限は、応答に標準フィールド、カスタムフィールド、またはその両方を含めることができるかどうかを決定します。 応答には非表示のフィールドも含まれます。

#### 名前別

[名前でプログラムメンバーフィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/getProgramMemberFieldByNameUsingGET) エンドポイントは、プログラムメンバーオブジェクトの1つのフィールドのメタデータを取得します。 必須の`fieldApiName` パスパラメーターは、フィールドのAPI名を指定します。

応答はプログラムメンバーの説明の応答に似ていますが、追加のメタデータが含まれています。 例えば、`isCustom`属性は、フィールドがカスタムかどうかを示します。

```http
GET /rest/v1/programs/members/schema/fields/{fieldApiName}.json
```

```json
{
    "requestId": "15416#17e955554de",
    "result": [
        {
            "displayName": "Status",
            "name": "statusName",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true
}
```

#### 参照

[プログラムメンバーフィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/getProgramMemberFieldsUsingGET)エンドポイントは、プログラムメンバーオブジェクトのすべてのフィールドのメタデータを取得します。 デフォルトでは、最大300件のレコードが返されます。 この数を減らすには、`batchSize` クエリパラメーターを使用します。

`moreResult` 属性が true の場合、さらに多くの結果が使用可能です。 返された`nextPageToken`でエンドポイントの呼び出しを続行し、moreResultがfalseになるまで呼び出します。

```http
GET /rest/v1/programs/members/schema/fields.json?batchSize=5
```

```json
{
    "requestId": "102f6#17e9557f123",
    "result": [
        {
            "displayName": "Acquired By",
            "name": "acquiredBy",
            "description": null,
            "dataType": "boolean",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Nurture Cadence",
            "name": "nurtureCadence",
            "description": null,
            "dataType": "string",
            "length": 4,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Nurture Exhausted",
            "name": "isExhausted",
            "description": null,
            "dataType": "boolean",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Member Date",
            "name": "membershipDate",
            "description": null,
            "dataType": "datetime",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Program",
            "name": "program",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true,
    "nextPageToken": "BC7J6EPVLT6T4B5FKUU3APCYN4======",
    "moreResult": true
}
```

### フィールドの作成

[&#x200B; プログラムメンバーフィールドの作成](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/createProgramMemberFieldUsingPOST) エンドポイントは、プログラムメンバーオブジェクトにカスタムフィールドを作成します。 [Marketo Engage UI](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/program-member-custom-fields)と同等の機能を提供します。 このエンドポイントを使用して、最大20個のカスタムフィールドを作成できます。

実稼動Marketo Engage インスタンスで作成する前に、各フィールドを慎重に検討します。 フィールドを作成した後は、削除できません。[非表示にできるのは](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/field-management/delete-a-custom-field-in-marketo)のみです。 未使用のフィールドは、インスタンスを混乱させます。

必須の `input` パラメーターは、プログラムメンバーフィールドオブジェクトの配列です。 各オブジェクトには、1 つ以上の属性が含まれます。

- 必要な属性は`displayName`、`name`、`dataType`です。 UIの表示名、API名、フィールドタイプにそれぞれ対応します。
- オプションの属性は`description`、`isHidden`、`isHtmlEncodingInEmail`、および`isSensitive`です。

`name`および`displayName`属性には、次の命名ルールがあります。

- `name`属性は一意で、文字で始まり、文字、数字、アンダースコアのみを含める必要があります。
- *`isplayName`は一意である必要があり、特殊文字を含めることはできません。

一般的な規則は、[&#x200B; キャメルケース &#x200B;](https://en.wikipedia.org/wiki/Camel_case#)を`displayName`に適用して`name`を生成することです。 例えば、「My Custom Field」の`displayName`は、「myCustomField」の`name`を生成します。

```http
POST /rest/v1/programs/members/schema/fields.json
```

```json
{
  "input": [
    {
        "displayName": "PMCF Custom Field 03",
        "name": "pMCFCustomField03",
        "description": "My third custom field",
        "dataType": "string"
    }
  ]
}
```

```json
{
    "requestId": "13a7#17e955fcb44",
    "result": [
        {
            "name": "pMCFCustomField03",
            "status": "created"
        }
    ],
    "success": true
}
```

### フィールドの更新

[&#x200B; プログラムメンバーフィールドの更新](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/updateProgramMemberFieldUsingPOST) エンドポイントは、プログラムメンバーオブジェクトの1つのカスタムフィールドを更新します。 Marketo Engage UIで利用できるフィールドの更新のほとんどは、APIからも利用できます。 次の表に、その違いをまとめました。

| 属性 | API で更新可能？ | UI で更新可能？ | API で更新可能？ | UI で更新可能？ |
| --- | --- | --- | --- | --- |
| dataType | いいえ | いいえ | いいえ | はい |
| description | はい | はい | はい | はい |
| displayName | いいえ | いいえ | はい | はい |
| isCustom | いいえ | いいえ | いいえ | いいえ |
| isHidden | いいえ | はい | はい（API で作成されている場合） | はい |
| isHtmlEncodingInEmail | はい | はい | はい | はい |
| isSensitive | はい | はい | はい | はい |
| length | いいえ | いいえ | いいえ | いいえ |
| name | いいえ | いいえ | いいえ | いいえ |

リクエストには次のパラメーターが必要です。

- `fieldApiName`：更新するフィールドのAPI名を指定するパスパラメーター。
- `input`: 1つ以上の属性を持つ1つのリードフィールドオブジェクトを含む配列。

```http
POST /rest/v1/programs/members/schema/fields/pMCFCustomField03.json
```

```json
{
  "input": [
      {
        "displayName": "Lunch Preference",
        "description": "Attendee food preference",
        "isHtmlEncodingInEmail": true
      }
  ]
}
```

```json
{
    "requestId": "215f#17e95663955",
    "result": [
        {
            "name": "pMCFCustomField03",
            "status": "updated"
        }
    ],
    "success": true
}
```

## 削除

プログラムメンバーレコードを削除するには、[&#x200B; プログラムメンバーの削除](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/deleteProgramMemberUsingPOST) エンドポイントを使用します。 必須の`programId` パス パラメーターは、削除するメンバーを含むプログラムを指定します。

リクエスト本文には、リード IDの`input`配列が含まれています。 各呼び出しでは、最大300個のリード IDを使用できます。

応答には、「削除済み」または「スキップ済み」の`status`が含まれています。 スキップされた結果には、`reasons`配列も含まれます。 `seq` フィールドは、送信された各レコードと応答順序を関連付けるインデックスです。

```http
POST /rest/v1/programs/{programId}/members/delete.json
```

```text
Content-Type: application/json
```

```json
{
    "input":[
        {
            "leadId": 1235
        },
        {
            "leadId": 77
        }
    ]
}
```

```json
{
    "requestId": "302a#17916619417",
    "result": [
        {
            "seq": 0,
            "status": "deleted",
            "leadId": 1235
        },
        {
            "seq": 1,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1037",
                    "message": "Lead not in program"
                }
            ]
        }
    ],
    "success": true
}
```
