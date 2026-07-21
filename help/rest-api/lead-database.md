---
title: リードデータベース
feature: REST API, Database
description: オブジェクト、CRUDおよび記述方法、クエリパターン、バッチ制限、CRM統合の制限について説明するMarketo リードデータベース APIのガイドです。
exl-id: e62e381f-916b-4d56-bc3d-0046219b68d3
TQID: https://experienceleague.adobe.com/7lGbhE92lvIE-XkMyUIaK9GrreZVRdM-WVZTpHARhxE
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
source-wordcount: 1058
ht-degree: 6%

---

# リードデータベース

Marketo Lead Database APIは、Marketoと個人および人物関連のデータを交換します。 このデータには、アクティビティ、機会、企業が含まれます。

## オブジェクト

リードデータベースには、次のオブジェクトが含まれます。

- リード
- 会社／アカウント
- 重点顧客
- 商談
- 商談ロール
- セールス担当者
- カスタムオブジェクト
- アクティビティ
- リストとプログラムメンバーシップ

ほとんどのリードデータベースオブジェクトは、作成、読み取り、更新および削除メソッドをサポートしています。 Describe メソッドには、各オブジェクトタイプで使用可能なフィールドが用意されています。 リード以外のオブジェクトの場合は、重複排除に使用されるフィールドと、レコードの取得時に検索可能なフィールドも識別します。

リードオブジェクトは、Marketo アプリケーションで最も多様な用途をリードに持つため、最も幅広い機能セットをサポートします。

## API

リードデータベース API エンドポイント、パラメーター、モデリング情報の完全なリストについては、[&#x200B; リードデータベース API エンドポイント リファレンス &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi)を参照してください。

インスタンスにネイティブのMicrosoft DynamicsまたはSalesforce.com CRM統合がある場合、会社、商談、商談ロール、および営業担当者のAPIは無効になります。 CRMはこれらのレコードを管理するため、Marketo APIを通じてレコードにアクセスしたり更新したりすることはできません。

- 最大バッチサイズ（標準）：300 個のレコード
- 最大バッチサイズ（一括）：10 MB のファイル
- デフォルトのバッチサイズ：300 個レコード
- Content-type ヘッダー（標準）：application/json
- Content-type ヘッダー（一括）：multipart/form-data

## 説明

Describe APIは、リード、企業、商談、役割、セールス担当者、カスタムオブジェクトに対して使用できます。 これを使用すると、更新やクエリに使用できるオブジェクトメタデータとフィールドを取得できます。

リードを記述を除き、各Describe エンドポイントは次を返します。

- `dedupeFields`：重複排除に使用できるキー。
- `searchableFields`: クエリに使用できるキー。

```http
GET /rest/v1/opportunities/roles/describe.json
```

```json
{
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[
      {
         "name":"opportunityRole",
         "displayName":"Opportunity Role",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"marketoGUID",
         "dedupeFields":[
            "externalOpportunityId",
            "leadId",
            "role"
         ],
         "searchableFields":[
            [
               "externalOpportunityId",
               "leadId",
               "role"
            ],
            [
               "marketoGUID"
            ],
            [
               "leadId"
            ],
            [
               "externalOpportunityId"
            ]
         ],
         "fields":[
            {
               "name":"marketoGUID",
               "displayName":"Marketo GUID",
               "dataType":"string",
               "length":36,
               "updateable":false
            },
            {
               "name":"externalOpportunityId",
               "displayName":"External Opportunity Id",
               "dataType":"string",
               "length":50,
               "updateable":false
            },
            {
               "name":"leadId",
               "displayName":"Lead Id",
               "dataType":"integer",
               "updateable":false
            },
            {
               "name":"role",
               "displayName":"Role",
               "dataType":"string",
               "length":50,
               "updateable":false
            },
            {
               "name":"isPrimary",
               "displayName":"Is Primary",
               "dataType":"boolean",
               "updateable":true
            },
            {
               "name":"externalCreatedDate",
               "displayName":"External Created Date",
               "dataType":"datetime",
               "updateable":true
            }
         ]
      }
   ]
}
```

この例では、`dedupeFields`は複合キーです。 今後の作成と更新に`dedupeFields` モードを使用する場合は、各役割に`externalOpportunityId`、`leadId`および`role`を含めてください。

`searchableFields`配列には、役割レコードのクエリに使用できるフィールドが一覧表示されます。 このリストには、`externalOpportunityId`、`leadId`、`role`の複合キーが含まれています。

`fields`応答パラメーターは、各フィールドに次の情報を提供します。

- 名前：
- Marketo UIに表示されている`displayName`。
- データタイプ：
- 作成後にフィールドを更新できるかどうか。
- フィールドの長さ（該当する場合）。

## クエリ

リードデータベースオブジェクトは、1つのフィールドを参照する単純なキーの基本的なクエリパターンを共有します。

```http
GET /rest/v1/{type}.json?filterType={field to query}&filterValues={comma-separated list of possible values}
```

リードを除くすべてのオブジェクトに対して、対応する記述応答で`searchableFields`から`{field to query}`を選択します。 最大300個の値のコンマ区切りリストを指定します。

また、次のオプションのクエリパラメーターも含めることができます。

- `batchSize`：返す結果の数を指定する整数。 デフォルト値と最大値は300です。
- `nextPageToken`: ページングの前の呼び出しから返されたトークン。 詳しくは、[&#x200B; トークンのページング &#x200B;](paging-tokens.md)を参照してください。
- `fields`：各レコードに対して返されるフィールド名のコンマ区切りリスト。 有効なフィールドについては、対応する説明を参照してください。 返されないフィールドをリクエストした場合、その値はnullであることが暗黙的に示されます。
- `_method`: POST HTTP メソッドを使用してクエリを送信します。 使用方法については、_method=GET セクションを参照してください。

次の例では、商談に対してクエリを実行します。

```http
GET /rest/v1/opportunities.json?filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa&dff23271-f996-47d7-984f-f2676861b5fc,dff23271-f996-47d7-984f-f2676861b5fb
```

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fa ",
         "externalOpportunityId":"19UYA31581L000000",
         "name":"Chairs",
         "description":"Chairs",
         "amount":"1604.47",
         "source":"Inbound Sales Call/Email"
      },
      {
         "seq":1,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fc ",
         "externalOpportunityId":"29UYA31581L000000",
         "name":"Big Dog Day Care-Phase12",
         "description":"Big Dog Day Care-Phase12",
         "amount":"1604.47",
         "source":"Email"
      }
   ]
}
```

この呼び出しの`filterType`は、「marketoGUID」ではなく「idField」です。 「idField」と「dedupeFields」の両方は、対応するフィールドにエイリアスを使用できる特殊なケースです。 呼び出しは「marketoGUID」を明示的に設定していませんが、ルックアップフィールドは残ります。

オブジェクトの説明で`idField`と`dedupeFields`によって識別されたフィールドまたはフィールドセットは、クエリに対して常に有効な`filterTypes`です。 この呼び出しは、filterValuesのGUIDに一致するレコードを返します。 一致するレコードがない場合、応答は成功を示し、空の結果配列を返します。

一致するレコードセットが300または指定された`batchSize`のいずれか小さい方を超える場合、応答には値がtrueの`moreResult`と`nextPageToken`が含まれます。 その後の呼び出しにトークンを含めて、より多くのレコードを取得します。 詳しくは、[&#x200B; トークンのページング &#x200B;](paging-tokens.md)を参照してください。

### 長い URI

URIは、GUIDでクエリする場合など、REST サービスの8 KB制限を超える可能性があります。 この場合は、GETの代わりにHTTP POST メソッドを使用し、`_method=GET` クエリパラメーターを追加します。

POST本文の残りのクエリパラメーターを「application/x-www-form-urlencoded」文字列として渡します。 関連するコンテンツタイプヘッダーも渡します。

```http
POST /rest/v1/opportunities.json?_method=GET
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa&dff23271-f996-47d7-984f-f2676861b5fc,dff23271-f996-47d7-984f-f2676861b5fb,544fb7f5-2ddf-4fca-ae32-7e6ef1415e9f,f1ba41a2-69d1-4a35-9807-0e159d66f2c9,f7521272-3331-4a89-a768-222baff2f894
```

複合キーをクエリする場合は、`_method=GET` パラメーターも必要です。

### 複合キー

複合キーをクエリするには、JSON本文を使用してPOST リクエストを送信します。 このパターンは、`filterType`が複数のフィールドを持つ`dedupeFields` オプションである場合にのみ使用してください。

複合キーは現在、商談ロールと一部のカスタムオブジェクトでのみ使用されています。 次の例では、`dedupeFields`の複合キーを使用して商談ロールをクエリします。

```http
POST /rest/v1/opportunities/roles.json?_method=GET
```

```json
{
   "filterType":"dedupeFields",
   "fields":[
      "marketoGuid",
      "externalOpportunityId",
      "leadId",
      "role"
   ],
   "input":[
      {
        "externalOpportunityId":"Opportunity1",
        "leadId": 1,
        "role": "Captain"
      },
      {
        "externalOpportunityId":"Opportunity2",
        "leadId": 1872,
        "role": "Commander"
      },
      {
        "externalOpportunityId":"Opportunity3",
        "leadId": 273891,
        "role": "Lieutenant Commander"
      }
   ]
}
```

JSON オブジェクトは、`filterValues`を除く単純キークエリに使用されるすべてのクエリパラメーターを受け入れます。 `filterValues`の代わりに、JSON オブジェクトの「入力」配列を指定します。 各オブジェクトには、複合キーのすべてのフィールドを含める必要があります。 この例では、フィールドは`externalOpportunityId`、`leadId`および`role`です。

リクエストは指定された入力に対して`roles`をクエリし、一致する結果を返します。 応答に`moreResult=true`と`nextPageToken`が含まれる場合は、すべての元の入力と`nextPageToken`を次のリクエストに含めます。

## 作成と更新

JSON本文を使用してPOST リクエストを送信することで、リードデータベースレコードを作成および更新します。 商談、役割、カスタムオブジェクト、企業、営業担当者は、同じインターフェイスを使用しています。 リードは別のインターフェイスを使用します。詳しくは、リードのドキュメントを参照してください。

必須パラメーターは`input`のみです。最大300 オブジェクトの配列です。 各オブジェクトには、挿入または更新するフィールドが含まれます。

次のオプションのパラメーターも含めることができます。

- `action`: `createOnly`、`updateOnly`または`createOrUpdate`を受け入れます。 省略した場合、モードはデフォルトで`createOrUpdate`になります。
- `dedupeBy`: アクションがcreateOnlyまたは`createOrUpdate`に設定されている場合、`idField`または`dedupeFields`を受け入れます。 省略した場合、モードはデフォルトで`dedupeFields`になります。

`dedupeBy`が`idField`の場合、説明に記載されている`idField`は重複排除に使用され、各レコードに含める必要があります。 `idField` モードは、`createOnly` モードと互換性がありません。

`dedupeBy`が`dedupeFields`の場合、オブジェクトの説明にリストされている各`dedupeFields` フィールドをすべてのレコードに含めます。

フィールド値を渡すと、データベースは値`null`または空の文字列を`null`として書き込みます。

```http
POST /rest/v1/opportunities.json
```

```json
{
   "action":"createOrUpdate",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "externalOpportunityId":"19UYA31581L000000",
         "name":"Chairs",
         "description":"Chairs",
         "amount":"1604.47",
         "source":"Inbound Sales Call/Email"
      },
      {
         "externalOpportunityId":"29UYA31581L000000",
         "name":"Big Dog Day Care-Phase12",
         "description":"Big Dog Day Care-Phase12",
         "amount":"1604.47",
         "source":"Email"
      }
   ]
}
```

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "status":"updated",
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq":1,
         "status":"created",
         "marketoGUID":"cff23271-f996-47d7-984f-f2676861b5fb"
      }
   ]
}
```

リード APIを除き、create呼び出しとupdate呼び出しは、`result`配列内の各オブジェクトの`seq` フィールドを返します。 この番号は、リクエスト内の更新されたレコードの位置に対応します。

各結果は、オブジェクトタイプの`idField`値と、「作成済み」、「更新」、「スキップ済み」の`status`も返します。 ステータスがスキップされた場合、結果には「reasons」配列が含まれます。 理由オブジェクトには、レコードがスキップされた理由を説明するコードとメッセージが含まれています。 詳しくは、[&#x200B; エラーコード &#x200B;](error-codes.md)を参照してください。

### 削除

リードを除き、リードデータベースオブジェクトは標準の削除インターフェイスを使用します。 入力に加えて、必須パラメーターはidFieldまたは重複排除フィールドを受け入れる`deleteBy,`のみです。

次の例では、カスタムオブジェクトを削除します。

```http
POST /rest/v1/customobjects/{name}/delete.json
```

```json
{
   "deleteBy":"dedupeFields",
   "input":[
      {
         "vin":"19UYA31581L000000"
      },
      {
         "vin":"29UYA31581L000000"
      },
      {
         "vin":"39UYA31581L000000"
      }
   ]
}
```

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "status": "deleted"
      },
      {
         "seq":1,
         "marketoGUID":"da42707c-4dc4-4fc1-9fef-f30a3017240a",
         "status": "deleted"
      },
      {
         "seq":2,
         "status": "skipped"
         "reasons":[
            {
               "code":"1013",
               "message":"Object not found"
            }
         ]
      }
   ]
}
```

応答には、`seq`、`status`および`marketoGUID`が含まれます。 スキップされたレコードの場合は、`reasons`も含まれます。

特定のオブジェクトタイプのCRUD操作について詳しくは、そのオブジェクトのドキュメントを参照してください。
