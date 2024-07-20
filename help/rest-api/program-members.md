---
title: プログラムメンバー
feature: REST API
description: プログラムメンバーを作成および管理する。
exl-id: 22f29a42-2a30-4dce-a571-d7776374cf43
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 0%

---

# プログラムメンバー

[ プログラムメンバーエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members)

Marketoは、プログラムメンバーレコードの読み取り、作成、更新、削除のための API を公開しています。 プログラムメンバーレコードは、リード ID フィールドを介してリードレコードに関連付けられています。 レコードは、一連の標準フィールド、およびオプションで最大 20 個の追加カスタムフィールドで構成されます。 このフィールドは、各メンバーのプログラム固有のデータを含んでおり、フォーム、フィルター、トリガー、フローアクションで使用できます。 このデータは、Marketo EngageUI のプログラムの [ 「メンバー」タブ ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/manage-and-view-members) に表示されます。

## 説明

[ プログラムメンバーを記述 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) エンドポイントは、リードデータベースオブジェクトの標準パターンに従います。 `searchableFields` 配列は、クエリに有効なフィールドのセットを提供します。 `fields` 配列には、REST API 名、表示名、フィールドの更新機能などのフィールドメタデータが含まれています。

```
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

[ プログラムメンバーを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/getProgramMembersUsingGET) エンドポイントを使用すると、プログラムのメンバーを取得できます。 `programId` のパスパラメーターと、`filterType` および `filterValues` のクエリパラメーターが必要です。

`programId` は、検索するプログラムを指定するために使用されます。

`filterType` は、検索フィルターとして使用するフィールドを指定するために使用されます。 「プログラムメンバーの説明 [ エンドポイントによって返された「searchableFields」リスト内の任意のフィールドを受け入れ ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) す。 filterType をカスタムフィールドとして指定する場合、カスタムフィールドの dataType は、「string」または「integer」である必要があります。 「leadId」以外の filterType を指定した場合、リクエストで処理できるプログラムメンバーレコードは最大 100,000 個です。 Marketo インスタンスの設定方法に応じて、次のいずれかのエラーが表示されます。

- プログラムメンバーの合計数が 100,000 を超える場合は、「1003、合計メンバーシップサイズ：100,001 は、フィルターで許可されている上限である 100,000 を超えています」というエラーが返されます。
- プログラムメンバーの合計数 _フィルターに一致する_ が 100,000 を超える場合は、「1003、一致するメンバーシップサイズ : 100,001 は、この api で許可されている制限（100,000）を超えています」というエラーが返されます。

メンバーシップ数が制限を超えるプログラムをクエリするには、代わりに [Bulk Program Member Extract API](bulk-program-member-extract.md) を使用します。

`filterValues` は、検索する値を指定するために使用され、コンマ区切り形式で最大 300 個の値を受け入れます。 この呼び出しでは、プログラムメンバーのフィールドが含まれる filterValues のいずれかと一致するレコードが検索されます。

または、`startAt` および `endAt` の datetime パラメーターを持つ filterType として `updatedAt` を指定することで、日付範囲でフィルタリングすることもできます。 範囲は 7 日以内にする必要があります。 日時は、ミリ秒なしの ISO-8601 形式である必要があります。

オプションの `fields` クエリパラメーターは、[ プログラムメンバーを記述 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) エンドポイントによって返されるフィールド API 名のコンマ区切りリストを受け入れます。 含める場合、応答内の各レコードには、指定したフィールドが含まれます。 省略すると、返されるフィールドの既定のセットは、`acquiredBy`、`leadId`、`membershipDate`、`programId`、および `reachedSuccess` になります。

デフォルトでは、最大 300 件のレコードが返されます。 `batchSize` クエリパラメーターを使用して、この数を減らすことができます。 **moreResult** 属性が true の場合、より多くの結果が使用可能であることを意味します。 moreResult 属性が false を返す（使用できる結果がないことを意味する）まで、このエンドポイントの呼び出しを続行します。 この API から返された `nextPageToken` は、この呼び出しの次のイテレーションでは常に再利用する必要があります。

GETリクエストの全長が 8KB を超える場合は、「414, URI too long」（[RFC 7231](https://datatracker.ietf.org/doc/html/rfc72316.5.12) による）という HTTP エラーが返されます。 対応策として、GETをPOSTに変更し、パラメーター `_method=GET` 追加して、リクエスト本文にクエリ文字列を配置できます。

```
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

プログラムメンバーの作成/更新操作をサポートするエンドポイントが 2 つあります。 プログラムメンバーステータスのみを更新できます。 もう 1 つのオプションでは、「更新可能」とマークされたプログラムメンバーフィールドのセットを更新できます。 どちらのエンドポイントでも、1 回の呼び出しで最大 300 個のプログラムメンバーレコードを変更できます。

### プログラムメンバーステータス

[ プログラムメンバーステータスの同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/syncProgramMemberStatusUsingPOST) エンドポイントは、1 人以上のメンバーのプログラムステータスを作成または更新するために使用されます。

必須の `programId` パス パラメーターは、作成または更新するメンバーを含むプログラムを指定します。

必須の `statusName` パラメーターで、リードのリストに適用するプログラムステータスを指定します。 statusName は、プログラムのチャネルで使用可能なステータスと一致する必要があります。 [ チャネルを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Channels/operation/getAllChannelsUsingGET) エンドポイントを使用して、有効なステータスを取得できます。 リードのステータスのステップ値が指定された statusName よりも大きい場合、そのリードはスキップされます。

必須の `input` パラメーターは、プログラムメンバーに対応する `leadId` の配列です。 1 回の呼び出しで最大 300 個の leadIds を送信できます。 各レコードに対してアップサート操作が実行されます。 leadId がプログラムメンバーに関連付けられている場合、そのメンバーシップステータスが更新されます。 そうでない場合は、新しいプログラムメンバーレコードが作成され、レコードが leadId に関連付けられ、メンバーシップステータスが割り当てられます。

エンドポイントは、「更新済み」、「作成済み」、または「スキップ」の `status` で応答します。 スキップした場合は、`reasons` 配列も含まれます。 エンドポイントは、送信されたレコードを応答の順序に関連付けるために使用できるインデックスである `seq` フィールドでも応答します。

呼び出しが成功すると、「プログラムステータスを変更」アクティビティがリードのアクティビティログに書き込まれます。

```
POST /rest/v1/programs/{programId}/members/status.json
```

```
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

[ プログラムメンバーデータの同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/syncProgramMemberDataUsingPOST) エンドポイントは、1 つ以上のメンバーのプログラムメンバーフィールドデータを更新するために使用されます。 カスタムフィールドや、「更新可能」な標準フィールドを変更できます（「プログラムメンバーの説明 [ エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) を参照）。

必須の `programId` パス パラメーターは、更新するメンバーを含むプログラムを指定します。

必須の `input` パラメーターは配列です。 各配列要素には、更新する `leadId` フィールドと 1 つ以上のフィールドが含まれます（API 名を使用）。 各レコードに対して更新操作が実行されます。 leadId は、プログラムメンバーに関連付ける必要があります。 フィールドを更新可能にする必要があります。 1 回の呼び出しで最大 300 個の leadIds を送信できます。

エンドポイントは、「更新済み」または「スキップ」の `status` で応答します。 スキップした場合は、`reasons` 配列も含まれます。 エンドポイントは、送信されたレコードを応答の順序に関連付けるために使用できるインデックスである `seq` フィールドでも応答します。

呼び出しが成功すると、「プログラムメンバーデータを変更」アクティビティがリードのアクティビティログに書き込まれます。

```
POST /rest/v1/programs/{programId}/members.json
```

```
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

プログラムメンバーオブジェクトには、標準フィールドとオプションのカスタムフィールドが含まれています。 標準フィールドはすべてのMarketo Engage購読に存在するのに対して、カスタムフィールドは必要に応じてユーザーが作成します。 各フィールド定義は、フィールドを説明する一連の属性で構成されます。 属性の例としては、表示名、API 名、データタイプがあります。 これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、プログラムメンバーオブジェクトのフィールドに対してクエリ、作成、および更新を実行できます。 これらの API では、所有している API ユーザーに、**読み取り/書き込みスキーマ標準フィールド** または **読み取り/書き込みスキーマカスタムフィールド** 権限の一方または両方の役割が必要です。

### クエリフィールド

プログラムメンバーフィールドのクエリは簡単です。 API 名で 1 つのプログラムメンバーフィールドに対してクエリを実行することも、すべてのプログラムメンバーフィールドのセットに対してクエリを実行することもできます。 使用する役割の権限に応じて、標準フィールドとカスタムフィールドの両方を取得できます。 非表示のフィールドも取得されます。

#### 名前別

[ 名前によるプログラムメンバーフィールドの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/getProgramMemberFieldByNameUsingGET) エンドポイントは、プログラムメンバーオブジェクト上の 1 つのフィールドのメタデータを取得します。 必須の `fieldApiName` パスパラメーターは、フィールドの API 名を指定します。 応答は、「プログラムメンバーの説明」エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す `isCustom` 属性などの追加メタデータが含まれています。

```
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

[ プログラムメンバーフィールドの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/getProgramMemberFieldsUsingGET) エンドポイントは、プログラムメンバーオブジェクト上のすべてのフィールドのメタデータを取得します。 デフォルトでは、最大 300 件のレコードが返されます。 `batchSize` クエリパラメーターを使用して、この数を減らすことができます。 `moreResult` 属性が true の場合は、より多くの結果が利用可能であることを意味します。 moreResult 属性が false を返す（使用できる結果がないことを意味する）まで、このエンドポイントの呼び出しを続行します。 この API から返された `nextPageToken` は、この呼び出しの次のイテレーションでは常に再利用する必要があります。

```
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

### フィールドを作成

[ プログラムメンバーフィールドの作成 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/createProgramMemberFieldUsingPOST) エンドポイントは、プログラムメンバーオブジェクトに 1 つ以上のカスタムフィールドを作成します。 このエンドポイントは、[Marketo EngageUI で使用できる ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/program-member-custom-fields) 機能と同等の機能を提供します。 このエンドポイントを使用して最大 20 個のカスタムフィールドを作成できます。

API を使用してMarketo Engageの実稼動インスタンスで作成する各フィールドについては、慎重に検討してください。 作成したフィールドは削除できません（[ 非表示にしかできません ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/delete-a-custom-field-in-marketo)）。 未使用のフィールドの急増は望ましくない手法であり、インスタンスが煩雑になります。

必須の `input` パラメーターは、プログラムメンバーフィールドオブジェクトの配列です。 各オブジェクトには、1 つ以上の属性が含まれます。 必須の属性は、フィールドの UI 表示名、フィールドの API 名、フィールドタイプにそれぞれ対応する `displayName`、`name`、`dataType` です。 オプションで、`description`、`isHidden`、`isHtmlEncodingInEmail`、`isSensitive` を指定できます。

`name` と `displayName` の命名には、いくつかのルールが関連付けられています。 `name` 属性は一意で、文字で始まり、文字、数字、アンダースコアのみを含める必要があります。 *`isplayName` は一意である必要があり、特殊文字を含めることはできません。 一般的な命名規則は、キャメルケース [ を適用して `name` ータを作成する `displayName` とです ](https://en.wikipedia.org/wiki/Camel_case#) 例えば、「My Custom Field」という `displayName` を指定すると、「myCustomField」という `name` が生成されます。

```
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

### フィールドを更新

[ プログラムメンバーフィールドを更新 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/updateProgramMemberFieldUsingPOST) エンドポイントは、プログラムメンバーオブジェクト上の 1 つのカスタムフィールドを更新します。 通常、Marketo EngageUI を使用して実行されるフィールド更新操作は、API を使用して実行できます。 次の表にまとめた違いがいくつかあります。

| 属性 | API で更新可能ですか？ | UI で更新可能ですか？ | API で更新可能ですか？ | UI で更新可能ですか？ |
|---|---|---|---|---|
| dataType | なし | なし | なし | はい |
| description | はい | はい | はい | はい |
| displayName | なし | なし | はい | はい |
| isCustom | なし | なし | なし | なし |
| isHidden | なし | はい | 対応（API で作成されている場合） | はい |
| isHtmlEncodingInEmail | はい | はい | はい | はい |
| isSensitive | はい | はい | はい | はい |
| length | なし | なし | なし | なし |
| 名前 | なし | なし | なし | なし |

必須の `fieldApiName` パスパラメーターは、更新するフィールドの API 名を指定します。 必須の `input` パラメーターは、単一のリードフィールドオブジェクトを含む配列です。 フィールドオブジェクトには、1 つ以上の属性が含まれています。

```
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

[ プログラムメンバーの削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/deleteProgramMemberUsingPOST) エンドポイントは、プログラムメンバーレコードの削除に使用されます。 必須の `programId` path パラメーターは、削除するメンバーを含むプログラムを指定します。 リクエスト本文には、リード ID の `input` 配列が含まれます。 最大 300 個のリード id  呼び出しごとに許可されます。

エンドポイントは、「削除済み」または「スキップ」の `status` で応答します。 スキップした場合は、`reasons` 配列も含まれます。 エンドポイントは、送信されたレコードを応答の順序に関連付けるために使用できるインデックスである `seq` フィールドでも応答します。

```
POST /rest/v1/programs/{programId}/members/delete.json
```

```
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
