---
title: SOAP API
feature: SOAP
description: Marketo SOAPの概要
exl-id: 6618cc82-15ae-4030-aa00-438e635d8369
source-git-commit: 8ad3e3f0958ea705375651b1c8a75967d807ca80
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---

# SOAP API

SOAP API は非推奨（廃止予定）となっており、2025 年 10 月 31 日（PT）以降は使用できなくなります。 すべての新規開発はMarketo [REST API](../rest-api/rest-api.md) を使用して行う必要があり、サービスが中断されないように、既存のサービスはその日までに移行する必要があります。 SOAP API を使用するサービスがある場合は、SOAP API [ 移行ガイド ](./migration.md) を参照して、移行方法を確認してください。

## SOAP WSDL

SOAP WSDL ドキュメントを取得するには、**[!UICONTROL 管理者]**/**[!UICONTROL 統合]**/**[!UICONTROL web サービス]** メニューからSOAP API エンドポイントを取得します。

![SOAP エンドポイント ](assets/endpoint-soap.png)

WSDL URL は次のとおりです。

`<SOAP API Endpoint> + ?WSDL`

WSDL で定義されているエンドポイントを使用しないでください。 各Marketo インスタンスには、を呼び出す一意のエンドポイントがあります。

## 制限

- **毎日の割り当て量：** ほとんどの購読には、1 日あたり 10,000 回の API 呼び出しが割り当てられます（毎日 12:00 にリセットされます）。 アカウントマネージャーを通じて、1 日の割り当て量を増やすことができます。
- **レート制限：インスタンスあたりの** API アクセスは、20 秒あたり 100 回の呼び出しに制限されています。
- **同時実行制限：**  最大 10 回の同時 API 呼び出し。

バッチサイズは 300 以下にすることをお勧めします。 大きいサイズはサポートされず、タイムアウトや、極端な場合はスロットリングが発生する可能性があります。

## MarketoでのSOAP API 設定

1. 「**[!UICONTROL 管理者]**」セクションに移動し、「**[!UICONTROL Web サービス]**」をクリックします。

![admin-web-services2](assets/admin-web-services2.png)

1. 適切な [!UICONTROL &#x200B; 暗号化キー &#x200B;] を設定し、「**[!UICONTROL 変更を保存]**」をクリックして、SOAP API [!UICONTROL &#x200B; エンドポイント &#x200B;]、[!UICONTROL &#x200B; ユーザー ID]、[!UICONTROL &#x200B; 暗号化キー &#x200B;] の値を使用して、各SOAP API 呼び出しに正しい [ 認証署名 ](authentication-signature.md) を生成します。

![admin-web-services3](assets/admin-web-services3.png)
