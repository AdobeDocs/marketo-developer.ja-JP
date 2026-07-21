---
title: トランザクションメール
feature: REST API
description: トランザクションメール用にMarketoを設定し、REST API Request Campaignを介してトリガーする方法（設定手順とJava コード例を含む）を説明します。
exl-id: 057bc342-53f3-4624-a3c0-ae619e0c81a5
TQID: https://experienceleague.adobe.com/eUw2THnwDdIuEO3MsuG4cSaoPnKVvdZ0ZTV-gxP-pJQ
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 897
ht-degree: 52%

---

# トランザクションメール

[Request Campaign](https://developer.adobe.com/marketo-apis/api/mapi#tag/Campaigns/operation/triggerCampaignUsingPOST) APIを使用して、特定のMarketo レコードにトランザクションメールを送信します。 リクエストを行う前に、メールとトリガーキャンペーンを設定します。

- 受信者がMarketo レコードを持っていることを確認します。
- Marketo インスタンスでトランザクションメールを作成して承認します。
- 「Campaign is Requested, 1.」を使用するトリガーキャンペーンをアクティブ化します。 Source: Web Service API」を呼び出し、メールを送信します。

最初に、[電子メールを作成して承認](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ja)します。 電子メールが正式に運用可能と認定された場合は、電子メールアクション/電子メール設定で運用可能として設定します。

![リクエスト-キャンペーンのメール-設定](assets/request-campaign-email-settings.png)

![リクエスト-キャンペーン-運用](assets/request-campaign-operational.png)

キャンペーンを作成する前にメールを承認します。

![リクエストキャンペーン-承認-ドラフト](assets/request-campaign-approve-draft.png)

必要に応じて、[新しいスマートキャンペーンの作成](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/creating-a-smart-campaign/create-a-new-smart-campaign.html?lang=ja)を参照してください。 キャンペーンのスマートリストを「キャンペーンはリクエスト済み」トリガーで設定します。

![リクエスト-キャンペーン-スマート-リスト](assets/request-campaign-smart-list.png)

トランザクションメールを参照するメール送信フローステップを設定します。

![リクエスト-キャンペーン-フロー](assets/request-campaign-flow.png)

アクティベーションの前に、「スケジュール」タブで資格設定を設定します。 各レコードが1回だけ電子メールを受信する必要がある場合は、デフォルト設定を維持します。 そうでない場合は、受信者が毎回または利用可能な頻度でクオリフィケーションを行えるようにします。

キャンペーンをアクティブ化します。

![リクエスト-キャンペーン-スケジュール](assets/request-campaign-schedule.png)

## API 呼び出しの送信

Javaの例では、[minimal-json パッケージ ](https://github.com/ralfstx/minimal-json)を使用してJSON表現を処理します。

メールを送信する前に、メールアドレスにMarketo レコードが存在することを確認し、そのリード IDを取得します。 この例では、メールアドレスが既に存在することを前提としています。

フィルターの種類](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/getLeadsByFilterUsingGET)で[ リードを取得を使用して、IDを取得します。 次のメインメソッドは、キャンペーンをリクエストします。

```java
package dev.marketo.blog_request_campaign;

import com.eclipsesource.json.JsonArray;

public class App
{
    public static void main( String[] args )
    {
        //Create an instance of Auth so that we can authenticate with our Marketo instance
        Leads leadsRequest = new Leads(auth).setFilterType("email").addFilterValue("requestCampaign.test@marketo.com");

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

`JsonObject`応答から結果配列を抽出し、インデックス 0のオブジェクトを取得します。

```java
JsonArray leadsResult = leadsRequest.getData().get("result").asArray();
int leadId = leadsResult.get(0).asObject().get("id").asInt();
```

リクエスト URLにキャンペーン IDを含むコールリクエストキャンペーン。 リクエスト本文には、`id` メンバーを持つJSON オブジェクトの配列が含まれています。

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
            System.out.println("Executing RequestCampaign call\n" + "Endpoint: " + endpoint + "\nRequest Body:\n"  + requestBody);
            URL url = new URL(endpoint);
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
            System.out.println("Result:\n" + result);
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

このクラスには、Auth とキャンペーンの ID を受け取る 1 つのコンストラクターがあります。 レコードの ID を含む `ArrayList<Integer>` を setLeads に渡すか、1 つの整数を受け取り、leads プロパティの既存の ArrayList に追加する addLead を使用することによって、リードがオブジェクトに追加されます。 API 呼び出しをトリガーしてリードレコードをキャンペーンに渡すには、リクエストからの応答データを含む JsonObject を返す postData を呼び出す必要があります。 リクエストキャンペーンを呼び出すと、呼び出しに渡されたすべてのリードが Marketo のターゲットトリガーキャンペーンによって処理され、以前に作成したメールが送信されます。 これで、Marketo REST APIを通じてメールがトリガーされました。 パート 2 では、リクエストキャンペーンを通じてメールのコンテンツを動的にカスタマイズする方法について説明します。

### メールの作成

コンテンツをカスタマイズするには、最初に Marketo で[プログラム](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/programs/creating-programs/create-a-program.html?lang=ja)と[メール](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ja)を設定する必要があります。 カスタムコンテンツを生成するには、プログラム内でトークンを作成し、送信するメールに配置する必要があります。 簡単にするために、この例では 1 つのトークンのみを使用していますが、メール内、送信元メール、送信者名、返信先、またはメール内の任意のコンテンツで、任意の数のトークンを置き換えることができます。 ここで、置換用のトークンリッチテキストを 1 つ作成し、「bodyReplacement」という名前を付けます。 リッチテキストを使用すると、トークン内の任意のコンテンツを、入力する任意の HTML に置き換えることができます。

![新規トークン](assets/New-Token.png)

空の間はトークンを保存できないので、ここにプレースホルダーテキストを挿入してください。 次に、メールにトークンを挿入する必要があります。

![トークンを追加](assets/Add-Token.png)

このトークンにアクセスして、リクエストキャンペーン呼び出しを通じて置き換えることができます。 このトークンは、メールごとに置き換える必要がある 1 行のテキストとしてシンプルにすることも、メールのレイアウトのほとんど全体を含めることもできます。

### コード

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
        String bodyReplacement = "<div class=\"replacedContent\"><p>This content has been replaced</p></div>";
        rc.addToken("{{my.bodyReplacement}}", bodyReplacement);
        rc.postData();
    }
}
```

コードが使い慣れているように見える場合は、上記のメインメソッドから2行しか追加されていないためです。 今回は、bodyReplacement変数でトークンのコンテンツを作成し、addToken メソッドを使用してリクエストに追加します。 addToken はキーと値を受け取り、JsonObject 表現を作成して、内部の tokens 配列に追加します。 その後、これが postData メソッド中にシリアル化され、次のような本文が作成されます。

```json
{
    "input":
    {
        "leads": [
            {
                "id": 1
            }
        ],
        "tokens": [
            {
                "name": "{{my.bodyReplacement}}",
                "value": "<div class=\"replacedContent\"><p>This content has been replaced</p></div>"
            }
        ]
    }
}
```

組み合わせると、コンソール出力は次のようになります。

```bash
Token is empty or expired. Trying new authentication
Trying to authenticate with ...
Got Authentication Response: {"access_token":"19d51b9a-ff60-4222-bbd5-be8b206f1d40:st","token_type":"bearer","expires_in":3565,"scope":"apiuser@mktosupport.com"}
Executing RequestCampaign call
Endpoint: .../rest/v1/campaigns/1578/trigger.json
Request Body:
{"input":{"leads":[{"id":1}],"tokens":[{"name":"{{my.bodyReplacement}}","value":"<div class=\"replacedContent\"><p>This content has been replaced</p></div>"}]}}
Result:
{"requestId":"1e8d#14eadc5143d","result":[{"id":1578}],"success":true}
```

## まとめ

この方法は、様々な方法で拡張可能で、個々のレイアウトセクション内またはメール外部のメールのコンテンツを変更し、カスタム値をタスクや注目のアクションに渡すことができます。 プログラム内からトークンを使用できる場所はすべて、この方法を使用してカスタマイズできます。 また、同様の機能は、[キャンペーンをスケジュール](https://developer.adobe.com/marketo-apis/api/mapi#tag/Campaigns/operation/scheduleCampaignUsingPOST)呼び出しでも使用でき、バッチキャンペーン全体をまたいでトークンを処理できます。 これらはリードごとにカスタマイズすることはできませんが、幅広いリードを対象にコンテンツをカスタマイズするのに役立ちます。
