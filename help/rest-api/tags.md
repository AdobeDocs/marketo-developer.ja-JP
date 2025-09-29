---
title: タグ
feature: REST API, Tags
description: タグのタイプをクエリし、名前で許容値を取得し、REST Asset API を使用してMarketoのプログラムタグを更新または削除し、リクエスト例を示します。
exl-id: 64731d1a-a749-4d6f-b336-16c733d002f0
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 90%

---

# タグ

[タグエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tags)

タグは、プログラムのユーザ定義フィールドです。各タグは、1 つ以上のプログラムタイプに適用され、タグの定義方法に応じて必須またはオプションになります。また、タグは、使用時に選択する必要がある許容値のリストを提供する場合もあります。

## クエリ

タグは、標準のアセットパターンでクエリが実行されますが、ID 別のエンドポイントはありません。タグの許容値のリストは、タグに対して名前でクエリを実行した場合にのみ返されます。

### タグの取得

```
GET /rest/asset/v1/tagTypes.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "1488a#1504ecfccf8",
    "result": [
        {
            "tagType": "AAA1 Required Tag Type",
            "applicableProgramTypes": "[program,email_batch,nurture,event,webinar]",
            "required": true
        },
        {
            "tagType": "AAA2 Required Event Tag Type",
            "applicableProgramTypes": "[event]",
            "required": true
        },
        {
            "tagType": "AAA3 Not Required Tag Type",
            "applicableProgramTypes": "[program,email_batch,nurture,event,webinar]",
            "required": false
        }
    ]
}
```

### 名前別

```
GET /rest/asset/v1/tagType/byName.json?name=AAA1 Required Tag Type
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "8a44#1504ed0da2f",
    "result": [
        {
            "tagType": "AAA1 Required Tag Type",
            "applicableProgramTypes": "[program,email_batch,nurture,event,webinar]",
            "required": true,
            "allowableValues": "[AAA1 RT1, AAA1 RT2, AAA1 RT3, AAA1 RT4]"
        }
    ]
}
```

## 更新

[プログラムタグを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/updateProgramUsingPOST)エンドポイントを使用すると、特定のタグタイプの値を更新できます。エンドポイントは、プログラム ID と更新するタグタイプを指定する `id` および `tagType` パスパラメーターを受け取ります。`tagValue` クエリパラメーターは、タグタイプの新しい値を指定するのに使用されます。すべてのパラメーターは必須です。

```
POST /rest/asset/v1/program/{id}/tag/{tagType}.json?tagValue=David
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "fd84#17f84a885a6",
    "warnings": [],
    "result": [
        {
            "id": 1067
        }
    ]
}
```

[プログラムメタデータを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/updateProgramUsingPOST)エンドポイントを使用して、タグを一括更新できます。その例について詳しくは、[こちら](programs.md#update)を参照してください。

## 削除

[プログラムタグを削除](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/deleteProgramUsingPOST)エンドポイントを使用すると、不要なタグタイプを削除できます。エンドポイントは、プログラム ID と削除するタグタイプを指定する `id` および `tagType` パスパラメーターを受け取ります。

```
POST /rest/asset/v1/program/{id}/tag/{tagType}/delete.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "d998#17f84ad36a7",
    "warnings": [],
    "result": [
        {
            "id": 1067
        }
    ]
}
```
