---
title: フォーム
feature: REST API, Forms
description: Marketo Forms REST API ガイド：フォームの作成と管理、IDまたは名前による取得、ステータスフィルターによる参照、フィールド、フィールドセット、ルールの管理に役立ちます。
exl-id: 2e5dfa70-3163-4ab4-b269-3112417714c3
TQID: https://experienceleague.adobe.com/56tc1a14d8okxweS7TK7SzfGB8G03WAI2KBlFKQbSdM
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: a7170d27-32ab-462b-a333-269abc654483id: b0bb9048-d951-48d8-8232-45cf248a7e27id: d65b4a73-87a3-4d56-b638-74e74d9939ceid: e64968b2-4ee5-47f9-8cae-0588f184b9eb
subfeature_v2: id: d0251300-e25f-466f-9856-7e11ce8fa7aa
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1494
ht-degree: 6%

---

# フォーム

[Forms エンドポイントリファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms)

[フォームフィールドエンドポイントリファレンス](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields)

フォームエンドポイントを使用して、リモートシステムからフォームを管理します。 フォームには、複数のオブジェクトタイプを含めることができます。

- フォーム
- フィールド
- Fieldsets
- 表示ルール
- フォローアップページルール

## クエリ

Formsでは、標準のアセット取得方式（[id](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByIdUsingGET)、[名前](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByNameUsingGET)、および[参照](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/browseForms2UsingGET)）がサポートされています。 フォーム応答には、フィールドリストを除くすべてのフォームプロパティが含まれます。

### ID 別

フォーム `id`をパス パラメーターとして[IDでフォームを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByIdUsingGET)に渡します。 エンドポイントは、一致するフォームレコードを返します。

```http
GET /rest/asset/v1/form/{id}.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "948f#154e3bad8e3",
    "result": [
        {
            "id": 736,
            "name": "newForm",
            "description": "test",
            "createdAt": "2016-05-24T17:05:54Z+0000",
            "updatedAt": "2016-05-24T17:05:54Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO736B2",
            "status": "draft",
            "theme": "simple",
            "language": "French",
            "locale": "fr_FR",
            "progressiveProfiling": false,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Envoyer",
            "waitingLabel": "Veuillez patienter"
        }
    ]
}
```

### 名前別

フォーム `name`を渡して[名前でフォームを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByNameUsingGET)します。 エンドポイントは、一致するフォームレコードを返します。

```http
GET /rest/asset/v1/form/byName.json?name=newForm
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "948f#154e3bad8e3",
    "result": [
        {
            "id": 736,
            "name": "newForm",
            "description": "test",
            "createdAt": "2016-05-24T17:05:54Z+0000",
            "updatedAt": "2016-05-24T17:05:54Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO736B2",
            "status": "draft",
            "theme": "simple",
            "language": "French",
            "locale": "fr_FR",
            "progressiveProfiling": false,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Envoyer",
            "waitingLabel": "Veuillez patienter"
        }
    ]
}
```

### 参照

[Get Forms](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/browseForms2UsingGET)は、標準のAsset API参照パターンに従っています。 次のオプションのフィルターをサポートしています。

- `status`: `approved`、`approved with draft`または`draft`でフィルタリングします。
- `maxReturn`：返されるレコードの数を制限します。
- `offset`：結果セットをページ化します。

```http
GET /rest/asset/v1/forms.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "645d#154e3d499ac",
    "result": [
        {
            "id": 227,
            "name": "aKAUVDfbsX",
            "description": "",
            "createdAt": "2016-05-18T20:36:20Z+0000",
            "updatedAt": "2016-05-18T20:36:20Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO227B2",
            "status": "draft",
            "theme": "simple",
            "language": "English",
            "locale": "en_US",
            "progressiveProfiling": false,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Submit",
            "waitingLabel": "Please Wait"
        },
        {
            "id": 695,
            "name": "AoMXgfFbma",
            "description": "",
            "createdAt": "2016-05-19T18:50:40Z+0000",
            "updatedAt": "2016-05-19T18:50:40Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO695B2",
            "status": "draft",
            "theme": "simple",
            "language": "English",
            "locale": "en_US",
            "progressiveProfiling": true,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 565,
                "folderName": "WfUvYmlcyT"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Submit",
            "waitingLabel": "Please Wait"
        }
    ]
}
```

### フィールドリスト

フォーム IDを渡して、各フォームのフィールドリストを個別に取得します。

```http
GET /rest/asset/v1/form/{id}/fields.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "2165#154eee00d01",
    "result": [
        {
            "id": "FirstName",
            "label": "First Name:",
            "dataType": "text",
            "validationMessage": "This field is required.",
            "rowNumber": 0,
            "columnNumber": 0,
            "maxLength": 255,
            "required": false,
            "formPrefill": true,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            }
        },
        {
            "id": "LastName",
            "label": "Last Name:",
            "dataType": "text",
            "validationMessage": "This field is required.",
            "rowNumber": 1,
            "columnNumber": 0,
            "maxLength": 255,
            "required": false,
            "formPrefill": true,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            }
        },
        {
            "id": "Email",
            "label": "Email Address:",
            "dataType": "email",
            "validationMessage": "Must be valid email. <span class='mktoErrorDetail'>example@yourdomain.com</span>",
            "rowNumber": 2,
            "columnNumber": 0,
            "required": false,
            "formPrefill": true,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            }
        },
        {
            "id": "Profiling",
            "dataType": "profiling",
            "rowNumber": 3,
            "columnNumber": 0
        }
    ]
}
```

フィールドを更新または削除したり、その動作を変更したりする前に、フォームのフィールドリストを取得します。 後続のリクエストで返されたフィールド IDを使用します。

### フィールドのタイプ

| UI タイプ | API 名 |
| --- | --- |
| チェックボックス | checkbox |
| ラジオボタン | radio |
| テキストエリア | textarea |
| 選択リスト | picklist |
| 文字列 | string |
| メール | email |
| 日付 | date |
| 数字 | number |
| Double | double |
| 電話 | phone |
| URL | URL |
| 通貨 | currency |
| チェックボックス | single_checkbox |
| スライダ | range |

### 依存関係

フォーム `id`をパス パラメーターとして[使用するフォームを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getFormUsedByUsingGET)に渡します。 エンドポイントは、フォームに依存するアセットを返します。

フォームを使用できるアセットタイプは次のとおりです。

- ランディングページ
- スマートリスト
- スマートキャンペーン
- レポート
- メールプログラム

```http
GET /rest/asset/v1/form/{id}/usedBy.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "fdf4#17285b25038",
    "warnings": [],
    "result": [
        {
            "id": 1038,
            "name": "LP Redirect Rules Program.LP Test 01",
            "type": "Landing Page",
            "status": "approved",
            "updatedAt": "2020-02-23T01:31:21Z+0000"
        }
    ]
}
```

## 作成と更新

[ フォームを作成](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/createLpFormsUsingPOST)するには、次の2つの必須フィールドを指定します。

- フォームの親フォルダー。
- フォーム名。

その他のすべてのパラメーターはオプションで、デフォルト値があります。 新しいフォームには、3つのデフォルト フィールド（名、姓、電子メール）が含まれます。

```http
POST /rest/asset/v1/forms.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=newForm&description=test&folder={"type": "Folder","id": 293}&language=French
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "948f#154e3bad8e3",
    "result": [
        {
            "id": 736,
            "name": "newForm",
            "description": "test",
            "createdAt": "2016-05-24T17:05:54Z+0000",
            "updatedAt": "2016-05-24T17:05:54Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO736B2",
            "status": "draft",
            "theme": "simple",
            "language": "French",
            "locale": "fr_FR",
            "progressiveProfiling": false,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Envoyer",
            "waitingLabel": "Veuillez patienter"
        }
    ]
}
```

[ フォームを更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/updateFormsUsingPOST)するには、そのIDを渡します。 作成または更新時に、フォームの表示方法を制御する基本スタイル設定パラメーターを設定できます。

```http
POST /rest/asset/v1/form/736.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=updated name&description=This is a test for updateapi&language=English&progressiveProfiling=true&locale=en_US
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "6307#154e3cf6efe",
    "result": [
        {
            "id": 736,
            "name": "updated name",
            "description": "This is a test for update api",
            "createdAt": "2016-05-24T17:05:54Z+0000",
            "updatedAt": "2016-05-24T17:28:23Z+0000",
            "status": "draft",
            "theme": "simple",
            "language": "English",
            "locale": "en_US",
            "progressiveProfiling": true,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Submit",
            "waitingLabel": "Please Wait"
        }
    ]
}
```

フォームエンドポイントを作成および更新しても、既知の訪問者やサンキューページの動作は変更されません。 対応するエンドポイントを使用して、これらの動作を管理します。

## フィールドメタデータ

フォームフィールドを追加または編集する前に、ターゲットインスタンスの有効なフィールドを取得します。 フィールド操作では、各フィールドに対して返される`id` プロパティを使用します。

リードフィールドの場合は、[使用可能なフォームフィールドを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/getAllFieldsUsingGET) エンドポイントを使用します。 応答には、各フィールドのデータタイプと、フィールドがフォームに追加されたときに適用されるデフォルトのメタデータが含まれます。

```http
GET /rest/asset/v1/form/fields.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "176ca#167a9808f4c",
    "warnings": [],
    "result": [
        {
            "id": "AnnualRevenue",
            "isRequired": false,
            "dataType": "currency"
        },
        {
            "id": "City",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Company",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Country",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Description",
            "isRequired": false,
            "dataType": "textarea",
            "maxLength": 32000,
            "visibleRows": 2
        },
        {
            "id": "Email",
            "isRequired": false,
            "dataType": "email"
        },
        {
            "id": "Fax",
            "isRequired": false,
            "dataType": "phone"
        },
        {
            "id": "FirstName",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Industry",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "LastName",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "LeadSource",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "MobilePhone",
            "isRequired": false,
            "dataType": "phone"
        },
        {
            "id": "NumberOfEmployees",
            "isRequired": false,
            "dataType": "int"
        },
        {
            "id": "Phone",
            "isRequired": false,
            "dataType": "phone"
        },
        {
            "id": "PostalCode",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Rating",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Salutation",
            "isRequired": false,
            "dataType": "picklist",
            "picklistValues": "Mr.,Ms.,Mrs.,Dr.,Prof."
        },
        {
            "id": "State",
            "isRequired": false,
            "dataType": "picklist",
            "picklistValues": "AK::AK,AL::AL,AR::AR,AZ::AZ,CA::CA,CO::CO,CT::CT,DE::DE,FL::FL,GA::GA,HI::HI,IA::IA,ID::ID,IL::IL,IN::IN,KS::KS,KY::KY,LA::LA,MA::MA,MD::MD,ME::ME,MI::MI,MN::MN,MO::MO,MS::MS,MT::MT,NC::NC,ND::ND,NE::NE,NH::NH,NJ::NJ,NM::NM,NV::NV,NY::NY,OH::OH,OK::OK,OR::OR,PA::PA,RI::RI,SC::SC,SD::SD,TN::TN,TX::TX,UT::UT,VA::VA,VT::VT,WA::WA,WI::WI,WV::WV,WY::WY"
        },
        {
            "id": "Street",
            "isRequired": false,
            "dataType": "textarea",
            "maxLength": 2000,
            "visibleRows": 2
        },
        {
            "id": "Title",
            "isRequired": false,
            "dataType": "picklist"
        }
    ]
}
```

プログラムメンバーのカスタムフィールドの場合は、[利用可能なフォームプログラムメンバーフィールドを取得](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/getAllProgramMemberFieldsUsingGET) エンドポイントを呼び出します。 応答には、プログラムメンバーカスタムフィールドデータタイプとデフォルトメタデータが含まれます。

これらのフィールドを使用するには、フォームがDesign Studioではなくプログラムの下にある必要があります。 これらのフィールドを含むフォームを含むランディングページも、プログラムの下にある必要があります。 Design Studio内で作成したり、Design Studioに複製したりすることはできません。

```http
GET /rest/asset/v1/form/programMemberFields.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "109c6#16fa0b9c51a",
    "warnings": [],
    "result": [
        {
            "id": "pMCFCustomField01",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "pMCFCustomField02",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "myPMCF",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        }
    ]
}
```

### フィールドの編集

各フォームには、フォームの読み込み時にユーザーに表示される編集可能なフィールドのリストがあります。 対応するエンドポイントを使用して、一度に1つのフィールドを追加、更新または削除します。

[ フィールド ](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/addFieldToAFormUsingPOST)を追加するには、親フォーム IDとフィールド `fieldId`を指定します。 その他のすべてのプロパティは空であるか、フィールドのデータタイプとメタデータに基づいてデフォルトを使用します。

データをJSONではなく`application/x-www-form-urlencoded`を使用したPOSTとして送信します。

```http
POST /rest/asset/v1/form/{id}/fields.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
fieldId=NumberOfEmployees&maxLength=125&defaultValue=this is default&required=true&fieldWidth=100&validationMessage=hey, you there?&label=employee count&hintText=Hint me&minValue=10
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "1826e#154f41b214c",
    "result": [
        {
            "id": "NumberOfEmployees",
            "label": "employee count",
            "fieldWidth": 100,
            "dataType": "number",
            "defaultValue": "this is default",
            "validationMessage": "hey, you there?",
            "rowNumber": 5,
            "columnNumber": 0,
            "required": true,
            "formPrefill": true,
            "fieldMetaData": {
                "minValue": 10,
                "maxValue": null
            },
            "visibilityRules": {
                "ruleType": "alwaysShow"
            },
            "hintText": "Hint me"
        }
    ]
}
```

更新プログラムは、フィールドの追加時に使用するのと同じプロパティを編集できます。 また、フォーム IDと`fieldId`が必要ですが、更新エンドポイントは`fieldId`をクエリパラメーターではなくパスパラメーターとして渡します。

```http
POST /rest/asset/v1/form/{id}/field/LastName.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
label=enter the last name here
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "5634#15508303abb",
    "result": [
        {
            "id": "LastName",
            "label": "enter the last name here",
            "dataType": "text",
            "validationMessage": "This field is required.",
            "rowNumber": 0,
            "columnNumber": 0,
            "maxLength": 255,
            "required": false,
            "formPrefill": true,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            }
        }
    ]
}
```

前の例では、単純な文字列フィールドである`LastName`を更新しています。 その他のフォームフィールドには、より複雑なメタデータがあります。 例えば、`Salutation`は、項目のリストとデフォルト値を持つ`select` フィールドです。

選択フィールドを追加または更新する際に、1つの選択肢の`isDefault`値を`true`に設定します。 それ以外の場合、最初の選択肢には値がなく、`Select...`というラベルが付けられます。

![敬称](assets/form-field-salutation.png)

リスト項目を更新するには、次の例に示すように`values` パラメーターを書式設定します。

```http
POST /rest/asset/v1/form/{id}/field/Salutation.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```sql
values=[{"label":"Select...","value":"","isDefault":true,"selected":true}, {"label":"MR","value":"MR"}, {"label":"MS","value":"MS"}, {"label":"MRS","value":"MRS"}, {"label":"DR","value":"DR"}, {"label":"PROF","value":"PROF"}]
```

```json
{
  "success": true,
  "warnings": [ ],
  "errors": [ ],
  "requestId": "71fd#1588d9d1b0c",
  "result": [
    {
      "id": "Salutation",
      "label": "Salutation:",
      "dataType": "select",
      "validationMessage": "This field is required.",
      "rowNumber": 3,
      "columnNumber": 0,
      "required": false,
      "formPrefill": true,
      "fieldMetaData": {
        "multiSelect": false,
        "values": [
          {
            "label": "Select...",
            "value": "",
            "isDefault": true,
            "selected": true
          },
          {
            "label": "MR",
            "value": "MR"
          },
          {
            "label": "MS",
            "value": "MS"
          },
          {
            "label": "MRS",
            "value": "MRS"
          },
          {
            "label": "DR",
            "value": "DR"
          },
          {
            "label": "PROF",
            "value": "PROF"
          }
        ],
        "visibleLines": 1
      },
      "visibilityRules": {
        "ruleType": "alwaysShow"
      }
    }
  ]
}
```

複雑なフォームフィールドの書式設定方法を決定するには、「フォームにフィールドを追加」応答を使用します。

### フィールドの並べ替え

[ フォームフィールドの位置を変更](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/updateFieldPositionsUsingPOST) エンドポイントを使用して、すべてのフォームフィールドを1つの単位として並べ替えます。 エンドポイントには、次の3つのメンバーを持つオブジェクトのJSON配列である`positions`が必要です。

- `columnNumber`
- `rowNumber`
- `fieldName`。フィールド IDを参照します

フォームフィールドでは、最大3列10行の表のような配置を使用できます。 行と列のインデックスは0から始まるので、最初の行と列の両方で0を使用します。 すべてのフィールドは一意の位置を占める必要があります。

ターゲットフィールドがフィールドセットの場合、`positions`のレコードにも`fieldList`が含まれている必要があります。 このパラメーターは、同じ`columnNumber`、`rowNumber`、`fieldName`のメンバーを持つオブジェクトの配列です。

親リストは、フィールドセットを1つのフィールドとして扱います。 `fieldList`の位置によって、子フィールドの配置が決まります。

```http
POST /rest/asset/v1/form/{id}/reArrange.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
positions=[{"columnNumber":0,"rowNumber":0,"fieldName":"FirstName"},{"columnNumber":0,"rowNumber":1,"fieldName":"LastName"}, {"columnNumber":0,"rowNumber":2, "fieldName":"Email"}]
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "bb18#15508ef9c04",
    "result": [
        {
            "id": 764
        }
    ]
}
```

### リッチテキスト

[個別のエンドポイント ](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/addRichTextFieldUsingPOST)を使用して、リッチテキストフィールドを追加します。 `multipart/form-data` リクエストでコンテンツをHTMLとして渡します。 HTMLには、スクリプト、メタタグまたはリンクタグを含めることはできません。

```http
POST /rest/asset/v1/form/{id}/richText.json
```

```html
Content-Type: multipart/form-data; boundary=---------------------------9051914041544843365972754266
-----------------------------9051914041544843365972754266
Content-Disposition: form-data; name="text"
Content-Type: text/html
<div>Fancy Rich Text Component</div>
-----------------------------9051914041544843365972754266--
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "82c8#154f423bf5c",
    "result": [
        {
            "id": "SHRtbFRleHRfMjAxNi0wNS0yN1QxNDozNDoyNC4xMTVa",
            "labelWidth": 260,
            "dataType": "htmltext",
            "rowNumber": 8,
            "columnNumber": 0,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            },
            "text": "<div>Fancy Rich Text Component</div>"
        }
    ]
}
```

### フィールドセット

フィールドセットは、オプションのフィールドグループです。 トップレベルのフィールドリストでは、フィールドセットはポジショニングルールと表示ルール用の1つのフィールドとして扱われます。 例えば、「コンプライアンス要件」フィールドで「はい」を選択すると、HIPAAおよびPCI コンプライアンスのフィールドを含むフィールドセットを表示できます。

フィールドはフォーム内で一意である必要があります。 フォームの親フィールドリストと子フィールドセットの両方に同じフィールドを表示することはできません。

[Add Fieldset to Form](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/addFieldSetUsingPOST) エンドポイントを使用してフィールドセットを追加します。 次に、フィールドセットがフォーム ](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/getFormFieldByFormVidUsingGET)の応答の[ フィールドを取得に表示されます。 フィールドセットにフィールドを追加するには、[ フィールド位置の更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/updateFieldPositionsUsingPOST)を使用して、フィールドを`fieldList`に移動します。

これらのエンドポイントの場合は、JSONではなく`application/x-www-form-urlencoded`を使用してPOSTとしてデータを送信します。

## 表示ルール

表示ルールは、フォームに入力された値に基づいて、訪問者がフィールドを表示できるかどうかを決定します。 各ルールは、フォーム内の`subjectField`の値とルール内の値のリストを比較します。

フィールドには、1つの表示ルールタイプ（`show`、`hide`、または`alwaysShow`）を指定できます。 APIは、フィールドのルールを上から下に評価し、最初のルールをtrueに評価して適用します。

表示ルールの変更は、破壊的な更新です。

```http
POST /rest/asset/v1/form/{id}/field/Email/visibility.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
visibilityRule={"ruleType":"show", "rules":[{"subjectField": "LastName", "operator": "isNotEmpty", "values": [], "altLabel": "Email:"}]}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "ab4a#15509030601",
    "result": [
        {
            "formFieldId": "Email",
            "ruleType": "show",
            "rules": [
                {
                    "subjectField": "LastName",
                    "operator": "isNotEmpty",
                    "values": [],
                    "altLabel": "Email:"
                }
            ]
        }
    ]
}
```

演算子の完全なリストについては、[ フォームフィールドの表示ルールの追加](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/addFormFieldVisibilityRuleUsingPOST)を参照してください。

## フォローアップ

動的なフォローアップルールにより、送信時に指定されたフィールド値にもとづいて、訪問者をページにリダイレクトしたり、現在のページに維持したりできます。 サンキューページルールとフォローアップページルールは、同じ動作を参照します。

ルールを、`followupType`、`followupValue`、`operator`、`subjectField`、`values`および`default`を含むレコードを持つJSON配列として表します。 配列内の1つのレコードのみが、ブール値`default`を`true`に設定できます。 フォームは、訪問者が別のルールに適格でない場合に、そのレコードを使用します。

`followupType`の値は`lp`または`url`です。 `lp`値は、`followupValue`がMarketo ランディングページ IDであることを示します。 `url`値は、`followupValue`が別のページのURLであることを示します。 オペレーターは、件名フィールドの値と指定された値を比較します。

## 送信ボタン

送信ボタンのスタイル設定を変更するには、[送信ボタンを更新](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/updateFormSubmitButtonUsingPOST) エンドポイントを使用します。 `buttonPosition`、`buttonStyle`、`label`および`waitingLabel`を更新できます。 送信が保留中の間、`waitingLabel`が表示されます。

これは破壊的な更新です。

## 承認

Formsは、ドラフト承認済みのライフサイクルに従います。 フォームには、ドラフトバージョン、承認済みバージョン、またはその両方を含めることができます。 更新は常にドラフトに適用され、承認後にのみ公開されます。

フォームを承認すると、既存の承認済みバージョンがある場合は、現在のドラフトに置き換えられます。 ライブフォームの承認を解除すると、現在のドラフトが削除され、承認されたバージョンはドラフトのみの状態に格下げされます。 フォームを削除する前に、必ず承認を取り消してください。

## プログレッシブプロファイリング

プログレッシブプロファイリングが有効になっている場合、フォームフィールドリストには`Profiling`という名前のフィールドセットが含まれます。 「フィールド位置を更新」エンドポイントを使用して、プログレッシブプロファイルリストからフィールドを追加または削除します。

このエンドポイントは破壊的な更新を実行するので、すべてのリクエストにはフォームのすべてのフィールドを含める必要があります。 次の例では、プログレッシブプロファイリングリストに`Phone`を追加します。

```http
POST /rest/asset/v1/form/{id}/reArrange.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
positions=[{"columnNumber":0,"rowNumber":0,"fieldName":"Email"},{"columnNumber":0,"rowNumber":1,"fieldName":"LastName"},{"columnNumber":0,"rowNumber":2,"fieldName":"Company"},{"columnNumber":0,"rowNumber":3,"fieldName":"Website"},{"columnNumber":0,"rowNumber":4,"fieldName":"Profiling","fieldList":[{"columnNumber":0,"rowNumber":0,"fieldName":"Phone"}]}]
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "3d6a#164190dbdf2",
    "result": [
        {
            "id": 1031
        }
    ]
}
```
