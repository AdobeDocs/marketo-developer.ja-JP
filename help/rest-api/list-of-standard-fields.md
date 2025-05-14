---
title: 標準フィールド
feature: REST API, Field Management
description: 標準の Marketo フィールドのテーブル。
exl-id: 147dbdff-4bc9-4ab3-8918-c4de3e1aa97a
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '1140'
ht-degree: 100%

---

# 標準フィールド

API 経由でアクセスできる Marketo で使用可能な標準フィールドのリストを以下に示します。

REST [リードを説明](https://developer.adobe.com/marketo-apis/api/mapi/)エンドポイントを使用して、リードレコードで使用可能なすべてのサポートされているフィールド名のリストを取得できます。

| REST API 名 | SOAP API 名 | わかりやすいラベル | 説明 |
| --- | --- | --- | --- |
| address | Address | Address | リードの住所 |
| annualRevenue | AnnualRevenue | 年間売上高 | リードの会社の年間売上高 |
| anonymousIP | AnonymousIP | 匿名 IP | リードの最初の web 訪問時に記録された IP アドレス |
| billingCity | BillingCity | 請求先住所（市区町村） | リードの請求先住所の市区町村 |
| billingCountry | BillingCountry | 請求先住所（国） | リードの請求先住所の国 |
| billingPostalCode | BillingPostalCode | 郵便番号 | リードの請求先住所の郵便番号 |
| billingState | BillingState | 請求先住所（都道府県） | リードの請求先住所の都道府県 |
| billingStreet | BillingStreet | 請求先住所 | リードの会社の請求先住所 |
| city | 市区町村 | 市区町村 | リードの市区町村 |
| company | 企業 | 企業名 | リードの会社名 |
| country | 国 | 国 | リードの国 |
| dateOfBirth | DateofBirth | 生年月日 | リードの生年月日 |
| department | Department | Department | リードの会社の部門 |
| doNotCall | DoNotCall | 電話連絡拒否 | リードの電話連絡拒否の環境設定 |
| doNotCallReason | DoNotCallReason | 電話連絡拒否の理由 | リードの電話連絡拒否の環境設定の説明 |
| email | メール | メールアドレス | リードのメールアドレス。リードレコードの標準 Marketo キーフィールド |
| fax | FAX | FAX 番号 | リードの FAX 番号 |
| firstName | FirstName | 名前（名） | リードの名前（名） |
| industry | 業界 | 業界 | リードの業界 |
| inferredCompany | InferredCompany | 推測される会社 | リードの最初の web 訪問の逆 IP 検索によって推測される会社名 |
| inferredCountry | InferredCountry | 推測される国 | リードの最初の web 訪問の逆 IP 検索によって推測される国 |
| lastName | LastName | 名前（姓） | リードの名前（姓） |
| leadRole | LeadRole | Role | リードの会社でのロール |
| leadScore | LeadScore | リードのスコア | キャンペーンとプログラムのスコアリングによってリードに付与される整数スコア |
| leadSource | LeadSource | リードのソース | リードの元となるソースを記録するフィールド |
| leadStatus | LeadStatus | リードのステータス | リードの現在のマーケティング／販売ステータスを記録するフィールド |
| mainPhone | MainPhone | 代表電話 | リードの会社の代表電話番号 |
| jigsawContactId | Marketo Jigsaw 取引先責任者 ID | Marketo Data.com ID | リードの Data.com ID（使用可能な場合） |
| jigsawContactStatus | Marketo Jigsaw 取引先責任者ステータス | Marketo Data.com ステータス | リードの Data.com ステータス（使用可能な場合） |
| facebookDisplayName | MarketoSocialFacebookDisplayName | Marketo ソーシャル Facebook の表示名 | リードの Facebook 表示名。ソーシャルログイン中にシステムが入力します |
| facebookId | MarketoSocialFacebookId | Marketo ソーシャル Facebook ID | リードの Facebook ID。ソーシャルログイン中にシステムが入力します |
| facebookPhotoURL | MarketoSocialFacebookPhotoURL | Marketo ソーシャル Facebook の画像 URL | リードの Facebook プロフィール写真の URL。 ソーシャルログイン中にシステムが入力します |
| facebookProfileURL | MarketoSocialFacebookProfileURL | Marketo ソーシャル Facebook のプロファイル URL | リードの Facebook プロファイルの URL。ソーシャルログイン中にシステムが入力します |
| facebookReach | MarketoSocialFacebookReach | Marketo ソーシャル Facebook のリーチ | リードの Facebook リーチ。ソーシャルログイン中にシステムが入力します |
| facebookReferredEnrollments | MarketoSocialFacebookReferredEnrollments | Marketo ソーシャル Facebook を参照元とする登録数 | Facebook 経由のリードに帰属する参照元からの登録件数。システムが管理します |
| facebookReferredVisits | MarketoSocialFacebookReferredVisits | Marketo ソーシャル Facebook を参照元とする訪問数 | Facebook 経由のリードに帰属する参照元からの訪問数。システムが管理します |
| gender | MarketoSocialGender | Marketo ソーシャル性別 | リードの性別。ソーシャルログイン中にシステムが入力します |
| lastReferredEnrollment | MarketoSocialLastReferredEnrollment | Marketo ソーシャルを最後の参照元とする登録 | 最終的な紹介が完了した日付。システムが管理します |
| lastReferredVisit | MarketoSocialLastReferredVisit | Marketo ソーシャルの最後の参照訪問 | 最後の参照訪問の日付。システムが管理します |
| linkedInDisplayName | MarketoSocialLinkedInDisplayName | Marketo ソーシャル LinkedIn の表示名 | リードの LinkedIn の表示名。ソーシャルログイン中にシステムが入力します |
| linkedInId | MarketoSocialLinkedInId | Marketo ソーシャル LinkedIn Id | リードの LinkedIn ID。ソーシャルログイン中にシステムが入力します |
| linkedInPhotoURL | MarketoSocialLinkedInPhotoURL | Marketo ソーシャル LinkedIn の画像 URL | リードの LinkedIn 画像 URL。ソーシャルログイン中にシステムが入力します |
| linkedInProfileURL | MarketoSocialLinkedInProfileURL | Marketo ソーシャル LinkedIn のプロファイル URL | リードの LinkedIn プロファイル。ソーシャルログイン中にシステムが入力します |
| linkedInReach | MarketoSocialLinkedInReach | Marketo ソーシャル LinkedIn のリーチ | リードの LinkedIn リーチ。ソーシャルログイン中にシステムが入力します |
| linkedInReferredEnrollments | MarketoSocialLinkedInReferredEnrollments | Marketo ソーシャル LinkedIn を参照元とする登録数 | LinkedIn 経由のリードに帰属する参照元からの登録件数。システムが管理します |
| linkedInReferredVisits | MarketoSocialLinkedInReferredVisits | Marketo ソーシャル LinkedIn を参照元とする訪問数 | LinkedIn 経由のリードに帰属する参照元からの訪問数。システムが管理します |
| syndicationId | - | Marketo ソーシャル Syndication ID | リードの内部 Marketo ソーシャル ID。 システムが管理します |
| totalReferredEnrollments | MarketoSocialTotalReferredEnrollments | Marketo ソーシャルを参照元とする合計登録数 | リードに帰属する完了済みのリファラル登録の合計数 |
| totalReferredVisits | MarketoSocialTotalReferredVisits | Marketo ソーシャルを参照元とする合計訪問数 | リードに帰属する参照元からの訪問の合計数 |
| twitterDisplayName | MarketoSocialTwitterDisplayName | Marketo ソーシャル Twitter の表示名 | リードの Twitter 表示名。ソーシャルログイン中にシステムが入力します |
| twitterId | MarketoSocialTwitterId | Marketo ソーシャル Twitter Id | リードの Twitter ID。ソーシャルログイン中にシステムが入力します |
| twitterPhotoURL | MarketoSocialTwitterPhotoURL | Marketo ソーシャル Twitter の画像 URL | リードの Twitter の画像 URL。ソーシャルログイン中にシステムが入力します |
| twitterProfileURL | MarketoSocialTwitterProfileURL | Marketo ソーシャル Twitter のプロファイル URL | リードの Twitter プロファイル URL。ソーシャルログイン中にシステムが入力します |
| twitterReach | MarketoSocialTwitterReach | Marketo ソーシャル Twitter のリーチ | リードの Twitter リーチ。ソーシャルログイン中にシステムが入力します |
| twitterReferredEnrollments | MarketoSocialTwitterReferredEnrollments | Marketo ソーシャル Twitter を参照元とする登録数 | Twitter 経由でリードに帰属する参照元からの登録件数。システムが管理します |
| twitterReferredVisits | MarketoSocialTwitterReferredVisits | Marketo ソーシャル Twitter を参照元とする訪問数 | Twitter 経由でリードに帰属する参照元からの訪問数。システムが管理します |
| middleName | MiddleName | ミドルネーム | リードのミドルネーム |
| mobilePhone | MobilePhone | 携帯電話番号 | リードの携帯電話番号 |
| numberOfEmployees | NumberOfEmployees | 従業員数 | リードの会社の従業員数 |
| phone | 電話 | 電話番号 | リードの電話番号 |
| postalCode | PostalCode | 郵便番号 | リードの郵便番号 |
| rating | Rating | リード評価 | リードのマーケティング／セールス評価 |
| salutation | 敬称 | 敬称 | リードが使用する敬称（Mr.、Mis. など）。 |
| sicCode | SICCode | SIC コード | リードの会社の標準産業分類コード |
| site | Site | Site |  |
| state | State | State | リードの都道府県 |
| title | Title | Job Title | リードの職位 |
| unsubscribed | 登録解除済み | 登録解除済み | リードのメール登録解除済みステータス。部分的にシステムで管理されます。true に設定すると、運用以外のメールの受信が防止されます。 |
| unsubscribedReason | UnsubscribedReason | 登録解除の理由 | リードの登録解除済みステータスの理由。部分的にシステムで管理されます。リードが Marketo のメールから直接登録解除された場合、メール情報が入力されます。 |
| website | Web サイト | Web サイト | リードの会社の web サイトの URL |
| createdAt | - | 作成日時 | リードレコードの作成日時。システムが管理します |
| updatedAt | - | 更新日時 | リードレコードを最後に更新した日時。システムが管理します |
| emailInvalid | - | メール無効 | メール無効ステータス。true に設定すると、そのアドレスへのすべてのメールがブロックされます。メールが無効であることを示すバウンスは、このフィールドを自動的に true に設定します。 |
| emailInvalidCause | - | メール無効の理由 | メール無効ステータスの理由。メール無効を true に設定されている場合、原因となるバウンスメッセージがこのフィールドに記録されます。 |
| inferredCity | - | 推測される市区町村 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの市区町村。 |
| inferredMetropolitanArea | - | 推測される都市圏 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの都市圏。 |
| inferredPhoneAreaCode | - | 推測される市外局番 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの市外局番。 |
| inferredPostalCode | - | 推測される郵便番号 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの郵便番号。 |
| inferredStateRegion | - | 推測される都道府県／地域 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの都道府県／地域。 |
| isAnonymous | - | 匿名 | リードレコードの匿名ステータス。システムが管理します。 |
| priority | - | 優先度 | リードのセールスインサイトの優先度。システムが管理します。 |
| relativeScore | - | 相対スコア | リードのセールスインサイトの相対スコア。システムが管理します。 |
| urgency | - | 緊急度 | リードのセールスインサイトの緊急度。システムが管理します。 |
