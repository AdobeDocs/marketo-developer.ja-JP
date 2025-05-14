---
title: SOAP API
feature: SOAP
description: Marketo SOAP の概要
exl-id: 6618cc82-15ae-4030-aa00-438e635d8369
source-git-commit: 8ad3e3f0958ea705375651b1c8a75967d807ca80
workflow-type: ht
source-wordcount: '245'
ht-degree: 100%

---

# SOAP API

SOAP API は非推奨（廃止予定）となり、2025年10月31日（PT）以降は使用できなくなります。すべての新規開発は、Marketo [REST API](../rest-api/rest-api.md) を使用して行う必要があり、サービスの中断を回避するために、既存のサービスをその日までに移行する必要があります。SOAP API を使用するサービスがある場合、移行方法について詳しくは、SOAP API [移行ガイド](./migration.md)を参照してください。

## SOAP WSDL

SOAP WSDL ドキュメントを取得するには、**[!UICONTROL 管理]**／**[!UICONTROL 統合]**／**[!UICONTROL Web サービス]**&#x200B;メニューから SOAP API エンドポイントを取得します。

![SOAP エンドポイント](assets/endpoint-soap.png)

WSDL URL は次のとおりです。

`<SOAP API Endpoint> + ?WSDL`

WSDL で定義されているエンドポイントを使用しないでください。各 Marketo インスタンスには、呼び出しを行う一意のエンドポイントがあります。

## 制限

- **毎日の割り当て量：**&#x200B;ほとんどのサブスクリプションには 1 日あたり 10,000 回の API 呼び出しが割り当てられます（毎日午前 12:00 CST にリセットされます）。アカウントマネージャーを通じて、毎日の割り当て量を増やすことができます。
- **レートの制限：**&#x200B;インスタンスあたりの API アクセスは、20 秒あたり 100 回の呼び出しに制限されます。
- **同時実行の制限：**&#x200B;同時 API 呼び出しは最大 10 回までです。

バッチサイズは 300 を超えないようにすることをお勧めします。これより大きなサイズはサポートされず、タイムアウトや、極端な場合はスロットルが発生することがあります。

## Marketo での SOAP API 設定

1. 「**[!UICONTROL 管理]**」セクションに移動し、「**[!UICONTROL Web サービス]**」をクリックします。

![admin-web-services2](assets/admin-web-services2.png)

1. 適切な[!UICONTROL 暗号化キー]を設定し、「**[!UICONTROL 変更を保存]**」をクリックし、SOAP API [!UICONTROL エンドポイント]、[!UICONTROL ユーザ ID]、[!UICONTROL 暗号化キー]の値を使用して、各 SOAP API 呼び出しの正しい[認証署名](authentication-signature.md)を生成します。

![admin-web-services3](assets/admin-web-services3.png)
