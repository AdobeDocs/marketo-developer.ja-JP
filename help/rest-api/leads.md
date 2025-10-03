---
title: リード
feature: REST API
description: 説明、ID またはフィルターによるクエリ、デフォルトフィールド、制限、ECID の取得など、Marketo Leads REST API の機能について説明します。
exl-id: 0a2f7c38-02ae-4d97-acfe-9dd108a1f733
source-git-commit: cc4bd7c18124bb039386a1cec06b9f1da0d047cb
workflow-type: tm+mt
source-wordcount: '3411'
ht-degree: 96%

---

# リード

[リードエンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads)

Marketo リードの API には、リードレコードに対するシンプルな CRUD アプリケーション用の大規模な機能セットと、静的リストやプログラムでのリードのメンバーシップを変更したり、リードに対するスマートキャンペーン処理を開始したりする機能が用意されています。

## 説明

Leads API の主な機能の 1 つに Describe メソッドがあります。「リードを説明」を使用し、REST API 経由でインタラクションに使用できるフィールドの完全なリストと、それぞれの次のメタデータを取得します。

* データタイプ
* REST API 名
* 長さ（該当する場合）
* 読み取り専用
* わかりやすいラベル

説明は、フィールドが使用可能かどうか、およびこれらのフィールドに関するメタデータに対する信頼できるプライマリソースです。

### リクエスト

```
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

通常、応答の結果配列には非常に大きなフィールドセットが含まれますが、デモ目的で省略しています。結果配列内の各項目は、リードレコードで使用可能なフィールドに対応し、少なくとも id、displayName、datatype が含まれます。特定のフィールドには、rest および soap 子オブジェクトが存在する場合と存在しない場合があります。これらは、フィールドが REST API または SOAP API のいずれかでの使用に有効かどうかを示します。`readOnly` プロパティは、対応する API（REST または SOAP）経由でフィールドが読み取り専用であるかどうかを示します。length プロパティは、フィールドが存在する場合、その最大長を示します。dataType プロパティは、フィールドのデータタイプを示します。

## クエリ

リードの取得には、「ID でリードを取得」と「フィルタータイプでリードを取得」という 2 つの主なメソッドがあります。「ID によるリードの取得」では、単一のリード ID をパスパラメーターとして受け取り、単一のリードレコードを返します。

オプションで、返されるフィールド名のコンマ区切りリストを含む fields パラメーターを渡すこともできます。このリクエストに fields パラメーターが含まれていない場合、`email`、`updatedAt`、`createdAt`、`lastName`、`firstName`、`id` のデフォルトフィールドが返されます。フィールドのリストをリクエストする際に、特定のフィールドがリクエストされたが返されない場合、その値は null であると見なされます。

### リクエスト

```
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

このメソッドの場合、結果配列の先頭には常に 1 つのレコードがあります。

「フィルタータイプでリードを取得」では、同じタイプのレコードが返されますが、1 ページあたり最大 300 個が返される場合があります。`filterType` と `filterValues` のクエリパラメーターが必要です。

`filterType` では、任意のカスタムフィールドや、一般的に使用されるほとんどのフィールドを受け入れます。`Describe2` エンドポイントを呼び出して、`filterType` で使用できる検索可能なフィールドの包括的なリストを取得します。カスタムフィールドで検索する場合、`string`、`email`、`integer` のデータタイプのみがサポートされます。前述の Describe メソッドを使用して、フィールドの詳細（説明、タイプなど）を取得できます。

`filterValues` は、コンマ区切り形式で最大 300 個の値を受け入れます。この呼び出しでは、リードのフィールドが含まれる `filterValues` のいずれかと一致するレコードを検索します。リードフィルターに一致するリードの数が 1,000 を超える場合、「1003、フィルターに一致する結果が多すぎます」というエラーが返されます。

GET リクエストの合計長が 8 KB を超えると、HTTP エラー「414、URI が長すぎます」（RFC 7231 に準拠）という HTTP エラーが返されます。回避策として、GET を POST に変更し、_method=GET パラメーターを追加して、リクエスト本文にクエリ文字列を配置できます。

### リクエスト

```
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

この呼び出しでは、`filterValues` に含まれる ID に一致するレコードを検索し、一致するレコードを返します。

レコードが見つからない場合、応答は成功を示しますが、結果配列は空になります。

### 応答

```json
{
"requestId": "177a1#1578b643357",
"result": [],
"success": true
}
```

「ID でリードを取得」と「フィルタータイプでリードを取得」はどちらも、API フィールドのコンマ区切りリストを受け入れる fields クエリパラメーターも受け入れます。これが含まれている場合、応答内の各レコードにはリストされているフィールドが含まれます。省略した場合は、`id`、`email`、`updatedAt`、`createdAt`、`firstName`、`lastName` のデフォルトのフィールドセットが返されます。

## Adobe ECID

Adobe Experience Cloud オーディエンス共有機能を有効にすると、Adobe Experience Cloud ID（ECID）を Marketo リードに関連付ける cookie 同期プロセスが発生します。上記のリード取得方法を使用して、関連する ECID 値を取得できます。これを行うには、fields パラメーターで `ecids` を指定します。例：`&fields=email,firstName,lastName,ecids`。

## 作成と更新

リードデータの取得に加えて、API 経由でリードレコードを作成、更新、削除することもできます。リードの作成と更新は、リクエストで定義されている操作タイプと同じエンドポイントを共有し、最大 300 個のレコードを同時に作成または更新できます。

>[!NOTE]
>
> [リードの同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST)エンドポイントを使用した会社フィールドの更新はサポートされていません。代わりに、[会社の同期](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST)エンドポイントを使用します。

>[!NOTE]
>
> ユーザレコードのメール値を作成または更新する際、メールアドレスフィールドでは ASCII 文字のみがサポートされます。

### リクエスト

```
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

このリクエストには、`action` と `lookupField` という 2 つの重要なフィールドが表示されます。`action` は、リクエストの操作タイプを指定し、`createOrUpdate`、`createOnly`、`updateOnly`、または `createDuplicate` を指定できます。省略した場合、アクションはデフォルトで `createOrUpdate` になります。`lookupField` パラメーターは、アクションが `createOrUpdate` または `updateOnly` の場合に使用するキーを指定します。`lookupField` を省略した場合、デフォルトのキーは `email` になります。

デフォルトでは、デフォルトのパーティションが使用されます。オプションで、`partitionName` パラメーターを指定できます。これは、アクションが `createOnly` または `createOrUpdate` の場合にのみ機能します。`partitionName` が追加の重複排除条件として機能するには、カスタム重複排除ルールのソースタイプの一部である必要があります。更新操作中に、指定したパーティションにリードが存在しない場合は、エラーが返されます。API のみのユーザが、指定されたパーティションにアクセスする権限を持たない場合は、エラーが返されます。

`id` はシステムによって管理される一意のキーなので、`updateOnly` アクションを使用する場合にのみ、`id` フィールドをパラメーターとして含めることができます。

リクエストには、リードレコードの配列である `input` パラメーターも必要です。各リードレコードは、任意の数のリードフィールドを持つ JSON オブジェクトです。レコードに含まれるキーは、そのレコードに対して一意である必要があり、すべての JSON 文字列は UTF-8 でエンコードされている必要があります。`externalCompanyId` フィールドを使用すると、リードレコードを会社レコードにリンクできます。`externalSalesPersonId` フィールドを使用すると、リードレコードをセールス担当者レコードにリンクできます。

メモ：リードのアップサートリクエストを同時にまたは連続して実行する際、最初のリクエストが返される前に同じ値で後続の呼び出しが行われた場合、同じキー値で複数のリクエストを行うと、重複レコードが発生する場合があります。これを回避するには、`createOnly` または `updateOnly` を適切に使用するか、呼び出しをキューに入れて、呼び出しが返されるのを待ってから、同じキーで後続のアップサート呼び出しを実行します。

## フィールド

リードオブジェクトには、標準フィールドとオプションのカスタムフィールドが含まれます。標準フィールドは、すべての Marketo Engage サブスクリプションに存在します。カスタムフィールドは、必要に応じてユーザが作成します。各フィールド定義は、フィールドを説明する属性のセットで構成されます。属性の例としては、表示名、API 名、dataType があります。これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、リードオブジェクトのフィールドに対してクエリ、作成、更新を行うことができます。これらの API では、所有する API ユーザに、「読み取り／書き込みスキーマ標準フィールド」権限または「読み取り／書き込みスキーマカスタムフィールド」権限のいずれかまたは両方を含むロールを用意する必要があります。

## クエリフィールド

リードフィールドのクエリの実行は簡単です。API 名で単一のリードフィールドに対してクエリを実行することも、すべてのリードフィールドのセットに対してクエリを実行することもできます。使用するロール権限に応じて、標準フィールドとカスタムフィールドの両方を取得できます。また、非表示のフィールドも取得されます。

## 名前別

「名前によるリードフィールドを取得」エンドポイントでは、リードオブジェクトの単一フィールドのメタデータを取得します。必須の fieldApiName パスパラメーターは、フィールドの API 名を指定します。応答は「リードの説明」エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す isCustom 属性などの追加のメタデータが含まれます。

### リクエスト

```
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

「リードフィールドの取得」エンドポイントでは、以下を含むリードオブジェクトから、すべてのフィールドのメタデータを取得します。デフォルトでは、最大 300 個のレコードが返されます。`batchSize` クエリパラメーターを使用して、この数を減らすことができます。`moreResult` 属性が true の場合、さらに多くの結果が使用可能です。`moreResult` 属性が false を返すまで、つまり使用可能な結果が存在しなくなるまで、このエンドポイントを引き続き呼び出します。この API から返される `nextPageToken` は、この呼び出しの次の反復で常に再利用する必要があります。

### リクエスト

```
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

「リードフィールドの作成」エンドポイントでは、リードオブジェクトに 1 つ以上のカスタムフィールドを作成します。このエンドポイントには、Marketo Engage UI で使用できる機能と同等の機能が用意されています。このエンドポイントを使用して、最大 100 個のカスタムフィールドを作成できます。
API を使用して Marketo Engage の実稼動インスタンスで作成する各フィールドを慎重に検討してください。フィールドは一度作成すると削除できません（非表示にすることしかできません）。未使用のフィールドが急増すると、インスタンスが乱雑になります。

必須の入力パラメーターは、リードフィールドオブジェクトの配列です。各オブジェクトには、1 つ以上の属性が含まれます。必須の属性はそれぞれ、フィールドの UI 表示名、フィールドの API 名、フィールドタイプに対応する `displayName`、`name`、`dataType` です。オプションで、`description`、`isHidden`、`isHtmlEncodingInEmail`、`isSensitive` を指定できます。

name と `displayName` の命名にはいくつかのルールが関連付けられています。name 属性は一意にして、文字で始まり、文字、数字、またはアンダースコアのみを含める必要があります。`displayName` は一意にする必要があり、特殊文字を含めることはできません。一般的な命名規則では、`displayName` にキャメルケースを適用して名前を生成します。例えば、`displayName` が &quot;My Custom Field&quot; の場合、myCustomField&quot; という名前を生成します。

### リクエスト

```
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

「リードフィールドの更新」エンドポイントでは、リードオブジェクトの単一のカスタムフィールドを更新します。ほとんどの場合、Marketo Engage UI を使用して実行されるフィールド更新操作は、API を使用して実行できます。次の表に、いくつかの違いをまとめて示します。

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

必須の `fieldApiName` パスパラメーターは、更新するフィールドの API 名を指定します。必須の入力パラメーターは、単一のリードフィールドオブジェクトを含む配列です。フィールドオブジェクトには、1 つ以上の属性が含まれています。

### リクエスト

```
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

「リードをプッシュ」は、リードを Marketo に同期するための代替手段で、主に標準の「リードを同期」（Marketo フォームと同様の使用方法）よりも高度なトリガー機能を可能にするように設計されています。このエンドポイントでは、リードフィールドの同期に加えて、エンドポイントに渡される cookie 値に基づいてリードの関連付けが可能になります。これを行うには、Marketo のメールをクリックして生成された `mkt_tok` 値を渡すか、呼び出しでプログラム名を渡します。また、このエンドポイントでは、Marketo のプログラムやキャンペーンに関連付けられた単一のトリガー可能なアクティビティも作成します。これにより、特定のキャンペーンまたはプログラムに関連付けられたリードキャプチャイベントをトリガーして、Marketo 内から関連するワークフローを開始できます。

「リードをプッシュ」インターフェイスは「リードを同期」と非常によく似ています。同じプライマリキーはすべて有効で、フィールドには同じ API 名が使用されます（これは常にアップサート操作なので、アクションパラメーターはありません）。`programName` および input パラメーターは必須で、`lookupField`、`source`、`reason` パラメーターはオプションです。この入力パラメーターは、リードオブジェクトの配列です。結果として得られるアクティビティは、対応する名前付きプログラムに起因します。`source` と `reason` パラメーターは、結果として得られるアクティビティにこれらの値を埋め込むためにリクエストに追加できる任意の文字列フィールドです。これらは、対応するトリガー（リードが Marketo にプッシュされる）とフィルター（リードが Marketo にプッシュされる）の制約として使用できます。

匿名アクティビティに関するメモ。以前の匿名アクティビティを新しく作成したリードに関連付ける場合は、リードオブジェクトで cookies 属性を指定せず、「リードをプッシュ」に続いて「リードを関連付け」を呼び出します。アクティビティ履歴のない新しいリードを作成する場合は、リードオブジェクトで cookies 属性を指定するだけです。

### リクエスト

```
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
             "marketoSocialFacebookProfileURL": "http://www.facebook.com/id/23434456",
             "jobTitle": "Prime Minister"
         },
         {
             "email": "Justin.Trudeau@ottowa.gov.ca",
             "country": "canada",
             "firstName": "Justin",
             "website": "www.take-off-eh.com",
             "leadScore": 92,
             "marketoSocialFacebookProfileURL": "http://www.facebook.com/id/42434",
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

`mkt_tok` パラメーターを渡すには、次のように入力パラメーターのリードレコード内で、mktToken メンバーに値を割り当てます。

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

「フォームを送信」は、リードを Marketo に同期するための代替手段で、Marketo フォームの送信と同等の機能を提供するように設計されています。これにより、特定のキャンペーンまたはプログラムに関連付けられたリードキャプチャイベントをトリガーして、Marketo 内から関連するワークフローを開始できます。

「フォームを送信」エンドポイントは、次の機能をサポートしています。

* メールフィールドをプライマリキーとして使用してリードレコードをアップサート
* プログラムやキャンペーンに関連付けられた「フォームに入力」アクティビティを作成
* cookie 値に基づいてリードの関連付けを許可
* フォームフィールドの検証を実行

フォームの送信は、標準のリードデータベースパターンに従います。単一のオブジェクトレコードが、POST リクエストの JSON 本文の必須入力メンバーに渡されます。必須の `formId` メンバーには、ターゲットの Marketo フォーム ID が含まれます。

オプションの `programId` を使用すると、リードを追加するプログラムを指定したり、プログラムメンバーのカスタムフィールドを追加するプログラムを指定したりできます。`programId` を指定した場合は、リードがプログラムに追加され、フォーム内に存在するプログラムメンバーフィールドも追加されます。指定したプログラムは、フォームと同じワークスペースにある必要があります。フォームにプログラムメンバーのカスタムフィールドが含まれず、`programId` を指定していない場合、リードはプログラムに追加されません。フォームがプログラム内に存在し、`programId` を指定していない場合、フォーム内に 1 つ以上のプログラムメンバーカスタム フィールドが存在する場合にこのプログラムが使用されます。

入力レコード内には、`leadFormFields` オブジェクトが必要です。このオブジェクトには、入力するフォームフィールドに対応する 1 つ以上の名前と値のペアが含まれます。指定したすべてのフィールドは、指定したフォーム内で定義する必要があります。名前は、フィールドの REST API 名です。`email` フィールドは必須です。

`visitorData` メンバーオブジェクトはオプションで、`pageURL`、`queryString`、`leadClientIpAddress`、`userAgentString` などのページ訪問データに対応する名前と値のペアが含まれます。フィルタリングやトリガーの目的で追加のアクティビティフィールドに入力するために使用できます。

ccookie メンバー文字列はオプションで、これを使用すると、Munchkin cookie を Marketo のユーザレコードに関連付けることができます。新しいリードを作成すると、cookie 値が以前に別の既知のレコードに関連付けられていない限り、以前の匿名アクティビティはこのリードに関連付けられます。cookie 値を以前に関連付けていた場合、新しいアクティビティはレコードに対して追跡されますが、古いアクティビティは既存の既知のレコードから移行されません。アクティビティ履歴のない新しいリードを作成するには、cookie メンバーを省略するだけです。

新しいリードは、フォームが存在するワークスペースのプライマリパーティションに作成されます。

### リクエスト

```
POST /rest/v1/leads/submitForm.json
```

### ヘッダー

```
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

ここでは、Marketo Engage UI 内から対応する「フォームに入力」アクティビティの詳細を確認できます。

![「フォームに入力」の UI](assets/fill_out_form_activity_details.png)

## マージ

>[!NOTE]
>2026 年 3 月 31 日（PT）以降、結合リード API 呼び出しの `leadIds` パラメーターに 25 個を超える ID を含む呼び出しは、エラーコード 1080 が発生し、呼び出しはスキップされます。 25 を超えるレコードを 1 つに統合する必要があるジョブは、これらの呼び出しを確実に成功させるために複数のジョブに分割する必要があります。
>

時には、重複したレコードを結合する必要が出ることがあります。Marketo では Merge Leads API を通じてこれを容易にします。リードを結合すると、アクティビティログ、プログラム、キャンペーン、リストメンバーシップ、CRM 情報が組み合わされ、すべてのフィールド値が 1 つのレコードに結合されます。リードを結合では、リード ID をパスパラメーターとして使用し、単一の `leadId` をクエリパラメーターとして使用するか、`leadIds` パラメーターにコンマ区切りの ID を 25 個以下で指定します


### リクエスト

```
POST /rest/v1/leads/{id}/merge.json?leadId=1324
```

### 応答

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true
}
```

パスパラメーターで指定されたリードは、獲得リードです。したがって、結合されるレコード間に競合するフィールドがある場合は、獲得レコードのフィールドが空で、対応するフィールドが失注レコードでない限り、獲得レコードの値が取得されます。`leadId` または `leadIds` パラメーターのいずれかで指定されたリードは、失注リードです。

SFDC 同期が有効なサブスクリプションがある場合は、リクエストで `mergeInCRM` パラメーターを使用することもできます。true に設定すると、CRM 内の対応する結合も実行されます。両方のリードが SFDC にあり、一方が CRM リードでもう一方が CRM 取引先責任者である場合、（どちらのリードが獲得として指定されているかに関係なく）CRM 取引先責任者が獲得したことになります。リードの 1 つが SFDC にあり、もう 1 つが Marketo のみにある場合、（どちらのリードが獲得として指定されているかに関係なく）SFDC リードが獲得したことになります。

## Web アクティビティの関連付け

Marketo は、リードトラッキング（Munchkin）を通じて、web サイトおよび Marketo ランディングページへの訪問者の web アクティビティを記録します。これらのアクティビティ（訪問回数およびクリック数）は、リードのブラウザーに設定された「_mkto_trk」cookie に対応するキーを使用して記録され、Marketo はこれを使用して同じユーザのアクティビティを追跡します。通常、リードレコードへの関連付けは、リードが Marketo のメールをクリックするか、Marketo フォームに入力した際に発生しますが、関連付けは別のタイプのイベントによってトリガーされることもあり、そのためには「リードを関連付け」エンドポイントを使用できます。エンドポイントでは、既知のリードレコードの ID をパスパラメーターとして受け取り、cookie クエリパラメーターで「_mkto_trk」Cookie 値を受け取ります。

### リクエスト

```
POST /rest/v1/leads/{id}/associate.json?cookie=id:287-GTJ-838%26token:_mch-marketo.com-1396310362214-46169
```

### 応答

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true
}
```

cookie が既知のリードレコードに既に関連付けられている場合、別のリードレコードでこの API を使用すると、このレコードに対して新しい web アクティビティが記録されますが、既存の web アクティビティは新しいレコードに移動されません。
メンバーシップ

リードレコードは、静的リストまたはプログラムのメンバーシップに基づいて取得することもできます。さらに、リードがメンバーになっているすべての静的リスト、プログラム、またはスマートキャンペーンを取得することもできます。

応答構造とオプションのパラメーターは、「フィルタータイプでリードを取得」のものと同じですが、filterType と filterValues はこの API では使用できません。
Marketo UI を通じてリスト ID にアクセスするには、リストに移動します。リスト `id` は、静的リストの URL（`https://app-**&#x200B;**.marketo.com/#ST1001A1`）にあります。この例では、1001 がリストの `id` です。

### リクエスト

```
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

「リード ID でリストを取得」エンドポイントでは、リードレコード `id` パスパラメーターを受け取り、リードがメンバーであるすべての静的リストレコードを返します。

### リクエスト

```
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

プログラムメンバーシップは、リストと同様の方法で取得できます。「プログラム ID でリードを取得」エンドポイントを呼び出して `programId` パスパラメーターを渡す際にも、同じオプションのリクエストパラメーターを使用できます。

オプションで、返されるフィールド名のコンマ区切りリストを含む fields パラメーターを渡すこともできます。このリクエストに fields パラメーターが含まれていない場合、`email`、`updatedAt`、`createdAt`、`lastName`、`firstName`、`membership`、`id` のデフォルトフィールドが返されます。 フィールドのリストをリクエストする際に、特定のフィールドがリクエストされたが返されない場合、その値は null であると見なされます。

応答構造は非常に似ており、結果配列の各項目はリードですが、各レコードには「メンバーシップ」と呼ばれる子オブジェクトもあります。このメンバーシップ オブジェクトには、呼び出しで示されたプログラムとリードの関係に関するデータが含まれ、`progressionStatus`、`acquiredBy`、`reachedSuccess`、`membershipDate` が常に表示されます。親プログラムもエンゲージメントプログラムである場合、メンバーシップには、エンゲージメントプログラムでの位置とアクティビティを示すために、`stream`、`nurtureCadence`、`isExhausted` のメンバーが含まれます。

### リクエスト

```
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

「リード ID でプログラムを取得」エンドポイントでは、リードレコード id パスパラメーターを受け取り、リードがメンバーであるすべてのプログラムレコードを返します。オプションの `filterType` および `filterValues` パラメーターを使用すると、プログラム ID でフィルタリングできます。

### リクエスト

```
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

「リード ID でスマートキャンペーンを取得」エンドポイントでは、リードレコード id パスパラメーターを受け取り、リードがメンバーであるすべてのスマートキャンペーンレコードを返します。

### リクエスト

```
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

「リードを削除」エンドポイントを使用すると、リードの削除は簡単です。本文の id 属性を使用して、削除するリード ID を指定します。リクエストあたりの最大リード数は 300 です。Content-Type: application/json ヘッダーを使用します。

### リクエスト

```
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

* リードレコードの externalCompanyId フィールドを通じた会社
* リードレコードの externalSalesPersonId フィールドを通じた SalesPerson
* プログラムメンバーシップを通じたプログラム
* リストメンバーシップを通じたリスト
* アクティビティの leadId フィールドを通じたアクティビティ
* リードレコードの個々のセグメントフィールドを通じたセグメント化
* リードレコードの leadPartitionId を通じたパーティション

## タイムアウト

「リード」エンドポイントは、以下に記載されていない限り、タイムアウトが 30 秒になります。

* リードを同期：90 秒
* リードを関連付け：60 秒
* リードを結合：180 秒
* リードパーティションを更新：60 秒
* Marketo にリードをプッシュ：90 秒
* フィルタータイプでリードを取得：60 秒
* リスト ID でリードを取得：60 秒
