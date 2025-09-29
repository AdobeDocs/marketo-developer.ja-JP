---
title: アクティビティ
feature: REST API
description: Marketo Engage Activities REST API を使用して、アクティビティタイプのリスト、ページングトークンを使用したリードアクティビティの取得、カスタムおよびデータ値の変更の処理を行います。
exl-id: 1e69af23-2b0c-467a-897c-1dcf81343e73
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '2046'
ht-degree: 98%

---

# アクティビティ

Marketo では、リードレコードに関連する様々なアクティビティタイプが許可されます。ほとんどすべての変更、アクション、フローステップは、リードのアクティビティログに対して記録され、API 経由で取得したり、スマートリストやスマートキャンペーンのフィルターとトリガーで活用したりできます。アクティビティは常に、leadId 経由でリードレコードに関連付けられます。leadId は、レコードの「ID」フィールドに対応し、一意の ID を持っています。

潜在的なアクティビティタイプは非常に多く、サブスクリプションごとに異なる場合があり、それぞれに一意の定義があります。すべてのアクティビティには、一意の `id`、`leadId` および `activityDate` がありますが、`primaryAttributeValueId` と `primaryAttributeValue` の値の意味は異なります。

また、Marketo では、Custom Activities Metadata API を通じてカスタムアクティビティタイプを作成することもできます。カスタムアクティビティの追加は、 Add Custom Activities API を通じて行われます。

ほとんどのアクティビティは、一定期間後にパージされます。

## 説明

インスタンスで使用可能なタイプとその定義のリストを取得するには、[アクティビティタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getAllActivityTypesUsingGET)エンドポイントを使用できます。

```
GET /rest/v1/activities/types.json
```

```json
  "requestId": "6e78#148ad3b76f1",
  "success": true,
  "result": [
    {
      "id": 2,
      "name": "Fill Out Form",
      "description": "User fills out and submits form on web page",
      "primaryAttribute": {
        "name": "Webform ID",
        "dataType": "integer"
      },
      "attributes": [
        {
          "name": "Client IP Address",
          "dataType": "string"
        },
        {
          "name": "Form Fields",
          "dataType": "text"
        },
        {
          "name": "Query Parameters",
          "dataType": "string"
        },
        {
          "name": "Referrer URL",
          "dataType": "string"
        },
        {
          "name": "User Agent",
          "dataType": "string"
        },
        {
          "name": "Webpage ID",
          "dataType": "integer"
        }
      ]
    }
  ]
}
```

現実の応答には、はるかに多くの定義が含まれます。この例では、表示されるタイプは「フォームに入力」で、プライマリ属性は「Webform ID」です。これは、入力したフォームの Marketo ID を参照し、Marketo 内の特定のアセットに関連付けるために使用できます。さらに、このタイプの特定のアクティビティレコードの可能な各属性とそのデータタイプの定義もあります。フィールドが空の場合、その特定の属性は個々のアクティビティレコードから省略されます。

## クエリ

Marketo からアクティビティを取得するには、[リードアクティビティを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET)エンドポイントを呼び出します。最初に、アクティビティの取得を開始する日時のページングトークンを取得する必要があります。次に、`nextPageToken` クエリパラメーターでページングトークンを渡します。さらに、`activityTypeIds` クエリパラメーターに、最大 10 個のアクティビティタイプ ID をコンマ区切りのリストとして渡します。

オプションで、listId クエリパラメーターを追加して、特定の静的リストに含まれるレコードのみに検索を絞り込むことも、leadIds クエリパラメーターを追加して、指定したリードセットのみのアクティビティを検索することもできます。最大 30 個の leadId をコンマ区切りのリストとして渡すことができます。

```
GET /rest/v1/activities.json?activityTypeIds=1&nextPageToken=WQV2VQVPPCKHC6AQYVK7JDSA3I3LCWXH3Y6IIZ7YSGQLXHCPVE5Q====
```

```json
{
  "requestId": "24fd#15188a88d7f",
  "result": [
    {
      "id": 102988,
      "marketoGUID": "102988",
      "leadId": 1,
      "activityDate": "2023-01-16T23:32:19Z",
      "activityTypeId": 1,
      "primaryAttributeValueId": 71,
      "primaryAttributeValue": "localhost/munchkintest2.html",
      "attributes": [
        {
          "name": "Client IP Address",
          "value": "10.0.19.252"
        },
        {
          "name": "Query Parameters",
          "value": ""
        },
        {
          "name": "Referrer URL",
          "value": ""
        },
        {
          "name": "User Agent",
          "value": "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.95 Safari/537.36"
        },
        {
          "name": "Webpage URL",
          "value": "/munchkintest2.html"
        }
      ]
    }
  ],
  "success": true,
  "nextPageToken": "WQV2VQVPPCKHC6AQYVK7JDSA3J62DUSJ3EXJGDPTKPEBFW3SAVUA====",
  "moreResult": false
}
```

最初の呼び出しでは、Get Paging Token API を使用して `nextPageToken` を取得します。このエンドポイントへの後続の呼び出しでは、応答から返された `nextPageToken returned` を使用します。このエンドポイントは常に `the nextPageToken` を返します。

`moreResult` 属性が true の場合、さらに多くの結果が使用可能です。`moreResult` 属性が false を返すまで、つまり使用可能な結果が存在しなくなるまで、このエンドポイントを引き続き呼び出します。この API から返される `nextPageToken` は、この呼び出しの次の反復で常に再利用する必要があります。

場合によっては、この API は 300 未満のアクティビティ項目で応答しますが、`moreResult` 属性は true に設定されます。これは、返されるアクティビティがさらに存在することと、返された `nextPageToken` を後続の呼び出しに含めて、エンドポイントでより最近のアクティビティに対してクエリを実行できることを示しています。

各結果配列項目内で、`id` 整数属性は、一意の ID として `marketoGUID` 文字列属性に置き換えられます。

### データ値変更

データ値変更アクティビティには、アクティビティ API の専用バージョンが提供されます。[リード変更を取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadChangesUsingGET)エンドポイントでは、データ値変更レコードのアクティビティのみをリードフィールドに返します。インターフェイスは Get Lead Activities API と同じですが、次の 2 つの違いがあります。

* エンドポイントは、データ値変更アクティビティと新規リードアクティビティのみを返すので、`activityTypeIds` パラメーターはありません。
* `fields` クエリパラメーターは必須です。ここでは、変更を取得するフィールドを示すために、コンマ区切りのフィールドリストを渡すことができます。

```
GET /rest/v1/activities/leadchanges.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ&fields=firstName,lastName,department
```

```json
{
  "requestId": "a9ae#148add1e53d",
  "success": true,
  "nextPageToken": "GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBRGA3TQ===",
  "moreResult": true,
  "result": [
    {
      "id": 1078,
      "marketoGUID": "1078",
      "leadId": 775,
      "activityDate": "2014-09-17T22:31:49+0000",
      "activityTypeId": 13,
      "fields": [
        {
          "id": 48,
          "name": "firstName",
          "newValue": "FirstName_6176",
          "oldValue": "FirstName_4914"
        }
      ],
      "attributes": [
        {
          "name": "Reason",
          "value": "Web service API"
        },
        {
          "name": "Source",
          "value": "Web service API"
        },
        {
          "name": "Lead ID",
          "value": 775
        }
      ]
    }
  ]
}
```

応答内の各アクティビティには、アクティビティ内の変更のリストを含むフィールド配列があり、変更されたフィールドの `id` と `name`、変更に関連する新しい値と古い値が指定されます。

各結果配列項目内で、`id` 整数属性は、一意の ID として `marketoGUID` 文字列属性に置き換えられます。

### 削除されたリード

Marketo から削除されたアクティビティを取得するための特別なエンドポイントの[削除されたリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET)もあります。

```
GET /rest/v1/activities/deletedleads.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ
```

```json
{
  "requestId": "a9ae#148add1e53d",
  "success": true,
  "nextPageToken": "GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBRGA3TQ===",
  "moreResult": true,
  "result": [
    {
      "id": 2,
      "marketoGUID": "2",
      "leadId": 6,
      "activityDate": "2013-09-26T06:56:35+0000",
      "activityTypeId": 37,
      "primaryAttributeValueId": 6,
      "primaryAttributeValue": "Owyliphys Iledil",
      "attributes": []
    },
    {
      "id": 3,
      "marketoGUID": "3",
      "leadId": 9,
      "activityDate": "2013-12-28T00:39:45+0000",
      "activityTypeId": 37,
      "primaryAttributeValueId": 4,
      "primaryAttributeValue": "First Last",
      "attributes": []
    }
  ]
}
```

各結果配列項目内で、`id` 整数属性は、一意の ID として `marketoGUID` 文字列属性に置き換えられます。

### ページスルーの結果

デフォルトでは、この節で説明するエンドポイントは、一度に 300 個のアクティビティ項目を返します。`moreResult` 属性が true の場合、さらに多くの結果が使用可能です。`moreResult` 属性が false を返すまで、つまり使用可能な結果が存在しなくなるまで、エンドポイントを呼び出します。このエンドポイントから返される `nextPageToken` は、この呼び出しの次の反復で常に再利用する必要があります。

場合によっては、このエンドポイントは 300 未満のアクティビティ項目で応答しますが、`moreResult` 属性は true に設定されます。これは、返されるアクティビティがさらに存在し、返された `nextPageToken` を後続の呼び出しに含めることで、エンドポイントでより最近のアクティビティに対してクエリを実行できることを示しています。`nextPageToken` は、リクエスト内で URL エンコードする必要があります。

## カスタムアクティビティタイプ

カスタムアクティビティは、標準アクティビティと同様に機能しますが、スキーマが Marketo ではなくサードパーティによって管理される点が異なります。カスタムアクティビティのインスタンスは、標準アクティビティと同様に `leadId` を通じてリードレコードにリンクされますが、プライマリ属性とセカンダリ属性の両方が任意に定義されます。カスタムアクティビティタイプが承認されると、対応するスマートリストトリガーとフィルターが作成され、現在のカスタムアクティビティデータまたは履歴カスタムアクティビティデータに基づいてリードを処理できます。

* カスタムアクティビティの最大数：10
* カスタムアクティビティあたりの属性の最大数：20

カスタムアクティビティデータの取得は、標準アクティビティと同じ方法で、[Get Lead Activities](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET) API を通じて行われます。

## クエリタイプ

標準の「アクティビティタイプを取得」エンドポイントに加えて、[カスタムアクティビティタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getCustomActivityTypeUsingGET)エンドポイントおよび[カスタムアクティビティタイプを説明](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/describeCustomActivityTypeUsingGET)エンドポイントでは、Marketo インスタンスでプロビジョニングされたアクティビティタイプの詳細と、特定のタイプの属性に関するメタデータを返します。通常の[アクティビティタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getAllActivityTypesUsingGET)では、カスタムアクティビティに関するメタデータが返されますが、特定のタイプがカスタムであるかどうかは示されません。

### タイプの取得

```
GET /rest/v1/activities/external/types.json
```

```json
{
  "requestId": "185d6#14b51985ff0",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attends Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved"
    }
  ]
}
```

### タイプの説明

タイプの説明では、`apiName` をパスパラメーターとして渡す必要があります。デフォルトでは、アクティビティの承認済みバージョンが取得されます。オプションで `draft=true` パラメーターを渡して、アクティビティのドラフトバージョンを取得できます。

```
GET /rest/v1/activities/external/type/{apiName}/describe.json
```

```json
{
  "requestId": "185d6#14b51985ff0",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attends Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      },
      "attributes": [
        {
          "apiName": "conferenceDate",
          "name": "Conference Date",
          "description": "Date of the conference",
          "dataType": "datetime"
        },
        {
          "apiName": "numberOfAttendees",
          "name": "Number of Attendees",
          "description": "Number of people attending conference",
          "dataType": "integer"
        }
      ]
    }
  ]
}
```

## タイプの作成

各カスタムアクティビティタイプには、表示名、API 名、トリガー名、フィルター名およびプライマリ属性が必要です。

タイプと Marketo 規則の一貫性を確保し、競合を回避するには、タイプを作成する際にいくつかのガイドラインに従うことが重要です。

**表示名：**&#x200B;アクティビティタイプの表示名では、「メールを送信」や「データ値を変更」など、アクティビティレコードが表す内容を簡単に説明する必要があります。これらの名前は通常、「Attend Event（イベントに参加）」という不定詞形式で指定する必要があります。表示名には、英数字、スペース、アンダースコアを使用できます。表示名には 1 文字以上を含める必要があります。

**API 名：** API 名は、英数字（最大長 255）で構成されています。Launchpoint パートナーの場合は、アクティビティタイプの API 名の前に代表的な名前空間を追加する必要があります。これは、お客様がプロビジョニングしたタイプとの競合を回避するためです。規則では、他のテキスト文字列を区別しやすくするために、すべて小文字または camelCase を使用します。

**説明：**&#x200B;明確でない動作をする場合があるアクティビティについては、リードとの関係でアクティビティタイプが表している内容の説明を含める必要があります。

**トリガー名：**&#x200B;各アクティビティタイプには、一意で人間が読み取れるトリガー名が必要です。トリガー名は、「Attends an Event（イベントに参加）」など、三人称現在形で指定する必要があります。Launchpoint パートナーは、「ウェビナーに参加 - Acme Company」など、アクティビティに会社名を含める必要があります。

**フィルター名：**&#x200B;各アクティビティタイプには、一意で人間が読み取れるフィルター名が必要です。フィルター名は、「Attended an Event（イベントに参加しました）」など、三人称過去形で指定する必要があります。Launchpoint パートナーは、「ウェビナーに参加しました - Acme Company」など、アクティビティに会社名を含める必要があります。

**プライマリ属性：**&#x200B;カスタムアクティビティのプライマリ属性は、アクティビティタイプに対して最も重要なフィールドに指定する必要があります。例えば、「Attended Event（イベントに参加しました）」アクティビティの場合、これはイベントの名前になります。プライマリ属性は、このアクティビティタイプのトリガーまたはフィルターのすべてのインスタンスにデフォルトでパラメーターとして含まれ、アクティビティへのドリルダウンを必要とせずに、ユーザレコードのアクティビティログに値が表示されます。

カスタムアクティビティを作成すると、ドラフトとして作成されます。また、このタイプのアクティビティレコードを追加するために、使用する前に承認される必要があります。すべての更新は、このタイプのドラフトバージョンに暗黙的に適用されます。このタイプのライブバージョンに変更を反映するには、承認される必要があります。カスタムアクティビティタイプが承認され、使用中の場合、上記のフィールドを変更できません。

タイプを作成する際、description パラメーターはオプションですが、`apiName`、`name`、`triggerName`、`filterName`、`primaryAttribute` のすべてのパラメーターは必須です。

```
POST /rest/v1/activities/external/type.json
```

```json
{
  "apiName": "attendConference",
  "name": "Attend Conference",
  "description": "Attend the conference",
  "triggerName": "Attends Conference",
  "filterName": "Attended Conference",
  "primaryAttribute": {
    "apiName": "conferenceName",
    "name": "Conference Name",
    "description": "Name of the conference"
  }
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attends Conference",
      "filterName": "Attended Conference",
      "status": "draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      }
    }
  ]
}
```

## タイプの更新

タイプの更新は非常に似ていますが、パスパラメーターとして必要なパラメーターは apiName のみである点が異なります。

```
POST /rest/v1/activities/external/type/{apiName}.json
```

```json
{
  "name": "Attend Conference",
  "description": "Attend the conference",
  "triggerName": "Attend Conference",
  "filterName": "Attended Conference",
  "primaryAttribute": {
    "apiName": "conferenceName",
    "name": "Conference Name",
    "description": "Name of the conference"
  }
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attend Conference",
      "filterName": "Attended Conference",
      "status": "draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      }
    }
  ]
}
```

## タイプの承認

タイプは、標準の Marketo アセットと同様に、「カスタムアクティビティタイプを承認」、「カスタムアクティビティタイプのドラフトを破棄」、「カスタムアクティビティタイプを削除」を使用して管理できます。

## カスタムアクティビティタイプの属性

各カスタムアクティビティタイプには、0～20 個のセカンダリ属性を指定できます。セカンダリ属性には、Marketo フィールドに有効な任意のフィールドタイプを指定できます。これらは親タイプとは別に追加、更新、削除されますが、アクティビティタイプの使用中に編集して承認できます。ライブタイプでフィールドを編集する際、承認後に作成されたこのタイプのすべてのアクティビティに新しいセカンダリ属性が指定されます。変更は、このタイプを共有する既存のアクティビティに遡って適用されることはありません。

属性を削除すると、対応するフィルターでの使用ができなくなります。

セカンダリ属性リストの更新では、各属性の API 名がプライマリキーとして使用されます。属性の API 名は変更できません。削除して、目的の API 名で再度追加する必要があります。

属性の有効なデータタイプは、文字列、ブール値、整数、浮動小数点、リンク、メール、通貨、日付、日時、電話、テキストです。

アクティビティタイプのプライマリ属性を変更する際は、最初に `isPrimary` を false に設定して、既存のプライマリ属性を降格させる必要があります。

### 属性の作成

属性の作成には、必須の `apiName` パスパラメーターを使用します。また、`name` パラメーターと `dataType` パラメーターも必須です。`The description and` `isPrimary` パラメーターはオプションです。

```
POST /rest/v1/activities/external/type/{apiName}/attributes/create.json
```

```json
{
  "attributes": [
    {
      "apiName": "conferenceDate",
      "name": "Conference Date",
      "description": "Date of the conference",
      "dataType": "datetime"
    },
    {
      "apiName": "numberOfAttendees",
      "name": "Number of Attendees",
      "description": "Number of people attending conference",
      "dataType": "integer"
    }
  ]
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attend Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved with draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      },
      "attributes": [
        {
          "apiName": "conferenceDate",
          "name": "Conference Date",
          "description": "Date of the conference",
          "dataType": "datetime"
        },
        {
          "apiName": "numberOfAttendees",
          "name": "Number of Attendees",
          "description": "Number of people attending conference",
          "dataType": "integer"
        }
      ]
    }
  ]
}
```

### 属性の更新

属性の更新を実行する場合、属性の `apiName` がプライマリキーになります。更新を成功させるには、`apiName` パラメーターが存在している必要があります（つまり、更新を使用して `apiName` パラメーターを変更できません）。

```
POST /rest/v1/activities/external/type/{apiName}/attributes/update.json
```

```json
{
  "attributes": [
    {
      "apiName": "conferenceDate",
      "name": "Conference Date",
      "description": "Date of the conference",
      "dataType": "datetime"
    },
    {
      "apiName": "numberOfAttendee",
      "name": "Number of Attendee",
      "description": "Number of people attending conference",
      "dataType": "integer"
    }
  ]
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attend Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved with draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      },
      "attributes": [
        {
          "apiName": "conferenceDate",
          "name": "Conference Date",
          "description": "Date of the conference",
          "dataType": "datetime"
        },
        {
          "apiName": "numberOfAttendee",
          "name": "Number of Attendee",
          "description": "Number of people attending conference",
          "dataType": "integer"
        }
      ]
    }
  ]
}
```

### 属性の削除

属性の削除するには、カスタムアクティビティの API 名である必須の `apiName` パスパラメーターを受け取ります。また、属性オブジェクトの配列である属性パラメーターも必要です。各オブジェクトには、カスタムアクティビティタイプの API 名である `apiName` パラメーターを含める必要があります。

```
POST /rest/v1/activities/external/type/{apiName}/attributes/delete.json
```

```json
{ "attributes":[ { "apiName":"conferenceDate" }, { "apiName":"numberOfAttendees" } ] }
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attend Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved with draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      }
    }
  ]
}
```

## カスタムアクティビティの追加

カスタムアクティビティは、Marketo 内の個々のユーザレコードに関連する履歴アクティビティの追記型レコードです。これらのアクティビティには、Marketo Admin によって管理されるスキーマや、API 統合を通じてリモートで管理されるスキーマがあります。カスタムアクティビティは、[カスタムアクティビティを追加](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/addCustomActivityUsingPOST)エンドポイント経由でリードレコードに追加され、`leadId` フィールド経由で各リードレコードに関連付けられます。カスタムアクティビティは、リードアクティビティログ経由でユーザインターフェイスで表示したり、カスタムアクティビティのタイプ ID を指定して「リードアクティビティを取得」エンドポイント経由で取得したりできます。

カスタムアクティビティは、単一のユーザレコードに関連し、更新または上書きする必要のないデータを記録するのに適しています。例えば、イベントに参加したユーザを「イベントに参加済み」アクティビティとして記録することが考えられます。変更の可能性があり、ユーザに関連するレコード（学生の登録など）では、カスタムアクティビティで更新できない場合があるので、代わりに更新可能なカスタムオブジェクトを使用する必要があります。

入力メンバーは、アクティビティオブジェクトの配列です。一度に送信できるアクティビティレコードは最大 300 個です。

`leadId`、`activityDate`、`activityTypeId`、`primaryAttributeValue`、attributes メンバーは必須です。attributes 配列には、プライマリ以外の属性を含める必要があります。これは、name（フィールド名）または apiName（API 名）と、設定する値に対応する値のいずれかを使用して指定できます。

```
POST /rest/v1/activities/external.json
```

```json
{
  "input": [
    {
      "leadId": 1001,
      "activityDate": "2016-09-26T06:56:35+07:00",
      "activityTypeId": 1001,
      "primaryAttributeValue": "Game Giveaway",
      "attributes": [
        {
          "apiName": "uRL",
          "value": "http://www.nvidia.com/game-giveaway"
        }
      ]
    },
    {
      "leadId": 1200,
      "activityDate": "2016-09-26T06:56:35+07:00",
      "activityTypeId": 1001,
      "primaryAttributeValue": "Game Giveaway",
      "attributes": [
        {
          "apiName": "uRL",
          "value": "http://www.nvidia.com/game-giveaway"
        }
      ]
    },
    {
      "leadId": 3000,
      "activityDate": "2016-09-26T06:56:35+07:00",
      "activityTypeId": 1001,
      "primaryAttributeValue": "Contest Form",
      "attributes": [
        {
          "apiName": "uRL",
          "value": "http://www.nvidia.com/game-giveaway"
        }
      ]
    }
  ]
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "id": 50,
      "marketoGUID": "50",
      "status": "added"
    },
    {
      "id": 51,
      "marketoGUID": "51",
      "status": "added"
    },
    {
      "status": "skipped",
      "errors": [
        {
          "code": "1004",
          "message": "Lead not found"
        }
      ]
    }
  ]
}
```

## タイムアウト

「アクティビティ」エンドポイントのタイムアウトは 30 秒です（以下に記載されている場合を除く）。

* ページングトークンの取得：300 秒
* カスタムを追加アクティビティ：90 秒
