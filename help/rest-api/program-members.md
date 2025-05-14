---
title: プログラムメンバー
feature: REST API
description: プログラムメンバーを作成および管理します。
exl-id: 22f29a42-2a30-4dce-a571-d7776374cf43
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '1712'
ht-degree: 100%

---

# プログラムメンバー

[プログラムメンバーエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members)

Marketo は、プログラムメンバーレコードの読み取り、作成、更新、削除のための API を公開しています。プログラムメンバーレコードは、リード ID フィールドを通じてリードレコードに関連付けられます。レコードは、一連の標準フィールドと、オプションで最大 20 個の追加のカスタムフィールドで構成されます。フィールドには、各メンバーのプログラム固有のデータが含まれ、フォーム、フィルター、トリガー、フローアクションで使用できます。このデータは、Marketo Engage UI のプログラムの[「メンバー」タブ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/manage-and-view-members)で表示できます。

## 説明

[プログラムメンバーを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2)エンドポイントは、リードデータベースオブジェクトの標準パターンに従います。`searchableFields` 配列は、クエリの実行に有効なフィールドのセットを提供します。`fields` 配列には、REST API 名、表示名、フィールドの更新機能などのフィールドメタデータが含まれます。

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

[プログラムメンバーを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/getProgramMembersUsingGET)エンドポイントを使用すると、プログラムのメンバーを取得できます。`programId` パスパラメーターと、`filterType` および `filterValues` クエリパラメーターが必要です。

`programId` は、検索するプログラムを指定するために使用されます。

`filterType` は、検索フィルターとして使用するフィールドを指定するために使用されます。[プログラムメンバーを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2)エンドポイントから返される &quot;searchableFields&quot; リスト内の任意のフィールドを受け取ります。カスタムフィールドである filterType を指定する場合、カスタムフィールドの dataType は&quot;string&quot; または &quot;integer&quot; のいずれかである必要があります。&quot;leadId&quot; 以外の filterType を指定した場合、リクエストによって最大 100,000 個のプログラムメンバーレコードを処理できます。Marketo インスタンスの設定方法に応じて、次のいずれかのエラーが表示されます。

- プログラムメンバーの合計数が 100,000 を超えると、「1003、合計メンバーシップサイズ：100,001 は、フィルターで許可されている制限の 100,000 を超えています」というエラーが返されます。
- _フィルターに一致する_&#x200B;プログラムメンバーの合計数が 100,000 を超えると、「1003、一致するメンバーシップサイズ：100,001 は、この API で許可されている制限（100,000）を超えています」というエラーが返されます。

メンバーシップ数が制限を超えるプログラムのクエリを実行するには、代わりに [Bulk Program Member Extract API](bulk-program-member-extract.md) を使用します。

`filterValues` は、検索する値を指定するために使用され、コンマ区切り形式で最大 300 個の値を指定できます。この呼び出しは、プログラムメンバーのフィールドが含まれる filterValues のいずれかと一致するレコードを検索します。

または、`startAt` および `endAt` 日時パラメーターを使用して、filterType として `updatedAt` を指定することで、日付範囲でフィルタリングすることもできます。範囲は 7日以内にする必要があります。日時形式は、ミリ秒を含まない ISO-8601 形式にする必要があります。

オプションの `fields` クエリパラメーターは、[プログラムメンバーを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2)エンドポイントによって返されるフィールド API 名のコンマ区切りリストを受け取ります。このパラメーターを含めた場合、応答内の各レコードには指定されているフィールドが含まれます。省略した場合、返されるフィールドのデフォルトセットは、`acquiredBy`、`leadId`、`membershipDate`、`programId`、`reachedSuccess` です。

デフォルトでは、最大 300 個のレコードが返されます。`batchSize` クエリパラメーターを使用して、この数を減らすことができます。**moreResult** 属性が true の場合、さらに多くの結果を使用できます。moreResult 属性が false を返すまで、つまり使用可能な結果が存在しなくなるまで、このエンドポイントを引き続き呼び出します。この API から返される `nextPageToken` は、この呼び出しの次の反復処理で必ず再利用する必要があります。

GET リクエストの合計長が 8 KB を超えると、HTTP エラー「414、URI が長すぎます」（[RFC 7231](https://datatracker.ietf.org/doc/html/rfc72316.5.12) に準拠）という HTTP エラーが返されます。回避策として、GET を POST に変更し、`_method=GET` パラメーターを追加して、リクエスト本文にクエリ文字列を配置します。

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

プログラムメンバーの作成／更新操作をサポートするエンドポイントは 2 つあります。1 つは、プログラムメンバーのステータスのみを更新できます。もう 1 つは、「更新可能」とマークされたプログラムメンバーフィールドのセットを更新できます。両方のエンドポイントで、呼び出しごとに最大 300 個のプログラムメンバーレコードを変更できます。

### プログラムメンバーステータス

[プログラムメンバーステータスを同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/syncProgramMemberStatusUsingPOST)エンドポイントは、1 個以上のメンバーのプログラムステータスを作成または更新するために使用されます。

必須の `programId` パスパラメーターは、作成または更新するメンバーを含むプログラムを指定します。

必須の `statusName` パラメーターは、リードのリストに適用するプログラムステータスを指定します。statusName は、プログラムのチャネルで使用可能なステータスと一致する必要があります。 有効なステータスは、[チャネルを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Channels/operation/getAllChannelsUsingGET)エンドポイントを使用して取得できます。リードのステータスのステップ値が指定された statusName より大きい場合、そのリードはスキップされます。

必須の `input` パラメーターは、プログラムメンバーに対応する `leadId` の配列です。呼び出しごとに、最大 300 個のリード ID を送信できます。各レコードに対してアップサート（更新）操作が実行されます。leadId がプログラムメンバーに関連付けられている場合は、そのメンバーシップステータスが更新されます。関連付けられていない場合は、新しいプログラムメンバーレコードが作成され、レコードがリード ID に関連付けられ、メンバーシップステータスが割り当てられます。

エンドポイントは、&quot;updated&quot;、&quot;created&quot;、&quot;skipped&quot; の `status` で応答します。skipped の場合は、`reasons` 配列も含まれます。また、エンドポイントは、送信したレコードを応答の順序に関連付けるために使用できるインデックスである `seq` フィールドも返します。

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

[プログラムメンバーデータを同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/syncProgramMemberDataUsingPOST)エンドポイントは、1 個以上のメンバーのプログラムメンバーフィールドデータを更新するために使用されます。任意のカスタムフィールドまたは &quot;updateable&quot; な標準フィールドを変更できます（[プログラムメンバーを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2)エンドポイントを参照）。

必須の `programId` パスパラメーターは、更新するメンバーを含むプログラムを指定します。

必須の `input` パラメーターは配列です。各配列要素には、`leadId` と更新する 1 つ以上のフィールド（API 名を使用）が含まれます。各レコードに対して更新操作が実行されます。leadId は、プログラムメンバーに関連付ける必要があります。フィールドを更新可能にする必要があります。呼び出しごとに、最大 300 個のリード ID を送信できます。

エンドポイントは、&quot;updated&quot; または &quot;skipped&quot;. の `status` で応答します。 スキップ済みの場合は、`reasons` 配列も含まれます。また、エンドポイントは、送信したレコードを応答の順序に関連付けるために使用できるインデックスである `seq` フィールドも返します。

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

プログラムメンバーオブジェクトには、標準フィールドとオプションのカスタムフィールドが含まれます。標準フィールドは、すべての Marketo Engage サブスクリプションに存在します。カスタムフィールドは、必要に応じてユーザが作成します。各フィールド定義は、フィールドを説明する属性のセットで構成されます。属性の例としては、表示名、API 名、dataType があります。これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、プログラムメンバーオブジェクトのフィールドに対してクエリ、作成、更新を行うことができます。これらの API では、API を所有するユーザが、**読み取り／書き込みスキーマ標準フィールド**&#x200B;権限または&#x200B;**読み取り／書き込みスキーマカスタムフィールド**&#x200B;権限のいずれかまたは両方を含むロールを持っている必要があります。

### クエリフィールド

プログラムメンバーフィールドのクエリの実行は簡単です。API 名で単一のプログラムメンバーフィールドに対してクエリを実行することも、すべてのプログラムメンバーフィールドのセットに対してクエリを実行することもできます。使用するロール権限に応じて、標準フィールドとカスタムフィールドの両方を取得できます。また、非表示のフィールドも取得されます。

#### 名前別

[名前によりプログラムメンバーフィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/getProgramMemberFieldByNameUsingGET)エンドポイントでは、プログラムメンバーオブジェクトの単一フィールドのメタデータを取得します。必須の `fieldApiName` パスパラメーターは、フィールドの API 名を指定します。応答は「プログラムメンバーを説明」エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す `isCustom` 属性などの追加のメタデータが含まれます。

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

[プログラムメンバーフィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/getProgramMemberFieldsUsingGET)エンドポイントは、プログラムメンバーオブジェクトのすべてのフィールドのメタデータを取得します。デフォルトでは、最大 300 個のレコードが返されます。`batchSize` クエリパラメーターを使用して、この数を減らすことができます。`moreResult` 属性が true の場合、さらに多くの結果が使用可能です。moreResult 属性が false を返すまで、つまり使用可能な結果が存在しなくなるまで、このエンドポイントを引き続き呼び出します。この API から返される `nextPageToken` は、この呼び出しの次の反復処理で必ず再利用する必要があります。

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

### フィールドの作成

[プログラムメンバーフィールドを作成](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/createProgramMemberFieldUsingPOST)エンドポイントは、プログラムメンバーオブジェクトに 1 つ以上のカスタムフィールドを作成します。 このエンドポイントには、[Marketo Engage UI で使用できる](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/program-member-custom-fields)機能と同等の機能が用意されています。このエンドポイントを使用して、最大 20 個のカスタムフィールドを作成できます。

API を使用して Marketo Engage の実稼動インスタンスで作成する各フィールドを慎重に検討してください。フィールドは一度作成すると削除できません（[非表示にすることしかできません](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/field-management/delete-a-custom-field-in-marketo)）。未使用のフィールドが急増すると、インスタンスが乱雑になります。

必須の `input` パラメーターは、プログラムメンバーフィールドオブジェクトの配列です。各オブジェクトには、1 つ以上の属性が含まれます。必須の属性は、それぞれフィールドの UI 表示名、フィールドの API 名、フィールドタイプに対応する `displayName`、`name`、`dataType` です。オプションで、`description`、`isHidden`、`isHtmlEncodingInEmail`、`isSensitive` を指定できます。

`name` と `displayName` の命名にはいくつかのルールが関連付けられています。`name` 属性は一意にする必要があり、文字で始まり、文字、数字、またはアンダースコアのみを含める必要があります。*`isplayName` は一意にする必要があり、特殊文字を含めることはできません。一般的な命名規則では、`displayName` に[キャメルケース](https://en.wikipedia.org/wiki/Camel_case#)を適用して `name` を生成します。例えば、`displayName` が「My Custom Field」の場合、 `name` は「myCustomField」 になります。

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

### フィールドの更新

[プログラムメンバーフィールドを更新](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/updateProgramMemberFieldUsingPOST)エンドポイントでは、プログラムメンバーオブジェクトの単一のカスタムフィールドを更新します。一般的に、Marketo Engage UI を使用して実行されるフィールド更新操作は、API を使用して実行できます。次の表に、いくつかの違いをまとめて示します。

| 属性 | API で更新可能？ | UI で更新可能？ | API で更新可能？ | UI で更新可能？ |
|---|---|---|---|---|
| dataType | いいえ | いいえ | いいえ | はい |
| description | はい | はい | はい | はい |
| displayName | いいえ | いいえ | はい | はい |
| isCustom | いいえ | いいえ | いいえ | いいえ |
| isHidden | いいえ | はい | はい（API で作成されている場合） | はい |
| isHtmlEncodingInEmail | はい | はい | はい | はい |
| isSensitive | はい | はい | はい | はい |
| length | いいえ | いいえ | いいえ | いいえ |
| name | いいえ | いいえ | いいえ | いいえ |

必須の `fieldApiName` パスパラメーターは、更新するフィールドの API 名を指定します。必須の `input` パラメーターは、単一のリードフィールドオブジェクトを含む配列です。フィールドオブジェクトには、1 つ以上の属性が含まれています。

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

[プログラムメンバーを削除](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/deleteProgramMemberUsingPOST)エンドポイントは、プログラムメンバーレコードを削除するために使用されます。必須の `programId` パスパラメーターは、削除するメンバーを含むプログラムを指定します。リクエスト本文には、リード ID の `input` 配列が含まれます。1 回の呼び出しにつき最大 300 個のリード ID が許可されます。

エンドポイントは、&quot;deleted&quot; または &quot;skipped&quot; の `status` で応答します。 スキップ済みの場合は、`reasons` 配列も含まれます。また、エンドポイントは、送信したレコードを応答の順序に関連付けるために使用できるインデックスである `seq` フィールドも返します。

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
