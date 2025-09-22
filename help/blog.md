---
title: ブログアーカイブ
description: 2014 年から 2023 年までのMarketo Developers ブログのアーカイブ
exl-id: d7ae88dd-9938-4957-9798-db43090dab4e
source-git-commit: 36e768d562e6f69aeb70a83253dfcf41653f217a
workflow-type: tm+mt
source-wordcount: '61712'
ht-degree: 1%

---

# ブログアーカイブ

>[!INFO]
>
>これは、2014 年から 2023 年にわたるMarketoのブログのアーカイブです。 これは、履歴参照としてのみ提供されています。
>&#x200B;>一部の情報が古くなっている可能性があります。  最新の機能については、常に最新のドキュメントを確認してください。
>

>[!IMPORTANT]
>SOAP API は非推奨（廃止予定）となっており、2026 年 1 月 31 日（PT）以降は使用できなくなります。 すべての新しい開発はMarketo REST API を使用して行う必要があり、サービスが中断されないように、既存のサービスはその日までに移行する必要があります。 SOAP API を使用するサービスがある場合は、[SOAP API Migration Guide](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/migration) を参照して、移行方法を確認してください。
>

>[!IMPORTANT]
>`access_token` クエリパラメーターを使用した認証のサポートは、2026 年 1 月 31 日（PT）に削除されます。 プロジェクトでクエリパラメーターを使用してアクセストークンを渡す場合は、[Authorization ヘッダー ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/authentication#using-an-access-token) を使用するように直ちに更新する必要があります。 新しい開発では、Authorization ヘッダーのみを使用する必要があります。
>

## このたびは、Marketo Developer ブログをご利用いただき、誠にありがとうございます

Marketoの開発者向けサイトへようこそ。 Marketoでは、マーケターがこれまで以上に成功するための新機能をリリースするのに非常に忙しく取り組んでいます。 現在のマーケターは、驚異的な開発者コミュニティによってサポートされています。 このブログは、急速に進化する最新のマーケターのニーズをサポートする web 開発者とソフトウェアエンジニアを対象としています。 Marketo Platform の進化に合わせて、新しい統合オプションと API バージョンのアップデートがリリースされるたびに、こちらからお知らせします。 また、Marketo Platform との統合に関するコードサンプルとベストプラクティスを紹介する新しい一連のハウツー記事も導入する予定です。 このシリーズの最初の記事では、API を使用して、Marketo内に保存されている人（顧客/連絡先/リード）に関する情報を効率的に取得する方法を説明します。 最新の情報を入手するには、上記のフォームを使用して購読してください。 新しい記事が公開されると、更新情報をメールでお知らせします。

Posted on _2014-03-06_ by _David_

## 2014 年 1 月リリースアップデート

### Forms 2.0

Forms 2.0 を使用すると、マーケターは、プログラミングの知識がなくても、美しく安定した柔軟な web フォームを作成できます。 大幅に改善されたエディター、条件付きロジック、堅牢なデザインに加えて、web サイトの任意のページにMarketo forms を埋め込むのが、これまでより簡単になりました。 開発者は、JavaScriptを使用してコア機能を拡張できます。使用例は次のとおりです。

* 送信に成功した後にフォームを非表示にして、訪問者がフォームに入力した後もページに残るようにする
* カスタムビジネスロジックに基づいた送信に基づくカスタムエラーメッセージの表示
* ライトボックススタイルダイアログボックスでのフォームの表示

開発者向けドキュメントは [ こちら ](/help/javascript-api/forms-api-reference.md) で参照できます。

### SOAP API バージョン 2_3 が利用可能になりました

* [getLeadChanges:](/help/soap-api/getleadchanges.md) リクエストフィールド `activityNameFilter` が導入されました
* [ListOperation:](/help/soap-api/listoperation.md) 削除された要求フィールド `skipActivityLog`

**メモ：** SOAP API リビジョンには下位互換性があります

Posted on _2014-01-26_ by _Travis Kaufman_

## Zapier Part II:Marketo統合に関するお知らせ

以前の投稿では、Zapier を使用して外部データソースをMarketoと統合する方法について説明しました。 この投稿では、Marketoと他のアプリを統合するために、独自の Zapier ワークフロー（または「Zap」）をゼロから構築するための実践的なアプローチを紹介しました。 Marketoで Zapier を使用するアイデアは気に入りますが、使い始める際にサポートが必要ですか？ 良いニュース！ Zapier は、すぐに作業を開始できるMarketo向け Zaps の例をいくつかリリースしました。

* 新しいリードをキャプチャ
* 顧客の育成
* 連絡先情報の配布
* 新しい見込み客への反応

これらの例に加えて、[Marketo統合 ](https://zapier.com/apps/marketo/integrations) ページで Zapier 上の数百の他のアプリを参照し、独自の自動ワークフローを数分で作成できます。 コーディングは不要です。 時間を節約し、自動化で手作業を行えるようにします。 クリエイティブになりましょう。 空は限界だ！

Posted on _2016-06-01_ by _David_

## API を使用したMarketoからのお客様および見込み客情報の取得

`getLead` およびSOAP API を使用して、Marketo内に保存されている顧客や見込み客に関する情報 [`getMultipleLeads`](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads) 取得できます。 顧客や見込み客に関する情報が更新されたり、Marketoに新しいレコードが作成されたりしたときに別のシステムが常に更新されるように、この情報を繰り返し抽出することが多くの場合、望まれます。 Marketoで更新をポーリングするために繰り返し実行されるコードサンプルを示します。 次の図は、設定された定期的なタイマーで行われる API 呼び出しを示しています。 ユースケースによっては、定期タイマーを設定して、以下のコードを 10 分ごとに実行することができます。

[`getMultipleLeads`](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads) の最初の呼び出しでは、時間範囲、batchSize および返されるフィールドを設定します。 指定された時間範囲内に更新されたMarketo内のすべてのリードは、指定された batchSize よりも多くのレコードが使用可能な場合、streamPosition と共に返されます。

**getMultipleLeads の最初の呼び出しのSOAP リクエスト：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:paramsGetMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <leadSelector xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ns2:LastUpdateAtSelector">
    <latestUpdatedAt>2014-02-13T11:51:08.710-08:00</latestUpdatedAt>
    <oldestUpdatedAt>2014-02-12T11:51:08.713-08:00</oldestUpdatedAt>
  </leadSelector>
  <batchSize>2</batchSize>
  <includeAttributes>
    <stringItem>FirstName</stringItem>
    <stringItem>LastName</stringItem>
    <stringItem>Email</stringItem>
  </includeAttributes>
</ns2:paramsGetMultipleLeads>
```

**getMultipleLeads への最初の呼び出しからのSOAPの応答：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:successGetMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <result>
 <returnCount>2</returnCount><remainingCount>24</remainingCount><newStreamPosition>id:1089965:to:1392234668:tl:1392321068:os:2:rc:24</newStreamPosition><leadRecordList>
      <leadRecord>
        <Id>84105</Id>
        <Email>eimang@marketo.com</Email>
        <ForeignSysPersonId xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
        <ForeignSysType xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
        <leadAttributeList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true">
          <attribute>
            <attrName>FirstName</attrName>
            <attrType>string</attrType>
            <attrValue>French</attrValue>
          </attribute>
          <attribute>
            <attrName>LastName</attrName>
            <attrType>string</attrType>
            <attrValue>Lead</attrValue>
          </attribute>
        </leadAttributeList>
      </leadRecord>
      <leadRecord>
        <Id>1089965</Id>
        <Email>t@t.com</Email>
        <ForeignSysPersonId xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
        <ForeignSysType xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
        <leadAttributeList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true">
          <attribute>
            <attrName>FirstName</attrName>
            <attrType>string</attrType>
            <attrValue>George</attrValue>
          </attribute>
          <attribute>
            <attrName>LastName</attrName>
            <attrType>string</attrType>
            <attrValue>of the Jungle</attrValue>
          </attribute>
        </leadAttributeList>
      </leadRecord>
    </leadRecordList>
  </result>
</ns2:successGetMultipleLeads>
```

`<remainingCount/>` の値が 0 より大きい限り、前の呼び出しで返された `getMultipleLeads` の値を `<newStreamPosition/>` パラメーターに渡すことによって、以降の呼び出しで `<streamPosition/>` を呼び出し、残りの値をページ分割します。 **後続の getMultipleLeads 呼び出しのSOAP リクエスト：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:paramsGetMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <leadSelector xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ns2:LastUpdateAtSelector">
    <latestUpdatedAt>2014-02-13T11:51:08.710-08:00</latestUpdatedAt>
    <oldestUpdatedAt>2014-02-12T11:51:08.713-08:00</oldestUpdatedAt>
  </leadSelector><streamPosition>id:1089965:to:1392234668:tl:1392321068:os:2:rc:24</streamPosition><batchSize>2</batchSize>
  <includeAttributes>
    <stringItem>FirstName</stringItem>
    <stringItem>LastName</stringItem>
    <stringItem>Email</stringItem>
  </includeAttributes>
</ns2:paramsGetMultipleLeads>
```

このロジックは、`<remainingCount/>` が 0 より大きい限り継続されます。 **上記のシナリオを実行する Java プログラムのサンプルを以下に示します**。

```java
import com.marketo.mktows.\*;
import java.net.URL;
import javax.xml.namespace.QName;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.GregorianCalendar;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;
import javax.xml.datatype.DatatypeFactory;
import javax.xml.datatype.XMLGregorianCalendar;

public class GetMultipleLeads {
  public static void main(String[] args) {
    System.out.println("Executing GetMultipleLeads");
        try {
        URL marketoSoapEndPoint = new URL("CHANGE ME" + "?WSDL");
        String marketoUserId = "CHANGE ME";
        String marketoSecretKey = "CHANGE ME";
        QName serviceName = new QName("<http://www.marketo.com/mktows/>",
        "MktMktowsApiService");
        MktMktowsApiService service = new
        MktMktowsApiService(marketoSoapEndPoint, serviceName);
        MktowsPort port = service.getMktowsApiSoapPort();

        // Create Signature
        DateFormat df = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
        String text = df.format(new Date());
        String requestTimestamp = text.substring(0, 22) + ":" +         text.substring(22);
        String encryptString = requestTimestamp + marketoUserId ;

        SecretKeySpec secretKey = new         SecretKeySpec(marketoSecretKey.getBytes(), "HmacSHA1");

        Mac mac = Mac.getInstance("HmacSHA1");
        mac.init(secretKey);
        byte[] rawHmac = mac.doFinal(encryptString.getBytes());
        char[] hexChars = Hex.encodeHex(rawHmac);
        String signature = new String(hexChars);

        // Set Authentication Header
        AuthenticationHeader header = new AuthenticationHeader();
        header.setMktowsUserId(marketoUserId);
        header.setRequestTimestamp(requestTimestamp);
        header.setRequestSignature(signature);

        // Create Request
        ParamsGetMultipleLeads request = new ParamsGetMultipleLeads();

        // Build Request Using LastUpdateAtSelector
        LastUpdateAtSelector leadSelector = new LastUpdateAtSelector();
        GregorianCalendar gc = new GregorianCalendar();
        gc.setTimeInMillis(new Date().getTime());
        gc.add( GregorianCalendar.DAY_OF_YEAR, -20);
        DatatypeFactory factory = DatatypeFactory.newInstance();
        ObjectFactory objectFactory = new ObjectFactory();
        JAXBElement<XMLGregorianCalendar> until =         objectFactory.createLastUpdateAtSelectorLatestUpdatedAt(factory.newXMLGregorianCalendar(gc));

        GregorianCalendar since = new GregorianCalendar();
        since.setTimeInMillis(new Date().getTime());
        since.add( GregorianCalendar.DAY_OF_YEAR, -21);
        leadSelector.setOldestUpdatedAt(factory.newXMLGregorianCalendar(since));
        leadSelector.setLatestUpdatedAt(until);
        request.setLeadSelector(leadSelector);

        ArrayOfString attributes = new ArrayOfString();
        attributes.getStringItems().add("FirstName");
        attributes.getStringItems().add("LastName");
        attributes.getStringItems().add("Email");
        request.setIncludeAttributes(attributes);

        JAXBElement<Integer> batchSize = new
        ObjectFactory().createParamsGetMultipleLeadsBatchSize(2);
        request.setBatchSize(batchSize);

        SuccessGetMultipleLeads result = null;

        int count = 0;

        do {
        if (count > 0) {
        // Set the streamPosition on subsequent calls to paginate
        through large result sets
        String pos = result.getResult().getNewStreamPosition();
        JAXBElement<String> streamPos = new
        ObjectFactory().createParamsGetMultipleLeadsStreamPosition(pos);
        request.setStreamPosition(streamPos);
        }

        JAXBContext context =
        JAXBContext.newInstance(ParamsGetMultipleLeads.class);
        Marshaller m = context.createMarshaller();
        m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
        System.out.println("REQUEST:");
        m.marshal(request, System.out);
        result = port.getMultipleLeads(request, header);
        System.out.println("RESPONSE:");
        m.marshal(result, System.out);
        count = result.getResult().getReturnCount();
        } while (result.getResult().getRemainingCount() > 0);
        }

        catch(Exception e) {
        // Update to include appropriate retry/error handling
        e.printStackTrace();
        }

  }

}
```

### ヒントとテクニック

Marketoから大量の連絡先を抽出する場合は、次のパラメーターに従って API リクエストを調整することをお勧めします。

* `<includeAttributes/>`：システムとの同期を保つために、関心のあるフィールドのみをリクエストすることをお勧めします。 これにより、応答のペイロードが減少し、クエリのパフォーマンスが向上します。
* `<batchSize/>`：この API は、1 回の呼び出しで返される最大 1000 個のレコードをサポートしています。 この値を 500 レコードに調整すると、応答のペイロードも削減されます。
* `<LastUpdatedAtSelector/>`：日付範囲を制限するには、`<oldestUpdatedAt/>` と `<latestUpdatedAt/>` パラメーターの両方を設定することをお勧めします。 例えば、1 年分のデータに対して 1 回のリクエストを行う代わりに、 API 呼び出しを分割して、より小さな日付範囲をリクエストします。

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _2014-03-05_ by _Travis Kaufman_

## 2014 年 2 月リリースアップデート

### SOAP API の更新

* [syncMObjects](/help/soap-api/syncmobjects.md)：既存のプログラムのタグとチャネルを追加および更新できるようになりました。

更新は [2_3 WSDL](http://app.marketo.com/soap/mktows/2_3?WSDL) に組み込まれます。

Posted on _2014-02-26_ by _Travis Kaufman_

## 2014 年 3 月リリースアップデート

### SOAP API の更新

* [syncLead](/help/soap-api/synclead.md) および [syncMultipleLeads](/help/soap-api/syncmultipleleads.md) のパフォーマンスの向上

更新は [2_3 WSDL](http://app.marketo.com/soap/mktows/2_3?WSDL) に組み込まれます。

Posted on _2014-03-20_ by _Travis Kaufman_

## 訪問者がフォームに入力したときに匿名訪問者アクティビティを結合

「ビジネスロジックに基づく匿名訪問者アクティビティのキャプチャ」というタイトルのブログ投稿では、カスタムイベントに基づいてMarketoで匿名リードレコードを作成する方法について説明しました。 このブログ投稿では、その投稿を基に、ユーザーの連絡先情報を受け取った後、匿名のリードレコードを既知のユーザーに関連付けます。 Marketoの [Munchkin トラッキングコード ](/help/javascript-api/lead-tracking.md) は、web サイトへの訪問を追跡するのに役立ちます。 Munchkin トラッキングコードを持つ web サイトのページに初めてアクセスしたユーザーは、Marketoによって匿名のリードが作成され、ブラウザーの Cookie を使用してトラッキングされます。 ユーザーが識別すると、そのユーザーは既知のリードになり、ブラウザーの cookie に関連付けられた履歴がMarketoのリードレコードに結合されます。 **匿名リードは次のユーザーの場合に作成されます。**

1. Marketoのランディングページを初めて訪問
1. Munchkin トラッキングコードを持つページを訪問
1. Marketo メールの「Web ページとして表示」リンクをクリックします

**匿名のリードは、次の場合に新しいリードまたは既存の既知のリードに結合されます。**

1. Marketo メールへのリンクをクリックします
1. Marketo フォームに入力します
1. 次の手法の 1 つを使用して、匿名リードを既知のレコードに関連付けます。

ユーザーデータを送信したり、ブラウザーの web トラッキング cookie をMarketoの対応するユーザーレコードに関連付けたりするには、次のいずれかの方法を使用します。**ブラウザーサイド送信** ユースケースでブラウザーからのユーザーデータの送信が必要な場合は、バックグラウンドでフォーム送信を使用する必要があります。 **サーバーサイド送信** ブラウザーサイド送信が必要ない場合、REST API には、人物データ送信用の多くの方法と、Cookie を人物レコードに関連付けるための専用の方法が用意されています。

Posted on _2014-04-22_ by _Murta_

## 2014 年 4 月リリースアップデート

### Marketo Formsのセキュリティ更新

単一の IP アドレスからのフォーム投稿送信の数と頻度に制限が導入されました。 この制限は、プログラムによるフォーム送信の悪意のある使用から顧客を保護するために、1 分あたり 30 件の投稿で適用されるようになりました。 [syncLead API](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/leads/synclead) は、Marketoで新しい連絡先をプログラムで送信するための推奨される統合手段です。

Posted on _2014-04-29_ by _Travis Kaufman_

## フォーム投稿統合をMarketo API に置き換えます

Marketoを使用するマーケターは、特定の web フォームに入力した連絡先/リードの数に基づいて、特定のマーケティングキャンペーンの成功を関連付けるのが一般的な方法です。 マーケターは、新しいMarketo フォームを作成し、ランディングページに配置してから、Marketoでトリガーキャンペーンを設定し、そのフォームに入力したすべての連絡先をそのマーケティングプログラムの成果として関連付けるだけです。 （下のスクリーンショットを参照）。 キャンペーンの成功がフォームを入力するユーザーの外部にある場合でも、プログラムの成功を記録する際に同じアプローチを使用するのは自然な拡張です。 例えば、マーケターがプロモーションオファーを実行し、コンバージョンが電話で予約を取る場合などです。 見込み客は、プロセスのどの時点でもフォームに入力していません。 以下の記事では、Marketo syncLead API を使用して、新規の連絡先である場合は新しい連絡先を作成し、requestCampaign API を使用して特定のマーケティングプログラムの成功を記録する方法を示します。

Posted on _1970-01-01_ by _Travis Kaufman_

## Marketo API を使用したリードの削除

Marketo API を使用してリードを削除するとします。 これを実現するには、リードを削除するフローアクションが事前に定義されているキャンペーンで requestCampaign API を呼び出します。 最初に、スマートキャンペーンの作成方法、2 番目に、API を使用してキャンペーンを実行するためのトリガーの設定方法、3 番目に、フローアクションの一部としてリードの削除を定義する方法、4 番目に、このキャンペーンを実行するために使用するコードサンプルを示します。 **Marketoで新しいスマートキャンペーンを作成する方法** Marketoのスマートキャンペーンは、すべてのマーケティングアクティビティを実行します。 スマートキャンペーンでは、連絡先のスマートリストに対して実行する一連の自動アクションを設定できます。 リードを削除する場合は、以下に示すように、キャンペーンでトリガーを設定します。 まず、スマートキャンペーンを設定します。

1. 「マーケティングアクティビティ」で、プログラムを選択し、「新規」ドロップダウンで「新規ローカルアセット 1」をクリックします。 「スマートキャンペーン」をクリック
1. スマートキャンペーン名を入力し、「作成」「スマートキャンペーンにトリガーを追加」をクリックし**す。スマートキャンペーンにトリガーを追加すると、ライブイベント（この場合は requestCampaign API を介したリクエスト）に基づいて、スマートキャンペーンを 1 人のユーザーに対して一度に実行できます。
1. 「キャンペーンがリクエストされました」トリガーを検索し、キャンバスにドラッグ&amp;ドロップします。
1. トリガーで、「is」と「Web サービス API」を選択します。

**キャンペーンで「リードフローを削除」アクションを作成する方法** 上部のメニューで「フロー」をクリックします。 右側のメニューから「リードを削除」を検索し、中央にドラッグして、キャンペーンにトリガーとして追加します。 メモ：Marketoからのみリードを削除して CRM に残した場合、そのリードのデータが更新されると、そのリードはMarketoで再作成されます。  **requestCampaign API を呼び出すコードサンプル** Marketo インターフェイスでキャンペーンとトリガーを設定したら、API を使用してこのキャンペーンを実行する方法を示します。 最初のサンプルは XML リクエストで、2 番目は XML 応答で、最後のサンプルは XML リクエストの生成に使用できる Java コードサンプルです。 また、requestCampaign API を呼び出す際に使用するキャンペーン ID を見つける方法についても説明します。 また、API 呼び出しでは、事前にMarketo キャンペーンの ID を知っておく必要があります。 次のいずれかの方法を使用して、キャンペーン ID を決定できます。

1. [getCampaignsForSource](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCampaignsUsingGET) API の使用
1. ブラウザーでMarketo キャンペーンを開き、URL アドレスバーを確認します。 キャンペーン ID （4 桁の整数で表されます）は、「SC」の直後にあります。 たとえば、`https://app-stage.marketo.com/#SC**1025**A1` のように設定します。太字で示した部分は、キャンペーン ID 「1025」です。 requestCampaign のSOAP リクエスト

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809939944BFABAE58E5D27</mktowsUserId><requestSignature>48397ad47b71a1439f13a51eea3137df46441979</requestSignature><requestTimestamp>2013-08-01T12:31:14-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsRequestCampaign>
      <source>MKTOWS</source>
      <campaignId>4496</campaignId>
      <leadList>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>lead@company.com</keyValue>
        </leadKey>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>anotherlead@company.com</keyValue>
        </leadKey>
      </leadList>
    </ns1:paramsRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

requestCampaign に対するSOAP応答

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successRequestCampaign>
      <result>
        <success>true</success>
      </result>
    </ns1:successRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

上記のシナリオを実行する Java プログラムのサンプルを以下に示します。

```java
import com.marketo.mktows.*;
import java.net.URL;
import javax.xml.namespace.QName;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;


public class RequestCampaign {

    public static void main(String[] args) {
        System.out.println("Executing Request Campaign");
        try {
            URL marketoSoapEndPoint = new URL("CHANGE ME" + "?WSDL");
            String marketoUserId = "CHANGE ME";
            String marketoSecretKey = "CHANGE ME";

            QName serviceName = new QName("http://www.marketo.com/mktows/", "MktMktowsApiService");
            MktMktowsApiService service = new MktMktowsApiService(marketoSoapEndPoint, serviceName);
            MktowsPort port = service.getMktowsApiSoapPort();

            // Create Signature
            DateFormat df = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
            String text = df.format(new Date());
            String requestTimestamp = text.substring(0, 22) + ":" + text.substring(22);
            String encryptString = requestTimestamp + marketoUserId ;

            SecretKeySpec secretKey = new SecretKeySpec(marketoSecretKey.getBytes(), "HmacSHA1");
            Mac mac = Mac.getInstance("HmacSHA1");
            mac.init(secretKey);
            byte[] rawHmac = mac.doFinal(encryptString.getBytes());
            char[] hexChars = Hex.encodeHex(rawHmac);
            String signature = new String(hexChars);

            // Set Authentication Header
            AuthenticationHeader header = new AuthenticationHeader();
            header.setMktowsUserId(marketoUserId);
            header.setRequestTimestamp(requestTimestamp);
            header.setRequestSignature(signature);

            // Create Request
            ParamsRequestCampaign request = new ParamsRequestCampaign();

            request.setSource(ReqCampSourceType.MKTOWS);

            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Integer> campaignId = objectFactory.createParamsRequestCampaignCampaignId(4496);
            request.setCampaignId(campaignId);

            ArrayOfLeadKey leadKeyList = new ArrayOfLeadKey();
            LeadKey key = new LeadKey();
            key.setKeyType(LeadKeyRef.EMAIL);
            key.setKeyValue("lead@company.com");

            LeadKey key2 = new LeadKey();
            key2.setKeyType(LeadKeyRef.EMAIL);
            key2.setKeyValue("anotherlead@company.com");

            leadKeyList.getLeadKeies().add(key);
            leadKeyList.getLeadKeies().add(key2);

            JAXBElement<ArrayOfLeadKey> arrayOfLeadKey = objectFactory.createParamsRequestCampaignLeadList(leadKeyList);
            request.setLeadList(arrayOfLeadKey);

            SuccessRequestCampaign result = port.requestCampaign(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessRequestCampaign.class);
            Marshaller m = context.createMarshaller();
            m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
            m.marshal(result, System.out);

        }
        catch(Exception e) {
            e.printStackTrace();
        }
    }
}
```

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _2014-05-16_ by _Murta_

## Munchkin AP を使用したカスタムアクティビティトラッキング – 

Marketoでカスタムアクティビティを追跡するとします。 例えば、web ページにビデオがあり、50% を超えるビデオを視聴する訪問者を追跡するとします。 それには、Munchkinのカスタムアクティビティトラッキング機能を使用します。 これは、ページ上でイベント（50% に達するビデオ）をリッスンし、Munchkin API を呼び出すことで実装されます。 これを行うには、Marketoでカスタムアクティビティを設定し、ページでこのイベントに基づいて呼び出す必要があります。 ビデオプレーヤーにYouTubeを使用し、[YouTube Iframe API](https://developers.google.com/youtube/iframe_api_reference) を使用してMunchkin API のメソッドを呼び出します。

最初に、MarketoでMunchkin トラッキングコードを生成する方法、2 番目に、ページイベントに基づいてMunchkin サンプルコードをトリガーに変更する方法、3 番目に、フローステップを使用してページ上のアクションで定義されるスマートリストを含むキャンペーンを設定する方法、5 番目に、匿名ユーザーからのページ訪問がMarketoで記録されたことを確認する方法を説明します。 ====このブログ投稿は、説明されているコードのライブ例です。 このフォームに入力して、Marketoの既知のユーザーになるようにしてください。 こうすることで、ビデオの 50% を視聴すると、ビデオの残りが送信され、ビデオを 100% 視聴すると、別のブログ投稿へのリンクが送信されます。=== <https://developers.google.com/youtube/iframe_api_reference>

**Munchkin トラッキングコードの生成方法** Munchkin トラッキングコードを使用すると、web サイトへの訪問を追跡できます。 以下に示すMunchkin コードには 3 つのタイプがありますが、この例では、非同期Munchkin トラッキングコードを使用します。 A） シンプル：コードは最も少ないですが、web ページの読み込み時間に対して最適化されません。 このコードは、web ページが読み込まれるたびに jQuery ライブラリを読み込みます。 B）非同期：Web ページの読み込み時間を短縮します。 このコードは、jQuery ライブラリが既に存在するかどうかを確認し、存在しない場合は読み込み、Web ページの残りの部分が読み込まれると、トラッキングコードの実行に使用します。 C）非同期 jQuery:Web ページの読み込み時間を短縮し、システムパフォーマンスも向上させます。 既に jQuery があると想定し、チェックも読み込みも行いません。

1. アプリの右上にある「管理者」をクリックします。
1. 左側のツリーでMunchkinをクリックします。
1. トラッキングコードタイプは「非同期」を選択します。
1. 「」をクリックし、JavaScript トラッキングコードをコピーして web サイトに配置します。 **YouTube コード** <https://developers.google.com/youtube/js_api_reference#EventHandlers> <https://developers.google.com/youtube/iframe_api_reference> プレイヤー。

`getCurrentTime()` ビデオの再生が開始されてからの経過時間（秒単位）を返します。 `player.getDuration()` 現在再生中のビデオのデュレーション（秒）を返します。 `getDuration()` は、ビデオのメタデータが読み込まれるまでは 0 を返します（通常、これはビデオの再生が開始された直後に行われます）。 cookie を設定していないユーザーがMunchkin トラッキングコードを使用しているページに移動すると、ユーザーのブラウザーで新しい cookie が作成され、新しい匿名リードがMarketoで作成されます。 ユーザーが既に Cooked で、そのユーザーがMarketoの既存のリードである場合、ページへの訪問は、Marketoのそのユーザーのアクティビティログに記録されます。 **Cookie ユーザーおよびトラッキングイベントのコードサンプル** Web ページの `</body>` タグの直前にトラッキングコードを配置します。 Marketoで作成されたランディングページにはトラッキングコードが自動的に含まれるので、このコードを適用する必要はありません。 このコードサンプルでは、スクリプトの読み込み後にMunchkin API を呼び出します。

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      Munchkin.init('XXX-XXX-XXX');
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin.js';
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName('head')[0].appendChild(s);
})();
</script>
```

このコードサンプルでは、ユーザーがページに 5 秒間滞在し、さらに 500 ピクセル下にスクロールした後で、Munchkin API を呼び出します。

```javascript
<script src="https://code.jquery.com/jquery-2.1.0.min.js"></script>
<script type="text/javascript">
$(function(){
 setTimeout(function(){
  $(window).scroll(function() {
      var y_scroll_position = window.pageYOffset;
      var scroll_position = 500; //Sets number of pixels user must scroll to be tracked

  if(y_scroll_position > scroll_position) {
  //Munchkin tracking code
   (function() {
     var didInit = false;
     function initMunchkin() {
      if(didInit === false) {
        didInit = true;
        Munchkin.init('XXX-XXX-XXX');
      }
     }

     var s = document.createElement('script');
     s.type = 'text/javascript';
     s.async = true;
    s.src = '//munchkin.marketo.net/munchkin.js';
     s.onreadystatechange = function() {
      if (this.readyState == 'complete' || this.readyState == 'loaded') {
          initMunchkin();
      }
     };
     s.onload = initMunchkin;
     document.getElementsByTagName('head')[0].appendChild(s);
   })();
   }
 },5000); //Sets time delay before tracking user
});
</script>
```

**匿名ユーザーによるページ訪問がMarketoに記録されたことを確認する方法**

1. 上部メニューで「Analytics」をクリックし、「新しいレポート」をクリックします。 レポートタイプとして「Web ページアクティビティ」を選択し、レポートに名前を付けます。
1. レポートを作成したら、「スマート・リスト」をクリックします。 次に、右側のボックスから「訪問済み web ページ」フィルターを選択します。 Munchkin トラッキングコードを配置する web ページを入力します。
1. 「設定」をクリックします。 ISP から匿名訪問者を選択して、オプションを表示に変更します。
1. レポートをクリックします。 選択した web ページでアクティビティが追跡されているのが確認できます。
1. リードレコードをダブルクリックすると、アクティビティログが表示され、匿名ユーザーが訪問した特定のページを確認できます。

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

例えば、マルチメディアコンテンツを含むページの場合は、カスタムトラッキングの実行が必要な場合があります。 一般的な例の 1 つは、ページにMunchkin トラッキングコードを追加し、Munchkin API を使用して、ビデオの再生やオーディオクリップのリッスンなどのアクティビティ用のイベントをMarketo インスタンスに生成することです。 Munchkin トラッキングコードは、ほとんどまたはすべての web ページに配置することをお勧めします。 Munchkinのトラッキングコードは、Marketoを使用して作成するランディングページに自動的に含まれます。 この呼び出しを使用して、Ajax、Flash、またはその他の RIA 環境でのページ訪問など、ユーザーが何らかの操作を行ったことを記録します。 URL には「」やドメインを含めることはできません。ただし、存在しないページも含め、どのページも指すことができます。 URL パラメーターを追加する場合は、params 引数を使用します。
このイベントは、呼び出し元の web ページのドメインにあるユーザーのアクティビティログに、訪問 web ページ イベントとして表示されます。 メモ `mktoMunchkin()` を最初に呼び出すと、常に現在のページの訪問 web ページ イベントが作成されます。 追加の web ページ訪問を追跡する場合を除き、`visitWebPage` を呼び出す必要はありません。 `mktoMunchkinFunction('visitWebPage', { url: '/MyFlashMovie/Story1', params: 'x=y&2=3' });` メモ経験豊富なJavaScript開発者にアクセスできることを確認してください。 Marketo テクニカルサポートは、カスタム JavaScriptのトラブルシューティングを支援するように設定されていません。 Munchkin JavaScript API を使用すると、サードパーティの web システムをMarketo アカウントと統合できます。 一部の web 開発では、新しいリードを取り込んだり、web サイト上の既存のアプリケーションで現在のリードを更新したりできます。 例えば、新しい顧客情報を取得する顧客登録用の web アプリケーションがあるとします。 ほんの少しのプログラミングで、Marketoで取得したユーザーのリード情報を取得したり、将来の web トラッキング用にMarketo Cookie を設定したりできます。

また、別の機能を使用すると、web 開発者は、Flash や Ajax などのリッチ web 環境から web アクティビティ情報を取得および追跡できます。 メモ：適切な開発リソースがある場合は、この API の代わりにSOAP API を使用した統合を検討してください。 SOAP API は、Munchkin API よりも堅牢で、より多くの機能を備えています。 Marketo SOAP API 要件この機能を使用するには、web ページにMunchkin JavaScript コードを含める必要があります。 必要なスクリプトタグについては、Munchkin チュートリアルを参照してください。 また、Munchkin API を有効にします。これについては、チュートリアルでも説明しています。
内部Munchkin API 呼び出しを行った後、Cookie がない場合は自動的に Cookie が作成されます。 Marketoでは、イベント（リンクのクリック、web ページへの訪問、または新しいリード）をユーザーのアクティビティログに記録します。 クリックリンクを使用しているか、web ページ呼び出しを訪問している場合、イベントはそのリードのアクティビティログ（既知または匿名）に追加されます。 これが新しいリードで、「リードを関連付け」呼び出しを使用した場合、そのリードは既知のリードになり、アクティビティ履歴は保持されます。 これが既存のリードである場合（メールアドレスの一致に基づく）、変更された値や新しい値はそのリードのレコードで更新されます。

`munchkinFunction` 呼び出しの一般的な形式は次のとおりです。 Web ページの呼び出し先にタグとして含めます。 これは、他のJavaScript関数と同様に呼び出すことができます。 ただし、`mktoMunchkin()` の呼び出しを行う前に、Munchkin トラッキング関数 `mktoMunchkinFunction()` を呼び出す必要があります。

```javascript
<script src="http://munchkin.marketo.net/munchkin.js" type="text/javascript"> mktoMunchkin("###-###-###"); mktoMunchkinFunction('function', { key: 'value', key2: 'value'}, 'hash');
```

ここで、`###-###-###` は、アカウント関数のMunchkin アカウント ID です。params を、呼び出しハッシュに必要なパラメーターの配列にしたい呼び出しは、`associateLead` にのみ必要です。

Posted on _1970-01-01_ by _Murta_

## Marketoへのデータの取り込み

次のプレゼンテーションでは、データをMarketoに取り込む様々な方法を示します。 フォーム、カスタムオブジェクト、統合に重点を置いています。

[ データをMarketoに取り込む ](https://www.slideshare.net/MurtzaManzur/getting-data-into-marketo-35662408) [Murtza Manzur](https://www.slideshare.net/MurtzaManzur)

Posted on _2014-06-06_ by _Murta_

## Workspaceでのリードの作成

会社に北米とヨーロッパの 2 つの部門があるとします。 Marketoの企業部門に基づいてリードをセグメント化したいと考えています。 これは、Workspaces を使用して実行できます。これはMarketoの機能で、リードへのアクセスを制限できます。 これを行うには、北米用のワークスペースとヨーロッパ用のワークスペースを作成します。 その後、[syncLead API](/help/soap-api/synclead.md) を使用して、特定のワークスペースでリードを作成できます。 組織に次の要件がある場合は、ワークスペースとリードパーティションの使用を検討する必要があります。

1. 複数の製品ラインに対する個別のマーケティングチーム
1. 様々な地域や国に対して別々のマーケティングチーム
1. 親会社及び子会社
1. 親会社及び販売者

リード・パーティションおよびワークスペースを使用する場合は、次のことができます。

1. 組織内のリードへのアクセスを制限
1. 組織内のアセットへのアクセスを制限する
1. マーケティングチーム間でのアセットの共有

まず、UI を使用してMarketoでワークスペースを作成する方法を示し、次に、[syncLead API](/help/soap-api/synclead.md) を使用してワークスペースにリードを書き込む方法を示します。 **Workspaceの作成** ワークスペースは、一連のリードとMarketo アセットです。 ワークスペースでは、そのワークスペースからのリードと、そのワークスペース内のアセット（メール、キャンペーン、リストなど）のみを表示できます。 そのワークスペースのスマートキャンペーンが影響するのは、そのワークスペースのリードのみです。 アカウントのワークスペースを表示するには：

1. 「Admin」セクションの「Workspaces &amp; Lead Partitions」ページに移動します。 ワークスペースが「ワークスペース」タブに表示されます。 1.新しい作業領域を作成するには、「作業領域」タブのメニューバーにある「新規Workspace」ボタンをクリックします。
1. ダイアログで、新しいワークスペースに関する情報を追加する必要があります。

* **Workspace名** - インターフェイスに表示されるこのワークスペースの名前
* **説明** - ワークスペースの説明（オプション）。
* **リードパーティション** – このパーティションに表示されるリード。
* **すべてのリード・パーティション** – 現在および将来のすべてのパーティションのリードが表示されます。
* **個々のパーティションを選択** – これらのパーティションからのリードのみが表示されます（将来のパーティションは表示されません）
* **プライマリリードパーティション** - ランディングページにアクセスしたリードは、デフォルトでこのパーティションに追加されます
* **言語** - ワークスペースのビジネス言語

特定のワークスペースへの API 書き込みリードの使用方法を説明します。 最初のサンプルは XML リクエストで、2 番目のサンプルは XML 応答で、最後のサンプルは XML リクエストの生成に使用できる Ruby コードサンプルです。 1. リードを作成した後、「リードパーティション」は「リード情報」のフィールドになります。 SOAP `requestCampaign` のリクエスト

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809939944BFABAE58E5D27</mktowsUserId><requestSignature>48397ad47b71a1439f13a51eea3137df46441979</requestSignature><requestTimestamp>2013-08-01T12:31:14-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsRequestCampaign>
      <source>MKTOWS</source>
      <campaignId>4496</campaignId>
      <leadList>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>lead@company.com</keyValue>
        </leadKey>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>anotherlead@company.com</keyValue>
        </leadKey>
      </leadList>
    </ns1:paramsRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

requestCampaign に対するSOAP応答

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successRequestCampaign>
      <result>
        <success>true</success>
      </result>
    </ns1:successRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

上記のシナリオを実行する Java プログラムのサンプルを以下に示します。

```java
import com.marketo.mktows.*;
import java.net.URL;
import javax.xml.namespace.QName;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;


public class RequestCampaign {

    public static void main(String[] args) {
        System.out.println("Executing Request Campaign");
        try {
            URL marketoSoapEndPoint = new URL("CHANGE ME" + "?WSDL");
            String marketoUserId = "CHANGE ME";
            String marketoSecretKey = "CHANGE ME";

            QName serviceName = new QName("http://www.marketo.com/mktows/", "MktMktowsApiService");
            MktMktowsApiService service = new MktMktowsApiService(marketoSoapEndPoint, serviceName);
            MktowsPort port = service.getMktowsApiSoapPort();

            // Create Signature
            DateFormat df = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
            String text = df.format(new Date());
            String requestTimestamp = text.substring(0, 22) + ":" + text.substring(22);
            String encryptString = requestTimestamp + marketoUserId ;

            SecretKeySpec secretKey = new SecretKeySpec(marketoSecretKey.getBytes(), "HmacSHA1");
            Mac mac = Mac.getInstance("HmacSHA1");
            mac.init(secretKey);
            byte[] rawHmac = mac.doFinal(encryptString.getBytes());
            char[] hexChars = Hex.encodeHex(rawHmac);
            String signature = new String(hexChars);

            // Set Authentication Header
            AuthenticationHeader header = new AuthenticationHeader();
            header.setMktowsUserId(marketoUserId);
            header.setRequestTimestamp(requestTimestamp);
            header.setRequestSignature(signature);

            // Create Request
            ParamsRequestCampaign request = new ParamsRequestCampaign();

            request.setSource(ReqCampSourceType.MKTOWS);

            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Integer> campaignId = objectFactory.createParamsRequestCampaignCampaignId(4496);
            request.setCampaignId(campaignId);

            ArrayOfLeadKey leadKeyList = new ArrayOfLeadKey();
            LeadKey key = new LeadKey();
            key.setKeyType(LeadKeyRef.EMAIL);
            key.setKeyValue("lead@company.com");

            LeadKey key2 = new LeadKey();
            key2.setKeyType(LeadKeyRef.EMAIL);
            key2.setKeyValue("anotherlead@company.com");

            leadKeyList.getLeadKeies().add(key);
            leadKeyList.getLeadKeies().add(key2);

            JAXBElement<ArrayOfLeadKey> arrayOfLeadKey = objectFactory.createParamsRequestCampaignLeadList(leadKeyList);
            request.setLeadList(arrayOfLeadKey);

            SuccessRequestCampaign result = port.requestCampaign(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessRequestCampaign.class);
            Marshaller m = context.createMarshaller();
            m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
            m.marshal(result, System.out);

        }
        catch(Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Workspaces とリードパーティションにサインアップするにはどうすればよいですか？** Marketo Enterprise のお客様は、ワークスペースとリードパーティションに無料でアクセスできます。 有効化と実装について詳しくは、カスタマーイネーブルメントマネージャーにお問い合わせください。 その他のお客様は、Marketo担当営業またはセールスチームにお問い合わせください。

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _1970-01-01_ by _Murta_

## 2014 年 6 月リリースアップデート

### Marketo Real-Time Personalization API

Marketo リアルタイム Personalization（RTP）JavaScript API は、プラットフォームの Automated Personalization 機能を拡張します。 これにより、web ページのイベントトラッキングと動的なカスタマイズが可能です。完全なドキュメントを参照してください [ こちら ](/help/javascript-api/web-personalization.md)。

Posted on _2014-06-20_ by _Travis Kaufman_

## Marketoでの外部キーの保存

専有 CRM やデータウェアハウスなどのシステム間で連絡先レコードとリードレコードを同期する場合、リードレコードを一意のシステム識別子に関連付けることは一般的な要件です。 Marketoでは、一意のシステム ID を使用して、[syncMultipleLeads API](/help/soap-api/syncmultipleleads.md) 呼び出しを通じてリードレコードを作成または更新できます。 これを実現するには、一意のシステム ID （プライマリキー）を外部キーとしてMarketoに保存します。 外部キーを格納するMarketoのこのフィールドの名前は foreignSysPersonId です。 注意すべき 3 つの重要な点を次に示します。

1. foreignSysPersonId がMarketoの UI に表示されない。 したがって、カスタム属性フィールドにもこの値を入力することがベストプラクティスです。
1. foreignSysPersonId はリードに固有ですが、1 つのリードが複数の foreignSysPersonId を持つ場合があります。
1. foreignSysPersonId は、更新または削除することはできませんが、別のレコードに再割り当てすることができます。

[syncMultipleLeads API](/help/soap-api/syncmultipleleads.md) を呼び出して、Marketoの 2 つの既存のリードレコードに foreignSysPersonId 値を書き込む方法を示します。 **syncMultipleLeads API を使用して foreignSysPersonId を記述する方法** 新しいリードレコードを挿入して、foreignSysPersonId を指定できます。 また、Marketo ID と foreignSysPersonId の両方を指定することで、既存のリードにこの ID を追加することもできます。 その後の事件について順を追って説明します。 **syncMultipleLeads SOAP API 呼び出しに対する XML のリクエスト**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809934544BFABAE58E5D27</mktowsUserId>
      <requestSignature>b5e21953ae9f1b263e644da5eccce9ff33802513</requestSignature>
      <requestTimestamp>2013-08-01T18:22:30-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsSyncMultipleLeads>
      <leadRecordList>
        <leadRecord>
          <leadId>1090240</leadId>
          <foreignSysPersonId>1224191</foreignSysPersonId>
          <leadAttributeList>
            <attribute>
              <attrName>Company</attrName>
              <attrValue>Marketo1000</attrValue>
            </attribute>
            <attribute>
              <attrName>Phone</attrName>
              <attrValue>650-555-1000</attrValue>
            </attribute>
          </leadAttributeList>
        </leadRecord>
        <leadRecord>
          <leadId>1090239</leadId>
          <foreignSysPersonId>1224192</foreignSysPersonId>
          <leadAttributeList>
            <attribute>
              <attrName>Company</attrName>
              <attrValue>Marketo1001</attrValue>
            </attribute>
            <attribute>
              <attrName>Phone</attrName>
              <attrValue>650-555-1001</attrValue>
            </attribute>
          </leadAttributeList>
        </leadRecord>
      </leadRecordList>
      <dedupEnabled>true</dedupEnabled>
    </ns1:paramsSyncMultipleLeads>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

**syncMultipleLeads SOAP API 呼び出しの応答 XML**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successSyncMultipleLeads>
      <result>
        <syncStatusList>
          <syncStatus>
            <leadId>1090240</leadId>
            <status>UPDATED</status>
            <error xsi:nil="true" />
          </syncStatus>
          <syncStatus>
            <leadId>1090239</leadId>
            <status>UPDATED</status>
            <error xsi:nil="true" />
          </syncStatus>
        </syncStatusList>
      </result>
    </ns1:successSyncMultipleLeads>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

**上記のリクエスト XML を出力する Ruby プログラムのサンプルを以下に示します。**

```java
require 'savon' # Use version 2.0 Savon gem
require 'date'

mktowsUserId = "" # CHANGE ME
marketoSecretKey = "" # CHANGE ME
marketoSoapEndPoint = "" # CHANGE ME
marketoNameSpace = "<http://www.marketo.com/mktows/>"

# Create Signature
Timestamp = DateTime.now
requestTimestamp = Timestamp.to_s
encryptString = requestTimestamp + mktowsUserId
digest = OpenSSL::Digest.new('sha1')
hashedsignature = OpenSSL::HMAC.hexdigest(digest, marketoSecretKey, encryptString)
requestSignature = hashedsignature.to_s

# Create SOAP Header
headers = {
 'ns1:AuthenticationHeader' => { "mktowsUserId" => mktowsUserId, "requestSignature" => requestSignature,
 "requestTimestamp"  => requestTimestamp
 }
}

client = Savon.client(wsdl: '<http://app.marketo.com/soap/mktows/2_3?WSDL>', soap_header: headers, endpoint: marketoSoapEndPoint, open_timeout: 90, read_timeout: 90, namespace_identifier: :ns1, env_namespace: 'SOAP-ENV')

# Create Request
request = {
        :lead_record_list => {
                :lead_record => {
                        :lead_id => "1090240",
                        :foreign_sys_person_id => "1224191",
                :lead_attribute_list => {
                        :attribute => {
                                :attr_name => "Company",
                                :attr_value => "Marketo1000" },
                         :attribute! => {
                                :attr_name => "Phone",
                                :attr_value => "650-555-1000" }
                }
        },
        :lead_record! => {
                        :lead_id => "1090239",
                        :foreign_sys_person_id => "1224192",
                :lead_attribute_list => {
                        :attribute => {
                                :attr_name => "Company",
                                :attr_value => "Marketo1001" },
                         :attribute! => {
                                :attr_name => "Phone",
                                :attr_value => "650-555-1001" }
                }
        }
        },
    :dedup_enabled => "True"
}

response = client.call(:sync_multiple_leads, message: request)

puts response
```

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _2014-06-27_ by _Murta_

## リードのメールアドレスの更新

ユーザーがサイト上のMarketo フォームに入力するとします。 何が起こるの？ Marketoは、ユーザーを cookie に登録し、提供されたメールに関連付けます。 次回ユーザーが web サイトを訪問し、同じフォームに別のメールで再度入力した場合。 何が起こるの？ Marketoは、新しいリードレコードを作成し、ユーザーのブラウザーの最初の cookie を上書きします。 これで、ユーザーはMarketoの新しいリードまたは別のリードになります。 [syncLead API メソッド ](/help/soap-api/synclead.md)、フォームメソッドのカスタムフィールド、Marketo UI、リストの読み込みなど、Marketoでリードのメールアドレスを更新する 4 つの方法を示します。 **syncLead API 経由**&#x200B;[syncLead API](/help/soap-api/synclead.md) を使用して、Marketo ID と新しいメールアドレスを使用してリードレコードを更新できます。 SOAP API 呼び出し用 `syncMultipleLeads`XML をリクエスト

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>bigcorp1_461839624B16E06BA2D663</mktowsUserId>
      <requestSignature>92f05a7be4838ae1c0e5aafe814891ee72968a08</requestSignature>
      <requestTimestamp>2013-07-31T12:38:47-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsSyncLead>
      <leadRecord>
        <leadId>1090240</leadId>
        <Email>t@t.com</Email>
      </leadRecord>
      <returnLead>false</returnLead>
    </ns1:paramsSyncLead>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

syncMultipleLeads SOAP API 呼び出しの応答 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successSyncLead>
      <result>
        <leadId>1090240</leadId>
        <syncStatus>
          <leadId>1090240</leadId>
          <status>UPDATED</status>
          <error xsi:nil="true" />
        </syncStatus>
        <leadRecord xsi:nil="true" />
      </result>
    </ns1:successSyncLead>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

上記のリクエスト XML を出力する Ruby プログラムのサンプルを以下に示します。

```java
require 'savon' # Use version 2.0 Savon gem
require 'date'

mktowsUserId = "" # CHANGE ME
marketoSecretKey = "" # CHANGE ME
marketoSoapEndPoint = "" # CHANGE ME
marketoNameSpace = "<http://www.marketo.com/mktows/>"

# Create Signature
Timestamp = DateTime.now
requestTimestamp = Timestamp.to_s
encryptString = requestTimestamp + mktowsUserId
digest = OpenSSL::Digest.new('sha1')
hashedsignature = OpenSSL::HMAC.hexdigest(digest, marketoSecretKey, encryptString)
requestSignature = hashedsignature.to_s

# Create SOAP Header
headers = {
 'ns1:AuthenticationHeader' => { "mktowsUserId" => mktowsUserId, "requestSignature" => requestSignature,
 "requestTimestamp"  => requestTimestamp
 }
}

client = Savon.client(wsdl: '<http://app.marketo.com/soap/mktows/2_3?WSDL>', soap_header: headers, endpoint: marketoSoapEndPoint, open_timeout: 90, read_timeout: 90, namespace_identifier: :ns1, env_namespace: 'SOAP-ENV')

# Create Request
request = {
 :lead_record => {
  :Email => "<t@t.com>",
  :lead_id => "1090240",
 :return_lead => "false"
}

response = client.call(:sync_lead, message: request)

puts response
```

**フォームのカスタムフィールドを使用** Marketoで「新しいメールアドレス」のカスタムフィールドを作成できます。 次に、この新しいフィールドを含むフォームに入力するようにユーザーに依頼します。 次に、Marketoで、新しいカスタムフィールド「新しいメールアドレス」に変更があった場合に、システムメールアドレスのフィールドのデータ値をトークン `{{lead.newEmailAddress}}` に変更するプログラムを作成します。 **Marketo UI を使用** Marketo UI を使用して、リードのメールアドレスを手動で更新できます。 これを行う方法を説明する [ ヘルプ記事 ](https://nation.marketo.com/) を以下に示します（この記事を参照するにはMarketoへのログインが必要です）。 **リストの読み込みを使用** Marketoで説明されているリストの読み込み方法 [ こちら ](https://nation.marketo.com/) を使用して、リードのメールアドレスを更新できます（記事を参照するにはMarketoへのログインが必要です）。  

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _1970-01-01_ by _Murta_

## リードの 2 番目のメールアドレスの保存

API を使用してMarketoでリードのスコアを変更するとします。 これは、リードの作成/更新エンドポイントを使用した REST API で実行できます。 1 つのリードレコードに複数のメールを保存する場合は、カスタムフィールドを作成し、そこに 2 番目のメールを保存する必要があります。 詳細については、次のヘルプ記事を参照してください。以下は、この呼び出しを行う方法を示す Ruby のコードサンプルです。

```java
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/leads.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
request_url = marketo_instance + endpoint + auth_token

# Build request body
data = { "action" => "updateOnly", "input" => [ { "email" => "<example@email.com>", "leadScore" => "30" } ] }

# Make request
response = RestClient.post request_url, data.to_json, :content_type => :json, :accept => :json

# Returns Marketo API response
puts response
```

Posted on _2015-02-20_ by _Murta_

## Marketoでカスタムフィールドを作成し、AP を使用してこのフィールドを更新する

標準のMarketo フィールドに適合しないリードに関する追加データがあるとします。 例えば、このカスタムフィールドにはサードパーティのスコアを使用できます。 Marketoでサードパーティのスコアのカスタムフィールドを作成し、Marketo [REST API](https://developer.adobe.com/marketo-apis/) または [SOAP API](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/activity-type-filters) を使用してこのフィールドの値を更新できます。 まず、Marketoでカスタムフィールドを作成する方法を示し、次に、REST API を使用してこのフィールドを更新する方法を示します。

### Marketoでのカスタムフィールドの作成方法

1. 「管理者」で、「フィールド管理」をクリックします。
1. 「新規カスタムフィールド」ボタンをクリックします。
1. 「タイプ」フィールドを選択します。これにより、MarketoのスマートリストおよびFormsでのレンダリング方法が変わります。
1. Marketo に表示する名前を入力します。フィールド名の変更は困難な場合があり、状況によっては不可能な場合があるので、名前と API 名は慎重に選択します。
1. 作成したカスタムフィールドに API からアクセスできるようになりました。

### REST API を使用してカスタムフィールドを更新する方法

前の節では、データタイプが文字列の `myCustomField` というカスタムフィールドを作成しました。 そのフィールドの値を更新するには、リードの作成/更新と呼ばれる REST API エンドポイントを使用します。 REST API にリクエストを送信する前に、認証する必要があります。 これはこの記事の範囲外ですが、詳細は [Marketo開発者サイトで入手可能 ](/help/rest-api/authentication.md) です。

**エンドポイント**

`/rest/v1/leads.json`

**リクエスト本文**

```json
{
   "action":"createOrUpdate",
   "input":[
      {
         "email":"<example@example.com>",
         "myCustomField":"examplestring"
      }
   ]
}
```

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _2014-08-19_ by _Murta_

## Unbounce とMarketoの統合

**メモ：これは Fab Capodicasa によるゲストブログの投稿です。 B2C を専門とするMarketo LaunchPoint エージェンシーパートナーである [Hoosh Marketing](http://hooshmarketing.com.au/) のMarketo認定コンサルタントです。 同氏は過去 13 年間、SaaS とマーケティングの両方で働いてきました。 彼のバックグラウンドは、ハードコア IT、ダイレクトマーケティング、エンタープライズセールスの融合です。 Fab はMarketoの元社員でもあります**。

**概要** この記事では、一般的なランディングページツールである Unbounce をMarketoと統合する方法について説明します。 まず、Unbounce にMarketo トラッキングを挿入する方法を示し、次に、Unbounce フォームを変更してMarketoに直接データを挿入する方法を示します。 Unbounce をMarketoと統合する際の課題は、Unbounce を使用してデフォルトのフィールドの名前を変更できないことです（例えば、first_name を FirstName に変更することはできません）。 また、フィールドラベルとフィールド名を異なるものにすることはできません。 この統合には、既存のフォームを調整してMarketoと互換性を持たせるJavaScriptが含まれます。 この記事の作業を完了するには、少なくともJavaScriptの初級レベルとMarketoの中級レベルの知識を持っていることをお勧めします。
**パート 1：アンバウンスへのMarketo トラッキングコードの追加** 分析とフォーム統合の両方を機能させるには、アンバウンスページにMarketo Munchkin トラッキングスクリプトを追加する必要があります。 次の手順に従ってください。MarketoからMunchkin コードをコピーします。管理者/ Munchkinに移動し、JavaScriptの「シンプル」バージョンをコピーします。 Unbounce ランディングページを開き、JavaScript/新しいJavaScriptを追加をクリックします。  「追加」をクリックし、スクリプト「Munchkin」を呼び出して、「本文終了タグの前」を選択し、Munchkin コードを貼り付けます。 「完了」ボタンをクリックします。 今後のバウンスページの場合は、JavaScriptに移動して、作成したMunchkin スクリプトを有効にします。 再作成する必要はありません。
**パート 2：バウンスフォームをMarketo フォームに変換する** 新しい非表示フィールドとJavaScriptを追加して、バウンスフォームを変更し、バウンスランディングページでリード情報を直接Marketoに送信できるようにする必要があります。 まず、Marketoのプレースホルダーフォームを作成します。 Marketoで、空白のフォームを作成し、承認します。

これは、バウンスフォームを表すMarketoのプロキシフォームです。 バウンスフォームに非表示フィールドを追加します。 これらの非表示フィールドは、Marketoが、このフォーム送信が適用されるフォームとユーザーセッションを示すMarketo インスタンスを判断するために必要です。 Unbounce で、ダブルクリックしてフォームを開きます。 `_mkt_trk` という非表示フィールドを追加します。 `formid` という 2 番目の非表示フィールドを追加します。  233 は、フォームの id に置き換える必要があります。これは、MarketoのMarketo フォーム埋め込みコードにあります。 Marketoでフォームを開き、「フォームのアクション」/「埋め込みコード」を選択します。 `returnurl` という非表示フィールドを追加します。 `http://hooshmarketing.com.au/thank-you` は、フォローアップ URL に置き換える必要があります。これは、フォームの送信後にユーザーをリダイレクトする URL です。 例えば、「ありがとうございます」ページがあります。
**パート 3:Marketoへのバウンスフォームの誘導** フォローアップ URL は、リードがMarketoに送信された後にリードがリダイレクトされるページです。 Unbounce では、次の手順に従ってください。フォームをクリックします。 フォーム確認セクションを変更します。 確認を変更して、フォームデータを URL に POST します。 必要なフォローアップページの URL を設定します。 `fpmarkets` は、Marketo アカウント文字列に置き換える必要があります。この文字列は、Marketoの管理者/ランディングページにあります。
**第 4 部：バウンスページへのJavaScriptの追加** このJavaScriptは、Marketoと互換性を持つようにフォームを変換し、Marketoに送信します。 Unbounce では、次の手順に従ってください：Unbounce ランディングページを開き、JavaScript/新しいJavaScriptを追加をクリックします。 「追加」をクリックし、スクリプト「Marketo Form Convert」を呼び出して「Before Body End Tag」を選択します。 以下のJavaScript コードを貼り付けます。

```javascript
var MARKETO_MUNCHKIN_ID='614-CGT-700';
var MARKETO_ACCOUNT_STRING = 'fpmarkets';

var UNBOUNCE_MARKETO_FIELD_MAP = new Object();

//default field mappings
UNBOUNCE_MARKETO_FIELD_MAP['first_name'] = 'FirstName';
UNBOUNCE_MARKETO_FIELD_MAP['email'] = 'Email';
UNBOUNCE_MARKETO_FIELD_MAP['last_name'] = 'LastName';
UNBOUNCE_MARKETO_FIELD_MAP['phone_number'] = 'Phone';

function getMarketoField(k) {
    return UNBOUNCE_MARKETO_FIELD_MAP[k];
}


var formFields = [];
var hiddenClonedFields = [];
var firstForm = document.forms[0];

//Convert Unbounce form names to Marketo field names
for(i=0; i<firstForm.elements.length; i++){
 var formField = firstForm.elements[i];
 var newFieldName = getMarketoField(formField.name);

  if(newFieldName != undefined) {


    //save original field as hidden field
    var hiddenField = document.createElement("input");
    hiddenField.setAttribute("type", "hidden");
    hiddenField.setAttribute("name", formField.name);
    hiddenField.setAttribute("id", formField.id);
    hiddenClonedFields.push(hiddenField);

    //change original field
    console.log ( 'Changed form field name: ' + formField.name + '=>' + newFieldName );
    formField.name = newFieldName;
    formField.id = newFieldName;
    formFields.push(formField);


  } else {
    console.log ( 'Couldn't map:' + formField.name );
  }
}

//Add hidden cloned Unbounce fields to form
//for Unbounce validation
for(i=0; i<hiddenClonedFields.length; i++){
    firstForm.appendChild(hiddenClonedFields[i]);
    formFields[i].onchange = (function(hf) {
        return function(event) {
            hf.value = event.target.value;
          console.log('Changed hidden cloned field:' + hf.name + '=>' + hf.value);
        };
    }(hiddenClonedFields[i]));
    console.log ( 'Added cloned field: ' + hiddenClonedFields[i].name );
}


//Add MunchkinId to form
var input = document.createElement("input");
input.setAttribute("type", "hidden");
input.setAttribute("name", "munchkinId");
input.setAttribute("value", MARKETO_MUNCHKIN_ID);
firstForm.appendChild(input);
console.log('Added hidden field:' + input.name + '=' + input.value);
```

API 名に Unbounce との互換性のないカスタムフィールドがある場合は、JavaScriptのマッピングにこれらを追加できます。 例えば、Marketoのカスタムフィールドの 1 つが `Comments_c` で、フィールドラベルをコメントとして表示したい場合、Unbounce では、フィールド名を `Comments_c` に変更することはできません。

```
//default field mappings
UNBOUNCE_MARKETO_FIELD_MAP['comments'] = 'Comments_c';
UNBOUNCE_MARKETO_FIELD_MAP['first_name'] = 'FirstName';
UNBOUNCE_MARKETO_FIELD_MAP['email'] = 'Email';
```

_comments は Unbounce のフィールド名です。 _Comments_c_ は、Marketoのフィールドの名前です。 今後のバウンスページでは、JavaScriptに移動して、作成したMunchkin スクリプトを有効にするだけです。 再作成する必要はありません。
**パート 5：テスト** 最後の手順は、このフォーム統合が機能していることをテストすることです。 Marketoでトリガーを作成します。このエディターは、Marketo フォームの入力に対してをアクティブ化し、リードがMarketoに正しく挿入されていることを確認します。 フォームが送信されると、ページはフォローアップ URL にリダイレクトされます。

Posted on _2014-08-04_ by _

## 2014 年 7 月リリースアップデート

### Munchkin の更新

Munchkinの新しいバージョンは 141 です。 バージョン 142 はサポートされておらず、2011 年 9 月上旬に削除される予定です。 バージョン 142 では、開発者向けサイトに記載されていない、公開アクセス可能な機能がありました。 これらのドキュメントに記載されていない関数は、公開されなくなりました。 開発者向けサイトのドキュメント化された機能は、引き続き長期的にサポートされます。

### RTP 更新

RTP API には、訪問者データの取得と呼ばれる新しい関数があります。 この RTP API 呼び出しを使用すると、組織、業界、場所、セグメントコードの一致など、リアルタイムの訪問者データを取得できます。

Posted on _2014-07-30_ by _Murta_

## 1 つのページでの複数のMunchkin トラッキングコードの使用

複数のMarketo インスタンスがあり、これらの複数のインスタンスにページ訪問やクリックリンクなどの web トラッキングイベントを送信したい場合、Munchkinを使用してこれを行うことができます。 Marketoは、ドメイン（「marketo.com」など）別に web サイトへの訪問者を追跡します。 プライマリドメインとは異なるドメイン（「company.com」など）でこのMunchkin スクリプトをホストしている場合、そのドメインのフォームに入力するまで、訪問者は匿名のリードとして表示されます。 これを行うには、`altIds` 呼び出しに `Munchkin.init` パラメーターを追加します。 altIds パラメーターには、web イベントを送信する必要がある追加のMunchkin ID の配列が含まれています。 次の例では、ハイライト表示されたMunchkin ID （XXX-XXX-XXX、YYY-YYY-YYY および ZZZ-ZZZ-ZZZ）を、トラッキング情報が送信される各Marketo インスタンスのMunchkin ID に置き換えます。

```javascript
<script src="http://munchkin.marketo.net/munchkin.js" type="text/javascript"></script>
<script>Munchkin.init('XXX-XXX-XXX', { altIds:['YYY-YYY-YYY', 'ZZZ-ZZZ-ZZZ'] });</script>
```

Munchkin初期化パラメーターについて詳しくは、[ このドキュメント ](/help/javascript-api/configuration.md) を参照してください。

Posted on _2014-08-08_ by _Murta_

## MunchkinとGoogle Tag Manage の統合

Google タグマネージャーを使用すると、web サイトにタグを追加できます。 Munchkinなどのトラッキングスクリプトを web サイトのソースコードに手動で追加するのではなく、サイトに [Google Tag Manager](https://marketingplatform.google.com/about/tag-manager/) を配置してから、Google Tag Manager の UI を使用して [Munchkin](/help/javascript-api/lead-tracking.md) などのタグを追加することができます。 この投稿では、まずMarketoでMunchkin トラッキングコードを生成する方法を示し、次に、このMunchkin トラッキングコードをGoogle Tag Manager に追加する方法を示します。

### Munchkin トラッキングコードの生成方法

1. アプリの右上にある「**管理者**」をクリックします。
1. 左側のツリーで **0&rbrace;Munchkin&rbrace; をクリックします。**
1. トラッキングコードタイプは「**非同期**」を選択します。
1. 「」をクリックして、JavaScript トラッキングコードをコピーします。

**Google タグマネージャーにMunchkin トラッキングコードを追加する方法**

1. Google Tag Manager アカウントにログインし、**新しいタグを追加** します。
1. 新しい **カスタム HTML タグ** を作成します。
1. Munchkin コードをコピーして「**HTML**」フィールドに貼り付け、「**続行**」をクリックします。
1. 「**すべてのページで実行**」を選択し、「**タグを作成」をクリックします。** 注意：Web サイトのトラフィックが非常に多い場合は、**一部のページで実行** を使用してサイトのセクションを除外できます。
1. 「保存」をクリックし、Munchkin トラッキングコードが web サイトに読み込まれたことを確認します。

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _2014-08-05_ by _Murta_

## フォーム送信後にライトボックスを非表示

### 概要

フォームを送信する際に、Marketoで生成された現在の Lightbox 埋め込みコードが消えない。 フォームの送信後にページが再読み込みされ、フォームが再び表示されます。 フォーム送信後に非表示になるライトボックスを作成する場合は、次の手順に従ってください。

### ガイド方法

1. Marketoでフォームを作成したら、埋め込みコードを生成します。 コードの種類として [ フォームの操作 ] をクリックし、[ Lightbox ] をクリックします。 このコードをコピーしてテキストエディターに貼り付け、次の手順で編集できるようにします。
1. 埋め込みコード内の「（form）」の後のすべてのコードを以下のコードに置き換えます。

```javascript
{
var lightbox = MktoForms2.lightbox(form).show();
form.onSuccess(function(){
lightbox.hide();
return false;
});
});
</script>
```

手順 2 を完了すると、完了したバージョンは次のコードのようになります。 これで、コードを web サイトで使用する準備が整いました。

```javascript
<script src="http://app-sj04.marketo.com/js/forms2/js/forms2.js"></script>
<form id="mktoForm_0000"></form>
<script>MktoForms2.loadForm("http://app-sj04.marketo.com", "AAA-BBB-CCC", 0000, function (form){
var lightbox = MktoForms2.lightbox(form).show();
form.onSuccess(function(){
lightbox.hide();
return false;
});
});
</script>
```

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _2014-08-21_ by _Murta_

## Marketo REST API のクイックスタートガイド

このガイドでは、Marketo REST API を 10 分で初めて呼び出す方法について説明します。 [ リード ID でリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) REST API エンドポイントを使用して 1 つのリードを取得する方法を説明します。 これを行うには、認証プロセスを順を追って説明し、アクセストークンを生成します。アクセストークンは、[ID でリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) するための HTTP GET リクエストを行う際に使用します。 次に、JSON 形式でリード情報を返すリクエストを実行するためのコードを提供します。

### 認証トークンの生成方法

>[!NOTE]
> 2025 年 6 月をもって、認証トークンはサポートされなくなりました。 認証ヘッダーを使用する必要があります。
>

Marketoのカスタムサービスを使用すると、アプリケーションがアクセスできるデータを記述して定義できます。 カスタムサービスを作成し、そのサービスを 1 人の API のみのユーザーに関連付けるには、Marketo管理者としてログインする必要があります。

1. Marketo アプリケーションの管理領域に移動します。
1. 左側のパネルで、ユーザーと役割ノードをクリックします。
1. 新しい役割を作成します。 「Access API」をクリックして、役割の権限のリストを表示します。 下にスクロールして、必要な権限のみを選択します。 この場合は、「読み取り専用リード」権限を選択するだけです。
1. 次に、API のみのユーザーを作成し、前の手順で作成した API の役割に関連付けます。 これを行うには、ユーザーの作成時に API のみのユーザーチェックボックスをオンにします。
1. カスタムサービスは、クライアントアプリケーションを一意に識別するために必要です。 カスタムアプリケーションを作成するには、管理/ LaunchPoint 画面に移動して、新しいサービスを作成します。
1. 表示名を入力し、「カスタム」サービスタイプを選択し、説明と、手順 1 で作成したユーザーのメールアドレスを入力します。 このカスタム REST API サービスの会社または目的を表す説明的な表示名を使用することをお勧めします。
1. グリッドの「詳細を表示」リンクをクリックして、クライアント ID とクライアントシークレットを取得します。 クライアントアプリケーションで、クライアント ID とクライアント秘密鍵を使用してアクセストークンを生成できます。
1. 認証トークンをコピーしてテキストエディターに貼り付けます。 認証トークンは、次の例のようになります。

`cdf01657-110d-4155-99a7-f986b2ff13a0:int`

### エンドポイント URL の決定方法

Marketo API にリクエストを送信するには、エンドポイント URL にMarketo インスタンスを指定する必要があります。 Marketo REST API に対する非一括 API リクエストはすべて、次の形式に従います。

`<REST API Endpoint URL>/rest/`

REST API エンドポイント URL は、Marketo管理者/web サービスパネルにあります。 Marketo エンドポイント URL の構造は、次の例のようになります。

`https://100-AEK-913.mktorest.com/rest/v1/lead/{id}.json`

**メモ：一括 API の URL の先頭には「/rest/」は付きません。 Bulk API の場合は、ホストのみを使用し、** のように適切なパスを追加する必要があります。

`https://100-AEK-913.mktorest.com/bulk/v1/leads/export/create.json`

### 認証トークンを使用して Get Lead by Id AP を呼び出す方法

前の節で、認証トークンを生成し、エンドポイント URL を見つけました。 次に、「ID によるリードの取得 [ という REST API エンドポイントにリクエストを送信し ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) す。 Marketo REST API に対するリクエストを行う最も簡単な方法は、URL を web ブラウザーのアドレスバーに貼り付けることです。 次の形式に従います。

`https://<REST API Endpoint URL for your Marketo instance>/rest/v1/<API that you are calling>?access_token=<access_token>`

### 例

`https://100-AEK-913.mktorest.com/rest/v1/lead/318581.json?access_token=cdf01657-110d-4155-99a7-f986b2ff13a0:int`

呼び出しが成功した場合、次の形式の JSON が返されます。

```json
{
    "requestId": "d82a#14e26755a9c",
    "result": [
        {
            "id": 318581,
            "updatedAt": "2015-06-11T23:15:23Z",
            "lastName": "Doe",
            "email": "<jdoe@marketo.com>",
            "createdAt": "2015-03-17T00:18:40Z",
            "firstName": "John"
        }
    ],
    "success": true
}
```

Marketo REST API について詳しく知りたい場合は、ここから [ 開始することをお勧めします ](https://developer.adobe.com/marketo-apis/)。

Posted on _2015-09-04_ by _David_

## Marketo トラッキング Cookie の削除方法

質問：「セールスチームがメールメッセージから削除するよう口頭で依頼した個人を登録解除するためのフォームを web サイトに設定しました。 ただし、メールに入力し、そのメールアドレスでクッキーが作成されたことを送信し、当社の web サイトでのアクティビティに関するアラートの受信を開始した場合は何が見つかります。 現在のフォームは、埋め込みフォームです。 埋め込みフォームで cook のトラッキングを無効にする方法を誰かが考え出したので、Marketoのランディングページでする方法は理解できました。」 私たちはこれを行うことができます。 これを実装するには、cookie の有効期限を高速化します。 フォームで cookie が作成されたら、直ちに期限切れにすることができます。 cookie の有効期限が切れているので、ブラウザーによって自動的に削除されます。 このプロセスを開始するには、ネイティブフォーム機能を使用して、`deleteCookie` という関数の下でを呼び出します。

Posted on _2014-08-26_ by _Travis Kaufman_

## Marketo ランディングページと Wordpress の統合

例えば、web サイトが Wordpress を使用して構築されていて、いずれかのページにMarketo ランディングページを埋め込むとします。 これは、iframe を使用すると可能です。 iframe では、ページを別のページ内に埋め込むことができます。 この記事では、Wordpress ページにMarketo ランディングページを埋め込む方法を説明します。 **Wordpress のプラグインを選ぶ** Wordpress いくつかの Wordpress のプラグインを使用できます：`http://wordpress.org/plugins/iframe/` このアプローチを使用する上でいくつかの長所と短所があります：`http://www.elixiter.com/marketo-landing-page-and-form-hosting-options/` Great post Murtza! Colby では、iframe はフォームの送信後にPDFにリダイレクトされる部分を保持します。 私たちは長い間サイトで iframe を使用しました。 素晴らしいポスト Murtza! Colby では、iframe はフォームの送信後にPDFにリダイレクトされる部分を保持します。 私たちは長い間サイトで iframe を使用しました。 なお、メイン URL から iframe に URL パラメーターを渡す場合は、コーディングが必要です。 また、Google Analyticsが正しく設定されていることを確認します。 iframe を使用して、ページに訪問するたびにページビューが 2 回カウントされないようにする必要がある。

Posted on _1970-01-01_ by _Murta_

## Optimizely とMarketoのランディングページの統合

[Optimizely](https://www.optimizely.com/) を使用すると、サイトで A/B テスト、複数ページおよび多変量分析テストを実行できます。 Optimizely は、Marketoのランディングページで使用できます。 その方法を次に示します。

1. Optimizely のコードスニペットを探してコピーします。Optimizely のダッシュボードに移動**、「プロジェクトコード」リンクをクリックします。 ポップアップに表示されるコード行をコピーします。
1. Marketoにログインし、ランディングページテンプレートを選択します。 次に、「ドラフトを編集」をクリックします。**
1. 「ランディングページのアクション」をクリックします。 次に、「ページのメタタグを編集」をクリックし**す。
1. Optimizely コードスニペットを「カスタム HEAD HTML」セクションに貼り付けて、「保存」をクリックします。
1. ランディングページをテストして、Optimizely スニペットが機能していることを確認します

Posted on _2014-09-18_ by _Murta_

## Marketo REST API を使用したフルネームによる検索

**質問：** リードのフルネームのみを使用して、Marketo API でリードをクエリする方法はありますか？
**回答：** 直接実行することはできません。 ただし、以下に説明する回避策では、これを行うことができます。

1. Marketoで「Fullname」というカスタムフィールドを作成します。
1. [getMultipleLeads](/help/soap-api/getmultipleleads.md)SOAP API または [ フィルタータイプによる複数のリードの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) のいずれかを使用して、リードデータベースに対してクエリを実行します。 REST またはSOAP API へのリクエストに、属性として名と姓を含めます。
1. リードデータベースをクエリした後、各リードの「名」と「姓」を連結し、このデータを「フルネーム」列に保存します。 1. SOAP API [syncMultipleLeads](/help/soap-api/syncmultipleleads.md) を使用してこのデータを「Fullname」カスタムフィールドにプッシュします。 または、[ リードを読み込み ](/help/rest-api/leads.md) API を使用するか、Marketo UI を使用して CSV または XLS を読み込むこともできます。
1. これで、[ フィルタータイプで複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)API を使用してフルネームでクエリし、このカスタムフィールドを検索できるようになりました。 「Fullname」を「filterType」として指定し、「filterValue」を「Joe Johnson」とし、フィルタータイプの REST API 呼び出しで複数のリードを取得します。

Posted on _2014-09-09_ by _Murta_

## Marketo トラッキング Cookie の削除

このメソッドは、cookie を完全に削除する目的で使用する場合にのみ使用してください。

このコードサンプルを使用すると、Marketoのフォーム送信後にユーザーのブラウザーからMarketo トラッキング cookie を削除できます。 これは、ユーザーがフォーム `deleteMarketoCookie` 送信した後にメソッドを呼び出すことによって機能します。 このメソッドでは、有効期限を過去の日付に設定することで、cookie の有効期限が切れます。 この cookie は有効期限が切れているので、ブラウザーのデフォルトの動作で削除されます。

Posted on _2014-09-09_ by _Murta_

## フォーム入力時のフリーメールドメイン制限

サイト訪問者が Gmail や Yahoo などの無料のメールドメインを使用してフォームを送信することを制限するとします。 これを行うには、Marketo フォームを使用して、ページのソースコードに以下のスクリプトを含めます。 業務以外のメール（Gmail、Hotmail など）を入力したかどうかを確認し、入力した場合はMarketoのフォーム送信を防ぎます。 9 行目を変更して制限するドメインを含めることで、ブロックされたメールドメインのリストを拡張できます。

Posted on _2014-09-09_ by _Murta_

## API 経由でアクセスできないフィールドのデバッグ

このフィールドに移動する場合は <https://nation.marketo.com/> SOAP API を使用してフィールド AnnualRevenue を更新しようとすると、応答ではレコードが更新されたと言われますが、AnnualRevenue フィールドは変更を保持しません。 リードデータベースを使用してフィールドを手動で更新しようとすると、このフィールドに対する変更も保持されません。 管理者でフィールドがブロックされているかどうかを確認します。 もう 1 つ発生する可能性があるのは、SFDCから同期されたアカウントフィールドである可能性があることです。 多くの場合、SFDCが記録システムであるため、これらのフィールドへの変更はデフォルトでブロックされます。 1）作成日 2） Marketo SFDC ID 3） Marketo固有コード 4） SFDC タイプ 5）更新日 6）緊急度 7）優先度 8）販売作成日

Posted on _1970-01-01_ by _Murta_

## Marketo ランディングページへのカスタムコードの追加

Marketo ランディングページにGoogle Analyticsなどのサードパーティのトラッキングスクリプトを追加するとします。 これは、Marketo UI を通じて実行できます。 より一般的には、以下の手順に従って、任意のカスタムコード（HTML、CSS、JavaScript）をMarketo ランディングに追加できます。

1. ランディングページを選択し、「ドラフトを編集」をクリックします。
1. HTML要素内をドラッグします。
1. カスタムコードを入力し、「保存」をクリックします。

Posted on _2014-09-10_ by _Murta_

## サーバーサイドのフォーム投稿

`https://community.marketo.com/MarketoResource?id=kA650000000GsXXCA0`

Posted on _2014-09-11_ by _Murta_

## Forms 2.0 送信からのMarketo トラッキング Cookie の消去

### 概要

Forms 1.0 では、Munchkin トラッキング cookie の値が DOM のフィールドとして含まれていました。 これは、他のすべての入力と共に送信されました。 [Forms 2.0](/help/javascript-api/forms-api-reference.md) このフィールドを省略し、フォームの読み込み時ではなく送信時に動的に値を入力します。 これは通常は許容できますが、意図しないトラッキングと事前入力を避けるためにトラッキング Cookie をクリアする必要がある、ユースケースのクラスが作成されます。 例えば、Marketoのお客様が同じデバイスで同じフォームを使用し、複数のユーザーから連絡先情報を取得している展示会で発生する可能性があります。 以下のスニペットを使用すると、ユーザーのブラウザーから cookie 自体を削除することなく、フォームの送信時に cookie の値をクリアすることができます。

### コードサンプル

このスニペットでは、ページ上に 1 つのフォーム読み込みが想定されています。 フォームが複数ある場合は、[loadForm メソッドまたは getForm メソッド ](/help/javascript-api/forms-api-reference.md) を使用してコールバックを実装する必要があります。

```javascript
<script>
//add a callback to the first ready form on the page
MktoForms2.whenReady( function(form){
 //add the tracking field to be submitted
        form.addHiddenFields({"_mkt_trk":""});
        //clear the value during the onSubmit event to prevent tracking association
 form.onSubmit( function(form){
  form.vals({"_mkt_trk":""});
 })
})
</script>
```

Posted on _2014-09-11_ by _Kenny_

## 2014 年 9 月リリースアップデート

### REST API の更新

[ 複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) API に新しいオプションフィールド値を追加しました。この API は、リードレコードに関連付けられたMunchkin cookie の値を返します。 リクエストに「?fields=cookies」を追加するだけです。

Posted on _2014-09-16_ by _Murta_

## RTP API からMarketo フォームに場所データを追加する

**このブログ投稿で説明されているユースケースを実装するには、アクティブな RTP および MLM 購読が必要です。**
[RTP JavaScript API](/help/javascript-api/web-personalization.md) および [Marketo Forms 2.0](/help/javascript-api/forms-api-reference.md) を使用すると、RTP から推論された場所データを取り込み、フォーム入力を介してMarketoにプッシュできます。 これにより、最新のフォームアクティビティで、ユーザーの推測される場所（IP アドレスに基づく）を確認できます。 開始するには、Marketoで 3 つのカスタム文字列フィールドを作成する必要があります。 これは、CRM （Marketoとのネイティブ統合がある場合）またはMarketoの「管理者」セクションの「フィールド管理」メニューから実行できます。 これらのフィールドには、「最新の国」、「最新の状態」、「最新の市区町村」という名前を付けることをお勧めします。 この命名規則を使用して、このブログを続けます。 これらのフィールドの API 名は、「mostRecentCountry」、「mostRecentState」、「mostRecentCity」です。 場所データを取得するには、[RTP メソッドを使用して訪問者の場所データを取得し ](/help/javascript-api/web-personalization.md)Marketo Forms 2.0 から [addHiddenFields および vals メソッド ](/help/javascript-api/forms-api-reference.md) を使用してフォームに渡します。ページに RTP JS タグとMarketo フォームを追加します。 次に、以下のスクリプトを含めます。 上記とは異なる命名規則を使用する場合は、サンプルコード内のターゲットフォームフィールドの名前を変更する必要があります。

```javascript
<script>
//modify the form and grab the user
MktoForms2.whenReady( function(form) {
        //add the hidden fields to the form
 form.addHiddenFields({
  "mostRecentCountry":"",
  "mostRecentState":"",
  "mostRecentCity":""});
 //Grab the visitor data, a JS object with it is passed in the callback function of the third argument
 rtp('get','visitor',function(visitor){
  //add the desired info from the visitor object to the form fields
  form.vals({
   "mostRecentCountry":visitor.results.location.country,
   "mostRecentCity":visitor.results.location.city,
   "mostRecentState":visitor.results.location.state});
  }
  );
 });
</script>
```

Posted on _2014-09-17_ by _Kenny_

## Marketo ランディングページのクローリングと検索インデックス作成をブロックする

Marketo ランディングページがクロールされず、Googleなどの検索エンジンによって結果に表示されないようにする場合を考えてみましょう。 その方法を次に示します。

1. Marketoにログインし、ランディングページを選択します。 次に、「ドラフトを編集」をクリックします。
1. 「ランディングページのアクション」をクリックします。 次に、「ページのメタタグを編集」をクリックします
1. 「ロボット」フィールドを「インデックスなし、フォローなし」に変更します。 次に、「保存」をクリックします。

Posted on _2014-09-19_ by _Murta_

## Marketo REST とSOAP API の FAQ

**更新：2016 年 3 月** Marketo [REST](/help/rest-api/rest-api.md) および [SOAP](/help/soap-api/soap-api.md) API に関するよくある質問への回答を以下に示します。 **Q:Marketo REST API とSOAP API の主な違いは何ですか。** A:REST API およびSOAP API を使用して特定のデータをプッシュ/プルする機能はほとんど重複していますが、REST API またはSOAP API のいずれかにのみ存在する特定の機能があります。 パフォーマンスに関しては、REST API はSOAP API よりも優れた [ スループット ](https://en.wikipedia.org/wiki/Throughput) を備えています。 認証モデルに関しては、REST API には、有効期限が切れるトークンを使用する認証モデルがあります。 また、REST API からMarketo[assets](https://developer.adobe.com/marketo-apis/api/asset/) にもアクセスできます。   **Q:SOAP API では使用できない、REST API で使用できる機能には何がありますか。** A:[List of lists API](/help/rest-api/list-of-standard-fields.md)、[list API からリードを削除 ](/help/rest-api/lead-database.md)、[Usage API](/help/rest-api/rest-api.md) および [Error API](/help/rest-api/rest-api.md) は、REST API でのみ使用できます。 **Q:SOAP API で使用できる API の数を増やす予定はありますか。A** いいえ。 **Q:REST API で使用できる API の数を増やす予定はありますか。** A：はい。 現時点では、Marketo API 開発の主な焦点は REST です。

Posted on _2014-09-20_ by _Murta_

## サーバーサイドのフォーム投稿

**メモ：これは非公開のサポートされていない API で、サポートされておらず、動作はいつでも変わる可能性があり** す。web サイトで独自のフォームを使用する場合でも、サーバーサイドの投稿を使用してMarketoにこのデータを送信できます。 このアプローチの利点は、既存のフォームとアプリケーションロジックを維持できても、Marketoへの実際のフォーム投稿を使用できることです。 これにより、Marketo ユーザーに「フォームに入力」イベントが提供され、自動プロセスのトリガー化またはセグメント化に使用できます。 **メモ：1 つの IP アドレスに対して、1 分あたり 30 サーバーサイドのフォーム投稿のレート制限があります。** スクリプティング言語またはプログラミング言語ごとに、サーバーサイドのフォーム送信を実行するオプションは異なります。また、Post 呼び出しに使用できるオブジェクトやメソッドも異なる場合があります。 例えば PHP では、多くの人が cURL ライブラリを使用します。 いずれの場合も、指定した URL に対して名前と値のペアをポストします。 名前は、Marketo フィールドの API 名と同一である必要があります。 さらに、フォーム送信を正しく取得するために、いくつかのシステムフィールドを含める必要があります。

1. フォームを作成します。 最初の手順は、Marketoでフォームを作成するか、送信する既存のフォームを使用することです。 フォームの名前は、説明的である必要がありますが、実際にはフォームフィールドは必要ありません。 新しいフォームを作成する場合は、名前を入力し、「フォームエディターを開く」ボックスのチェックを外すだけで、完了です。
1. フォーム ID を検索します。 Marketo UI で、フォームを選択し、URL を確認します。`https://app-x.marketo.com/#FO8B2ZN12` の形式である必要があります。 #記号の後ろに、「FO」の直後の数字を見て、フォーム ID を見つけます。 この場合、フォーム ID は 8 です。 場合によっては、最初のフォームに 1001 という番号が付けられ、そこからカウントされることがあります。 フォーム ID は変数なので、様々なフォームの送信をトリガーできます。
1. Marketo アカウント ID を取得します。 管理者/ Munchkinに移動し、Munchkin アカウント ID （000-AAA-000 の形式）をコピーします。この情報が必要なため、フォームが正しいMarketo インスタンスに送信されます。
1. POST URL を決定します。 Marketoのユーザーインターフェイスで、通常は `<http://app-x.marketo.com/>` という形式で、ロケーションバーにドメインをメモします。 スラッシュの後はすべて破棄し、「index.php/leadCapture/save」を付加して完全な形式の POST URL を取得します。 メモ 1：これは大文字と小文字を区別します。 メモ 2:Marketo サンドボックスは、実稼動Marketo システムとは異なるドメインを持つ場合があります。 そのため、URL の例は次のようになります。`http://app-x.marketo.com/index.php/leadCapture/save` HTTP の代わりに HTTPS を使用することもできます（セキュリティの例外が発生するので、CNAME を使用しないでください）。
1. フォームフィールド名を見つけ**す。管理/フィールド管理に移動し、「フィールド名の書き出し」ボタンをクリックして、API フィールド名を含むスプレッドシートをダウンロードします。 API 名を名前と値のペアの名前として使用します。
1. 投稿するフィールドを決定します。 フォーム送信には、任意のMarketo リードフィールドを含めることができます。 フィールド名では大文字と小文字が区別されることに注意してください。 送信するフィールドに加えて、次の 2 つの必須フィールドと 2 つの推奨フィールドがあります。フォームの必須フィールド : （1） `munchkinId` – このフィールドは、Munchkin アカウント ID に使用されます。（2） `formid` – このフィールドは、Marketoのどのフォームが送信されたかを示します。フォームの推奨フィールド : （1） メール – このフィールドは、重複排除のプライマリキーとして使用されます。 Marketoは、Marketo データベース内で一致するメールアドレスを見つけると、既存のレコードを更新します。それ以外の場合は、新しいレコードを作成します。 複数の一致がある場合は、最近更新されたレコードを更新します（2） `_mkt_trk` – このフィールドには cookie 情報が格納されているので、個人の web ページ訪問を追跡できます。 フォームページにMunchkinがある場合、Munchkinはこの非表示のフォームフィールドに値を自動入力します。 そうでない場合は、同じ名前の Cookie から読み取り、このフィールドでMarketoに渡します。 メモ：Marketo フォームへの POST の本文は URL エンコードする必要があります。
1. 応答を参照してください**フォーム投稿への応答は、HTTP 302 リダイレクトコードになります。 一部のシステムでは、これはエラーとして表示されます。 ただし、この場合は、リードが正常に作成または更新されたことを意味します。 エラーが発生した場合は、4xx または 5xx のエラーコードが表示されます。

次に、この手法を購読解除シナリオに使用する方法について [ 投稿 ](https://nation.marketo.com:443/t5/product-blogs/how-to-build-an-external-subscription-center/ba-p/242185) します [Justin Cooperman、シニアプロダクトマネージャー ]

Posted on _2014-11-07_ by _Murta_

## 特定の日付範囲で更新されたリードを検索

[Marketo API](/help/soap-api/soap-api.md) を使用して特定の日付に更新されたリードを検索するとします。 これは、[getMultipleLeads SOAP API](/help/soap-api/getmultipleleads.md) で可能です。 このメソッドは、リクエストした日付範囲に、Marketoでデータ値が変更された、または新しいアクティビティを持つリードを返します。 `leadSelector` の場合は、`LastUpdateAtSelector` を指定します。 次に、`oldestUpdatedAt` と `latestUpdatedAt` の時間範囲を持つ日付範囲を定義します。 2014 年 6 月 6 日午前 12 時（PST）から 2011 年 6 月 7 日午前 12 時（PST）の間に更新されたリードを見つける方法を示す、以下のリクエスト XML のサンプルを参照してください。 注意：日付範囲は 30 日を超えないようにします。

**日付別に更新されたリードを検索するリクエスト XML のサンプル**

```xml
<soapenv:Envelope xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
<soapenv:Header>
<mkt:AuthenticationHeader>
<mktowsUserId>REPLACE</mktowsUserId>
<requestSignature>REPLACE</requestSignature>
<requestTimestamp>2014-10-23T12:19:51-07:00</requestTimestamp>
</mkt:AuthenticationHeader>
</soapenv:Header>
<soapenv:Body>
<mkt:paramsGetMultipleLeads>
<leadSelector xsi:type="mkt:LastUpdateAtSelector">
<oldestUpdatedAt>2014-06-06T00:00:00-08:00</oldestUpdatedAt>
<latestUpdatedAt>2014-06-07T00:00:00-08:00</latestUpdatedAt>
</leadSelector>
</mkt:paramsGetMultipleLeads>
</soapenv:Body>
</soapenv:Envelope>
```

Posted on _2014-09-24_ by _Murta_

## メールへの動的コンテンツの追加

例えば、毎日メールを送信し、その日の日付をメールテンプレートに自動的に含めたいとします。 これを行うには、Marketoでトークンとメールスクリプティングを使用します。

1. トークンを作成します。** トークンを使用するプログラムに移動します。 マイトークンをクリックします。
1. メールスクリプトをダブルクリックします。 次に、このトークンに名前を付けます。 次に、「編集」をクリックします。
1. 以下のメールスクリプトをこのウィンドウに貼り付けます。 次に、「保存」をクリックします。

## Velocity のカレンダーオブジェクトへのアクセス

`set($x = $date.calendar)`

## 日付を書式設定

`set($current_date = $date.format('dd-MM-yyyy', $x.getTime()))`

## 今日の日付を返します

`$current_date`

1. メールテンプレートのトークンを参照します。** トークンの名前をメモしておきます。 メールドラフトに移動します。 トークンを含めます。  メールが送信されると、トークンの値が入力されます。 詳しくは、[ メールスクリプティング開発者向けドキュメント ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/email-scripting) を参照してください。

投稿日：_2014-11-22_ by _Murta_

## Bash セキュリティアドバイザリ

Marketoは、Bash の脆弱性である [Shellshock （CVE-2014-6271） ](https://nvd.nist.gov/view/vuln/detail?vulnId=CVE-2014-6271) を徹底的に調査し、これらの攻撃の影響を受けないと結論付けました。 また、[CERT recommendation](https://www.cisa.gov/news-events/alerts/2014/09/25/gnu-bourne-again-shell-bash-shellshock-vulnerability-cve-2014-6271) に対応するため、最新版へアップデートすることで予防措置を講じています。

Posted on _2014-09-26_ by _Murta_

## SOAP API 資格情報の更新方法

[SOAP API](/help/soap-api/soap-api.md) 資格情報を定期的に更新することをお勧めします。 現在、Marketo API を使用してプログラムでこれを行う方法はありません。 以下の手順は、Marketo UI を使用してSOAP API 資格情報を更新する方法を示しています。

1. 「管理者」セクションに移動し、「web サービス」をクリックします。
1. 10 文字以上の暗号化キーを設定し、「変更を保存」をクリックします。

Posted on _2014-09-29_ by _Murta_

## Marketo データベースをクリーンアップする方法

**メモ：これはゲストのブログ投稿です。 Josh Hill は、マーケティング自動化機関の Perkuto でMarketo Practice Lead を務めています。 Josh は、マーケティング、セールス、テクノロジーの交差点で働き、収益創出システムを提供しています。 彼はマーケティングオートメーションと需要の生成について [MarketingRockstarGuides.com](https://www.marketingrockstarguides.com/) で書いています。** Marketo データベースをクリーンに保つことは、この強力なシステムを管理する上で重要な役割を果たします。 Marketoのデータが汚れていたり、CRM のデータが汚れていたりすると、キャンペーンが間違った人物に送信された理由やレポートが「方向性」を持つ理由を説明するので、マーケティングマネージャーとしての仕事が非常に難しくなります。 [Gartner の 2011 年の調査では ](https://www.data.com/export/sites/data/common/assets/pdf/DS_Gartner.pdf) データの質が低いと、労働生産性が 20% 低下したと指摘しています。 これは、データを修正する必要があったために無駄になっている時間の 20% （1 週間あたり 8 時間または 1 日）です。 しかし、ターゲティングが間違っていたために失われた売上高と比較すると、この損失は青ざめています。 データをクリーンな状態に保つために投資する理由のトップ 5 を以下に示します。- リードとクライアントのより良いセグメント化が可能になり、適切なタイミングで適切な人物にメッセージを集中させることができます。 この 20% オフのクーポンは、新規見込み客にのみ適用され、最高のクライアントには適用されません。 - メールを重複して送信しないようにします。 すべての予防措置にもかかわらず、通常、重複レコードが結合されないことが原因で、同じリードに複数のメールを送信することが可能です。  – 上司への正確な報告。 CMO は収益テーブルの席に配置されるので、正確で一貫性のある繰り返し可能なレポートを用意する必要があります。そうしないと、収益マーケターになることはできません。  – 営業交渉中に主要な見込み客に間違ったマーケティング資料を E メールで送信すると、保留中の取引が損なわれる。

データベースがライフサイクルステージでその詳細を提供しない場合、1 つか 2 つの取引を沈没させる可能性があります。  – 不正なリードや古いリードを削除して、価格のしきい値を下回るようにします。 悪いデータのコストについては多くのものが書かれています。 最も直接的な懸念事項は、多くの不正、重複、または古いリードによって、MarketoまたはSalesforceの価格帯が超過しているので、1 年に数千人単位の料金が発生する可能性があることです。 データベースをクリーンな状態に保つにはどうすればよいでしょうか。 データのクリーン性に関するこれらの原則に従うことができますが、Marketo内でのデータのクリーン性の実現にはどうすればよいでしょうか。 お使いのシステムに関していくつかの前提を立てます。– 標準のMarketo システムがあります。  – 通常、リードと連絡先のアカウントのSalesforceが設定されています。 - システム間ですべてのレコードを同期しています。  – 意図的な重複を使用していない。

適切なリードを見つけて修正**最初に、潜在的な問題であるリードを見つけましょう。 クライアントごとに、一連のスマートリストを調べて、データベースの正常性を判断します。 私はあなたが月単位で同じことをすることをお勧めします。 スマートリストが機能するようになると、ユーザーは月に 15 分以内で作業を完了できます。 これは、作業とMarketoの ROI を示すための優れた方法です。 データベースに与える合計影響を把握するためのテーブルを作成します。 次の例には、検索する条件が含まれているので、ビジネスにとって重要な他のフィールドを必ず含めてください。 Marketoのみ、SFDC リードおよびSFDC連絡先で各グループを分類します。

自動化を使用したデータ値の修正：一般的なスペルミスやデータ欠落を修正するための自動化ルールの使用は、何十年も前にさかのぼります。 1960 年代には、ダイレクトメールを送信する際のデータ品質が低いと、何千ドルもの無駄が生じる可能性がありました。 今日では、データ品質のミスは、間違ったメールよりも早く評判を台無しにします。 メールの評判、言語の選択、顧客体験は重要です。間違いは数分で一般に広がる可能性があるからです。 自動データクレンジングで会社の評判を節約します。 これらのデータ管理フローは、Marketoで最初に設定する作業の 1 つです。 ほとんどの企業は同様のフローを設定します：- カントリーコレクター（これを必要としないためには原則 1 に従うべきでしたが） – ステートコレクターまたはマッパー – 国と推定状態がある場合に役立ちます。  – 従業員範囲に対する従業員数。  – 悪いリード Sourceから良いリードにSource - メールが変更された場合、メールは無効になり良いリードになります。  – 古いフィールド値を新しいフィールドに変換する（完全から空）。 たとえば、このフローでは、従業員番号に基づいて従業員範囲が調整されます。

データ追加ツール データベースをより良くセグメント化するには、空のフィールドに入力することが重要です。 リードは、必ずしも適切な業界や職務を記入するとは限らず、フォームのタイトルを記入する場合もあります。 古いシステムのレガシーデータが存在する場合があります。 データが不足しているということは、そのメールをより少ない人に送信するか、間違った人に送信する必要があるということです。 これを修正するには、データ追加ツールが必要です。

オプション 1：自分で入力します。 データを補間して、空のフィールドをバックフィルできる場合があります。 業界名や年間売上高と年間売上高の範囲の代わりに SIC コードがある場合があります。 Marketoでは、これらの修正を簡単に自動化できます。

オプション 2:LaunchPoint を介してデータ追加/エンリッチメントベンダーを見つける [Launchpoint には、リードデータのエンリッチメントに役立つ NetProspex や ReachForce など ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) 複数のベンダーがあります。 データのシートを要求するユーザーもいます。その後、データを消去して送り返します。 より良い方法は、MarketoまたはSalesforceの自動化されたツールです。このツールでは、必要なフィールドをチェックし、適切なデータをプッシュします。 ほとんどのベンダーは、[Marketo API または Webhook](/help/home.md) を使用してこれを実現しています。

オプション 3:Marketo API を使用してリードを更新するMarketo API を使用して、クレンジングする必要があるリードを特定し、API を使用して更新できます。 [ フィルタータイプ REST API による複数のリードの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) は、特定の条件に一致するMarketoからデータを取り出すための出発点として適しています。 リードを更新するには、[ リード REST API を作成/更新 ](/help/rest-api/leads.md) を参照してください。

または、[Marketo Webhook](/help/webhooks/webhooks.md) を設定して、フォームの入力など、特定のイベントが発生したことを外部システムに通知することもできます。 その後、リードを更新する値を返すことができます。

何を自動化する必要があるか。 私はステップ 1 でいくつかの提案をしました。 しかし、より多くのデータベースをクリーンアップする場合は、データ値を修正する以上の作業を行う必要があります。  – 競合他社のブラックリストへの登録：競合他社の収集とブラックリストへの登録を自動化していることを確認します。 競合他社のパートナーがいる場合でも、それらを適切にマークし、リストに配置して抑制することは可能です。   – 複数のハードバウンス：このフローは必ず自動化します。 リードが 30 日間に 2 回以上ハードバウンスした場合は、そのリードを「休止」または「無効」に設定します。 その後、月に 1 回、イシューがタイプミスだったかどうかを確認します。  - 30 日以内に複数のソフトバウンス：これらを 30 日間、マーケティングの中断=TRUE に設定します。  - スパムトラップの停止/削除：製品がスパムトラップアドレスを使用する可能性がある場合は注意が必要です。 スパムトラップのリストを参照してください。 スマート・リスト。

**自動化しないもの** 間違ったレコードを誤って一括削除するリスクが高すぎるため、リードの削除を自動化しないでください。 代わりに、1 か月に 1 回、ごみ箱としてマークされたリードをレビューします。 ただし、ハッシュ化されたリードを削除する場合は、30 日間の待機で次のようなフローを実行します。

注意事項：自動化を使用すると、時間を節約し、データベースをクリーンに保つことができます。 自動処理は両刃の剣です。間違って設定すると、数分で大混乱を引き起こす可能性があります。 これらのプロセスを実行する際は注意が必要で、すべてのユーザーが常に情報を把握するようにします。 通常、SFDCの連絡先は、アクティブなオポチュニティ、クライアント、元クライアントである可能性が高いので、削除しないことをお勧めします。 財務部門または法務部門から特定のレコードの保持が要求される場合があり、そのレコードには連絡先が添付されます。 代わりに、ハードバウンス、無効、または既に無効になっている連絡先に焦点を当てます。 これで、Marketo データベースをクリーンに保つためのテクニックをいくつか学びました。 API や Webhook を使用してこれらのプロセスを自動化する他の方法を考え出した場合は、お知らせください。

投稿日：_2014-10-08_ by _Josh_

## 2014 年 10 月リリースアップデート

### 外部ページの事前入力

Marketo forms は、Marketo ランディングページ以外で読み込まれた場合、ネイティブの事前入力機能を提供しません。 ただし、[Marketo API と ](/help/rest-api/rest-api.md)2&rbrace;Forms 2.0 JavaScript API[ を使用して、これを実装することはできます。 ](/help/javascript-api/forms-api-reference.md/)最初の手順は、サーバーからの REST 呼び出しを使用して、Marketoからリードデータを取得することです。 サーバーからリード ID またはその他の一意の ID を相互参照する手段がすぐにはないのであれば、Munchkin Cookie 「_mkto_trk」を使用して、[Get Leads By Filter Type メソッド ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) を使用してMarketo サーバーからデータを取得する必要があります。
この呼び出しを行うには、インスタンスから認証エンドポイントと REST エンドポイントが必要です。 Marketo インスタンスで認証が完了したら、リード API を呼び出す必要があります（`https://<host>/rest/v1/leads.json`）。 次に、次のように、Marketo cookie に対してフィルタリングするクエリ文字列を作 `?filterType=cookie&filterValues=` する必要があります。 クライアントからサーバーに送信された「_mkto_trk」キーから、特定の値を取得する必要があります。 メモ：_mkto_trk cookie の値にはアンパサンドが含まれており、Marketo エンドポイントで適切に受け入れられるよ `%26` に URL でエンコードする必要があります。 デフォルトでは、リード API は 4 つのフィールド（`id`、`email`、`firstName`、`updatedAt`）を返します。 特定のフィールドのセットを設定するには、次のようにフィールド名をコンマで区切った `fields` クエリパラメーターを含める必要があります。`&fields=email,firstName,lastName,company` 最終的に、呼び出しは次のようになります。

`https://<host>/rest/v1/leads.json?filterType=cookie&filterValues=<cookie>&fields=email,firstName,lastName,company&access_token=<token>`

この呼び出しを行うと、次のような JSON オブジェクトが返されます。

```json
{
    "requestId":"e42b#14272d07d78",
    "success":true,
    "result":[
        {
        "id":50,
        "firstName":"Kenny",
 "lastName":"Elkington",
        "email":"<mkto@example.com>",
 "company":"Marketo Inc."
        }]
};
```

これでリードの詳細が用意できたので、JavaScriptの whenReady および vals メソッドを使用して、これらをMarketo フォームにマッピングします。 まず、リードの結果をページの変数として設定する必要があります。

```javascript
<script>
//print your JSON object dynamically as the mktoLead variable
var mktoLead = {
    "requestId":"e42b#14272d07d78",
    "success":true,
    "result":[
        {
        "id":50,
        "firstName":"Kenny",
  "lastName":"Elkington",
        "email":"mkto@example.com",
  "company":"Marketo Inc."
        }]
}
</script>
```

ページに結果が表示されたら、それらをフォームフィールドにマッピングできます。

```javascript
<script>
MktoForms2.whenReady( function(form) {
 //set the first result as local variable
 var mktoLeadFields = mktoLead.result[0];
    //map your results from REST call to the corresponding field name on the form
 var prefillFields = {
   "Email" : mktoLeadFields.email,
   "FirstName" : mktoLeadFields.firstName,
   "LastName" : mktoLeadFields.lastName,
   "Company" : mktoLeadFields.company
   };
 //pass our prefillFields objects into the form.vals method to fill our fields
 form.vals(prefillFields);
 }
 );
</script>
```

Posted on _2014-10-24_ by _Kenny_

## メール HTML の置換

この投稿では、メールに対してMarketoによって生成されたHTMLを削除する方法を説明します。 その後、Marketoで再フォーマットすることなく、独自のHTMLを使用できます。

1. メールに移動し、「ドラフトを編集」をクリックします。
1. [ 電子メールの操作 ] をクリックし、[ HTML ツール ]、[ HTMLの置換 ] の順にクリックします。
1. このボックスのコードを自分のHTMLに置き換えます。 次に、「保存」をクリックします。

投稿日：_2014-10-28_ by _Murta_

## 訪問者の Cookie ID を取得し、関連するリードデータをクエリします

[ フィルタータイプで複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)REST エンドポイントを使用すると、ユーザーの cookie ID に基づいてリードデータをクエリできます。 例えば、この方法を使用して、Marketo以外のランディングページのフォームを事前入力できます。 この投稿では、Web ページ訪問中にユーザーの Cookie 値を取得し、その Cookie ID で [ 複数のリードの REST API を取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) クエリを実行して、ユーザーのリードデータを返す方法について説明します。 まず、ユーザーのMunchkin cookie の値「_mkto_trk」が必要です。 cookie の値を取得するために使用できるJavaScript関数の例を次に示します。 このアプローチについて詳しくは、[ この StackOverflow ページ ](https://stackoverflow.com/questions/10730362/get-cookie-by-name) を参照してください。 この関数を呼び出す前に、ページの読み込みイベント後に 500 ミリ秒の遅延を設定することをお勧めします。 これにより、Munchkinの読み込みに時間がかかり、ユーザーに cookie が設定されます。

```javascript
//Function to read value of a cookie
function readCookie(name) {
    var cookiename = name + "=";
    var ca = document.cookie.split(';');
    for(var i=0;i < ca.length;i++) {
        var c = ca[i];
        while (c.charAt(0)==' ') c = c.substring(1,c.length);
        if (c.indexOf(cookiename) == 0) return c.substring(cookiename.length,c.length);
    }
    return null;
}

//Call readCookie function to get value of user's Marketo cookie
var value = readCookie('_mkto_trk');
```

次に、&#39;_mkto_trk&#39; cookie の値をサーバーに渡します。 リードデータを取得するには、サーバーからこの cookie 値を使用して [ 複数のリードを取得 REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) を呼び出します。 インスタンスの認証エンドポイントと REST エンドポイントが必要です。 呼び出しは、次のような構造にする必要があります。

メモ：`_mkto_trk` の Cookie の値にはアンパサンドが含まれており、Marketo エンドポイントで適切に受け入れられるよ `%26` にするには、URL エンコードされる必要があります。

```java
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/leads.json"
# Replace with your access token
auth_token =  "?access_token=" + "cde42eff-aca0-48cf-a1ac-576ffec65a84:ab"
# Replace with filter type and values
filter_type_and_values = "&filterType=cookies&filterValues=id:AAA-BBB-CCC%26token:_mch-marketo.com-1418418733122-51548&fields=cookies,email"
request_url = marketo_instance + endpoint + auth_token + filter_type_and_values

# Make request
response = RestClient.get request_url

# Returns Marketo API response
puts response
```

上記の例では、電子メールと、ユーザーに関連付けられたすべての Cookie が返されます。 その後、このデータを使用して、ユーザーが訪問する後続のページをパーソナライズできます。

`{"requestId":"aa00#14a405aa786","result":[{"id":583,"email":"<testaccount@gmail.com>","cookies":"_mch-marketo.com-1418418733122-51548"}],"success":true}`

Posted on _2014-10-30_ by _Murta_

## マーケティング自動化を支援する開発者が必要なタイミング

メモ：これはゲストのブログ投稿です。 Josh Hill は、マーケティング自動化機関の Perkuto でMarketo Practice Lead を務めています。 Josh は、マーケティング、セールス、テクノロジーの交差点で働き、収益創出システムを提供しています。 彼はマーケティングオートメーションと需要の生成について [MarketingRockstarGuides.com](https://www.marketingrockstarguides.com/) で書いています。

マーケティングオートメーションプラットフォームは、すぐに使用でき、経験豊富なオペレーターの手の中で非常に強力です。 プラットフォームは、定義によって、拡張機能アプリケーションを使用して、システムがチームにとってさらに素晴らしいことを行えるようにすることができます。 Marketoのロジックエンジンには、非常に多くの機能があると思うかもしれませんが、制限があります。 Marketoはあなたのためにすべてを行うことはできないし、そうすべきでもありません。

Marketoで構築するよりも適切に機能を実行するツールが他にもあります。 Marketoのプラットフォームは非常にオープンで、アプリケーションの [LaunchPoint エコシステム ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) を構築できます。 また、この公開性を使用して、ビジネスニーズに合わせてサイトとMarketoの機能を拡張することもできます。 Marketoのようなプラットフォームの優れた点は、一般的なマーケターが、本格的なプログラマーでなくても、ページ、メール、ルーティングロジックを構築できることです。
最近のマーケターは、ロジックを理解する必要がありますが、実際のプログラミングはエキスパートに任せるのが最善です。 開発者を呼び出す必要があるタイミングを知るには、どうすればよいですか？ プログラマーが関与すべきタイミングを決定するための基本的なルールやヒューリスティックがいくつかあります。- Marketoに明らかなフィルター、トリガー、または必要な機能がない場合、多くの場合、いくつかのJavaScriptまたは jQuery で行うことができます。  – これは、Marketo単体では複雑すぎますか？ - Marketoでさえこれができますか。  – この Web サイトのカスタマイズは容易にはサポートされないのですか。 - Marketoは、web サイトや他のデータベースと通信する必要がありますか。  – パソコンで出来る様に聞こえるが、Marketoには機能がないのか。 Marketoは標準機能を提供していない場合もありますが、多くのサードパーティ統合やカスタム接続には接続しません。

[LaunchPoint Marketplace](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) でこれらのカテゴリをいくつか見てみましょう。- [Analytics ツール ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) - [ データ追加 ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) - [ コンテンツ管理システム ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) 一部のサードパーティアプリケーションでは、プラットフォーム内で直感的なコントロールパネルと設定ツールを利用できます（GoToWeb セミナー）。 これらは「ネイティブ」統合であり、必要な作業のほとんどは、ログインを設定してMarketoで使用することです。 ただし、他の拡張機能では、より直接的にプログラムする必要がある、より複雑な API を使用する必要があります。

**Marketo統合オプション** - LaunchPoint 統合 – 通常、ログインまたは簡単な設定。 - API 統合：API とプログラミングの設定が必要です。（1） [REST API](/help/rest-api/rest-api.md) （2） [SOAP API](/help/soap-api/soap-api.md) （3） [Webhook 統合 ](/help/webhooks/webhooks.md) – 特別なコードの設定が必要ですが、かなり簡単です。 （4） [ メールスクリプティング ](./email-scripting.md) （速度） – JavaScriptと jQuery:（1） [Forms 2.0](/help/javascript-api/forms-api-reference.md) （2） [ リードトラッキング（Munchkin） ](/help/javascript-api/lead-tracking.md) （3） [RTP JS](/help/javascript-api/web-personalization.md) 以下に、デベロッパーを使用してMarketo プラットフォームの機能を拡張するユースケースを示します。 これらのユースケースはありますか？ その場合は、開発者に問い合わせる時間かもしれません。 [LaunchPoint のサービスパートナーセクションにアクセスします ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO)。

投稿日：_2014-11-06_ by _Josh_

## SlackとMarketoの統合

[Slackはエンタープライズ コラボレーション プラットフォーム ](https://slack.com/) です。 チームがSlackを使用している場合は、Marketoの通知をワークフローに簡単に取り込むことができます。 この投稿では、Marketoで特定のリードアクティビティが発生した場合にチャットログに通知を追加する方法を説明します。 考えられるユースケースとしては、フォームの記入、価格ページへの訪問、30 日以内に連絡されていないリードについてチーム全体に通知することが挙げられます。 次のスクリーンショットは、このヘルプ記事の手順に従った後、SlackでMarketo通知がどのように表示されるかを示しています。

1. Slackにログインします。 Slackでの「統合」をクリックします。
1. 受信 Webhook の「追加」ボタンをクリックします
1. Marketo通知用のチャネルを選択します。 次に、「受信 Webhook 統合を追加」をクリックします。
1. Webhook URL （手順 8 で必要）をコピー&amp;ペーストします。
1. 通知の名前を選択
1. Marketoにログインします。 管理者に移動します。 Webhook をクリックします。
1. 「新規 Webhook」をクリックします
1. Webhook の名前を入力します。 手順 4 の Webhook URL を入力します。 リクエストタイプとして Post と入力します。 ペイロードテンプレートを入力します。

スクリーンショットのペイロードテンプレートを以下に示します。 リードレベルの名、会社およびメールアドレスのトークンを使用します。

`payload={"text": "DEVELOPER SITE ALERT: {{lead.First Name:default=edit me}} {{lead.Company=edit me}}, {{lead.Email Address:default=no email address}}" }`

1. Marketoでトリガーキャンペーンを設定します。 フローステップは、Webhook をSlackに呼び出すことです。 スマートリストは web ページ訪問です。
1. 動作することを確認します。

Marketoの Webhook について詳しくは、[ 開発者向けドキュメント ](./webhooks/webhooks.md) を参照してください。

Posted on _2014-11-10_ by _Murta_

## Litmus とMarketoの統合

[Litmus は、ブラウザーとメールクライアントをまたいでメールをテストするためのサービスです ](https://www.litmus.com/)。 Litmus では、クリック数、開封数、削除数など、メールに関する分析も提供しています。 この投稿では、Marketoと Litmus を統合する方法について説明します。

1. Marketoでメールプログラムを設定する際に、プログラムダッシュボードの「マイトークン」をクリックします
1. 「メールスクリプト」トークンを中央のパネルにドラッグして追加します。
1. トークンに名前を付け、「Click to edit」をクリックします。
1. 右側の「標準オブジェクト」の下にある「リード」カテゴリを展開します。 「メールアドレス」フィールドを見つけて、ボックスをオンにします。 この同じページの左側にある空のスクリプトスペースに、Litmus から提供されるトラッキングコードを貼り付けます。 Litmus コードで、`{{lead.Email Address}}` のすべてのインスタンスを `${lead.Email}` に置き換えます。 「保存」をクリックして Lightbox ウィンドウを閉じ、トークンページで再度「保存」をクリックします。
1. トークン `{{my.LitmusToken}}` の名前をメモしておきます。 トラッキングするメールを開きます。 メールの一番下に、新しいスクリプトトークンを配置します。 Litmus バージョンの `{{my.LitmusToken:default=editme}}` に一致するように、デフォルトの情報を追加することもできます。

メールが送信されると、スクリプトはMarketoによってメールに配置されます。

Posted on _2014-11-18_ by _Murta_

## Marketoのランディングページが Facebook で共有される場合の画像の指定

例えば、Facebook でMarketoのランディングページを共有する際に、画像を自動的に表示するとします。 この画像をMarketoのランディングページ自体ではなく、Facebook のシェアに表示したい場合もあります。 これを行うには、Marketo ランディングページに開いたグラフのメタタグを追加します。 これを行う手順を以下に示します。

1. ランディングページを選択します。次に、「ドラフトを編集」をクリックします。
1. 「ページのメタタグを編集」をクリックします。
1. Facebook OG タグセクションにオープングラフメタを追加します。 次に、「保存」をクリックします。 次の形式を使用します。`<meta property="og:image" content="http://example.com/example.jpg"/>`

詳しくは、オープングラフメタタグに関する [Facebook の開発者向けドキュメント ](https://developers.facebook.com/docs/sharing/best-practices) を参照してください。

投稿日：_2014-11-17_ by _Murta_

## リファラーに基づくリダイレクトページ

Marketo ランディングページへの直接トラフィックを防ぐとします。 このページに、PDFなどのダウンロード可能なコンテンツがあり、受信する前にユーザーがフォームに最初に入力できるようにしたい場合を考えてみましょう。 この問題を解決するには、ユーザーが特定のページから来たことを確認します。 この場合、ユーザーがフォームに入力する必要があるページになります。 ユーザーがそのページから送信されたのではない場合は、フォーム入力ページにユーザーをリダイレクトできます。 これを行うには、コンテンツを含んだランディングページへのリファラーページがフォーム入力ページかどうかを確認する必要があります。
以下のスニペットにある `http://example.com/PageWithForm` の両方のインスタンスを、このユーザーの元となるページへのリンクに置き換えます。 これは、フォーム入力ページである可能性があります**。

```javascript
<script>
window.onload = function() {
  if (document.referrer !== "http://example.com/PageWithForm") {
    document.location.href = "http://example.com/PageWithForm";
  };
 };
</script>
```

コンテンツを含むMarketo ランディングページの終了タグの前に、カスタマイズしたJavaScript スニペットを含めます。** ユーザーがフォーム入力ページのコンテンツを含んだランディングページに送信されない場合、ユーザーはフォーム入力ページにリダイレクトされるようになりました。

Posted on _2014-11-18_ by _Murta_

## Trello とMarketoの統合

Trello は [Web ベースの一般的なプロジェクト管理アプリケーション ](https://trello.com/) です。 チームで Trello を使用している場合は、Marketoの通知を簡単にワークフローに取り込むことができます。 この投稿では、Marketo通知を含むカードを Trello ボードに追加する方法を示します。 このカードは、Marketoで特定のリードアクティビティが発生した場合に追加されます。 考えられるユースケースとしては、フォームの記入、価格ページへの訪問、30 日以内に連絡されていないリードについてチーム全体に通知することが挙げられます。

1. Trello にログインします。 Marketo通知を追加する Trello ボードに移動します。 [ リストの追加 ] をクリックし、名前を付けます。
1. 「サイドバーを表示」をクリックします。 「E メール送信設定」をクリックします。 「このボードのメールアドレス」ボックスにメールアドレスが入力されていることに注意してください。 このメールは、手順 6 で使用します。 Marketo通知を追加するリストを選択します。
1. Marketoにログインします。 新しいスマートキャンペーンをクリックします。 名前を入力し、「保存」をクリックします。
1. スマート・リストに移動します。 このスマートキャンペーンのトリガーを選択します。 以下の例では、フォーム入力トリガーを使用します。 入力フォームトリガーを中央のパネルにドラッグします。 この通知をトリガーにするフォームを選択します。
1. メールを作成します。「新規」をクリックします。 「ローカルアセット」をクリックします。 「新規メール」をクリックします。 メールに名前を付けます。 次に、「作成」をクリックします。
1. 手順 5 で作成したメールの「ドラフトを編集」をクリックします。 トレローカードに表示する関連トークンをドラッグします。 Marketoメールの件名が Trello カードのタイトルに表示され、Marketoメールの本文が Trello カードの説明に表示されます。 例えば、リードの姓と名を Trello カードのタイトルに使用する場合は、「LEAD ALERT: `{{lead.First Name:default=edit me}}` `{{lead.Last Name:default=edit me}}`」と入力します。 次に、メールを承認します。
1. Smart Campaign に移動します。 「フロー」をクリックします。 中央のパネルに [ アラートの送信 ] をドラッグします。 作成したばかりのメールを選択します。 「送信先」を「なし」に設定します。 手順 2 の Trello メールとして、「To Other Emails」を選択します。
1. 上部のメニューで「スケジュール」をクリックします。 アクティブ化をクリックします。 「確認」をクリックします。
1. 統合をテストします。 タイトルにリードの姓と名が含まれているカードが Trello ボードに表示されます。 詳しくは、[Trello のドキュメント ](https://support.atlassian.com/trello/) を参照してください。

Posted on _2014-11-18_ by _Murta_

## カスタムフィールド値でリードを検索

アクティビティまたは非アクティビティの特定の条件に一致するリードをMarketo API から取得するとします。 例えば、過去 30 日間にスコアが変更されていないリードを検索したい場合があります。 この投稿の手順に従うと、このリードのリストを取得できます。 これを行うには、Marketoで、過去 30 日間にスコアが変更されていないリードを特定するスマートキャンペーンを作成したあと、これらのリードに値を保存してリードを特定します。 次に、この値で API に対してクエリを実行します。

1. customLeadStatus という新しいカスタムフィールドを作成**Marketoにログインし、管理パネルに移動します。 「フィールド管理」をクリックします。 「新しいカスタムフィールド」をクリックします。  フィールドに名前を付けます。次に、「作成」をクリックします。
1. 30 日以内に更新されていないリードを検索するスマートリストを含むスマートキャンペーンを作成します。**新規スマートキャンペーン」をクリックします。 新しいスマートキャンペーンに名前を付けます。 ドラッグ非スコアが右のパネルから中央のパネルに変更されました。
1. 手順 3 からスマートキャンペーンにフローステップを追加して、customLeadStatus フィールドを新しい値で更新します。** データ値を右のパネルから中央のパネルにドラッグします。
1. リードが複数回実行されるように Smart Campaign を更新します。** スケジュール」をクリックします。 次に、「編集」をクリックします。  を毎回選択します。 次に、「保存」をクリックします。 キャンペーンの実行が開始されます。
1. [ フィルタータイプの REST API で複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) をクエリします。 パラメーター filterType=customLeadStatus &amp; filterValue=needsEnrichment.**を指定

これは、このデータを返すリクエストの例です。

`<https://AAA-BBB-CCC.mktorest.com/rest/v1/leads.json?access_token=><yourAccessToken>&filterType=customLeadStatus&filterValues=needsEnrichment`

API 呼び出しが成功すると、customLeadStatus フィールドが needsEnrichment の値と一致するリードを含む JSON データが返されます。 詳しくは、[ フィルタータイプ REST API で複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) を参照してください。

投稿日：_2014-11-22_ by _Murta_

## SOAP API を使用したオポチュニティ同期

ここでは、SOAP API を使用してMarketoにオポチュニティを挿入し、それらを会社やリードに関連付ける方法について説明します。 最初に、このプロセスの仕組みについて説明し、次に各シナリオのコードサンプルを示します。

**テーブル構造図** まず、以下の図にテーブル構造を示します。 ID は、レコード（連続番号）の作成時に自動生成されます。 太字のフィールドは必須です。オポチュニティ担当業務のみ必須フィールドがあります。 括弧内のフィールドはオプションで、点線で囲まれた接続も同様です。

**基本的なオポチュニティの挿入** 最初にオポチュニティを挿入し、次にオポチュニティ担当者の役割を挿入します。これにより、オポチュニティがリードにリンクされます。 この例では、リード ID とオポチュニティ ID を使用して、オポチュニティ人物の役割を指定します。 オポチュニティの作成時に、SOAPの応答でオポチュニティ ID を取得します。 リード ID は、Marketo リードデータベースのすべてのリードに表示されます。

**会社リンク** ほとんどの場合、個人に加えて、機会を会社にリンクします。 Marketoでは、SOAP API を使用して会社レコードにアクセスすることはできません。リードレコードにのみアクセスします（リードレコードには会社フィールドが含まれています）。 各リードに一意の会社 ID を追加し、その ID を商談で使用することで、商談を会社にリンクすることはできます。 手順 1 は、リードレコードに「会社 ID」フィールドを作成し、通常はバックエンドシステムから、一意の ID を入力することです。 手順 2 は、Opportunity に「Company Id」フィールドを作成することです。Marketo サポートまたはコンサルティングに依頼して、このようなフィールドを作成する必要があります。 次に、商談を作成するときにこのフィールドに値を入力します。これにより、商談が会社につながります。 これは、Marketo Revenue Cycle Analytics を使用する際に、会社情報に応じて Opportunity Influence Analyzer を使用する場合に特に重要です。

**外部識別子の使用** 多くの場合、バックエンドシステムと統合する際に独自の識別子を持つことができます。 外部キーを介して、Marketoでこれらの一意の ID を使用できます。 リードの場合、通常は、外部システムのユーザー ID （FSPID）を使用します。この ID は、一意の ID としてMarketo ID またはメールアドレスの代わりに使用されます。 FSPID は、非表示のシステムフィールドで、Marketo内には表示されません。 まだ保存していない場合は、商談同期で、FSPID を「Foreign Id」などのカスタムフィールドにも保存する必要があります（フィールドに何らかの名前を付けることができます）。 このフィールドは、Marketo管理者が自分で作成できます。 商談の場合、Marketo サポートは、例えば「Foreign Id」という名前など、商談に別のカスタムフィールドを作成します（任意の名前を付けることができます）。 オポチュニティを挿入する際に、このフィールドに値を入力します。 最後に、オポチュニティ担当者の役割を作成する場合は、Marketo ID を使用する代わりに、両方の外部キーを使用してリードとオポチュニティの間のリンクを指定します。 外部キーを使用して、商談のリードを更新することもできます。 現時点では、商談ユーザーロールレコードに外部キーを追加することはできないので、このために自動生成されたMarketo ID を使用する必要があります（商談ユーザーロール作成後のSOAP応答で取得します）。

**コードの例** 手順：1. 外部キーおよび会社 Id 1 を使用してリードを挿入/更新 外部キー 1 を使用してオポチュニティを挿入します。 外部キーを使用してオポチュニティ人物の役割を挿入する 1. SOAP リクエスト – 外部キーと会社 Id を使用した既存のリードの更新これは、外部キー「12346」とアカウント /会社 Id 「C123」を使用して、既存のリード（Marketo Id 「6」）を更新します。 また、機会担当者の役割で必要なので、カスタムフィールドに外部キーを保存しています。 外部キーの使用はオプションです。Marketo ID を使用して、このリードを Opportunity にリンクすることもできます。 会社 ID の使用もオプションですが、RCA で Opportunity Influence Analyzer を使用する場合は必須です。 リクエスト :

```xml
<soapenv:Envelope xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
   <soapenv:Header>
      <mkt:AuthenticationHeader>
         <mktowsUserId>\*\*\*</mktowsUserId>
         <requestSignature>\*\*\*</requestSignature>
         <requestTimestamp>2014-11-20T15:18:30-07:00</requestTimestamp>
      </mkt:AuthenticationHeader>
   </soapenv:Header>
   <soapenv:Body>
      <mkt:paramsSyncLead>
         <leadRecord>
            <Id>6</Id>
            <ForeignSysPersonId>12346</ForeignSysPersonId>
            <leadAttributeList>
               <attribute>
                  <attrName>FSPID</attrName>
                  <attrValue>12346</attrValue>
               </attribute>
               <attribute>
                  <attrName>cAccountFSID</attrName>
                  <attrValue>C123</attrValue>
               </attribute>
            </leadAttributeList>
         </leadRecord>
         <returnLead>false</returnLead>
      </mkt:paramsSyncLead>
   </soapenv:Body>
</soapenv:Envelope>
```

応答：

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xmlns:ns1="<http://www.marketo.com/mktows/">
   <SOAP-ENV:Body>
      <ns1:successSyncLead>
         <result>
            <leadId>6</leadId>
            <syncStatus>
               <leadId>6</leadId>
               <status>UPDATED</status>
               <error xsi:nil="true"/>
            </syncStatus>
            <leadRecord xsi:nil="true"/>
         </result>
      </ns1:successSyncLead>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

SOAP リクエスト – 商談の作成この場合、商談テーブルには 2 つのカスタムフィールドが作成されています。- `opportunityId` →は商談の一意の ID を保持する – `cAccountFSID` は会社の参照を保持する独自の商談 ID を指定す→代わりに、 Marketoで生成されたオポチュニティ ID を使用することもできます。 その場合は、外部キーノードを除外します。 会社の関連付けもオプションですが、RCA で Opportunity Influence Analyzer を使用する場合は必須です。 リクエスト :

```xml
<soapenv:Envelope xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
   <soapenv:Header>
      <mkt:AuthenticationHeader>
         <mktowsUserId>\*\*\*</mktowsUserId>
         <requestSignature>\*\*\*</requestSignature>
         <requestTimestamp>2014-11-20T15:03:28-07:00</requestTimestamp>
      </mkt:AuthenticationHeader>
   </soapenv:Header>
   <soapenv:Body>
      <mkt:paramsSyncMObjects>
         <mObjectList>
            <!--Zero or more repetitions:-->
            <mObject>
               <type>Opportunity</type>
               <externalKey>
                  <name>opportunityId</name>
                  <value>Opportunity_4</value>
               </externalKey>
               <attribList>
                  <attrib>
                     <name>opportunityId</name>
                     <value>Opportunity_4</value>
                  </attrib>
                  <attrib>
                     <name>Name</name>
                     <value>Opportunity 4 for ACME</value>
                  </attrib>
                  <attrib>
                     <name>IsClosed</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>IsWon</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>Amount</name>
                     <value>501.00</value>
                  </attrib>
                  <attrib>
                     <name>CloseDate</name>
                     <value>2014-10-24</value>
                  </attrib>
                  <attrib>
                     <name>ExpectedRevenue</name>
                     <value>501</value>
                  </attrib>
                  <attrib>
                     <name>Probability</name>
                     <value>100</value>
                  </attrib>
               </attribList>
               <associationList>
                  <mObjAssociation>
                     <mObjType>Company</mObjType>
                     <externalKey>
                        <name>cAccountFSID</name>
                        <value>C123</value>
                     </externalKey>
                  </mObjAssociation>
               </associationList>
            </mObject>
         </mObjectList>
         <operation>UPSERT</operation>
      </mkt:paramsSyncMObjects>
   </soapenv:Body>
</soapenv:Envelope>
```

応答：

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
   <SOAP-ENV:Body>
      <ns1:successSyncMObjects>
         <result>
            <mObjStatusList>
               <mObjStatus>
                  <id>40</id>
                  <externalKey>
                     <name>opportunityId</name>
                     <value>Opportunity_4</value>
                  </externalKey>
                  <status>CREATED</status>
               </mObjStatus>
            </mObjStatusList>
         </result>
      </ns1:successSyncMObjects>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

SOAP リクエスト – 商談担当者ロールこのリクエストは、リードを商談にリンクします。 1 つのSOAP リクエストに複数のリンクを指定できます（この例では、Opportunity を 1 つのリードにのみリンクしています）。 これは外部キーを使用してリンクを指定しますが、コメントでは実際の ID の使用方法も示します（この場合、リード ID は 6、商談 ID は 40）。 この「IsPrimary」フィールドと「Role」フィールドはオプションです。 リクエスト :

```xml
<soapenv:Envelope xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
   <soapenv:Header>
      <mkt:AuthenticationHeader>
         <mktowsUserId>\*\*\*</mktowsUserId>
         <requestSignature>\*\*\*</requestSignature>
         <requestTimestamp>2014-11-20T15:18:30-07:00</requestTimestamp>
      </mkt:AuthenticationHeader>
   </soapenv:Header>
   <soapenv:Body>
      <mkt:paramsSyncMObjects>
         <mObjectList>
            <!--Zero or more repetitions:-->
            <mObject>
               <type>OpportunityPersonRole</type>
               <attribList>
                  <attrib>
                     <name>IsPrimary</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>Role</name>
                     <value>Marketing Manager</value>
                  </attrib>
               </attribList>
               <associationList>
                  <mObjAssociation>
                     <mObjType>Lead</mObjType>
                     <!--id>6</id-->
                     <externalKey>
                      <name>FSPID</name>
                      <value>12346</value>
                     </externalKey>
                  </mObjAssociation>
                  <mObjAssociation>
                     <mObjType>Opportunity</mObjType>
                     <!--id>40</id-->
                     <externalKey>
                      <name>opportunityId</name>
                      <value>Opportunity_4</value>
                    </externalKey>
                  </mObjAssociation>
               </associationList>
            </mObject>
         </mObjectList>
         <operation>UPSERT</operation>
      </mkt:paramsSyncMObjects>
   </soapenv:Body>
</soapenv:Envelope>
```

応答：

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
   <SOAP-ENV:Body>
      <ns1:successSyncMObjects>
         <result>
            <mObjStatusList>
               <mObjStatus>
                  <id>11</id>
                  <status>CREATED</status>
               </mObjStatus>
            </mObjStatusList>
         </result>
      </ns1:successSyncMObjects>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

**代替アプローチ （1 回の呼び出しでステップ 2 と 3 を実行）** 最初にオポチュニティを挿入し、次にオポチュニティ担当者のロールを挿入できますが、1 回のSOAP呼び出しでこれを実行することもできます。 ただし、商談には外部キーを使用する必要があります（自動生成された商談 ID は、商談がまだ生成されていないので、商談担当者役割では使用できません）。 もちろん、この同じ API 呼び出しで、複数のリードをこのオポチュニティにリンクすることもできます（この例では、オポチュニティを 1 つのリードにのみリンクしています）。 リクエスト :

```xml
<soapenv:Envelope xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
   <soapenv:Header>
      <mkt:AuthenticationHeader>
         <mktowsUserId>\*\*\*</mktowsUserId>
         <requestSignature>\*\*\*</requestSignature>
         <requestTimestamp>2014-11-20T15:44:08-07:00</requestTimestamp>
      </mkt:AuthenticationHeader>
   </soapenv:Header>
   <soapenv:Body>
      <mkt:paramsSyncMObjects>
         <mObjectList>
            <!--Zero or more repetitions:-->
            <mObject>
               <type>Opportunity</type>
               <externalKey>
                  <name>opportunityId</name>
                  <value>Opportunity_5</value>
               </externalKey>
               <attribList>
                  <attrib>
                     <name>opportunityId</name>
                     <value>Opportunity_5</value>
                  </attrib>
                  <attrib>
                     <name>Name</name>
                     <value>Opportunity 5 for ACME</value>
                  </attrib>
                  <attrib>
                     <name>IsClosed</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>IsWon</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>Amount</name>
                     <value>1500</value>
                  </attrib>
                  <attrib>
                     <name>CloseDate</name>
                     <value>2014-10-24</value>
                  </attrib>
                  <attrib>
                     <name>ExpectedRevenue</name>
                     <value>1500</value>
                  </attrib>
                  <attrib>
                     <name>Probability</name>
                     <value>100</value>
                  </attrib>
               </attribList>
               <associationList>
                  <mObjAssociation>
                     <mObjType>Company</mObjType>
                     <externalKey>
                        <name>cAccountFSID</name>
                        <value>C123</value>
                     </externalKey>
                  </mObjAssociation>
               </associationList>
            </mObject>
             <mObject>
               <type>OpportunityPersonRole</type>
               <attribList>
                  <attrib>
                     <name>IsPrimary</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>Role</name>
                     <value>Marketing Manager</value>
                  </attrib>
               </attribList>
               <associationList>
                  <mObjAssociation>
                     <mObjType>Lead</mObjType>
                     <!--id>6</id-->
                     <externalKey>
                      <name>FSPID</name>
                      <value>12346</value>
                     </externalKey>
                  </mObjAssociation>
                  <mObjAssociation>
                     <mObjType>Opportunity</mObjType>
                     <externalKey>
                      <name>opportunityId</name>
                      <value>Opportunity_5</value>
                    </externalKey>
                  </mObjAssociation>
               </associationList>
            </mObject>
         </mObjectList>
         <operation>UPSERT</operation>
      </mkt:paramsSyncMObjects>
   </soapenv:Body>
</soapenv:Envelope>
```

応答：

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
   <SOAP-ENV:Body>
      <ns1:successSyncMObjects>
         <result>
            <mObjStatusList>
               <mObjStatus>
                  <id>41</id>
                  <externalKey>
                     <name>opportunityId</name>
                     <value>Opportunity_5</value>
                  </externalKey>
                  <status>CREATED</status>
               </mObjStatus>
               <mObjStatus>
                  <id>12</id>
                  <status>CREATED</status>
               </mObjStatus>
            </mObjStatusList>
         </result>
      </ns1:successSyncMObjects>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

Posted on _2014-11-26_ by _Jep_

## マルチスレッド REST API リクエスト

Marketo API を呼び出す際のパフォーマンスを向上したい場合は、同時リクエストを行うことができます。 このアプローチにより、より短い期間でより多くのデータを取得できます。 API リクエストを行う場合、クライアントとサーバー間の往復時間の一部がワイヤー上の転送時間になります。 したがって、リクエスト全体の転送時間を短縮できれば、パフォーマンスが向上します。 以下のサンプルコードは、Ruby でこれを行う方法を示しています。 これは、マルチスレッドリクエストの実行に使用される [ イベント処理ライブラリ ](https://github.com/igrigorik/em-http-request/wiki/Parallel-Requests) である EventMachine を使用します。 以下の例では、[Lead Activities API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET) を呼び出し、2 つの同時リクエストを作成します。 このアプローチにより、2 回目のリクエストに対するクライアントからサーバーへの転送時間がなくなります。 これを行うには、最初のリクエストと同時に 2 番目のリクエストを含めます。 API 応答は、テキストファイルに書き込まれます。

```java
require 'em-http-request'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/activities.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
# Specify datetime needed as nextPageToken
since_date_time = ["&nextPageToken=A5YMOYZQBOGD2OSYYBYDAQGEMGLBDGDANAABQGRAQWAAKKID", "&nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ"]
# Specify activities needed
activity_type_ids = "&activityTypeIds=1&activityTypeIds=12"
requesturl_a = marketo_instance + endpoint + auth_token + since_date_time.at(0) + activity_type_ids
requesturl_b = marketo_instance + endpoint + auth_token + since_date_time.at(1) + activity_type_ids

# Make request
EventMachine.run do
  http1 = EventMachine::HttpRequest.new(requesturl_a).get
  http2 = EventMachine::HttpRequest.new(requesturl_b).get

# When API response is received, write response to a text file
  http1.callback {
  File.open('response1.txt', 'w') do |t|
  t.puts http1.response
  end }

  http2.callback {
  File.open('response2.txt', 'w') do |t|
  t.puts http2.response
  end }
end
```

Posted on _2014-12-03_ by _Murta_

## パフォーマンスチューニング API リクエスト

この投稿では、Marketo API からデータをリクエストする際のパフォーマンスを向上させる方法について説明します。 ただし、これらの戦略のメリットをMarketo API の 1 日あたりの上限であるオペレーティング制約と比較検討する必要があります。
**方法 1 – 各 API 呼び出しでリクエストするデータの量を減らす** 通常、API 呼び出しでリクエストするデータが増えると、Marketo サーバーがデータベース内のデータを検索するのに要する時間が長くなります。 [getMultipleLeads SOAP API](/help/soap-api/getmultipleleads.md) などの日付範囲で API 呼び出しを行う場合は、呼び出しごとの時間範囲を短縮し、より多くの呼び出しを補正します。 例えば、6 月 1 日から 7 月 1 日のデータをリクエストする代わりに、6 月 1 日から 2 日を呼び出し、6 月 2 日から 1 日を呼び出すなど、一度に 1 日をリクエストします。 Marketoのリードフィールドからデータを返す API 呼び出しを行う場合は、必要なフィールドのみをリクエストします。 リードフィールドを追加するたびに、API 呼び出しにかかる時間が徐々に長くなります。 もう 1 つのアプローチは、バッチサイズまたは 1 回の呼び出しでリクエストされるリード数を減らすことです。
**方法 2 – 同時リクエストの実行** パフォーマンスを向上させ、一度にさらにデータを取り込む。 API に対して同時にリクエストを実行できます。 このアプローチにより、Wire API リクエストが合計で費やす時間が短縮されます。 例えば、フィルタータイプによって複数のリードを取得するようにリクエストしているとします。 リード 1 から 300 を問い合わせる 1 つのリクエストと、リード 301 から 600 を問い合わせる別のリクエストでは、同時にリクエストを実行できます。
**方法 3 - データをキャッシュする** Marketoの一部のデータは、リードフィールドの一覧など、リードアクティビティデータなどの他のデータよりも変更される頻度が低くなります。 更新頻度の低いデータをキャッシュする場合は、実行する必要がある API 呼び出しの数を減らします。 また、通常はリモートの Web サービスからアクセスするよりもローカルでデータを検索する方が高速なので、パフォーマンスも向上します。

投稿日：_2014-12-05_ by _Murta_

## Marketo フォームデータのGoogle Analyticsへの送信

Google Analyticsでは、カスタムデータイベントを送信し、そのデータを利用して web サイトのパフォーマンスをセグメント化して分析できます。 以下のJavaScript コードスニペットを使用すると、訪問者が web フォームを送信した後、Marketo 2.0 フォームデータをGoogle Analyticsに自動的にプッシュできます。 次に、その設定方法を示します。

**手順 1** コードの下部（タグの前）にJavaScript Formsを含むすべてのページに、Marketo タグを挿入します。 JavaScriptは、非表示でないフィールドのみ送信します（sendHiddenFields : false）。 これは、sendHiddenFields を false から true に変更することで調整できます。 また、「fieldsToExclude」配列にフィールド ID を追加することで、除外するフィールドを選択することもできます。

```javascript
function pushFormDataToGa(a){
setTimeout(function () {
document.getElementsByTagName('form')[0].getElementsByClassName(a.submitButton)[0].addEventListener('click', function() {
  allFields = document.getElementsByTagName('form')[0].getElementsByTagName('input');
  for(i=0;i<allFields.length;i++){
   if( (allFields[i].type !="hidden" && allFields[i].type !="submit" && allFields[i].value !="" && a.fieldsToExclude.indexOf(allFields[i].id) === -1  ) || (allFields[i].type === "hidden" && a.sendHiddenFields) ){
    console.log( allFields[i].name + ": "  + allFields[i].value);
    if(typeof(_gaq) != "undefined"){
    //Classic
    _trackEvent("Marketo Form Submission", allFields[i].value , allFields[i].name
{'nonInteraction': 1});
    }else if(typeof(ga) !="undefined"){
    //Universal
    ga('send', 'event',"Marketo Form Submission", allFields[i].value , allFields[i].name, {'nonInteraction': 1});
}}}}, false);
}, 3000);}
pushFormDataToGa({
 submitButton: "mktoButton",
 fieldsToExclude: ["Email","LastName", "FirstName"],
 sendHiddenFields : false
});
```

**手順 2** GA のデータが「レポート」セクションに表示される。 動作/ イベント /上位のイベントに移動します。 **スクリプトの制限：** – このコードサンプルは、[Marketo Forms 2.0](/help/javascript-api/forms-api-reference.md) とのみ互換性があります。 - Googleのプライバシーポリシーにより、お客様は個人情報（メールまたは名前）を送信することはできません。 プライバシーに関する潜在的な懸念以外にも、これは個人を特定できる情報なので、[Google Analytics の利用規約 ](https://marketingplatform.google.com/about/analytics/terms/us/) に違反しています。

「お客様は、本サービスを使用して、個人を特定するデータ（氏名、メールアドレス、請求先など）、またはGoogleがそのようなデータに合理的にリンクできるその他のデータのトラッキング、収集、アップロードを行いません（また、第三者による使用も認めません）。」

Posted on _2014-12-16_ by _Yanir_

## Marketo フォームへの「フルネーム」フィールドの追加

Web フォームを短くすると、コンバージョン率が向上することがわかっています。 以下のJavaScript コードのサンプルを使用すると、名フィールドと姓フィールドを 1 つのフルネーム フィールドに結合することで、フォームをさらに短くすることができます。 訪問者が姓名を入力すると、スクリプトによってテキストが自動的に姓と名のフィールドに分割されます。 既知の訪問者の場合、スクリプトは名と姓を結合してから新しいフィールドにコピーすると、フィールドを再度入力する必要がなくなります。 次に、その設定方法を示します。

**手順 1** Marketoに、フルネームという新しいカスタムフィールドを作成します。 スクリプトはフルネームの表示にこのフィールドのみを使用するので、CRM プラットフォームで作成する必要はありません。
**手順 2** このフィールドをすべての web フォームに追加します。 名と姓のフィールドを非表示として設定します。 JavaScriptで、「splitFullName」設定を変更して 3 つのフィールド名を含めます。 注意：これらの名前がページの他の場所に表示されないようにしてください。
**手順 3** コードの下部、タグの前にあるすべてのランディングページにJavaScriptを挿入します。

```javascript
<script>
MktoForms2.whenReady(function (form){
        function splitFullName(a,b,c){
                String.prototype.capitalize = function(){
                        return this.replace( /(^|s)([a-z])/g , function(m,p1,p2){ return p1+p2.toUpperCase(); } );
                };
                document.getElementsByName[c](0).oninput=function(){
                        var fullName = document.getElementsByName[c](0).value;
                        if((fullName.match(/ /g) || []).length ===0 || fullName.substring(fullName.indexOf(" ")+1,fullName.length) === ""){
                                var first = fullName.capitalize();;
                                var last = "null";
                        }else if(fullName.substring(0,fullName.indexOf(" ")).indexOf(".")>-1){
                                var first = fullName.substring(0,fullName.indexOf(" ")).capitalize() + " " + fullName.substring(fullName.indexOf(" ")+1,fullName.length).substring(0,fullName.substring(fullName.indexOf(" ")+1,fullName.length).indexOf(" ")).capitalize();
                                var last = fullName.substring(first.length +1,fullName.length).capitalize();
                        }else{
                                var first = fullName.substring(0,fullName.indexOf(" ")).capitalize();
                                var last = fullName.substring(fullName.indexOf(" ")+1,fullName.length).capitalize();
                        }
                        document.getElementsByName[a](0).value = first;
                        document.getElementsByName[b](0).value = last;
                };
                //Initial Values
                if(document.getElementsByName[c](0).value.length < 2 && document.getElementsByName[b](0).value.length.length >2 && document.getElementsByName[a](0).value.length.length >2 ){
                        var first = document.getElementsByName[a](0).value.capitalize();
                        var last = document.getElementsByName[b](0).value.capitalize();
                        var fullName =  first + " " + last ;
                        console.log(fullName);
                        document.getElementsByName[c](0).value = fullName;
                }
        }
        splitFullName("FirstName","LastName","leadFullName");
});
</script>
```

メモ：このコードはMarketo Forms 2.0 でのみ機能します。

Posted on _2014-12-16_ by _Yanir_

## cURL を使用した REST API 経由のリードの読み込み

REST API を使用して CSV ファイルからリードを読み込みますが、Postman Chrome拡張機能を使用してこれが行うのが難しいことに気がつきました。 この投稿では、cURL でこれをおこなう方法を説明します。

1. [cURL をダウンロードしてインストールします ](https://curl.se/download.html) は、REST API を使用してMarketoにデータをプッシュするために使用するコマンドラインツールです。
1. コマンドラインを開き、CSV ファイルがある場所に移動します。 CSV ファイルの列ヘッダーは、Marketoのフィールド名ではなく、API フィールド名と一致する必要があります。
1. アクセス トークンが必要です。 Marketoにログインし、管理者/ LaunchPoint の順に移動します。 REST API ユーザーを見つけて、「詳細を表示」をクリックします。 「トークンを取得」ボタンをクリックします。
1. また、お使いのMarketo インスタンスに固有の REST エンドポイントも必要です。 Marketoにログインし、「管理者」、「Web サービス」の順に移動します。 「REST API」とマークされたセクションで、エンドポイント URL を見つけます。
1. コマンドラインで、cURL 呼び出しに次の形式に従います。 手順 3 のアクセストークンで `<accesstoken>` を置き換え、手順 4 の REST API エンドポイント URL で `<REST API Endpoint URL>` を置き換えます。 詳しくは、[ こちらを参照 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/importLeadUsingPOST) してください。 ここで「/bulk」は、エンドポイント URL の末尾にある「/rest」を置き換えます。 /rest/bulk のエンドポイントが設定されている場合は、エラーを返します。

`curl -i -F format=csv -F file=@leaddata.csv -F access_token=<accesstoken> <REST API Endpoint URL>/bulk/v1/leads.json`

Posted on _2014-12-16_ by _Jordan_

## Marketoに次の確認アラートを追加：

例えば、ユーザーがMarketo フォームの「送信」ボタンをクリックしたときに、「本当に送信してもよろしいですか？」という通知を表示するとします。 これを実現するには、数行のJavaScriptを実装し、誰かが「送信」ボタンをクリックすると確認ボックスが表示されるようにします。 次に、その方法の例を示します。 次に示すように、Marketo フォームに onSubmit 関数を追加します。 Marketo Forms API について詳しくは、[ 開発者向けドキュメント ](/help/javascript-api/forms-api-reference.md) を参照してください。

```javascript
<script src="//app-e.marketo.com/js/forms2/js/forms2.js"></script>
<form id="mktoForm_19"></form>
<script>
MktoForms2.loadForm("//app-e.marketo.com", "212-RBI-463", 19,function(form){

//Add this function to your Marketo form script
form.onSubmit(function(){
alert("Do you really want to submit the form?");
});
});
</script>
```

Posted on _2014-12-17_ by _David_

## フォローアップのランディングページなしでお礼のメッセージを表示

通常、Marketo フォームを使用する場合は、2 つのランディングページを作成します。1 つはフォームを配置するため、もう 1 つはフォームが完了した後にリダイレクトするためのものです。 ただし、場合によっては、2 つの異なるが非常に類似したランディングページを維持する必要がないことがあります。 Forms 2.0 JavaScript API を使用すると、フォームと「ありがとうございます」メッセージに同じランディングページを実際に使用できます。 これを行うには、通常どおりに登録ランディングページとフォームを作成し、ランディングページにフォームを配置します。 次に、ページにHTML要素を追加します。 この要素には、フォームが送信された時点でアクティベートされるコードを追加します。 その後、フォームを非表示にし、非表示のを表示します <div> お礼のメッセージが含まれています。 JavaScriptは次のようになります。

```javascript
//Edit host with your Marketo instance info
<script src="//<host>/js/forms2/js/forms2.js"></script>
<script>
MktoForms2.whenReady(function (form){
 //Add an onSuccess handler
  form.onSuccess(function(values, followUpUrl){
   //get the form's jQuery element and hide it
   form.getFormElem().hide();
   document.getElementById('confirmform').style.visibility = 'visible';
   //return false to prevent the submission handler from taking the lead to the follow up url.
   return false;
 });
});
</script>
```

「ありがとうございます」メッセージテキストを編集します。

`<div id="confirmform" style="visibility:hidden;"><p><strong>Thank you. Check your email for details on your request.</strong></p></div>`

コードサンプルでは、ホスト名を編集して、「ありがとうございます」メッセージを表示する必要があります。 1 つ目はMarketo インスタンス（例：「//app-sj06.marketo.com/js/forms2/js/forms2.js」）を参照し、2 つ目はフォームの入力後に表示するありがとうテキストを含める必要があります。 テキストは、ランディングページのHTML要素の配置場所と同じ場所に表示されるので、プロパティシートで必ず編集してください。 また、HTML要素のレイヤーがフォームのレイヤーよりも小さいことを確認する必要があります。 デフォルトでは、どちらもレイヤー 15 に配置されるので、HTML要素をレイヤー 11 にしても安全です。 この操作を行わないと、「ありがとうございます」メッセージと重なるフォーム フィールド ボックスに入力できなくなります。 JavaScriptによって設定が上書きされるので、フォームまたはランディングページでフォローアップタイプを変更する必要はありません。 Marketo Forms API について詳しくは、[ 開発者向けドキュメント ](/help/javascript-api/forms-api-reference.md) を参照してください。

Posted on _2014-12-19_ by _Kristin_

## Marketo Platform で作成された、開いているSource プロジェクトのハイライト

これは、開発者向けコミュニティがMarketo プラットフォームを中心に構築したオープンソースプロジェクトに焦点を当てた、進行中のシリーズの最初の投稿です。 アドビでは [Marketoの GitHub アカウントのリスト ](https://github.com/Marketo/Community-Supported-Client-Libraries) を維持管理しており、Marketo開発者コミュニティが作成したクライアントライブラリおよびプロジェクトをトラッキングしています。 Marketo REST API とSOAP API に関して開発された 3 つのプロジェクトを以下に示します。 Daniel Chesterton は [Marketo REST API 用のクライアントライブラリを PHP で作成しました ](https://github.com/dchesterton/marketo-rest-api)。 現在、クライアントライブラリは 12 個の REST API エンドポイントをカバーしています。Elixiter の Kyle Halstvedt**、[Marketoの静的リストからリードをGoogle スプレッドシートに取り込む ](https://github.com/Elixiter/mkto_google-spreadsheet) プロジェクトを作成しました。 Kyle のプロジェクトではMarketo REST API を使用しています。  David Santoso は、Marketo SOAP API 用の [Ruby Gem を作成しました。](https://github.com/davidsantoso/markety) このプロジェクトを使用すると、Marketo SOAP API を Ruby on Rails アプリにすばやく統合できます。  Marketo プラットフォーム上で、デベロッパーコミュニティによって作成されたプロジェクトが増えることを楽しみにしています。 Marketo プラットフォームのオープンソースプロジェクトに取り組んでいる場合は、[ プルリクエストを通じてこの GitHub リポジトリーに送信 ](https://github.com/Marketo/Community-Supported-Client-Libraries) してください。

Posted on _2015-01-02_ by _Murta_

## ユーザーの場所に基づいてページコンテンツを動的に変更

ランディングページの電話番号を、ユーザーの場所に応じて動的に変更するとします。 例えば、ユーザーがカリフォルニアにいる場合、ランディングページでカリフォルニアのオフィスの電話番号を表示したいのですが、日本にいる場合は、日本のオフィスの電話番号を表示したいのですが、  これを実装する 1 つの方法は、JavaScriptと [HTML5 Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API) を使用することです。 このアプローチの利点は、複数の静的ランディングページではなく、1 つのランディングページを作成し、ユーザーの場所に基づいて動的に変更できることです。 以下の技術実装の詳細について説明します。 緯度と経度の座標を持つオフィスの場所のオブジェクトと、オフィスの電話番号を持つ 2 つ目のオブジェクトを作成します。 実稼動環境では、これら 2 つのオブジェクトを 1 つのオブジェクトに結合する方が効果的です。

```json
//Coordinates for Marketo offices
var officeLocations = {
    "San Mateo": {latitude: 37.5596465, longitude: -122.2870142},
    "Atlanta": {latitude: 33.8547013, longitude: -84.35552349999999},
    "Tokyo": {latitude: 35.6895, longitude: 139.6917},
    "Dublin": {latitude: 53.3478, longitude: -6.2603097},
    "Sydney": {latitude: -33.873651, longitude: 151.2068896},
    "Portland": {latitude: 45.512089, longitude: -122.6763367},
    "Tel Aviv": {latitude: 32.0852999, longitude: 34.78176759999999}
}

//Phone numbers for Marketo offices
var officePhoneNumbers = {
    "San Mateo": "+1-650-376-2300",
    "Atlanta": "+1-877-260-6586",
    "Tokyo": "+81-03-6759-8280",
    "Dublin": "+353-1-242-3000",
    "Sydney": "+61-2-9045-2711",
    "Portland": "+1-877-260-6586",
    "Tel Aviv": "+1-877-260-6586"
}
```

ユーザーの場所をリクエストするメソッドを作成します。 エラーを処理するために、ユーザーの場所にアクセスできない場合は、デフォルトでMarketoの本社と電話番号を使用します。

```javascript
//Method to get user's current location. Returns a position object with user's geo coordinates
function getLocation() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(findNearestOffice);
    } else {
        x.innerHTML = "Marketo Location: San Mateo
Marketo Phone Number: +1-877-260-6586";
    }
}
```

最後に、ユーザーの場所に最も近いオフィスを見つける方法を作成し、ページ上の最も近いオフィスの電話番号を返します。 この手法では、地理空間操作を提供するJavaScript ライブラリである [Geolib](https://github.com/manuelbieh/Geolib) の findNearest メソッドを使用します。

```javascript
//Find nearest Marketo office to user's location
function findNearestOffice(position) {
        var nearestOffice = geolib.findNearest({latitude: position.coords.latitude, longitude: position.coords.longitude}, officeLocations);
        x.innerHTML = "Marketo Location: " + nearestOffice.key + "
Marketo Phone Number: " +  officePhoneNumbers[nearestOffice.key];
}
```

これが完全な実装です。 ユーザーがページ上のボタンをクリックすると、getLocation メソッドがトリガーされます。 この [GitHub リポジトリ ](https://github.com/MurtzaM/Find-Nearest-Marketo-Office) には、このデモを設定するために必要なファイルが含まれています。

投稿日：_2014-12-20_ by _Murta_

## リードトラッキングと複数のドメイン

MarketoのMunchkin トラッキングコードは、web サイトへの訪問を追跡するのに役立ちます。 Munchkin トラッキングコードを使用して、Web サイト上のほとんどのページまたはすべてのページの匿名リードを Cookie に記録する必要が生じる場合があります。 Munchkinの仕組みを説明します。 このページへの訪問は、既存のリードについて記録されます。cookie を使用しない訪問者がこのページに訪問すると、新しい cookie が作成および保存され、新しい匿名リードがMarketo データベースに作成されます。 現在のドメインの Cookie がまだ存在しない場合、Munchkin トラッカーは自動的に訪問者に Cookie を設定します。 Marketoでは、イベント（リンクのクリック、web ページへの訪問、または新しいリード）をリードのアクティビティログに記録します。 cookie に格納される値は、特定の訪問者に対して一意です。 値は、一意のMunchkin アカウントトラッキング ID、ドメイン名、タイムスタンプおよびランダムな整数の組み合わせです。
**複数のドメインがある場合はどうなりますか？** 追跡するサイトが `<www.apples.com>` と `<www.bananas.com>` の 2 つあるとします。 トラッキングコードは両方のサイトに配置できますが、次の点を考慮する必要があります。 Marketo cookie は「ファーストパーティ cookie」なので、ドメイン固有です。 つまり、サイト 1 への訪問者はMarketoで匿名リードとして作成され、同じリードがサイト 2 に移動すると、Marketoで 2 つ目の個別の匿名リードが作成されます。 リードがサイト 1 のフォームに入力するとこのレコードが既知になり、サイト 2 の匿名レコードは残り、その後のサイトへの訪問が引き続き累積されます。 その後、リードがサイト 1 で使用されたものとまったく同じメールアドレスでサイト 2 のフォームに入力した場合、両方の既知のリードは自動的に結合され、過去と将来のすべての行動がMarketoの 1 つのレコードで追跡されます。 両方の cookie ID は同じリードに関連付けられており、（いずれかのドメインからの）すべての web アクティビティがそのリードに基づきます。
**複数のサブドメインについてはどうですか？** サブドメインは問題ではありません。 例として、Marketo.comを使用します。 fr.marketo.comやde.marketo.comなど、異なる言語用に複数のサブドメインがあります。 サブドメインを使用すると、すべてのアクティビティが同じリードレコード/cookie に対して記録されます。

Posted on _2015-01-13_ by _David_

## Marketo フォームのヒントテキストの色の変更

例えば、Forms 2.0 でヒントテキストの色（プレースホルダーテキストとも呼ばれます）を変更するとします。これは、カスタム CSS を使用することで可能です。 例えば、以下のスクリーンショットでは、このMarketo フォームのヒントテキストを青にしました。 Marketo Formsの使用方法に応じて、これを行う方法は 3 つあります。

**オプション 1:Marketo フォームを埋め込む場合は、以下の CSS をメインの CSS ファイルに直接追加する。**

```css
::-webkit-input-placeholder {
  color: blue;
}
::-moz-placeholder {
  color: blue;
}
:-ms-input-placeholder {
  color: blue;
}
:-moz-placeholder {
  color: blue;
}
```

**オプション 2:Marketo フォームを埋め込む場合は、CSS をページの「`<style></style>`」セクションの `<head>` のタグの間に直接追加できます。**

```css
<style>
::-webkit-input-placeholder {
  color: blue;
}
::-moz-placeholder {
  color: blue;
}
:-ms-input-placeholder {
  color: blue;
}
:-moz-placeholder {
  color: blue;
}
</style>
```

**オプション 3:Marketo ランディングページでMarketo フォームを使用している場合は、Marketo UI を通じてこのカスタム CSS を追加できます。** Marketoのナビゲーションツリーでランディングページを検索」をクリックします。 次に、「ドラフトを編集」をクリックします。 「ページのメタタグを編集」をクリックします。 カスタム HEAD HTML セクションに以下の CSS を追加します。 `<style></style>` タグを含める必要があります。

```css
<style>
::-webkit-input-placeholder {
  color: blue;
}
::-moz-placeholder {
  color: blue;
}
:-ms-input-placeholder {
  color: blue;
}
:-moz-placeholder {
  color: blue;
}
</style>
```

「ドラフトを承認」をクリックします。 Marketo ランディングページにアクセスする場合、ヒントテキストは CSS で定義したカラーです。 Marketo Formsについて詳しくは [ ドキュメントを参照してください ](/help/javascript-api/forms-api-reference.md)。

Posted on _2015-01-14_ by _Murta_

## REST API を使用したアクティビティデータの取得

今月リストに追加されたすべてのリードを取得するとします。 [ リードアクティビティ REST API を取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET) を使用すると、このデータを取得できます。 リードアクティビティ API を呼び出す前に、認証 API からアクセストークンを取得するとともに、[ ページングトークン API を取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getActivitiesPagingTokenUsingGET) から開始日トークンを取得する必要があります。 以下は Ruby のコード例で、今月リストに追加されたすべてのリードを返すために呼び出す必要がある個々の API エンドポイントを順を追って示しています。 1. アクセストークンの取得**

```ruby
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com/identity/oauth/token?grant_type=client_credentials>"
# Relace with your client id
client_id = "99985d09-22a9-3jl2-84av-f5baae7c3a45"
# Replace with your your  client secret
client_secret = "tZPVrKiEmUDezE18yZfeaPlTJ2vKn2fw"
request_url = marketo_instance + "&client_id=" + client_id + "&client_secret=" + client_secret

# Make request
response = RestClient.get request_url

# Parse reponse and return only access token
results = JSON.parse(response.body)
access_token = results["access_token"]
puts access_token
```

1. ページトークンの取得

```ruby
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/activities/pagingtoken.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
# Specify date
since_date_time = "&sinceDatetime=2015-01-01T00:00:00-08:00"
request_url = marketo_instance + endpoint + auth_token + since_date_time

# Make request
response = RestClient.get request_url

# Returns Marketo API response
puts response
```

1. アクティビティデータを取得**この呼び出しに必要なアクティビティタイプ ID を判断するには、[Gotting アクティビティタイプ API](/help/rest-api/activities.md) をクエリします。 Get Activity Types API は、すべてのアクティビティタイプと関連する ID を含むスキーマを返します。 例えば、作成された新しいリードに対しては ID 12、web ページ訪問に対しては ID 1 を返します。

```java
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/activities.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
# Specify datetime needed as nextPageToken
since_date_time = "&nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ"
# Specify activities needed
activity_type_ids = "&activityTypeIds=24"
request_url = marketo_instance + endpoint + auth_token + since_date_time + activity_type_ids

# Make request
response = RestClient.get request_url

# Returns Marketo API response
puts response
```

1. リードアクティビティ API は、結果セットのページ番号に使用できる各レスポンスを含んだページングトークンを返します。**詳しくは、[REST API ドキュメント ](/help/rest-api/rest-api.md) を参照してください。

Posted on _2015-01-20_ by _Murta_

## Marketo Platform に基づいて作成された、開いているSource プロジェクトのハイライト：第 2 部

これは、開発者向けコミュニティがMarketo プラットフォームを中心に構築したオープンソースプロジェクトに焦点を当てた、進行中のシリーズの 2 番目の投稿です。 アドビでは [Marketoの GitHub アカウントのリスト ](https://github.com/Marketo/Community-Supported-Client-Libraries) を維持管理しており、Marketo開発者コミュニティが作成したクライアントライブラリおよびプロジェクトをトラッキングしています。 Marketo SOAP API とMunchkin API に関して開発された 3 つのプロジェクトを以下に示します。 [PunchTab](https://www.punchtab.com/) は [Marketo SOAP API 用のクライアントライブラリ ](https://github.com/PunchTab/suds-marketo) を Python で作成しました。 [Flickerbox](https://www.flickerbox.com/) は、Marketo SOAP API 用に [PHP のクライアントライブラリ ](https://github.com/flickerbox/marketo) を作成しました。* [Richard Morrison](https://x.com/mozz100) は、Marketo SOAP API からリードデータを取得し、JavaScriptを使用してこのデータをクライアントに渡す PHP スクリプト [ を作成しました。](https://github.com/mozz100/marketo-whodat) このプロジェクトは、Marketoでユーザーのデータに基づいてページを変更するのに役立ちます。  Marketo プラットフォーム上で、デベロッパーコミュニティによって作成されたプロジェクトが増えることを楽しみにしています。 Marketo プラットフォームのオープンソースプロジェクトに取り組んでいる場合は、[ プルリクエストを通じてこの GitHub リポジトリーに送信 ](https://github.com/Marketo/Community-Supported-Client-Libraries) してください。

Posted on _2015-01-20_ by _Murta_

## RTP レコメンデーションエンジンのクリック数のGoogle Analytics への送信

以下は、Marketo リアルタイム Personalization（RTP）ユーザーがGoogle Analytics内のコンテンツレコメンデーションエンジンからのクリック数を確認するためのソリューションです。 訪問者がコンテンツレコメンデーションバーをクリックすると、イベントカテゴリ「RTP-Recommendations」の下のGoogle Analyticsにイベントが送信されます。 Analytics では、推奨テキスト（バーに表示される）がイベントラベルに追加され、推奨アセットの URL がイベントアクションに追加されます。 スクリプトは、Classic Google AnalyticsとGoogle Universal Analytics の両方で機能します。 このタグは、HTMLのページコードの末尾に貼り付ける必要があるため、`</body>` のタグの前の最後のタグになります。

```javascript
$( document ).ready(function() {
if(document.getElementsByClassName("insightera-bar-content").length
 >0){
document.getElementsByClassName("insightera-bar-content")[0].getElementsByTagName('a')[0].addEventListener("click",
 function(){
assetName
 = document.getElementsByClassName("insightera-bar-content")[0].getElementsByTagName('a')[0].innerText;
assetURL
 = document.getElementsByClassName("insightera-bar-content")[0].getElementsByTagName('a')[0].href;
assetURL=
 assetURL.substring(assetURL.lastIndexOf("/"),assetURL.indexOf("?iesrc"));
console.log(assetName

 * " | " + assetURL);
if(typeof(_gaq)
 != "undefined"){
//Classic
_trackEvent("RTP-Recommendations",
 assetName , assetURL , {'nonInteraction': 1});
}else
 if(typeof(ga) !="undefined"){
//Universal
ga('send',
 'event',"RTP-Recommendations", assetName , assetURL, {'nonInteraction': 1});
}
});
}
});
```

Posted on _2015-01-22_ by _Yanir_

## Boomi でのMarketo REST API の使用：REST 認証トークンの取得と保存

特定の条件を満たすリードの自動エクスポートの設定は、Marketoの非常に一般的なユースケースです。 これは、現在、Marketo インターフェイスでは実行できませんが、Dell Boomi などのサードパーティツール、一部のデータ管理キャンペーンを含む静的リスト、およびMarketo REST API を使用すると、非常に簡単に実行できます。 REST API とは Boomi にはMarketo REST API コネクタがないと思っていました。 現在のところ、サポートはされませんが、HTTP コネクタを使用して、jSON 応答図形を手動で定義することで、同じ処理を実行できます。 最初の手順は、[REST API Marketo デベロッパーページ ](/help/rest-api/rest-api.md) に記載されている REST API を使用するようにMarketo インスタンスを設定することです。 また、お客様がデルの Boomi アカウントにアクセスし、Boomi スキルを持って、このような統合プロセスを作成できることを前提としています。 最終プロセスは次のようになります。これには、以下のMarketo REST API 操作への呼び出しが含まれ、各操作には、開発者サイトにある関連する jSON 応答図形があります。 時間を節約するために、以下に [ 認証 ](/help/rest-api/authentication.md) のための JSON の例を示しました

```json
{
  "access_token": "",
  "token_type": "",
  "expires_in": 0,
  "scope": ""
}
```

[ リスト ID で複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists) 用の JSON の例

```json
{
  "requestId": "",
  "success": true,
  "nextPageToken": "",
  "result": [
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    },
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    },
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    }
  ]
}
```

[ リストからリードを削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE) 用の JSON の例

```json
{
  "requestId": "",
  "success": true,
  "result": [
    {
      "id": 1,
      "status": ""
    },
    {
      "id": 2,
      "status": "",
      "reasons": [
        {
          "code": "",
          "message": ""
        }
      ]
    }
  ]
}
```

プロパティの定義：REST の呼び出しを開始する前に、使用する変数を外部化し、カプセル化することが重要です。 以下のように定義しました。

* ClientID：これを REST ランチポイントサービスから取得します
* クライアントシークレット：これを REST ランチポイントサービスから取得します
* AccessToken：これは REST 呼び出しから取得します
* Static ListID：操作する静的リストのリスト ID。 Marketoの URL からこれを取得
* フィールド：Marketoから REST サービスが取得する各リードのフィールドのコンマ区切りリスト。 Mine is &quot;id, email,firstName,lastName&quot; * IDStringToDelete：最終的に、リストからの削除で使用される静的リスト内のすべてのリードの ID が含まれます
* ActivityTypes：このブログの第 2 部で使用されます。ここで詳しく説明します。
* SinceDateTime：このブログの第 2 部で使用されます。
* PagingToken：このブログの第 2 部で使用されます。ここで、これについて詳しく説明します。
* Folder - Outgoing: SFTP サーバーの送信フォルダーへのパス。 この例では「/data/outgoing」を使用します。 これにより、SFTP 操作をパラメーター化して汎用にすることができます。

認証トークン：前述のように、「データなし」開始図形を使用してプロセスを作成した後、キャンバスにコネクタを配置します（これは単なる個人的な選択であり、私のすべてのコネクタは英国のプラグのように見えるのが好きです）。
コネクタは次のように設定する必要があります。- コネクタは HTTP GET クライアントです – 接続は URL を使用します。`https://123-ABC-456.mktorest.com` （末尾には/rest を付けないでください。REST 呼び出しにこれを使用し、ID アクセストークンを取得するために使用します。 さらに、123-ABC-456 をMarketo インスタンスに適した値に変更します） – Operation は&quot;Get oAuth Token&quot;（新規！） – Request Profile = None - Response Profile = JSON - Content Type: Plain - HTTP Method: GET - Resource Path （4 を引用符なしで追加）: &quot;identity/oAuth/token?grant_type=client_credentials&amp;client_id=&quot;; &quot;ClientID （Replacement variable）&quot;; &quot;&amp;client_secret=&quot; 「ClientSecret （Replacement variable）」 – 設定でパラメーターを設定 – > パラメーター – > （+）:ClientID = Process Property Client ID を設定；ClientSecret = Process Property Client Secret を設定この後、次に示すように、成功トークンをプロセスプロパティの「AccessToken」変数に保存し、jSON 応答から抽出します。
この手順のパターンは、次の手順でも繰り返されますが、異なる jSON 戻りプロファイルを持つ新しい操作を使用します。 実際、REST 呼び出しの多くは、マイナーな変更と同じ方法で処理されます。 次回は、これをさらに展開し、REST を使用して静的リストからリードのリストを取得します。 今はプロセスを実行しますが、「プロパティを設定」の後に停止図形を配置し、デバッグで実行して、Marketoに表示されるのと同じトークンが表示されることを確認します。 彼らは完全に一致するはずです！

Posted on _2015-01-26_ by _John_

## Google Font API を使用したMarketo ランディングページへのカスタムフォントの追加

**メモ：これは [Murtza Manzur](https://www.linkedin.com/in/murtzam) によるブログ投稿です。 Murtza は、サンフランシスコのベイエリアを拠点とするMarketoのデベロッパーエバンジェリストです。**
例えば、Marketoでランディングページを作成し、カスタムフォントを使用するとします。 これは、Google Font API を使用して実行できます。  Google Fonts を参照して、CSS ファイルに読み込みメソッドを追加します。

`@import url(http://fonts.googleapis.com/css?family=Open+Sans:400,300,600);`

Posted on _2015-01-26_ by _Murta_

## 電子メールスクリプティングを使用してリードの名を大文字にする

例えば、リードの名前を「John doe」のように小文字で入力するとします。 ただし、メールキャンペーンを送信する場合、John Doe のように、メール内のリードの名前を大文字にしたいと考えます。 メールスクリプティングを使用して、リードの名前を大文字にすることができます。 その方法を次に示します。

1. メールプログラムで、「マイトークン」タブをクリックします。
1. 「メールスクリプト」を右側のパネルから中央のパネルにドラッグして、新しいメールスクリプトトークンを作成します。 トークンに名前を付けます。
1. 「スクリプトトークンを編集」テキストボックスに、以下のコードをペーストします。 右側のパネルのリードオブジェクトの下にある「名」チェックボックスをオンにします。 次に、「保存」をクリックします。

```javascript
# set($name = ${lead.FirstName})
# set($formattedFirstName = $name.substring(0).toUpperCase())
$formattedFirstName
```

1. メールアセットでトークンを参照します。 最初の文字が大文字のリードの名が出力されます。 メールスクリプティングについて詳しくは、[ メールスクリプティングドキュメント ](/help/email-scripting.md) を参照してください。

Posted on _2015-01-26_ by _Murta_

## Marketo REST API からのすべてのリードを取得

[StackOverflow で、REST API を使用してMarketoからすべてのリードのリストを取得する方法を尋ねる質問 ](https://stackoverflow.com/questions/28184900/how-do-i-get-the-list-of-all-the-leads-in-marketo) がありました。 このデータは、[ フィルタータイプによる複数のリードの取得 REST API エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) を使用してクエリできます。 Marketoのリードには、1 から順にリード ID が割り当てられます。 [ フィルタータイプ REST API エンドポイントで複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) を使用すると、各呼び出しでリード ID で 300 件のリードをクエリできます。 このエンドポイントを呼び出すたびに、id を filterType として指定し、リード ID を filterValues として指定する必要があります。 すべてのリードを取得するには、一度にリードの合計数 300 を反復処理します。 Y
Marketo インスタンス内のリードの合計数は、Marketo UI から取得できます。 Marketo UI で、「リードデータベース」タブに移動し、「システムスマートリスト」をクリックします。次に、「すべてのリードスマートリスト」をクリックし、最後に「リード」タブをクリックします。 次に、ID 列をクリックして降順に並べ替えます。 リードが並べ替えられた後、すべてのリードをクエリする場合、最初のリードの ID がリード ID の上限になります。 Marketo UI にアクセスしてリードの合計数を取得できない場合は、[ リードの取得アクティビティ REST API を使用してこの値を取得する代替アプローチ ](https://stackoverflow.com/questions/28419967/get-all-leads-programmatically-in-marketo-v1) を使用できます。

1. 最初の API 呼び出し：...を、以下の範囲のすべての値に置き換えます。

`/rest/v1/leads.json?filterType=Id&filterValues=1,2,3,...,298,299,300`

次に、最初の呼び出し用の Ruby のサンプルコードを示します。

```java
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/leads.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
# Replace with filter type and values
ids_needed = (1..300).to_a.join(",")
filter_type_and_values = "&filterType=Id&filterValues=" + ids_needed
request_url = marketo_instance + endpoint + auth_token + filter_type_and_values

# Make request
response = RestClient.get request_url

# Returns Marketo API response
puts response
```

1. 2 回目の API 呼び出しと、それに続く各 API 呼び出しは、リードの合計数に達するまで同じパターンに従います。

```
//replace ... with all the values in between
/rest/v1/leads.json?filterType=Id&filterValues=301,302,303,...,598,599,600
```

詳しくは、[REST API ドキュメント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) を参照してください。

Posted on _2015-01-28_ by _Murta_

## Iframe から親ページへのフォーム送信アクションの実行

ユーザーが iframe フォームを使用し、フォームに入力した訪問者を「ありがとうございます」ページやPDF、ビデオなどに誘導する例をいくつか確認しました。 問題は、フォームが親ページとは異なるランディングページに埋め込まれているので、アクションはフォームがある内部ページでのみ発生することです。 これを解決するために、作成した 2 つのJavaScript タグを以下に示します。 iframe ページにHTML要素として挿入するか、iframe に使用するランディングページテンプレートに直接挿入します。 最後の `</body>` タグの前に挿入します。 最初のタグは親ページに対してアクションを実行し、2 番目のタグは新しいタブでページを開きます。

**親ページでのフォームアクション**

```javascript
<script>
MktoForms2.whenReady(function (form){
form.onSuccess(function (values, url){
window.parent.location.assign(url);
return false;
           });
});
</script>
```

**新しいタブのフォームアクション**

```javascript
<script>
MktoForms2.whenReady(function (form){
var newWin;
form.onSubmit(function (){
newWin = window.open('about:blank', 'myWindow');
});
form.onSuccess(function (values, url){
newWin.location.replace(url);
return
 false;
});
});
</script>
```

Posted on _2015-02-02_ by _Yanir_

## YouTube ビデオから市場にビューデータを送信

例えば、特定のビデオを開始または終了したかどうかに基づいて、Marketoでリードをセグメント化するとします。 これは、Munchkin、YouTubeの Iframe API およびMarketoのスマートリストを使用して実行できます。 この投稿のサンプルコードを使用すると、ビデオの開始イベントとビデオの終了イベントをMunchkinを通じてMarketoに送信できます。 これを機能させるには、ビデオビューイベントのMarketoへの送信を開始する前に、Munchkinをページに読み込む必要もあります。 開始および終了したビデオは、リードのアクティビティログに表示されます。 データをMarketoに取り込んだ後、スマートリストを作成し、ビデオを開始または終了したリードをセグメント化できます。

1. 埋め込むYouTube ビデオの ID を取得します。**使用するYouTube ビデオの URL から、`v=` の後の一連のランダムな文字である ID をメモします。
1. このコードサンプルの 8 行目の手順 1 のYouTube ビデオ ID を配置します。 次に、ページのHTMLで `</body>` の前にコードを配置します。

```javascript
<div id="player"></div>
<script>
var tag = document.createElement('script');
tag.src = "https://www.youtube.com/iframe_api";
document.getElementsByTagName('head')[0].appendChild(tag);

//Change 'iiqxcjxJ5Us' to video needed
var player, videoId = 'iiqxcjxJ5Us';
function onYouTubeIframeAPIReady() {
player = new YT.Player('player', {
height: '390',
width: '640',
videoId: videoId,
events: {
'onStateChange': onPlayerStateChange
}
});
}

function onPlayerStateChange(event) {
switch( event.data ) {
//Send video started event to Marketo
case YT.PlayerState.PLAYING: Munchkin.munchkinFunction('visitWebPage', {
url: '/video/'+videoId
, params: 'video=started'
}
);
break;
//Send video finished event to Marketo
case YT.PlayerState.ENDED: Munchkin.munchkinFunction('visitWebPage', {
url: '/video/'+videoId
, params: 'video=finished'
}
);
break;
}

}
</script>
```

1. ビデオの URL と、検索するビューイベントを「Querystring contains」の値として使用して、Marketoでスマートリストを作成します。 YouTube Iframe API について詳しくは、[YouTube API ドキュメント ](https://developers.google.com/youtube/iframe_api_reference) を参照してください。 Marketoについて詳しくは、[Munchkin開発者向けドキュメント ](/help/javascript-api/lead-tracking.md) を参照してください。

Posted on _2015-02-02_ by _Murta_

## Marketo SOAP API のヒントとテクニック

メモ：これはゲストのブログ投稿です。 [Ed Blachman はシニアアーキテクト ](https://www.linkedin.com/uas/login?session_redirect=https%3A%2F%2Fwww.linkedin.com%2Fprofile%2Fview%3Fid%3D2777965) [TIBCO Software, a well-known vendor of enterprise software](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) です。 Ed は、Gartner が「市民開発者」と呼ぶ製品を、プログラミングを自ら行わなくても使用するクラウドサービスと統合できるように取り組んでいます。 [MarketoのSOAP API](/help/soap-api/soap-api.md) は、デベロッパーがMarketoの機能を活用し、独自のアプリケーションと統合できる強力なツールです。 [ 正式なドキュメント ](./getting-started.md) と [ コミュニティリソース ](https://nation.marketo.com/) の間には、その使用方法に関する多くの情報が提供されています。 使い始めた頃、私はその情報に大いに頼り、非常に貴重なものだと思いました。 しかし、その過程で、私はそれらのどの場所でも見たことのないヒントやコツを積み上げました。 私が考えたもののいくつかを以下に示します。

**開発者のサンドボックス** サンドボックスは、もちろん API 開発者にとって素晴らしいリソースです。組織の実際のMarketo ユーザーが行う実際のマーケティングアクティビティに干渉することなく、Marketoの機能を試し、オブジェクトを追加および削除できる安全な場所です。 ただし、サンドボックスは万能薬ではありません。
例えば、サンドボックスを別の開発グループと共有する必要がありましたが、サンドボックスを所有しているという考えに慣れていたので、ある程度の手間がかかりました。 最終的に、共有のベストプラクティスをいくつか考え出しました。- サンドボックスの内容の完全な知識に依存するテストを記述しないでください。 共有リソースの場合、スキーマは予告なく変更される場合があります。また、リードデータベース、プログラム、その他のエンティティのエントリ全体も変更される場合があります。 テストでサンドボックスについて完全に知識していることが前提の場合、開発サイクルは、それを共有しているグループのブラックアウト期間を作成します。 通常、開発サイクルはユーザーの開発サイクルと一致しないので、これはリソースを大量に消費するだけで冷却にはならないことに相当します。 考え抜く限り、これは必要ありません。  – 規則を使って、リード、リードスキーマフィールド、プログラムなど、すべての要素にラベルを付けてください。 自分の物を自分の物として見つけ、他の物は自分の物として残す事を共同入居者に認めれば、共有のための固い土台を築くべきです。 リードの場合は、カスタムフィールドを作成し、このカスタムフィールドを使用して規則を作成し、これらのリードをテストリードとして識別できます。 リストまたはプログラムの場合は、オブジェクトの名前の先頭に、そのオブジェクトが自分に属していることを示す文字列を付ける場合があります。  – 自分でクリーンアップするテストを記述することを検討します。テストでは、まず目的のオブジェクトを作成し、次に、それらのオブジェクトにアクセス、更新、または選択的に削除してから、最終的に削除します。 （これは、SOAP API では 100% 達成できないことに注意してください。サンドボックス内のすべて、またはその問題の実際のインスタンスがSOAP API を介して管理できるわけではありません。 それでも、できる限りこれを行う価値があります。

**実際のインスタンス** サンドボックスの問題は、実稼動環境で使用されていないので、Marketo インスタンスでの実際の使用方法を把握するのが難しいことです。 運よくMarketoのパワーユーザーを採用できたとしても、社内のMarketo ユーザー向けにカスタム開発を行っていたとしても、それほど問題にはなりません。 でも私のチームの場合は本当に大変でした。 私たちは誰もMarketoの専門家ではなく、多くのクラウドサービスを理解するように求められたので、私たちは何の専門家になるための人員を持っていませんでした。 実際のインスタンスへのアクセスから得たインサイトの一部を次に示します。– 大規模なリードスキーマ。 アクセスした実稼動インスタンスのリードスキーマには、200 を超えるフィールドがあります。 そのため、UI デザイナーは、デザインする UI がそのサイズ（またはそれ以上）のスキーマに対応する必要があることがはっきりしました。 - バースト使用。 最も使用率が高い時間と低い時間（作成または更新されたリードの数の観点から）の間に、大きな違いが 2 つ見つかりました。 これは、API 呼び出しから返されるデータの量（明白な）と、API 呼び出しが応答するまでにかかる時間（明白でない可能性がある）の両方に影響を与えました。

**API 呼び出し応答時間** 時間帯、API 呼び出しの詳細、インスタンスの内容によっては、SOAP API の応答時間が平均より長くなる場合があります。 API 呼び出しに 1 分半かかることもありました。 あなたはそれに対処する可能性を認識する必要があります：- テスト。 使用に関する問題ではないかもしれません。 しかし、単にそう仮定するのではなく、テストを行います。  – 使用状況を調整します。 この例では、[getMultipleLeads](/help/soap-api/getmultipleleads.md) への呼び出しのページサイズを API で許可されている大きさに設定するのが最大の問題でした。 お客様の API 割り当てをできる限り効率的にすることが目標なので、ある程度の意味を持つコンテキストで。 ただし、コンテキストによっては、ユーザーの API 呼び出し割り当て制限について集中的に心配する必要がない場合があります。この場合、データの小さいページを要求することで、確実に応答時間が向上します。

**リードのパーティション化** Marketoには強力なツールであるパーティションとワークスペースが用意されており、複数のマーケティンググループで 1 つのMarketo インスタンスを共有できます。 ただし、これらのツールは、SOAP API に直接反映されません。 例えば、getMultipleLeads を使用して、特定の日時以降に更新または作成されたすべてのリードを取得する場合、どのパーティションまたはワークスペースに特定のリードが含まれているかに関係なく、インスタンス内でその条件に当てはまるすべてのリードを取得します。 リードの作成とリストへのリードの追加は、リードのパーティション化が API 呼び出しの実際の動作に影響を与える可能性がある他のコンテキストです。 これは、パーティションとワークスペースが、上記のサンドボックス共有の問題を解決するのに必要なソリューションではない可能性があることを意味します。 これが問題かどうかを把握するにはどうすればよいでしょうか？ これらすべてが役に立つことを私は見つけました：開発者エバンジェリストは、API の使用に関する成功に全力を注いでおり、質問がある場合は、答えを見つけるために取り組むのが驚くほど得意です。 - [API ドキュメント ](./getting-started.md). エバンジェリストは、すでにこの問題をドキュメントの一部に取り入れており、私たちの成功への取り組みの一環として、ドキュメントの更新に非常に優れています。  – 独自のテストケース。 サンドボックスを共有するためにパーティションとワークスペースを使用することは素晴らしいアイデアではないかもしれませんが、サンドボックスは、パーティションとワークスペースを操作して、意図した使用に課題が生じるかどうかを把握するのに最適な場所です。 （エバンジェリストへの質問を絞り込む良い方法でもあります。

**TIMTOWTDI とテスト** 「実行する方法は複数あります」 – Perl プログラミングのモットーは、特定のコンテキストでMarketo SOAP API に実際に適用されます。 例えば、一連のリードの更新と、それらのリードを何らかのリストに追加することを組み合わせたいと考えました。 SOAP API では、次の 2 つの方法でこれを実行できます。1. [importToList](/help/soap-api/importtolist.md) + [getImportToListStatus](/help/soap-api/getimporttoliststatus.md). ドキュメントを読むと、これは明らかに、これを行う「通常の」方法です。 しかし、インポート操作のステータスをポーリングする必要があるという事実は、私にとって黄色のフラグを発生させました。 インポートを実装する方法は本当にありましたか？ 1. [syncMultipleLeads](/help/soap-api/syncmultipleleads.md) + [listOperation](/help/soap-api/listoperation.md)。 これは、単一の importToList 呼び出しよりもエレガントではないように思われますが、ポーリングには依存しません。 それは実行可能な選択肢でしたか？ このようなケースは、エバンジェリストが対処するのが難しいのです。なぜなら、これらのケースは、あなたが扱っているインスタンスの性質と、あなたが何をしようとしているかにかかっているからです。 幸いにも、堅牢な単体テスト環境を設定したら、それを使用して次のような質問も検討できるはずです。 この特定のケースでは、オプション 2 がオプション 1 よりも私のユースケースに適していることがわかりました。これは、ポーリングのためではなく、importToList に関してフィールド指向の制限に遭遇したことや、制御できないコンテキストやインスタンスで使用できるコードを記述しようとしたためです。 ただし、ユースケースは異なる場合があり、テストが唯一の確認方法です。

**結論付け** これは大きな秘密ではないと思います。 一方で、始める前にこれらすべてを知っていたら、私はゲームの前に進んでいたでしょう。 私はあなたがそれを役に立つと思うことを願っています。

Posted on _2015-02-05_ by _David_

## Boomi でのMarketo REST API の使用：静的リストからのリードの取得と削除

このシリーズの第 1 部では、Boomi HTTP コネクタを使用して、Boomi を通じて REST API の使用を開始する方法、具体的には REST API へのアクセスに必要な認証トークンを取得し、プロセス変数に保存する方法について説明しました。 次に、Marketoへの呼び出しを開始します。この取り組みでは、[ リスト ID で複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists) と [ リストからリードを削除 ](/help/rest-api/lead-database.md) の両方を実行する方法を示します。 リストからのリードの削除には特に注意を払ってください。なぜなら、私がそこに着いたときに拡大する、Boomi の仕事の非常に「軽く文書化された」そして微妙な側面があるからです。

Out NEXT では、この機能を拡張して、リードアクティビティの取得などの興味深い作業を開始しますが、それは別の日のブログです。 今回は、2 番目と 3 番目の重点領域を取り上げます。 確認として、以下に必要な JSON 応答を含めました。 Boomi で JSON プロファイルを作成するには、JSON タイプのプロファイルコンポーネントを作成し、「import」をクリックしてファイルを選択するだけです。 残りの作業は Boomi が行い、複数の ID を許可する必要がある場合などに適用されます。 [ リスト ID で複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists) 用の JSON の例

```json
{
  "requestId": "",
  "success": true,
  "nextPageToken": "",
  "result": [
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    },
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    },
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    }
  ]
}
```

[ リストリクエストからリードを削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE) 用の JSON の例

```json
{
   "input":[
      {
         "id": ""
      },
      {
         "id": ""
      }
   ]
}
```

[ リスト応答からリードを削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE) 用の JSON の例

```json
{
  "requestId": "",
  "success": true,
  "result": [
    {
      "id": 1,
      "status": ""
    },
    {
      "id": 2,
      "status": "",
      "reasons": [
        {
          "code": "",
          "message": ""
        }
      ]
    }
  ]
}
```

「リスト ID で複数のリードを取得」**前の記事で定義したのと同じ接続を使用して、別のコネクタ（Get）をプロセスにドロップします。 「リスト ID で複数のリードを取得」という新しい操作を作成します（一貫性を求めるステッカーです）。属性は次のとおりです。- リクエストプロファイル：なし（これはリクエスト URL を使用します） – 応答プロファイルタイプ : jSON – 応答プロファイル：上記のリスト ID で複数のリードを取得の応答に基づいて、新しいプロファイルを作成します。 リストされているフィールドだけでなく、必要なフィールドが返されるように変更できます。 重要な点は、JSON 応答プロファイルは、REST API から要求しているフィールドのリストと実際に一致する必要があり、必要なフィールドのみをリクエストする必要があることです。 プロセスプロパティ オブジェクトで、「fields」というプロパティを定義しました。これは、REST で返すフィールドのコンマ区切りリストです。 これが、プロファイルに一致する必要があるリストです。 Content Type: text/plain （これは単なる URL リクエストです） HTTP メソッド：GET（REST API ドキュメントで参照します。常にリストされています） リソースパス（5 つ追加） rest/v1/list/ listID （置換変数） /leads.json?access_token= access_token （置換変数） &amp;fields= fields （置換変数）。 次に、コネクタの「パラメーター」タブで、変数値を入力できます。これらの変数値はすべて、以前にプロセスプロパティに入力したものです。 次の節では、これらを手動で入力するのを回避する方法について説明します。 このプロセスの一部をスキップします。ここでは、「リスト ID で複数のリードを取得」の応答をフラットファイルプロファイルにマッピングし、FTP サーバーに貼り付けます。これは単純な Boomi 機能だからです。

リストからリードを削除するというわけで、これは興味深いことです。同僚の一人である [ 丹羽健 ](https://www.linkedin.com/uas/login?session_redirect=https%3A%2F%2Fwww.linkedin.com%2Fprofile%2Fview%3Fid%3D7429494) がこの次のテクニックを教えてくれました。それはかなりクールで、以下に示す「RESTful アプリケーション用の POST リクエストを作成する方法」という Boomi の記事に基づいています。 最初から。 このプロセスでは、「リスト ID で複数のリードを取得」から出て、「リスト ID で複数のリードを取得」応答図形が表示されます。これを「リスト要求からリードを削除」にマッピングする必要があります。元のリストのリードから取得した ID を、削除 jSON に渡す ID リストにマッピングするだけです。 次に、同じ接続を使用して、「送信」アクションの別のコネクタをドロップします。「リスト要求からリードを削除」という新しい操作を作成します。 リクエストプロファイルの属性：jSON コンテンツタイプ：application/json リクエストプロファイル：[JSON プロファイル ] リストリクエストからリードを削除（上記のファイルから作成）応答プロファイルタイプ：jSON レスポンスプロファイル：[JSON プロファイル ] リストからリードを削除（上記のファイルから作成）コンテンツタイプ：application/json HTTP メソッド：DELETE リソースパス（add 4） rest/v1/lists/ listID （replacement 変数） /leads.json?access_token= access_token （replacement 変数） Here&#39;このコネクタの興味深い点。 コネクタタブにパラメーターを明示的に追加することはありません。 代わりに、記事で述べたように、置き換え変数と同じ名前の動的なドキュメントプロパティを作成します。 この場合、これらの変数は listID と access_token です。 これを行うと、jSON 図形が REST 呼び出しに流れ込み、パラメーターが URL の適切な場所に表示されます。 以前の呼び出しでは、これはGETであって POST ではないので、実行できません。 これで、GETと POST REST API 呼び出しが表示され、これらの REST 呼び出しを行うパターンを確認できます。 次回は、REST API を使用したリードアクティビティの書き出しについて見ていきます。これは、もう少し複雑です。

Posted on _2015-02-06_ by _John_

## Marketo ランディングページへのYouTube ビデオのリードトラッキングの埋め込み

以前のブログ投稿では、特定のYouTube ビデオを開始または終了したかどうかに基づいて、Marketoでリードをセグメント化する方法を説明しました。 このブログ投稿では、その投稿から実装を取得してMarketo ランディングページで使用する方法を説明します。

1. 新しいランディングページを作成するMarketoのプログラムに移動します。 「新規ローカルアセット」をクリックし、「ランディングページ」をクリックします。
1. ランディングページに名前を付けます。 ページ URL を割り当てます。 テンプレートを選択します。 次に、「作成」をクリックします。
1. ランディングページを作成したら、「ドラフトを編集」をクリックします。
1. 右側のパネルから「HTML」ボタンを左側のメインキャンバスにドラッグします。
1. ポップアップ表示されるカスタム HTML エディターボックスで。 次に、「保存」をクリックします。
1. ボックスの輪郭をドラッグして、HTML要素のサイズを調整します。 次に、「承認して閉じる」をクリックします。
1. 「承認済みページを表示」をクリックして、ランディングページのライブバージョンをテストします。 YouTubeを含むランディングページが新しいウィンドウで開きます。 開始および終了したビデオは、以下の 1 番目と 2 番目のスクリーンショットに示すように、リードのアクティビティログに表示されます。 データをMarketoに取り込んだ後、次のスクリーンショットに示すように、スマートリストを作成し、ビデオを開始または終了したリードをセグメント化できます。 YouTube Iframe API について詳しくは、[YouTube API ドキュメント ](https://developers.google.com/youtube/iframe_api_reference) を参照してください。 Marketoについて詳しくは、[Munchkin開発者向けドキュメントを参照してください ](/help/javascript-api/lead-tracking.md)。

Posted on _2015-02-09_ by _Murta_

## Munchkinを使用したシングルページアプリケーションの web トラッキング

単一ページアプリケーションは、最初にページを読み込んだ際にサイト内を移動するために必要なすべてのリソースを読み込む web サイトです。 ユーザーがリンクをクリックすると、コンテンツは最初のページ読み込みデータから読み込まれます。 アドレスバーの URL が従来のページナビゲーションに似ているので、ユーザーにとっては、web サイトは期待どおりに動作します。 Munchkinはユーザーが新しいページを読み込むたびに実行されるので、Munchkinは従来の web サイトとうまく連携します。 ただし、シングルページアプリケーションでは、新しいページを読み込まない場合、Munchkinは 1 回だけ実行されます。 この投稿では、ユーザーがリンクをクリックしたタイミングを追跡し、その情報をMunchkinに送信する方法を説明します。 `clickLink` Munchkin関数を使用して実装します。 クリックイベントを `clickLink` Munchkin メソッドにバインドする jQuery の実装例を以下に示します。 `clickLink` Munchkin メソッドを呼び出すと、クリックされた URL のパラメーターが渡されます。

```javascript
<script>
$("a").on('click', function(event) {
    var urlThatWasClicked = $(this).attr('href');
    Munchkin.munchkinFunction('clickLink', { href: urlThatWasClicked});
});
</script>
```

Posted on _2015-02-11_ by _Murta_

## REST API を使用したリードのスコアの変更

API を使用してMarketoでリードのスコアを変更するとします。 これは、リードの作成/更新エンドポイントを使用した REST API で実行できます。 次に、この呼び出しを行う方法を示す Ruby のコードサンプルを示します。

```ruby
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "https://AAA-BBB-CCC.mktorest.com"
endpoint = "/rest/v1/leads.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
request_url = marketo_instance + endpoint + auth_token

# Build request body
data = { "action" => "updateOnly", "input" => [ { "email" => "<example@email.com>", "leadScore" => "30" } ] }

# Make request
response = RestClient.post request_url, data.to_json, :content_type => :json, :accept => :json

# Returns Marketo API response
puts response
```

リクエストの JSON 本文では、`updateOnly` をアクションとして指定します。 つまり、リードが存在する場合にのみリクエストが機能し、存在しない場合は失敗します。 存在しないリードを作成する場合は、`createOrUpdate` をアクションとして指定します。 Marketoでリードレコードを検索するためのプライマリ ID として、リードのメールを使用します。 最後に、`leadScore` キーを使用して、リードのスコアの値を指定します。 この方法を使用すると、一度に 300 件のリードを更新できます。

Posted on _2015-02-19_ by _Murta_

## Marketo Platform で構築されたオープンなSource プロジェクトのハイライト：第 3 部

これは、開発者向けコミュニティがMarketo プラットフォームを中心に構築したオープンソースプロジェクトに焦点を当てた、進行中のシリーズの 3 番目の投稿です。 アドビでは [Marketoの GitHub アカウントのリスト ](https://github.com/Marketo/Community-Supported-Client-Libraries) を維持管理しており、Marketo開発者コミュニティが作成したクライアントライブラリおよびプロジェクトをトラッキングしています。 Marketo REST API を中心に開発された 3 つのプロジェクトを以下に示します。 **[ユーザー精神 ](http://www.usermind.com/)Marketo REST API 用に [Node.js クライアントライブラリ ](https://github.com/MadKudu/node-marketo) を作成しました。**&#x200B;**[Arunim Samat](https://github.com/asamat) は、[Marketo REST API 用のクライアントライブラリ ](https://github.com/asamat/python_marketo) を Python に作成しました。Marketoの** **[Jacques Lemieux](https://www.linkedin.com/in/jalemieux) は、Marketo REST API 用に Ruby で [ クライアントライブラリを作成しました。](https://github.com/jalemieux/mkto_rest)** 開発者向けコミュニティがMarketo プラットフォームで作成したプロジェクトが増えることを楽しみにしています。 Marketo プラットフォームのオープンソースプロジェクトに取り組んでいる場合は、[ プルリクエストを通じてこの GitHub リポジトリーに送信 ](https://github.com/Marketo/Community-Supported-Client-Libraries) してください。

Posted on _2015-02-20_ by _Murta_

## RTP キャンペーンへのMarketo フォームの挿入

多くのマーケターは、Marketo フォームをMarketo リアルタイム Personalization（RTP）キャンペーンに配置することに関心があります。 ダイアログ、ゾーン、ウィジェットなどの RTP キャンペーンタイプに関係なく、フォームのHTML コードをコピーして RTP のキャンペーンエディターに貼り付けることができます。  – 訪問者がサイトで 2～3 回クリックした後にニュースレターにサインアップできるようにする – ウェビナー用の迅速で効果的なサインアップフォーム – ゲート付きケーススタディのダウンロード – 以前に購読解除したリードを再登録するキャンペーンのフォームに入力して、リクエストされたお礼やコンテンツを受け取り、目標に到達するまでのクリック数を 1 減らします。 それでは、その方法と、Marketo RTP キャンペーンにMarketo Form 2.0 を埋め込む方法について説明します。 マーケターである RTP ユーザーが一歩進んで、訪問者にお礼のページを送る代わりに、RTP キャンペーン内にお礼のメッセージを表示することにした例を紹介します。 このオプションのコードも以下に示します。 ぜひご覧ください。あなたの体験を聞いて嬉しいです。

1. 承認済みフォームを右クリックします。 「**埋め込みコード**」を選択します。
1. **Code.** をコピーします。
1. Marketo RTP で、**キャンペーン** に移動します。
1. **新規キャンペーンを作成** をクリックします。
1. リッチテキストエディターで、**HTML アイコン** をクリックします。
1. フォーム埋め込みコードを HTML ソースエディターにペーストします。「**更新**」をクリックします。
1. フォームはエディタービューには表示されませんが、プレビューしてキャンペーンでのレンダリング方法を確認することができます。
1. 「**起動**」をクリックすると、キャンペーンが始まります。

### メモ

フォームへの変更は、フォームの「ドラフトを編集」のMarketo マーケティングアクティビティ内で行う必要があります。

### 関連記事

* [Forms 2.0](/help/javascript-api/forms-api-reference.md)

Posted on _2015-12-20_ by _Yanir_

## Marketo フォームへのリセットボタンの追加

```javascript
<script src="//app-sj01.marketo.com/js/forms2/js/forms2.min.js"></script>
<form id="mktoForm_116"></form>
<script>MktoForms2.loadForm("//app-sj01.marketo.com", "410-XOR-673", 116,
function(form) { form.getFormElem()[0].querySelector('button[type="submit"]').insertAdjacentHTML('afterend','<button type="reset" class="mktoButton">Reset</button>') });
</script>
```

Posted on _2015-03-18_ by _Murta_

## 2015 年 3 月リリースアップデート

[Marketo REST Asset API は、2015 年 3 月リリース ](https://developer.adobe.com/marketo-apis/api/asset/) でリリースされました。 この API を使用すると、Marketoのファイル、フォルダー、トークン、メールおよびメールテンプレートオブジェクトにアクセスできます。 Asset API エンドポイントへのアクセスを提供するために、読み取り専用Assets、読み取り/書き込みAssetsの 2 つのロール権限が追加されました。 API ユーザーの役割が Asset API のリリースより前の日付になっている場合は、これらの権限を使用して新しい API ユーザーの役割を作成し、アクセスを有効にする必要があります。 そうしないと、「Access Denied （アクセスが拒否されました）」という 603 エラー応答が返されます。 REST Asset API のリリースに加えて、既存の REST API エンドポイントが更新されました。 [ リード REST API エンドポイントを結合 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/mergeLeadsUsingPOST) が更新され、複数のリードを結合できるようになりました。 [ キャンペーン REST API エンドポイントのスケジュール ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST) が更新され、キャンペーンのスケジュール設定時にキャンペーンのクローンを作成できるようになりました。

Posted on _2015-03-23_ by _Murta_

## 遅延を伴う RTP キャンペーンのトリガー

このカスタム JavaScriptを使用すると、RTP ユーザーは web ページの読み込み後数秒後にキャンペーンを表示できます。 これは、ダイアログボックスおよびウィジェットキャンペーンに推奨されます。 これを使用すると、訪問者がページ上の通常のコンテンツを表示してから遅延が発生したキャンペーンを表示できます。 このコードは、キャンペーンを表示する特定のページにのみ実装することをお勧めします。 パフォーマンスに影響を与える可能性があるので、このコードをすべてのページで使用することはお勧めしません。 **設定手順** カスタムコードは、RTP カスタムデータイベント（t=timeOnPage、つまり t=60）を送信し、このイベントに一致するキャンペーンを読み込みます。 デフォルトでは、60 秒後にトリガーされます。 sendCustomRTPEvent パラメーターを他の任意の数値に変更することで、変数をカスタマイズできます。 標準 RTP コードの直後にコードを配置します。

```javascript
<script>
function sendCustomRTPEvent(a){
 var eventValue="t="+a;
 setTimeout(function(){
  rtp('send', 'event', {value: eventValue});
  rtp('get', 'campaign',true);
 }, 1000 \* a);
}
sendCustomRTPEvent(60); //Seconds
</script>
```

遅延時間の経過後に反応するように RTP キャンペーンを設定するには、次の手順に従います。1. RTP アカウントにログイン 1. 新しいセグメントの作成 1. セグメントイベント セクションで、`t=60` を追加します。 訪問者は各 RTP セグメントとセッションごとに 1 回だけ一致できるので、各キャンペーンは（スティッキーに設定されていない限り） 1 回しか表示されません。

Posted on _2015-03-24_ by _Yanir_

## 2015 年 4 月リリースアップデート

### Marketo Mobile Engagement SDK v0.3.2

Marketoに、モバイルアプリのマーケティングの自動処理とユーザーエンゲージメントが含まれるようになりました。 [Marketo Mobile SDK](/help/mobile/mobile.md) をiOSまたはAndroid アプリにインストールすると、マーケターはアプリのイベントをリッスンして、関連するプッシュ通知を送信できます。

### REST API の機能強化

* カスタムオブジェクト

新しい [ カスタムオブジェクトエンドポイント ](/help/rest-api/custom-objects.md) が導入され、Marketo カスタムオブジェクトに存在するデータをプログラムでリスト、記述、CRUD できるようになりました。

カスタムオブジェクト API エンドポイントへのアクセスを提供するために、役割の権限が追加されました。読み取り専用カスタムオブジェクト、読み取り/書き込みカスタムオブジェクトです。 API ユーザーの役割がカスタムオブジェクト API のリリースより前の場合は、これらの権限を使用して新しい API ユーザーの役割を作成し、アクセスを有効にする必要があります。 そうしないと、「Access Denied （アクセスが拒否されました）」という 603 エラー応答が返されます。

* キャンペーンのスケジュール – プログラムの複製

新しいオプションパラメーター「cloneToProgramName」が [schedule campaign API](/help/rest-api/data-ingestion.md) に導入されました。 このパラメーターが存在する場合、キャンペーンの親プログラムのクローンが作成され、新しく作成されたキャンペーンがスケジュールされます。 パラメーターは、生成されるプログラムの目的の名前を指定します。

Posted on _2015-04-28_ by _Travis Kaufman_

## インスタンス間でのメール購読解除の同期

Marketoの複数のインスタンスを管理していますか？ 複数のインスタンス間でリード情報を同期し続けるのは、困難な場合があります。 外部 web サービスを呼び出す Webhook を使用して、インスタンス間でメール購読解除を同期する方法を次に示します。 外部 web サービスは、各インスタンスをループし、登録解除イベントをトリガーした既知のリードを探します。 一致するリードが見つかると、対応するリードレコードの「購読解除」フィールドが更新されます。 次に、そのアイデアを示す図を示します。  Web サービスを実装するかどうかはユーザー次第ですが、以下のコードはプロセスをすぐに開始するのに役立ちます。

### 外部 Web サービス

外部 web サービスは、同期が必要な各Marketo インスタンスに対して、次の手順を実行します。

1. インスタンス固有の REST API を作成します [ エンドポイント URL](/help/rest-api/endpoint-reference.md)
1. [Identity](/help/rest-api/authentication.md) を使用してアクセストークンを取得します
1. [ フィルタータイプ別に複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) を使用して、メールアドレスに一致するリードレコードのリストを取得します
1. リードの作成/更新を使用して、各リードレコードの「購読解除」フィールドを更新

次の図は、外部 web サービス呼び出しとMarketo REST API 呼び出しの詳細を示しています。  以下のサンプルコードは標準提供の web サービスではありません。 代わりに、コマンドラインを介してに引数を渡すことができるコンソールモードプログラムです。 適切なMarketo API を呼び出してインスタンス間でリードレコードを更新する方法を示すことを目的としています。 Web サービスの実装は、読者の演習として残されています。
**サンプルコード** サンプルコードを起動して実行するには、お気に入りの IDE で Java プロジェクトを作成する必要があります。 その後、次の変更を行う必要があります。1. サンプルコードでは [json-simple](https://code.google.com/archive/p/json-simple) を使用して JSON 文字列を解析します。 json-simple jar を Java プロジェクトに追加します。 1. サンプルコードは、各Marketo インスタンスのメタデータを保持する構造になっています。 インスタンスの実際の値を、構造に次のように配置します。

```java
public static String instanceInfo[][] = {
{ "AccountId1", "ClientId1","ClientSecret1" },    // Instance 1 metadata
{ "AccountId2", "ClientId2","ClientSecret2" },    // Instance 2 metadata
{ "AccountId3", "ClientId3","ClientSecret3" }     // Instance 3 metadata
};
```

Marketo管理パネルで、インスタンスのメタデータを確認できます。

* アカウント Id 管理者/統合/Munchkin/Munchkin アカウント
* クライアント Id とクライアントシークレット管理者/統合/ LaunchPoint / メールの購読解除同期/詳細を表示

このサンプルコードでは、上記の外部 web サービスの「id」および「email」クエリパラメーターをシミュレートする 2 つのコマンドライン引数を使用します。

1. args[0] = アカウント Id
1. args[1] = メールアドレス

インスタンスの実際の値を引数としてプログラムに渡します。 以下は、Intellij IDEA のプロジェクト設定のスクリーンショットです。

**SyncEmailUnsubscribe.java**

```java
package com.marketo;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;
import org.json.simple.parser.ParseException;

import javax.net.ssl.HttpsURLConnection;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.Iterator;
import java.util.NoSuchElementException;
import java.util.Scanner;

public class SyncEmailUnsubscribe {
    // Define Marketo instance meta data here.
    // Each row contains three elements: Account Id, Client Id, Client Secret.
    // For example:
    //  public static String instanceData[][] = {
    //    {"111-AAA-222", "2f4a4435-f6fa-4bd9-3248-098754982345", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W"},
    //    {"222-BBB-333", "5f4a6657-f6fa-4cd9-4356-123083238821", "gfjgfIVE9h4Jjcl59cOMAKFSk78ut12W"},
    //    {"444-CCC-444", "9f4a4678-f6fa-4dd9-7735-908713247721", "xzcxvbVE9h4Jjcl59cOMAKFSk78ut12W"}
    //  };
    //
    public static String instanceData[][] = {
            // ADD YOUR INSTANCE META DATA HERE
    };

    public static void main(String[] args) {
        String accountId = args[0];     // Account id that processed the unsubscribe
        String emailAddress = args[1];  // Email address of lead that unsubscribed

        SyncEmailUnsubscribe seu = new SyncEmailUnsubscribe();

        // Loop through each Marketo instance
        for (int i = 0; i < instanceData.length; i++) {

            // Make sure we skip instance that triggered the webhook
            if (!accountId.equals(instanceData[i][0])) {
                String endpointUrl = String.format("https://%s.mktorest.com", instanceData[i][0]);

                // Generate access token
                String identityUrl = String.format("%s/identity/oauth/token?grant_type=client_credentials&client_id=%s&client_secret=%s", endpointUrl, instanceData[i][1], instanceData[i][2]);
                String token = seu.getToken(identityUrl);

                // Get lead records for given email address (may be duplicates)
                String getLeadsUrl = String.format("%s/rest/v1/leads.json?access_token=%s&filterType=email&filterValues=%s", endpointUrl, token, emailAddress);
                String leads = seu.getLeads(getLeadsUrl);

                // Update unsubscribed field in lead record
                String updateLeadsUrl = String.format("%s/rest/v1/leads.json?access_token=%s", endpointUrl, token);
                seu.updateLeads(updateLeadsUrl, leads, accountId);
            }
        }

        System.exit(0);
    }

    // Call Identity Service to generate access token
    public String getToken(String url) {
        // Call Identity Service
        String tokenData = getData(url);

        // Convert response into JSONObject
        JSONParser parser = new JSONParser();
        Object obj = null;
        try {
            obj = parser.parse(tokenData);
        } catch (ParseException pe) {
            System.out.println("position: " + pe.getPosition());
            System.out.println(pe);
        }

        // Retrieve access_token
        JSONObject jsonObject = (JSONObject)obj;
        return jsonObject.get("access_token").toString();
    }

    // Call Get Multiple Leads by Filter Type Service to get lead records
    public String getLeads(String url) {
        return getData(url);
    }

    // Call Create/Update Lead Service to update "unsubscribed" flag in lead record
    public void updateLeads(String url, String leads, String account) {
        JSONObject body = composeBody(leads, account);
        if (body != null) {
            postData(url, body);
        }
    }

    // Compose JSON body for Create/Update Leads Service
    private JSONObject composeBody(String leads, String account) {
        JSONObject body = new JSONObject();

        // Convert leads into JSONObject
        JSONParser parser = new JSONParser();
        Object obj = null;
        try {
            obj = parser.parse(leads);
        } catch (ParseException pe) {
            System.out.println("position: " + pe.getPosition());
            System.out.println(pe);
        }
        JSONObject leadsObj = (JSONObject)obj;

        Object success = leadsObj.get("success");
        if (success.equals(true)) {
            body.put("action", "updateOnly");
            body.put("lookupField", "id");
            body.put("asyncProcessing", "true");

            // Build array of lead objects
            JSONArray input = new JSONArray();
            JSONArray result = (JSONArray) leadsObj.get("result");
            Iterator<JSONObject> iterator = result.iterator();
            while (iterator.hasNext()) {
                JSONObject leadIn = (JSONObject)iterator.next();
                JSONObject lead = new JSONObject();
                lead.put("id", leadIn.get("id"));
                lead.put("unsubscribed", "true");
                lead.put("unsubscribedReason", "Cross instance synch triggered by webhook from: " + account);
                input.add(lead);
            }

            body.put("input", input);
        }
        return body;
    }

    // HTTP POST request
    private String postData(String endpoint, JSONObject body) {
        String data = "";
        try {
            // Make request
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("POST");
            urlConn.setAllowUserInteraction(false);
            urlConn.setDoOutput(true);
            urlConn.setRequestProperty("Content-type", "application/json");
            urlConn.setRequestProperty("accept", "application/json");
            urlConn.connect();
            OutputStream os = urlConn.getOutputStream();
            os.write(body.toJSONString().getBytes());
            os.close();
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                System.out.println("Status: 200");
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
                System.out.println(data);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    // HTTP GET request
    private String getData(String endpoint) {
        String data = "";
        try {
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("GET");
            urlConn.setAllowUserInteraction(false);
            urlConn.setDoOutput(true);
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                System.out.println("Status: 200");
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
                System.out.println(data);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    private String convertStreamToString(InputStream inputStream) {
        try {
            return new Scanner(inputStream).useDelimiter("A").next();
        } catch (NoSuchElementException e) {
            return "";
        }
    }
}
```

### Marketoの設定

同期するMarketo インスタンスごとに、次の手順を実行します。

1. 「リードの読み取り/書き込み」の役割の権限を持つカスタムサービスを作成します。 カスタムサービスの作成に慣れていない場合は、[ こちら ](/help/rest-api/custom-services.md) をクリックします。
1. 外部 web サービスを呼び出す Webhook を作成します。 Webhook の作成に慣れていない場合は、[ こちら ](/help/webhooks/webhooks.md) をクリックします。
1. Webhook を Smart Campaign のフローステップとして追加します。

以下のスクリーンショットは、クエリパラメーターを自動入力するトークンを使用して、上記で指定したサービスを呼び出す Webhook を作成する方法を示しています。 Webhook を作成したので、フローアクションとしてスマートキャンペーンに追加できます。  スマート・リストには、「電子メールの登録解除」トリガーが含まれている必要があります。

### 検証

これをすべてテストするには、複数のMarketo インスタンスで同じメールアドレスを持つリードを作成します。 メールアドレスを必ず所有するようにしてください。 1 つのインスタンストリガーで、「メールを送信」フローアクションを実行し、結果のメールを開いて、「購読解除」をクリックします。 結果を検証するには、他の各インスタンスにログインし、メールアドレスに関連付けられているリードレコードを調べます。 「Unsubscribed」チェックボックスがオンになり、「Unsubscribed Reason」フィールドには、同期を開始したソースアカウント ID を含むメモが含まれています。

Posted on _2015-05-11_ by _David_

## REST API を使用したリードデータの変更の同期

この POST では、Marketoに更新をポーリングするために繰り返し実行できるコードサンプルを提示しました。 その目的は、Marketo API を使用してリードデータの変更内容を特定し、変更があったリードデータを抽出することでした。 このデータは、同期のために外部システムにプッシュできます。 提示されたコードサンプルは、SOAP API を使用していました。 [ 新しい歩き方 ](https://www.youtube.com/watch?v=G-7ZJjLy5D8&feature=youtu.be) がありますが、それは [Marketo REST API](/help/rest-api/rest-api.md) を使用する方法です。 この投稿では、[ リードの変更を取得 ](/help/rest-api/rest-api.md)、[ リードを ID で取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) の 2 つの REST エンドポイントを使用して同じ目標を達成する方法を説明します。 プログラムには、2 つの主な手順が含まれています。

1. Get Lead Changes を呼び出して、特定のリードフィールドが変更された、または特定の期間内に追加されたすべてのリード ID のリストを生成します。
1. リスト内の各リード ID に対して Get Lead ID を呼び出し、リードレコードからフィールドデータを取得します。

手順 2 で取得したデータを取得し、外部システムで使用できるようにフォーマットします。  **プログラム入力** デフォルトでは、プログラムは現在の日付から 1 日後に「戻り」変更を探します。 したがって、例えば、このプログラムを毎日同時に実行できます。 さらに時間を遡るには、コマンドライン引数として日数を指定すると、時間ウィンドウを効果的に増やすことができます。 プログラムには、変更可能ないくつかの変数が含まれています。CUSTOM_SERVICE_DATA – これには、Marketo[ カスタムサービス ](/help/rest-api/custom-services.md) データ（アカウント ID、クライアント ID、クライアントシークレット）が含まれます。 LEAD_CHANGE_FIELD_FILTER – 変更について検査するリードフィールドのコンマ区切りリストが含まれます。 READ_BATCH_SIZE – 一度に取得するレコードの数です。 これを使用して、体のサイズに合わせて応答を調整します。 **プログラム出力** プログラムは、変更されたすべてのリードレコードを収集し、次のようにリードオブジェクトの配列として JSON にフォーマットします。

```json
{
    "result": [
        {
            "leadId": "318592",
            "updatedAt": "2015-07-22T19:19:07Z",
            "firstName": "David",
            "lastName": "Everly",
            "email": "<deverly@marketo.com>"
        },

        ...more lead objects here...
    ]
}
```

その後、この JSON をリクエストペイロードとして外部 web サービスに渡し、データを同期させることができるということです。 **プログラムロジック** まず、時間枠を確立し、REST エンドポイント URL を作成して、認証アクセストークンを取得します。 次に、Get Paging Token/Get Lead Changes ループを起動します。このループは、リードの変更の供給が枯渇するまで実行されます。 このループの目的は、一意のリード ID のリストを蓄積して、プログラムの後半でリード ID でリードを取得するためにそれらを渡すことができるようにすることです。 この例では、「リードの変更を取得」で「firstName」、「lastName」、「email」の各フィールドへの変更を検索するように指定します。 目的に合わせてフィールドの任意の組み合わせを選択できます。 リードの変更を取得は、結果をフィルタリングするために使用できる、アクティビティタイプ ID を含む「結果」オブジェクトを返します。 メモ：[ アクティビティタイプを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getAllActivityTypesUsingGET) REST エンドポイントを呼び出すことで、アクティビティタイプのリストを取得できます。 返される 2 つのアクティビティタイプに関心があります。1. 新しいリード （12）

```json
{
    "id": 12024682,
    "leadId": 318581,
    "activityDate": "2015-03-17T00:18:41Z",
    "activityTypeId": 12,
    "primaryAttributeValueId": 318581,
    "primaryAttributeValue": "David Everly",
    "attributes": [
        {
            "name": "Created Date",
            "value": "2015-03-16"
        },
        {
            "name": "Source Type",
            "value": "New lead"
        }
    ]
}
```

1. Change Data Value （13） Change Data Value 応答の「name」プロパティを調べることで、どのフィールドが変更されたかを知ることができます。

```json
{
    "id": 12024689,
    "leadId": 318581,
    "activityDate": "2015-03-17T22:58:18Z",
    "activityTypeId": 13,
    "fields": [
        {
            "id": 31,
            "name": "lastName",
            "newValue": "Evely",
            "oldValue": "Everly"
        }
    ],
    "attributes": [
        {
            "name": "Source",
            "value": "Web form fillout"
        }
    ]
}
```

これら 2 つのタイプのアクティビティのいずれかが返された場合、関連するリード ID がリストに保存されます。 リストを取得したら、項目ごとに「Get Lead by Id」を呼び出して、リストを繰り返し呼び出すことができます。 これにより、リスト内の各リードの最新のリードデータが取得されます。 この例では、`leadId`、`updatedAt`、`firstName`、`lastName`、`email` のリードフィールドを取得します。 目的に合わせてフィールドの任意の組み合わせを選択できます。 これを行うには、フィールド パラメーターを指定して、リードを ID で取得します。 最後に、上記のようにリードオブジェクトの配列として結果を JSON 化します。

**プログラムコード**

```java
package com.marketo;

// minimal-json library (<https://github.com/ralfstx/minimal-json>)
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;
import com.eclipsesource.json.JsonValue;

import java.io.\*;
import java.net.MalformedURLException;
import java.net.URL;
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.\*;

import javax.net.ssl.HttpsURLConnection;

public class LeadChanges {
    //
    // Define Marketo REST API access credentials: Account Id, Client Id, Client Secret.  For example:
    //    public static String CUSTOM_SERVICE_DATA[] =
    //      {"111-AAA-222", "2f4a4435-f6fa-4bd9-3248-098754982345", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W"};
    //
    private static final String CUSTOM_SERVICE_DATA[] =
            {INSERT YOUR CUSTOM SERVICE DATA HERE};

    // Lead fields that we are interested in
    private static final String LEAD_CHANGE_FIELD_FILTER = "firstName,lastName,email";

    // Number of lead records to read at a time
    private static final String READ_BATCH_SIZE = "200";

    // Activity type ids that we are interested in
    private static final int ACTIVITY_TYPE_ID_NEW_LEAD = 12;
    private static final int ACTIVITY_TYPE_ID_CHANGE_DATA_VALE = 13;

    public static void main(String[] args) {
        // Command line argument to set how far back to look for lead changes (number of days)
        int lookBackNumDays = 1;
        if (args.length == 1) {
            lookBackNumDays = Integer.parseInt(args[0]);
        }

        // Establish "since date" using current timestamp minus some number of days (default is 1 day)
        Calendar cal = Calendar.getInstance();
        cal.add(Calendar.DAY_OF_MONTH, -lookBackNumDays);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
        String sinceDateTime = sdf.format(cal.getTime());

        // Compose base URL
        String baseUrl = String.format("https://%s.mktorest.com",
                CUSTOM_SERVICE_DATA[0]);

        // Compose Identity URL
        String identityUrl = String.format("%s/identity/oauth/token?grant_type=%s&client_id=%s&client_secret=%s",
                baseUrl, "client_credentials", CUSTOM_SERVICE_DATA[1], CUSTOM_SERVICE_DATA[2]);

        // Call Identity API
        JsonObject identityObj = JsonObject.readFrom(getData(identityUrl));
        String accessToken = identityObj.get("access_token").asString();

        // Compose URLs for Get Lead Changes, and Get Paging Token
        String leadChangesUrl = String.format("%s/rest/v1/activities/leadchanges.json?access_token=%s&fields=%s&batchSize=%s",
                baseUrl, accessToken, LEAD_CHANGE_FIELD_FILTER, READ_BATCH_SIZE);
        String pagingTokenUrl = String.format("%s/rest/v1/activities/pagingtoken.json?access_token=%s&sinceDatetime=%s",
                baseUrl, accessToken, sinceDateTime);

        HashSet leadIdList = new HashSet();

        // Call Get Paging Token API
        JsonObject pagingTokenObj = JsonObject.readFrom(getData(pagingTokenUrl));
        if (pagingTokenObj.get("success").asBoolean()) {

            String nextPageToken = pagingTokenObj.get("nextPageToken").asString();
            boolean moreResult;

            do {
                moreResult = false;

                // Call Get Lead Changes API
                JsonObject leadChangesObj = JsonObject.readFrom(getData(String.format("%s&nextPageToken=%s",
                        leadChangesUrl, nextPageToken)));
                if (leadChangesObj.get("success").asBoolean()) {
                    moreResult = leadChangesObj.get("moreResult").asBoolean();
                    nextPageToken = leadChangesObj.get("nextPageToken").asString();

                    if (leadChangesObj.get("result") != null) {
                        JsonArray resultAry = leadChangesObj.get("result").asArray();
                        for (JsonValue resultObj : resultAry) {
                            int activityTypeId = resultObj.asObject().get("activityTypeId").asInt();


                            // Store lead ids for later use
                            boolean storeThisId = false;
                            if (activityTypeId == ACTIVITY_TYPE_ID_NEW_LEAD) {
                                storeThisId = true;
                            } else if (activityTypeId == ACTIVITY_TYPE_ID_CHANGE_DATA_VALE) {
                                // See if any of the changed fields are of interest to us
                                JsonArray fieldsAry = resultObj.asObject().get("fields").asArray();
                                for (JsonValue fieldsObj : fieldsAry) {
                                    String name = fieldsObj.asObject().get("name").asString();
                                    if (LEAD_CHANGE_FIELD_FILTER.contains(name)) {
                                        storeThisId = true;
                                    }
                                }

                            }

                            if (storeThisId) {
                                leadIdList.add(resultObj.asObject().get("leadId").toString());
                            }
                        }
                    }
                }

            } while (moreResult);
        }

        JsonObject result = new JsonObject();
        JsonArray leads = new JsonArray();

        for (Object o : leadIdList) {
            String leadId = o.toString();

            // Compose Get Lead by Id URL
            String getLeadUrl = String.format("%s/rest/v1/lead/%s.json?access_token=%s",
                    baseUrl, leadId, accessToken);

            // Call Get Lead by Id API
            JsonObject leadObj = JsonObject.readFrom(getData(getLeadUrl));
            if (leadObj.get("success").asBoolean()) {
                if (leadObj.get("result") != null) {
                    JsonArray resultAry = leadObj.get("result").asArray();
                    for (JsonValue resultObj : resultAry) {

                        // Create lead object
                        JsonObject lead = new JsonObject();
                        lead.add("leadId", leadId);
                        lead.add("updatedAt", resultObj.asObject().get("updatedAt").asString());
                        lead.add("firstName", resultObj.asObject().get("firstName").asString());
                        lead.add("lastName", resultObj.asObject().get("lastName").asString());
                        lead.add("email", resultObj.asObject().get("email").asString());

                        // Add lead object to leads array
                        leads.add(lead);
                    }
                }
            }
        }

        // Add leads array to result object
        result.add("result", leads);

        // Print out result object
        System.out.println(result);

        System.exit(0);
    }

    // Perform HTTP GET request
    private static String getData(String endpoint) {
        String data = "";
        try {
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("GET");
            urlConn.setAllowUserInteraction(false);
            urlConn.setDoOutput(true);
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    private static String convertStreamToString(InputStream inputStream) {
        try {
            return new Scanner(inputStream).useDelimiter("A").next();
        } catch (NoSuchElementException e) {
            return "";
        }
    }
}
```

だから、あなたはそれを持っています [ 人生は幸せな歌です ](https://www.youtube.com/watch?v=zFaBwZDywLk)。 これで、お試しいただくことができます。

Posted on _2015-07-31_ by _David_

## 2015 年 5 月リリースの更新

### REST API

* 商談 API。 新しい [opportunity endpoints](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities) が導入され、Marketo商談オブジェクト内にあるデータをプログラムでリスト、記述、CRUD できるようになりました。

注：役割の権限が追加され、Opportunity のエンドポイント（読み取り専用 Opportunity、読み取り/書き込み Opportunity）へのアクセス権が付与されました。 API ユーザーの役割が Opportunity API のリリースより前の場合は、これらの権限を持つ新しい API ユーザーの役割を作成して、アクセスを有効にする必要があります。 そうしないと、「Access Denied （アクセスが拒否されました）」という 603 エラー応答が返されます。

* Asset API - スニペット。 新しい [ スニペットのアセットエンドポイント ](https://developer.adobe.com/marketo-apis/api/asset/#snippet_endpoints) が導入され、スニペットオブジェクトをプログラムで操作できるようになりました。 スニペットは、メールおよびランディングページで動的コンテンツブロックとして使用することができます。
* Leads API - Leads パーティションを更新します。 新しい [ パーティションのリードエンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/updatePartitionsUsingPOST) が追加され、1 つ以上のリードのパーティションを更新できるようになりました。
* リード関連の API で、「createdAt」属性と「updatedAt」属性にタイムゾーンオフセットが欠落していた問題を修正しました。
* 1 日あたりの最大呼び出し数を超えると、スケジュールキャンペーンが適切なエラーコードを返さない問題を修正しました。
* ID によるフォルダーの取得が「parent」属性と「description」属性に対して null を返す場合がある問題を修正しました。
* ID でメールを承認すると、特定の場合にシステムエラーが発生する問題を修正しました。
* フォルダー ID でトークンを作成すると、特定のケースで使用できないトークンが生成される問題を修正しました。

### リアルタイムPersonalization（RTP）

* リッチメディアレコメンデーション API。 RTP JavaScript API に新しい [ リッチメディアレコメンデーション ](/help/javascript-api/web-personalization.md) 機能が追加されました。 リッチメディアコンテンツのレコメンデーションでは、機械学習と予測分析を活用して、最も関連性の高いコンテンツを web 訪問者に提供します。 テキストの説明や画像を使用してコンテンツアセットを強化し、web サイトに複数のコンテンツレコメンデーションを埋め込みます。

### Mobile Engagement SDK

iOS v0.3.4/Android v0.3.3

* カスタムアクション。 カスタムアクションを送信してユーザーインタラクションを追跡する機能を追加しました。 詳しくは、「カスタムアクションの送信 [ を参照してください ](/help/mobile/mobile.md)。
* trackPushNotification メソッドは非推奨（廃止予定）になりました。

Posted on _2015-05-26_ by _David_

## 2015 年 6 月リリースアップデート

### REST API

* 会社 API

新しい [ 会社エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies) が導入され、Marketoの会社オブジェクト内にあるデータをプログラムでリスト、記述、CRUD できるようになりました。

注：プログラム エンドポイントへのアクセスを提供するために、次の役割の権限が追加されました：読み取り専用会社、読み取り/書き込み可能会社。 API ユーザーの役割が会社の API のリリースより前の日付になっている場合、アクセスを有効にするにはこれらの権限で API ユーザーの役割を更新する必要があります。 そうしないと、「Access Denied （アクセスが拒否されました）」という 603 エラー応答が返されます

* Asset API - プログラム

Asset API が更新されて、アプリケーションフォルダーとプログラムフォルダーの両方がサポートされるようになりました。 複数の Asset API が、整数の形式でリクエストのフォルダー ID を受け入れていました。 フォルダー ID は、API に応じて、URI の一部として渡すことも、リクエスト本文の一部として渡すこともできます。

次に、フォルダー id とフォルダータイプを指定する必要があります。 フォルダータイプは「プログラム」または「フォルダー」です。 「フォルダー」はアプリケーションフォルダーを指定し、「プログラム」はプログラムフォルダーを指定します。 フォルダータイプの指定には、呼び出す API に応じて 2 つの方法があります。

1. 「FolderIdType」データ構造を使用します。 FolderIdType は、次のように ID とタイプのペアを含む単純な JSON ブロックです。

`{ "id" : **id**, "type" : "**type**" }`

ここで、**id** はフォルダー id で、「**type**」はフォルダータイプです。 「**type**」の許容値は、「Folder」または「Program」です。

例 – フォルダーの作成

`POST /asset/v1/folders.json`

`parent={"id":416,"type":"Folder"}&name=Test Folder&description=This is a test folder`

1. 既存の id パラメーターを使用し、「type」クエリパラメーターを使用してそのタイプを指定します。

例 – Id によるフォルダーの取得

`GET /rest/asset/v1/folder/1016.json?type=Program`

結果オブジェクトにフォルダー ID を含んでいたすべての API 応答に、値が FolderIdType の folderId 属性も含まれるようになりました。 特定のフォルダー ID のフォルダータイプを決定するために使用できます。

例 – 名前によるフォルダーの取得

`GET /rest/asset/v1/folder/byName.json?name=Social Media`

```json
"result": [
{
...

"folderId": {"id":341, "type": "Program"},
...

"id":"341"
}
]
```

特定の ID のフォルダータイプを判断するには、[Browse Folders](https://developer.adobe.com/marketo-apis/api/asset/browse-folders/) API を使用します。

API 応答の「type」属性の名前が「folderType」に変更されました。 これは、FolderIdType に含まれる「type」要素との混乱を避けるためです。

例えば、次の場合：

&quot;**type**&quot;:&quot;マーケティングフォルダー&quot;

を次のように変更します。

「**folderType**」:「マーケティングフォルダー」

### Mobile Engagement SDK

iOS 0.3.5

* テストデバイスを設定ダイアログがメインスレッドで動作していた問題を修正しました。 [MOB-638]
* テストデバイスの登録に失敗した場合のエラー処理を追加しました。 [MOB-639]

Android 0.3.3

* テストデバイスを追加し、向きを変更した際に、進行状況ダイアログが閉じないように、android:configChanges 属性を AndroidManifest.xml `<activity>` 要素に追加しました。 [MOB-687]

Posted on _2015-06-30_ by _David_

## RTP API を使用したアプリ内 Web Personalization（Beta）

アドビのお客様の一部はユーザーに web アプリソリューションを提供しており、セキュリティで保護された web アプリ環境内でMarketo リアルタイム Personalization（RTP）を使用できる場合は、リクエストを受け取ります。 答えは「はい」です。 アプリ内メッセージの API がリリースされました。これにより、コンテンツをパーソナライズし、ウェビナー、新機能リリース、アップセルなどのマーケティングアクティビティを促進し、web アプリデータに基づいてユーザーを引き付けることができます。 例えば、次のアプリ内コンテンツのパーソナライズなどです。

* ユーザーアクティビティに基づく体験版オファー
* 様々なサブスクリプションタイプ（アップセル、クロスセル、ウェビナートレーニング）
* ユーザーアクティビティに関連する新機能

**使用例** Marketoのカスタマーサクセスチームは、アプリ内 Web Personalizationを使用して、パーソナライズされたコンテンツで特定のサブスクリプションタイプ（Spark、Standard、Select、または Enterprise）と通信し、プログレッシブキャンペーンを表示し、エンゲージメントに基づいてアプリ内ユーザーを育成していることを確認します。 Enterprise サブスクリプションタイプを持つユーザーに対してこれを行う方法を見てみましょう。 **前提条件** [RTP User Context API](/help/javascript-api/web-personalization.md) について説明します。 **User Context API を有効にする** Marketo サポートからのリクエストで、RTP アカウントの User Context API を有効にします。 **カスタム変数の設定** RTP には、データの送信先となる 5 つのカスタム変数スロットがあります。 この例では、ユーザー購読タイプ Enterprise をカスタム変数 1 に送信します。

`rtp('set', 'customVar1', 'Enterprise');`

**新規 RTP セグメントの作成** **セグメント** に移動し、「**新規作成**」をクリックします。

1. **User Context API** フィルターをセグメントビルダーにドラッグします。
1. **value** が **Enterprise** である **カスタム変数 1** （購読タイプ）を選択します。

**以前の訪問履歴に基づいてキャンペーンを表示** 以前の訪問で既にキャンペーンをクリックしている場合に別のキャンペーンを訪問者に表示します。

1. **User Context API** 内で **（+）をクリックして** 別の User Context API 属性を追加します
1. **演算子（AND または OR）を追加します。**
1. **キャンペーン – クリック済み」を選択します。** キャンペーン ID **をキャンペーンの ID に** 定します。 （キャンペーン ID を見つける方法については、以下のメモを参照してください）。
1. **キャンペーンを保存して定義** をクリックして、キャンペーンクリエイティブを作成します。

全体的に、訪問者がエンタープライズと等しいカスタム変数（サブスクリプションタイプ）に関連付けられている場合や、訪問者が以前の訪問でキャンペーン（ID:5390）をクリックした場合には、このセグメントは一致します。 次の手順では、このセグメント用にパーソナライズされたキャンペーンを定義します。 次のスクリーンショットは、My Marketo ページに表示される RTP ダイアログキャンペーン（左下）で、大規模法人ユーザー向けのウェビナーのプロモーションを行っています。  **注意：**&#x200B;**キャンペーン ID の検索**&#x200B;**キャンペーン** に移動し、**キャンペーン名** にカーソルを合わせてキャンペーン ID を検索します。
Posted on _2015-06-17_ by _David_

## Marketo REST API を使用したトランザクションメールの送信：パート 1

Marketo REST API を使用して必要な呼び出しを実行するには、Marketo にいくつかの設定要件があります。

* .受信者は、Marketo 内にレコードを持っている必要があります。
* Marketo インスタンスでトランザクションメールを作成し、承認する必要があります。
* メールを送信するように設定された、キャンペーンがリクエストされた、Source:web サービス API を含むアクティブなトリガーキャンペーンが必要です

最初に[メールを作成して承認します](https://experienceleague.adobe.com/ja/docs/marketo/using/home)。メールが真にトランザクション型である場合は、運用可能に設定する必要が生じる可能性がありますが、法的には運用可能と認定されていることを確認してください。 これは、メールのアクション / メール設定の下の編集画面を使用して設定します。 承認すると、キャンペーンを作成する準備が整います。 キャンペーンの作成を初めて行う場合は、docs.marketo.comにある [ 新しいスマートキャンペーンの作成 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/creating-a-smart-campaign/create-a-new-smart-campaign) 記事を参照してください。 キャンペーンを作成したら、これらの手順を実行する必要があります。 キャンペーンがリクエストされたトリガーでスマートリストを設定する：次に、メールを送信手順をメールに指定するようにフローを設定する必要があります。 アクティベーションの前に、「スケジュール」タブで一部の設定を決定する必要があります。 この特定のメールを特定のレコードに 1 回だけ送信する場合は、選定の設定はそのままにしておきます。ただし、メールを複数回受信する必要がある場合は、毎回または使用可能な頻度のいずれかに調整する必要があります。 これで、アクティブ化する準備が整いました。

### API 呼び出しの送信

**注意：** 以下の Java の例では、最小限の json パッケージを使用して、コード内で JSON 表現を処理しています。 このプロジェクトについて詳しくは、[https://github.com/ralfstx/minimal-jsonを参照してください ](https://github.com/ralfstx/minimal-json)API を介してトランザクションメールを送信する最初の部分は、対応するメールアドレスを持つレコードがMarketo インスタンスに存在し、リード ID にアクセスできることを確認することです。 この投稿の目的上、メールアドレスは既にMarketoにあり、レコードの ID を取得するだけで済むと仮定します。 この場合、[ フィルタータイプで複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) 呼び出しを使用し、前の投稿の Java コードの一部を再利用します。 キャンペーンをリクエストするための、の主なメソッドを見てみましょう。

```java
package dev.marketo.blog_request_campaign;

import com.eclipsesource.json.JsonArray;

public class App
{
    public static void main( String[] args )
    {
     //Create an instance of Auth so that we can authenticate with our Marketo instance
        Leads leadsRequest = new Leads(auth).setFilterType("email").addFilterValue("<requestCampaign.test@marketo.com>");

        //Create and parameterize an instance of Leads
        //Set your email filterValue appropriately
        Leads leadsRequest = new Leads(auth).setFilterType("email").addFilterValue("test.requestCamapign@example.com");

        //Get the inner results array of the response
        JsonArray leadsResult = leadsRequest.getData().get("result").asArray();

        //Get the id of the record indexed at 0
        int lead = leadsResult.get(0).asObject().get("id").asInt();

        //Set the ID of your campaign from Marketo
        int campaignId = 0;
        RequestCampaign rc = new RequestCampaign(auth, campaignId).addLead(lead);

        //Send the request to Marketo
        rc.postData();
    }
}
```

leadsRequest の JsonObject 応答からこれらの結果を取得するには、コードを記述する必要があります。 配列の最初の結果を取得するには、JsonObject から配列を抽出し、0 でインデックス付けされたオブジェクトを取得する必要があります。

`JsonArray leadsResult = leadsRequest.getData().get("result").asArray();`
`int leadId = leadsResult.get(0).asObject().get("id").asInt();`

今後は、キャンペーンをリクエスト呼び出しのみを行う必要があります。 これには、リクエストの URL 内の ID と、1つのメンバー &quot;id&quot; を含む JSON オブジェクトの配列が必要です。このコードを見てみましょう。

```java
package dev.marketo.blog_request_campaign;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import javax.net.ssl.HttpsURLConnection;
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

public class RequestCampaign {
 private String endpoint;
 private Auth auth;
 public ArrayList leads = new ArrayList();
 public ArrayList tokens = new ArrayList();

 public RequestCampaign(Auth auth, int campaignId) {
  this.auth = auth;
  this.endpoint = this.auth.marketoInstance + "/rest/v1/campaigns/" + campaignId + "/trigger.json";
 }
 public RequestCampaign setLeads(ArrayList leads) {
  this.leads = leads;
  return this;
 }
 public RequestCampaign addLead(int lead){
  leads.add(lead);
  return this;
 }
 public RequestCampaign setTokens(ArrayList tokens) {
  this.tokens = tokens;
  return this;
 }
 public RequestCampaign addToken(String tokenKey, String val){
  JsonObject jo = new JsonObject().add("name", tokenKey);
  jo.add("value", val);
  tokens.add(jo);
  return this;
 }
 public JsonObject postData(){
  JsonObject result = null;
  try {
   JsonObject requestBody = buildRequest(); //builds the Json Request Body
   String s = endpoint + "?access_token=" + auth.getToken(); //takes the endpoint URL and appends the access_token parameter to authenticate
   System.out.println("Executing RequestCampaign calln" + "Endpoint: " + s + "nRequest Body:n"  + requestBody);
   URL url = new URL(s);
   HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection(); //Return a URL connection and cast to HttpsURLConnection
   urlConn.setRequestMethod("POST");
   urlConn.setRequestProperty("Content-type", "application/json");
            urlConn.setRequestProperty("accept", "text/json");
            urlConn.setDoOutput(true);
   OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
   wr.write(requestBody.toString());
   wr.flush();
   InputStream inStream = urlConn.getInputStream(); //get the inputStream from the URL connection
   Reader reader = new InputStreamReader(inStream);
   result = JsonObject.readFrom(reader); //Read from the stream into a JsonObject
   System.out.println("Result:n" + result);
  } catch (MalformedURLException e) {
   e.printStackTrace();
  } catch (IOException e) {
   e.printStackTrace();
  }
  return result;
 }

 private JsonObject buildRequest(){
  JsonObject requestBody = new JsonObject(); //Create a new JsonObject for the Request Body
  JsonObject input = new JsonObject();
  JsonArray leadsArray = new JsonArray();
  for (int lead : leads) {
   JsonObject jo = new JsonObject().add("id", lead);
   leadsArray.add(jo);
  }
  input.add("leads", leadsArray);
  JsonArray tokensArray = new JsonArray();
  for (JsonObject jo : tokens) {
   tokensArray.add(jo);
  }
  input.add("tokens", tokensArray);
  requestBody.add("input", input);
  return requestBody;
 }

}
```

このクラスには、Auth とキャンペーンの ID を受け取る 1 つのコンストラクターがあります。リードをオブジェクトに追加するには、setLeads にレコードの ID を含む ArrayList `<Integer>` を渡すか、addLead を使用します。この場合、1 つの整数を使用して、leads プロパティ内の既存の ArrayList に追加します。 リードレコードをキャンペーンに渡すための API 呼び出しをトリガーするには、postData を呼び出す必要があります。このメソッドは、リクエストからのレスポンスデータを含んだ JsonObject を返します。 リクエストキャンペーンが呼び出されると、その呼び出しに渡されるすべてのリードがMarketoのターゲットトリガーキャンペーンで処理され、以前に作成されたメールが送信されます。 これで、Marketo REST API を使用してメールをトリガーしました。リクエストキャンペーンを通じてメールのコンテンツを動的にカスタマイズする方法については、パート 2 で説明しています。

Posted on _2015-07-17_ by _Kenny_

## REST API を使用したMarketoからのリードデータの認証と取得

**注意：** 以下の Java の例では、最小限の json パッケージを使用して、コード内で JSON 表現を処理しています。 このプロジェクトについて詳しくは、こちらを参照してください。[https://github.com/ralfstx/minimal-json](https://github.com/ralfstx/minimal-json)Marketoと統合する際の最も一般的な要件の 1 つは、リードデータの取得です。 ほとんどの場合、すべての統合でMarketo サブスクリプションからのリードデータの取得または送信が必要になるとは限りません。そのため、本日は、サブスクリプションで [ 認証 ](/help/rest-api/authentication.md) してから、リードデータを取得するという、基本的なリード情報の取得タスクについて説明します。 リードを取得するには、まず、OAuth 2.0 を使用してターゲット Marketo インスタンスを認証する必要があります。Marketoでの認証に必要な情報には、クライアント ID、クライアントシークレット、Marketo インスタンスのホストの 3 つがあります。 認証に使用するクラスは次のとおりです。

```java
package dev.marketo.blog_leads;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import javax.net.ssl.HttpsURLConnection;
import com.eclipsesource.json.JsonObject;

public class Auth {
 protected String marketoInstance; //Instance Host obtained from Admin -> Web Service
 private String clientId; //clientId obtained from Admin -> Launchpoint -> View Details for selected service
 private String clientSecret; //clientSecret obtained from Admin -> Launchpoint -> View Details for selected service
 private String idEndpoint; //idEndpoint constructed to authenticate with service when constructor is used
 private String token; //token is stored for reuse until expiration
 private Long expiry; //used to store time of expiration

 //Creates an instance of Auth which is used to Authenticate with a particular service on a particular instance
 public Auth(String id, String secret, String instanceUrl) {
  this.clientId = id;
  this.clientSecret = secret;
  this.marketoInstance = instanceUrl;
  this.idEndpoint = marketoInstance + "/identity/oauth/token?grant_type=client_credentials&client_id=" + clientId + "&client_secret=" + clientSecret;
 }
 //The only public method of Auth, used to check if the current value of Token is valid, and then to retrieve a new one if it is not
 public String getToken(){
  long now  = System.currentTimeMillis();
  if (expiry == null || expiry < now){
   System.out.println("Token is empty or expired. Trying new authentication");
   JsonObject jo = getData();
   System.out.println("Got Authentication Response: " + jo);
   this.token = jo.get("access_token").asString();
                        //expires_in is reported as seconds, set expiry to system time in ms + expires \* 1000
   this.expiry = System.currentTimeMillis() + (jo.get("expires_in").asLong() \* 1000);
  }
  return this.token;
 }
 //Executes the authentication request
 private JsonObject getData(){
  JsonObject jsonObject = null;
  try {
   URL url = new URL(idEndpoint);
   HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
   urlConn.setRequestMethod("GET");
            urlConn.setRequestProperty("accept", "application/json");
            System.out.println("Trying to authenticate with " + idEndpoint);
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                InputStream inStream = urlConn.getInputStream();
                Reader reader = new InputStreamReader(inStream);
                jsonObject = JsonObject.readFrom(reader);
            }else {
                throw new IOException("Status: " + responseCode);
            }
  } catch (MalformedURLException e) {
   e.printStackTrace();
  }catch (IOException e) {
            e.printStackTrace();
        }
  return jsonObject;
 }
}
```

このコードを使用すると、管理者/ローンチポイント（ID と秘密鍵）、管理者/web サービス（ホスト）から、クライアント ID、クライアントシークレットおよびホスト（marketoInstance）を使用して認証のインスタンスを作成できます。 getToken メソッドを公開します。このメソッドは、現在格納されているトークンが null または期限切れかどうかをテストして、既存のトークンを返すか、新しい認証リクエストを行って JSON 応答の「access_token」メンバーから新しいトークンを返します。 これでMarketo インスタンスを使用して認証を行うことができるので、次の手順はリードを取得することです。 ここでは、次のクラスを使用します。

```java
package dev.marketo.blog_leads;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import javax.net.ssl.HttpsURLConnection;
import com.eclipsesource.json.JsonObject;

public class Leads {
 private StringBuilder endpoint;
 private Auth auth;
 public String filterType;
 public ArrayList filterValues = new ArrayList();
 public Integer batchSize;
 public String nextPageToken;
 public ArrayList fields = new ArrayList();

 public Leads(Auth a) {
  this.auth = a;
  this.endpoint = new StringBuilder(this.auth.marketoInstance + "/rest/v1/leads.json");
 }
 public Leads setFilterType(String filterType) {
  this.filterType = filterType;
  return this;
 }
 public Leads setFilterValues(ArrayList filterValues) {
  this.filterValues = filterValues;
  return this;
 }
 public Leads addFilterValue(String filterVal) {
  this.filterValues.add(filterVal);
  return this;
 }
 public Leads setBatchSize(Integer batchSize) {
  this.batchSize = batchSize;
  return this;
 }
 public Leads setNextPageToken(String nextPageToken) {
  this.nextPageToken = nextPageToken;
  return this;
 }
 public Leads setFields(ArrayList fields) {
  this.fields = fields;
  return this;
 }

 public JsonObject getData() {
        JsonObject result = null;
        try {
         endpoint.append("?access_token=" + auth.getToken() + "&filterType=" + filterType + "&filterValues=" + csvString(filterValues));
         if (batchSize != null && batchSize > 0 && batchSize <= 300){
             endpoint.append("&batchSize=" + batchSize);
            }
            if (nextPageToken != null){
             endpoint.append("&nextPageToken=" + nextPageToken);
            }
            if (fields != null){
             endpoint.append("&fields=" + csvString(fields));
            }
            URL url = new URL(endpoint.toString());
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("GET");
            urlConn.setRequestProperty("accept", "text/json");
            InputStream inStream = urlConn.getInputStream();
            Reader reader = new InputStreamReader(inStream);
            result = JsonObject.readFrom(reader);
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return result;
    }
 private String csvString(ArrayList fields) {
  StringBuilder fieldCsv = new StringBuilder();
     for (int i = 0; i < fields.size(); i++){
      fieldCsv.append(fields.get(i));
      if (i + 1 != fields.size()){
       fieldCsv.append(",");
      }
     }
  return fieldCsv.toString();
 }
}
```

このクラスは、Auth オブジェクトを受け入れる単一のコンストラクタを持ち、その後、オプションおよび必須パラメーターの両方に対して複数のセッターを公開します。 この場合、実際に必要なのは、filterType と filterValues を設定して、メールアドレスでリードを取得を実行することだけです。 そのため、「メール」には setFilterType を使用し、ID の取得が必要なメールアドレスには addFilterValue を使用します。 パラメーターを設定したら、getData メソッドを使用してリードエンドポイントから JsonObject を取得できます。この中には、取得されたリードレコードの JSON 表現を持つ結果の配列が含まれています。

### まとめ

使用しているサンプルコードを確認したので、簡単な例を見て、テストメールアドレス <testlead@marketo.com> に一致するリードを取得します。 この場合、「email」には setFilterType を使用し、情報を取得する必要があるメールアドレスには addFilterValue を使用する必要があります。 パラメーターを設定したら、getData メソッドを使用してリードエンドポイントから JsonObject を取得できます。この中には、取得されたリードレコードの JSON 表現を持つ結果の配列が含まれています。

```java
package dev.marketo.blog_leads;

import com.eclipsesource.json.JsonObject;

public class App
{
    public static void main( String[] args )
    {
     //Create an instance of Auth so that we can authenticate with our Marketo instance
        //Change the credentials here to your own
        Auth auth = new Auth("CHANGE ME", "CHANGE ME", "CHANGE ME");
        //Create and parameterize an instance of Leads
        Leads getLeads = new Leads(auth)
              .setFilterType("email")
              .addFilterValue("<testlead@marketo.com>");
        //get the inner results array of the response
        JsonObject leadsResult = getLeads.getData();
        System.out.println(leadsResult);
    }
}
```

この主なメソッドの例では、Auth のインスタンスを作成し、これを新しい Leads コンストラクターに渡します。 setFilterType と addFilterValue を使用して、メールアドレス「<testlead@marketo.com>」に一致するリードのみを取得するようにリードのインスタンスを設定します。 次の例では、これをコンソールに出力します。

トークンが空か、期限切れです。 新しい認証を試しています
<https://299-BYM-827.mktorest.com/identity/oauth/token?grant_type=client_credentials&client_id=b417d98f-9289-47d1-a61f-db141bf0267f&client_secret=0DipOvz4h2wP1ANeVjlfwMvECJpo0ZYc> で認証しようとしています
認証応答を取得：{&quot;access_token&quot;:&quot;ec0f02c0-28ac-4d6c-b7d7-00e47ae85ff1:st&quot;,&quot;token_type&quot;:&quot;bearer&quot;,&quot;expires_in&quot;:538,&quot;scope&quot;:&quot;<apiuser@mktosupport.com>&quot;}
{&quot;requestId&quot;:&quot;14fb6#14e6a7a9ad6&quot;,&quot;result&quot;:[{&quot;id&quot;:1026322,&quot;updatedAt&quot;:&quot;2015-07-07T21:43:25Z&quot;,&quot;lastName&quot;:&quot;Lead&quot;,&quot;email&quot;:&quot;<testlead@marketo.com>&quot;,&quot;createdAt&quot;:&quot;2015-07-07T21:43:25Z&quot;,&quot;firstName&quot;:&quot;Name test&quot;},{&quot;id&quot;:1026323,&quot;updatedAt&quot;:&quot;2015-07-07T21:43:43Z&quot;,&quot;lastName&quot;:&quot;Lead2&quot;,&quot;email&quot;:&quot;<testlead@marketo.com>&quot;,&quot;createdAt&quot;:&quot;2015-07-07T21:43:43Z&quot;,&quot;firstName&quot;:&quot;Test&quot;}],&quot;success&quot;:true}

今、私たちは私たちが必要とするすべての方法で処理できるリードデータを持っています。 読んでいただきありがとうございます、とあなたがコメントに持っている任意のフィードバックを残してください。

Posted on _2015-07-10_ by _Kenny_

## 2015 年 7 月リリースアップデート

REST API

* 販売担当者 API

新しい [ 営業担当者エンドポイント ](/help/rest-api/sales-persons.md) が導入され、Marketoの営業担当者オブジェクト内にあるデータをプログラムでリスト、記述、CRUD できるようになりました。 さらに、販売担当者をリード、オポチュニティまたは会社に割り当てることができます。 これを行うには、リード、オポチュニティまたは会社の作成/更新/アップサート エンドポイントを呼び出す際に、「externalSalesPersonId」属性を指定します。

注：プログラム エンドポイントへのアクセスを提供するために、Role 権限が追加されました。Read-Only Sales Person、Read-Write Sales Person。 API ユーザーの役割が販売担当者 API のリリースより前の日付になっている場合は、これらの権限で API ユーザーの役割を更新してアクセスを有効にする必要があります。 そうしないと、「Access Denied （アクセスが拒否されました）」という 603 エラー応答が返されます。

* Asset API - ランディングページテンプレート

新しい [ ランディングページテンプレートエンドポイント ](https://developer.adobe.com/marketo-apis/api/asset/#landing_page_templates_endpoints) が導入され、ランディングページテンプレートに関連付けられたデータをプログラムによってリスト化、作成および更新できるようになりました。

* Asset API - セグメント

セグメント関連のエンドポイントが 2 つ導入されました。

[ セグメントを取得 ](https://developer.adobe.com/marketo-apis/api/asset/get-segments)

[Id によるセグメント化の取得 ](https://developer.adobe.com/marketo-apis/api/asset/get-segmentation-by-id)

* 「名前によるフォルダーの取得」で「workSpace」パラメーターが尊重されない問題を修正しました。 [LM-61059]
* カスタムオブジェクト API のパフォーマンスをいくつか改善しました。

Posted on _2015-07-17_ by _David_

## リード、会社およびオポチュニティを作成して、Marketo REST API に関連付けます。

Marketoの分析を最大限に活用するには、リード、会社、商談のレコード間に正しく堅牢な関連付けを構築することが重要です。 ネイティブの CRM 同期を利用していない場合、これらの関係を構築すると問題が発生する可能性があるので、今日は構築の手順を進めます。

### オブジェクトの関係

Marketoには、商談レポートを完全に確立するために重要な関係がいくつかあります。

* リードと商談は、OpportunityRole オブジェクトと多くの関係があります。
* OpportunityRole には leadId フィールドと externalopportunityid フィールドの両方があり、リードからオポチュニティへの関係を作成します。
* 「商談を持つ」スマートリストフィルターの資格を得るには、リードに商談に関連する OpportunityRole が必要です。
* オポチュニティは、externalCompanyId フィールドを介して会社オブジェクトと多対 1 の関係を持ちます。
* リードは、externalCompanyId フィールドを介して会社と 1 対多の関係を持ちます。
* 商談は、リードの獲得プログラム、またはプログラムのメンバーシップと成功に基づいて、プログラムに関連付けられます（[ アトリビューションについて ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/reporting/revenue-cycle-analytics/revenue-tools/attribution/understanding-attribution) を参照）。

リードデータベース全体でこれらの関係を構築すると、Marketo Analytics を最大限に活用し、プログラムがオポチュニティの創出と獲得率に与える影響を確認できます。

### 会社

これらの関係を構築する最も簡単な方法は、会社の作成から始めることです。 これにより、オポチュニティを作成した後にオポチュニティを更新するために追加の API 呼び出しを実行する代わりに、作成時に externalCompanyId をオポチュニティに渡すことができます。 既存の設定によっては、これが必要な手順である場合とない場合がありますが、関連会社との関係を構築するには、新しいリードや連絡先をMarketo インスタンスに追加する必要があります。そのため、会社レコードを作成するためのいくつかのコードを見てみましょう。

```java
package dev.marketo.opportunities;

import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import javax.net.ssl.HttpsURLConnection;

import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

public class UpsertCompanies {
 public List<JsonObject> input; //a list of Companies to use for input.  Each must have a member "externalCompanyId".
 public String action; //specify the action to be undertaken, createOnly, updateOnly, createOrUpdate
 public String dedupeBy; //select mode of Deduplication, dedupeFields for all dedupe parameters(externalCompanyId), idField for marketoId
 private String endpoint; //endpoint URL created with Constructor
 private Auth auth; //Marketo Auth Object


 //Constructs an UpsertOpportunities with Auth, but with no input set
 public UpsertCompanies(Auth auth){
  this.auth = auth;
  this.endpoint = this.auth.marketoInstance + "/rest/v1/companies.json";
 }
 //Constructs and UpsertOpportunities with Auth and input set
 public UpsertCompanies(Auth auth, List<JsonObject> input) {
  this(auth);
  this.input = input;
 }
 //adds input to existing list, creates arraylist if it was built without a list
 public UpsertCompanies addCompanies(JsonObject... companies){
  if (this.input == null){
   this.input = new ArrayList();
  }
  for (JsonObject jo : companies) {
   System.out.println(jo);
   this.input.add(jo);
  }
  return this;
 }

 public JsonObject postData(){
  JsonObject result = null;
  try {
   JsonObject requestBody = buildRequest(); //builds the Json Request Body
   String s = endpoint + "?access_token=" + auth.getToken(); //takes the endpoint URL and appends the access_token parameter to authenticate
   URL url = new URL(s);
   HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection(); //Return a URL connection and cast to HttpsURLConnection
   urlConn.setRequestMethod("POST");
   urlConn.setRequestProperty("Content-type", "application/json");
            urlConn.setRequestProperty("accept", "text/json");
            urlConn.setDoOutput(true);
   OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
   wr.write(requestBody.toString());
   wr.flush();
   InputStream inStream = urlConn.getInputStream(); //get the inputStream from the URL connection
   Reader reader = new InputStreamReader(inStream);
   result = JsonObject.readFrom(reader); //Read from the stream into a JsonObject
   urlConn.disconnect();
  } catch (MalformedURLException e) {
   e.printStackTrace();
  } catch (IOException e) {
   e.printStackTrace();
  }
  return result;
 }

 private JsonObject buildRequest(){
  JsonObject requestBody = new JsonObject(); //Create a new JsonObject for the Request Body
  JsonArray in = new JsonArray(); //Create a JsonArray for the "input" member to hold Opp records
  for (JsonObject jo : input) {
   in.add(jo); //add our company records to the input array
  }
  requestBody.add("input", in);
  if (this.action != null){
   requestBody.add("action", action); //add the action member if available
  }
  if (this.dedupeBy != null){
   requestBody.add("dedupeBy", dedupeBy); //add the dedupeBy member if available
  }
  return requestBody;
 }
 //Getters and Setters
 //Setters return the UpsertCompanies instance to allow simple formatting:
 public List<JsonObject> getInput() {
  return input;
 }
 //sets or replaces existing input with list
 public UpsertCompanies setInput(List input) {
  this.input = input;
  return this;
 }
 public String getAction() {
  return action;
 }
 public UpsertCompanies setAction(String action) {
  this.action = action;
  return this;
 }
 public String getDedupeBy() {
  return dedupeBy;
 }
 public UpsertCompanies setDedupeBy(String dedupeBy) {
  this.dedupeBy = dedupeBy;
  return this;
 }

}
```

会社 API は 2 つの重複排除オプションを提供し、リクエストの dedupeBy パラメーターで「dedupeFields」と「idField」を設定します。 これらは、Describe Companies を呼び出すことで明示的に取得できます。 dedupeBy が未設定の場合は、デフォルトで dedupeFields になります。 会社レコードの場合、dedupeFields は常に、外部ソースによって設定された任意の文字列である「externalCompanyId」に対応し、idField は、作成後にMarketoによって生成されて返される整数である「marketoId」フィールドに対応します。 dedupeBy の選択に応じて、会社レコードのアップサート呼び出しには externalCompanyId または marketoId のいずれかを含める必要があります。 これらと同じ要件が、Opportunity と Opportunity Role のオブジェクト API に適用されます。 このコードは 2 つのコンストラクターを公開します。1 つは Auth オブジェクトの 1 つの引数を受け入れるコンストラクター、もう 1 つは Auth と [JsonObject](https://github.com/ralfstx/minimal-json) 会社レコードのリストを受け入れるコンストラクターです。 入力リストを指定せずに構築した場合は、会社レコードを addCompanies メソッドで追加する必要があります。このメソッドは、入力が null の場合に新しい ArrayList を作成し、入力リストにすべての JsonObject 引数を追加するかどうかをチェックします。 使用例を次に示します。

```java
//Create a new company to associate to
JsonObject myCompany = new JsonObject().add("externalCompanyId", "myCompany");
UpsertCompanies upsertCompanies = new UpsertCompanies(auth).addCompanies(myCompany);
JsonObject companiesResult = upsertCompanies.postData();
System.out.println(companiesResult);
```

フィールド `externalCompanyId` を 1 つだけ持つ単一の会社 JsonObject を作成したあと、UpsertCompanies のインスタンスを作成し、`addCompanies` を使用して入力リストに会社を追加します。

### 商談

会社オブジェクトと同様に、商談 API には `dedupeBy` パラメーターがあり、「dedupeFields」または「idField」を受け入れます。それぞれ「externalopportunityid」と「marketoGUID」に対応します。 次に示すのは、UpsertCompanies クラスに非常に似たコードです。

```java
package dev.marketo.opportunities;

import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import javax.net.ssl.HttpsURLConnection;

import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

public class UpsertOpportunities {
 public List<JsonObject> input; //a list of Opportunities to use for input.  Each must have a member "externalopportunityid".  Each can optionally include "externalCompanyId" for company association
 public String action; //specify the action to be undertaken, createOnly, updateOnly, createOrUpdate
 public String dedupeBy; //select mode of Deduplication, dedupeFields for all dedupe parameters, idField for marketoId
 private String endpoint; //endpoint URL created with Constructor
 private Auth auth; //Marketo Auth Object


 //Constructs an UpsertOpportunities with Auth, but with no input set
 public UpsertOpportunities(Auth auth){
  this.auth = auth;
  this.endpoint = this.auth.marketoInstance + "/rest/v1/opportunities.json";
 }
 //Constructs and UpsertOpportunities with Auth and input set
 public UpsertOpportunities(Auth auth, List<JsonObject> input) {
  this(auth);
  this.input = input;
 }
 public UpsertOpportunities addOpportunities(JsonObject... opp){
  if (this.input == null){
   this.input = new ArrayList();
  }
  for (JsonObject jo : opp) {
   System.out.println(jo);
   this.input.add(jo);
  }
  return this;
 }

 public JsonObject postData(){
  JsonObject result = null;
  try {
   JsonObject requestBody = buildRequest(); //builds the Json Request Body
   String s = endpoint + "?access_token=" + auth.getToken(); //takes the endpoint URL and appends the access_token parameter to authenticate
   URL url = new URL(s);
   HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection(); //Return a URL connection and cast to HttpsURLConnection
   urlConn.setRequestMethod("POST");
   urlConn.setRequestProperty("Content-type", "application/json");
            urlConn.setRequestProperty("accept", "text/json");
            urlConn.setDoOutput(true);
   OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
   wr.write(requestBody.toString());
   wr.flush();
   InputStream inStream = urlConn.getInputStream(); //get the inputStream from the URL connection
   Reader reader = new InputStreamReader(inStream);
   result = JsonObject.readFrom(reader); //Read from the stream into a JsonObject
   urlConn.disconnect();
  } catch (MalformedURLException e) {
   e.printStackTrace();
  } catch (IOException e) {
   e.printStackTrace();
  }
  return result;
 }

 private JsonObject buildRequest(){
  JsonObject requestBody = new JsonObject(); //Create a new JsonObject for the Request Body
  JsonArray in = new JsonArray(); //Create a JsonArray for the "input" member to hold Opp records
  for (JsonObject jo : input) {
   in.add(jo); //add our Opportunity records to the input array
  }
  requestBody.add("input", in);
  if (this.action != null){
   requestBody.add("action", action); //add the action member if available
  }
  if (this.dedupeBy != null){
   requestBody.add("dedupeBy", dedupeBy); //add the dedupeBy member if available
  }
  return requestBody;
 }
 //Getters and Setters
 //Setters return the UpsertOpportunites instance to allow simple formatting:
 public List<JsonObject> getInput() {
  return input;
 }
 public UpsertOpportunities setInput(List<JsonObject> input) {
  this.input = input;
  return this;
 }
 public String getAction() {
  return action;
 }
 public UpsertOpportunities setAction(String action) {
  this.action = action;
  return this;
 }
 public String getDedupeBy() {
  return dedupeBy;
 }
 public UpsertOpportunities setDedupeBy(String dedupeBy) {
  this.dedupeBy = dedupeBy;
  return this;
 }

}
```

同じコンストラクターオプションが提供され、Auth または `Auth+List<JsonObject>` と、JsonObject のオポチュニティを入力する `addOpportunities` メソッドを取ります。 次に使用例を示します。

```java
//Create some JsonObjects for Opportunity Data
JsonObject opp1 = new JsonObject().add("name", "opportunity1")
    .add("externalopportunityid", "Opportunity1Test")
    .add("externalCompanyId", "myCompany")
    .add("externalCreatedDate", "2015-01-01T00:00:00z");
JsonObject opp2 = new JsonObject().add("name", "opportunity2")
    .add("externalopportunityid", "Opportunity2Test")
    .add("externalCompanyId", "myCompany")
    .add("externalCreatedDate", "2015-01-01T00:00:00z");

//Create an Instance of UpsertOpportunities and POST it
UpsertOpportunities upsertOpps = new UpsertOpportunities(auth)
                        .setAction("createOnly")
                        .addOpportunities(opp1, opp2);
JsonObject oppsResult = upsertOpps.postData();
System.out.println(oppsResult);
```

ここでは、2 つの機会の例を作成し、name、externalopportunityid、externalCompanyId、および externalCreatedDate フィールドに値を指定します。 まだ externalCreatedDate については説明していませんが、を利用することが重要です。オポチュニティが作成された際に RCE でマスターフィールドとして扱われるため、適切なアトリビューションにするために重要です。 組織のビジネスロジックを使用して、既存の商談データをバックフィルするのか、その場で新しい商談データを作成するのかに基づいて、このフィールドに入力する内容を決定できます。 UpsertOpportunity のインスタンスを作成し、addOpportunity を使用して JsonObjects を追加します。 インスタンスが設定されたので、postData でこれをMarketoにプッシュし、結果を印刷できます

### ロール

ロールは、dedupeBy を dedupeFields に設定する際の要件が多少異なる点を除き、前の 2 つのオブジェクトと非常によく似ています。 役割では、このメソッド「leadId」、「role」、「externalopportunityid」を使用してレコードを作成または更新する際に、3 つのフィールドを含める必要があります。 「role」には任意の文字列値を指定できますが、他の 2 つの値は、それぞれリードの有効な ID とオポチュニティの有効な ID を参照する必要があります。

```java
package dev.marketo.opportunities;

import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import javax.net.ssl.HttpsURLConnection;

import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

public class UpsertOpportunityRoles {
 public List<JsonObject> input; //Array of Opportunity Roles as JsonObjects, must have "leadId", "role" and "externalopprtunityid"
 public String action; //specify the action to be undertaken, createOnly, updateOnly, createOrUpdate, defaults to createOrUpdate if unset
 public String dedupeBy;//select mode of Deduplication, dedupeFields for all dedupe parameters, idField for marketoId
 private String endpoint; //endpoint URL created with Constructor
 private Auth auth; //Marketo Auth Object

 //Constructs an UpsertOpportunityRoles with Auth, but with no input set
 public UpsertOpportunityRoles(Auth auth) {
  this.auth = auth;
  this.endpoint = this.auth.marketoInstance + "/rest/v1/opportunities/roles.json";
 }
 //Constructs and UpsertOpportunities with Auth and input set
 public UpsertOpportunityRoles(Auth auth, List<JsonObject> input) {
  this(auth);
  this.input = input;
 }
 public UpsertOpportunityRoles addRoles(JsonObject... role){
  if (this.input == null){
   this.input = new ArrayList();
  }
  for (JsonObject jo : role) {
   System.out.println(jo);
   this.input.add(jo);
  }
  return this;
 }
 //executes the request to Marketo, body will be empty if input is not set
 public JsonObject postData(){
  JsonObject result = null;
  try {
   JsonObject requestBody = buildRequest(); //builds the Json Request Body
   String s = endpoint + "?access_token=" + auth.getToken(); //takes the endpoint URL and appends the access_token parameter to authenticate
   URL url = new URL(s);
   HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection(); //Return a URL connection and cast to HttpsURLConnection
   urlConn.setRequestMethod("POST");
   urlConn.setRequestProperty("Content-type", "application/json");//"application/json" content-type is required.
            urlConn.setRequestProperty("accept", "text/json");
            urlConn.setDoOutput(true);
   OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
   wr.write(requestBody.toString());
   wr.flush();
   InputStream inStream = urlConn.getInputStream();  //get the inputStream from the URL connection
   Reader reader = new InputStreamReader(inStream);
   result = JsonObject.readFrom(reader); //Read from the stream into a JsonObject
   urlConn.disconnect();
  } catch (MalformedURLException e) {
   e.printStackTrace();
  } catch (IOException e) {
   e.printStackTrace();
  }
  return result;
 }

 public JsonObject buildRequest(){
  JsonObject requestBody = new JsonObject();
  JsonArray in = new JsonArray();
  for (JsonObject jo : input) {
   in.add(jo);
  }
  requestBody.add("input", in);
  if (this.action != null){
   requestBody.add("action", action);
  }
  if (this.dedupeBy != null){
   requestBody.add("dedupeBy", dedupeBy);
  }
  return requestBody;
 }
 //Getters and Setters
 //Setters return the UpsertOpportunites instance to allow simple formatting:
 public List<JsonObject> getInput() {
  return input;
 }
 public UpsertOpportunityRoles setInput(List<JsonObject> input) {
  this.input = input;
  return this;
 }
 public String getAction() {
  return action;
 }
 public UpsertOpportunityRoles setAction(String action) {
  this.action = action;
  return this;
 }
 public String getDedupeBy() {
  return dedupeBy;
 }
 public UpsertOpportunityRoles setDedupeBy(String dedupeBy) {
  this.dedupeBy = dedupeBy;
  return this;
 }

}
```

前の例と同様に、コンストラクターと addRoles メソッドのパターンに従います。 次に例を示します。

```java
//Create Some opp roles now
JsonObject opp1Role = new JsonObject()
                        .add("role", "Captain")
                        .add("externalopportunityid", opp1.get("externalopportunityid").asString())
                        .add("leadId", 318794);
JsonObject opp2Role = new JsonObject()
                        .add("role", "Commander")
                        .add("externalopportunityid", opp2.get("externalopportunityid").asString())
                        .add("leadId", 318795);

//Create an Instance of UpsertOpportunityRoles and POST it
UpsertOpportunityRoles upsertRoles = new UpsertOpportunityRoles(auth)
                        .setAction("createOnly")
                        .addRoles(opp1Role, opp2Role);
JsonObject rolesResult = upsertRoles.postData();
System.out.println(rolesResult);
```

ここでは、2 つのサンプルの役割に新しい JsonObjects を作成し、必要な dedupeFields を追加して、作成済みのオポチュニティから externalopportunityid を取り込み、Marketoにプッシュします。

### まとめ

主なメソッドの完全な例を次に示します。

```java
package dev.marketo.opportunities;

import com.eclipsesource.json.JsonObject;

public class App
{
    public static void main( String[] args )
    {
     //create an Instance of Auth
        Auth auth = new Auth("CLIENT_ID_CHANGE_ME", "CLIENT_SECRET_CHANGE_ME", "MARKETO_HOST_CHANGE_ME");

        //Create a new company to associate to
        JsonObject myCompany = new JsonObject().add("externalCompanyId", "myCompany");
        UpsertCompanies upsertCompanies = new UpsertCompanies(auth).addCompanies(myCompany);
        JsonObject companiesResult = upsertCompanies.postData();
        System.out.println(companiesResult);

        //Create some JsonObjects for Opportunity Data
        JsonObject opp1 = new JsonObject().add("name", "opportunity1")
           .add("externalopportunityid", "Opportunity1Test")
           .add("externalCompanyId", "myCompany")
           .add("externalCreatedDate", "2015-01-01T00:00:00z");
        JsonObject opp2 = new JsonObject().add("name", "opportunity2")
           .add("externalopportunityid", "Opportunity2Test")
           .add("externalCompanyId", "myCompany")
           .add("externalCreatedDate", "2015-01-01T00:00:00z");

        //Create an Instance of UpsertOpportunities and POST it
        UpsertOpportunities upsertOpps = new UpsertOpportunities(auth)
                                .setAction("createOnly")
                                .addOpportunities(opp1, opp2);
        JsonObject oppsResult = upsertOpps.postData();
        System.out.println(oppsResult);

        //Create Some opp roles now
        JsonObject opp1Role = new JsonObject()
           .add("role", "Captain")
           .add("externalopportunityid", opp1.get("externalopportunityid").asString())
           .add("leadId", 318794);
        JsonObject opp2Role = new JsonObject()
           .add("role", "Commander")
           .add("externalopportunityid", opp2.get("externalopportunityid").asString())
           .add("leadId", 318795);

        //Create an Instance of UpsertOpportunityRoles and POST it
        UpsertOpportunityRoles upsertRoles = new UpsertOpportunityRoles(auth)
           .setAction("createOnly")
           .addRoles(opp1Role, opp2Role);
        JsonObject rolesResult = upsertRoles.postData();
        System.out.println(rolesResult);

    }
}
```

会社、機会、役割を作成するシーケンスを確認できます。 これで、会社と商談のデータをMarketoに同期する準備がすべて整いました。

Posted on _2015-08-07_ by _Kenny_

## Marketo REST API を使用したトランザクションメールの送信：第 2 部、カスタムコンテンツ

今週は、Request Campaign API 呼び出しを使用して、動的コンテンツをメールに渡す方法を確認しています。 リクエストキャンペーンを使用すると、メールを外部からトリガーできるだけでなく、メール内の [ マイトークン ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/tokens/understanding-my-tokens-in-a-program) のコンテンツを置き換えることもできます。 マイトークンは、プログラムまたはマーケティングフォルダーレベルでカスタマイズできる再利用可能なコンテンツです。 また、これらは、リクエストキャンペーンの呼び出しで置き換えるプレースホルダーとしてのみ存在する可能性があります。

### メールの作成

コンテンツをカスタマイズするには、まずMarketoで [ プログラム ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/creating-programs/create-a-program) と [ メール ](https://experienceleague.adobe.com/ja/docs/marketo/using/home) を設定する必要があります。 カスタムコンテンツを生成するには、プログラム内でトークンを作成し、送信するメールに配置する必要があります。 簡単にするために、この例では 1 つのトークンのみを使用していますが、送信元メール、送信者名、返信先またはメール内の任意のコンテンツで、メール内の任意の数のトークンを置き換えることができます。 ここで、置換用のトークンリッチテキストを 1 つ作成し、「bodyReplacement」という名前を付けます。リッチテキストを使用すると、トークン内の任意のコンテンツを入力したい任意のHTMLに置き換えることができます。 トークンは空のままでは保存できないので、ここにプレースホルダーテキストを挿入します。次に、トークンをメールに挿入する必要があります。このトークンにアクセスして、リクエストキャンペーンの呼び出しを通じて置き換えることができます。 このトークンは、メールごとに置き換える必要がある 1 行のテキストとして単純にすることも、メールのレイアウトのほぼ全体を含めることもできます。

### コード

先週からコードを拡張して、カスタマイズしたトークンをリクエストキャンペーン呼び出しに渡しています。

```java
package dev.marketo.blog_request_campaign;

import com.eclipsesource.json.JsonArray;

public class App
{
    public static void main( String[] args )
    {
     //Create an instance of Auth so that we can authenticate with our Marketo instance
        Auth auth = new Auth("Client ID - CHANGE ME", "Client Secret - CHANGE ME", "Host - CHANGE ME");

        //Create and parameterize an instance of Leads
        Leads leadsRequest = new Leads(auth).setFilterType("email").addFilterValue("requestCampaign.test@marketo.com");

        //get the inner results array of the response
        JsonArray leadsResult = leadsRequest.getData().get("result").asArray();

        //get the id of the record indexed at 0
        int lead = leadsResult.get(0).asObject().get("id").asInt();

        //Set the ID of our campaign from Marketo
        int campaignId = 1578;
        RequestCampaign rc = new RequestCampaign(auth, campaignId).addLead(lead);

        //Create the content of the token here, and add it to the request
        String bodyReplacement = "<div class="replacedContent"><p>This content has been replaced</p></div>";
        rc.addToken("{{my.bodyReplacement}}", bodyReplacement);
        rc.postData();
    }
}
```

今回は、bodyReplacement 変数にトークンの内容を作成し、addToken メソッドを使用してリクエストに追加します。addToken はキーと値を受け取り、JsonObject 表現を作成して、内部の tokens 配列に追加します。その後、これが postData メソッド中にシリアル化され、次のような本文が作成されます。

`{"input":{"leads":[{"id":1}],"tokens":[{"name":"{{my.bodyReplacement}}","value":"<div class="replacedContent"><p>This content has been replaced</p></div>"}]}}`

組み合わせると、コンソール出力は次のようになります。

```bash
Token is empty or expired. Trying new authentication
Trying to authenticate with&nbsp;...
Got Authentication Response: {"access_token":"19d51b9a-ff60-4222-bbd5-be8b206f1d40:st","token_type":"bearer","expires_in":3565,"scope":"<apiuser@mktosupport.com>"}
Executing RequestCampaign call
Endpoint: .../rest/v1/campaigns/1578/trigger.json?access_token=19d51b9a-ff60-4222-bbd5-be8b206f1d40:st
Request Body:
{"input":{"leads":[{"id":1}],"tokens":[{"name":"{{my.bodyReplacement}}","value":"<div class="replacedContent"><p>This content has been replaced</p></div>"}]}}
Result:
{"requestId":"1e8d#14eadc5143d","result":[{"id":1578}],"success":true}
```

### まとめ

この方法は、様々な方法で拡張可能で、個々のレイアウトセクション内またはメール外部のメールのコンテンツを変更し、カスタム値をタスクや注目のアクションに渡すことができます。プログラム内からトークンを使用できる場所はすべて、この方法を使用してカスタマイズできます。また、同様の機能は、[キャンペーンをスケジュール](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST)呼び出しでも使用でき、バッチキャンペーン全体をまたいでトークンを処理できます。これらはリードごとにカスタマイズすることはできませんが、幅広いリードセットにわたってコンテンツをカスタマイズする場合に非常に役立ちます。

Posted on _2015-07-24_ by _Kenny_

## API を使用したMarketoのリードデータの更新

1 年以上前に、API を使用してMarketoの顧客情報と見込み客情報の更新を投稿しました。 この POST では、外部システムに更新をポーリングするために繰り返し実行できるコードサンプルを示しました。 考え方としては、外部データを取得してMarketoにプッシュし、リード情報を更新することでした。 提示されたコードサンプルは、SOAP API を使用していました。 同じ目標を達成するための REST エンドポイント。 **プログラム入力** 外部システムからのデータを、Marketo REST API で使用可能な形式に変換する必要が生じる可能性があります。 リードを作成/更新 API を使用しているので、データはリクエスト本文で送信される JSON としてフォーマットする必要があります。 これは、例で説明するのが最適です。 以下の Java サンプルコードでは、モックリードデータを文字列の配列に配置しています。 各リードのデータに続く各文字列：名、姓、メールアドレス、役職。

```java
private static String externalLeadData[] = {
        "Henry, Adams, <henry@superstar.com>, Director of Demand Generation",
        "Suzie, Smith, <ssmith@gmail.com>, VP Marketing"
};
```

サンプルコードは、配列を以下の JSON ブロックに変換します。

```json
{
"input":
    [
        {"firstName":"Henry", "lastName":"Adams", "email":"<henry@superstar.com>", "title":"Director of Demand Generation"},
        {"firstName":"Suzie", "lastName":"Smith", "email":"<ssmith@gmail.com>", "title":"VP Marketing"}
    ]
}
```

各「入力」配列項目は、Marketoの個々のリードに対応します。 配列項目は、1 つ以上のMarketo リードフィールド名とそれぞれの値を含む JSON オブジェクトです。 指定するフィールド名（この場合は firstName、lastName、email および title）は、Marketo配信登録で定義された REST API 名と一致する必要があります。 Marketo管理パネルのフィールド管理セクションで、フィールド名を書き出すと、REST API 名を見つけることができます。 フィールド名は、以下に示すように Excel ファイルに書き出されます。 または、[Describe Lead](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeUsingGET_2) API を呼び出すことで、プログラムでフィールド名を見つけることもできます。 例えば、次に示す Describe 応答スニペットには、「名」フィールド用の REST API 名が含まれています。

```json
{
    "id": 29,
    "displayName": "First Name",
    "dataType": "string",
    "length": 255,
    "soap": {
        "name": "FirstName",
        "readOnly": false
    },
    "rest": {
        "name": "firstName",
        "readOnly": false
    }
},
```

**プログラムロジック** ペイロードが適切な形式になったら、リードの作成/更新を呼び出す準備が整います。 このサンプルでは、オプションのパラメーターは指定しません。 デフォルトの動作では、リードレコード（アップサート）を作成または更新し、重複排除のためにメールを使用し、同期処理を使用します。 リードの作成/更新の呼び出しが成功した場合、応答本文には、Marketoのリード ID とリードの作成/更新処理のステータスを含む「result」配列が含まれます。 リクエストで渡した「アクション」パラメーターに応じて、ステータスは「更新済み」、「作成済み」、「スキップ」のいずれかです。 この例で続けて、最初のリードが存在せず（Henry Adams）、2 番目のリードが存在したとします（Suzie Smith）。 次のような応答は、最初のリードが作成され、2 番目のリードが更新されたことを示します。

```json
{
    "success":true,
    "requestId":"118f8#14f1a0b82fc",
    "result":[
        {
            "id":318798,
            "status":"created"
        },
        {
            "id":318797,
            "status":"updated"
        }
    ]
}
```

今のところはこれで終わりです。 ハッピーコーディング！ **プログラムコード**

```java
package com.marketo;

// minimal-json library (<https://github.com/ralfstx/minimal-json>)
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

import javax.net.ssl.HttpsURLConnection;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStreamWriter;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.\*;

public class CreateUpdateLeads {
    //
    // Define Marketo REST API access credentials: Account Id, Client Id, Client Secret.  For example:
    //    public static String CUSTOM_SERVICE_DATA[] =
    //      {"111-AAA-222", "2f4a4435-f6fa-4bd9-3248-098754982345", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W"};
    //
    private static final String CUSTOM_SERVICE_DATA[] =
            { INSERT YOUR CUSTOM SERVICE DATA HERE };

    //
    // Mock up data that could be read from an external data source.
    // An array of CSV strings the form:
    //   "firstName, lastName, email, title"
    private static String externalLeadData[] = {
        "Henry, Adams, henry@superstar.com, Director of Demand Generation",
        "Suzie, Smith, ssmith@gmail.com, VP Marketing"
    };

    public static void main(String[] args) {
        // Compose base URL
        String baseUrl = String.format("https://%s.mktorest.com",
                CUSTOM_SERVICE_DATA[0]);

        // Compose Identity URL
        String identityUrl = String.format("%s/identity/oauth/token?grant_type=%s&client_id=%s&client_secret=%s",
                baseUrl, "client_credentials", CUSTOM_SERVICE_DATA[1], CUSTOM_SERVICE_DATA[2]);

        // Call Identity API
        JsonObject identityObj = JsonObject.readFrom(httpRequest("GET", identityUrl, null));
        String accessToken = identityObj.get("access_token").asString();

        // Compose URL for Create/Update Leads
        String createUpdateLeadsUrl = String.format("%s/rest/v1/leads.json?access_token=%s", baseUrl, accessToken);

        // Convert String array into JsonArray to pass as part of request body
        JsonArray input = convertExternalLeadDataToJson(externalLeadData);

        // Build request body JSON
        JsonObject requestObj = new JsonObject();
        requestObj.add("input", input);

        // Call Create/Update Lead API
        JsonArray result = new JsonArray();
        JsonObject leadObj = JsonObject.readFrom(httpRequest("POST", createUpdateLeadsUrl, requestObj.toString()));
        if (leadObj.get("success").asBoolean()) {
            if (leadObj.get("result") != null) {
                result = leadObj.get("result").asArray();
            }
        }

        // Print out results object
        System.out.println(result);
        System.exit(0);
    }

    // Convert array of CSV formatted Strings into an array of JSON objects
    private static JsonArray convertExternalLeadDataToJson(String input[]) {
        JsonArray output = new JsonArray();

        // Loop through each CSV row in array
        for (int i = 0; i < input.length; i++) {
            // Split CSV row into separate fields
            List items = Arrays.asList(input[i].split(","));

            // Add fields to JSON object
            JsonObject lead = new JsonObject();
            lead.add("firstName", items.get(0));
            lead.add("lastName", items.get(1));
            lead.add("email", items.get(2));
            lead.add("title", items.get(3));
            output.add(lead);
        }
        return output;
    }

    // Perform HTTP request
    private static String httpRequest(String method, String endpoint, String body) {
        String data = "";
        try {
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setDoOutput(true);
            urlConn.setRequestMethod(method);
            switch (method) {
                case "GET":
                    break;
                case "POST":
                    urlConn.setRequestProperty("Content-type", "application/json");
                    urlConn.setRequestProperty("accept", "text/json");
                    OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
                    wr.write(body);
                    wr.flush();
                    break;
                default:
                    System.out.println("Error: Invalid method.");
                    return data;
            }
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    private static String convertStreamToString(InputStream inputStream) {
        try {
            return new Scanner(inputStream).useDelimiter("A").next();
        } catch (NoSuchElementException e) {
            return "";
        }
    }
}
```

Posted on _2015-08-14_ by _David_

## Marketoへの SalesPerson データの追加

新しい SalesPerson API を使用すると、ネイティブの CRM 統合がなくても、インスタンスの SalesPerson レコードにMarketo リードを自由に関連付けることができます。 これにより、Marketo内で {{lead.Lead Owner Email Address}} および関連するフィールドとトークンを使用できます。

### 販売担当者レコードの作成

リードを販売担当者レコードに関連付けるには、まず販売担当者レコードをMarketoに入力する必要があります。 PHP のクラスの例を以下に示します。

```php
<?php

class SalesPerson{
 private $auth;//auth object
 private $action;// string designating request action, createOnly, updateOnly, createOrUpdate
 private $dedupeBy;//dedupeFields or idField
 private $input;//array of salesperson objects for input

 //takes an Auth object as the first argument
 public function _construct($auth, $input){
  $this->auth = $auth;
  $this->input = $input;
 }

 //constructs the json request body
 private function bodyBuilder(){
  $body = new stdClass();
  $body->input = $this->input;
  if (isset($this->action)){
   $body->action = $this->action;
  }
  if (isset($this->dedupeBy)){
   $body->dedupeBy = $this->dedupeBy;
  }
  return json_encode($body);
 }
 //submits the request to Marketo and returns the response as a string
 public function postData(){
  $url = $this->auth->getHost() . "/rest/v1/salespersons.json?access_token=" . $this->auth->getToken();
  $ch = curl_init($url);
  $requestBody = $this->bodyBuilder();
  curl_setopt($ch,  CURLOPT_RETURNTRANSFER, 1);
  curl_setopt($ch, CURLOPT_HTTPHEADER, array('accept: application/json','Content-Type: application/json'));
  curl_setopt($ch, CURLOPT_POST, 1);
  curl_setopt($ch, CURLOPT_POSTFIELDS, $requestBody);
  curl_getinfo($ch);
  $response = curl_exec($ch);
  curl_close($ch);
  return $response;
 }
 //getters and setters
 public function setAction($action){
  $this->action = $action;
 }
 public function getAction($action){
  return $this->action;
 }
 public function setDedupeBy($dedupeBy){
  $this->dedupeBy = $dedupeBy;
 }
 public function getDedupeBy($dedupeBy){
  return $this->dedupeBy;
 }
 public function addSalesPersons($input){
  if($this->input != null){
   if (is_array($input)){
    foreach($input as $item){
     array_push($this->input, $item);
    }
   }else{
    array_push($this->input, $input);
   }
  }else{
   $this->input = $input;
  }
 }
 public function getInput(){
  return $this->input;
 }

}
```

上記のクラスの$input 変数は、可能なメンバを持つ stdClass オブジェクトの配列です。

* externalSalesPersonId （create でのみ有効）
* id （キー入力 updateOnly モードとしてのみ）
* email
* fax
* firstName
* lastName
* mobilePhone
* phone
* title

タイプとフィールドの長さに関する詳細は、Describe SalesPerson 呼び出しで取得できます。

### リードの同期

必要なリードを同期するための簡単なサンプルクラスを次に示します。

```php
<?php

class Leads{
 private $auth;//auth object
 private $action;// string designating request action, createOnly, updateOnly, createOrUpdate
 private $lookupField;//dedupeFields or idField
 private $input;//array of salesperson objects for input
 private $asyncProcessing;//specify whether input should be processed asynchronously
 private $partitionName;//partition name for update if requires

 //takes an Auth object as the first argument
 public function _construct($auth, $input){
  $this->auth = $auth;
  $this->input = $input;
 }

 //constructs the json request body
 private function bodyBuilder(){
  $body = new stdClass();
  $body->input = $this->input;
  if (isset($this->action)){
   $body->action = $this->action;
  }
  if (isset($this->lookupField)){
   $body->lookupField = $this->lookupField;
  }
  return json_encode($body);
 }
 //submits the request to Marketo and returns the response as a string
 public function postData(){
  $url = $this->auth->getHost() . "/rest/v1/leads.json?access_token=" . $this->auth->getToken();
  $ch = curl_init($url);
  $requestBody = $this->bodyBuilder();
  curl_setopt($ch,  CURLOPT_RETURNTRANSFER, 1);
  curl_setopt($ch, CURLOPT_HTTPHEADER, array('accept: application/json','Content-Type: application/json'));
  curl_setopt($ch, CURLOPT_POST, 1);
  curl_setopt($ch, CURLOPT_POSTFIELDS, $requestBody);
  curl_getinfo($ch);
  $response = curl_exec($ch);
  curl_close($ch);
  return $response;
 }
 //getters and setters
 public function setAction($action){
  $this->action = $action;
 }
 public function getAction(){
  return $this->action;
 }
 public function setDedupeBy($lookupField){
  $this->dedupeBy = $lookupField;
 }
 public function getDedupeBy(){
  return $this->dedupeBy;
 }
 public function addLeads($input){
  if($this->input != null){
   if (is_array($input)){
    foreach($input as $item){
     array_push($this->input, $item);
    }
   }else{
    array_push($this->input, $input);
   }
  }else if (is_array($input)){
   $this->input = $input;
  }else{
   $this->input = [$input];
  }
 }
 public function getInput(){
  return $this->input;
 }
 public function setAsyncProcessing($asyncProcessing){
  $this->asyncProcessing = $asyncProcessing;
 }
 public function getAsyncProcessing() {
  return $this->asyncProcessing;
 }
 public function setPartitionName($partitionName){
  $this->partitionName = $partitionName;
 }
 public function getPartitionName() {
  return $this->partitionName;
 }

}
```

### 処理

次の例では、2 つの営業担当者レコードを作成し、それらを 2 つのリードレコードに関連付けます。

```php
<?php

require 'Auth.php';
require 'SalesPerson.php';
require 'Leads.php';

//Create an Auth object for authentication
$auth = new Auth("https://284-RPR-133.mktorest.com", "7f99bd49-0e0e-4715-a72a-0c9319f75552", "O5lZHhrQDfDKRhulY89IU42PfdhRSe6m");

//Compose new SalesPerson Records
$sales1 = new stdClass();
$sales1->externalSalesPersonId = "SalesPerson 1";
$sales1->email = "sales1@example.com";
$sales1->firstName = "Jane";
$sales1->lastName = "Doe";

$sales2 = new stdClass();
$sales2->externalSalesPersonId = "SalesPerson 2";
$sales2->email = "sales2@example.com";
$sales2->firstName = "John";
$sales2->lastName = "Doe";

//Compose lead records
$lead1 = new stdClass();
$lead1->email = "marketoDev@example.com";
//Add the external id of the desired salesperson
$lead1->externalSalesPersonId = $sales1->externalSalesPersonId;

$lead2 = new stdClass();
$lead2->email = "devBlog@example.com";
$lead2->externalSalesPersonId = $sales2->externalSalesPersonId;

//Create a new instance of SalesPerson to submit records
$salesPerson = new SalesPerson($auth, [$sales1, $sales2]);
$spResponse = $salesPerson->postData();
print_r($spResponse . "rn");
$json = json_decode($spResponse);

//Check for success on synching SalesPersons
if ($json->success){
 $leads = new Leads($auth, [$lead1, $lead2]);
 $leadsResponse = $leads->postData();
 print_r($leadsResponse . "rn");
}else{
 print_r("SalesPerson request failed with errors:rn");
 foreach ($json->errors as $error){
  print_r("code: " . $error->code . ", message: " . $error->message . "rn");
 }
}
```

サンプルクラスでは、同期する必要がある SalesPerson と Lead のレコードを表す stdClass オブジェクトを作成し、必要な各フィールドをメンバーとして追加します。 このコードを実行すると、リード <marketoDev@example.com> と <devBlog@example.com> の両方に「リード所有者のメール」、「リード所有者の名」、「リード所有者の姓」の各フィールドが設定され、これらのフィールドに関連するトークンを使用して、関連するスマートリストフィルターでフィルタリングできるようになります。

### 認証クラス

```php
<?php

class Auth{
 private $host;//host of the target Marketo instance
 private $clientId;//client Id
 private $clientSecret;//client secret
 private $token;//access_token
 private $expiry;

 function _construct($host, $clientId, $clientSecret){
  $this->host = $host;
  $this->clientId = $clientId;
  $this->clientSecret = $clientSecret;
 }
 public function getToken(){
  if (!isset($this->token) || $this->expiry > time()){
   $data = $this->getData();
   $this->expiry = time() + $data->expires_in;
   $this->token = $data->access_token;
   return $this->token;
  }else{
   return $this->token;
  }
 }
 private function getData(){
  $url = $this->host . "/identity/oauth/token?grant_type=client_credentials&client_id=" . $this->clientId . "&client_secret="
     . $this->clientSecret;
  $ch = curl_init($url);
  curl_setopt($ch,  CURLOPT_RETURNTRANSFER, 1);
  curl_setopt($ch, CURLOPT_HTTPHEADER, array('accept: application/json','Content-Type: application/json'));
  $response = curl_exec($ch);
  $json = json_decode($response);
  curl_close($ch);
  return $json;
 }
 public function getHost(){
  return $this->host;
 }
}
```

Posted on _2015-08-21_ by _Kenny_

## API ユーザーとカスタムサービスのベストプラクティス

Marketoの REST API は、認証にカスタムサービスを使用し、これらの各サービスは、API のみのMarketo ユーザーが所有しています。 各カスタムサービスの機能は、そのユーザーに割り当てられた各役割の権限によって決まります。 個々のユーザーとカスタムサービスを統合に割り当てると、次のような複数の利点があります。

* ユーザーに与えられた役割を通じて、個々のサービスに与えられる [ 権限 ](/help/rest-api/custom-services.md) を微調整できます。
* 対応するカスタムサービスを削除することで、他のサービスを無効にせずに個々の web サービスでインスタンスへの呼び出しを無効にすることができます。
* API 呼び出しの使用状況に関するレポートはユーザーごとに分類され、高い使用率と異常な使用率を特定できます
* 各 web サービスにアクセスできるデータを確認する方が簡単です
* Workspace対応インスタンスでは、アクセス可能なワークスペースに役割を付与するだけで、特定のビジネスユニットへのアクセスを制限できます

### API 使用量

各 API ユーザは API 使用量レポートで個別に報告されるので、web サービスをユーザごとに分割すると、各統合の使用量を簡単に把握できます。インスタンスへの API 呼び出しの数が制限を超え、後続の呼び出しが失敗する場合は、この方法を使用すると、各サービスからのボリュームを把握し、問題を解決する方法を評価できます。管理/web サービスに移動し、過去 7 日間の呼び出し数をクリックして、使用状況を確認します。

### サービスの無効化

統合に望ましくない効果がある場合、個別のカスタムサービスを割り当てていないと、面倒で無効にするのが難しい可能性があります。 管理者/ランチポイントで問題のあるサービスを削除するのと同じくらい簡単に、1 つずつ分類することができます。

### Workspaceの管理

Marketo Enterprise サブスクリプションの場合、サービスが 1 つのワークスペースへのアクセスのみを必要とするのが一般的であり、これは [API ユーザーへのロールの割り当てによって適用 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/allow-user-access-to-a-workspace) できます。 各ユーザーの役割は、グローバルに、またはワークスペースごとに割り当てることができるので、ワークスペース内で適切な場所へのアクセスを制限でき、可能な限り最小限の権限セットを提供します。

Posted on _2015-08-28_ by _Kenny_

## REST API を使用したリードパーティションの指定方法

**リードのパーティション化** Marketoのリードパーティションを使用すると、リードを簡単に分離できます。 パーティションを使用すると、組織内の様々なマーケティンググループが 1 つのMarketo インスタンスを共有できます。 詳細は、「ワークスペースとリード・パーティションについて [ を参照してください ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/understanding-workspaces-and-person-partitions)。 Marketo REST API を使用して、リードパーティションを使用し、プログラムでリードを作成しているとします。 作成したリードが正しいパーティションに配置されるようにするには、どうすればよいですか。 この投稿では、その方法を説明します。 この例では、Workspaces と Partitions を使用して、地域に基づいてリードを分離します。

まず、「国」というワークスペースを定義します。 次に、そのワークスペース内に「Mexico」と「Canada」という 2 つのパーティションを作成します。  **Create Lead in Partition** 「Mexico」パーティションに 2 つのリードを作成するとします。 リードを作成するには、を呼び出します。 パーティションを指定するには、リクエスト本文に「partitionName」属性を含める必要があります。 partitionName の値に何を使用すればよいかを知る方法を教えてください。 インスタンスの有効なパーティション名の値のリストを取得するには、次のように [Get Lead Partitions](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeProgramMemberUsingGET) API を呼び出します。

`GET /rest/v1/leads/partitions.json`

```json
{
    "requestId": "20ae#14f9a1a5a30",
    "result": [
        {
            "id": 1,
            "name": "Default",
            "description": "Initial system lead partition"
        },
        {
            "id": 2,
            "name": "Mexico",
            "description": "Leads that live in Mexico"
        },
        {
            "id": 3,
            "name": "Canada",
            "description": "Leads that live in Canada"
        }
    ],
    "success": true
}
```

この場合、正しい値は「Mexico」なので、次のようにリードの作成/更新に渡します。

`POST /rest/v1/leads.json`

```json
{
    "input": [
        {"email":"enrique.pena-nieto@gob.mx"},
        {"email":"angelica.rivera@gob.mx"}
    ],
    "action":"createOrUpdate",
    "partitionName":"Mexico"
}
```

Marketoに新しく作成されたリードは次のとおりです。  **パーティション内のリードを更新** パーティション内の既存のリードを更新するには、単純に Create/Update Leads を呼び出して、以前と同じように partitionName を指定します。 この更新では、上で作成したリードに名、姓およびタイトルを割り当てます。

`POST /rest/v1/leads.json`

```json
{
"input": [
        {"email":"enrique.pena-nieto@gob.mx", "firstName":"Enrique", "lastName":"Pena Neito", "title": "El Presidente"},
        {"email":"angelica.rivera@gob.mx", "firstName":"Angelica", "lastName": "Rivera", "title": "Primera Dama"}
    ],
    "action":"createOrUpdate",
    "partitionName":"Mexico"
}
```

Marketoの新しく更新されたリードは次のとおりです。
**リードのパーティションの特定** リードが入っているパーティションを把握するにはどうすればよいですか？ この場合は、[ リードを ID で取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) API を使用し、「fields」クエリパラメーターに「leadPartitionId」を指定します。 この場合、上記で作成したリード ID 318816 の情報を取得します。

`GET /rest/v1/lead/318816.json?fields=leadPartitionId,email,firstName,lastName,title`

```json
{
    "requestId": "5c57#14f9a495b1f",
    "result": [
        {
            "id": 318816,
            "lastName": "Pena Neito",
            "title": "El Presidente",
            "email": "enrique.pena-nieto@gob.mx",
            "firstName": "Enrique",
            "leadPartitionId": 2
        }
    ],
    "success": true
}
```

partitionName ではなく、leadPartitionId が返されることに注意してください。 partitionName を取得するには、上記の Get Lead Partitions API からの出力を再確認する必要があります。

```json
{
    "id": 2,
    "name": "Mexico",
    "description": "Leads that live in Mexico"
},
```

この場合、leadPartitionId の値が 2 であれば、「Mexico」の partitionName にマッピングされます。 今のところは以上です。 分割おめでとうございます！

Posted on _2015-09-04_ by _David_

## Marketoのメールスクリプティングにおけるスコアフィールドの比較

**注：** これは Cathal Moran によるゲストの投稿です。 Cathal は、アイルランドのダブリンにあるMarketoの EMEA オフィスで働くソリューションコンサルタントです。

### スコアフィールドの比較

Marketoの多くのお客様、特にクロスセルに重点を置いているユーザーは、複数のスコアフィールドを持っています。これは、特定の商品/領域に対するリードの関心を測定するためによく使用されます。 私がリンゴとバナナを売っていると想像してくださいリードがリンゴで 50 のスコアを持ちバナナで 10 のスコアを持っているなら好みの場所は明らかです私のコンテンツがこの好みを反映しているなら良くはないでしょう メールスクリプティングを使用すると、スコアを比較したり、メールを受信するその特定のリードに対する最高スコア（または最低スコア）に応じてメールのコンテンツをパーソナライズしたりできます。

### 2 つの数値を比較する場合は、フィールド値を整数に変換する必要があります

```
#set ($score1 = $math.toInteger(${lead.Apple_Score}))
#set ($score2 = $math.toInteger(${lead.Banana_Score}))
##check if the lead score is greater than feature score
#if($score1 >= $score2)
                ##if Apple score is greater
                #set($Interest = "Special offer on Apples")
##check is the feature score is higher
#elseif($score2 >= $score1)
                ##if Feature score is greater
                #set($Interest = "Special offer on Bananas")
#else
                ##otherwise
                #set($Interest = "Special offer on Fruit")
#end
##display the Interest as content
${Interest}
```

上記の例では、テキストをパーソナライズするだけですが、同じように簡単に、より高いスコアに基づいて別の画像を表示できます。

Posted on _2015-09-14_ by _Kenny_

## Marketo フォームの送信をバックグラウンドで行う

組織が web コンテンツや顧客データをホストするための様々なプラットフォームを持つ場合、結果のデータを別々のプラットフォームに収集できるように、フォームから並列で送信する必要があるケースはかなり一般的になります。 これを行うには様々な方法がありますが、多くの場合、最も簡単な方法が最善です。Forms 2 API を使用して、非表示のMarketo フォームを送信します。 これは新しいMarketo フォームで機能しますが、フィールドのない空のフォームを作成することをお勧めします。 これにより、何もレンダリングする必要がなくなるので、フォームが必要以上にデータを読み込むことがなくなります。 次に、フォームから [ 埋め込みコード ](https://experienceleague.adobe.com/ja/docs/marketo/using/home) を取得し、目的のページの本文に追加して、小さな変更を加えます。 埋め込みコードには、次のようなフォーム要素が含まれています。

`<form id="mktoForm_1068"></form>`

次のように、要素が表示されないように、「style=&quot;display:none&quot;」を要素に追加します。

`<form id="mktoForm_1068" style="display:none"></form>`

フォームが埋め込まれ、非表示になると、フォームを送信するコードは非常にシンプルになります。

```javascript
var myForm = MktoForms2.allForms()[0];
myForm.addHiddenFields({
 //These are the values which will be submitted to Marketo
 "Email":"test@example.com",
 "FirstName":"John",
 "LastName":"Doe"
 });
myForm.submit();
```

この方法で送信されたFormsは、リードが表示可能なフォームに入力して送信した場合とまったく同じように動作します。 送信のトリガーは、実装ごとに異なるアクションがプロンプトを表示するので、実装間で異なりますが、基本的にどのアクションでも実行させることができます。 重要な部分は、フィールドと値を正しく設定することです。 値が正しく送信されるように、フィールドのSOAP API 名を使用します。これは [ フィールド名の書き出し ](/help/rest-api/list-of-standard-fields.md) で確認できます。

Munchkin Associate Lead からの移行

バックグラウンドでのフォームの送信は、Munchkinのアソシエイトリードにとって推奨される代替手段の 1 つです。 以下のHTMLのサンプルページでは、リードを関連付けるために送信されたのと同じ値を再利用することで、高レベルでの移行を示しています。

```html
<html>
<head>
    <!--
      Munchkin Code
      Replace with your own instance code
    -->
    <script type="text/javascript">
        (function() {
          var didInit = false;
          function initMunchkin() {
            if(didInit === false) {
              didInit = true;
              Munchkin.init('CHANGE ME');
            }
          }
          var s = document.createElement('script');
          s.type = 'text/javascript';
          s.async = true;
          s.src = '//munchkin.marketo.net/munchkin-beta.js';
          s.onreadystatechange = function() {
            if (this.readyState == 'complete' || this.readyState == 'loaded') {
              initMunchkin();
            }
          };
          s.onload = initMunchkin;
          document.getElementsByTagName('head')[0].appendChild(s);
        })();
        </script>
</head>

<body>
  <!--
    Start Embed code.
    Pasted from Form Actions -> Embed Code except for addition of 'style="display:none"' to the form tag in order to hide it, and instance-specific codes redacted
    Replace with your own code for testing
  -->
  <script src="CHANGE ME"></script>
  <form id="CHANGE ME" style="display:none"></form>
  <script>MktoForms2.loadForm("CHANGE ME", "CHANGE ME", "CHANGE ME TO AN INTEGER ID");</script>
  <!--End Embed Code-->

  <!--Demo code-->
    <script>
        //The same map which is assembled for the Munchkin submission can be reused for the form submission
        let values = {
            "Email": "email@example.com",
            "FirstName": "Test",
            "LastName": "Record"
        }
        //whenReady lets us apply a callback to all mkto forms on the page
        //the callback function fires whenever a form is completely loaded
        //for most use cases this will just be used to capture a reference to the form for later usage
        //submission is done in line here for demonstration only
        MktoForms2.whenReady(function(form){

            //the addHiddenFields methods lets us add arbitrary fields to the form as well as their values
            form.addHiddenFields(values);

            //submit the form
            form.submit();


        })
    </script>
</body>
</html>
```

Posted on _2015-09-25_ by _Kenny_

## Marketo REST API の例外とエラー処理：第 1 部

Marketo REST API は exception または error を返す場合があります。これは便宜上、ここからエラーを呼び出すだけです。 エラーは、次の 3 つの異なるレベルで発生する可能性があります。

* HTTP レベル。これらのエラーは 4xx コードで示されます。
* 応答レベル。これらのエラーは、JSON 応答の「errors」配列に含まれます
* レコードレベル。これらのエラーは JSON 応答の「結果」配列に含まれ、「ステータス」フィールドと「理由」配列を使用して、個々のレコードごとに示されます

### HTTP エラー

通常の操作環境では、Marketoは、2 つの HTTP ステータスエラー、413 リクエストエンティティが大きすぎる、および 414 リクエスト URI が長すぎるエラーのみを返します。 これらは、エラーをキャッチし、リクエストを変更して再試行することで復元できますが、スマートコーディングの手法を使用すると、野生で発生することはありません。 リクエストペイロードが 1MB を超える場合はMarketoから 413、[ リードの読み込み ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) の場合は 10MB が返されます。 ほとんどのシナリオでは、これらの制限に達する可能性はほとんどありませんが、リクエストのサイズにチェックを追加して、制限を超える原因となったレコードを新しいリクエストに移動すると、このエラーが返される原因となる状況がエンドポイントで防ぐことができます。 GET リクエストの URI が 8 KiB を超える場合、414 が返されます。 これを回避するには、クエリ文字列の長さがこの制限を超えていないかどうかを確認します。リクエストが POST メソッドに変わる場合は、追加のパラメーター「_method=GET」を使用してリクエスト本文としてクエリ文字列を入力します。 これにより、URI の制限がなくなります。ほとんどの場合、この制限に達することはまれですが、GUID などの長い個々のフィルター値を持つレコードを大量に取得する場合は、やや一般的です。

### 応答レベルのエラー

応答の「成功」パラメーターが false に設定されている場合、応答レベルのエラーが発生します。 「errors」の各エントリには 2 つのメンバーがあり、「code」には 6xx または 7xx の数字と、エラーの理由を平文で示す「message」があります。 6xx コードは常に、リクエストが完全に失敗し、実行されなかったことを示します。例えば、601 「Access token invalid」は、再認証してリクエストで新しいアクセストークンを渡すことで回復できます。 7xx エラーは、データが返されなかったか、無効な日付が含まれている、必須パラメータが欠落しているなど、リクエストが誤ってパラメーター化されたことにより、リクエストが失敗したことを示します。

### レコードレベルのエラー

レコードレベルのエラーは、個々のレコードに対する操作は完了できなかったが、リクエスト自体は有効であったことを示します。これらは、応答の「結果」配列の個々のレコード内で発生します。 これらのレコードの「ステータス」フィールドは「スキップ」され、「理由」配列が存在します。 各理由には、&quot;code&quot; メンバーと &quot;message&quot; メンバーが含まれます。コードは常に 1xxx になり、メッセージはレコードがスキップされた理由を示します。 例えば、リードの作成/更新リクエストの「アクション」が「createOnly」に設定されていて、送信されたレコードのいずれかのキーに対してリードが既に存在する場合です。 この場合、コード 1005 が返され、「Lead already exists」というメッセージが表示されます。 次のいくつかの投稿では、回復可能なエラーと、コード内でこれらを処理する方法の例を見ていきます。

Posted on _2015-10-09_ by _Kenny_

## ゲストでの投稿 – Marketo データベースへの直接 SQL コネクタ

**これは Sumit Sarkar of Progress, Inc.からのゲスト投稿です**

Marketo データベースへの **SQL コネクタ** Marketoには、データにアクセスするための API がドキュメント化されています。 ただし、組織が SQL への直接アクセスを必要とする場合もあります。 Marketoの店舗では、マーケティングと IT の間でラインがぼやけているため、標準ベースの SQL 接続性に対する需要が高まっています。 Marketoへの直接 SQL コネクタは、[Progress DataDirect Cloud](https://www.progress.com/connectors/cloud-data-integration) を通じて使用できます。 DataDirect Cloud は、ODBC （「Open Database Connectivity」）または JDBC （「Java Database Connectivity」）を介した SQL アクセスと、OData （「Open Data Protocol」）を使用した REST に関するオープンな業界標準を通じて、Marketo データを公開するデータ接続サービスです。 DataDirect Cloud を使用してMarketo データを標準で接続する際の一般的なユースケースを以下に示します。

* データの検出とビジュアライゼーション（Qlik、Tableau、SAP Lumira）
* エンタープライズ・レポート（SAP ビジネス・オブジェクト、Microstrategy、Cognos）
* データ統合（SQL Server Integration Services - SSIS、Oracle Data Integrator - ODI、Informatica）
* データ フェデレーション （SQL Server リンク サーバー、SAP HANA SDA、Oracle Database Gateway）
* アドホッククエリ （Microsoft Office、DB ビジュアライザー、Aqua Data Studio）
* データ準備（Alteryx、Trifecta、Paxata）

**Marketoへの SQL アクセスはどのように機能しますか？**

* DataDirect Cloud は、Marketo Integration API によって公開されたデータの論理スキーマを作成します。
* DataDirect Cloud は、Marketo API から取得したデータに対して、柔軟なリアルタイムクエリエンジンを使用して、軽量の ODBC または JDBC クライアントからの SQL リクエストを処理します。
* DataDirect Cloud の接続性は、データの重複がなく、直接かつリアルタイムです。
* DataDirect Cloud ServiceはMarketo API を抽象化するので、エンドユーザーは API バージョンの変更や、SOAPと REST の使用について心配する必要はありません。

DataDirect は、2006 年以来、SaaS データソースへの接続を Web サービス API 上に構築された最初のSalesforce ODBC ドライバーから構築してきました。 **Marketoへの接続の概要：**

1. [DataDirect Cloud ログインの登録 ](https://pacific.progress.com/console/register?productName=d2c&ignoreCookie=true)
1. 「データソース」をクリックし、「+新規データSource」ボタンをクリックします
1. 「Marketo」を選択し、設定を入力してください。 Marketo管理者またはログインに問い合わせて、[SOAP integration の接続情報 ](/help/soap-api/soap-api.md) を見つけることができます。
1. 「接続をテスト」ボタンをクリックします。 Marketoから OData を生成する「OData」タブがあることに注意してください。これについては、今後のブログ投稿で説明します。
1. 公開されたMarketo スキーマを調べる場合や、UI 内から基本的な SQL クエリを発行する場合は、「SQL テスト」をクリックします。
1. 左側の「ダウンロード」をクリックし、インストールするアプリケーションとプラットフォームの DataDirect Cloud ODBC または JDBC ドライバーを選択します。
1. DataDirect Cloud ODBC または JDBC ドライバーをインストールすると、標準ベースのアプリケーションをMarketoに接続できます。

次に、[DataDirect Cloud ODBC クライアントを使用して接続する ](https://www.youtube.com/watch?v=H6PHra56Iig) のビデオ例を示します。 Marketoに適用されるその他の DataDirect Cloud チュートリアルを次に示します。

* [SAP Data Analytics](http://scn.sap.com/community/lumira/blog/2015/08/05/connect-sap-lumira-to-eloqua-marketo-google-analytics)
* [Microstrategy エンタープライズレポート ](https://community.microstrategy.com/t5/Tech-Corner/What-MSTR-developers-should-know-about-Cloud-Data-Sources/ba-p/253083)
* [Oracle Data Integration](https://www.ateam-oracle.com/post/a-universal-cloud-applications-adapter-for-odi/)

**R&amp;D の課題Marketoなどのクラウドソース間で SQL 接続を構築**

すべての SaaS API が標準クエリ言語を公開しているわけではありません。 その場合、エンジニアリングチームは各オブジェクトを個別に確認します。 各オブジェクトは、呼び出し、検索フィルタリングなどに関する一意のルールを持つ異なる API で公開される場合があります。 データモデル全体に対してクエリを実行する標準のエクスペリエンスを提供するには、かなりの労力が必要でした。

完全結合機能の処理。 SaaS API が JOIN 機能を備えたクエリ言語をサポートしていない場合、エンジニアリングチームはその操作を実行する必要があります。 これには、結合を実行する前に最小限のデータを返すようにMarketo API を効率的に呼び出すための SQL からの変換が必要です。 2 つの非常に大きなオブジェクトを結合する場合、データアクセスレイヤーがアプリケーションサーバーまたはデスクトップ上のリソースを大量に消費する可能性があります。 したがって、データアクセスレイヤーを DataDirect Cloud などの Elastic Cloud Service にデプロイすることは、次の 2 つの理由で非常に理にかなっています。

1. クライアントアプリケーションサーバーまたはデスクトップのパフォーマンスが向上し、使用するメモリ/CPU リソースが減少します。
1. DataDirect Cloud とMarketoの間で、事前結合されたデータセットが交換される優れた帯域幅を活用します。

データモデルの処理方法 静的か動的か。 変更を検出してクライアントに伝える方法 SaaS データソースはそれぞれ異なり、Marketoの場合は、特定のオブジェクトに対してビューを介したクエリが実行され、その他のオブジェクトに対してはテーブルを介したクエリが実行されます。 すべての SaaS ソースをまたいでデータモデルとオブジェクトのこのマトリックスを処理することは、確かに課題でした。

**開発者向けのMarketoおよび DataDirect Cloud リファレンス：**

* Marketo接続プロパティ（[ ドキュメントへのリンク ](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html)）
* Marketoでサポートされる SQL および拡張機能（[ ドキュメントへのリンク ](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html,-hubspot,-and-marketo.html)）
* 公開済みのMarketo テーブルおよびビュー（[ ドキュメントへのリンク ](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html)）
* Marketoから返される一般的なエラーメッセージ（[ ドキュメントへのリンク ](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html)）

**Biography:** Sumit Sarkar は、Progress のチーフデータエバンジェリストで、データ接続分野で 10 年以上の経験があります。 クラウドデータとのオープンデータ標準接続に関する世界をリードするコンサルタントである Sumit は、分析に特許出願中のテクノロジーを開発したデータアクセスレイヤーのパフォーマンスチューニング、SaaS プラットフォーム向けのビジネスインテリジェンスとデータウェアハウジング、ODBC、JDBC、ADO.NET、ODATA などの標準に重点を置いた PaaS 環境向けのデータ接続に興味を持っています。 同氏は、IBM・コグノス・Business IntelligenceのIBM認定コンサルタントであり、TDWI のメンバーでもあります。 Dreamforce、Oracle OpenWorld、Strata Hadoop、MongoDB World、SAP Analytics and Business Objects Conference など、様々なカンファレンスでデータ接続性に関するセッションを開催しています。 Twitter: @SAsInSumit LinkedIn: [www.linkedin.com/in/meetsumit](http://www.linkedin.com/in/meetsumit)

Posted on _2015-12-07_ by _Kenny_

## API の使用状況とエラー数のダッシュボードを作成

Marketo API コンシューマーとして、注目すべき有用な情報です。 経時的なトレンドの検出に役立つ過去の使用状況データを取得できるとしたらどうでしょうか？ 統合の正常性の測定に役立つ API エラーコードの概要を取得できるとしたらどうでしょうか？ Marketo テクノロジーパートナーとして、すべてのカスタマーアカウントの使用状況とエラーデータを 1 つのダッシュボードで取得できるとしたらどうでしょうか？ この投稿は、上記の質問に答えるアプローチを提供します。 頑張れ行け！
**統計取得用にスケジュールされたジョブ** エンドポイント「[ 毎日の使用状況を取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLast7DaysErrorsUsingGET)」および「[ 毎日のエラーを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getDailyErrorsUsingGET)」を使用して使用状況とエラーデータを取得するアプリを作成します。 アプリは、1 日に 1 回実行するようにスケジュールされるように設計されています。 アプリを実行するたびに、1 日分の使用状況データが 1 つのファイルに、1 日分のエラーデータが別のファイルに追加されます。 毎月の初めに、新しいファイルペアが作成されます。 これらのファイルは、いつでもアクセスできる履歴記録として機能します。 次に示すのは、アプリロジックです。

* 外部ソースからMarketo アカウント情報（Munchkin ID およびクライアント資格情報）を読み取ります。 メモ：他のユーザーがアカウントデータにアクセスできないようにするには、このソースを保護する必要があります。
* 各アカウントを反復処理し、
   * 1 日の使用状況データを取得するには、Get Daily Usage を呼び出します
   * 毎月の「使用状況」ファイルに毎日の使用状況データを追加
   * Get Daily Errors を呼び出して、1 日のエラーデータを取得します
   * 毎月の「エラー」ファイルに日別エラーデータを追加する

出力ファイル形式出力ファイルの形式は、それぞれの API 呼び出しから返される「result」配列（使用状況とエラー）に一致する JSON 形式です。 「result」配列の各要素は、1 日分のデータを含む JSON オブジェクトです。 出力ファイル命名出力ファイルの名前は次のようになります。

`<type>_<yyyy>_<mm>_<account>.json`

ここで、

`<type>` - データのタイプ（「使用状況」または「エラー」） `<yyyy>` – 年（4 桁） `<mm>` – 月（2 桁） `<account>` - アカウント id （Munchkin id）

出力ファイルの例 usage_2015_10_111-AAA-222.json

```json
[
    { "date": "2015-10-15", "total": 0, "users" : [] },
    { "date": "2015-10-16", "total": 9, "users": [ { "userId": "some.body@yahoo.com", "count": 9 } ] },
    { "date": "2015-10-17", "total": 1120, "users": [ { "userId": "some.body@yahoo.com", "count": 200 }, { "userId": "some.body@marketo.com", "count": 200 }, { "userId": "some.body@gmail.com", "count": 720 } ] },
]
```

`errors_2015_10_111-AAA-222.json:`

```json
[
    { "date": "2015-10-15", "total":80, "errors": [ { "errorCode":"1003", "count":80 } ] },
    { "date": "2015-10-16", "total":148, "errors": [ { "errorCode":"612", "count":40 }, { "errorCode":"609", "count":70 }, { "errorCode":"1008", "count":38 } ] },
    { "date": "2015-10-17", "total":73, "errors": [ { "errorCode":"604", "count":1 }, { "errorCode":"609", "count":56 }, { "errorCode":"610", "count":16 } ] },
]
```

このアプリのコードは、この投稿の最後に記載されています（Stats.java）。 **統計 Web サービス** したがって、このデータをブラウザーに取り込む方法が必要です。 データを配信する web サービスを作成するという提案です。 Web サービスはアプリの出力ファイルを使用し、簡単に提示できる形式でデータをブラウザーに返します。 簡単にするために、また同じ接触チャネルのポリシー制限を回避するために、[JSONP](https://en.wikipedia.org/wiki/JSONP) パターンを活用します。 外部 web サービスの REST エンドポイントの仕様の提案は次のとおりです。**URI**: /stats **メソッド**:GET

**パラメーター**

**説明**

**例**

month

今月のデータを取得します。 含める月のコンマ区切りリスト（2 桁の表記）。 デフォルトではすべての月に設定されています。

10,11

year

今年のデータを取得します。 含める年のコンマ区切りリスト （4 桁表記）。 すべての年をデフォルトにします。

2015年

account

このアカウントのデータを取得します（Munchkin ID）。

111-AAA-222

callback

JSON コンテンツをラップする関数の名前。

processstats

リクエストの例

`GET //localhost:8080/stats?month=10&year=2015&account=111-AAA-222&callback=processStats`

Web サービスは、「usage」ファイルと「error」ファイルを読み取り、それらを組み合わせて、次の形式で返します。

```html
**<Name of Callback here>**

<Contents of Usage file here>,

<Contents of Error file here>
```

これは、2 つの引数を持つ JSONP コールバックです。 最初の引数は、使用方法の「result」配列です。 2 番目の引数は、エラーの「result」配列です。 応答の例

```json
processStats(
    [
        { "date": "2015-10-15", "total": 0, "users" : [] },
        { "date": "2015-10-16", "total": 9, "users": [ { "userId": "some.body@yahoo.com", "count": 9 } ] },
        { "date": "2015-10-17", "total": 1120, "users": [ { "userId": "some.body@yahoo.com", "count": 200 }, { "userId": "some.body@marketo.com", "count": 200 }, { "userId": "some.body@gmail.com", "count": 720 } ] }
    ],
    [
        { "date": "2015-10-15", "total":80, "errors": [ { "errorCode":"1003", "count":80 } ] },
        { "date": "2015-10-16", "total":148, "errors": [ { "errorCode":"612", "count":40 }, { "errorCode":"609", "count":70 }, { "errorCode":"1008", "count":38 } ] },
        { "date": "2015-10-17", "total":73, "errors": [ { "errorCode":"604", "count":1 }, { "errorCode":"609", "count":56 }, { "errorCode":"610", "count":16 } ] },
    ]
);
```

ご覧のように、web サービスは、アプリから 2 つの出力ファイルのコンテンツを単にラップしています。 [Mocky](https://designer.mocky.io) を使用してモック web サービス応答を作成しました。 モック用 web サービスの例は [ こちら](http://www.mocky.io/v2/5627b2f9270000f2226eec63?month=10&year=2015&account=111-AAA-222&callback=processStats) この web サービスの作成は、読者の演習としておきます。**ダッシュボード web ページ** したがって、必要なのは、web サービスを呼び出し、データを書式設定する web ページだけです。 JSONP パターンを使用するには、web サービスを呼び出す `<script>` タグを追加するだけです。

`<script src="http: //<hostname>/stats?month=10&year=2015&account=284-RPR-133&callback=processStats"></script>`

これにより、web サービスの応答本文がHTML ページに直接挿入されます。 次に、JSONP コールバック関数を追加します。

```javascript
function processStats(usage, errors) {
    var cfg = { maxDepth: 5};
    document.write("<h2>Usage</h2>");
    document.body.appendChild(prettyPrint(usage, cfg));
    document.write("<h2>Errors</h2>");
    document.body.appendChild(prettyPrint(errors, cfg));
;
```

この関数は、web サービスの呼び出し後に自動的に呼び出されます。 この例では、各配列で [prettyPrint.js](https://github.com/padolsey-archive/prettyprint.js/tree/master) という単純なJavaScriptの「変数ダンパー」を呼び出します。 prettyPrint 関数は、配列の内容を使用してHTML テーブルを生成するだけです。 以下はHTML テーブルのスクリーンショットです。 Voilà、それは私たちのダッシュボードです！ これは非常にエレガントではありませんが、それはあなたが何が可能であるかを把握する必要があります。 自分の目を引くビジュアライゼーションを作成するために、好きなようにデータを変換することを止めるものは何もありません。 HTMLページは以下のとおりです（Index.html）上記のテーブルは、次の手順でブラウザーにライブ表示されます。

1. Index.html のローカルコピーを保存
1. プリティプリント.js のローカルコピーを保存
1. ブラウザーで Index.html を開きます

以上です。 この投稿で、Marketo API の統計情報の監視に関するアイデアが得られることを願っています。 ハッピーコーディング！ **Stats.java**

```java
package com.marketo;

// minimal-json library (https://github.com/ralfstx/minimal-json)
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

import java.io.\*;
import java.lang.reflect.Array;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.\*;

import java.nio.file.Files;
import java.nio.file.Paths;

import javax.net.ssl.HttpsURLConnection;

public class Stats {
    //
    // Define Marketo instance meta data here. Each row contains three elements: Account Id, Client Id, Client Secret.
    //
    // Note: that this information would typically be stored read from an external source (i.e. database)
    //
    // For example:
    //
    // private static String final CUSTOM_SERVICE_DATA[][] = {
    // {"111-AAA-222", "2f4a4435-f6fa-4bd9-3248-098754982345", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W"},
    // {"222-BBB-333", "5f4a6657-f6fa-4cd9-4356-123083238821", "gfjgfIVE9h4Jjcl59cOMAKFSk78ut12W"},
    // {"444-CCC-444", "9f4a4678-f6fa-4dd9-7735-908713247721", "xzcxvbVE9h4Jjcl59cOMAKFSk78ut12W"}
    // };
    //
    private static final String CUSTOM_SERVICE_DATA[][] = {
    };

    // Output directory for stats files
    private static final String OUTPUT_DIR = "C:stats";

public static void main(String[] args) {

    // Loop through each Marketo instance
    for (int i = 0; i < CUSTOM_SERVICE_DATA.length; i++) {

        // Compose base URL
        String baseUrl = String.format("https://%s.mktorest.com",
            CUSTOM_SERVICE_DATA[i][0]);

        // Compose Identity URL
        String identityUrl = String.format("%s/identity/oauth/token?grant_type=%s&client_id=%s&client_secret=%s",
            baseUrl, "client_credentials", CUSTOM_SERVICE_DATA[i][1], CUSTOM_SERVICE_DATA[i][2]);

        // Call Identity API
        JsonObject identityObj = JsonObject.readFrom(httpRequest("GET", identityUrl, null));
        String accessToken = identityObj.get("access_token").asString();

        // Compose Get Last 7 Days Usage URL
        String usageUrl = String.format("%s/rest/v1/stats/usage/last7days.json?access_token=%s",
            baseUrl, accessToken);

        // Compose Get Last 7 Days Errors URL
        String errorsUrl = String.format("%s/rest/v1/stats/errors/last7days.json?access_token=%s",
            baseUrl, accessToken);

        // Process usage data
        JsonObject usageObj = JsonObject.readFrom(httpRequest("GET", usageUrl, null));
        if (usageObj.get("success").asBoolean()) {
            if (usageObj.get("result") != null) {
                updateFile(usageObj, "usage", CUSTOM_SERVICE_DATA[i][0]);
            }
        }

        // Process errors data
        JsonObject errorsObj = JsonObject.readFrom(httpRequest("GET", errorsUrl, null));
        if (usageObj.get("success").asBoolean()) {
            if (errorsObj.get("result") != null) {
                updateFile(errorsObj, "errors", CUSTOM_SERVICE_DATA[i][0]);
            }
        }
    }
    System.exit(0);
}

// Write yesterday's data to output file
private static void updateFile(JsonObject usageObj, String statsType, String account){

    JsonArray usageResultAry = usageObj.get("result").asArray();
    JsonObject yesterdayUsageResultObj = usageResultAry.get(1).asObject();

    String yesterdayDate = yesterdayUsageResultObj.get("date").asString();
    String[] yesterdayDateAry = yesterdayDate.split("[-]+");

    // "C:statsstats_yyyy_mm_account.json"
    String statsFile = String.format("%s%s_%s_%s_%s.json",
        OUTPUT_DIR, statsType, yesterdayDateAry[0], yesterdayDateAry[1], account);

    // Create file
    File file = new File(statsFile);
    try {
        if (file.createNewFile()) {
            // created new file, seed with empty array
            FileWriter fw = new FileWriter(file.getAbsoluteFile());
            BufferedWriter bw = new BufferedWriter(fw);
            bw.write("[n]");
            bw.close();
        }
    } catch (IOException e) {
        e.printStackTrace();
    }

    // Read file
    String content = null;
    try {
        content = new String(Files.readAllBytes(Paths.get(statsFile)));
    } catch (IOException e) {
        e.printStackTrace();
    }

    // Remove trailing "]", append new record, append trailing "]"
    content = content.substring(0, content.length() - 1);
    content += yesterdayUsageResultObj.toString();
    content += "n]";

    // Write file
    FileWriter fw = null;
    try {
        fw = new FileWriter(file.getAbsoluteFile());
        BufferedWriter bw = new BufferedWriter(fw);
        bw.write(content);
        bw.close();
    } catch (IOException e) {
        e.printStackTrace();
    }
}

// Perform HTTP request
private static String httpRequest(String method, String endpoint, String body) {
    String data = "";
    try {
        URL url = new URL(endpoint);
        HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
        urlConn.setDoOutput(true);
        urlConn.setRequestMethod(method);
        switch (method) {
            case "GET":
                break;
            case "POST":
                urlConn.setRequestProperty("Content-type", "application/json");
                urlConn.setRequestProperty("accept", "text/json");
                OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
                wr.write(body);
                wr.flush();
                break;
            default:
                System.out.println("Error: Invalid method.");
                return data;
        }
        int responseCode = urlConn.getResponseCode();
        if (responseCode == 200) {
            InputStream inStream = urlConn.getInputStream();
            data = convertStreamToString(inStream);
        } else {
            System.out.println(responseCode);
            data = "Status:" + responseCode;
        }
    } catch (MalformedURLException e) {
        System.out.println("URL not valid.");
    } catch (IOException e) {
        System.out.println("IOException: " + e.getMessage());
        e.printStackTrace();
    }
    return data;
}

private static String convertStreamToString(InputStream inputStream) {
    try {
        return new Scanner(inputStream).useDelimiter("A").next();
    } catch (NoSuchElementException e) {
        return "";
    }
}
}
```

**Index.html**

```html
<html>
<head>
<title>Marketo API Stats</title>
<!-- Browser JavaScript variable dumper                  -->
<!-- https://github.com/padolsey-archive/prettyprint.js  -->
<script src="prettyPrint.js"></script>
</head>
<body>

<h1>Marketo API Stats</h1>

<script>
// JSONP callback that uses prettyPrint to format API stats
function processStats(usage, errors) {
    var cfg = { maxDepth: 5};
    document.write("<h2>Usage</h2>");
    document.body.appendChild(prettyPrint(usage, cfg));
    document.write("<h2>Errors</h2>");
    document.body.appendChild(prettyPrint(errors, cfg));
};
</script>

<!-- Web service for you to implement as an exercise                                                        -->
<!-- <script src="http://localhost:8080/stats?month=10&account=111-AAA-222&callback=processStats"></script> -->

<!-- Mock web service that returns sample payload -->
<!-- http://www.mocky.io/                         -->
<script src="http://www.mocky.io/v2/5627b2f9270000f2226eec63?month=10&year=2015&account=111-AAA-222&callback=processStats"></script>"
</body>
</html>
```

Posted on _2015-10-22_ by _David_

## Marketo REST API の例外とエラー処理：第 3 部

ほとんどの場合、Marketo REST API から返されるエラーは自動的には復元できません。 ただし、自動的に回復したり、特定のタイプのエラーが表示されないようにする場合がいくつかあります。

### リクエストサイズのエラー

このシリーズの最後の投稿で見たように、Marketoは、URI の長さが 8KiB を超える場合は HTTP ステータスコード 414、リクエスト本文が 1MB を超える場合は 413、読み込みリードの場合は 10MB を生成します。 414 は稀ですが、「リードの取得方法」フィルタータイプを使用して、300 個の個別の GUID または同様の条件に基づいてレコードをリクエストする場合は、これらが表示されることがあります。 次のリクエストがあるとします。`<https://AAA-BBB-CCC.mktorest.com/rest/v1/leads.json?filterType=customGUID&fields=email`、company...firstName、lastName> リクエストを送信すると、URI が 8KiB を超えているので、Marketoはステータス 414 を返します。

これを処理するには、GETの代わりに POST を送信し、URI に&#39;_method=GET&#39;を追加し、リクエスト本文に x-www-form-urlencoded リクエストとしてクエリ文字列を渡します。URI: `<https://AAA-BBB-CCC.mktorest.com/rest/v1/leads.json?_method=GET>` リクエスト本文：filterType=customGUID&amp;fields=email,company...firstName, lastName ただし、HTTP レスポンスからこの例外をキャッチする代わりに、実行時にリクエストの全長を確認し、URI が 8K を超える場合にデプロイします。 または、すべての場合に POST メソッドを使用して、レコードをバッチ取得することもできます。 413 の場合も同様のパターンに従い、シリアル化ステップでレコードを追加する際にリクエスト本文の長さを確認し、この制限を超える場合はリクエストを複数の部分に分割します。

### 認証エラー

次の回復可能なエラーのクラスは、認証に関するものです。 expires_in 期間が経過した後に以前有効なアクセストークンを使用した場合、最初の使用ではエラーコード 602 が返されます。「Access token expired. その後、同じトークンを使用すると、「Access token invalid」という 601 が返されます。 ターゲットサブスクリプションの有効なアクセストークンではない文字列をその他に使用すると、601 が発生します。 どちらの場合も、このエラーは、再認証を行い、失敗したリクエストを再試行して新しいアクセストークンを渡すことで、から回復できます。

### タイムアウト

ごくまれに、30 秒のタイムアウト期間が経過すると、呼び出しで「Request timed out」という 604 が返される場合があります。 リードの作成/更新などのバッチ化されたリクエストの場合、リクエストを小さなバッチに分割し、成功が返されるまで再試行できます（バッチが 100 件未満のレコードに分割され、リクエストがまだタイムアウトしている場合は、サポートケースを報告する必要があります）。 その他の最も一般的なケースは、アセット承認の呼び出しです。この呼び出しでは、[ メール ](https://developer.adobe.com/marketo-apis/api/asset/approve-email-by-id/) や [ メールテンプレート ](https://developer.adobe.com/marketo-apis/api/asset/approve-email-template-by-id/) の場合など、別のユーザーやサービスによって現在承認されているレコードがロックされる可能性があります。 このような場合、既存のロックを解決するための再試行には、[ 指数バックオフ ](https://en.wikipedia.org/wiki/Exponential_backoff) を使用する必要があります。 今後数週間のうちに、このシリーズの最後のパートをご確認ください。ここでは、復旧不可能な特定のエラーについて詳しく見ていきます。

Posted on _2015-10-30_ by _Kenny_

## Marketoのセキュリティ機能の強化

Marketoではセキュリティを重視しています。 Marketoは、**[業界全体の取り組み ](https://security.googleblog.com/2014/09/gradually-sunsetting-sha-1.html)** の一環として、セキュリティ保護を強化するために、web 認証と暗号化をアップグレードしています。 ロールアウトは 2011 年 12 月 12 日に行われる予定です。 **誰が影響を受けますか？** 影響を受けるのは、ごく少数のユーザーのみです。10 年以上前のシステムからMarketoに統合され、最近更新されていないユーザーのみです。 サポートされているシステムとバージョンについて詳しくは、**[このリスト ](https://www.digicert.com/faq/sha2/sha-2-compatibility)** を参照してください。 **次のユーザーは影響を受けません：**

* 最新のブラウザーを使用してMarketo.comにアクセスするエンドユーザー（[ リストを参照 ](https://www.digicert.com/faq/sha2/sha-2-compatibility)）
* Informatica、Dell Boomi、Scribe などの統合パートナーを使用しているお客様。
* Launchpoint パートナーを使用しているお客様。

その他のすべてのMarketo ドメインでは、既に SHA2 証明書が使用されています。

Posted on _2015-11-18_ by _Kenny_

## REST API を使用したアクティビティのポーリング

アクティビティは、Marketo Platform のコアオブジェクトです。 アクティビティは、すべての web ページの訪問、メールの開封、ウェビナーの出席、展示会の出席に関して保存される行動データです。 一般的なユースケースは、アクティビティデータと、組織の他の部分からのデータを組み合わせることです。 このサンプルプログラムには 6 つの手順が含まれています。

1. [ リードアクティビティを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET) を呼び出して、特定の日時に作成されたすべてのアクティビティレコードのリストを生成します。 フィルターを使用して、返されるアクティビティレコードのタイプを制限します。
1. 各アクティビティレコードから関心のあるフィールドを抽出します。
1. [ フィルタータイプで複数のリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) を呼び出して、手順 1 のアクティビティに対応するリードレコードのリストを生成します。 手順 2 のアクティビティレコードから抽出した leadId フィールドをフィルターとして使用して、返されるリードを指定します。
1. 各リードレコードから関心のあるフィールドを抽出します。
1. 手順 2 のアクティビティデータを手順 4 のリードデータと結合します。
1. 手順 5 で取得したデータを、外部システムで使用できる形式に変換します。

次の図に示すように、この例では、メール関連のアクティビティを取り込むことを選択しました。

**プログラム入力** デフォルトでは、プログラムは変更を探すために現在の日付から 1 日後に戻ります。 したがって、例えば、このプログラムを毎日同時に実行できます。 さらに時間を遡るには、コマンドライン引数として日数を指定すると、時間のウィンドウを効果的に増やすことができます。 プログラムには、変更できるいくつかの変数が含まれています。CUSTOM_SERVICE_DATA – これには、Marketo カスタムサービスデータ（アカウント ID、クライアント ID、クライアントシークレット）が含まれます。 READ_BATCH_SIZE – 一度に取得するレコードの数です。 これを使用して、体のサイズに合わせて応答を調整します。 LEAD_FIELDS – 収集するリードフィールドのリストが含まれます。 ACTIVITY_TYPES – 収集するアクティビティタイプのリストが含まれます。

**プログラムロジック** まず、時間枠を確立し、REST エンドポイント URL を作成して、認証アクセストークンを取得します。 次に、アクティビティの供給が枯渇するまで実行される Get Paging Token/Get Lead Activities ループを起動します。 このループの目的は、アクティビティレコードを取得し、それらのレコードから関心のあるフィールドを抽出することです。 リードを取得アクティビティでは、次のアクティビティタイプのみを検索するように指定します。

* 配信済みメール
* メールを配信停止
* メールを開く
* 「メール」をクリックします。

各アクティビティレコードから次の関心のあるフィールドを抽出します。

* leadId
* activityType
* activityDate
* primaryAttributeValue

目的に合わせて、アクティビティタイプとアクティビティフィールドの任意の組み合わせを自由に選択できます。 次に、Get Multiple Leads by Filter Type ループを起動します。このループは、リードの供給が枯渇するまで実行されます。 「filterType=id」パラメーターを一連の「filterValues」パラメーターと組み合わせて使用することで、取得したリードレコードを、以前に取得したアクティビティに関連するリードのみに制限できます。 各リードレコードから以下の関心のあるフィールドを抽出します。

* firstName
* lastName
* email

ここでも、好きなリードフィールドを選択できます。 次に、リード ID を使用してリードフィールドをアクティビティフィールドとリンクさせます。 最後に、すべてのデータをループ処理し、JSON 形式に変換して、コンソールに出力します。 **プログラム出力** サンプルプログラムの出力例を以下に示します。 これは、アクティビティフィールドとリードフィールドを JSON の「結果」オブジェクトとして組み合わせたものになります。 ここでの考え方は、この JSON をリクエストペイロードとして外部 web サービスに渡すことができるということです。

```json
{
    "result": [
        {
            "leadId": 318581,
            "activityType": "Email Delivered",
            "activityDate": "2015-03-17T20:00:06Z",
            "primaryAttributeValue": "My Email Program",
            "firstName": "David",
            "lastName": "Everly",
            "email": "everlyd@marketo.com"
        },
        {
            "leadId":318581,
            "activityType":"Open Email",
            "activityDate":"2015-03-17T23:23:12Z",
            "primaryAttributeValue":"My Email Program - Auto Response",
            "firstName":"David",
            "lastName":"Everly",
            "email":"everlyd@marketo.com"
       },
        ... more result objects here...
    ]
}
```

**プログラムコード**

```java
package com.marketo;

// minimal-json library (https://github.com/ralfstx/minimal-json)
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;
import com.eclipsesource.json.JsonValue;

import java.io.\*;
import java.net.MalformedURLException;
import java.net.URL;
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.\*;

import javax.net.ssl.HttpsURLConnection;

public class LeadActivities {
//
// Define Marketo REST API access credentials: Account Id, Client Id, Client Secret.  For example:
    private static Map<String, String> CUSTOM_SERVICE_DATA;
    static {
        CUSTOM_SERVICE_DATA = new HashMap<String, String>();
//        CUSTOM_SERVICE_DATA.put("accountId", "111-AAA-222");
//        CUSTOM_SERVICE_DATA.put("clientId", "2f4a4435-f6fa-4bd9-3248-098754982345");
//        CUSTOM_SERVICE_DATA.put("clientSecret", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W");
    }

    // Number of lead records to read at a time
    private static final String READ_BATCH_SIZE = "200";

    // Lookup lead records using lead id as primary key
    private static final String LEAD_FILTER_TYPE = "id";

    // Lead record lookup returns these fields
    private static final String LEAD_FIELDS = "firstName,lastName,email";

    // Lookup activity records for these activity types
    private static Map<Integer, String> ACTIVITY_TYPES;
    static {
        ACTIVITY_TYPES = new HashMap<Integer, String>();
        ACTIVITY_TYPES.put(7, "Email Delivered");
        ACTIVITY_TYPES.put(9, "Unsubscribe Email");
        ACTIVITY_TYPES.put(10, "Open Email");
        ACTIVITY_TYPES.put(11, "Click Email");
    }

    public static void main(String[] args) {
        // Command line argument to set how far back to look for lead changes (number of days)
        int lookBackNumDays = 1;
        if (args.length == 1) {
            lookBackNumDays = Integer.parseInt(args[0]);
        }

        // Establish "since date" using current timestamp minus some number of days (default is 1 day)
        Calendar cal = Calendar.getInstance();
        cal.add(Calendar.DAY_OF_MONTH, -lookBackNumDays);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
        String sinceDateTime = sdf.format(cal.getTime());

        // Compose base URL
        String baseUrl = String.format("https://%s.mktorest.com",
            CUSTOM_SERVICE_DATA.get("accountId"));

        // Compose Identity URL
        String identityUrl = String.format("%s/identity/oauth/token?grant_type=%s&client_id=%s&client_secret=%s",
                baseUrl, "client_credentials", CUSTOM_SERVICE_DATA.get("clientId"), CUSTOM_SERVICE_DATA.get("clientSecret"));

        // Call Identity API
        JsonObject identityObj = JsonObject.readFrom(getData(identityUrl));
        String accessToken = identityObj.get("access_token").asString();

        // Compose URLs for Get Lead Changes, and Get Paging Token
        String activityTypesUrl = String.format("%s/rest/v1/activities/types.json?access_token=%s",
                baseUrl, accessToken);
        String pagingTokenUrl = String.format("%s/rest/v1/activities/pagingtoken.json?access_token=%s&sinceDatetime=%s",
                baseUrl, accessToken, sinceDateTime);

        // Use activity ids to create filter parameter
        String activityTypeIds = "";
        for (Integer id : ACTIVITY_TYPES.keySet()) {
            activityTypeIds += "&activityTypeIds=" + id.toString();
        }

        // Compose URL for Get Lead Activities
        // Only retrieve activities that match our defined activity types
        String leadActivitiesUrl = String.format("%s/rest/v1/activities.json?access_token=%s%s&batchSize=%s",
                baseUrl, accessToken, activityTypeIds, READ_BATCH_SIZE);

        Map<Integer, List> activitiesMap = new HashMap<Integer, List>();
        Set leadsSet = new HashSet();

        // Call Get Paging Token API
        JsonObject pagingTokenObj = JsonObject.readFrom(getData(pagingTokenUrl));
        if (pagingTokenObj.get("success").asBoolean()) {
            String nextPageToken = pagingTokenObj.get("nextPageToken").asString();
            boolean moreResult;
            do {
                moreResult = false;

                // Call Get Lead Activities API to retrieve activity data
                JsonObject leadActivitiesObj = JsonObject.readFrom(getData(String.format("%s&nextPageToken=%s",
                        leadActivitiesUrl, nextPageToken)));
                if (leadActivitiesObj.get("success").asBoolean()) {
                    moreResult = leadActivitiesObj.get("moreResult").asBoolean();
                    nextPageToken = leadActivitiesObj.get("nextPageToken").asString();

                    if (leadActivitiesObj.get("result") != null) {
                        JsonArray activitiesResultAry = leadActivitiesObj.get("result").asArray();
                        for (JsonValue activitiesResultObj : activitiesResultAry) {

                            // Extract activity fields of interest (leadID, activityType, activityDate, primaryAttributeValue)
                            JsonObject leadObj = new JsonObject();
                            int leadId = activitiesResultObj.asObject().get("leadId").asInt();
                            leadObj.add("activityType", ACTIVITY_TYPES.get(activitiesResultObj.asObject().get("activityTypeId").asInt()));
                            leadObj.add("activityDate", activitiesResultObj.asObject().get("activityDate").asString());
                            leadObj.add("primaryAttributeValue", activitiesResultObj.asObject().get("primaryAttributeValue").asString());

                            // Store JSON containing activity fields in a map using lead id as key
                            List leadLst = activitiesMap.get(leadId);
                            if (leadLst == null) {
                                activitiesMap.put(leadId, new ArrayList());
                                leadLst = activitiesMap.get(leadId);
                            }
                            leadLst.add(leadObj);

                            // Store unique lead ids for use as lead filter value below
                            leadsSet.add(leadId);
                        }
                    }
                }
            } while (moreResult);
        }

        // Use unique lead id values to create filter parameter
        String filterValues = "";
        for (Object object : leadsSet) {
            if (filterValues.length() > 0) {
                filterValues += ",";
            }
            filterValues += String.format("%s", object);
        }

        // Compose Get Multiple Leads by Filter Type URL
        // Only retrieve leads that match the list of lead ids that was accumulated during activity query
        String getMultipleLeadsUrl = String.format("%s/rest/v1/leads.json?access_token=%s&filterType=%s&fields=%s&filterValues=%s&batchSize=%s",
                baseUrl, accessToken, LEAD_FILTER_TYPE, LEAD_FIELDS, filterValues, READ_BATCH_SIZE);
        String nextPageToken = "";

        do {
            String gmlUrl = getMultipleLeadsUrl;

            // Append paging token to Get Multiple Leads by Filter Type URL
            if (nextPageToken.length() > 0) {
                gmlUrl = String.format("%s&nextPageToken=%s", getMultipleLeadsUrl, nextPageToken);
            }

            // Call Get Multiple Leads by Filter Type API to retrieve lead data
            JsonObject multipleLeadsObj = JsonObject.readFrom(getData(gmlUrl));
            if (multipleLeadsObj.get("success").asBoolean()) {
                if (multipleLeadsObj.get("result") != null) {
                    JsonArray multipleLeadsResultAry = multipleLeadsObj.get("result").asArray();

                    // Iterate through lead data
                    for (JsonValue leadResultObj : multipleLeadsResultAry) {
                        int leadId = leadResultObj.asObject().get("id").asInt();

                        // Join activity data with lead fields of interest (firstName, lastName, email)
                        List leadLst = activitiesMap.get(leadId);
                        for (JsonObject leadObj : leadLst) {
                            leadObj.add("firstName", leadResultObj.asObject().get("firstName").asString());
                            leadObj.add("lastName", leadResultObj.asObject().get("lastName").asString());
                            leadObj.add("email", leadResultObj.asObject().get("email").asString());
                        }
                    }
                }
            }

            nextPageToken = "";
            if (multipleLeadsObj.asObject().get("nextPageToken") != null) {
                nextPageToken = multipleLeadsObj.get("nextPageToken").asString();
            }
        } while (nextPageToken.length() > 0);

        // Now place activity data into an array of JSON objects
        JsonArray activitiesAry = new JsonArray();
        for (Map.Entry<Integer, List> activity : activitiesMap.entrySet()) {
            int leadId = activity.getKey();
            for (JsonObject leadObj : activity.getValue()) {
                // do something with leadId and each leadObj
                leadObj.add("leadId", leadId);
                activitiesAry.add(leadObj);
            }
        }

        // Print out result objects
        JsonObject result = new JsonObject();
        result.add("result", activitiesAry);
        System.out.println(result);

        System.exit(0);
    }

    // Perform HTTP GET request
    private static String getData(String endpoint) {
        String data = "";
        try {
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("GET");
            urlConn.setAllowUserInteraction(false);
            urlConn.setDoOutput(true);
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    private static String convertStreamToString(InputStream inputStream) {
        try {
            return new Scanner(inputStream).useDelimiter("A").next();
        } catch (NoSuchElementException e) {
            return "";
        }
    }
}
```

作業は以上です。ハッピーコーディング！

Posted on _2015-11-20_ by _David_

## SoundCloud Player とMunchkin API の統合

SoundCloud は、意欲的なインディーロックアーティストから音楽業界のトップ EDM アーティスト、ストーリーテリングのポッドキャストまで、あらゆる要素に対応する豊富な分析と機能を備えた、信じられないほどのオーディオホスティングプラットフォームを提供します。 プラットフォームの信じられないほどのネイティブ機能に加えて、データを移動し、リスニング動作を追跡するためのワールドクラスの API プログラムが付属しています。 これは特にポッドキャスターに便利で、再生、一時停止、共有などの特定のリスニングアクションを、スクリプトやオーディオの特定のコンテンツに関連付けることができます。 今日は、[SoundCloud の Widget API](https://developers.soundcloud.com/docs/api/html5-widget) を活用して、Marketoでこれらのアクティビティを送信およびトラッキングする方法について説明します。 まず、リードのアクティビティログインMarketoに記録されるMunchkin アクティビティの生成について見てみましょう。 最も基本的には、Munchkin.munchkinFunction を呼び出し、「visitWebPage」を最初の引数として渡します。 これにより、Marketoを使用して web ページ訪問アクティビティがログに記録され、メソッドに渡した任意の URL とクエリ文字列データが記録されます。 2 番目の引数は、データを含んだJavaScript オブジェクトを受け入れます。このオブジェクトには、「url」と「params」という 2 つのメンバーがあり、両方の文字列を持っています。 URL メンバーはMarketoのアクティビティの web ページに対応し、params はクエリ文字列に対応します。 この目的のために、URL を SoundCloud 関連のアクション「soundCloudInteraction」の識別子として使用し、パラメーターには特定のアクティビティに関する追加データを含めます。 各アクションの追跡に使用する関数を次に示します。

```javascript
var trackActivity = function(action){

    //set action param to be the string passed to the function
    var qs = "action=" + action;

    //use getCurrentSound callback to get the name of the current track
    soundCloudMunchkin.widget.getCurrentSound(function(currentSound){

        //add it to our querystring
        qs = qs + "&sound=" + currentSound.title;

        //use the getPosition callback to get the position of the track in ms
        soundCloudMunchkin.widget.getPosition(function(position){

            //add it to the querystring
            qs = qs + "&position=" + position;

            //assemble our data object for the munchkin activity
            var dataObject = {
                "url": "soundCloudInteraction",
                "params": qs
            }

            //call the munchkinFunction to submit the activity
            Munchkin.munchkinFunction("visitWebPage", dataObject);
        });
    });
}
```

標準の SoundCloud ウィジェットは iframe に埋め込まれているため、ウィジェットは POST メッセージを使用して通信し、currentSound メソッドと getPosition メソッドで見ることができるように、コールバックを使用してデータを取得する必要があります。 SoundCloud Widget API は、Player 内の個々のイベントに応答してそれらをJavaScriptに送信するために使用できる、Marketo コールバックのセットを提供します。 関心のあるイベントは、ユーザーがリッスンしている内容、ユーザーがリッスンする時間、ユーザーとのインタラクションです。そのため、次のイベントを見ています。

* PLAY
* PAUSE
* 終了
* シーク
* CLICK_DOWNLOAD
* CLICK_BUY
* OPEN_SHARE_PANEL

また、ウィジェットの bind （） メソッドを使用して、これらの各イベントにコールバックを追加する必要があります。 次に例を 1 つ示します。

```javascript
widget.bind(SC.Widget.Events.PLAY, function(){
    soundCloudMunchkin.trackPlay();
});
```

これにより、トラックが再生されるたびに、trackPlay メソッドを実行して、現在のトラックに関するデータを含むイベントをMarketoに送信します。 完全なスクリプトは [ こちら ](https://gist.github.com/kelkingtron/6750bb07c1397d93d9c7#file-soundcloudmunchkin-js) にあります。 soundCloudMunchkin オブジェクトには init メソッドがあり、このメソッドは SoundCloud ウィジェットオブジェクトを唯一の引数として受け入れ、トラッキングメソッドを関連するコールバックにバインドし、Marketoまでアクティビティを追跡するようにウィジェットを設定します。 [Munchkin コード ](/help/javascript-api/lead-tracking.md) と [SoundCloud API ライブラリ ](https://w.soundcloud.com/player/api.js) が読み込まれている必要があります。 実際の SoundCloud ウィジェットを埋め込むだけでなく、すべてを初期化する必要もあります。

```javascript
window.onload=function(){
var iframe = document.getElementById(iframeId);
    if(iframe) {
        widget = SC.Widget(iframe);
        soundCloudMunchkin.init(widget);
    };
};
```

Posted on _2015-12-21_ by _Kenny_

## RTP と EU 電子プライバシー指令

この投稿では、RTP を使用して、トラッキング中の web サイト訪問者に通知する方法、またはヨーロッパの訪問者のトラッキングを自動的に無効にする方法を説明します。 2012 年以降、ヨーロッパの訪問者が利用できるすべてのウェブサイトは、EU E-Privacy Directive に準拠する必要があります。 2011 年に施行された新しい法律では、ユーザーの知識と同意なしにユーザーのコンピューターに識別情報が保存されることを防ぎます。 Cookie またはその他のテクノロジーを不必要なトラッキングに使用している場合は、次の操作を行う必要があります。

1. トラッキングテクノロジーが使用されていることをユーザーに伝えます。
1. これらのテクノロジーを使用する理由を説明します。
1. その技術を使用する前にユーザーの同意を得て、いつでも許可を取り消すことができます。

Posted on _1970-01-01_ by _Yanir_

## AP を使用したMarketoのお客様および見込み客情報の更新

顧客情報や見込み客情報の更新に独自のシステムを使用するシナリオがあります。 マーケティングチームは、マーケティングキャンペーンで使用する最も正確なレコードのシステムを実現するために、それらの更新をMarketoに反映したいと考えています。 以下の方法を使用すると、Marketoへの定期的なアップロードを設定して、独自のシステムで変更されたデータでMarketoの連絡先情報を更新することができます。 次の図は、設定された定期的タイマーで行われる API 呼び出しを示しています。 定期タイマーがトリガーされると、クライアントロジックはまず更新された連絡先を独自システムから取得します。 これを行う方法は、API または独自システムからのデータ書き出しを使用して、システムによって異なります。 更新された連絡先情報が取得されると実行されるMarketo API について詳しく説明します。 syncMultipleLeads のSOAP リクエスト :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:paramsSyncMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <leadRecordList>
    <leadRecord>
      <Email>henry@superstar.com</Email>
      <ns2:leadAttributeList>
        <attribute>
          <attrName>FirstName</attrName>
          <attrValue>Henry</attrValue>
        </attribute>
        <attribute>
          <attrName>LastName</attrName>
          <attrValue>Adams</attrValue>
        </attribute>
        <attribute>
          <attrName>Title</attrName>
          <attrValue>Director of Demand Generation</attrValue>
        </attribute>
      </ns2:leadAttributeList>
    </leadRecord>
    <leadRecord>
      <Email>ssmith@gmail.com</Email>
      <ns2:leadAttributeList>
        <attribute>
          <attrName>FirstName</attrName>
          <attrValue>Suzie</attrValue>
        </attribute>
        <attribute>
          <attrName>LastName</attrName>
          <attrValue>Smith</attrValue>
        </attribute>
        <attribute>
          <attrName>Title</attrName>
          <attrValue>VP Marketing</attrValue>
        </attribute>
      </ns2:leadAttributeList>
    </leadRecord>
  </leadRecordList>
  <dedupEnabled>true</dedupEnabled>
</ns2:paramsSyncMultipleLeads>
```

syncMultilpeLeads からのSOAPの応答：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:successSyncMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <result>
    <syncStatusList>
      <syncStatus>
        <leadId>1094593</leadId>
        <status>UPDATED</status>
        <error xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
      </syncStatus>
      <syncStatus>
        <leadId>1094594</leadId>
        <status>UPDATED</status>
        <error xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
      </syncStatus>
    </syncStatusList>
  </result>
</ns2:successSyncMultipleLeads>
```

`syncMultipleLeads` はアップサート操作を実行します。 送信されたメールアドレスに基づいてMarketo内に連絡先が既に存在する場合、属性は更新されます。 連絡先が存在しない場合は作成されます。 `syncMultipleLeads` からの応答は、送信された各連絡先のステータスを返します。 `<attrName/>` 内の `<leadAttributeList/>` の値は、そのMarketo サブスクリプション用に定義されたSOAP API 名と一致する必要があります。 フィールド名を書き出すと、Marketo管理パネルの「フィールド管理」セクションでSOAP API 名を確認できます。

上記のシナリオを実行する以下のサンプル Java プログラムを参照してください。

```java
 import com.marketo.mktows.\*;
import java.net.URL;
import javax.xml.namespace.QName;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;
import java.util.\*;

public class SyncMultipleLeadsExample {

  public static void main(String[] args) {

    try {
      URL marketoSoapEndPoint = new URL("CHANGE ME" + "?WSDL");
      String marketoUserId = "CHANGE ME";
      String marketoSecretKey = "CHANGE ME";

      QName serviceName = new QName("http://www.marketo.com/mktows/", "MktMktowsApiService");
      MktMktowsApiService service = new MktMktowsApiService(marketoSoapEndPoint, serviceName);
      MktowsPort port = service.getMktowsApiSoapPort();

      // Create Signature
      DateFormat df = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
      String text = df.format(new Date());
      String requestTimestamp = text.substring(0, 22) + ":" + text.substring(22);
      String encryptString = requestTimestamp + marketoUserId ;

      SecretKeySpec secretKey = new SecretKeySpec(marketoSecretKey.getBytes(), "HmacSHA1");
      Mac mac = Mac.getInstance("HmacSHA1");
      mac.init(secretKey);
      byte[] rawHmac = mac.doFinal(encryptString.getBytes());
      char[] hexChars = Hex.encodeHex(rawHmac);
      String signature = new String(hexChars);

      // Set Authentication Header
      AuthenticationHeader header = new AuthenticationHeader();
      header.setMktowsUserId(marketoUserId);
      header.setRequestTimestamp(requestTimestamp);
      header.setRequestSignature(signature);

      // Create Request
      ParamsSyncMultipleLeads request = new ParamsSyncMultipleLeads();

      ObjectFactory objectFactory = new ObjectFactory();

      JAXBElement dedup = objectFactory.createParamsSyncMultipleLeadsDedupEnabled(true);
      request.setDedupEnabled(dedup);

      // The list of contacts defined here would be retrieved from the proprietary system
      Contact contact = new Contact("Henry","Adams","henry@superstar.com", "Director of Demand Generation");
      Contact contact2 = new Contact("Suzie","Smith","ssmith@gmail.com", "VP Marketing");

      ArrayList updatedContacts = new ArrayList();
      updatedContacts.add(contact);
      updatedContacts.add(contact2);

      ArrayOfLeadRecord arrayOfLeadRecords = new ArrayOfLeadRecord();

      Iterator it = updatedContacts.iterator();
      while(it.hasNext())
      {
        Contact c = it.next();

        LeadRecord leadRec = new LeadRecord();

        JAXBElement email = objectFactory.createLeadRecordEmail(c.email);
        leadRec.setEmail(email);

        Attribute attr1 = new Attribute();
        attr1.setAttrName("FirstName");
        attr1.setAttrValue(c.fname);

        Attribute attr2 = new Attribute();
        attr2.setAttrName("LastName");
        attr2.setAttrValue(c.lname);

        Attribute attr3 = new Attribute();
        attr3.setAttrName("Title");
        attr3.setAttrValue(c.title);

        ArrayOfAttribute aoa = new ArrayOfAttribute();
        aoa.getAttributes().add(attr1);
        aoa.getAttributes().add(attr2);
        aoa.getAttributes().add(attr3);

        QName qname = new QName("http://www.marketo.com/mktows/", "leadAttributeList");
        JAXBElement attrList = new JAXBElement(qname, ArrayOfAttribute.class, aoa);

        leadRec.setLeadAttributeList(attrList);
        arrayOfLeadRecords.getLeadRecords().add(leadRec);

      }

      request.setLeadRecordList(arrayOfLeadRecords);

      JAXBContext context = JAXBContext.newInstance(SuccessSyncMultipleLeads.class);
      Marshaller m = context.createMarshaller();
      m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
      m.marshal(request, System.out);

      SuccessSyncMultipleLeads result = port.syncMultipleLeads(request, header);

      m.marshal(result, System.out);
    }

    catch(Exception e) {
      e.printStackTrace();
    }
  }

  public static class Contact {
    public String fname, lname, email, title;

      public Contact(String fname, String lname, String email, String title) {
          this.fname = fname;
          this.lname = lname;
          this.email = email;
          this.title = title;
      }
  }
}
```

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _2014-03-24_ by _Travis Kaufman_

## API を使用したMarketoからのトランザクションメールの送信

Marketo UI を使用して既存のスマートキャンペーンを作成する必要があります。 また、メールの受信者がMarketoに存在する必要もあります。 そのため、requestCampaign API を呼び出す前に、[getLead API] （/help/soap-api/getlead.mdを使用して、メールがMarketoに存在するかどうかを確認します。 requestCampaign API を使用して呼び出しを行った後、Marketoでスマートキャンペーンが実行されたかどうかを確認することで、呼び出しを確定できます。 最初に、スマートキャンペーンの作成方法、2 番目に、API を使用してキャンペーンを送信するトリガーの設定方法、3 番目に、フローアクションの一部としてメールを定義する方法、4 番目に、このキャンペーンを実行するために使用するコードサンプルを示します。
**Marketoで新しいスマートキャンペーンを作成する方法** Marketoのスマートキャンペーンは、すべてのマーケティングアクティビティを実行します。 連絡先のスマートリストに対して実行する一連の自動アクションを設定できます。 トランザクションメールを送信する場合は、以下に示すように、API を使用してメールを送信するように、キャンペーンでトリガーを設定します。 まず、スマートキャンペーンを設定します。 1. マーケティングアクティビティで、プログラムを選択し、「新規」ドロップダウンで「新規ローカルアセット」をクリックします。

1. 「スマートキャンペーン」をクリック
1. スマートキャンペーン名を入力し、「作成」をクリックします。

**スマートキャンペーンにトリガーを追加** スマートキャンペーンにトリガーを追加すると、ライブイベント（この場合は [requestCampaign API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/triggerCampaignUsingPOST) を介したリクエスト）に基づいて、スマートキャンペーンを 1 人のユーザーに対して一度に実行できます。 1. 「キャンペーンがリクエストされました」トリガーを検索して、キャンバスにドラッグ&amp;ドロップします。

1. トリガーで、「is」と「Web サービス API」を選択します。

**キャンペーンでメールフローアクションを作成する方法** メールとスマートキャンペーンを関連付けると、マーケターはメールの外観を管理でき、サードパーティアプリケーションでメールの受信者とタイミングを決定できるようになります。 メールを新しいローカルアセットとして作成した後、キャンペーンのフローアクションとして設定できます。  送信するメールを探して選択します。

**requestCampaign API を呼び出すコードサンプル** Marketo インターフェイスでキャンペーンとトリガーを設定したら、API を使用してメールを送信する方法を示します。 最初のサンプルは XML リクエストで、2 番目は XML 応答で、最後のサンプルは XML リクエストの生成に使用できる Java コードサンプルです。 また、`requestCampaign` API を呼び出す際に使用するキャンペーン ID を見つける方法についても説明します。
また、API 呼び出しでは、事前にMarketo キャンペーンの ID を知っておく必要があります。 次のいずれかの方法を使用して、キャンペーン ID を決定できます。1. [getCampaignsForSource](/help/soap-api/getcampaignsforsource.md) API 1 を使用します。 ブラウザーでMarketo キャンペーンを開き、URL アドレスバーを確認します。 キャンペーン ID （4 桁の整数で表されます）は、「SC」の直後にあります。 たとえば、`<https://app-stage.marketo.com/#SC**1025**A1>` のように設定します。太字で示した部分は、キャンペーン ID 「1025」です。 SOAP `requestCampaign` のリクエスト

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809939944BFABAE58E5D27</mktowsUserId><requestSignature>48397ad47b71a1439f13a51eea3137df46441979</requestSignature><requestTimestamp>2013-08-01T12:31:14-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsRequestCampaign>
      <source>MKTOWS</source>
      <campaignId>4496</campaignId>
      <leadList>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>lead@company.com</keyValue>
        </leadKey>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>anotherlead@company.com</keyValue>
        </leadKey>
      </leadList>
    </ns1:paramsRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

requestCampaign に対するSOAP応答

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successRequestCampaign>
      <result>
        <success>true</success>
      </result>
    </ns1:successRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

上記のシナリオを実行する Java プログラムのサンプルを以下に示します。

```java
import com.marketo.mktows.*;
import java.net.URL;
import javax.xml.namespace.QName;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;


public class RequestCampaign {

    public static void main(String[] args) {
        System.out.println("Executing Request Campaign");
        try {
            URL marketoSoapEndPoint = new URL("CHANGE ME" + "?WSDL");
            String marketoUserId = "CHANGE ME";
            String marketoSecretKey = "CHANGE ME";

            QName serviceName = new QName("http://www.marketo.com/mktows/", "MktMktowsApiService");
            MktMktowsApiService service = new MktMktowsApiService(marketoSoapEndPoint, serviceName);
            MktowsPort port = service.getMktowsApiSoapPort();

            // Create Signature
            DateFormat df = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
            String text = df.format(new Date());
            String requestTimestamp = text.substring(0, 22) + ":" + text.substring(22);
            String encryptString = requestTimestamp + marketoUserId ;

            SecretKeySpec secretKey = new SecretKeySpec(marketoSecretKey.getBytes(), "HmacSHA1");
            Mac mac = Mac.getInstance("HmacSHA1");
            mac.init(secretKey);
            byte[] rawHmac = mac.doFinal(encryptString.getBytes());
            char[] hexChars = Hex.encodeHex(rawHmac);
            String signature = new String(hexChars);

            // Set Authentication Header
            AuthenticationHeader header = new AuthenticationHeader();
            header.setMktowsUserId(marketoUserId);
            header.setRequestTimestamp(requestTimestamp);
            header.setRequestSignature(signature);

            // Create Request
            ParamsRequestCampaign request = new ParamsRequestCampaign();

            request.setSource(ReqCampSourceType.MKTOWS);

            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Integer> campaignId = objectFactory.createParamsRequestCampaignCampaignId(4496);
            request.setCampaignId(campaignId);

            ArrayOfLeadKey leadKeyList = new ArrayOfLeadKey();
            LeadKey key = new LeadKey();
            key.setKeyType(LeadKeyRef.EMAIL);
            key.setKeyValue("lead@company.com");

            LeadKey key2 = new LeadKey();
            key2.setKeyType(LeadKeyRef.EMAIL);
            key2.setKeyValue("anotherlead@company.com");

            leadKeyList.getLeadKeies().add(key);
            leadKeyList.getLeadKeies().add(key2);

            JAXBElement<ArrayOfLeadKey> arrayOfLeadKey = objectFactory.createParamsRequestCampaignLeadList(leadKeyList);
            request.setLeadList(arrayOfLeadKey);

            SuccessRequestCampaign result = port.requestCampaign(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessRequestCampaign.class);
            Marshaller m = context.createMarshaller();
            m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
            m.marshal(result, System.out);

        }
        catch(Exception e) {
            e.printStackTrace();
        }
    }
}
```

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _2014-03-27_ by _Murta_

## API を使用したMarketoからの動的コンテンツを含むメールの送信

コールセンターへのフォローアップメールを自動化するとします。 サポート担当者がお客様と話した後で、お客様に連絡を取っていただいたお礼のメールを自動的に送信したいと考えています。 これをさらに一歩進めて、CRM で追跡している顧客と話し合った特定の会話トピックを含めたいとします。 requestCampaign SOAP API を使用してMarketoからこれを実行し、動的コンテンツを含むメールを送信できます。 requestCampaign API を使用すると、リードまたはリードを渡すことができます。 また、既存のキャンペーンで使用できるプログラムトークンを渡して、動的コンテンツを送信することもできます。 requestCampaign SOAP API では、メール受信者がMarketoに存在する必要があります。 そのため、requestCampaign API を呼び出す前に、[getLead API](/help/soap-api/getlead.md) を使用して、メールがMarketoに存在するかどうかを確認します。 最初に、スマートキャンペーンの作成方法、2 番目に、API を使用してキャンペーンを送信するトリガーの設定方法、3 番目に、プログラムトークンを使用して動的コンテンツを受け入れるメールの作成方法、4 番目に、フローアクションの一部としてメールを定義する方法、5 番目にこのキャンペーンを実行するために使用するコードサンプルを示します。 **Marketoで新しいスマートキャンペーンを作成する方法** Marketoのスマートキャンペーンは、すべてのマーケティングアクティビティを実行します。 連絡先のスマートリストに対して実行する一連の自動アクションを設定できます。 トランザクションメールを送信する場合は、以下に示すように、API を使用してメールを送信するように、キャンペーンでトリガーを設定します。 まず、スマートキャンペーンを設定します。 1. マーケティングアクティビティで、プログラムを選択し、「新規」ドロップダウンで「新規ローカルアセット」をクリックします。

1. 「スマートキャンペーン」をクリック
1. スマートキャンペーン名を入力し、「作成 **スマートキャンペーンにトリガーを追加**」をクリックします。スマートキャンペーンにトリガーを追加すると、ライブイベントに基づいてスマートキャンペーンを一度に 1 人のユーザーに対して実行できます。この場合、[requestCampaign API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/triggerCampaignUsingPOST) を使用したリクエストです。
1. 「キャンペーンがリクエストされました」トリガーを検索し、キャンバスにドラッグ&amp;ドロップします。
1. トリガーで、「is」と「Web サービス API」を選択します。

**API を使用して動的コンテンツを渡す方法** Marketoでは、マイトークンはプログラムで使用できる変数です。 マイトークンを使用すると、プログラムに関する情報を 1 か所で入力し、その情報を指定した値に置き換え、アプリケーションの他の部分（メールテンプレートなど）でこの情報を取得できます。 requestCampaign SOAP API を使用すると、既存のトークンを上書きするプログラムトークンの配列を渡すことができます。 キャンペーンの実行後、トークンは破棄されます。 マイトークンは、キャンペーンフォルダーレベルまたはプログラムレベルで作成します。 キャンペーンフォルダーレベルのマイトークンは、Campaign フォルダー内に含まれるすべてのプログラムに継承されます。 キャンペーンフォルダーレベルでマイトークンを作成すると、継承された値をプログラムレベルで上書きできます。 例えば、キャンペーンフォルダーレベルでプログラム日とプログラム説明のトークンを定義した場合、個々のプログラムレベルでこれらの値を上書きできます。

その方法を次に示します。 1. マーケティングアクティビティ ツリーで、トークンを作成する Campaign フォルダーまたはプログラムを選択します。 上部のメニューバーから、「マイトークン」を選択します。 次に、マイトークン キャンバスが表示されます。 右側のツリーからトークン・タイプ（この場合は「Text」）をキャンバスにドラッグします。 「トークン名」フィールドで「マイトークン」をハイライト表示し、一意のトークン名（この場合は「my.conversationtopic」）を入力します。 「値」フィールドに、トークンに関連する値を入力します。この場合は「Thank you for calling us today」となります。 API を使用することで、デフォルトのマイトークン値を上書きします。 「保存」をクリックして、カスタムトークンを保存します。  1. 「新規」をクリックして新規メールを作成します。 次に、「新規ローカルAssets」をクリックし、「メール」を選択します。 次に、関連するフィールドに入力して、メールに名前を付けます。 メールのドラフトを作成する際に、トークン アイコンをクリックすると、メールにトークンが含まれます。 トークンを含むテンプレートメールを作成したので、次の手順でキャンペーンのフローアクションとしてメールを追加します。 そのため、API を使用してキャンペーンを呼び出すと、メールが送信されます。
**キャンペーンでメールフローアクションを作成する方法** メールとスマートキャンペーンを関連付けると、マーケターはメールの外観を管理でき、サードパーティアプリケーションでメールの受信者とタイミングを決定できるようになります。 メールを新しいローカルアセットとして作成した後、キャンペーンのフローアクションとして設定できます。 送信するメールを検索して選択します。
**requestCampaign API を呼び出すコードサンプル** Marketo インターフェイスでキャンペーンとトリガーを設定したら、API を使用してメールを送信する方法を示します。 最初のサンプルは XML リクエストで、2 番目は XML 応答で、最後のサンプルは XML リクエストの生成に使用できる Java コードサンプルです。 また、requestCampaign API を呼び出す際に使用するキャンペーン ID を見つける方法についても説明します。 また、API 呼び出しでは、事前にMarketo キャンペーンの ID を知っておく必要があります。 次のいずれかの方法を使用して、キャンペーン ID を決定できます。1. [getCampaignsForSource](/help/soap-api/getcampaignsforsource.md) API 1 を使用します。 ブラウザーでMarketo キャンペーンを開き、URL アドレスバーを確認します。 キャンペーン ID （4 桁の整数で表されます）は、「SC」の直後にあります。 たとえば、`<https://app-stage.marketo.com/#SC&#x200B;**1025**&#x200B;A1>` のように設定します。太字で示した部分は、キャンペーン ID 「1025」です。 requestCampaign のSOAP リクエスト

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809939944BFABAE58E5D27</mktowsUserId><requestSignature>48397ad47b71a1439f13a51eea3137df46441979</requestSignature><requestTimestamp>2013-08-01T12:31:14-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsRequestCampaign>
      <source>MKTOWS</source>
      <campaignId>4496</campaignId>
      <leadList>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>lead@company.com</keyValue>
        </leadKey>
      </leadList>
      <programTokenList>
        <attrib>
          <name>{{my.conversationtopic}}</name>
          <value>Thank you for calling about adding a line of service to your current plan.</value>
        </attrib>
      </programTokenList>
    </ns1:paramsRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

requestCampaign に対するSOAP応答

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successRequestCampaign>
      <result>
        <success>true</success>
      </result>
    </ns1:successRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

上記のシナリオを実行する Java プログラムのサンプルを以下に示します。

```java
import com.marketo.mktows.\*;
import java.net.URL;
import javax.xml.namespace.QName;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;


public class RequestCampaign {

    public static void main(String[] args) {
        System.out.println("Executing Request Campaign");
        try {
            URL marketoSoapEndPoint = new URL("CHANGE ME" + "?WSDL");
            String marketoUserId = "CHANGE ME";
            String marketoSecretKey = "CHANGE ME";

            QName serviceName = new QName("http://www.marketo.com/mktows/", "MktMktowsApiService");
            MktMktowsApiService service = new MktMktowsApiService(marketoSoapEndPoint, serviceName);
            MktowsPort port = service.getMktowsApiSoapPort();

            // Create Signature
            DateFormat df = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
            String text = df.format(new Date());
            String requestTimestamp = text.substring(0, 22) + ":" + text.substring(22);
            String encryptString = requestTimestamp + marketoUserId ;

            SecretKeySpec secretKey = new SecretKeySpec(marketoSecretKey.getBytes(), "HmacSHA1");
            Mac mac = Mac.getInstance("HmacSHA1");
            mac.init(secretKey);
            byte[] rawHmac = mac.doFinal(encryptString.getBytes());
            char[] hexChars = Hex.encodeHex(rawHmac);
            String signature = new String(hexChars);

            // Set Authentication Header
            AuthenticationHeader header = new AuthenticationHeader();
            header.setMktowsUserId(marketoUserId);
            header.setRequestTimestamp(requestTimestamp);
            header.setRequestSignature(signature);

            // Create Request
            ParamsRequestCampaign request = new ParamsRequestCampaign();

            request.setSource(ReqCampSourceType.MKTOWS);

            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Integer> campaignId = objectFactory.createParamsRequestCampaignCampaignId(4496);
            request.setCampaignId(campaignId);

            ArrayOfLeadKey leadKeyList = new ArrayOfLeadKey();
            LeadKey key = new LeadKey();
            key.setKeyType(LeadKeyRef.EMAIL);
            key.setKeyValue("lead@company.com");

            leadKeyList.getLeadKeies().add(key);

            JAXBElement<ArrayOfLeadKey> arrayOfLeadKey = objectFactory.createParamsRequestCampaignLeadList(leadKeyList);
            request.setLeadList(arrayOfLeadKey);

            ArrayOfAttrib aoa = new ArrayOfAttrib();

            Attrib attrib = new Attrib();
            attrib.setName("{{my.conversationtopic}}");
            attrib.setValue("Thank you for calling about adding a line of service to your current plan.");

            aoa.getAttribs().add(attrib);

            JAXBElement<ArrayOfAttrib> arrayOfAttrib = objectFactory.createParamsRequestCampaignProgramTokenList(aoa);
            request.setProgramTokenList(arrayOfAttrib);

            SuccessRequestCampaign result = port.requestCampaign(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessRequestCampaign.class);
            Marshaller m = context.createMarshaller();
            m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
            m.marshal(result, System.out);

        }
        catch(Exception e) {
            e.printStackTrace();
        }
    }
}
```

requestCampaign API を使用して呼び出しを行った後、Marketoでスマートキャンペーンが実行されたかどうかを確認することで、呼び出しを確定できます。

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

Posted on _2014-04-03_ by _Murta_

## ビジネスロジックに基づいた匿名の訪問者アクティビティのキャプチャ

会社のブログ上で特定の投稿にアクセスしたユーザーを追跡するとします。 投稿を訪問したユーザーの合計数のうち、少なくとも 5 秒を費やしてページをスクロールして、興味を示すユーザーのみを追跡したい場合を考えてみましょう。 匿名ユーザーの場合は、このイベントを使用してMarketoに新しいリードを作成し、既知のユーザーの場合は、このイベントを使用してリードアクティビティを更新します。 これは、web サイトで [Munchkin トラッキングコード ](/help/javascript-api/lead-tracking.md) を使用することで実現できます。 cookie を設定していないユーザーがMunchkin トラッキングコードを使用しているページに移動すると、ユーザーのブラウザーで新しい cookie が作成され、新しい匿名リードがMarketoで作成されます。 ユーザーが既に Cooked で、そのユーザーがMarketoの既存のリードである場合、ページへの訪問は、Marketoのそのユーザーのアクティビティログに記録されます。 最初に、MarketoでMunchkin トラッキングコードを生成する方法、2 番目に、特定の条件が満たされた場合にのみトリガーされるようにMunchkin サンプルコードを変更する方法、3 番目に、匿名ユーザーからのページ訪問がMarketoに記録されたことを確認する方法を説明します。

**Munchkin トラッキングコードの生成方法**&#x200B;Munchkin トラッキングコードを使用すると、web サイトへの訪問を追跡できます。 以下に示すMunchkin コードには 3 つのタイプがありますが、この例では、非同期Munchkin トラッキングコードを使用します。 A） シンプル：コードは最も少ないですが、web ページの読み込み時間に対して最適化されません。 このコードは、web ページが読み込まれるたびに jQuery ライブラリを読み込みます。 B）非同期：Web ページの読み込み時間を短縮します。 このコードは、jQuery ライブラリが既に存在するかどうかを確認し、存在しない場合は読み込み、Web ページの残りの部分が読み込まれると、トラッキングコードの実行に使用します。 C）非同期 jQuery:Web ページの読み込み時間を短縮し、システムパフォーマンスも向上させます。 このコードは、jQuery が既に存在することを前提としていますが、読み込むためにはをチェックしません。 1. アプリの右上にある [ 管理者 ] をクリックします。  1.左側のツリーでMunchkinをクリックします。  1. 「コードタイプを追跡」で「非同期」を選択します。 1. 「JavaScript トラッキングコード」をクリックしてコピーし、Web サイトに配置します。
**Cookie ユーザーおよびトラッキングイベントのコードサンプル** Web ページの `</body>` タグの直前にトラッキングコードを配置します。 Marketoで作成されたランディングページにはトラッキングコードが自動的に含まれるので、このコードを適用する必要はありません。 このコードサンプルでは、スクリプトの読み込み後にMunchkin API を呼び出します。

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      Munchkin.init('XXX-XXX-XXX');
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin.js';
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName('head')[0].appendChild(s);
})();
</script>
```

このコードサンプルでは、ユーザーがページに 5 秒間滞在し、さらに 500 ピクセル下にスクロールした後で、Munchkin API を呼び出します。

```javascript
<script src="https://code.jquery.com/jquery-2.1.0.min.js"></script>
<script type="text/javascript">
$(function(){
 setTimeout(function(){
  $(window).scroll(function() {
      var y_scroll_position = window.pageYOffset;
      var scroll_position = 500; //Sets number of pixels user must scroll to be tracked

  if(y_scroll_position > scroll_position) {
  //Munchkin tracking code
   (function() {
     var didInit = false;
     function initMunchkin() {
      if(didInit === false) {
        didInit = true;
        Munchkin.init('XXX-XXX-XXX');
      }
     }

     var s = document.createElement('script');
     s.type = 'text/javascript';
     s.async = true;
    s.src = '//munchkin.marketo.net/munchkin.js';
     s.onreadystatechange = function() {
      if (this.readyState == 'complete' || this.readyState == 'loaded') {
          initMunchkin();
      }
     };
     s.onload = initMunchkin;
     document.getElementsByTagName('head')[0].appendChild(s);
   })();
   }
 },5000); //Sets time delay before tracking user
});
</script>
```

**匿名ユーザーによるページ訪問がMarketoに記録されたことを確認する方法**

1. 上部メニューで「Analytics」をクリックし、「新しいレポート」をクリックします。 レポートタイプとして「Web ページアクティビティ」を選択し、レポートに名前を付けます。
1. レポートを作成したら、「スマート・リスト」をクリックします。 次に、右側のボックスから「訪問済み web ページ」フィルターを選択します。 Munchkin トラッキングコードを配置する web ページを入力します。
1. 「設定」をクリックします。 ISP から匿名訪問者を選択して、オプションを表示に変更します。
1. レポートをクリックします。 選択した web ページでアクティビティが追跡されているのが確認できます。
1. リードレコードをダブルクリックすると、アクティビティログが表示され、匿名ユーザーが訪問した特定のページを確認できます。

この記事には、カスタム統合の実装に使用するコードが含まれています。 カスタマイズされた特性により、Marketo テクニカルサポートチームはカスタム作業のトラブルシューティングを行うことができません。 適切な技術的経験がなく、経験豊富な開発者にアクセスすることなく、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-04-17_ by _Murta_

## RTP を使用したローカル電話番号の動的な変更

Personalizationがすべてです – 私たちは長い時間前にこれを考え出しました。 とはいえ、私が迅速な支援を必要とするたびに、関連する地域電話番号を web サイトで見つけるのが非常に難しいことは、まだ驚くべきことです。 [Marketo Real-Time Personalization](https://business.adobe.com/products/marketo/content-personalization.html) （RTP）が <https://business.adobe.com/products/marketo/adobe-marketo.html> にインストールされています。 [RTP Visitor API](/help/javascript-api/web-personalization.md) を活用して、web サイトの様々なセクションで web 訪問者に表示される電話番号を動的に変更できます。 すごい。信じられますか？ この魔法の使い方 まず、[ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) に説明されているように、Web サイトに RTP をインストールする必要があります。 次に、以下の手順に従って、web サイトにJavaScript コードを実装します。

1. 国際電話番号を **defaultPhone** 設定に挿入します
1. HTML要素 ID を **divIds** 設定に挿入します
1. 電話番号をモバイルブラウザーのクリックトゥコールリンクにする場合は、「**mobileLink**」設定を **true** に設定します。
1. **cityPhone**、**statePhone**、および **countryPhone** 設定の電話番号を使用して、様々な場所をマッピングします

例えば、構成設定のサンプル値を次に示します。

```json
  defaultPhone:"+1.503.608.4679", // Optional
  divIds:["phoneId1","phoneId2"],
  mobileLink: true,
  cityPhone: {
    "<a href="#">yanir</a>": ["San Mateo", "San Francisco"],
    "+353.1.242.3000": ["tel-aviv"]
  },
  statePhone: {
    "+1.650.376.2300": ["CA"],
    "+1.650.376.2302": ["OR"]
  },
  countryPhone: {
    "+1.650.376.2300": ["United States"],
    "+353.1.242.3000": ["Israel"]
  }
```

最後に、（上記の手順 2 の） **divIds** のいずれかの id に一致する id を含むHTML アンカータグを挿入します。 例えば、**divIds** に「phoneId1」を指定した場合、HTML アンカータグは次のようになります。

`<a href="tel:+1800229933" id="phoneId1">+1800229933</a>`

スクリプトは、この順序で一致があるかどうかを確認します。cityPhone/statePhone/countryPhone/defaultPhone 電話番号をテキストに置き換えることもできます（例：「Join our San Francisco User Group!」） またはHTMLのコードを参照し、地域や場所に基づいてコンテンツを動的に変更します。 これで、お試しいただくことができます。

```html
<a href="tel:+1800229933" id="phoneId1">+1800229933</a>
<script>
(function(a){
    rtp('get','visitor',function(yc){
        var location = yc.results.location;
        var loop = true;
        var phoneChanged = false;
        console.log(yc.results);
        function checkObj(obj){
            return Object.getOwnPropertyNames(obj).length >0;
        }
        function changePhone(p){
            d=a.divIds;
            for(i=0;i<d.length;i++){
                if(document.getElementById(d[i]) !== null){
                    document.getElementById(d[i]).innerHTML = p;
                    if(a.mobileLink){
                        document.getElementById(d[i]).href= "tel:" + p;
                    }
                    console.log(p);
                }
            }
            loop = false;
            phoneChanged = true;
        }
        function matchLocation(loc,objc){
            for (var key in objc) {
                for(i=0;i<objc[key].length && loop;i++){
                    if (!loop) { return true;};
                    val = objc[key][i];
                    //console.log(loc + location[loc] + " ? " + val);
                    if(location[loc].toLowerCase() === val.toLowerCase()){
                        changePhone(key);
                    }
                }
            }
        }
        if(checkObj(a.cityPhone)){
            matchLocation("city",a.cityPhone);
        }else if(checkObj(a.statePhone)){
            matchLocation("state",a.statePhone);
        }else if(checkObj(a.countryPhone)){
            matchLocation("country", a.countryPhone);
        }else if(!phoneChanged && a.defaultPhone.length > 0 ){
            changePhone(a.divId,a.defaultPhone);
        }
    });
})({
    defaultPhone:"",  //  [Optional] the number to show if visitor does not match the mapping below
    divIds:["phoneId1","Floater"],  //the phone HTML element ID, can be <div>, <a>, <span>, <p> etc.
    mobileLink: true,  //if you use click to call link (with href="tel:") you can also change its number

    cityPhone: {
        "<a href='#'>yanir</a>": ["San Mateo", "San Francisco"],
        "+353.1.242.3000": ["tel-aviv"]
    },
    statePhone: {
        "+1.650.376.2300": ["CA"],
        "+1.650.376.2302": ["OR"]
    },
    countryPhone: {
        "+1.650.376.2300": ["United States"],
        "+353.1.242.3000": ["Israel"]
    }
});
</script>
```

Posted on _2016-02-02_ by _Yanir_

## 2016 年冬の更新

### カスタムオブジェクト

* [ カスタムオブジェクト N:N 関係がサポートされるようになりました ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects)
   * リードレコードまたはアカウントレコードは、中間オブジェクトの定義を介したカスタムオブジェクトを介して多対多の関係を持つようになりました。 スタンドアロンのカスタムオブジェクトタイプを作成した後、スタンドアロンオブジェクトとリードまたはアカウントの両方へのリンクフィールドを使用して、中間オブジェクトタイプを作成できます。
   * この機能に対する新しい API 呼び出しはありませんが、API を通じてこれらの関係を活用するには、オブジェクト定義が正しく設定されている必要があります。
* `getLeadActivities` と `getLeadChanges` は、匿名リードのアクティビティを返さなくなります。 詳しくは、[ 次世代のMunchkin トラッキング FAQ](https://experienceleague.adobe.com/ja/docs/marketo/using/home) を参照してください

Posted on _2016-02-05_ by _Kenny_

## REST API を使用した 1 つのリードのアクティビティの取得

以下は、開発者コミュニティから繰り返し質問される質問です。

「個々のリードの過去のアクティビティのリストを取得するにはどうすればよいですか？」

最近まで、REST API を使用してこれを実行する簡単な方法はありませんでした。 しかし、今があります！ REST API の 2016 年冬リリースには、少し改善が含まれています。 [ リードを取得アクティビティ ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET) では、リード ID の指定に使用できる **leadIds** パラメーターを受け入れるようになりました。 **leadIds** パラメーターが指定されている場合、そのリード ID のアクティビティのみが返されます。 これは、リード ID フィルターと考えることができます。 複数のリード（最大 30）で結果をフィルターしたい場合、**leadIds** パラメーターにリード ID のコンマ区切りリストを指定することもできます。 これは、例えば、特定の会社のリードに対してアクティビティを制限する場合に便利です。 **例** 以下は、[leadIds](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET) パラメーターを含む **リードアクティビティの取得** に対するサンプルリクエストです。 **leadIds** パラメーターに値「50」を指定しました。これは、Marketo インスタンス内の任意のリードに対応します。 activityTypeIds パラメーターに値「129」を指定しました。これは、Marketo インスタンスの「モバイルアプリセッション」アクティビティに対応しています。

`<https://123-abc-456.mktorest.com/rest/v1/activities.json?leadIds=50&activityTypeIds=129&nextPageToken=WQV2VQVPPCKHC6AQYVK7JDSA3J4SMAZRQO4RKIXCEMLFCM2APRSQ====>`

上記のリクエストからの応答の抜粋を以下に示します。 ご覧のように、「leadId」が 50 で「activityTypeId」が 129 の結果オブジェクトのみが含まれています。

```json
{
    "id": 846,
    "leadId": 50,
    "activityDate": "2015-04-06T21:58:59Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 7
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
{
    "id": 879,
    "leadId": 50,
    "activityDate": "2015-04-07T00:45:11Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 5
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
{
    "id": 1114,
    "leadId": 50,
    "activityDate": "2015-04-08T00:02:41Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 241
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
{
    "id": 1551,
    "leadId": 50,
    "activityDate": "2015-04-09T23:31:56Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 223
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
{
    "id": 1716,
    "leadId": 50,
    "activityDate": "2015-04-15T22:44:19Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 223
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
```

## Zapier を使用したMarketoおよび 500 を超えるアプリケーションとのシームレスな統合

これは、Marketo、プリンシパルソリューションコンサルタント、Philippe Delle Case からの投稿です。

### 目標

この記事では、Zapier のおかげで、Marketoを 500 を超える可能性のあるクラウドアプリと統合する方法を詳しく説明します。 そのために、Marketo用の Zapier コネクタをゼロから作成し、2 つの実用的な統合ユースケースを実装します。ユースケース 1:FullContact Card ReaderからMarketoへの一方向リードの統合

* FullContact モバイルカードReaderアプリで連絡先の名刺をスキャンすると、Marketoでリードが自動的に作成されます。
* 既存のリードをMarketoの静的リストに追加し、Google シートに自動的に追加されたリードを見つけます。
* Google シート内のリードを変更し、変更内容がMarketoに返されているのを確認します。

### 前提条件

**Zapier で無料アカウントにサインアップ**&#x200B;[Zapier](https://zapier.com/) は、プログラマーや IT リソースを必要とせずに、他のオンラインアプリ間のタスクを簡単に自動化できる web アプリ自動化サービスです。 簡単な概要は、[ こちら ](https://zapier.com/api/v4/helpdocs/category/redirect/what-is-zapier) を参照してください。 現在、Zapier は、マーケティング、CRM、CMS、カスタマーサポート、電子サイン、Formsなど、さまざまな分野で 500 を超えるアプリをサポートしています。 あるアプリと別のアプリの間の単一の統合は、Zap と呼ばれます。 サポートされている Web アプリの完全なリストについては、Zapier の [zapbook](https://zapier.com/apps) を確認してください。  無料アカウントに新規登録 [ こちら ](https://zapier.com/sign-up/)。 15 分ごとに実行される最大 100 個のタスク/月、5 個の ZAP、ZAP にアクセスできます。 もちろん、Zapier の有料プラン（基本、ビジネス、ビジネスプラスなど）に登録すると、さらに多くのプランを利用できます。

**管理者として、または提供された API ユーザーアカウントを使用してMarketo インスタンスにアクセスします** アドビの Zapier コネクタは、Marketo REST API を使用してリードデータをMarketoにプッシュします。 この API を使用するには、Marketo インスタンスの管理者が自分で作成できる API ユーザーとカスタムサービスが必要です。 そうでない場合は、管理者がそれらを提供する必要があります。 また、作成する Webhook もあり、Marketo管理者のみがアクセスできます。 Marketo API ユーザーとカスタムサービスの作成方法に関する詳しい手順については、[ こちら ](http://rest-api/custom-services/) を参照してください。 完了したら、Marketo REST API を呼び出すための次の資格情報が必要です：クライアント ID、クライアントの秘密鍵、Munchkin アカウント ID、Munchkin アカウント ID

Munchkin アカウント ID は、Munchkinまたは web サービスの管理画面から取得できます。 パターンは次のようになります。`000-XXX-000`  アクセストークンは 1 時間のみ有効なので、取得する必要はありません。 コネクタは、自動的にトークンを生成します。
**Google Docs、シート、スライドを使用した無料アカウントへのサインアップは、さまざまな種類のオンライン ドキュメントを作成し、他のユーザーとリアルタイムで作業し、それらをGoogle Drive Online に保存できる生産性向上アプリです。 このユースケースにはGoogle シートが必要です。 Google Docsの様々な機能と、Googleを使用したアカウントの作成については、[ こちら ](https://workspace.google.com/products/docs/) を参照してください。
**FullContact で無料アカウントにサインアップ** FullContact は、すべての連絡先を取り込み、ソーシャルプロファイル、写真、電子メール署名、会社情報などの変更を継続的に同期することで、最も重要な人物と完全につながることができます。 Zapier を含む 250 以上のウェブアプリにカードをスキャンできるモバイル名刺リーダーを提供します。 無料アカウントに新規登録できます [ こちら ](https://app.fullcontact.com/login)。 また、より多くの機能と容量を備えたプレミアム有料アカウントを購読することもできます。 モバイルアプリは、[Apple AppStore](https://apps.apple.com/us/app/fullcontact-business-card/id576780807) または [Google Play](https://play.google.com/store/apps/details?id=com.fullcontact.cardreader) からダウンロードできます。 FullContact Zap は [ こちら ](https://zapier.com/apps/contacts-plus/integrations) に記載されています。

### Marketo Connector for Zapier の実装

**Marketo アプリの作成** Zapier web インターフェイスから、開発者ポータルに移動します。 「**新しいアプリを追加**」をクリックし、少なくともタイトル（「Marketo」など）と説明を入力します。 ロゴはオプションですが、持っていてうれしいです。\ **認証** この節では、Marketo REST API 認証と認証設定に使用される様々なフィールドを宣言します。 最初に次のフィールドを作成します。

「認証設定」を編集します。

* 認証タイプ：セッション認証
* 認証マッピング：

  `{"access_token":"{{access_token}}"}`

* アクセストークン配置&#x200B;**:Querystring 内の** トークン

Marketo カスタムサービスを作成すると、クライアント ID とクライアント秘密鍵が使用可能になります。 クライアント ID とクライアントシークレットを使用して、REST API[ 認証 ](/help/rest-api/authentication.md) エンドポイントを介してアクセストークンを生成します。 その後、このアクセストークンを使用して、REST API に対して後続のリクエストを実行できます。 トークンは 1 時間後に有効期限が切れ、REST API の呼び出しを続行するには再度生成する必要があります。 セッショントークンの有効期限が切れるたびにカスタム認証スクリプトを実行できるので、認証タイプ = 「セッション認証」を選択しました。 このタイプの認証でのみ動作するこのメカニズムを実装する方法については、「スクリプティング API」の節で説明します。
**トリガー** Zapier トリガーは、データを Zapier に取り込むために使用します。 代わりにMarketo Webhook を利用するので、ユースケースには必要ありません。 ただし、Marketo コネクタの必須テストとして、ダミーのトリガーを記述する必要があります。 Marketo REST API[ 毎日の使用状況を取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getDailyUsageUsingGET) エンドポイントを呼び出すテストトリガーを作成します。 「**新規トリガーを追加**」をクリックしてウィザードを起動し、次のフィールドに入力します（記載されていないフィールドは空白のままにすることができます）。名前と説明

* 名前：テストトリガー
* キー：test_トリガー
* 説明：Marketo アプリケーションのテストトリガー
* 重要？ 未確認
* 隠れる？ チェック済み

トリガーフィールド

* None

データの取得元

* Data Source：ポーリング
* ポーリング URL: `https://{{munchkin_account_id}}.mktorest.com/rest/v1/stats/usage.json`

サンプル結果

* 空白のままにします

**トリガー設定の管理** をクリックし、ユーザーの資格情報の検証に使用するトリガーとして「テスト環境」を設定します。 **アクション** Zapier Zapier からデータを送信するためのアクションがあります。 Marketo REST API を呼び出して、Create_Update Lead Action を実装します。 このアクションにより、Marketo内に新しいリードを作成できます。リードが既に存在する場合は、送信された値を使用して更新されます。 重複除外には「email」フィールドを使用します。 「**新しいアクションを追加**」をクリックしてウィザードを起動し、次のフィールドに入力します（記載されていないフィールドは空白のままにすることができます）。名前と説明

* 名前：リードを作成_更新
* 名詞：リード
* キー：create-update-lead
* 説明：Marketo内で新しいリードを作成します。リードが既に存在する場合は、送信された値を使用して更新します
* 重要？ チェック済み
* 隠れる？ 未確認

アクションフィールド アクションフィールドは、ユーザーがデータをマッピングするフィールドです。 Marketoで更新できるすべてのデータを表しているので、独自のニーズに応じて慎重に選択してください。 Zapier には、Marketoで使用可能なすべてのフィールドをエンドユーザーに提供するオプションがありますが、これにより、使い捨てコネクタには必要なく、より多くのコードと複雑さが発生します。 例えば、次のフィールドを選択しました。

Marketo インスタンスにはリードパーティションがサービスにあるので、パーティション名はこのケースでは必須です。 それ以外の場合は省略される可能性があります。 同期するフィールドでないことをエンドユーザーが理解できるように、「入力」グループから分離しました。 「メモ」フィールドは、MarketoとSalesforceの同期から取得したものです。Marketo インスタンスに存在しない場合は使用しないでください。 フィールド「被呼び出し」は、Marketo インスタンスで作成されました。Marketo インスタンスにフィールドがない場合は使用しないでください。 もちろん、Marketoから必要なフィールドを選択できるようにすることが目標です。 最初は小さく、後で余分なフィールドを追加することをお勧めします。 データの送信先

* アクション エンドポイント URL: `https://{{munchkin_account_id}}.mktorest.com/rest/v1/leads.json`

サンプル結果

* 空白のままにします

### Zapier スクリプティング API

Zapier のスクリプト機能を使用すると、アプリの API と Zapier の間で交換されるリクエストと応答を操作できます。 HTTP リクエストは、送信される直前に変更することができ、Zapier がリクエストに対して何らかの処理を行う前にレスポンスを解析することができます。 Marketoで動作するように、カスタム「セッション認証」認証を完了する必要があります。 詳しくは、[ こちら ](https://zapier.com/developer/documentation/scripting/) を参照してください。 次のコードをコピーして、後で説明を進めます。

```javascript
var Zap = {

    get_session_info: function(bundle) {

       console.log('Entering get_session_info method ...');

         var access_token,
            access_token_request_payload,
            access_token_response;


        // Assemble the meta data for our Access Token swap request
         console.log('building Request with client_id=' + bundle.auth_fields.client_id + ', and client_secret=' + bundle.auth_fields.client_secret);
        access_token_request_payload = {
            method: 'POST',
            url: 'https://' + bundle.auth_fields.munchkin_account_id + '.mktorest.com/identity/oauth/token',
            params: {
                'grant_type' : 'client_credentials',
                'client_id' : bundle.auth_fields.client_id,
                'client_secret' : bundle.auth_fields.client_secret
            },
            headers: {
                'Content-Type': 'application/json',  // Could be anything.
                Accept: 'application/json'
            }
        };

        // Fire off the Access Token request.
        access_token_response = z.request(access_token_request_payload);

        // Extract the Access Token from returned JSON.
        access_token = JSON.parse(access_token_response.content).access_token;
        console.log('New Access_Token=' + access_token);

        // This will be mixed into bundle.auth_fields in future calls.
        //bundle.auth_fields.access_token=access_token;
        return {'access_token': access_token};
    },


    test_trigger_pre_poll: function(bundle) {

         console.log('Entering test_trigger_pre_poll method ...');

         bundle.request.params = {
         'access_token':bundle.auth_fields.access_token
         };

         return bundle.request;

    },


    test_trigger_post_poll: function(bundle) {

        console.log('Entering test_trigger_post_poll method ...');

        var data = JSON.parse(bundle.response.content);
        if ((!data.success)&&((data.errors[0].code=="601")||(data.errors[0].code=="600"))){
            console.log('Access Token expired or invalid, requesting new one - data.success=' + data.success + ', data.errors[0].code=' + data.errors[0].code);

           throw new InvalidSessionException(); // Calling get_session_info() to regenerate Access Token
        }

        return JSON.parse(bundle.response.content);
    },

    create_update_lead_pre_write: function(bundle) {

       bundle.request.params = {'access_token':bundle.auth_fields.access_token};
       return bundle.request;
    },

    create_update_lead_post_write: function(bundle) {

         var data = JSON.parse(bundle.response.content);
         if ((!data.success)&&((data.errors[0].code=="601")||(data.errors[0].code=="600"))){
            console.log('Access Token expired or invalid, requesting new one - data.success=' + data.success + ', data.errors[0].code=' + data.errors[0].code);
            throw new InvalidSessionException(); // Calling get_session_info() to regenerate Access Token
        }
        return JSON.parse(bundle.response.content);
    }
};
```

**メソッド** **get_session_info**

* このメソッドは、Marketo REST API [ 認証 ](/help/rest-api/authentication.md) エンドポイントを呼び出すアクセストークンを生成または再生成します。
* 「post_poll」メソッドで「Access Token Expired」エラーが発生するたびに呼び出されます。 アクセストークンは 1 時間ごとに期限切れになるようにスケジュールされているので、これは想定されています。
* アクション エンドポイント URL: https://{{munchkin_account_id}}.mktorest.com/identity/oauth/token

**pre_poll, pre_write**

* HTTP リクエストを送信する直前に変更するために、作成した任意のトリガーに対して「pre-poll」メソッドを作成する必要があります。これにより、パラメーターにMarketo アクセストークンを追加できます。
* 同じ理由で、作成したアクションに「pre-write」メソッドを作成する必要があります。

**post_poll, post_write**

* Zapier が何らかの処理を行う前にレスポンスを解析し、最終的に「Access Token Expired」エラーをインターセプトするために、作成したトリガーで「post-poll」メソッドを作成する必要があります。
* 同じ理由で、作成したアクションに「post-write」メソッドを作成する必要があります。
* このようなエラーが発生した場合、Zapier に認証を再現し、get_session_info メソッドを再実行するよう指示する InvalidSessionException をスローします。

バンドルログには、画面の右上隅にある「クイックリンク」メニューからスクリプティング API にアクセスできます。 これは、スクリプトのデバッグに非常に役立ちます。

ユースケース 1:Marketoと FullContact Card Readerの統合

この統合では、FullContact からMarketoへの Zap を 1 つ作成します。 この Zap を使用すると、FullContact モバイルカードReaderで名刺をスキャンし、リードをMarketoにプッシュできます。   **Zap FullContact -> Marketo** Zapier Dashboard で「Make a new Zap」ボタンをクリックします。

**ザピアのトリガー**

* アプリの FullContact を選択
* FullContact トリガー &#39;新しい名刺&#39;を選択する
* FullContact アカウントへの接続
* FullContact アプリのテスト

**ザピアにおけるアクション**

* 先ほど作成したアプリ Marketoを選択すると、Betaに表示されます
* Marketo アクション「リードを作成/更新」を選択します
* 認証パラメーター（Marketo アカウント ID、クライアント ID、クライアント秘密鍵）を入力して、Munchkin アカウントに接続します。
* FullContact からMarketoへのフィールドのマッピング
* 最終的に、新しいリードが配置されるパーティション名を入力します（Marketo インスタンスにパーティションが存在する場合のみ）。
* Marketo アプリのテスト
* Zap の有効化

注：FullContact から名刺Readerをダウンロードし、お使いのモバイルデバイスから Zapier 統合を有効化してください。

ユースケース 2:MarketoとGoogle シートの統合

この統合では、2 つの Zap を作成します。 1 つはMarketoからGoogle Sheets に、もう 1 つはGoogle Sheets からMarketoに送信されます。 この Zap を使用すると、MarketoとGoogle シートの間でリードや連絡先の一部を同期させることができます。   **Zap Marketo Webhook -> Google シート**
最初の Zap については、Marketoのカスタムコネクタには依存しませんが、Marketoの Webhook と「Zapier による Webhook」トリガーを活用します。 Zapier Dashboard で、「Make a new Zap」ボタンをクリックします。 **ザピアのトリガーパート 1**

* 「Webhook by Zapier」トリガーアプリを選択
* Zapier URL への POST またはGETを待機できるようにする「キャッチフック」をオンにします
* 子キーを選択する必要はありません
* Zapier は、リクエストを送信してクリップボードにコピーするためのカスタム **webhook URL** を生成しました

**Marketoの Webhook （管理者が行う手順）**

* 管理者/ Webhook に移動します。
* 「リードを Zapier にプッシュ」という新しい Webhook を作成し、Webhook フォームを編集します。

テンプレートのフィールドで、Zapier に転送するすべてのリードのフィールドを宣言し、Marketoのトークンを活用します。 このユースケースでは、リードをMarketoにプッシュするカスタム Zapier コネクタに対して定義したのと同じフィールドを使用します。

```json
{
"firstName":"{{lead.First Name}}",
"lastName":"{{lead.Last Name}}",
"email":"{{lead.Email Address}}",
"phone":"{{lead.Phone Number}}",
"leadOwner":"{{lead.Lead Owner First Name}} {{lead.Lead Owner Last Name}}",
"leadOwnerEmail":"{{lead.Lead Owner Email Address}}",
"leadNotes":"{{lead.Lead Notes:default=edit me}}",
"called":"{{lead.Called}}"
}
```

* フォームを保存します
* 応答マッピングは必要ないので、Webhook で完了です

**Marketoでのキャンペーンのテスト（マーケターまたは管理者が実行する手順）**

* マーケティングアクティビティから、新しいスマートキャンペーンを作成します

テストの目的で、リードのステータスが MQL に変わるたびに Webhook をトリガーにするキャンペーンを作成します。 もちろん、他のビジネス目的にも Webhook を使用できます。

* スマート・リストの編集
* フローでの Webhook の呼び出し
* キャンペーンのスケジュール
* 各リードが毎回フローを通過できることを確認する
* スマートキャンペーンの有効化

**ザピアのトリガーパート 2**

* 「Zapier による Webhook」トリガーアプリを完成させるには、Marketo Smart Campaign を 1 回実行し、Zapier で Webhook をキャッチする必要があります
* テストケースでは、Marketoのリードデータベースに移動して、リードを開き、そのステータスを「MQL」に変更するだけです

**Google Sheets でのスプレッドシートの作成**

* 新しいスプレッドシートの作成
* ワークシートを作成するか、デフォルトのワークシートを使用します
* Marketoから同期する各フィールド（Marketo Webhook で宣言されたフィールド）に列を追加します

  **ザピアにおけるアクション**

* アプリのGoogle シートを選択
* 「スプレッドシート行を作成」オプションをオンにします
* Google Sheets アカウントへの接続
* Google スプレッドシートを選択します
* ワークシートを選択します
* 「Webhook by Zapier」トリガーアプリとGoogle シートの間のすべてのフィールドをマッピングします。

* Google Sheets アプリのテスト
* Zap の有効化

**Zap Google Sheets -> Marketo**

Zapier Dashboard で、「Make a new Zap」ボタンをクリックします。

**ザピアのトリガー**

* 「Googleシート」トリガーアプリを選択
* スプレッドシートで新しい行が追加または変更されたときにトリガーする「更新されたスプレッドシート行」にチェックマークを付けます
* Google アカウントへの接続
* トリガーを設定するスプレッドシート（前の Zap で使用したものと同じ）とワークシートを選択します
* トリガー列を「any_column」に設定
* Google Sheets アプリのテスト

**ザピアにおけるアクション**

* 先ほど作成したアプリ Marketoを選択すると、Betaに表示されます
* Marketo アクション「リードを作成/更新」を選択します
* 認証パラメーター（Marketo アカウント ID、クライアント ID、クライアント秘密鍵）を入力して、Munchkin アカウントに接続します。
* Google シートからMarketoへのフィールドのマッピング
* 最終的に、新しいリードが配置されるパーティション名を入力します（Marketo インスタンスにパーティションが存在する場合のみ）。
* Marketo アプリのテスト
* Zap の有効化

### まとめ

Zapier 用Marketo コネクタの改善案を次に示します。

* 様々なMarketo オブジェクト（リスト、カスタムオブジェクトなど）に関連するその他のトリガーおよびアクションの追加
* Marketoからフィールドをハードコーディングする代わりに、Marketoから動的にフィールドを取り込むことができますが、その場合は、Marketoと Zapier の間で技術的な翻訳作業が必要になります。
* コネクタを開発チームと共有し、最終的には一般公開します。

Zapier が Premium Marketo アダプタを導入する可能性があり、これにより、ユースケースの実装がはるかに簡単になります。 いずれにせよ、この記事は、無料の Zapier プランでMarketoと Zapier を統合し、プレミアムアダプターでサポートされていないカスタムユースケースを構築するために常に活用できます。 この記事を楽しんで、Marketoと Zapier とさらに成功するために役立つことを願っています。 ありがとうございました。

Posted on _2016-04-17_ by _David_

## 2016 年春の更新

**REST API**

* Asset API - Web ページ
   * **ランディングページ** は、15 個の新しいエンドポイントを介して公開されるようになりました。これにより、ランディングページの作成、更新、削除、クローン作成、ドラフト管理が可能になります。 ランディングページテンプレートには、ドラフト管理エンドポイントも公開されるようになりました
      * ランディングページを取得
      * ID によるランディングページを取得
      * 名前によるランディングページを取得
      * ランディングページを作成
      * ランディングページメタデータを更新
      * ランディングページコンテンツを取得
      * ランディングページコンテンツセクションを追加
      * ランディングページコンテンツセクションを更新
      * ランディングページコンテンツセクションを削除
      * 動的コンテンツの取得セクション
      * 「動的コンテンツの更新」セクション
      * ランディングページのドラフトを破棄
      * ランディングページの承認
      * ランディングページのドラフトを未承認
      * ランディングページを削除
   * **ランディングページテンプレート**
      * ランディングページテンプレートのドラフトを破棄
      * ランディングページテンプレートの承認
      * ランディングページテンプレートのナビゲーション解除
      * ランディングページテンプレートを削除
   * **Forms** には、API を介して完全な作成、編集、管理の機能を提供する、21 個の新しいエンドポイントがリリースされています。 この API は、Forms 1.0 フォームに対する変更をサポートしていません。
      * フォームを取得
      * ID によるフォームを取得
      * 名前によるフォームを取得
      * フォームフィールドリストの取得
      * フォームフィールドリストを更新
      * フォームを作成
      * フォームを取得するありがとうページ
      * フォームの更新「ありがとうございます」ページ
      * フォームを更新
      * フォームのドラフトを破棄
      * フォームの承認
      * フォームの未承認
      * フォームを複製
      * フォームを削除
      * フォームフィールドを更新
      * フォームフィールドを削除
      * フォームフィールド表示ルールの更新
      * リッチテキストフォームフィールドの追加
      * Add Fieldset
      * フィールドセットからフィールドを削除
      * 使用可能なフォームフィールドを取得
      * フォームフィールドの位置の変更
      * 送信ボタンを更新
   * **プログラムの取得と参照** を使用すると、SFDC キャンペーンにリンクされているプログラムに対してSFDC キャンペーン ID が返されます

**カスタムオブジェクト** カスタムオブジェクトでテキスト領域データタイプがサポートされ、このタイプのカスタムオブジェクトフィールドに最大 2000 文字の文字列フィールドを保存できるようになりました。 **IP アドレスの許可リストへの登録** 管理者ユーザーは、API を介した不正アクセスを防ぐために、IP アドレスの許可リストを管理できるようになりました。 [ この機能について詳しくは、こちらを参照してください ](https://experienceleague.adobe.com/ja/docs/marketo/using/home)。 **カスタムアクティビティ UI** 管理者ユーザーは、管理メニューでカスタムアクティビティタイプを定義し、[ カスタムアクティビティの追加 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addCustomActivityUsingPOST) API を使用してリードにレコードを追加できるようになりました。 [ カスタムアクティビティタイプの定義については、こちらを参照してください ](https://experienceleague.adobe.com/ja/docs/marketo/using/home)。

Posted on _2016-06-01_ by _Kenny_

## 2016 年夏のアップデート

9 月 23 日（PT）の 2016 年夏版リリースでは、開発者向けの機能が 3 つリリースされています。

### REST API での E メール 2.0 のサポート

v1.0 のメールおよびテンプレートとのみ互換性があった [ 既存の Asset API](/help/rest-api/assets.md) はすべて、v2.0 のメールアセットで使用できるようになりました。

### Marketo にリードをプッシュ

[ リードをプッシュ ](/help/rest-api/leads.md) は、スマートキャンペーンでより簡単にトリガーできるように設計された代替リード同期方法です。 1 回の呼び出しで、1 つのアクティビティログ項目を作成し、リードを関連付けて、リードレコードを更新できます。 これは、リードによる単一フォームの入力と同様に機能し、既存の同期リードの手法を使用する代わりに、フォーム送信のプロキシ方法としてより簡単に使用できます。

### HTTP 圧縮

REST API で、HTTP 1.1 仕様で定義された標準を使用して応答を圧縮できるようになりました。 これにより、応答のサイズを縮小でき、転送速度が向上し、帯域幅の使用率が最小限に抑えられます。  

Posted on _2016-09-23_ by _Kenny_

## Marketoでの swagger-codegen の使用

[Swagger-codegen](https://github.com/swagger-api/swagger-codegen) は、Swagger 定義からサーバースタブと API クライアントの両方を生成できる強力な Java ライブラリです。 これにより、特定の言語のクライアントを生成する際の困難さとコストを大幅に軽減できます。 最初のクライアントの作成を開始するには、まずMarketoの Swagger 定義の 1 つのインスタンス固有のコピーを取得します。 テストに使用するインスタンスのMunchkin ID を入力します。 ID 定義から開始します。 インスタンスに固有の定義ができたので、次に swagger-codegen をダウンロードしてインストールする必要があります。 このプロセスはオペレーティングシステムに固有で、手順を参照できます [ こちら ](https://github.com/swagger-api/swagger-codegen#prerequisites)。デフォルト設定では、codegen は、提供されたすべてのエンドポイントとモデルをカバーするクライアントを出力します。 これらは通常、「docs」フォルダーに提供された例を使用して使用可能なエンドポイントを呼び出すためのメソッドを含む、DefaultApi と呼ばれるクラスを通じて管理されます（すべての言語にデフォルトでこれに対するテンプレートが含まれているわけではありません）。 次に、最初のクライアントを作成します。 コードを実行するフォルダーを作成してターミナルセッションに移動し、generate コマンドを使用して目的の言語でクライアントを作成します（homebrew のインストールメソッドを使用したと仮定します）。

swagger-codegen 生成 – i $definitionLocation -l $yourLanguage -o $yourLocation

これにより、クライアントコードが目的の場所に出力されます。 次に、これを使用して ID エンドポイントを呼び出し、アクセストークンを取得する方法を見てみましょう。

```java
 public static void main(String[] args){
  String client_id = args[0];
  String client_secret = args[1];
  ApiClient client = new ApiClient();
  DefaultApi id = new DefaultApi();
  try {
   String token = id.identityOauthTokenGet(client_id, client_secret, "client_credentials").getAccessToken();
   System.out.println(token);
  } catch (ApiException e) {
   e.printStackTrace();
  }
 }
```

```php
<?php
require_once(_DIR_ . '/vendor/autoload.php');

$api_instance = new Swagger\\Client\\Api\\DefaultApi();
$client_id = "client_id_example";
$client_secret = "client_secret_example";
$grant_type = "grant_type_example";

try {
    $result = $api_instance->identityOauthTokenGet($client_id, $client_secret, $grant_type);
    print_r($result->getAccessToken);
} catch (Exception $e) {
    echo 'Exception when calling DefaultApi->identityOauthTokenGet: ', $e->getMessage(), "\\n";
}
?>
```

```c#
  public static void Main(string[] args)
  {
      string clientId = "CHANGE ME";
      string clientSecret = "CHANGE ME";

      IdentityApi instance = new IdentityApi();
      ResponseOfIdentity response = instance.IdentityUsingGET(clientId, clientSecret, "client_credentials");

      string message = string.Format("Access Token: {0}, Expires In: {1}, Scope: {2}, Token Type: {3}",
          response.AccessToken, response.ExpiresIn, response.Scope, response.TokenType);
      Console.WriteLine(message);
  }
```

認証方法がわかったので、今後数週間で、自動生成クライアントのより高度なユースケースについて説明します。

Posted on _2016-10-10_ by _Kenny_

## Excel 統合（パート 1）:Power Query を使用したMarketo データの抽出と形状設定

これは、Microsoft Excel に組み込まれているPower BI テクノロジーを活用して、Marketoで真のセルフサービスのビジネス分析エクスペリエンスを作成する方法を説明する一連の記事の最初の記事です。 これらの記事で説明されている概念を使用すると、次のことができます。

* Marketoから Excel へのデータのインポート
* 他のソース（SaaS アプリケーション、データベース、フラットファイルなど）からのデータのインポートと結合
* ビジネスニーズと分析目的に合わせたデータの作成
* Excel からのデータをオンデマンドで更新
* 数式を使用して計算列およびメジャーを作成する
* 異機種データ間の関係の作成
* データを分析し、ピボットテーブルとピボットグラフを使用して高度なレポートを作成する
* 魅力的なデータビジュアライゼーションの作成

### Power Query for Excel

この最初の記事では、Power Query テクノロジーを使用したデータのインポートおよびシェーピングプロセスについて説明します。 Power Query は、分析ニーズに合わせてデータソースを検出、接続、組み合わせ、調整できるデータ接続テクノロジーです。 Power Query の機能は、Excel およびPower BI Desktop で使用できます。 Power Query は、データベース、Facebook、Salesforce、MS Dynamics CRM など、多くのデータソースに接続できます。 Marketoは初期設定ではサポートされていませんが、幸いにも、Marketo REST API を使用してシステムの機能の多くをリモートで実行できます。また、Power Query には、カスタムデータソースをスクリプト化できる豊富な式のセット（非公式には「M」）が付属しています。

### カスタムコネクタ

Power Query では、1 回の REST API 呼び出しをスクリプト化することはまれですが、次の要件を処理するのはさらに困難になります。

* アクセストークン管理（認証メカニズムおよび定期的なトークン更新を含む）
* 大量のデータセットに対するページネーションのメカニズム
* エラー処理

この記事では、Marketoの REST API を使用してあらゆる種類のデータ（リード、アクティビティ、カスタムオブジェクト、プログラムなど）を取り込むことができる、堅牢なカスタムコネクタを作成する方法について説明します。 唯一の制限は、Marketo API の 1 日のリクエスト制限以下です。 ここで説明する概念は、Marketoに重点を置いていますが、REST API を提供する他の SaaS ソリューションを統合するためにも使用できます。

### 前提条件

#### パワークエリ

Excel 2016 のリリース以前は、Microsoft Power Query for Excel は、Excel 2010 または Excel 2011 にダウンロードしてインストールした Excel アドインとして機能していました。 Excel 2016 以降、この技術は「取得と変換」セクションの「データ」リボンに統合されたネイティブ機能です。 この記事で作成されたすべてのスクリプトは、Windows 用の Excel 2016 でテストされています。 Excel 2013 または Excel 2010 の場合は同じ概念を使用できますが、いくつかの調整が必要になる場合があります。  Power Query は現在、Microsoft Windows 版の Excel でのみ使用できます。Mac版はサポートされていません。

#### Marketo

Power Query は、Marketo REST API を使用してMarketoのデータにアクセスします。 これらの API を使用するには、Marketo インスタンスの管理者が自分で作成できる API ユーザーとカスタムサービスが必要です。 そうでない場合は、管理者がそれらを提供する必要があります。 Marketo API ユーザーとカスタムサービスの作成方法に関する詳しい手順については、[ こちら ](/help/rest-api/custom-services.md) を参照してください。 完了したら、Marketo REST API を呼び出すための次の資格情報が必要です。**クライアント ID** および **クライアント秘密鍵**。 **REST API エンドポイント** は、Marketoの web サービス管理の REST API セクションにあり、次のパターンになっているはずです。

`<https://XXX-XXX-XXX.mktorest.com/rest>`

Marketoには、API に対する 1 日あたりのリクエスト制限があり、この制限は、使用状況レポートと共に web サービス管理で確認できます。 **レポートのデータの一部が欠落する可能性があるので、クエリをデザインする際は、1 日の上限を超えないようにしてください**。

### Power Query ブックの作成

新しい Excel ブックから開始します。 すべてのMarketo REST API 設定を宣言するための具体的な設定ワークシートを作成します。 このワークシートでは、次の 3 つのテーブルを作成します。

テーブル「**REST_API_Authentication**」と列 **URL**：お使いのMarketo REST API エンドポイント。 **クライアント ID**:Marketo REST API OAuth2.0 資格情報から。 **クライアント秘密鍵**:Marketo REST API OAuth2.0 資格情報から。
列を持つテーブル「**Scoping**」:**ページングトークン SinceDatetime**：最初の「日付ベース」のページングトークンにより、特定の期間からのMarketo アクティビティの取得に使用される、ISO 8601 標準の日付表記（「2016-10-06T13:22:17-08:00」、「2016-10-06」は 0 の有効日時）に従う日付。 この日付は、主にワークブックにインポートするデータ量を制限するために使用されます。 **リスト ID**：扱っているすべてのリード/連絡先を参照する、Marketoの静的リストの ID。 この静的リストは、Marketoで自由に管理できます（例えば、スマートキャンペーンは、定期的またはリアルタイムでリードや連絡先をフィードできます）。
静的リストの ID を取得するには、Marketoでリストを開き、URL から数値 ID を取得します（例：`<https://myorg.marketo.com/#ST3517A1LA1>`、リスト ID=3511）。 **最大レコードページ数**：これは、Marketo出力データを繰り返し処理する疑似再帰アルゴリズムに使用されます。ページあたりの最大レコード数が 300 個の「位置ベース」のページングトークンを使用します。 これは、1 ページにつき可能な限り多くのレコードを取得するという当社の関心事なので、300 に固執します。 したがって、通常、33.333 に設定された最大レコードページは、33.333 X 300 = 9.9999 万レコードの処理能力を意味しますが、Marketo API の 1 日のリクエスト制限では 33.333 K も意味します。 クエリからのすべてのデータが取得されるとすぐにアルゴリズムは停止するので、このパラメーターはループの安全性制限にすぎません。

列 `Leads` リードフィールド **を含むテーブル**：リードと連絡先をクエリする際にMarketoから収集されるリードフィールドのコンマ区切り。 Excel でのテーブルの宣言は簡単です。 スプレッドシートに列の名前と値を入力して 2 行を入力し、テーブルの周囲をマウスで強調表示し、[ 挿入 ] メニューの [ テーブル ] アイコンを選択して名前を付けます。 テーブルと列に指定される名前は、スクリプトによって直接呼び出されるので、重要です。

## 認証およびアクセストークン

### Marketo REST API 認証について

Marketo の REST API は、2-legged OAuth 2.0 で認証されます。クライアント ID とクライアント秘密鍵は、定義したカスタムサービスによって提供されます。各カスタムサービスは、サービスが特定のアクションを実行することを許可するロールと権限のセットを持つ API 専用ユーザによって所有されます。アクセストークンは、1 つのカスタムサービスに関連付けられます。
完全な認証メカニズムについては、Marketo Developer サイトで [ こちら ](/help/rest-api/authentication.md) ドキュメント化されています。 アクセストークンが最初に作成されたときの有効期間は 3600 秒または 1 時間です。 同じカスタムサービスに対して連続する認証呼び出しが行われるたびに、現在のアクセストークンと残りの存続期間が返されます。 トークンの有効期限が切れると、認証は新しいアクセストークンを返します。 アクセストークンの有効期限の管理は、統合がスムーズに動作し、通常の操作中に予期しない認証エラーが発生するのを防ぐために重要です。

#### クエリを作成

「データ」メニューの「Get&amp;Transform」セクションの「新しいクエリ」アイコンをクリックして、新しいクエリを作成します。 先頭に使用する空白のクエリを選択し、「MktoAccessToken」などの名前を付けます。 クエリエディターから詳細エディターを起動し、一部の Power Query 式を手動でスクリプト化できるようにします。 詳細エディターに次のコードを入力します。

```
let
    // Get url and credentials from config worksheet - Table REST_API_Authentication
    mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
    clientIdStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[Client ID],
    clientSecretStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[Client Secret],

    // Calling Marketo API Get Access Token
    getAccessTokenUrl = mktoUrlStr & "/identity/oauth/token?grant_type=client_credentials&client_id=" & clientIdStr & "&client_secret=" & clientSecretStr,
    TokenJson = try Json.Document(Web.Contents(getAccessTokenUrl)) otherwise "Marketo REST API Authentication failed, please check your credentials",

    // Parsing access token
    accessTokenStr = TokenJson [access_token]

in
    accessTokenStr
```

ソースコードに埋め込まれたコメントの先頭に「//」が付いている場合、コードは自明になります。 関数の参照が必要な場合は、この記事の参照の節に記載されているリンクを確認してください。 ボタン「完了」をクリックしてください。 最後に適用されたステップ「accessTokenStr」の出力でアクセストークンが正常に表示されていることを確認します。  Excel のセキュリティに関する簡単なコメントです。黄色のバナーから外部データ接続を有効にするよう求められる場合があります。 これは、クエリを正しく動作させるために必要です。

#### クエリから関数への変換

詳細エディターに戻り、コードを次の関数宣言で囲みます。

```
let
    FnMktoGetAccessToken =()=>

        let
            // Get url and credentials from config worksheet - Table REST_API_Authentication
            mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
            clientIdStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[Client ID],
            clientSecretStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[Client Secret],

            // Calling Marketo API Get Access Token
           getAccessTokenUrl = mktoUrlStr & "/identity/oauth/token?grant_type=client_credentials&client_id=" & clientIdStr & "&client_secret=" & clientSecretStr,
           TokenJson = try Json.Document(Web.Contents(getAccessTokenUrl)) otherwise "Marketo REST API Authentication failed, please check your credentials",

            // Parsing access token from Json
           accessTokenStr = TokenJson [access_token]

        in
            accessTokenStr

in FnMktoGetAccessToken
```

この関数は、入力にパラメーターを受け取らず、設定ワークシートからパラメーターを取得します。 出力としてアクセストークンが生成されます。 クエリ `FnMktoGetAccessToken` の名前を変更して保存します。 データ メニューの [ 取得と変換 ] セクションの [ クエリの表示 ] ボタンをクリックすると、Excel でいつでも、すべてのクエリを表示できることに注意してください。 これで、関数は関数アイコン「Fx」でマークされます。

### 静的リストのメンバの読み込み

#### リードを取得

Marketo Lead API は、リードレコードに対する簡単な CRUD 操作、静的リストおよびプログラムでのリードのメンバーシップの変更機能、リードの Smart Campaign 処理の開始機能を提供します。 これらすべての機能については、[ こちら ](/help/rest-api/leads.md) を参照してください。 多数のリードレコードのセットは、静的リストまたはプログラムのメンバーシップに基づいて取得できます。 静的リストの ID を使用すると、その静的リストのメンバーであるすべてのリードレコードを取得できます。 リストの ID は、呼び出しのパスパラメーターです。 詳しくは、Marketo Developers ドキュメントの「リストとプログラムメンバーシップ」の章を参照してください。 API 呼び出しごとに取得できるリードレコードの最大数は 300 なので、ページングトークンを活用して 300 レコードのページごとにレコードを収集する必要があります。 最初の呼び出しの後、JSON 応答でページングトークンが取得され、ページングトークンが出力に含まれなくなった場合に完了することがわかります。

### 基本クエリ

静的リストからすべてのリードをダウンロードすることを目的とした完全に機能するクエリから始めましょう。 「MktoLeads」という名前の新しい空のクエリを作成し、詳細エディターで次のコードを入力します。

```
let
    // Get Url from config worksheet - Table REST_API_Authentication
    mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
    // Get the number of iterations (pages of 300 records) - Table Scoping
    iterationsNum = Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[Max Records Pages],
    // Get the List id - Table Scoping
    listIdStr = Number.ToText(Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[List ID], "D", ""),
    // Get the Lead fields to extract - Table Leads
    LeadFieldsStr = Excel.CurrentWorkbook(){[Name="Leads"]}[Content]{0}[Lead Fields],


    // Build Multiple Leads by List Id URL
    getMultipleLeadsByListIdUrl = mktoUrlStr & "/rest/v1/list/" & listIdStr & "/leads.json?fields=" & LeadFieldsStr,

    // Build Marketo Access Token URL parameter
    accessTokenParamStr = "&access_token=" & FnMktoGetAccessToken(),

    pagingTokenParamStr = "",

    // Function iterating though the pages
    FnProcessOnePage =
    (accessTokenParamStr, pagingTokenParamStr) as record =>
        let

            // Send REST API Request
            content = Web.Contents(getMultipleLeadsByListIdUrl & accessTokenParamStr & pagingTokenParamStr),

            // Recover Json output and watch if token is expired, in that case, regenerate access token
            newAccessTokenParamStr = if Json.Document(content)[success]=true then accessTokenParamStr else "?access_token=" & FnMktoGetAccessToken(),
            getMultipleLeadsByListIdJson = if Json.Document(content)[success]=true then Json.Document(content) else Json.Document(Web.Contents(getMultipleLeadsByListIdUrl & newAccessTokenParamStr & pagingTokenParamStr)),

            // Parse Json outputs: data and next page token
            data = try getMultipleLeadsByListIdJson[result] otherwise null,
            next  = try  "&nextPageToken=" & getMultipleLeadsByListIdJson[nextPageToken] otherwise null,
            res = [Data=data, Next=next, Access=newAccessTokenParamStr]
        in
            res,

    // Generates a list of values given four functions that generate the initial value initial, test against a condition, and if successful select the result and generate the next value next. An optional parameter, selector, may also be specified
    GeneratedList =
        List.Generate(
            ()=>[i=0, res = FnProcessOnePage(accessTokenParamStr, pagingTokenParamStr)],
            each [i]<iterationsNum and [res][Data]<>null,
            each [i=[i]+1, res = FnProcessOnePage([res][Access],[res][Next])],
            each [res][Data])
in
    GeneratedList
```

Power Query には、従来のループ機能（例：For-loop、While-loop）を指定します。再帰はサポートされません。 List.Generate を使用して For ループを実装するのが良い回避策です。 この関数は、[ こちら ](http://msdn.microsoft.com/query-bi/m/list-generate) のドキュメントに記載されています。 リスト付き。 ページに対して繰り返し処理を行うことができます。 イテレーションの各ステップで、次のページのページングトークンを含む URL を保持してデータのページを抽出し、生成されたリストの次の項目に結果を保存します。 [Datachant](https://datachant.com/2016/06/27/cursor-based-pagination-power-query/) のブログは、これを解決するための素晴らしいリソースでした。 パラメータ「最大レコードページ」は、ページ数を制限し、無限ループを避ける現実的な範囲に制限するために使用します。 もう 1 つの課題は、アクセストークンの有効期限が切れていないことを確認することです。 その残りの存続期間の追跡は、Power Query では複雑すぎます。 そのため、REST API へのすべての呼び出しは、エラーチェックによってバックアップされます。エラーが発生した場合、トークンの有効期限が切れていると想定し、最初に更新してから、呼び出しを再度再生します。 2 回目の呼び出しが失敗すると、2 回目の失敗が Excel に通知されます（最悪の場合、結果としてデータは取得されません）。 クエリを保存した後、または「更新ボタン」をクリックしていつでもクエリを起動できます。  今回の例では、5 つのリスト内の 5 ページのデータに適合する 1364 件のリードレコードが抽出されました。

### データのシェイプ

これらのレコードをすべて 1 つのフラットなレコードリストに含めるようにデータを形作る必要があります。 これを行うには、次の 2 つの方法があります。

* その他のコードの使用
* Power Query UI の活用

出力グリッドを右クリックし、コンテキストメニューで「テーブルへ」を選択して、リストのテーブルに変換します。  「To Table」ポップアップで、2 つのピックリストにデフォルト値を残します。  次に、結果のリストのテーブルを展開します。 これで、すべてのレコードが 1 つのリストに含まれるようになりました。 Json 形式でエンコードされたレコードには、フィールドおよび関連する値が含まれます。 もう一度展開します。 保持するすべてのフィールドをポップアップで選択し、「元の列名をプレフィックスとして使用」チェックボックスをオフにします。  エット・ヴォイラ！ 私たちのテーブルにはすべてのレコードがきれいに表示されている。 詳細エディターを再度開くと、データを形成するために 3 行のコードが追加されていることがわかります。

```
# "Converted to Table" = Table.FromList(GeneratedList, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
# "Expanded Column1" = Table.ExpandListColumn(#"Converted to Table", "Column1"),
# "Expanded Column2" = Table.ExpandRecordColumn(#"Expanded Column1", "Column1", {"id", "updatedAt", "lastName", "email", "createdAt", "firstName"}, {"id", "updatedAt", "lastName", "email", "createdAt", "firstName"})
```

Power Query を使用すると、計算値を含む追加の列を作成するなど、より多くの作業を行うことができます。後でいくつかの可能性を確認します。 このクエリを保存して閉じます。 現在は、いつでも手動で、またはバックグラウンド更新によって自動的に更新できます。

### 結果のリダイレクト

問題は、結果データをどこに送信するかです。 クエリの上にマウスを置き、コンテキストメニューの「読み込み先」メニューを選択します。 ポップアップで、次の項目を選択できます。

* 「テーブル」（Table）：すべてのシェイプデータをワークシート（新規または既存）に送信する場合、
* Power Pivot で詳細な分析を行う目的がある場合は、[ 接続の作成のみ ] を選択します。

「これをデータモデルに追加する」チェックボックスをオンにすると、Power Pivot のデータを活用できます。これがこの記事の第 2 部で必要になります。

### ページネーションの管理

私たちのプロジェクトの目的は、さらに多くのクエリを作成することなので、リファクタリングを行い、ページネーションを管理する再利用可能な関数を抽出しましょう。 **FnMktoGetPagedData** という新しい空のクエリを作成し、拡張エディターで次のコードを入力します。

```
let
    FnMktoGetPagedData =(url, accessTokenParamStr, pagingTokenParamStr)=>

    let

        // Get the number of iterations (pages of 300 records) - Table Scoping
        iterationsNum = Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[Max Records Pages],

        // Sub-function iterating though the REST API service result pages
        FnProcessOnePage =
        (accessTokenParamStr, pagingTokenParamStr) as record =>
            let

                // Send REST API Request
                content = Web.Contents(url& accessTokenParamStr & pagingTokenParamStr),

                // Recover Json output and watch if token is expired, in that case, regenerate access token
                newAccessTokenParamStr = if Json.Document(content)[success]=true then accessTokenParamStr else "?access_token=" & FnMktoGetAccessToken(),
                contentJson = if Json.Document(content)[success]=true then Json.Document(content) else Json.Document(Web.Contents(url & newAccessTokenParamStr & pagingTokenParamStr)),

                // Parse Json outputs: data and next page token
                data = try contentJson[result] otherwise null,
                next  = try  "&nextPageToken=" & contentJson[nextPageToken] otherwise null,
                res = [Data=data, Next=next, Access=newAccessTokenParamStr]
            in
                res,

        // Generates a list of values given four functions that generate the initial value initial, test against a condition, and if successful select the result and generate the next value next. An optional parameter, selector, may also be specified
        GeneratedList =
            List.Generate(
                ()=>[i=0, res = FnProcessOnePage(accessTokenParamStr, pagingTokenParamStr)],
                each [i]<iterationsNum and [res][Data]<>null,
                each [i=[i]+1, res = FnProcessOnePage([res][Access],[res][Next])],
                each [res][Data])
    in
        GeneratedList

in FnMktoGetPagedData
```

クエリを保存します。 次に使用します。

### 簡略化されたクエリ

**FnMktoGetPagedData** 関数を呼び出すクエリ「MktoLeads」をもう一度書き換えましょう。

```
let
    // Get Url from config worksheet - Table REST_API_Authentication
    mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
    // Get the List id - Table Scoping
    listIdStr = Number.ToText(Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[List ID], "D", ""),
    // Get the Lead fields to extract - Table Leads
    LeadFieldsStr = Excel.CurrentWorkbook(){[Name="Leads"]}[Content]{0}[Lead Fields],


    // Build Multiple Leads by List Id URL
    getMultipleLeadsByListIdUrl = mktoUrlStr & "/rest/v1/list/" & listIdStr & "/leads.json?fields=" & LeadFieldsStr,

    // Build Marketo Access Token URL parameter
    accessTokenParamStr = "&access_token=" & FnMktoGetAccessToken(),

    // No initial paging token required for this call
    pagingTokenParamStr = "",

    // Invoke the multiple REST API calls through the FnMktoGetPagedData function
    result = FnMktoGetPagedData (getMultipleLeadsByListIdUrl , accessTokenParamStr, pagingTokenParamStr)

in
    result
```

ご覧のように、クエリは読み取りと管理が非常に簡単になりました。 **FnMktoGetPagedData** 関数を他のクエリに再び活用します。

### 定義した期間から特定のアクティビティを読み込む

#### ページネーションを使用したアクティビティの取得

Marketoでは、リードレコードに関連する様々なアクティビティタイプが許可されています。 ほとんどすべての変更、アクションまたはフローステップは、リードのアクティビティログに対して記録され、API を介して取得したり、スマートリストおよびスマートキャンペーンのフィルターとトリガーで活用したりできます。 アクティビティは、常に、レコードの ID に対応する leadId を介してリードレコードに関連付けられ、独自の一意の整数 ID も持ちます。 完全な REST API のドキュメントは [ こちら ](/help/rest-api/activities.md) にあります。

潜在的なアクティビティタイプは非常に多数あり、サブスクリプションによって異なる可能性があり、それぞれに一意の定義があります。 すべてのアクティビティには独自の一意の ID、leadId および activityDate がありますが、primaryAttributeValueId と primaryAttributeValue の意味は異なります。 次に、ID 41 のMarketoでトラッキングされたアクティビティの 1 つである興味深いモーメントについて説明します。 我々が解決しようとしている新たな課題は以下の通りです。

* アクティビティが発生した期間を定義するには、「日付ベース」のページングトークンを開始する必要があります。
* データの形成は、アクティビティのタイプに応じて、アクティビティ固有の属性のリストが JSON で提供されるので、分析を容易にするために解析し、フラット化する必要があるので、少し難しいです。

#### 日付ベースのページングトークン

最初にこの関数を作成して、最初の「日付ベース」のページングトークンを生成する必要があります。これは、アクティビティクエリの期間をスコープするために必要です。 ページングトークンに関するドキュメントは [ こちら ](/help/rest-api/paging-tokens.md) にあります。 **FnMktoGetPagingToken** という新しい空白のクエリを作成し、詳細エディターで次のコードを入力します。

```
let
    FnMktoGetPagingToken =(accessTokenStr)=>

        let
            // Get url from config worksheet - Table REST_API_Authentication
            mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],

            // Get Paging Token SinceDatetime from config worksheet - Table Scoping
            mktoPTSinceDatetimeStr = DateTime.ToText(Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[Paging Token SinceDatetime], "yyyy-MM-ddThh:mm:ss"),

            // Building URL for API Call
            getPagingTokenUrl = mktoUrlStr & "/rest/v1/activities/pagingtoken.json?access_token=" & accessTokenStr & "&sinceDatetime=" & mktoPTSinceDatetimeStr,

            // Calling Marketo API Get Paging Token
            content = Web.Contents(getPagingTokenUrl),

            // Recover Json output and watch if access token is expired, in that case, regenerate it
            newAccessTokenStr = if Json.Document(content)[success]=true then accessTokenStr else "?access_token=" & FnMktoGetAccessToken(),
            pagingTokenJson = if Json.Document(content)[success]=true then Json.Document(content) else Json.Document(Web.Contents(mktoUrlStr & "/rest/v1/activities/pagingtoken.json?access_token=" & newAccessTokenStr & "&sinceDatetime=" & mktoPTSinceDatetimeStr)),

            // Parsing Paging Token
            pagingTokenStr = pagingTokenJson[nextPageToken]

        in
            pagingTokenStr

in FnMktoGetPagingToken
```

関数を保存します。 次に使用します。

#### 注目のアクションアクティビティ

次に、「FnMktoGetPagedData」関数と「FnMktoGetPagingToken **関数を呼び出すクエリ「MktoInterestingMomentsActivities** を記述し **みましょう**。

```
let

    // Get Url from config worksheet - Table REST_API_Authentication
    mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
    // Get the List id - Table Scoping
    listIdStr = Number.ToText(Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[List ID], "D", ""),

    // Build Get Activities URL
    getActivitiesUrl = mktoUrlStr & "/rest/v1/activities.json?ListId=" & listIdStr & "&activityTypeIds=46",

    // Build Marketo Access Token URL parameter
    accessTokenStr = FnMktoGetAccessToken(),
    accessTokenParamStr = "&access_token=" & accessTokenStr,

    // Obtain date-based paging token used to scope in time the activities
    pagingTokenParamStr = "&nextPageToken=" & FnMktoGetPagingToken(accessTokenStr),

    // Invoke the multiple REST API calls through the FnMktoGetPagedData function
    result = FnMktoGetPagedData (getActivitiesUrl , accessTokenParamStr, pagingTokenParamStr)

in
    result
```

このクエリの結果は、再びリストのリストになるので、分析に使用するには、さらにデータを処理する必要があります。

### データのシェイプ

リードに対して行ったのと同じシェーピング操作を行います。

* 出力グリッドを右クリックし、コンテキストメニューで「テーブルに追加」を選択して、リストのテーブルに変換します。
* 結果のリストのテーブルを展開します。
* もう一度展開し、保持するすべてのフィールドをポップアップで選択します（「元の列名をプレフィックスとして使用」チェックボックスをオフにします）。

列と値を表示できます。ただし、注目のモーメントに関連付けられた特定の属性のリストがまだ含まれている「属性」列は除きます。 これらの属性を展開しましょう。 これでリストがレコードに展開され、必要なフィールド（各属性の名前と値）を選択して再度展開し、「元の列名をプレフィックスとして使用」チェックボックスをオフにします。  その結果、属性を含むすべてのデータが表示されますが、それぞれの興味深いモーメントアクティビティは 3 行に及びます。 これは分析に使いにくいだろう。  アクティビティごとに 1 行だけ、すべての属性が追加の列として表示されていることが理想的です。 テーブルから 3 つの属性をピボットすると、簡単に行うことができます。 アクティビティ属性から 2 つの列「名前」と「値」を選択し、「変換」メニューの「ピボット列」をクリックします。 ポップアップで詳細オプションを確認し、「Values Column」 = value および「Don&#39;t aggregate」 value 関数を選択します。  「OK」をクリックすると、アクティビティごとに 1 行のデータを出力する必要があります。  次の「データシェーピング」コード行が、クエリのスクリプトに自動的に追加されているはずです。

```
  #"Converted to Table" = Table.FromList(result, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    #"Expanded Column1" = Table.ExpandListColumn(#"Converted to Table", "Column1"),
    #"Expanded Column2" = Table.ExpandRecordColumn(#"Expanded Column1", "Column1", {"id", "leadId", "activityDate", "activityTypeId", "campaignId", "primaryAttributeValue", "attributes"}, {"id", "leadId", "activityDate", "activityTypeId", "campaignId", "primaryAttributeValue", "attributes"}),
    #"Expanded attributes" = Table.ExpandListColumn(#"Expanded Column2", "attributes"),
    #"Expanded attributes1" = Table.ExpandRecordColumn(#"Expanded attributes", "attributes", {"name", "value"}, {"name", "value"}),
    #"Pivoted Column" = Table.Pivot(#"Expanded attributes1", List.Distinct(#"Expanded attributes1"[name]), "name", "value")
in
    #"Pivoted Column"
```

### 次の手順

これで、REST API を通じて使用可能な特定のMarketo データにアクセスするために必要なすべてのクエリを設計できるようになりました。 この記事をお楽しみいただき、Excel とMarketoを組み合わせた大きな利点を活かすのに役立ったことを願っています。 2 番目の記事では、すべてのクエリを含むサンプルワークブックも提供しています。

### 参照

#### パワークエリ

* [Power Query – 概要と学習 ](https://support.microsoft.com/en-us/article/Power-Query-Overview-and-Learning-ed614c81-4b00-4291-bd3a-55d80767f81d)
* [ パワークエリ式リファレンス ](http://msdn.microsoft.com/query-bi/m/power-query-m-reference)
* [Matt Masson Blog](http://www.mattmasson.com/tag/power-query/) は、Power Query に関する優れたリソースを提供しています。
* [DataChant Blog](https://datachant.com/2016/06/27/cursor-based-pagination-power-query/) は、ページネーションメカニズムの実装に非常に役立ちます

Posted on _2016-10-18_ by _Philippe_

## 2016 年秋のアップデート

2016 年秋のリリースで、メール v2 の変数とモジュールに対する CRUD サポートと、指定アカウントに対する CRUD サポートを追加します。 これで、Marketo REST API を使用してコンテンツをローカルで読み取り、編集できるだけでなく、コンテンツの移動、並べ替え、削除も行えるようになりました。 以下のアップデートの完全なリストを参照してください。

### リードデータベース API

* [**重点顧客**](/help/rest-api/named-accounts.md)
   * 重点顧客の読み取り、更新、削除のための新しいエンドポイント
   * 既知の問題
      * 2016 年秋リリースの時点では、API を使用してリードを名前付きアカウントに関連付けることはできません

### アセットAPI

* [**電子メール**](https://developer.adobe.com/marketo-apis/api/asset/#operation/describeUsingGET_5)
   * Email v2 変数を操作するための新しいエンドポイント
   * Email v2 モジュールを操作するための新しいエンドポイント
   * 既知の問題
      * 予測トークンを含むセクションに対するクエリと更新では、エラーが返されます
      * 予測トークンを含むコンテンツセクションを含むメールは、API を使用して承認できない場合があります

Posted on _2016-12-07_ by _Kenny_

## Twitter Handl3@MarketoDev 廃止した理由

Twitter で@MarketoDev のハンドルを廃止することにしました。 アカウントは 2011 年 12 月 9 日に無効になります。 なぜ？ **2014 年初頭に遡る…** アドビでは、デベロッパーが API に対抗して構築できるように、Marketo Developers Site を立ち上げたところです。 Marketoの認知度を高め、開発者の参入障壁を減らしたいと考えました。 それに伴い、Marketoと統合ソリューションを構築したいと考えていたテクノロジーパートナーやお客様との連携を@MarketoDev 定しました。 他の勇敢な新しい事業と同様に、これがどのように機能するかわかりませんでした。 最初は、新しいブログ投稿と新しい API リリースをツイートしました。 良かった。開発者サイトへのトラフィックが増加した。 私たちはまた、質問の品揃えを受け取り始め、私たちは忠実に答えました。 **2016 年後半まで早送り…** [LaunchPoint パートナー ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) のエコシステムが成長するにつれて、ツイートのアクティビティの量が増加しました。 @MarketoDev に投稿された質問の量に対応することは、私たちの小さなチームにとって大きな仕事になりました。 一般商品や営業関連のお問い合わせも増え、@Marketoや@MarketoCares にリダイレクトしました。 また、開発関連の質問には 140 文字では不十分であることがわかりました。 これに答えると、多くの場合、会話のスレッドが長くなり、複雑になり、規模を拡大できないアプローチが生まれました。 最後に、開発者サイトの訪問者のトラフィックソースを分析したところ、大部分はオーガニック検索によるもので、ブログの「今すぐ登録」機能が使用されていることがわかりました。 これらの理由から、私たちはプラグを@MarketoDev に引き出すことにしました。 **今後も…** Twitter ファンであれば（そしてファンでない場合は）、恐れてはいけません！ 当社の企業 Twitter は@Marketoを扱い、カスタマーサポートが@MarketoCares を扱うのと同様です。

Posted on _2016-12-02_ by _David_

## Excel 統合（パート 2）:Power Pivot と Power View を使用した高度なMarketo レポートおよびデータビジュアライゼーションの作成 – 

これは、Microsoft Excel に組み込まれたPower BI テクノロジーを活用して、Marketoで真のセルフサービスのビジネス分析エクスペリエンスを作成する方法を説明する一連の 2 つの記事の 2 番目です。 これらの記事で説明されている概念を使用すると、次のことができます。

* Marketoから Excel へのデータのインポート
* 他のソース（SaaS アプリケーション、データベース、フラットファイルなど）からのデータのインポートと結合
* ビジネスニーズや分析目的に合わせたデータの形成
* Excel 内でオンデマンドでデータを更新
* 数式を使用して計算列およびメジャーを作成する
* 異機種データ間の関係の作成
* データを分析し、ピボットテーブルとピボットグラフを使用して高度なレポートを作成する
* 魅力的なデータビジュアライゼーションの作成

### Power Pivot と Power View for Excel

この記事では、以下の構築方法の例を示します。

* Power Pivot を使用してMarketo データの異なるコレクション間の関係を活用する高度なMarketo レポート
* Power View を使用して静的およびアニメーションの優れたビジュアライゼーションを実現

**Power Pivot** は、Excel 2016 に既に含まれている Excel アドインで、強力なデータ分析を実行したり、高度なデータ モデルを作成したりできます。 Power Pivot を使用すると、様々なソースから大量のデータをマッシュアップし、迅速に情報分析を実行し、インサイトを簡単に共有できます。 Power Query を使用して様々なデータソースから抽出されたデータは、データモデル、Excel スプレッドシート、またはその両方に送信できます。 最初の記事では、Marketoからデータをインポートして整形し、データモデルに送信して、スプレッドシートで利用できるようにする前に、より高度な分析を実行しました。 **Power View** は、Excel ビジュアライゼーションレイヤーの代替となるものです。 これは、直感的なアドホックレポートとダッシュボーディングを推進するインタラクティブなデータ探索、ビジュアライゼーション、プレゼンテーション体験です。

この記事で説明する手順はすべて、Windows 版 Excel 2016 でテストされています。 Excel 2013 または Excel 2010 （Power View なし）の場合は同じ概念を使用する必要がありますが、適応が必要になる場合もあります。 Power Pivot と Power View は、現在、Microsoft Windows 版の Excel 2016 でのみ利用できます。Office 365 版の Excel 2016 は、Power Pivot と Power View を完全にはサポートしていません。

### Marketo Power ワークブック

#### ワークブックをダウンロード

最初の記事では、Power Query テクノロジーを使用したデータのインポートおよびシェーピングプロセスについて説明しました。 Marketoからリードやアクティビティを抽出するために、いくつかの高度なパワークエリを実装する方法を学びました。 コーディングを行わずに、レポートやビジュアライゼーションを作成するポイントに直接ジャンプしたい人もいるからです。 このワークブックには、最初の記事で詳しく説明したすべてのクエリと、あと数回説明したクエリが含まれています。 エラー処理を改善し、設定ワークシートに追加のパラメーターをいくつか追加しました。 最初の記事を参照した場合でも、Marketo Power ワークブックをダウンロードし、追加された内容を確認することをお勧めします。

免責事項：Marketo Power ワークブックはMarketoの公式製品ではないので、Marketoではサポートされていません。 個人のビジネスニーズに合わせて自由に使用および拡張できますが、自分の責任で行ってください。

#### ワークブックの設定

Marketo設定ワークシートから、必要なすべての情報を入力します。

* **Marketo REST API 認証：** が必要です
* **スコーピング：** ページングトークンの SinceDatetime と、分析するすべてのリードを含むMarketo静的リストの ID を設定します
* **リード：** レポートを作成するには、少なくとも次のリードフィールドを指定する必要があります：`id`、`firstName`、`lastName`、`email`、create`edAt`、`updatedAt`、`title`、`company`、`industry`、`inferredCountry`、`inferredCity`
   * いずれかのカスタムフィールドで市区町村情報がより正確な場合は、代わりに独自のフィールドを使用できます
* **アクティビティ：** Marketo データベースから取得するアクティビティタイプは、アクティビティセットごとにここで指定します。今すぐ変更する必要はありません。
   * ワークブックにユーティリティクエリを用意しました。このクエリでは、後でこの情報を調整する場合、既存のすべてのアクティビティタイプが Excel ワークブックに一覧表示されます

セキュリティ関連のポップアップが表示される場合があります。 外部接続を信頼し、[ パブリック ] に設定してください。 以下のポップアップが表示された場合は、「匿名」の Web アクセスコンテンツを保持します。 Marketoへの認証はカスタムクエリで直接管理されるので、その他のアクセスを有効にする必要はありません。

#### Marketo Data のダウンロード

最初に、Marketo設定ワークシートのスコーピング エリアで定義したパラメーターによってダウンロードされるデータが多くなりすぎず、Marketo API の 1 日あたりのリクエスト制限を超えないことを確認してください。 準備ができたら、「データ」メニューから「すべて更新」ボタンをクリックして、すべてのデータがワークブックにダウンロードされるのを待ちます。 データのダウンロード時に「列 1 が見つかりませんでした」と同様に書式設定エラーメッセージが表示される場合は、1 つ以上のクエリがデータの取得に失敗していることを意味し、書式設定も失敗しています。 後でもう一度試してください。エラーが解決しない場合は、Excel のバージョンを確認してください（Office 365 の Excel 2016 を使用しないでください）。 また、Marketo プラットフォームからの待ち時間を考慮することも重要です。 静的リストまたはリードデータで変更を行う場合は、Power Queries を起動する前に待つことをお勧めします。

### Power Pivot でのデータ モデリング

上部メニューバーにある Power Pivot メニューの [ 管理 ] ボタンをクリックして Power Pivot を開きます（使用できない場合は、Excel のバージョンを確認してください。Power Pivot は、Excel の一部のバージョンでアドインとしてインストールできます）。 Marketoからダウンロードされ、データモデルに送信されたすべてのデータは、Power Pivot ウィンドウの下部にあるさまざまなタブからアクセスできる必要があります。

### データ分析式（DAX）

一部のレポートでは、データをエンリッチメントまたは再フォーマットする必要があります。 Power Pivot データ分析式（DAX）を使用して、一部のカスタム計算を計算列およびメジャー（計算フィールドとも呼ばれます）として定義します。 DAX の詳細については、参照セクションの「DAX in Power Pivot」リンクを参照してください。 [Power Pivot] ウィンドウに計算領域が表示されていることを確認します。表示されていない場合は、[Power Pivot ホーム ] メニューから有効にします。  「**MktoLeads**」タブを選択し、リード計算領域の任意の場所に **リード数** メジャーを追加します：**リード数：=**&#x200B;**DISTINCTCOUNT**&#x200B;**&#x200B; （[id]）**。 この測定では、リストで使用可能な個別のリードを ID に基づいてカウントします。 また、レポートのコンテキストで実行される最終的なフィルターも考慮に入れます。 レポートはリード数を合計できるので、この測定は実際には必要ありませんが、「MktoLeads の合計」よりも優れた名前のリード数を使用するようにしました。 また、これは、特定のタイプのデータ入力（スコアが 50 を超えるすべてのリード、平均スコアなど）に対して平均、最小、最大を実行する、より複雑な測定を簡単に想像できる簡単な例です。 ...）..  次に、「**MktoWebActivities** タブを選択して、3 つの計算列を作成します。 テーブルの右端までスクロールし、列「列を追加」をクリックして、次の計算列を挿入します。 **Activity:** テーブル MktoActivtyTypes でアクティビティ ID を検索して、使いやすい Activity ラベルを取得します。 **\=**&#x200B;**LOOKUPVALUE**&#x200B;**&#x200B; （MktoActivityTypes[name],MktoActivityTypes[id],[activityTypeId]）**&#x200B;**Year-Month:** 一部のレポートにより適したパターン「YYYYmm」でアクティビティの日付を再フォーマットします。 **\=**&#x200B;**LEFT**&#x200B;**&#x200B; （[activityDate],4）&amp;**&#x200B;**MID**&#x200B;**&#x200B; （[activityDate],6,2）**&#x200B;**日付：** アクティビティの日付は、元のクエリの文字列で、適切な日付に変換します。 **\=**&#x200B;**DATE**&#x200B;**&#x200B; （**&#x200B;**LEFT**&#x200B;**&#x200B; （[activityDate],4）,**&#x200B;**MID**&#x200B;**&#x200B; （[activityDate],6,2）,**&#x200B;**MID**&#x200B;**&#x200B; （[activityDate],9,2））** 次に、「**MktoEmailActivities**」タブと 2 つの追加で 3 つの同じ測定値を作成します。**Campaign:** MktoCampaigns テーブルでキャンペーン ID を検索して、わかりやすいキャンペーン名をを取得します。 **\=**&#x200B;**LOOKUPVALUE**&#x200B;**&#x200B; （MktoCampaigns[name],MktoCampaigns[id],[campaignId]）**&#x200B;**プログラム：** MktoCampaigns テーブル内のキャンペーン ID を検索して、わかりやすいプログラム名を取得します。 MktoPrograms の表には、フォルダー、ワークスペースなど、プログラムに関する詳細が表示されます。 **\=**&#x200B;**LOOKUPVALUE**&#x200B;**&#x200B; （MktoCampaigns[programName],MktoCampaigns[id],[campaignId]）**

### エンティティの関係

以前は、モデル内の別のテーブルの情報を検索して、欠落している情報を完成させる方法を見ました。 Power Pivot は、データ モデルの一部のテーブル間の関係を定義するためのより強力なオプションを提供し、それらの関係をレポートから直接活用できるようにします。 レポートの主要な関係を定義します。 「電源ピボット」ウィンドウから図ビューを選択します。 データモデル図内で次の関係をトレースします。

* **MktoInterestingMomentActivities:leadId →** **MktoLeads:id**
* **MktoScoringActivities:leadId →** **MktoLeads:id**
* **MktoRevenueStageActivities:leadId →** **MktoLeads:id**
* **MktoWebActivities:leadId →** **MktoLeads:id**
* **MktoEmailActivities:leadId →** **MktoLeads: id**

これらの関係やオブジェクトはすべてレポートで使用せず、リード、web アクティビティ、メールアクティビティのみを使用します。 次に、レポートを作成します。

### Emails Performance Pivot Chart

この最初のレポートでは、標準の Excel ピボットグラフに基づいて、メールのパフォーマンス KPI を表示します。 業界やキャンペーン別にデータをフィルタリングできます。 「ピボットテーブル」セレクターから「ピボットグラフ」を選択すると、Power Pivot メニューから直接ピボットグラフを作成できます。  別の方法として、Excel スプレッドシートから直接ピボットグラフを作成し、「このワークブックのデータモデルを使用」オプションを選択します。  **MktoEmailActivities** および **MktoLeads** テーブルからフィールドをドラッグ&amp;ドロップします。例：**MktoEmailActivities.Activity →** **Legend** （これは、以前に **MktoEmailActivities** に実装した DAX 計算列を使用します） **MktoEmailActivities.Date →**&#x200B;**Axis** （**MktoEmailActivities** に以前に実装したした DAX 計算列をを使用します） **EMAILActivITIES.Id →** **∑→ → Values** **&#x200B;**&#x200B;**&#x200B;** **&#x200B;**&#x200B;**&#x200B;**

ドロップされた各フィールドで「値フィールド設定」を選択して、カスタム名を作成できます。 この例では、「メール アクティビティ ID」フィールドを「∑値」セクションにドロップし、カスタム名を「アクティビティの数」に編集しました。 次に、ピボットグラフを設定します。 グラフを右クリックし、コンテキストメニューの「グラフタイプを変更」オプションを選択します。 このようにして、すべてのデータシリーズに異なるグラフタイプを選択しました。

### 電源表示を使用したリードマップ

2 番目のレポートでは、リードと取引先責任者が地域別に世界地図上および業界別に表示されます。 このレポートには Power View が必要です。 Excel のメニューを有効にするには、以下の参照リンクに従ってください。 または、Excel の検索ボックスに「power view」と入力します。 [ パワービューレポートを挿入 ] を選択します。  空白の Power View レポートで、右側のパネルの **MktoLeads** テーブルを選択し、リードロケーションフィールド（例：**inferredCity**）をドラッグ&amp;ドロップします。 これで、メインメニューに「デザイン」メニューが表示されます。

Power View の「デザイン」メニューで「マップ」を選択して、マップビジュアライゼーションに切り替えます。 **MktoLeads** テーブルからフィールドをドラッグ&amp;ドロップします（下図を参照）。**MktoLeads.industry →**&#x200B;**Color** **MktoLeads.inferredCity →**&#x200B;**Locations** **MktoLeads.Leads Count →** **∑ Size** （これは、**MktoLeads** 以前に実装した DAX 測定を使用します）。リードマップの準備がができました！ マップのサイズを調整し、タイトルと凡例をカスタマイズするだけです。 Power View を使用すると、1 つのスプレッドシートに複数のグラフを含む高度なダッシュボードを作成できます。 Power View を使用してさらに多くのダッシュボードコンポーネントを使用する方法については、以下の参照チュートリアル「[Amazing Power View レポートを作成 ](https://support.microsoft.com/en-us/article/Tutorial-Create-Amazing-Power-View-Reports-Part-1-e2842c8f-585f-4a07-bcbd-5bf8ff2243a7)」をご覧ください。

### 3D マップ上でアニメーション化された Web アクティビティ

この 3 番目のレポートは、業界別のリード web アクティビティを 3D の世界地図上に表示します。 このレポートには 3D マップが必要です。 Excel の検索ボックスに「3D」と入力し、「3D Map」を選択してください。 ポップアップウィンドウから新規ツアーを作成します。  右側のパネルでバブル・チャートを選択します。 **MktoLeads** および **MktoWebActivities** の各テーブルから、次の図のようにフィールドをドラッグ&amp;ドロップします。**MktoLeads.industry →**&#x200B;**Category**&#x200B;**MktoLeads.inferredCity →**&#x200B;**Location** **MktoWebActivities.Activity →**&#x200B;**Time** （これは、前に **MktoWebActivities** で実装した DAX 計算列を使用します。 ID フィールドは、アクティビティのカウントにも使用できます。） **MktoWebActivities.Date →** **Time** （これは、以前に **MktoWebActivities** で実装した DAX 計算列を使用します） **MktoWebActivities.Activity** も、様々なタイプの web アクティビティを除外するフィルターとして使用できます。

「テーマ」ボタンを使用して、3D マップのカラースキームを変更します。 「シーンオプション」を開き、アニメーションをカスタマイズします。
3D 世界地図を使えば、地球をアニメーション化し、そこからビデオを作成することができます。

### 次の手順

Excel Power BI ツールで実行できることに関して、表面的な問題を残しました。 Excel のスキルを向上させ、ビジネス目標を達成するために必要なレポートを設計するために、他の優れた記事やチュートリアルを Web で検索することをお勧めします。 これらの記事をお楽しみいただき、Excel とMarketoの大きな利点を組み合わせて活用するのに役立つことを願っています。

### 参照

#### パワーピボット

* [Power Pivot: Excel での強力なデータ分析とデータモデリング ](https://support.microsoft.com/en-us/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)
* [Power Pivot のデータ分析式（DAX） ](https://support.microsoft.com/en-us/article/Data-Analysis-Expressions-DAX-in-Power-Pivot-bab3fbe3-2385-485a-980b-5f64d3b0f730)

#### Power View

* [Excel 2016 で Power View を有効にする ](https://support.microsoft.com/en-us/article/Turn-on-Power-View-in-Excel-2016-for-Windows-f8fc21a6-08fc-407a-8a91-643fa848729a)
* [ チュートリアル：優れた Power View レポートの作成 ](https://support.microsoft.com/en-us/article/Tutorial-Create-Amazing-Power-View-Reports-Part-1-e2842c8f-585f-4a07-bcbd-5bf8ff2243a7)

Posted on _2017-02-02_ by _Philippe_

## Marketo API のアクティビティレコードに対する重要な変更

**メモ：この投稿は、新しいインフラストラクチャへの移行に伴い、API によって返されたアクティビティレコードに加えられた変更を反映するように更新されます。** **最終更新日：2018 年 9 月 13 日** 2017 年 9 月より開始される、Marketoの次世代アクティビティサービスのロールアウトにより、Marketo API から返されるアクティビティ、データ値の変更、リード削除レコードで、整数「id」フィールドの一意性または有無を適用できなくなります。 アクティビティレコードを取得する統合のサービスが中断されないようにするには、「id」フィールドをオプションとして扱う必要があります。 この変更のカットオーバーは、購読と今後のリリースに影響を与え始めます。 この変更は、次のエンドポイントに影響します：REST API

影響を受けるSOAPのタイプは `ActivityRecord` と `LeadChangeRecord` です。

### 例

次の例は、影響を受けるレコードタイプを示しています。 どちらの例でも、影響を受けるフィールドは「id」と呼ばれます。

**REST フィールドの例：id**

```json
  {
      "id" : 102988,
      "leadId" : 1,
      "activityDate" : "2015-01-16T23:32:19Z",
      "activityTypeId" : 1,
      "primaryAttributeValueId" : 71,
      "primaryAttributeValue" : "localhost/munchkintest2.html",
      "attributes" : [
          {
              "name" : "Client IP Address",
              "value" : "10.0.19.252"
          },
          {
              "name" : "Query Parameters",
              "value" : ""
          },
          {
              "name" : "Referrer URL",
              "value" : ""
          },
          {
              "name" : "User Agent",
              "value" : "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.95 Safari/537.36"
          },
          {
              "name" : "Webpage URL",
              "value" : "/munchkintest2.html"
          }
      ]
  }
```

**例SOAP フィールド：id**

```xml
  <activityRecord>
    <id>1030680</id>
    <activityDateTime>2013-07-09T16:44:28-05:00</activityDateTime>
    <activityType>Visit Webpage</activityType>
    <mktgAssetName>ClickDemo</mktgAssetName>
    <activityAttributes>
      <attribute>
        <attrName>Webpage ID</attrName>
        <attrType xsi:nil="true" />
        <attrValue>2547</attrValue>
      </attribute>
      <attribute>
        <attrName>Webpage URL</attrName>
        <attrType xsi:nil="true" />
        <attrValue>/ClickDemo.html</attrValue>
      </attribute>
    </activityAttributes>
    <campaign />
    <personName xsi:nil="true" />
    <mktPersonId>1089965</mktPersonId>
    <foreignSysId xsi:nil="true" />
    <orgName xsi:nil="true" />
    <foreignSysOrgId xsi:nil="true" />
  </activityRecord>
```

Posted on _2017-03-01_ by _Kenny_

## 2017 年冬の更新

2017 年冬リリースでは、カスタムオブジェクトデータを非同期で一括読み込みする機能と、ガイド付きランディングページで変数を操作する機能を追加しています。 以下のアップデートの完全なリストをご覧ください。

### リードデータベース API

#### カスタムオブジェクトの一括読み込み

カスタムオブジェクトの一括読み込みをサポートする新しいエンドポイント。 詳しくは、[ こちら ](/help/rest-api/custom-objects.md) を参照してください。

#### アクティビティの今後の変更のお知らせ

Marketoが次世代のアクティビティサービスをリリースすると、大きな変化が生じることに注意してください。 この変更は、次のエンドポイントに影響を与えます。

SOAP

[getLeadActivity](/help/soap-api/getleadactivity.md), [getLeadChanges](/help/soap-api/getleadchanges.md)

これらのエンドポイントによって返されるレコードに含まれる整数「id」フィールドは、一意であることが保証されなくなりました。 これは、アクティビティ、データ値の変更およびリード削除レコードタイプに影響を与えます。 これらのレコードタイプを取得する統合のサービスが中断されないようにするには、「id」フィールドをオプションとして扱う必要があります。

#### プッシュトークンの削除

SDK API を介してプッシュトークンを削除する機能が追加されました。 詳細については、[iOS](/help/mobile/push-notifications.md)、[Android](/help/mobile/push-notifications.md) をご覧ください。

Posted on _2017-03-01_ by _David_

## 2017 年春の更新

2017 年春リリースでは、リードおよびアクティビティオブジェクトのデータを非同期で一括抽出する機能と、名前付きアカウントリストを操作する機能が追加されました。 以下のアップデートの完全なリストをご覧ください。

### リードの一括抽出

リードの一括抽出をサポートする新しいエンドポイント。 様々なオプションを使用して、レコード選択条件を指定します。 詳しくは、[ こちら ](/help/rest-api/bulk-lead-extract.md) を参照してください。

### アクティビティの一括抽出

アクティビティの一括抽出をサポートする新しいエンドポイント。 日付範囲とアクティビティリストを使用して、レコード選択条件を指定します。 詳しくは、[ こちら ](/help/rest-api/bulk-extract.md) を参照してください。

### 重点顧客リスト

指定アカウントリストでの CRUD 操作をサポートする新しいエンドポイント。 詳しくは、[ こちら ](/help/rest-api/named-account-lists.md) を参照してください。

### その他の機能強化

* [ キャンペーンを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCampaignByIdUsingGET) エンドポイントを使用して、「トリガー可能」なキャンペーンをフィルタリングできるようになりました。 これを実現するには、「isTriggerable=true」をクエリパラメーターとして渡します。
* [ クローンプログラム ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) エンドポイントで、SMS メッセージを除くすべてのアセットタイプを含むプログラムがサポートされるようになりました。

### Ionic

これで、Marketo Mobile MME と [Ionic](https://ionicframework.com/) アプリケーションフレームワークを使用できます。 詳しくは、[ こちら ](/help/mobile/ionic.md) を参照してください。

### プッシュ通知トークンの登録解除

Marketoでプッシュ通知トークンの登録を解除できる新しいメソッドがSDKに追加されました。 これは、ユーザーがアプリからログアウトする場合などに便利です。 使用方法については、`unregisterPushDeviceToken` （iOS）または `uninitializeMarketoPush` （Android）のメソッド [ こちら ](/help/mobile/push-notifications.md) を参照してください。

Posted on _2017-06-16_ by _David_

## IFTTT と Zapier を使用したマーケター向けのモノのインターネット

IoT （Internet of Things）とは、コネクテッド機器や家電、ウェアラブル機器、自動車などのネットワーク間を結ぶ技術のことです。 組み込みの電子機器、ソフトウェア、センサー、ネットワーク接続により、これらのオブジェクトはクラウド情報システムを使用してデータを収集および交換できます。 これらのテクノロジーは急速に成長し、トレンドが変化しているため、私たちの暮らし方、働き方、ビジネス方法にすぐに影響を与えます。 業界をリードするマーケティングエンゲージメントプラットフォームであるMarketoは、あらゆる形態のコミュニケーションチャネルを拡張し、やり取りする機能を備えた IoT に対応しています。 Marketoでは、既に 70 を超えるタイプのメール、web、モバイル、CRM に関連するアクティビティをトラッキングできます。また、サードパーティのシステムからフィードできる [ カスタムアクティビティ ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/administration/marketo-custom-activities/create-a-custom-activity.html?lang=ja) もサポートしています。 Marketo[ カスタムオブジェクト ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/administration/marketo-custom-objects/understanding-marketo-custom-objects.html?lang=ja) を使用すると、ビジネスに関連するすべての種類のサードパーティ指標を追跡でき、マーケターはMarketo スマートキャンペーンフィルターおよびトリガーからこれらの指標を直接活用できます。 コンシューマー向け IoT を導入するには、コンシューマーデバイスとやり取りするための一元化されたサーバーが必要になり、このサーバーは REST API、カスタムオブジェクト、カスタムアクティビティなどの機能を備えたMarketo オープンプラットフォームとデータを交換します。 - ドキュメント化 [ こちら ](http://eto.com/)。 ブログ投稿で示すのは簡単ではありません。 代わりに、IFTTT サービスをMarketoと統合して、マーケター向けの IoT の優れたユースケースを実現します。

* オフィスで色付きのライトを点滅させることで、リードがロードショーに登録されるたびにマーケティングチームを元気づけます
* 接続された電源プラグに接続されたベルを自動的に起動して、取引が成立するたびにセールス・チームを支援する
* LinkedIn、Facebook、Slackなどのソーシャルネットワークにマーケティング成功マイルストーンを自動的に投稿します。 ...
* 次の項目に基づいてマーケティングキャンペーンを自動的に開始：
   * 天気予報（風、温度、雨など）が発生したとき
   * ニューヨークタイムズ紙などの新聞で新しい記事が発行された場合、いくつかの特定の基準に合致する
   * 米国上院又は下院が投票したとき
   * 国際宇宙ステーションが特定の場所を通過したとき
   * 等。 ...

これらのシナリオは楽しくても役に立たないと思うかもしれませんが、人々だけでなく、つながる世界の物事でもマーケティングを行う新しい概念的な方法を示すために、ここにいます。 この記事のもう 1 つの興味深い点は、例えば、サードパーティシステムとMarketoの間で、Zapier などのオープン web 統合プラットフォームを「サービングハッチ」として活用して、認証を管理する方法です。

### IFTTT サービス

IFTTT は「IF This Then That」の頭字語です。 これは、アプレットと呼ばれる単純な条件文のチェーンを作成するために使用される無料の web ベースのサービスです。 アプレットは、一部のパートナー Web サービス内で発生する変更によってトリガーされ、その結果、アクションが他のパートナー Web サービスに送信されます。 IFTTT は、2011 年にサンフランシスコのリンデン・ティベット、ジェシー・タネ、スコット・トン、アレクサンダー・ティベットによって立ち上げられた。 一見すると、IFTTT は [Zapier](https://zapier.com/) のようなサービスに似ています。例えば、消費者や IoT デバイス（リモコン、アラーム、ライト、サーモスタット、車、プリンター、携帯電話など）に対してはるかに強い焦点を当てています。  まず、[IFTTT web サイト ](https://ifttt.com/explore) から IFTTT のアカウントを作成する必要があります。 すでに利用可能なすべてのクールなアプレットを自由に見つけてください。そうすれば、他のシナリオのアイデアが確実に得られます。

### Maker チャネル

チャネル（IFTTT とのパートナーシップ）を持たない web アプリケーションは、Maker Channel を使用する必要があります。 Maker チャネルを使用すると、web リクエストを作成または受信できる任意のデバイスやアプリで動作するアプレットを作成できます。 次の統合機能を提供します。

* サードパーティシステムからアクションをトリガーするための web リクエストを受信するインバウンドトリガー
* サードパーティのシステムに対する web リクエストをインターネット上で公開してアクセスするためのアウトバウンドアクション

IFTTT から、「Maker」サービスを検索してクリックします。  初めて、「接続」ボタンをクリックしてアクティブにする必要があります。  これで、Maker チャンネルがアクティブになります。 Maker Settings ボタンをクリックすると、秘密鍵を取得できます。詳しくは、指定した URL をコピーしてブラウザーに貼り付けます。

### 市場からの IFTTT アクションの直接トリガー

まず、Marketoからあらゆる種類のサードパーティ web サービスのアクションをトリガーすることに重点を置きます。 そのために、[Marketo Webhook](https://experienceleague.adobe.com/docs/marketo/using/product-docs/administration/additional-integrations/create-a-webhook.html?lang=ja) を使用します。 まず、IFTTT モバイルアプリを介した携帯電話やタブレットでのプッシュメッセージから始めて、Philips Hue ライトを点滅させる IoT シナリオを実装します。

### Marketo Webhook

Marketoからイベントをトリガーするには、IFTTT の「if」として機能するのは簡単です。 必要な手順は、次のパターン URL に従って、イベント名と秘密鍵を使用して POST web リクエストを IFTTT に送信するだけです。

`<https://maker.ifttt.com/trigger/{event_name}/with/key/{secret_key}>`

Maker を使用すると、web リクエストを介して最大 3 つのパラメーターを通信することもできます。 これを行うには、クエリパラメーターを使用します。

`<https://maker.ifttt.com/trigger/{event_name}/with/key/{secret_key}?value1={value1}&value2={value2}&value3={value3}>`

または、最大 3 つの値で構成される JSON 本文を使用します。

`{ "value1" : "{value1}", "value2" : "{value2}", "value3" : "{value3}" }`

Marketoで、管理者インターフェイスから新しい Webhook を作成します。  新しい Webhook に次の情報を提供します。

**Webhook 名：** IFTTT プログラム成功

**説明：** プログラムを成功させるために、スマートキャンペーンから IFTTT でイベントをトリガーする

**URL:** `<https://maker.ifttt.com/trigger/{event_name}/with/key/{secret_key}?value1={{program.name}}&value2={{lead.Email> Address}}&value3={{lead.Full Name}}`

event_name、MarketoProgramSuccess を使用（例：）

secret_key、IFTTT Maker Service の秘密鍵を使用します

使用可能な 3 つの値に対して静的テキストまたはMarketo トークンを使用します。 プログラムレベルで独自のトークンを定義し、これらの値を渡すことで、よりインタラクティブなメッセージをプッシュできます。

**要求の種類：** POST

**テンプレート：** 空白のままにします

**リクエストトークンエンコーディング：** フォーム/Url

**応答タイプ：** なし

応答マッピングを定義する必要はありません。

### IFTTT アプレット

IFTTT Web ポータルで、メインメニューの「マイアプレット」を選択します。  ボタン「新しいアプレット」をクリックして、セクションをクリックしてください **+this**。  Maker サービスを検索します。  Maker サービスが web リクエストを受け取ってイベントを通知するたびに起動するトリガーを作成します。 Marketo Webhook の URL で指定されたものと同じイベント名を使用します（例：「MarketoProgramSuccess」）。「トリガーを作成」ボタンをクリックします。  次に、**+that** セクションをクリックして、アクションサービスを指定します。  まずは、IoT デバイスに投資しなくても誰でもテストできるシンプルなアクションサービス、通知サービスから始めます。 Notifications Service を検索して選択します。
デバイスに通知を送信する「通知を送信」アクションを選択します。  Marketoから送信した 3 つの値を要素として追加して、意味のある通知をユーザーに提供することで、活用できます（以下の例と同様です）。次に、「アクションを作成」ボタンをクリックします。 IFTTT アプレットを確認して終了します。 有効になっていることを確認します。

### IFTTT アプレットのテスト

モバイルで通知を受け取るには、まずデバイスの IFTTT アプリをダウンロードする必要があります。  Marketo スマートキャンペーンフローで Webhook を使用すると、Marketo プログラム成功イベントをトリガーできます。 Marketo Webhook は、トリガーされたスマートキャンペーン（連絡先が記入したフォームがリストに追加された後のトリガーなど）でのみ機能することに注意してください。  次に、携帯電話での IFTTT 通知の例を示します。

### IFTTT でCreativeを入手しましょう

IFTTT は 300 以上のパートナーとアプレットアクションを提供しているので、あなたの想像力と一緒にアプリやアプライアンスのポートフォリオは限界です。. .あなたが電子店やオンラインでどこでも購入できる [ フィリップスの色相ライト ](https://www.philips-hue.com/en-us) を例に取りましょう。 次のアプレットは、Marketoがプログラムの成功をトリガーする際に、現在の割り当てられた色でライトの 1 つを点滅させ、オフィスのマーケティングチームを後押しする可能性があります。 以前と同じ手順で新しいアプレットを作成します。ここでは、Marketoが Webhook でトリガーされますが、今回は Philips Hue サービスからアクションを選択します。

「ライトを点滅」アクションを選択します。 アプリは Philips Hue から使用可能なすべてのライトをリクエストするので、点滅させるライトを選択できます。 まず、Philips Hue、Hue ブリッジ、そしてもちろん少なくとも 1 つの Hue 電球、ライトストリップ、プロジェクタまたはランプを持つアカウントを設定する必要があります。  リードがロードショーやウェビナーに登録されるたびに色付きのライトが点滅する新しいアプレットを追加しました。 マーケティングチームは、そのセットアップをオフィスで毎日元気づけます。

### Zapie を使用して IFTTT からMarketo アクションを実行

次に、IFTTT プラットフォームからMarketo スマートキャンペーンをトリガーします。 そのために、[Marketo REST API](/help/rest-api/rest-api.md) を使用します。 この API はセキュリティで保護されており、何かを呼び出す前に OAuth2 認証が必要なので、Zapier などの別のプラットフォームを介してその認証を処理する必要があります。これは、IFTTT は Maker Channel で API の 2 つの連続する呼び出しをチェーン化できないためです。 既に Zapier を紹介し、Zapier 用のカスタム Marketo コネクタを実装する方法を段階的に説明して公開してから、[Zapier](https://zapier.com/) web アプリ自動化サービスを選択しました。 [Workato](https://www.workato.com/integrations/marketo) などの他のプラットフォームも解決策となる可能性があります。

### Marketo キャンペーン

スケジュールされたスマートキャンペーンでMarketo プログラムを作成します。 テストの目的で、次のスマートキャンペーンを例として作成できます。**スマートリスト**&#x200B;トリガーではなくフィルターのみを使用します。 少なくともあなたが資格を得ることを確認してください。 **フロー** メールやその他の種類の通知を送信します。 **スケジュール** 複数のテストを処理するために、毎回フローを実行できることを確認します。 スマートキャンペーン ID は URL から取得できます。 例：_https://{{marketo_url}}/#SC4289A1_ - スマートキャンペーン ID は 4289 になります。 Marketo REST API を使用して、このキャンペーンをトリガーできます。 例えば、Chromeの [Postman](https://www.postman.com/) プラグインを使用して、次の 2 つの連続した HTTPS 呼び出しを送信できます。**認証手順：**

`https://{{Your Munchkin_Account_id}}.mktorest.com/identity/oauth/token?grant_type=client_credentials&client_id={{Your_Client_Id}}&client_secret={{Your_Client_Secret}}`

JSON 応答からアクセストークンを復元します。 **キャンペーンのキックオフ手順：**

`https://{{Your_Munchkin_Account_id}}.mktorest.com/rest/v1/campaigns/{{Campaign_Id}}/schedule.json?access_token={{access_token}}`

### Marketo キャンペーンを開始するための中間 Zapier カスタムコネクタ

Marketo REST API で認証を行い、スマートキャンペーンを開始するカスタム Zapier コネクタを構築する必要があります。

* 前提条件
* Marketo Connector for Zapier の実装
* 「Marketo キャンペーン」など、別のタイトルを使用します
   * 「認証」ステップの実行
   * 「トリガー」手順を実行（Zapier テストで必要）
   * 以下に説明するMarketo キャンペーンを開始する特定の「アクション」手順を実行します。

データアクションエンドポイント URL の送信先：

`https://{{munchkin_account_id}}.mktorest.com/rest/v1/campaigns/{{CampaignId}}/schedule.json`

その他のオプションフィールドは空白のままにします。

#### スクリプト API

Zapier のスクリプト機能を使用すると、アプリの API と Zapier の間で交換されるリクエストと応答を操作できます。 HTTP リクエストは、送信される直前に変更することができ、Zapier がリクエストに対して何らかの処理を行う前にレスポンスを解析することができます。 カスタム「セッション認証」認証を完了するために必要です。 詳しくは、元の記事を参照してください。 次のコードを元のコードと非常によく似たものにコピーします。ここでは、アクションメソッドを変更しました。

```javascript
var Zap = {

 get_session_info: function(bundle) {

 console.log('Entering get_session_info method ...');

 var access_token,
 access_token_request_payload,
 access_token_response;


 // Assemble the meta data for our Access Token swap request
 console.log('building Request with client_id=' + bundle.auth_fields.client_id + ', and client_secret=' + bundle.auth_fields.client_secret);
 access_token_request_payload = {
 method: 'POST',
 url: 'https://' + bundle.auth_fields.munchkin_account_id + '.mktorest.com/identity/oauth/token',
 params: {
 'grant_type' : 'client_credentials',
 'client_id' : bundle.auth_fields.client_id,
 'client_secret' : bundle.auth_fields.client_secret
 },
 headers: {
 'Content-Type': 'application/json', // Could be anything.
 Accept: 'application/json'
 }
 };

 // Fire off the Access Token request.
 access_token_response = z.request(access_token_request_payload);

 // Extract the Access Token from returned JSON.
 access_token = JSON.parse(access_token_response.content).access_token;
 console.log('New Access_Token=' + access_token);

 // This will be mixed into bundle.auth_fields in future calls.
 //bundle.auth_fields.access_token=access_token;
 return {'access_token': access_token};
 },

 test_trigger_pre_poll: function(bundle) {

 console.log('Entering test_trigger_pre_poll method ...');

 bundle.request.params = {
 'access_token':bundle.auth_fields.access_token
 };

 return bundle.request;

 },

 test_trigger_post_poll: function(bundle) {

 console.log('Entering test_trigger_post_poll method ...');

 var data = JSON.parse(bundle.response.content);
 if ((!data.success)&&((data.errors[0].code=="601")||(data.errors[0].code=="600"))){
 console.log('Access Token expired or invalid, requesting new one - data.success=' + data.success + ', data.errors[0].code=' + data.errors[0].code);

 throw new InvalidSessionException(); // Calling get_session_info() to regenerate Access Token
 }

 return JSON.parse(bundle.response.content);
 },

 launch_campaign_pre_write: function(bundle) {

 bundle.request.params = {'access_token':bundle.auth_fields.access_token};
 return bundle.request;
 },

 launch_campaign_post_write: function(bundle) {

 var data = JSON.parse(bundle.response.content);
 if ((!data.success)&&((data.errors[0].code=="601")||(data.errors[0].code=="600"))){
 console.log('Access Token expired or invalid, requesting new one - data.success=' + data.success + ', data.errors[0].code=' + data.errors[0].code);
 throw new InvalidSessionException(); // Calling get_session_info() to regenerate Access Token
 }
 return JSON.parse(bundle.response.content);
 }

};
```

##### 新規ザップ

Zapier ダッシュボードから「新しい Zap を作る」ボタンをクリックします。 **トリガー**

* 「Webhook by Zapier」トリガーアプリを選択します
* 「Catch Hook」をオンにします。
* 子キーを選択する必要はありません
* Zapier は、リクエストを送信して安全な場所に保管するためのカスタム Webhook URL を生成しました
* 以下の「Zapier Webhook を呼び出す IFTTT アプレット」シナリオを開始して、Webhook URL をテストします。 これにより、Zapier は Webhook ペイロードについて学習し、キャンペーン ID をアクションに割り当てることができます

**アクション**

* 作成済みのMarketo Campaign コネクタを選択します
* 使用可能な唯一のアクションを選択：**キャンペーンを開始**
* 認証パラメーター（Marketo アカウント ID、クライアント ID、クライアント秘密鍵）を入力して、Munchkin アカウントに接続します。
* テンプレートを編集し、トリガーのキャンペーン ID を「キャンペーンを開始」キャンペーン ID パラメーターに関連付けます。
* このステップをテストし、Marketo Campaign が起動することを確認します

### Zapier Webhook を呼び出す IFTTT アプレット

まず、テストしやすいシンプルなシナリオから始めます。 IFTTT では、1 時間ごとにMarketo キャンペーンを開始する日時トリガーを選択します。 アクションは、Zapier Webhook URL に投稿し、スマートキャンペーン ID を渡す web リクエストです。 Zapier Zap と IFTTT アプレットの両方がアクティブであることを確認し、すべてが期待どおりに動作していることをテストします。

### IFTTT を使用してCreativeを取得しましょう

IFTTT は 300 以上のパートナーとアプレットトリガーを提供しているので、あなたのアプリやアプライアンスのポートフォリオと想像力は限界です。. .では、天気予報に関するMarketoキャンペーンを開始するために使用する [Weather Underground](https://www.wunderground.com/) サービスを例に見てみましょう。 雨の状態が発表されると、次のトリガーが開始されます。 次に、トリガーを Maker Webhook Action に関連付け、以前と同様に Zapier Webhook パラメーターを入力します。  Et voila、あなたはちょうどこれが実際に機能していることをダブルチェックに来て今は良い雨が必要です。

この記事で提供されている概念を適用して、多くの楽しみを持っていることを願っています。 しかし、最も重要なことは、この記事の主なコンセプトのおかげで、Marketoを他のサードパーティシステムと統合したい人にとって役に立つと思うことです。

* MARKETO REST API
* Marketo Webhook
* サードパーティシステムとMarketoの間で、Zapier などのオープン web インテグレーションプラットフォームを「サービングハッチ」として活用して、認証を管理する方法（例：）

Posted on _2017-06-20_ by _Philippe_

## 2017 年夏のアップデート

2017 年夏リリースでは、プログラム API のマイナーな機能強化をリリースしています。

### プログラムの参照

オプションの earliestUpdatedAt および latestUpdatedAt パラメーターを追加して、プログラムを日付範囲別に取得する機能を [ プログラムの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/browseProgramsUsingGET) エンドポイントに追加します。 任意の日時を持つどちらか一方または両方のパラメーターを設定して、2 つの日時の間に作成または更新されたプログラムのみを返すことができます。 これは、新しい販促物や更新された販促物のセットを取得する場合に役立ちます。最も重要なのは、翻訳とビジネスインテリジェンスのユースケースです。

投稿日：_1970-01-01_ by _Kenny_

## Marketo Cloud 機能を使用したGoogle ビジネスロジックの拡張 – 

この記事では、次の簡単な例に基づいて、Google Cloud Platform （GCP）でMarketoをビジネスロジック機能で拡張するソリューションについて説明します。Marketo リードレコードの 3 つのカスタムフィールド：

* **OnLinePreference**：オンライン通信に対する見込み客/顧客の興味を示す増分スコア。
* **OfflinePreference**：オフライン通信に対する見込み客/お客様の興味を示す増分スコア。
* **環境設定**:GCP によって計算されたフィールドで、オフラインスコアがオンラインより高い場合は「オフライン」、逆の場合は「オンライン」と表示されます

このテクノロジは、より高度なビジネスロジックへの道を開き、最終的には外部 web サービスを呼び出し、結果をMarketoで変換および統合します。  

### Google Cloud Platform と関数について

[Google Cloud Platform](https://cloud.google.com/) （GCP）は、Google Search やYouTubeなど、Googleが社内でエンドユーザー向けに使用するのと同じインフラストラクチャ上で動作する、クラウドコンピューティングサービススイートです。 一連の管理ツールに加えて、コンピューティング、データストレージ、データ分析、機械学習、ビッグデータなどの一連のモジュール型クラウドサービスを提供します。 私たちのニーズに応じて、Compute Engine、App Engine、Kubernetes Engine など、多くの異なる GCP サービスを使用できましたが、次の主な利点のために（Betaに残っている） [Cloud Functions](https://cloud.google.com/functions) を選択しました。

* サーバーレスクラウドコンピューティングでは、HTTP 呼び出しなどのイベントに応答して、ロジックをオンデマンドで実行できます。
* サーバのメンテナンスと導入に伴う問題を軽減します。
* GCP は関数呼び出しごとにのみ支払われ、サーバーの稼働を維持する場合には支払われないので、コスト効率が高くなります。
* アプリケーションロジックにのみ焦点を当てるので、実装がシンプルで迅速です。
* 自動スケーリングで、非常に高いワークロードに対応。

この技術とその価格の詳細については、[GCP ウェブサイト ](https://cloud.google.com/) をご確認ください。 通常、このチュートリアルは重要なコストを発生させず、GCP 体験版の無料クレジット内に完全に収まります。  

### Google Cloud 環境の準備

Google Cloud アカウントが必要です。 このチュートリアルを実行するのに十分なクレジットで GCP を無料で試すことができます。[GCP web サイト ](https://cloud.google.com/) の「無料で試す」ボタンをクリックするだけです。 Googleの [HTTP チュートリアル ](https://cloud.google.com/functions/docs/calling) の「始める前に」の節のすべての手順に従います。

1. Cloud Platform プロジェクトを作成します。リソースを管理ページに移動します。
1. プロジェクトの請求を有効化：[ 請求を有効化 ](https://cloud.google.com/billing/docs/how-to/modify-project?visit_id=638816637273392093-1926929734&rd=1)
1. クラウド関数 API を有効にします。[API を有効にします ](https://accounts.google.com/InteractiveLogin?continue=https://console.cloud.google.com/flows/enableapi?apiid%3Dcloudfunctions%26redirect%3Dhttps://cloud.google.com/functions/docs/tutorials/http&followup=https://console.cloud.google.com/flows/enableapi?apiid%3Dcloudfunctions%26redirect%3Dhttps://cloud.google.com/functions/docs/tutorials/http&osid=1&passive=1209600&service=cloudconsole&ifkv=ASKV5Mh81NGNsqcJqhx7hst0KFnyA0MJ-2zay8ovyluBfpvDoM820nF9Wq_SKbC1m_sjQvvRNoKSuA)
1. [Cloud SDKのインストールと初期化 ](https://cloud.google.com/sdk/docs/)
1. Gcloud コンポーネントの更新とインストール

   **gcloud コンポーネントのアップデートと**&#x200B;**Gcloud コンポーネントのインストールベータ版**

1. Node.js 開発用の環境を準備します。[ セットアップガイドを参照してください ](https://cloud.google.com/nodejs/docs/setup)

### scoreCompare クラウド関数の実装

1. クラウド関数ファイルをステージングするクラウドストレージバケットを作成します。 これを行うには、次のコマンドラインを使用します。

   `gsutil mb gs://[YOUR_STAGING_BUCKET_NAME]`

   または、Google Cloud Web インターフェイスでプロジェクトを選択し、ストレージ メニューをクリックします。
   * ストレージバケットに一意の名前を付けます
   * デフォルトストレージクラスを選択
   * 最適な地域を選択

1. ローカルシステム上に、アプリケーションコード用のディレクトリを作成します。
1. 次のJavaScript コードを使用して、このディレクトリに「index.js」ファイルを作成します。コードは非常に理解しやすいです。 HTTP リクエスト本文の 2 つの入力パラメーターを JSON で解析し、処理を実行して、HTTP 応答を JSON でエンコードします。

```javascript
 /\*\*
     \* HTTP scoreCompare Cloud Function.
     \*
     \* @param {Object} req Cloud Function request context.
     \* @param {Object} res Cloud Function response context.
     \*/
    exports.scoreCompare = function scoreCompare (req, res) {
     var onlineScore=parseInt(req.body.onlineScore);
     var offlineScore=parseInt(req.body.offlineScore);
     console.log('/scoreCompare: got values onlineScore =' + onlineScore + ', offlineScore =' + offlineScore);
     var result;
     if (onlineScore>offlineScore) {result = 'online';} else {result = 'offline';}
     console.log('/scoreCompare: and result is ' + result);
     res.status(200).json({output: result}).end();
    };
```

HTTP トリガーを使用して scoreCompare 関数をデプロイします。 ディレクトリから次のコマンドを実行します。

**gcloud ベータ版ファンクション deploy [FUNCTION] —stage-bucket [YOUR_STAGING_BUCKET_NAME] —トリガー-http**

ここで [YOUR_STAGING_BUCKET_NAME] は、ステージング用クラウドストレージバケットの名前です。 この例では、次のようになります。

**gcloud ベータ版の関数 deploy scoreCompare – ステージバケット mktostorage —トリガー http**

1. コンソール出力のクラウド関数 URL （httpsTrigger URL）は次のようになります。`https://[YOUR_REGION]-[YOUR_PROJECT_ID].cloudfunctions.net/[FUNCTION]` ここで

   * [YOUR_REGION] は、関数がデプロイされている地域です。 関数のデプロイが完了すると、これがターミナルに表示されます。
   * [YOUR_PROJECT_ID] はクラウドプロジェクト ID です。 関数のデプロイが完了すると、これがターミナルに表示されます。
   * [FUNCTION] は関数名です。

   この例では、[**https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare**](https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare)
1. [Postman](https://www.postman.com/) などのツールを使用して関数をテストします。
   * HTTP 動詞：POST
   * URL: [https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare](https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare)
   * ヘッダー：content-type = application/json
   * 本文：{&quot;onlineScore&quot;:110, &quot;offlineScore&quot;:200}Output は {&quot;output&quot;: &quot;offline&quot;} を返します。

### Marketoの Webhook からクラウド関数を呼び出す

Marketoのリードレコードで、次の 3 つのカスタムフィールドを作成する必要があります。

* **OnlinePreference**：整数
* **OfflinePreference**：整数
* **Preference**：文字列

「scoreCompare」クラウド関数 URL とカスタムフィールドのトークンを使用して、Marketo管理インターフェイスから次の Webhook を作成します。 Marketoでトリガーされたスマートキャンペーンを使用して Webhook をテストします。

* **Marketo Webhook は、トリガーされたスマートキャンペーンからのみ呼び出すことができ、バッチスマートキャンペーンからは呼び出せません。**
* **クラウド機能を使用しない場合は、Google Cloud Platform アカウントに料金が発生しないように、クラウド機能を削除するか、プロジェクト全体を削除します。**

このチュートリアルがあなたの時間の価値があり、複雑な処理やサードパーティのサービスを含むより高度なシナリオについて考えさせてくれることを願っています。 良い例は、Googleの機械学習サービスであるGoogle Cloud AI を活用することです。 例えば、Marketo フォームのフリーテキストを解析して、Google Natural Language API でテキストの構造と意味を確認し、この分析をMarketoに保存できます。アイデアの洪水を開くだけです。

Posted on _2017-11-21_ by _Philippe_

## 2017 年秋のアップデート

2017 年秋リリースでは、Asset API にいくつかの機能強化をリリースしています。 以下のアップデートの完全なリストをご覧ください。

### プログラムを日付範囲別に参照

[ プログラムを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneEmailUsingPOST) エンドポイントに、日付範囲でプログラムを取得する機能が追加されました。 これは、`earliestUpdatedAt` パラメーターと `latestUpdatedAt` パラメーターを使用しておこないます。 任意の日時を持つどちらか一方または両方のパラメーターを設定して、2 つの日時の間に作成または更新されたプログラムのみを返すことができます。

### メールのプレビュー

多くの場合、[ メールの完全なコンテンツを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailFullContentUsingGET) エンドポイントを使用してメールをプレビューするようになりました。このエンドポイントは、シリアル化されたHTML バージョンのメールを返します。 すべてのトークン、スニペット、動的コンテンツおよび埋め込みコンポーネントは、完全にレンダリングされます。 任意の **leadId** パラメーターを渡して、特定のリードとして実行できます。

### Email 2.0 のHTMLを置換

[ メールの完全なコンテンツを更新 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/createEmailFullContentUsingPOST) エンドポイントが追加され、HTML メールコンテンツのブロックを置き換えられるようになりました。 Marketo Email 2.0 エディターを使用してMarketo メールのHTML コードを編集すると、メールとそのテンプレートとの関係が壊れます。詳しくは、[ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/edit-an-emails-html) を参照してください。 このエンドポイントを使用すると、関係が壊れたメールのHTMLのコンテンツをプログラムによって更新できます。 さらに、関係が壊れたメールと互換性を持たせるために、他のすべてのメールライフサイクル関連エンドポイントを変更しました。

* メールのドラフトを承認
* メールを未承認
* メールの削除
* メールのドラフトを破棄
* メールの複製
* メールメタデータを更新

### その他の機能強化

* 日付範囲フィルターの最大タイムスパンが 31 日に増えました。 これは、[ 一括リード抽出フィルター ](/help/rest-api/bulk-lead-extract.md) （createdAd または updatedAt）および [ 一括アクティビティ抽出フィルター ](/help/rest-api/bulk-activity-extract.md) （createdAt）に関連します。

Posted on _2017-12-15_ by _David_

## テスト – コミュニティの外部ビデオリンク

[ メール配信品質の電源パックのチュートリアルビデオ ](https://nation.marketo.com:443/t5/product-space-archive-videos/email-deliverability-power-pack-tutorial-video/m-p/283550)  

Posted on _1970-01-01_ by _David_

## 2018 年冬のアップデート

2018 年冬リリースでは、API にいくつかの機能強化をリリースしています。 以下のアップデートの完全なリストをご覧ください。

### トリガーキャンペーンの有効化/無効化

トリガーキャンペーンをアクティブ化および非アクティブ化する機能が追加されました。これにより、プログラムテンプレートの自動化プロセスを簡素化できます。 これを実現するには、新しく追加された 2 つのエンドポイント（[ スマートキャンペーンをアクティブ化 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/activateSmartCampaignUsingPOST) および [ スマートキャンペーンを非アクティブ化 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/deactivateSmartCampaignUsingPOST) を呼び出します。 詳しくは、[Campaigns](/help/rest-api/assets.md) ドキュメントのトリガーの節を参照してください。

### 名前によるプログラムを取得

[ 名前によるプログラムの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getProgramByNameUsingGET) エンドポイントに 2 つのパラメーターを追加して、プログラムコストとプログラムタグを簡単に取得できるようにしました。 詳しくは、**プログラム** ドキュメントの **includeCosts** および [includeTags](/help/rest-api/assets.md) パラメーターを参照してください。

### その他の機能強化

一括抽出 API は「ワークスペース対応」になりました。 [ カスタムサービス ](/help/rest-api/custom-services.md) 用に API 専用ユーザーを作成する場合、1 つ以上のワークスペースに対して、API アクセスを持つユーザーの役割を選択する必要があります。 以前は、カスタムサービスには、すべてのワークスペースへのアクセス権が付与されていました。 現在、カスタムサービスには、API のみのユーザーの作成時に選択したワークスペースへのアクセスのみが許可されています。

Posted on _2018-03-02_ by _David_

## 2018 年春の更新

2018 年春リリースでは、新しい REST API と web トラッキングプライバシーの機能強化をリリースしています。 以下のアップデートの完全なリストをご覧ください。

REST API

### 静的リスト CRUD

静的リスト レコードをリモートで作成、読み取り、更新、および削除できるようにします。 メンバーシップの入力や維持を含め、静的リストのライフサイクル全体を REST API を使用して管理できます。 詳しくは、[ こちら ](/help/rest-api/static-lists.md) を参照してください。

### カスタムアクティビティメタデータ

ユーザーがカスタムアクティビティレコードをリモートで作成できるようにします。 タイプやタイプ属性の操作を含め、REST API を使用して、カスタムアクティビティのライフサイクル全体を管理できます。 詳しくは、[ こちら ](/help/rest-api/activities.md) を参照してください。

### スマート・リストのメタデータ

スマート・リスト・レコードのリモートでの読取り、クローニングおよび削除を可能にします。 REST API を使用したスマートリストの管理を有効にする。 詳しくは、[ こちら ](/help/rest-api/smart-lists.md) を参照してください。

### Web トラッキングプライバシー

Munchkin JavaScriptの web トラッキングコードが強化され、次のようなプライバシー関連の機能強化が含まれるようになりました。

* オプトアウト – 訪問者が web トラッキングを永続的にオプトアウトできる機能。 詳しくは、[ こちら ](/help/javascript-api/lead-tracking.md) を参照してください。
* IP アドレスの匿名化 – web 訪問者の IP アドレスを匿名化する機能を提供することで、ローカルおよび国際的なプライバシー規制に準拠します。 **anonymizeIP** 設定パラメーター [ こちら ](/help/javascript-api/configuration.md) を参照してください。

### その他の機能強化

* [ フォルダーを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getFolderUsingGET) エンドポイントは、ルート以外の親と maxDepth=1 が指定されている場合、すべてのフォルダーを返すようになりました。
* [ID でランディングページを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getLandingPageByIdUsingGET) エンドポイントは、すべての場合（http://またはhttps://）でプロトコルを含む URL 属性を返すようになりました。

Posted on _2018-06-29_ by _David_

## 2018 年夏のアップデート

2018 年夏リリースは、主にマイナーな機能強化と欠陥解決で構成されるメンテナンスリリースです。 以下のアップデートの完全なリストをご覧ください。

### REST API

* 最初に不必要に省略された「E メールの廃棄」フィールドがサポートされるようになりました。 これらのフィールドは、必要に応じて、REST での読み取りと書き込みに使用できるようになりました。
   * ブロックリストに登録済み
   * マーケティング中断
   * メールの中断
   * 相対的緊急度
* [ フィルタータイプ別リードの取得 ](https://developer.adobe.com/marketo-apis/api/lead-database-endpoint-reference/#/Leads/getLeadsByFilterUsingGET) エンドポイントで、leadPartionId が filterType としてサポートされるようになりました。

### 欠陥の解決

**REST エンドポイント**

**説明**

[ プログラムを承認 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveProgramUsingPOST)

プログラムの作成時にブロックの操作不可メールを false に設定していた場合、プログラムを承認する呼び出しは true にリセットされます。

[一括抽出](/help/rest-api/bulk-extract.md)

抽出出力ファイルで特定の Unicode 文字が破損していました。

[ プログラムの複製 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST)

* メールプログラムをクローンした場合、初期設定に関係なく、結果のプログラムで SmartList フィルターロジックが「すべて」にリセットされていました。
* 静的リスト（削除された）を含んだプログラムを複製しようとすると、「次のアセットはサポートされていません」という 709 エラーが発生し :List す。
* ワークスペース間でプログラムをクローンしようとすると、「プログラムをクローンできません」という 611 エラーが発生します。

[ID による静的リストを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getStaticListByIdUsingGET)

カスタムサービスが読み取り専用アセットの役割の権限を持っている場合は、603 「アクセスが拒否されました」エラーが発生します。

[ リードをMarketoにプッシュ ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/pushToMarketoUsingPOST)

**cookies** 属性が **入力** 配列のリードオブジェクトで指定されていた場合、以前の匿名アクティビティは新しく作成されたリードに関連付けられませんでした。

[キャンペーンをスケジュール](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST)

**runAt** 日付をずっと先の日付に指定した場合、キャンペーンは実行されず、**success=true** が返されます。 ここで、**runAt** の日付が 2 年以上先の場合、エラー [1042](/help/rest-api/error-codes.md) が返されます。

[ リードを同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST)

（新しいリードを既存の会社に関連付けるために） `action=createDuplicate` および `externalCompanyId` パラメーターを指定した場合、リードは（指定した会社ではなく）空の会社に関連付けられました。

#### その他

* すべてのエンドポイント応答から次のデータ変更値を削除しました：mktoClientReqId。 これは内部でのみ使用されていました。
* エラー参照機能を追加しました。 検索ボックスに REST API エラーコードを入力し、その下にあるオートコンプリートリストからを選択して、エラーの説明にジャンプします。
* [ エンドポイント参照 ](/help/rest-api/endpoint-reference.md) ページを追加しました。 これは、すべての REST API エンドポイントの並べ替え可能なリストです。 また、このページを使用して、アプリケーションで必要な最小限の権限セットを生成することもできます。 これは、カスタムサービスを作成する際に便利です。

Posted on _2018-10-12_ by _David_

## 2018 年秋のアップデート

2019 年秋リリースは、主にマイナーな機能強化と欠陥解決で構成されるメンテナンスリリースです。 以下のアップデートの完全なリストをご覧ください。

### 機能強化

* [Asset API](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/email-cc) のサポート [ メール CC フィールド ](/help/rest-api/assets.md) を追加しました。 CC フィールドの設定は、承認/複製操作（メールまたはメールテンプレートのドラフト承認、メールまたはプログラムの複製）の間、期待どおりに反映されます。 すべてのメール関連エンドポイントは、**ccFields** プロパティで CC Fields 値を返すようになりました。 以下の応答を下にスクロールして、例を確認します。 この変更は、次のエンドポイントに影響します。[ID によるメールの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailByIdUsingGET)、[ 名前によるメールの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailByNameUsingGET)、[ メールの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailUsingGET)、[ メールのドラフトの承認 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveDraftUsingPOST)、[ メールテンプレートのドラフトの承認 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveDraftUsingPOST_1)、[ メールの複製 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneEmailUsingPOST)、[ プログラムの複製 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST)

```json
{
    "success": true,
    "errors": [],
    "requestId": "cc96#166e836348b",
    "warnings": [],
    "result": [
        {
            "id": 2061,
            "name": "Test Email",
            "description": "This is a test",
            "createdAt": "2018-11-06T05:27:10Z+0000",
            "updatedAt": "2018-11-06T08:33:16Z+0000",
            "url": "<https://app-sjqe.marketo.com/#EM2061A1LA1>",
            "subject": {
                "type": "Text",
                "value": "This is a test with CC Fields"
            },
            "fromName": {
                "type": "Text",
                "value": "Tommy Tester"
            },
            "fromEmail": {
                "type": "Text",
                "value": "<tommy.tester@marketo.com>"
            },
            "replyEmail": {
                "type": "Text",
                "value": "<tommy.tester@marketo.com>"
            },
            "folder": {
                "type": "Program",
                "value": 7494,
                "folderName": "Initiative"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": false,
            "status": "approved",
            "template": 1218,
            "workspace": "Default",
            "version": 2,
            "autoCopyToText": true,
            "ccFields": [
                {
                    "attributeId": "855",
                    "objectName": "lead",
                    "displayName": "emailcc",
                    "apiName": "emailcc"
                },
                {
                    "attributeId": "857",
                    "objectName": "lead",
                    "displayName": "leadDetails",
                    "apiName": "leadDetails"
                },
                {
                    "attributeId": "859",
                    "objectName": "company",
                    "displayName": "headquarters",
                    "apiName": "headquarters"
                }
            ]
        }
    ]
}
```

### 欠陥の解決

* [Asset API](https://experienceleague.adobe.com/ja/docs/marketo/using/home) のサポートを調整しました [ 複数のブランディングドメイン ](/help/rest-api/assets.md)。 以前は、メールのドラフトを承認する際、メールをクローンする際、またはプログラムをクローンする際に、複数のブランディングドメインの設定が反映されていませんでした。 この問題は修正されました。 この変更は、次のエンドポイントに影響します：[ メールのドラフトを承認 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveDraftUsingPOST)、[ メールを複製 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneEmailUsingPOST)、[ プログラムを複製 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST)
* [apiOnly](/help/javascript-api/configuration.md) 設定を追加しました。 デフォルトでは、Munchkin タグを含む web ページがブラウザーに読み込まれると、「Visits Web Page」イベントが発生します。 場合によっては、これは望ましくないこともあります。 例えば、このイベントが発生した場合に完全なコントロールを必要とする単一ページ web アプリケーションなどです。 このユースケースをサポートするために、新しい **apiOnly** 設定を追加しました。 true に設定した場合、Munchkin タグはページの読み込み中に「Web ページを訪問」アクティビティを生成しません。
* [domainSelectorV2](/help/javascript-api/configuration.md) 設定を追加しました。 デフォルトでは、Munchkin タグは、2 文字の [ 国コードのトップレベルドメイン ](https://en.wikipedia.org/wiki/Country_code_top-level_domain) （例：.io、.co、.ly）を持つサイトでホストされる web ページを正しく処理しません。 これにより、Munchkinの cookie ドメイン属性が正しく設定されません。 より良い標準のエクスペリエンスを実現するために、新しい **domainSelectorV2** 設定を追加しました。 true に設定すると、改善されたアルゴリズムを使用して、Munchkin cookie ドメイン属性が自動的に設定されます。
* [ オプトアウト ](/help/javascript-api/lead-tracking.md) Cookie ドメインを調整しました。 場合によっては、Munchkin オプトアウト Cookie のドメイン属性（mkto_opt_out）が正しく設定されていませんでした。 Munchkin オプトアウト cookie は、Munchkin cookie （_mkto_trk）と同じロジックを使用して、**domainLevel** 設定を遵守するなど、ドメイン cookie 属性を決定するようになりました。
* Android アプリケーション開発者は、このSDKでGoogle[Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/) （FCM）を直接使用できるようになりました。 詳しくは、[ こちら ](/help/mobile/installation.md) を参照してください。

Posted on _2018-12-07_ by _David_

## 2019 年春の更新

2019 年春リリースは、主にマイナーな機能強化と欠陥解決で構成されるメンテナンスリリースです。 以下のアップデートの完全なリストをご覧ください。

Posted on _2019-03-19_ by _David_

## 2019 年 6 月更新

2019 年 6 月リリースは、主にマイナーな機能強化と欠陥解決で構成されるメンテナンスリリースです。 以下のアップデートの完全なリストをご覧ください。

### REST API

1. 一括書き出しステータスエンドポイントにチェックサムを追加しました。 チェックサムを取得したファイルのハッシュと比較して、取得したファイルの整合性を確認できます。 チェックサムは、エクスポートされたファイルの SHA-256 ハッシュであり、エクスポートジョブが完了すると fileCheckSum 属性に保存されます。

次のエンドポイントはチェックサムを返します：[ エクスポートリードジョブステータスの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsStatusUsingGET)、[ エクスポートリードジョブの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsFileUsingGET)、[ エクスポートアクティビティジョブステータスの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsStatusUsingGET)、[ エクスポートアクティビティジョブの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportActivitiesUsingGET)

#### 欠陥の解決

1. 整数フィールドに小数値を読み込む際の [ カスタムオブジェクトの一括読み込み ](/help/rest-api/bulk-custom-object-import.md) の問題を修正しました。 修正前は、整数の部分を割り当て、小数部分を破棄することで、小数を整数に変換していました（例えば 5.432 は 5 に変換されていました）。 データの不一致を含む行ごとに、「フィールド Source ID のデータ型が無効です」エラーが生成されるようになりました。
1. [ プログラムの複製 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) エンドポイントを使用して作成されたメールプログラムが、特定の場合に通信制限設定に従わない問題を修正しました。
1. [ ランディングページのドラフトを承認 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveLandingPageUsingPOST) エンドポイントで 611 が返される問題を修正しました。 ランディングページにメール購読解除フォームが含まれている場合、「システムエラー」が発生する。
1. [ ランディングページのドラフトを承認 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveLandingPageUsingPOST) エンドポイントで 611 が返される問題を修正しました。 [ ランディングページのクローン ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneLandingPageUsingPOST) エンドポイントを使用してランディングページのクローンが作成されたときの「システムエラー」。

#### 廃止予定機能

1. [Email Editor 1.0 の廃止 ](https://nation.marketo.com:443/t5/knowledgebase/email-editor-1-0-is-being-deprecated-june-18th/ta-p/250666) の一環として、1.0 Email Assetsは 2019 年末に読み取り専用になります。 すべての 1.0 Email Assetsは、2.0 に変換する必要があります。descriDiscard Email Draft, bed[ こちら ](https://nation.marketo.com:443/t5/knowledgebase/email-editor-1-0-is-being-deprecated-june-18th/ta-p/250666) とします。 1.0 Email Assetsを変更しようとするすべての Email 関連のエンドポイントに警告を追加しました。 次に、警告を含む応答の例を示します。

`{` `"success": true,` `"errors": [],` `"requestId": "15c57#16b338d6e75",` `"warnings": [` `"This is a v1 email asset. API support for modifying v1 emails is being dropped, and this operation will not work on v1 emails in the future. To avoid service interruptions, upgrade this and related assets by editing them in the User Interface."` `],` `"result": [` `"{\"service\":\"sendTestEmail\",\"result\":true}"` `]` `}`

次のメール関連のエンドポイントは、警告を返します。

* メールの完全なコンテンツを更新
* メールコンテンツを更新
* サンプルメールを送信
* メールを未承認
* プログラムを複製
* メールの複製
* メールのドラフトを承認
* メール動的コンテンツセクションを更新
* メールメタデータを更新
* プログラムを承認

メールスクリプティング（Apache Velocity）

#### 廃止予定機能

1. セキュリティ上の理由から、Velocity スクリプト機能のサブセットが無効になりました。 これには、getClass （）、$class、$context、$text のメソッドと変数が含まれます。 詳しくは[こちら](https://nation.marketo.com:443/t5/knowledgebase/unsupported-velocity-tools-disabled-in-june-2019-release/ta-p/251177)をご覧ください。

Posted on _2019-06-14_ by _David_

## 2019 年 8 月の更新

2019 年 8 月に、新しい REST API をリリースし、既存の API を強化して、欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

### 機能強化

1. Smart Campaign のライフサイクル機能の強化。 スマートキャンペーンで名前による取得、作成、更新、複製、削除の操作を実行できる新しいエンドポイントが追加されました。 完全な情報については、[ こちら ](/help/rest-api/smart-campaigns.md) を参照してください。
1. スマートリストエンドポイントが強化され、クエリ機能が改善されました。
   1. [ID によるスマートリストの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListByIdUsingGET) エンドポイントで **includeRules** boolean パラメーターを渡す際に、スマートリストルールの説明（トリガーとフィルター）を返すようになりました。
   1. [ スマートリストの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListsUsingGET) エンドポイントで、**earliestUpdatedAt** および **latestUpdatedAt** 日時パラメーターを渡す際に、日付範囲で結果をフィルタリングできるようになりました。 さらに、このエンドポイントは、キャンペーンおよびメールプログラムのメンバーであるスマートリストを返すようになりました。
1. スマートリスト定義を抽出するためのエンドポイントを追加しました。
   1. [ スマートキャンペーン ID によるスマートリストの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListBySmartCampaignIdUsingGET) エンドポイントは、特定のスマートキャンペーン ID のスマートリストレコードを返します。
   1. [ プログラム ID によるスマート リストの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListByProgramIdUsingGET) エンドポイントは、特定のプログラム ID のスマート リスト レコードを返します。
1. [ メールコンテンツを更新 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/updateEmailContentUsingPOST) エンドポイントを強化し、テンプレートから（件名、名前、メールから、返信先）切れたメールのメールヘッダーフィールドを更新できるようになりました。 テンプレートからの離脱については、[ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/edit-an-emails-html) で説明しています。

### 欠陥の解決

1. 承認されたランディングページで [ ランディングページを削除 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/deleteLandingPageByIdUsingPOST) を呼び出すと、ランディングページが削除される問題を修正しました。 「709、承認されたランディングページを削除できません」というエラーが正しく返されるようになりました。 [LM-127271]
1. [ サンプルメールを送信 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/sendSampleEmailUsingPOST) エンドポイントで 611 が返される問題を修正しました。 メールがテンプレートから破損していた際の「システムエラー」。 [LM-127288]
1. [ プログラムを削除 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) エンドポイントの問題を修正しました。「709, プログラムを削除できません。 アセットが他の場所で使用されているか、削除できません」というエラーが発生します。 [LM-125431]

### 廃止予定機能

1. メールエディター 1.0 の API サポートは、2020 年 1 月に非推奨（廃止予定）になる予定です。 その前に、アセットを 2.0 に変換することを忘れないでください。 1 月以降に Email 1.0 アセットに書き込みまたは複製を試みると、警告ではなくエラーが発生します。 メール API について詳しくは [ こちら ](https://nation.marketo.com:443/t5/knowledgebase/email-2-0-and-email-api-faq-s/ta-p/251423) を参照してください。
1. Adobeのワールドクラスのセキュリティ標準に準拠するために、2019 年 12 月 13 日（PT）以降、Transport Layer Security （TLS） 1.0 および 1.1 のサポートを廃止する予定です。 1.2 プロトコルに準拠していないMarketoと統合されたシステムは、Marketo Engage サービスへのアクセスが失われる可能性があります。 Marketo Engageへのアクセスを維持するには、2019 年 12 月 13 日（PT）より前に、すべてのクライアントシステムが TLS 1.2 準拠であることを確認してください。 詳細は[こちら](https://nation.marketo.com:443/t5/knowledgebase/tls-1-0-1-1-deprecation-faq/ta-p/249085)をご覧ください。

1. すべてのスマートキャンペーン関連コンテンツが [ スマートキャンペーン ](/help/rest-api/smart-campaigns.md) メニュー項目（REST API/Assetsの下）に配置されるようになりました。

Posted on _2019-08-16_ by _David_

## 2020 年 1 月更新

2020 年 1 月には、新しい REST API をリリースし、既存の API を強化して、欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

* カスタムオブジェクトスキーマ定義をプログラムで作成する機能を追加しました。 これにより、カスタムオブジェクトを 1 回定義し、必要な数のインスタンスにプロビジョニングできます。 これにより、ユーザーはサンドボックスとセンターオブエクセレンスのモデルを効果的に活用できます。 また、ISV はお客様のオンボーディングプロセスを簡素化できます。 カスタムオブジェクトメタデータ API にアクセスするには、適切なサブスクリプションタイプが必要です。
* プログラムメンバーの一括読み込みおよび書き出し機能を追加しました。 この新しいエンドポイントセットは、非同期の一括処理ジョブを作成するための既存のMarketo REST API パターンに従います。 プログラムメンバーレコードには、プログラムメンバーのカスタムフィールドやリードフィールドを含めることができます。
* プログラムメンバーカスタムフィールドをフォームフィールドとして使用できるように、利用可能なフォームプログラムメンバーフィールドを取得エンドポイントを追加しました。 これにより、Marketo フォームで使用できるすべてのプログラムメンバーカスタムフィールドのリストが返されます。
* 特定のメールテンプレートに依存するメールアセットのリストを返す [ ユーザーが使用するメールテンプレートを取得 ](/help/rest-api/email-templates.md) エンドポイントを追加しました。 これにより、潜在的なメールテンプレートの変更の影響をすばやく把握し、これらの依存関係により簡単に対処できます。

Posted on _2020-01-17_ by _David_

## すべてのカスタムオブジェクトの取得方法

Marketo API を使用してすべての [ カスタムオブジェクト ](https://experienceleague.adobe.com/ja/docs/marketo/using/home) （CO）のリストを取得する方法を尋ねられることがよくあります。 CO のクエリには、その名前よりも多くの情報が必要です。各 CO に関する _事前_ の知識も必要です。 API には知識を直接問い合わせる方法がないので、その知識を取得する方法は明確でない可能性があります。 Marketo Engageの多くの目標と同様に、スマートリストでは人物（リード）にリンクされた CO に対する回答を提供します。 スマートリストは会社との動作が異なり、会社がフィルターのオブジェクトのタイプにリンクされているすべてのユーザーのリストが表示されるので、目標に応じて会社の重複を排除する必要がある場合があります。 新しいカスタムオブジェクトが承認されるたびに、関連するフィルターが作成されます。 「**CO NAME**」という形式で名前が付けられます。 次の例では、カスタムオブジェクト名は「**Conference Track Subscription」で** そのフィルターの名前は「**Has Conference Track Subscription**」です。 スマートリストを作成したら、[ カスタムオブジェクトエンドポイント ](/help/rest-api/custom-objects.md) を使用して、関連付けられた CO のクエリを実行するために必要な情報を取得できます。 リンクされたフィールド（ID またはメールアドレス）が含まれていることを確認してリストをエクスポートします。 [ 一括リード抽出 API](/help/rest-api/bulk-lead-extract.md) フィルターの **smartListName** または **smartListId** フィルターによるフィルタリング、または [UI からの書き出し ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/managing-people-in-smart-lists/export-people-to-excel-from-a-list-or-smart-list) を使用して書き出すことができます。 次の手順では、リンクされた各フィールド値を使用して、関連するカスタムオブジェクトを個別にクエリします。 この例では、カスタムオブジェクトの名前は **&quot;Conference Track Subscription&quot;** で、API 名は **conferenceTrackSubscription_c** です。 API 名は、UI で「**API Name**」として見つけ、API を使用して「**name**」として見つけます。  Admin | Marketo カスタムオブジェクト [/caption] そして、[List Custom Objects API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/listCustomObjectsUsingGET) エンドポイントによって返されるフラグメントは次のとおりです。

```json
{
    "name": "conferenceTrackSubscription_c",
    "displayName": "Conference Track Subscription",
    "description": "Track subscription for conference attendees",
    "createdAt": "2020-01-13T19:50:06Z",
    "updatedAt": "2020-01-13T19:50:06Z",
    "idField": "marketoGUID",
    "dedupeFields": [
        "subscriptionID"
    ],
    "searchableFields": [
        [
            "subscriptionID"
        ],
        [
            "marketoGUID"
        ],
        [
            "leadID"
        ]
    ],
    "relationships": [
        {
            "field": "leadID",
            "type": "child",
            "relatedTo": {
                "name": "Lead",
                "field": "Id"
            }
        }
    ]
}
```

スマート・リスト内の個人に 1 対 1 （1:1）または 1 対多（1:N）で関連付けられたカスタム・オブジェクトを取得するには、次のようなリクエストを行います：

`GET /rest/v1/customobjects/conferenceTrackSubscription_c.json?filterType=leadID&filterValues=1000302,1000303,1000304,1000306,1000307`

この例では、このカスタムオブジェクトは **leadID** フィールドによって人物にリンクされているので、フィルタータイプは「**leadID**」となります。 フィルター値パラメーターは、スマートリストの書き出しから取得した ID のコンマ区切りリストです。 リクエストには、1 つのリクエスト URI に収めることができる限り、最大 8K 文字のフィルター値を含めることができます。 この長さを超えるリクエストは、414 HTTP レベルのエラーコードを返します。 応答は複数のチャンクで返される場合があります。 その場合は、**moreResult** が **true** になり、**nextPageToken** が含まれます。 その後、（moreResult[ が ](/help/rest-api/paging-tokens.md)false **になるまで、結果を** ページスルー **する必要があ** ます。 上記の API リクエストの結果の一部を次に示します。

```json
"result": [
    {
        "seq": 0,
        "marketoGUID": "d6b3ed3d-4eb8-4066-a9cd-184c8d385cfe",
        "leadID": "1000302",
        "subscriptionID": "4ad59184-6bf1-4eeb-a583-d82aeee68210",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    },
    {
        "seq": 1,
        "marketoGUID": "e5e0aba4-f27f-494d-93ed-9cb580989bf3",
        "leadID": "1000303",
        "subscriptionID": "fc5596d5-6fa2-4848-b4a2-89d96e245c59",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    },
    {
        "seq": 2,
        "marketoGUID": "e65007cd-86b1-4c17-8d55-057c96e1788a",
        "leadID": "1000304",
        "subscriptionID": "7e54b8a0-2170-4d81-a809-4eac349508d0",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    },
    {
        "seq": 3,
        "marketoGUID": "39d956b2-85e2-4c24-94e7-e9fa5a09d3d0",
        "leadID": "1000306",
        "subscriptionID": "644c8e5b-fc0c-4d4a-80f8-358a65ce0a68",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    },
    {
        "seq": 4,
        "marketoGUID": "a2151350-50c8-437f-bc71-7a054bb601f0",
        "leadID": "1000307",
        "subscriptionID": "bf14218c-ae6a-42b3-a14e-f7182903cbcd",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    }
```

これで、各カスタム・オブジェクトの値がスマート・リスト内の個人に直接関連付けられ、値を取得する以外に、**marketoGUID** を使用してこれらのオブジェクトを [ 更新 ](/help/rest-api/custom-objects.md) または [ 削除 ](/help/rest-api/custom-objects.md) できます。 多対多の関係の人物に関連付けられたカスタムオブジェクトの場合（N:N）、上記のテクニックは、各人物を複数の第 2 レベル CO に接続する仲介オブジェクトである第 1 レベルのオブジェクトを返します。

これらの第 2 レベル CO を取得するには、リンク フィールドと第 1 レベル中間オブジェクトから抽出された値をフィルタリングして、第 2 レベル CO タイプの新しいクエリ セットを開始します。 例えば、上記の「**Conference Track Subscription」オブジェクトには** おそらく **subscriptionID** によってリンクされる「**&quot;Session&quot;** と呼ばれるセッションを表す別のレベルのオブジェクトを含めることができます。 上記の電話会議トラック サブスクリプションにリンクされたセッションを取得するリクエストは、次のようになります：

`GET /rest/v1/customobjects/session_c.json?filterType=subscriptionID&filterValues=4ad59184-6bf1-4eeb-a583-d82aeee68210,e5e0aba4-f27f-494d-93ed-9cb580989bf3,e65007cd-86b1-4c17-8d55-057c96e1788a,39d956b2-85e2-4c24-94e7-e9fa5a09d3d0,bf14218c-ae6a-42b3-a14e-f7182903cbcd`

_脚注_ _1）**smartListName**&#x200B;および&#x200B;**smartListId**&#x200B;フィルタータイプが、一部の購読で使用できない。 サブスクリプションで利用できない場合は、書き出しリードジョブの作成エンドポイントを呼び出すとエラーが発生します（**「1035、ターゲットのサブスクリプションでサポートされていないフィルタータイプ」**）。 お客様は、Marketo サポートに連絡して、この機能をサブスクリプションで有効にすることができます。_

_2020-01-14_ に投稿しました：_Tony_

## すべてのユーザーを取得する方法（リード）

すべてのユーザー（リード）をMarketo Engage インスタンスから取得するために必要なプロセスに関する問い合わせが多くあります。 役に立つ答えは多くありますが、これほど完璧な答えはありません。 Marketoの一括抽出 API を使用して、すべてのリードを抽出するために必要な重要な概念をいくつか特定しました。 その他の詳細はすべて、私が作成したデモコードから学ぶことができます。 この投稿を読み、デモコードを探索すると、Marketo Engage インスタンスからすべてのリードを取得するために必要な情報がすべて得られます。

### 概要

コアテクニックでは [Bulk Lead Extract API](/help/rest-api/bulk-lead-extract.md) を使用します。 フィルターなしで一括リード書き出しジョブを作成できそうかもしれませんが、次の操作はできません。**API にはフィルターが必要です**。 使用可能なフィルターは、**createdAt**、**staticListName**、**staticListId、** **updatedAt**、**smartListName**、および **smartListId** です。 フィルターのないスマートリストによるフィルタリングも魅力的です。 それを試してみると、システムは、フィルターのないスマートリストを扱うのに十分なスマートさがあることがわかります。API にも、ここでフィルターが必要です。 フィルターが必要なので、使用する信頼できる正規フィルターは **createdAt** です。 このフィルタータイプでは日時範囲を最大 31 日間使用できるので、複数のジョブを実行して結果を組み合わせる必要があります。 まず、ターゲットインスタンス内のリードに対して作成可能な最も古い日付を見つけます。 この可能な最も古い日付から、31 日 – 1 秒のジョブを作成します（これについては後で詳しく説明します）。 各ジョブを作成したら、キューに入れて、完了するまで待ちます。 次に、結果のファイルをダウンロードし、チェックサムを使用して整合性を確認します。 最後に、ID でリードの重複を排除し、一意のリードを出力の CSV ファイルに書き込みます。

### 最も古いリードを見つける

少しの「トリック」を使用して、ターゲットインスタンスのリードに対して可能な限り古い日付を取得しています。 このタスクに専用の API エンドポイントはないので、少し創造性が必要です。 実行するのは、**maxDepth = 1 を持つすべてのフォルダーをクエリすることで** インスタンス内のすべての最上位フォルダーのリストが表示されます。 それから私は **createdAt** の日付を収集し、それらを解析し、最も古い日付を見つけます。 この方法が機能するのは、一部のデフォルトの最上位フォルダーがインスタンスで作成され、それ以前はリードを作成できなかったからです。

### 必須フィールドを選択

抽出する必要があるフィールドを決定する必要があります。 [ リード 2 のエンドポイントを説明 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeUsingGET_2) を使用して、ターゲットインスタンスで使用可能なフィールドを見つけます。 そのリクエストへの応答には、「fields」という名前のリストが含まれます。 応答の例から抜粋を以下に示します。

```json
  "fields": [
      {
          "name": "AccountSource",
          "displayName": "Account Source",
          "dataType": "string",
          "length": 40,
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "acquisitionProgramId",
          "displayName": "Acquisition Program",
          "dataType": "reference",
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "Active_c",
          "displayName": "Active",
          "dataType": "string",
          "length": 255,
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "address",
          "displayName": "Address",
          "dataType": "text",
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "Address_lead",
          "displayName": "Address (L)",
          "dataType": "string",
          "length": 255,
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "annualRevenue",
          "displayName": "Annual Revenue",
          "dataType": "currency",
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "anonymousIP",
          "displayName": "Anonymous IP",
          "dataType": "string",
          "length": 255,
          "updateable": true,
          "crmManaged": false
      }, ...
```

このエンドポイントは、標準フィールドとカスタムフィールドの両方を含む完全なリストを返します。 リクエストするフィールドが多いほど、書き出しジョブの完了に時間がかかり、結果のファイルが大きくなります。 通常は、必要なフィールドのみを選択します。 使用可能なすべてのフィールドを要求することを防ぐフィールドはないので、デモを行います。 エクスポートジョブを作成する際に必要なフィールド識別子は **name** 値です。 名前の値をすべてのフィールド名のリストに抽出します。 次に、各エクスポートジョブを作成する際に、使用可能なすべてのフィールドをリクエストするために使用します。

### 書き出しジョブの日付範囲：31 日

各書き出しジョブは最大 31 日までです。 使用しているデモインスタンスは 2016 年 8 月に作成されたので、今は 40 人以上のジョブを作成する必要があります。 これは、最初の作成日からの日数を 31 で割った値です。 API を使用すると、2 つのエクスポートジョブを同時に処理できるので、2 つのジョブを並行して実行して抽出できます。 一括抽出ジョブは他のすべての統合で共有されるリソースなので、私はうまくやっていくつもりです。 他の統合に使用できるその他のジョブを残し、1 つのジョブを順番に実行する方法を示します。 **createdAt** フィルターに使用する日付は、[ISO 8601 仕様 ](https://www.w3.org/TR/NOTE-datetime) を使用して書式設定されます。 タイムゾーンは常に GMT （Z+0000）なので、単に「Z」または「+00:00」として表されます。 2016 年 8 月 1 日は **2016-08-01T00:00:00+00:00** で、31 日後は 2016 年 9 月 1 日（**2016-09-01T00:00:00+00:00）です。** 開始時刻と終了時刻の両方が含まれているので、その終了時刻から 1 秒差し引きます。**2016-09-01T00:00:00+00:00** は **2016-08-31T23:59:59+00:00** になります。 秒を引くと、重複する時間を回避できます。 デフォルトは GMT なので、**Z** または **+00:00** をオフにすることもできます。

### 重複排除

重複時間を避けるという手間を惜しみましたが、重複除外も導入しました。 これは、時間が変更され（[ 夏時間 ](https://en.wikipedia.org/wiki/Daylight_saving_time)）、値があいまいになるエッジケースがあり、その結果、Marketoの Bulk Extract API が、予期しない重複リードを返す可能性があるためです。 これが発生することはまれですが、日時フィルター範囲を使用する統合では考慮する必要があります。 私は時間が包括的であることを明確にするために 1 秒を取り除きました。 **2016-08-01T00** 00Z **および** 2016-09-01T00 **00Z:00: の** createdAt **および :00:endAt** でジョブを作成しても、それぞれ **2016-09-01T00:00:00Z** で作成されたリードは含まれないと考めないでください。

### ジョブの作成

最初の手順は、[ 書き出しリードジョブの作成エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createExportLeadsUsingPOST) を使用してジョブを作成することです。 このデモでは、最初の書き出しジョブを作成するリクエストは次のようになります。

`POST /bulk/v1/leads/export/create.json`

```json
{ "filter": {"createdAt": {"startAt": "2016-08-01T00:00:00",
                           "endAt": "2016-09-01T00:00:00"}},
"fields":["AccountSource","acquisitionProgramId","Active_c","address","Address_lead","annualRevenue","anonymousIP","BillingAddress","billingCity","billingCountry","BillingGeocodeAccuracy","BillingLatitude","BillingLongitude","billingPostalCode","billingState","billingStreet","blackListed","blackListedCause","city","CleanStatus","CleanStatus_account","company","CompanyDunsNumber","contactCompany","cookies","country","createdAt","customfield","DandbCompanyId","DandbCompanyId_account","dateOfBirth","dddS","department","doNotCall","doNotCallReason","dS","dueDate","DunsNumber","email","EmailBouncedDate","EmailBouncedReason","emailInvalid","emailInvalidCause","emailSuspended","emailSuspendedAt","emailSuspendedCause","externalCompanyId","externalSalesPersonId","facebookDisplayName","facebookId","facebookPhotoURL","facebookProfileURL","facebookReach","facebookReferredEnrollments","facebookReferredVisits","fax","firstName","gender","GeocodeAccuracy","holll","id","industry","inferredCity","inferredCompany","inferredCountry","inferredMetropolitanArea","inferredPhoneAreaCode","inferredPostalCode","inferredStateRegion","interested","interestedIn","isAnonymous","IsEmailBounced","isLead","iSTRUE","Jigsaw","JigsawCompanyId_account","JigsawContactId_lead","Jigsaw_account","Languages_c","lastName","LastReferencedDate","LastReferencedDate_account","lastReferredEnrollment","lastReferredVisit","LastViewedDate","LastViewedDate_account","Latitude","leadPartitionId","leadPerson","leadRevenueCycleModelId","leadRevenueStageId","leadRole","leadScore","leadSource","leadStatus","linkedInDisplayName","linkedInId","linkedInPhotoURL","linkedInProfileURL","linkedInReach","linkedInReferredEnrollments","linkedInReferredVisits","links","Longitude","MailingAddress","MailingGeocodeAccuracy","MailingLatitude","MailingLongitude","mainPhone","marketingSuspended","marketingSuspendedCause","middleName","mktoAcquisitionDate","mktocomment1","mktocomments2","mktoCompanyNotes","mktoDoNotCallCause","mktoIsCustomer","mktoIsPartner","mktoName","mktoPersonNotes","mktosync","mktotest1","mobile","mobilePhone","NaicsCode","NaicsDesc","newcustom","numberOfEmployees","originalReferrer","originalSearchEngine","originalSearchPhrase","originalSourceInfo","originalSourceType","OtherAddress","OtherGeocodeAccuracy","OtherLatitude","OtherLongitude","personPrimaryLeadInterest","personTimeZone","personType","phone","PhotoUrl","PhotoUrl_account","postalCode","priority","ProductInterest_c","rating","referal","registrationSourceInfo","registrationSourceType","relativeScore","relativeUrgency","requiredNumberofCylinder","salutation","sfdcAccountId","sfdcContactId","sfdcId","sfdcLeadId","sfdcLeadOwnerId","sfdcType","ShippingAddress","ShippingGeocodeAccuracy","ShippingLatitude","ShippingLongitude","sicCode","SicDesc","site","state","surveyAnswers","syndicationId","testBooleanField","testscore","title","totalReferredEnrollments","totalReferredVisits","Tradestyle","twitterDisplayName","twitterId","twitterPhotoURL","twitterProfileURL","twitterReach","twitterReferredEnrollments","twitterReferredVisits","uNSUBSCIBE","unsubscribed","unsubscribedReason","updatedAt","urgency","url","website","YearStarted"]}
```

応答は次のようになります。

```json
{
  "requestId": "6902#16fb52118bf",
  "result": [
      {
          "exportId": "4f2b9115-c3f2-4e40-a87c-bf803bbfed99",
          "format": "CSV",
          "status": "Created",
          "createdAt": "2020-01-17T20:10:43Z"
      }
  ],
  "success": true
}
```

### ジョブをエンキュー

ジョブは作成されましたが、何もしないでそこに座っています。 ジョブを実行するには、[exportId](https://developer.adobe.com/marketo-apis/api/mapi/#operation/enqueueExportLeadsUsingPOST) 値を使用して **enqueue エンドポイント** を呼び出し、リクエストの URI を作成する必要があります。 次のようになります。

`POST /bulk/v1/leads/export/4f2b9115-c3f2-4e40-a87c-bf803bbfed99/enqueue.json`

この POST には本文がありません。ここでは POST HTTP 動詞を使用します。 このリクエストは、次のような応答を生成します。

```json
{
  "requestId": "1836a#16fb5238a48",
  "result": [
      {
          "exportId": "4f2b9115-c3f2-4e40-a87c-bf803bbfed99",
          "format": "CSV",
          "status": "Queued",
          "createdAt": "2020-01-17T20:10:43Z",
          "queuedAt": "2020-01-17T20:13:23Z"
      }
  ],
  "success": true
}
```

先ほど述べたように、一度に実行できるジョブの数には制限があります。 また、一度にキューに入れられるジョブの数には制限もあります（10）。 限界があることで、すべてのジョブを一度に作成できなくなるように、40 以上のジョブが必要です。 他の統合もジョブを実行できるので、すべてのスロットがいっぱいになる可能性を考慮する必要があります。 キュー内のジョブが既に 10 個ある場合に新しいジョブをキューに入れようとすると、[1029](/help/rest-api/error-codes.md) エラーが発生します。 **1029** を受け取ったら、ジョブがキューに入れられるまで、指数バックオフを使用します。 1 分待ってから、リクエスト間に最大 4 分間、**1029** エラーコードを取得するたびに、その値を 2 倍にしますが、それ以上の時間は設定しません。 この手法は、[ 切り捨てられたバイナリ指数バックオフ ](https://devopedia.org/binary-exponential-backoff) と呼ばれ、回復可能なエラーとステータスチェックのベストプラクティスです。

### ジョブが完了するのを待ちます

各ジョブの実行には時間がかかるので、[ ステータスエンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsStatusUsingGET) を呼び出して進行状況を監視します。 ここでも、次のように、リクエスト URI に **exportId** を含めます。

`GET /bulk/v1/leads/export/4f2b9115-c3f2-4e40-a87c-bf803bbfed99/status.json`

ジョブが完了する前に、次のような応答が返されます。

```json
{
    "requestId": "153cb#16fb525435d",
    "result": [
        {
            "exportId": "4f2b9115-c3f2-4e40-a87c-bf803bbfed99",
            "format": "CSV",
            "status": "Processing",
            "createdAt": "2020-01-17T20:10:43Z",
            "queuedAt": "2020-01-17T20:13:23Z",
            "startedAt": "2020-01-17T20:13:49Z"
        }
    ],
    "success": true
}
```

ジョブのステータスが「待機中」の間に、同じ指数バックオフ（1 分から 4 分まで）を実行します。 ステータスはリアルタイムではありません。1 分ごとに更新されるので、より高速にポーリングするメリットはほとんどありません。 ジョブのステータスが「処理中」に変わると、バックオフがリセットされます。 ステータス「完了」が次のようになるのを待っています：

```json
{
  "requestId": "10ad9#16fb5268f9b",
  "result": [
      {
          "exportId": "4f2b9115-c3f2-4e40-a87c-bf803bbfed99",
          "format": "CSV",
          "status": "Completed",
          "createdAt": "2020-01-17T20:10:43Z",
          "queuedAt": "2020-01-17T20:13:23Z",
          "startedAt": "2020-01-17T20:13:49Z",
          "finishedAt": "2020-01-17T20:15:28Z",
          "numberOfRecords": 59,
          "fileSize": 74436,
          "fileChecksum": "sha256:de553362e7ffad6556ae9ea749655c35010c7f0e944fc5a85782183130dca18d"
      }
  ],
  "success": true
}
```

**numberOfRecords** 値は、リクエストがリードを返さない場合は 0 になります。 この値をチェックして、意味がある場合は次の手順をスキップします。 リードが返されたら、**fileChecksum** 値を抽出します。 この機能を使用して、ダウンロード時のファイルの整合性を確認します。

### リードを取得

**numberOfRecords** が 0 より大きい場合は、次のようなリクエストを行って、[ 書き出しリードファイルを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsFileUsingGET) を使用して書き出したファイルをダウンロードします。

`GET /bulk/v1/leads/export/4f2b9115-c3f2-4e40-a87c-bf803bbfed99/file.json`

エラーなしで転送されたファイルを確認してください。ファイルのチェックサムを計算し、以前に保存した **fileChecksum** と比較します。 [SHA-2](https://en.wikipedia.org/wiki/SHA-2) （特に SHA256 ハッシュ関数）を使用してチェックサムを計算します。 計算されたチェックサムが一致しない場合、ファイル転送でエラーが発生しました。転送を再試行するか、中止して手動でリカバリできます。

### データを集計

最初のリードから今日まで 31 日間の範囲ごとにサイクリングした後、完全なセットが得られます。 また、範囲ごとに 1 つのファイルを作成します。 すべてのリードで単一の集計ファイルを作成する最も簡単な方法は、最初のファイルを除くすべてのヘッダー行を削除した後でこれらのファイルを連結することです。 その場合は、後でデータ処理パイプラインで重複の可能性を期待し、計画することを忘れないでください。 デモでは、ダウンロードしたファイルを処理します。 データの各行を出力ファイルに追加する前に、行のリード ID が既に書き込まれているかどうかを確認して重複排除を行います。

[ こちら ](https://github.com/Marketo/REST-Sample-Code/tree/master/python/LeadDatabase/Leads) でホストされるデモコードを開発しました。このプロセスの詳細を入力して、独自の開発のテンプレートとして使用できることを願っています。 デモコードは学習ツールとなることを目的としているので、実稼動システムで必要になる堅牢性の向上を図ることができます。 **このコードは MIT ライセンスの下で AS-IS** で提供されていますが、人間の監督による 1 回限りの使用には十分でしょう。 今は何もあなたを止めることはありません！ このプロセスに従うと、Marketoの一括抽出 API を使用してすべてのリードを抽出し、場合によってはターゲットのMarketo Engage インスタンスのすべてのフィールドを抽出します。 データをさらに拡張するには、手法を使用して各リードのアクティビティを取得します。

Posted on _2020-03-05_ by _Tony_

## 2020 年 2 月の更新

2020 年 2 月に、新しい REST API をリリースします。 以下のアップデートの完全なリストをご覧ください。

### お知らせ

* 2020 年 9 月以降、[Asset API](/help/rest-api/assets.md) エンドポイントは **_method** クエリパラメーターを受け付けなくなります。 これは、URI の長さの制限を回避するために、POST 本文にクエリパラメーターを渡すために使用されました。 このパラメーターを必要とするリクエストに対応するために、Asset API の URI 制限が 6KiB から 65KiB に増加されます。
* ITP での立場に関しては、thisMarketo Community の投稿を参照してください。[ ブラウザー Cookie の更新：Marketo/Munchkinへの影響 ](https://nation.marketo.com:443/t5/knowledgebase/browser-cookie-updates-how-marketo-munchkin-is-affected/ta-p/251524)
* 「進行状況のステータスを変更」アクティビティが変更されました。 次回の機能「プログラムメンバーカスタムフィールド」をサポートするために、「プログラムメンバー ID」属性がに追加されました。

Posted on _2020-02-26_ by _David_

## Munchkin Associate Lead Method の廃止

Munchkin JavaScript Client バージョン 159 の次回リリースでは、Munchkin[Associate Lead Method](/help/javascript-api/api-reference.md) の廃止を開始します。 このバージョン以降、メソッドが呼び出されると、ブラウザーコンソールで、メソッドが今後のリリースで削除されることを示す警告が表示されます。 メソッドを削除した後にメソッドを使用しようとすると、失敗します。 この方法を最近使用したと当社が特定したMarketoのお客様には、個別に使用に関する通知が送信されます。 Munchkin 159 リリースについて詳しくは、[ このマーケティングネーションに関する投稿を参照 ](https://nation.marketo.com:443/t5/product-documents/munchkin-javascript-version-159-amp-associate-lead-deprecation/ta-p/299687) してください。

### よくある質問（FAQ）

影響を受けているかどうかを知る方法

Adobeは、サブスクリプションでこのメソッドの使用を確認した場合にお客様に通知し、廃止期間を通じて複数回通知します。

メソッドはいつ削除されますか？

この手法は、2021 年 10 月のMarketo リリースと共に一般公開される予定のMunchkin JS v161 で削除されます。

このメソッドが削除される理由

この方法の導入以降、同じユースケースをよりパフォーマンスの高い方法で実現する方法が実装およびリリースされました。 サービスのパフォーマンスと健全性を向上させるために、許容基準に適合しない機能を削除する必要が生じる場合があります。

このメソッドの代わりに何を使用するとよいですか？

Munchkin Associate Lead には、ユーザーデータの送信と、ブラウザーの web トラッキング cookie をMarketoの対応するユーザーレコードに関連付ける 2 つの主なユースケースがあります。 Munchkin Associate Lead が導入されて以来、より堅牢なデータ送信および cookie の関連付け方法が実装されてきました。

#### サーバーサイド送信

ブラウザーサイドの送信が必要ない場合、REST API には、[ 人物データ送信 ](/help/rest-api/leads.md) のための多くの方法と、[Cookie を人物レコードに関連付けるための目的別の方法 ](/help/rest-api/leads.md) が用意されています。

Munchkinのバージョン 159 はいつ公開されますか。

バージョン 159 は、2020 年 10 月のMarketo リリースから一般公開されています。

Posted on _2020-05-06_ by _Kenny_

## Marketo フォームの送信をバックグラウンドで行う

組織が web コンテンツや顧客データをホストするための様々なプラットフォームを持つ場合、結果のデータを別々のプラットフォームに収集できるように、フォームから並列で送信する必要があるケースはかなり一般的になります。 これを行うには様々な方法がありますが、多くの場合、最も簡単な方法が最善です。Forms 2 API を使用して、非表示のMarketo フォームを送信します。 これは新しいMarketo フォームで機能しますが、フィールドのない空のフォームを作成することをお勧めします。 これにより、何もレンダリングする必要がなくなるので、フォームが必要以上にデータを読み込むことがなくなります。 次に、フォームから [ 埋め込みコード ](https://experienceleague.adobe.com/ja/docs/marketo/using/home) を取得し、目的のページの本文に追加して、小さな変更を加えます。 埋め込みコードには、次のようなフォーム要素が含まれています。

`<form id="mktoForm_1068"></form>`

次のように、要素が表示されないように、「style=&quot;display:none&quot;」を要素に追加します。

`<form id="mktoForm_1068" style="display:none"></form>`

フォームが埋め込まれ、非表示になると、フォームを送信するコードは非常にシンプルになります。

```javascript
var myForm = MktoForms2.allForms()[0];
myForm.addHiddenFields({
 //These are the values which will be submitted to Marketo
 "Email":"<test@example.com>",
 "FirstName":"John",
 "LastName":"Doe"
 });
myForm.submit();
```

この方法で送信されたFormsは、リードが表示可能なフォームに入力して送信した場合とまったく同じように動作します。 送信のトリガーは、実装ごとに異なるアクションがプロンプトを表示するので、実装間で異なりますが、基本的にどのアクションでも実行させることができます。 重要な部分は、フィールドと値を正しく設定することです。 フィールド名の書き出しで見つけることができるフィールドのSOAP API 名を使用して、値が正しく送信されていることを確認してください。

### Munchkin Associate Lead からの移行

バックグラウンドでのフォームの送信は、Munchkinのアソシエイトリードにとって推奨される代替手段の 1 つです。 以下のHTMLのサンプルページでは、リードを関連付けるために送信されたのと同じ値を再利用することで、高レベルでの移行を示しています。

```html
<html>
<head>
    <!--
      Munchkin Code
      Replace with your own instance code
    -->
    <script type="text/javascript">
        (function() {
          var didInit = false;
          function initMunchkin() {
            if(didInit === false) {
              didInit = true;
              Munchkin.init('CHANGE ME');
            }
          }
          var s = document.createElement('script');
          s.type = 'text/javascript';
          s.async = true;
          s.src = '//munchkin.marketo.net/munchkin-beta.js';
          s.onreadystatechange = function() {
            if (this.readyState == 'complete' || this.readyState == 'loaded') {
              initMunchkin();
            }
          };
          s.onload = initMunchkin;
          document.getElementsByTagName['head'](0).appendChild(s);
        })();
        </script>
</head>

<body>
  <!--
    Start Embed code.
    Pasted from Form Actions -> Embed Code except for addition of 'style="display:none"' to the form tag in order to hide it, and instance-specific codes redacted
    Replace with your own code for testing
  -->
  <script src="CHANGE ME"></script>
  <form id="CHANGE ME" style="display:none"></form>
  <script>MktoForms2.loadForm("CHANGE ME", "CHANGE ME", "CHANGE ME TO AN INTEGER ID");</script>
  <!--End Embed Code-->

  <!--Demo code-->
    <script>
        //The same map which is assembled for the Munchkin submission can be reused for the form submission
        let values = {
            "Email": "email@example.com",
            "FirstName": "Test",
            "LastName": "Record"
        }
        //whenReady lets us apply a callback to all mkto forms on the page
        //the callback function fires whenever a form is completely loaded
        //for most use cases this will just be used to capture a reference to the form for later usage
        //submission is done in line here for demonstration only
        MktoForms2.whenReady(function(form){

            //the addHiddenFields methods lets us add arbitrary fields to the form as well as their values
            form.addHiddenFields(values);

            //pass the same set of values to associateLead
            //hashString: secret + email
            Munchkin.munchkinFunction('associateLead', values, "CHANGE ME");

            //submit the form
            form.submit();


        })
    </script>
</body>

</html>
```

Posted on _2020-05-26_ by _Kenny_

## 2020 年 7 月の更新

2020 年 7 月に、新しい REST API をリリースし、既存の API を強化して、欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

* まだ招待を受け入れていない（「保留中」のユーザーなど）ユーザーをクエリおよび削除できる 2 つのエンドポイントを追加しました。 [ 招待ユーザーを ID で取得 ](/help/rest-api/user-management.md) エンドポイントを使用すると、保留中のユーザーをクエリできます。 [ 招待ユーザーの削除 ](/help/rest-api/user-management.md) エンドポイントを使用すると、保留中のユーザーを削除できます。
* [ ユーザーを招待 ](/help/rest-api/user-management.md) エンドポイントが更新されて、**expiresAt** パラメーターの ISO 8601 準拠の日時文字列を受け入れるようになりました。
* [ID によるユーザーの取得 ](/help/rest-api/user-management.md) と [ ユーザー属性の更新 ](/help/rest-api/user-management.md) の両方のエンドポイントが更新され、**lastLoginAt** 属性の最後のユーザーログイン時間を返すようになりました。
* 既に存在する静的リストを作成しようとすると [ 静的リストを作成 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/createStaticListUsingPOST) エンドポイントが「611、システムエラー」というエラーを返す問題を修正しました。 「709、同じ名前の静的リストが既に存在します」というエラーを返すように変更しました。 [LM-135934]
* 既に存在するメールを作成しようとすると [ メールを作成 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/createEmailUsingPOST) エンドポイントが「611、システムエラー」というエラーを返す問題を修正しました。 次のエラーを返すように変更されました。「709、同じ名前のメールが既に存在します」 [LM-138648]
* ランディングページのクエリエンドポイントで誤った **createdAt** 値が返される問題を修正しました。 ランディングページが最後に承認された時刻をエンドポイントが返していました。 これで、ランディングページが作成された時間に戻ります。 [LM-138648]
* [ リードを結合 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/mergeLeadsUsingPOST) エンドポイントが、無効な結合操作に対してエラー「611, システムエラー」を返す問題を修正しました。 結合の結果リードが重複し、**mergeinCRM** が true に設定されていた場合に発生しました。 エラー「712。重複レコードを作成しています。 代わりに、既存のレコードを使用することをお勧めします」。 [LM-137463]

Posted on _2020-08-01_ by _David_

## ゲストの投稿 – 詳細：カスタムオブジェクトとカスタムアクティビティとカスタムフィールド

**これは、MarTech IT Specialist のMarketo Champion 2020 の Amit Jain によるゲスト投稿です** エンタープライズレベルのマーケティング自動化プラットフォームであるMarketoは、複数のソースから取得したユーザー/顧客/見込み客情報を管理し、パーソナライゼーション、セグメント化、レポートの改善のためにMarketoで維持管理します。 これらのソースは、web サイトフォームからリストビルド、CRM データ、e コマースデータまで様々です。 Marketoは、リード、会社、オポチュニティ、アクティビティなどの標準オブジェクトを提供します。 これらの標準オブジェクトは、Marketoで使用できる拡張データセットという新たなマーケティングニーズを満たすには不十分な場合があります。

例えば、買い物かごに追加された項目、異なるコースに申し込んだ学生、特定のユーザーが所有する製品、異なるサブスクリプションへの同意などです。 この情報は、よりパーソナライズされたコンテンツと統一されたユーザーエクスペリエンスをプラットフォーム全体で提供することで、マーケターが顧客や見込み客のエンゲージメントを維持するために重要になる可能性があります。 これらのビジネスニーズに対応するために、Marketoでは、このタイプのデータをカスタムフィールド、カスタムアクティビティ、カスタムオブジェクトに保存するカスタムの方法を提供します。 どのオプションをいつ使えばいいのか分からない人が多いのを見てきました。 このブログ記事では **この 3 つのことが実際に何であるのか、またいつ使うべきか、いくつかの例を交えて詳しく説明します** と述べています。

**カスタムフィールド**

Marketoの「リード」オブジェクトはマスターオブジェクトで、他のすべてがこのオブジェクトに直接または間接的に接続されています。 Marketoでは、「リード」オブジェクト、「会社」オブジェクトにカスタムフィールドを作成でき、最近、「プログラムメンバー」カスタムフィールドのサポートを発表しました。 これらのカスタムフィールドは、特定のタイプのデータを保存する必要性を満たします。 例えば、ジョブ関数やユーザーの別の同意の保存が必要になる場合があります。 Marketoには次の 2 種類のカスタムフィールドがあります。

1. **CRM フィールドから同期：** Marketoは、自動Marketo ↔︎ SFDC同期の一環として、リード、連絡先、アカウント、商談オブジェクトのSFDCでMarketo ユーザーに表示されるすべてのカスタムフィールドを同期します。
1. **Marketoのみのフィールド：** Marketoでフィールドを直接作成できます。 これらのフィールドのデータは、SFDCとは同期されません。

**クイックヒント**

* Marketoのみのフィールドがあり、SFDCでデータを同期しますか？ その方法については、[ このブログ ](https://themarketingautomationblog.com/2019/12/06/field-management-merging-remapping-hiding-marketo-fields/) を参照してください。
* カスタムフィールドについて詳しくは [ こちら ](https://themarketingautomationblog.com/2019/11/15/knowing-your-marketo-fields/) を参照してください。
* 現時点では、Marketo API はカスタムフィールドの更新/作成をサポートしていません。

**カスタムオブジェクト**

Marketoでは、標準のオブジェクトとは別に、独自のカスタムオブジェクトを作成できます。 _カスタムオブジェクトを作成して、会社またはリードオブジェクト、または別のカスタムオブジェクトに関連付けることができます。_ カスタムオブジェクトは、標準のリードおよび会社レコードを補完するカスタムレコードのセットです。 カスタムオブジェクトを使用すると、追加のデータをスケーラブルに保存し、そのデータをリードまたは会社のレコードにリンクできます。 標準（リンクフィールド）とカスタムフィールドを任意に組み合わせてカスタムオブジェクトを作成し、それらのフィールドに値を入力してカスタムオブジェクト _レコード_ を作成してから、それらのレコードをリードまたは会社のレコードにリンクできます。 リードフィールドや会社フィールドにない情報を含むアセットを作成できるので、リンクされた強力で柔軟なレコードを使用して、セグメント、スマートリスト、キャンペーンを強化できます。 カスタムオブジェクトには、次のいずれかのタイプの関係を持つことができます。

* **1 対 1 の関係**：各カスタムオブジェクトには、1 つのリード/会社オブジェクトのレコードがあります。
* **1 対多の関係**：各カスタムオブジェクトには、リード/会社に関連する複数のカスタムオブジェクトレコードが含まれます。
* **多対多の関係：** 複数のカスタムオブジェクトレコードが複数のリード/会社オブジェクトにリンクされる場合。 例えば、コースカタログに記載されている複数のコースに、複数の受講者が登録されているとします。

**クイックヒント**

* カスタムオブジェクトのセットアップについて詳しくは [ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/home) を参照してください。
* Marketo カスタムオブジェクトは、中間オブジェクトとして使用できるほか、カスタムオブジェクトのカスタムオブジェクトも意味します。

### カスタムオブジェクトを使用する理由

カスタムオブジェクトを使用すると、会社やリードに関連する一意のデータをコンパイルして使用できますが、会社やリードに関する静的な情報でなくてもかまいません。 リードフィールドは個人のリード情報（_メールアドレス_、_郵便番号_ など）、事業情報（_役職_、_業界_ など）、またはシステム駆動情報（_Marketo ID_、SFDC ID、作成日など）に関連していますが、カスタムオブジェクトフィールドは完全にカスタマイズ可能です。 例えば、次のような情報を格納するには、カスタムオブジェクトを使用します。

* ユーザーの購入履歴。
* 買い物かご情報。
* 顧客が期間限定のプロモーション割引コードを使用したかどうか。
* アンケート結果、インタビュー、イベント出席から取得した補足情報。
* ユーザーの体験版情報（体験版インスタンス URL、開始日、終了日、ユーザーの数など）。

### Marketo カスタムオブジェクトの制限

1. デフォルトでは、Marketoで 10 個のカスタムオブジェクトを作成できます。 サブスクリプション料金を追加すると、上限を増やすことができます。
1. オブジェクトあたりのデフォルトのフィールド数は 50 ですが、必要に応じて、追加のフィールドに対するMarketo サポートをリクエストできます。 [Michael Florin](https://www.linkedin.com/in/michaelflorin/) の皆さま、ご協力に感謝いたします。
1. すべてのカスタムオブジェクトで使用できるレコードの数には制限があります。 Marketoのサブスクリプションによって異なります。 この制限は、追加のサブスクリプション料金で増やすことができます。
1. API を使用してカスタムオブジェクトが作成された場合、Marketoでは、Marketo UI から CO スキーマを編集できません。

**クイックヒント**

* Marketo API では、カスタムオブジェクトに対する CRUD （作成、読み取り、更新、削除）操作をサポートしています。
* このカスタムオブジェクトデータは、Velocity スクリプトを使用したメールのパーソナライゼーションに使用できます。
* カスタムオブジェクトに関連するすべてのエンドポイントを確認できます [ こちら ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportProgramMembersStatusUsingGET)。

### カスタムオブジェクトの用語

**カスタムオブジェクト**：すべてのカスタムオブジェクトレコードのグループを保持するコンテナ。 正式には、データカードセットまたはカスタムテーブルと呼ばれます。 **カスタムオブジェクトレコード**：リードまたは会社に関連付けることができる追加のフィールド情報を含むデータレコード。 レコードは、標準のリードまたは会社フィールド、およびカスタムオブジェクトレコードフィールドで構成できます。 正式には、データ カードまたはデータ テーブル行と呼ばれます。 **カスタムオブジェクトレコードフィールド**：完全にカスタマイズ可能なフィールドで、一意の情報や一時的な情報を収集します。 これらのフィールドは作成され、カスタムオブジェクト自体の中に格納されます。 正式には、データカードフィールドまたはデータベーステーブルのフィールド/列と呼ばれます。 **リンクフィールド**：カスタムオブジェクトレコードとリンクされたリード/会社オブジェクトレコードの間の関係を定義する、カスタムオブジェクトレコードフィールドの特別なタイプ。 カスタムオブジェクトを作成する場合は、カスタムオブジェクトレコードを正しい親レコードに接続するためのリンクフィールドを指定する必要があります。

* 1 対多または 1 対 1 のカスタム構造の場合は、カスタムオブジェクトのリンクフィールドを使用して、個人または会社に接続します。
* 多対多構造の場合は、2 つのリンクフィールドを使用し、別に作成した中間オブジェクト（カスタムオブジェクトの一種でもある）から接続します。1 つのリンクはデータベース内の人や会社に接続し、もう 1 つのリンクはカスタムオブジェクトに接続します。この場合、リンクフィールドはカスタムオブジェクト自体に配置されません。

### カスタムアクティビティ

**誰かが組織とやり取りする方法はいくつかあります。 貴社のウェブサイトを訪問したり、展示会に参加したり、貴社から送信されたメールのリンクをクリックしたりする場合があります。 これらのアクションはアクティビティで** どのようなアクションを実行してもMarketoがそのアクションを取り込むため、マーケティングチームやセールスチームは、パーソナライズされた統一されたエンゲージメントに対するユーザーの行動をより深く理解できます。 **_カスタムアクティビティ_**&#x200B;_Marketo フォーム、メール、ランディングページに関連しないアクティビティを追跡するのに役立ちます_。 例えば、誰かが web サイトでビデオを閲覧した日時や調査を行った日時を追跡したい場合、カスタムアクティビティを使用します。 カスタムアクティビティは、カスタムオブジェクトとは異なります。値が変化する（例えば、「車の色」が青から赤に変化する）場合は、カスタムオブジェクトを使用します。発生したモーメントを追跡し、その詳細を変更できない場合（例：「購入車」）は、カスタムアクティビティを使用します。 デフォルトでは、定義できるカスタムアクティビティの最大数は 10 です。 これは、追加のサブスクリプション料金で増やすことができます。 [Marketo データ保持ポリシー ](https://nation.marketo.com/t5/knowledgebase/tkb-p/support_solutions-documents) に従い、カスタムアクティビティは 25 か月後に自動的に削除されます。

**カスタムアクティビティ：** Marketo内でトラッキングするMarketo以外のイベント。 **カスタムアクティビティ ID:** Marketoは、Marketo API を使用してアクティビティデータのプッシュ/プルを試みる際に使用できる数値 ID をカスタムアクティビティに割り当てます。 **カスタムアクティビティフィールド：** アクティビティメタデータは、アクティビティフィールドに保存できます。 例えば、ビデオのビューをトラッキングする場合、これらのフィールドはページ URL、ビデオタイトルなどです。 **カスタムアクティビティプライマリフィールド：** スマートリストファイラー条件として使用できるカスタムアクティビティフィールド。

**クイックヒント**

* カスタムアクティビティの API エンドポイントは [ こちら ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addCustomActivityUsingPOST) から入手できます。

## カスタムオブジェクトとカスタムアクティビティの比較

**カスタムオブジェクト**

**カスタムアクティビティ**

1

デフォルトでは、インスタンスあたり最大 10 個のカスタムオブジェクト。

デフォルトでは最大 10 個のカスタムアクティビティ。

2

カスタムオブジェクト 1 つにつき最大 50 個のカスタムオブジェクトフィールド。

各カスタムアクティビティタイプには、最大 20 個のセカンダリ属性を設定できます。

3

最大 1 MM のカスタムオブジェクトレコード。サブスクリプションに大きく依存する場合があります。

25 か月後、カスタムアクティビティは、Marketo データ保持ポリシーに従って削除されます。

4

スマートリストおよびスマートキャンペーンのフィルターおよびトリガーとして使用できます。

スマートリストおよびスマートキャンペーンのフィルターおよびトリガーとして使用できます。

5

メールコンテンツのパーソナライズに使用できます。

メールコンテンツのパーソナライズには使用できません。

6

カスタムオブジェクトレコードに対して CRUD 操作を実行できます。

カスタムアクティビティでは、作成と読み取りのみ許可されています。

7

値が変化する（「車の色」が青から赤に変わる）可能性がある場合は、カスタムオブジェクトを使用します。

発生するタイミングをトラックする際に詳細が変わらない場合（例えば、「購入した車」）は、カスタムアクティビティを使用します。

8

カスタムオブジェクトは、その事実を示します。 （現在価値）。

カスタムアクティビティは、過去に発生したイベントを表示します。

Posted on _2020-10-18_ by _Amit_

## 2021 年 1 月更新

2021 年 1 月に、新しい REST API をリリースし、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

* プログラムによるフォーム送信を実行できる [ フォームを送信 ](/help/rest-api/leads.md) エンドポイントを追加しました。 サードパーティのフォームをMarketo フォームと統合して、既存のマーケティングワークフローを活用できるようになりました。
* ランディングページのシリアル化されたHTML バージョンを返す [ ランディングページの完全なコンテンツを取得 ](/help/rest-api/landing-pages.md) エンドポイントを追加しました。 Marketo Engageにログインしなくても、ランディングページの完全にパーソナライズされたプレビューをレンダリングできます。 これにより、統合アプリケーション内で編集および翻訳ワークフローを効率化できます。
* Velocity スクリプト経由でアクセスできるカスタムオブジェクトの数を設定できるようになりました。 設定手順については、[ こちら ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/email-setup/change-custom-object-retrieval-limits-in-velocity-scripting) を参照してください。

### 欠陥の解決

* [ ユーザーを削除 ](/help/rest-api/user-management.md) エンドポイントを使用すると、カスタムサービスで使用されていた API 専用ユーザーを削除できる問題を修正しました。 次に、「611, You cannot delete an API user that is used in API service」エラーを返します。 [LM-141893]
* [ ユーザーを取得 ](/help/rest-api/user-management.md) エンドポイントが、場合によっては削除されたユーザーを返す問題を修正しました。 [LM-141542]
* [ プログラムを複製 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) エンドポイントの問題を修正しました。 255 文字を超えるプログラム名を指定した場合は、「611, Unable to clone program error」が返されます。 次に、「701、名前の長さが 255 文字を超えることはできません」が返されます。 [LM-143436]
* [ ランディングページのドラフトを承認 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveLandingPageUsingPOST) エンドポイントの問題を修正しました。 モバイルバージョンをアクティベートしたランディングページを承認すると、場合によっては、デスクトップバージョンでモバイルバージョンのコンテンツが表示されることがありました。 [LM-146867]
* [ ランディングページを未承認 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/unapproveLandingPageByIdUsingPOST) エンドポイントで、1 つ以上のフォームによってフォローアップページとして使用されていたランディングページの承認を取り消すことができた問題を修正しました。 「709, ランディングページの承認の取り消しに失敗しました」エラーを返すようになりました。 ランディングページが、1 つ以上のフォームによって、フォーム ID （[_formId1,formId2,..._]&quot;）のフォローアップページとして使用されています。 [LM-143326]

Posted on _2021-01-15_ by _David_

## Munchkin 160 Betaおよびビーコン API

**2021 年 1 月 27 日（PT）:** リードの関連付けの非推奨（廃止予定）の影響を受けるMarketo ユーザーの一部には、1 つ以上のインスタンスでMunchkin Beta設定が有効になっていることを示すメール通知がエラーで届きました。 このリリースは、正しいオーディエンスに通知できるようになるまで開催されます。 Munchkin JavaScriptのバージョン 160 以降、MunchkinがMarketo バックエンドと通信するデフォルトの方法は [Beacon API](https://developer.mozilla.org/ja/docs/Web/API/Beacon_API) になります。 これは、2020 年夏に、**useBeaconAPI** 設定パラメーターを介したバージョン 159 のリリースでオプションとして利用できるようになりました。 ビーコン API には、古い XMLHttpRequest メソッドを使用する場合よりもいくつかの利点がありますが、主な改善点は、HTTP 通信用の非ブロッキング非同期 API であり、最新のすべてのインターネットブラウザーで使用できるということです。 Munchkinのほとんどのユーザーは、web サイトの動作の変化に気付くことはありませんが、この更新は、バックエンドにクリックイベントを送信するのを待っている間、Munchkinがナビゲーションをブロックするのを防ぎます。つまり、より簡単に言えば、Munchkinが新しいページへのリンクをクリックした後にブラウザーが「ハング」する可能性をほとんどなくなります。 これは、Marketoの一部のお客様にとって、まれではあるものの不満が生じる出来事でした。

2021 年 1 月 27 日（PT）現在、このバージョンのロールアウトは保留中で、再スケジュール保留中です。 この変更点に関連する問題は予想されておらず、テスト中に問題が特定されることはありませんが、MarketoでMunchkinのデプロイメント設定をすべてテストすることは不可能です。これらの変更点を事前にテストすることも、このバージョンが一般提供されるまでこの変更点のテストを控えることもできます。 様々なシナリオの手順を以下に示します。

### テストビーコン API

今後のバージョンを見越して更新されたビーコン API をテストする場合は、外部テストページでMunchkin設定に **useBeaconAPI** パラメーターを追加することで、その操作を実行できます。 このテストは、Munchkinの一般提供バージョンまたはベータ版で動作します。 設定パラメーターは、7 行目の `Munchkin.init()` メソッドの呼び出しの 2 番目の引数に次のように表示されます。`{ 'useBeaconAPI': true}`

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      Munchkin.init('299-BYM-827', {"useBeaconAPI":true});
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin.js';
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName['head'](0).appendChild(s);
})();
</script>
```

### Marketo ランディングページでMunchkin Betaを無効にする

MarketoのランディングページでMunchkin Betaを無効にするには、サブスクリプションの「管理者」セクションの [ 宝箱 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features) メニューにアクセスし、ランディングページのMunchkin Beta設定を無効に変更する必要があります。

### 外部ページでのMunchkin Betaの無効化

Beta バージョンのMunchkin JavaScriptを外部の web ページにデプロイした場合、それが一般に提供されるまでこの変更を適用しないようにするには、Munchkin JS スニペットを変更して、**munchkin をターゲットにする必要があります。**&#x200B;munchkin-beta の代わりに&#x200B;**&#x200B;**&#x200B;js **&#x200B; ファイルを使用します。**&#x200B;**js** ファイル。 次の例では、これは 11 行目の **s.src** 変数の値です。 スニペットが例によく似ていなかったり、タグマネージャーによって外部ページにデプロイされたりする場合は、IT リソースや、Munchkin トラッキングを有効にして web サイトを管理するユーザーに連絡する必要がある可能性があります。

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      Munchkin.init('299-BYM-827');
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin.js';//This line should have the munchkin.js file, not munchkin-beta.js
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName['head'](0).appendChild(s);
})();
</script>
```

Posted on _2021-01-08_ by _Kenny_

## 電子メール V1 の最終的な非推奨（廃止予定）

[Email V1 の廃止はほぼ 2 年前に始まりました ](https://nation.marketo.com:443/t5/knowledgebase/email-editor-1-0-is-being-deprecated-june-18th/ta-p/250666)2021 年 3 月 17 日のロンドンとオランダのサブスクリプションおよび 2021 年 3 月 19 日の他のすべてのサブスクリプションへの 3 月のメンテナンスリリースを皮切りに、V1 メールのすべての API サポートが終了します。 このリリース以降、Asset API を使用して V1 メールでやり取りしようとすると、エラーが発生し、アクションは実行されません。 2021 年 2 月 24 日（PT）以降の既知の残りのすべてのユーザーに通知されましたが、これらのアセットとのやり取りを試みる統合がまだ存在する可能性があります。 影響を受ける統合の最も一般的なタイプは、デジタルアセット管理、翻訳、ローカライゼーションを提供するサービスです。 この変更の結果、統合エラーが発生した場合でも、[ 問題のあるアセットを編集して承認すれば、そのアセットをアップグレードできます ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/transitioning-to-email-editor-2-0)。 メールアセットを V2 にアップグレードすると、統合サービスで再開して使用できるようになります。

Posted on _2021-03-17_ by _Kenny_

## 2021 年 5 月更新

2021 年 5 月には、新しい REST API をリリースし、既存の REST API を強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

* プログラムメンバーシップレコードを取得、更新、削除できるプログラムメンバー API を追加しました。 詳しくは、[REST API/リードデータベース/プログラムメンバー ](/help/rest-api/program-members.md) を参照してください。
* 一括カスタムオブジェクト抽出 API が追加され、1 対多の関係のリードに関連付けられた第 1 レベルのMarketo カスタムオブジェクトレコードを書き出せるようになりました。 詳しくは、[REST API/一括抽出/カスタムオブジェクトの一括抽出 ](/help/rest-api/bulk-custom-object-extract.md) を参照してください。
* [Lead API](/help/rest-api/leads.md) と [Bulk Lead Extract API](/help/rest-api/bulk-lead-extract.md) の両方を強化して、Adobe Experience Cloud ID （ECID）を取得できるようになりました。 これにより、[Adobe Experience Cloudのオーディエンスを同期 ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-experience-cloud-audience-sharing.html?lang=ja) したユーザーは、関連する ECID を持つリードを識別できます。 これにより、他のAdobe Experience Cloud製品との [ 統合の可能性 ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024277392-Adobe-Experience-Cloud-Using-the-ECID-for-integration) が開きます。
* [ 一括リード読み込み API](/help/rest-api/bulk-lead-import.md) が強化され、読み込みプロセス中に会社レコードへのリードを追加できるようになりました。 これを行うには、読み込みファイルに **externalCompanyId** フィールドを含めます。
* Marketo Engage UI の機能と同等になるように、いくつかのプログラムエンドポイントを強化しました。 [ プログラムの作成 ](/help/rest-api/assets.md) エンドポイントと [ プログラムのクローン ](https://developer.adobe.com/marketo-apis/api/asset/) エンドポイントを強化し、イベントプログラムに対する作成、クローン、移動の操作を許可しました。 これは、イベントプログラムを他のプログラムタイプの下に「ネスト」して整理するユーザー向けです。 また、[ プログラムを削除 ](https://developer.adobe.com/marketo-apis/api/asset/) エンドポイントが強化され、ソーシャルAssetsが埋め込まれたプッシュ通知、アプリ内メッセージ、レポート、ランディングページなどのアセットを含むプログラムを削除できるようになりました。
* Marketo管理者は、特定のフィールドを [ 機密」としてマークすることで ](https://experienceleague.adobe.com/ja/docs/marketo/using/home) その値が [ フォームに事前入力されない ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/forms/form-fields/disable-pre-fill-for-a-form-field) ようにし、ユーザーの機密データを保護できます。 いくつかのフォームフィールドエンドポイントを拡張して、Marketo Engage UI にあるこの機能と同等の機能を提供しました。

### 欠陥の解決

* プログラムのエンドポイントを削除する際の問題を修正しました。 共有フォルダー内のプログラムを削除しようとすると、「611, System Error」が返されます。 次に、「」が返されます。ターゲットプログラムは共有フォルダーにあり、削除できません。 削除を試みる前に、フォルダーの共有を解除する必要があります。」
* クローンプログラムエンドポイントの問題を修正しました。 フローステップで日時を含むプログラムを複製しようとすると、「611, System Error」が返されます。 これで、プログラムのクローンが正常に作成されました。
* プログラムを作成エンドポイントで、誤ってメールプログラムの下にプログラムを作成できなかった問題を修正しました（この問題は許可されていません）。
* クローンプログラムエンドポイントの問題を修正しました。 ランディングページを含むプログラムのクローンを作成した場合、ターゲットプログラム内のランディングページの名前に、プログラム名とランディングページ名の間にアンダースコアが欠落していました。 例：`http://<_pod_\>.marketo.com/lp/<_munchkin_\>/<_program name_\>**_**<_LP name_\>.html`

Posted on _2021-05-07_ by _David_

## Adobe取引所への期間限定オファー

Marketo Engage パートナーコミュニティサポートは、お客様の成功の柱の 1 つです。 Marketo Engage統合エコシステムが Exchange Marketplace に適切に表されていることを確認し、LaunchPoint パートナー向けの特別オファーを用意したいと考えています。 延長されない非常に限られた期間に、LaunchPoint パートナーに 2022 年末までの Exchange プログラムで無料の Innovate パートナーシップを提供しています（約 15,000 ドル価値）。 このオファーは、LaunchPoint パートナーが Exchange パートナーポータルで統合リストを作成し、Adobe Exchange Marketplace で公開できるように促すことを目的として設計されました。 2022 年 12 月まで Innovate パートナーシップのメリットの完全なリストを無料でご覧いただけます。

1. [Adobe Exchange パートナーサポート センター ](https://adobeexchangeec.zendesk.com/hc/en-us?mkt_tok=NjA4LURIVi05MTUAAAF-P5lIeVWOuBmKMS_uE_NpgFKtC0ukt7z_ksnq_Sbzb6mzXUuXpqpqQeujtPdZ24WcjMdptygQSR9XrYt_Cw) に移動します
1. 右上隅の「リクエストを送信」をクリックします
1. **以下で問題を選択してください** ドロップダウンで「Adobe Exchange サポート」を選択します
1. **メールアドレス** にメールアドレスを入力します
1. **件名** ボックスに「LaunchPoint オファー」と入力します
1. 「**説明**」ボックスに「LaunchPoint Offer」と入力します
1. **サポートタイプ** ドロップダウンで、「プログラムサポート」を選択します
1. **Adobe Exchange製品** ドロップダウンで「Adobe Exchange プログラム」を選択します
1. フォームを送信します 当社のチームから間もなくご連絡いたします。

Posted on _2021-07-22_ by _David_

## 2021 年 8 月の更新

2021 年 8 月には、既存の REST API を強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

* Bulk Activity Extract API が強化され、6 つの異なるアクティビティタイプのプライマリ属性を使用してユーザーがフィルタリングできるようになりました。 詳しくは、[ 一括アクティビティ抽出 ](/help/rest-api/bulk-activity-extract.md) を参照してください。
* Marketo Sales Connect のユーザーがセールスアクティビティのデータにより多くのアクセス権を持つように、セールスアクティビティ属性を追加しました。 「Sales Email」アクティビティ、「Open Sales Email」アクティビティ、「Click Sales Email」アクティビティに次の属性を追加しました。

* Marketo Sales Person ID - Sales Connect における人物レコードの一意の ID
* 販売キャンペーン名 – メールが販売キャンペーンの一部であった場合の販売キャンペーンの名前
* Sales Campaign URL - メールが Sales Campaign に含まれていた場合の Sales Connect URL
* Sales Template Name - テンプレートが使用されていた場合の、Sales Connect のメールテンプレートの名前
* 営業テンプレート URL - テンプレートが使用されていた場合の、メールテンプレートの営業接続 URL

### メール

* `earliestUpdatedAt`/`latestUpdatedAt` フィルターを追加して、メールの取得エンドポイントを強化しました。 これにより、「`updatedAt`」フィールドを使用してメールのサブセットのみを検索し、増分同期を可能にできます。
* [ チャンピオンおよびチャレンジャー ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/email-tests-champion-challenger/add-an-email-champion-challenger) タイプのメールレコードの取得をサポートするために、メールの取得、名前によるメールの取得、ID によるメールの取得エンドポイントを強化しました。

### 欠陥の解決

* ユーザーを取得エンドポイントの問題を修正しました。 [ マーケティングカレンダー ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/marketing-calendar/understanding-the-calendar/issue-revoke-a-marketing-calendar-license) ライセンスを発行されたユーザーは返されませんでした。 マーケティングカレンダーユーザーが正しく返されるようになりました。
* 送信フォームエンドポイントに関する問題を修正しました。 リードレコードが重複する場合、送信フォームを使用して「1007、複数のリード一致検索条件」エラーが発生します。 送信フォームは、[Forms 2.0 API](/help/javascript-api/forms-api-reference.md) と同じ方法で、最近更新されたレコードを更新するようになりました。
* リードフィールドの更新およびリードフィールドの作成エンドポイントから返される誤解を招くエラーメッセージをいくつか改善しました。 [LM-151890、LM-151888、LM-151889]
* 名前によるリードフィールドの取得およびリードフィールドの取得エンドポイントの問題を修正しました。 両方のエンドポイントが、わずかに古い情報を返す可能性があります。 常に現在の情報を返すようになりました。
* 部分取得に「range」 HTTP ヘッダーを使用した際に、範囲内の最後のバイトが返されなかった [Bulk Extract API](/help/rest-api/bulk-extract.md) の問題を修正しました。
* 更新スニペットメタデータエンドポイントの問題を修正しました。 スニペットの名前または説明を更新する際に、スニペットのステータスが「ドラフトで承認済み」に変更されました。 スニペットの名前または説明を更新しても、スニペットのステータスは変わりません。
* メールモジュールを追加エンドポイントに関する問題を修正しました。 スニペットを含むモジュールを追加すると、「611、システムエラー」が返されました。 これで、モジュールがメールに正しく追加されるようになりました。
* プログラムのエンドポイントを削除する際の問題を修正しました。 アプリ内メッセージのローカルアセットを含むプログラムを削除すると、「611、システムエラー」が返されていました。 プログラムが正しく削除されるようになりました。

Posted on _2021-08-22_ by _David_

## Munchkin バージョン 161 ロールアウト

2021 年 9 月 7 日に、Munchkinのバージョン 161 がMunchkin Betaを有効にしたサブスクリプションの 10% へのロールアウトを開始し、9 月 16 日に 50%、9 月 30 日に 100% が続きます。 この変更は、Marketo ランディングページと、外部ランディングページに提供されるファイル munchkin-beta.js のバージョンに影響を与えます。このファイルは、新しいバージョンがロールアウトされたサブスクリプションから読み込まれます。 このバージョンでは、Munchkinのリードの関連付けメソッドが完全に廃止されています。このメソッドは、Marketo サブスクリプションに人物データを送信し、関連する web ブラウジング履歴を既知の人物レコードと関連付けることができる機能です。 [Forms JS API](/help/javascript-api/forms-api-reference.md)、Form Submit API、[Associate Lead REST API](/help/rest-api/leads.md) など、より現代的で安全な代替手段に置き換わり、リードの関連付けが削除されています。 ユーザーまたは組織がこの方法を使用している場合、10 月のリリースのロールアウトが開始される予定の 2021 年 10 月 12 日までに使用状況から移行する必要があります。 Munchkin ベータ版をオプトインしない場合は、「Marketo ランディングページのMunchkin Beta」機能を切り替えて `disabled` 宝箱メニュー [ に ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features) り込み、ランディングページでの使用を無効にすることができます。 Munchkin Beta JavaScriptを外部 web ページにデプロイしており、デフォルトのMunchkin リリースチャネルに切り替える場合は、コードスニペットを更新して、munchkin-beta.js ではなく munchkin.js からMunchkin JavaScriptを読み込む必要があります。

Posted on _2021-08-24_ by _Kenny_

## Munchkin サービスの TLS 1.0 および TLS 1.1 のサポート終了

2021 年 10 月 21 日以降、Munchkin JavaScriptを訪問者に提供するために使用されるmunchkin.marketo.netでは、[TLS 1.0 または TLS 1.1.](https://en.wikipedia.org/wiki/Transport_Layer_Security) を使用した接続を受け付けなくなります。これらの暗号化標準は、web セキュリティのベストプラクティスの一部として受け入れられなくなり、最新のブラウザーバージョンではサポートされなくなります。 この変更による悪影響は予想されません。

Posted on _2021-10-04_ by _Kenny_

## 2021 年 10 月の更新

2021 年 10 月には、既存の REST API を強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

* [ 送信フォーム ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/SubmitFormUsingPOST) エンドポイントが強化され、フォーム送信の一環としてプログラムメンバーのカスタムフィールドをサポートするようになりました。 必要に応じて、フォームを追加するプログラムや、プログラムメンバーのカスタムフィールドを追加するプログラムとして、プログラムを指定することもできます [ こちら ](/help/rest-api/leads.md)。
[ プログラムメンバーの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getProgramMembersUsingGET) エンドポイントが強化され、updatedAt 属性に基づいて日付範囲ベースのクエリをサポートするようになりました。 これは、[ こちら ](/help/rest-api/program-members.md) で説明しているように、開始および終了の datetime パラメーターを渡すことで行われます。
* [ リードフィールド ](/help/rest-api/leads.md)API を拡張して、「機密フィールド [ をサポートするようにしました ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/field-management/mark-a-field-as-sensitive)。 [ 名前によるリードフィールドの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadFieldByNameUsingGET)、[ リードフィールドの取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadFieldsUsingGET)、[ リードフィールドの作成 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createLeadFieldUsingPOST) および [ リードフィールドの更新 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/updateLeadFieldUsingPOST) エンドポイントで isSensitive 属性がサポートされるようになりました。

### 欠陥の解決

* [User Management](/help/rest-api/user-management.md) API に関する問題を修正しました。 [Marketo](https://business.adobe.com/products/marketo/sales-insight.html) で使用するように設定されているセールスInsightユーザーに関連します。 これらのユーザーは [ ユーザーを取得 ](https://developer.adobe.com/marketo-apis/api/user/#operation/getUsersUsingGET) エンドポイントから返されるようになりました。また、これらのユーザーは [ ユーザーを削除 ](https://developer.adobe.com/marketo-apis/api/user/#operation/deleteUserUsingPOST) エンドポイントを使用して削除できるようになりました。 [LM-155864]
* [ リッチテキストフィールド ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/addRichTextFieldUsingPOST) エンドポイントの追加に関する問題を修正しました。 メール、ランディングページ、スニペットまたはフォームに 65,000 文字を超えるリッチテキストフィールドを追加すると、「611、システムエラー」が返されました。 エラー「701、操作を完了できません。 &#39;content&#39;は最大長の 65,535 バイトを超えています。

Posted on _2021-10-25_ by _David_

## 2022 年 1 月更新

2022 年 1 月には、既存の REST API を強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

* [ 一括カスタムオブジェクト抽出 ](/help/rest-api/bulk-custom-object-extract.md) API が強化され、ユーザーが **updatedAt** の日付範囲を使用してフィルタリングできるようになりました。
* プログラムメンバーフィールドのメタデータを作成、更新、取得できるプログラムメンバーフィールドのメタデータ API を追加しました。 詳しくは、[ プログラムメンバー/フィールド ](/help/rest-api/program-members.md) を参照してください。
* 会社フィールドのメタデータを取得できる、会社フィールドメタデータ API を追加しました。 詳しくは、[ 会社/フィールド ](/help/rest-api/companies.md) を参照してください。
* 商談フィールドのメタデータを取得できる、商談フィールドメタデータ API を追加しました。 詳しくは、[ 商談/フィールド ](/help/rest-api/opportunities.md) を参照してください。
* 名前付きアカウントフィールドのメタデータを取得できる、名前付きアカウントフィールドメタデータ API を追加しました。 詳しくは、[ 重点顧客/フィールド ](/help/rest-api/named-accounts.md) を参照してください。
* フィールドが REST API によって作成されたかどうかを示す新しいブール型プロパティ **isApiCreated** を返すように、フィールドメタデータエンドポイントを更新しました。

### 欠陥の解決

* [ リードフィールドを作成 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createLeadFieldUsingPOST) エンドポイントへの呼び出しの時間と、新しく作成されたリードフィールドがスマートリストで使用可能になった時間の間の待ち時間の問題を修正しました。 [LM-152838]
* Marketo Engage UI で [ フォームにフィールドを追加 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createLeadFieldUsingPOST) するために使用されるフォームフィールドドロップダウンリストで、作成したフィールドが使用できない [ リードフィールドを作成 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/demand-generation/forms/creating-a-form/add-a-field-to-a-form) エンドポイントの問題を修正しました。 [LM-158243]
* isTriggerable=true パラメーターが指定されている場合に、トリガー可能なキャンペーンが返されなかった [ キャンペーンを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCampaignsUsingGET) エンドポイントの問題を修正しました。 [LM-158283]
* [ リスト ID でリードを取得 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteTokenByNameUsingPOST) エンドポイントが、特定の場合に「611、システムエラー」というエラーを返す問題を修正しました。 [LM-157214]
* [ リードフィールドを更新 ](/help/rest-api/leads.md) エンドポイントから返される複数のエラーメッセージをクリーンアップしました。 [LM-151886、LM-151888、LM-151889]

Posted on _2022-01-27_ by _David_

## 2022 年 3 月更新

2022 年 3 月には、既存の REST API を強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

* Bulk Activity Extract API で生成された書き出しファイルに **actionResult** フィールドを追加しました。 このフィールドは、成功、スキップ、失敗の各アクティビティを区別するために使用できます。
* **Emails API** からの応答に「[isOpenTrackingDisabled](/help/rest-api/emails.md)」フィールドを追加しました。 このフィールドは、「[ 開封トラッキングを無効にする ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-editor-v2-0-overview) 機能が有効になっているかどうかを判断するために使用できます。
* プログラムタグを選択的に管理できる 2 つのエンドポイントを追加しました。 [ プログラムタグを更新 ](/help/rest-api/programs.md) エンドポイントを使用すると、プログラムタグを選択的に更新できます。 [ プログラムタグを削除 ](/help/rest-api/programs.md) エンドポイントを使用すると、プログラムタグを選択的に削除できます。
* **isExecutable** パラメーターを [Clone Smart Campaign](/help/rest-api/smart-campaigns.md) エンドポイントに追加しました。 このパラメーターを使用すると、プログラムを実行可能プログラムとして複製できます。
* **headStart** フィールドを [Programs API](/help/rest-api/programs.md) に追加しました。 これにより、メールプログラムの [Head Start](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/email-programs/email-program-actions/head-start-for-email-programs) 設定を作成、更新、取得できます。

### 欠陥の解決

* [ メール動的コンテンツの取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailDynamicContentUsingGET) エンドポイントの問題を修正しました。 テンプレートの関係が壊れたメールから動的コンテンツを含む件名行を取得しようとすると、「API はテンプレートを含むメールに対してのみ操作を許可します」というエラーが返されていました。 エンドポイントが動的コンテンツを返すようになりました。 [LM-152331]
* [ リードを同期 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) エンドポイントに関する問題を修正しました。 externalSalesPersonId を使用して externalSalesPersonId を使用し、action = createDuplicate を使用して Sales Person をリードに関連付けると、Sales Person の関連付けが発生しません。 [LM-158990]

### Adobe IMSの統合

* Adobe IMS [User](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview) にオンボーディングされたユーザーは、[Marketo User Management API](/help/rest-api/user-management.md) のすべてを使用することはできません。 Adobe IMSと統合されているMarketo インスタンスで呼び出されると、次のエンドポイントはエラーを返します。[ ユーザーを招待 ](https://developer.adobe.com/marketo-apis/api/user/#operation/inviteUserUsingPOST)、[ID で招待ユーザーを取得 ](https://developer.adobe.com/marketo-apis/api/user/#operation/getInvitedUserUsingGET)、[ ユーザー属性を更新 ](https://developer.adobe.com/marketo-apis/api/user/#operation/updateUserAttributeUsingPOST)、[ ユーザーを削除 ](https://developer.adobe.com/marketo-apis/api/user/#operation/deleteUserUsingPOST)、および [ 招待ユーザーを削除 ](https://developer.adobe.com/marketo-apis/api/user/#operation/deleteInvitedUserUsingPOST)。 代わりに、[Adobe User Management API](https://developer.adobe.com/umapi/) を使用してください。

Posted on _2022-03-14_ by _David_

## 2022 年 5 月の更新 – 

2022 年 5 月には、既存の REST API を強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストをご覧ください。

* Marketo Engage インスタンスで [SFDC Sync](/help/rest-api/companies.md) または [Microsoft Dynamics Sync](/help/rest-api/opportunities.md) が有効になっている場合に [ 会社 ](/help/rest-api/sales-persons.md) [、&lbrace; 商談 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync) および [ 営業担当者 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync) のレコードを取得する機能が追加されました。
* [ メールの動的コンテンツを取得 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailDynamicContentUsingGET) エンドポイントを更新して、メールの件名から [ 動的コンテンツ ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/using-dynamic-content-in-an-email) を取得できるようになりました。 これは、特定のメールがメールテンプレートにリンクされているかどうかに関係なく機能します。

`POST /rest/asset/v1/form/{id}/field/State.json?values=[{"label":"Alaska"},{"value":"AK"},{"label":"West Virginia","value":"WV"},{"label":"Wyoming","value":"WY"}]`

* [ フォームフィールド表示ルールを追加 ](https://developer.adobe.com/marketo-apis/api/asset/#operation/getAllProgramMemberFieldsUsingGET) エンドポイントを更新し、**isNot** タイプの [ 非表示ルール ](/help/rest-api/forms.md) に複数の比較値を追加できるようになりました。 次に例を示します。

`POST /rest/asset/v1/form/{id}/field/LastName/visibility.json?visibilityRule={"ruleType":"show","rules":[{"subjectField":"LastName","operator":"isNot","values":["A","B","C"]}`

### 欠陥の解決

* [leadFormFields](/help/rest-api/leads.md) パラメーターの属性に「null」を渡すときに発生する [ 送信フォーム ](/help/rest-api/leads.md) エンドポイントの問題を修正しました。「611、システムエラー」というエラーが返されました。 「1003、フォームの検証に失敗しました」エラーを正しく返すようになりました。 [LM-162213]

Posted on _2022-05-09_ by _David_

## 2022 年 8 月の更新

2022 年 8 月に、既存の REST API を強化しています。 以下のアップデートの完全なリストをご覧ください。

書き出しプログラムメンバージョブの作成エンドポイントを呼び出す際に使用できるフィルターをいくつか新しく追加しました。 フィルターの多くは、相互に組み合わせて使用し、抽出したデータセットを絞り込むことができます。

* **programIds** フィルターを使用して、スループットの向上に役立つ最大 10 個のプログラム識別子を指定できます。
* **isExhausted** フィルターを使用して、レコードを [ コンテンツを使い果たした人 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/drip-nurturing/using-engagement-programs/people-who-have-exhausted-content) にフィルターを適用できます。
* **nurtureCadence** フィルターを使用すると、[ エンゲージメントプログラム頻度 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/program-flow-actions/change-engagement-program-cadence) に基づいてレコードをフィルタリングできます。
* **statusNames** フィルターは、1 つ以上の [ プログラムステータス ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/creating-programs/understanding-program-membership) のレコードをフィルタリングするために使用できます。
* **updatedAt** フィルターを使用すると、日付範囲に基づいてレコードをフィルターできます。

### お知らせ

* [ID](https://developer.adobe.com/marketo-apis/api/identity/#operation/identityUsingGET) エンドポイントの動作が変更されました。 エンドポイントを呼び出し、**access_token** パラメーターを含めない場合、「603, Access denied」エラーが返されます。 以前は、「600、空のアクセストークン」エラーが返されていました。 「600、空のアクセストークン」エラーは非推奨（廃止予定）となりました。

Posted on _2022-09-03_ by _David_

## 2022 年 10 月の更新

2022 年 10 月に、既存の REST API を強化します。 以下のアップデートの完全なリストをご覧ください。

* [ 一括リード読み込み API](/help/rest-api/bulk-lead-import.md) が強化され、読み込みプロセス中に販売担当者レコードにリードを追加できるようになりました。 これを行うには、インポートファイルに **externalSalesPersonId** フィールドを含めます。
* スコアタイプフィールドの作成時に発生した [ リードフィールドを作成 ](/help/rest-api/leads.md) エンドポイントの問題を修正しました。 これらのフィールドは、Marketo Engage UI の [ スコアを変更 ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/change-score) フローアクションでは使用できませんでした。 [LM-166815]

### お知らせ

* プログラム メンバーシップ属性 `acquiredBy` が更新可能に変更されました。

Posted on _2022-10-18_ by _David_

## Marketo Forms REST AP に対する今後の変更

2023 年 3 月 24 日（PT）の週に現在スケジュールされている 2022.R2 リリース以降、Adobe Marketo Engage Forms Asset API は、フォームがプログラムの子であるかどうかに関係なく、常にプリフィックスの付いたプログラム名なしのフォーム名のみを返します。 この変更により、アセット名に関するForms API の動作が他のAdobe Marketo Engage Asset API と一致するようになります。 サービスの中断を避けるために、Marketo Engage Forms API を使用する統合を確認し、インテグレーターと協力して、これに対応するための変更が必要かどうかを確認する必要があります。この今後の変更に先立ち、Forms API から返される名前には、マーケティングアクティビティのプログラムの子であるフォームのプログラム名の先頭に一貫性のないプレフィックスが付けられます。 例えば、「Program 1」の子である「Form 1」という名前のフォームは、API によって次のように名前が返される場合があります。Program 1.Form 1 または Form 1 2022.R2 リリース以降、フォームの名前は常に、プレフィックスが付いたプログラム名なしで返されます。 同じ例を使用すると、名前は常に Form 1 になります。

Posted on _2022-11-04_ by _Kenny_

## 2023 年 1 月更新

2023 年 1 月に、管理 UI の API 関連の機能強化を行い、2 つのお知らせを行っています。 以下のアップデートの完全なリストをご覧ください。

管理 UI

### リードの一括抽出

* Marketo Engage管理 UI が強化され、サブスクリプションの Bulk Extract API の 1 日あたりの処理能力の配分を確認できるようになりました。 さらに、過去 7 日間の API ユーザーによる容量使用状況を表示できます。 詳しくは[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/settings/bulk-export-api-information)をご覧ください。

### 欠陥の解決

* [ 商談を削除 ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteOpportunitiesUsingPOST) エンドポイントの問題を修正しました。 場合によっては、「オポチュニティから削除」アクティビティが生成されていませんでした。 [LM-172208]

### お知らせ

* REST API と HTTP 応答メッセージ [ 理由句 ](https://nation.marketo.com/t5/product-documents/upcoming-change-to-marketo-rest-api/ta-p/331698) の変更点については、Marketo Community の [ この記事 ](https://www.rfc-editor.org/rfc/rfc7230#section-3.1.2) を参照してください。
* プログラム メンバーシップ属性 **statusReason** が更新可能に変更されました。

Posted on _2023-01-21_ by _David_
