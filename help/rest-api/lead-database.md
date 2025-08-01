---
title: リードデータベース
feature: REST API, Database
description: メインのリードデータベースを操作します。
exl-id: e62e381f-916b-4d56-bc3d-0046219b68d3
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 97%

---

# リードデータベース

Marketo Lead Database API は、Marketo が提供する最も頻繁に利用される API で、アクティビティ、商談、会社など、Marketo からのユーザおよびユーザ関連データのデータ交換が可能になります。

## オブジェクト

リードデータベースオブジェクトには、次が含まれます。

- リード
- 会社／アカウント
- 重点顧客
- 商談
- 商談ロール
- セールス担当者
- カスタムオブジェクト
- アクティビティ
- リストとプログラムメンバーシップ

これらのオブジェクトのほとんどには、少なくとも Create、Read、Update および Delete メソッドが含まれています。また、各タイプで使用可能なフィールドのリスト、重複排除に使用されるフィールドのリスト（リード以外のオブジェクトの場合）、レコードの取得時に検索可能なフィールドのリストを提供する「Describe」メソッドも含まれています。Marketo アプリケーション内で最も多様な機能を持つリードには、最も豊富な機能セットが提供されています。

## API

パラメーターやモデリング情報を含む、Lead Database API エンドポイントの完全なリストについて詳しくは、[Lead Database API エンドポイント参照](https://developer.adobe.com/marketo-apis/api/mapi/)を参照してください。

ネイティブ CRM 統合（Microsoft Dynamics または Salesforce.com）が有効なインスタンスの場合、Company API、Opportunity API、Opportunity Role API、Sales Person API は無効になります。レコードは、CRM を通じて管理され、Marketo API 経由でアクセスまたは更新できません。

- 最大バッチサイズ（標準）：300 個のレコード
- 最大バッチサイズ（一括）：10 MB のファイル
- デフォルトのバッチサイズ：300 個レコード
- Content-type ヘッダー（標準）：application/json
- Content-type ヘッダー（一括）：multipart/form-data

## 説明

リード、会社、商談、ロール、セールス担当者、カスタムオブジェクトの場合は、説明 API が提供されます。これを呼び出すと、オブジェクトのメタデータと、更新およびクエリに使用できるフィールドのリストが取得されます。説明は、Marketo との適切な統合を設計する上で重要な部分です。オブジェクトとやり取りできる方法とできない方法や、オブジェクトの作成、更新、クエリを実行する方法に関する豊富なメタデータを提供します。「リードを説明」を除き、これらはそれぞれ、`dedupeFields` 応答パラメーターで `deduplication` に使用できるキーのリストを返します。フィールドのリストは、`searchableFields` 応答パラメーターでクエリを実行するキーとして使用できます。

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

この例では、`dedupeFields` は実際には複合キーです。つまり、今後の更新と作成で `dedupeFields` モードを使用する際は、各ロールに対して `externalOpportunityId`、`leadId` および `role` の 3 つすべてを含める必要があります。`searchableFields` 配列は、ロールレコードのクエリに使用できるフィールドのリストも提供します。これには、`externalOpportunityId`、`leadId`、`role` の複合キーも含まれます。

また、fields 応答パラメーターもあります。各フィールドの名前、Marketo UI に表示される `displayName`、フィールドのデータタイプ、作成後に更新できるかどうか、該当する場合はフィールドの長さを提供します。

## クエリ

リードデータベースオブジェクトはすべて、1 つのフィールドのみが参照されるシンプルなキーに対してクエリを実行する基本パターンを共有します。

```
GET /rest/v1/{type}.json?filterType={field to query}&filterValues={comma-separated list of possible values}
```

リードを除くすべてのオブジェクトで、対応する describe 呼び出しの searchableFields から {field to query} を選択し、最大 300 個の値のコンマ区切りリストを作成できます。 次のオプションのクエリパラメーターもあります。

- `batchSize` - 返される結果の数の整数値。デフォルトと最大値は 300 です。
- `nextPageToken` - ページングの前回の呼び出しから返されたトークン。詳しくは、[ページングトークン](paging-tokens.md)を参照してください。
- `fields` - 各レコードに対して返されるフィールド名のコンマ区切りのリスト。有効なフィールドのリストについて詳しくは、対応する説明を参照してください。特定のフィールドがリクエストされたが返されない場合、その値は null であると見なされます。
- `_method` - POST HTTP メソッドを使用してクエリを送信するのに使用されます。使用方法について詳しくは、以下の _method=GET の節を参照してください。

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

この呼び出しで指定された `filterType` は、「marketoGUID」ではなく「idField」です。これと「dedupeFields」は、両方とも特殊なケースで、idField または dedupeFields に対応するフィールドに、この方法でエイリアスを設定できます。「marketoGUID」は、引き続き呼び出しの結果のルックアップフィールドですが、呼び出しでは明示的に設定されません。オブジェクトの説明の `idField` および `dedupeFields` によって示されるフィールドやフィールドセットは、常にクエリの有効な `filterTypes` になります。この呼び出しでは、filterValues に含まれる GUID に一致するレコードを検索し、一致するレコードを返します。このメソッドを使用してレコードが見つからない場合、応答は引き続き成功を示します。ただし、検索は正常に実行されたが返されるレコードがなかったので、結果配列は空になります。

クエリ内のレコードのセットが 300 を超えるか、指定された `batchSize` のいずれか小さい方を超える場合、応答には、値が true のメンバー `moreResult` と、セットのさらに多くを取得する後続の呼び出しに含めることができる `nextPageToken` が含まれます。詳しくは、[ページングトークン](paging-tokens.md)を参照してください。

### 長い URI

GUID でクエリを実行する際など、URI が長くなり、REST サービスで許可されている 8 KB を超える場合があります。この場合、GET の代わりに HTTP POST メソッドを使用し、クエリパラメーター `_method=GET` を追加する必要があります。さらに、残りのクエリパラメーターは、POST 本文で「application/x-www-form-urlencoded」文字列として渡され、関連する Content-type ヘッダーを渡す必要があります。

```
POST /rest/v1/opportunities.json?_method=GET
```

```
Content-Type: application/x-www-form-urlencoded
```

```
filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa&dff23271-f996-47d7-984f-f2676861b5fc,dff23271-f996-47d7-984f-f2676861b5fb,544fb7f5-2ddf-4fca-ae32-7e6ef1415e9f,f1ba41a2-69d1-4a35-9807-0e159d66f2c9,f7521272-3331-4a89-a768-222baff2f894
```

長い URI に加えて、複合キーのクエリを実行する場合にもこのパラメータが必要です。

### 複合キー

複合キーのクエリを実行するパターンは、JSON 本文を含む POST を送信する必要があるので、シンプルなキーとは異なります。これは、すべてのケースで必要なわけではなく、`filterType` として複数のフィールドを持つ `dedupeFields` オプションを使用する場合にのみ必要です。現在、複合キーは商談ロールと一部のカスタムオブジェクトでのみ使用されます。`dedupeFields` の複合キーを使用した商談ロールのクエリの例を見てみましょう。

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

JSON オブジェクトの構造はほとんどフラットで、`filterValues` を除き、シンプルなキーを持つクエリのすべてのクエリパラメーターは有効なメンバーです。フィルター値の代わりに、JSON オブジェクトの「input」配列があり、各配列には複合キーの各フィールドのメンバーが必要です。この場合、これらは `externalOpportunityId`、`leadId` および `role` です。これにより、指定された入力に対して `roles` のクエリが実行され、一致する結果が返されます。応答で `moreResult=true` のパラメーターと `nextPageToken` が返される場合、クエリを正しく実行するには、元の入力と `nextPageToken` をすべて含める必要があります。

## 作成と更新

リードデータベースレコードの作成と更新はすべて、JSON 本文を含む POST を通じて実行されます。商談、ロール、カスタムオブジェクト、会社、セールス担当者のインターフェイスはそれぞれ同じです。リードのインターフェイスは少し異なります。詳しくは、こちらを参照してください。

唯一の必要なパラメーターは、最大 300 個のオブジェクトを含む `input` と呼ばれる配列です。各オブジェクトには、メンバーとして挿入／更新するフィールドが含まれます。オプションで、`createOnly`、`updateOnly`、`createOrUpdate` のいずれかの `action` パラメーターを含めることもできます。アクションを省略すると、モードはデフォルトで `createOrUpdate` になります。`dedupeBy` は、アクションが createOnly または `createOrUpdate` に設定されている場合に使用できる別のオプションパラメーターです。` dedupeBy` は、`idField` または `dedupeFields` のいずれかに指定できます。`idField` を選択した場合、説明にリストされている `idField` が重複排除に使用され、各レコードに含める必要があります。`idField` モードは、`createOnly` モードと互換性がありません。`dedupeFields` を選択した場合、オブジェクトの説明にリストされている `dedupeFields` が使用され、各レコードにそれぞれ含める必要があります。`dedupeBy` パラメーターを省略すると、モードはデフォルトで `dedupeFields` になります。

フィールド値のリストを渡すと、`null` 値または空の文字列が `null` としてデータベースに書き込まれます。

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

リード API 以外で、リードデータベースオブジェクトを作成または更新する呼び出しでは、`result` 配列内の各オブジェクトの `seq` フィールドが返されます。リストされる番号は、リクエスト内で更新されたレコードの順序に対応します。各項目は、オブジェクトタイプの `idField` の値と `status` を返します。ステータスフィールドは、「作成済み」、「更新済み」または「スキップ済み」のいずれかを示します。ステータスがスキップされた場合、レコードがスキップされた理由を示すコードとメッセージを含む 1 つ以上の理由オブジェクトを含む対応する「reasons」配列も存在します。詳しくは、[エラーコード](error-codes.md)を参照してください。

### 削除

削除のインターフェイスは、リード以外のリードデータベースオブジェクトに対しては標準です。入力以外には、idField または dedupeFields の値を持つことができる必須パラメーター `deleteBy,` が 1 つだけあります。いくつかのカスタムオブジェクトの削除を見てみましょう。

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

`seq`、`status`、`marketoGUID`、`reasons` はすべて、今ではよくご存知のはずです。

それぞれのオブジェクトタイプに対する CRUD 操作について詳しくは、それぞれのページを参照してください。
