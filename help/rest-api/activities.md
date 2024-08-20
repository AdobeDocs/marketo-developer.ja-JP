---
title: アクティビティ
feature: REST API
description: Marketo Engageアクティビティを管理するための API。
source-git-commit: 13a567be067a8a1272e981fad4e03b0a8519f132
workflow-type: tm+mt
source-wordcount: '2029'
ht-degree: 0%

---


# アクティビティ

Marketoでは、リードレコードに関連する様々なアクティビティタイプが許可されています。  ほとんどすべての変更、アクションまたはフローステップは、リードのアクティビティログに対して記録され、API を介して取得したり、スマートリストおよびスマートキャンペーンのフィルターとトリガーで活用したりできます。  アクティビティは、常に、レコードの「ID」フィールドに対応する leadId を介してリードレコードに関連付けられ、独自の一意の ID も持ちます。

潜在的なアクティビティタイプは非常に多数あり、サブスクリプションによって異なる可能性があり、それぞれに一意の定義があります。 すべてのアクティビティには独自の `id`、`leadId`、`activityDate` がありますが、`primaryAttributeValueId` と `primaryAttributeValue` の値はその意味で異なります。

Marketoでは、カスタムアクティビティメタデータ API を使用してカスタムアクティビティタイプを作成することもできます。 カスタムアクティビティの追加は、カスタムアクティビティ追加 API を通じて行われます。

ほとんどのアクティビティは、一定期間後にパージされます。

## 説明

インスタンスで使用可能なタイプとその定義の一覧を取得するには、[ アクティビティタイプを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getAllActivityTypesUsingGET) エンドポイントを使用します。

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

現実の対応には、はるかに多くの定義が含まれています。 この例で表示されるタイプは「入力フォーム」で、プライマリ属性は「Webform ID」です。これは、入力されたフォームのMarketo ID を参照し、Marketoのその特定のアセットに関連付けるために使用できます。 さらに、このタイプの特定のアクティビティレコードの可能な属性ごとに、そのデータタイプに関する定義があります。 フィールドが空の場合、その特定の属性は個々のアクティビティレコードから省略されます。

## クエリ

Marketoからアクティビティを取得するには、[ リードアクティビティを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET) エンドポイントを呼び出します。 最初に、アクティビティの取得を開始する日時のページングトークンを取得する必要があります。 その後、`nextPageToken` クエリパラメーターでページングトークンを渡します。 さらに、`activityTypeIds` クエリパラメーターで最大 10 個のアクティビティタイプ ID を、コンマ区切りリストとして渡します。

オプションで、listId クエリパラメーターを含めて、特定の静的リストに含まれるレコードのみに検索を絞り込むか、leadIds クエリパラメーターを含めて、指定したリードセットからのみアクティビティを検索することができます。 最大 30 個の leadIds をコンマ区切りリストとして渡すことができます。

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

最初の呼び出しでは、ページングトークン API を取得に使用 `nextPageToken` ます。 このエンドポイントへの後続の呼び出しには、応答の `nextPageToken returned` を使用します。 このエンドポイントは常に `the nextPageToken` を返します。

`moreResult` 属性が true の場合は、より多くの結果が利用可能であることを意味します。 `moreResult` 属性が false を返す（使用できる結果がないことを意味する）まで、このエンドポイントの呼び出しを続行します。 この API から返された `nextPageToken` は、この呼び出しの次のイテレーションでは常に再利用する必要があります。

場合によっては、この API は 300 個未満のアクティビティ項目で応答する一方で、`moreResult` 属性が true に設定されることもあります。  これは、返される可能性のあるアクティビティがより多く、返されたアクティビティを後続の呼び出しに含めることで、エンドポイントに対してより新しいアクティビティのクエ `nextPageToken` を実行できることを示しています。

各結果配列項目内では、`id` integer 属性が一意の識別子として `marketoGUID` string 属性に置き換えられています。 

## データ値変更

データ値の変更アクティビティの場合は、アクティビティ API の専用バージョンが提供されます。 [ リード変更を取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadChangesUsingGET) エンドポイントは、データ値変更レコードのアクティビティをリードフィールドにのみ返します。 このインターフェイスは、Get Lead Activities API と同じですが、次の 2 つの違いがあります。

* エンドポイントは「データ値の変更」アクティビティと「新しいリード」アクティビティのみを返すので、`activityTypeIds` のパラメーターはありません。
* `fields` クエリパラメーターは必須です。このパラメーターで、フィールドのコンマ区切りリストを渡して、変更を取得するフィールドを示すことができます。

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

応答内の各アクティビティにはフィールド配列があります。この配列には、変更されたフィールドの `id` と `name`、および変更に関連する新しい値と古い値を指定する、アクティビティの変更のリストが含まれています。

各結果配列項目内では、`id` integer 属性が一意の識別子として `marketoGUID` string 属性に置き換えられています。

## 削除されたリード

また、Marketoから削除されたアクティビティを取得するための特別なエンドポイント [ 削除されたリードの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET) もあります。

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

各結果配列項目内では、`id` integer 属性が一意の識別子として `marketoGUID` string 属性に置き換えられています。

## ページスルーの結果

デフォルトでは、この節で説明するエンドポイントは、一度に 300 個のアクティビティ項目を返します。  `moreResult` 属性が true の場合は、より多くの結果を利用できます。 `moreResult` 属性が false を返し、使用できる結果がなくなるまでエンドポイントを呼び出します。 このエンドポイントから返された `nextPageToken` は、この呼び出しの次の反復で常に再利用する必要があります。

場合によっては、このエンドポイントは、300 個未満のアクティビティ項目で応答する一方で、`moreResult` 属性が true に設定されている場合もあります。  つまり、返される追加のアクティビティがあり、返されたアクティビティを後続の呼び出しに含めることで、エンドポイントに対してより新しいアクティビティのクエ `nextPageToken` を行うことができます。 リクエストでは `nextPageToken` を URL エンコードする必要があります。

## カスタムアクティビティタイプ

カスタムアクティビティは、標準アクティビティと同様に機能します。ただし、スキーマはMarketoではなく、サードパーティによって管理されます。 カスタムアクティビティのインスタンスは、標準アクティビティと同様に `leadId` 経由でリードレコードにリンクされますが、プライマリ属性とセカンダリ属性の両方が任意に定義されます。 カスタム・アクティビティ・タイプが承認されると、対応するスマート・リスト・トリガーおよびフィルタが作成され、現在または過去のカスタム・アクティビティ・データに基づいてリードを処理できます。

* カスタムアクティビティの最大数：10
* カスタムアクティビティあたりの最大属性数：20

カスタムアクティビティデータの取得は、[ リードアクティビティを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET) API を使用して、標準のアクティビティと同じ方法で行います。

## クエリタイプ

標準のアクティビティタイプの取得エンドポイントに加えて、[ カスタムアクティビティタイプの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getCustomActivityTypeUsingGET) エンドポイントと [ カスタムアクティビティタイプの説明 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/describeCustomActivityTypeUsingGET) エンドポイントは、Marketo インスタンスでプロビジョニングされたアクティビティタイプの詳細と、特定のタイプの属性に関するメタデータを返します。 通常の [ アクティビティタイプを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getAllActivityTypesUsingGET) では、引き続きカスタムアクティビティに関するメタデータが返されますが、特定のタイプがカスタムかどうかは示されません。

### タイプを取得

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

タイプの説明には、`apiName` をパスパラメーターとして渡す必要があります。 デフォルトでは、アクティビティの承認済みバージョンが取得されます。 オプションで、`draft=true` パラメーターを渡して、アクティビティのドラフトバージョンを取得できます。

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

### タイプを作成

カスタムアクティビティタイプごとに、表示名、API 名、トリガー名、フィルター名およびプライマリ属性が必要です。

型とMarketoの規則の一貫性を確保し、競合を避けるために、型を作成する際には、次のガイドラインに従うことが重要です。

**表示名：** アクティビティタイプの表示名では、「メールの送信」や「データ値の変更」など、アクティビティレコードが表す内容を簡単に説明する必要があります。 これらの名前は通常、「Attend Event」という不定詞の形式で指定します。  表示名には、英数字、スペース、アンダースコアを使用できます。 表示名には少なくとも 1 文字を含める必要があります。

**API 名：** API 名は英数字（最大長 255）で構成されています。 LaunchPoint パートナーの場合は、アクティビティタイプの API 名の前に代表的な名前空間を付加する必要があります。 これは、顧客がプロビジョニングしたタイプとの競合を避けるためです。  規則では、他のテキスト文字列を区別するために、すべての小文字または camelCase を使用します。

**説明：** アクティビティが明確でない可能性がある場合は、アクティビティの種類がリードと何を表しているかの説明を含める必要があります。

**トリガー名：** 各アクティビティの種類には、人間が読み取れる一意のトリガー名が必要です。 トリガー名は、「あるイベントに出席する」のように、3 人目現在形にする必要があります。 LaunchPoint パートナーは、「出席ウェビナー – Acme Company」のように、アクティビティに会社名を含める必要があります。

**フィルター名：**  各アクティビティタイプには、人間が判読できる一意のフィルター名が必要です。 フィルター名は、「Attended an Event」のように、3 人称の過去形にする必要があります。 LaunchPoint パートナーは、「出席ウェビナー – Acme Company」という企業名をアクティビティに含める必要があります。

**プライマリ属性：** カスタムアクティビティのプライマリ属性は、アクティビティタイプの最も重要なフィールドである必要があります。 例えば、「出席イベント」アクティビティの場合、これはイベントの名前になります。 プライマリ属性は、そのアクティビティ・タイプのトリガーまたはフィルタのすべてのインスタンスに、デフォルトでパラメータとして含まれています。この値は、アクティビティへのドリルダウンを必要とせずに、個人レコードのアクティビティ・ログに表示されます。

カスタムアクティビティを作成すると、そのアクティビティはドラフトとして作成されます。そのタイプのアクティビティレコードの追加に使用する前に、承認する必要があります。 すべての更新は、タイプのドラフトバージョンに暗黙的に適用されます。 タイプのライブバージョンに変更を反映するには、タイプを承認する必要があります。 カスタムアクティビティタイプが承認され、使用中の場合、上記のフィールドは変更されません。

タイプを作成する場合、説明パラメーターはオプションですが、パラメーター `apiName`、`name`、`triggerName`、`filterName`、`primaryAttribute` はすべて必須です。

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

### 更新の種類

タイプの更新は非常によく似ていますが、apiName がパスパラメーターとして必要な唯一のパラメーターである点が異なります。

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

## 承認タイプ

タイプは、標準のMarketo Assets と同様に、「カスタムアクティビティタイプを承認」、「カスタムアクティビティタイプのドラフトを破棄」、「カスタムアクティビティタイプを削除」で管理できます。


## カスタムアクティビティタイプの属性

各カスタムアクティビティタイプには、0～20 のセカンダリ属性を指定できます。 セカンダリ属性には、Marketo フィールドに有効なフィールドタイプを含めることができます。 追加、更新、削除は親タイプとは別に行われますが、アクティビティタイプを使用中に編集してから承認することができます。 ライブタイプでフィールドを編集する場合、承認後に作成されたそのタイプのすべてのアクティビティには、新しいセカンダリ属性が設定されます。 そのタイプを共有している既存のアクティビティに対する変更は、さかのぼって適用されません。

属性の削除は、対応するフィルターで使用する際に影響を与えるので、注意が必要です。

セカンダリ属性リストに対して行われた更新では、各属性の API 名がプライマリキーとして使用されます。 属性の API 名は変更できません。削除して、目的の API 名で再度追加する必要があります。

属性の有効なデータタイプは、文字列、ブール値、整数、浮動小数点、リンク、メール、通貨、日付、日時、電話、テキストです。

アクティビティタイプのプライマリ属性を変更する場合は、まず `isPrimary` を false に設定して、既存のプライマリ属性をすべて降格させる必要があります。

## 属性を作成

属性の作成には、必須の `apiName` パスパラメーターを使用します。 `name` パラメーターと `dataType` パラメーターも必須です。`isPrimary`` The description and` パラメーターはオプションです。

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

## 属性を更新

属性の更新を実行する場合、属性の `apiName` がプライマリキーになります。 更新を成功させるには、`apiName` パラメーターが存在する必要があります（つまり、update を使用して `apiName` パラメーターを変更することはできません）。

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

## 属性を削除

属性を削除するには、必須の `apiName` パスパラメーター（カスタムアクティビティ API 名）を使用します。  また、属性オブジェクトの配列である属性パラメーターも必要です。  各オブジェクトには、カスタムアクティビティタイプの API 名である `apiName` パラメーターを含める必要があります。

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

カスタムアクティビティは、Marketo内の個々の人物レコードに関連する履歴アクティビティの追記型レコードです。 これらのアクティビティには、Marketo管理者によって、または API 統合を介してリモートで管理されるスキーマがあります。 カスタムアクティビティは、[ カスタムアクティビティの追加 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/addCustomActivityUsingPOST) エンドポイントを介してリードレコードに追加され、`leadId` フィールドを介して各リードレコードに関連付けられます。 カスタムアクティビティは、リードのアクティビティログを使用してユーザーインターフェイスで表示したり、カスタムアクティビティのタイプ ID を指定することで、リードアクティビティを取得エンドポイントで取得したりできます。

カスタムアクティビティは、1 人の人物レコードに関連し、更新や上書きを必要としないデータの記録に適しています。 例えば、イベントに参加する人を「出席イベント」アクティビティとして記録するとします。 学生登録など、変更される可能性のある人物に関連するレコードの場合は、カスタムオブジェクトを代わりに使用してください。カスタムオブジェクトは更新できますが、カスタムアクティビティは更新できません。

入力メンバーは、アクティビティオブジェクトの配列です。 一度に送信できるアクティビティレコードは最大 300 個です。

`leadId`、`activityDate`、`activityTypeId`、`primaryAttributeValue`、および属性メンバーが必要です。 属性配列には非プライマリ属性を含める必要があります。 これは、name （フィールド名）または apiName （API 名）、および設定している値に対応する値を使用して指定できます。

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

アクティビティエンドポイントのタイムアウトは、以下に示す場合を除き 30 秒です。

* ページングトークンの取得：300 秒 
* カスタム アクティビティの追加：90s 