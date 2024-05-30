---
title: 「Forms」
feature: REST API, Forms
description: "API を使用したフォームの作成と管理。"
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '1598'
ht-degree: 2%

---


# フォーム

[Forms エンドポイントのリファレンス](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms)

[フォームフィールドエンドポイントのリファレンス](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields)

Marketo forms にはエンドポイントの複雑なセットがあり、リモートシステムからフォームを完全に管理できます。 フォームの一部として管理する必要のあるオブジェクトには様々なタイプ（Forms、フィールド、フィールドセット、表示ルール、フォローアップページルール）があるので、フォームの構造は複雑になる場合があります。

## クエリ

Formsでは、アセットを取得する標準的な方法をサポートしています。 [id 別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByIdUsingGET), [名前別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET)、および [ブラウジングによる](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/browseForms2UsingGET). 各フォーム応答には、フィールドリストを除くすべてのプロパティが含まれます。

### ID 別

[Id でフォームを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByIdUsingGET) フォームを作成 `id` パスパラメーターとして指定し、フォームレコードを返します。

```
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

[名前によるフォームの取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET) フォームを作成 `name` パスパラメーターとして指定し、フォームレコードを返します。

```
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

[Formsの取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/browseForms2UsingGET) フォームは他の Asset API 参照エンドポイントと同様に機能し、以下に対してオプションのフィルタリングを可能にします `status`, `maxReturn`、および `offset`. ステータスは、承認済み、ドラフトで承認済み、ドラフトのいずれかです。

```
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

フォームのフィールドリストの取得は、フォームごとに行われます。

```
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

フィールドまたはフォーム内でのフィールドの動作を編集する場合は、編集を試みる前に、必ずフィールドリストを取得する必要があります。 これにより、更新や削除の際に、適切なフィールド ID が確実に付与されます。

### フィールドのタイプ

| UI タイプ | API 名 |
|--------------|-----------------|
| 複数選択チェックボックス | チェックボックス |
| ラジオボタン | ラジオ |
| テキストエリア | テキストエリア |
| 選択リスト | 選択リスト |
| 文字列 | 文字列 |
| メール | メール |
| 日付 | 日 |
| 数字 | number |
| 二重 | 二重線 |
| 電話 | 電話 |
| URL | URL |
| 通貨 | currency |
| チェックボックス | single_checkbox |
| スライダ | 範囲 |


### 依存関係

この [フォームの取得者](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getFormUsedByUsingGET) エンドポイントのフォーム `id` をパスパラメーターとして使用し、フォームに依存するアセットのリストを返します。 Formsは、ランディングページ、スマートリスト、スマートキャンペーン、レポート、メールプログラムのアセットタイプで使用できます。

```
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

条件 [フォームの作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/createLpFormsUsingPOST) 必須フィールドは 2 つだけです。フォームの親フォルダー、フォームの名前です。 その他のパラメーターはすべてオプションで、デフォルト値を使用します。 フォームを作成すると、名、姓、メールの 3 つのデフォルトフィールドが表示されます。

```
POST /rest/asset/v1/forms.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

Forms: [更新日](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/updateFormsUsingPOST) id を介して同様の呼び出しを持つ。 作成時または更新時に、任意の基本スタイルパラメーターにアクセスして編集できるので、エンドユーザーに対するフォームの表示方法を変更できます。

```
POST /rest/asset/v1/form/736.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

既知の訪問者ページやありがとうページの動作は、作成または更新フォーム呼び出しを使用して変更することはできず、それぞれのエンドポイントを使用してアクセスする必要があります。

## フィールドメタデータ

フォームに属するフィールドを適切に追加または編集するには、ターゲットインスタンスの有効なフィールドのリストを取得する必要があります。 フィールドのインタラクションは、常にフィールドの id プロパティに基づいて行われます。このプロパティは、結果に項目ごとに表示されます。

リードフィールドの場合は、を使用して行います。 [使用可能なフォームフィールドを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/getAllFieldsUsingGET) のエンドポイントであり、フォームに追加された際にフィールドのデータタイプとデフォルトのメタデータを含みます。

```
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

プログラムメンバーカスタムフィールドの場合は、を呼び出します [利用可能なフォームプログラムメンバーフィールドを取得する](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/getAllProgramMemberFieldsUsingGET)  プログラムメンバーのカスタムフィールドのデータタイプとデフォルトのメタデータを取得するエンドポイント。 これらのフィールドをフォームで使用するには、フォームが（Design Studio ではなく）プログラムの下にある必要があります。 これらのフィールドを使用するフォームを含むランディングページも、プログラムの下に存在する必要があります（Design Studio 内に存在したり、Design Studio に複製したりすることはできません）。

```
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

各フォームには、読み込み時にエンドユーザーに表示される、編集可能なフィールドのリストが含まれています。 各フィールドは、フィールドリストから各エンドポイントを介して一度に 1 つずつ追加、更新または削除されます。

[フィールドの追加](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addFieldToAFormUsingPOST) 親フォームの ID とフィールドの fieldId のみが必要です。 その他のフィールドはすべて、データタイプとフィールドメタデータに基づいて、空になるか、デフォルト値になります。 データは、JSON としてではなく、POST x-www-form-urlencoded として渡されます。

```
POST /rest/asset/v1/form/{id}/fields.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

アップデートは、フィールドの追加と同じフィールドをすべて編集する可能性があります。同様に、fieldId がパスパラメーターで、アップデートを実行する際にクエリパラメーターではないことを除き、フォーム ID と fieldId が必要です。

```
POST /rest/asset/v1/form/{id}/field/LastName.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

上記の例では、単純な文字列である LastName フィールドを更新しています。 一部のフォームフィールドはより複雑です。 例えば、「敬称」フィールドは、項目のリストとデフォルト値を含む「選択」フィールドタイプです。 タイプを選択フィールドを追加または更新する場合。ただし、選択肢の 1 つに `isDefault` 値が true の場合、最初の選択肢に値がなく、「選択」というラベルが付きます。

![敬称](assets/form-field-salutation.png)

リスト項目を更新するには、「values」パラメーターの形式を次に示します。

```
POST /rest/asset/v1/form/{id}/field/Salutation.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

 

複雑なフォームフィールドの書式設定方法を決定するには、「フィールドをフォームに追加」からの応答を確認してください。

### 並べ替えフィールド

フォーム内のフィールドは、 [フォームフィールドの位置の変更](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/updateFieldPositionsUsingPOST) エンドポイント。 エンドポイントにはというパラメーターが必要です `positions`は、次の 3 つのメンバーを持つオブジェクトの JSON 配列です。

- columnNumber
- rowNumber
- fieldName （フィールドの ID を指します）

フォーム内のフィールドは、最大 3 列、最大 10 行のテーブル状のインターフェイスで配置されます。 行と列の両方に 0 からインデックスが付けられるので、最初の行と最初の列は両方とも 0 を渡すことで示されます。 すべてのフィールドが一意の位置を占める必要があります

ターゲットフィールドが fieldset である場合は、positions 配列内のレコードにも fieldList というパラメーター（同じ columnNumber、rowNumber、および fieldName メンバーを含むオブジェクトの配列）が含まれている必要があります。 フィールドセット自体は、親リスト内の位置に対して単一のフィールドとして扱われますが、サブフィールドは fieldList パラメーターの指定された位置に従って配置されます。

```
POST /rest/asset/v1/form/{id}/reArrange.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

リッチテキストフィールドは、 [個別のエンドポイント](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addRichTextFieldUsingPOST) リードフィールドから。 フィールドコンテンツは、multipart/form-data として渡されます。 スクリプト、メタタグまたはリンクタグを含まないHTMLコンテンツとして構造化する必要があります。

```
POST /rest/asset/v1/form/{id}/richText.json
```

```
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

Marketo forms には、fieldsets というオプションのコンポーネントがあります。 フィールドセットは、表示ルールによる移動や処理の目的で、最上位のフィールドリスト内の単一のフィールドとして扱われるフィールドのグループです。 例えば、コンプライアンス要件のフィールドがあり、クライアントが「はい」を選択した場合、HIPAA および PCI のコンプライアンス要件のフィールドを含むフィールドセットが表示される場合があります。

フィールドセット内のフィールドは、フォーム全体に固有なので、重複したフィールドは、フォームの親フィールドリストと子フィールドセットの両方に存在しない場合があります。 フィールドセットは、 [フォームにフィールドセットを追加](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addFieldSetUsingPOST) エンドポイントであり、の結果に表示されます。 [フォームのフィールドの取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/getFormFieldByFormVidUsingGET). フィールドは、次の方法でフィールドセットの fieldList に移動することで、フィールドセットに追加されます。 [フィールド位置の更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/updateFieldPositionsUsingPOST). これらのエンドポイントの場合、データは JSON ではなく、POST x-www-form-urlencoded として渡されます。

## 表示ルール

各フィールドには、フォームに入力した値に応じて訪問者がフィールドを表示できるかどうかを決定する、一連の表示ルールを含めることができます。 ルールは、フォーム内に存在する subjectField の値と、ルールで指定された値のリストを比較します。 各フィールドには、表示ルール、表示、非表示、または alwaysShow の 1 つのタイプと、評価するルールのリストが含まれる場合があります。 ルールは上から下のように評価され、true と評価される最初のルールが適用されるルールです。

表示ルールの変更は、破壊的な更新です。

```
POST /rest/asset/v1/form/{id}/field/Email/visibility.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

使用可能な演算子の完全なリストについては、のエンドポイント参照ページを参照してください [フォームフィールド表示ルールの追加](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addFormFieldVisibilityRuleUsingPOST).

## フォローアップ

Marketo forms には、特定のページにリダイレクトするルールや現在のページに留まるルールが、送信時に指定されたフィールドの内容に基づいて適用される、動的なフォローアップページの動作が含まれる場合があります。 ルールは、「ありがとうございます」ページルールまたはフォローアップページルールと同義に呼ばれます。 これらのルールは、メンバーを含む JSON 配列として表されます `followupType`, `followupValue`, `operator`, `subjectField`, `values`、および `default`. `default` は、配列内の 1 つのレコードのみが true になるブール値です。 訪問者がその他のルールの対象とならない場合は、デフォルトとして指定されたルールが使用されます。 `followupType` lp または url。lp はのMarketo ランディングページ ID を示します。 `followupValue`、および url は別のページへの URL を示します。 演算子は、件名フィールドの値を指定された値のリストと比較するために使用されます。

## 送信ボタン

フォームの送信ボタンのスタイル設定は、で管理されます。 [送信ボタンを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/updateFormSubmitButtonUsingPOST) エンドポイント。 buttonPosition、buttonStyle、label、および waitingLabel （送信が保留中の間に表示されるラベル）は変更できます。

これは破壊的な更新です。

## 承認

他のほとんどのアセットと同様に、フォームはドラフト承認済みモデルに従います。ドラフトバージョンや承認済みバージョンを使用できます。 フォームに更新が適用されるたびに、常に最初にドラフトバージョンに適用され、フォームが承認されたときにのみライブで表示されます。 フォームを承認すると、現在のドラフトバージョンが取得され、承認済みのバージョンがある場合は、そのバージョンがドラフトに置き換えられます。 フォームをライブから削除する必要がある場合は、まず未承認にする必要があります。これにより、現在のドラフトがすべて削除され、承認済みバージョンがドラフトのみの状態に降格されます。 Formsを削除する前に、常に承認を取り消す必要があります。

## プログレッシブ プロファイリング

フォームに対してプログレッシブプロファイルが有効になっている場合、「プロファイル」というフィールドセットがフィールドリストに含まれます。 プログレッシブプロファイルリストにフィールドを追加または削除するには、「フィールド位置を更新」エンドポイントを使用する必要があります。 このエンドポイントは、破壊的な更新を行うので、フォーム内のすべてのフィールドを各リクエストに含める必要があります。 次の例では、「Phone」フィールドをプログレッシブプロファイルリストに追加します。

```
POST /rest/asset/v1/form/{id}/reArrange.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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
