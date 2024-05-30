---
title: "リードデータベース"
feature: REST API, Database
description: メインのリードデータベースを操作します。
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 0%

---


# リードデータベース

Marketo Lead Database API は、Marketoが提供する最も頻繁に使用される API で、アクティビティ、オポチュニティ、会社など、Marketoからの人物および人物に関連するデータのデータをやり取りできます。

## オブジェクト

リードデータベースオブジェクトには、以下が含まれます。

- リード
- 会社/アカウント
- 重点顧客
- 商談
- オポチュニティの役割
- 営業担当者
- カスタムオブジェクト
- アクティビティ
- リストとプログラムメンバーシップ

これらのオブジェクトの多くには、少なくとも Create、Read、Update、および Delete メソッドが含まれています。 また、タイプごとに使用可能なフィールドのリストを提供する「説明」方法、重複排除（リード以外のオブジェクトの場合）に使用されるフィールドのリスト、およびレコードの取得に使用できるフィールドのリストも含まれます。 Marketo アプリケーション内で最も多様な機能を備えているため、最も豊富なセットがリードに提供されます。

## API

パラメーターやモデリング情報を含む、リードデータベース API エンドポイントの完全なリストについては、を参照してください。 [リードデータベース API エンドポイントのリファレンス](https://developer.adobe.com/marketo-apis/api/mapi/).

ネイティブ CRM 統合が有効なインスタンス（Microsoft Dynamics またはSalesforce.com）の場合、会社、商談、商談の役割、営業担当者の API は無効になります。 レコードは、有効な場合は CRM を通じて管理され、Marketoの API を使用してアクセスまたは更新することはできません。

- 最大バッチサイズ （標準）:300 レコード
- 最大バッチサイズ （バルク）:10 MB のファイル
- デフォルトのバッチサイズ : 300 レコード
- Content-type ヘッダー（標準）:application/json
- コンテンツタイプヘッダー（一括）:multipart/form-data

## 説明

リード、会社、商談、役割、販売担当者、カスタムオブジェクトの場合は、説明 API が提供されます。 これを呼び出すと、オブジェクトのメタデータと、更新およびクエリに使用できるフィールドのリストが取得されます。 説明は、Marketoとの適切な統合を設計する上で重要な役割を果たします。 オブジェクトの操作の仕組みと禁止、オブジェクトの作成、更新、クエリの方法に関する豊富なメタデータを提供します。 リードを記述とは別に、これらはそれぞれ使用可能なキーのリストを返します `deduplication` が含まれる `dedupeFields` 応答パラメーター。 フィールドのリストは、でクエリするためのキーとして使用できます。 `searchableFields` 応答パラメーター。

```
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

この例では、 `dedupeFields` は、実際には複合キーです。 つまり、を使用すると、今後は更新や作成がおこなわれます `dedupeFields` モードです。3 つすべてを含める必要があります `externalOpportunityId`, `leadId`、および `role` 役割ごとに調整します。 この `searchableFields` また、配列には、役割レコードのクエリに使用できるフィールドのリストも含まれています。 これには、の複合キーも含まれます `externalOpportunityId`, `leadId`、および `role`.

また、各フィールドの名前を提供するフィールド応答パラメーターもあり、 `displayName` Marketo UI に表示されるとおり、フィールドのデータタイプ、作成後に更新できるかどうか、および該当する場合はフィールドの長さです。

## クエリ

リードデータベースオブジェクトはすべて、1 つのフィールドのみが参照される単純なキーに対するクエリの基本的なパターンを共有します。

```
GET /rest/v1/{type}.json?filterType={field to query}&filterValues={comma-separated list of possible values}
```

リードを除くすべてのオブジェクトで、対応する describe 呼び出しの searchableFields から {field to query} を選択し、最大 300 個の値のコンマ区切りリストを作成できます。 次のオプションのクエリパラメーターもあります。

- `batchSize`  – 返される結果の数の整数。 デフォルトおよび最大値は 300 です。
- `nextPageToken`  – 前回のページング呼び出しから返されたトークン。 参照： [ページングトークン](paging-tokens.md) を参照してください。
- `fields`  – 各レコードに対して返すフィールド名のコンマ区切りリスト。 有効なフィールドのリストについては、対応する説明を参照してください。 特定のフィールドがリクエストされても、返されなかった場合、値は null であることが暗示されます。
- `_method` - POST HTTP メソッドを使用してクエリを送信する場合に使用します。 使用方法については、以下の_method=GETの節を参照してください。

簡単な例として、商談のクエリを見てみましょう。

```
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

この `filterType` この呼び出しで指定されているのは「marketoGUID」ではなく「idField」です。 このフィールドと「dedupeFields」は、両方とも特殊なケースで、idField または dedupeFields に対応するフィールドに、この方法でエイリアスを設定できます。 「marketoGUID」は、引き続き呼び出しでの結果のルックアップフィールドですが、呼び出しで明示的に設定されているわけではありません。 によって示されるフィールドやフィールドのセット `idField` および `dedupeFields` オブジェクトの説明は常に有効です `filterTypes` クエリの場合。 この呼び出しは、filterValues に含まれる GUID に一致するレコードを検索し、一致するレコードを返します。 このメソッドを使用してレコードが見つからない場合でも、応答は成功を示しますが、検索が正常に実行されたにもかかわらず、返されるレコードが存在しなかったため、結果の配列は空になります。

クエリ内のレコードのセットが 300 を超えた場合、または `batchSize` が指定された場合、いずれか小さい方の応答にはメンバーが含まれます `moreResult` 値が true で、 `nextPageToken`。これを後続の呼び出しに含めて、より多くのセットを取得できます。 参照： [ページングトークン](paging-tokens.md) を参照してください。

### 長い URI

GUID によるクエリ時など、URI が長くなり、REST サービスで許可されている 8 KB を超える場合があります。 この場合、GETの代わりに HTTP POSTメソッドを使用し、クエリパラメーターを追加する必要があります `_method=GET`. さらに、残りのクエリパラメーターは、「application/x-www-form-urlencoded」文字列としてPOSTー本文に渡し、関連する Content-type ヘッダーを渡す必要があります。

```
POST /rest/v1/opportunities.json?_method=GET
```

```
Content-Type: application/x-www-form-urlencoded
```

```
filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa&dff23271-f996-47d7-984f-f2676861b5fc,dff23271-f996-47d7-984f-f2676861b5fb,544fb7f5-2ddf-4fca-ae32-7e6ef1415e9f,f1ba41a2-69d1-4a35-9807-0e159d66f2c9,f7521272-3331-4a89-a768-222baff2f894
```

長い URI に加えて、複合キーをクエリする場合にも、このパラメーターが必要です。

### 複合キー

複合キーをクエリするパターンは、JSON 本文を持つPOSTを送信する必要があるので、単純なキーとは異なります。 これは、すべてのケースで必要というわけではなく、 `dedupeFields` 複数のフィールドを持つオプションは、として使用されます `filterType`. 現在、複合キーは、商談役割と一部のカスタムオブジェクトでのみ使用されています。 から複合キーを使用した商談の役割クエリの例を見てみましょう `dedupeFields`:

```
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

JSON オブジェクトの構造はほとんどフラットで、単純なキーを持つクエリのクエリパラメーターはすべて、次を除き、有効なメンバーです `filterValues`. フィルター値の代わりに、JSON オブジェクトの「入力」配列があります。この配列には、複合キーの各フィールドのメンバーが必要です。この場合、これらは次のようになります `externalOpportunityId`, `leadId`、および `role`. これにより、次のクエリが実行されます `roles`指定された入力に対して、と一致する結果を返します。 応答がパラメーターを返す場合 `moreResult=true`、および `nextPageToken`を設定する場合は、元の入力をすべて含めて、 `nextPageToken` クエリが正しく実行されるようにするには、次の操作を行います。

## 作成と更新

リードデータベースレコードの作成と更新はすべて、JSON 本文を含む POST を通じて実行されます。 商談、役割、カスタムオブジェクト、会社、営業担当者のインターフェイスはそれぞれ同じです。 リードのインターフェイスは少し異なります。詳しくは、このページを参照してください。

必須パラメーターはという配列のみです。 `input` 最大 300 個のオブジェクトが含まれ、各オブジェクトには、メンバーとして挿入/更新するフィールドが含まれます。 オプションで、次を含めることもできます `action` パラメーター。次のいずれかを指定できます。 `createOnly`, `updateOnly`、または `createOrUpdate`. アクションを省略すると、モードのデフォルト値はになります。 `createOrUpdate`. `dedupeBy` は、action が createOnly またはに設定されている場合に使用できるもう 1 つのオプションパラメーターです `createOrUpdate`. ` dedupeBy` 次のいずれかになります `idField`、または `dedupeFields`. 次の場合 `idField` が選択されている場合、が選択されてから `idField` 説明内にリストされているは、重複排除に使用され、各レコードに含める必要があります。 `idField` モードはと互換性がありません `createOnly` モード。 次の場合 `dedupeFields` が選択された後、 `dedupeFields` 使用するオブジェクトの説明にリストされ、各レコードにそれぞれを含める必要があります。 次の場合 `dedupeBy` パラメーターを省略した場合、モードのデフォルトは `dedupeFields`.

フィールド値のリストを渡す場合、の値 `null`または空の文字列がとしてデータベースに書き込まれます。 `null`.

```
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

リード API 以外で、リードデータベースオブジェクトを作成または更新する呼び出しでは、 `seq` 内の各オブジェクトのフィールド `result` 配列。 リストされる番号は、行われたリクエスト内の更新されたレコードの順序に対応します。 各項目は、の値を返します `idField` オブジェクトタイプの場合、および `status`. ステータスフィールドは、「作成済み」、「更新済み」、または「スキップ済み」のいずれかを示します。  ステータスがスキップされた場合は、コードとメッセージを含む 1 つ以上の理由オブジェクトを含む、対応する「理由」配列も存在し、レコードがスキップされた理由を示します。 参照： [エラーコード](error-codes.md) （詳細情報）。

### 削除

削除用のインタフェースは、リード以外のリード・データベース・オブジェクトに対して標準で使用されます。 入力以外に、必要なパラメーターは 1 つだけです `deleteBy,` 値は、idField または dedupeFields にすることができます。 次に、いくつかのカスタムオブジェクトの削除を見てみましょう。

```
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

この `seq`, `status`, `marketoGUID`、および `reasons` 全員が今頃よく知っているはずだ。

個々のオブジェクトタイプでの CRUD 操作の操作について詳しくは、それぞれのページを参照してください。
