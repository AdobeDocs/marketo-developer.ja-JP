---
title: SOAP API
feature: SOAP
description: Marketo SOAP APIは、2025年10月31日以降に非推奨（廃止予定）になります。 RESTへの移行、WSDLの取得、クォータ、レート制限、認証の設定を参照してください。
exl-id: 6618cc82-15ae-4030-aa00-438e635d8369
source-git-commit: ff0a95e838cecd1d8b1f90ca029a320043824242
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 63%

---

# SOAP API

SOAP APIは非推奨（廃止予定）であり、2026年7月31日以降は使用できなくなります。 すべての新規開発は、Marketo [REST API](../rest-api/rest-api.md) を使用して行う必要があり、サービスの中断を回避するのに既存のサービスはその日までに移行する必要があります。 SOAP API を使用するサービスがある場合、移行方法について詳しくは、SOAP API [移行ガイド](./migration.md)を参照してください。

## SOAP WSDL

SOAP WSDL ドキュメントを取得するには、**[!UICONTROL 管理]**／**[!UICONTROL 統合]**／**[!UICONTROL Web サービス]**&#x200B;メニューから SOAP API エンドポイントを取得します。

![SOAP エンドポイント](assets/endpoint-soap.png)

WSDL URL は次のとおりです。

`<SOAP API Endpoint> + ?WSDL`

WSDL で定義されているエンドポイントを使用しないでください。 各 Marketo インスタンスには、呼び出しを行う一意のエンドポイントがあります。

## 制限

- **毎日の割り当て量：**&#x200B;ほとんどのサブスクリプションには、1日あたり10,000回のAPI呼び出しが割り当てられます（毎日12:00AM CSTでリセットされます）。 アカウントマネージャーを通じて、毎日の割り当て量を増やすことができます。
- **レートの制限：**&#x200B;インスタンスあたりの API アクセスは、20 秒あたり 100 回の呼び出しに制限されます。
- **同時実行の制限：**&#x200B;同時 API 呼び出しは最大 10 回までです。

バッチサイズは 300 を超えないようにすることをお勧めします。 これより大きなサイズはサポートされず、タイムアウトや、極端な場合はスロットルが発生することがあります。

## Marketo での SOAP API 設定

1. **[!UICONTROL 管理者]** セクションに移動し、**[!UICONTROL Web サービス]**&#x200B;を選択します。

![admin-web-services2](assets/admin-web-services2.png)

1. 適切な[!UICONTROL 暗号化キー]を設定し、**[!UICONTROL 変更を保存]**&#x200B;を選択し、SOAP API [!UICONTROL &#x200B; エンドポイント &#x200B;]、[!UICONTROL &#x200B; ユーザーID]、および[!UICONTROL 暗号化キー]の値を使用して、SOAP API呼び出しごとに正しい[認証シグネチャ &#x200B;](authentication-signature.md)を生成します。

![admin-web-services3](assets/admin-web-services3.png)
