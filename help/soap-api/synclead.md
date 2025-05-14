---
title: syncLead
feature: SOAP
description: syncLead SOAP 呼び出し
exl-id: e6cda794-a9d4-4153-a5f3-52e97a506807
source-git-commit: ebe8faf41dff0e0ba5f4323f5909cc3c9813fd10
workflow-type: ht
source-wordcount: '518'
ht-degree: 100%

---

# syncLead

この関数は、単一のリードレコードを挿入または更新します。既存のリードを更新する場合、リードは次のいずれかのキーで識別されます。

- Marketo ID
- 外部システム ID（`foreignSysPersonId` として実装）
- Marketo cookie（Munchkin JS スクリプトで作成）
- メール

既存の一致が見つかった場合、呼び出しは更新を実行します。見つからない場合は、リードを挿入して作成します。匿名のリードは、Marketo cookie ID を使用して更新でき、更新時に認識されます。

メールを除き、これらの識別子はすべて一意のキーとして処理されます。Marketo ID は、他のすべてのキーよりも優先されます。リードレコードに `foreignSysPersonId` と Marketo ID の両方が存在する場合、Marketo ID が優先され、そのリードの `foreignSysPersonId` が更新されます。`foreignSysPersonId` のみが指定された場合は、一意の ID として使用されます。`foreignSysPersonId` とメールの両方が存在するが、Marketo ID が存在しない場合は、`foreignSysPersonId` が優先され、そのリードのメールが更新されます。

オプションで、コンテキストヘッダーを指定して、ターゲットワークスペースに名前を付けることができます。

Marketo ワークスペースが有効で、ヘッダーが使用されている場合、次のルールが適用されます。

- 割り当てルールが設定され、新しいリードが、設定されたルールのいずれかに該当する場合、割り当てルールによって定義されたパーティションに新しいリードが作成されます。それ以外の場合、新しいリードは名前付きワークスペースのプライマリパーティションに作成されます。
- Marketo リード ID、外部システム ID、または Marketo cookie に一致するリードは、指定されたワークスペースのプライマリパーティションに存在する必要があります。存在しない場合はエラーが返されます
- 既存のリードがメールで一致した場合、指定されたワークスペースは無視され、リードは現在のパーティションで更新されます

Marketo ワークスペースが有効で、ヘッダーが使用されていない場合、次のルールが適用されます。

- 割り当てルールが設定され、新しいリードが、設定されたルールのいずれかに該当する場合、割り当てルールによって定義されたパーティションに新しいリードが作成されます。それ以外の場合、新しいリードは「デフォルト」ワークスペースのプライマリパーティションに作成されます。
- 既存のリードは、現在のパーティションで更新されます

Marketo ワークスペースが有効になっていない場合、ターゲットワークスペースを「デフォルト」ワークスペースにする必要があります。ヘッダーを渡す必要はありません。

## リクエスト

| フィールド名 | 必須／オプション | 説明 |
| --- | --- | --- |
| leadRecord／Id | 必須 - メールまたは `foreignSysPersonId` が存在しない場合のみ | リードレコードの Marketo ID |
| leadRecord／Email | 必須 - ID または `foreignSysPersonId` が存在しない場合のみ | リードレコードに関連付けられたメールアドレス |
| leadRecord／`foreignSysPersonId` | 必須 - ID またはメールが存在しない場合のみ | リードレコードに関連付けられた外部システム ID |
| leadRecord／foreignSysType | オプション - `foreignSysPersonId` が存在する場合のみ必須 | 外部システムのタイプ。使用可能な値：CUSTOM、SFDC、NETSUITE |
| leadRecord／leadAttributeList／attribute／attrName | 必須 | 値を更新するリード属性の名前。 |
| leadRecord／leadAttributeList／attribute／attrValue | 必須 | attrName で指定されたリード属性に設定する値。 |
| returnLead | 必須 | true の場合、更新時に更新された完全なリードレコードを返します。 |
| marketoCookie | オプション | [Munchkin JavaScript](../javascript-api/lead-tracking.md) cookie |

## リクエスト XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
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
        <Email>t@t.com</Email>
        <leadAttributeList>
          <attribute>
            <attrName>FirstName</attrName>
            <attrValue>George</attrValue>
          </attribute>
          <attribute>
            <attrName>LastName</attrName>
            <attrValue>of the Jungle</attrValue>
          </attribute>
        </leadAttributeList>
      </leadRecord>
      <returnLead>false</returnLead>
    </ns1:paramsSyncLead>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 応答 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successSyncLead>
      <result>
        <leadId>1089965</leadId>
        <syncStatus>
          <leadId>1089965</leadId>
          <status>UPDATED</status>
          <error xsi:nil="true" />
        </syncStatus>
        <leadRecord xsi:nil="true" />
      </result>
    </ns1:successSyncLead>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## サンプルコード - PHP

```php
 <?php
 
  $debug = true;
 
  $marketoSoapEndPoint     = "";  // CHANGE ME
  $marketoUserId           = "";  // CHANGE ME
  $marketoSecretKey        = "";  // CHANGE ME
  $marketoNameSpace        = "http://www.marketo.com/mktows/";
 
  // Create Signature
  $dtzObj = new DateTimeZone("America/Los_Angeles");
  $dtObj  = new DateTime('now', $dtzObj);
  $timeStamp = $dtObj->format(DATE_W3C);
  $encryptString = $timeStamp . $marketoUserId;
  $signature = hash_hmac('sha1', $encryptString, $marketoSecretKey);
 
  // Create SOAP Header
  $attrs = new stdClass();
  $attrs->mktowsUserId = $marketoUserId;
  $attrs->requestSignature = $signature;
  $attrs->requestTimestamp = $timeStamp;
  $authHdr = new SoapHeader($marketoNameSpace, 'AuthenticationHeader', $attrs);
  $options = array("connection_timeout" =20, "location" =$marketoSoapEndPoint);
  if ($debug) {
    $options["trace"] = true;
  }
 
  // Create Request
  $leadKey = new stdClass();
  $leadKey->Email = "george@jungle.com";
 
  // Lead attributes to update
  $attr1 = new stdClass();
  $attr1->attrName  = "FirstName";
  $attr1->attrValue = "George";
 
  $attr2= new stdClass();
  $attr2->attrName  = "LastName";
  $attr2->attrValue = "of the Jungle";
 
  $attrArray = array($attr1, $attr2);
  $attrList = new stdClass();
  $attrList->attribute = $attrArray;
  $leadKey->leadAttributeList = $attrList;
 
  $leadRecord = new stdClass();
  $leadRecord->leadRecord = $leadKey;
  $leadRecord->returnLead = false;
  $params = array("paramsSyncLead" =$leadRecord);
 
  $soapClient = new SoapClient($marketoSoapEndPoint ."?WSDL", $options);
  try {
    $result = $soapClient->__soapCall('syncLead', $params, $options, $authHdr);
  }
  catch(Exception $ex) {
    var_dump($ex);
  }
 
  if ($debug) {
    print "RAW request:\n" .$soapClient->__getLastRequest() ."\n";
    print "RAW response:\n" .$soapClient->__getLastResponse() ."\n";
  }
  print_r($result);
 
?>
```

## サンプルコード - Java

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
 
 
public class SyncLead {
 
    public static void main(String[] args) {
        System.out.println("Executing syncLead");
        try {
            URL marketoSoapEndPoint = new URL("https://100-AEK-913.mktoapi.com/soap/mktows/2_1" + "?WSDL");
            String marketoUserId = "demo17_1_809934544BFABAE58E5D27";
            String marketoSecretKey = "27272727aa";
             
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
            ParamsSyncLead request = new ParamsSyncLead();
            LeadRecord key = new LeadRecord();
             
            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Stringemail = objectFactory.createLeadRecordEmail("george@jungle.com");
            key.setEmail(email);
            request.setLeadRecord(key);
             
            Attribute attr1 = new Attribute();
            attr1.setAttrName("FirstName");
            attr1.setAttrValue("George2");
             
            Attribute attr2 = new Attribute();
            attr2.setAttrName("LastName");
            attr2.setAttrValue("of the Jungle");
             
            ArrayOfAttribute aoa = new ArrayOfAttribute();
            aoa.getAttributes().add(attr1);
            aoa.getAttributes().add(attr2);
             
            QName qname = new QName("http://www.marketo.com/mktows/", "leadAttributeList");
            JAXBElement<ArrayOfAttributeattrList = new JAXBElement(qname, ArrayOfAttribute.class, aoa);         
            key.setLeadAttributeList(attrList);
             
            MktowsContextHeader headerContext = new MktowsContextHeader();
            headerContext.setTargetWorkspace("default");
             
            SuccessSyncLead result = port.syncLead(request, header, headerContext);
 
            JAXBContext context = JAXBContext.newInstance(SuccessSyncLead.class);
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

## サンプルコード - Ruby

```ruby
require 'savon' # Use version 2.0 Savon gem
require 'date'

mktowsUserId = "" # CHANGE ME
marketoSecretKey = "" # CHANGE ME
marketoSoapEndPoint = "" # CHANGE ME
marketoNameSpace = "http://www.marketo.com/mktows/"

#Create Signature
Timestamp = DateTime.now
requestTimestamp = Timestamp.to_s
encryptString = requestTimestamp + mktowsUserId
digest = OpenSSL::Digest.new('sha1')
hashedsignature = OpenSSL::HMAC.hexdigest(digest, marketoSecretKey, encryptString)
requestSignature = hashedsignature.to_s

#Create SOAP Header
headers = { 
    'ns1:AuthenticationHeader' ={ "mktowsUserId" =mktowsUserId, "requestSignature" =requestSignature, 
    "requestTimestamp"  =requestTimestamp 
    }
}

client = Savon.client(wsdl: 'http://app.marketo.com/soap/mktows/2_3?WSDL', soap_header: headers, endpoint: marketoSoapEndPoint, open_timeout: 90, read_timeout: 90, namespace_identifier: :ns1, env_namespace: 'SOAP-ENV')

#Create Request
request = {
    :lead_record ={
        :Email ="t@t.com",
          :lead_attribute_list ={
              :attribute ={
                :attr_name ="FirstName",
                :attr_value ="George" },
              :attribute! ={
                :attr_name ="LastName",
                :attr_value ="of the Jungle" }
        }
    },
    :return_lead ="false"
}

response = client.call(:sync_lead, message: request)

puts response
```
