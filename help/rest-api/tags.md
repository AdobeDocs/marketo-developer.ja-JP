---
title: タグ
feature: REST API, Tags
description: タグタイプのクエリ、名前による許可される値の取得、REST Asset APIを介したMarketoのプログラムタグの更新または削除などを、リクエストサンプルを交えて実行できます。
exl-id: 64731d1a-a749-4d6f-b336-16c733d002f0
TQID: 'https://experienceleague.adobe.com/zjdyfoofVWytE0Q-K4lk598jmleTSFOD7tSRqeAHsjk'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
    internal-label: Programs
  - id: dca84292-69e9-4116-a575-667d31fa060d
    internal-label: APIs
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
    internal-label: Administration
subfeature_v2:
  - id: cf1396d8-ab85-4e93-b35d-d9b573024abf
    internal-label: REST APIs
  - id: eabd8318-c438-41ef-8756-bedd6f38b8fc
    internal-label: Tag administration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 5620f050ba834be3f6648650b5cc7d781ea394bf
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 7%
---
# タグ

[タグエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset#tag/Tags)

タグは、プログラムのユーザが定義するフィールドです。 タグは、1つ以上のプログラムタイプに適用でき、必須または任意です。 タグは、ユーザーが選択する必要がある許可される値のリストを定義することもできます。

## クエリ

標準のアセットパターンを使用してタグをクエリします。 タグにはID別エンドポイントがありません。 タグの使用可能な値を取得するには、タグを名前でクエリします。

### タグの取得

```http
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

```http
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

タグ タイプの値を更新するには、[&#x200B; プログラム タグの更新](https://developer.adobe.com/marketo-apis/api/asset#operation/updateProgramUsingPOST) エンドポイントを使用します。 すべてのパラメーターが必要です。

- `id` パス パラメーターは、プログラム IDを指定します。
- `tagType` パス パラメーターは、更新するタグの種類を指定します。
- `tagValue` クエリパラメーターは、新しい値を指定します。

```http
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

複数のタグを更新するには、[&#x200B; プログラムメタデータの更新](https://developer.adobe.com/marketo-apis/api/asset#operation/updateProgramUsingPOST) エンドポイントを使用します。 [&#x200B; プログラム更新セクション &#x200B;](programs.md#update)の例を参照してください。

## 削除

不要なタグタイプを削除するには、[&#x200B; プログラムタグの削除](https://developer.adobe.com/marketo-apis/api/asset#operation/deleteProgramUsingPOST) エンドポイントを使用します。 `id` パス パラメーターはプログラム IDを指定し、`tagType` パス パラメーターは削除するタグ タイプを指定します。

```http
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
