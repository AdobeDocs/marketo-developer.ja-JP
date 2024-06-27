---
title: SOAP API
feature: SOAP
description: Marketo SOAPの概要
exl-id: 6618cc82-15ae-4030-aa00-438e635d8369
source-git-commit: 6fc45ff98998217923e2a5b02d00d1522fe3272c
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 2%

---

# SOAP API

SOAP API は現在開発中ではありません。 呼び出しは引き続き機能しますが、開発の焦点は次のとおりです [REST](https://developer.adobe.com/marketo-apis/) 先に進む。

Marketo SOAP API を使用すると、Marketoに保存されているエンティティとデータを作成、取得、削除できます。 次を見つけることができます [Marketo-SOAP-SDK](https://github.com/Marketo/SOAP-API-Java-Client) GitHub で。 次のものがあります [クライアントライブラリ](https://github.com/Marketo/Community-Supported-Client-Libraries) 時間を節約するために。

最新の API バージョン：3_1

## SOAP WSDL

SOAP SOAP WSDL ドキュメントを取得するには、 **[!UICONTROL Admin]** > **[!UICONTROL 統合]** > **[!UICONTROL Web サービス]** メニュー。

![SOAP エンドポイント](assets/endpoint-soap.png)

WSDL URL は次のとおりです。

`<SOAP API Endpoint> + ?WSDL`

WSDL で定義されているエンドポイントを使用しないでください。 各Marketo インスタンスには、を呼び出す一意のエンドポイントがあります。

## 制限

- **毎日のクォータ：** ほとんどのサブスクリプションには、1 日に 10,000 回の API 呼び出しが割り当てられます（毎日 12:00 にリセットされます）。 アカウントマネージャーを通じて、1 日の割り当て量を増やすことができます。
- **レート制限：** インスタンスごとの API アクセスは、20 秒あたり 100 回の呼び出しに制限されています。
- **同時実行制限：**  最大 10 回の同時 API 呼び出し。

バッチサイズは 300 以下にすることをお勧めします。 大きいサイズはサポートされず、タイムアウトや、極端な場合はスロットリングが発生する可能性があります。

## MarketoでのSOAP API 設定

1. に移動します **[!UICONTROL Admin]** セクションでクリック **[!UICONTROL Web サービス]**.

![admin-web-services2](assets/admin-web-services2.png)

1. 適切な [!UICONTROL 暗号化キー]を選択し、 **[!UICONTROL 変更を保存]** およびSOAP API の使用 [!UICONTROL エンドポイント], [!UICONTROL ユーザー ID]、および [!UICONTROL 暗号化キー] 正しいを生成するための値 [認証署名](authentication-signature.md) （SOAP API 呼び出しごとに）。

![admin-web-services3](assets/admin-web-services3.png)
