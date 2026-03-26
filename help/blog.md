---
title: ブログのアーカイブ
description: Marketo Developer Blog archive 2014-2023 Forms 2.0、Zapier、API アップデート、SOAPの非推奨化、RESTへの移行に関する過去の投稿を紹介します。
exl-id: d7ae88dd-9938-4957-9798-db43090dab4e
source-git-commit: a0901d2c67aa42368f03494dc8157d2ae93b3dce
workflow-type: tm+mt
source-wordcount: '65252'
ht-degree: 3%

---

# ブログのアーカイブ

>[!INFO]
>
>これは、2014年から2023年までのMarketoブログのアーカイブです。 ここでは歴史的な参考資料としてのみ提供されています。
>一部の情報が古くなっている可能性があります。  最新の機能については、常に現在のドキュメントを確認してください。
>

>[!IMPORTANT]
>SOAP APIは非推奨（廃止予定）であり、2026年7月31日をもって使用できなくなります。 新しい開発はすべてMarketo REST APIで行い、サービスの中断を避けるために、その日までに既存のサービスを移行する必要があります。 SOAP APIを使用するサービスがある場合は、移行方法について[SOAP API Migration Guide](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/migration)を参照してください。
>

>[!IMPORTANT]
>`access_token` クエリパラメーターを使用した認証のサポートは、2026年7月31日（PT）に削除されます。 プロジェクトでクエリパラメーターを使用してアクセストークンを渡す場合は、できるだけ早く[認証ヘッダー](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/rest/authentication#using-an-access-token)を使用するように更新する必要があります。 新しい開発では、Authorization ヘッダーのみを使用する必要があります。
>

## Marketo開発者ブログへようこそ

Marketo Developersへようこそ！ アドビは、Marketoにおいて、マーケターの成果を向上させる新機能をリリースするのに多忙を極めています。 今日のマーケターは、驚異的な開発者コミュニティに支えられています。 このブログは、現代のマーケターの急速に進化するニーズをサポートするweb開発者やソフトウェアエンジニアに捧げられています。 Marketo Platformの進化に伴い、新しい統合オプションとAPI バージョンのアップデートが公開されます。 また、Marketo Platformとの統合に関するコードサンプルとベストプラクティスを共有する新しい一連のハウツー記事も紹介します。 このシリーズの最初の記事では、APIを使用してMarketo内に保存されている人物（顧客/連絡先/リード）に関する情報を効率的に取得する方法について説明します。 上記のフォームを使用して購読し、最新の情報を入手してください。 新しい記事が公開されると、更新情報をメールで送信します。

投稿日：_2014-03-06_ by _David_

## 2014年1月のリリースアップデート

### Forms 2.0

Forms 2.0を使用すれば、プログラミングの知識がなくても、美しく安定した柔軟なweb フォームを作成できます。 エディター、コンディショナルロジック、堅牢なデザインの大幅な改善に加え、web サイトのあらゆるページにMarketo formsを簡単に埋め込めるようになりました。 開発者は、JavaScriptを使用してコア機能を拡張できます。ユースケースは次のとおりです。

* 送信に成功した後にフォームを非表示にして、訪問者がフォームに入力した後もページに残るようにします
* カスタムビジネスロジックに基づく送信時のカスタムエラーメッセージの表示
* ライトボックススタイルダイアログボックスでのフォームの表示

開発者ドキュメントは[こちら](/help/javascript-api/forms-api-reference.md)から入手できます。

### SOAP API バージョン 2_3が利用可能になりました

* [getLeadChanges:](/help/soap-api/getleadchanges.md) リクエストフィールド `activityNameFilter`を導入しました
* [ListOperation:](/help/soap-api/listoperation.md)がリクエストフィールド `skipActivityLog`を削除しました

**注：** SOAP API リビジョンは下位互換性があります

投稿日：_2014-01-26_ by _Travis Kaufman_

## Zapier パート II:Marketo統合のお知らせ

以前の記事では、Zapierを使用して外部データソースをMarketoと統合する方法について説明しました。 この記事では、Marketoやその他のアプリケーションを統合するために、独自のZapier ワークフロー（または「Zap」）をゼロから構築する方法について解説しました。 MarketoでZapierを使うというアイデアは気に入っていますが、始めるにはサポートが必要ですか？ 朗報です！ Zapierは、Marketo用のZapの例を数多くリリースしました。これにより、すぐに使い始めることができます。

* 新しいリードの獲得
* 顧客の育成
* 連絡先情報の配布
* 新しい見込み客への対応

これらの例に加えて、Zapier上の他の数百ものアプリケーションと[Marketo統合](https://zapier.com/apps/marketo/integrations) ページを参照して、独自の自動ワークフローを数分で構築できます。 コーディングは必要ありません。 時間を節約し、手作業を自動化。 クリエイティブになりましょう。 空は限界です！

投稿日：_2016-06-01_ by _David_

## APIを使用したMarketoからの顧客および見込み顧客の情報の取得

`getLead`および[`getMultipleLeads`](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads) SOAP APIを使用して、Marketo内に保存されている顧客と見込み客に関する情報を取得できます。 顧客や見込み客の情報が更新されたり、Marketoで新しいレコードが作成されたりすると、別のシステムが更新されないように、これらの情報を定期的に抽出することが必要になることがよくあります。 更新を求めてMarketoをポーリングするために、定期的に実行されるコードサンプルを示します。 次の図は、設定された定期的なタイマーで行われるAPI呼び出しを示しています。 ユースケースによっては、10分ごとに次のコードを実行するように定期的なタイマーを設定できます。

[`getMultipleLeads`](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads)への最初の呼び出しでは、時間範囲、batchSizeおよび返されるフィールドが設定されます。 指定された時間範囲で更新されたMarketo内のすべてのリードは、指定されたbatchSizeよりも多くのレコードが使用可能な場合、streamPositionとともに返されます。

**SOAP getMultipleLeads:**&#x200B;への最初の呼び出しに対するリクエスト

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

getMultipleLeads:**への最初の呼び出しからの** SOAP応答

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

`<remainingCount/>`の値が0より大きい限り、前回の呼び出しで返された`<newStreamPosition/>`の値を`<streamPosition/>` パラメーターに渡すことで、残りの部分をページネーションするために`getMultipleLeads`に対する後続の呼び出しを行います。**getMultipleLeads:**&#x200B;への後続の呼び出しに対するSOAP リクエスト

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

このロジックは、`<remainingCount/>`が0より大きい限り続きます。**上記のシナリオを実行するサンプル Java プログラムを以下に示します。**

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

### ヒント&amp;テクニック

Marketoから大量の連絡先を抽出する場合は、次のパラメーターに従ってAPI リクエストを調整することをお勧めします。

* `<includeAttributes/>`: システムとの同期を維持するために必要なフィールドのみをリクエストすることをお勧めします。 これにより、応答のペイロードが削減され、クエリのパフォーマンスが向上します。
* `<batchSize/>`: APIは、1回の呼び出しで返される最大1000件のレコードをサポートしています。 この値を500 レコードまで調整すると、応答のペイロードも削減されます。
* `<LastUpdatedAtSelector/>`: `<oldestUpdatedAt/>`と`<latestUpdatedAt/>` パラメーターの両方を設定して、日付範囲を制限することをお勧めします。 たとえば、1年分のデータについて1回のリクエストをおこなう代わりに。 より小さな日付範囲をリクエストするために、API呼び出しを分割します。

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-03-05_ by _Travis Kaufman_

## 2014年2月のリリースアップデート

### SOAP API アップデート

* [syncMObjects](/help/soap-api/syncmobjects.md)：既存プログラムのタグとチャネルを追加および更新できるようになりました。

更新は、[2_3 WSDL](http://app.marketo.com/soap/mktows/2_3?WSDL)に組み込まれます。

投稿日：_2014-02-26_ by _Travis Kaufman_

## 2014年3月リリースの更新

### SOAP API アップデート

* [syncLead](/help/soap-api/synclead.md)および[syncMultipleLeads](/help/soap-api/syncmultipleleads.md)のパフォーマンスが向上しました

更新は、[2_3 WSDL](http://app.marketo.com/soap/mktows/2_3?WSDL)に組み込まれます。

投稿日：_2014-03-20_ by _Travis Kaufman_

## 訪問者がフォームに入力したときに匿名の訪問者アクティビティを結合

「ビジネスロジックに基づく匿名の訪問者のアクティビティのキャプチャ」というタイトルのブログ記事では、カスタムイベントに基づいてMarketoで匿名のリードレコードを作成する方法について説明しました。 このブログ記事では、その記事を基に作成し、ユーザーの連絡先情報を受け取った後、匿名のリードレコードを既知のユーザーに関連付けます。 Marketoの[Munchkin トラッキングコード ](/help/javascript-api/lead-tracking.md)は、web サイトへの訪問をトラッキングするのに役立ちます。 Munchkinのトラッキングコードが適用されたweb サイトのページに初めてアクセスした場合、Marketoは匿名のリードを作成し、ブラウザーCookieを使用してそれらのリードをトラッキングします。 識別されると、既知のリードになり、ブラウザーCookieに関連付けられた履歴がMarketoリードレコードにマージされます。**匿名リードは、次のユーザーが作成したときに作成されます：**

1. Marketoのランディングページに初めてアクセス
1. Munchkinのトラッキングコードがあるページにアクセスします
1. Marketoの電子メールで「Web ページとして表示」リンクをクリックします

**匿名のリードは、次のユーザーが**&#x200B;になったときに、新規または既存の既知のリードに統合されます

1. Marketoの電子メールへのリンクをクリック
1. Marketo フォームへの入力
1. 次のいずれかの手法を使用して、匿名リードを既知のレコードに関連付けます。

人物データを送信するか、ブラウザーのweb トラッキング CookieをMarketoの対応する人物レコードに関連付けるには、次のいずれかの方法を使用します。**ブラウザー側の送信** ユースケースでブラウザーから人物データを送信する必要がある場合は、バックグラウンドフォーム送信を使用する必要があります。**サーバー側の送信** ブラウザー側の送信が必要ない場合、REST APIには、人物データ送信のための多くのメソッドと、Cookieを人物レコードに関連付けるための専用のメソッドが用意されています。

投稿日：_2014-04-22_ by _Murta_

## 2014年4月リリースの更新

### Marketo Formsのセキュリティアップデート

1つのIP アドレスからのフォーム投稿数と頻度の制限を導入しました。 この制限は、プログラマティックフォーム送信の悪意のある使用から顧客を保護するために、1分あたり30件の投稿で適用されるようになりました。 [syncLead API](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/soap/leads/synclead)は、Marketoで新しい連絡先をプログラムで送信する場合に推奨される統合手段です。

投稿日：_2014-04-29_ by _Travis Kaufman_

## Marketo APIを使用したフォームのポスト統合の置き換え

Adobe Marketoを使用するマーケターは、特定のweb フォームに入力したコンタクト数やリード数にもとづいて、マーケティング施策の成果を関連付けることが一般的です。 マーケターは、新しいMarketoフォームを作成し、ランディングページに配置してから、Marketoでトリガーキャンペーンを設定し、そのフォームに入力したすべてのコンタクトを、マーケティングプログラムの成功として関連付けるだけです。 （以下のスクリーンショットを参照）。 キャンペーンの成功がフォームに入力する外部にある場合でも、プログラムの成功を記録する際に同じアプローチを使用することは自然な拡張です。 たとえば、マーケターがプロモーションオファーを実行し、コンバージョンが電話をかけたり予約を入れたりする場合。 見込み客がフォームに記入していない場合。 次の記事では、Marketo syncLead APIを使用して新しい連絡先を作成し、その連絡先が新しい連絡先である場合はrequestCampaign APIを使用して、特定のマーケティングプログラムの成功を記録する方法について説明します。

投稿日：_1970-01-01_ by _Travis Kaufman_

## Marketo APIを使用したリードの削除

例えば、Marketo APIを使用してリードを削除するとします。 これは、リードを削除するために事前に定義されたフローアクションを持つキャンペーンでrequestCampaign APIを呼び出すことによって実現できます。 最初にスマートキャンペーンを作成する方法、2番目にAPIを介してキャンペーンを実行するトリガーを設定する方法、3番目にフローアクションの一部としてリードを削除する方法、4番目にこのキャンペーンを実行するために使用されるコードサンプルを示します。**Marketoで新しいスマートキャンペーンを作成する方法** Marketoのスマートキャンペーンは、すべてのマーケティング活動を実行します。 スマートキャンペーンでは、一連の自動化アクションを設定して、連絡先のスマートリストに対して実行できます。 リードを削除する場合は、次に示すように、キャンペーンでトリガーを設定します。 まず、スマートキャンペーンを設定します。

1. マーケティングアクティビティで、プログラムを選択し、「新規」ドロップダウンで「新規ローカルアセット 1」をクリックします。 「スマートキャンペーン」をクリックすると
1. スマートキャンペーン名を入力し、「スマートキャンペーンにトリガーを追加」をクリックします。スマートキャンペーンにトリガーを追加すると**ライブイベントに基づいて一度に1人ずつスマートキャンペーンを実行できます。この場合は、requestCampaign APIを介したリクエストです。
1. 「Campaign is Requested」トリガーを検索し、キャンバスにドラッグ&amp;ドロップします。
1. トリガーで、「is」と「Web Service API」を選択します。

**キャンペーンでリードフローを削除アクションを作成する方法**&#x200B;上部メニューの「フロー」をクリックします。 右側のメニューから、「リードを削除」を検索し、中央にドラッグしてトリガーとしてキャンペーンに追加します。 注：Marketoからのみリードを削除し、CRMに残すと、そのリードのデータのいずれかが更新されると、そのリードはMarketoで再作成されます。  **requestCampaign APIを呼び出すコードサンプル** Marketo インターフェイスでキャンペーンとトリガーを設定した後、このキャンペーンを実行するためにAPIを使用する方法を示します。 最初のサンプルはXML リクエストで、2番目はXML レスポンスで、最後のサンプルはXML リクエストの生成に使用できるJava コードサンプルです。 また、requestCampaign APIを呼び出す際に使用されるキャンペーン IDを見つける方法も示します。 また、API呼び出しには、MarketoキャンペーンのIDを事前に把握する必要があります。 次のいずれかの方法を使用して、キャンペーン IDを決定できます。

1. [getCampaignsForSource](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCampaignsUsingGET) APIの使用
1. ブラウザーでMarketo キャンペーンを開き、URL アドレスバーを確認します。 キャンペーン ID （4桁の整数で表されます）は、「SC」の直後に見つけることができます。 たとえば、`https://app-stage.marketo.com/#SC**1025**A1` のように設定します。 太字の部分はキャンペーン ID 「1025」です。 requestCampaignに対するSOAP リクエスト

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

requestCampaignのSOAP Response

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

上記のシナリオを実行するサンプル Java プログラムを以下に示します。

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

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-05-16_ by _Murta_

## Munchkin APIを使用したカスタムアクティビティトラッキング

ここでは、Marketoでカスタムアクティビティを追跡し。 例えば、web ページに動画があり、動画の50%以上を視聴している訪問者を追跡したい場合、 これは、Munchkinのカスタムアクティビティトラッキング機能を使用して実行できます。 これは、ビデオが50%に達するイベントをリッスンし、Munchkin APIを呼び出すことによって実装されます。 これを行うには、ページ上のこのイベントに基づいて、Marketoで呼び出すカスタムアクティビティを設定する必要があります。 ビデオプレーヤーにはYouTubeを使用し、[YouTube Iframe API](https://developers.google.com/youtube/iframe_api_reference)を使用してMunchkin APIでメソッドを呼び出します。

最初に、MarketoでMunchkin トラッキングコードを生成する方法、2番目にページイベントに基づいてMunchkin サンプルコードをトリガーに変更する方法、3番目にフローステップを含むページ上のアクションによって定義されるスマートリストを使用してキャンペーンを設定する方法、5番目に匿名ユーザーからのページ訪問がMarketoに記録されたことを確認する方法を示します。 ====このブログ記事は、説明されているコードの実例です。 Marketoの既知のユーザーである方は、このフォームに記入してください。 このようにして、動画の50%を視聴すると、その動画の残りの部分が送信され、動画の100%を視聴すると、別のブログ投稿へのリンクが送信されます。 === <https://developers.google.com/youtube/iframe_api_reference>

**Munchkin トラッキングコードの生成方法** Munchkin トラッキングコードを使用すると、web サイトへの訪問をトラッキングできます。 以下に示すMunchkin コードには3つの種類がありますが、この例では、非同期Munchkin トラッキングコードを使用しています。 A）単純：コードの行が少ないですが、web ページの読み込み時間に最適化されません。 このコードは、web ページを読み込むたびに jQuery ライブラリーを読み込みます。 B）非同期：web ページの読み込み時間を短縮します。 このコードは、jQuery ライブラリが既に存在するかどうかを確認し、存在しない場合は読み込み、web ページの残りの部分が読み込まれたらトラッキングコードを実行するために使用します。 C）非同期jQuery:web ページの読み込み時間を短縮し、システムパフォーマンスも向上させます。 既に jQuery があると想定し、チェックも読み込みも行いません。

1. アプリの右上にある「管理」をクリックします。
1. 左側のツリーで「Munchkin」をクリックします。
1. トラッキングコードタイプは「非同期」を選択します。
1. クリックしてJavaScript トラッキングコードをコピーし、web サイトに配置します。**YouTube コード** <https://developers.google.com/youtube/js_api_reference#EventHandlers> <https://developers.google.com/youtube/iframe_api_reference> player.

`getCurrentTime()` ビデオの再生が開始されてからの経過時間を秒単位で返します。`player.getDuration()` 現在再生中のビデオのデュレーションを秒単位で返します。 `getDuration()`は、ビデオのメタデータが読み込まれるまで0を返します。通常、ビデオの再生が開始された直後に発生します。 Cookieを使用していないユーザーがMunchkin トラッキングコードを使用してページにアクセスすると、ユーザーのブラウザーに新しいCookieが作成され、Marketoに新しい匿名リードが作成されます。 ユーザーが既にCookieを使用しており、そのユーザーがMarketoの既存のリードである場合、そのページへの訪問はMarketoのユーザーのアクティビティログに記録されます。**コードサンプルをCookie ユーザーに送信してイベントを追跡** トラッキングコードを`</body>` タグの直前にweb ページに配置します。 Marketo で作成したランディングページには、自動的にトラッキングコードが追加されるので、このコードを貼り付ける必要はありません。 このコードサンプルは、スクリプトの読み込み後にMunchkin APIを呼び出します。

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

このコードサンプルは、ユーザーが5秒間ページにアクセスし、ページを500 ピクセル下にスクロールした後に、Munchkin APIを呼び出します。

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

1. 上部メニューの「分析」をクリックし、「新しいレポート」をクリックします。 レポートタイプとして「Web ページアクティビティ」を選択し、レポートに名前を付けます。
1. レポートを作成したら、「スマートリスト」をクリックします。 次に、右側のボックスから「訪問したWeb ページ」フィルターを選択します。 Munchkinのトラッキングコードを入力するweb ページを入力します。
1. 「設定」をクリックします。 ISPから「匿名の訪問者」を選択し、「表示」オプションを変更します。
1. 「Report」をクリックします。 これで、選択したweb ページで追跡されたアクティビティが表示されます。
1. リードレコードをダブルクリックすると、アクティビティログが表示され、匿名ユーザーが訪問した特定のページを確認できます。

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

例えば、マルチメディアコンテンツを含むページの場合、カスタムトラッキングを実行できます。 一般的な例としては、Munchkin トラッキングコードをページに追加し、Munchkin APIを使用して、ビデオの再生やオーディオクリップのリスニングなどのアクティビティに対するMarketo インスタンスのイベントを生成します。 Munchkinのトラッキングコードは、ほとんどまたはすべてのweb ページに配置することをお勧めします。 Munchkin トラッキングコードは、Marketoを使用して作成したランディングページに自動的に含まれます。 この呼び出しを使用して、ユーザーがAjax、Flash、またはその他のRIA環境のページにアクセスするなど、何かをしたことを記録します。 URLには「」または任意のドメインを含めることはできませんが、存在しないページであっても、任意のページを指すことができます。 URL パラメーターを追加する場合は、params引数を使用します。
このイベントは、呼び出し元のweb ページのドメインの下にあるユーザーのアクティビティログに訪問web ページ イベントとして表示されます。 メモ `mktoMunchkin()`への最初の呼び出しでは、現在のページに対して常にWeb ページ訪問イベントが作成されます。 追加のweb ページ訪問を追跡しない限り、`visitWebPage`を呼び出す必要はありません。`mktoMunchkinFunction('visitWebPage', { url: '/MyFlashMovie/Story1', params: 'x=y&2=3' });`  メモ JavaScriptの経験豊富な開発者にアクセスできることを確認してください。 Marketo テクニカルサポートでは、カスタム JavaScript のトラブルシューティングについては対応できません。 Munchkin JavaScript APIを使用すると、サードパーティのweb システムとMarketo アカウントを統合できます。 一部のweb開発では、web サイト上の既存のアプリケーションで、新しいリードを獲得したり、現在のリードを更新したりできます。 たとえば、新規顧客情報を取得する顧客登録用のweb アプリケーションがあるとします。 ほんの少しプログラミングするだけで、Marketoでキャプチャされたユーザーのリード情報と、今後のweb トラッキング用に設定されたMarketo cookieを入手できます。

さらに、web開発者は、FlashやAjaxなどのリッチなweb環境からweb アクティビティ情報を取得して追跡できます。 注：適切な開発リソースがある場合は、このAPIの代わりにSOAP APIを使用して統合を行うことを検討してください。 SOAP APIは、Munchkin APIよりも堅牢で、より多くの機能を備えています。 Marketo SOAP API要件これらのいずれかが機能するためには、web ページにMunchkin JavaScript コードを含める必要があります。 必要なスクリプトタグは、Munchkin チュートリアルで確認できます。 チュートリアルにも記載されているMunchkin APIも有効にします。
「Munchkin API呼び出しを行った後、Cookieを持っていないユーザーは自動的にCookieを使用します。 Marketoでは、ユーザーのアクティビティログにイベント（リンクをクリック、web ページにアクセス、または新しいリード）が記録されます。 クリックリンクを使用している場合、またはweb ページ呼び出しにアクセスしている場合、イベントはそのリードのアクティビティログ（既知または匿名）に追加されます。 これが新しいリードで、アソシエイトリード呼び出しを使用すると、そのリードは既知のリードになり、アクティビティ履歴が保持されます。 これが既存のリードである場合（メールアドレスの一致に基づく）、変更された値または新しい値はそのリードのレコードで更新されます。

これが`munchkinFunction`呼び出しの一般的な形式です。 呼び出す場所にweb ページのタグとして含めます。 この関数は、他のJavaScript関数と同様に呼び出すことができます。 ただし、`mktoMunchkinFunction()`呼び出しを行う前に、Munchkin トラッキング関数`mktoMunchkin()`を呼び出す必要があります。

```javascript
<script src="http://munchkin.marketo.net/munchkin.js" type="text/javascript"> mktoMunchkin("###-###-###"); mktoMunchkinFunction('function', { key: 'value', key2: 'value'}, 'hash');
```

ここで、`###-###-###`はアカウント関数のMunchkin アカウント IDです。これは、`associateLead`に対してのみ必要なコールハッシュに必要なパラメーターの配列としてパラメーターを作成する呼び出しです

投稿日：_1970-01-01_ by _Murta_

## Marketoへのデータの取り込み

Marketoにデータを取り込むさまざまな方法を次に示します。 フォーム、カスタムオブジェクト、統合に重点を置きます。

[Murtza Manzur](https://www.slideshare.net/MurtzaManzur)からMarketo](https://www.slideshare.net/MurtzaManzur/getting-data-into-marketo-35662408)にデータを取り込む[

投稿日：_2014-06-06_ by _Murta_

## Workspaceでのリードの作成

例えば、自社に北米と欧州の2つの部門があるとします。 Marketoの会社部門にもとづいてリードをセグメンテーションしたい場合。 これを実現するには、Marketoの機能であるワークスペースを使用して、リードへのアクセスを制限できます。 これを行うには、北米のワークスペースとヨーロッパのワークスペースを作成します。 その後、[syncLead API](/help/soap-api/synclead.md)を使用して、特定のワークスペースでリードを作成できます。 組織に次の機能がある場合は、ワークスペースとリードパーティションの使用を検討する必要があります。

1. 複数の製品ラインを担当する個別のマーケティングチーム
1. 地域や国ごとにマーケティングチームを分ける
1. 親会社および子会社
1. 親会社とリセラー

リード・パーティションおよびワークスペースを使用する場合は、次のことができます。

1. 組織内のリードへのアクセスを制限
1. 組織内のアセットへのアクセスを制限
1. マーケティング部門とアセットを共有

最初にUIを使用してMarketoでワークスペースを作成する方法を示し、次に[syncLead API](/help/soap-api/synclead.md)を使用してそのワークスペースにリードを書き込む方法を示します。**Workspaceの作成** ワークスペースとは、リードとMarketo アセットのセットです。 ワークスペースでは、そのワークスペースとアセット（メール、キャンペーン、リストなど）のリードのみを表示できます そのワークスペースで。 そのワークスペース内のスマートキャンペーンは、そのワークスペース内のリードにのみ影響します。 アカウント内のワークスペースを表示するには：

1. 管理者セクションの「ワークスペースとリードパーティション」ページに移動します。 ワークスペースが「ワークスペース」タブに表示されます。 1. 新しいワークスペースを作成するには、「ワークスペース」タブのメニューバーにある「新規Workspace」ボタンをクリックします。
1. ダイアログで、新しいワークスペースに関する情報を追加する必要があります。

* **Workspace名** - インターフェイスに表示されるこのワークスペースの名前
* **説明** - ワークスペースのオプションのテキスト説明
* **リード パーティション** – このパーティションに表示されるリード。
* **すべてのリード パーティション** – 現在および将来のすべてのパーティションからのリードが表示されます
* **個々のパーティションを選択** – それらのパーティションからのリードのみが表示されます（将来のパーティションはありません）
* **プライマリリードパーティション** - ランディングページにアクセスしたリードは、デフォルトでこのパーティションに追加されます
* **言語** - ワークスペースのビジネス言語

特定のワークスペースにAPI書き込みリードを使用する方法を示します。 最初のサンプルはXML リクエストで、2番目はXML レスポンスで、最後のサンプルはXML リクエストの生成に使用できるRuby コードサンプルです。 1. リードを作成した後、「リード分割」はリード情報のフィールドです。 `requestCampaign`に対するSOAP リクエスト

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

requestCampaignのSOAP Response

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

上記のシナリオを実行するサンプル Java プログラムを以下に示します。

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

**ワークスペースとリードパーティションにサインアップするにはどうすればよいですか？** Marketo Enterpriseをご利用のお客様は、ワークスペースとリードパーティションに無料でアクセスできます。 有効化と実装について詳しくは、顧客イネーブルメントマネージャーにお問い合わせください。 その他のお客様は、Marketoの営業担当者にお問い合わせいただくか、営業部門にメールでお問い合わせください。

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_1970-01-01_ by _Murta_

## 2014年6月リリースの更新

### Marketo Real-Time Personalization API

Marketo Real-Time Personalization（RTP）JavaScript APIは、プラットフォームの自動パーソナライゼーション機能を拡張します。 これにより、web ページのイベントトラッキングと動的なカスタマイズが可能です。 完全なドキュメント [こちら](/help/javascript-api/web-personalization.md)を参照してください。

投稿日：_2014-06-20_ by _Travis Kaufman_

## Marketoでの外部キーの保存

独自のCRMやデータウェアハウスなどのシステム間で取引先責任者とリードのレコードを同期する場合、リードレコードを一意のシステム IDに関連付けることが一般的な要件となります。 Marketoでは、一意のシステム IDを使用して[syncMultipleLeads API](/help/soap-api/syncmultipleleads.md)呼び出しを通じて、リードレコードを作成または更新できます。 これを実現するには、一意のシステム ID （プライマリキー）をMarketoの外部キーとして保存します。 外部キーを格納するMarketoのこのフィールドの名前は、foreignSysPersonIdです。 次の3つの重要な点に注意してください。

1. foreignSysPersonIdは、MarketoのUIには表示されません。 カスタム属性フィールドにこの値を入力するのもベストプラクティスです。
1. foreignSysPersonIdはリードに固有ですが、リードには複数のforeignSysPersonIdを指定できます。
1. foreignSysPersonIdは更新または削除できませんが、別のレコードに再割り当てできます。

Marketoの2つの既存のリードレコードにforeignSysPersonId値を書き込むために、[syncMultipleLeads API](/help/soap-api/syncmultipleleads.md)を呼び出す方法を説明します。**syncMultipleLeads API**&#x200B;を使用したforeignSysPersonIdの書き込み方法新しいリードレコードを挿入し、foreignSysPersonIdを指定できます。 また、Marketo IDとforeignSysPersonIdの両方を指定して、既存のリードに追加することもできます。 後のケースを順を追って説明します。**syncMultipleLeads SOAP API呼び出しにXMLを要求**

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

**syncMultipleLeads SOAP API呼び出し用の応答XML**

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

**上記のリクエスト XMLを出力するサンプル Ruby プログラムの下を参照してください。**

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

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-06-27_ by _Murta_

## リードのメールアドレスの更新

例えば、オーディエンスがMarketoフォームに入力したとします。 どのような処理が行われますか？ Marketoは利用者をCookieとし、利用者が提供したメールに関連付けます。 オーディエンスが次回web サイトにアクセスし、別の電子メールで同じフォームに再度入力した場合、どうすればよいでしょうか。 どうなりますか？ Marketoは新しいリードレコードを作成し、ユーザーのブラウザーで最初のCookieを上書きします。 ユーザーがMarketoの新規または別のリードになりました。 Marketoでリードのメールアドレスを更新する4つの方法をご紹介します。これには、[syncLead API メソッド ](/help/soap-api/synclead.md)、フォームメソッドのカスタムフィールド、Marketo UI、およびリストの読み込みがあります。**syncLead API**&#x200B;を介して、[syncLead API](/help/soap-api/synclead.md)を使用して、Marketo IDと新しい電子メールアドレスを使用してリードレコードを更新できます。 `syncMultipleLeads` SOAP API呼び出しにXMLをリクエスト

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

syncMultipleLeads SOAP API呼び出しの応答XML

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

上記のリクエスト XMLを出力するサンプル Ruby プログラムを以下に示します。

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

**フォームのカスタムフィールドを使用** Marketoで「新しいメールアドレス」のカスタムフィールドを作成できます。 次に、この新しいフィールドを含むフォームに入力するようにユーザーに依頼します。 次に、新しいカスタムフィールド「新しい電子メールアドレス」に変更があった場合に、トークン `{{lead.newEmailAddress}}`を使用してシステム電子メールアドレス フィールドのデータ値を変更するプログラムをMarketoで作成します。**Marketo UI** Marketo UIを使用して、リードの電子メールアドレスを手動で更新できます。 この方法について説明した[ ヘルプ記事](https://nation.marketo.com/)があります（記事を参照するにはMarketo ログインが必要です）。**リストの読み込み**&#x200B;を使用して、Marketoのリストの読み込み方法（[ここ](https://nation.marketo.com/)）を使用して、リードの電子メールアドレスを更新できます（記事を参照するにはMarketo ログインが必要）。  

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_1970-01-01_ by _Murta_

## リードの2番目のメールアドレスを保存する

例えば、APIを使用してMarketoのリードのスコアを変更するとします。 これは、リードエンドポイントの作成/更新を使用してREST APIで実行できます。 1つのリードレコードに複数の電子メールを保存する場合は、カスタムフィールドを作成し、2番目の電子メールをそこに保存する必要があります。 詳しくは、ヘルプ記事をご覧ください。以下は、この呼び出しの方法を示すRubyのコードサンプルです。

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

投稿日：_2015-02-20_ by _Murta_

## Marketoでカスタムフィールドを作成し、AP経由でこのフィールドを更新する

例えば、Adobe Marketoの標準フィールドに収まらないリードに関する追加データがあるとします。 たとえば、このカスタムフィールドはサードパーティスコアにすることができます。 サードパーティスコア用にMarketoでカスタムフィールドを作成し、Marketo [REST API](https://developer.adobe.com/marketo-apis/)または[SOAP API](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/activity-type-filters)のいずれかを使用して、このフィールドの値を更新できます。 最初にMarketoでカスタムフィールドを作成する方法を示し、2番目にREST APIを使用してこのフィールドを更新する方法を示します。

### Marketoでのカスタムフィールドの作成方法

1. 「管理」で、「フィールド管理」をクリックします。
1. 「新規カスタムフィールド」ボタンをクリックします。
1. 「タイプ」フィールドを選択します。 これにより、スマートリストおよびMarketoのFormsでのレンダリング方法が変わります。
1. Marketo に表示する名前を入力します。 フィールド名の変更は困難な場合があり、場合によっては不可能なため、名前とAPI名を慎重に選択してください。
1. 作成したカスタムフィールドに、APIを介してアクセスできるようになりました。

### REST APIでカスタムフィールドを更新する方法

前のセクションでは、データタイプ文字列を含む`myCustomField`というカスタムフィールドを作成しました。 このフィールドの値を更新するには、リードの作成/更新というREST API エンドポイントを使用します。 REST APIにリクエストを行う前に、認証する必要があります。 この記事の対象外ですが、詳細については、[Marketo開発者サイト ](/help/rest-api/authentication.md)を参照してください。

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

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-08-19_ by _Murta_

## UnbounceとMarketoの統合

**注：これはFab Capodicasaによるゲストブログ投稿です。 Marketo LaunchPointのB2C エージェンシーパートナーである[Hoosh Marketing](http://hooshmarketing.com.au/)で、Marketo認定コンサルタントを務めています。 SaaSとマーケティングの両方に13年間携わってきました。 バックグラウンドは、ハードコア IT、ダイレクトマーケティング、エンタープライズセールスの融合です。 Fabは元Marketo社員でもあります。**

**概要**この記事では、人気のランディングページツールであるUnbounceをMarketoと統合する方法について説明します。 最初に、Marketo トラッキングをバウンス解除に挿入する方法を示し、次に、バウンス解除フォームを変更してデータをMarketoに直接挿入する方法を示します。 Marketoにバウンス解除を統合する際の課題は、バウンス解除ではデフォルトのフィールドの名前を変更できないことです（例えば、first_nameをFirstNameに変更することはできません）。 また、フィールドラベルをフィールド名と異なることもできません。 この統合では、JavaScriptを使用して、既存のフォームを調整し、Marketoとの互換性を維持します。 この記事では、少なくともJavaScriptの初心者レベルとMarketoの中級レベルの知識を持っていることをお勧めします。
**パート 1: Marketo トラッキングコードをアンバウンスに追加** MarketoのMunchkin トラッキングスクリプトをアンバウンスのページに追加することは、Analyticsとフォームの統合の両方が機能するために必要です。 次の手順に従ってください。MarketoからMunchkin コードをコピーします。Admin -> Munchkinに移動し、JavaScriptの「シンプル」バージョンをコピーします。 バウンス解除ランディングページを開き、JavaScript/新しいJavaScriptを追加をクリックします。  「追加」をクリックし、スクリプト「Munchkin」を呼び出し、「Body End Tagの前」を選択して、Munchkin コードを貼り付けます。 「完了」ボタンをクリックします。 今後のバウンス解除ページでは、JavaScriptに移動し、作成したMunchkin スクリプトを有効にします。 再作成する必要はありません。
**パート 2: バウンス解除フォームをMarketo フォームに変換**&#x200B;次に、いくつかの新しい非表示フィールドとJavaScriptを追加してバウンス解除フォームを変更し、バウンス解除ランディングページがMarketoに直接情報を送信できるようにします。 まず、Marketoのプレースホルダーフォームを作成します。 Marketoで、空白のフォームを作成して承認します。

これは、バウンス解除フォームを表すMarketoのプロキシフォームです。 バウンス解除フォームに非表示フィールドを追加します。 これらの非表示フィールドは、このフォーム送信が適用されるフォームとユーザーセッションのMarketo インスタンスを判断するためにMarketoで必要です。 「バウンス解除」で、フォームをダブルクリックして開きます。 `_mkt_trk`という非表示フィールドを追加します。 `formid`という2つ目の非表示フィールドを追加します。  233は、MarketoのMarketo フォーム埋め込みコードにあるフォームのidに置き換える必要があります。 Marketoでフォームを開き、フォームアクション/埋め込みコードを選択します。 `returnurl`という非表示フィールドを追加します。`http://hooshmarketing.com.au/thank-you` これは、ユーザーがフォームの送信後にリダイレクトするURLです。 たとえば、お礼を述べるようなページを作成しましょう。
**パート 3: Marketoへの直帰解除フォーム** フォローアップ URLは、リードがMarketoに送信された後にリードがリダイレクトされるページです。 「バウンス解除」で、次の手順に従ってください。フォームをクリックします。 「フォームの確認」セクションを変更します。 「確認」を「フォームデータをURLに投稿」に変更します。 必要なフォローアップページのURLを設定します。`fpmarkets` Marketo アカウント文字列に置き換える必要があります。これは、Marketoの管理/ランディングページにあります。
**パート 4: JavaScriptをバウンス解除ページに追加**&#x200B;このJavaScriptは、フォームをMarketoと互換性のある形式に変換し、Marketoに送信します。 「バウンス解除」で、次の手順に従ってください。バウンス解除ランディングページを開き、JavaScript/新しいJavaScriptを追加をクリックします。 「追加」をクリックし、「Marketo フォーム変換」スクリプトを呼び出して、「Body End Tagの前」を選択します。 以下のJavaScript コードを貼り付けます。

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

バウンスと互換性のないAPI名を持つカスタムフィールドがある場合は、JavaScriptのマッピングにこれらを追加できます。 例えば、Marketoのカスタムフィールドの1つが`Comments_c`であるが、フィールドラベルをコメントとして表示したい場合、バウンス解除ではフィールド名を`Comments_c`に変更できません。

```
//default field mappings
UNBOUNCE_MARKETO_FIELD_MAP['comments'] = 'Comments_c';
UNBOUNCE_MARKETO_FIELD_MAP['first_name'] = 'FirstName';
UNBOUNCE_MARKETO_FIELD_MAP['email'] = 'Email';
```

_commentsは、バウンス解除のフィールド名です。_Comments_c_は、Marketoのフィールド名です。 今後のバウンス解除ページでは、JavaScriptに移動し、作成したMunchkin スクリプトを有効にするだけです。 再作成する必要はありません。
**パート 5: テスト**&#x200B;最後の手順は、このフォーム統合が機能しているかどうかをテストすることです。 Marketoでトリガーを作成し、Marketo フォームの入力を有効にして、リードがMarketoに正しく挿入されていることを確認します。 フォームが送信されたら、ページをフォローアップ URLにリダイレクトします。

投稿日：_2014-08-04_ by _

## 2014年7月リリースの更新

### Munchkin の更新

Munchkinの新しいバージョンは141です。 バージョン 142はサポートされておらず、2011年9月上旬に削除されます。 バージョン 142では、開発者のサイトで文書化されていない一般にアクセス可能な機能がありました。 これらの文書化されていない機能は、もはや公開されていません。 開発者のサイトで文書化された機能は、長期的にサポートされ続けます。

### RTPの更新

RTP APIには、「訪問者データを取得」という新しい関数があります。 このRTP API呼び出しを使用すると、組織、業界、場所、セグメントコード一致などのリアルタイムの訪問者データを取得できます。

投稿日：_2014-07-30_ by _Murta_

## 1つのページで複数のMunchkin トラッキングコードを使用する

例えば、複数のMarketo インスタンスがあり、ページへの訪問や複数のインスタンスへのクリックリンクなどのweb トラッキングイベントを送信する場合、Munchkinでこれを行うことができます。 Marketoは、web サイトへの訪問者をドメイン別に追跡します（例：「marketo.com」）。 このMunchkin スクリプトをプライマリドメインとは異なるドメイン（例えば「company.com」）でホストしている場合、それらの訪問者は、その他のドメインでフォームに入力するまで匿名リードとして表示されます。 これを実現するには、`Munchkin.init`呼び出しに`altIds` パラメーターを追加します。 altIds パラメーターには、web イベントを送信するMunchkin IDの配列が含まれます。 以下の例を使用して、強調表示されたMunchkin ID （XXX-XXX-XXX、YYY-YYY-YYY、ZZZ-ZZZ-ZZZ）を、トラッキング情報を送信する各Marketo インスタンスのMunchkin IDに置き換えます。

```javascript
<script src="http://munchkin.marketo.net/munchkin.js" type="text/javascript"></script>
<script>Munchkin.init('XXX-XXX-XXX', { altIds:['YYY-YYY-YYY', 'ZZZ-ZZZ-ZZZ'] });</script>
```

Munchkinの初期化パラメーターについて詳しくは、[このドキュメント ](/help/javascript-api/configuration.md)を参照してください。

投稿日：_2014-08-08_ by _Murta_

## MunchkinとGoogle Tag Manageの統合

Googleのタグマネージャーを使用すれば、web サイトにタグを追加できます。 Munchkinのような各トラッキングスクリプトをweb サイトのソースコードに手動で追加するのではなく、[Google Tag Manager](https://marketingplatform.google.com/about/tag-manager/)をサイトに配置し、Google Tag ManagerのUIを通じて[Munchkin](/help/javascript-api/lead-tracking.md)のようなタグを追加できます。 この記事では、最初にMarketoでMunchkin トラッキングコードを生成する方法を示し、次にこのMunchkin トラッキングコードをGoogle Tag Managerに追加する方法を示します。

### Munchkinのトラッキングコードの生成方法

1. アプリの右上にある「**管理者**」をクリックします。
1. 左側のツリーで「**Munchkin**」をクリックします。
1. トラッキングコードタイプは「**非同期**」を選択します。
1. JavaScript トラッキングコードをクリックしてコピーします。

**Google Tag ManagerにMunchkin トラッキングコードを追加する方法**

1. Google Tag Manager アカウントにログインし、**新しいタグを追加します。**
1. 新しい&#x200B;**カスタム HTML タグ**&#x200B;を作成します。
1. Munchkin コードをコピーして&#x200B;**HTML** フィールドに貼り付け、**続行**&#x200B;をクリックします。
1. **すべてのページに適用**&#x200B;を選択し、**タグを作成**&#x200B;をクリックします。 注：トラフィックが非常に多いWeb サイトの場合は、**一部のページで実行**&#x200B;を使用して、サイトのセクションを除外できます。
1. 「保存」をクリックし、Munchkin トラッキングコードがweb サイトに読み込まれていることを確認します。

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-08-05_ by _Murta_

## フォーム送信後にライトボックスを非表示にする

### 概要

Marketoによって生成された現在のライトボックス埋め込みコードは、フォームの送信時に消えません。 フォーム送信後にページがリロードされ、フォームが再度表示されます。 フォーム送信後に非表示になるライトボックスを作成する場合は、次の手順に従ってください。

### ガイド

1. Marketoでフォームを作成したら、埋め込みコードを生成します。 これを行うには、「フォームアクション」をクリックし、コードタイプとして「ライトボックス」をクリックします。 このコードをテキストエディターにコピー&amp;ペーストして、次の手順で編集できるようにします。
1. 埋め込みコードの「（form）」の後のすべてのコードを次のコードに置き換えます。

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

ステップ 2の後、完成したバージョンは以下のコードのようになります。 これで、コードをweb サイトで使用する準備が整いました。

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

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-08-21_ by _Murta_

## Marketo REST APIのクイックスタートガイド

このガイドでは、Marketo REST APIへの最初の呼び出しを10分で行う方法について説明します。 [Get Lead by Id](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) REST API エンドポイントを使用して、単一のリードを取得する方法について説明します。 これを行うには、認証プロセスを順を追って説明し、アクセストークンを生成します。アクセストークンを使用して、HTTP GET リクエストを[IDでリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)します。 そして、リード情報をJSON形式で返すリクエストを行うためのコードを提供します。

### 認証トークンの生成方法

>[!NOTE]
> 2025年6月をもって、認証トークンはサポートされなくなりました。 認証ヘッダーを使用する必要があります。
>

Marketoのカスタムサービスでは、アプリケーションがアクセスできるデータを記述および定義できます。 カスタムサービスを作成し、そのサービスを1人のAPI専用ユーザーに関連付けるには、Marketo管理者としてログインする必要があります。

1. Marketo アプリケーションの管理領域に移動します。
1. 左側のパネルの「ユーザーと役割」ノードをクリックします。
1. 新しい役割を作成します。 「Access API」をクリックして、役割の権限のリストを表示します。 次に、下にスクロールして、必要な権限のみを選択します。 この場合は、読み取り専用のリード権限を選択します。
1. 次の手順では、APIのみのユーザーを作成し、前の手順で作成したAPI ロールに関連付けます。 これは、ユーザー作成時に「API-Only ユーザー」チェックボックスをオンにすることで可能です。
1. カスタムサービスは、クライアントアプリケーションを一意に識別するために必要です。 カスタムアプリケーションを作成するには、管理者 / LaunchPoint画面に移動し、新しいサービスを作成します。
1. 表示名を指定し、「カスタム」サービスタイプを選択し、説明と手順1で作成したユーザーメールアドレスを指定します。 このカスタム REST API サービスの会社または目的を表す記述的な表示名を使用することをお勧めします。
1. グリッドの「詳細を表示」リンクをクリックして、クライアント IDとクライアントシークレットを取得します。 クライアントアプリケーションは、クライアント IDとクライアントシークレットを使用してアクセストークンを生成できます。
1. 認証トークンをテキストエディターにコピー&amp;ペーストします。 認証トークンは、次の例のようになります。

`cdf01657-110d-4155-99a7-f986b2ff13a0:int`

### エンドポイント URLの決定方法

Marketo APIにリクエストを行う場合は、エンドポイント URLにMarketo インスタンスを指定する必要があります。 Marketo REST APIに対するすべての非バルク API リクエストは、次のフォーマットに従います。

`<REST API Endpoint URL>/rest/`

REST API エンドポイント URLは、Marketo管理者 / Web サービスパネルにあります。 Marketo エンドポイントのURL構造は、次の例のようになります。

`https://100-AEK-913.mktorest.com/rest/v1/lead/{id}.json`

**注意：一括API URLの先頭に「/rest/」を付けることはできません。 Bulk APIの場合は、ホストのみを使用し、次のように適切なパスを追加する必要があります。**

`https://100-AEK-913.mktorest.com/bulk/v1/leads/export/create.json`

### 認証トークンを使用してGet Lead by Id APを呼び出す方法

前のセクションでは、認証トークンを生成し、エンドポイント URLを見つけました。 次に、[IDでリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)というREST API エンドポイントにリクエストを行います。 Marketo REST APIへのリクエストを行う最も簡単な方法は、URLをweb ブラウザーのアドレスバーに貼り付けることです。 以下の形式に従います。

`https://<REST API Endpoint URL for your Marketo instance>/rest/v1/<API that you are calling>?access_token=<access_token>`

### 例

`https://100-AEK-913.mktorest.com/rest/v1/lead/318581.json?access_token=cdf01657-110d-4155-99a7-f986b2ff13a0:int`

呼び出しが成功した場合は、次の形式のJSONが返されます。

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

Marketo REST APIについて詳しく知りたい場合は、[開始するのに適した場所です](https://developer.adobe.com/marketo-apis/)。

投稿日：_2015-09-04_ by _David_

## Marketo トラッキング Cookieを削除する方法

質問：「私たちは、営業部門がメールのメッセージから削除することを口頭で求めた個人を登録解除するためのフォームをweb サイトに設定しました。 しかし、私たちが発見しているのは、彼らがメールに入力し、そのメールアドレスでCookieを使用していることを送信し、当社のweb サイトでのアクティビティに関するアラートを受け取り始めたときです。 現在のフォームは埋め込みフォームです。 埋め込まれたフォームでクック追跡を無効にする方法を誰かが考え出しました、私はMarketoのランディングページでそれを行う方法を理解しています。」 成功を収めました。 これを実装するには、Cookieの有効期限を短縮します。 Cookieがフォームによって作成された後、直ちに期限切れにすることができます。 Cookieの有効期限が切れているため、ブラウザーはCookieを自動的に削除します。 このプロセスを開始するには、ネイティブフォーム機能を使用して、`deleteCookie`という関数の下で呼び出します。

投稿日：_2014-08-26_ by _Travis Kaufman_

## MarketoのランディングページをWordpressと統合する

例えば、web サイトがWordpressを利用して構築されており、そのページのひとつにMarketoのランディングページを埋め込みたい場合、 これはiframeを使えば可能です。 iframeでは、ページを別のページに埋め込むことができます。 この記事では、Marketo ランディングページをWordpress ページに埋め込む方法について説明します。**Wordpress プラグインを選択する** Wordpress次のような数があります。`http://wordpress.org/plugins/iframe/`このアプローチを使用する際のプロと長所を紹介します。`http://www.elixiter.com/marketo-landing-page-and-form-hosting-options/`素晴らしい投稿Murtza! Colbyを使用すると、フォームを送信した後にPDFにリダイレクトされる部分がiframeに保持されます。 私たちは長い間、私たちのサイトでiframeを使用しました。 素晴らしいポスト Murtza! Colbyを使用すると、フォームを送信した後にPDFにリダイレクトされる部分がiframeに保持されます。 私たちは長い間、私たちのサイトでiframeを使用しました。 注意して、メイン URLからiframeにURL パラメーターを渡す場合は、コーディングを行う必要があります。 また、Google Analyticsが適切に設定されていることを確認してください。 iframeを使用してページにアクセスするたびにページビューが2回カウントされるような事態は避けたいものです。

投稿日：_1970-01-01_ by _Murta_

## Marketoランディングページとの最適な連携

[Optimizer](https://www.optimizely.com/)を使用すると、サイトでA/B テスト、マルチページ テスト、多変量テストを実行できます。 MarketoのランディングページでOptimizerを使用できます。 その方法は次のとおりです。

1. Optimizely コードスニペットを見つけてコピーします。** Optimizelyのダッシュボードに移動し、「プロジェクトコード」リンクをクリックします。 ポップアップに表示されるコード行をコピーします。
1. Marketoにログインし、ランディングページテンプレートを選択します。 次に、「ドラフトを編集」をクリックします**
1. 「ランディングページのアクション」をクリックします。 次に、「ページのMeta タグを編集」をクリックし**
1. カスタム HEAD HTML セクションにOptimizely コードスニペットを貼り付け、「保存」をクリックします。
1. ランディングページをテストして、Optimizer スニペットが機能していることを確認します

投稿日：_2014-09-18_ by _Murta_

## Marketo REST APIを使用したフルネームによる検索

**質問：** Marketo APIを使用して、リードのフルネームだけを使用してリードを照会する方法はありますか？
**回答：**&#x200B;直接使用することはできません。 ただし、以下で説明する回避策では、これを行うことができます。

1. Marketoで「Fullname」というカスタムフィールドを作成します。
1. [getMultipleLeads](/help/soap-api/getmultipleleads.md) SOAP APIまたは[ フィルタータイプで複数のリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)のいずれかを使用して、リードデータベースをクエリします。 RESTまたはSOAP APIへのリクエストに、名前と姓を属性として含めます。
1. リードデータベースをクエリした後、各リードの「名」と「姓」を連結し、このデータを「フルネーム」列に格納します。 1. [syncMultipleLeads](/help/soap-api/syncmultipleleads.md) SOAP APIを使用して、このデータを「Fullname」カスタムフィールドにプッシュします。 または、[ リードの読み込み](/help/rest-api/leads.md) APIを使用するか、Marketo UIを使用してCSVまたはXLSを読み込むこともできます。
1. これで、[ フィルタータイプ API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)による複数のリードの取得を使用して、フルネームでクエリを実行し、このカスタムフィールドを検索できるようになりました。 「Fullname」を「filterType」として指定し、「filterValue」は「Get Multiple Leads by Filter Type REST API呼び出しを使用して「Joe Johnson」になります。

投稿日：_2014-09-09_ by _Murta_

## Marketo Tracking Cookieの削除

この方法は、目的の効果がCookieを完全に削除する場合にのみ使用する必要があります。

このコードサンプルは、Marketo フォーム送信後にユーザーのブラウザーからMarketo トラッキング Cookieを削除するために使用できます。 ユーザーがフォームを送信した後に`deleteMarketoCookie` メソッドを呼び出すことで機能します。 この方法は、有効期限を過去の日付に設定することで、Cookieを期限切れにします。 ブラウザーのデフォルトの動作は、このCookieが期限切れになっているため、削除します。

投稿日：_2014-09-09_ by _Murta_

## フォームへの入力時に無料メールドメインを制限する

例えば、サイト訪問者がGmailやYahooなどの無料のメールドメインを使用してフォームを送信することを制限したいとします。 これを実現するには、Marketo フォームを使用して、以下のスクリプトをページのソースコードに含めます。 利用者が業務外の電子メール（Gmail、Hotmailなど）を入力したかどうかを確認し、入力した場合にMarketoフォームが送信されないようにします。 9行目を変更して、制限するドメインを含めることで、ブロックされたメールドメインのリストを拡張できます。

投稿日：_2014-09-09_ by _Murta_

## API経由でアクセスできないフィールドのデバッグ

このフィールド <https://nation.marketo.com/>にアクセスすると、SOAP APIを使用してフィールド AnnualRevenueを更新しようとすると、レコードが更新されますが、AnnualRevenue フィールドは変更を保持しません。 リードデータベースを使用してフィールドを手動で更新しようとすると、このフィールドへの変更も保持されません。 管理画面でフィールドがブロックされているかどうかを確認します。 他にも、SFDCから同期されたアカウントフィールドが原因で発生することがあります。 SFDCは多くの場合、それらのフィールドの記録システムであるため、デフォルトでフィールドの変更をブロックします。 1）作成日：2）SFDCID 3）Marketo固有コード 4）SFDCタイプ 5）更新日：6）緊急度7）優先度8）売上作成日

投稿日：_1970-01-01_ by _Murta_

## Marketo ランディングページへのカスタムコードの追加

例えば、Google AnalyticsなどのサードパーティのトラッキングスクリプトをMarketo ランディングページに追加するとします。 これは、MarketoのUIから可能です。 一般的には、次の手順に従って、任意のカスタムコード（HTML、CSS、JavaScript）をMarketo ランディングに追加できます。

1. ランディングページを選択して、「ドラフトを編集」をクリックします。
1. HTML要素をドラッグします。
1. カスタムコードを入力し、「保存」をクリックします。

投稿日：_2014-09-10_ by _Murta_

## サーバーサイドフォーム投稿

`https://community.marketo.com/MarketoResource?id=kA650000000GsXXCA0`

投稿日：_2014-09-11_ by _Murta_

## Forms 2.0の送信からのMarketo トラッキング Cookieの消去

### 概要

Forms 1.0には、Munchkin トラッキング Cookieの値がDOMのフィールドとして含まれていました。 これは他のすべての入力と一緒に送信されました。[Forms 2.0](/help/javascript-api/forms-api-reference.md)はこのフィールドを省略し、フォームの読み込み時ではなく送信時に値を動的に入力します。 これは一般的に許容されますが、ユースケースのクラスを作成します。このクラスでは、意図しないトラッキングと事前入力を避けるために、トラッキング Cookieをクリアする必要があります。 例えば、Marketoのお客様が同じデバイスで同じフォームを使用し、複数の人から連絡先情報を取得するトレードショーで発生する可能性があります。 以下のスニペットを使用すると、ユーザーのブラウザーからcookie自体を削除することなく、フォームの送信時にcookie値をクリアできます。

### コードサンプル

このスニペットでは、ページにフォームが1回読み込まれることを想定しています。 複数のフォームがある場合は、[loadForm メソッドまたはgetForm メソッド ](/help/javascript-api/forms-api-reference.md)を使用してコールバックを実装する必要があります。

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

投稿日：_2014-09-11_ by _Kenny_

## 2014年9月リリースの更新

### REST APIの更新

リードレコードに関連付けられたMunchkin Cookie値を返す[複数のリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) APIに新しいオプションフィールド値を追加しました。 リクエストに「?fields=cookies」を追加するだけです。

投稿日：_2014-09-16_ by _Murta_

## RTP APIからMarketo フォームへの位置情報の入力

**このブログ記事に記載されているユースケースを実装するには、アクティブなRTPおよびMLM サブスクリプションが必要です。**
[RTP JavaScript API](/help/javascript-api/web-personalization.md)と[Marketo Forms 2.0](/help/javascript-api/forms-api-reference.md)を使用すると、RTPから推測された場所データを取得し、フォーム入力を介してMarketoにプッシュできます。 これにより、最新のフォームアクティビティ中にユーザーが推測した場所（IP アドレスに基づく）を確認できます。 初めに、Marketoで3つのカスタム文字列フィールドを作成する必要があります。 これは、CRMでMarketoとネイティブに統合されている場合や、Marketoの管理セクションのフィールド管理メニューから実行できます。 これらのフィールドには、「最新の国」、「最新の状態」、「最新の都市」という名前を付けることをお勧めします。 この命名規則を使用してこのブログを続けます。 これらのフィールドのAPI名は、「mostRecentCountry」、「mostRecentState」、「mostRecentCity」です。 場所データを取得するには、[RTP メソッドを使用して訪問者の場所データ ](/help/javascript-api/web-personalization.md)を取得し、Marketo Forms 2.0から[addHiddenFields メソッドとvals メソッド ](/help/javascript-api/forms-api-reference.md)を使用してフォームに渡します。 ページで、RTP JS タグとMarketo フォームを追加します。 次に、以下のスクリプトを含めます。 上記とは異なる命名規則を使用している場合は、サンプルコードのターゲットフォームフィールドの名前を変更する必要があります。

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

投稿日：_2014-09-17_ by _Kenny_

## Marketo ランディングページのクロールとインデックス作成をブロック

例えば、Marketoのランディングページが、Googleなどの検索エンジンによってクロールされ、結果に表示されないようにしたいとします。 その方法は次のとおりです。

1. Marketoにログインし、ランディングページを選択します。 次に、「ドラフトを編集」をクリックします。
1. 「ランディングページのアクション」をクリックします。 次に、「ページのMeta タグを編集」をクリックします
1. 「Robots」フィールドを「No Index, No Follow」に変更します。 「Save」をクリックします。

投稿日：_2014-09-19_ by _Murta_

## Marketo RESTとSOAP APIの比較に関するFAQ

**更新日：2016年3月** Marketo [REST](/help/rest-api/rest-api.md)および[SOAP](/help/soap-api/soap-api.md) APIに関するよくある質問に対する回答を次に示します。**質問：Marketo REST APIとSOAP APIの主な違いは何ですか？** 回答：REST APIとSOAP APIを介して特定のデータをプッシュ/プルする機能はほとんど重複しますが、REST APIまたはSOAP APIにのみ存在する特定の機能があります。 パフォーマンスに関しては、REST APIはSOAP APIよりも[ スループット ](https://en.wikipedia.org/wiki/Throughput)が優れています。 認証モデルに関しては、REST APIには、期限切れのトークンを使用する認証モデルがあります。 REST APIでは、Marketo [assets](https://developer.adobe.com/marketo-apis/api/asset/)にもアクセスできます。   **Q: SOAP APIでは使用できないREST APIで使用できる機能は何ですか？** A: [ リスト API](/help/rest-api/list-of-standard-fields.md)、[ リスト API](/help/rest-api/lead-database.md)からリードを削除、[使用状況API](/help/rest-api/rest-api.md)、[ エラーAPI](/help/rest-api/rest-api.md)は、REST APIでのみ使用できます。**質問：SOAP APIで利用できるAPIの数を増やす計画はありますか？** A：いいえ。**質問：REST APIで利用できるAPIの数を増やす計画はありますか？** A：はい。 現時点では、RESTはMarketoのAPI開発の主要な焦点となっています。

投稿日：_2014-09-20_ by _Murta_

## サーバーサイドフォーム投稿

**注：これは非公開でサポートされていないAPIであり、サポートされていないため、いつでも動作が変わる可能性があります** web サイトで独自のフォームを使用している場合でも、サーバーサイドの投稿を使用してMarketoにこのデータを送信できます。 このアプローチの利点は、既存のフォームとアプリケーションロジックを維持できるのに対して、実際のフォーム投稿をMarketoに使用できることです。 これにより、Marketo ユーザーは「フォームへの入力」イベントを行うことができ、自動プロセスのトリガーやセグメント化に使用できます。**メモ：1つの単一のIP アドレスから1分あたり30件のサーバーサイド フォーム投稿のレート制限があります。** 各スクリプト言語またはプログラミング言語には、サーバーサイドのフォーム送信を行うための異なるオプションがあり、Post Callを作成するために使用できる異なるオブジェクトまたはメソッドがある場合があります。 例えば、PHPでは、多くの人がcURL ライブラリを使用しています。 いずれの場合も、指定したURLに名前と値のペアを投稿します。 名前は、Marketo フィールドのAPI名と同じである必要があります。 さらに、フォーム送信を正しく取得するために含める必要があるシステムフィールドがいくつかあります。

1. フォームを作成します。 最初の手順は、Marketoでフォームを作成するか、送信する既存のフォームを使用することです。 フォームの名前は説明的である必要がありますが、実際にはフォームフィールドは必要ありません。 新しいフォームを作成する場合は、名前を入力するだけで、「フォームエディターを開く」ボックスのチェックを外せば完了です。
1. フォーム IDを検索します。 Marketo UIで、フォームを選択し、URLを確認します。URLは`https://app-x.marketo.com/#FO8B2ZN12`形式にする必要があります。 「#」記号の後ろで、「FO」の直後にある番号を見て、フォーム IDを見つけます。 この場合、フォーム IDは8です。 場合によっては、最初のフォームに1001という番号が付けられ、そこからカウントアップされることがあります。 フォーム IDは変数であるため、異なるフォームの送信をトリガーできます。
1. Marketo アカウント IDを取得します。 管理者/ Munchkinに移動し、000-AAA-000のフォーマットを持つMunchkin Account IDをコピーします。フォームが正しいMarketo インスタンスに送信されるようにするには、これを必要とします。
1. POST URLを決定します。 Marketo ユーザーインターフェイスの場合、ロケーションバーに通常は`<http://app-x.marketo.com/>`という形式のドメインを書き留めます。 スラッシュの後に何かを破棄し、「index.php/leadCapture/save」を追加して完全なフォーム POST URLを取得します。 注1：大文字と小文字が区別されます。 注意2: Marketo サンドボックスは、実稼動Marketo システムとは異なるドメインを持っている場合があります。 例えば、URLは次のようになります。`http://app-x.marketo.com/index.php/leadCapture/save` HTTPの代わりにHTTPSを使用することもできます（セキュリティ例外が発生するため、CNAMEは使用しないでください）。
1. フォームフィールド名を見つける**管理者/フィールド管理に移動し、「フィールド名を書き出し」ボタンをクリックして、API フィールド名を含むスプレッドシートをダウンロードします。 API名を名前と値のペアの名前として使用します。
1. 投稿するフィールドを決める。 フォーム送信には、任意のMarketo リードフィールドを含めることができます。 フィールド名では大文字と小文字が区別されます。 送信するフィールドに加えて、2つの必須フィールドと2つの推奨フィールドがあります。フォームの必須フィールド：（1） `munchkinId` – このフィールドはMunchkin アカウント IDに使用されます（2） `formid` – このフィールドは、Marketoのどのフォームが送信されたかを示します。 MarketoがMarketo データベース内で一致するメールアドレスを見つけた場合、既存のレコードを更新し、そうでない場合は新しいレコードを作成します。 複数の一致がある場合は、最新に更新されたレコード （2） `_mkt_trk`を更新します。このフィールドにはCookie情報が含まれているため、個人のweb ページ訪問を追跡できます。 フォームページにMunchkinがある場合、Munchkinはこの非表示フォームフィールドに値を自動的に入力します。 そうでない場合は、同じ名前のCookieから読み取り、このフィールドでMarketoに渡します。 注：Marketo フォームへのPOSTの本文は、URL エンコードする必要があります。
1. 応答を参照してください** フォームの投稿に対する応答は、HTTP 302 リダイレクトコードになります。 一部のシステムでは、これはエラーとして表示されます。 ただし、この場合は、リードが正常に作成または更新されたことを意味します。 エラーが発生した場合は、4xxまたは5xxのエラーコードが表示されます。

購読解除シナリオにこの手法を使用する方法について[投稿](https://nation.marketo.com:443/t5/product-blogs/how-to-build-an-external-subscription-center/ba-p/242185)を次に示します[by Justin Cooperman, Sr. Product Manager]

投稿日：_2014-11-07_ by _Murta_

## 特定の日付範囲で更新されたリードを検索

例えば、[Marketo API](/help/soap-api/soap-api.md)を介して、特定の日付に更新されたリードを見つけたいとします。 これは、[getMultipleLeads SOAP API](/help/soap-api/getmultipleleads.md)で可能です。 このメソッドは、リクエストした日付範囲について、Marketoでデータ値が変更されたリードまたは新しいアクティビティを返します。 `leadSelector`には、`LastUpdateAtSelector`を指定します。 次に、日付範囲を`oldestUpdatedAt`と`latestUpdatedAt`の時間境界で定義します。 2014年6月6日の午前12時PSTから2011年6月7日の午前12時PSTの間に更新されたリードを見つける方法を示す、以下のサンプルのリクエスト XMLを参照してください。 注意：日付範囲は30日を超えることはできません。

**日付ごとに更新されたリードを検索するためのXMLのサンプル**

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

投稿日：_2014-09-24_ by _Murta_

## メールへの動的コンテンツの追加

例えば、毎日の電子メールを配信し、その日の日付を自動的にメールテンプレートに含めたいとします。 これには、Marketoでトークンとメールスクリプトを使用します。

1. トークンを作成します。** トークンを使用するプログラムに移動します。 「My Tokens」をクリックします。
1. メールスクリプトをダブルクリックします。 このトークンに名前を付けます。 「Edit」をクリックします。
1. 以下のメールスクリプトをこのウィンドウに貼り付けます。 「Save」をクリックします。

## Velocityのカレンダーオブジェクトにアクセスする

`set($x = $date.calendar)`

## 日付を書式設定

`set($current_date = $date.format('dd-MM-yyyy', $x.getTime()))`

## 今日の日付を返します

`$current_date`

1. メールテンプレートでトークンを参照します** トークンの名前をメモします。 メールのドラフトに移動します。 トークンを含めます。  メールが送信されると、トークンの値が入力されます。 詳しくは、[ メールスクリプティング開発者ドキュメント ](https://experienceleague.adobe.com/ja/docs/marketo-developer/marketo/email-scripting)を参照してください。

投稿日：_2014-11-22_ by _Murta_

## Bash セキュリティアドバイザリー

Marketoは、[Shellshock （CVE-2014-6271） ](https://nvd.nist.gov/view/vuln/detail?vulnId=CVE-2014-6271)としても知られるBashの脆弱性を徹底的に調査し、これらの攻撃の影響を受けないと結論付けました。 また、[CERTの推奨事項](https://www.cisa.gov/news-events/alerts/2014/09/25/gnu-bourne-again-shell-bash-shellshock-vulnerability-cve-2014-6271)に準拠するように、ソフトウェアを最新バージョンに更新することで、予防措置を講じています。

投稿日：_2014-09-26_ by _Murta_

## SOAP API資格情報の更新方法

[SOAP API](/help/soap-api/soap-api.md)資格情報を定期的に更新することをお勧めします。 現在、Marketo APIを使用してプログラムでこれを行う方法はありません。 次の手順では、Marketo UIを使用してSOAP API資格情報を更新する方法を示します。

1. 「Admin」セクションに移動し、「Web Services」をクリックします。
1. 10文字以上の暗号化キーを設定し、「変更を保存」をクリックします。

投稿日：_2014-09-29_ by _Murta_

## Marketo データベースのクリーンアップ方法

**注：これはゲスト ブログ投稿です。 Josh Hillは、マーケティングオートメーションエージェンシーであるPerkutoのMarketoプラクティスリードです。 Josh氏は、マーケティング、セールス、テクノロジーを一元管理し、売上ジェネレーションシステムを構築しています。 [MarketingRockstarGuides.com](https://www.marketingrockstarguides.com/).**&#x200B;で、マーケティングオートメーションと需要創出について執筆しています Marketoのデータベースをクリーンに保つことは、この強力なシステムを管理する上で重要です。 Marketo データが汚れていたり、CRM データが汚れていたりすると、キャンペーンが間違ったユーザーに送信された理由やレポートが「方向性を示す」理由を説明すると、マーケティングマネージャーとしての業務が非常に困難になります。[2011年のGartnerの調査によると](https://www.data.com/export/sites/data/common/assets/pdf/DS_Gartner.pdf)、データ品質が低いと、労働生産性が20%低下します。 これは、データを修正する必要があったため、時間（週に8時間または週に1日）の20%を浪費します。 しかし、この損失は、ターゲティングが間違っていたために失われた売上に比べて痛いものです。 データをクリーンに保つために投資する理由のトップ 5は次のとおりです。- リードとクライアントのより優れたセグメンテーションを行うことで、適切なタイミングで適切な人にメッセージを集中させることができます。 20% オフのクーポンは、新規見込み客のみに適用し、優良顧客には適用されません？ - メールの重複した送信を避けます。 ただし、同じリードに対して複数の電子メールを配信することは、慎重に検討する必要があります。通常は、重複するレコードが統合されていないためです。  – あなたの上司への正確なレポート。 CMOは収益テーブルに座っているので、正確で一貫性のある再現可能なレポートを作成する必要があります。さもなければ、もはや収益マーケターにはなれません。  – 販売交渉中に主要な見込み顧客に間違ったマーケティング資料を電子メールで送信すると、保留中の取引を傷つける。

データベースがライフサイクル段階でその詳細を提供していない場合、1～2件程度の商談に達する可能性があります。  – 悪いリードや古いリードを削除して、価格のしきい値を下回らないようにします。 悪いデータのコストについて多くのことが書かれています。 最も差し迫った懸念事項は、不良、重複、古いリードが多すぎると、MarketoやSalesforceの価格帯を超えてしまい、年間数千もの手数料が発生する可能性があることです。 では、どのようにデータベースをクリーンに保つのでしょうか？ データクレンジングの原則に従うこともできますが、Marketoの内部ではどうすればよいでしょうか？ お使いのシステムについて、いくつかの仮定を行います。 – 標準のMarketo システムがあります。  – 典型的なリード連絡先アカウント Salesforceの設定があります。 - システム間ですべてのレコードを同期している。  – 目的の重複を使用していない。

修正する適切なリードを見つける**最初に潜在的な問題であるリードを見つけましょう。 各クライアントでは、一連のスマートリストを使用して、データベースの健全性を判断します。 同じことを月単位で行うことをお勧めします。 スマートリストが機能するようになれば、1 ヶ月に15分以内で完了します。 これは、マーケティング部門とAdobe MarketoのROIを実証する優れた方法です。 データベースに対する全体的な影響を把握するためのテーブルを作成します。 以下の例には、私が探している基準が含まれているので、ビジネスにとって重要な他のフィールドも必ず含めてください。 Marketoのみ、SFDCリード、SFDC連絡先ごとにグループを分類します。

データ値の修正にAutomationを使用する：Automation ルールを使用して、一般的なスペルの間違いやデータの欠落を修正することは、数十年前に遡ります。 1960年代には、ダイレクトメールを送信する際のデータ品質が低いと、数千ドルものデータが無駄になる可能性がありました。 今日では、データ品質のミスは、見当違いの電子メールよりも早く評判を台無しにしています。 電子メールの評判、言葉の選択、顧客体験は重要です。ミスが数分で大きく取り上げられることがあるので、その重要性は高まります。 自動データクレンジングで企業の評判を守る。 これらのデータ管理フローは、Marketoで最初に設定したことのひとつです。 ほとんどの企業は同様のフローを設定しています： – 国別修正者（ただし、この方法を必要としないために原則1に従う必要があります） – 国別修正者またはマッパー – 国と推測状態がある場合によく役立ちます。  – 従業員の数から従業員範囲まで。 - Bad Lead Source to Good Lead Source - Email Invalid to Email is Good if the Email changed.  – 古いフィールドの値を新しいフィールドに変換します（Full to Empty）。 たとえば、このフローでは、従業員番号に基づいて従業員範囲を調整します。

データ追加ツール データベースをより適切にセグメンテーションするには、空のフィールドにデータを入力することが重要です。 リードは、フォームに適切な業種、機能、タイトルを入力しているとは限りません。 古いシステムのレガシーデータがある場合もあります。 このようなデータの欠如により、より少ない人員で電子メールを送信しなければならなくなったり、間違った人員で送信する可能性が生じます。 これを修正するには、データ追加ツールが必要です。

方法1：自分で入力する データを補間して空のフィールドをバックフィルできる場合があります。 例えば、業界名や「年間収益と年間収益の範囲」の代わりにSIC コードを使用している場合です。 Marketoでは、これらの修正を簡単に自動化できます。

オプション 2: LaunchPointを介したデータ追加/強化ベンダーの検索Launchpoint](https://exchange.adobe.com/apps/browse/ec?product=MRKTO)には、リードデータの強化に役立つNetProspexやReachForceなどの[いくつかのベンダーがあります。 データシートの入力を求める人もいれば、クリーニングをおこない、送り返します。 MarketoやSalesforceでは、フィールドを自動的に検証して、必要なデータを入力し直します。 ほとんどのベンダーは、[Marketo APIまたはWebhook](/help/home.md)を使用して、これを実現します。

オプション 3: Marketo APIを使用してリードを更新するMarketo APIを使用して、クレンジングが必要なリードを特定し、API経由で更新できます。 フィルターの種類REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)による[複数のリードの取得は、特定の条件に一致するデータをMarketoから取得するための優れた出発点です。 リードを更新するには、[ リードの作成/更新REST API](/help/rest-api/leads.md)を参照してください。

または、[Marketo Webhook](/help/webhooks/webhooks.md)を設定して、フォームへの入力など、特定のイベントが発生したことを外部システムに通知することもできます。 その後、値で応答して、リードを更新できます。

自動化すべきことは何か？ 手順1でいくつか提案しました。 しかし、データベースをより多くクリーンアップしたい場合は、データ値の固定を超える必要があります。  – 競合他社ブラックリスト：競合他社の収集とブラックリストへの登録を自動化していることを確認してください。 競合他社パートナーがいる場合は、それを適切にマークし、リストに配置して抑制することをお勧めします。   – 複数のハードバウンス：間違いなくこのフローを自動化します。 リードが30日間に2回以上ハードバウンスした場合は、「休止」または「無効」に設定します。 そして、月に1回はタイプミスやその他の問題がないか確認します。  - 30日間の複数のソフトバウンス：30日間はmarketing suspended=TRUEに設定します。  - スパムトラップの停止/削除：製品がスパムトラップの可能性のあるアドレスを使用することを意味する場合は注意してください。 スパムトラップのリストを確認。 スマートリスト：

**自動化すべきではないこと**&#x200B;間違ったレコードを誤って大量に削除するとリスクが高すぎるため、リードの削除を自動化しないでください。 月に1回、ごみ箱としてマークされたリードを確認してください。 しかし、ゴミ箱に入ったリードを削除したい場合は、30日間待ってからフローを実行します。

注意事項：自動化を利用することは、時間を節約し、データベースをクリーンに保つための優れた方法です。 自動化は諸刃の剣である。なぜなら、設定を間違えると数分で大混乱に陥るかもしれないからだ。 これらのプロセスを進める際には、注意を払い、全員に情報を提供します。 通常、SFDCの連絡先は、アクティブな商談、クライアント、または元クライアントである可能性が高いため、削除することをお勧めします。 財務または法務により、特定のレコードを保持し、連絡先がそのレコードに添付されていることを要求される場合があります。 ハードバウンス、無効、またはもはや存在しない連絡先に焦点を当てます。 ここでは、Marketo データベースをクリーンに保つためのテクニックをいくつか紹介します。 APIまたはWebhookを使用してこれらのプロセスを自動化する他の方法を考え出したかどうかお知らせください。

投稿日：_2014-10-08_ by _Josh_

## 2014年10月リリースの更新

### 外部ページの事前入力

Marketo formsは、Marketo ランディングページの外部に読み込まれた場合、ネイティブの事前入力機能を提供しません。 ただし、[Marketo API](/help/rest-api/rest-api.md)と[Forms 2.0 JavaScript API](/help/javascript-api/forms-api-reference.md/)を使用して、引き続きこれを実装できます。 最初の手順は、サーバーからREST呼び出しを介してMarketoからリードデータを取得することです。 リード IDまたはサーバーからの別の一意のIDを相互参照する方法がすぐに見つからないことを前提として、[ フィルターの種類でリードを取得メソッド ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)を使用して、Munchkin Cookie &#39;_mkto_trk&#39;を使用してMarketo サーバーからデータを取得する必要があります。
この呼び出しを行うには、インスタンスの認証エンドポイントとREST エンドポイントが必要です。 Marketo インスタンスで認証が完了したら、`https://<host>/rest/v1/leads.json`でリード APIを呼び出す必要があります。 次に、この`?filterType=cookie&filterValues=`のようにMarketo Cookieをフィルタリングするためのクエリ文字列を作成する必要があります。 クライアントによってサーバーに送信された&#39;_mkto_trk&#39; キーから特定の値を取得する必要があります。 メモ：_mkto_trk cookieの値にはアンパサンドが含まれており、Marketo エンドポイントで正しく受け入れるには、`%26`にエンコードされたURLが必要です。 デフォルトでは、リード APIは`id`、`email`、`firstName`、`updatedAt`の4つのフィールドを返します。 特定のフィールドセットを設定するには、`fields` クエリパラメーターを含める必要があります。フィールド名は次のようにコンマで区切ります。`&fields=email,firstName,lastName,company`。 最終的なコールは次のようになります。

`https://<host>/rest/v1/leads.json?filterType=cookie&filterValues=<cookie>&fields=email,firstName,lastName,company&access_token=<token>`

この呼び出しを行うと、次のようなJSON オブジェクトが返されます。

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

リードの詳細ができたので、JavaScriptのwhenReadyおよびvals メソッドを使用して、これらをMarketoフォームにマッピングします。 まず、リードの結果をページ上の変数として設定する必要があります。

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

これで、ページに結果が表示されたので、フォームフィールドにマッピングできます。

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

投稿日：_2014-10-24_ by _Kenny_

## メール HTML の置換

この記事では、メール用にMarketoによって生成されたHTMLを削除する方法について説明します。 その後、Marketoの再フォーマットなしで独自のHTMLを使用できます。

1. メールに移動し、「ドラフトを編集」をクリックします。
1. 「メールアクション」をクリックし、「HTML ツール」をクリックしてから、「HTMLを置き換え」をクリックします。
1. このボックス内のコードをHTMLに置き換えます。 次に、「保存」をクリックします。

投稿日：_2014-10-28_ by _Murta_

## 訪問者のCookie IDを取得し、関連するリードデータをクエリする

フィルターの種類](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)REST エンドポイントで[複数のリードを取得する」を使用すると、ユーザーのCookie IDに基づいてリードデータをクエリできます。 例えば、Marketo以外のランディングページでフォームを事前入力する場合に、この方法を使用できます。 この記事では、web ページ訪問中にユーザーのCookie値を取得し、そのCookie IDを使用して[複数のリード REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)を取得し、ユーザーのリードデータを返す方法について説明します。 まず、ユーザーのMunchkin cookieの値&#39;_mkto_trk&#39;が必要です。 Cookie値の取得に使用できるJavaScript関数の例を次に示します。 このアプローチについて詳しくは、[このStackOverflow ページ ](https://stackoverflow.com/questions/10730362/get-cookie-by-name)を参照してください。 この関数を呼び出す前に、ページ読み込みイベントの後に500 ミリ秒の遅延を設定することをお勧めします。 これにより、Munchkinの読み込み時間が確保され、ユーザーはCookieを使用します。

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

次に、「_mkto_trk」 Cookieの値をサーバーに渡します。 サーバーからリードデータを取得するには、このCookie値を使用して[Get Multiple Leads REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)を呼び出します。 インスタンスには認証エンドポイントとREST エンドポイントが必要です。 呼び出しは、次のように構造化する必要があります。

メモ：`_mkto_trk` cookie値にはアンパサンドが含まれており、Marketo エンドポイントで正しく受け入れるには、`%26`にエンコードされたURLが必要です。

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

上記の例では、ユーザーに関連付けられたすべてのCookieと電子メールが返されます。 それらのデータを使用して、その後にユーザーがアクセスするページをパーソナライズできます。

`{"requestId":"aa00#14a405aa786","result":[{"id":583,"email":"<testaccount@gmail.com>","cookies":"_mch-marketo.com-1418418733122-51548"}],"success":true}`

投稿日：_2014-10-30_ by _Murta_

## マーケティングオートメーションに携わる開発者が必要なケース

注：これはゲストブログの投稿です。 Josh Hillは、マーケティングオートメーションエージェンシーであるPerkutoのMarketoプラクティスリードです。 Josh氏は、マーケティング、セールス、テクノロジーを一元管理し、売上ジェネレーションシステムを構築しています。 [MarketingRockstarGuides.com](https://www.marketingrockstarguides.com/)で、マーケティングオートメーションと需要創出について執筆しています。

MA プラットフォームは、経験豊富なオペレーターの手に委ねることで、すぐに使える非常に強力な機能を備えています。 プラットフォームは、定義により、拡張機能アプリケーションを使用して、システムをチームにとってさらに素晴らしいことにすることができます。 Marketoのロジックエンジンは非常に多くの機能を備えていると思われるかもしれませんが（実際にそうです）、限界があります。 Marketoはあなたのために全てをすることはできないし、そうするべきでもありません。

Marketoが構築できるよりも、自社の機能を発揮するツールは、他にもあります。 Marketo プラットフォームは非常にオープンで、[LaunchPoint エコシステムのアプリケーション ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO)を利用できます。 また、このオープン性を利用して、ビジネスニーズに合わせてサイトとMarketoの機能を拡張することもできます。 Marketoのようなプラットフォームの大きな利点は、一般的なマーケターが、本格的なプログラマーでなくても、ページ、メール、ルーティングロジックを構築できることです。
最近のマーケターはロジックを理解する必要がありますが、実際のプログラミングは専門家に任せるのが最善です。 では、開発者を呼び出す必要がある場合は、どうすればわかりますか？ プログラマーが関与する必要がある場合は、いくつかの基本的なルールまたはヒューリスティクスを使用します。- Marketoに必要な明確なフィルター、トリガー、または機能がない場合は、JavaScriptやjQueryを使用して行うことができます。 - Marketoだけでは複雑すぎるのでしょうか？ - Marketoはこれもできますか？  – これは簡単にサポートされていないWeb サイトのカスタマイズですか？ - MarketoはWeb サイトや他のデータベースと話す必要がありますか？ - コンピューターで可能なように聞こえますが、Marketoには機能がないのでしょうか？ Marketoは、すぐに利用できる機能を提供しているわけではありませんが、多くのサードパーティ製品との連携やカスタム接続に対応しています。

[LaunchPoint Marketplace](https://exchange.adobe.com/apps/browse/ec?product=MRKTO)で、これらのカテゴリのいくつかを見てみましょう：- [分析ツール ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) - [ データ追加](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) - [ コンテンツ管理システム ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO)一部のサードパーティ製アプリケーションは、プラットフォーム（GoToWebinar）内で直感的なコントロールパネルとセットツールを提供します。 これらは「ネイティブ」統合であり、最も必要な作業はログインを設定してMarketoで使用することです。 ただし、他の拡張機能では、より複雑なAPIを使用する必要があり、より直接プログラムする必要があります。

**Marketo統合オプション** - LaunchPoint統合 – 通常はログインまたは簡単な設定です。 - API統合 – APIとプログラミングのセットアップが必要：（1） [REST API](/help/rest-api/rest-api.md) （2） [SOAP API](/help/soap-api/soap-api.md) （3） [Webhook Integration](/help/webhooks/webhooks.md) – 特別なコードのセットアップが必要ですが、かなり簡単です。 （4） [ メールスクリプト ](./email-scripting.md) （速度） - JavaScriptとjQuery: （1） [Forms 2.0](/help/javascript-api/forms-api-reference.md) （2） [ リードトラッキング （Munchkin） ](/help/javascript-api/lead-tracking.md) （3） [RTP JS](/help/javascript-api/web-personalization.md)開発者を使用してMarketo プラットフォームの機能を拡張する場合の使用例を以下に示します。 次のユースケースはありますか？ その場合は、開発者に相談する時期かもしれません。[LaunchPoint](https://exchange.adobe.com/apps/browse/ec?product=MRKTO)のサービスパートナーの節にアクセスします。

投稿日：_2014-11-06_ by _Josh_

## SlackとMarketoの統合

[Slackはエンタープライズ コラボレーション プラットフォームです](https://slack.com/)。 Slackを使用していれば、Marketo通知を容易にワークフローに取り込むことができます。 この記事では、Marketoで特定のリードアクティビティが発生した場合に、チャットログに通知を追加する方法について説明します。 ユースケースとして、フォームへの入力、価格ページへのアクセス、30日以内に連絡がないリードについて、チーム全体に通知することが考えられます。 以下のスクリーンショットは、このヘルプ記事の手順に従った後、SlackでMarketo通知がどのように表示されるかを示しています。

1. Slackにログインします。 「Slackの統合」をクリックします
1. 受信Webhookの「追加」ボタンをクリックします
1. Marketo通知のチャネルを選択します。 次に、「受信Webhook統合を追加」をクリックします。
1. Webhook URLのコピーと貼り付け（手順8で必要）
1. 通知の名前を選択
1. Marketoにログインします。 管理者に移動します。 「Webhook」をクリックします。
1. 「新規Webhook」をクリックします
1. Webhookの名前を入力します。 手順4からWebhook URLを入力します。 「リクエストタイプ」として「投稿」を入力します。 ペイロードテンプレートを入力します。

これはスクリーンショットのペイロードテンプレートです。 リードレベルのファーストネーム、企業、メールアドレスのトークンを使用します。

`payload={"text": "DEVELOPER SITE ALERT: {{lead.First Name:default=edit me}} {{lead.Company=edit me}}, {{lead.Email Address:default=no email address}}" }`

1. Marketoでトリガー施策を設定する。 フローステップは、WebhookをSlackに呼び出すことです。 スマートリストは、web ページ訪問です。
1. 機能することを確認します。

MarketoのWebhookについて詳しくは、[開発者向けドキュメント ](./webhooks/webhooks.md)を参照してください。

投稿日：_2014-11-10_ by _Murta_

## LitmusとMarketoの統合

[Litmusは、ブラウザーと電子メールクライアント全体で電子メールをテストするためのサービス ](https://www.litmus.com/)です。 Litmusは、クリック数、開封数、削除数を含むメールに関する分析も提供しています。 この記事では、MarketoをLitmusと統合する方法について説明します。

1. Marketoでメールプログラムを設定する際、プログラムダッシュボードの「マイトークン」をクリックします
1. 「メールスクリプト」トークンを中央のパネルにドラッグして追加します。
1. トークンに名前を付け、「クリックして編集」をクリックします
1. 右側の「標準オブジェクト」の下にある「リード」カテゴリを展開します。 「電子メールアドレス」フィールドを見つけてチェックボックスをオンにします。 同じページの左側にある空のスクリプトスペースに、Litmusが提供するトラッキングコードを貼り付けます。 Litmus コードで、`{{lead.Email Address}}`のすべてのインスタンスを`${lead.Email}`に置き換えます。 「保存」をクリックしてライトボックスウィンドウを閉じ、トークンページで「保存」をもう一度クリックします。
1. トークン `{{my.LitmusToken}}`の名前をメモします。 追跡する電子メールを開きます。 メールの一番下に、新しいスクリプトトークンを配置します。 Litmus バージョン `{{my.LitmusToken:default=editme}}`と一致するように既定の情報を追加することもできます。

メールが送信されると、スクリプトはMarketoによってメールに配置されます。

投稿日：_2014-11-18_ by _Murta_

## MarketoのランディングページをFacebookで共有する際に画像を指定する

たとえば、FacebookでMarketoのランディングページを共有する際に、画像が自動的に表示されるようにしたいとします。 また、この画像をMarketoのランディングページ自体ではなく、Facebook シェアに配置することもできます。 これは、Marketoのランディングページにオープングラフのメタタグを追加することで可能です。 その手順は次のとおりです。

1. ランディングページを選択します。 「ドラフトを編集」をクリックします。
1. 「ページのMeta タグを編集」をクリックします。
1. Facebook OG Tags セクションにオープングラフのメタを追加します。 「Save」をクリックします。 形式は次のとおりです：`<meta property="og:image" content="http://example.com/example.jpg"/>`

詳しくは、[Open-graph メタタグに関するFacebookの開発者ドキュメント ](https://developers.facebook.com/docs/sharing/best-practices)を参照してください。

投稿日：_2014-11-17_ by _Murta_

## リファラーに基づいてページをリダイレクト

例えば、Marketoのランディングページへの直接トラフィックを防ぎたいとします。 PDFのように、オーディエンスがフォームに入力してから電子メールを受信するように、ダウンロード可能なコンテンツを配信しているページを想像しましょう。 オーディエンスが特定のページからアクセスしたかどうかを確認することで、この問題を解決できます。 この場合、ユーザーがフォームに入力する必要があるページです。 ユーザーがそのページから来ていない場合は、フォームの入力ページにユーザーをリダイレクトできます。 これを実現するには、コンテンツを含むランディングページへのリファラーページがフォーム入力ページかどうかを確認する必要があります。
以下のスニペット内の`http://example.com/PageWithForm`の両方のインスタンスを、ユーザーに表示するページへのリンクに置き換えます。 これはフォームの入力ページかもしれませ**。

```javascript
<script>
window.onload = function() {
  if (document.referrer !== "http://example.com/PageWithForm") {
    document.location.href = "http://example.com/PageWithForm";
  };
 };
</script>
```

カスタマイズしたJavaScript スニペットを、Marketo ランディングページのクロージングタグの前に含めます。** フォームの入力ページのコンテンツがランディングページに送信されない場合、ユーザーはフォームの入力ページにリダイレクトされます。

投稿日：_2014-11-18_ by _Murta_

## TrelloとMarketoの統合

Trelloは[人気のweb ベースのプロジェクト管理アプリケーション ](https://trello.com/)です。 Trelloを利用していれば、Marketo通知を容易にワークフローに取り込むことができます。 この記事では、Trello ボードにMarketo通知を含むカードを追加する方法について説明します。 このカードは、Marketoで特定のリードアクティビティが発生したときに追加されます。 ユースケースとして、フォームへの入力、価格ページへのアクセス、30日以内に連絡がないリードについて、チーム全体に通知することが考えられます。

1. Trelloにログインします。 Marketo通知を追加するTrello ボードに移動します。 「リストを追加」をクリックし、名前を付けます。
1. 「サイドバーを表示」をクリックします。 「E メールからボードへの設定」をクリックします。 「この掲示板の電子メールアドレス」ボックスに電子メールを記録します。 このメールはステップ 6で使用します。 Marketo通知を追加するリストを選択します。
1. Marketoにログインします。 新しいスマートキャンペーンをクリックします。 名前を入力し、「保存」をクリックします。
1. スマートリストに移動します。 トリガーの選定： この例では、フォーム入力トリガーを使用します。 フォームの入力トリガーを中央のパネルにドラッグします。 この通知をトリガーするフォームを選択します。
1. メールを作成します。 「新規」をクリックします。 「ローカルアセット」をクリックします。 「New Email」をクリックします。 メールに名前を付けます。 「Create」をクリックします。
1. 手順5で作成した電子メールの「ドラフトを編集」をクリックします。 Trello カードに表示する関連トークンをドラッグします。 Marketo電子メールの件名はTrello カードのタイトルに表示され、Marketo電子メールの本文はTrello カードの説明に表示されます。 例えば、リードの姓と名をTrello カードのタイトルに含める場合は、「LEAD ALERT: `{{lead.First Name:default=edit me}}` `{{lead.Last Name:default=edit me}}`」を使用できます。 次に、メールを承認します。
1. スマートキャンペーンに移動します。 「フロー」をクリックします。 中央のパネルに「アラートを送信」をドラッグします。 作成したメールを選択します。 「送信先」を「なし」に選択します。 手順2のTrello メールとして「他のメールに」を選択します。
1. 上部メニューの「スケジュール」をクリックします。 「Activate」をクリックします。 「確認」をクリックします。
1. 統合のテスト： タイトルにリードの氏名が記載されたカードが、Trello ボードに表示されます。 詳しくは、[Trelloのドキュメント ](https://support.atlassian.com/trello/)を参照してください。

投稿日：_2014-11-18_ by _Murta_

## カスタムフィールド値によるリードの検索

たとえば、Marketo APIから、特定のアクティビティまたは非アクティビティの条件に一致するリードを取得するとします。 例えば、過去30日以内にスコアが変更されていないリードを探したい場合、 この記事の手順に従うことで、このリードのリストを取得できます。 そのために、Marketoでスマートキャンペーンを作成し、過去30日以内にスコアが変更されていないリードを特定し、そのリードに値を保存して特定します。 次に、この値を持つAPIをクエリします。

1. customLeadStatusという新しいカスタムフィールドを作成し**Marketoにログインして、管理パネルに移動します。 「フィールド管理」をクリックします。 「新規カスタムフィールド」をクリックします。  フィールドに名前を付けます。 「Create」をクリックします。
1. 30日以内に更新されていないリードを検索するスマートリストを使用して、スマートキャンペーンを作成します。** 「新規スマートキャンペーン」をクリックします。 新しいスマートキャンペーンに名前を付けます。 「スコアなし」を右パネルから中央パネルにドラッグしました。
1. 手順3からスマートキャンペーンにフローステップを追加して、customLeadStatus フィールドを新しい値で更新します**。右パネルから中央パネルに「データ値を変更」をドラッグします。
1. スマートキャンペーンを更新して、リードを複数回に分けて実行できるようにします** スケジュールをクリックします。 「Edit」をクリックします。  毎回選択してください。 「Save」をクリックします。 キャンペーンが実行され始めます。
1. フィルターの種類REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)で[複数のリードを取得するクエリを実行します。 パラメーターfilterType=customLeadStatus &amp; filterValue=needsEnrichment.**を指定します。

このデータを返すリクエストの例です。

`<https://AAA-BBB-CCC.mktorest.com/rest/v1/leads.json?access_token=><yourAccessToken>&filterType=customLeadStatus&filterValues=needsEnrichment`

API呼び出しが成功すると、needsEnrichmentの値と一致するcustomLeadStatus フィールドを持つリードのJSON データが返されます。 詳細については、[ フィルターの種類REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)による複数のリードの取得を参照してください。

投稿日：_2014-11-22_ by _Murta_

## SOAP APIを介した商談同期

この記事では、SOAP APIを介してMarketoに商談を挿入し、企業やリードに関連付ける方法について説明します。 このプロセスの仕組みの説明から始まり、各シナリオのコードサンプルを提供します。

**テーブル構造図**&#x200B;まず、次の図はテーブル構造を示しています。 Idは、レコード（連続番号）の作成時に自動生成されます。 太字のフィールドは必須です。商談担当者の役割のみが必須フィールドを持ちます。 括弧内のフィールドはオプションであり、点線を含む接続もオプションです。

**基本的な商談挿入**&#x200B;最初に商談を挿入し、次に商談担当者の役割を挿入すると、商談がリードにリンクされます。 この例では、リード IDと商談IDを使用して、商談担当者の役割を指定します。 商談を作成する際に、SOAP応答で商談IDを取得します。 リード IDは、Marketo リードデータベースのすべてのリードに表示されます。

**会社リンク**&#x200B;ほとんどの場合、商談を個人に加えて会社にリンクする必要があります。 Marketoでは、SOAP APIを介して会社レコードにアクセスできず、リードレコードのみがアクセスされます（リードレコードには会社フィールドが含まれます）。 引き続き、各リードに一意の会社識別子を追加し、そのIDを商談で使用することで、商談を会社にリンクできます。 ステップ 1は、リードレコードに「会社ID」フィールドを作成し、通常はバックエンドシステムから一意の識別子を入力することです。 ステップ 2は、商談に「会社ID」フィールドを作成することです。このようなフィールドを作成するには、Marketo サポートまたはコンサルティングに依頼する必要があります。 次に、商談を作成する際にこのフィールドに入力します。商談を会社に接続します。 これは、Marketo Revenue Cycle Analyticsを使用しており、会社情報に依存する商談インフルエンスアナライザーを使用する場合に特に重要です。

**外部識別子の使用**&#x200B;多くの場合、バックエンドシステムと統合する際に、独自の一意の識別子を持っている可能性があります。 これらの一意のIDは、外部キーを使用してMarketoで使用できます。 リードの場合は、通常、Marketo IDまたは電子メールアドレスの代わりに一意のIDとして使用されるForeign System Person Id （FSPID）を使用します。 FSPIDは非表示のシステムフィールドで、Marketo内では表示されません。 まだ実行していない場合は、商談の同期で、FSPIDを「Foreign Id」などのカスタムフィールドに保存する必要があります（フィールドに任意の名前を付けることができます）。 このフィールドは、Marketo管理者として自分で作成できます。 商談の場合、商談に別のカスタムフィールド（例えば「Foreign Id」）をMarketo サポートが作成します（任意の名前を付けることができます）。 商談を挿入する際にこのフィールドに入力します。 最後に、商談担当者の役割を作成する場合は、Marketo IDを使用する代わりに、両方の外部キーを使用してリードと商談間のリンクを指定します。 外部キーを使用して、商談のリードを更新することもできます。 現時点では、商談人物の役割レコードに外部キーを追加することはできないので、これには自動生成されたMarketo IDを使用する必要があります（商談人物の役割を作成した後にSOAP応答で取得します）。

**コード例**&#x200B;手順：1. 外部キーと会社IDを使用してリードを挿入/更新する1. 外部キー1で商談を挿入します。 外部キーを使用して商談人物の役割を挿入する1. SOAP リクエスト – 外部キーと会社IDで既存のリードを更新すると、外部キー「12346」とアカウント/会社ID 「C123」で既存のリード（Marketo Id 「6」）が更新されます。 商談担当者の役割に必要なので、カスタムフィールドに外部キーも保存しています。 外部キーの使用はオプションです。Marketo IDを使用して、このリードを商談にリンクすることもできます。 会社IDの使用もオプションですが、RCAで商談インフルエンスアナライザーを使用する場合は必須です。 リクエスト：

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

SOAP リクエスト – 商談作成この場合、商談テーブルに2つのカスタムフィールドが作成されました：- `opportunityId` →商談一意のIDを保持 – `cAccountFSID` →は、独自の商談IDを指定するのではなく、会社参照を保持します。 Marketoで生成した商談IDを使用することもできます。 その場合、外部キーノードは除外されます。 会社の関連付けもオプションですが、RCAで商談インフルエンスアナライザーを使用する場合は必須です。 リクエスト：

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

SOAP リクエスト – オポチュニティ人物ロールこのリクエストは、リードをオポチュニティにリンクします。 1つのSOAP リクエストで複数のリンクを指定できます（この例では、商談を1つのリードにのみリンクしています）。 これは外部キーを使用してリンクを指定しますが、コメントでは実際のIDの使用方法も示されます（この場合は、リード IDは6で、商談IDは40）。 この「IsPrimary」フィールドと「Role」フィールドはオプションです。 リクエスト：

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

**別のアプローチ （1回の通話で手順2と3を実行）**&#x200B;最初に商談を挿入し、次に商談担当者の役割を挿入できますが、1回のSOAP通話でこれを行うこともできます。 ただし、商談には外部キーを使用する必要があります（商談がまだ生成されていないため、商談人物の役割で自動生成された商談IDを使用することはできません）。 もちろん、同じAPI呼び出しで、複数のリードをこの商談にリンクすることもできます（この例では、商談を1つのリードにのみリンクしています）。 リクエスト：

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

投稿日：_2014-11-26_ by _Jep_

## マルチスレッド REST API リクエスト

Marketo APIを呼び出す際のパフォーマンスを向上したい場合は、同時リクエストを行うことができます。 この手法により、より多くのデータをより短期間で取得できます。 API リクエストを行う場合、クライアントとサーバー間のラウンドトリップ時間の一部は、ワイヤー上の転送時間です。 したがって、リクエストのワイヤ上の転送時間を集計して短縮できれば、パフォーマンスが向上します。 以下のサンプルコードは、Rubyでこれを行う方法を示しています。 マルチスレッド要求の作成に使用される[ イベント処理ライブラリであるEventMachineを使用します](https://github.com/igrigorik/em-http-request/wiki/Parallel-Requests)。 次の例では、[ リードアクティビティ API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET)を呼び出し、2つの同時リクエストを行います。 このアプローチにより、2回目のリクエストのクライアントからサーバーへの転送時間がなくなります。 これは、最初のリクエストと同時に2番目のリクエストを含めることで実現します。 API応答はテキストファイルに書き込まれます。

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

投稿日：_2014-12-03_ by _Murta_

## パフォーマンス調整API リクエスト

この記事では、Marketo APIからデータをリクエストする際のパフォーマンスを向上させる戦略について説明します。 ただし、これらの戦略の利点を、Marketo APIの日別制限の運用制約と比較検討する必要があります。
**Strategy 1 - Request Less Data in Each API Call** API呼び出しでより多くのデータをリクエストすると、Marketo サーバーがデータベース内のデータを検索するのにかかる時間が増加します。 [getMultipleLeads SOAP API](/help/soap-api/getmultipleleads.md)などの日付範囲でAPI呼び出しを行う場合は、呼び出しごとに時間範囲を短縮し、より多くの呼び出しを補償します。 例えば、6月1日から7月1日までのデータをリクエストする代わりに、6月1日から2日までの1回の呼び出しや、6月2日から1日までの別の呼び出しなど、1日ずつリクエストします。 Marketo リードフィールドからデータを返すAPI呼び出しを行う場合は、必要なフィールドのみをリクエストしてください。 リードフィールドが追加されるたびに、API呼び出しにかかる時間が段階的に増加します。 また、バッチサイズ、つまりコールごとにリクエストされるリード数を減らすこともできます。
**戦略2 – 同時リクエストを行う** パフォーマンスを向上させ、より多くのデータを一度に取得します。 APIに対して同時リクエストを行うことができます。 このアプローチにより、ワイヤーAPI リクエストにかかる時間を集計して削減できます。 例えば、「フィルターの種類で複数のリードを取得」に対してリクエストを行っているとします。 1つのリクエストクエリのリード 1 ～ 300と、別のリクエストクエリのリード 301 ～ 600に対して、同時リクエストを実行できます。
**戦略3 - データのキャッシュ** Marketoの一部のデータは、リードフィールドのリストなどの変更頻度が、リードアクティビティデータなどの他のデータよりも低くなっています。 更新の頻度が低いデータをキャッシュする場合は、API呼び出しの回数を減らします。 また、データをローカルで検索することは、一般的にリモート web サービスからデータにアクセスするよりも高速であるため、パフォーマンスが向上します。

投稿日：_2014-12-05_ by _Murta_

## Marketo フォームデータをGoogle Analyticsに送信する

Google Analyticsでは、カスタムデータイベントを送信し、そのデータを利用してweb サイトのパフォーマンスをセグメント化および分析できます。 以下のJavaScript コードスニペットを使用すると、訪問者がweb フォームを送信した後に、Marketo 2.0 フォームデータをGoogle Analyticsに自動的にプッシュできます。 次に設定方法を示します。

**手順1** コードの下部（タグの前）にあるMarketo Formsを含むページにJavaScript タグを挿入します。 JavaScriptは、非表示でないフィールドのみを送信します（sendHiddenFields : false）。 これは、sendHiddenFieldsをfalseからtrueに変更することで調整できます。 また、「fieldsToExclude」配列にフィールド IDを追加して、除外するフィールドを選択することもできます。

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

**手順2** GAのデータがレポート セクションに表示されます。 ビヘイビアー/イベント/上位イベントに移動します。**スクリプトの制限：** – このコードサンプルは[Marketo Forms 2.0](/help/javascript-api/forms-api-reference.md)とのみ互換性があります。 - Googleのプライバシーポリシーにより、お客様は個人情報（メールアドレスまたは名前）を送信することはできません。 潜在的なプライバシーに関する懸念を除いて、これは個人を特定できる情報であるため、[Google Analyticsの利用規約](https://marketingplatform.google.com/about/analytics/terms/us/)に違反します。

「お客様は、本サービスを利用して、個人を特定するデータ（名前、メールアドレス、請求情報など）またはGoogleによって合理的にリンクされるその他のデータを追跡、収集、またはアップロードすることはできません。」

投稿日：_2014-12-16_ by _Yanir_

## Marketo フォームへのフルネームフィールドの追加

web フォームを短くすれば、コンバージョン率が向上します。 以下のJavaScript コードサンプルでは、名フィールドと姓フィールドを1つの氏名フィールドに結合することで、フォームをさらに短くすることができます。 訪問者がフルネームを入力すると、スクリプトはテキストを自動的にファーストネームとラストネームのフィールドに分割します。 既知の訪問者に対しては、スクリプトは名前と姓を結合し、新しいフィールドにコピーして、フィールドに再度入力する必要がないようにします。 次に設定方法を示します。

**手順1** Marketoにフルネームという新しいカスタムフィールドを作成します。 スクリプトはこのフィールドを使用してフルネームを表示するだけなので、CRM プラットフォームで作成する必要はありません。
**手順2**このフィールドをすべてのweb フォームに追加します。 名フィールドと姓フィールドを非表示に設定します。 JavaScriptで、「splitFullName」設定を変更して、3つのフィールド名を含めます。 注意：これらの名前がページ上の他の場所に表示されないようにしてください。
**ステップ 3** タグの前に、コードの下部にあるすべてのランディングページにJavaScriptを挿入します。

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

注意：このコードは、Marketo Forms 2.0でのみ機能します。

投稿日：_2014-12-16_ by _Yanir_

## REST APIを介してリードをインポートするcURLの使用

REST APIを使用してCSV ファイルからリードを読み込みますが、Postman Chrome拡張機能を使用すると読み込みが困難になることに気づきました。 この記事では、cURLでこれを行う方法を説明します。

1. [MarketoのREST APIにデータをプッシュするために使用するコマンドラインツールであるcURL](https://curl.se/download.html)をダウンロードしてインストールします。
1. コマンドラインを開き、CSV ファイルが配置されている場所に移動します。 CSV ファイルの列ヘッダーは、Marketo フィールド名ではなく、API フィールド名と一致する必要があります。
1. アクセストークンが必要です。 Marketoにログインし、Adminに移動してからLaunchPointに移動します。 REST API ユーザーを見つけて、「詳細を表示」をクリックします。 「トークンを取得」ボタンをクリックします。
1. また、Marketo インスタンスに固有のREST エンドポイントも必要です。 Marketoにログインし、「管理者」、「Web サービス」の順に選択します。 「REST API」とマークされたセクションには、エンドポイント URLがあります。
1. コマンドラインで、cURL呼び出しの形式に従います。 `<accesstoken>`をステップ 3のアクセストークンに置き換え、`<REST API Endpoint URL>`をステップ 4のREST API エンドポイント URLに置き換えます。 詳細については、[こちらをご覧ください](https://developer.adobe.com/marketo-apis/api/mapi/#operation/importLeadUsingPOST)。 ここでの「/bulk」は、エンドポイント URLの最後にある「/rest」を置き換えます。 /rest/bulkにエンドポイントが設定されている場合は、エラーが返されます。

`curl -i -F format=csv -F file=@leaddata.csv -F access_token=<accesstoken> <REST API Endpoint URL>/bulk/v1/leads.json`

投稿日：_2014-12-16_ by _Jordan_

## Marketoに次の確認アラートを追加：

例えば、Marketoフォームの「送信」ボタンをクリックした際に、「本当に送信して良いですか？」と尋ねる通知を表示したいとします。 これは、JavaScriptを数行実装することで可能です。これにより、オーディエンスが「送信」ボタンをクリックすると、確認ボックスが表示されます。 例を紹介します。 次に示すように、onSubmit関数をMarketo フォームに追加します。 Marketo Forms APIについて詳しくは、開発者用ドキュメント ](/help/javascript-api/forms-api-reference.md)を[確認してください。

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

投稿日：_2014-12-17_ by _David_

## フォローアップランディングページなしで「ありがとうございます」メッセージを表示する

通常、Marketo フォームを使用する場合は、2つのランディングページを作成します。1つはフォームを配置し、1つはフォームが完了した後にリダイレクトします。 ただし、場合によっては、ふたつの異なるランディングページを個別に管理する必要がない場合もあります。 Forms 2.0 JavaScript APIを使用すると、フォームとサンキューメッセージに同じランディングページを実際に使用できます。 そのためには、まず登録ランディングページとフォームを作成し、通常どおりランディングページにフォームを配置します。 次に、HTML要素をページに追加します。 この要素では、フォームが送信された時点でアクティブ化されるコードを追加します。 フォームが非表示になり、非表示が表示されます <div> サンキューメッセージが含まれています。 JavaScriptは次のようになります。

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

サンキューメッセージテキストを編集します。

`<div id="confirmform" style="visibility:hidden;"><p><strong>Thank you. Check your email for details on your request.</strong></p></div>`

コードサンプルでホスト名とサンキューメッセージを編集します。 最初にMarketo インスタンス（「//app-sj06.marketo.com/js/forms2/js/forms2.js」など）を参照し、2番目にフォームが完了したら表示するサンキューテキストを含める必要があります。 テキストは、HTML要素を配置した正確な位置にランディングページに表示されるので、必ずプロパティシートで編集してください。 また、HTML要素のレイヤーが、フォームのレイヤーよりも小さいことを確認する必要があります。 デフォルトでは、両方がレイヤー15に配置されるので、HTMLのエレメントレイヤー11を作成する場合は安全です。 この操作を行わない場合、「ありがとうございます」メッセージと重なるフォームフィールドボックスを入力することはできません。 フォローアップタイプは、JavaScriptによって上書きされるため、フォームやランディングページで変更する必要はありません。 Marketo Forms APIについて詳しくは、[開発者向けドキュメント ](/help/javascript-api/forms-api-reference.md)を参照してください。

投稿日：_2014-12-19_ by _Kristin_

## Marketoプラットフォーム上に構築されたオープンなSourceプロジェクトのハイライト

これは、開発者コミュニティによってMarketo プラットフォームを中心に構築されたオープンソースプロジェクトを取り上げた、継続的なシリーズの最初の投稿です。 MarketoのGitHub アカウント ](https://github.com/Marketo/Community-Supported-Client-Libraries)のリストを[管理しています。このリストでは、Marketo デベロッパーコミュニティによって作成されたクライアントライブラリとプロジェクトを追跡しています。 ここでは、Marketo RESTとSOAP APIを中心に開発された3つのプロジェクトを紹介します。 Daniel Chestertonは、Marketo REST API](https://github.com/dchesterton/marketo-rest-api)用にPHPで[ クライアントライブラリを作成しました。 クライアントライブラリは現在、12のREST API エンドポイントをカバーしています。**ElixiterのKyle Halstvedt氏は、[Marketoの静的リストからリードをGoogle スプレッドシートに取り込む](https://github.com/Elixiter/mkto_google-spreadsheet) プロジェクトを作成しました。 Kyleのプロジェクトでは、Marketo REST APIを使用しています。  David Santosoは、Marketo SOAP API用に[Ruby Gemを作成しました。](https://github.com/davidsantoso/markety) このプロジェクトは、Marketo SOAP APIとRuby on Rails アプリをより迅速に統合するのに役立ちます。  Marketoプラットフォームで、開発者コミュニティによって作成されたより多くのプロジェクトを確認できることを嬉しく思います。 Marketo プラットフォームのオープンソースプロジェクトで作業している場合は、[ プルリクエストを介してこのGitHub リポジトリに送信してください](https://github.com/Marketo/Community-Supported-Client-Libraries)。

投稿日：_2015-01-02_ by _Murta_

## ユーザーの場所に基づいてページコンテンツを動的に変更する

例えば、ユーザーの所在地に応じて、ランディングページの電話番号を動的に変更するとします。 例えば、カリフォルニア在住の方は、カリフォルニアのオフィスの電話番号をランディングページに表示し、日本の場合は、日本のオフィスの電話番号を表示します。  これを実装する方法の1つは、JavaScriptと[HTML5 Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API)を使用することです。 このアプローチの利点は、ひとつのランディングページを作成し、複数の静的なランディングページではなく、ユーザーの場所にもとづいて動的に変更できることです。 技術実装の詳細は次のとおりです。 緯度と経度の座標を持つオフィスの場所のオブジェクトと、オフィスの電話番号を持つ2番目のオブジェクトを作成します。 実稼動環境では、これらの2つのオブジェクトを1つのオブジェクトに結合することをお勧めします。

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

ユーザーの場所をリクエストするメソッドを作成します。 エラーを処理するために、ユーザーの場所にアクセスできない場合は、Marketo本社とその電話番号がデフォルトで使用されます。

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

最後に、ユーザーの場所に最も近いオフィスを見つける方法を作成し、ページ上の最も近いオフィスの電話番号を返します。 このメソッドは、[GeolibのfindNearest メソッドを使用します。これは、地理空間演算](https://github.com/manuelbieh/Geolib)を提供するJavaScript ライブラリです。

```javascript
//Find nearest Marketo office to user's location
function findNearestOffice(position) {
        var nearestOffice = geolib.findNearest({latitude: position.coords.latitude, longitude: position.coords.longitude}, officeLocations);
        x.innerHTML = "Marketo Location: " + nearestOffice.key + "
Marketo Phone Number: " +  officePhoneNumbers[nearestOffice.key];
}
```

Adobe Workfrontを導入しました。 ユーザーがページのボタンをクリックすると、getLocation メソッドがトリガーされます。 この[GitHub リポジトリ ](https://github.com/MurtzaM/Find-Nearest-Marketo-Office)には、このデモの設定に必要なファイルが含まれています。

投稿日：_2014-12-20_ by _Murta_

## リードの追跡と複数ドメイン

MarketoのMunchkin トラッキングコードを使用すると、web サイトへの訪問をトラッキングできます。 多くの場合、Munchkinのトラッキングコードを使用して、web サイトの各ページの匿名のリードを特定します。 Munchkinの仕組みを説明しましょう。 ページへの訪問は既存のリードに対して記録され、Cookieのない訪問者がページに訪問すると、新しいCookieが作成および保存され、新しい匿名リードがMarketo データベースに作成されます。 現在のドメインに既存のCookieがない場合、Munchkin-trackerは訪問者を自動的にCookieします。 Marketoでは、リードのアクティビティログにイベント（リンクをクリック、web ページにアクセス、または新しいリード）が記録されます。 Cookie内に保存される値は、特定の訪問者に対して一意です。 値は、一意のMunchkin アカウントトラッキング ID、ドメイン名、タイムスタンプ、ランダムな整数の組み合わせです。
**複数のドメインがある場合はどうなりますか？** 例えば、追跡するサイトが2つあるとします：`<www.apples.com>`と`<www.bananas.com>`。 トラッキングコードは両方のサイトに配置できますが、次の点を考慮する必要があります。 Marketo Cookieは「ファーストパーティ Cookie」であり、ドメイン固有です。 つまり、サイト 1への訪問者はMarketoで匿名リードとして作成されます。同じリードがサイト 2に移動すると、Marketoで2番目の別の匿名リードが作成されます。 リードがサイト 1でフォームに入力すると、このレコードが既知になり、サイト 2の匿名レコードは残り、そのサイトへの後続の訪問が引き続き蓄積されます。 その後、リードがサイト 1で使用されているのとまったく同じメールアドレスをサイト 2でフォームに入力すると、既知のリードの両方が自動的にマージされ、過去および将来のすべての行動がMarketoの1つのレコードで追跡されます。 両方のCookie IDが同じリードに関連付けられており、すべてのweb アクティビティ（いずれかのドメインから）がそのリードに存在します。
**複数のサブドメインについて教えてください。** サブドメインは問題ではありません。 例としてMarketo.comを使用してみましょう。 fr.marketo.comやde.marketo.comなど、異なる言語に対して複数のサブドメインがあります。 サブドメインを使用すると、すべてのアクティビティが同じリードレコード/Cookieに対して記録されます。

投稿日：_2015-01-13_ by _David_

## Marketo フォームのヒント テキストの色を変更する

Forms 2.0でヒント テキストの色（プレースホルダーテキストとも呼ばれます）を変更するとします。 カスタム CSSを使用すれば、この操作が可能です。 例えば、下のスクリーンショットでは、このMarketo フォームのヒントテキストを青にしました。 Marketo Formsの使用方法に応じて、3つのオプションがあります。

**オプション 1: Marketo フォームを埋め込む場合は、以下のCSSをメインのCSS ファイルに直接追加します。**

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

**オプション 2: Marketo フォームを埋め込む場合、`<head>` セクションの`<style></style>` タグ間のページにCSSを直接追加できます。**

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

**オプション 3: Marketo ランディングページでMarketo フォームを使用している場合は、Marketo UIからこのカスタム CSSを追加できます。** Marketo ナビゲーションツリーでランディングページを見つけます。 「ドラフトを編集」をクリックします。 「ページのMeta タグを編集」をクリックします。 以下のCSSを「カスタム HEAD HTML」セクションに追加します。 `<style></style>` タグを含めてください。

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

「ドラフトを承認」をクリックします。 Marketoのランディングページにアクセスすると、ヒントテキストはCSSで定義した色になります。 Marketo Formsについて詳しくは、[ ドキュメント ](/help/javascript-api/forms-api-reference.md)を参照してください。

投稿日：_2015-01-14_ by _Murta_

## REST APIを介したアクティビティデータの取得

例えば、今月リストに追加されたすべてのリードを取得したい場合、 [ リード アクティビティの取得REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET)を使用すると、このデータを取得できます。 リード活動を取得APIを呼び出す前に、認証APIからアクセストークンを取得し、[ ページングトークンを取得API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getActivitiesPagingTokenUsingGET)からも開始日トークンを取得する必要があります。 以下は、今月リストに追加されたすべてのリードを返すために呼び出す必要がある個々のAPI エンドポイントを順を追って説明するRubyのサンプルコードです。 1. アクセストークンを取得する**

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

1. アクティビティデータの取得**この呼び出しに必要なアクティビティタイプ IDを決定するには、[取得アクティビティタイプ API](/help/rest-api/activities.md)をクエリします。 Get Activity Types APIは、すべてのアクティビティタイプと関連IDを含むスキーマを返します。 例えば、新しいリードが作成された場合はID 12を、web ページ訪問の場合はID 1を返します。

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

1. リード活動を取得APIは、結果セットを通じてページネーションするために使用できる各応答を含むページングトークンを返します**。詳細については、[REST API ドキュメント ](/help/rest-api/rest-api.md)を参照してください。

投稿日：_2015-01-20_ by _Murta_

## Adobe Marketo上に構築されたオープンなSourceプロジェクトのハイライト：パート 2

これは、開発者コミュニティによってMarketo プラットフォームを中心に構築されたオープンソースプロジェクトを取り上げた、進行中のシリーズの2番目の投稿です。 MarketoのGitHub アカウント ](https://github.com/Marketo/Community-Supported-Client-Libraries)のリストを[管理しています。このリストでは、Marketo デベロッパーコミュニティによって作成されたクライアントライブラリとプロジェクトを追跡しています。 ここでは、Marketo SOAPとMunchkin APIを中心に開発された3つのプロジェクトを紹介します。[PunchTab](https://www.punchtab.com/)は、Marketo SOAP API](https://github.com/PunchTab/suds-marketo)用に[ クライアントライブラリをPythonで作成しました。[Flickerbox](https://www.flickerbox.com/)が[Marketo SOAP API](https://github.com/flickerbox/marketo)用のPHPのクライアントライブラリを作成しました。* [Richard Morrison](https://x.com/mozz100)が[Marketo SOAP APIからリードデータを取得し、JavaScriptを使用してこのデータをクライアントに渡すPHP スクリプトを作成しました。](https://github.com/mozz100/marketo-whodat) このプロジェクトは、Marketoのユーザーのデータに基づいてページを変更するのに役立ちます。  Marketoプラットフォームで、開発者コミュニティによって作成されたより多くのプロジェクトを確認できることを嬉しく思います。 Marketo プラットフォームのオープンソースプロジェクトで作業している場合は、[ プルリクエストを介してこのGitHub リポジトリに送信してください](https://github.com/Marketo/Community-Supported-Client-Libraries)。

投稿日：_2015-01-20_ by _Murta_

## Google AnalyticsへのRTP レコメンデーションエンジンのクリックの送信

ここでは、Marketo Real-Time Personalization（RTP）のユーザーがGoogle Analytics内のコンテンツレコメンデーションエンジンからクリックを確認するためのソリューションを紹介します。 訪問者がコンテンツレコメンデーションバーをクリックすると、イベントカテゴリ「RTP-Recommendations」の下のGoogle Analyticsにイベントが送信されます。 Analyticsでは、（バーに表示される）推奨テキストがイベントラベルに追加され、推奨アセットのURLがイベントアクションに追加されます。 このスクリプトは、Classic Google AnalyticsとGoogle Universal Analyticsの両方で機能します。 このタグは、HTML ページコードの最後に貼り付ける必要があるので、`</body>` タグの前の最後のタグになります。

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

投稿日：_2015-01-22_ by _Yanir_

## BoomiでのMarketo REST APIの使用：REST認証トークンの取得と保存

Marketoでは、特定の基準を満たすリードを自動的に書き出す設定をすることが非常に一般的なユースケースです。 これは現在、Marketoのインターフェイスでは実行できませんが、Dell Boomi、一部のデータ管理キャンペーンを含む静的リスト、Marketo REST APIなどのサードパーティ製ツールを使用すれば、容易に実行できます。 REST APIとは？ BoomiにはMarketo REST API コネクタがないと思いました。 現在は、そうではありませんが、HTTP コネクタを使用してjSON応答シェイプを手動で定義することで、同じことを実現できます。 最初の手順は、[REST API Marketo開発者ページ ](/help/rest-api/rest-api.md)で説明されているように、REST APIを使用するようにMarketo インスタンスを設定することです。 また、Dell Boomi アカウントにアクセスでき、このような統合プロセスを作成するためのBoomi スキルを持っていることも前提としています。 最後のプロセスは次のようになり、次のMarketo REST API操作への呼び出しが含まれます。それぞれの操作には、開発者サイトに表示されるjSON応答形状が関連付けられています。 時間を節約するために、[認証](/help/rest-api/authentication.md)のJSON例の下にリストしました

```json
{
  "access_token": "",
  "token_type": "",
  "expires_in": 0,
  "scope": ""
}
```

[ リスト IDで複数のリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)のJSONの例

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

[ リストからリードを削除](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE)のJSONの例

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

プロパティの定義：RESTの呼び出しを開始する前に、使用している変数を外部化してカプセル化することが重要です。 以下に示すように定義しました。

* ClientID:REST Launchpoint サービスからこれを取得します
* クライアントシークレット：REST Launchpoint サービスからこれを取得します
* AccessToken: REST呼び出しからこれを取得します
* Static ListID：操作する静的リストのLIST ID。 MarketoのURLから取得します
* フィールド：REST サービスがMarketoからリードごとに取得するフィールドのコンマ区切りリスト。 Mine is &quot;id, email,firstName,lastName&quot; * IDStringToDelete：最終的に、リストから削除する際に使用する静的リスト内のすべてのリードのIDが含まれます
* ActivityTypes：このブログのパート 2で使用されます。
* SinceDateTime：このブログのパート 2で使用されます。
* PagingToken：このブログのパート 2で使用されます。
* フォルダー – 送信：SFTP サーバー上の送信フォルダーへのパス。 この例では「/data/outgoing」を使用します。 これにより、SFTP操作をパラメーター化して汎用にすることができます。

認証トークン：先ほど述べたように、「データなし」の開始形状を持つプロセスを作成した後、キャンバスにコネクタを配置します（これは個人的な選択です。私は英国のプラグのように見えるすべてのコネクタが好きです）。
コネクターは次のように設定する必要があります。- コネクターはHTTP GET クライアントです – コネクションはURL: `https://123-ABC-456.mktorest.com`を使用します（最後に/restをメモします。これにより、これをREST呼び出しに使用したり、ID アクセストークンを取得したりできます。 123-ABC-456をMarketo インスタンスに適したものに変更します） – オペレーションは「Get OAuth Token」（新機能）です。 - Request Profile = None - Response Profile = JSON - New Profile called &quot;Authentication Token Response&quot; - Content Type: Plain - HTTP Method: GET - Resource Path （add 4 without quotation marks）: &quot;identity/oAuth/token?grant_type=client_credentials&amp;client_id=&quot;; &quot;ClientID （Replacement variable）&quot;; &quot;&amp;client_secret=&quot;; &quot;ClientSecret （Replacement variable）&quot; - Set Parameters under Configure> Parameters —> （+）: Set ClientID = Process Property Client ID; Set ClientSecretこのトークンの後に、プロセストークンが成功します図に示すように、「AccessToken」変数をjSON応答から抽出します。
このステップのパターンは次のステップでも繰り返されますが、異なるjSON リターンプロファイルで新しい操作を使用します。 実際、REST呼び出しの多くは、軽微な変更でも同じように処理されます。 次の記事では、RESTを使用して、これを拡大し、静的リストからリードのリストを取得します。 今のところ、プロセスを実行しますが、「プロパティを設定」の後にストップシェイプを置き、デバッグで実行して、Marketoに表示されているのと同じトークンを確認します。 彼らは完璧に一致する必要があります！

投稿日：_2015-01-26_ by _John_

## Google Font APIを使用したMarketo ランディングページへのカスタムフォントの追加

**注：これは[Murtza Manzur](https://www.linkedin.com/in/murtzam)によるブログ投稿です。 Murtzaは、サンフランシスコ湾岸地域を拠点とするMarketo Developer Evangelistです。**
例えば、Marketoでランディングページを制作し、カスタムフォントを使用したいとします。 これは、Google Font APIを使用することで可能です。  Google Fontsを参照して、CSS ファイルにimport メソッドを追加します。

`@import url(http://fonts.googleapis.com/css?family=Open+Sans:400,300,600);`

投稿日：_2015-01-26_ by _Murta_

## メールスクリプトを使用して、リードの名前を大文字にする

「John doe」のように、リードが小文字で名前を入力したとします。 しかし、メールキャンペーンを展開する際には、John Doe氏のようにメール内のリードの名前を大文字に変換したいと考えます。 メールスクリプトを使用して、リードの名前を大文字に変換できます。 その方法は次のとおりです。

1. メールプログラムで、「マイトークン」タブをクリックします。
1. 右側のパネルから中央のパネルに「メールスクリプト」をドラッグして、新しいメールスクリプトトークンを作成します。 トークンに名前を付けます。
1. スクリプトトークンを編集テキストボックスに、以下のコードを貼り付けます。 右側のパネルの「リードオブジェクト」で、「名」チェックボックスを選択します。 「Save」をクリックします。

```javascript
# set($name = ${lead.FirstName})
# set($formattedFirstName = $name.substring(0).toUpperCase())
$formattedFirstName
```

1. メールアセットでトークンを参照します。 先頭の文字を大文字にしたリードの名前が出力されます。 電子メールの作成について詳しくは、[電子メールの作成に関するドキュメント ](/help/email-scripting.md)を参照してください。

投稿日：_2015-01-26_ by _Murta_

## Marketo REST APIからすべてのリードを取得する

StackOverflowで[件の質問があり、REST APIを介してMarketoからすべてのリードのリストを取得する方法を尋ねました](https://stackoverflow.com/questions/28184900/how-do-i-get-the-list-of-all-the-leads-in-marketo)。 このデータは、[ フィルターの種類REST API エンドポイントによる複数のリードの取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)を使用してクエリできます。 Marketoのリードには、1から始まる順にリード IDが割り当てられます。 フィルターの種類REST API エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)で[複数のリードを取得を使用すると、呼び出しごとにリード IDで300 リードをクエリできます。 このエンドポイントを呼び出すたびに、idをfilterTypeとして、リード IDをfilterValuesとして指定する必要があります。 すべてのリードを取得するには、リードの総数を一度に300回繰り返します。 Y
Marketo UIを使用して、Marketo インスタンス内のリードの合計数を取得できます。 Marketo UIで、「リードデータベース」タブに移動し、「システムスマートリスト」をクリックし、「すべてのリードスマートリスト」をクリックして、最後に「リード」タブをクリックします。 次に、「ID」列をクリックし、降順で並べ替えます。 リードを並べ替えた後、すべてのリードをクエリする場合、最初のリードのIDはリード IDの上限になります。 Marketo UIにアクセスしてリードの合計数を取得できない場合は、[別のアプローチを使用して、リード アクティビティの取得REST API](https://stackoverflow.com/questions/28419967/get-all-leads-programmatically-in-marketo-v1)を使用してこの値を取得します。

1. 最初のAPI呼び出し：...を次の間のすべての値に置き換えます。

`/rest/v1/leads.json?filterType=Id&filterValues=1,2,3,...,298,299,300`

最初の呼び出しに対するRubyのサンプルコードを以下に示します。

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

1. 2回目のAPI呼び出しと、その後の各API呼び出しは、リードの合計数に達するまで同じパターンに従います。

```
//replace ... with all the values in between
/rest/v1/leads.json?filterType=Id&filterValues=301,302,303,...,598,599,600
```

詳しくは、[REST API ドキュメント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)を参照してください。

投稿日：_2015-01-28_ by _Murta_

## Iframeから親ページへのフォーム送信アクションの実行

ユーザーがiframe フォームを使用し、フォームに入力した訪問者をサンキューページやPDF、ビデオなどに誘導するケースがいくつか見られました。問題は、フォームが親ページとは異なるランディングページに埋め込まれているため、アクションはフォームが存在する内部ページでのみ行われることです。 これを解決するために、以下に2つのJavaScriptタグを作成しました。 HTMLのエレメントとしてiframe ページに挿入するか、iframeに使用するランディングページテンプレートに直接挿入します。 最後の`</body>` タグの前に配置します。 最初のタグは親ページでアクションを実行し、2番目のタグは新しいタブでアクションを開きます。

親ページの&#x200B;**フォームアクション**

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

**新しいタブでのフォームアクション**

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

投稿日：_2015-02-02_ by _Yanir_

## YouTube動画のビューデータを市場に投入

例えば、Marketoでリードが特定の動画を始めたり終えたりしたかどうかにもとづいて、リードをセグメンテーションするとします。 これは、Munchkin、YouTubeのIframe API、およびMarketoのスマートリストを使用して実行できます。 この記事のサンプルコードでは、Munchkinを通じて、Marketoにビデオの開始イベントとビデオ終了イベントを送信できます。 これを機能させるには、Marketoにビデオビューイベントを送信する前に、Munchkinをページに読み込む必要があります。 開始および終了したビデオは、リードのアクティビティログに表示されます。 Marketoにデータを取り込み、スマートリストを作成して、動画の開始または終了したリードをセグメンテーションできます。

1. 埋め込むYouTube ビデオのIDを取得します。**使用するYouTube ビデオのURLから、`v=`の後の一連のランダムな文字であるIDに注意してください。
1. このコードサンプルの8行目に、手順1のYouTube ビデオ IDを配置します。 次に、ページのHTMLの`</body>`の前にコードを配置します。

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

1. Marketoでスマートリストを作成し、ビデオのURLと「クエリ文字列に含まれる」の値として探しているビューイベントを指定します。 YouTube Iframe APIについて詳しくは、[YouTubeのAPI ドキュメント ](https://developers.google.com/youtube/iframe_api_reference)を参照してください。 Munchkinについて詳しくは、[Marketo開発者向けドキュメント ](/help/javascript-api/lead-tracking.md)を参照してください。

投稿日：_2015-02-02_ by _Murta_

## Marketo SOAP APIに関するヒントとテクニック

注：これはゲストブログの投稿です。[Ed Blachmanは、[TIBCO Softwareのシニアアーキテクト ](https://www.linkedin.com/uas/login?session_redirect=https%3A%2F%2Fwww.linkedin.com%2Fprofile%2Fview%3Fid%3D2777965)で、エンタープライズソフトウェアの有名なベンダー](https://exchange.adobe.com/apps/browse/ec?product=MRKTO)です。 Edは、Gartnerが「市民開発者」と呼ぶものを、プログラミング自体を行うことなく、使用するクラウドサービスを統合できる製品に取り組んでいます。[MarketoのSOAP API](/help/soap-api/soap-api.md)は、開発者がMarketoの機能を活用し、自社のアプリケーションと統合できる強力なツールです。 [公式ドキュメント ](./getting-started.md)と[ コミュニティリソース ](https://nation.marketo.com/)の間には、その使用方法に関する多くの情報があります。 私は最初この情報に大きく依存していましたが、非常に貴重なものでした。 しかし、そのプロセスで、私はそれらの場所では見られないいくつかのヒントとコツを構築しました。 私が導き出した結果の一部をご紹介します。

**The Developers&#39; Sandbox** サンドボックスは、もちろん、API開発者にとって素晴らしい資料です。組織の実際のMarketo ユーザーが実行するマーケティングアクティビティを妨げることなく、Marketoの機能を試したり、オブジェクトを追加したり削除したりできる安全な場所です。 ただし、サンドボックスは万能ではありません。
例えば、サンドボックスを別の開発グループと共有する必要があり、サンドボックスを所有しているという考え方に慣れていたので、これには少し時間がかかりました。 最終的に、共有に関するベストプラクティスをいくつか考え出しました。- サンドボックスの内容に関する完全な知識に依存するテストを書かないでください。 共有リソースとして、スキーマは予告なく変更される可能性があります。また、リードデータベースやプログラムなどのエンティティのエントリ全体も変更される可能性があります。 テストでサンドボックスに関する完全な知識を前提としている場合、開発サイクルでは、サンドボックスを共有しているグループに対してブラックアウト期間が発生します。 通常、開発サイクルは企業と一致しないため、リソースを過剰に消費することになります。 また、それを踏まえたうえで。 - リード、リードスキーマフィールド、プログラムなど、すべてのものにラベルを付けるには、規則を使用します。 自分のオブジェクトを特定でき、自分のオブジェクトを他のオブジェクトに残すという共同テナントに同意できる場合は、共有のための強固な基盤に基づいています。 リードの場合は、カスタムフィールドを作成し、このカスタムフィールドを使用して規則を作成して、これらのリードをテストリードとして識別できます。 リストまたはプログラムの場合、オブジェクトの名前を、自分に属するオブジェクトを識別する文字列で開始できます。  – 最初に興味のあるオブジェクトを作成し、次にアクセスするか更新するか、選択して削除し、最後にそれらを削除する、自分自身の後にクリーンアップするテストを書くことを検討してください。 （SOAP APIでは、サンドボックス内のすべての要素、または実際のインスタンスでSOAP APIを介して管理できるわけではないため、これは100%達成可能ではないことに注意してください。 それでも、できる限りそれを行うことは価値があることだと思います。

**リアルインスタンス** サンドボックスの問題は、実稼動環境で使用されていないことです。そのため、Marketo インスタンスでの実際の使用状況を把握するのが困難です。 さて、運よくMarketoのパワーユーザーを持っている場合や、Marketoの内部ユーザー向けにカスタムメイド開発を行っている場合は、それほど問題はありません。 しかし、私のチームの場合、それは確かに多くのことでした。 Marketoのエキスパートは私たちの誰もいませんでした。多くのクラウドサービスを理解するよう求められていたため、エキスパートになるための人材が不足していました。 以下に、実際のインスタンスへのアクセスから得られたインサイトを示します。 – 大規模なリードスキーマ。 アクセスした実稼動インスタンスのリードスキーマには、200を超えるフィールドがあります。 これにより、UI デザイナーは、デザインするUIがそのサイズ（またはそれ以上）のスキーマに対応する必要があることが明確になりました。 - バーストの使用状況。 「最も高い利用時間と低い利用時間の間に（作成または更新されたリード数の点で）大きさの2つの違いが見られました。 これは、API呼び出しから返されるデータの量（明白）と、API呼び出しが応答するのにかかる時間（明らかではない可能性があります）の両方に影響を与えました。

**API呼び出し応答時間**&#x200B;時間帯、API呼び出しの詳細、インスタンスの内容によっては、SOAP APIの応答時間が平均よりも長くなる場合があります。 時折、API呼び出しが発生し、応答に1分半かかりました。 あなたはそれに対処する可能性を認識する必要があります：- テスト。 使用する上で問題にならないかもしれません。 しかし、それを想定するのではなく、テストをおこないます。  – 使用状況を調整します。 私たちの場合、最大の問題は、呼び出しのページサイズを[getMultipleLeads](/help/soap-api/getmultipleleads.md)に設定し、APIが許可する大きさにすることでした。 お客様のAPI割り当てを可能な限り効率的にすることが目標であるため、この点は一定の意味を持ちます。 しかし、コンテキストでは、ユーザーのAPI呼び出しクォータについて強く心配する必要はないかもしれません。その場合、データの小さいページを求めることで、確実に応答時間が向上します。

**リードパーティション設定** Marketoには、複数のマーケティンググループが1つのMarketo インスタンスを共有できる強力なツールであるパーティションとワークスペースが用意されています。 ただし、これらのツールは、SOAP APIに直接反映されるわけではありません。 例えば、getMultipleLeadsを使用して、特定の日付以降に更新または作成されたすべてのリードを取得する場合、特定のリードを含むパーティションまたはワークスペースを無視して（そして何も示さずに）、インスタンス内のすべてのリードを取得します。 リードの作成とリストへのリードの追加は、リードのパーティション化がAPI呼び出しの実際の動作に影響を与える可能性があるその他のコンテキストです。 これは、パーティションとワークスペースが、上記のサンドボックス共有の問題に必要な解決策ではない可能性があることに注意してください。 では、どうすればこれが自分の課題なのでしょうか？ 開発者エバンジェリストは、APIの使用に成功することにコミットしており、質問がある場合は、回答を見つけるのに驚くほど優れています。 - [API ドキュメント ](./getting-started.md)。 この問題は既に一部のドキュメントに取り入れられており、当社の成功への取り組みの一環として、ドキュメントの更新に非常に熱心です。  – 独自のテストケース。 パーティションとワークスペースを使用してサンドボックスを共有することは良いアイデアではないかもしれませんが、サンドボックスは、パーティションとワークスペースを使用して、意図した使用に課題をもたらすかどうかを把握するのに最適な場所です。 （また、伝道者に対する質問を絞り込むのも良い方法です。これは常に良いアイデアです。）

**TIMTOWTDIとテスト** 「これを行うには複数の方法があります」。Perl プログラミングのモットーは、特定のコンテキストでMarketo SOAP APIに実際に適用されます。 たとえば、リードのセットを更新することと、そのリードをリストに追加することを組み合わせたいとします。 SOAP APIは、次の2つの方法で実行できます。1. [importToList](/help/soap-api/importtolist.md) + [getImportToListStatus](/help/soap-api/getimporttoliststatus.md)。 ドキュメントを読むと、これは明らかにこれを行うための「通常の」方法です。 しかし、インポート操作のステータスを調査する必要があるという事実は、私にとって黄色いフラグを上げました。 インポートを実行する際に、これは本当に必要な方法だったのか？ 1. [syncMultipleLeads](/help/soap-api/syncmultipleleads.md) + [listOperation](/help/soap-api/listoperation.md)。 これは、単一のimportToList呼び出しよりもはるかにエレガントではないように思えますが、ポーリングには依存しません。 実現可能な選択肢だったのか？ このようなケースはエバンジェリストが対処するのは難しいので、対処しているインスタンスの性質とあなたが何をしようとしているかによって本当に異なります。 幸いなことに、堅牢な単体テスト環境を設定していれば、このような質問にも対応できるはずです。 この特定のケースでは、ポーリングのためではなく、importToListにフィールド指向の制限を設けたため、また、私が制御できないコンテキストやインスタンスで使用できるコードを書こうとしていたため、オプション 2がオプション 1よりも私のユースケースに適していることが判明しました。 しかし、ユースケースは異なるかもしれません。テストは、それを把握する唯一の方法です。

**結論**&#x200B;私はこれらのいずれも巨大な秘密ではないと思います。 一方、もし私が始める前にこれをすべて知っていれば、私はゲームの前に行っていただろう。 皆さんのお役に立てば幸いです。

投稿日：_2015-02-05_ by _David_

## BoomiでのMarketo REST APIの使用：静的リストからのリードの取得と削除

このシリーズのパート 1では、Boomi HTTP コネクタを使用してBoomiを介してREST APIを使用し始める方法、特にREST APIにアクセスするために必要な認証トークンを取得し、それをプロセス変数に保存する方法について説明しました。 次に、Marketoへの呼び出しを開始します。この記事では、[ リスト IDで複数のリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)する方法と[ リストからリードを削除](/help/rest-api/lead-database.md)する方法について説明します。 リストからリードを取り除くことには特に注意を払います。私がリストにアクセスしたときに展開するBoomiの非常に「軽く文書化された」微妙な側面があります。

「次の記事では、この機能を拡張して、リードのアクティビティを取得するなどの興味深いことをおこなっていますが、これは別の日のブログです。 この記事では、2つ目と3つ目の強調表示された領域について説明します。 レビューとして、以下に必要なJSON応答を含めました。 BoomiでJSON プロファイルを作成するには、JSON タイプのプロファイルコンポーネントを作成し、「インポート」をクリックしてファイルを選択するだけです。 Boomiが残りの部分を処理し、複数のIDを許可する必要があるかどうかなどを予測します。 [ リスト IDで複数のリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)のJSONの例

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

[ リスト要求からリードを削除](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE)のJSON例

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

[ リスト応答からリードを削除](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE)のJSON例

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

リスト IDで複数のリードを取得**前の記事で定義したのと同じ接続を使用して、プロセスに別のコネクタ（Get）をドロップします。 「リスト IDで複数のリードを取得する」という新しい操作を作成します（私は一貫性のためのステッカーです）その属性は次のとおりです – リクエストプロファイル：なし（これはリクエスト URLを使用します） – 応答プロファイルタイプ：jSON – 応答プロファイル：上記の「リスト IDで複数のリードを取得する」応答に基づいて新しいプロファイルを作成します。 リストされているフィールドだけでなく、必要なフィールドを返すように変更できます。 JSON応答プロファイルは、REST APIから要求するフィールドのリストと本当に一致する必要があり、必要なフィールドのみをリクエストする必要があることを覚えておくことが重要です。 プロセスプロパティオブジェクトでは、RESTで返すフィールドのコンマ区切りリストである「fields」というプロパティを定義しました。 それがプロファイルと一致する必要があるリストです。 Content Type: text/plain （これは単なるURL リクエストです） HTTP Method: GET （これはREST API ドキュメントで検索します。常にリストされます） Resource Path （add 5） rest/v1/list/ listID （replacement variable） /leads.json?access_token= access_token （replacement variable） &amp;fields= fields （replacement variable）。 次に、コネクタの「パラメーター」タブで、以前にプロセスプロパティに入力した変数値を入力できます。 次のセクションでは、これらを手動で入力しない方法について説明します。 「リスト IDで複数のリードを取得」の応答をフラットファイルプロファイルにマッピングするプロセスの部分をスキップし、それが簡単なBoomi機能であるため、FTP サーバーに固定します。

リストからリードを削除します。これは興味深いことです。同僚の一人である[Niwa](https://www.linkedin.com/uas/login?session_redirect=https%3A%2F%2Fwww.linkedin.com%2Fprofile%2Fview%3Fid%3D7429494)さんが次のテクニックを教えてくれました。これは、以下に示す「RESTful アプリケーションのPOST リクエストを作成する方法」というタイトルのBoomi記事に基づいた、とても便利なテクニックです。  しかし、まずは最初のものです。 プロセスでは、「リスト IDで複数のリードを取得」から取得します。リスト IDで複数のリードを取得する応答シェイプがあり、マッピングがかなり簡単で、元のリストのリードから取得したIDをdelete jSONに渡すID リストにマッピングするだけです。 次に、同じ接続を使用して「送信」アクションを持つ別のコネクタをドロップします。「リスト要求からリードを削除」という新しい操作を作成します。 属性は次のとおりです。Request Profile: jSON Content Type: application/json Request Profile: [JSON Profile] Remove Leads from List Request （上記のファイルから作成） Response Profile Type: jSON Response Profile: [JSON Profile] Remove Leads From List Response （上記のファイルから作成） Content Type: application/json HTTP Method: DELETE Resource Path （add 4） rest/v1/lists/ listID （replacement variable） /leads.json?access_token= access_token （replacement variable） Here&#39;s the interesting thing about this connector. コネクタタブにパラメーターを明示的に追加するつもりはありません。 代わりに、記事に記載されているように、置換変数と同じ名前の動的ドキュメントプロパティを作成します。 この場合、これらの変数はlistIDとaccess_tokenです。 これを行うと、jSONのシェイプがREST呼び出しに流れ込み、パラメーターがURL上の適切な場所に表示されます。 これはGETのPOSTではないため、前の呼び出しでは実行できません。 この時点で、GETとPOST REST API呼び出しが表示され、これらのREST呼び出しを行うためのパターンを確認できます。 次の記事では、REST APIを介したリードアクティビティの書き出しについて説明します。

投稿日：_2015-02-06_ by _John_

## Marketoのランディングページへのリードトラッキング付きYouTube ビデオの埋め込み

以前のブログ記事では、YouTubeの特定の動画に対するリードの開始点や終了点にもとづいて、Marketoでリードをセグメンテーションする方法について説明しました。 この記事では、Adobe Marketoのランディングページで、その記事の実装方法を説明します。

1. 新しいランディングページを作成するMarketoのプログラムに移動します。 「新規ローカルアセット」をクリックし、「ランディングページ」をクリックします。
1. ランディングページに名前を付けます。 ページ URLを割り当てます。 テンプレートを選択します。 「Create」をクリックします。
1. ランディングページを作成したら、「ドラフトを編集」をクリックします。
1. 右側のパネルから、「HTML」ボタンを左側のメインキャンバスにドラッグします。
1. ポップアップ表示されるカスタムHTMLエディターボックスで編集します。 「Save」をクリックします。
1. ボックスのアウトラインをドラッグして、HTML要素のサイズを調整します。 次に、「承認して閉じる」をクリックします。
1. 「承認済みページを表示」をクリックして、ランディングページのライブバージョンをテストします。 YouTubeを含むランディングページが新しいウィンドウで開きます。 開始および終了したビデオは、以下の1番目と2番目のスクリーンショットに示すように、リードのアクティビティログに表示されます。 Marketoにデータを取り込んだら、スマートリストを作成し、動画の開始または終了したリードをセグメント化できます（下のスクリーンショットを参照）。 YouTube Iframe APIについて詳しくは、[YouTubeのAPI ドキュメント ](https://developers.google.com/youtube/iframe_api_reference)を参照してください。 Munchkinについて詳しくは、[Marketo開発者向けドキュメント ](/help/javascript-api/lead-tracking.md)を参照してください。

投稿日：_2015-02-09_ by _Murta_

## Munchkinによるシングルページアプリケーションのweb トラッキング

シングルページアプリケーションとは、最初のページ読み込み時にサイトをナビゲートするために必要なすべてのリソースを読み込むweb サイトのことです。 ユーザーがリンクをクリックすると、最初のページ読み込みデータからコンテンツが読み込まれます。 アドレスバーのURLは従来のページナビゲーションと似ているので、ユーザーにとってweb サイトは期待どおりに動作します。 Munchkinは、ユーザーが新しいページを読み込むたびに実行されるため、従来のweb サイトで適切に動作します。 ただし、新しいページを読み込まない場合、Munchkinは1回だけ実行されます。 この記事では、オーディエンスがリンクをクリックしたタイミングを追跡し、その情報をMunchkinに送信する方法を解説します。 これを実装するには、`clickLink` Munchkin関数を使用します。 以下は、クリックイベントを`clickLink` Munchkin メソッドにバインドするjQueryの実装例です。 `clickLink` Munchkin メソッドを呼び出すと、クリックされたURLのパラメーターが渡されます。

```javascript
<script>
$("a").on('click', function(event) {
    var urlThatWasClicked = $(this).attr('href');
    Munchkin.munchkinFunction('clickLink', { href: urlThatWasClicked});
});
</script>
```

投稿日：_2015-02-11_ by _Murta_

## REST APIを使用したリードのスコアの変更

例えば、APIを使用してMarketoのリードのスコアを変更するとします。 これは、リードエンドポイントの作成/更新を使用してREST APIで実行できます。 以下は、この呼び出しを行う方法を示すRubyのコードサンプルです。

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

リクエストのJSON本文で、アクションとして`updateOnly`を指定します。 つまり、リクエストはリードが存在する場合にのみ機能し、そうでない場合は失敗します。 リードが存在しない場合は、`createOrUpdate`をアクションとして指定します。 Marketoでリードレコードを検索する際に、主な識別子としてリードのメールを使用します。 最後に、キー`leadScore`を使用してリードのスコアの値を指定します。 この方法を使用して、一度に300件のリードを更新できます。

投稿日：_2015-02-19_ by _Murta_

## Marketo プラットフォーム上に構築されたオープンなSource プロジェクトのハイライト：第3部

これは、開発者コミュニティによってMarketo プラットフォームを中心に構築されたオープンソースプロジェクトを取り上げたシリーズの3つ目の投稿です。 MarketoのGitHub アカウント ](https://github.com/Marketo/Community-Supported-Client-Libraries)のリストを[管理しています。このリストでは、Marketo デベロッパーコミュニティによって作成されたクライアントライブラリとプロジェクトを追跡しています。 ここでは、Marketo REST APIを中心に開発された3つのプロジェクトを紹介します。**[Usermind](http://www.usermind.com/)は、Marketo REST API](https://github.com/MadKudu/node-marketo)用に[a Node.js クライアントライブラリを作成しました。**  **[Arunim Samat](https://github.com/asamat)がMarketo REST API](https://github.com/asamat/python_marketo)用に[ クライアントライブラリをPythonで作成しました。**  Marketo](https://www.linkedin.com/in/jalemieux)の&#x200B;**[Jacques Lemieuxが、Marketo REST API用に[ クライアントライブラリをRubyで作成しました。](https://github.com/jalemieux/mkto_rest)**  Marketoプラットフォームで、開発者コミュニティによって作成されたより多くのプロジェクトを確認できることを嬉しく思います。 Marketo プラットフォームのオープンソースプロジェクトで作業している場合は、[ プルリクエストを介してこのGitHub リポジトリに送信してください](https://github.com/Marketo/Community-Supported-Client-Libraries)。

投稿日：_2015-02-20_ by _Murta_

## Marketo フォームをRTP キャンペーンに挿入する

多くのマーケターは、Marketo フォームをMarketo Real-Time Personalization（RTP）キャンペーンに配置することに関心があります。 ダイアログ、ゾーン内、またはウィジェットのRTP キャンペーンタイプのいずれでも、Form HTML コードをコピーしてRTPのキャンペーンエディターに貼り付けることができます。 例として、次のものが使用されています。 – 訪問者がサイトを2回または3回クリックした後、ニュースレターに登録できるようにする – ウェビナーの迅速かつ効果的なサインアップフォーム – ゲーテッドケーススタディのダウンロード – 過去に購読解除したリードを提供して再購読するキャンペーンにフォームに記入し、リクエストされた感謝やコンテンツを受け取ることで、目標を達成するためのクリック数が1つ減ります。 ここでは、これを行う方法と、Marketo Form 2.0をMarketo RTP キャンペーンに埋め込む方法について説明します。 以下の素晴らしい例を見てみましょう。RTP ユーザーは、さらに一歩進んで、訪問者をサンキューページに誘導する代わりに、RTP キャンペーン内にサンキューメッセージを表示することにしました。 このオプションのコードも下にあります。 楽しんで、私はそれであなたの経験について聞いて幸せです！

1. 承認済みフォームを右クリックします。 **埋め込みコードを選択してください。**
1. **コードをコピーします。**
1. Marketo RTPで、**Campaigns**&#x200B;に移動します。
1. 「**新しいキャンペーンを作成**」をクリックします。
1. リッチテキストエディターで、**HTML アイコン**&#x200B;をクリックします。
1. フォーム埋め込みコードを HTML ソースエディターにペーストします。 「**更新**」をクリックします。
1. フォームはエディタービューには表示されませんが、プレビューしてキャンペーンでのレンダリング方法を確認することができます。
1. 「**起動**」をクリックすると、キャンペーンが始まります。

### メモ

フォームの変更は、フォームの「ドラフトを編集」のMarketo マーケティングアクティビティ内で行う必要があります。

### 関連記事

* [Forms 2.0](/help/javascript-api/forms-api-reference.md)

投稿日：_2015-12-20_ by _Yanir_

## Marketo フォームへのリセットボタンの追加

```javascript
<script src="//app-sj01.marketo.com/js/forms2/js/forms2.min.js"></script>
<form id="mktoForm_116"></form>
<script>MktoForms2.loadForm("//app-sj01.marketo.com", "410-XOR-673", 116,
function(form) { form.getFormElem()[0].querySelector('button[type="submit"]').insertAdjacentHTML('afterend','<button type="reset" class="mktoButton">Reset</button>') });
</script>
```

投稿日：_2015-03-18_ by _Murta_

## 2015年3月リリースの更新

[Marketo REST Asset APIは、2015年3月リリース ](https://developer.adobe.com/marketo-apis/api/asset/)でリリースされました。 このAPIを使用すると、Marketoのファイル、フォルダー、トークン、メール、メールテンプレートオブジェクトにアクセスできます。 Asset API エンドポイントへのアクセスを提供するために、読み取り専用Assets、読み取り/書き込みAssetsの2つのロール権限が追加されました。 API ユーザーロールがAsset APIのリリースより前の場合は、これらの権限を持つ新しいAPI ユーザーロールを作成してアクセスを有効にする必要があります。 それ以外の場合は、「アクセス拒否」という603 エラー応答が表示されます。 REST Asset APIのリリースに加えて、既存のREST API エンドポイントに対する更新も行われました。 [Merge リード REST API エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/mergeLeadsUsingPOST)が更新され、複数のリードの結合が可能になりました。 キャンペーンのスケジュール中にキャンペーンを複製できるように、[ キャンペーン REST API エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST)が更新されました。

投稿日：_2015-03-23_ by _Murta_

## 遅延を伴うRTP キャンペーンのトリガー

このカスタム JavaScriptを使用すると、RTP ユーザーはweb ページが読み込まれてから数秒後にキャンペーンを表示できます。 これは、ダイアログボックスおよびウィジェットキャンペーンに推奨されます。 訪問者がページの通常のコンテンツを閲覧すると、遅延後にキャンペーンを表示するために使用できます。 このコードは、キャンペーンを表示する特定のページにのみ実装することをお勧めします。 このコードを全ページで使用することは、パフォーマンスに影響を与える可能性があるため、お勧めしません。**設定手順** カスタムコードは、RTP カスタムデータイベント （t=timeOnPage、つまりt=60）を送信し、このイベントに一致するキャンペーンを読み込みます。 デフォルトでは、60秒後にトリガーされます。 sendCustomRTPEvent パラメーターを他の任意の数値に変更することで、カスタマイズできます。 標準のRTP コードの直後にコードを配置します。

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

遅延時間の後に応答するようにRTP キャンペーンを設定するには：1. RTP アカウントにログインします1. 新しいセグメントを作成する1. セグメントイベントセクションに「`t=60`」を追加します。 訪問者は、各RTP セグメントを1 セッションにつき1回しか照合できないため、各キャンペーンは1回しか表示されません（スティッキーに設定されている場合を除く）。

投稿日：_2015-03-24_ by _Yanir_

## 2015年4月リリースの更新

### Marketo Mobile Engagement SDK v0.3.2

Marketoには、モバイルアプリ向けのマーケティングオートメーションとユーザーエンゲージメントが追加されました。 [Marketo モバイル SDK](/help/mobile/mobile.md)をiOSまたはAndroid アプリにインストールすると、マーケターはアプリ内イベントをリッスンして、関連するプッシュ通知を送信できます。

### REST APIの機能強化

* カスタムオブジェクト

Marketo カスタムオブジェクトに格納されているデータをプログラムでリスト化、記述、CRUDできる新しい[ カスタムオブジェクトエンドポイント ](/help/rest-api/custom-objects.md)が導入されました。

カスタムオブジェクト API エンドポイントへのアクセスを提供するために、役割の権限が追加されました。読み取り専用カスタムオブジェクト、読み取り/書き込みカスタムオブジェクト。 API ユーザーの役割がカスタムオブジェクト APIのリリースより前の場合は、アクセスを有効にするには、これらの権限を持つ新しいAPI ユーザーの役割を作成する必要があります。 それ以外の場合は、「アクセス拒否」という603 エラー応答が表示されます。

* キャンペーンのスケジュール – コピープログラム

新しいオプション パラメーター「cloneToProgramName」が[ スケジュール キャンペーン API](/help/rest-api/data-ingestion.md)に導入されました。 このパラメーターが存在する場合、キャンペーンの親プログラムが複製され、新しく作成されたキャンペーンがスケジュールされます。 パラメーターは、結果のプログラムの目的の名前を指定します。

投稿日：_2015-04-28_ by _Travis Kaufman_

## インスタンス間でのメール登録解除の同期

Marketoのインスタンスを複数管理していますか？ インスタンス間でリード情報を同期し続けるのは困難な場合があります。 次に、外部web サービスを呼び出すWebhookを使用して、インスタンス間でメール登録解除を同期する方法を示します。 外部web サービスは、購読解除イベントをトリガーした既知のリードを各インスタンスで検索してループします。 一致するリードが見つかった場合、対応するリードレコードの「購読解除」フィールドが更新されます。 下の図はその考えを示しています。  Web サービスを実装するのは自分の責任ですが、以下のコードは、プロセスを迅速に開始するのに役立ちます。

### 外部Web サービス

外部web サービスは、同期が必要な各Marketo インスタンスに対して次の手順を実行します。

1. インスタンス固有のREST API [ エンドポイント URL](/help/rest-api/endpoint-reference.md)を構成します
1. [ID](/help/rest-api/authentication.md)を使用してアクセストークンを取得します
1. [ フィルターの種類](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)で複数のリードを取得を使用して、メールアドレスに一致するリード レコードのリストを取得します
1. リードの作成/更新を使用して、各リードレコードの「購読解除」フィールドを更新します

次に、外部web サービス呼び出しとMarketo REST API呼び出しの詳細を示す別の図を示します。  以下のサンプルコードは、標準搭載のweb サービスではありません。 むしろ、コマンドラインを介して引数を渡すことができるコンソールモードプログラムです。 ここでの目的は、適切なMarketo APIを呼び出して、インスタンス間でリードレコードを更新する方法を示すことです。 Web サービスの実装は、読者のための演習として残されています。
**サンプルコード** サンプルコードを実行するには、お気に入りのIDEでJava プロジェクトを作成する必要があります。 その後、次の変更を加える必要があります。1. サンプルコードでは、[json-simple](https://code.google.com/archive/p/json-simple)を使用してJSON文字列を解析しています。 Java プロジェクトにjson-simple jarを追加します。 1. サンプルコードには、各Marketo インスタンスのメタデータを保持する構造があります。 インスタンスの実際の値を次のように構造に配置します。

```java
public static String instanceInfo[][] = {
{ "AccountId1", "ClientId1","ClientSecret1" },    // Instance 1 metadata
{ "AccountId2", "ClientId2","ClientSecret2" },    // Instance 2 metadata
{ "AccountId3", "ClientId3","ClientSecret3" }     // Instance 3 metadata
};
```

インスタンスのメタデータは、Marketo管理パネルで確認できます。

* Account Id Admin > Integration > Munchkin > Munchkin Account
* クライアント Idとクライアント秘密鍵の管理者/統合/LaunchPoint/メール購読解除の同期/詳細を表示

サンプルコードは、前述の外部web サービスの「id」および「email」クエリパラメーターをシミュレートする2つのコマンドライン引数を取ります。

1. args[0] = アカウント ID
1. args[1] = メールアドレス

インスタンスから実際の値を引数としてプログラムに渡します。 Intellij IDEAのプロジェクト設定のスクリーンショットを次に示します。

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

### Marketo設定

同期する各Marketo インスタンスに対して、次の手順を実行します。

1. 役割の権限を持つカスタムサービスを作成する：リードの読み取りと書き込み。 カスタムサービスの作成に慣れていない場合は、[こちら](/help/rest-api/custom-services.md)をクリックしてください。
1. 外部web サービスを呼び出すWebhookを作成します。 Webhookの作成に慣れていない場合は、[こちら](/help/webhooks/webhooks.md)をクリックしてください。
1. スマートキャンペーンでWebhookをフローステップとして追加します。

以下のスクリーンショットは、トークンを使用してクエリパラメーターを自動的に入力するために、上記で指定したサービスを呼び出すWebhookを作成する方法を示しています。 Webhookを作成したので、フローアクションとしてスマートキャンペーンに追加できます。  スマートリストには、「メールの購読解除」トリガーを含める必要があります。

### 検証

Marketoの複数のインスタンスで、同じメールアドレスを使用してリードを作成し、検証します。 メールアドレスを所有していることを確認してください。 メールを送信フローアクションをトリガーする1つのインスタンスで、結果のメールを開き、「購読を解除」をクリックします。 結果を検証するには、他の各インスタンスにログインし、メールアドレスに関連付けられているリードレコードを調べます。 「購読解除」チェックボックスをオンにし、「購読解除の理由」フィールドには、同期を開始したソースアカウント IDを含むメモを含める必要があります。

投稿日：_2015-05-11_ by _David_

## REST APIを使用したリードデータの変更の同期

その投稿には、更新を求めてMarketoに対して定期的にポーリングを実行できるコードサンプルが表示されていました。 Marketo APIを使用してリードデータの変化を特定し、変化したリードデータを抽出するというアイデアでした。 このデータは、同期目的で外部システムにプッシュできます。 提示されたコードサンプルは、SOAP APIを使用していました。 [新しい歩き方](https://www.youtube.com/watch?v=G-7ZJjLy5D8&feature=youtu.be)があり、その方法は[Marketo REST API](/help/rest-api/rest-api.md)を使用しています。 この記事では、2つのREST エンドポイントを使用して同じ目標を達成する方法について説明します。[ リードの変更を取得](/help/rest-api/rest-api.md)、[ リードのIDを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)。 このプログラムには、主に2つのステップが含まれています。

1. 「リードを取得」を呼び出すと、特定のリードフィールドが変更されたか、特定の期間に追加されたすべてのリード IDのリストが生成されます。
1. リスト内の各リード IDのリード IDを取得を呼び出して、リードレコードからフィールドデータを取得します。

手順2で取得したデータを、外部システムで使用できるようにフォーマットします。  **プログラム入力**&#x200B;既定では、プログラムは現在の日付から1日戻って変更を探します。 たとえば、このプログラムを毎日同じ時間に実行できます。 さらに時間を遡るには、コマンドライン引数として日数を指定することで、時間ウィンドウを効果的に増やすことができます。 プログラムには、次の変更が可能な複数の変数が含まれています。CUSTOM_SERVICE_DATA – これには、Marketo [ カスタムサービス ](/help/rest-api/custom-services.md) データ（アカウント ID、クライアント ID、クライアントシークレット）が含まれます。 LEAD_CHANGE_FIELD_FILTER – これには、変更を検査するリードフィールドのコンマ区切りリストが含まれます。 READ_BATCH_SIZE – 一度に取得するレコードの数です。 これを使用して、ボディサイズに合わせて応答を調整します。**プログラム出力** プログラムは、変更されたすべてのリードレコードを収集し、次のようにリードオブジェクトの配列としてJSONにフォーマットします。

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

つまり、このJSONをリクエストペイロードとして外部web サービスに渡して、データを同期させることができるということです。**プログラムロジック**&#x200B;まず、時間ウィンドウを確立し、REST エンドポイント URLを構成し、認証アクセストークンを取得します。 次に、「Get Paging Token/Get Lead Changes」ループを起動します。このループは、リードの変更の供給が終了するまで実行されます。 このループの目的は、一意のリード IDのリストを蓄積して、プログラムの後半でリード IDを取得するためにそれらを渡すことができるようにすることです。 この例では、「リードの変更を取得」に対して、firstName、lastName、emailのフィールドの変更を確認するように指示しています。 目的に合わせてフィールドの組み合わせを自由に選択できます。 Get Lead Changesは、Activity Type Idを含む「result」オブジェクトを返します。これを使用して結果をフィルタリングできます。 注意：[ アクティビティタイプを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getAllActivityTypesUsingGET) REST エンドポイントを呼び出すことで、アクティビティタイプのリストを取得できます。 返される2つのアクティビティタイプに興味があります：1. 新しいリード （12）

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

1. データ値の変更（13） データ値の変更レスポンスの「name」プロパティを調べることで、変更されたフィールドを把握できます。

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

これらの2種類のアクティビティのいずれかが返された場合、関連付けられたリード IDはリストに保存されます。 リストができたら、各項目の「Get Lead by Id」というタイトルで繰り返し処理します。 これにより、リストの各リードの最新のリードデータが取得されます。 この例では、`leadId`、`updatedAt`、`firstName`、`lastName`、および`email`のリードフィールドを取得します。 目的に合わせてフィールドの組み合わせを自由に選択できます。 これは、「IDでリードを取得」にフィールドパラメーターを指定することによって実行します。 最後に、上記のように、結果をリードオブジェクトの配列としてJSONifyします。

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

これで終わりです。[人生は幸せな歌です](https://www.youtube.com/watch?v=zFaBwZDywLk)。 これで、お試しいただくことができます。

投稿日：_2015-07-31_ by _David_

## 2015年5月リリースの更新

### REST API

* 商談API: Marketo オポチュニティオブジェクト内のデータをプログラムでリスト化、記述、CRUDできる新しい[ オポチュニティエンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities)が導入されました。

注意：商談エンドポイントへのアクセスを提供するために、役割の権限が追加されました：読み取り専用の商談、読み取り/書き込み商談。 API ユーザーの役割が商談APIのリリースよりも前の場合は、これらの権限を持つ新しいAPI ユーザーの役割を作成してアクセスを有効にする必要があります。 それ以外の場合は、「アクセス拒否」という603 エラー応答が表示されます。

* アセット API - スニペット。 スニペット ](https://developer.adobe.com/marketo-apis/api/asset/#snippet_endpoints)の新しい[ アセットエンドポイントが導入され、スニペットオブジェクトをプログラムで操作できるようになりました。 スニペットは、メールやランディングページの動的コンテンツブロックとして使用できます。
* リード API - リード パーティションを更新します。 パーティション ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/updatePartitionsUsingPOST)の新しい[ リードエンドポイントが追加され、1つ以上のリードのパーティションを更新できるようになりました。
* 「createdAt」および「updatedAt」属性にリード関連APIのタイムゾーンオフセットが見つからない問題を修正しました。
* 1日の最大呼び出し数を超えた場合に、スケジュール キャンペーンで適切なエラーコードが返されない問題を修正しました。
* 「親」属性と「説明」属性に対してGet Folder by Idがnullを返すことがある問題を修正しました。
* 特定のケースで「電子メールをIDで承認」がシステムエラーになる問題を修正しました。
* フォルダーIDでトークンを作成すると、特定のケースで使用できないトークンが生成される問題を修正しました。

### Real-Time Personalization（RTP）

* リッチメディア推奨API。 新しい[ リッチメディアのレコメンデーション ](/help/javascript-api/web-personalization.md)機能がRTP JavaScript APIに追加されました。 リッチメディアコンテンツレコメンデーションは、マシンラーニング（機械学習）と予測分析を利用して、web訪問者に最適なコンテンツを提供します。 テキストの説明や画像でコンテンツアセットを強化し、web サイトに複数のコンテンツレコメンデーションを埋め込むことができます。

### Mobile Engagement SDK

iOS v0.3.4/Android v0.3.3

* カスタムアクション： カスタムアクションを送信して、ユーザーのインタラクションを追跡する機能を追加しました。 詳しくは、「カスタムアクションの送信」を参照してください[ここ](/help/mobile/mobile.md)。
* trackPushNotification メソッドは廃止されました。

投稿日：_2015-05-26_ by _David_

## 2015年6月リリースの更新

### REST API

* 会社 API

Marketo company オブジェクト内のデータをプログラムでリスト化、記述、およびCRUDできる新しい[会社エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies)が導入されました。

注意：プログラムエンドポイントへのアクセスを提供するために、役割の権限が追加されました：読み取り専用の会社、読み取り/書き込み会社。 API ユーザーの役割が会社APIのリリースよりも前の場合は、アクセスを有効にするには、これらの権限でAPI ユーザーの役割を更新する必要があります。 それ以外の場合は、603 「アクセス拒否」エラー応答が表示されます

* Asset API - プログラム

アプリケーションフォルダーとプログラムフォルダーの両方をサポートするようにAsset APIを更新しました。 複数のアセット APIが、リクエストのフォルダーIDを整数の形式で受け入れていました。 フォルダーIDは、APIに応じて、URIの一部またはリクエスト本文の一部として渡すことができます。

次に、フォルダーIDと一緒にフォルダータイプを指定する必要があります。 フォルダータイプは「プログラム」または「フォルダー」です。 「フォルダー」はアプリケーションフォルダーを、「プログラム」はプログラムフォルダーを指定します。 フォルダータイプは、呼び出すAPIに応じて、次の2つの異なる方法で指定されます。

1. 「FolderIdType」データ構造を使用します。 FolderIdTypeは、IDとタイプ ペアを含むシンプルなJSON ブロックです。

`{ "id" : **id**, "type" : "**type**" }`

ここで、**id**&#x200B;はフォルダーIDで、「**type**」はフォルダータイプです。 「**type**」に使用できる値は「フォルダー」または「プログラム」です。

例 – フォルダーを作成

`POST /asset/v1/folders.json`

`parent={"id":416,"type":"Folder"}&name=Test Folder&description=This is a test folder`

1. 既存のID パラメーターを使用し、「type」クエリパラメーターを使用してタイプを指定します。

例 – IDによるフォルダーの取得

`GET /rest/asset/v1/folder/1016.json?type=Program`

結果オブジェクトにフォルダーIDが含まれていたAPI応答には、値がFolderIdTypeであるfolderId属性も含まれるようになりました。 これは、特定のフォルダーIDのフォルダータイプを決定するために使用できます。

例：名前でフォルダーを取得

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

特定のIDのフォルダーの種類を判断するには、[ フォルダーを参照](https://developer.adobe.com/marketo-apis/api/asset/browse-folders/) APIを使用します。

API応答の「type」属性の名前が「folderType」に変更されました。 これは、FolderIdTypeに含まれる「type」要素との混同を避けるためです。

例えば、次のように指定します。

「**type**」:「Marketing Folder」

を次のように変更します。

&quot;**folderType**&quot;: &quot;Marketing Folder&quot;

### Mobile Engagement SDK

iOS 0.3.5

* テストデバイスの設定ダイアログがメインスレッドで実行されていた問題を修正しました。[MOB-638]
* テストデバイスの登録に失敗した場合のエラー処理を追加しました。[MOB-639]

Android 0.3.3

* AndroidManifest.xml `<activity>`要素にandroid:configChanges属性を追加しました。これにより、テストデバイスを追加して向きを変更した際に、進行状況ダイアログが閉じるのを防ぐことができます。[MOB-687]

投稿日：_2015-06-30_ by _David_

## RTP APIを使用したアプリ内Web Personalization（Beta）

アドビのお客様の中には、お客様にweb アプリソリューションを提供しているお客様もいますが、セキュリティで保護されたweb アプリ環境内でMarketo Real-Time Personalization（RTP）を使用できる場合は、リクエストを受け取ります。 答えは「イエス」です！ アプリ内メッセージ用のAPIをリリースしました。これにより、コンテンツをパーソナライズし、web アプリのデータにもとづいて、ウェビナー、新機能リリース、アップセルなどのマーケティング活動を宣伝したり、オーディエンスをエンゲージしたりできます。 例えば、次のようなアプリ内コンテンツのパーソナライズを行います。

* ユーザーのアクティビティに基づく体験版オファー
* 様々なサブスクリプションタイプ（アップセル、クロスセル、ウェビナーのトレーニング）
* ユーザーアクティビティに関連する新機能

**ユースケース例** Marketo カスタマーサクセス チームは、アプリ内Web Personalizationを使用して、特定のサブスクリプションタイプ（Spark、Standard、Select、Enterprise）とパーソナライズされたコンテンツでコミュニケーションし、プログレッシブキャンペーンを確認し、エンゲージメントに基づいてアプリ内ユーザーを育成しています。 Enterprise サブスクリプションの種類を持つユーザーに対してこれを実行する方法を見てみましょう。**前提条件** [RTP ユーザーコンテキスト API](/help/javascript-api/web-personalization.md)について理解します。**Marketo サポートからのUser Context API** リクエストを有効にして、RTP アカウントのUser Context APIを有効にします。**カスタム変数を設定** RTPでデータの送信先として使用できるカスタム変数スロットは5つあります。 この例では、ユーザー購読タイプ Enterpriseをカスタム変数1に送信します。

`rtp('set', 'customVar1', 'Enterprise');`

**新しいRTP セグメントを作成** **セグメント**&#x200B;に移動し、**新規作成**&#x200B;をクリックします。

1. **ユーザーコンテキスト API** フィルターをセグメントビルダーにドラッグします。
1. **value**&#x200B;が&#x200B;**Enterprise**&#x200B;である&#x200B;**カスタム変数1** （サブスクリプションタイプ）を選択します。

**以前の訪問履歴に基づくキャンペーンを表示**&#x200B;以前の訪問で既にキャンペーンをクリックした訪問者に別のキャンペーンを表示します。

1. **ユーザーコンテキスト API**&#x200B;内で、**（+）**&#x200B;をクリックして、別のユーザーコンテキスト API属性を追加します
1. **演算子（ANDまたはOR）を追加します。**
1. 「**キャンペーン – クリック済み」を選択します。** **キャンペーン ID**&#x200B;をキャンペーンのIDに設定します。 （Campaign IDの検索方法については、以下のメモを参照してください）。
1. 「**SAVE &amp; DEFINE CAMPAIGN**」をクリックして、キャンペーンクリエイティブを作成します。

全体として、このセグメントは、訪問者がEnterpriseと同じカスタム変数（サブスクリプションタイプ）に関連付けられている場合と、以前の訪問でキャンペーン（ID:5390）をクリックした場合に一致します。 次のステップは、このセグメントにパーソナライズされたキャンペーンを定義することです。 下のスクリーンショットは、My Marketo ページに表示されるRTP ダイアログキャンペーン（左下）を示しています。  **メモ：** **キャンペーン IDの検索** **キャンペーン**&#x200B;に移動し、**キャンペーン名**にカーソルを合わせてキャンペーン IDを検索します。
投稿日：_2015-06-17_ by _David_

## Marketo REST APIを使用したトランザクションメールの送信：パート 1

Marketo REST API を使用して必要な呼び出しを実行するには、Marketo にいくつかの設定要件があります。

* .受信者は、Marketo 内にレコードを持っている必要があります。
* Marketo インスタンスで作成および承認されたトランザクションメールがある必要があります。
* Campaignがリクエストされたアクティブなトリガーキャンペーン、Source:Web サービス APIが必要です。これは、メールを送信するように設定されています

最初に[メールを作成して承認します](https://experienceleague.adobe.com/ja/docs/marketo/using/home)。 電子メールが真にトランザクション的なものである場合は、それを業務的に設定する必要がある可能性が高いですが、法的に業務的なものとして認められることを確認してください。 これは、メールアクション/メール設定の編集画面で設定します。 キャンペーンを作成する準備が整いました。 キャンペーンの作成を初めて行う場合は、docs.marketo.comの「[新しいスマートキャンペーンの作成](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/creating-a-smart-campaign/create-a-new-smart-campaign)」の記事をご覧ください。 キャンペーンを作成したら、次の手順に従う必要があります。 Campaignがリクエストされたトリガーでスマートリストを設定します。次に、メールを送信ステップをメールにポイントするようにフローを設定する必要があります。 アクティベーションの前に、「スケジュール」タブで設定を決定する必要があります。 この特定のメールを特定のレコードに 1 回だけ送信する場合は、選定の設定はそのままにしておきます。 しかし、複数回メールを受け取る必要がある場合は、毎回または利用可能なケイデンスのいずれかに調整することをお勧めします。 次に、アクティブ化の準備が整います。

### API 呼び出しの送信

**注：**&#x200B;以下のJavaの例では、コード内のJSON表現を処理するためにminimal-json パッケージを使用しています。 このプロジェクトの詳細については、こちらをご覧ください。[https://github.com/ralfstx/minimal-json](https://github.com/ralfstx/minimal-json) APIを介してトランザクションメールを送信する最初の部分は、対応するメールアドレスを持つレコードがMarketo インスタンスに存在し、そのリード IDにアクセスできることを確認することです。 この記事では、メールアドレスが既にMarketoにあることを前提としており、レコードのIDを取得するだけで済みます。 このために、フィルタータイプ ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)呼び出しで[複数のリードを取得するを使用しており、以前の投稿のJava コードの一部を再利用しています。 キャンペーンをリクエストするための主な方法を見てみましょう。

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

leadsRequestのJsonObject応答からこれらの結果を取得するには、いくつかのコードを記述する必要があります。 配列の最初の結果を取得するには、JsonObjectから配列を抽出し、0でインデックス付けされたオブジェクトを取得する必要があります。

`JsonArray leadsResult = leadsRequest.getData().get("result").asArray();`
`int leadId = leadsResult.get(0).asObject().get("id").asInt();`

ここからは、リクエストキャンペーンの呼び出しだけです。 これには、リクエストの URL 内の ID と、1つのメンバー &quot;id&quot; を含む JSON オブジェクトの配列が必要です。 このコードを見てみましょう。

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

このクラスには、Auth とキャンペーンの ID を受け取る 1 つのコンストラクターがあります。 リードは、setLeadsにレコードのIdを含むArrayList `<Integer>`を渡すか、addLeadを使用してオブジェクトに追加されます。これは、1つの整数を取り、leads プロパティの既存のArrayListに追加します。 API呼び出しをトリガーしてリードレコードをキャンペーンに渡すには、postDataを呼び出す必要があります。これは、リクエストの応答データを含むJsonObjectを返します。 リクエストキャンペーンが呼び出されると、呼び出しに渡されたすべてのリードは、Marketoのターゲットトリガーキャンペーンによって処理され、以前に作成されたメールが送信されます。 これで、Marketo REST API を使用してメールをトリガーしました。 リクエストキャンペーンを通じてメールのコンテンツを動的にカスタマイズするパート 2に注目してください。

投稿日：_2015-07-17_ by _Kenny_

## REST APIを使用したMarketoからのリードデータの認証と取得

**注：**&#x200B;以下のJavaの例では、コード内のJSON表現を処理するためにminimal-json パッケージを使用しています。 このプロジェクトの詳細については、こちらをご覧ください。[https://github.com/ralfstx/minimal-json](https://github.com/ralfstx/minimal-json) Marketoと統合する際の最も一般的な要件のひとつは、リードデータの取得です。 ほとんどの場合、すべての統合でMarketo サブスクリプションからリードデータの取得または送信が必要になるわけではないので、本日は、サブスクリプションで[認証](/help/rest-api/authentication.md)し、その後リードデータを取得するという基本的なリード情報取得タスクを見ていきます。 リードを取得するには、まずOAuth 2.0を使用してターゲットのMarketo インスタンスで認証する必要があります。 Marketoで認証する必要がある情報は、クライアント ID、クライアントシークレット、Marketo インスタンスのホストの3つです。 以下は、認証に使用するクラスです。

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

このコードを使用すると、Admin -> Launchpoint （IDおよびSecret）およびAdmin -> Web Services （Host）から、クライアント ID、クライアントシークレット、およびホスト（marketoInstance）を使用してAuthのインスタンスを作成できます。 現在保存されているトークンがnullか期限切れかをテストし、既存のトークンを返すか、新しい認証リクエストを作成してから、JSON応答の「access_token」メンバーから新しいトークンを返すgetToken メソッドを公開します。 Marketoインスタンスで認証できたので、次のステップはリードを取得することです。 私たちはこのクラスを使用しています：

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

このクラスには、Auth オブジェクトを受け入れる1つのコンストラクターがあり、オプションと必須の両方のパラメーターに対して複数のセッターを公開します。 この場合、filterTypeとfilterValuesを設定して、メールアドレスによるリードの取得を実行することにのみ注意が必要です。 そこで、「email」にはsetFilterTypeを使用し、IDを取得する必要があるメールアドレスにはaddFilterValueを使用します。 パラメーターを設定したら、getData メソッドを使用して、取得したリードレコードのJSON表現を持つ結果配列を含むリードエンドポイントからJsonObjectを取得できます。

### まとめ

これで、使用しているサンプルコードを理解できました。テスト用メールアドレス <testlead@marketo.com>に一致するリードを取得する簡単な例を見てみましょう。 この場合、「email」にはsetFilterTypeを使用し、情報を取得する必要があるメールアドレスにはaddFilterValueを使用する必要があります。 パラメーターを設定したら、getData メソッドを使用して、取得したリードレコードのJSON表現を持つ結果配列を含むリードエンドポイントからJsonObjectを取得できます。

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

このメインメソッドの例では、Authのインスタンスを作成し、これを新しいリードコンストラクターに渡します。 setFilterTypeとaddFilterValueを使用して、リードのインスタンスを設定し、電子メールアドレス「<testlead@marketo.com>」に一致するリードのみを取得します。 次の例では、これをコンソールに出力します。

トークンが空または期限切れです。 新しい認証を試しています
<https://299-BYM-827.mktorest.com/identity/oauth/token?grant_type=client_credentials&client_id=b417d98f-9289-47d1-a61f-db141bf0267f&client_secret=0DipOvz4h2wP1ANeVjlfwMvECJpo0ZYc>を使用した認証を試みます
認証応答を取得しました：{&quot;access_token&quot;:&quot;ec0f02c0-28ac-4d6c-b7d7-00e47ae85ff1:st&quot;,&quot;token_type&quot;:&quot;bearer&quot;,&quot;expires_in&quot;:538,&quot;scope&quot;:&quot;<apiuser@mktosupport.com>&quot;}
{&quot;requestId&quot;:&quot;14fb6#14e6a7a9ad6&quot;,&quot;result&quot;:[{&quot;id&quot;:1026322,&quot;updatedAt&quot;:&quot;2015-07-07T21:43:25Z&quot;,&quot;lastName&quot;:&quot;Lead&quot;,&quot;email&quot;:&quot;<testlead@marketo.com>&quot;,&quot;createdAt&quot;:&quot;2015-07T21:43:25Z&quot;,&quot;firstName&quot;:{&quot;}} :1026323,&quot;updatedAt&quot;:&quot;2015-07-07T21:43:43Z&quot;,&quot;lastName&quot;:&quot;Lead2&quot;,&quot;email&quot;:&quot;<testlead@marketo.com>&quot;,&quot;createdAt&quot;:&quot;2015-07-07T21:43:43Z&quot;,&quot;firstName&quot;:&quot;Test&quot;}],&quot;success&quot;:true}

今では、必要に応じて処理できるリードデータがあります。 ご意見をお寄せいただきありがとうございます。コメントにフィードバックを残してください。

投稿日：_2015-07-10_ by _Kenny_

## 2015年7月リリースの更新

REST API

* セールス担当者API

Marketoの営業担当者オブジェクト内にあるデータをプログラムでリスト化、説明、およびCRUDできる新しい[営業担当者エンドポイント ](/help/rest-api/sales-persons.md)が導入されました。 さらに、セールス担当者は、リード、オポチュニティ、企業に割り当てることができます。 これは、リード、商談、または会社のCreate/Update/Upsert エンドポイントを呼び出す際に、「externalSalesPersonId」属性を指定することで行います。

注意：プログラムエンドポイントへのアクセスを提供するために、役割の権限が追加されました：読み取り専用セールス担当者、読み取り/書き込みセールス担当者。 API ユーザーの役割がセールス担当者APIのリリースよりも前の場合は、アクセスを有効にするには、これらの権限でAPI ユーザーの役割を更新する必要があります。 それ以外の場合は、「アクセス拒否」という603 エラー応答が表示されます。

* Asset API - ランディングページテンプレート

ランディングページテンプレートに関連するデータをプログラムでリスト、作成、更新できる新しい[ ランディングページテンプレートエンドポイント ](https://developer.adobe.com/marketo-apis/api/asset/#landing_page_templates_endpoints)が導入されました。

* Asset API - セグメント

セグメントに関連する2つのエンドポイントが導入されました。

[Get Segments](https://developer.adobe.com/marketo-apis/api/asset/get-segments)

[Id別のセグメント化を取得](https://developer.adobe.com/marketo-apis/api/asset/get-segmentation-by-id)

* 「名前でフォルダーを取得」が「workSpace」パラメーターを尊重しない問題を修正しました。[LM-61059]
* カスタムオブジェクト APIに対して、いくつかのパフォーマンスの改善を行いました。

投稿日：_2015-07-17_ by _David_

## Marketo REST APIを使用してリード、企業、商談を作成し、関連付ける

Marketoを最大限に活用するためには、リード、企業、商談のレコードを適切かつ堅牢に関連付ける必要があります。 ネイティブのCRM同期を活用していない場合、それらの関係を構築するのが困難になる可能性があります。次は、その構築について説明します。

### オブジェクトの関係

Marketoでは、オポチュニティレポートを確立するために、次のようないくつかの重要な要素を備えています。

* リードと商談は、OpportunityRole オブジェクトと多くの関係があります。
* OpportunityRoleには、リードから商談への関係を作成するためのleadId フィールドとexternalopportunityid フィールドの両方があります。
* 「商談あり」スマートリストフィルターの対象にするには、リードに商談に関連するOpportunityRoleが必要です。
* 商談は、externalCompanyId フィールドを介してCompany オブジェクトと多対一の関係を持ちます。
* リードは、externalCompanyId フィールドを介して会社と1対多の関係を持ちます。
* 商談は、リードの獲得プログラム、またはプログラムでのメンバーシップと成功に基づいてプログラムに関連付けられます（[ アトリビューションの理解](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/reporting/revenue-cycle-analytics/revenue-tools/attribution/understanding-attribution)を参照）。

リードデータベース全体でこれらの関連性を構築することで、Marketo analyticsを最大限に活用し、プログラムが商談創出や成約率に与える影響を確認できます。

### 会社

これらの関係を構築する最も簡単な方法は、まず会社設立から始めることです。 これにより、作成後に商談を更新するために追加のAPI呼び出しを実行する代わりに、作成中に外部CompanyIdを商談に渡すことができます。 既存の設定に応じて、これは必要な手順である場合とそうでない場合がありますが、関係を構築するには、関連する企業の新規リードと取引先責任者がこれらのレコードをMarketo インスタンスに追加する必要があります。会社レコードを作成するコードを見てみましょう。

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

companies APIには、2つの重複排除オプションがあります。このオプションは、リクエストのdedupeBy パラメーター「dedupeFields」および「idField」で設定されます。 これらは、「会社を記述」を呼び出すことによって明示的に取得できます。 dedupeByが未設定の場合、デフォルトではdedupeFieldsになります。 会社レコードの場合、重複排除フィールドは常に、外部ソースによって設定された任意の文字列である「externalCompanyId」と、作成後にMarketoによって生成され返される整数である「marketoId」フィールドに対応するidFieldに対応します。 dedupeByの選択に応じて、会社レコードのアップサート呼び出しには、externalCompanyIdまたはmarketoIdのいずれかを含める必要があります。 同じ要件が、商談および商談ロールオブジェクト APIにも適用されます。 このコードでは、2つのコンストラクターを公開しています。1つはAuth オブジェクトの1つの引数を受け入れ、もう1つはAuthを受け入れ、[JsonObject](https://github.com/ralfstx/minimal-json)企業レコードのリストを受け入れます。 入力リストなしで構築された場合は、addCompanies メソッドを使用して会社レコードを追加する必要があります。このメソッドは、入力がnullの場合に新しいArrayListを作成をチェックし、すべてのJsonObject引数を入力リストに追加します。 使用例を次に示します。

```java
//Create a new company to associate to
JsonObject myCompany = new JsonObject().add("externalCompanyId", "myCompany");
UpsertCompanies upsertCompanies = new UpsertCompanies(auth).addCompanies(myCompany);
JsonObject companiesResult = upsertCompanies.postData();
System.out.println(companiesResult);
```

1つのフィールド `externalCompanyId`を持つ単一の会社JsonObjectを作成し、UpsertCompaniesのインスタンスを作成し、`addCompanies`を持つ入力リストに会社を追加します。

### 商談

会社オブジェクトと同様に、商談APIには`dedupeBy` パラメーターがあり、それぞれ「externalopportunityid」と「marketoGUID」に対応する「dedupeFields」または「idField」を受け入れます。 私たちのコードは、UpsertCompanies クラスによく似ています。

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

同じコンストラクターのオプションが提供され、Authまたは`Auth+List<JsonObject>`と`addOpportunities` メソッドを使用してJsonObjectの機会を入力します。 使用例を次に示します。

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

ここでは、2つの例の商談を作成し、名前、externalopportunityid、externalCompanyId、およびexternalCreatedDate フィールドの値を指定します。 externalCreatedDateについてはまだ説明していませんが、商談が作成された時点ではRCEのマスターフィールドとして扱われるため、利用することが重要です。 組織のビジネスロジックを利用して、既存の商談データをバックフィルしているか、新しい商談データを即座に作成しているかにもとづいて、このフィールドに入力した内容を決定できます。 UpsertOpportunitiesのインスタンスを作成し、addOpportunitiesを介してJsonObjectsを追加します。 これで、インスタンスが設定されたので、これをpostDataでMarketoにプッシュし、結果を印刷できます

### ロール

ロールは、前の2つのオブジェクトとかなり似ていますが、dedupeByをdedupeFieldsに設定する際の要件が少し異なります。 役割では、このメソッドを使用してレコードを作成または更新する際に、「leadId」、「role」、「externalopportunityid」の3つのフィールドを含める必要があります。 「role」は任意の文字列値を指定できますが、他の2つはリードの有効なIDと商談の有効なIDをそれぞれ参照する必要があります。

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

先ほどの例と同様に、コンストラクターとaddRoles メソッドのパターンに従っています。 次に例を示します。

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

ここでは、2つのサンプルロールの新しいJsonObjectを作成し、必要な重複排除フィールドを追加し、作成した商談からexternalopportunityidを引き出し、それをMarketoにプッシュします。

### あらゆる要素をまとめる

主な方法の完全な例を次に示します。

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

企業、機会、役割の作成順序を確認できます。 これで、会社と商談のデータをMarketoに同期する準備が整いました。

投稿日：_2015-08-07_ by _Kenny_

## Marketo REST APIを使用したトランザクションメールの送信：第2部、カスタムコンテンツ

今週は、Request Campaign API呼び出しを介してメールに動的コンテンツを渡す方法を見ています。 Request Campaignは、外部からのメールのトリガーを許可するだけでなく、メール内の[ マイトークン ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/core-marketo-concepts/programs/tokens/understanding-my-tokens-in-a-program)のコンテンツを置き換えることもできます。 マイトークンは、プログラムレベルまたはマーケティングフォルダーレベルでカスタマイズできる再利用可能なコンテンツです。 また、リクエストキャンペーンの呼び出しを通じて置き換えるプレースホルダーとして存在することもできます。

### メールの作成

コンテンツをカスタマイズするには、まず[ プログラム ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/creating-programs/create-a-program)と[電子メール ](https://experienceleague.adobe.com/ja/docs/marketo/using/home)をMarketoで設定する必要があります。 カスタムコンテンツを生成するには、プログラム内でトークンを作成し、送信するメールに配置する必要があります。 簡単にするために、この例では1つのトークンのみを使用していますが、メール内の任意の数のトークンを、メールから、名前、返信先、またはメール内の任意のコンテンツで置き換えることができます。 ここで、置換用のトークンリッチテキストを 1 つ作成し、「bodyReplacement」という名前を付けます。 リッチテキストを使用すると、トークン内の任意のコンテンツを、入力する任意の HTML に置き換えることができます。 トークンは空のままでは保存できないので、ここにプレースホルダーテキストを挿入します。 次に、トークンをメールに挿入する必要があります。このトークンは、リクエストキャンペーン呼び出しを通じて置き換えるためにアクセスできるようになります。 このトークンは、1行のテキストから成るシンプルなもので、メールごとに置き換える必要があるか、メールのレイアウト全体を含めることができます。

### コード

私たちは、カスタマイズされたトークンをリクエストキャンペーンコールに渡すために、先週からコードを拡張しています。

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

今回は、bodyReplacement 変数にトークンの内容を作成し、addToken メソッドを使用してリクエストに追加します。 addToken はキーと値を受け取り、JsonObject 表現を作成して、内部の tokens 配列に追加します。 その後、これが postData メソッド中にシリアル化され、次のような本文が作成されます。

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

この方法は、様々な方法で拡張可能で、個々のレイアウトセクション内またはメール外部のメールのコンテンツを変更し、カスタム値をタスクや注目のアクションに渡すことができます。 プログラム内からトークンを使用できる場所はすべて、この方法を使用してカスタマイズできます。 また、同様の機能は、[キャンペーンをスケジュール](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST)呼び出しでも使用でき、バッチキャンペーン全体をまたいでトークンを処理できます。 これらは、リードごとにカスタマイズすることはできませんが、幅広いリードを対象としたコンテンツのカスタマイズに非常に役立ちます。

投稿日：_2015-07-24_ by _Kenny_

## APIを使用したMarketoでのリードデータの更新

1年以上前に、APIを使用してMarketoの顧客と見込み客の情報を更新しました。 その投稿には、更新のために外部システムに対してポーリングを行うために定期的に実行できるコードサンプルが表示されていました。 外部データを取得してMarketoにプッシュし、リード情報を更新することがアイデアでした。 提示されたコードサンプルは、SOAP APIを使用していました。 REST エンドポイントを使用して同じ目標を達成します。**プログラム入力** データを外部システムからMarketo REST APIで使用できる形式に変換する必要がある可能性があります。 リードの作成/更新APIを使用しているので、データはリクエスト本文で送信されるJSONとしてフォーマットする必要があります。 これは、例で最もよく説明できます。 以下のJava サンプルコードでは、モックリードデータを文字列の配列に配置しました。 各文字列は、各リードのデータ（名、姓、電子メールアドレス、役職）に続きます。

```java
private static String externalLeadData[] = {
        "Henry, Adams, <henry@superstar.com>, Director of Demand Generation",
        "Suzie, Smith, <ssmith@gmail.com>, VP Marketing"
};
```

サンプルコードは、配列を以下のJSON ブロックに変換します。

```json
{
"input":
    [
        {"firstName":"Henry", "lastName":"Adams", "email":"<henry@superstar.com>", "title":"Director of Demand Generation"},
        {"firstName":"Suzie", "lastName":"Smith", "email":"<ssmith@gmail.com>", "title":"VP Marketing"}
    ]
}
```

各「input」配列項目は、Marketoの個々のリードに対応します。 配列項目は、1つ以上のMarketo リードフィールド名とそれぞれの値を含むJSON オブジェクトです。 指定するフィールド名（この場合はfirstName、lastName、email、title）は、Marketo サブスクリプションに定義されたREST API名と一致する必要があります。 REST API名は、Marketo管理パネルのフィールド管理セクションでフィールド名を書き出すことによって確認できます。 フィールド名は、次に示すようにExcel ファイルに書き出されます。 または、[ リードを記述](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeUsingGET_2)APIを呼び出して、プログラムでフィールド名を検索することもできます。 例えば、「名」フィールドのREST API名を含む「応答を記述」スニペットがあります。

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

**プログラムロジック** ペイロードが適切な形式になると、リードの作成/更新を呼び出す準備が整います。 このサンプルでは、オプションのパラメーターは指定しません。 デフォルトの動作は、リードレコード（アップサート）の作成または更新、重複排除の目的での電子メールの使用、同期処理の使用です。 リードの作成/更新の呼び出しが成功した場合、応答本文には、Marketo リード IDと作成/更新操作のステータスを含む「結果」配列が含まれます。 リクエストで渡した「action」パラメーターに応じて、ステータスは「更新」、「作成」、「スキップ」のいずれかになります。 この例を続けて、最初のリードが存在しなかったとし（Henry Adams）、2番目のリードが存在したとします（Suzie Smith）。 次のような応答は、最初のリードが作成され、2番目のリードが更新されたことを示します。

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

今のところはここまでです。 ハッピーコーディング！**プログラムコード**

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

投稿日：_2015-08-14_ by _David_

## MarketoへのSalesPerson データの追加

新しいSalesPerson APIを使用すると、ネイティブのCRM統合がなくても、Marketo リードをSalesPerson レコードにインスタンス内で自由に関連付けることができます。 これにより、Marketo内で{{lead.Lead Owner Email Address}}および関連するフィールドとトークンを使用できます。

### SalesPerson レコードの作成

リードをSalesPerson レコードに関連付けるには、まずSalesPerson レコードをMarketoに入力する必要があります。 PHPのクラスの例を以下に示します。

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

上記のクラスでは、$input変数は可能なメンバーを持つstdClass オブジェクトの配列です。

* externalSalesPersonId （作成時のみ有効）
* id （キー入力updateOnly モードとしてのみ）
* email
* fax
* firstName
* lastName
* mobilePhone
* phone
* title

タイプとフィールドの長さに関する詳細な情報は、Describe SalesPerson呼び出しを通じて取得できます。

### リードの同期

必要なリードを同期するためのクラスの例を次に示します。

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

次に、2つの営業担当者レコードを作成し、それらを2つのリードレコードに関連付ける例を示します。

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

この例のクラスでは、SalesPersonおよびLead レコードを表すstdClass オブジェクトを作成します。これらのレコードは、同期する必要があり、各フィールドはメンバーとして追加されます。 このコードの実行後、リード <marketoDev@example.com>と<devBlog@example.com>の両方にリード所有者の電子メール、リード所有者の名前、リード所有者の姓フィールドが入力され、それらのフィールドに関連するトークンを使用し、関連するスマートリストフィルターでフィルタリングできます。

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

投稿日：_2015-08-21_ by _Kenny_

## API ユーザーとカスタムサービスのベストプラクティス

MarketoのREST APIは、認証にカスタムサービスを使用し、これらの各サービスはAPIのみのMarketo ユーザーが所有します。 各カスタムサービスの機能は、そのユーザーに割り当てられた各役割の権限によって決まります。 統合に個々のユーザーとカスタムサービスを割り当てることで、複数の利点が得られます。

* ユーザーに与えられた役割を通じて、個々のサービスに与えられた[権限](/help/rest-api/custom-services.md)を微調整できます。
* 他のサービスを無効にすることなく、対応するカスタムサービスを削除することで、個々のweb サービスがインスタンスに対して呼び出しを行わないようにすることができます。
* API呼び出しの使用状況に関するレポートはユーザーごとに分類され、高い使用率と異常な使用率を特定できます
* 各web サービスに与えられているデータを判断するのは簡単です
* Workspace対応インスタンスでは、アクセス可能なワークスペースに役割を割り当てるだけで、特定の事業部へのアクセスを制限できます

### API 使用量

各 API ユーザは API 使用量レポートで個別に報告されるので、web サービスをユーザごとに分割すると、各統合の使用量を簡単に把握できます。 インスタンスへの API 呼び出しの数が制限を超え、後続の呼び出しが失敗する場合は、この方法を使用すると、各サービスからのボリュームを把握し、問題を解決する方法を評価できます。 管理者 / Web サービスに移動し、過去7日間の通話数をクリックして、使用状況を確認します。

### サービスを無効にする

統合に望ましくない効果がある場合、各統合に個別のカスタムサービスを割り当てていない場合、面倒で無効にするのが困難になる可能性があります。 それらをひとつずつ分割することで、Admin -> Launchpointで問題のあるサービスを削除するのと同じくらい簡単になります。

### Workspace Management

Marketo Enterprise サブスクリプションの場合、サービスは1つのワークスペースにのみアクセスする必要があるのが一般的です。これは、API ユーザー](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/allow-user-access-to-a-workspace)へのロール割り当てによって[強制できます。 各ユーザーの役割は、グローバルまたはワークスペースごとに割り当てることができるため、必要に応じてワークスペースでアクセスを制限し、可能な限り最小限の権限を提供できます。

投稿日：_2015-08-28_ by _Kenny_

## REST APIを使用したリードパーティションの指定方法

**リードの分割** Marketoのリードの分割は、リードを分離する便利な方法を提供します。 パーティションを使用すると、組織内の様々なマーケティンググループが1つのMarketo インスタンスを共有できます。 詳しくは、[ ワークスペースとリードパーティションについて](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/understanding-workspaces-and-person-partitions)を参照してください。 Marketo REST APIを使用して、リードパーティションを使用し、プログラムでリードを作成するとします。 作成したリードが適切なパーティションに移動することを確認する方法？ この記事では、その方法をご紹介します！ この例では、ワークスペースとパーティションを使用して、地域にもとづいてリードを分離します。

まず「国」というワークスペースを定義します。 次に、そのワークスペース内に「メキシコ」と「カナダ」という2つのパーティションを作成します。  **パーティションでリードを作成** 「メキシコ」パーティションに2つのリードを作成するとします。 リードを作成するには、を呼び出します。 パーティションを指定するには、リクエスト本文に「partitionName」属性を含める必要があります。 partitionName値に何を使用するかを知るにはどうすればよいですか？ インスタンスの有効なパーティション名の値のリストを取得するには、[Get Lead Partitions](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeProgramMemberUsingGET) APIを次のように呼び出します。

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

この場合、正しい値は「メキシコ」なので、次のようにリードの作成/更新に渡します。

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

Marketoに新しく作成されたリードを紹介します。  **パーティションでリードを更新** パーティション内の既存のリードを更新するには、Create/Update リードと呼び、以前と同じようにpartitionNameを指定するだけです。 今回のアップデートでは、上記で作成したリードに名前、姓、タイトルを割り当てます。

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

Marketoに新しく更新されたリードをご紹介します。
**リードのパーティションを特定** リードがどのパーティションに属しているかを知るにはどうすればよいですか？ このために、[Get Lead by Id](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) APIを使用し、「fields」クエリパラメーターに「leadPartitionId」を指定します。 この場合、上記で作成したリード ID 318816の情報を取得します。

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

partitionNameではなくleadPartitionIdが返されることに注意してください。 partitionNameを取得するには、上記のGet Lead Partitions APIの出力を再確認する必要があります。

```json
{
    "id": 2,
    "name": "Mexico",
    "description": "Leads that live in Mexico"
},
```

この場合、leadPartitionIdの値2は、「Mexico」のpartitionNameにマッピングされます。 今のところはこれまで。 ハッピーパーティション！

投稿日：_2015-09-04_ by _David_

## Marketo メールスクリプトのスコアフィールドの比較

**注：**&#x200B;これはキャサル・モランによるゲスト投稿です。 Cathalは、アイルランドのダブリンにあるMarketoのEMEA オフィスのソリューションコンサルタントです。

### スコアフィールドの比較

多くのMarketoのお客様、特にクロスセルに重点を置いている顧客は、複数のスコアフィールドを持っており、特定の商品/分野に対するリードの関心を測定するためによく使用されます。 例えば、リンゴとバナナを販売する場合、リードのスコアがリンゴで50、バナナで10の場合、その嗜好がどこにあるのかが明確になります。私のコンテンツがこの嗜好を反映しているのであれば、それは良いことではありません。 メールスクリプトを使用すると、スコアを比較したり、メールを受信する特定のリードのスコアが最も高い（または低い）電子メール内のコンテンツをパーソナライズしたりできます。

### 2つの数値を比較するには、フィールド値を整数に変換する必要があります

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

上記の例では、テキストをパーソナライズするだけですが、例えば、より高いスコアに基づいて異なる画像を簡単に表示できます。

投稿日：_2015-09-14_ by _Kenny_

## バックグラウンドでのMarketo フォーム送信

web コンテンツや顧客データをホスティングするための様々なプラットフォームが存在する企業では、フォームから並行してデータを送信し、別々のプラットフォームでデータを収集できるようにする必要があることが一般的になっています。 これを行う方法はいくつかありますが、最も優れているのは、多くの場合、最もシンプルなものです。Forms 2 APIを使用して、非表示のMarketo フォームを送信します。 これは新しいMarketo フォームでも機能しますが、理想的にはこれにはフィールドがない空のフォームを作成する必要があります。 これにより、フォームは何もレンダリングする必要がなくなるため、必要以上にデータを読み込むことがなくなります。 次に、フォームから[埋め込みコード ](https://experienceleague.adobe.com/ja/docs/marketo/using/home)を取得し、目的のページの本文に追加して、小さな変更を加えます。 埋め込みコードには、次のようなフォーム要素が含まれています。

`<form id="mktoForm_1068"></form>`

要素に「style=&quot;display:none&quot;」を追加して、次のように要素が表示されないようにします。

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

この方法で送信されたFormsは、リードが記入し、目に見えるフォームを送信した場合とまったく同じように動作します。 送信のトリガーは、実装によって異なります。各トリガーにはプロンプトを表示するアクションが異なりますが、基本的に任意のアクションで実行できます。 重要なのは、フィールドと値を正しく設定することです。 値を正しく送信するには、[ フィールド名を書き出し](/help/rest-api/list-of-standard-fields.md)で検索できるフィールドのSOAP API名を必ず使用してください。

Munchkin Associate Leadからの移行

バックグラウンドフォームの送信は、Munchkin アソシエイトリードの推奨される代替方法の1つです。 下のサンプル HTML ページでは、リードの関連付けに送信された値と同じ値を再利用して、マイグレーションの概要を示しています。

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

投稿日：_2015-09-25_ by _Kenny_

## Marketo REST APIの例外とエラー処理：第1部

Marketo REST APIは、例外またはエラーを返す場合があります。これは、便宜上、ここからエラーを呼び出すだけです。 エラーは、次の3つのレベルで発生する可能性があります。

* HTTP レベルでは、これらのエラーは4xx コードで示されます
* 応答レベル。これらのエラーは、JSON応答の「errors」配列に含まれます
* レコードレベルでは、これらのエラーはJSON応答の「結果」配列に含まれ、「ステータス」フィールドと「理由」配列を使用して個々のレコードベースで示されます

### HTTP エラー

通常の運用環境では、Marketoは2つのHTTP ステータスエラー（「413 Request Entity Too Large」、「414 Request URI Too Long」）のみを返す必要があります。 これらは両方とも、エラーをキャッチし、リクエストを変更して再試行することで復元できますが、スマートコードプラクティスを使用すれば、実際にこのような問題が発生することはありません。 Marketoは、リクエストペイロードが1 MBを超えた場合は413、リードの読み込み[の場合は10 MBを返します。](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) ほとんどのシナリオでは、これらの制限に達することはほとんどありませんが、リクエストのサイズにチェックを追加し、制限を超えるレコードを新しいリクエストに移動すると、このエラーにつながる状況がエンドポイントによって返されないようにする必要があります。 GET リクエストのURIが8 KiBを超えると、414が返されます。 これを回避するには、クエリ文字列の長さがこの制限を超えていないかどうかを確認します。 リクエストをPOST メソッドに変更する場合は、クエリ文字列をリクエスト本文として追加パラメーター&#39;_method=GET&#39;で入力します。 これにより、URI の制限がなくなります。 ほとんどの場合、この制限に達することはまれですが、GUID などの長い個別のフィルター値を持つ大量のレコードを取得する場合は、比較的よくで発生します。

### 応答レベルのエラー

応答レベルのエラーは、応答の「成功」パラメーターがfalseに設定されている場合に発生します。 「errors」の各エントリには、6xxまたは7xxのいずれかの番号を「code」する2つのメンバーと、エラーの平文の理由を示す「message」があります。 6xx コードは常に、リクエストが完全に失敗し、実行されなかったことを示します。 例えば、601の「アクセストークンが無効です」は、新しいアクセストークンをリクエストに再認証して渡すことによって回復可能です。 7xx エラーは、データが返されなかったか、無効な日付が含まれている、必須パラメータが欠落しているなど、リクエストが誤ってパラメーター化されたことにより、リクエストが失敗したことを示します。

### レコードレベルのエラー

レコードレベルのエラーは、個々のレコードに対する操作は完了できなかったが、リクエスト自体は有効であったことを示します。 これらは、応答の「結果」配列内の個々のレコード内で発生します。 これらのレコードの「status」フィールドは「スキップ」され、「reasons」配列が存在します。 各理由には、&quot;code&quot; メンバーと &quot;message&quot; メンバーが含まれます。 コードは常に1xxxになり、メッセージはレコードがスキップされた理由を示します。 例えば、リードの作成/更新リクエストで「アクション」が「createOnly」に設定されているものの、送信されたレコード内のキーの1つにリードが既に存在する場合があります。 この場合は、1005のコードを返し、「リードは既に存在します」というメッセージが表示されます。 次のいくつかの投稿では、回復可能なエラーと、コード内でこれらを処理する方法の例について説明します。

投稿日：_2015-10-09_ by _Kenny_

## ゲスト投稿 – Marketo データベースへの直接SQL コネクタ

**これは、Sumit Sarkar of Progress, Inc.**&#x200B;のゲスト投稿です。

Marketo データベースへの&#x200B;**SQL コネクタ** Marketoには、データにアクセスするためのAPIが十分に文書化されています。 しかし、組織がSQLに直接アクセスする必要がある場合もあります。 Marketoでは、マーケティング部門とIT部門の境界線が曖昧になり、標準ベースのSQL接続に対する需要が高まっています。 Marketoへの直接SQL コネクタは、[Progress DataDirect Cloud](https://www.progress.com/connectors/cloud-data-integration)を通じて利用できます。 DataDirect Cloudは、ODBC （「Open Database Connectivity」）またはJDBC （「Java Database Connectivity」）とOData （「Open Data Protocol」）を介したSQL アクセス用のオープン業界標準を介してMarketo データを公開するデータ接続サービスです。 次に、DataDirect Cloudを使用してMarketo データを標準で接続する一般的なユースケースをいくつか示します。

* データの発見と可視化（Qlik、Tableau、SAP Lumira）
* エンタープライズレポート（SAP ビジネスオブジェクト、マイクロストラテジー、Cognos）
* データ統合（SQL Server Integration Services - SSIS、Oracle Data Integrator - ODI、Informatica）
* データフェデレーション （SQL Server Linked Server、SAP Hana SDA、Oracle Database Gateway）
* アドホッククエリ（Microsoft Office、DB Visualizer、Aqua Data Studio）
* データ準備（Alteryx、Trifecta、Paxata）

**SQLからMarketoへのアクセスの仕組み**

* DataDirect Cloudは、Marketoの統合APIによって公開されるデータの論理スキーマを作成します。
* DataDirect Cloudは、Marketo APIから取得したデータに対して、Elastic Real-Time Query Engineを使用して、軽量ODBCまたはJDBC クライアントからSQL リクエストを処理します。
* DataDirect クラウド接続は、データの複製を行うことなく、直接かつリアルタイムです。
* DataDirect Cloud Serviceは、エンドユーザーがAPI バージョンの変更やMarketoとRESTの比較について心配する必要がないように、SOAP APIを抽象化します。

DataDirectは、2006年からSaaS データソースへのこのスタイルの接続性を構築しており、最初のSalesforce ODBC ドライバーはweb サービス API上に構築されました。**Marketoへの接続を開始します：**

1. [DataDirect Cloud ログインの登録](https://pacific.progress.com/console/register?productName=d2c&ignoreCookie=true)
1. 「データソース」をクリックし、「+新規データSource」ボタンをクリックします。
1. 「Marketo」を選択し、接続情報を入力します。 Marketo管理者またはログイン担当者に確認して、SOAP統合](/help/soap-api/soap-api.md)の[接続情報を確認できます。
1. 「接続をテスト」ボタンをクリックします。 MarketoからODataを生成するための「OData」タブがあり、今後のブログ記事で解説します。
1. 公開されているMarketo スキーマを調べたり、UI内から基本的なSQL クエリを発行したりする場合は、「SQL テスト」をクリックします。
1. 左側の「ダウンロード」をクリックし、インストールするアプリケーションとプラットフォームのDataDirect Cloud ODBCまたはJDBC ドライバーを選択します。
1. DataDirect Cloud ODBCまたはJDBC ドライバーをインストールすると、任意の標準ベースのアプリケーションをMarketoに接続できます。

次に、[DataDirect Cloud ODBC クライアント ](https://www.youtube.com/watch?v=H6PHra56Iig)を使用して接続するビデオの例を示します。 Marketoに適用されるその他のDataDirect Cloud チュートリアルを以下に示します。

* [SAP Data Analytics](http://scn.sap.com/community/lumira/blog/2015/08/05/connect-sap-lumira-to-eloqua-marketo-google-analytics)
* [Microstrategy Enterprise Reporting](https://community.microstrategy.com/t5/Tech-Corner/What-MSTR-developers-should-know-about-Cloud-Data-Sources/ba-p/253083)
* [Oracleとの連携](https://www.ateam-oracle.com/post/a-universal-cloud-applications-adapter-for-odi/)

Marketoなどのクラウドソース間のSQL接続を構築する&#x200B;**R&amp;Dの課題**

あらゆるSaaS APIが標準のクエリ言語を公開しているわけではありません。 そのような場合、エンジニアリングチームは各オブジェクトを個別に見ます。 各オブジェクトは、呼び出し、検索フィルタリングなどの一意のルールを持つ異なるAPIで公開できます。データモデル全体で標準的なエクスペリエンスのクエリを提供するには、膨大な労力が必要でした。

完全結合機能の処理。 SaaS APIがJOIN機能を備えたクエリ言語をサポートしていない場合、エンジニアリングチームはその操作を実行する必要があります。 これには、結合を実行する前に最小限のデータを返すために、SQLからMarketo APIを効率的に呼び出すための翻訳が必要です。 2つの非常に大きなオブジェクトを結合する場合、データアクセス層は、アプリケーションサーバーまたはデスクトップ上のかなりのリソースを使用する可能性があります。 したがって、DataDirect Cloudなどの弾性クラウドサービスへのデータアクセスレイヤーのデプロイメントは、次の2つの理由から非常に理にかなっています。

1. クライアントアプリケーションサーバーまたはデスクトップでのパフォーマンスの高速化とメモリ/CPU リソースの使用量の削減
1. 事前に結合されたデータセットが交換されるDataDirect CloudとMarketo間の優れた帯域幅を活用します。

データモデルの処理方法？ 静的か動的か？ 変更はどのように検出され、クライアントに伝えられますか？ 各SaaS データソースは異なり、Marketoの場合、特定のオブジェクトはビューを通じて、テーブルを通じて、より適切にクエリされます。 あらゆるSaaS ソースをまたいで、このデータモデルとオブジェクトのマトリックスを扱うことは、確かに課題でした。

**開発者向けMarketoおよびDataDirect Cloud リファレンス：**

* Marketo接続のプロパティ （[ ドキュメントへのリンク ](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html)）
* MarketoでサポートされているSQLと拡張機能（[ ドキュメントへのリンク ](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html,-hubspot,-and-marketo.html)）
* 公開されたMarketo テーブルとビュー（[ ドキュメントへのリンク ](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html)）
* Marketoから返される一般的なエラーメッセージ（[ ドキュメントへのリンク ](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html)）

**伝記：** Sumit Sarkarは、Progressのチーフデータエバンジェリストであり、データ接続の分野で10年以上の経験があります。 オープンデータ標準のクラウドデータとの接続性に関する世界的なコンサルタントであるSumit氏は、分析のための特許取得済みの技術を開発したデータアクセスレイヤーのパフォーマンスチューニング、SaaS プラットフォームのビジネスインテリジェンスとデータウェアハウス、そしてODBC、JDBC、ADO.NET、ODATAなどの標準に重点を置いたPaaS環境向けのデータ接続性に関心を持っています。 IBM・コグノス・Business IntelligenceのIBM認定コンサルタントであり、TDWIのメンバーでもあります。 また、Dreamforce、Oracle OpenWorld、Strata Hadoop、MongoDB World、SAP Analytics and Business Objects Conferenceなど、様々なカンファレンスでデータ接続に関するセッションを発表しています。 Twitter: @SAsInSumit LinkedIn: [www.linkedin.com/in/meetsumit](http://www.linkedin.com/in/meetsumit)

投稿日：_2015-12-07_ by _Kenny_

## APIの使用状況とエラー数に関するダッシュボードの作成

Marketo API コンシューマーとして、これは常に注意を払うべき有用な情報です。 過去の利用状況データを取得し、長期的なトレンドを検出できたらどうでしょうか？ API エラーコードの概要を取得して、統合の健全性を測定できる場合はどうなりますか？ Marketoのテクノロジーパートナーとして、あらゆる顧客アカウントの使用状況やエラーデータを1つのダッシュボードで確認できたら、どうでしょうか？ 本記事では、上記の質問に対する回答を提供します。 早く行くぞ！
**Stats Retrieval**&#x200B;のスケジュール済みジョブ [毎日の使用状況を取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLast7DaysErrorsUsingGET)および[毎日のエラーを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getDailyErrorsUsingGET) エンドポイントを使用して、使用状況とエラーデータを取得するアプリを作成しましょう。 このアプリは、1日に1回実行するようにスケジュールされています。 アプリが実行されるたびに、1日分の使用状況データがあるファイルに、1日分のエラーデータが別のファイルに追加されます。 毎月の初めに、新しいファイルのペアが作成されます。 これらのファイルは、いつでもアクセスできる履歴レコードとして機能します。 これがアプリロジックです…

* 外部ソースからMarketo アカウント情報（Munchkin IDおよびクライアント資格情報）を読み取ります。 注意：このソースは、他のユーザーがアカウントデータにアクセスできないように安全である必要があります。
* 各アカウントを繰り返し利用して、
   * 1日の使用状況データを取得するには、「Get Daily Usage」を呼び出します
   * 1日の使用状況データを毎月の「使用状況」ファイルに追加
   * 1日のエラーデータを取得するには、「Get Daily Errors」を呼び出します
   * 毎日のエラーデータを月次の「errors」ファイルに追加

出力ファイル形式出力ファイルの形式は、それぞれのAPI呼び出し（使用状況とエラー）から返される「結果」配列と一致するJSONです。 「result」配列の各要素は、1日のデータを含むJSON オブジェクトです。 出力ファイルの命名出力ファイルの名前は次のとおりです。

`<type>_<yyyy>_<mm>_<account>.json`

どこで，

`<type>` - データの種類（「使用状況」または「エラー」） `<yyyy>` – 年（4桁） `<mm>` – 月（2桁） `<account>` - アカウント ID （Munchkin ID）

出力ファイルの例usage_2015_10_111-AAA-222.json

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

このアプリのコードは、この記事（Stats.java）の最後に示されます。**Web サービス**&#x200B;を統計します。このデータをブラウザーに取り込む方法が必要です。 提案は、データを配信するweb サービスを作成することです。 Web サービスは、アプリの出力ファイルを使用し、すぐに表示できる形式でデータをブラウザーに返します。 簡素化のために、および同一生成元のポリシー制限を回避するために、[JSONP](https://en.wikipedia.org/wiki/JSONP) パターンを活用します。 外部web サービスに対して提案されているREST エンドポイントの仕様は次のとおりです。**URI**: /stats **Method**: GET

**パラメーター**

**説明**

**例**

month

今月のデータを取得。 含める月のカンマ区切りリスト（2桁の表現）。 デフォルトは全月です。

10,11

year

今年のデータを取得します。 含める年のコンマ区切りリスト（4桁の表現）。 デフォルトは全年です。

2015年

account

このアカウントのデータを取得（Munchkin ID）。

111-AAA-222

callback

JSON コンテンツをラップする関数の名前。

processStats

リクエストの例

`GET //localhost:8080/stats?month=10&year=2015&account=111-AAA-222&callback=processStats`

Web サービスは、「使用状況」ファイルと「エラー」ファイルを読み取り、それらを結合し、次の形式で返します。

```html
**<Name of Callback here>**

<Contents of Usage file here>,

<Contents of Error file here>
```

これは2つの引数を持つJSONP コールバックです。 最初の引数は、使用状況の「result」配列です。 2番目の引数はエラー「result」配列です。 レスポンスの例

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

ご覧のとおり、web サービスは、アプリから2つの出力ファイルの内容を単純にラップしています。 [Mocky](https://designer.mocky.io)を使用してモック Web サービス応答を作成しました。 モックのweb サービスの例は[ここにあります。](http://www.mocky.io/v2/5627b2f9270000f2226eec63?month=10&year=2015&account=111-AAA-222&callback=processStats) このweb サービスの作成は、読者のエクササイズとして残されています：**ダッシュボード Web ページ**&#x200B;したがって、必要なのは、web サービスを呼び出してデータをフォーマットするweb ページだけです。 JSONP パターンを使用するには、Web サービスを呼び出す`<script>` タグを追加するだけです。

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

この関数は、web サービス呼び出しの後に自動的に呼び出されます。 この例では、各配列に[prettyPrint.js](https://github.com/padolsey-archive/prettyprint.js/tree/master)という単純なJavaScriptの「バリアブルダンパー」を呼び出します。 prettyPrint関数は、配列の内容を使用してHTML テーブルを生成します。 これはHTML テーブルのスクリーンショットです。 Voilà、これがダッシュボードです！ これは非常にエレガントではありませんが、それはあなたに何が可能であるかについてのアイデアを与えるべきです。 自分の目を引くビジュアライゼーションにしたい場合は、データの変換を妨げるものは何もありません。 HTMLのページは以下のとおりです（Index.html）上記の表は、次の手順でブラウザーでライブで表示できます。

1. Index.htmlのローカルコピーを保存します
1. prettyPrint.jsのローカルコピーを保存します
1. ブラウザーでIndex.htmlを開きます

私は。 この記事では、Marketo API統計のモニタリングに関するアイデアをいくつか紹介しました。 ハッピーコーディング！**Stats.java**

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

投稿日：_2015-10-22_ by _David_

## Marketo REST APIの例外とエラー処理：第3部

ほとんどの場合、Marketo REST APIから返されたエラーは自動的に回復できません。 ただし、自動的に回復したり、特定のタイプのエラーが表示されないようにしたりできるケースがいくつかあります。

### リクエストサイズエラー

このシリーズの最後の記事で見たように、URIが8 KiBを超える場合はMarketoがHTTP ステータスコード 414、リクエスト本文が1 MBを超える場合は413、リードの読み込みに10 MBを超える場合は413を生成します。 414は稀ですが、「フィルターでリードを取得」タイプを使用して、300の個別のGUIDまたは類似の条件に基づいてレコードをリクエストする場合は、それらを表示する可能性があります。 次のリクエストがあるとします：`<https://AAA-BBB-CCC.mktorest.com/rest/v1/leads.json?filterType=customGUID&fields=email`, company...firstName, lastName> リクエストを送信すると、URIが8KiBを超えているため、Marketoはステータス 414を返します。

これを処理するには、このリクエストのパターンを変更し、GETの代わりにPOSTを送信し、URIに「_method=GET」を追加し、リクエスト本文のクエリ文字列をx-www-form-urlencoded リクエストとして渡す必要があります。URI: `<https://AAA-BBB-CCC.mktorest.com/rest/v1/leads.json?_method=GET>` リクエスト本文：filterType=customGUID&amp;fields=email,company..firstName, lastName HTTP応答からこの例外を取得する代わりに、実行時にリクエストの合計長チェック結果を確認確認行を行うことができます。 または、レコードのバッチ取得にPOST メソッドを使用することもできます。 413sの場合、同様のパターンに従い、シリアル化ステップ中にレコードを追加する際にリクエスト本文の長さを確認し、この制限を超える場合はリクエストを複数の部分に分割することができます。

### 認証エラー

次のクラスの回復可能なエラーは、認証に関連しています。 以前の有効なアクセストークンがexpires_in期間が経過した後に使用されると、最初の使用では「アクセストークンが期限切れになりました」というエラーコードが602を返します。 この後、同じトークンを使用すると、「アクセストークンが無効です」という601が返されます。 ターゲットサブスクリプションの有効なアクセストークンではない文字列を他に使用すると、601が発生します。 いずれの場合も、失敗したリクエストの再試行を使用して新しいアクセストークンを再認証して渡すことで、このエラーを回復できます。

### タイムアウト

非常にまれな状況では、30秒のタイムアウト期間が経過した後に、呼び出しが604、「リクエストがタイムアウトしました」を返す場合があります。 リードの作成/更新などのバッチ処理されたリクエストの場合、リクエストを小さなバッチに分割し、成功が返されるまで再試行できます（バッチが100未満のレコードに分割され、リクエストがまだタイムアウトしている場合は、サポートケースを提出する必要があります）。 その他の最も一般的なケースは、アセット承認呼び出しです。この場合、[電子メール ](https://developer.adobe.com/marketo-apis/api/asset/approve-email-by-id/)や[電子メールテンプレート ](https://developer.adobe.com/marketo-apis/api/asset/approve-email-template-by-id/)などの別のユーザーまたはサービスによって、現在の承認済みレコードにロックが保持される可能性があります。 このような場合、既存のロックを解決できるように、[指数的バックオフ ](https://en.wikipedia.org/wiki/Exponential_backoff)を再試行に使用する必要があります。 シリーズの最後の部分については、今後数週間で確認し、回復不可能な特定のエラーを詳しく見ていきます。

投稿日：_2015-10-30_ by _Kenny_

## Marketoのセキュリティ機能強化

Marketoでは、セキュリティを重視しています。 **[業界全体の取り組み](https://security.googleblog.com/2014/09/gradually-sunsetting-sha-1.html)**&#x200B;の一環として、Marketoでは、セキュリティ保護を強化するために、web認証と暗号化をアップグレードしています。 ロールアウトは2011年12月12日に実行される予定です。**影響を受けるのは誰ですか？** 影響を受けるユーザーは少数で、10年以上経過したシステムからMarketoへの統合を行い、最近更新されていないユーザーのみが対象です。 サポートされているシステムとバージョンの詳細については、**[このリスト ](https://www.digicert.com/faq/sha2/sha-2-compatibility)**&#x200B;を参照してください。**次のユーザーは影響を受けません：**

* 最新のブラウザーを使用してMarketo.comにアクセスするエンドユーザー（[ リストを参照](https://www.digicert.com/faq/sha2/sha-2-compatibility)）
* Informatica、Dell Boomi、Scribeなどの統合パートナーをご利用のお客様。
* Launchpoint パートナーを使用しているお客様。

他のすべてのMarketo ドメインでは、既にSHA2証明書を使用しています。

投稿日：_2015-11-18_ by _Kenny_

## REST APIを使用したアクティビティのポーリング

アクティビティは、Marketo Platformのコアオブジェクトです。 アクティビティとは、web ページへの訪問、メール開封、ウェビナーへの参加、展示会への参加ごとに保存される行動データです。 一般的なユースケースは、アクティビティデータと組織の他の部分からのデータを組み合わせることです。 このサンプルプログラムには、次の6つの手順が含まれています。

1. [ リードアクティビティの取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET)を呼び出して、特定の日時に作成されたすべてのアクティビティレコードのリストを生成します。 フィルターを使用して、返されるアクティビティレコードのタイプを制限します。
1. 各アクティビティレコードから関心のあるフィールドを抽出します。
1. フィルターの種類](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)で[複数のリードを取得して、手順1のアクティビティに対応するリード レコードのリストを生成します。 手順2のアクティビティレコードから抽出したleadId フィールドをフィルターとして使用して、返されるリードを指定します。
1. 各リードレコードから関心のあるフィールドを抽出します。
1. 手順2のアクティビティデータを、手順4のリードデータと結合します。
1. ステップ 5のデータを、外部システムが使用できる形式に変換します。

下の図が示すように、この例では、メール関連のアクティビティをキャプチャするように選択しました。

**プログラム入力** デフォルトでは、プログラムは現在の日付から1日遡って変更を探します。 たとえば、このプログラムを毎日同じ時間に実行できます。 さらに時間を遡るには、コマンドライン引数として日数を指定すると、時間のウィンドウを効果的に増やすことができます。 このプログラムには、次の変数が含まれます。CUSTOM_SERVICE_DATA – これには、Marketo カスタムサービスデータ（アカウント ID、クライアント ID、クライアントシークレット）が含まれます。 READ_BATCH_SIZE – 一度に取得するレコードの数です。 これを使用して、ボディサイズに合わせて応答を調整します。 LEAD_FIELDS – 収集するリードフィールドのリストが含まれます。 ACTIVITY_TYPES – 収集するアクティビティタイプのリストが含まれます。

**プログラムロジック**&#x200B;まず、時間ウィンドウを設定し、REST エンドポイント URLを構成し、認証アクセストークンを取得します。 次に、「Get Paging Token/Get Lead Activities」ループを起動します。このループは、アクティビティの供給が終了するまで実行されます。 このループの目的は、アクティビティレコードを取得し、これらのレコードから関心のあるフィールドを抽出することです。 リード活動を取得するには、次の活動型のみを検索するように指示します。

* 配信済みメール
* メールを配信停止
* メールを開く
* 「メール」をクリックします。

各アクティビティレコードから次のフィールドを抽出します。

* leadId
* activityType
* activityDate
* primaryAttributeValue

目的に合わせて、アクティビティタイプとアクティビティフィールドの任意の組み合わせを自由に選択できます。 次に、リードの供給を使い果たすまで実行されるフィルタータイプループによる「複数のリードを取得」を起動します。 「filterType=id」パラメーターと一連の「filterValues」パラメーターを組み合わせて使用することで、取得したリードレコードを、先に取得したアクティビティに関連付けられたリードのみに制限することに注意してください。 各リードレコードから次のフィールドを抽出します。

* firstName
* lastName
* email

リードフィールドを自由に選択できます。 次に、リード IDを使用してリードフィールドとアクティビティフィールドを結合し、リンクします。 最後に、すべてのデータをループしてJSON形式に変換し、コンソールに出力します。**プログラム出力** サンプルプログラムの出力例を次に示します。 これは、アクティビティフィールドとリードフィールドをJSONの「結果」オブジェクトとして組み合わせて表示します。 ここでのアイデアは、このJSONをリクエストペイロードとして外部web サービスに渡すことができるということです。

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

作業は以上です。 ハッピーコーディング！

投稿日：_2015-11-20_ by _David_

## SoundCloud PlayerとMunchkin APIの統合

SoundCloudは素晴らしいオーディオホスティングプラットフォームを提供し、インディーロックのアクトから、音楽業界のトップにいるEDM アーティスト、storytellingポッドキャストまで、あらゆることに対する豊富な分析機能と機能性を備えています。 プラットフォームの優れたネイティブ機能に加えて、データを移動し、リスニング行動を追跡するための世界トップクラスのAPI プログラムが用意されています。 これはポッドキャスターにとって特に便利で、再生、一時停止、共有などの特定のリスニングアクションを、スクリプトやオーディオ内の特定のコンテンツに関連付けることができます。 本日は、[SoundCloudのウィジェット API](https://developers.soundcloud.com/docs/api/html5-widget)を活用して、Marketoでこれらのアクティビティを送信およびトラッキングする方法を紹介します。 まず、リードのアクティビティログインMarketoに記録されるMunchkin アクティビティの生成を見てみましょう。 その最も基本的な方法は、Munchkin.munchkinFunctionを呼び出し、最初の引数として&quot;visitWebPage&quot;を渡すことです。 これにより、Marketoを使用して訪問Web ページのアクティビティが記録され、メソッドに渡される任意のURLとクエリ文字列データが記録されます。 2番目の引数は、データを持つJavaScript オブジェクトを受け入れます。このデータには、2つのメンバー、「url」と「params」があり、両方の文字列があります。 url メンバーはMarketoのアクティビティのWeb ページに対応し、paramsはクエリ文字列に対応します。 この目的では、URLをSoundCloud関連のアクションの識別子として使用し、パラメーターには特定のアクティビティに関する追加データを含めます。 各アクションを追跡するために使用している関数は次のとおりです。

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

標準のSoundCloud ウィジェットはiframeに埋め込まれているため、ウィジェットはpost メッセージを使用して通信し、コールバックを使用してデータを取得する必要があります。これはcurrentSound メソッドとgetPosition メソッドで確認できます。 SoundCloud ウィジェット APIは、プレーヤー内の個々のイベントに対応し、これらをMarketoに送信するために使用できる一連のJavaScript コールバックを提供します。 私たちが興味を持っているイベントは、ユーザーが何を聞いているか、ユーザーが聞く時間、ユーザーがプレーヤーと行うインタラクションです。したがって、次のイベントを見ています。

* プレイ
* 一時停止
* 終了
* シーク
* CLICK_DOWNLOAD
* CLICK_BUY
* OPEN_SHARE_PANEL

また、ウィジェットのbind （） メソッドを使用して、これらの各イベントにコールバックを追加する必要があります。 次の例を見てみましょう。

```javascript
widget.bind(SC.Widget.Events.PLAY, function(){
    soundCloudMunchkin.trackPlay();
});
```

これにより、トラックが再生されるたびに、trackPlay メソッドを実行して、現在のトラックに関するデータを含むイベントをMarketoに送信します。 完全なスクリプトは[ここ](https://gist.github.com/kelkingtron/6750bb07c1397d93d9c7#file-soundcloudmunchkin-js)にあります。 soundCloudMunchkin オブジェクトにはinit メソッドがあり、これはSoundCloud ウィジェットオブジェクトを唯一の引数として受け入れ、トラッキングメソッドを関連するコールバックにバインドし、ウィジェットを設定してアクティビティをMarketoまでトラッキングします。 [Munchkin コード ](/help/javascript-api/lead-tracking.md)と[SoundCloud API ライブラリ ](https://w.soundcloud.com/player/api.js)を読み込む必要があります。 実際のSoundCloud ウィジェットを埋め込むだけでなく、すべてを初期化する必要もあります。

```javascript
window.onload=function(){
var iframe = document.getElementById(iframeId);
    if(iframe) {
        widget = SC.Widget(iframe);
        soundCloudMunchkin.init(widget);
    };
};
```

投稿日：_2015-12-21_ by _Kenny_

## RTPとEU E-Privacy Directive

この記事では、RTPを使用して、トラッキング中のweb サイト訪問者に通知したり、ヨーロッパの訪問者のトラッキングを自動的に無効にしたりする方法について説明します。 2012年以降、欧州の訪問者が利用できるウェブサイトは、EUのE プライバシー指令に準拠する必要があります。 2011年に施行された新しい法律は、ユーザーの知識や同意なしにユーザーのコンピューターに識別情報が保存されるのを防ぎます。 Cookieやその他のテクノロジーを必須ではないトラッキングに使用する場合は、次の手順を実行する必要があります。

1. トラッキングテクノロジーが使用されていることをユーザーに伝える。
1. これらのテクノロジーを使用する理由を説明します。
1. テクノロジーを使用する前にユーザーの同意を得て、いつでも許可を取り消すことができます。

投稿日：_1970-01-01_ by _Yanir_

## アプリを使用してMarketoの顧客および見込み客の情報を更新する

顧客や見込み客の情報を更新するために、独自のシステムを使用するシナリオもあります。 マーケティング部門は、マーケティング施策で最も正確な記録システムを使用するために、更新をMarketoに反映したいと考えています。 以下のアプローチを使用すると、Marketoへの定期的なアップロードを設定して、その独自システムで変更されたデータでMarketoの連絡先情報を最新の状態に保つことができます。 次の図は、設定された定期的なタイマーで行われるAPI呼び出しを示しています。 定期的なタイマーがトリガーされると、クライアントロジックは最初に更新された連絡先を独自のシステムから取得します。 これが行われる方法は、独自のシステムからのAPIまたはデータ書き出しを使用するシステムによって異なります。 更新された連絡先情報を取得すると実行されるMarketo APIについて詳しく説明します。 syncMultipleLeadsに対するSOAP リクエスト：

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

syncMultiLeadsからのSOAPの応答：

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

`syncMultipleLeads`はUPSERT操作を実行します。 送信されたメールアドレスに基づいてMarketo内の連絡先が既に存在する場合、属性が更新されます。 連絡先が存在しない場合は、作成されます。 `syncMultipleLeads`からの応答は、送信された各連絡先のステータスを返します。 `<leadAttributeList/>`内の`<attrName/>`値は、そのMarketo サブスクリプションに定義されているSOAP API名と一致する必要があります。 SOAP API名は、フィールド名を書き出すことで、Marketo管理パネル内のフィールド管理セクションで確認できます。

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

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-03-24_ by _Travis Kaufman_

## APIを使用してMarketoからトランザクションメールを送信する

Marketo UIを使用して既存のスマートキャンペーンを作成する必要があります。 また、メール受信者がMarketoに存在する必要もあります。 requestCampaign APIを呼び出す前に、[getLead API] （/help/soap-api/getlead.md）を使用して、メールがMarketoに存在するかどうかを確認します。 requestCampaign APIを介して呼び出しを行った後、Marketoでスマートキャンペーンが実行されているかどうかを確認して確認できます。 最初にスマートキャンペーンを作成する方法、2番目にAPIを介してキャンペーンを送信するトリガーを設定する方法、3番目にフローアクションの一部としてメールを定義する方法、4番目にこのキャンペーンを実行するために使用されるコードサンプルを示します。
**Marketoで新しいスマートキャンペーンを作成する方法** Marketoのスマートキャンペーンは、すべてのマーケティング活動を実行します。 一連の自動化されたアクションを設定して、連絡先のスマートリストを実行できます。 トランザクションメールを送信する場合、以下に示すように、キャンペーンでトリガーを設定して、APIを使用してメールを送信します。 まず、スマートキャンペーンを設定します。 1. マーケティングアクティビティで、プログラムを選択し、「新規」ドロップダウンで「新規ローカルアセット」をクリックします。

1. 「スマートキャンペーン」をクリックすると
1. スマートキャンペーン名を入力し、「作成」をクリックします

**トリガーをスマートキャンペーンに追加** トリガーをスマートキャンペーンに追加すると、ライブイベントに基づいて一度に1人のユーザーでスマートキャンペーンを実行できます。この場合は、[requestCampaign API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/triggerCampaignUsingPOST)を介したリクエストです。 1. 「キャンペーンがリクエストされました」トリガーを検索し、キャンバスにドラッグ&amp;ドロップします。

1. トリガーで、「is」と「Web Service API」を選択します。

**キャンペーンでメールフローアクションを作成する方法**&#x200B;電子メールとスマートキャンペーンとの関連付けにより、マーケターは電子メールをどのように表示するかを管理でき、サードパーティのアプリケーションは誰がいつ受信するかを決定できます。 新しいローカルアセットとしてメールを作成した後、キャンペーンでフローアクションとして設定できます。  送信するメールを探して選択します。

**requestCampaign APIを呼び出すコードサンプル** Marketo インターフェイスでキャンペーンとトリガーを設定した後、APIを使用してメールを送信する方法を示します。 最初のサンプルはXML リクエストで、2番目はXML レスポンスで、最後のサンプルはXML リクエストの生成に使用できるJava コードサンプルです。 また、`requestCampaign` APIを呼び出す際に使用されるキャンペーン IDを見つける方法も示します。
また、API呼び出しには、MarketoキャンペーンのIDを事前に把握する必要があります。 キャンペーン IDは、次のいずれかの方法を使用して決定できます。1. [getCampaignsForSource](/help/soap-api/getcampaignsforsource.md) API 1を使用します。 ブラウザーでMarketo キャンペーンを開き、URL アドレスバーを確認します。 キャンペーン ID （4桁の整数で表されます）は、「SC」の直後に見つけることができます。 たとえば、`<https://app-stage.marketo.com/#SC**1025**A1>` のように設定します。 太字の部分はキャンペーン ID 「1025」です。 `requestCampaign`に対するSOAP リクエスト

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

requestCampaignのSOAP Response

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

上記のシナリオを実行するサンプル Java プログラムを以下に示します。

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

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-03-27_ by _Murta_

## アプリを使用してMarketoから動的コンテンツを含むメールを送信する

コールセンターのフォローアップメールを自動化するとします。 サポート担当者が顧客と話した後、企業への問い合わせに感謝するメールを自動的に送信する必要があります。 さらに一歩踏み込んで、CRMで追跡する顧客と議論した特定の会話のトピックを含めるとします。 これは、requestCampaign SOAP APIを使用してMarketoから実行し、動的コンテンツを含むメールを送信できます。 requestCampaign APIでは、リードまたはリードを渡すことができます。 また、既存のCampaignで使用できるプログラムトークンを渡して、動的コンテンツを送信することもできます。 requestCampaign SOAP APIでは、メール受信者がMarketoに存在する必要があります。 requestCampaign APIを呼び出す前に、[getLead API](/help/soap-api/getlead.md)を使用して、メールがMarketoに存在するかどうかを確認します。 最初にスマートキャンペーンを作成する方法、2番目にAPIを介してキャンペーンを送信するトリガーを設定する方法、3番目にプログラムトークンを介して動的コンテンツを受け入れるメールを作成する方法、4番目にフローアクションの一部としてメールを定義する方法、5番目にこのキャンペーンを実行するために使用されるコードサンプルを示します。**Marketoで新しいスマートキャンペーンを作成する方法** Marketoのスマートキャンペーンは、すべてのマーケティング活動を実行します。 一連の自動化されたアクションを設定して、連絡先のスマートリストを実行できます。 トランザクションメールを送信する場合、以下に示すように、キャンペーンでトリガーを設定して、APIを使用してメールを送信します。 まず、スマートキャンペーンを設定します。 1. マーケティングアクティビティで、プログラムを選択し、「新規」ドロップダウンで「新規ローカルアセット」をクリックします

1. 「スマートキャンペーン」をクリックすると
1. スマートキャンペーン名を入力し、「**トリガーをスマートキャンペーンに追加**」をクリックします。トリガーをスマートキャンペーンに追加すると、ライブイベントに基づいて1人ずつスマートキャンペーンを実行できます。この場合は、[requestCampaign API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/triggerCampaignUsingPOST)を介したリクエストです。
1. 「Campaign is Requested」トリガーを検索し、キャンバスにドラッグ&amp;ドロップします。
1. トリガーで、「is」と「Web Service API」を選択します。

**APIを使用して動的コンテンツを渡す方法** Marketoでは、マイトークンはプログラムで使用できる変数です。 マイトークンを使用すると、プログラムに関連する情報を1か所に入力し、その情報を指定した値に置き換え、メールテンプレートなどのアプリケーションの他の部分でこの情報を取得できます。 requestCampaign SOAP APIを使用すると、プログラムトークンの配列を渡すことができ、これにより既存のトークンが上書きされます。 キャンペーンの実行後、トークンは破棄されます。 マイトークンは、Campaign フォルダーレベルまたはプログラムレベルで作成します。 Campaign フォルダーレベルのマイトークンは、Campaign フォルダー内に含まれるすべてのプログラムに継承されます。 Campaign フォルダーレベルでマイトークンを作成する場合は、継承された値をプログラムレベルで上書きできます。 例えば、プログラムの日付とプログラムの説明のトークンをCampaign フォルダーレベルで定義する場合、個々のプログラムレベルでこれらの値を上書きできます。

その方法は次のとおりです。 1. マーケティング活動ツリーから、トークンを作成するキャンペーンフォルダーまたはプログラムを選択します。 上部のメニューバーから、「マイトークン」を選択します。 マイトークンのキャンバスが表示されます。 右側のツリーから、トークンタイプをキャンバスにドラッグします。この場合は「テキスト」です。 「トークン名」フィールドで「マイトークン」を強調表示し、一意のトークン名を入力します。この場合は「my.conversationtopic」です。 「値」フィールドに、トークンの関連する値を入力します。この場合は、「本日お電話いただきありがとうございます」です。 APIを使用すると、デフォルトのマイトークン値を上書きすることに注意してください。 「保存」をクリックして、カスタムトークンを保存します。  1. 「新規」をクリックして、新しい電子メールを作成します。 次に、「新規ローカルAssets」をクリックし、「電子メール」を選択します。 次に、関連するフィールドに入力して、メールに名前を付けます。 メールを作成するときは、「トークン」アイコンをクリックして、メールにトークンを含めます。 トークンを使用してテンプレートメールを作成したので、次の手順でキャンペーンのフローアクションとしてメールを追加します。 APIを介してキャンペーンを呼び出すと、メールが送信されます。
**キャンペーンでメールフローアクションを作成する方法** メールとスマートキャンペーンとの関連付けにより、マーケターはメールの表示方法を管理でき、サードパーティのアプリケーションはメールを誰がいつ受信するかを決定できます。 新しいローカルアセットとしてメールを作成した後、キャンペーンでフローアクションとして設定できます。 送信する電子メールを検索して選択します。
**requestCampaign APIを呼び出すコードサンプル** Marketo インターフェイスでキャンペーンとトリガーを設定した後、APIを使用してメールを送信する方法を示します。 最初のサンプルはXML リクエストで、2番目はXML レスポンスで、最後のサンプルはXML リクエストの生成に使用できるJava コードサンプルです。 また、requestCampaign APIを呼び出す際に使用されるキャンペーン IDを見つける方法も示します。 また、API呼び出しには、MarketoキャンペーンのIDを事前に把握する必要があります。 キャンペーン IDは、次のいずれかの方法を使用して決定できます。1. [getCampaignsForSource](/help/soap-api/getcampaignsforsource.md) API 1を使用します。 ブラウザーでMarketo キャンペーンを開き、URL アドレスバーを確認します。 キャンペーン ID （4桁の整数で表されます）は、「SC」の直後に見つけることができます。 たとえば、`<https://app-stage.marketo.com/#SC**1025**A1>` のように設定します。 太字の部分はキャンペーン ID 「1025」です。 requestCampaignに対するSOAP リクエスト

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

requestCampaignのSOAP Response

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

上記のシナリオを実行するサンプル Java プログラムを以下に示します。

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

requestCampaign APIを介して呼び出しを行った後、Marketoでスマートキャンペーンが実行されているかどうかを確認して確認できます。

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-04-03_ by _Murta_

## ビジネスロジックにもとづいて匿名の訪問者のアクティビティを取得する

自社ブログの特定の投稿を訪問したオーディエンスを追跡するとします。 例えば、投稿を訪問したユーザーの総数のうち、少なくとも5秒間を費やし、ページを下にスクロールして、興味を示したユーザーのみを追跡したいとします。 匿名ユーザーの場合は、このイベントを使用してMarketoで新しいリードを作成し、既知のユーザーの場合は、このイベントを使用してリードアクティビティを更新します。 これは、web サイトで[Munchkin トラッキングコード ](/help/javascript-api/lead-tracking.md)を使用することで実現できます。 Cookieを使用していないユーザーがMunchkin トラッキングコードを使用してページにアクセスすると、ユーザーのブラウザーに新しいCookieが作成され、Marketoに新しい匿名リードが作成されます。 ユーザーが既にCookieを使用しており、そのユーザーがMarketoの既存のリードである場合、そのページへの訪問はMarketoのユーザーのアクティビティログに記録されます。 最初に、MarketoでMunchkin トラッキングコードを生成する方法、2番目に、特定の条件が満たされた場合にのみトリガーするようにMunchkin サンプルコードを変更する方法、および3番目に、匿名ユーザーからのページ訪問がMarketoに記録されたことを確認する方法について説明します。

**Munchkin トラッキングコードの生成方法** Munchkin トラッキングコードを使用すると、web サイトへの訪問をトラッキングできます。 以下に示すMunchkin コードには3つの種類がありますが、この例では、非同期Munchkin トラッキングコードを使用しています。 A）単純：コードの行が少ないですが、web ページの読み込み時間に最適化されません。 このコードは、web ページを読み込むたびに jQuery ライブラリーを読み込みます。 B）非同期：web ページの読み込み時間を短縮します。 このコードは、jQuery ライブラリが既に存在するかどうかを確認し、存在しない場合は読み込み、web ページの残りの部分が読み込まれたらトラッキングコードを実行するために使用します。 C）非同期jQuery:web ページの読み込み時間を短縮し、システムパフォーマンスも向上させます。 既に jQuery があると想定し、チェックも読み込みも行いません。 1. アプリの右上にある「管理」をクリックします。  1. 左側のツリーで「Munchkin」をクリックします。  1. トラッキングコードタイプは「非同期」を選択します。 1. JavaScript トラッキングコードをクリックしてコピーし、web サイトに配置します。
**コードサンプルをCookie ユーザーに送信してイベントを追跡** トラッキングコードを`</body>` タグの直前にweb ページに配置します。 Marketo で作成したランディングページには、自動的にトラッキングコードが追加されるので、このコードを貼り付ける必要はありません。 このコードサンプルは、スクリプトの読み込み後にMunchkin APIを呼び出します。

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

このコードサンプルは、ユーザーが5秒間ページにアクセスし、ページを500 ピクセル下にスクロールした後に、Munchkin APIを呼び出します。

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

1. 上部メニューの「分析」をクリックし、「新しいレポート」をクリックします。 レポートタイプとして「Web ページアクティビティ」を選択し、レポートに名前を付けます。
1. レポートを作成したら、「スマートリスト」をクリックします。 次に、右側のボックスから「訪問したWeb ページ」フィルターを選択します。 Munchkinのトラッキングコードを入力するweb ページを入力します。
1. 「設定」をクリックします。 ISPから「匿名の訪問者」を選択し、「表示」オプションを変更します。
1. 「Report」をクリックします。 これで、選択したweb ページで追跡されたアクティビティが表示されます。
1. リードレコードをダブルクリックすると、アクティビティログが表示され、匿名ユーザーが訪問した特定のページを確認できます。

この記事には、カスタム統合の実装に使用するコードが含まれています。 そのカスタマイズされた性質により、Marketo テクニカルサポートチームはカスタム作業をトラブルシューティングできません。 適切な技術的経験や経験豊富な開発者へのアクセスなしに、次のコードサンプルを実装しようとしないでください。

投稿日：_2014-04-17_ by _Murta_

## RTPを使用したローカル電話番号の動的な変更

Personalizationがすべてです。私たちはずっと以前にそれを認識していました。 しかし、私が緊急の支援を必要とするたびに、ウェブサイトで関連する現地の電話番号を見つけるのが非常に難しいことは、まだ驚いています。 <https://business.adobe.com/products/marketo/adobe-marketo.html>には[Marketo Real-Time Personalization](https://business.adobe.com/products/marketo/content-personalization.html) （RTP）がインストールされています。 [RTP訪問者API](/help/javascript-api/web-personalization.md)を活用して、Web サイトの様々なセクションでWeb訪問者に表示される電話番号を動的に変更できます。 すごい。 こんなこと信じられますか。 この魔法はどのように機能しますか？ まず、Web サイトにRTPをインストールする必要があります（[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)）。 次に、以下の手順に従って、web サイトにJavaScript コードを実装します。

1. **defaultPhone**&#x200B;設定に国際電話番号を挿入します
1. HTML要素IDを&#x200B;**divIds**&#x200B;設定に挿入します
1. 電話番号をモバイルブラウザーのクリックトゥコールリンクにする場合は、**mobileLink**&#x200B;設定を&#x200B;**true**&#x200B;に設定します。
1. **cityPhone**、**statePhone**、**countryPhone**&#x200B;の設定で、異なる場所を電話番号でマッピングします

例えば、設定設定のサンプル値を次に示します。

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

最後に、**divIds**&#x200B;のいずれかのIDに一致するIDを含むHTML アンカータグを挿入します（上記の手順2以降）。 例えば、**divIds**&#x200B;で「phoneId1」を指定した場合、HTML アンカータグは次のようになります。

`<a href="tel:+1800229933" id="phoneId1">+1800229933</a>`

スクリプトは、次の順序で一致するかどうかをチェックします。cityPhone > statePhone > countryPhone > defaultPhone電話番号をテキストに置き換えることもできます（例：「Join our San Francisco User Group!」）。 位置情報にもとづいてコンテンツを動的に変更できます。 これで、お試しいただくことができます。

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

投稿日：_2016-02-02_ by _Yanir_

## 2016年冬アップデート

### カスタムオブジェクト

* [カスタムオブジェクト N:N関係がサポートされるようになりました](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects)
   * リードレコードまたはアカウントレコードは、中間オブジェクトの定義を介して、カスタムオブジェクトを通じて多対多の関係を持つことができます。 スタンドアロンのカスタムオブジェクトタイプを作成した後、中間オブジェクトタイプは、スタンドアロンオブジェクトとリードまたはアカウントの両方へのリンクフィールドを使用して作成できます。
   * この機能に対する新しいAPI呼び出しはありませんが、APIを介してこれらの関係を活用するには、オブジェクト定義を正しく設定する必要があります。
* `getLeadActivities`と`getLeadChanges`は、匿名リードのアクティビティを返さなくなります。 詳しくは、[次世代Munchkin トラッキング FAQ](https://experienceleague.adobe.com/ja/docs/marketo/using/home)を参照してください

投稿日：_2016-02-05_ by _Kenny_

## REST APIを使用した1つのリードのアクティビティの取得

ここでは、開発者コミュニティから繰り返し質問される質問があります。

「個々のリードの過去のアクティビティのリストを取得するにはどうすればよいですか？」

最近まで、REST APIを使用してこれを達成するための簡単な方法はありませんでした。 しかし、今はあります！ REST APIの2016年冬リリースには、若干の機能強化が含まれています。[リード アクティビティを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET)は、リード IDの指定に使用できる&#x200B;**leadIds** パラメーターを受け入れるようになりました。 **leadIds** パラメーターを指定すると、そのリード IDのアクティビティのみが返されます。 これは、リード ID フィルターと考えることができます。 **leadIds** パラメーターは、複数のリード （最大30）で結果をフィルタリングする場合に備えて、リード IDのコンマ区切りリストを取ることができます。 これは、例えば、特定の企業のリードにアクティビティを制限する場合に便利です。**例**&#x200B;以下は、**leadIds** パラメーターを含む[ リードアクティビティを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET)するためのサンプルリクエストです。 **leadIds** パラメーターに「50」の値を指定しました。これは、Marketo インスタンスの任意のリードに対応します。 activityTypeIds パラメーターに「129」の値を指定しました。これは、Marketo インスタンスの「モバイルアプリセッション」アクティビティに対応します。

`<https://123-abc-456.mktorest.com/rest/v1/activities.json?leadIds=50&activityTypeIds=129&nextPageToken=WQV2VQVPPCKHC6AQYVK7JDSA3J4SMAZRQO4RKIXCEMLFCM2APRSQ====>`

以下は、上記のリクエストからの応答の一部です。 ご覧のとおり、「leadId」:50および「activityTypeId」:129の結果オブジェクトのみが含まれます。

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

## Zapierを使用したMarketoおよび500以上のアプリケーションとのシームレスな統合

Marketoのプリンシパルソリューションコンサルタント、Philippe Delle Case氏による投稿です。

### 目標

この記事では、Zapierを使用して、Marketoを500以上のCloud Appsと統合する方法について詳しく説明します。 そのために、Marketo用のZapier コネクタをゼロから構築し、実用的な2つの統合ユースケースを実装します。ユースケース 1: FullContact Card ReaderからMarketoへの単方向リード統合

* FullContact モバイルカードReaderアプリを使用して、任意のコンタクトの名刺をスキャンすると、Marketoで自動的にリードが作成されます。
* 既存のリードをMarketoの静的リストに追加すると、そのリードがGoogle シートに自動的に追加されます。
* Google シートの任意のリードを変更し、Marketoに反映された変化を見つけます。

### 前提条件

**Zapier**&#x200B;で無料アカウントにサインアップ [Zapier](https://zapier.com/)は、プログラマーやIT リソースを必要とせずに、他のオンラインアプリ間のタスクを簡単に自動化できるweb アプリ自動化サービスです。 簡単な概要は[こちら](https://zapier.com/api/v4/helpdocs/category/redirect/what-is-zapier)にあります。 現在、Zapierは、マーケティング、CRM、CMS、カスタマーサポート、電子サイン、Formsなど、様々な領域で500以上のアプリケーションをサポートしています。あるアプリと別のアプリとの間の単一の統合はZapと呼ばれます。 サポートされているWeb アプリの詳細なリストについては、Zapierの[zapbook](https://zapier.com/apps)を確認してください。  無料アカウント [こちら](https://zapier.com/sign-up/)にサインアップしてください。 1か月あたり最大100件のタスク、5件のザップ、15分ごとに実行されるザップにアクセスできます。 Zapierの有料プラン（ベーシック、ビジネス、ビジネスプラスなど）に加入することで、さらに多くのことを得ることができます。

**管理者または指定されたAPI ユーザーアカウントを使用したMarketo インスタンスへのアクセス** Zapier コネクタでは、Marketo REST APIを使用してリード データをMarketoにプッシュします。 このAPIを使用するには、Marketo インスタンスの管理者であれば、自分で作成できるAPI ユーザーとカスタムサービスが必要です。 そうでない場合は、管理者がそれらを提供する必要があります。 また、Marketo AdministratorのみがアクセスできるWebhookを作成することもできます。 Marketo API ユーザーとカスタムサービスの作成方法について、手順ごとの説明は[こちら](http://rest-api/custom-services/)を参照してください。 完了したら、Marketo REST APIを呼び出すための次の資格情報が必要です。クライアント ID、クライアントシークレット、Munchkin アカウント ID、Munchkin アカウント ID

Munchkin アカウント IDは、MunchkinまたはWeb サービスの管理画面から取得できます。 パターンは次のようになります：`000-XXX-000`。  アクセストークンは1時間のみ有効なので、取得する必要はありません。 コネクタが自動的にトークンを生成します。
**Google Docs、Sheets、Slidesで無料アカウントにサインアップすると、さまざまな種類のオンラインドキュメントを作成し、他のユーザーとリアルタイムで作業し、Google Drive Onlineに保存できる生産性向上アプリです。 このユースケースにはGoogleシートが必要です。 Google Docsのさまざまな機能と、Googleを使用したアカウントの作成については、[こちら](https://workspace.google.com/products/docs/)を参照してください。
**FullContact** FullContactで無料アカウントにサインアップすると、すべての連絡先を引き出して、ソーシャルプロファイル、写真、電子メール署名、会社情報などの変更と継続的に同期することで、最も重要な人物とつながることができます。 同社は、Zapierを含む250以上のWeb アプリにカードをスキャンできるモバイル名刺リーダーを提供しています。 無料アカウントに登録できます[こちら](https://app.fullcontact.com/login)。 また、より多くの機能と容量を備えたプレミアム有料アカウントに登録することもできます。 モバイルアプリは、[Apple AppStore](https://apps.apple.com/us/app/fullcontact-business-card/id576780807)または[Google Play](https://play.google.com/store/apps/details?id=com.fullcontact.cardreader)からダウンロードできます。 FullContact Zapsは[こちら](https://zapier.com/apps/contacts-plus/integrations)に記載されています。

### Zapier用Marketo コネクタの実装

**Marketo アプリを作成** Zapier web インターフェイスから、Developers Portalに移動します。 「**新しいアプリを追加**」をクリックし、少なくともタイトル（「Marketo」など）と説明を入力します。 このロゴはオプションですが、あると便利です。\ **Authentication**&#x200B;この節では、Marketo REST API認証と認証設定に使用される様々なフィールドを宣言します。 最初に次のフィールドを作成します。

「認証設定」を編集します。

* 認証タイプ：セッション認証
* 認証マッピング：

  `{"access_token":"{{access_token}}"}`

* アクセストークンの配置**：クエリ文字列の** トークン

Marketo カスタムサービスを作成すると、クライアント IDとクライアントシークレットが使用可能になります。 クライアント IDとクライアント秘密鍵を使用して、REST API [認証](/help/rest-api/authentication.md) エンドポイントを介してアクセストークンを生成します。 その後、このアクセストークンを使用して、REST APIに対するその後のリクエストを行うことができます。 トークンは1時間後に期限切れになり、REST APIの呼び出しを続行するには再度生成する必要があります。 セッショントークンが期限切れになるたびにカスタム認証スクリプトを実行できるため、認証タイプ = 「セッション認証」を選択しました。 このタイプの認証でのみ動作するメカニズムを実装する方法については、「スクリプト API」の節を参照してください。
**トリガー**&#x200B;のZapier トリガーが存在し、データをZapierに取り込みます。 代わりにMarketo Webhookを活用するため、ユースケースに使用する必要はありません。 ただし、Marketo コネクタの必須テストとしてダミートリガーを記述する必要があります。 Marketo REST API [毎日の使用状況を取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getDailyUsageUsingGET) トリガーを呼び出すテスト エンドポイントを作成します。 「**新しいトリガーを追加**」をクリックしてウィザードを開始し、次のフィールドに入力します（言及されていないフィールドは空白のままにできます）。名前と説明

* 名前：テストトリガー
* キー：test_トリガー
* 説明：Marketo アプリのテストトリガー
* 重要ですか？ 未検証
* 隠す？ チェック済み

トリガーフィールド

* None

データの出所

* Data Source：ポーリング
* ポーリング URL: `https://{{munchkin_account_id}}.mktorest.com/rest/v1/stats/usage.json`

サンプル結果

* 空白のままにする

「**トリガー設定を管理**」をクリックし、ユーザーの資格情報の検証に使用するテストトリガーを設定します。**アクション** Zapierからデータを送信するためのアクションがあります。 Marketo REST APIを呼び出すCreate_Update リードアクションを実装します。 このアクションにより、Marketo内で新しいリードを作成できます。または、リードが既に存在する場合は、送信された値でリードを更新します。 重複排除には「email」フィールドを使用します。 「**新しいアクションを追加**」をクリックしてウィザードを開始し、次のフィールドに入力します（言及されていないフィールドは空白のままにできます）。名前と説明

* 名前：Create_Update リード
* 名詞：リード
* キー：create-update-lead
* 説明：Marketo内で新しいリードを作成するか、リードが既に存在する場合は、送信された値でリードを更新します
* 重要ですか？ チェック済み
* 隠す？ 未検証

アクションフィールド アクションフィールドとは、ユーザーがデータをマッピングするフィールドです。 Marketoで更新できるあらゆるデータを表すカスタムオブジェクトを、ニーズに合わせて注意深く選択してください。 Zapierには、Marketoで利用可能なすべてのフィールドをエンドユーザーに提供するオプションがありますが、これは、使い捨てコネクタに必要なコードや複雑さを引き起こします。 例として、次のフィールドを選択しました。

Marketo インスタンスではリード パーティションがサービス中であるため、パーティション名は必須です。 それ以外の場合は省略できます。 エンドユーザーが、同期するフィールドではないことを理解できるように、「input」グループから分離しました。 「メモ」フィールドは、MarketoとSalesforce間の同期に基づいています。Marketo インスタンスに同期がない場合は、このフィールドを使用しないでください。 「呼び出し済み」フィールドはMarketo インスタンスで作成されました。Marketo インスタンスにフィールドがない場合は、このフィールドを使用しないでください。 Marketoから必要なフィールドを選択できます。 小さく始めて、後で追加のフィールドを追加することをお勧めします。 データの送信先

* アクション エンドポイント URL: `https://{{munchkin_account_id}}.mktorest.com/rest/v1/leads.json`

サンプル結果

* 空白のままにする

### Zapier Scripting API

Zapierのスクリプト機能を使用すると、アプリのAPIとZapier間で交換されるリクエストと応答を操作できます。 HTTP リクエストを送信する直前に変更し、Zapierがリクエストを処理する前にレスポンスを解析できます。 Marketoで動作するように、カスタム「セッション認証」認証を完了する必要があります。 詳細については、[こちら](https://zapier.com/developer/documentation/scripting/)を参照してください。 次のコードをコピーして、後でいくつかの説明を説明します。

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

* このメソッドは、Marketo REST API [Authentication](/help/rest-api/authentication.md) エンドポイントを呼び出すアクセストークンの生成または再生成を担当します。
* これは、「post_poll」メソッドが「Access Token Expired」エラーを検出するたびに呼び出されます。 アクセストークンは1時間ごとに有効期限が切れるようにスケジュールされているので、これは想定されています。
* アクション エンドポイント URL: https://{{munchkin_account_id}}.mktorest.com/identity/oauth/token

**pre_poll, pre_write**

* 作成したトリガーに「事前調査」メソッドを作成し、HTTP リクエストが送信される直前に変更して、Marketo アクセストークンをパラメーターに追加できるようにする必要があります。
* 同じ理由で、作成したアクションに「プリライト」メソッドを作成する必要があります。

**post_poll, post_write**

* Zapierが何かを行う前に回答を解析し、最終的に「アクセストークン期限切れ」エラーをインターセプトするために、作成したトリガーに「post-poll」メソッドを作成する必要があります。
* 同じ理由で、作成したアクションに「書き込み後」メソッドを作成する必要があります。
* そのようなエラーが発生した場合は、認証を再生し、get_session_info メソッドを再実行するようZapierに指示するInvalidSessionExceptionをスローします。

なお、スクリプティング APIからバンドルログには、画面の右上隅にある「クイックリンク」メニューからアクセスできます。 これは、スクリプトをデバッグするのに非常に便利です。

ユースケース 1: MarketoとFullContact Card Readerの統合

この統合のために、FullContactからMarketoへの1つのZapを作成します。 このZapを使用すると、FullContact Mobile Card Readerで名刺をスキャンし、リードをMarketoにプッシュできます。   **Zap FullContact -> Marketo** Zapier ダッシュボードから「新しいZapを作成」ボタンをクリックします。

Zapier **の**&#x200B;トリガー

* アプリ FullContactを選択
* FullContact トリガー「New Business Card」を選択
* FullContact アカウントに接続
* FullContact アプリのテスト

**Zapierでのアクション**

* 先ほど作成したアプリMarketoを選択します。Betaに表示されます
* Marketo アクション「Create_Update リード」を選択
* Marketo アカウントに接続し、認証パラメーター（Munchkin アカウント ID、クライアント ID、クライアントシークレット）を入力します
* FullContactからMarketoへのフィールドのマッピング
* 新しいリードを追加するパーティション名を入力します（Marketo インスタンスにパーティションがある場合のみ）。
* Marketo アプリのテスト
* Zapを有効化

注意：FullContactから名刺Readerをダウンロードし、モバイルデバイスから直接Zapier Integrationを有効にしてください。

ユースケース 2:MarketoとGoogle シートの統合 – 

この統合では、2つのZapを作成します。 1つはMarketoからGoogleシートに、もう1つはGoogleシートからMarketoに変換されます。 このZapを使用すると、MarketoとGoogle シートの間でリードや連絡先の一部を同期できます。   **Zap Marketo Webhook -> Google Sheets**
最初のZapでは、Marketo用のカスタムコネクタに依存していませんが、MarketoのWebhookと「Webhook by Zapier」トリガーを活用しています。 Zapier ダッシュボードから、「新しいZapを作成」ボタンをクリックします。**Zapier**&#x200B;のトリガー パート 1

* 「Webhook by Zapier」トリガーアプリを選択
* POSTまたはGETからZapier URLへの待機を許可する「キャッチフック」をチェックします
* 子キーをオフにする必要はありません
* Zapierは、リクエストを送信するためのカスタム **Webhook URL**&#x200B;を生成し、クリップボードにコピーしました

**MarketoのWebhook （管理者が実行する手順）**

* 管理者 / Webhookに移動します
* 「リードをZapierにプッシュ」という新しいWebhookを作成し、Webhook フォームを編集します。

テンプレートのフィールドで、Zapierに転送するリードのフィールドをすべて宣言し、Marketoのトークンを活用します。 このユースケースでは、リードをMarketoにプッシュするカスタム Zapier コネクタに定義したフィールドと同じフィールドを使用します。

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

* フォームを保存
* 応答マッピングは不要なので、Webhookを使用します

**MarketoでCampaignをテストする（マーケターまたは管理者が実行する手順）**

* マーケティング活動から、新しいスマートキャンペーンを作成し

テスト目的では、リードステータスがMQLに変更されるたびにWebhookをトリガーとするキャンペーンを作成します。 もちろん、Webhookは他のビジネス目的でも使用できます。

* スマートリストの編集
* フローでWebhookを呼び出します
* キャンペーンのスケジュール
* 各リードが毎回フローを実行できるようにし
* スマートキャンペーンのアクティベート

Zapier **の**&#x200B;トリガー パート 2

* 「Webhook by Zapier」トリガーアプリを完成させるには、Marketo Smart Campaignを一度起動し、ZapierでWebhookをキャッチする必要があります
* テストケースでは、Marketo リードデータベースに移動し、リードを開き、ステータスを「MQL」に変更するだけです

**Google シートでスプレッドシートを作成**

* 新しいスプレッドシートの作成
* ワークシートを作成するか、デフォルトを使用します
* Marketoから同期する各フィールドの列（MarketoのWebhookで宣言された列）を追加します

  **Zapierでのアクション**

* アプリのGoogle シートを選択
* 「スプレッドシート行を作成」オプションをオンにします
* Google Sheets アカウントに接続
* Google Sheets スプレッドシートを選択
* ワークシートを選択
* 「Webhook by Zapier」トリガーアプリとGoogle Sheetsの間のすべてのフィールドをマッピングします。

* Google Sheets アプリのテスト
* Zapを有効化

**Zap Google Sheets -> Marketo**

Zapier ダッシュボードから、「新しいZapを作成」ボタンをクリックします。

Zapier **の**&#x200B;トリガー

* 「Google Sheets」トリガーアプリを選択
* スプレッドシートで新しい行が追加または変更されたときにトリガーされる「更新されたスプレッドシート行」をクリックします
* Google アカウントに接続する
* トリガー元のスプレッドシート（前のZapで使用したものと同じである必要があります）とワークシートを選択します
* トリガーカラムを「any_column」に設定
* Google Sheets アプリのテスト

**Zapierでのアクション**

* 先ほど作成したアプリMarketoを選択します。Betaに表示されます
* Marketo アクション「Create_Update リード」を選択
* Marketo アカウントに接続し、認証パラメーター（Munchkin アカウント ID、クライアント ID、クライアントシークレット）を入力します
* Google シートからMarketoへのフィールドのマッピング
* 新しいリードを追加するパーティション名を入力します（Marketo インスタンスにパーティションがある場合のみ）。
* Marketo アプリのテスト
* Zapを有効化

### まとめ

Zapier用Marketo コネクタの改善点をいくつか紹介します。

* 様々なMarketo オブジェクト（リスト、カスタムオブジェクトなど）に関連するその他のトリガーとアクションの追加
* Marketoからフィールドをハードコーディングする代わりに、Marketoからフィールドを動的に取り込むことができますが、これにはMarketoとZapierの間の技術的な翻訳作業が必要になります。
* コネクタを開発チームと共有し、最終的に一般公開します。

ZapierがPremium Marketo アダプタをデプロイする可能性があります。これにより、ユースケースの実装がはるかに簡単になります。 いずれにしても、この記事は、MarketoとZapierを無料のZapier プランと統合したり、プレミアムアダプタでサポートされていないカスタムユースケースを構築したりするために、いつでも活用できます。 この記事を楽しんでいただき、MarketoとZapierでさらに成功を収めることができることを願っています。 ありがとうございました。

投稿日：_2016-04-17_ by _David_

## 2016年春アップデート

**REST API**

* Asset API - Web ページ
   * **ランディングページ**&#x200B;は、15個の新しいエンドポイントを介して公開されるようになりました。これにより、ランディングページの作成、更新、削除、複製、ドラフト管理が可能になります。 ランディングページテンプレートには、ドラフト管理エンドポイントも公開されるようになりました
      * ランディングページを取得
      * ID によるランディングページを取得
      * 名前によるランディングページを取得
      * ランディングページを作成
      * ランディングページメタデータを更新
      * ランディングページコンテンツを取得
      * ランディングページコンテンツセクションを追加
      * ランディングページコンテンツセクションを更新
      * ランディングページコンテンツセクションを削除
      * 動的コンテンツセクションを取得
      * 動的コンテンツセクションの更新
      * ランディングページのドラフトを破棄
      * ランディングページの承認
      * ランディングページのドラフトを未承認にする
      * ランディングページを削除
   * **ランディングページテンプレート**
      * ランディングページテンプレートのドラフトを破棄
      * ランディングページテンプレートの承認
      * ランディングページテンプレートを無効にする
      * ランディングページテンプレートを削除
   * **Forms**&#x200B;には21の新しいエンドポイントがリリースされ、APIを介した完全な作成、編集、管理機能が提供されます。 APIは、Forms 1.0 フォームへの変更をサポートしません。
      * フォームを取得
      * ID によるフォームを取得
      * 名前によるフォームを取得
      * フォームフィールドリストを取得
      * フォームフィールドリストの更新
      * フォームを作成
      * フォームのサンキューページを取得
      * フォームのサンキューページを更新
      * フォームを更新
      * フォームのドラフトを破棄
      * フォームの承認
      * フォームを承認しない
      * フォームを複製
      * フォームを削除
      * フォームフィールドを更新
      * フォームフィールドを削除
      * フォームフィールドの表示ルールの更新
      * リッチテキストフォームフィールドを追加
      * Add Fieldset
      * フィールドセットからフィールドを削除
      * 使用可能なフォームフィールドを取得
      * フォームフィールドの位置を変更
      * 送信ボタンを更新
   * **プログラムの取得または参照**&#x200B;を使用する場合、SFDC キャンペーンにリンクされているプログラムに対して、SFDC キャンペーン IDが返されます

**カスタムオブジェクト** カスタムオブジェクトは、テキスト領域のデータタイプをサポートするようになり、このタイプのカスタムオブジェクトフィールドに最大2000文字の文字列フィールドを格納できるようになりました。**IP アドレスのホワイトリストへの登録**&#x200B;管理者ユーザーは、API経由での不正アクセスを防ぐために、IP アドレスのホワイトリストを管理できるようになります。[この機能について詳しくは、](https://experienceleague.adobe.com/ja/docs/marketo/using/home)を参照してください。**カスタムアクティビティ UI**&#x200B;管理者ユーザーは、管理メニューでカスタムアクティビティタイプを定義し、[ カスタムアクティビティを追加](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addCustomActivityUsingPOST) APIを介してリードにレコードを追加できるようになりました。[カスタムアクティビティタイプの定義については、こちらを参照してください](https://experienceleague.adobe.com/ja/docs/marketo/using/home)。

投稿日：_2016-06-01_ by _Kenny_

## 2016年夏アップデート

9月23日の2016年夏リリースでは、3つの開発者向け機能がリリースされています。

### REST APIでのメール 2.0のサポート

v1.0電子メールとテンプレートにのみ対応していた既存の[既存のアセット API](/help/rest-api/assets.md)はすべて、v2.0電子メールアセットで使用できるようになりました。

### Marketo にリードをプッシュ

[ プッシュリード ](/help/rest-api/leads.md)は、スマートキャンペーンで簡単にトリガーできるように設計された代替リード同期方法です。 1回の呼び出しで、1つのアクティビティログ項目を作成し、リードを関連付け、リードレコードを更新できます。 これは、リードが単一のフォームに入力する場合と同様に機能し、既存のリード同期メソッドを使用する代わりに、フォーム送信のプロキシメソッドとしてより簡単に使用できます。

### HTTP 圧縮

REST APIは、HTTP 1.1仕様で定義された標準を使用して応答を圧縮できるようになりました。 これは、転送速度を向上させる応答のサイズを小さくし、帯域幅の利用を最小限に抑えるのに役立ちます。  

投稿日：_2016-09-23_ by _Kenny_

## Marketoでのswagger-codegenの使用

[Swagger-codegen](https://github.com/swagger-api/swagger-codegen)は、Swagger定義からサーバースタブとAPI クライアントの両方を生成できる強力なJava ライブラリです。 これにより、特定の言語に対して顧客を生成する際の困難さとコストを大幅に軽減できます。 最初に、最初のクライアントを生成するには、まず、MarketoのSwagger定義の1つのインスタンス固有のコピーを取得します。 テスト対象のインスタンスからMunchkin IDを入力します。 ID定義から始めます。 これで、インスタンスに固有の定義ができたので、swagger-codegenをダウンロードしてインストールする必要があります。 このプロセスはオペレーティング システムに固有であり、次の手順を実行できます。[ここ](https://github.com/swagger-api/swagger-codegen#prerequisites) デフォルト設定では、codegenは提供されたすべてのエンドポイントとモデルをカバーするクライアントを出力します。 これらは通常、DefaultApiと呼ばれるクラスを通じて管理され、「docs」フォルダーに指定された例を使用して利用可能なエンドポイントを呼び出すメソッドが含まれます（すべての言語にデフォルトでこれに対するテンプレートが含まれているわけではありません）。 次に、最初のクライアントを作成します。 コードを公開するフォルダーを作成し、ターミナルセッションに移動し、生成コマンドを使用して、必要な言語でクライアントを構築します（homebrew install メソッドを使用したと仮定します）。

swagger-codegen generate -i $definitionLocation -l $yourLanguage -o $yourLocation

これにより、クライアントコードが目的の場所に出力されます。 次に、これを使用してID エンドポイントを呼び出し、アクセストークンを取得します。

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

承認方法を理解したところで、自動生成されたクライアントのより高度なユースケースを今後数週間で見ていきます。

投稿日：_2016-10-10_ by _Kenny_

## Excel統合パート 1:Power Queryを使用したMarketo データの抽出とシェイプ

Microsoft Excelに組み込まれたPower BI テクノロジを活用して、Marketoで真のセルフサービス型のビジネス分析体験を構築する方法について解説した一連の記事の最初の記事です。 これらの記事で取り上げた概念を使用すると、次のことが可能になります。

* MarketoからExcelへのデータのインポート
* 他のソース（SaaS アプリケーション、データベース、フラットファイルなど）からのデータをインポートして組み合わせる
* ビジネスニーズや分析目的に合わせたデータの形成
* Excelからデータをオンデマンドで更新します
* 数式を使用した分かりやすい計算列と測定の作成
* 異種データ間の関係の構築
* ピボットテーブルとピボットチャートによるデータ分析と高度なレポートの作成
* 優れたデータビジュアライゼーションの作成

### Power Query for Excel

この最初の記事では、Power Query テクノロジーを使用したデータの読み込みと整形プロセスについて説明します。 Power Queryは、分析ニーズに合わせてデータ ソースを検索、接続、結合、調整できるデータ接続テクノロジーです。 Power Queryの機能は、ExcelとPower BI Desktopで利用できます。 Power Queryは、データベース、Facebook、Salesforce、MS Dynamics CRMなど、多くのデータソースに接続できます。Marketoは標準でサポートされていませんが、幸いなことに、システムの多くの機能をリモートで実行するためにMarketo REST APIを使用できます。Power Queryには、カスタムデータソースをスクリプト化できる豊富な数式（非公式では「M」）が付属しています。

### カスタムコネクタ

Power Queryを使用して1回のREST API呼び出しをスクリプト化することは簡単ですが、次の要件を処理するのは困難になります。

* 認証メカニズムと定期的なトークン更新を含むアクセストークン管理
* 大規模データセットのページネーション機構
* エラー処理

ここでは、MarketoのREST APIを使用して、あらゆる種類のデータ（リード、アクティビティ、カスタムオブジェクト、プログラムなど）を取得できる堅牢なカスタムコネクタを構築する方法について説明します。 制限は、Marketo APIの日次リクエスト制限までです。 ここで説明する概念はMarketoに重点を置いていますが、REST APIを提供する他のSaaS ソリューションを統合するために使用することもできます。

### 前提条件

#### Power Query

Excel 2016のリリース以前は、Excel用Microsoft Power Queryは、Excel 2010またはExcel 2011にダウンロードしてインストールされたExcel アドインとして機能していました。 Excel 2016から、この技術は「Get &amp; Transform」セクションの「Data」リボンに統合されたネイティブ機能です。 この記事のために作成されたすべてのスクリプトは、Windows用のExcel 2016でテストされています。 コンセプトはExcel 2013またはExcel 2010と同じである必要がありますが、一部の適応が必要になる場合があります。  Power Queryは現在、Microsoft Windows版のExcelでのみ利用できます。Mac版は残念ながらサポートされていません。

#### Marketo

Power Queryは、Marketo REST APIを使用してMarketoからデータにアクセスします。 これらのAPIを使用するには、Marketo インスタンスの管理者であれば、自分で作成できるAPI ユーザーとカスタムサービスが必要です。 そうでない場合は、管理者がそれらを提供する必要があります。 Marketo API ユーザーとカスタムサービスの作成方法について、手順ごとの説明は[こちら](/help/rest-api/custom-services.md)を参照してください。 完了したら、次の資格情報を使用してMarketo REST APIを呼び出す必要があります。**クライアント ID**&#x200B;と&#x200B;**クライアントシークレット**。 **REST API エンドポイント**&#x200B;は、MarketoのWeb サービス管理者のREST API セクションにあり、次のパターンを持つ必要があります。

`<https://XXX-XXX-XXX.mktorest.com/rest>`

MarketoにはAPIの日次リクエスト制限があり、この制限はWeb サービス管理者と使用状況レポートで確認できます。**レポート**&#x200B;の一部のデータを見逃す可能性があるため、クエリをデザインするときは、1日の制限を超えないようにしてください。

### Power Query Workbookの作成

新しいExcel ブックを作成します。 すべてのMarketo REST API設定を宣言するための特定の設定ワークシートを作成します。 このワークシートでは、次の3つのテーブルを作成します。

次の列を含むテーブル &#39;**REST_API_Authentication**&#39;: **URL**: Marketo REST API エンドポイント。**クライアント ID**:Marketo REST API OAuth2.0資格情報から。**クライアント秘密鍵**:Marketo REST API OAuth2.0資格情報から。
表&#39;**スコーピング**&#39;と列：**Paging Token SinceDatetime**: ISO 8601標準日付表記法に従う日付（例：「2016-10-06T13:22:17-08:00」、「2016-10-06」は有効な日付/時刻）。これは、最初の「日付ベース」のページングトークンのおかげで、指定された期間からMarketo アクティビティ取得に使用されます。 この日付は、主にワークブックに読み込むデータ量を制限するために使用されます。**リスト ID**：扱っているすべてのリード/取引先責任者を参照するMarketoの静的リストのID。 この静的リストは、Marketoで自由に管理できます（例：スマートキャンペーンは、リードや取引先責任者に定期的またはリアルタイムで提供できます）。
静的リストのIDを取得するには、静的リストをMarketoで開き、URLから数値IDを取得します（例：`<https://myorg.marketo.com/#ST3517A1LA1>`、List ID=3511）。**最大レコードページ**：これは、1 ページあたり最大レコード数が300の「ポジションベース」ページングトークンを使用して、Marketo出力データを繰り返し処理する疑似再帰アルゴリズムに使用されます。 ページごとにできるだけ多くのレコードを取得することが私たちの関心なので、300にとどまります。 そのため、通常、最大レコードページ数が33.333に設定されている場合、33.333 X 300 = 9.9999百万レコードのキャパシティを意味します。Marketo APIの日次リクエスト制限では、33.333 Kも意味します。 アルゴリズムは、クエリからのすべてのデータが取得されるとすぐに停止します。そのため、このパラメーターはループの安全制限に過ぎません。

列が&#x200B;**リードフィールド**&#x200B;のテーブル `Leads`：リードと取引先責任者のクエリ時にMarketoから収集するリードフィールドをコンマで区切りました。 Excelで表を宣言するのは簡単です。 スプレッドシートに列の名前と値を含む2つの行を入力し、マウスで表の周囲を強調表示し、「挿入」メニューでアイコン「表」を選択して、名前を付けます。 テーブルとその列に与えられた名前は、スクリプトによって直接呼び出されるため重要です。

## 認証とアクセストークン

### Marketo REST API認証について

MarketoのREST APIは、2 レッグ OAuth 2.0で認証されます。 クライアント IDとクライアントシークレットは、定義したカスタムサービスによって提供されます。 各カスタムサービスは、サービスが特定のアクションを実行することを許可するロールと権限のセットを持つ API 専用ユーザによって所有されます。 アクセストークンは、単一のカスタムサービスに関連付けられます。
完全な認証メカニズムについては、Marketo Developer サイトの[ここ](/help/rest-api/authentication.md)に記載されています。 アクセストークンが最初に作成された場合、その有効期間は3600秒または1時間です。 同じカスタムサービスに対する連続した認証呼び出しごとに、残りの有効期間を含む現在のアクセストークンが返されます。 トークンの有効期限が切れると、認証によって新しいアクセストークンが返されます。 アクセストークンの有効期限を管理することは、統合がスムーズに機能し、通常の操作中に予期しない認証エラーが発生するのを防ぐために重要です。

#### クエリを作成

「データ」メニューの「Get&amp;Transform」セクションの「New Query」アイコンをクリックして、新しいクエリを作成します。 最初に空白のクエリを選択し、「MktoAccessToken」などの名前を付けます。 クエリエディターから高度なエディターを起動して、Power Queryの数式を手動でスクリプト化できます。 アドバンスドエディターに次のコードを入力します。

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

ソースコードに埋め込まれたコメントの前に「//」を付けると、コードが自明になります。 関数の参照が必要な場合は、この記事の「参照」セクションに記載されているリンクを確認してください。 「完了」ボタンをクリックしてください。 最後に適用されたステップ「accessTokenStr」の出力にアクセストークンが正常に表示されていることを確認します。  Excelのセキュリティに関する簡単なコメントです。黄色いバナーから外部データ接続を有効にするように求められることがあります。 これは、クエリを適切に動作させるために必要です。

#### クエリを関数に変換する

アドバンスドエディターに戻り、コードを次の関数宣言でラップします。

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

関数は入力のパラメーターを受け取りませんが、設定ワークシートからパラメーターを取得します。 出力としてアクセストークンが生成されます。 クエリ `FnMktoGetAccessToken`の名前を変更して保存します。 データ メニューの「取得と変換」セクションの「クエリを表示」ボタンをクリックすると、すべてのクエリをいつでもExcelで表示できます。 これで、関数アイコン「Fx」が表示されます。

### 静的リストのメンバーの読み込み

#### ガイドを読む

Marketo リード APIは、リードレコードに対するシンプルなCRUD操作、静的リストおよびプログラムでのリードのメンバーシップを変更する機能、リードに対してスマートキャンペーン処理を開始する機能を提供します。 これらの機能はすべて[こちら](/help/rest-api/leads.md)に記載されています。 静的リストまたはプログラムのメンバーシップに基づいて、大規模なリードレコードのセットを取得できます。 静的リストのIDを使用すると、その静的リストのメンバーであるすべてのリードレコードを取得できます。 リストのIDは、呼び出しのパスパラメーターです。 詳しくは、Marketo Developers ドキュメントの「リストとプログラムメンバーシップ」の章を参照してください。 API呼び出しごとに取得できるリードレコードの最大数は300なので、ページングトークンを活用して300件のレコードのページごとにレコードを収集する必要があります。 最初の呼び出しの後、Jsonの回答でページングトークンを取得します。ページングトークンが出力に表示されなくなった場合に実行されます。

### 基本クエリ

静的リストからすべてのリードをダウンロードすることを目的とした、完全に機能するクエリを始めましょう。 「MktoLeads」という名前の新しい空のクエリを作成し、詳細エディターに次のコードを入力します。

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

Power Queryでは、従来のループ機能（例：For-loop、While-loop）と呼ばれ、繰り返しはサポートされていません。 良い回避策は、List.Generateを使用してFor ループを実装することです。 この関数は[こちら](http://msdn.microsoft.com/query-bi/m/list-generate)で文書化されています。 リスト付き。 生成するページを繰り返し処理できます。 反復の各ステップで、データのページを抽出し、次のページのページングトークンを含むURLを保持し、生成されたリストの次の項目に結果を保存します。 [Datachant](https://datachant.com/2016/06/27/cursor-based-pagination-power-query/)のブログは、この問題を解決するための素晴らしいリソースでした。 パラメーター「最大レコードページ」は、ページ数を制限し、無限ループを回避する現実的な範囲に制限するためにここにあります。 もう1つの課題は、アクセストークンが期限切れにならないようにすることです。 残りの有効期間を追跡すると、Power Queryでは複雑すぎるでしょう。 そのため、REST APIへのすべての呼び出しはエラーチェックでバックアップされます。エラーが発生した場合、トークンは期限切れであると見なされ、最初に更新して、呼び出しを再度再生します。 2回目の呼び出しが失敗した場合、2回目の失敗はExcelに通知されます（最悪の場合、結果としてデータは取得されません）。 クエリを保存するか、いつでも「更新ボタン」をクリックして、クエリを起動します。  今回の例では、5つのリスト内の5 ページのデータから1,364件のリードレコードを抽出しました。

### データの形成

あらゆるレコードを単一のフラットリストで保持するように、データを整形する必要があります。 これにはふたつの方法があります。

* その他のコードの使用
* Power Query UIの活用

出力グリッドを右クリックし、コンテキストメニューの「表へ」を選択して、リストの表に変換します。  「テーブルへ」ポップアップで、2つのピックリストにデフォルト値を残します。  次に、リストのテーブルを展開します。 これで、すべてのレコードが単一のリストになりました。 Json形式でエンコードされたレコードには、フィールドと関連する値が含まれています。 もう一度展開します。 保持するフィールドをすべてポップアップで選択し、「元の列名をプレフィックスとして使用」チェックボックスのチェックを外します。  ほら！ すべてのレコードがテーブルに表示されます。 詳細エディターを再度開くと、データを形作るために3行のコードが追加されていることがわかります。

```
# "Converted to Table" = Table.FromList(GeneratedList, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
# "Expanded Column1" = Table.ExpandListColumn(#"Converted to Table", "Column1"),
# "Expanded Column2" = Table.ExpandRecordColumn(#"Expanded Column1", "Column1", {"id", "updatedAt", "lastName", "email", "createdAt", "firstName"}, {"id", "updatedAt", "lastName", "email", "createdAt", "firstName"})
```

計算された値を持つ追加の列を作成するなど、Power Queryでさらに多くのことができます。後でさらに多くの可能性が表示されます。 クエリを保存して閉じます。 いつでも手動で更新することも、バックグラウンド更新を通じて自動的に更新することもできます。

### 結果のリダイレクト

問題は、結果データをどこで送信するかです？ クエリにマウスを合わせ、コンテキストメニューの「読み込み先…」メニューを選択します。 ポップアップで、次を選択できます。

* すべてのシェイプデータをワークシート（新規または既存）に送信する場合は、「テーブル」,
* Power Pivotでさらに分析を行う場合は、「接続を作成する」のみを選択します。

「データモデルに追加」チェックボックスをオンにすると、Power ピボットのデータを活用できます。この記事の2番目の部分では、このオプションを使用します。

### ページネーションの管理

このプロジェクトの目的は、さらに多くのクエリを作成することなので、リファクタリングを行って、ページネーションを管理する再利用可能な関数を抽出しましょう。 **FnMktoGetPagedData**&#x200B;という名前の新しい空のクエリを作成し、詳細エディターに次のコードを入力します。

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

クエリを保存します。 次に使おうと思います。

### 簡素化されたクエリ

**FnMktoGetPagedData**&#x200B;関数を呼び出すクエリ &#39;MktoLeads&#39;をもう一度書き換えましょう。

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

ご覧のとおり、クエリの読み取りとメンテナンスが本当に簡単になりました。 他のクエリに対して&#x200B;**FnMktoGetPagedData**&#x200B;関数を再び活用します。

### 定義された期間から特定のアクティビティを読み込む

#### ページネーションを使用したアクティビティの取得

Marketo では、リードレコードに関連する様々なアクティビティタイプが許可されます。 ほとんどすべての変更、アクション、フローステップは、リードのアクティビティログに対して記録され、API 経由で取得したり、スマートリストやスマートキャンペーンのフィルターとトリガーで活用したりできます。 アクティビティは、常にleadIdを介してリードレコードに関連付けられ、レコードのIDに対応し、独自の一意の整数IDも持ちます。 完全なREST API ドキュメントは[こちら](/help/rest-api/activities.md)にあります。

潜在的なアクティビティタイプは非常に多く、サブスクリプションごとに異なる場合があり、それぞれに一意の定義があります。 各アクティビティには独自の一意のID、leadIdおよびactivityDateがありますが、primaryAttributeValueIdおよびprimaryAttributeValueの意味は異なります。 MarketoがID 41で追跡したアクティビティの1つである「Interesting Moments」に焦点を当てます。 これから解決する新しい課題は次のとおりです。

* アクティビティが発生した時間を定義するために、「日付ベース」のページングトークンを開始する必要があります，
* アクティビティのタイプに応じて、アクティビティ固有の属性のリストがJsonで提供されるため、分析を容易にするためにデータを解析してフラットアウトする必要があるため、データの整形は少し難しくなります。

#### 日付ベースのページングトークン

最初にこの関数を構築して、Activity クエリの期間をスコープするために必要な、最初の「日付ベース」のページングトークンを生成する必要があります。 ページングトークン [に関するドキュメントは、こちら](/help/rest-api/paging-tokens.md)にあります。 **FnMktoGetPagingToken**&#x200B;という名前の新しい空のクエリを作成し、詳細エディターに次のコードを入力します。

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

関数を保存します。 次に使おうと思います。

#### 注目のアクション

次に、**FnMktoGetPagedData**&#x200B;および&#x200B;**FnMktoGetPagingToken**&#x200B;関数を呼び出すクエリ &#39;MktoInterestingMomentsActivities&#39;を記述します。

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

このクエリの結果もリストのリストであるため、分析に使用するには、さらにデータ処理が必要です。

### データの形成

リードに対して実行したのと同じシェーピングオペレーションを実行します。

* 出力グリッドを右クリックし、コンテキストメニューで「テーブルへ」を選択して、リストのテーブルに変換します。
* 作成されたリストのテーブルを展開し、
* もう1回展開し、ポップアップで保持するフィールドをすべて選択します（チェックボックスの「元の列名をプレフィックスとして使用」をオフにします）。

値を含む列を表示できますが、注目のモーメントに関連付けられた特定の属性のリストが含まれている列「属性」は表示されません。 これらの属性を拡張してみましょう。 リストがレコードに展開され、目的のフィールド（各属性の名前と値）を選択して再度展開し、チェックボックス「元の列名をプレフィックスとして使用」のチェックを外します。  その結果、属性を含むすべてのデータが表示されますが、各興味深いモーメントのアクティビティは3行にまたがっています。 これは分析に使いにくくなります。  アクティビティごとに1行だけを作成し、すべての属性を追加の列として表示することが理想です。 テーブルから3つの属性をピボットで選択することで簡単にできます。 アクティビティ属性から「名前」と「値」の2列を選択し、「変形」メニューの「ピボット列」をクリックします。 ポップアップで「詳細設定」オプションを尋ね、「値の列」=「値」および「集計しない」の値関数を選択します。  「OK」をクリックすると、アクティビティごとに1行のデータを出力する必要があります。  次の「データシェイプ」行のコードは、クエリのスクリプトに自動的に追加される必要があります。

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

REST APIを通じて利用可能な特定のMarketo データにアクセスするために必要なすべてのクエリをデザインできるようになりました。 この記事を楽しんでいただき、ExcelとMarketoの大きなメリットを組み合わせて活用していただいたことを願っています。 2つ目の記事では、すべてのクエリを含むサンプルワークブックも提供されています。

### 参照

#### Power Query

* [Power Query – 概要と学習](https://support.microsoft.com/en-us/article/Power-Query-Overview-and-Learning-ed614c81-4b00-4291-bd3a-55d80767f81d)
* [Power クエリ数式参照](http://msdn.microsoft.com/query-bi/m/power-query-m-reference)
* [Matt Masson Blog](http://www.mattmasson.com/tag/power-query/)は、Power Queryに関するいくつかの良いリソースを提供しています
* [DataChant Blog](https://datachant.com/2016/06/27/cursor-based-pagination-power-query/)は、ページネーション メカニズムの実装に非常に便利です

投稿日：_2016-10-18_ by _Philippe_

## 2016年秋アップデート

2016年秋リリースでは、メール v2変数とモジュールに対するCRUD サポートと、名前付きアカウントに対するCRUD サポートが追加されました。 これで、Marketo REST APIを使用してコンテンツをローカルに読み取り、編集したり、移動、並べ替え、削除したりできるようになります。 以下のアップデートの完全なリストを参照してください。

### リードデータベース API

* [**名前付きアカウント**](/help/rest-api/named-accounts.md)
   * 名前付きアカウントの読み取り、更新、削除のための新しいエンドポイント
   * 既知の問題：
      * 2016年秋リリースの時点では、リードはAPIを介して名前付きアカウントに関連付けることはできません

### アセットAPI

* [**メール**](https://developer.adobe.com/marketo-apis/api/asset/#operation/describeUsingGET_5)
   * メール v2変数を操作するための新しいエンドポイント
   * メール v2 モジュールを操作するための新しいエンドポイント
   * 既知の問題：
      * 予測トークンを含むセクションのクエリと更新では、エラーが返されます
      * 予測トークンを含むコンテンツセクションを含むメールは、APIを使用して承認できません

投稿日：_2016-12-07_ by _Kenny_

## Twitter Handl3@MarketoDev引退した理由

私たちはTwitter上の@MarketoDevのハンドルを廃止することを決めました。 このアカウントは2011年12月9日に無効になります。 興味を持った方は？**2014年初頭に戻ります…** Marketo Developers サイトを立ち上げたばかりで、開発者がAPIに対してビルドを行えるようにしました。 Marketoプラットフォームの認知度を高め、開発者の参入障壁を減らしたいと考えていました。 その取り組みと併せて、Marketoとの統合ソリューションの構築に関心のあるテクノロジーパートナーやお客様とエンゲージするための@MarketoDevールも作成しました。 どんな大胆な新しいプロジェクトと同じように、私たちはこれがどのように機能するのか確信していませんでした。 最初は、新しいブログ記事と新しいAPI リリースをツイートしました。 開発者向けサイトへのトラフィックが増加しました！ 私たちはまた一連の質問を受け始めました、そして私たちは忠実に答えました。**2016年後半に向けて…** [LaunchPoint Partner](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) エコシステムの成長に伴い、ツイートのアクティビティが増加しました。 膨大な量の質問に対して@MarketoDevが回答することが、私たちの小規模なチームにとって大きな課題でした。 一般商品や販売関連の質問が増え、@Marketoや@MarketoCaresにリダイレクトしました。 また、140文字だけでは開発関連の質問には不十分であることも分かりました。 これらの質問に答えるために、長い時間をかけて膨大な会話をおこなう必要があり、このアプローチは拡張性がありませんでした。 そして最後に、開発者サイトへの訪問者のトラフィックソースを分析し、大部分がオーガニック検索とブログの「今すぐ購読する」機能からのものであることがわかりました。 これらの理由から、私たちはプラグを@MarketoDevに引っ張ることにしました。**ここからは…**&#x200B;あなたがTwitterのファンなら（そうでない人なら）、恐れずに行ってください！ 当社の企業Twitterは@Marketoを扱っています。当社のカスタマーサポートも@MarketoCaresを扱っています。

投稿日：_2016-12-02_ by _David_

## Excel統合パート 2:Power ピボットとPower ビューを使用した高度なMarketo レポートとデータビジュアライゼーションの構築 – 

これは、Marketoに組み込まれたPower BI テクノロジを利用して、Microsoftで真のセルフサービス型のビジネス分析体験を構築する方法について解説した2つの記事のシリーズの2番目です。 これらの記事で取り上げた概念を使用すると、次のことが可能になります。

* MarketoからExcelへのデータのインポート
* 他のソース（SaaS アプリケーション、データベース、フラットファイルなど）からのデータをインポートして組み合わせる
* ビジネスニーズや分析目的でデータを形成する
* Excel内のオンデマンドのデータの更新
* 数式を使用した分かりやすい計算列と測定の作成
* 異種データ間の関係の構築
* ピボットテーブルとピボットチャートによるデータ分析と高度なレポートの作成
* 優れたデータビジュアライゼーションの作成

### Power ピボットとPower View for Excel

この記事では、次の構築方法の例を示します。

* Power Pivotを使用して、Marketo データの異なるコレクション間の関係を活用する高度なMarketo レポート
* Power Viewを使用した静的ビジュアライゼーションとアニメーションビジュアライゼーション

**Power ピボット**&#x200B;はExcel アドインで、既にExcel 2016に含まれています。このアドインを使用すると、強力なデータ分析を実行したり、高度なデータ モデルを作成したりできます。 Power Pivotを使用すると、様々なソースから大量のデータをマッシュアップし、情報分析を迅速に実行し、インサイトを簡単に共有できます。 Power Queryを使用して異なるデータソースから抽出されたデータは、データモデル、Excel スプレッドシート、またはその両方に送信できます。 最初の記事では、Marketoからデータを読み込んで整形し、スプレッドシートで使用できるようにする前に、より高度な分析を実行するためにデータモデルに送信しました。**Power View**&#x200B;は、Excel ビジュアライゼーションレイヤーの代わりです。 直観的かつ高度なレポート作成とダッシュボード機能を促進できる、インタラクティブなデータ探索、ビジュアライゼーション、プレゼンテーション体験を提供します。

この記事で説明するすべての手順は、Windows用Excel 2016でテストされています。 コンセプトはExcel 2013またはExcel 2010 （Power Viewなし）と同じである必要がありますが、一部の調整が必要になる場合があります。 Power PivotとPower Viewは現在、Microsoft Windows バージョンのExcel 2016でのみ利用できます。Office 365 バージョンのExcel 2016では、完全なPower PivotとPower Viewはサポートされていません。

### Marketo Power Workbook

#### ワークブックをダウンロード

最初の記事では、Power Query テクノロジーを使用したデータの読み込みと整形のプロセスについて説明しました。 Marketoからリードやアクティビティを抽出するための高度なパワークエリの実装方法を学びました。 レポートやビジュアライゼーションを作成する場所に、コーディングなしで直接移動したい人もいるからです。 このブックには、最初の記事で詳しく説明したすべてのクエリと、その他のクエリが含まれています。 エラー処理を改善し、設定ワークシートにいくつかの追加パラメーターを追加しました。 最初の記事を実行した場合でも、Marketo Power Workbookをダウンロードして、追加されたものを確認することをお勧めします。

免責事項：Marketo Power WorkbookはMarketoの公式製品ではないため、Marketoではサポートされていません。 個人的なビジネスニーズに合わせて自由に使用したり、拡張したりできますが、ご自身のリスクで使用してください。

#### ワークブックの設定

Marketoの設定ワークシートから、必要なすべての情報を入力します。

* **Marketo REST API認証：**&#x200B;が必要です
* **スコーピング：**&#x200B;は、Paging Token SinceDatetimeと、分析するすべてのリードを含むMarketo静的リストのIDを設定します
* **リード：** レポートを作成するには、少なくとも次のリードフィールドを指定する必要があります：`id`、`firstName`、`lastName`、`email`、create`edAt`、`updatedAt`、`title`、`company`、`industry`、`inferredCountry`、`inferredCity`
   * 市区町村情報がカスタムフィールドの1つでより正確な場合は、代わりに独自のフィールドを使用できます
* Marketo データベースから取得する&#x200B;**アクティビティ：**&#x200B;のアクティビティ タイプは、各アクティビティ セットに対してここで指定されます。今すぐ変更する必要はありません。
   * 後でこの情報を調整する場合は、Excel ブック内で、既存のすべてのアクティビティ タイプを一覧表示するユーティリティ クエリをブック上で提供していることに注意してください

セキュリティ関連のポップアップが表示される場合があります。 外部コネクションを信頼し、「パブリック」に設定します。 下のポップアップが表示された場合は、「匿名」のweb アクセスコンテンツを使用してください。 Marketoへの認証は、アドビのカスタムクエリで直接管理されるため、他の種類のアクセスを有効にする必要はありません。

#### Marketo Dataのダウンロード

まず、Marketo設定ワークシートのスコーピング領域で定義したパラメーターが、Marketo APIの日次リクエスト制限を超えて、ダウンロードが多すぎないようにしてください。 準備ができたら、「データ」メニューの「すべてを更新」ボタンをクリックし、すべてのデータがワークブックにダウンロードされるのを待ちます。 データのダウンロード時に「column1 not found」と同様の形式エラーメッセージが表示される場合は、1つ以上のクエリがデータの取得に失敗しているため、形式も失敗しています。 エラーが解決しない場合は、後でもう一度やり直してから、お使いのバージョンのExcelを確認してください（Office 365からExcel 2016を使用しないでください）。 Marketoの遅延を尊重することも重要です。 静的リストまたはリードデータで変更を行う場合は、Power Queriesを起動する前に待つことが望ましいです。

### Power Pivotでのデータモデリング

上部のメニューバーにあるPower Pivot メニューから「管理」ボタンをクリックしてPower Pivotを開きます（使用できない場合は、ご使用のバージョンのExcelを確認してください。Power Pivotは、一部のバージョンのExcelにアドインとしてインストールできます）。 Marketoからダウンロードしてデータモデルに送信されたすべてのデータには、Power Pivot ウィンドウの下部にある様々なタブからアクセスできます。

### データ分析式（DAX）

レポート用にデータを拡充したり、フォーマットを変更したりする必要があります。 Power Pivot Data Analysis Expressions （DAX）を使用して、一部のカスタム計算を計算列およびメジャー（計算フィールドとも呼ばれます）として定義します。 DAXについて詳しくは、「参照」セクションの「Power PivotのDAX」リンクを参照してください。 計算エリアがPower Pivot ウィンドウに表示されていることを確認します。表示されていない場合は、Power Pivot ホーム メニューから計算エリアを有効にします。  「**MktoLeads**」タブを選択し、**リード数** メジャーをリード計算エリアの任意の場所に追加します：**リード数：=****DISTINCTCOUNT**** （[id]）**。 この指標は、IDにもとづいて、リストで利用可能なリードをカウントします。 レポートのコンテキストで使用される最終的なフィルターも考慮します。 レポートはリード数を合計できるので、この測定は本当に必要ではありませんが、「MktoLeadsの合計」よりも優れた名前のリード数を持つように作成しました。 また、特定のタイプのデータ入力（スコアが50を超えるすべてのリード、平均スコアなど）に対する平均、最小、最大を実行する、より複雑な測定を簡単に想像できる簡単な例でもあります。  次に、**MktoWebActivities** タブを選択し、3つの計算列を作成します。 テーブルの右端までスクロールし、「列を追加」列をクリックして、次の計算列を挿入します。**アクティビティ：** テーブル MktoActivtyTypesのアクティビティ IDを検索して、ユーザーフレンドリーなアクティビティ ラベルを取得します。**\=****LOOKUPVALUE**** （MktoActivityTypes[name],MktoActivityTypes[id],[activityTypeId]）****年 – 月：**&#x200B;一部のレポートに適したパターン「YYYYmm」でアクティビティ日を再フォーマットします。**\=****LEFT**** （[activityDate],4）&amp;****MID**** （[activityDate],6,2）** **日付：** アクティビティ日は、元のクエリの文字列にすぎず、適切な日付に変換します。**\=****DATE**** （****LEFT**** （[activityDate],4）,****MID**** （[activityDate],6,2）,****MID**** （[activityDate],9,2）**）次に、**MktoEmailActivities** タブに対して同じ3つのメジャーを作成し、さらに2つのメジャーを作成しましょう：**Campaign:** ユーザーフレンドリーを取得MktoCampaign テーブルのCampaign IDを検索して、キャンペーン名を指定します。**\=****LOOKUPVALUE**** （MktoCampaigns[name],MktoCampaigns[id],[campaignId]）****プログラム：** テーブル MktoCampaignsでCampaign Idを検索して、ユーザーフレンドリーなプログラム名を取得します。 テーブル MktoProgramsは、プログラムの詳細（フォルダー、ワークスペースなど）を提供できます。**\=****LOOKUPVALUE**** （MktoCampaigns[programName],MktoCampaigns[id],[campaignId]）**

### Entity-Relationships

「以前は、モデル内の別のテーブルから情報を検索して、欠けている情報を補完する方法を見ていました。 Power Pivotでは、データモデルの一部のテーブル間の関係を定義する、より強力なオプションが提供され、レポートから直接それらの関係を活用できます。 レポートの主要な関係を定義します。 Power Pivot ウィンドウからダイアグラム表示を選択します。 データモデル図内で次の関係をトレースします。

* **MktoInterestingMomentActivities:leadId →** **MktoLeads:id**
* **MktoScoringActivities:leadId →** **MktoLeads:id**
* **MktoRevenueStageActivities:leadId →** **MktoLeads:id**
* **MktoWebActivities:leadId →** **MktoLeads:id**
* **MktoEmailActivities:leadId →** **MktoLeads: id**

これらの関係とオブジェクトのすべてをレポートで使用するのではなく、リード、Web アクティビティ、メールアクティビティのみを使用します。 続いて、レポートを作成します。

### 電子メールのパフォーマンスピボットチャート

最初のレポートでは、標準のExcel ピボットチャートにもとづいた電子メールパフォーマンス KPIを示しています。 業種やキャンペーン別にデータをフィルタリングすることができます。 「ピボットテーブル」セレクターから「ピボットチャート」を選択すると、Power ピボットメニューからピボットチャートを作成できます。  別の方法として、Excel スプレッドシートから直接ピボットチャートを作成し、「このワークブックのデータモデルを使用」オプションにチェックを入れます。  次の図のように、**MktoEmailActivities**&#x200B;および&#x200B;**MktoLeads** テーブルからフィールドをドラッグ&amp;ドロップします：**MktoEmailActivities.Activity →** **Legend** （これは、先の&#x200B;**MktoEmailActivities**&#x200B;に実装したDAX計算列を使用します） **MktoEmailActivities.Date →** **Axis** （これは、実装したDAX計算列をを使用します） **MktoEmailActivities**&#x200B;前） **MktoEmailActivities.Id →** **∑ Values** **MktoEmailActivities.Campaign →** **Filter** **MktoLeads.industry →** **Filter**

ドロップされた各フィールドで「値フィールド設定」を選択して、カスタム名を作成できます。 この場合、メールアクティビティ ID フィールドを「∑値」セクションにドロップし、カスタム名を「アクティビティの数」として編集しました。 次にピボットチャートを設定します。 グラフ上で直接クリックし、コンテキストメニューの「グラフタイプを変更」オプションを選択します。 このように、すべてのデータ系列に異なるチャートタイプを選択しました。

### Power Viewを使用したリードマップ

2つ目のレポートは、世界地図と業界別に、地域ごとにリードと連絡先を表示しています。 Power Viewが必要です。 Excelのメニューをオンにするには、以下のリファレンスリンクに従ってください。 または、Excel検索ボックスに「power view」と入力します。 「Power View レポートを挿入」を選択します。  空白のPower View レポートで、右側のパネルの&#x200B;**MktoLeads** テーブルを選択し、リードの場所フィールド （例：**inferredCity**）をドラッグ&amp;ドロップします。 これで、メインメニューに「デザイン」メニューが表示されます。

Power Viewの「デザイン」メニューで「マップ」を選択して、マップビジュアライゼーションに切り替えます。 次の図のように、**MktoLeads** テーブルからフィールドをドラッグ&amp;ドロップします。**MktoLeads.industry →** **Color** **MktoLeads.inferredCity →** **Locations** **MktoLeads.Leads Count →****∑ Size** （これは先ほど&#x200B;**MktoLeads**&#x200B;で実装したDAX測定を使用します）。そして、リードマップの準備ができました！ マップのサイズを調整し、タイトルと凡例をカスタマイズするだけです。 Power Viewを使用すると、単一のスプレッドシートに複数のグラフを含む高度なダッシュボードを構築できます。 「[Power View レポートを作成](https://support.microsoft.com/en-us/article/Tutorial-Create-Amazing-Power-View-Reports-Part-1-e2842c8f-585f-4a07-bcbd-5bf8ff2243a7)」の下の参照チュートリアルを参照して、Power Viewでより多くのダッシュボードコンポーネントを実行する方法を確認してください。

### 3D マップ上でアニメーション化されたWeb アクティビティ

3つ目のレポートでは、リードのweb アクティビティを業界別に3D世界地図で表示しています。 このレポートには3D マップが必要です。 Excelの検索ボックスに「3D」と入力し、「3D マップ」を選択するだけです。 ポップアップウィンドウから新しいツアーを作成します。  右側のパネルでバブル チャートを選択します。 以下の図のように、**MktoLeads**&#x200B;および&#x200B;**MktoWebActivities** テーブルからフィールドをドラッグ&amp;ドロップします。**MktoLeads.industry →** **Category** **MktoLeads.inferredCity →** **Location** **MktoWebActivities.Activity →** **Time** （この使用は、DAX計算列を実装しました&#x200B;**MktoWebActivities**&#x200B;以前。 ID フィールドは、アクティビティのカウントにも使用できます。） **MktoWebActivities.Date →** **時間** （これは&#x200B;**MktoWebActivities**&#x200B;に実装したDAX計算列を使用します） **MktoWebActivities.Activity**&#x200B;をフィルターとして使用して、さまざまな種類のweb アクティビティを除外することもできます。

「テーマ」ボタンを使用して、3D マップの配色を変更します。 「シーンオプション」を開いて、アニメーションをカスタマイズします。
これで3D世界地図が完成しました。これで、地球をアニメーション化し、そこからビデオを作成する楽しい時間を過ごすことができます。

### 次の手順

Excel Power BIツールで可能なことの表面を傷つけただけです。 Excelのスキルを拡張し、ビジネス目標を達成するために必要なレポートを設計するための他の素晴らしい記事やチュートリアルをWebで検索することをお勧めします。 これらの記事を楽しんでいただき、ExcelとMarketoの大きなメリットを組み合わせて活用していただければ幸いです。

### 参照

#### Power ピボット

* [Power Pivot：強力なデータ分析とExcelでのデータモデリング](https://support.microsoft.com/en-us/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)
* [Power Pivotのデータ分析式（DAX）](https://support.microsoft.com/en-us/article/Data-Analysis-Expressions-DAX-in-Power-Pivot-bab3fbe3-2385-485a-980b-5f64d3b0f730)

#### Power View

* [Excel 2016でPower Viewを有効にする](https://support.microsoft.com/en-us/article/Turn-on-Power-View-in-Excel-2016-for-Windows-f8fc21a6-08fc-407a-8a91-643fa848729a)
* [チュートリアル：素晴らしいPower View レポートの作成](https://support.microsoft.com/en-us/article/Tutorial-Create-Amazing-Power-View-Reports-Part-1-e2842c8f-585f-4a07-bcbd-5bf8ff2243a7)

投稿日：_2017-02-02_ by _Philippe_

## Marketo APIでのアクティビティレコードの重要な変更

**注意：この投稿は、新しいインフラストラクチャへの移行によりAPIから返されたアクティビティレコードに加えられた変更を反映するように更新されます。** **最終更新日：2018年9月13日** 2017年9月からMarketoの次世代Activity Serviceのロールアウトが開始されるため、Marketo APIから返されるアクティビティ、データ値の変更、またはリード削除レコードに整数の「id」フィールドの一意性や有無を適用できなくなります。 アクティビティレコードを取得する統合のサービスの中断を回避するには、ID フィールドをオプションとして扱う必要があります。 この変更のカットオーバーは、サブスクリプションと今後のリリースに影響を与え始めます。 この変更は、次のエンドポイントに影響します。REST API

影響を受けるSOAPの種類は`ActivityRecord`と`LeadChangeRecord`です。

### 例

次の例は、影響を受けるレコードタイプを示しています。 どちらの例でも、エフェクトフィールドは「id」と呼ばれます。

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

**SOAP フィールドの例：id**

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

投稿日：_2017-03-01_ by _Kenny_

## 2017年冬アップデート

2017年冬リリースでは、カスタムオブジェクトデータを非同期で一括インポートする機能と、ガイド付きランディングページで変数を操作する機能が追加されました。 以下のアップデートの完全なリストを参照してください。

### リードデータベース API

#### カスタムオブジェクトの一括読み込み

カスタムオブジェクトの一括読み込みをサポートする新しいエンドポイント 詳細については、[こちら](/help/rest-api/custom-objects.md)を参照してください。

#### 今後のアクティビティの変更のお知らせ

Marketoが次世代のActivity Serviceをリリースする際に発生する大きな変化に注意してください。 この変更は、次のエンドポイントに影響します。

SOAP

[getLeadActivity](/help/soap-api/getleadactivity.md)、[getLeadChanges](/help/soap-api/getleadchanges.md)

これらのエンドポイントによって返されるレコードに含まれる整数「id」フィールドは、一意であることが保証されなくなります。 これは、アクティビティ、データ値の変更、リード削除のレコードタイプに影響を与えます。 これらのレコードタイプを取得する統合のサービスの中断を避けるために、id フィールドはオプションとして扱う必要があります。

#### プッシュトークンの削除

SDK APIを介してプッシュトークンを削除する機能を追加しました。 詳細については、[iOS](/help/mobile/push-notifications.md)、[Android](/help/mobile/push-notifications.md)を参照してください。

投稿日：_2017-03-01_ by _David_

## 2017年春アップデート

2017年春のリリースでは、リードとアクティビティオブジェクトデータを非同期で一括抽出し、名前付きアカウントリストを操作する機能が追加されました。 以下のアップデートの完全なリストを参照してください。

### リードの一括抽出

リードの一括抽出をサポートする新しいエンドポイント。 様々なオプションを使用して、レコードの選択基準を指定します。 詳細については、[こちら](/help/rest-api/bulk-lead-extract.md)を参照してください。

### アクティビティの一括抽出

アクティビティの一括抽出をサポートする新しいエンドポイント。 日付範囲とアクティビティリストを使用して、レコードの選択基準を指定します。 詳細については、[こちら](/help/rest-api/bulk-extract.md)を参照してください。

### 重点顧客リスト

名前付きアカウントリストでのCRUD操作をサポートする新しいエンドポイント。 詳細については、[こちら](/help/rest-api/named-account-lists.md)を参照してください。

### その他の機能強化

* [Get キャンペーン ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCampaignByIdUsingGET) エンドポイントで、「トリガー可能」なキャンペーンをフィルタリングできるようになりました。 これは、「isTriggerable=true」をクエリパラメーターとして渡すことによって実現されます。
* [ コピープログラム ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) エンドポイントは、SMS メッセージを除くすべてのアセットタイプを含むプログラムをサポートするようになりました。

### Ionic

Marketo Mobile MMEと[Ionic](https://ionicframework.com/) アプリケーションフレームワークを使用できるようになりました。 詳細については、[こちら](/help/mobile/ionic.md)を参照してください。

### プッシュ通知トークンの登録解除

プッシュ通知トークンをMarketoに登録解除できる新しいメソッドがSDKに追加されました。 これは、ユーザーがアプリからログアウトする場合などに便利です。 使用方法については、`unregisterPushDeviceToken` （iOS）または`uninitializeMarketoPush` （Android）メソッド [ここ](/help/mobile/push-notifications.md)を参照してください。

投稿日：_2017-06-16_ by _David_

## IFTTTとZapierを使用したマーケター向けのモノのインターネット

モノのインターネット（IoT）とは、デバイス、アプライアンス、ウェアラブル、車両などの接続機器と、組み込み電子機器、ソフトウェア、センサー、ネットワーク接続を介してネットワークを構築することで、これらのオブジェクトがクラウド情報システムとデータを収集して交換できるようにすることです。 これらのテクノロジーは急速に成長し、トレンドを促進しているため、私たちの生活や働き方、ビジネス方法に大きな影響を与えます。 業界をリードするマーケティングエンゲージメントプラットフォームであるMarketoは、あらゆる形式のコミュニケーションチャネルと連携できる拡張性を備え、IoTに対応できます。 Marketoでは、電子メール、web、モバイル、CRMなどに関連する70種類以上のアクティビティを既に追跡できます。また、任意のサードパーティシステムでフィードできる[ カスタムアクティビティ ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/administration/marketo-custom-activities/create-a-custom-activity.html)もサポートしています。 Marketo [ カスタムオブジェクト ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/administration/marketo-custom-objects/understanding-marketo-custom-objects.html?lang=ja)を使用すると、ビジネスに関連するあらゆる種類のサードパーティ指標を追跡でき、マーケターはMarketo スマートキャンペーンのフィルターとトリガーから直接、これらの指標を活用できます。 IoTを実装するには、コンシューマーデバイスと対話するための一元化されたサーバーが必要です。このサーバーは、REST API、カスタムオブジェクト、カスタムアクティビティなどの機能を備えたMarketo オープンプラットフォームとデータを交換します。[こちら](http://eto.com/)を参照してください。 ブログ記事で紹介するのは簡単ではありません。 代わりに、IFTTT サービスとMarketoを統合して、マーケター向けのクールなIoT ユースケースを実装します。

* リードがロードショーに登録されるたびに、オフィスで色付きのライトを点滅させることで、マーケティングチームをサポートします
* 取引が成立するたびに、接続された電源プラグに接続されたベルを自動的に起動することで、営業部門を支援します
* LinkedIn、Facebook、Slackなどのソーシャルネットワークに、マーケティングの成功のマイルストーンを自動投稿する…
* 次の要素にもとづいてマーケティングキャンペーンを自動的に開始します。
   * 気象警報が発生した場合（風、気温、雨など）
   * ニューヨークタイムズなどの新聞によって、特定の基準に一致する新しい記事が公開されたとき
   * 米国上院または下院が投票する場合
   * 国際宇宙ステーションが特定の場所を通過するとき
   * など…

これらのシナリオは楽しいものの役に立たないものと感じるかもしれませんが、ここでは、人とのマーケティングだけでなく、人とつながる世界のものとのマーケティングを行うための新しい概念的な方法を示しています。 この記事で取り上げたもう1つの興味深いポイントは、例えば、サードパーティシステムとMarketoの間の「サービングハッチ」としてZapierなどのオープンなweb統合プラットフォームを活用して、認証を管理する方法です。

### IFTTT サービス

IFTTTとは&quot;IF This Then That&quot;の頭字語です。 これは、人々がアプレットと呼ばれる単純な条件文のチェーンを作成するために使用する無料のweb ベースのサービスです。 アプレットは、一部のパートナーweb サービス内で発生した変更によってトリガーされ、その結果、アクションが他のパートナーweb サービスに送信されます。 IFTTTは2011年にサンフランシスコのLinden Tibbets、Jesse Tane、Scott Tong、Alexander Tibbetsによって立ち上げられた。 一見すると、IFTTTは[Zapier](https://zapier.com/)のようなサービスに似ています。例えば、消費者やIoT デバイス（リモート、アラーム、ライト、サーモスタット、車、プリンター、携帯電話など）に重点を置いています。  まず、[IFTTT web サイト ](https://ifttt.com/explore)からIFTTT アカウントを作成する必要があります。 既に利用可能なすべてのクールなアプレットを自由に発見してください。それはあなたにいくつかの他のシナリオのアイデアを確実に提供します！

### The Maker Channel

チャネルを持たないWeb アプリケーション（IFTTTとのパートナーシップ）は、Maker Channelを使用する必要があります。 Maker Channelを使用すると、web リクエストを作成または受信できる任意のデバイスまたはアプリで動作するアプレットを作成できます。 次のような統合機能があります。

* アクションをトリガーするために、サードパーティシステムからweb リクエストを受け取るインバウンドトリガー
* インターネット上で一般にアクセス可能なサードパーティシステムへのweb リクエストを行うためのアウトバウンドアクション

IFTTTから、「Maker」サービスを検索してクリックします。  初めて、「接続」ボタンをクリックしてアクティブにする必要があります。  Maker Channelがアクティブになりました。 Maker設定ボタンをクリックすると、秘密鍵を取得できます。詳細については、提供されたURLをコピーしてブラウザーに貼り付けます。

### 市場から直接IFTTT アクションをトリガー

まず、Marketoから、あらゆる種類の3rd パーティ web サービスのアクションをトリガーすることに重点を置きます。 そのために、[Marketo Webhook](https://experienceleague.adobe.com/docs/marketo/using/product-docs/administration/additional-integrations/create-a-webhook.html?lang=ja)を使用します。 まずIFTTT モバイルアプリを介して携帯電話またはタブレットにプッシュメッセージを送信し、次にPhilips Hue ライトを点滅させるIoT シナリオを実装します。

### Marketo Webhook

Marketoからイベントをトリガーするには、IFTTTの「if」として機能するのは簡単です。 必要な操作は、次のパターン URLに従って、イベント名と秘密鍵を使用してPOST web リクエストをIFTTTに送信するだけです。

`<https://maker.ifttt.com/trigger/{event_name}/with/key/{secret_key}>`

Makerは、web リクエストを介して最大3つのパラメーターを通信することも可能にします。 これは、クエリパラメーター，

`<https://maker.ifttt.com/trigger/{event_name}/with/key/{secret_key}?value1={value1}&value2={value2}&value3={value3}>`

また、最大3つの値で構成されるJSON本文を使用することもできます。

`{ "value1" : "{value1}", "value2" : "{value2}", "value3" : "{value3}" }`

Marketoで、管理者インターフェイスから新しいWebhookを作成します。  新しいWebhookに次の情報を提供します。

**Webhook名：** IFTTT プログラムの成功

**説明：** プログラムを成功させるためにスマートキャンペーンからIFTTTでイベントをトリガーする

**URL:** `<https://maker.ifttt.com/trigger/{event_name}/with/key/{secret_key}?value1={{program.name}}&value2={{lead.Email> Address}}&value3={{lead.Full Name}}`

event_nameの場合は、MarketoProgramSuccessを使用します

secret_keyの場合は、IFTTT Maker サービスの秘密鍵を使用します

使用可能な3つの値には、静的テキストまたはMarketo トークンを使用します。 プログラムレベルで独自のトークンを定義し、これらの値を通じて渡すことで、よりインタラクティブなメッセージをプッシュできます。

**要求タイプ：**&#x200B;投稿

**テンプレート：**&#x200B;空白のままにする

**トークン エンコーディングの要求：** フォーム/Url

**応答の種類：**&#x200B;なし

応答マッピングを定義する必要はありません。

### IFTTT アプレット

IFTTT web ポータルで、メインメニューの「マイアプレット」を選択します。  「新規アプレット」ボタンをクリックし、「**+this**」セクションをクリックします。  Maker サービスを検索します。  Maker サービスがweb リクエストを受信するたびに起動するトリガーを作成して、イベントを通知します。 Marketo WebhookのURLで指定したイベント名と同じイベント名（「MarketoProgramSuccess」など）を使用し、「トリガーを作成」ボタンをクリックします。  次に、セクション **+その**をクリックして、アクションサービスを指定します。  まず、誰でもIoT機器に投資しなくてもテストできる簡単なアクションサービス、Notifications Serviceから始めます。 「通知サービス」を検索して選択します。
デバイスに通知を送信するアクション「通知を送信」を選択します。  Marketoから送信した3つの値をIngredientsとして追加して、次の例のようにユーザーに意味のある通知を配信することで、活用できます。次に、「アクションを作成」ボタンをクリックします。 IFTTT アプレットを確認して終了します。 有効になっていることを確認します。

### IFTTT アプレットのテスト

モバイルで通知を受け取りたい場合は、まずデバイス用のIFTTT アプリをダウンロードする必要があります。  Marketo Smart Campaign フローでWebhookを使用すると、Marketo Program Success イベントをトリガーできます。 Marketo Webhookは、トリガーされたスマートキャンペーンでのみ機能します（連絡先の入力フォームがリストに追加された後のトリガーなど）。  次に、携帯電話でのIFTTT通知の例を示します。

### CreativeとIFTTTの連携

IFTTTは300社以上のパートナーとのアプレットアクションを提供しているため、アプリとアプライアンスのポートフォリオと想像力が限界です…電子機器ショップやオンラインでどこでも購入できるPhilips](https://www.philips-hue.com/en-us)の[Hue ライトの例を見てみましょう。 次のアプレットを使用すると、Marketoがプログラムの成果をトリガーすると、現在の割り当てられた色でライトの1つを点滅させ、マーケティング部門をオフィスで強化することができます。 MarketoがWebhookでトリガーされる以前と同じ手順に従って、新しいAppletを作成しますが、今回はPhilips Hue サービスからアクションを選択します。

「点滅」アクションを選択しましょう。 アプリはPhilips Hueに利用可能なすべてのライトをリクエストするので、点滅するライトを選択できます。 Philips Hueでアカウントを設定する必要があります最初に、Hue ブリッジ、そしてもちろん少なくとも1つのHue電球、ライトストリップ、プロジェクターまたはランプ。  リードがロードショーやウェビナーに登録されるたびに、色付きの光を点滅させる新しいアプレットを追加したばかりです。 マーケティング部門は、オフィス環境を整え、日々の業務をサポートできます。

### Zapieを介したIFTTTからのMarketo アクションの実行

次に、IFTTT プラットフォームからMarketo Smart Campaignをトリガーします。 そのために、[Marketo REST API](/help/rest-api/rest-api.md)を使用します。 このAPIは保護されており、何かを呼び出す前にOAuth2認証が必要なので、Zapierなどの別のプラットフォームを介してその認証を処理する必要があります。なぜなら、IFTTTではAPI上の2つの連続した呼び出しをMaker Channelと連鎖させることができないからです。 既にZapierを導入し、Zapier用のカスタム Marketo コネクタを実装する方法をステップバイステップで説明しているので、[Zapier](https://zapier.com/)のWeb アプリ自動化サービスを選択しました。 [Workato](https://www.workato.com/integrations/marketo)などの他のプラットフォームも解決策になる可能性があります。

### Marketo Campaign

スケジュール済みのスマートキャンペーンでMarketo プログラムを作成します。 テスト目的では、次のスマートキャンペーンを例として作成できます。**スマートリスト** フィルターのみを使用し、トリガーは使用しません。 少なくとも資格を得られることを確認してください。**フロー** メールまたは他の種類の通知を送信します。**スケジュール**&#x200B;複数のテストを処理するために、毎回フローを実行できるようにしてください。 URLからスマートキャンペーン IDを取得できます。 例：_https://{{marketo_url}}/#SC4289A1_ - スマートキャンペーン IDは4289です。 このキャンペーンは、Marketo REST APIを介してトリガーできます。 例えば、[Postman](https://www.postman.com/) プラグインをChromeに使用して、次の2つの連続したHTTPS呼び出しを送信できます。**認証手順：**

`https://{{Your Munchkin_Account_id}}.mktorest.com/identity/oauth/token?grant_type=client_credentials&client_id={{Your_Client_Id}}&client_secret={{Your_Client_Secret}}`

JSON応答からアクセストークンを回復します。**キャンペーン キックオフ ステップ：**

`https://{{Your_Munchkin_Account_id}}.mktorest.com/rest/v1/campaigns/{{Campaign_Id}}/schedule.json?access_token={{access_token}}`

### Marketo Campaignを起動するための中級Zapier カスタムコネクタ

Marketo REST APIで認証し、スマートキャンペーンを開始するカスタムのZapier コネクタを構築する必要があります。

* 前提条件
* Zapier用Marketo コネクタの実装
* 「Marketo Campaign」などの別のタイトルを使用
   * 「認証」手順を実行します
   * 「トリガー」ステップを実行します（Zapier テストの目的で必要）
   * Marketo キャンペーンを起動する責任を負う次の「アクション」手順を実行します。手順は次のとおりです。

データアクションエンドポイント URLの送信先：

`https://{{munchkin_account_id}}.mktorest.com/rest/v1/campaigns/{{CampaignId}}/schedule.json`

その他のオプションフィールドは空白のままにします。

#### スクリプト API

Zapierのスクリプト機能を使用すると、アプリのAPIとZapier間で交換されるリクエストと応答を操作できます。 HTTP リクエストを送信する直前に変更し、Zapierがリクエストを処理する前にレスポンスを解析できます。 カスタムの「セッション認証」認証を完了する必要があります。 詳しい情報は元の記事に記載されています。 次のコードを元のコードと非常によく似てコピーします。アクション方法を変更しただけです。

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

##### 新規Zap

Zapier ダッシュボードから、「新しいZapを作成」ボタンをクリックします。**トリガー**

* 「Webhook by Zapier」トリガーアプリを選択
* 「フックをキャッチ」をチェック
* 子キーをオフにする必要はありません
* Zapierがカスタム Webhook URLを生成し、リクエストを送信して、どこかに安全に保つことができます
* 以下の「Zapier Webhookを呼び出すIFTTT アプレット」シナリオを開始して、Webhook URLをテストします。 これにより、ZapierはWebhook ペイロードについて学習し、キャンペーン IDをアクションに割り当てることができます

**アクション**

* 以前に作成したMarketo Campaign コネクタを選択
* 使用可能なアクションのみを選択：**キャンペーンを起動**
* Marketo アカウントに接続し、認証パラメーター（Munchkin アカウント ID、クライアント ID、クライアントシークレット）を入力します
* テンプレートを編集し、トリガーのCampaign IDを「Launch Campaign」 Campaign ID パラメーターに関連付けます
* ステップをテストし、Marketo Campaignが起動されることを確認します

### Zapier Webhookを呼び出すIFTTT アプレット

テストしやすいシンプルなシナリオから始めます。 私たちは、毎時間Marketo キャンペーンを開始する日時トリガーをIFTTTで選択します。 アクションは、Zapier Webhook URLに投稿し、スマートキャンペーン IDを渡すweb リクエストです。 Zapier ZapとIFTTT アプレットの両方がアクティブであることを確認し、すべてが期待どおりに動作していることをテストします。

### CreativeとIFTTTの連携

IFTTTは300社以上のパートナーとアプレットトリガーを提供しているため、アプリとアプライアンスのポートフォリオと想像力が限界です…気象警報でMarketo キャンペーンを開始するために使用する[Weather Underground](https://www.wunderground.com/) サービスの例を見てみましょう。 次のトリガーは、雨の条件が発表されたときに開始されます。 その後、トリガーをMaker Webhook Actionに関連付け、以前と同様にZapier Webhook パラメーターを入力します。  ほら、この結果が実際に機能しているか確認するために、今は良い雨が降る必要があります。

この記事で提供されている概念を適用して多くの楽しみを持っていることを願っています。 しかし、最も重要なことは、この記事の重要な概念のおかげで、Marketoを他の3rd パーティシステムと統合したい人に役立つと思います。

* MARKETO REST API
* Marketo Webhook
* 例えば、ZapierなどのオープンなWeb統合プラットフォームを、サードパーティシステムとMarketoの間の「サービングハッチ」として活用して、認証を管理する方法

投稿日：_2017-06-20_ by _Philippe_

## 2017年夏アップデート

2017年夏リリースでは、プログラム APIに対するいくつかのマイナーな機能強化をリリースしています。

### プログラムを参照

オプションのearliestUpdatedAt パラメーターとlatestUpdatedAt パラメーターの追加により、日付範囲でプログラムを取得する機能を[ プログラムを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/browseProgramsUsingGET) エンドポイントに追加します。 選択した日時で両方または一方のパラメーターを設定して、2つの日時の間に作成または更新されたプログラムのみを返すことができます。 これは、新しいマーケティング資料や更新されたマーケティング資料のセットを取得するのに役立ち、最も重要なのは翻訳とビジネスインテリジェンスのユースケースです。

投稿日：_1970-01-01_ by _Kenny_

## GoogleでMarketoのビジネスロジックを拡張 – 

この記事では、次の簡単な例に基づいて、Google Cloud Platform （GCP）でビジネスロジック機能を使用してMarketoを拡張するソリューションを提案します。Marketo リードレコードの3つのカスタムフィールド：

* **OnLinePreference**: オンラインコミュニケーションの見込み顧客/顧客の興味を示す増分スコア。
* **OfflinePreference**: オフラインコミュニケーションに対する見込み顧客/顧客の興味を示す増分スコア。
* **Preference**: オフライン スコアがオンライン スコアよりも高い場合は「オフライン」を表示し、その逆の場合は「オンライン」を表示するGCPによって計算されたフィールド

このテクノロジーは、より高度なビジネスロジック、そして最終的には外部web サービスの呼び出し、Marketoでの結果の変換と統合への道を開きます。  

### Google Cloud PlatformとFunctionsについて

[Google Cloud Platform](https://cloud.google.com/) （GCP）は、Googleが社内でGoogle検索やYouTubeなどのエンドユーザー製品に使用するのと同じインフラストラクチャ上で動作するクラウドコンピューティングサービスのスイートです。 一連の管理ツールに加えて、コンピューティング、データストレージ、データ分析、マシンラーニング、ビッグデータなどを含む一連のモジュラー型クラウドサービスを提供します。 Compute Engine、App Engine、Kubernetes Engineなど、様々なGCP サービスを必要に応じて使用できましたが、次の主な利点を考慮して、[Cloud Functions](https://cloud.google.com/functions) （Beta内）を選択しました。

* サーバーレスクラウドコンピューティングでは、HTTP呼び出しなどのイベントに応じてロジックをオンデマンドで作成できます。
* サーバーのメンテナンスとデプロイメントによって発生する問題のほとんどを軽減します。
* GCPは関数呼び出しごとに支払われるので、サーバーを稼働させておくためではなく、コスト効率が高くなります。
* アプリケーションロジックのみに専念するため、シンプルで迅速に実装できます。
* 自動スケーリングで高負荷にも対応。

このテクノロジーとその価格について詳しくは、[GCP web サイト ](https://cloud.google.com/)を確認してください。 通常、このチュートリアルは重要なコストを引き起こしてはならず、GCP体験版の無料クレジット内に完全に収まります。  

### Google Cloud環境の準備

Google Cloud アカウントが必要です。 このチュートリアルを実行するのに十分すぎるほどのクレジットでGCPを無料で試すことができます。[GCP web サイト ](https://cloud.google.com/)の「無料で試す」ボタンをクリックするだけです。 Googleの[HTTP チュートリアル ](https://cloud.google.com/functions/docs/calling)の「開始する前に」セクションのすべての手順に従います。

1. Cloud Platform プロジェクトを作成する：リソースの管理ページに移動します
1. プロジェクトの請求を有効にする：[請求を有効にする](https://cloud.google.com/billing/docs/how-to/modify-project?visit_id=638816637273392093-1926929734&rd=1)
1. Cloud Functions APIを有効にする：[APIを有効にする](https://accounts.google.com/InteractiveLogin?continue=https://console.cloud.google.com/flows/enableapi?apiid%3Dcloudfunctions%26redirect%3Dhttps://cloud.google.com/functions/docs/tutorials/http&followup=https://console.cloud.google.com/flows/enableapi?apiid%3Dcloudfunctions%26redirect%3Dhttps://cloud.google.com/functions/docs/tutorials/http&osid=1&passive=1209600&service=cloudconsole&ifkv=ASKV5Mh81NGNsqcJqhx7hst0KFnyA0MJ-2zay8ovyluBfpvDoM820nF9Wq_SKbC1m_sjQvvRNoKSuA)
1. [Cloud SDKのインストールと初期化](https://cloud.google.com/sdk/docs/)
1. Gcloud コンポーネントの更新とインストール

   **gcloud コンポーネントの更新と更新** **Gcloud コンポーネントのインストール ベータ**

1. Node.js開発用に環境を準備します。[設定ガイドに移動](https://cloud.google.com/nodejs/docs/setup)

### scoreCompare Cloud Functionの実装

1. Cloud Storage バケットを作成して、Cloud Functions ファイルをステージングします。 コマンドラインで実行できます。

   `gsutil mb gs://[YOUR_STAGING_BUCKET_NAME]`

   または、Google Cloud web インターフェイスから、プロジェクトを選択し、ストレージメニューをクリックします。
   * ストレージバケットに一意の名前を付けます
   * デフォルトのストレージクラスを選択
   * 最適な地域を選択する

1. アプリケーションコードのローカルシステム上にディレクトリを作成します。
1. 次のJavaScript コードを使用して、このディレクトリに「index.js」ファイルを作成します。コードは非常に簡単に理解できます。 これは、HTTP リクエスト本文の2つの入力パラメーターをJSONで解析し、処理を行い、HTTP応答をJSONでエンコードします。

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

関数scoreCompareをHTTP トリガーでデプロイします。 ディレクトリから次のコマンドを実行します。

**gcloud ベータ関数のデプロイ [FUNCTION] —stage-bucket [YOUR_STAGING_BUCKET_NAME] —トリガー-http**

ここで、[YOUR_STAGING_BUCKET_NAME]は、ステージング用クラウドストレージバケットの名前です。 この例では：

**gcloud ベータ版の関数deploy scoreCompare —stage-bucket mktostorage —トリガー-http**

1. コンソール出力のCloud Function URL （httpsTrigger URL）に注意してください。次のようになります。`https://[YOUR_REGION]-[YOUR_PROJECT_ID].cloudfunctions.net/[FUNCTION]`

   * [YOUR_REGION]は、関数がデプロイされるリージョンです。 これは、関数のデプロイが完了すると、ターミナルに表示されます。
   * [YOUR_PROJECT_ID]はCloud プロジェクト IDです。 これは、関数のデプロイが完了すると、ターミナルに表示されます。
   * [FUNCTION]は関数名です。

   この例では、[**https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare**](https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare)
1. [Postman](https://www.postman.com/)のようなツールで関数をテストします。
   * HTTP Verb: POST
   * URL: [https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare](https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare)
   * ヘッダー：content-type = application/json
   * 本文：{&quot;onlineScore&quot;:110, &quot;offlineScore&quot;:200}出力には、{&quot;output&quot;: &quot;offline&quot;}が与えられます。

### MarketoのWebhookからのCloud Functionの呼び出し

Marketoのリードレコードには、次の3つのカスタムフィールドを作成する必要があります。

* **OnlinePreference**：整数
* **OfflinePreference**：整数
* **Preference**：文字列

「scoreCompare」クラウド関数URLとカスタムフィールドのトークンを使用して、Marketoの管理インターフェイスから次のWebhookを作成します。 MarketoをトリガーとしたスマートキャンペーンでWebhookをテストします。

* **Marketo webhookは、トリガーされたスマートキャンペーンからのみ呼び出すことができ、バッチスマートキャンペーンからは呼び出せません。**
* **クラウド機能を使用しない場合は、Google Cloud Platform アカウントに課金が発生しないように、クラウド機能を削除するか、プロジェクト全体を削除します。**

このチュートリアルが時間を費やす価値があり、複雑な処理やサードパーティのサービスを含むより高度なシナリオについて考えられることを願っています。 たとえば、Googleのマシンラーニング（機械学習）サービスであるGoogle Cloud AIを活用することです。 例えば、Marketo フォームから一部のフリーテキストを解析し、Google自然言語APIに対してテキストの構造と意味を明らかにするよう求め、その後、Marketoでこの解析を保存できます。アイデアのフラッジゲートを開くだけです。

投稿日：_2017-11-21_ by _Philippe_

## 2017年秋アップデート

2017年秋リリースでは、Asset APIに対するいくつかの機能強化をリリースしています。 以下のアップデートの完全なリストを参照してください。

### 日付範囲別のプログラムの参照

日付範囲でプログラムを取得する機能を[ プログラムを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneEmailUsingPOST) エンドポイントに追加しました。 これは、`earliestUpdatedAt`および`latestUpdatedAt` パラメーターを使用して行われます。 選択した日時で両方または一方のパラメーターを設定して、2つの日時の間に作成または更新されたプログラムのみを返すことができます。

### メールのプレビュー

多くのユーザーは、[ メールの完全なコンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailFullContentUsingGET) エンドポイントを使用してメールをプレビューし、シリアル化されたHTML バージョンのメールを返すようになりました。 すべてのトークン、スニペット、動的コンテンツ、埋め込みコンポーネントが完全にレンダリングされます。 オプションの&#x200B;**leadId** パラメーターを渡して、特定のリードを偽装できます。

### メール 2.0のHTMLを置き換える

HTMLのメールコンテンツのブロックを置き換えることができるように、[ メール完全コンテンツの更新](https://developer.adobe.com/marketo-apis/api/asset/#operation/createEmailFullContentUsingPOST) エンドポイントが追加されました。 Marketo Email 2.0 Editorを使用してMarketo電子メールのHTML コードを編集すると、電子メールとそのテンプレートの関係が壊れます。詳しくは、[こちら](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/edit-an-emails-html)を参照してください。 このエンドポイントを使用すると、関係が壊れたメールのHTML コンテンツをプログラムで更新できます。 さらに、関係が壊れたメールと互換性があるように、他のすべてのメールライフサイクル関連エンドポイントを変更しました。

* メールのドラフトを承認
* メールを未承認
* メールの削除
* メールのドラフトを破棄
* メールの複製
* メールメタデータを更新

### その他の機能強化

* 日付範囲フィルターの最大期間が31日に増加しました。 これは、[ リードの一括抽出フィルター](/help/rest-api/bulk-lead-extract.md) （createdAdまたはupdatedAt）および[ アクティビティの一括抽出フィルター](/help/rest-api/bulk-activity-extract.md) （createdAt）に関連します。

投稿日：_2017-12-15_ by _David_

## テスト – コミュニティの外部ビデオリンク

[ メール配信品質のPower Pack チュートリアルビデオ ](https://nation.marketo.com:443/t5/product-space-archive-videos/email-deliverability-power-pack-tutorial-video/m-p/283550)  

投稿日：_1970-01-01_ by _David_

## 2018年冬アップデート

2018年冬リリースでは、APIに対するいくつかの機能強化をリリースしています。 以下のアップデートの完全なリストを参照してください。

### トリガーキャンペーンのアクティベート/ディアクティベート

トリガーキャンペーンをアクティブ化および非アクティブ化する機能が追加され、プログラムテンプレートを自動化するプロセスを簡素化できます。 これは、新しく追加された2つのエンドポイントを呼び出すことによって達成されます。[ スマートキャンペーンをアクティブ化](https://developer.adobe.com/marketo-apis/api/asset/#operation/activateSmartCampaignUsingPOST)、[ スマートキャンペーンを非アクティブ化](https://developer.adobe.com/marketo-apis/api/asset/#operation/deactivateSmartCampaignUsingPOST)。 詳しくは、[ キャンペーン ](/help/rest-api/assets.md) ドキュメントのトリガーの節を参照してください。

### 名前によるプログラムを取得

プログラム コストとプログラム タグの検索を容易にするために、[ プログラムの名前を取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getProgramByNameUsingGET) エンドポイントに2つのパラメーターを追加しました。 詳しくは、[ プログラム ](/help/rest-api/assets.md) ドキュメントの&#x200B;**includeCosts**&#x200B;および&#x200B;**includeTags** パラメーターを参照してください。

### その他の機能強化

Bulk Extract APIが「ワークスペース対応」になりました。 [ カスタムサービス ](/help/rest-api/custom-services.md)に対してAPI専用ユーザーを作成する場合は、1つ以上のワークスペースに対してAPI アクセスを持つユーザーロールを選択する必要があります。 以前は、カスタムサービスにはすべてのワークスペースへのアクセス権が付与されていました。 これで、カスタムサービスには、APIのみのユーザー作成時に選択したワークスペースのみにアクセス権が付与されます。

投稿日：_2018-03-02_ by _David_

## 2018年春アップデート

2018年春リリースでは、新しいREST APIとweb トラッキングプライバシーの機能強化がリリースされます。 以下のアップデートの完全なリストを参照してください。

REST API

### 静的リスト CRUD

ユーザーが静的リストレコードをリモートで作成、読み取り、更新および削除できるようにします。 メンバーシップの入力と維持を含む、REST APIを介した静的リストのライフサイクル全体の管理を有効にします。 詳細については、[こちら](/help/rest-api/static-lists.md)を参照してください。

### カスタムアクティビティメタデータ

ユーザーがカスタムアクティビティレコードをリモートで作成できるようにします。 タイプとタイプ属性の操作を含む、REST APIを介したカスタムアクティビティのライフサイクル全体の管理を有効にします。 詳細については、[こちら](/help/rest-api/activities.md)を参照してください。

### スマートリストメタデータ

ユーザーがスマートリストレコードをリモートで読み取り、複製、削除できるようにします。 REST APIによるスマートリストの管理を有効にします。 詳細については、[こちら](/help/rest-api/smart-lists.md)を参照してください。

### Web トラッキングプライバシー

Munchkin JavaScriptのweb トラッキングコードが強化され、プライバシーに関連する次の機能強化が含まれるようになりました。

* オプトアウト – 訪問者がweb トラッキングを完全にオプトアウトできるようにします。 詳細については、[こちら](/help/javascript-api/lead-tracking.md)を参照してください。
* IP アドレスの匿名化 – Web訪問者のIP アドレスを匿名化する機能を提供することで、地域および国際的なプライバシー規制に準拠します。 **anonymizeIP**&#x200B;設定パラメーター[ここ](/help/javascript-api/configuration.md)を参照してください。

### その他の機能強化

* ルート以外の親とmaxDepth=1が指定されている場合、[Get Folders](https://developer.adobe.com/marketo-apis/api/asset/#operation/getFolderUsingGET) エンドポイントはすべてのフォルダーを返すようになりました。
* [Get Landing Page by Id](https://developer.adobe.com/marketo-apis/api/asset/#operation/getLandingPageByIdUsingGET) エンドポイントは、すべての場合（http://またはhttps://）にプロトコルを含むURL属性を返すようになりました。

投稿日：_2018-06-29_ by _David_

## 2018年夏のアップデート

2018年夏リリースは、主にマイナーな機能強化と欠陥解決で構成されるメンテナンスリリースです。 以下のアップデートの完全なリストを参照してください。

### REST API

* 最初に不必要に省略されたメールの配置フィールドのサポートを追加しました。 これらのフィールドは、必要に応じて、REST経由での読み取りと書き込みが可能になります。
   * ブロックリストに登録済み
   * マーケティング中断
   * メールの中断
   * 相対的緊急度
* フィルタータイプ別リードを取得[ エンドポイント ](https://developer.adobe.com/marketo-apis/api/lead-database-endpoint-reference/#/Leads/getLeadsByFilterUsingGET)は、filterTypeとしてleadPartionIdをサポートするようになりました。

### 欠陥解決

**REST エンドポイント**

**説明**

[プログラムを承認](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveProgramUsingPOST)

プログラムの作成時に「運用以外の電子メールをブロック」を「false」に設定した場合、「プログラムを承認」の呼び出しは「true」にリセットされます。

[一括抽出](/help/rest-api/bulk-extract.md)

一部のUnicode文字が抽出出力ファイルで破損しました。

[プログラムを複製](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST)

* メールプログラムを複製した場合、SmartList フィルターロジックは、初期設定に関係なく、結果のプログラムで「すべて」にリセットされました。
* 静的リスト （削除された）を含むプログラムを複製しようとすると、709 「次のアセットはサポートされていません:List」というエラーが表示されました。
* ワークスペース間でプログラムを複製しようとすると、「プログラムを複製できません」という611 エラーが表示されます。

[Idによる静的リストの取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getStaticListByIdUsingGET)

カスタムサービスに読み取り専用アセットの役割の権限がある場合、603、「アクセス拒否」エラーが表示されます。

[Marketo にリードをプッシュ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/pushToMarketoUsingPOST)

**cookie**&#x200B;属性が&#x200B;**input**&#x200B;配列リードオブジェクトで指定された場合、以前の匿名アクティビティは新しく作成されたリードに関連付けられませんでした。

[キャンペーンをスケジュール](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST)

**runAt**&#x200B;日を未来の日付に指定した場合、キャンペーンは実行されず、**success=true**&#x200B;が返されました。 現在、**runAt**&#x200B;の日付が2年を超えている場合、エラーが[1042](/help/rest-api/error-codes.md)に返されます。

[リードを同期](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST)

`action=createDuplicate`と`externalCompanyId` パラメーターを指定した場合（新しいリードを既存の会社に関連付ける場合）、そのリードは（指定された会社ではなく）空の会社に関連付けられました。

#### その他

* すべてのエンドポイント応答から次のデータ変更値を削除しました：mktoClientReqId。 これは内部使用のみでした。
* エラー検索機能を追加しました。 検索ボックスにREST API エラーコードを入力し、下のオートコンプリートリストから選択して、エラーの説明に移動します。
* [ エンドポイント参照](/help/rest-api/endpoint-reference.md) ページを追加しました。 これは、すべてのREST API エンドポイントを1か所に並べ替え可能なリストです。 このページを使用して、アプリケーションで必要な最小限の権限セットを生成することもできます。 これは、カスタムサービスを作成する際に便利です。

投稿日：_2018-10-12_ by _David_

## 2018年秋アップデート

2019年秋リリースは、主にマイナーな機能強化と欠陥解決で構成されるメンテナンスリリースです。 以下のアップデートの完全なリストを参照してください。

### 機能強化

* [Asset API](/help/rest-api/assets.md)の[電子メール CC フィールド ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/email-cc)のサポートを追加しました。 CC フィールドの設定は、承認/クローン操作（電子メールまたは電子メールテンプレートのドラフトの承認、電子メールまたはプログラムの複製）中に想定どおりに反映されます。 すべての電子メール関連エンドポイントが、**ccFields** プロパティのCC Fields値を返すようになりました。 下の応答を下にスクロールして、例を表示します。 この変更は、次のエンドポイントに影響します。[Get Email by ID](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailByIdUsingGET)、[Get Email by Name](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailByNameUsingGET)、[Get Email](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailUsingGET)、[E メールドラフトの承認](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveDraftUsingPOST)、[E メールテンプレートの承認](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveDraftUsingPOST_1)、[電子メールの複製](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneEmailUsingPOST)、[ コピープログラム。](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST)

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

### 欠陥解決

* [Asset API](/help/rest-api/assets.md)に対する[複数のブランディングドメイン ](https://experienceleague.adobe.com/ja/docs/marketo/using/home)のサポートを調整しました。 以前は、電子メールのドラフトの承認、電子メールの複製、プログラムの複製を行う際に、複数のブランディングドメインの設定が反映されませんでした。 これは修正されました。 この変更は、次のエンドポイントに影響します。[電子メール ドラフトの承認](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveDraftUsingPOST)、[電子メールの複製](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneEmailUsingPOST)、[複製プログラム ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST)。
* [apiOnly](/help/javascript-api/configuration.md)構成設定を追加しました。 デフォルトでは、Munchkin タグを含むweb ページは、web ページがブラウザーに読み込まれると、「Web ページにアクセス」イベントを起動します。 場合によっては、これは望ましくありません。 例えば、このイベントがいつ発生するかを完全に制御する必要があるシングルページ web アプリケーションなどです。 このユースケースをサポートするために、新しい&#x200B;**apiOnly**&#x200B;構成設定を追加しました。 trueに設定すると、Munchkin タグは、ページ読み込み中に「Web ページにアクセス」アクティビティを生成しません。
* [domainSelectorV2](/help/javascript-api/configuration.md)構成設定を追加しました。 デフォルトでは、Munchkin タグは、2文字の[国コードの最上位ドメイン ](https://en.wikipedia.org/wiki/Country_code_top-level_domain)を持つサイトでホストされているweb ページを正しく処理しません（例：.io、.co、.ly）。 これにより、Munchkin cookie ドメイン属性が正しく設定されなくなります。 より優れた既成のエクスペリエンスを実現するために、新しい&#x200B;**domainSelectorV2**&#x200B;構成設定を追加しました。 trueに設定すると、改善されたアルゴリズムを使用して、Munchkin cookie ドメイン属性が自動的に設定されます。
* [ オプトアウト ](/help/javascript-api/lead-tracking.md) Cookie ドメインを調整しました。 一部のケースでは、Munchkin オプトアウト cookie （mkto_opt_out）のdomain属性が正しく設定されていませんでした。 Munchkin オプトアウト Cookieは、Munchkin Cookie （_mkto_trk）と同じロジックを使用して、**domainLevel**&#x200B;の設定設定を尊重するなど、ドメイン Cookie属性を判断するようになりました。
* Android アプリケーションの開発者は、このSDKで[Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/) （FCM）をGoogleで直接使用できるようになりました。 詳細については、[こちら](/help/mobile/installation.md)を参照してください。

投稿日：_2018-12-07_ by _David_

## 2019年春アップデート

2019年春リリースは、主にマイナーな機能強化と欠陥解決で構成されるメンテナンスリリースです。 以下のアップデートの完全なリストを参照してください。

投稿日：_2019-03-19_ by _David_

## 2019年6月の更新

2019年6月リリースは、主にマイナーな機能強化と欠陥解決で構成されるメンテナンスリリースです。 以下のアップデートの完全なリストを参照してください。

### REST API

1. 一括書き出しステータスエンドポイントにチェックサムを追加しました。 チェックサムと取得したファイルのハッシュを比較して、取得したファイルの整合性を確認できます。 チェックサムは、書き出されたファイルのSHA-256 ハッシュで、書き出しジョブが完了するとfileCheckSum属性に格納されます。

次のエンドポイントはチェックサムを返します。[ リードジョブのステータスのエクスポート ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsStatusUsingGET)を取得、[ リードジョブのステータスのエクスポート ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsFileUsingGET)を取得、[ アクティビティジョブのステータスのエクスポート ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsStatusUsingGET)を取得、[ アクティビティジョブのエクスポート ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportActivitiesUsingGET)を取得

#### 欠陥解決

1. 整数フィールドに10進数を読み込む際の[一括カスタムオブジェクト読み込み](/help/rest-api/bulk-custom-object-import.md)の問題を修正しました。 修正の前に、整数部分を割り当てて分数部分を破棄することで、10進数を整数に変換しました（例えば、5.432は5に変換されました）。 これで、データの不一致を含む行ごとに「フィールドSource IDのデータタイプが無効です」エラーが生成されました。
1. [ コピープログラム ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) エンドポイントを使用して作成された電子メールプログラムが、特定のケースで通信制限の設定を尊重しない問題を修正しました。
1. 611を返す[ ランディングページドラフトを承認](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveLandingPageUsingPOST) エンドポイントの問題を修正しました。 ランディングページにメール購読解除フォームが含まれている場合の「システムエラー」。
1. 611を返す[ ランディングページドラフトを承認](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveLandingPageUsingPOST) エンドポイントの問題を修正しました。 ランディングページが[ コピーランディングページ ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneLandingPageUsingPOST) エンドポイントを使用して複製された場合の「システムエラー」。

#### 廃止予定機能

1. [ メールエディター1.0の非推奨化](https://nation.marketo.com:443/t5/knowledgebase/email-editor-1-0-is-being-deprecated-june-18th/ta-p/250666)の一環として、1.0 メールAssetsは2019年末に読み取り専用になります。 すべての1.0電子メールAssetsは、説明として2.0に変換する必要がありますE メールドラフト、ベッド [ここ](https://nation.marketo.com:443/t5/knowledgebase/email-editor-1-0-is-being-deprecated-june-18th/ta-p/250666). このイベントに備えるために、1.0 Email Assetsを変更しようとするメール関連のエンドポイントに警告を追加しました。 以下に、警告を含む応答の例を示します。

`{` `"success": true,` `"errors": [],` `"requestId": "15c57#16b338d6e75",` `"warnings": [` `"This is a v1 email asset. API support for modifying v1 emails is being dropped, and this operation will not work on v1 emails in the future. To avoid service interruptions, upgrade this and related assets by editing them in the User Interface."` `],` `"result": [` `"{\"service\":\"sendTestEmail\",\"result\":true}"` `]` `}`

次のメール関連エンドポイントは、警告を返します。

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

メールスクリプティング （Apache Velocity）

#### 廃止予定機能

1. セキュリティ目的で、Velocity スクリプト機能のサブセットが無効化されました。 これには、getClass （）、$class、$context、$textなどのメソッドと変数が含まれます。 詳しくは[こちら](https://nation.marketo.com:443/t5/knowledgebase/unsupported-velocity-tools-disabled-in-june-2019-release/ta-p/251177)をご覧ください。

投稿日：_2019-06-14_ by _David_

## 2019年8月の更新

2019年8月に、新しいREST APIをリリースし、既存のAPIを強化し、欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

### 機能強化

1. 強化されたスマートキャンペーンのライフサイクル機能。 スマートキャンペーンで次の操作を実行できるようにするための新しいエンドポイントを追加しました：名前で取得、作成、更新、複製、削除。 完全な情報は[こちら](/help/rest-api/smart-campaigns.md)にあります。
1. クエリ機能を改善するための拡張スマートリストエンドポイント。
   1. [Get Smart List by Id](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListByIdUsingGET) エンドポイントは、**includeRules** ブール値パラメーターを渡すと、スマートリスト ルールの説明（トリガーとフィルター）を返すようになりました。
   1. [Get Smart Lists](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListsUsingGET) エンドポイントでは、**earliestUpdatedAt**&#x200B;および&#x200B;**latestUpdatedAt**&#x200B;日時パラメーターを渡す際に、日付範囲で結果をフィルタリングできるようになりました。 さらに、このエンドポイントは、キャンペーンとメールプログラムのメンバーであるスマートリストを返すようになりました。
1. スマートリスト定義を抽出するためのエンドポイントを追加しました。
   1. スマートキャンペーン IDで[ スマートリストを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListBySmartCampaignIdUsingGET) エンドポイントは、特定のスマートキャンペーン IDのスマートリストレコードを返します。
   1. プログラム IDで[ スマートリストを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListByProgramIdUsingGET) エンドポイントは、指定されたプログラム IDのスマートリストレコードを返します。
1. [ メールコンテンツの更新](https://developer.adobe.com/marketo-apis/api/asset/#operation/updateEmailContentUsingPOST) エンドポイントを強化して、テンプレート（件名、名前、メール、返信先）から壊れたメールのメールヘッダーフィールドを更新できるようにしました。 テンプレートからの破損については、[こちら](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/edit-an-emails-html)で説明しています。

### 欠陥解決

1. 承認済みのランディングページで[ ランディングページを削除](https://developer.adobe.com/marketo-apis/api/asset/#operation/deleteLandingPageByIdUsingPOST)を呼び出すと、ランディングページが削除される問題を修正しました。 「709、承認済みランディングページを削除できません」エラーが正しく返されるようになりました。[LM-127271]
1. 611を返す[ サンプルメールを送信](https://developer.adobe.com/marketo-apis/api/asset/#operation/sendSampleEmailUsingPOST) エンドポイントの問題を修正しました。 メールがテンプレートから壊れた場合の「システムエラー」。[LM-127288]
1. [ プログラムを削除](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) エンドポイントで、「709、プログラムを削除できません」を発行する代わりに使用中のプログラムを削除する問題を修正しました。 アセットが別の場所で使用されているか、削除できない」エラーが表示されます。[LM-125431]

### 廃止予定機能

1. メールエディター1.0のAPI サポートは、2020年1月に非推奨（廃止予定）になる予定です。 その前に、アセットを2.0に変換することを忘れないでください。 1月以降に電子メール 1.0 アセットに書き込んだり、複製したりすると、警告ではなくエラーが発生します。 メール API [の詳細については、こちらを参照してください](https://nation.marketo.com:443/t5/knowledgebase/email-2-0-and-email-api-faq-s/ta-p/251423)。
1. セキュリティに関するAdobeのワールドクラスの標準に合わせるため、2019年12月13日より、Transport Layer Security （TLS） 1.0および1.1のサポートを廃止します。 1.2 プロトコルに準拠していない Marketo と統合しているシステムは、Marketo Engage サービスにアクセスできなくなる可能性があります。 Marketo Engageへのアクセスを維持するには、すべてのクライアントシステムが2019年12月13日（PT）より前にTLS 1.2に準拠していることを確認してください。 詳細は[こちら](https://nation.marketo.com:443/t5/knowledgebase/tls-1-0-1-1-deprecation-faq/ta-p/249085)をご覧ください。

1. すべてのスマートキャンペーン関連コンテンツが、[ スマートキャンペーン ](/help/rest-api/smart-campaigns.md) メニュー項目（REST API/Assetsの下）に配置されるようになりました。

投稿日：_2019-08-16_ by _David_

## 2020年1月の更新

2020年1月には、新しいREST APIをリリースし、既存のAPIを強化し、欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

* カスタムオブジェクトスキーマ定義をプログラムで作成する機能を追加しました。 これにより、カスタムオブジェクトを1回定義し、必要な数のインスタンスにプロビジョニングできます。 これにより、サンドボックスやセンターオブエクセレンスのモデルを効果的に活用できるようになります。 ISVが顧客オンボーディングプロセスを簡素化することもできます。 カスタムオブジェクトメタデータ APIにアクセスするには、適切なサブスクリプションタイプが必要です。
* プログラムメンバーの一括インポートおよびエクスポート機能を追加しました。 この新しいエンドポイントのセットは、非同期の一括処理ジョブを作成するための既存のMarketo REST API パターンに従います。 プログラムメンバーレコードには、プログラムメンバーカスタムフィールドやリードフィールドを含めることができます。
* プログラムメンバーのカスタムフィールドをフォームフィールドとして使用できるように、「利用可能なフォームプログラムメンバーフィールドを取得」エンドポイントを追加しました。 これにより、Marketo フォームで使用できるすべてのプログラムメンバーのカスタムフィールドのリストが返されます。
* 特定の電子メールテンプレートに依存する電子メールアセットのリストを返す](/help/rest-api/email-templates.md) エンドポイントで使用される[電子メールテンプレートを取得を追加しました。 これにより、メールテンプレートが変更された場合の影響をすばやく把握し、それらの依存関係に容易に対処できます。

投稿日：_2020-01-17_ by _David_

## すべてのカスタムオブジェクトの取得方法

MarketoのAPIを使用して、すべての[ カスタムオブジェクト ](https://experienceleague.adobe.com/ja/docs/marketo/using/home) （CO）のリストを取得する方法を尋ねられることがよくあります。 COのクエリには、その名前よりも多くの情報が必要です。各COに関する一部の&#x200B;_a priori_&#x200B;の知識も必要です。 その知識を取得する方法は、APIが直接クエリする方法を提供しないので、明らかではないかもしれません。 Marketo Engageの多くの目標と同様に、スマートリストは、人物（リード）にリンクされたCOに対する回答を提供します。 スマートリストは会社の場合は異なる動作をし、フィルターのオブジェクトのタイプにリンクされているすべての会社のリストが表示されるので、目標に応じて会社の重複を排除する必要があります。 新しいカスタムオブジェクトが承認されるたびに、関連するフィルターが作成されます。 名前は「**Co NAME**」の形式で指定されます。 次の例では、カスタムオブジェクト名は「**Conference Track Subscription」**&#x200B;で、そのフィルター名は「**Has Conference Track Subscription**」です。 スマートリストを作成したら、[ カスタムオブジェクトエンドポイント ](/help/rest-api/custom-objects.md)を使用して、関連するCOのクエリに必要な情報を取得できます。 リンクされたフィールド（IDまたは電子メールアドレス）が含まれていることを確認して、リストを書き出します。 **smartListName**&#x200B;または&#x200B;**smartListId** フィルターによる[Bulk リード抽出API](/help/rest-api/bulk-lead-extract.md) フィルターを使用して書き出すか、UI](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/managing-people-in-smart-lists/export-people-to-excel-from-a-list-or-smart-list)から[書き出すことができます。 次の手順では、リンクされた各フィールド値を使用して、関連付けられたカスタムオブジェクトを個別にクエリします。 この例では、カスタムオブジェクトの名前は&#x200B;**「Conference Track Subscription」**&#x200B;で、API名は&#x200B;**conferenceTrackSubscription_c**&#x200B;です。 API名は、UIでは「**API Name**」として、API経由では「**name**」として検索できます。  管理者| Marketo カスタムオブジェクト [/キャプション ]次のフラグメントが[ カスタムオブジェクトのリスト API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/listCustomObjectsUsingGET) エンドポイントによって返されます。

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

スマートリスト内の人物に関連付けられた1対1のカスタムオブジェクト（1:1）または1対多のカスタムオブジェクト（1:N）を取得するには、次のようなリクエストを作成します。

`GET /rest/v1/customobjects/conferenceTrackSubscription_c.json?filterType=leadID&filterValues=1000302,1000303,1000304,1000306,1000307`

この例では、このカスタムオブジェクトは&#x200B;**leadID** フィールドによってPersonにリンクされているため、フィルタータイプは「**leadID**」です。 フィルター値パラメーターは、スマートリストの書き出しから取得したIDのコンマ区切りリストです。 リクエストには、1つのリクエスト URIに適合できる最大8,000文字のフィルター値を含めることができます。 この長さを超えるリクエストは、414 HTTP レベルのエラーコードを返します。 応答は複数のチャンクで返される可能性があります。 その場合、**moreResult**&#x200B;は&#x200B;**true**&#x200B;になり、**nextPageToken**&#x200B;が含まれます。 その後、**moreResult**&#x200B;が&#x200B;**false**&#x200B;になるまで、[ ページから](/help/rest-api/paging-tokens.md)の結果を表示する必要があります。 上記のAPI リクエストの結果の一部を以下に示します。

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

これで、スマートリスト内の人物に直接関連付けられた各カスタムオブジェクトの値が取得され、値を取得するだけでなく、**marketoGUID**&#x200B;を使用して[更新](/help/rest-api/custom-objects.md)または[削除](/help/rest-api/custom-objects.md)これらのオブジェクトを使用できます。 多対多の関係にある人物（N:N）に関連付けられたカスタムオブジェクトの場合、上記の技術は、各人物を複数の第2 レベル COに接続する中間オブジェクトである第1 レベルのオブジェクトを返します。

これらの2番目のレベル COを取得するには、リンクフィールドと1番目のレベルの中間オブジェクトから抽出された値をフィルタリングして、2番目のレベル CO タイプに対する新しいクエリのセットを開始します。 例えば、上記の「**Conference Track Subscription」** オブジェクトには、**「Session」**&#x200B;というセッションを表す別のレベルのオブジェクトがあり、これは&#x200B;**subscriptionID**&#x200B;によってリンクされている可能性があります。 上記のConference Track サブスクリプションにリンクされたセッションを取得するリクエストは、次のようになります。

`GET /rest/v1/customobjects/session_c.json?filterType=subscriptionID&filterValues=4ad59184-6bf1-4eeb-a583-d82aeee68210,e5e0aba4-f27f-494d-93ed-9cb580989bf3,e65007cd-86b1-4c17-8d55-057c96e1788a,39d956b2-85e2-4c24-94e7-e9fa5a09d3d0,bf14218c-ae6a-42b3-a14e-f7182903cbcd`

_脚注_ _1）**smartListName**と&#x200B;**smartListId**のフィルタータイプは、一部のサブスクリプションでは使用できません。 サブスクリプションで利用できない場合は、Create Export Lead Job エンドポイント （**&quot;1035, Unsupported filter type for target subscription&quot;**）の呼び出し中にエラーが発生します。 お客様は、Marketo サポートに連絡して、サブスクリプションでこの機能を有効にすることができます。_

投稿日：_2020-01-14_ by _Tony_

## リードの獲得方法

Marketo Engageのインスタンスから一人ひとり（リード）を取得するために必要なプロセスについて、多くの問い合わせが届きます。 これまで多くの有益な回答を提供してきましたが、これほど完全な回答は一つもありませんでした。 MarketoのBulk Extract APIを使用して、あらゆるリードを抽出するために必要な概念をいくつか特定しました。 他のすべての詳細は、私が作成したデモンストレーションコードから学ぶことができます。 この記事では、Marketo Engageインスタンスから各リードを取得するために必要な情報を包括的に解説します。

### 概要

コア手法は、[一括引き出しAPI](/help/rest-api/bulk-lead-extract.md)を使用します。 フィルターを使用せずにリードの一括書き出しジョブを作成できることが想定されますが、次の操作はできません。**APIにはフィルターが必要です**。 使用可能なフィルターは、**createdAt**、**staticListName**、**staticListId、** updatedAt **、** smartListName **、および** smartListId **です。**&#x200B;フィルターのないスマートリストによるフィルタリングも魅力的に思えます。 それを試してみると、システムがフィルターなしでスマートリストを扱うのに十分なスマートであることがわかります。APIにはここでもフィルターが必要です。 フィルターが必要なので、使用する信頼できる正規フィルターは&#x200B;**createdAt**&#x200B;です。 このフィルタータイプでは、最大31日間の日付範囲が許可されるため、複数のジョブを実行して結果を組み合わせる必要があります。 まず、ターゲットインスタンスでリードの可能な限り古い作成日を見つけます。 可能な限り最も古い日付から始めて、31日から1秒間のジョブを作成します（後ほど詳しく説明します）。 各ジョブを作成したら、キューに入れ、完了するのを待ちます。 次に、結果のファイルをダウンロードし、チェックサムを使用してその整合性を確認します。 最後に、IDでリードを重複排除し、一意のリードを出力CSV ファイルに書き込みます。

### 最も古いリードを探す

ターゲットインスタンスのリードの可能な限り古い日付を取得するために、少し「トリック」を使っています。 このタスクに特化したAPI エンドポイントはないので、少し創造性が必要です。 私がすることは、**maxDepth = 1**&#x200B;を持つすべてのフォルダーをクエリすることで、インスタンス内のすべてのトップレベルフォルダーのリストが表示されます。 次に、**createdAt**&#x200B;の日付を収集し、それらを解析して、最も古い日付を見つけます。 この方法は、デフォルトのトップレベルのフォルダーがインスタンスで作成され、それ以前にリードを作成できなかったため機能します。

### 必須フィールドを選択

抽出するフィールドを決定する必要があります。 [ リード 2の説明エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeUsingGET_2)を使用して、ターゲットインスタンスの使用可能なフィールドを検索します。 そのリクエストに対する応答には、「フィールド」という名前のリストが含まれます。 レスポンスの例を次に示します。

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

このエンドポイントは、標準フィールドとカスタムフィールドの両方を含む完全なリストを返します。 要求するフィールドが多いほど、書き出しジョブの完了に時間がかかり、結果として得られるファイルが大きくなります。 通常、必要なフィールドのみを選択する必要があります。 使用可能なすべてのフィールドをリクエストすることを妨げるものは何もありません。これがデモです。 書き出しジョブの作成時に必要なフィールド IDは、**name**&#x200B;の値です。 すべてのフィールド名のリストに名前の値を抽出します。 そして、各書き出しジョブを作成するときに、利用可能なすべてのフィールドをリクエストするために使用します。

### エクスポートのジョブ日付範囲：各31日

各エクスポートジョブは最大31日間に及びます。 私が使用しているデモインスタンスは2016年8月に作成されたので、現在は40を少し超えるジョブを作成する必要があります。 これは、最初の作成日から31を切り上げた日数です。 APIでは、2つの書き出しジョブを一度に処理できるので、2つのジョブを並行して実行しながら抽出できます。 一括抽出ジョブは、他のすべての統合と共有されるリソースなので、便利です。 他の仕事を他の統合に利用できるようにして、単一の仕事を次々と実行することを示します。 **createdAt** フィルターに使用される日付は、[ISO 8601仕様](https://www.w3.org/TR/NOTE-datetime)を使用して書式設定されます。 これらは常にGMT （Z+0000）にあるので、タイムゾーンは単に「Z」または「+00:00」として表されます。 2016年8月1日は&#x200B;**2016-08-01T00:00:00+00:00**&#x200B;で、31日後は&#x200B;**2016-09-01T00:00:00+00:00**。 開始時間と終了時間の両方が含まれているので、その終了時間から1秒減算します：**2016-09-01T00:00:00+00:00** ～ **2016-08-31T23:59:59+00:00**。 2番目の減算を行うと、重なり合う時間が回避されます。 GMTがデフォルトなので、**Z**&#x200B;または&#x200B;**+00:00**&#x200B;をオフにすることもできます。

### 重複の除外

重複を避けるという手間をかけたのに、重複排除も導入しました。 時間が変化した場合（[夏時間](https://en.wikipedia.org/wiki/Daylight_saving_time)）にエッジケースが発生して値が不明瞭になる場合があり、その結果、MarketoのBulk Extract APIで予期しない重複したリードが返される可能性があるので、これを行いました。 このようなことが起こることはまれですが、日時フィルター範囲を使用して統合を行う場合は、考慮する必要があります。 私は、時代が包摂的であることを明らかにするため、一秒を取り除きました。 **createdAt**&#x200B;と&#x200B;**endAt**&#x200B;の&#x200B;**2016-08-01T00:00:00Z**&#x200B;と&#x200B;**2016-09-01T00:00:00Z**&#x200B;でジョブを作成する場合、**2016-09-01T00:00:Z}で作成されたリードが含まれないと考えたくありませんそうします。**

### ジョブの作成

最初の手順は、[Create Export Lead Job エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createExportLeadsUsingPOST)を使用してジョブを作成することです。 このデモでは、最初の書き出しジョブを作成するリクエストは次のようになります。

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

### ジョブのエンキュー

今は仕事が作られているが、何もしないで座っているだけだ。 ジョブを実行するには、**exportId**&#x200B;値を使用して[enqueue エンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/enqueueExportLeadsUsingPOST)を呼び出し、リクエストのURIを構築する必要があります。 例えば、次のようになります。

`POST /bulk/v1/leads/export/4f2b9115-c3f2-4e40-a87c-bf803bbfed99/enqueue.json`

このPOSTに対する本文はありません。ここではPOST HTTP動詞を使用しています。 そのリクエストは次のような応答を生成します。

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

前述したように、一度に実行できるジョブの数には制限があります。 1回にキューに入れるジョブの数には制限があります（10）。 40以上が必要なので、制限によって一度にすべての仕事を作れなくなります。 他の統合でもジョブを実行できるので、すべてのスロットがいっぱいになる可能性を考慮する必要があります。 既に10個のキューに入っているジョブがある場合、新しいジョブをエンキューしようとすると、[1029](/help/rest-api/error-codes.md) エラーが発生します。 **1029**&#x200B;を取得した場合は、ジョブがエンキューされるまで指数関数的なバックオフを使用します。 リクエスト間で最大4分の&#x200B;**1029** エラーコードが表示されるたびに、1分待って、その値を2倍にします。ただし、それ以上の時間は絶対にありません。 この手法は、[切り捨てバイナリ指数バックオフ ](https://devopedia.org/binary-exponential-backoff)として知られており、回復可能なエラーとステータスチェックのベストプラクティスです。

### ジョブが完了するのを待つ

各ジョブの実行には時間がかかるため、[ ステータスエンドポイント ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsStatusUsingGET)を呼び出して、進行状況を監視します。 繰り返しますが、**exportId**&#x200B;を次のようにリクエスト URIに含めます。

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

ジョブステータスが「キューに入っている」間、同じ指数関数的バックオフ（1分から4分）を実行します。 ステータスはリアルタイムではなく、1分に1回更新され、より迅速にポーリングするためのメリットはほとんどありません。 ジョブのステータスが「処理中」に変わったら、バックオフをリセットします。 ステータス「完了」を待っています。次のようになります。

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

リクエストでリードが返されない場合、**numberOfRecords**&#x200B;の値は0です。 この値を確認し、意味のあるときに次のステップをスキップします。 リードが返されたら、**fileChecksum**&#x200B;値を抽出します。 ダウンロード時にファイルの整合性を確認するために使用します。

### リードを獲得

**numberOfRecords**&#x200B;が0より大きい場合は、[ リードファイルの書き出し](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsFileUsingGET)を使用して書き出したファイルを次のようなリクエストでダウンロードします。

`GET /bulk/v1/leads/export/4f2b9115-c3f2-4e40-a87c-bf803bbfed99/file.json`

エラーなしで転送されたファイルを確認します。ファイルのチェックサムを計算し、先ほど保存した&#x200B;**fileChecksum**&#x200B;と比較します。 [SHA-2](https://en.wikipedia.org/wiki/SHA-2)、特にSHA256 ハッシュ関数を使用してチェックサムを計算します。 計算されたチェックサムが一致しない場合、ファイル転送にエラーが発生したため、もう一度転送するか、手動で中断して回復します。

### データの集計

最初のリードから今日まで、31日間のレンジをすべてサイクリングした後は、完全なセットを入手できます。 また、範囲ごとに1つのファイルがあります。 各リードを含む単一の集約ファイルを作成する最も簡単な方法は、最初のファイルを除くすべてのヘッダー行を削除した後に、これらのファイルを連結することです。 そのような場合は、データ処理パイプラインの後半で重複する可能性を想定し、計画することを忘れないでください。 デモでは、ダウンロード時にファイルを処理します。 出力ファイルにデータの各行を追加する前に、行のリード IDが既に書き込まれているかどうかを確認して重複を除外します。

[ここ](https://github.com/Marketo/REST-Sample-Code/tree/master/python/LeadDatabase/Leads)でホストされているデモンストレーションコードを開発しました。このプロセスの詳細を記入し、独自の開発のテンプレートとして機能することを願っています。 デモコードは学習ツールとなることを目的としているため、実稼動システムに必要な堅牢性の改善が行われています。**このコードはAS-IS**&#x200B;としてMITのライセンスで提供されていますが、人間の監視下で1回限りの使用に適しています。 今は何もあなたを止めていません！ このプロセスに従うと、MarketoのBulk Extract APIを使用してすべてのリードを抽出し、場合によってはターゲットのMarketo Engage インスタンスのすべてのフィールドを抽出します。 さらに絞り込むには、各リードの手法を活用します。

投稿日：_2020-03-05_ by _Tony_

## 2020年2月の更新

2020年2月に、新しいREST APIをリリースします。 以下のアップデートの完全なリストを参照してください。

### お知らせ

* 2020年9月以降、[Asset API](/help/rest-api/assets.md) エンドポイントは&#x200B;**_method** クエリパラメーターを受け付けなくなります。 これは、URIの長さの制限を回避するために、POST本文のクエリパラメーターを渡すために使用されました。 このパラメーターを必要とするリクエストに対応するために、Asset APIのURI制限が6KiBから65KiBに増加します。
* ITPに関する私たちの見解については、次のMarketo コミュニティの投稿を参照してください。[ ブラウザーのCookieの更新：Marketo/Munchkinが影響を受ける方法](https://nation.marketo.com:443/t5/knowledgebase/browser-cookie-updates-how-marketo-munchkin-is-affected/ta-p/251524)
* 「進行状況のステータスを変更」アクティビティが変更されました。 「プログラムメンバーID」属性が、今後の機能「プログラムメンバーカスタムフィールド」のサポートでに追加されました。

投稿日：_2020-02-26_ by _David_

## Munchkin Associate Lead Methodの廃止

Munchkin JavaScript クライアントの次のリリースであるバージョン 159では、Munchkin [Associate Lead method](/help/javascript-api/api-reference.md)の廃止を開始します。 このバージョン以降、メソッドが呼び出されると、ブラウザーコンソールに、今後のリリースでメソッドが削除されることを示す警告が表示されます。 メソッドが削除されると、そのメソッドを使用しようとすると失敗します。 最近この方法を使用したことが確認されたMarketoのお客様には、個別に使用が通知されます。 Munchkin 159 リリースの詳細については、[このMarketing Nation Post](https://nation.marketo.com:443/t5/product-documents/munchkin-javascript-version-159-amp-associate-lead-deprecation/ta-p/299687)を参照してください。

### よくある質問（FAQ）

自分が影響を受けているかどうかを知るにはどうすればよいですか？

Adobeは、サブスクリプションでこのメソッドの使用状況を確認したユーザーに通知し、非推奨期間に何度か通知します。

この方法はいつ削除されますか？

このメソッドは、2021年10月のMarketo リリースと同時に一般提供が予定されているMunchkin JS v161で削除されます。

なぜこの方法が削除されるのですか？

この方法の導入以来、同じユースケースを実現するよりパフォーマンスの高い方法が実装され、リリースされました。 当社のサービスのパフォーマンスと健全性を向上させるために、許容可能な基準を満たさない機能を削除することが必要な場合があります。

この方法の代わりに何を使用すればよいですか？

Munchkin アソシエイトリードには、2つの主要なユースケース、人物データの提出、およびMarketoの対応する人物レコードへのブラウザーのweb トラッキング Cookieの関連付けがあります。 Munchkin アソシエイトリードが導入されて以来、データ送信とCookie関連付けをより堅牢に実行する方法が導入されました。

#### サーバーサイド送信

ブラウザー側での送信が必要ない場合、REST APIは[人データ送信](/help/rest-api/leads.md)のための多くのメソッドと、Cookieを人物レコード ](/help/rest-api/leads.md)に関連付けるための[専用のメソッドを提供します。

Munchkinのバージョン 159はいつ公開されますか？

バージョン 159は、2020年10月のMarketo リリースから一般提供されています。

投稿日：_2020-05-06_ by _Kenny_

## バックグラウンドでのMarketo フォーム送信

web コンテンツや顧客データをホスティングするための様々なプラットフォームが存在する企業では、フォームから並行してデータを送信し、別々のプラットフォームでデータを収集できるようにする必要があることが一般的になっています。 これを行う方法はいくつかありますが、最も優れているのは、多くの場合、最もシンプルなものです。Forms 2 APIを使用して、非表示のMarketo フォームを送信します。 これは新しいMarketo フォームでも機能しますが、理想的にはこれにはフィールドがない空のフォームを作成する必要があります。 これにより、フォームは何もレンダリングする必要がなくなるため、必要以上にデータを読み込むことがなくなります。 次に、フォームから[埋め込みコード ](https://experienceleague.adobe.com/ja/docs/marketo/using/home)を取得し、目的のページの本文に追加して、小さな変更を加えます。 埋め込みコードには、次のようなフォーム要素が含まれています。

`<form id="mktoForm_1068"></form>`

要素に「style=&quot;display:none&quot;」を追加して、次のように要素が表示されないようにします。

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

この方法で送信されたFormsは、リードが記入し、目に見えるフォームを送信した場合とまったく同じように動作します。 送信のトリガーは、実装によって異なります。各トリガーにはプロンプトを表示するアクションが異なりますが、基本的に任意のアクションで実行できます。 重要なのは、フィールドと値を正しく設定することです。 フィールド名の書き出しで確認できるフィールドのSOAP API名を使用して、値を正しく送信してください。

### Munchkin Associate Leadからの移行

バックグラウンドフォームの送信は、Munchkin アソシエイトリードの推奨される代替方法の1つです。 下のサンプル HTML ページでは、リードの関連付けに送信された値と同じ値を再利用して、マイグレーションの概要を示しています。

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

投稿日：_2020-05-26_ by _Kenny_

## 2020年7月の更新

2020年7月には、新しいREST APIをリリースし、既存のAPIを強化し、欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

* 招待を受け入れていないユーザー（つまり「保留中」のユーザー）をクエリおよび削除できる2つのエンドポイントを追加しました。 [Get Invited User by Id](/help/rest-api/user-management.md) エンドポイントを使用すると、保留中のユーザーをクエリできます。 [招待ユーザーを削除](/help/rest-api/user-management.md) エンドポイントを使用すると、保留中のユーザーを削除できます。
* [ ユーザーを招待](/help/rest-api/user-management.md) エンドポイントが更新され、**expiresAt** パラメーターのISO 8601準拠の日付時刻文字列を受け入れるようになりました。
* [Get User by Id](/help/rest-api/user-management.md)および[ ユーザー属性を更新](/help/rest-api/user-management.md) エンドポイントの両方が更新され、**lastLoginAt**&#x200B;属性の最後のユーザーログイン時間が返されました。
* 既に存在する静的リストを作成しようとすると、[静的リストを作成](https://developer.adobe.com/marketo-apis/api/asset/#operation/createStaticListUsingPOST) エンドポイントで「611、システムエラー」というエラーが返される問題を修正しました。 エラー「709、同じ名前の静的リストが既に存在する」を返すように変更されました。[LM-135934]
* 既に存在する電子メールを作成しようとすると、[電子メールを作成](https://developer.adobe.com/marketo-apis/api/asset/#operation/createEmailUsingPOST) エンドポイントで「611、システムエラー」というエラーが返される問題を修正しました。 エラー「709、同じ名前の電子メールが既に存在します」を返すように変更されました。[LM-138648]
* ランディングページクエリエンドポイントが誤った&#x200B;**createdAt**&#x200B;値を返していた問題を修正しました。 エンドポイントは、ランディングページが最後に承認された時間を返していました。 ランディングページを作成した時点に戻ります。[LM-138648]
* [ リードを結合](https://developer.adobe.com/marketo-apis/api/mapi/#operation/mergeLeadsUsingPOST) エンドポイントが無効な結合操作に対してエラー「611、システムエラー」を返す問題を修正しました。 結合によってリードが重複し、**mergeinCRM**&#x200B;がtrueに設定された場合に発生しました。 エラー「712、重複レコードを作成しています」を返すように変更されました。 代わりに既存のレコードを使用することをお勧めします。[LM-137463]

投稿日：_2020-08-01_ by _David_

## ゲスト投稿 – ディープダイブ：カスタムオブジェクトとカスタムアクティビティとカスタムフィールドの違い

**これは、Amit Jain氏、Marketo Champion 2020、マーテク IT スペシャリスト**&#x200B;によるゲスト投稿です。エンタープライズレベルのマーケティングオートメーションプラットフォームであるMarketoは、複数のソースから取得したユーザー/顧客/見込み顧客の情報を管理し、より優れたパーソナライゼーション、セグメンテーション、レポートのためにMarketoで管理します。 そうしたソースは、web サイトフォームからリスト構築、CRM データ、e コマースデータに至るまで、多岐にわたります。 Marketoでは、リード、会社、商談、アクティビティなどの標準オブジェクトを提供しています。これらの標準オブジェクトは、Marketoで使用できる拡張データセットの新たなマーケティングニーズを満たすのに十分でない場合があります。

例えば、カートに追加されたアイテム、様々なコースに申し込んだ学生、特定のユーザーが所有する製品、異なるサブスクリプションの同意など。この情報は、マーケターがさまざまなプラットフォームをまたいで、よりパーソナライズされたコンテンツと統合されたユーザーエクスペリエンスを提供することで、顧客や見込み客を惹きつけるために不可欠です。 このようなビジネスニーズに対応するために、Marketoでは、カスタムフィールド、カスタムアクティビティ、カスタムオブジェクトにこのタイプのデータを保存するカスタム方法を提供しています。 どのオプションをいつ使用するかを理解するのに問題がある人を観察しました。 このブログ記事では、**これら3つの要素が実際にどのようなものなのか、またどの要素をいつ使用するのかを詳しく説明します。**

**カスタムフィールド**

Marketoの「リード」オブジェクトはマスターオブジェクトであり、他のすべてが直接または間接的に接続されています。 Marketoでは、「リード」オブジェクト、「会社」オブジェクトにカスタムフィールドを作成でき、最近、「プログラムメンバー」カスタムフィールドのサポートが発表されました。 これらのカスタムフィールドは、特定のタイプのデータを保存する必要性を満たします。 例えば、ジョブ関数またはユーザーからの異なる同意を保存する必要がある場合があります。 Marketoのカスタムフィールドには、次の2種類があります。

1. **CRM フィールドから同期済み：**&#x200B;自動Marketo ↔︎ SFDC同期の一環として、Marketoは、リード、取引先責任者、アカウント、商談オブジェクトでMarketo ユーザーに表示されるすべてのカスタムフィールドをSFDCで同期します。
1. **Marketoのみフィールド：** Marketoでフィールドを直接作成できます。 これらのフィールドのデータは、SFDCと同期されません。

**簡単なヒント**

* Marketoのみのフィールドを使用して、SFDCでデータを同期しますか？ この方法については、[このブログ ](https://themarketingautomationblog.com/2019/12/06/field-management-merging-remapping-hiding-marketo-fields/)を参照してください。
* カスタムフィールドについて詳しくは、[こちら](https://themarketingautomationblog.com/2019/11/15/knowing-your-marketo-fields/)を参照してください。
* 現在、Marketo APIでは、カスタムフィールドの更新や作成はサポートされていません。

**カスタムオブジェクト**

Marketoでは、標準オブジェクトとは別に、独自のカスタムオブジェクトを作成できます。_カスタムオブジェクトを作成し、会社またはリードオブジェクトまたは別のカスタムオブジェクトに関連付けることができます。_ カスタムオブジェクトとは、標準的なリードレコードと企業レコードを補完する、一連のカスタムレコードのことです。 カスタムオブジェクトを使用すると、追加のデータをスケーラブルに保存し、そのデータをリードまたは会社のレコードにリンクできます。 標準（リンクフィールド）フィールドとカスタムフィールドを任意に組み合わせてカスタムオブジェクトを作成し、カスタムオブジェクト _レコード_&#x200B;を作成するためにこれらのフィールドを入力し、それらのレコードをリードまたは会社のレコードにリンクできます。 強力で柔軟なリンクされたレコードにより、セグメント、スマートリスト、キャンペーンを強化できます。リードのフィールドや会社のフィールドにはない情報を使用して、アセットを構築できます。 カスタムオブジェクトは、次のいずれかのタイプの関係を持つことができます。

* **1対1の関係**：各カスタムオブジェクトに1つのリード/企業オブジェクトレコードがあります。
* **一対多の関係**：各カスタムオブジェクトには、リード/会社に関連する複数のカスタムオブジェクトレコードが含まれています。
* **多対多の関係：**。複数のカスタムオブジェクトレコードを複数のリード/企業オブジェクトにリンクできます。 例えば、1つのコースカタログから複数のコースに複数の学生が登録されます。

**簡単なヒント**

* カスタムオブジェクトの設定について詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/home)を参照してください。
* Marketo カスタムオブジェクトは、中間オブジェクトとして使用できます。これは、カスタムオブジェクトのカスタムオブジェクトを意味します。

### カスタムオブジェクトの利点？

カスタムオブジェクトを使用すると、企業やリードに関連する一意のデータを収集して使用できますが、企業やリードに関する静的な情報とは限りません。 リードフィールドは、個人のリード情報（_電子メールアドレス_、_郵便番号_&#x200B;など）、ビジネス情報（_役職_、_業種_&#x200B;など）、またはシステム駆動情報（_Marketo ID_、SFDC ID、作成日など）に関連していますが、カスタムオブジェクトフィールドは完全にカスタマイズ可能です。 例えば、カスタムオブジェクトを使用して、次のような情報を保存します。

* ユーザーの購入履歴：
* カート情報：
* 顧客が期間限定のプロモーション割引コードを使用したかどうかも確認できます。
* 調査結果、インタビュー、イベントへの参加から取得した補足情報。
* 体験版のURL、開始日、終了日、ユーザーの数などを含むユーザーの体験版情報。

### Marketo カスタムオブジェクトの制限

1. Marketoでは、デフォルトで10個のカスタムオブジェクトを作成できます。 サブスクリプション料金を追加して、制限を増やすことができます。
1. オブジェクトあたりのデフォルトのフィールド数は50ですが、必要に応じてMarketo サポートに追加フィールドをリクエストできます。 [Michael Florin](https://www.linkedin.com/in/michaelflorin/)様、追加のご意見をお寄せいただきありがとうございます。
1. すべてのカスタムオブジェクトで保持できるレコードの数には制限があります。 Marketoのサブスクリプションによって異なります。 この制限は、追加のサブスクリプション料金で増やすことができます。
1. APIを使用してカスタムオブジェクトを作成した場合、MarketoではMarketo UIからCO スキーマを編集できません。

**簡単なヒント**

* Marketo APIでは、カスタムオブジェクトに対するCRUD （作成、読み取り、更新、削除）操作をサポートしています。
* Velocity Scriptを使用して、このカスタムオブジェクトデータをメールのパーソナライゼーションに使用できます。
* すべてのカスタムオブジェクト関連エンドポイント [ここ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportProgramMembersStatusUsingGET)を見つけることができます。

### カスタムオブジェクトの用語

**カスタムオブジェクト**：すべてのカスタムオブジェクトレコードのグループを保持するコンテナ。 正式にはデータカードセットまたはカスタムテーブルと呼ばれます。**カスタムオブジェクトレコード**: リードまたは会社に関連付けることができる追加のフィールド情報を保持するデータレコード。 レコードは、標準のリードまたは企業フィールドとカスタムオブジェクトレコードフィールドで構成できます。 正式にはデータカードまたはデータテーブル行と呼ばれます。**カスタムオブジェクトレコードフィールド**：一意または一時的な情報を収集するための完全にカスタマイズ可能なフィールド。 これらのフィールドは、カスタムオブジェクト自体の中に作成され、格納されます。 正式には、データカードフィールドまたはデータベーステーブルフィールド/列と呼ばれます。**リンクフィールド**: カスタムオブジェクトレコードとリンクされたリード/企業オブジェクトレコードとの関係を定義する、特殊なタイプのカスタムオブジェクトレコードフィールド。 カスタムオブジェクトを作成する場合は、カスタムオブジェクトレコードを正しい親レコードに接続するためのリンクフィールドを指定する必要があります。

* 1対多または1対1のカスタム構造の場合は、カスタムオブジェクトのリンクフィールドを使用して、個人または企業に接続します。
* 多対多構造の場合は、2 つのリンクフィールドを使用し、別に作成した中間オブジェクト（カスタムオブジェクトの一種でもある）から接続します。 1 つのリンクはデータベース内の人や会社に接続し、もう 1 つのリンクはカスタムオブジェクトに接続します。 この場合、リンクフィールドはカスタムオブジェクト自体に配置されません。

### カスタムアクティビティ

**組織と対話する方法はいくつかあります。 例えば、企業のweb サイトを訪問したり、展示会に参加したり、メールのリンクをクリックしたりすることができます。 これらのアクションはアクティビティ**&#x200B;であり、そのアクションが何であれ、Marketoはそれをキャプチャするため、マーケティング部門と営業部門は、パーソナライズされた統合されたエンゲージメントに対するユーザーの行動をより深く理解できます。**_カスタムアクティビティ_** _を使用すると、Marketo フォーム、メール、またはランディングページに関連しないアクティビティを追跡できます_。 たとえば、誰かがweb サイトの動画を視聴したり、アンケートに回答したりしたタイミングを追跡するには、カスタムアクティビティを使用します。 カスタムアクティビティは、カスタムオブジェクトとは異なります。 値が変化する（例えば、「車の色」が青から赤に変化する）場合は、カスタムオブジェクトを使用します。 発生するタイミングをトラックする際に詳細が変わらない場合（例えば、「購入した車」）は、カスタムアクティビティを使用します。 デフォルトでは、定義可能なカスタムアクティビティの最大数は10です。 これは、追加のサブスクリプション料金で増やすことができます。 [Marketo データ保持ポリシー](https://nation.marketo.com/t5/knowledgebase/tkb-p/support_solutions-documents)に従い、カスタムアクティビティは25か月後に自動的に削除されます。

**カスタムアクティビティ：** Marketo内でトラッキングするMarketo以外のイベント。**カスタムアクティビティ ID:** Marketoは、Marketo APIを使用してアクティビティデータをプッシュ/プルする際に使用できるカスタムアクティビティに数値IDを割り当てます。**カスタムアクティビティフィールド：** アクティビティメタデータは、アクティビティフィールドに保存できます。 例えば、ビデオのビューをトラッキングする場合、フィールドはページ URL、ビデオタイトルなどになります。**カスタムアクティビティプライマリフィールド：** スマートリストフィルター条件として使用できるカスタムアクティビティフィールド。

**簡単なヒント**

* カスタムアクティビティのAPI エンドポイントは、ここで[利用できます。](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addCustomActivityUsingPOST)

## カスタムオブジェクトとカスタムアクティビティ

**カスタムオブジェクト**

**カスタムアクティビティ**

1

インスタンスごとにデフォルトで最大10個のカスタムオブジェクト。

デフォルトでは最大10個のカスタムアクティビティ。

2

カスタムオブジェクトごとに最大50個のカスタムオブジェクトフィールド。

各カスタムアクティビティタイプには、最大20個のセカンダリ属性を設定できます。

3

最大1MMのカスタムオブジェクトレコード。サブスクリプションに応じて異なる場合があります。

25か月後、Marketo データ保持ポリシーに従ってカスタムアクティビティが削除されます。

4

スマートリストおよびスマートキャンペーンでフィルターおよびトリガーとして使用できます。

スマートリストおよびスマートキャンペーンでフィルターおよびトリガーとして使用できます。

5

メールコンテンツのパーソナライズに使用できます。

メールコンテンツのパーソナライズには使用できません。

6

カスタムオブジェクトレコードに対してCRUD操作を実行できます。

カスタムアクティビティでは、作成と読み取りのみが許可されます。

7

値が変化する（例えば、「車の色」が青から赤に変化する）場合は、カスタムオブジェクトを使用します。

発生するタイミングをトラックする際に詳細が変わらない場合（例えば、「購入した車」）は、カスタムアクティビティを使用します。

8

カスタムオブジェクトが事実を教えてくれます。 すなわち現在の価値。

カスタムアクティビティは、過去に起こったイベントを教えてくれます。

投稿日：_2020-10-18_ by _Amit_

## 2021年1月の更新

2021年1月に新しいREST APIをリリースし、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

* プログラムによるフォーム送信を実行できる[送信フォーム ](/help/rest-api/leads.md) エンドポイントを追加しました。 サードパーティフォームとMarketo formsを統合して、既存のマーケティングワークフローを活用できるようになりました。
* ランディングページのシリアル化されたHTML バージョンを返す[Get Landing Page Full Content](/help/rest-api/landing-pages.md) エンドポイントを追加しました。 Marketo Engageにログインすることなく、ランディングページの完全にパーソナライズされたプレビューをレンダリングできます。 これにより、統合アプリケーション内の編集と翻訳のワークフローを効率化できます。
* Velocity スクリプトを使用して、アクセスできるカスタムオブジェクトの数を設定できるようになりました。 設定手順については、[こちら](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/email-setup/change-custom-object-retrieval-limits-in-velocity-scripting)を参照してください。

### 欠陥解決

* [ ユーザーの削除](/help/rest-api/user-management.md) エンドポイントで、カスタムサービスで使用中のAPIのみのユーザーを削除できる問題を修正しました。 これで、「611、API サービスで使用されているAPI ユーザーを削除できません」というエラーが返されます。[LM-141893]
* [ ユーザーを取得](/help/rest-api/user-management.md) エンドポイントが削除されたユーザーを返す場合がある問題を修正しました。[LM-141542]
* [ コピープログラム ](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) エンドポイントの問題を修正しました。 255文字を超えるプログラム名を指定した場合、「611、プログラムのクローン作成ができません」エラーが返されます。 これで、「701、名前は255文字を超えることはできません」が返されます。[LM-143436]
* [ ランディングページドラフトを承認](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveLandingPageUsingPOST) エンドポイントの問題を修正しました。 モバイル版がアクティブ化されたランディングページを承認すると、デスクトップ版ではモバイル版のコンテンツが表示される場合があります。[LM-146867]
* 1つ以上のフォームでフォローアップページとして使用されていたランディングページを承認できない[ ランディングページを承認できない](https://developer.adobe.com/marketo-apis/api/asset/#operation/unapproveLandingPageByIdUsingPOST) エンドポイントの問題を修正しました。 エラー「709、未承認ランディングページが失敗しました」が返されるようになりました。 ランディングページは、フォーム ID:[_formId1,formId2,..._]&quot;のフォローアップページとして1つ以上のフォームで使用されています。[LM-143326]

投稿日：_2021-01-15_ by _David_

## Munchkin 160 BetaとBeacon API

**2021年1月27日：** アソシエイトのリードの廃止の影響を受ける一部のMarketo ユーザーが、1つ以上のインスタンスでMunchkin Beta設定が有効になっていることを示すメール通知を受信しました。 このリリースは、正しいオーディエンスに通知されるまで保持されます。 Munchkin JavaScriptのバージョン 160以降、[ ビーコン API](https://developer.mozilla.org/ja/docs/Web/API/Beacon_API)は、MunchkinがMarketo バックエンドと通信するデフォルトの方法になります。 これは、**useBeaconAPI**&#x200B;設定パラメーターを介したバージョン 159のリリースにより、2020年夏にオプションとして利用できるようになりました。 Beacon APIは、従来のXMLHttpRequest メソッドを使用するよりも複数の利点がありますが、主な改善は、HTTP通信の非ブロッキング非同期APIであり、現代のすべてのインターネットブラウザーで使用できることです。 Munchkinのほとんどのユーザーは、web サイトの動作の変化に気づきませんが、このアップデートにより、バックエンドへのクリックイベントの送信待ち中にMunchkinがナビゲーションをブロックするのを防ぐことができます。つまり、これは簡単なことですが、新しいページへのリンクをクリックした後にブラウザーが「ハング」する可能性を排除します。 Marketoのお客様の中には、珍しいが不満を抱いている方もいらっしゃいます。

2021年1月27日現在、このバージョンのロールアウトは保留中です。 この変更に関連する問題は予想されておらず、テスト中に特定されたものはありませんが、MarketoでMunchkinのデプロイメント設定をすべてテストすることは不可能です。事前にこれらの変更をテストするか、このバージョンが一般公開されるまで変更を先送りすることをお勧めします。 以下に、様々なシナリオの手順を示します。

### テストビーコン API

今後のバージョンを想定して更新されたBeacon APIをテストする場合は、外部テストページで&#x200B;**useBeaconAPI** パラメーターをMunchkin設定に追加することでテストできます。 このテストは、Munchkinの一般版またはベータ版で動作します。 設定パラメーターは、7行目の`Munchkin.init()` メソッドの呼び出しの2番目の引数に次のように表示されます：`{ 'useBeaconAPI': true}`

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

Marketo ランディングページでMunchkin Betaを無効にするには、サブスクリプションの管理セクションの[ トレジャーチェスト ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features) メニューにアクセスし、Munchkin Beta ランディングページの設定を無効に変更する必要があります。

### 外部ページでMunchkin Betaを無効にする

Beta版のMunchkin JavaScriptを外部web ページにデプロイし、一般公開されるまで変更を保留する場合は、Munchkin JS スニペットを変更して、**munchkin-beta.****js** ファイルではなく**munchkin.****js** ファイルをターゲティングする必要があります。 次の例では、11行目の&#x200B;**s.src**&#x200B;変数の値です。 スニペットは、この例とよく似ていない場合や、外部ページのタグマネージャーによってデプロイされている場合があります。また、Munchkin トラッキングが有効になっている場合は、IT リソースやweb サイトの管理者全員に連絡する必要が生じる場合があります。

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

投稿日：_2021-01-08_ by _Kenny_

## メール V1の最終的なAPI廃止

[ メール V1の廃止は、ほぼ2年前に開始されました](https://nation.marketo.com:443/t5/knowledgebase/email-editor-1-0-is-being-deprecated-june-18th/ta-p/250666)。2021年3月17日のロンドンとオランダのサブスクリプションに対する3月のメンテナンスリリース以降、および2021年3月19日のその他のすべてのサブスクリプションで、V1 メールに対するすべてのAPI サポートは終了します。 このリリースの後、Asset APIを介してV1 メールを操作しようとすると、エラーが発生し、アクションは実行されません。 2021年2月24日以降の既知の残りのユーザーはすべて通知されていますが、これらのアセットを操作しようとする統合がまだ存在する可能性があります。 影響を受ける統合の最も一般的なタイプは、デジタルアセット管理、翻訳、ローカライゼーションを提供するサービスです。 この変更の結果として統合エラーが発生した場合でも、[問題のあるアセットを編集して承認することで、引き続きアップグレードできます](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/transitioning-to-email-editor-2-0)。 メールアセットをV2にアップグレードすると、統合サービスでメールアセットの使用を再開できるようになります。

投稿日：_2021-03-17_ by _Kenny_

## 2021年5月の更新

2021年5月に、新しいREST APIをリリースし、既存のREST APIを強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

* プログラムメンバーシップのレコードを取得、更新、削除できるプログラムメンバーAPIを追加しました。 詳しくは、[REST API > リードデータベース > プログラムメンバー](/help/rest-api/program-members.md)を参照してください。
* 一括処理カスタムオブジェクト抽出APIを追加しました。一対多リレーションシップ内のリードに関連付けられているファーストレベルのMarketo カスタムオブジェクトレコードを書き出すことができます。 詳しくは、[REST API/一括抽出/一括カスタムオブジェクト抽出](/help/rest-api/bulk-custom-object-extract.md)を参照してください。
* [ リード API](/help/rest-api/leads.md)と[一括リード抽出API](/help/rest-api/bulk-lead-extract.md)の両方を強化して、ユーザーがAdobe Experience Cloud ID （ECID）を取得できるようにしました。 これにより、[Adobe Experience Cloud](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-experience-cloud-audience-sharing.html)からオーディエンスを同期するユーザーは、ECIDが関連付けられているリードを識別できます。 これにより、他のAdobe Experience Cloud製品との[統合の可能性](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024277392-Adobe-Experience-Cloud-Using-the-ECID-for-integration)が開きます。
* インポートプロセス中に会社レコードにリードを追加できるように、[一括リード読み込みAPI](/help/rest-api/bulk-lead-import.md)を強化しました。 これは、**externalCompanyId** フィールドをインポートファイルに含めることで行われます。
* Marketo Engage UIで見つかった機能をパリティに提供するために、いくつかのプログラムエンドポイントを強化しました。 イベントプログラムの作成、複製、操作の移動を許可するように、[ プログラムの作成](/help/rest-api/assets.md)および[ プログラムの複製](https://developer.adobe.com/marketo-apis/api/asset/) エンドポイントを強化しました。 これは、イベントプログラムを他のプログラムタイプの下に「ネスト」して整理するユーザー向けです。 また、[ プログラムの削除](https://developer.adobe.com/marketo-apis/api/asset/) エンドポイントを強化して、プッシュ通知、アプリ内メッセージ、レポート、埋め込みソーシャル Assetsを使用したランディングページなどのアセットを含むプログラムの削除を許可するようになりました。
* Marketo管理者は、特定のフィールドを[機密」としてマークできます](https://experienceleague.adobe.com/ja/docs/marketo/using/home)。したがって、その値[はフォームで事前に入力されることはありません](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/demand-generation/forms/form-fields/disable-pre-fill-for-a-form-field)。これにより、ユーザーの機密データを保護できます。 Marketo Engage UIにあるこの機能を使用してパリティを提供するように、いくつかのフォームフィールドエンドポイントを強化しました。

### 欠陥解決

* プログラムエンドポイントの削除に関する問題を修正しました。 共有フォルダー内のプログラムを削除しようとすると、「611、システムエラー」が返されます。 これで、「ターゲットプログラムは共有フォルダー内にあり、削除できません」が返されます。 削除を試みる前に、フォルダーを非共有にする必要があります。」
* コピープログラムエンドポイントの問題を修正しました。 フローステップでDateTimeを含むプログラムを複製しようとすると、「611, System Error」が返されます。 これで、プログラムを正常に複製できます。
* 誤ってメールプログラムの下にプログラムを作成できるプログラム作成エンドポイントの問題を修正しました（これは許可されていません）。
* コピープログラムエンドポイントの問題を修正しました。 ランディングページを含むプログラムを複製した場合、ターゲットプログラム内のランディングページの名前には、プログラム名とランディングページ名の間にアンダースコアが含まれていませんでした。 例：`http://<_pod_\>.marketo.com/lp/<_munchkin_\>/<_program name_\>**_**<_LP name_\>.html`

投稿日：_2021-05-07_ by _David_

## Adobe Exchangeへの期間限定オファー

Marketo Engage パートナーコミュニティのサポートは、お客様の成功の柱の1つです。 「Marketo Engage統合エコシステムがExchange Marketplaceで適切に表現され、LaunchPoint パートナーに特別なオファーを提供することを目指しています」。 延長されない非常に限られた期間で、2022年末まで、LaunchPoint パートナーにExchange プログラムの無料のInnovate パートナーシップを提供しています（約15,000 ドルの価値）。 このオファーは、LaunchPoint パートナーがExchange パートナーポータルで統合リストを作成することを促すために設計されました。その後、Adobe Exchange Marketplaceで一般に検索できます。 2022年12月まで無償で受け取れるInnovate partnership benefitsの完全なリストをご覧ください。

1. [Adobe Exchange パートナーサポートセンター](https://adobeexchangeec.zendesk.com/hc/en-us?mkt_tok=NjA4LURIVi05MTUAAAF-P5lIeVWOuBmKMS_uE_NpgFKtC0ukt7z_ksnq_Sbzb6mzXUuXpqpqQeujtPdZ24WcjMdptygQSR9XrYt_Cw)に移動
1. 右上隅の「リクエストを送信」をクリックします
1. **次の問題を選択してください** ドロップダウンから「Adobe Exchange サポート」を選択します
1. **メールアドレス**&#x200B;にメールアドレスを入力します
1. **件名** ボックスに「LaunchPoint Offer」と入力します
1. **説明** ボックスに「LaunchPoint Offer」と入力します
1. 「**サポートタイプ**」ドロップダウンで「プログラムサポート」を選択します
1. **Adobe Exchange製品** ドロップダウンで「Adobe Exchange プログラム」を選択します
1. フォームを送信します。 私たちのチームは、まもなく連絡しています！

投稿日：_2021-07-22_ by _David_

## 2021年8月の更新

2021年8月には、既存のREST APIを強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

* Bulk Activity Extract APIを強化し、ユーザーが6つの異なるアクティビティタイプのプライマリ属性を使用してフィルタリングできるようにしました。 詳しくは、[ アクティビティの一括抽出](/help/rest-api/bulk-activity-extract.md)を参照してください。
* 「Marketo Sales Connectのユーザーが、セールスアクティビティのデータにさらにアクセスできるようにするために、追加のセールスアクティビティ属性を有効にしました。 「セールスメールを送信」、「セールスメールを開く」、「セールスメールをクリック」アクティビティに、次の属性を追加しました。

* Marketo セールス担当者ID - Sales Connectの個人レコードの一意のID
* セールスキャンペーン名 – メールがセールスキャンペーンの一部であった場合のセールスキャンペーンの名前
* Sales Campaign URL - メールがセールスキャンペーンの一部であった場合のセールスキャンペーンのセールスコネクト URL
* Sales Template Name - テンプレートが使用された場合の、Sales Connectのメールテンプレートの名前
* Sales Template URL - テンプレートが使用された場合のメールテンプレートのSales Connect URL

### メール

* `earliestUpdatedAt`/`latestUpdatedAt` フィルターを追加して、メール取得エンドポイントを強化しました。 これにより、`updatedAt` フィールドを使用して、メールのサブセットのみを検索し、増分同期を許可できます。
* [ChampionおよびChallenger](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/email-tests-champion-challenger/add-an-email-champion-challenger) タイプのメールレコードの取得をサポートするために、「メールの取得」、「名前でメールを取得」、「IDでメールを取得」のエンドポイントを強化しました。

### 欠陥解決

* Get Users エンドポイントの問題を修正しました。 [ マーケティングカレンダー](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/marketing-calendar/understanding-the-calendar/issue-revoke-a-marketing-calendar-license) ライセンスが発行されたユーザーは返されませんでした。 マーケティングカレンダーのユーザーが正しく返されるようになりました。
* フォームエンドポイントの送信に関する問題を修正しました。 重複したリードレコードがある場合、送信フォームを使用して「1007, Multiple lead match lookup criteria」エラーを発行します。 送信フォームは、[Forms 2.0 API](/help/javascript-api/forms-api-reference.md)と同じように、最新に更新されたレコードを更新するようになりました。
* 「リードフィールドを更新」および「リードフィールドを作成」エンドポイントによって返される、いくつかの誤解を招くエラーメッセージを改善しました。[LM-151890、LM-151888、LM-151889]
* 「名前でリードフィールドを取得」および「リードフィールドを取得」エンドポイントの問題を修正しました。 両方のエンドポイントが若干古い情報を返す可能性があります。 現在は常に現在の情報を返しています。
* 範囲内の最後のバイトが返されない部分取得に「range」 HTTP ヘッダーを使用する場合の[Bulk Extract API](/help/rest-api/bulk-extract.md)の問題を修正しました。
* スニペットメタデータエンドポイントの更新に関する問題を修正しました。 スニペット名または説明を更新すると、スニペットのステータスが「ドラフトで承認済み」に変更されました。 これで、スニペット名または説明を更新した後も、切り抜かれたステータスは変更されません。
* メールモジュールの追加エンドポイントの問題を修正しました。 スニペットを含むモジュールを追加すると、「611、システムエラー」が返されました。 モジュールがメールに正しく追加されるようになりました。
* プログラムエンドポイントの削除に関する問題を修正しました。 アプリ内メッセージのローカルアセットを含むプログラムを削除すると、「611、システムエラー」が返されました。 プログラムが正しく削除されるようになりました。

投稿日：_2021-08-22_ by _David_

## Munchkin バージョン 161 ロールアウト

2021年9月7日（PT）に、Munchkin バージョン 161がMunchkin Betaを有効にしてサブスクリプションの10%にロールアウトされ、続いて9月16日（PT）に50%、9月30日（PT）に100%がロールアウトされます。 この変更は、Marketo ランディングページと、新しいバージョンがロールアウトされたサブスクリプションから読み込まれる外部ランディングページに配信されるファイル munchkin-beta.jsのバージョンに影響します。 このバージョンでは、Marketo サブスクリプションに人物データを送信し、既知の人物レコードを使用して関連するweb ブラウジング履歴を許可する機能であるMunchkin Associate Lead メソッドを完全に廃止しました。 アソシエイトリードは、[Forms JS API](/help/javascript-api/forms-api-reference.md)、フォーム送信API、および[ アソシエイトリード REST API](/help/rest-api/leads.md)など、より現代的で安全な代替手段を優先して削除されています。 お客様または組織がこの方法を使用している場合は、10月のリリースのロールアウトが開始される予定の2021年10月12日までに、使用から移行する必要があります。 Munchkin ベータ版へのオプトインを希望しない場合は、[宝箱メニュー](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features)で「Marketo ランディングページでMunchkin Beta」機能を`disabled`に切り替えることで、ランディングページでの使用を無効にできます。 Munchkin Beta JavaScriptを外部web ページにデプロイし、デフォルトのMunchkin リリースチャネルに切り替える場合は、コードスニペットを更新して、munchkin-beta.jsではなくmunchkin.jsからMunchkin JavaScriptを読み込む必要があります。

投稿日：_2021-08-24_ by _Kenny_

## MUNCHKIN サービスのTLS 1.0およびTLS 1.1の提供終了

2021年10月21日以降、Munchkin JavaScriptを訪問者に提供するために使用されるmunchkin.marketo.netは、[TLS 1.0またはTLS 1.1](https://en.wikipedia.org/wiki/Transport_Layer_Security)を使用した接続を受け付けなくなります。 これらの暗号化標準は、web セキュリティのベストプラクティスの一部として受け入れられなくなり、最新のブラウザーバージョンではサポートされなくなりました。 この変更の結果、予想される悪影響はありません。

投稿日：_2021-10-04_ by _Kenny_

## 2021年10月の更新

2021年10月には、既存のREST APIを強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

* フォーム送信の一環として、プログラムメンバーのカスタムフィールドをサポートするように、[ フォーム送信](https://developer.adobe.com/marketo-apis/api/mapi/#operation/SubmitFormUsingPOST) エンドポイントを強化しました。 オプションとして、フォームを追加するプログラムとしてプログラムを指定したり、プログラムメンバーのカスタムフィールドを追加するプログラムを指定したりできます（[こちら](/help/rest-api/leads.md)を参照）。
updatedAt属性に基づく日付範囲ベースのクエリをサポートするように、[ プログラムメンバーを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getProgramMembersUsingGET) エンドポイントを強化しました。 これは、[こちら](/help/rest-api/program-members.md)で説明されているように、開始日時パラメーターと終了日時パラメーターを渡すことによって行われます。
* [ リードフィールド ](/help/rest-api/leads.md) APIが拡張され、[機密フィールド ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/mark-a-field-as-sensitive)がサポートされるようになりました。 [名前でリードフィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadFieldByNameUsingGET)、[ リードフィールドを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadFieldsUsingGET)、[ リードフィールドを作成](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createLeadFieldUsingPOST)、[ リードフィールドを更新](https://developer.adobe.com/marketo-apis/api/mapi/#operation/updateLeadFieldUsingPOST)のエンドポイントは、isSensitive属性をサポートするようになりました。

### 欠陥解決

* [ ユーザー管理](/help/rest-api/user-management.md) APIの問題を修正しました。 [Sales Insight](https://business.adobe.com/products/marketo/sales-insight.html)で使用するように設定されているMarketo ユーザーに関連します。 これらのユーザーは、[ ユーザーを取得](https://developer.adobe.com/marketo-apis/api/user/#operation/getUsersUsingGET) エンドポイントによって返されるようになりました。これらのユーザーは、[ ユーザーを削除](https://developer.adobe.com/marketo-apis/api/user/#operation/deleteUserUsingPOST) エンドポイントを使用して削除できるようになりました。[LM-155864]
* 「[ リッチテキストフィールドを追加](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/addRichTextFieldUsingPOST)」エンドポイントの問題を修正しました。 65,000文字を超えるリッチテキストフィールドをメール、ランディングページ、スニペット、またはフォームに追加すると、「611、システムエラー」が返されました。 エラー「701、操作を完了できません」が返されるようになりました。 「content」の最大長が65,535 バイトを超えています。

投稿日：_2021-10-25_ by _David_

## 2022年1月の更新

2022年1月には、既存のREST APIを強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

* ユーザーが&#x200B;**updatedAt**&#x200B;日付範囲を使用してフィルターを実行できるように、[Bulk Custom Object Extract](/help/rest-api/bulk-custom-object-extract.md) APIを強化しました。
* プログラムメンバーフィールドのメタデータを作成、更新、取得できるプログラムメンバーフィールドメタデータ APIを追加しました。 詳しくは、[ プログラムメンバー/フィールド ](/help/rest-api/program-members.md)を参照してください。
* 会社フィールドのメタデータを取得できる会社フィールドメタデータ APIを追加しました。 詳しくは、[会社/ フィールド ](/help/rest-api/companies.md)を参照してください。
* 商談フィールドのメタデータを取得できる商談フィールドメタデータ APIを追加しました。 詳しくは、[商談/フィールド ](/help/rest-api/opportunities.md)を参照してください。
* 名前付きアカウントフィールドのメタデータを取得できる名前付きアカウントフィールドメタデータ APIを追加しました。 詳しくは、[名前付きアカウント/フィールド ](/help/rest-api/named-accounts.md)を参照してください。
* フィールドがREST APIによって作成されたかどうかを示すために、新しいブール型プロパティ **isApiCreated**&#x200B;を返すようにフィールドメタデータエンドポイントを更新しました。

### 欠陥解決

* [ リードフィールドを作成](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createLeadFieldUsingPOST) エンドポイントへの呼び出し時間と、新しく作成されたリードフィールドがスマートリストで使用可能になった時間との間の待ち時間の問題を修正しました。[LM-152838]
* Marketo Engage UIの[ フォーム ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/demand-generation/forms/creating-a-form/add-a-field-to-a-form)へのフィールドの追加に使用するフォームフィールド ドロップダウンリストで、作成されたフィールドが使用できなかった[ リードフィールドを作成](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createLeadFieldUsingPOST) エンドポイントの問題を修正しました。[LM-158243]
* isTriggerable=true パラメーターが指定されたときにトリガー可能なキャンペーンが返されない[Get キャンペーン ](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCampaignsUsingGET) エンドポイントの問題を修正しました。[LM-158283]
* 特定のケースで[ リスト IDでリードを取得](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteTokenByNameUsingPOST) エンドポイントが「611、システムエラー」というエラーを返す問題を修正しました。[LM-157214]
* [ リードフィールドを更新](/help/rest-api/leads.md) エンドポイントから返された複数のエラーメッセージをクリーンアップしました。[LM-151886、LM-151888、LM-151889]

投稿日：_2022-01-27_ by _David_

## 2022年3月の更新

2022年3月には、既存のREST APIを強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

* Bulk Activity Extract APIによって生成された書き出しファイルに&#x200B;**actionResult** フィールドを追加しました。 このフィールドは、成功、スキップ、失敗したアクティビティを区別するために使用できます。
* [電子メール API](/help/rest-api/emails.md)からの応答に&#x200B;**isOpenTrackingDisabled** フィールドを追加しました。 このフィールドは、[開封トラッキングを無効にする](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-editor-v2-0-overview)機能が有効かどうかを判断するために使用できます。
* プログラムタグを選択的に管理できる2つのエンドポイントを追加しました。 [ プログラムタグの更新](/help/rest-api/programs.md) エンドポイントを使用すると、プログラムタグを選択的に更新できます。 [ プログラムタグの削除](/help/rest-api/programs.md) エンドポイントを使用すると、プログラムタグを選択的に削除できます。
* **isExecutable** パラメーターを[Clone Smart Campaign](/help/rest-api/smart-campaigns.md) エンドポイントに追加しました。 このパラメーターを使用すると、プログラムを実行可能プログラムとして複製できます。
* **headStart** フィールドを[ プログラム API](/help/rest-api/programs.md)に追加しました。 これにより、電子メールプログラムの[Head Start](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/email-programs/email-program-actions/head-start-for-email-programs)設定を作成、更新、取得できます。

### 欠陥解決

* [ メール動的コンテンツの取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailDynamicContentUsingGET) エンドポイントに関する問題を修正しました。 テンプレート関係が壊れたメールから動的コンテンツを含む件名を取得しようとすると、709、「APIはテンプレートを含むメールの操作のみを許可する」というエラーが返されました。 これで、エンドポイントは動的コンテンツを返します。[LM-152331]
* [ リードを同期](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) エンドポイントの問題を修正しました。 externalSalesPersonIdを使用して、externalSalesPersonIdを使用し、action = createDuplicateを使用してSales Personをリードに関連付ける場合、Sales Personの関連付けは発生しません。[LM-158990]

### Adobe IMSの統合

* [ ユーザー](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)にオンボーディングされたユーザーは、[Marketo Adobe IMS管理API](/help/rest-api/user-management.md)のすべてを使用することはできません。 次のエンドポイントは、ユーザーと統合されたMarketo インスタンスに対して呼び出されたときにエラーを返します：[Invite User](https://developer.adobe.com/marketo-apis/api/user/#operation/inviteUserUsingPOST)、[Get Invited User by Id](https://developer.adobe.com/marketo-apis/api/user/#operation/getInvitedUserUsingGET)、[Update User Attributes](https://developer.adobe.com/marketo-apis/api/user/#operation/updateUserAttributeUsingPOST)、[Delete User](https://developer.adobe.com/marketo-apis/api/user/#operation/deleteUserUsingPOST)、および[Delete Invited User](https://developer.adobe.com/marketo-apis/api/user/#operation/deleteInvitedUserUsingPOST)。 代わりに、[Adobe User Management API](https://developer.adobe.com/umapi/)を使用する必要があります。

投稿日：_2022-03-14_ by _David_

## 2022年5月アップデート -

2022年5月には、既存のREST APIを強化し、いくつかの欠陥を解決しています。 以下のアップデートの完全なリストを参照してください。

* [Microsoft Dynamics Sync](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync)または[SFDC Sync](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync)のいずれかがMarketo Engage インスタンスで有効になっている場合に、[企業](/help/rest-api/companies.md)、[商談](/help/rest-api/opportunities.md)、および[営業担当者](/help/rest-api/sales-persons.md)のレコードを取得する機能が追加されました。
* メールの件名から[動的コンテンツ ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/using-dynamic-content-in-an-email)を取得できるように、[ メール動的コンテンツを取得](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailDynamicContentUsingGET) エンドポイントを更新しました。 これは、指定された電子メールがメールテンプレートにリンクされているかどうかに関係なく機能します。

`POST /rest/asset/v1/form/{id}/field/State.json?values=[{"label":"Alaska"},{"value":"AK"},{"label":"West Virginia","value":"WV"},{"label":"Wyoming","value":"WY"}]`

* **isNot** タイプ [Invisibility Rules](/help/rest-api/forms.md)の複数の比較値を追加できるように、[ フォームフィールドの表示ルールを追加](https://developer.adobe.com/marketo-apis/api/asset/#operation/getAllProgramMemberFieldsUsingGET) エンドポイントを更新しました。 次に例を示します。

`POST /rest/asset/v1/form/{id}/field/LastName/visibility.json?visibilityRule={"ruleType":"show","rules":[{"subjectField":"LastName","operator":"isNot","values":["A","B","C"]}`

### 欠陥解決

* [leadFormFields](/help/rest-api/leads.md) パラメーターの属性に「null」を渡したときに発生した[送信フォーム ](/help/rest-api/leads.md) エンドポイントの問題を修正しました。エラーは「611, System Error」と返されました。 「1003、フォーム検証に失敗しました」というエラーが正しく返されるようになりました。[LM-162213]

投稿日：_2022-05-09_ by _David_

## 2022年8月の更新

2022年8月には、既存のREST APIを強化する予定です。 以下のアップデートの完全なリストを参照してください。

プログラム メンバーの作成ジョブ エンドポイントを呼び出す際に使用できる、複数の新しいフィルターを追加しました。 多くのフィルターは、抽出したデータセットを調整するために互いに組み合わせて使用できます。

* **programIds** フィルターを使用して、最大10個のプログラム IDを指定できます。これは、スループットの向上に役立ちます。
* **isExhausted** フィルターを使用すると、コンテンツを使い果たした[人のレコードをフィルタリングできます](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/email-marketing/drip-nurturing/using-engagement-programs/people-who-have-exhausted-content)。
* **nurtureCadence** フィルターを使用して、[ エンゲージメントプログラムのケイデンス ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/program-flow-actions/change-engagement-program-cadence)に基づいてレコードをフィルタリングできます。
* **statusNames** フィルターを使用して、1つ以上の[ プログラムステータス ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/creating-programs/understanding-program-membership)のレコードをフィルタリングできます。
* **updatedAt** フィルターを使用して、日付範囲に基づいてレコードをフィルタリングできます。

### お知らせ

* [ID](https://developer.adobe.com/marketo-apis/api/identity/#operation/identityUsingGET) エンドポイントの動作が変更されました。 エンドポイントを呼び出し、**access_token** パラメーターを含まない場合、「603, Access denied」エラーが返されます。 以前は、「600, Empty access token」エラーが返されていました。 「600, Empty access token」エラーは廃止されました。

投稿日：_2022-09-03_ by _David_

## 2022年10月アップデート

2022年10月には、既存のREST APIを強化します。 以下のアップデートの完全なリストを参照してください。

* インポートプロセス中に営業担当者レコードにリードを追加できるように、[一括リード読み込みAPI](/help/rest-api/bulk-lead-import.md)を強化しました。 これは、インポートファイルに&#x200B;**externalSalesPersonId** フィールドを含めることで行われます。
* スコアタイプフィールドの作成時に発生した[ リードフィールドの作成](/help/rest-api/leads.md) エンドポイントの問題を修正しました。 これらのフィールドは、Marketo Engage UIの[ スコアの変更](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/change-score) フローアクションで使用できませんでした。[LM-166815]

### お知らせ

* プログラムメンバーシップ属性`acquiredBy`が更新可能に変更されました。

投稿日：_2022-10-18_ by _David_

## Marketo Forms REST APの今後の変更点

現在2023年3月24日の週に予定されている2022.R2 リリース以降、Adobe Marketo Engage Forms Asset APIは、フォームがプログラムの子であるかどうかに関係なく、接頭辞のないプログラム名なしでフォームの名前のみを返します。 この変更により、アセット名に関するForms APIの動作が、他のAdobe Marketo Engage Asset APIと一致するようになります。 サービスの中断を回避するには、Marketo Engage Forms APIを使用する統合を確認し、インテグレーターと連携して、これに対応するために必要な変更があるかどうかを確認する必要があります。この変更の前に、Forms APIによって返される名前に、マーケティングアクティビティのプログラムの子であるフォームのプログラム名の先頭に一貫性がない名前が付けられていました。 例えば、「Form 1」という名前のフォームは、「Program 1」の子でした。その名前は、APIによって次のように返される場合があります。Program 1.Form 1またはForm 1 2022.R2 リリース以降、フォームの名前は常に接頭辞を付けたプログラム名なしで返されます。 同じ例を使用すると、名前は常にフォーム 1になります。

投稿日：_2022-11-04_ by _Kenny_

## 2023年1月の更新

2023年1月、Admin UIにAPI関連の機能強化を行い、2つの発表を行っています。 以下のアップデートの完全なリストを参照してください。

管理者UI

### リードの一括抽出

* Marketo Engage管理UIが強化され、サブスクリプションのBulk Extract APIの日次キャパシティ割り当てを表示できるようになりました。 さらに、過去7日間のAPI-Userによるキャパシティ使用状況を表示できます。 詳しくは[こちら](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/settings/bulk-export-api-information)をご覧ください。

### 欠陥解決

* [商談を削除](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteOpportunitiesUsingPOST) エンドポイントの問題を修正しました。 場合によっては、「商談から削除」アクティビティが生成されていませんでした。[LM-172208]

### お知らせ

* REST APIおよびHTTP レスポンス メッセージ [理由フレーズ ](https://www.rfc-editor.org/rfc/rfc7230#section-3.1.2)の変更については、Marketo Communityの[この記事](https://nation.marketo.com/t5/product-documents/upcoming-change-to-marketo-rest-api/ta-p/331698)を参照してください。
* プログラムメンバーシップ属性&#x200B;**statusReason**&#x200B;が更新可能に変更されました。

投稿日：_2023-01-21_ by _David_
