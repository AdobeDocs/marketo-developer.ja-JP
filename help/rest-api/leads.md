---
title: リード
feature: REST API
description: リード API 呼び出しの詳細
exl-id: 0a2f7c38-02ae-4d97-acfe-9dd108a1f733
source-git-commit: 7a3df193e47e7ee363c156bf24f0941879c6bd13
workflow-type: tm+mt
source-wordcount: '3338'
ht-degree: 3%

---

# リード

[ リードエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads)

Marketo Lead の API は、リードレコードに対するシンプルな CRUD アプリケーションに対応する大規模な機能セットと、静的リストおよびプログラムにおけるリードのメンバーシップを変更する機能、リードに対する Smart Campaign 処理を開始する機能を提供します。

## 説明

Leads API の主な機能の 1 つに Describe メソッドがあります。 「リードを記述」を使用して、REST API 経由でのインタラクションに使用できるフィールドの完全なリストと、それぞれのメタデータを取得します。

* データタイプ
* REST API 名
* 長さ（該当する場合）
* Read-Only
* わかりやすいラベル

説明は、フィールドを使用できるかどうか、およびそれらのフィールドに関するメタデータの主要な情報源です。

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

通常、応答には結果の配列にはるかに大きなフィールドのセットが含まれていますが、デモ目的では省略しています。 結果の配列内の各項目は、リードレコードで使用可能なフィールドに対応し、少なくとも id、displayName、およびデータタイプが含まれます。 rest および soap 子オブジェクトは、特定のフィールドに存在する場合としない場合があり、その存在は、フィールドが REST またはSOAP API のいずれかで使用するのに有効かどうかを示します。 `readOnly` プロパティは、フィールドが対応する API （REST またはSOAP）経由で読み取り専用であるかどうかを示します。 length プロパティは、フィールドの最大長を示します（存在する場合）。 dataType プロパティは、フィールドのデータ型を示します。

## クエリ

リードを取得するには、主に 2 つの方法があります。Id でリードを取得する方法と、フィルタータイプでリードを取得する方法です。 リード ID でリードを取得は、単一のリード ID をパスパラメーターとして受け取り、単一のリードレコードを返します。

オプションで、返すフィールド名のコンマ区切りリストを含むフィールドパラメーターを渡すことができます。 fields パラメーターがこのリクエストに含まれていない場合は、デフォルトのフィールド `email`、`updatedAt`、`createdAt`、`lastName`、`firstName`、`id` が返されます。 フィールドのリストをリクエストするときに、特定のフィールドがリクエストされても返されなかった場合、値は null であることが暗示されます。

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

このメソッドの場合、結果の配列の最初の位置には常に 1 つのレコードがあります。

フィルタータイプ別のリードの取得では、同じタイプのレコードが返されますが、1 ページにつき最大 300 が返される場合があります。 `filterType` と `filterValues` のクエリパラメーターが必要です。

`filterType` では、任意のカスタムフィールドまたは一般的に使用されるフィールドのほとんどを使用できます。 `Describe2` エンドポイントを呼び出して、`filterType` での使用が許可されている検索可能なフィールドの包括的なリストを取得します。 カスタムフィールドで検索する場合、サポートされているデータタイプは `string`、`email`、`integer` のみです。 前述の説明メソッドを使用して、フィールドの詳細（説明、タイプなど）を取得できます。

`filterValues` には、最大 300 個の値をコンマ区切り形式で指定できます。 この呼び出しでは、リードのフィールドが含まれる `filterValues` のいずれかと一致するレコードが検索されます。 リードフィルターに一致するリードの数が 1,000 を超える場合は、「1003, フィルターに一致する結果が多すぎます」というエラーが返されます。

GETリクエストの全長が 8KB を超える場合は、「414, URI too long」（RFC 7231 準拠）という HTTP エラーが返されます。 対応策として、GETをPOSTに変更し、_method=GETパラメーターを付加して、リクエスト本文にクエリ文字列を配置できます。

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

この呼び出しでは、`filterValues` に含まれている ID に一致するレコードが検索され、一致するレコードが返されます。

レコードが見つからない場合、応答は成功を示しますが、結果の配列は空になります。

### 応答

```json
{
"requestId": "177a1#1578b643357",
"result": [],
"success": true
}
```

ID でリードを取得およびフィルタータイプでリードを取得の両方とも、API フィールドのコンマ区切りリストを受け入れるフィールドクエリパラメーターを受け入れます。 これが含まれる場合、応答内の各レコードには、これらのリストされたフィールドが含まれます。  この引数を省略すると、デフォルトのフィールドセット `id`、`email`、`updatedAt`、`createdAt`、`firstName`、`lastName` が返されます。

## ADOBEECID

Adobe Experience Cloudのオーディエンス共有機能が有効な場合、Adobe Experience Cloud ID （ECID）をMarketo リードに関連付ける Cookie 同期プロセスが発生します。  上記のリード取得方法を使用して、関連する ECID 値を取得できます。  これを行うには、fields パラメーターに `ecids` を指定します。 例：`&fields=email,firstName,lastName,ecids`。

## 作成と更新

リードデータを取得する以外にも、API を使用してリードレコードを作成、更新、削除できます。 リードの作成と更新は、リクエストで定義されている操作タイプと同じエンドポイントを共有し、同時に最大 300 個のレコードを作成または更新できます。

>[!NOTE]
>
> [ リードを同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST) エンドポイントを使用した会社フィールドの更新はサポートされていません。 代わりに、[ 会社を同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST) エンドポイントを使用します。

>[!NOTE]
>
> 人物レコードのメール値を作成または更新する場合、メールアドレスのフィールドでは ASCII 文字のみがサポートされます。

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

このリクエストには、`action` と `lookupField` という 2 つの重要なフィールドが表示されます。  `action` は、リクエストの操作タイプを指定し、`createOrUpdate`、`createOnly`、`updateOnly` または `createDuplicate` を指定できます。 省略すると、アクションはデフォルトで `createOrUpdate` になります。  `lookupField` パラメーターは、アクションが `createOrUpdate` または `updateOnly` の場合に使用するキーを指定します。 `lookupField` を省略すると、デフォルトのキーは `email` になります。

デフォルトでは、デフォルトのパーティションが使用されます。 オプションで、`partitionName` パラメーターを指定できます。このパラメーターは、action が `createOnly` または `createOrUpdate` の場合にのみ機能します。 `partitionName` が追加の重複排除条件として機能するには、カスタム重複排除ルールのソースタイプに含まれている必要があります。 更新操作中に、指定したパーティションにリードが存在しない場合は、エラーが返されます。 API のみのユーザーが指定されたパーティションにアクセスする権限を持っていない場合は、エラーが返されます。

`id` フィールドは、システムが管理する一意のキーなので、`updateOnly` アクションを使用する際に `id` パラメーターとしてのみ含めることができます。

リクエストには、`input` パラメーター（リードレコードの配列）も必要です。 各リードレコードは、任意の数のリードフィールドを持つ JSON オブジェクトです。 レコードに含まれるキーは、そのレコードで一意である必要があり、すべての JSON 文字列は UTF-8 でエンコードされている必要があります。 「`externalCompanyId`」フィールドを使用すると、リードレコードを会社レコードにリンクできます。 「`externalSalesPersonId`」フィールドを使用して、引合レコードを販売担当者レコードにリンクできます。

注意：リードのアップサート・リクエストを同時にまたは連続して実行する場合に、同じキー値を持つ複数のリクエストを行う際に、最初のリターンより前に同じ値を持つ後続のコールが行われると、レコードが重複する可能性があります。 これを回避するには、`createOnly` を使用するか、必要に応じて `updateOnly` を使用するか、呼び出しをキューに登録し、同じキーを使用して後続の upsert 呼び出しを行う前に呼び出しが戻るのを待ちます。

## フィールド

リードオブジェクトには、標準フィールドと、オプションでカスタムフィールドが含まれています。 標準フィールドはすべてのMarketo Engage購読に存在するのに対して、カスタムフィールドは必要に応じてユーザーが作成します。 各フィールド定義は、フィールドを記述する一連の属性で構成されます。 属性の例としては、表示名、API 名、データタイプがあります。 これらの属性はまとめてメタデータと呼ばれます。

次のエンドポイントを使用すると、リードオブジェクト上のフィールドに対してクエリ、作成および更新を行うことができます。 これらの API では、所有している API ユーザーが、読み取り/書き込みスキーマ標準フィールドまたは読み取り/書き込みスキーマカスタムフィールドの権限の一方または両方の役割を持っている必要があります。

## クエリフィールド

リードフィールドのクエリは簡単です。 API 名で 1 つのリードフィールドに対してクエリを実行することも、すべてのリードフィールドのセットに対してクエリを実行することもできます。 使用する役割の権限に応じて、標準フィールドとカスタムフィールドの両方を取得できます。 非表示のフィールドも取得されます。

## 名前別

「名前によるリードフィールドの取得」エンドポイントは、リードオブジェクト上の単一フィールドのメタデータを取得します。 必須の fieldApiName パスパラメーターは、フィールドの API 名を指定します。 この応答は Describe Lead エンドポイントに似ていますが、フィールドがカスタムフィールドであるかどうかを示す、isCustom 属性などの追加メタデータが含まれています。

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

リードフィールドの取得エンドポイントは、以下を含むリードオブジェクト上のすべてのフィールドのメタデータを取得します。 デフォルトでは、最大 300 件のレコードが返されます。 `batchSize` クエリパラメーターを使用して、この数を減らすことができます。 `moreResult` 属性が true の場合は、より多くの結果が利用可能であることを意味します。 `moreResult` 属性が false を返す（使用できる結果がないことを意味する）まで、このエンドポイントの呼び出しを続行します。 この API から返された `nextPageToken` は、この呼び出しの次のイテレーションでは常に再利用する必要があります。

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

## フィールドを作成

リードフィールドの作成エンドポイントは、リードオブジェクトに 1 つ以上のカスタムフィールドを作成します。 このエンドポイントは、Marketo EngageUI で利用できる機能と同等の機能を提供します。 このエンドポイントを使用して最大 100 個のカスタムフィールドを作成できます。
API を使用してMarketo Engageの実稼動インスタンスで作成する各フィールドについては、慎重に検討してください。  作成したフィールドは、削除できません（非表示にしかできません）。 未使用のフィールドの急増は望ましくない手法であり、インスタンスが煩雑になります。

必須の入力パラメーターは、リードフィールドオブジェクトの配列です。 各オブジェクトには、1 つ以上の属性が含まれます。 必須の属性は、フィールドの UI 表示名、フィールドの API 名、フィールドタイプにそれぞれ対応する `displayName`、`name`、`dataType` です。  オプションで、`description`、`isHidden`、`isHtmlEncodingInEmail` および `isSensitive` を指定できます。

名前と `displayName` の命名には、いくつかのルールが関連付けられています。 name 属性は一意で、文字で始まり、文字、数字、アンダースコアのみを含める必要があります。 `displayName` は一意である必要があり、特殊文字を含めることはできません。  一般的な命名規則は、キャメルケースを `displayName` に適用して名前を作成することです。 例えば、「My Custom Field」という `displayName` を指定すると、「myCustomField」という名前が生成されます。

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

## フィールドを更新

「リードフィールドを更新」エンドポイントは、リードオブジェクトの 1 つのカスタムフィールドを更新します。 ほとんどの場合、Marketo EngageUI を使用して実行されるフィールド更新操作は、API を使用して実行できます。 次の表にまとめた違いがいくつかあります。

<table>
<tbody>
<tr>
<td style="width: 26.5306%;" rowspan="2"><strong>属性</strong></td>
<td style="width: 35%;" colspan="2"><strong>標準フィールド</strong></td>
<td style="width: 38.2654%;" colspan="2"><strong>カスタムフィールド</strong></td>
</tr>
<tr>
<td style="width: 17.449%;"><strong>API で更新可能ですか？</strong></td>
<td style="width: 17.551%;"><strong>UI で更新可能ですか？</strong></td>
<td style="width: 19.3878%;"><strong>API で更新可能ですか？</strong></td>
<td style="width: 18.8776%;"><strong>UI で更新可能ですか？</strong></td>
</tr>
<tr>
<td style="width: 26.5306%;">dataType</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">いいえ</td>
<td style="width: 19.3878%;">いいえ</td>
<td style="width: 18.8776%;">○</td>
</tr>
<tr>
<td style="width: 26.5306%;">description</td>
<td style="width: 17.449%;">○</td>
<td style="width: 17.551%;">○</td>
<td style="width: 19.3878%;">○</td>
<td style="width: 18.8776%;">○</td>
</tr>
<tr>
<td style="width: 26.5306%;">displayName</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">いいえ</td>
<td style="width: 19.3878%;">○</td>
<td style="width: 18.8776%;">○</td>
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
<td style="width: 17.551%;">○</td>
<td style="width: 19.3878%;">対応（API で作成されている場合）</td>
<td style="width: 18.8776%;">○</td>
</tr>
<tr>
<td style="width: 26.5306%;">isHtmlEncodingInEmail</td>
<td style="width: 17.449%;">○</td>
<td style="width: 17.551%;">○</td>
<td style="width: 19.3878%;">○</td>
<td style="width: 18.8776%;">○</td>
</tr>
<tr>
<td style="width: 26.5306%;">isSensitive</td>
<td style="width: 17.449%;">○</td>
<td style="width: 17.551%;">○</td>
<td style="width: 19.3878%;">○</td>
<td style="width: 18.8776%;">○</td>
</tr>
<tr>
<td style="width: 26.5306%;">length</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">いいえ</td>
<td style="width: 19.3878%;">いいえ</td>
<td style="width: 18.8776%;">いいえ</td>
</tr>
<tr>
<td style="width: 26.5306%;">名前</td>
<td style="width: 17.449%;">いいえ</td>
<td style="width: 17.551%;">いいえ</td>
<td style="width: 19.3878%;">いいえ</td>
<td style="width: 18.8776%;">いいえ</td>
</tr>
</tbody>
</table>

必須の `fieldApiName` パスパラメーターは、更新するフィールドの API 名を指定します。 必須の入力パラメーターは、単一のリードフィールドオブジェクトを含む配列です。  フィールドオブジェクトには、1 つ以上の属性が含まれています。

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

リードのプッシュは、リードをMarketoに同期する代わりとなるもので、主に標準のトリガーリード（Marketo フォームと同様の使用方法）よりも高度な同期機能を可能にするように設計されています。 このエンドポイントを使用すると、リードフィールドの同期に加えて、Cookie 値に基づいてリードを関連付け、それをエンドポイントに渡すことができます。 これを行うには、Marketoのメールをクリックして生成された `mkt_tok` 値を渡すか、呼び出しでプログラム名を渡します。 また、このエンドポイントは、Marketoのプログラムやキャンペーンに関連付けられた、単一のトリガー可能なアクティビティも作成します。 これにより、特定のキャンペーンまたはプログラムに関連付けられたリードキャプチャイベントをトリガーし、Marketo内から関連ワークフローを開始できます。

リードのプッシュ インターフェイスは、リードの同期に非常に似ています。 同じプライマリキーがすべて有効で、同じ API 名がフィールドに使用されます（これは常にアップサート操作なので、アクションパラメーターはありません）。 `programName` と入力パラメーターは必須で、`lookupField`、`source`、`reason` の各パラメーターはオプションです。 入力パラメーターは、リードオブジェクトの配列です。 結果のアクティビティは、対応する名前付きプログラムに関連付けられます。 `source` パラメーターと `reason` パラメーターは任意の文字列フィールドであり、リクエストに追加して、それらの値を結果のアクティビティに埋め込むことができます。 これらは、対応するトリガー（リードがMarketoにプッシュされる）およびフィルター（リードがMarketoにプッシュされる）の制約として使用できます。

匿名アクティビティに関するメモ。 以前の匿名アクティビティを新しく作成されたリードに関連付ける場合は、リードオブジェクトに cookies 属性を指定せずに、プッシュリード後にリードを関連付けを呼び出します。 アクティビティ履歴のない新しいリードを作成する場合は、リードオブジェクトの cookies 属性を指定するだけです。

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

`mkt_tok` パラメーターを渡すには、次のように入力パラメーターのリードレコード内の mktToken メンバーに値を割り当てます。

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

## 送信フォーム

送信フォームは、Marketoへのリードを同期する代わりとなるもので、Marketo フォームの送信と同等の機能を提供するように設計されています。 これにより、特定のキャンペーンまたはプログラムに関連付けられたリードキャプチャイベントをトリガーし、Marketo内から関連ワークフローを開始できます。

送信フォームエンドポイントは、次の機能をサポートしています。

* メールフィールドをプライマリキーとして使用してリードレコードをアップサート
* プログラムやキャンペーンに関連付けられた「フォームに入力」アクティビティを作成します
* Cookie 値に基づいてリードの関連付けを許可
* フォームフィールドの検証を実行

フォームの送信は、標準のリードデータベースパターンに従います。 POSTリクエストの JSON 本文の必須の入力メンバーに、1 つのオブジェクトレコードが渡されます。 必須の `formId` メンバーには、ターゲット Marketo フォーム ID が含まれています。

オプションの `programId` を使用して、リードを追加するプログラムを指定したり、プログラムメンバーのカスタムフィールドを追加するプログラムを指定したりできます。 `programId` が指定されている場合、リードがプログラムに追加され、フォームに存在するプログラムメンバーフィールドも追加されます。 指定したプログラムは、フォームと同じワークスペースにある必要があります。 フォームにプログラムメンバーのカスタムフィールドが含まれておらず、`programId` が指定されていない場合、リードはプログラムに追加されません。 フォームがプログラム内にあり、`programId` が指定されていない場合、そのプログラムは、1 つ以上のプログラムメンバーのカスタムフィールドがフォームに存在する場合に使用されます。

入力レコード内には、`leadFormFields` オブジェクトが必要です。 このオブジェクトには、入力するフォームフィールドに対応する 1 つ以上の名前と値のペアが含まれています。  すべてのフィールドが、指定したフォーム内で定義されている必要があります。 名前はフィールドの REST API 名です。 「`email`」フィールドは必須です。

`visitorData` メンバーオブジェクトはオプションで、`pageURL`、`queryString`、`leadClientIpAddress`、`userAgentString` など、ページ訪問データに対応する名前と値のペアを含みます。 フィルタリングやトリガーのために、追加のアクティビティフィールドに値を入力する場合に使用できます。

cookie メンバー文字列はオプションで、Munchkin cookie をMarketoのユーザーレコードに関連付けることができます。 新しいリードが作成されると、cookie 値が以前に別の既知のレコードに関連付けられていない限り、以前の匿名アクティビティがそのリードに関連付けられます。 cookie の値が以前に関連付けられていた場合、新しいアクティビティはレコードに対して追跡されますが、古いアクティビティは既存の既知のレコードから移行されません。 アクティビティ履歴のない新しいリードを作成するには、cookie メンバーを省略します。

フォームが格納されているワークスペースのプライマリパーティションに、新しいリードが作成されます。

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

ここでは、Marketo EngageUI 内から対応する「フォームに入力」アクティビティの詳細を確認できます。

![ フォーム UI への入力 ](assets/fill_out_form_activity_details.png)

## マージ

重複したレコードを結合する必要が生じる場合があり、Marketoは Merge Leads API を使用してこれを容易にします。 リードを結合すると、アクティビティログ、プログラム、キャンペーン、リストのメンバーシップおよび CRM 情報を組み合わせ、すべてのフィールド値を 1 つのレコードに結合します。 リードを結合では、リード ID をパスパラメーターとして使用し、単一の `leadId` をクエリパラメーターとして使用するか、`leadIds` パラメーターでコンマ区切りの ID のリストを使用します。

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

パスパラメーターで指定されたリードは勝者リードなので、結合されるレコード間で競合するフィールドがある場合、勝者レコードのフィールドが空で、勝者レコードの対応するフィールドが空でない場合を除き、勝者の値が取得されます。 `leadId` または `leadIds` のパラメーターで指定されたリードが、失注リードです。

SFDC同期が有効になっているサブスクリプションをお持ちの場合は、`mergeInCRM` パラメーターをリクエストで使用することもできます。 true に設定すると、CRM での対応する結合も実行されます。 両方のリードがSFDCにあり、一方が CRM リードで、もう一方が CRM 連絡先である場合、勝者は CRM 連絡先（勝者として指定されたリードに関係なく）になります。 リードの 1 つがSFDCにあり、もう 1 つがMarketoのみである場合、勝者はSFDC リードです（どのリードが勝者として指定されているかに関係なく）。

## Web アクティビティを関連付け

Marketoは、リードトラッキング（Munchkin）を通じて、貴社の Web サイトとMarketo ランディングページへの訪問者の Web アクティビティを記録します。 これらのアクティビティ（訪問回数およびクリック数）は、リードのブラウザーに設定された「_mkto_trk」 cookie に対応するキーで記録され、Marketoはこれを使用して同じ人物のアクティビティを追跡します。 通常、リードレコードへの関連付けは、リードがMarketoのメールからクリックスルーするか、Marketoのフォームに入力する際に行われますが、場合によっては、関連付けが別のタイプのイベントによってトリガーされ、リードの関連付けエンドポイントを使用して実行できます。 エンドポイントは、既知のリードレコードの ID をパスパラメーターとして受け取り、cookie クエリパラメーターの「_mkto_trk」 cookie 値を取得します。

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

Cookie が既に既知のリードレコードに関連付けられている場合、別のリードレコードでこの API を使用すると、そのレコードに対して新しい web アクティビティが記録されますが、既存の web アクティビティは新しいレコードに移動されません。
メンバーシップ

リードレコードは、静的リストまたはプログラムのメンバーシップに基づいて取得することもできます。 さらに、リードがメンバーとして属するすべての静的リスト、プログラムまたはスマートキャンペーンを取得できます。

応答構造とオプションのパラメーターは、フィルタータイプによるリードの取得の構造と同じですが、filterType と filterValues はこの API では使用できません。
Marketo UI を使用してリスト id にアクセスするには、リストに移動します。 リスト `id` は、静的リスト `https://app-**&#x200B;**.marketo.com/#ST1001A1` の URL 内にあります。 この例では、1001 がリストの `id` です。

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

リード ID によるリストの取得エンドポイントは、パスパラメーター `id` リードレコードを受け取り、リードがメンバーになっているすべての静的リストレコードを返します。

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

プログラムメンバーシップは、リストと同様の方法で取得できます。 プログラム ID でリードを取得エンドポイントを呼び出して `programId` パスパラメーターを渡す場合も、同じオプションリクエストパラメーターを使用できます。

オプションで、返すフィールド名のコンマ区切りリストを含むフィールドパラメーターを渡すことができます。 fields パラメーターがこのリクエストに含まれていない場合は、デフォルトのフィールド `email`、`updatedAt`、`createdAt`、`lastName`、`firstName`、`membership` および `id` が返されます。 フィールドのリストをリクエストするときに、特定のフィールドがリクエストされても返されなかった場合、値は null であることが暗示されます。

応答構造は、結果の配列内の各項目がリードである点で非常に似ていますが、各レコードには「メンバーシップ」と呼ばれる子オブジェクトも含まれる点が異なります。 このメンバーシップオブジェクトには、呼び出しで示されたプログラムへのリードの関係に関するデータが含まれ、常に `progressionStatus`、`acquiredBy`、`reachedSuccess`、`membershipDate` が表示されます。 親プログラムがエンゲージメントプログラムでもある場合、メンバーシップには、エンゲージメントプログラムにおけるその位置とアクティビティを示す `stream`、`nurtureCadence`、`isExhausted` のメンバーが含まれます。

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

「リード ID でプログラムを取得」エンドポイントは、リードレコード ID のパスパラメーターを受け取り、リードがメンバーになっているすべてのプログラムレコードを返します。 オプションの `filterType` パラメーターと `filterValues` パラメーターを使用すると、プログラム ID でフィルタリングできます。

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

リード ID でスマートキャンペーンを取得エンドポイントは、リードレコード ID パスパラメーターを受け取り、リードがメンバーになっているすべてのスマートキャンペーンレコードを返します。

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

リードの削除は、リードを削除エンドポイントを使用すると簡単に行えます。  本文の id 属性を使用して、削除するリード id を指定します。  リクエストあたりの最大リード数は 300 です。  Content-Type:application/json ヘッダーを使用します。

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
* リード レコードの externalSalesPersonId フィールドを通じた SalesPerson
* プログラムメンバーシップによるプログラム
* リストのメンバーシップを使用したリスト
* アクティビティの leadId フィールドを通じたアクティビティ
* リードレコードの個々のセグメントフィールドを通じたセグメント化
* リードレコードの leadPartitionId によるパーティション

## タイムアウト

リードエンドポイントは、以下に記載されていない限り、タイムアウトが 30 秒になります。

* リードを同期：90 秒
* 関連付けられたリード：60s
* リードを結合：180s
* リード パーティションの更新：60s
* リードをMarketoにプッシュ：90 年代
* フィルタータイプ別のリードの取得：60s
* リスト ID によるリードの取得：60s
