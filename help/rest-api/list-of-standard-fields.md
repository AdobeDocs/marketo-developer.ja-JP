---
title: 標準フィールド
feature: REST API, Field Management
description: 標準のMarketo フィールドのテーブル。
exl-id: 147dbdff-4bc9-4ab3-8918-c4de3e1aa97a
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 30%

---

# 標準フィールド

以下は、API からアクセスできる、Marketoで使用できる標準フィールドのリストです。

REST [ リードを説明 ](https://developer.adobe.com/marketo-apis/api/mapi/) エンドポイントを使用すると、リードレコードで使用可能なすべてのサポートされているフィールド名のリストを取得できます。

| REST API 名 | SOAP API 名 | フレンドリ ラベル | 説明 |
| --- | --- | --- | --- |
| 住所 | 住所 | 住所 | リードのアドレス |
| annualRevenue | AnnualRevenue | 年間収益 | リードの会社の年間収益 |
| anonymousIP | AnonymousIP | 匿名 IP | リードの最初に記録された Web 訪問の IP アドレス |
| billingCity | BillingCity | 請求先住所（市区町村） | リードの請求先住所の都市 |
| billingCountry | BillingCountry | 請求先住所 (国) | リードの請求先住所の国 |
| billingPostalCode | BillingPostalCode | 請求先住所 (郵便番号) | リードの請求先住所の郵便番号 |
| billingState | BillingState | 請求先住所 (都道府県) | リードの請求先住所の都道府県 |
| billingStreet | BillingStreet | 請求先住所 | リードの会社の請求先住所 |
| 市 | 市区町村 | 市区町村 | リードの都市 |
| 会社 | 企業 | 企業名 | リードの会社名 |
| 国 | 国 | 国 | リードの国 |
| dateOfBorth | DateofBirth | 生年月日 | リードの生年月日 |
| department | Department | Department | 社内のリード部門 |
| doNotCall | DoNotCall | 電話連絡拒否 | リードの通話拒否環境設定 |
| doNotCallReason | DoNotCallReason | 電話連絡拒否の理由 | リードの通話拒否環境設定の説明 |
| メール | メール | メールアドレス | リードのメールアドレス。 リードレコードの標準Marketoキーフィールド |
| fax | FAX | FAX 番号 | リードの FAX 番号 |
| firstName | FirstName | 名前（名） | リードの名 |
| 業界 | 業界 | 業界 | リード業界 |
| inferredCompany | InferredCompany | 推測される企業 | リードの最初に記録された Web 訪問の逆引き IP 参照によって推測される会社名 |
| inferredCountry | InferredCountry | 推測される国 | リードの最初に記録された Web 訪問の逆引き IP 参照によって推測される国 |
| lastName | LastName | 名前（姓） | リードの姓 |
| leadRole | LeadRole | Role | 会社でのリードの役割 |
| leadScore | LeadScore | リードのスコア | キャンペーンおよびプログラムのスコアリングによってリードに付与される整数スコア |
| leadSource | LeadSource | リードのソース | リードの元となるソースを記録するフィールド |
| leadStatus | LeadStatus | リードのステータス | リードの現在のマーケティング /販売ステータスを記録するフィールド |
| mainPhone | MainPhone | 代表電話 | リードの会社のプライマリの電話番号 |
| jigsawContactId | Marketo Jigsaw 取引先責任者 ID | Marketo Data.com ID | リードのData.com ID （使用可能な場合） |
| jigsawContactStatus | Marketo Jigsaw 取引先責任者ステータス | Marketo Data.com ステータス | リードのData.com ステータス（使用可能な場合） |
| facebookDisplayName | MarketoSocialFacebookDisplayName | Marketo ソーシャル Facebook の表示名 | リードのFacebookの表示名。 ソーシャルログイン中に生成されたシステム |
| facebookId | MarketoSocialFacebookId | Marketo ソーシャル Facebook ID | リードのFacebook Id。 ソーシャルログイン中に生成されたシステム |
| facebookPhotourl | MarketoSocialFacebookPhotoURL | Marketo ソーシャル Facebook の画像 URL | リードのFacebook プロファイル写真の URL。 ソーシャルログイン中に生成されたシステム |
| facebookProfileURL | MarketoSocialFacebookProfileURL | Marketo ソーシャル Facebook のプロファイル URL | リードのFacebook プロファイルの URL。 ソーシャルログイン中に生成されたシステム |
| facebookReach | MarketoSocialFacebookReach | Marketo ソーシャル Facebook のリーチ | リードのFacebookリーチ。 ソーシャルログイン中に生成されたシステム |
| facebookReferredEnrollments | MarketoSocialFacebookReferredEnrollments | Marketo ソーシャル Facebook を参照元とする登録数 | リードからFacebookまでに起因する参照登録数。 システム管理 |
| facebookReferredVisits | MarketoSocialFacebookReferredVisits | Marketo ソーシャル Facebook を参照元とする訪問数 | facebook経由のリードに起因する参照回数。 システム管理 |
| 性別 | MarketoSocialGender | Marketo ソーシャル性別 | リードの性別。 ソーシャルログイン中に生成されたシステム |
| lastReferredEnrollment | MarketoSocialLastReferredEnrollment | Marketo ソーシャルを最後の参照元とする登録 | 最後に完了したリファラルの日付。 システム管理 |
| lastReferredVisit | MarketoSocialLastReferredVisit | Marketo ソーシャルを最後の参照元とする訪問 | 前回の参照訪問の日付。 システム管理 |
| linkedInDisplayName | MarketoSocialLinkedInDisplayName | Marketo ソーシャル LinkedIn の表示名 | リードのLinkedInの表示名。 ソーシャルログイン中に生成されたシステム |
| linkedInId | MarketoSocialLinkedInId | Marketo ソーシャル LinkedIn Id | リードのLinkedIn Id。 ソーシャルログイン中に生成されたシステム |
| linkedInPhotourl | MarketoSocialLinkedInPhotoURL | Marketo ソーシャル LinkedIn の画像 URL | リードのLinkedIn写真 URL。 ソーシャルログイン中に生成されたシステム |
| linkedInProfileURL | MarketoSocialLinkedInProfileURL | Marketo ソーシャル LinkedIn のプロファイル URL | リードのLinkedIn プロファイル。 ソーシャルログイン中に生成されたシステム |
| linkedInReach | MarketoSocialLinkedInReach | Marketo ソーシャル LinkedIn のリーチ | リードのLinkedInリーチ。 ソーシャルログイン中に生成されたシステム |
| linkedInReferredEnrollments | MarketoSocialLinkedInReferredEnrollments | Marketo ソーシャル LinkedIn を参照元とする登録数 | リードからLinkedInまでに起因する参照登録数。 システム管理 |
| linkedInReferredVisits | MarketoSocialLinkedInReferredVisits | Marketo ソーシャル LinkedIn を参照元とする訪問数 | linkedIn経由のリードに起因する参照回数。 システム管理 |
| syndicationId |  - | Marketo ソーシャル Syndication ID | リードの内部Marketo ソーシャル ID。 システム管理 |
| totalReferredEnrollments | MarketoSocialTotalReferredEnrollments | Marketo ソーシャルを参照元とする合計登録数 | リードに起因する完了済みのリファラル登録数の合計 |
| totalReferredVisits | MarketoSocialTotalReferredVisits | Marketo ソーシャルを参照元とする合計訪問数 | リードに起因する参照訪問の合計数 |
| twitterDisplayName | MarketoSocialTwitterDisplayName | Marketo ソーシャル Twitter の表示名 | リードのTwitterの表示名。 ソーシャルログイン中に生成されたシステム |
| twitterId | MarketoSocialTwitterId | Marketo ソーシャル Twitter Id | リードのTwitter Id。 ソーシャルログイン中に生成されたシステム |
| twitterPhotourl | MarketoSocialTwitterPhotoURL | Marketo ソーシャル Twitter の画像 URL | リードのTwitter写真 URL。 ソーシャルログイン中に生成されたシステム |
| twitterProfileURL | MarketoSocialTwitterProfileURL | Marketo ソーシャル Twitter のプロファイル URL | リードのTwitterプロファイル URL。 ソーシャルログイン中に生成されたシステム |
| twitterReach | MarketoSocialTwitterReach | Marketo ソーシャル Twitter のリーチ | リードのTwitterリーチ。 ソーシャルログイン中に生成されたシステム |
| twitterReferredEnrollments | MarketoSocialTwitterReferredEnrollments | Marketo ソーシャル Twitter を参照元とする登録数 | リードスルーTwitterに起因する参照登録数。 システム管理 |
| twitterReferredVisits | MarketoSocialTwitterReferredVisits | Marketo ソーシャル Twitter を参照元とする訪問数 | リードスルーTwitterに起因する参照回数。 システム管理 |
| middleName | MiddleName | ミドルネーム | リードのミドルネーム |
| mobilePhone | MobilePhone | 携帯電話番号 | リードの携帯電話番号 |
| numberOfEmployees | NumberOfEmployees | 従業員数 | リードの会社の従業員数 |
| 電話 | 電話 | 電話番号 | リードの電話番号 |
| postalCode | PostalCode | 郵便番号 | リードの郵便番号 |
| rating | Rating | リード評価 | リードのマーケティング /販売評価 |
| salutation | 敬称 | 敬称 | リードの好ましい敬称（ミスター、ミスなど）。 |
| sicCode | SICCode | SIC コード | 潜在顧客の会社の標準産業分類コード |
| サイト | サイト | サイト |  |
| state | 都道府県 | 都道府県 | リードの状態 |
| title | Title | Job Title | リードの職位 |
| unsubscribed | Unsubscribed | Unsubscribed | リードの購読解除済みステータス。 部分的にシステム管理されています。 true に設定されている場合、操作できない E メールを受信するのを防ぎます。 |
| unsubscribedReason | UnsubscribedReason | 登録解除の理由 | リードの購読解除状態の理由です。 部分的にシステム管理されています。 リードがMarketoのメールから直接登録解除した場合のメール情報が入力されます。 |
| website | Web サイト | Web サイト | リードの会社の web サイトの URL |
| createdAt |  - | 作成日時 | リードレコードが最初に作成された時間。 システム管理 |
| updatedAt |  - | 更新時刻 | リードレコードが最後に更新された時刻。 システム管理 |
| emailInvalid |  - | メール無効 | メールが無効なステータスです。 true に設定すると、そのアドレス宛てのすべてのメールがブロックされます。 メールが無効であることを示すバウンスは、このフィールドを自動的に true に設定します。 |
| emailInvalidCause |  - | メール無効の理由 | メールの原因が無効なステータスです。 無効なメールが true に設定されている場合、開始バウンスメッセージはこのフィールドに記録されます。 |
| inferredCity |  - | 推測される市区町村 | リードの最初に記録された web 訪問の逆引き IP 参照によって推測されるリードの市区町村。 |
| inferredMetropolitanArea |  - | 推測される都市圏 | リードの最初に記録された web 訪問の逆引き IP 参照によって推測されるリードのメトロポリタンエリア。 |
| inferredPhoneAreaCode |  - | 推測される市外局番 | リードの最初に記録された web 訪問の逆引き IP 参照によって推測されるリードの市外局番。 |
| 推測される郵便番号 |  - | 推測される郵便番号 | リードの最初に記録された web 訪問の逆引き IP 参照によって推測されるリードの郵便番号。 |
| inferredStateRegion |  - | 推測される都道府県／地域 | リードの最初に記録された web 訪問の逆引き IP 参照によって推測されるリードの状態領域。 |
| isAnonymous |  - | 匿名 | リードレコードの匿名ステータス。 システムが管理します。 |
| priority |  - | 優先度 | リードのセールスインサイトの優先度。 システムが管理します。 |
| relativeScore |  - | 相対スコア | リードの Sales Insight の相対スコア。 システムが管理します。 |
| 緊急度 |  - | 緊急度 | リードのセールスインサイトの緊急度。 システムが管理します。 |
