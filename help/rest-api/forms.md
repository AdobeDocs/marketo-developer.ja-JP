---
title: フォーム
feature: REST API, Forms
description: API を通じてフォームを作成および管理します。
exl-id: 2e5dfa70-3163-4ab4-b269-3112417714c3
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '1598'
ht-degree: 100%

---

# フォーム

[フォームエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms)

[フォームフィールドエンドポイント参照](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields)

Marketo フォームには、エンドポイントの複雑なセットがあり、リモートシステムからフォーム管理を完全に制御できます。フォームの一部として管理する必要があるオブジェクトのタイプには、フォーム、フィールド、フィールドセット、表示ルール、フォローアップページルールなど、様々なタイプがあるので、フォームの構造は複雑になる場合があります。

## クエリ

フォームは、[ID 別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByIdUsingGET)、[名前別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET)、[参照別](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/browseForms2UsingGET)でのアセット取得の標準的な方法をサポートしています。各フォーム応答には、フィールドリストを除くすべてのプロパティが含まれます。

### ID 別

[ID によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByIdUsingGET)では、フォーム `id` をパスパラメーターして受け取り、フォームレコードを返します。

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

[名前によるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET)では、フォーム `name` をパスパラメーターとして受け取り、フォームレコードを返します。

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

[フォームを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/browseForms2UsingGET)フォームでは、他の Asset API 参照エンドポイントと同様に機能し、`status`、`maxReturn`、`offset` でのオプションのフィルタリングが可能です。ステータスは、承認済み、ドラフトで承認済み、ドラフトのいずれかになります。

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

フィールドを編集する場合や、フォーム内でのフィールドの動作を編集する場合は、編集を試みる前に常にフィールドリストを取得する必要があります。これにより、更新や削除の際に、適切なフィールド ID が付与されます。

### フィールドのタイプ

| UI タイプ | API 名 |
|--------------|-----------------|
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

[使用されるフォームを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getFormUsedByUsingGET)エンドポイントでは、フォーム `id` をパスパラメーターとして受け取り、フォームに依存するアセットのリストを返します。フォームは、ランディングページ、スマートリスト、スマートキャンペーン、レポート、メールプログラムなどのアセットタイプで使用できます。

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

[フォームの作成](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/createLpFormsUsingPOST)時に必要なフィールドは、フォームの親フォルダーとフォーム名の 2 つだけです。その他のパラメーターはすべてオプションで、デフォルト値が設定されます。フォームを作成すると、名、姓、メールの 3 つのデフォルトフィールドが追加されます。

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

フォームは、ID を通じた同様の呼び出しで[更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/updateFormsUsingPOST)されます。作成中または更新中は、基本スタイル設定パラメーターのいずれかにアクセスして編集できるので、エンドユーザへのフォームの表示方法を変更できます。

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

既知の訪問者およびサンキューページの動作は、作成フォームや更新フォームの呼び出しを通じて変更できず、それぞれのエンドポイント経由でアクセスする必要があります。

## フィールドメタデータ

フォームに属するフィールドを適切に追加または編集するには、ターゲットインスタンスの有効なフィールドのリストを取得する必要があります。フィールドのインタラクションは常に、結果の各項目に表示されるフィールドの id プロパティに基づいて行われます。

リードフィールドの場合、これは[使用可能なフォームフィールドを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/getAllFieldsUsingGET)エンドポイントを使用して実行され、フォームに追加した際のフィールドのデータタイプとデフォルトのメタデータが含まれます。

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

プログラムメンバーのカスタムフィールドの場合は、[使用可能なフォームプログラムメンバーフィールドを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/getAllProgramMemberFieldsUsingGET)エンドポイントを呼び出して、プログラムメンバーのカスタムフィールドのデータタイプとデフォルトのメタデータを取得します。フォームでこれらのフィールドを使用するには、フォームがプログラム（Design Studio 内ではない）の下に存在する必要があります。また、これらのフィールドを使用するフォームを含むランディングページも、プログラムの下に存在する必要があります（Design Studio 内に存在したり、Design Studio に複製したりすることはできません）。

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

各フォームには、編集可能なフィールドのリストが含まれ、読み込むとエンドユーザに表示されます。各フィールドは、それぞれのエンドポイントを通じて、フィールドリストから 1 つずつ追加、更新または削除されます。

[フィールドの追加](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addFieldToAFormUsingPOST)には、親フォームの ID とフィールドの fieldId のみが必要です。他のすべてのフィールドは、空になるか、データタイプとフィールドメタデータに基づいてデフォルト値が設定されます。データは、JSON ではなく、POST x-www-form-urlencoded として渡されます。

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

更新では、フィールドの追加と同じフィールドがすべて編集される場合があり、同様にフォーム ID と fieldId が必要になります。ただし、更新を実行する際に fieldId はクエリパラメーターではなくパスパラメーターである点が異なります。

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

上記の例では、シンプルな文字列である LastName フィールドを更新しています。一部のフォームフィールドはより複雑です。例えば、「敬称」フィールドは、項目のリストとデフォルト値を含む「選択」フィールドタイプです。選択タイプフィールドを追加または更新する場合、選択の 1 つに `isDefault` 値を true に設定しない限り、最初の選択には値がなく、「選択…」というラベルが付けられます。

![敬称](assets/form-field-salutation.png)

リスト項目を更新する場合、「values」パラメーターの形式は次のようになります。

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

 

複雑なフォーム フィールドの書式設定方法を決定するには、「フォームにフィールドを追加」からの応答を確認します。

### フィールドの並べ替え

フォーム内のフィールドはすべて、[フォームフィールド位置を変更](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/updateFieldPositionsUsingPOST)エンドポイントを通じて単一の単位として並べ替える必要があります。エンドポイントには、`positions` というパラメーターが必要です。これは、次の 3 つのメンバーを持つオブジェクトの JSON 配列です。

- columnNumber
- rowNumber
- fieldName（フィールドの ID を指します）

フォーム内のフィールドは、最大 3 列、最大 10 行のテーブルのようなインターフェイスで配置されます。行と列は両方とも 0 からインデックス付けされるので、最初の行と最初の列は両方とも 0 を渡すことによって示されます。すべてのフィールドが一意の位置を占める必要があります

また、ターゲットフィールドもフィールドセットである場合、positions 配列内のこのレコードには、同じ columnNumber、rowNumber および fieldName メンバーを含むオブジェクトの配列である fieldList というパラメーターも含める必要があります。フィールドセット自体は親リスト内の位置に対して単一のフィールドとして処理され、このサブフィールドは fieldList パラメーターで指定した位置に従って配置されます。

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

リッチテキストフィールドは、リードフィールドとは[別のエンドポイント](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addRichTextFieldUsingPOST)を通じて追加されます。フィールドコンテンツは、multipart/form-data として渡されます。スクリプト、メタタグ、リンクタグを含まない HTML コンテンツとして構造化する必要があります。

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

Marketo フォームには、フィールドセットというオプションのコンポーネントがあります。フィールドセットは、表示ルールによる移動および処理の目的で、上位レベルのフィールドリスト内で単一のフィールドとして処理されるフィールドのグループです。例えば、コンプライアンス要件のフィールドがあり、クライアントが「はい」を選択した場合、HIPAA および PCI コンプライアンス要件のフィールドを含むフィールドセットが表示される可能性があります。

フィールドセット内のフィールドはフォーム全体に固有なので、重複するフィールドはフォームの親フィールドリストと子フィールドセットの両方に存在できません。フィールドセットは、[フォームにフィールドセットを追加](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addFieldSetUsingPOST)エンドポイントを通じて追加され、[フォームのフィールドを取得](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/getFormFieldByFormVidUsingGET)の結果に表示されます。フィールドは、[フィールド位置を更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/updateFieldPositionsUsingPOST)を使用してフィールドセットのフィールドリストに移動することで、フィールドセットに追加されます。これらのエンドポイントの場合、データは、JSON ではなく、POST x-www-form-urlencoded として渡されます。

## 表示ルール

各フィールドには、フォームに入力した値に応じて訪問者がフィールドを表示できるかどうかを決定する一連の表示ルールがある場合があります。ルールは、フォーム内に存在する subjectField の値と、ルールで指定された値のリストを比較します。各フィールドには、表示、非表示、または alwaysShow のいずれか 1 つのタイプの表示ルールと、評価するルールのリストを設定できます。ルールは上から下に向かって評価され、最初に true と評価されたルールが適用されます。

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

使用可能な演算子の完全なリストについては、[フォームフィールド表示ルールを追加](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addFormFieldVisibilityRuleUsingPOST)のエンドポイント参照ページを参照してください。

## フォローアップ

Marketo フォームには動的なフォローアップページ動作があり、送信時に指定したフィールドのコンテンツに基づいて、特定のページにリダイレクトするルールや現在のページに留まるルールが適用される場合があります。ルールは、サンキューページルールまたはフォローアップページルールとも呼ばれます。これらのルールは、`followupType`、`followupValue`、`operator`、`subjectField`、`values`、`default` のメンバーを含む JSON 配列として表されます。`default` はブール値で、配列内の 1 つのレコードのみが true になる場合があります。訪問者が他のルールの要件を満たさない場合は、デフォルトとして指定したルールが使用されます。`followupType` は lp または url のいずれかです。lp は `followupValue` の Marketo ランディング ページ ID を示し、url は別のページへの URL を示します。演算子は、件名フィールドの値を、指定した値のリストと比較するために使用されます。

## 送信ボタン

フォームの送信ボタンのスタイル設定は、[送信ボタンを更新](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/updateFormSubmitButtonUsingPOST)エンドポイントで管理されます。buttonPosition、buttonStyle、label、waitingLabel（送信が保留中に表示されるラベル）を変更できます。

これは破壊的な更新です。

## 承認

他のほとんどのアセットと同様に、フォームはドラフトバージョンや承認済みバージョンを指定できるドラフト承認済みモデルに従います。フォームに更新を適用するたびに、常に最初にドラフトバージョンに適用され、フォームが承認された場合にのみライブで表示されます。フォームを承認すると、現在のドラフトバージョンが取得され、承認済みバージョンがある場合はドラフトに置き換えられます。フォームをライブから削除する必要がある場合は、最初にフォームを未承認にする必要があります。これにより、現在のドラフトがすべて削除され、承認済みバージョンがドラフトのみの状態に降格されます。フォームは、削除を試みる前に、常に未承認にする必要があります。

## プログレッシブプロファイリング

フォームでプログレッシブプロファイリングが有効になっている場合、「プロファイリング」と呼ばれるフィールドセットがフィールドリストに含まれます。プログレッシブプロファイリングリストからフィールドを追加または削除するには、「フィールド位置を更新」エンドポイントを使用する必要があります。このエンドポイントは、破壊的な更新を行うので、フォーム内のすべてのフィールドを各リクエストに含める必要があります。次の例では、「電話」フィールドをプログレッシブプロファイルリストに追加します。

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
