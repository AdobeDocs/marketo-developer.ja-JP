---
title: リード
feature: REST API
description: Marketoが提供するREST APIの機能には、説明、IDまたはフィルターによるクエリ、デフォルトフィールド、制限、ECIDの取得などがあります。
exl-id: 0a2f7c38-02ae-4d97-acfe-9dd108a1f733
TQID: https://experienceleague.adobe.com/jZ-ecWTmHwq9gvp4fMaeuuGba6cgwYx0QCCyfkrEDHQ
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: a7170d27-32ab-462b-a333-269abc654483id: b0bb9048-d951-48d8-8232-45cf248a7e27id: c5f60233-d5ea-4453-a799-0ad258b4d399id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 2728
ht-degree: 11%

---

# リード

[リードエンドポイントリファレンス](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads)

Marketo リード APIは、リードレコードに対するCRUD操作をサポートしています。 また、静的リストおよびプログラムにおけるリードのメンバーシップを変更し、リードに対してスマートキャンペーン処理を開始することもできます。

## 説明

「リードを記述」を使用して、REST APIで使用可能なフィールドと各フィールドのメタデータを取得します。

- データタイプ
- REST API名
- 長さ（該当する場合）
- 読み取り専用ステータス
- わかりやすいラベル

「説明」は、フィールドの可用性とメタデータに関する信頼できる唯一の情報源です。

### リクエスト

```http
GET /rest/v1/leads/describe.json
```

### 応答

```json
{
   "requestId":"37ca#1475b74e276",
   "success":true,
   "result":[
      {
         "id":2,
         "displayName":"Company Name",
         "dataType":"string",
         "length":255,
         "rest":{
            "name":"company",
            "readOnly":false
         },
         "soap":{
            "name":"Company",
            "readOnly":false
         }
      }
}
```

実際の応答では、結果の配列にフィールドが追加されます。 各項目は、リードレコードで使用可能なフィールドを表し、少なくともID、displayName、およびデータタイプを含みます。

rest オブジェクトとsoap子オブジェクトは、対応するAPIに対してフィールドが有効な場合にのみ表示されます。 `readOnly` プロパティは、対応するAPIがフィールドを更新できるかどうかを示します。 存在する場合、length プロパティは最大フィールド長を与え、dataType プロパティはフィールドのデータタイプを与えます。

## クエリ

リードを取得するには、次のふたつの方法のいずれかを使用します。

- Get Lead by Idは、1つのリード IDをパスパラメーターとして受け取り、1つのリードレコードを返します。
- フィルタータイプでリードを取得は、選択したフィールドが指定された値のいずれかに一致するレコードを検索します。

「リードをIDで取得」では、オプションで、フィールド名のコンマ区切りリストを含むフィールドパラメーターを渡して返します。 リクエストでフィールドが省略された場合、応答には`email`、`updatedAt`、`createdAt`、`lastName`、`firstName`および`id`が含まれます。 要求されたフィールドが返されない場合、その値はnullであることが暗黙的に示されます。

### リクエスト

```http
GET /rest/v1/lead/{id}.json
```

### 応答

```json
{
   "requestId": "10226#14d3049e51b",
   "success": true,
   "result": [
      {
         "id": 318581,
         "updatedAt":"2015-05-07T11:47:30-08:00"
         "lastName": "Doe",
         "email": "jdoe@marketo.com",
         "createdAt": "2015-05-01T16:47:30-08:00",
         "firstName": "John"
      }
   ]
}
```

Get Lead by Idは、常に結果配列の最初の位置にある1つのレコードを返します。

フィルタータイプでリードを取得は、同じレコードタイプを返し、ページごとに最大300件のレコードを返すことができます。 `filterType`と`filterValues`のクエリパラメーターが必要です。

`filterType`は、任意のカスタムフィールドと最もよく使用されるフィールドを受け入れます。 `Describe2` エンドポイントを呼び出して、`filterType`に許可されている検索可能なフィールドを取得します。 カスタムフィールドで検索する場合、サポートされるデータタイプは`string`、`email`および`integer`です。 説明やタイプなどのフィールドの詳細を取得するには、「説明」メソッドを使用します。

`filterValues`は、最大300個のコンマ区切り値を受け入れます。 呼び出しは、選択したリードフィールドがその値のいずれかに一致するレコードを返します。 フィルターに一致するリードが1,000件を超える場合、APIは「1003、フィルターに一致する結果が多すぎる」を返します。

合計GET リクエストが8 KBを超える場合、APIはRFC 7231の下で「414, URI too long」を返します。 この制限を回避するには、GETをPOSTに変更し、_method=GET パラメーターを追加して、クエリ文字列をリクエスト本文に配置します。

### リクエスト

```http
GET /rest/v1/leads.json?filterType=id&filterValues=318581,318592
```

### 応答

```json
{
    "requestId": "12951#15699db5c97",
    "result": [
        {
            "id": 318581,
            "updatedAt": "2016-05-17T22:11:45Z",
            "lastName": "Lincoln",
            "email": "abe@usa.gov",
            "createdAt": "2015-03-17T00:18:40Z",
            "firstName": "Abraham"
        },
        {
            "id": 318592,
            "updatedAt": "2016-05-17T22:20:51Z",
            "lastName": "Washington",
            "email": "george@usa.gov",
            "createdAt": "2015-04-06T16:29:21Z",
            "firstName": "George"
        }
    ],
    "success": true
}
```

この呼び出しは、IDが`filterValues`の値と一致するレコードを返します。

一致するレコードがない場合、応答は成功を示し、空の結果配列が含まれます。

### 応答

```json
{
"requestId": "177a1#1578b643357",
"result": [],
"success": true
}
```

「IDでリードを取得」と「フィルタータイプでリードを取得」の両方で、API フィールドのコンマ区切りリストを含むフィールドクエリパラメーターを使用できます。 フィールドが存在する場合、各応答レコードにはリストされたフィールドが含まれます。 省略した場合、応答には`id`、`email`、`updatedAt`、`createdAt`、`firstName`および`lastName`が含まれます。

## Adobe ECID

Adobe Experience Cloud オーディエンス共有が有効になっている場合、Cookie同期はAdobe Experience Cloud ID （ECID）値をMarketo リードに関連付けます。 前のリード取得方法で関連するECID値を取得するには、「`ecids`」をfields パラメーターに含めます。 例：`&fields=email,firstName,lastName,ecids`。

## 作成と更新

リード APIは、リードレコードを作成、更新、削除できます。 作成と更新の操作は、リクエストで定義された操作タイプと同じエンドポイントを使用します。 1回のリクエストで最大300件のレコードを作成または更新できます。

>[!NOTE]
>
> [リードの同期](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/syncLeadUsingPOST)エンドポイントを使用した会社フィールドの更新はサポートされていません。 代わりに、[会社の同期](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/syncCompaniesUsingPOST)エンドポイントを使用します。

>[!NOTE]
>
> ユーザレコードのメール値を作成または更新する際、メールアドレスフィールドでは ASCII 文字のみがサポートされます。

### リクエスト

```http
POST /rest/v1/leads.json
```

### 本文

```json
{
   "action":"createOnly",
   "lookupField":"email",
   "input":[
      {
         "email":"kjashaedd-1@klooblept.com",
         "firstName":"Kataldar-1",
         "postalCode":"04828"
      },
      {
         "email":"kjashaedd-2@klooblept.com",
         "firstName":"Kataldar-2",
         "postalCode":"04828"
      },
      {
         "email":"kjashaedd-3@klooblept.com",
         "firstName":"Kataldar-3",
         "postalCode":"04828"
      }
   ]
}
```

### 応答

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "id":50,
         "status":"created"
      },
      {
         "id":51,
         "status":"created"
      },
      {
         "id":52,
         "status":"created"
      }
   ]
}
```

リクエストでは、次の2つの重要なフィールドが使用されます。

- `action`は、操作の種類を指定します：`createOrUpdate`、`createOnly`、`updateOnly`、または`createDuplicate`。 省略すると、デフォルトは`createOrUpdate`になります。
- アクションが`createOrUpdate`または`updateOnly`の場合、`lookupField`はキーを指定します。 省略すると、デフォルトは`email`になります。

デフォルトでは、操作はデフォルトのパーティションを使用します。 オプションの`partitionName` パラメーターは、アクションが`createOnly`または`createOrUpdate`の場合にのみ機能します。 `partitionName`を追加の重複除外条件として使用するには、カスタム重複排除ルールのソースタイプに含めます。

更新の際に、指定したパーティションにリードが存在しない場合、またはAPIのみのユーザーがそのパーティションにアクセスできない場合、APIはエラーを返します。

`id`はシステム管理の一意のキーであるため、`updateOnly` アクションにのみ含めます。

リクエストには、リードレコードの配列を含む`input` パラメーターを含める必要があります。 各リードレコードは、任意の数のリードフィールドを持つ JSON オブジェクトです。 キーは各レコード内で一意である必要があり、すべてのJSON文字列はUTF-8 エンコーディングを使用する必要があります。

`externalCompanyId`を使用して、リード レコードを会社レコードにリンクします。 `externalSalesPersonId`を使用して、リード レコードを営業担当者レコードにリンクします。

同時または密接にタイムリーなアップサートリクエストは、複数のリクエストが最初のリクエストが返される前に同じキー値を使用する場合、重複したレコードを作成できます。 重複を防ぐには、適切に`createOnly`または`updateOnly`を使用します。 または、呼び出しをキューに入れ、各呼び出しが返されるのを待ってから、同じキーで別のアップサートを送信します。

## フィールド

リードオブジェクトには、標準フィールドとオプションのカスタムフィールドが含まれています。 標準フィールドはMarketo Engageのサブスクリプションごとに用意されていますが、カスタムフィールドは必要に応じて作成できます。

各フィールド定義には、表示名、API名、dataTypeなどのメタデータ属性が含まれます。

リードオブジェクトのフィールドをクエリ、作成、更新するには、次のエンドポイントを使用します。 API ユーザーの役割には、読み取り/書き込みスキーマ標準フィールド権限、読み取り/書き込みスキーマカスタムフィールド権限、またはその両方が必要です。

## クエリフィールド

API名で1つのリードフィールドをクエリするか、すべてのリードフィールドをクエリします。 役割の権限に応じて、応答には標準フィールド、カスタムフィールド、非表示フィールドを含めることができます。

## 名前別

「名前でリードフィールドを取得」エンドポイントは、1つのリードフィールドのメタデータを取得します。 必須のfieldApiName パスパラメーターは、フィールドのAPI名を指定します。

この応答は、「リードを記述」応答に似ていますが、追加のメタデータが含まれています。 例えば、isCustom属性は、フィールドがカスタムかどうかを示します。

### リクエスト

```http
GET /rest/v1/leads/schema/fields/{fieldApiName}.json
```

### 応答

```json
{
    "requestId": "cd97#1793ee0fec4",
    "result": [
        {
            "displayName": "Email Address",
            "name": "email",
            "description": null,
            "dataType": "email",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        }
    ],
    "success": true
}
```

## 参照

「リードフィールドを取得」エンドポイントは、リードオブジェクトのすべてのフィールドのメタデータを取得します。 デフォルトでは、最大300件のレコードが返されます。 この数を減らすには、`batchSize` クエリパラメーターを使用します。

`moreResult`がtrueの場合、さらに多くの結果を利用できます。 `moreResult`がfalseになるまで、返された`nextPageToken`を後続の各呼び出しに渡します。

### リクエスト

```http
GET /rest/v1/leads/schema/fields.json
```

### 応答（切り捨て）

```json
{
    "requestId": "142c3#1793eb976d8",
    "result": [
        {
            "displayName": "Salutation",
            "name": "salutation",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "First Name",
            "name": "firstName",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Middle Name",
            "name": "middleName",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Last Name",
            "name": "lastName",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Date of Birth",
            "name": "dateOfBirth",
            "description": null,
            "dataType": "date",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Email Address",
            "name": "email",
            "description": null,
            "dataType": "email",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Phone Number",
            "name": "phone",
            "description": null,
            "dataType": "phone",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Mobile Phone Number",
            "name": "mobilePhone",
            "description": null,
            "dataType": "phone",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Fax Number",
            "name": "fax",
            "description": null,
            "dataType": "phone",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Job Title",
            "name": "title",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Unsubscribed",
            "name": "unsubscribed",
            "description": null,
            "dataType": "boolean",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": true,
            "isCustom": false
        },
        ...
    ],
    "success": true,
    "moreResult": false
}
```

## フィールドの作成

リードフィールドを作成エンドポイントは、リードオブジェクトに1つ以上のカスタムフィールドを作成し、Marketo Engage UIと同等の機能を提供します。 このエンドポイントを使用して、最大100個のカスタムフィールドを作成できます。

実稼動インスタンスで作成する前に、各フィールドを慎重に検討します。 フィールドを作成した後、非表示にすることはできますが、削除することはできません。 未使用のフィールドは、インスタンスを混乱させます。

必須の入力パラメーターは、リードフィールドオブジェクトの配列です。 各オブジェクトには、次の属性が必要です。

- `displayName`はフィールドのUI表示名です。
- `name`はフィールドのAPI名です。
- `dataType`はフィールドタイプです。

オプションの属性は`description`、`isHidden`、`isHtmlEncodingInEmail`、および`isSensitive`です。

name属性は一意で、文字で始まり、文字、数字、アンダースコアのみを含める必要があります。 `displayName`は一意である必要があり、特殊文字を含めることはできません。

一般的な規則では、名前を生成するためにキャメルケースを`displayName`に適用します。 例えば、「My Custom Field」の`displayName`は「myCustomField」という名前を生成します。

### リクエスト

```http
POST /rest/v1/leads/schema/fields.json
```

### 本文

```json
{
  "input": [
      {
        "displayName": "Acme Access Code",
        "name": "acmeAccessCode",
        "description": "Acme Direct Mail Integration",
        "dataType": "string"
      },
      {
        "displayName": "Acme Mail Date",
        "name": "acmeMailDate",
        "description": "Acme Direct Mail Integration",
        "dataType": "string"
      }
  ]
}
```

### 応答

```json
{
    "requestId": "d9f1#17943666811",
    "result": [
        {
            "name": "acmeAccessCode",
            "status": "created"
        },
        {
            "name": "acmeMailDate",
            "status": "created"
        }
    ],
    "success": true
}
```

## フィールドの更新

リードフィールドを更新エンドポイントは、リードオブジェクトの1つのカスタムフィールドを更新します。 Marketo Engage UIで利用できるフィールドの更新のほとんどは、APIからも利用できます。 次の表に、その違いをまとめました。

<table>
<tbody>
<tr>
<td style="width: 26.5306%;" rowspan="2"><strong>属性</strong></td>
<td style="width: 35%;" colspan="2"><strong>標準フィールド</strong></td>
<td style="width: 38.2654%;" colspan="2"><strong>カスタムフィールド</strong></td>
</tr>
<tr>
<td style="width: 17.449%;"><strong>API で更新可能？</strong></td>
<td style="width: 17.551%;"><strong>UI で更新可能？</strong></td>
<td style="width: 19.3878%;"><strong>API で更新可能？</strong></td>
<td style="width: 18.8776%;"><strong>UI で更新可能？</strong></td>
</tr>
<tr>
<td style="width: 26.5306%;">dataType</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">いいえ</td>
<td style="width: 19.3878%;">いいえ</td>
<td style="width: 18.8776%;">はい</td>
</tr>
<tr>
<td style="width: 26.5306%;">description</td>
<td style="width: 17.449%;">はい</td>
<td style="width: 17.551%;">はい</td>
<td style="width: 19.3878%;">はい</td>
<td style="width: 18.8776%;">はい</td>
</tr>
<tr>
<td style="width: 26.5306%;">displayName</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">いいえ</td>
<td style="width: 19.3878%;">はい</td>
<td style="width: 18.8776%;">はい</td>
</tr>
<tr>
<td style="width: 26.5306%;">isCustom</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">いいえ</td>
<td style="width: 19.3878%;">いいえ</td>
<td style="width: 18.8776%;">いいえ</td>
</tr>
<tr>
<td style="width: 26.5306%;">isHidden</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">はい</td>
<td style="width: 19.3878%;">はい（API で作成されている場合）</td>
<td style="width: 18.8776%;">はい</td>
</tr>
<tr>
<td style="width: 26.5306%;">isHtmlEncodingInEmail</td>
<td style="width: 17.449%;">はい</td>
<td style="width: 17.551%;">はい</td>
<td style="width: 19.3878%;">はい</td>
<td style="width: 18.8776%;">はい</td>
</tr>
<tr>
<td style="width: 26.5306%;">isSensitive</td>
<td style="width: 17.449%;">はい</td>
<td style="width: 17.551%;">はい</td>
<td style="width: 19.3878%;">はい</td>
<td style="width: 18.8776%;">はい</td>
</tr>
<tr>
<td style="width: 26.5306%;">length</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">いいえ</td>
<td style="width: 19.3878%;">いいえ</td>
<td style="width: 18.8776%;">いいえ</td>
</tr>
<tr>
<td style="width: 26.5306%;">name</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">いいえ</td>
<td style="width: 19.3878%;">いいえ</td>
<td style="width: 18.8776%;">いいえ</td>
</tr>
</tbody>
</table>

必須の `fieldApiName` パスパラメーターは、更新するフィールドの API 名を指定します。 必須の入力パラメーターは、1つ以上の属性を持つ1つのリードフィールドオブジェクトを含む配列です。

### リクエスト

```http
POST /rest/v1/leads/schema/fields/{fieldApiName}.json
```

### 本文

```json
{
  "input": [
      {
        "displayName": "Acme Access Code",
        "description": "Acme Direct Mail Integration",
        "isHtmlEncodingInEmail": true
      }
  ]
}
```

### 応答

```json
{
    "requestId": "9f57#1794324f44c",
    "result": [
        {
            "name": "acmeAccessCode",
            "status": "updated"
        }
    ],
    "success": true
}
```

## Marketo にリードをプッシュ

プッシュリードは、リードを同期する代わりの手段であり、Marketo フォームと同様に、より多くのトリガーオプションを提供します。 エンドポイントは、リードフィールドを同期するだけでなく、Cookieの値に基づいてリードを関連付けることができます。 Marketoの電子メールからクリックして生成された`mkt_tok`値を渡すか、呼び出しにプログラム名を渡します。

また、エンドポイントは、Marketo プログラム、キャンペーン、またはその両方に関連付けられた1つのトリガー可能なアクティビティも作成します。 このアクティビティを使用して、特定のキャンペーンまたはプログラムに関連付けられたリードキャプチャイベントからワークフローを開始します。

プッシュリードは、同期リードと同じプライマリキーとフィールド API名を使用します。 常にアップサートを実行するため、アクションパラメーターはありません。

`programName`と入力パラメーターが必要です。 入力パラメーターはリードオブジェクトの配列であり、結果のアクティビティは名前付きプログラムに関連付けられます。 `lookupField`、`source`および`reason` パラメーターはオプションです。 `source`と`reason`に任意の文字列を追加して、これらの値を結果のアクティビティに含めます。 値は、対応するトリガー（リードはMarketoにプッシュ）とフィルター（リードはMarketoにプッシュ）の制約として使用できます。

以前の匿名アクティビティを新しく作成したリードに関連付けるには、リードオブジェクトからcookie属性を省略し、プッシュリードの後に関連付けリードを呼び出します。 アクティビティ履歴を含まないリードを作成するには、リードオブジェクトでcookie属性を指定します。

### リクエスト

```http
POST /rest/v1/leads/push.json
```

### 本文

```json
{
    "programName": "Big Blue Thing Product Launch",
    "source": "Cool Sales Site",
    "reason": "Downloaded pricing sheet",
    "lookupField": "email",
    "input": [
        {
             "email": "Theresa.May@westminister.gov.uk",
             "country": "united kingdom",
             "firstName": "Theresa",
             "website": "www.brexit.com",
             "leadScore": 45,
             "jobTitle": "Prime Minister"
         },
         {
             "email": "Justin.Trudeau@ottowa.gov.ca",
             "country": "canada",
             "firstName": "Justin",
             "website": "www.take-off-eh.com",
             "leadScore": 92,
             "jobTitle": "Sonny"
         }
     ]
}
```

### 応答

```json
{
    "requestId": "939079529805",
    "success": true,
    "warnings": [],
    "result": [
       {
           "id": 483894,
           "status": "created"
       },
       {
           "id": 1087425,
           "status": "updated"
       },
       {
           "id": 3525,
           "reasons": [
                    {
                        "code": "501",
                        "message": "Bad stuff happened"
                    }
           ]
       }
    ]
}
```

`mkt_tok` パラメーターを渡すには、入力パラメーター内のリードレコードのmktToken メンバーにその値を割り当てます。

### 本文

```json
{
  "programName": "Big Blue Thing Product Launch",
  "source": "Cool Sales Site",
  "reason": "Downloaded pricing sheet",
  "lookupField": "mktToken",
  "input" : [
     {
       "mktToken" : "<tokenValue>",
       "firstName" : "Thelma"
     },
     {
       "mktToken" : "<tokenValue>",
       "firstName" : "Louise"
     }
   ]
}
```

## フォームを送信

送信フォームは、リードを同期するための代替手段であり、Marketo フォーム送信と同等の機能を提供します。 特定のキャンペーンやプログラムに起因するリードキャプチャイベントからワークフローを開始するために使用します。

「フォームを送信」エンドポイントは、次の機能をサポートしています。

- 電子メールフィールドをプライマリキーとして使用して、リードレコードを更新します。
- プログラム、キャンペーン、またはその両方に関連付けられた「フォームに入力」アクティビティを作成します。
- Cookieの値に基づいてリードを関連付けます。
- フォームフィールドを検証します。

標準のリードデータベースパターンを使用してフォームを送信します。 POST リクエストのJSON本文の必須の入力メンバーに1つのオブジェクトレコードを渡します。 必須の `formId` メンバーには、ターゲットの Marketo フォーム ID が含まれます。

オプションの`programId`を使用して、リード、プログラムメンバーのカスタムフィールド、またはその両方を受け取るプログラムを特定します。 `programId`が存在する場合、フォーム内の任意のプログラムメンバーフィールドとともに、リードがプログラムに追加されます。 プログラムは、フォームと同じワークスペースにある必要があります。

フォームにプログラムメンバーのカスタムフィールドが含まれておらず、`programId`が省略された場合、リードはプログラムに追加されません。 フォームがプログラムに属し、1つ以上のプログラムメンバーのカスタムフィールドを含み、`programId`を省略する場合、エンドポイントはフォームのプログラムを使用します。

必須の`leadFormFields` オブジェクトには、入力するフィールドの1つ以上の名前と値のペアが含まれています。 すべてのフィールドは、指定したフォームで定義する必要があり、各名前はフィールドのREST API名である必要があります。 `email` フィールドは必須です。

オプションの`visitorData` オブジェクトには、`pageURL`、`queryString`、`leadClientIpAddress`、`userAgentString`などのページ訪問データが含まれています。 フィルターやトリガーに追加のアクティビティフィールドを入力するために使用します。

オプションのcookie メンバーは、Munchkin cookieをMarketo人物レコードに関連付けます。 エンドポイントがリードを作成すると、Cookieが以前に別の既知のレコードに関連付けられていない限り、以前の匿名アクティビティがそのリードに関連付けられます。

Cookieが以前に関連付けられていた場合、新しいアクティビティは新しいレコードに対して追跡されますが、古いアクティビティは既存の既知のレコードに残ります。 アクティビティ履歴を含まないリードを作成するには、Cookie メンバーを省略します。

新しいリードは、フォームが存在するワークスペースのプライマリパーティションに作成されます。

### リクエスト

```http
POST /rest/v1/leads/submitForm.json
```

### ヘッダー

```text
Content-Type: application/json
```

### 本文

```json
{
  "formId": 1029,
  "input": [
    {
      "leadFormFields": {
        "firstName": "Marge",
        "lastName": "Simpson",
        "email": "marge.simpson@fox.com",
        "pMCFField": "PMCF value"
      },
      "visitorData": {
        "pageURL": "https://na-sjst.marketo.com/lp/063-GJP-217/UnsubscribePage.html",
        "queryString": "Unsubscribed=yes",
        "leadClientIpAddress": "192.150.22.5",
        "userAgentString": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.89 Safari/537.36"
      },
      "cookie": "id:063-GJP-217&token:_mch-marketo.com-1594662481190-60776"
    }
  ]
}
```

### 応答

```json
{
  "requestId": "10667#173bc585ca5",
  "result": [
    {
      "id": 319174,
      "status": "updated"
    }
  ],
  "success": true
}
```

次の図は、Marketo Engage UIの対応する「フォームに入力」アクティビティの詳細を示しています。

![「フォームに入力」の UI](assets/fill_out_form_activity_details.png)

## 結合

>[!NOTE]
>
>2026年3月31日（PT）以降、Merge Leads API呼び出しの`leadIds` パラメーターに25を超えるIDを含む呼び出しは、1080 エラーコードになり、呼び出しはスキップされます。 25以上のレコードを1つに結合する必要があるジョブは、それらの呼び出しを成功させるために複数のジョブに分割する必要があります。
>

Merge Leads APIを使用して、重複するレコードを1つのレコードに結合します。 結合では、アクティビティログ、プログラム、キャンペーン、リストメンバーシップ、CRM情報、フィールド値が組み合わされます。

勝者リード IDをパスパラメーターとして渡します。 クエリパラメーターとして1つの`leadId`を渡すか、`leadIds` パラメーターにコンマ区切りのIDを25個まで渡します。


### リクエスト

```http
POST /rest/v1/leads/{id}/merge.json?leadId=1324
```

### 応答

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true
}
```

パスパラメーターのリードは、勝者リードです。 フィールド値が競合する場合、その値が空で、失われるレコードの値が無効でない限り、結合は勝者の値を使用します。 `leadId`または`leadIds` パラメーター内のリードは、失われたリードです。

SFDC-syncが有効なサブスクリプションの場合は、`mergeInCRM` パラメーターを使用して、CRMで結合も実行します。 両方のレコードがSFDCにあり、一方がCRM リードで、もう一方がCRM コンタクトである場合、指定された勝者に関係なく、CRM コンタクトが勝者になります。 1つのレコードがSFDCにあり、もう1つのレコードがMarketoにのみ存在する場合、指定された勝者に関係なくSFDC リードが勝者になります。

## Web アクティビティの関連付け

リードトラッキング（Munchkin）は、web サイトとMarketoランディングページへの訪問者の訪問数とクリック数を記録します。 これらのアクティビティでは、リードのブラウザーの「_mkto_trk」 Cookieに対応するキーを使用して、Marketoが同じユーザーのアクティビティをトラッキングできるようにします。

通常、リードとリードレコードとの関連付けは、リードがMarketoの電子メールからのリンクをフォローするか、Marketoフォームを送信したときに行われます。 リードを別のタイプのイベントの後に関連付けるには、リードの関連付けエンドポイントを使用します。 既知のリードレコード IDをパスパラメーターとして渡し、cookie クエリパラメーターに「_mkto_trk」 cookie値を渡します。

### リクエスト

```http
POST /rest/v1/leads/{id}/associate.json?cookie=id:287-GTJ-838%26token:_mch-marketo.com-1396310362214-46169
```

### 応答

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true
}
```

Cookieが既に既知のリードに関連付けられている場合、別のリードにこのAPIを使用すると、新しいレコードに対して新しいweb アクティビティが記録されます。既存のWeb アクティビティは、新しいレコードに移動しません。
メンバーシップ

静的リストまたはプログラムのメンバーシップに基づいてリードレコードを取得します。 特定のリードを含むあらゆる静的リスト、プログラム、スマートキャンペーンを取得することもできます。

応答構造とオプションのパラメーターは、フィルターの種類によるリードの取得と一致しますが、このAPIでは`filterType`または`filterValues`は受け付けられません。

Marketo UIでリスト IDを検索するには、リストに移動し、そのURLを調べます。 `https://app-****.marketo.com/#ST1001A1`では、1001がリスト `id`です。

## リード IDでプログラムを取得

### リクエスト

```http
GET /rest/v1/list/{listId}/leads.json?batchSize=3
```

### 応答

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "nextPageToken":
"PS5VL5WD4UOWGOUCJR6VY7JQO2KUXL7BGBYXL4XH4BYZVPYSFBAONP4V4KQKN4SSBS55U4LEMAKE6===",
    "result":[
       {
            "id":50,
            "email":"kjashaedd@klooblept.com",
            "firstName":"Kataldar",
             "postalCode":"04828"
       },
       {
           "id":2343,
           "email":"kjashaedd@klooblept.com",
           "firstName":"Kataldar",
           "postalCode":"04828"
       },
      {
           "id":88498,
           "email":"kjashaedd@klooblept.com",
           "firstName":"Kataldar",
         "postalCode":"04828"
         }
    ]
}
```

## リード IDでリストを取得

リード ID別リスト取得エンドポイントは、リードレコード `id` パスパラメーターを取得し、リードを含むすべての静的リストを返します。

### リクエスト

```http
GET /rest/v1/leads/{id}/listMembership.json?batchSize=3
```

### 応答

```json
{
    "requestId": "1184b#1706f0ec23f",
    "result": [
        {
            "listId": 3379,
            "createdAt": "2016-05-17T19:32:44Z",
            "updatedAt": "2016-05-17T19:32:44Z"
        },
        {
            "listId": 2792,
            "createdAt": "2009-05-19T18:29:15Z",
            "updatedAt": "2009-05-19T18:29:15Z"
        },
        {
            "listId": 42,
            "createdAt": "2009-04-22T19:24:22Z",
            "updatedAt": "2009-04-22T19:24:22Z"
        }
    ],
    "success": true,
    "nextPageToken": "BFRV7OMVSNJWDVKVTUFS3XHT4E======",
    "moreResult": true
}
```

## プログラム

リスト メンバーシップと同じ方法でプログラム メンバーシップを取得します。 プログラム IDでリードを取得は、同じオプションのリクエストパラメーターを受け入れ、`programId` パスパラメーターを必要とします。

必要に応じて、フィールド名のコンマ区切りリストを含むfields パラメーターを渡します。 フィールドが省略された場合、応答には`email`、`updatedAt`、`createdAt`、`lastName`、`firstName`、`membership`および`id`が含まれます。 要求されたフィールドが返されない場合、その値はnullであることが暗黙的に示されます。

結果配列内の各項目は、「membership」という子オブジェクトを持つリードです。 このオブジェクトは、リクエストされたプログラムに対するリードの関係を説明し、常に`progressionStatus`、`acquiredBy`、`reachedSuccess`、および`membershipDate`を含みます。

親プログラムがエンゲージメントプログラムである場合、メンバーシップには、そのプログラムにおけるリードの位置とアクティビティを説明する`stream`、`nurtureCadence`および`isExhausted`も含まれます。

### リクエスト

```http
GET /rest/v1/leads/programs/{programId}.json?batchSize=3
```

### 応答

```json
{
    "requestId": "13ad4#1727b748a17",
    "result": [
        {
            "id": 319141,
            "firstName": "Meera",
            "lastName": "Reed",
            "email": "mree@housestark.com",
            "updatedAt": "2020-04-21T16:27:14Z",
            "createdAt": "2020-04-21T16:27:14Z",
            "membership": {
                "id": 1127,
                "progressionStatus": "Visited",
                "progressionStatusType": "Visited",
                "isExhausted": false,
                "acquiredBy": true,
                "reachedSuccess": false,
                "membershipDate": "2020-04-21T16:27:16Z",
                "updatedAt": "2020-04-21T16:27:16Z"
            }
        },
        {
            "id": 319142,
            "firstName": "Jon",
            "lastName": "Umber",
            "email": "jumb@housestark.com",
            "updatedAt": "2020-04-21T16:27:14Z",
            "createdAt": "2020-04-21T16:27:14Z",
            "membership": {
                "id": 1127,
                "progressionStatus": "Visited",
                "progressionStatusType": "Visited",
                "isExhausted": false,
                "acquiredBy": true,
                "reachedSuccess": false,
                "membershipDate": "2020-04-21T16:27:16Z",
                "updatedAt": "2020-04-21T16:27:16Z"
            }
        },
        {
            "id": 319143,
            "firstName": "Lyanna",
            "lastName": "Mormont",
            "email": "lmor@housestark.com",
            "updatedAt": "2020-04-21T16:27:14Z",
            "createdAt": "2020-04-21T16:27:14Z",
            "membership": {
                "id": 1127,
                "progressionStatus": "Visited",
                "progressionStatusType": "Visited",
                "isExhausted": false,
                "acquiredBy": true,
                "reachedSuccess": false,
                "membershipDate": "2020-04-21T16:27:16Z",
                "updatedAt": "2020-04-21T16:27:16Z"
            }
        }
    ],
    "success": true,
    "nextPageToken": "SW3PTMBVFCNHSHJGZ7LQH3ZWNUOHKADJZ3MOQ2LOZZVNO3WEIUPDKPRTTHBSMW756KOCWURTOF2XS==="
}
```

リード ID別プログラムを取得エンドポイントは、リードレコード ID パスパラメーターを取得し、リードを含むすべてのプログラムを返します。 オプションの`filterType`および`filterValues` パラメーターを使用して、プログラム IDでフィルタリングします。

### リクエスト

```http
GET /rest/v1/leads/{id}/programMembership.json
```

### 応答

```json
{
    "requestId": "12e84#1706f13a379",
    "result": [
        {
            "id": 1044,
            "progressionStatus": "Sent",
            "isExhausted": false,
            "acquiredBy": false,
            "reachedSuccess": false,
            "membershipDate": "2016-05-27T19:50:29Z",
            "updatedAt": "2016-05-27T19:50:29Z"
        }
    ],
    "success": true,
    "moreResult": false
}
```

## スマートキャンペーン

リード ID別スマートキャンペーンを取得エンドポイントは、リードレコード ID パスパラメーターを取り、リードを含むすべてのスマートキャンペーンを返します。

### リクエスト

```http
GET /rest/v1/leads/{id}/smartCampaignMembership.json?batchSize=3
```

### 応答

```json
{
    "requestId": "e7b0#1706f163632",
    "result": [
        {
            "smartCampaignId": 3746,
            "createdAt": "2018-06-01T18:00:04Z",
            "updatedAt": "2018-06-01T18:00:06Z"
        },
        {
            "smartCampaignId": 3678,
            "createdAt": "2015-04-06T18:37:30Z",
            "updatedAt": "2015-04-06T18:37:41Z"
        },
        {
            "smartCampaignId": 3680,
            "createdAt": "2015-04-06T18:37:30Z",
            "updatedAt": "2015-04-06T18:37:40Z"
        }
    ],
    "success": true,
    "nextPageToken": "TNGAH3NKDUFDHNXUVGTNBXJCQM======",
    "moreResult": true
}
```

## 削除

リードの削除エンドポイントを使用して、リードレコードを削除します。 ID属性を使用して、ボディ内のリード IDを指定します。 リクエストは最大300件のリードを削除できます。 Content-Type: application/json ヘッダーを送信します。

### リクエスト

```http
POST /rest/v1/leads/delete.json
```

### 本文

```json
{
   "input":[
      {
         "id": 235
      },
      {
         "id":766
      }
   ]
}
```

### 応答

```json
{
  "requestId":"3608#16664333670",
  "result":[
    {
      "id":235,
      "status":"deleted"
    },
    {
      "id":766,
      "status":"deleted"
    }
  ],
  "success":true
}
```

## 関係

- リード レコードのexternalCompanyId フィールドを使用して会社を作成します
- リードレコードのexternalSalesPersonId フィールドを使用したセールス担当者
- プログラムメンバーシップを通じたプログラム
- リストメンバーシップを通じたリスト
- アクティビティのleadId フィールドを介したアクティビティ
- リードレコードの個々のセグメントフィールドを使用したセグメント化
- リード レコードのleadPartitionId フィールドを介したパーティション

## タイムアウト

リードエンドポイントには、次のエンドポイントを除き、30秒のタイムアウトがあります。

- リードを同期：90 秒
- リードを関連付け：60 秒
- リードを結合：180 秒
- リードパーティションを更新：60 秒
- Marketo にリードをプッシュ：90 秒
- フィルタータイプでリードを取得：60 秒
- リスト ID でリードを取得：60 秒
