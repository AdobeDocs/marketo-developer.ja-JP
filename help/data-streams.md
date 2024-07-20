---
title: データストリーム
description: データストリームの概要
exl-id: 5617b6a5-ebc8-4d97-a290-e3b87f83e360
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 2%

---

# データストリーム

アドビのお客様のマーケティング組織は、ビジネスを常に把握し、競争力を高めるために、タイムリーで焦点を当てたマーケティングキャンペーンに依存しています。 ペースの速い意思決定をサポートし、迅速に戦略的な変化を可能にするには、フォーカスされたターゲット設定されたキャンペーンを提供する重要な意思決定をサポートし、推進するデータを持つことが重要です。 また、Marketo Engage内外の顧客セグメントのレベルでマーケティング活動を行っているお客様もいます。 このような様々な取り組みをサポートするために、Marketoでは、ほぼリアルタイムでデータストリームから大量のデータを取得する機能を開発しました。

ほぼリアルタイムのデータというメリットの他に、製品に関連するメリットがあります。

- 代わりにストリーミングが使用されるので、API 制限のボトルネックを軽減します。
- API 制限のシナリオを減らし、生成されるアラートメッセージを減らします。
- データストリーミング機能が原因で、はデータを抽出するために一括書き出しを実行する必要があります。

データストリームは、[Marketo Engageパフォーマンス層パッケージ ](https://nation.marketo.com/t5/product-documents/marketo-engage-performance-tiers/ta-p/328835) を購入したユーザーが利用できます。

## リードアクティビティデータストリームの概要

リードアクティビティデータストリームは、監査トラッキングのリードアクティビティのほぼリアルタイムのストリーミングを提供します。大量のリードアクティビティを顧客の外部システムに送信できます。 ストリームを使用すると、リード関連のイベントや使用パターンを効果的に監査し、様々なタイプのリードイベントに基づいて、リードの変化やトリガープロセスおよびワークフローに関するビューを提供できます。 購読してストリーム経由で送信できるアクティビティタイプは 144 以上あります。

ストリーミングされたリードデータのタイプ：

1. リード変更 – すべてのフィールドと新しいリードに関するすべての変更
1. リードアクティビティ – ドキュメントに説明されているすべてのリードアクティビティタイプ
1. 削除されたリード
1. リード上のすべてのカスタムオブジェクト （必要な場合）。 この時点ではすべてか何かです。

これにより、リードの変化に対するビューを提供することで、顧客はマーケティング戦略全体をより迅速に意思決定し、より焦点を絞ったターゲットキャンペーンを作成できます。 一般的なユースケースを次に示します。

- カスタムアラート：一貫性のない条件で特定のリードが見つかった場合は、そのリードをリストに追加できます。 アクティビティストリームはこれらを取得し、顧客の「リストに追加」アクティビティを後続のアクションにプッシュできます。
- ML モデルの強化：一部のお客様は、アクティビティインサイトを使用するスコアリングモデルを構築し、Marketoにフィードバックしたり、必要に応じて独自の内部スコアリングモデルで使用したりすることを計画しています。 リードをスコアリングすると、お客様はMarketoに通知して、キャンペーン育成に顧客を追加することでスコアリングを向上させることができます。

ストリーミングアクティビティのリスト：

| AchieveGoalInReferral | ClickPredictiveContent | ReceivedForwardToFriendEmail |
|--- |--- |--- |
| リストに追加 | ClickRTPCallToAction | ReceiveSalesEmail |
| AddToNurture | ClickSalesEmail | ReferToSocialApp |
| AddToOpportunity | ClickSharedLink | リストから削除 |
| AddToSalesCampaign | ConvertLead | 商談から削除 |
| CallWebhook | DeleteLead | RequestCampaign |
| ChangeDataValue | DisqualifySweepstakes | SalesEmailBounced |
| ChangeLeadPartition | EarnEntryInSocialApp | SendAlert |
| ChangeNurtureCadence | EmailBounced | SendEmail |
| ChangeNurtureTrack | EmailBouncedSoft | SendSalesEmail |
| ChangeOwner | EmailDelivered | SentForwardToFriendEmail |
| ChangeProgramData | EnrichWithDataDotCom | SFDCActivity |
| ChangeProgramMemberData | EnterSweepstakes | ShareContent |
| ChangeRevenueStage | FillOutFacebookLeadAdsForm | SignUpForReferralOffer |
| ChangeRevenueStageManually | FillOutForm | SyncLeadToMicrosoft |
| ChangeScore | InterestingMoment | SyncLeadToSFDC |
| ChangeSegment | MergeLeads | UnsubscribeEmail |
| ChangeStatusInProgression | NewLead | UpdateOpportunity |
| ChangeStatusInSalesCampaign | OpenEmail | VisitWebPage |
| ClickEmail | OpenSalesEmail | VoteInPoll |
| ClickLink | PushLeadToMarketo | WinSweepstakes |

カスタムオブジェクトをストリーミングする必要がある場合は、リード関連のすべてのカスタムオブジェクトである必要があります。 現時点ではどの方が望ましいかを選択する方法はない。

## ユーザー監査データストリームの概要

ユーザー監査データストリームは、&#x200B;ユーザーによるアセットの変更をほぼリアルタイムで監査トラッキングします。 これにより、アセットイベントを効果的に監査し、ユーザーの変更のビューを提供し、様々なタイプの監査イベントに基づいてプロセスまたはワークフローをトリガーすることができます。 ほぼリアルタイムで、アセットの変更内容が、Adobe I/Oイベントを介して設定可能なエンドポイントに送信されます。 監査イベントはアセットタイプ別に分類され、重要な監査イベントを登録できます。

このストリームの購読の良いユースケースは次のとおりです。

- 複数のマーケティングシステムを使用する場合の変更のトラッキング：Salesforce などの別のシステムで何らかのレベルのマーケティングアクティビティを実行してから、リードをMarketoに渡す顧客もいます。 リードは時々更新され、前後に同期されるので、最近の変更を加えたシステムを追跡することが重要です。

ストリーミングユーザー監査イベントのリスト：

| COMPONENT | イベントタイプリスト |
|--- |--- |
| デフォルトのプログラム | クローン、作成、削除、チャネル編集、エクスポート、プログラム設定の変更、プログラムトークンの変更、名前の変更 |
| メール | 承認、複製、作成、削除、編集、移動、名前を変更、未承認 |
| メールのバッチ送信プログラム | 承認、childUpdate、複製、作成、削除、編集、チャネルの編集、プログラムスケジュールの変更、プログラム設定の変更、プログラムトークンの変更、名前の変更、承認解除 |
| メールテンプレート | 承認、複製、作成、削除、draftCreate、draftDiscard、編集、名前を変更、未承認 |
| エンゲージメントプログラム | クローン、作成、削除、チャネルの編集、プログラム設定の変更、プログラムストリームの変更、プログラムトークンの変更、名前の変更 |
| イベントプログラム | クローン、作成、削除、チャネルの編集、プログラム スケジュールの変更、プログラム設定の変更、プログラム トークンの変更、名前の変更 |
| フォルダー | 作成、削除、編集、名前変更 |
| フォーム | 承認、複製、作成、削除、draftCreate、編集、移動、名前変更 |
| フォーム -> ランディングページフォーム | 作成、複製、編集、削除、承認、名前変更 |
| ランディングページ | 承認、複製、作成、削除、draftDiscard、編集、名前を変更、未承認 |
| ランディングページテンプレート | 承認、複製、作成、削除、draftCreate、draftDiscard、編集、名前を変更、未承認 |
| スマートリスト | 複製、作成、削除、編集、エクスポート、スマート リスト設定の変更、名前の変更 |
| マーケティング フォルダ | 作成、編集、削除 |
| 育成プログラム | クローン、作成、削除、チャネル編集、プログラム設定の変更、プログラムストリームの変更、プログラムトークンの変更、名前の変更 |
| セグメント | 作成、削除、編集、名前変更 |
| セグメント化 | 承認，作成，削除，draftCreated, draftDiscarded，名前を変更，未承認 |
| スマートキャンペーン | 中止、有効化、複製、作成、無効化、削除、キャンペーンスケジュールの変更、フローステップアクションの変更、スマートリスト設定の変更、移動、名前の変更 |
| スニペット | 承認、ドラフトなしで承認、複製、作成、削除、編集、名前を変更、未承認 |
| 管理 UI/起動ポイント/統合 | 作成、削除、編集 |
| 管理 UI/ユーザー | 作成、編集、削除（API のみのユーザーで同じ） |
| 管理者ログイン/ユーザー | ログイン成功、ログイン失敗 |
| プログラム/メールバッチプログラム | アセット API を編集（選択したメールアドレスの変更用） |
| プログラム/マーケティングプログラム | 作成、クローン |

ユーザー監査イベントの例：

```json
{
    "event_id": "a1b2c3d4-zyxw-9876-9z8y-a1b2c3d4e5f6",
    "event": {
        "specversion": "1.0",
        "id": "b77c743a-8e28-40f2-8aab-9541bbc85e68",
        "type": "com.adobe.platform.marketo.audit.user.email",
        "source": "https://www.marketo.com",
        "time": "2020-05-28T19:20:47.28Z",
        "datacontenttype": "application/json",
        "dataschema": "V1.0",
        "data": {
            "componentId": 232459,
            "componentType": "Email",
            "eventAction": "approve",
            "munchkinId": "123-ABC-456",
            "imsOrgId": "ADOBEORGID@AdobeOrg",
            "user": 253,
            "userId": "example@marketo.com"          
        }
    }
}
```

## 通知データストリームの概要

通知データストリームは、Marketo Engageのパフォーマンスレベルの製品の一部として利用できます。

現在、Marketoの通知センターは、通知をメールアドレスに送信するように設定できます。 通知データストリームを使用すると、通知イベントを介して設定可能なエンドポイントにAdobe I/Oを直接送信できます。 通知は現在 UI から提供されており、画面の右上にあるオレンジ色のベルによって参照できます。このストリームはこれらの通知を受け取り、ストリームを介して送信します。

通知イベントのリスト：

| COMPONENT | イベントタイプリスト |
|--- |--- |
| 通知 | キャンペーン中止、キャンペーン失敗、ナーチャリング （プログラムが使い果たされました）、Salesforce 同期の失敗、テストグループ （A/B テスト結果）、Web サービス （日割り当て） |

通知イベントの例：

```json
{
    "event_id": "a1b2c3d4-zyxw-9876-9z8y-a1b2c3d4e5f6",
    "event": {
        "specversion": "1.0",
        "type": "com.adobe.platform.marketo.notification.campaign_abort",
        "source": "https://www.marketo.com",
        "time": "2021-05-27T10:22:37.489-5:00",
        "datacontenttype": "application/json",
        "dataschema": "V1.0",
        "data": {
            "componentType": "campaign_abort",
            "subType": "user_campaign_abort",
            "eventAction": {
                "campaignId":1234,
                "userId":"example@marketo.com",
            }
            "imsOrgId":"ADOBEORGID@AdobeOrg",
            "munchkinId":"123-ABC-456"
        }
    }
}
```

## 技術的詳細

この節では、必要な操作、各ストリームでストリーミングデータを接続および受信する方法に関するガイドラインを示します。 それぞれに対して、ある程度のコーディングと設定が必要です。

### リードアクティビティデータストリーム

リードアクティビティストリームは、Marketoのリードアクティビティイベントのほぼリアルタイムのストリーミングを提供し、設定可能な属性で購読しているアクティビティタイプの変更を送信します。

- デフォルトでは、データのプッシュ頻度は 2 秒ごとに行われます。
- サブスクリプションあたり 100～500 のバッチ。
- 顧客の REST サービスのタイムアウトは 20 秒で、3 分ごとに 3 回の再試行が行われ、成功すると自動的に有効になります。 それ以外の場合は、一時停止されます。 一時停止したサービスは、手動でプロビジョニングを解除しない限り、3 分ごとに再有効化を試みます。
- キュー内のデータ保持は最大 7 日間です。

リードアクティビティデータストリームを実装するために、お客様が従う手順は次のとおりです。

1. パブリックインターネットから JSON 本文でPOSTリクエストを受け取ることができる HTTP エンドポイントを公開します。 アクティビティ プッシュデータストリームは、次に対してリクエストを送信します。
1. Adobeに次の情報を提供します。
   1. サブスクリプションのMarketo Munchkin ID
   1. 手順 1 のエンドポイントの URL
   1. 受け取るアクティビティタイプ（上記の完全なリスト）
   1. 認証の手段。これにより、顧客はリクエストが正当であることを確認できます。 次のいずれか：
      1. OAuth 用の ID プロバイダー URL、クライアント ID およびクライアント秘密鍵 [ クライアント資格情報認証 ](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)
      1. API トークン。リードアクティビティデータストリームから送信されるリクエストに、クエリパラメーターまたは認証ヘッダー（顧客が選択）で含めることができます

次に、Adobeによってデータストリームが有効になり、顧客はデータストリームでデータの受信を開始します。

典型的なリードアクティビティデータストリーム呼び出しの UML 図：

![ リードアクティビティのデータストリーム図 ](assets/lead-activity-data-stream.png)

URL エンドポイントの作成例：

```javascript
/*
Copyright 2022 Adobe
All Rights Reserved.

NOTICE: Adobe permits you to use, modify, and distribute this file in
accordance with the terms of the Adobe license agreement accompanying
it.
*/
constexpress=require('express')
constwinston=require('winston');
constport=3000

constapp=express().use(express.json())

constlogger=winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  defaultMeta: {service: 'activity-stream-consumer-example'},
  transports: [
    // - Write all logs with level `error` and below to `error.log`
    newwinston.transports.File({filename: 'error.log',level: 'error'}),
    // - Write all logs with level `info` and below to `combined.log`
    newwinston.transports.File({filename: 'combined.log'}),
    newwinston.transports.Console({format: winston.format.simple()})
  ],
});

app.get('/',(req,res)=>{
  logger.info(JSON.stringify(req.query))
  res.sendStatus(200)
})

app.post('/',(req,res)=>{
  logger.info(JSON.stringify(req.body))
  res.sendStatus(200)
})

app.listen(port,()=>{
  logger.info(`app listening on port ${port}`)
})
```

Marketo リードアクティビティデータストリームを使用するアプリケーションのコードサンプルは、[ こちら ](https://github.com/ihgrant/activity-stream-consumer-example) を参照してください。

### ユーザー監査データストリームおよび通知データストリーム

ユーザー監査イベントはAdobe IO に送信され、Adobe IDにログインして使用できます。 手順は次のとおりです。

1. お客様は、次のAdobeを提供します。
   1. Adobe ID
   1. サブスクリプションのMarketo Munchkin ID
1. 顧客は、イベントを通常は Webhook の形式で使用するように REST エンドポイントを公開します。
1. これが指定されると、Adobeは、顧客のサブスクリプション用にストリームを有効にします。
1. 次に、お客様はAdobe IO でストリームを設定します（手順は提供されます）。
   1. このステップにはAdobe組織が必要です
   1. Adobe組織ユーザーには、開発者またはシステム管理者の役割が必要です

Adobe IO を設定するには、公開ドキュメントの節 [Adobe IO を使用したMarketo ユーザー監査データストリームの設定 ](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-user-audit-data-stream-setup/) を参照してください。

### Marketoでのユーザー監査データストリームの設定

ユーザー監査データストリームは、現在、他の 3 つのデータストリームと共にパフォーマンスパッケージの一部として使用できます。 パッケージの詳細については、[ 製品説明ページ ](https://helpx.adobe.com/legal/product-descriptions/adobe-marketo-engage-product-description.html) で製品の制限事項や機能を確認してください。

### Adobe I/Oの設定

[Adobe I/Oイベントの概要を参照してください ](https://developer.adobe.com/runtime/docs/guides/getting-started/)

このユースケースの基本的な手順については、[console.adobe.io](https://developer.adobe.com/console) 以降を参照してください。

プロンプトが表示されたら、「**[!UICONTROL 新規プロジェクトを作成]**」または「**[!UICONTROL イベントを追加]**」を選択します。

### 新しいプロジェクトの基本を学ぶ

Adobe サービスの使用を開始するには、API、イベント、ランタイムを追加し、[ ドキュメント ](https://developer.adobe.com/runtime/docs/) を参照してください。

## 公開ドキュメント

- [Marketo データストリーム ](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-data-streams/)
- [Adobe IO イベントと Webhook の概要 ](https://developer.adobe.com/events/docs/guides/)
- [ データストリームブログ ](https://blog.developer.adobe.com/introducing-the-adobe-marketo-engage-data-streams-61198b567fbb)
