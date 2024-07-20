---
title: タグ
feature: REST API, Tags
description: Marketoでプログラムのタグを管理します。
exl-id: 64731d1a-a749-4d6f-b336-16c733d002f0
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 2%

---

# タグ

[ タグエンドポイントのリファレンス ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tags)

タグは、プログラムに対してユーザーが定義したフィールドです。 各タグは、1 つ以上のプログラムタイプに適用でき、タグの定義方法に応じて、必須またはオプションのいずれかになります。 タグは、使用するためにから選択する必要がある許容値のリストを提供することもできます。

## クエリ

タグは標準のアセットパターンでクエリされますが、「ID 別」のエンドポイントはありません。 タグに使用できる値のリストは、タグが名前でクエリされる場合にのみ返されます。

### タグを取得

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

[ プログラムタグを更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/updateProgramUsingPOST) エンドポイントを使用すると、特定のタグタイプの値を更新できます。 エンドポイントは、プログラム ID と更新するタグタイプを指定する `id` および `tagType` パスパラメーターを受け取ります。 `tagValue` クエリパラメーターを使用して、タグタイプの新しい値を指定します。 すべてのパラメーターが必要です。

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

タグは、「[ プログラムメタデータを更新 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/updateProgramUsingPOST) エンドポイントを使用して一括で更新できます。 その例については、[ こちら ](programs.md#update) を参照してください。

## 削除

[ プログラムタグを削除 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/deleteProgramUsingPOST) エンドポイントを使用すると、不要なタグタイプを削除できます。 エンドポイントは、プログラム ID と削除するタグタイプを指定する `id` および `tagType` パスパラメーターを受け取ります。

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
