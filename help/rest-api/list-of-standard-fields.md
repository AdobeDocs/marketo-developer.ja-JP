---
title: 標準フィールド
feature: REST API, Field Management
description: REST名、ラベル、説明を含むMarketo標準リードフィールドの完全なリストと、リードの説明APIを使用してそれらのフィールドを取得する方法を参照します。
exl-id: 147dbdff-4bc9-4ab3-8918-c4de3e1aa97a
TQID: https://experienceleague.adobe.com/vu2wGk36XJ243vwavhfLE7Vc9vMIJKGx6vmVqMRgEDA
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: bcf56d2102f2f60eac5ad3318d348fd020391e6b
workflow-type: tm+mt
source-wordcount: 688
ht-degree: 88%

---

# 標準フィールド

次の表に、APIを通じて使用可能な標準Marketo フィールドを示します。 各フィールドのREST API名、ラベル、説明が含まれます。

REST [&#x200B; リードの説明](https://developer.adobe.com/marketo-apis/api/mapi) エンドポイントを使用して、リード レコードでサポートされているすべてのフィールド名を取得します。

| REST API 名 | わかりやすいラベル | 説明 |
| --- | --- | --- |
| address | Address | リードの住所 |
| annualRevenue | 年間売上高 | リードの会社の年間売上高 |
| anonymousIP | 匿名 IP | リードの最初の web 訪問時に記録された IP アドレス |
| billingCity | 請求先住所（市区町村） | リードの請求先住所の市区町村 |
| billingCountry | 請求先住所（国） | リードの請求先住所の国 |
| billingPostalCode | 郵便番号 | リードの請求先住所の郵便番号 |
| billingState | 請求先住所（都道府県） | リードの請求先住所の都道府県 |
| billingStreet | 請求先住所 | リードの会社の請求先住所 |
| city | 市区町村 | リードの市区町村 |
| company | 企業名 | リードの会社名 |
| country | 国 | リードの国 |
| dateOfBirth | 生年月日 | リードの生年月日 |
| department | Department | リードの会社の部門 |
| doNotCall | 電話連絡拒否 | リードの電話連絡拒否の環境設定 |
| doNotCallReason | 電話連絡拒否の理由 | リードの電話連絡拒否の環境設定の説明 |
| メール | メールアドレス | リードのメールアドレス。 リードレコードの標準 Marketo キーフィールド |
| fax | FAX 番号 | リードの FAX 番号 |
| firstName | 名前（名） | リードの名前（名） |
| industry | 業種 | リードの業界 |
| inferredCompany | 推測される会社 | リードの最初の web 訪問の逆 IP 検索によって推測される会社名 |
| inferredCountry | 推測される国 | リードの最初の web 訪問の逆 IP 検索によって推測される国 |
| lastName | 名前（姓） | リードの名前（姓） |
| leadRole | Role | リードの会社でのロール |
| leadScore | リードのスコア | キャンペーンとプログラムのスコアリングによってリードに付与される整数スコア |
| leadSource | リードのソース | リードの元となるソースを記録するフィールド |
| leadStatus | リードのステータス | リードの現在のマーケティング／販売ステータスを記録するフィールド |
| mainPhone | 代表電話 | リードの会社の代表電話番号 |
| jigsawContactId | Marketo Data.com ID | リードの Data.com ID（使用可能な場合） |
| jigsawContactStatus | Marketo Data.com ステータス | リードの Data.com ステータス（使用可能な場合） |
| middleName | ミドルネーム | リードのミドルネーム |
| mobilePhone | 携帯電話番号 | リードの携帯電話番号 |
| numberOfEmployees | 従業員数 | リードの会社の従業員数 |
| phone | 電話番号 | リードの電話番号 |
| postalCode | 郵便番号 | リードの郵便番号 |
| rating | リード評価 | リードのマーケティング／セールス評価 |
| salutation | 敬称 | リードの好ましい挨拶、つまりミスター、ミス…などです |
| sicCode | SIC コード | リードの会社の標準産業分類コード |
| site | Site |  |
| state | State | リードの都道府県 |
| title | Job Title | リードの職位 |
| unsubscribed | 配信停止完了 | リードのメール登録解除済みステータス。 部分的にシステムで管理されます。 true に設定すると、運用以外のメールの受信が防止されます。 |
| unsubscribedReason | 登録解除の理由 | リードの登録解除済みステータスの理由。 部分的にシステムで管理されます。 リードが Marketo のメールから直接登録解除された場合、メール情報が入力されます。 |
| website | Web サイト | リードの会社の web サイトの URL |
| createdAt | 作成日時 | リードレコードの作成日時。 システムが管理します |
| updatedAt | 更新日時 | リードレコードを最後に更新した日時。 システムが管理します |
| emailInvalid | メール無効 | メール無効ステータス。 true に設定すると、そのアドレスへのすべてのメールがブロックされます。 メールが無効であることを示すバウンスは、このフィールドを自動的に true に設定します。 |
| emailInvalidCause | メール無効の理由 | メール無効ステータスの理由。 メール無効を true に設定されている場合、原因となるバウンスメッセージがこのフィールドに記録されます。 |
| inferredCity | 推測される市区町村 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの市区町村。 |
| inferredMetropolitanArea | 推測される都市圏 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの都市圏。 |
| inferredPhoneAreaCode | 推測される市外局番 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの市外局番。 |
| inferredPostalCode | 推測される郵便番号 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの郵便番号。 |
| inferredStateRegion | 推測される都道府県／地域 | リードの最初の web 訪問の逆 IP 検索によって推測されるリードの都道府県／地域。 |
| isAnonymous | 匿名 | リードレコードの匿名ステータス。 システムが管理します。 |
| priority | 優先度 | リードのセールスインサイトの優先度。 システムが管理します。 |
| relativeScore | 相対スコア | リードのセールスインサイトの相対スコア。 システムが管理します。 |
| urgency | 緊急度 | リードのセールスインサイトの緊急度。 システムが管理します。 |
