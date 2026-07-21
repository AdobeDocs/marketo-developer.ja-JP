---
title: アクティビティ
feature: REST API
description: Marketo Engage アクティビティ REST APIを使用して、アクティビティタイプの一覧表示、ページングトークンを使用したリードアクティビティの取得、カスタム値およびデータ値の変更の処理を行います。
exl-id: 1e69af23-2b0c-467a-897c-1dcf81343e73
TQID: https://experienceleague.adobe.com/62keaj4uNoxIPCzr9AQzKrIsfuHBvC25knYisZRUvF4
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1758
ht-degree: 6%

---

# アクティビティ

Marketoは、リードレコードに関連する多くのアクティビティタイプをサポートしています。 リードの変更、アクション、フローの各ステップのほぼすべてが、アクティビティログに記録されます。 これらのアクティビティは、APIを介して取得するか、スマートリストおよびスマートキャンペーンのフィルターとトリガーで使用できます。

各アクティビティには一意の`id`があり、レコードのID フィールドに対応する`leadId`を通じてリードレコードに接続します。 すべてのアクティビティには`activityDate`もあります。

利用できるアクティビティタイプはサブスクリプションによって異なり、各タイプには独自の定義があります。 `primaryAttributeValueId`と`primaryAttributeValue`の意味は、アクティビティタイプによって異なります。

カスタムアクティビティメタデータ APIを使用して、カスタムアクティビティタイプを作成します。 カスタムアクティビティを追加APIを使用して、カスタムアクティビティレコードを追加します。

ほとんどのアクティビティは、一定期間後にパージされます。

## 説明

「[&#x200B; アクティビティタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getAllActivityTypesUsingGET)」エンドポイントを使用して、インスタンスで使用可能なアクティビティタイプとその定義を取得します。

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

実際の応答には、より多くの定義が含まれます。 次の例は、「フォームに入力」アクティビティの種類を示しています。 プライマリ属性の「Webform ID」は、送信されたフォームのMarketo IDを参照し、アクティビティをそのアセットにリンクします。

この応答は、アクティビティタイプとそのデータタイプの各可能な属性も定義します。 フィールドが空の場合、その属性は個々のアクティビティレコードから省略されます。

## クエリ

アクティビティを取得するには、[&#x200B; リードアクティビティの取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadActivitiesUsingGET) エンドポイントを使用します。 まず、アクティビティの取得を開始する日時のページングトークンを取得します。 このトークンを`nextPageToken` クエリパラメーターに渡します。

最大10個のアクティビティタイプ IDを、`activityTypeIds` クエリパラメーターのコンマ区切りリストとして渡します。

必要に応じて、次のいずれかのパラメーターを使用してクエリを絞り込みます。

- `listId`は、特定の静的リスト内のレコードに結果を制限します。
- `leadIds`は、コンマ区切りのリストとして提供される、最大30件のリードのアクティビティに結果を制限します。

>[!CAUTION]
>
>2026-12-30以降、ターゲットリストに10,000人以上のリードが含まれる場合、`listId` パラメーターを含む`Get Lead Activities`および`Get Lead Changes` エンドポイントへの呼び出しは失敗します（エラーコード 1003）。 サービスの中断を回避するには、この制限を回避するために、呼び出しが適切にスコープ設定されていることを確認します。 [移行ガイド &#x200B;](migration.md)を参照してください。

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

最初の呼び出しでは、Get Paging Token APIを使用して`nextPageToken`を取得します。 後続の呼び出しごとに、前の応答から返された`nextPageToken`を渡します。 このエンドポイントは常に `nextPageToken` を返します。

`moreResult`がtrueの場合、さらに多くの結果を利用できます。 `moreResult`がfalseになるまで、返された`nextPageToken`でエンドポイントの呼び出しを続行します。

`moreResult`をtrueに設定すると、APIから返されるアクティビティ項目は300未満になります。 この場合、返された`nextPageToken`を別の呼び出しに含めて、より最近のアクティビティを取得します。

各結果配列項目内で、`marketoGUID`文字列属性が`id`整数属性を一意の識別子として置き換えています。

### データ値変更

[&#x200B; リード変更の取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadChangesUsingGET) エンドポイントを使用して、リードフィールドのデータ値変更レコードを取得します。 そのインターフェイスは、次の2つの方法でリード アクティビティを取得APIとは異なります。

- エンドポイントには`activityTypeIds` パラメーターがありません。これは、データ値の変更と新しいリードアクティビティのみを返すためです。
- 必須の`fields` クエリパラメーターは、変更を取得するフィールドのコンマ区切りリストを受け入れます。

>[!CAUTION]
>
>2026-12-30以降、ターゲットリストに10,000人以上のリードが含まれる場合、`listId` パラメーターを含む`Get Lead Activities`および`Get Lead Changes` エンドポイントへの呼び出しは失敗します（エラーコード 1003）。 サービスの中断を回避するには、この制限を回避するために、呼び出しが適切にスコープ設定されていることを確認します。 [移行ガイド &#x200B;](migration.md)を参照してください。

```http
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

レスポンスの各アクティビティには、変更をリストするフィールド配列があります。 各変更は、フィールドの`id`と`name`を、新しい値と古い値とともに指定します。

各結果配列項目内で、`marketoGUID`文字列属性が`id`整数属性を一意の識別子として置き換えています。

### 削除されたリード

[削除されたリードを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getDeletedLeadsUsingGET) エンドポイントを使用して、削除されたリードアクティビティをMarketoから取得します。

```http
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

各結果配列項目内で、`marketoGUID`文字列属性が`id`整数属性を一意の識別子として置き換えています。

### ページスルーの結果

デフォルトでは、このセクションのエンドポイントは一度に300個のアクティビティ項目を返します。 `moreResult`がtrueの場合、さらに多くの結果を利用できます。 `moreResult`がfalseになるまで、返された`nextPageToken`を後続の各呼び出しに渡します。

`moreResult`をtrueに設定すると、エンドポイントから返されるアクティビティ項目の数は300未満になります。 この場合、返された`nextPageToken`を別の呼び出しに含めて、より最近のアクティビティを取得します。 リクエストで`nextPageToken`をURL エンコードします。

## カスタムアクティビティタイプ

カスタムアクティビティは標準アクティビティと同様に機能しますが、サードパーティがスキーマを管理します。 カスタムアクティビティレコードは`leadId`を通じてリードレコードにリンクし、そのプライマリ属性とセカンダリ属性はユーザー定義です。

カスタムアクティビティタイプが承認されると、Marketoは対応するスマートリストトリガーとフィルターを作成します。 その後、現在または過去のカスタムアクティビティデータにもとづいてリードを処理できます。

- カスタムアクティビティの最大数：10
- カスタムアクティビティあたりの最大属性：20

[&#x200B; リードアクティビティを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadActivitiesUsingGET) APIを使用して、標準アクティビティを取得するのと同じ方法で、カスタムアクティビティデータを取得します。

## クエリタイプ

[&#x200B; カスタムアクティビティタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getCustomActivityTypeUsingGET)を使用して、Marketo インスタンスでプロビジョニングされたタイプに関する詳細を取得します。 [&#x200B; カスタムアクティビティタイプの説明](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/describeCustomActivityTypeUsingGET)を使用して、特定のタイプの属性メタデータを取得します。

標準の[Get Activity Types](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getAllActivityTypesUsingGET) エンドポイントは、カスタムアクティビティのメタデータも返しますが、タイプがカスタムであるかどうかも識別しません。

### タイプの取得

```http
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

型を記述するには、`apiName`をパスパラメーターとして渡します。 デフォルトでは、エンドポイントはアクティビティの承認済みバージョンを返します。 ドラフトバージョンを取得するには、オプションの`draft=true` パラメーターを渡します。

```http
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

各カスタムアクティビティタイプには、表示名、API 名、トリガー名、フィルター名およびプライマリ属性が必要です。 次のガイドラインを使用して、Marketoの規則に一致する型を維持し、名前の競合を回避します。

- **表示名：** アクティビティレコードの概要（電子メールの送信やデータ値の変更など）を簡単に説明します。 「イベントに参加」などの不定形形式を使用します。 表示名には、英数字、スペース、およびアンダースコアを使用でき、少なくとも1文字の文字を含める必要があります。

- **API名：**&#x200B;最大長255の英数字を使用します。 LaunchPoint パートナーの場合は、顧客がプロビジョニングしたタイプとの競合を避けるために、アクティビティタイプ API名の前に代表名前空間を追加します。 API名を他の文字列と区別するには、小文字またはキャメルケースを使用します。

- **説明：**&#x200B;明らかでない行動を伴うアクティビティの場合は、リードに関してアクティビティタイプが何を表しているかを説明します。

- **トリガー名：** 「イベントに参加する」など、人が判読できる一意の名前を、3人の現在時制で指定します。 LaunchPoint パートナーは、「Attends Webinar - Acme Company」などの会社名を含める必要があります。

- **フィルター名：** 「イベントに参加しました」など、人が判読できる一意の名前を、3人の過去の時系列で指定します。 LaunchPoint パートナーは、「Attended Webinar - Acme Company」などの会社名を含める必要があります。

- **プライマリ属性：** アクティビティタイプの最も重要なフィールドを選択します。 「出席イベント」アクティビティの場合、このフィールドはイベント名です。 プライマリ属性は、デフォルトでは、アクティビティタイプの各トリガーまたはフィルターのパラメーターとして表示されます。 この値は、アクティビティをドリルダウンすることなく、ユーザーのアクティビティログにも表示されます。

新しいカスタムアクティビティタイプがドラフトとして作成されます。 そのタイプのアクティビティレコードを追加する前に、タイプを承認します。 更新はドラフトバージョンに適用され、ライブバージョンに表示される前に承認する必要があります。 カスタムアクティビティタイプが承認され、使用中の場合、前のフィールドは変更できません。

タイプを作成する場合、説明パラメーターはオプションです。 必要なパラメーターは`apiName`、`name`、`triggerName`、`filterName`および`primaryAttribute`です。

```http
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

タイプを更新するには、必要なapiNameをパスパラメーターとして渡します。 その他のフィールドは、リクエスト本文で指定できます。

```http
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

Marketoの標準アセットと同様に、カスタムアクティビティタイプの承認、カスタムアクティビティタイプのドラフトの破棄、カスタムアクティビティタイプの削除を使用してタイプを管理します。

## カスタムアクティビティタイプの属性

各カスタムアクティビティタイプには、0 ～ 20個のセカンダリ属性を設定できます。 セカンダリ属性では、有効な任意のMarketo フィールドタイプを使用できます。 セカンダリ属性は、親タイプとは別に追加、更新、削除します。

アクティビティタイプの使用中に属性を編集し、変更を承認することができます。 承認後に作成されたアクティビティは、新しいセカンダリ属性セットを使用します。 変更は、そのタイプの既存のアクティビティに過去にさかのぼって適用されません。

属性を削除すると、対応するフィルターの可用性も削除されます。

セカンダリ属性リストの更新では、各属性のAPI名をプライマリキーとして使用します。 API名を変更するには、属性を削除し、目的のAPI名で再度追加します。

属性の有効なデータタイプは、文字列、ブール値、整数、浮動小数点、リンク、メール、通貨、日付、日時、電話、テキストです。

アクティビティタイプのプライマリ属性を変更する前に、`isPrimary`をfalseに設定して、既存のプライマリ属性を格下げします。

### 属性の作成

属性を作成するには、必須の`apiName` パスパラメーターを渡します。 `name`および`dataType` パラメーターも必要です。 説明と`isPrimary` パラメーターはオプションです。

```http
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

属性を更新する場合、属性`apiName`はプライマリキーであり、既に存在する必要があります。 更新内容で`apiName`を変更することはできません。

```http
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

属性を削除するには、カスタムアクティビティに必要な`apiName` パスパラメーターを渡します。 また、必要な属性パラメーターを属性オブジェクトの配列として渡します。 各オブジェクトには、カスタムアクティビティタイプの`apiName` パラメーターを含める必要があります。

```http
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

カスタムアクティビティとは、個人レコードの過去のアクティビティを一度だけ書き込むレコードです。 Marketoの管理者は、Marketoでスキーマを管理できます。また、API統合では、スキーマをリモートで管理できます。

カスタムアクティビティをリードレコードに追加するには、[&#x200B; カスタムアクティビティを追加](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/addCustomActivityUsingPOST) エンドポイントを使用します。 `leadId` フィールドは、各アクティビティをリードに関連付けます。 リードのアクティビティログでカスタムアクティビティを表示するか、カスタムアクティビティタイプ IDを指定してリードアクティビティを取得を通じて取得します。

更新または上書きされない1人のユーザーに関連するデータに対して、カスタムアクティビティを使用します。 例えば、イベントへの参加を「出席イベント」アクティビティとして記録します。

学生の登録など、変更できる人物関連のレコードにカスタムオブジェクトを使用できます。 カスタムオブジェクトは更新できますが、カスタムアクティビティは更新できません。

入力メンバーは、アクティビティオブジェクトの配列です。 一度に最大300件のアクティビティレコードを送信できます。

`leadId`、`activityDate`、`activityTypeId`、`primaryAttributeValue`、attributes メンバーは必須です。 attributes 配列には、プライマリ以外の属性を含める必要があります。 名前（フィールド名）またはapiName （API名）で指定し、設定する値の値を指定します。

```http
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

アクティビティ エンドポイントのタイムアウトは30秒です。ただし、次のエンドポイントは例外です。

- ページングトークンの取得：300秒
- カスタムを追加アクティビティ：90 秒
