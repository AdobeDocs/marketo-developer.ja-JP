---
title: syncMObjects
feature: SOAP
description: syncMObjects SOAP呼び出し
exl-id: 68bb69ce-aa8c-40b7-8938-247f4fe97b5d
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 7%

---

# syncMObjects

1 回の呼び出しで最大 100 まで作成または更新される [MObjects](marketo-objects.md) の配列を受け入れて、操作の結果（ステータス） （CREATED、UPDATED、FAILED、UNCHANGED、SKIPPED）および MObject のMarketo ID を返します。 この API は、次の 3 つの操作モードのいずれかで呼び出すことができます。

1. INSERT – 新しいオブジェクトのみを挿入し、既存のオブジェクトはスキップします
1. UPDATE：既存のオブジェクトのみを更新し、新しいオブジェクトはスキップします。
   - プログラム MObject の場合、API は、更新モードでのみ呼び出して、新しい期間のコスト情報を追加するか、既存のプログラムのタグ/チャネルを追加/更新できます。 （タグ/チャネルが既に定義されている必要があります。API から新しいタグ/チャネルを作成することはできません）
1. アップサート – 新しいオブジェクトを挿入し、既存のオブジェクトを更新します

UPDATE 操作と UPSERT 操作では、ID をキーとして使用します。 1 回の API 呼び出しで、一部の更新が成功し、一部が失敗する可能性があります。 失敗するたびにエラーメッセージが返されます

## リクエスト

| フィールド名 | 必須／オプション | 説明 |
| --- | --- | --- |
| mObjectList->mObject->type | 必須 | `Program`、`Opportunity`、`OpportunityPersonRole` のいずれかを指定できます。 |
| mObjectList->mObject->id | 必須 | オブジェクトの ID。 1 回の呼び出しで最大 100 個の MObjects を指定できます。 |
| mObjectList->mObject->typeAttribList->typeAttrib->attrType | 必須 | コスト （プログラム MObject の更新時にのみ使用）は、`Cost`、`Tag` のいずれかです。 |
| mObjectList->mObject->typeAttribList->typeAttrib->attrList->attrib->name | 必須 | プログラム MObject の場合、次の属性を名前と値のペアとして渡すことができます。 コスト：`Month (Required)`、`Amount (Required)`、`Id (Cost Id - Optional)`、`Note (Optional)` タグ/チャネル：`Type (Required)`、`Value (Required)` 商談 MObject の場合、[describeMObject](describemobject.md) の出力のすべてのフィールドは、名前と値のペアとして渡すことができます。 以下のリストは、すべてのオプションフィールドと属性の標準セットです。 Opportunity MObject には、サポート・リクエストを通じて作成された追加のフィールドを含めることができます。 |

1. 金額
1. CloseDate
1. 説明
1. ExpectedRevenue
1. ExternalCreatedDate
1. 会計
1. FiscalQuarter
1. FiscalYear
1. ForecastCategoryName
1. IsClosed
1. IsWon
1. LastActivityDate
1. LeadSource
1. 名前
1. NextStep
1. 可能性
1. 数
1. ステージ
1. タイプ

OpportunityPersonRole MObject の場合、[describeMObject](./describemobject.md) の出力からすべてのフィールドを名前と値のペアとして指定できます。 OpportunityPersonRole MObject の属性の標準セットは、次のとおりです。

1. OpportunityId （必須）
1. ユーザー Id （必須）
   1. Marketoの人物/連絡先 ID に対応します。
1. 役割（オプション）
1. ExternalCreatedDate （オプション）
1. IsPrimary （オプション）
1. 役割（オプション）

|
| mObjAssociationList->mObjAssociation->mObjType | オプション |関連するオブジェクトの ID または外部キーを使用して、Opportunity/OpportunityPersonRole MObjects を更新するために使用されます。 関連するオブジェクトは、会社（Opportunity MObject を更新する）、リード（OpportunityPersonRole MObject を更新する）、商談（OpportunityPersonRole MObject を更新する）|のいずれかです。
| mObjAssociationList->mObjAssociation->id | オプション |関連付けられたオブジェクトの ID （リード/会社/オポチュニティ） |
| mObjAssociationList->mObjAssociation->externalKey | オプション |関連オブジェクトのカスタム属性 |

## XML をリクエスト

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809934544BFABAE58E5D27</mktowsUserId>
      <requestSignature>40e6d89bd2f7f0daaddaf150ce7a7ca49788ffe7</requestSignature>
      <requestTimestamp>2013-08-05T14:22:45-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsSyncMObjects>
      <mObjectList>
        <mObject>
          <type>Program</type>
          <id>1970</id>
          <typeAttribList>
            <typeAttrib>
              <attrType>Cost</attrType>
              <attrList>
                <attrib>
                  <name>Month</name>
                  <value>2013-06</value>
                </attrib>
                <attrib>
                  <name>Amount</name>
                  <value>2000</value>
                </attrib>
                <attrib>
                  <name>Id</name>
                  <value>153</value>
                </attrib>
              </attrList>
            </typeAttrib>
          </typeAttribList>
        </mObject>
      </mObjectList>
      <operation>UPDATE</operation>
    </ns1:paramsSyncMObjects>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 応答 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successSyncMObjects>
      <result>
        <mObjStatusList>
          <mObjStatus>
            <id>1970</id>
            <status>UPDATED</status>
          </mObjStatus>
        </mObjStatusList>
      </result>
    </ns1:successSyncMObjects>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## サンプルコード - PHP

```php
<?php
$debug = true;
$marketoSoapEndPoint    = "";  // CHANGE ME
$marketoUserId      = ""; // CHANGE ME
$marketoSecretKey   = ""; // CHANGE ME
$marketoNameSpace   = "http://www.marketo.com/mktows/";
 
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
$options = array("connection_timeout" => 15, "location" => $marketoSoapEndPoint);
if ($debug) {
  $options["trace"] = 1;
}
 
// Create Request
////////////////////////////////
$params = prepareUpdateProgramRequest();
// -or- 
//$params = prepareCreateOpptyRequest();
// -or-
//$params= prepareCreateOpptyPersonRoleRequest();
////////////////////////////////
            
$soapClient = new SoapClient($marketoSoapEndPoint ."?WSDL", $options);
try {
  $leads = $soapClient->__soapCall('syncMObjects', array($params), $options, $authHdr);
}
catch(Exception $ex) {
  var_dump($ex);
}

if ($debug) {
  print "RAW request:\n" .$soapClient->__getLastRequest() ."\n";
  print "RAW response:\n" .$soapClient->__getLastResponse() ."\n";
}

function prepareUpdateProgramRequest() {
  $params = new stdClass();

  $mObj = new stdClass();
  $mObj->type = 'Program';
  $mObj->id="1970";

  $attrib1 = new stdClass();
  $attrib1->name="Month";
  $attrib1->value="2013-06";
        
  $attrib2 = new stdClass();
  $attrib2->name="Amount";
  $attrib2->value="2000";
        
  $attrib3 = new stdClass();
  $attrib3->name="Id";
  $attrib3->value="153";
  $attribList = array ($attrib1, $attrib2, $attrib3);
        
  $costAttrib = new stdClass();
  $costAttrib->attrType="Cost";
  $costAttrib->attrList = $attribList;

  $mObj->typeAttribList= array($costAttrib);
  $params->mObjectList = array($mObj);

  $params->operation="UPDATE";

  return $params;
}

function prepareCreateOpptyRequest() {
  $params = new stdClass();

  $mObj = new stdClass();
  $mObj->type = 'Opportunity';

  $attrib1 = new stdClass();
  $attrib1->name="Name";
  $attrib1->value="Q1 2014";
        
  $attrib2 = new stdClass();
  $attrib2->name="Amount";
  $attrib2->value="2000";
        
  $attrib3 = new stdClass();
  $attrib3->name="Probability";
  $attrib3->value="80%";
  $attribs = array ($attrib1, $attrib2, $attrib3);

  $attribList = new stdClass();
  $attribList->attrib = $attribs;

  $mObj->attribList = $attribList;
  $params->mObjectList = array($mObj);

  $params->operation="INSERT";
  
  return $params;
}

function prepareCreateOpptyPersonRoleRequest() {
  $params = new stdClass();

  $mObj = new stdClass();
  $mObj->type = 'OpportunityPersonRole';

  $attrib1 = new stdClass();
  $attrib1->name="OpportunityId";
  $attrib1->value="64";
        
  $attrib2 = new stdClass();
  $attrib2->name="PersonId";
  $attrib2->value="19";
        
  $attrib3 = new stdClass();
  $attrib3->name="Role";
  $attrib3->value="Influencer/Champion";
  $attribs = array ($attrib1, $attrib2, $attrib3);

  $attribList = new stdClass();
  $attribList->attrib = $attribs;

  $mObj->attribList = $attribList;
  $params->mObjectList = array($mObj);

  $params->operation="INSERT";
  return $params;
}
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
import javax.xml.bind.Marshaller;
 
 
public class SyncMObjects {
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
            ////////////////////////////////
            ParamsSyncMObjects request = prepareUpdateProgramRequest();
            // -or- 
            //ParamsSyncMObjects request = prepareCreateOpptyRequest();
            // -or-
            //ParamsSyncMObjects request = prepareCreateOpptyPersonRoleRequest();
            ////////////////////////////////
             
            SuccessSyncMObjects result = port.syncMObjects(request, header);
            
            JAXBContext context = JAXBContext.newInstance(SuccessSyncMObjects.class);
            Marshaller m = context.createMarshaller();
            m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
            m.marshal(result, System.out);
            
        }
        catch (Exception e) {
            e.printStackTrace();
        }
    }
    
    private static ParamsSyncMObjects prepareUpdateProgramRequest() {
        ParamsSyncMObjects request = new ParamsSyncMObjects();
        request.setOperation(SyncOperationEnum.UPDATE);

        MObject mobj = new MObject();
        mobj.setType("Program");
        mobj.setId(1970);
        
        TypeAttrib typeAttrib = new TypeAttrib();
        typeAttrib.setAttrType("Cost");
        
        Attrib attrib = new Attrib();
        attrib.setName("Month");
        attrib.setValue("2013-06");
        
        Attrib attrib2 = new Attrib();
        attrib1.setName("Amount");
        attrib1.setValue("2000");
        
        Attrib attrib3 = new Attrib();
        attrib1.setName("Id");
        attrib1.setValue("153");
        
        ArrayOfAttrib attribList = new ArrayOfAttrib();
        attribList.getAttribs().add(attrib);
        attribList.getAttribs().add(attrib2);
        attribList.getAttribs().add(attrib3);
        typeAttrib.setAttrList(attribList);
        
        ArrayOfTypeAttrib typeAttribList = new ArrayOfTypeAttrib();
        typeAttribList.getTypeAttribs().add(typeAttrib);
        mobj.setTypeAttribList(typeAttribList);
        
        ArrayOfMObject objList = new ArrayOfMObject();
        objList.getMObjects().add(mobj);
        request.setMObjectList(objList);
        
        return request;
    }

    private static ParamsSyncMObjects prepareCreateOpptyRequest() {
        ParamsSyncMObjects request = new ParamsSyncMObjects();
        request.setOperation(SyncOperationEnum.INSERT);
        
        MObject mobj = new MObject();
        mobj.setType("Opportunity");
        
        Attrib attrib = new Attrib();
        attrib.setName("Name");
        attrib.setValue("Q1 2014");

        Attrib attrib2 = new Attrib();        
        attrib1.setName("Amount");
        attrib1.setValue("2000");
        
        Attrib attrib3 = new Attrib();
        attrib1.setName("Probability");
        attrib1.setValue("80%");
        
        ArrayOfAttrib attribList = new ArrayOfAttrib();
        attribList.getAttribs().add(attrib);
        attribList.getAttribs().add(attrib2);
        attribList.getAttribs().add(attrib3);
        mobj.setAttribList(attribList);
        
        ArrayOfMObject objList = new ArrayOfMObject();
        objList.getMObjects().add(mobj);
        request.setMObjectList(objList);
        
        return request;
    }
    private static ParamsSyncMObjects prepareCreateOpptyPersonRoleRequest() {
        ParamsSyncMObjects request = new ParamsSyncMObjects();
        request.setOperation(SyncOperationEnum.INSERT);
        
        MObject mobj = new MObject();
        mobj.setType("OpportunityPersonRole");
        
        Attrib attrib = new Attrib();
        attrib.setName("OpportunityId");
        attrib.setValue("64"); // Id of the opportunity created earlier
        
        Attrib attrib2 = new Attrib();
        attrib1.setName("PersonId");
        attrib1.setValue("19");
        
        Attrib attrib3 = new Attrib();
        attrib1.setName("Role");
        attrib1.setValue("Influencer/Champion");
        
        ArrayOfAttrib attribList = new ArrayOfAttrib();
        attribList.getAttribs().add(attrib);
        attribList.getAttribs().add(attrib2);
        attribList.getAttribs().add(attrib3);
        mobj.setAttribList(attribList);
        
        ArrayOfMObject objList = new ArrayOfMObject();
        objList.getMObjects().add(mobj);
        request.setMObjectList(objList);
        
        return request;
    }
            
}
```

## サンプルコード - Ruby

```ruby
require 'savon' # Use version 1.0 Savon gem
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
    'ns1:AuthenticationHeader' => { "mktowsUserId" => mktowsUserId, "requestSignature" => requestSignature,                     
    "requestTimestamp"  => requestTimestamp 
    }
}

client = Savon.client(wsdl: 'http://app.marketo.com/soap/mktows/2_3?WSDL', soap_header: headers, endpoint: marketoSoapEndPoint, open_timeout: 90, read_timeout: 90, namespace_identifier: :ns1, env_namespace: 'SOAP-ENV')

#Create Request
request = {
    :m_object_list => {
          :m_object => {
              :type => "Program",
              :id => "1970",
              :type_attrib_list => {
                  :type_attrib => {
                      :attr_type => "Cost",
                      :attr_list => {
                          :attrib => {
                              :name => "Month",
                              :value => "2013-06" },
                        :attrib! => {
                              :name => "Amount",
                              :value =>  "2000" },
                        :attrib! => {
                              :name => "Id",
                              :value => "153" }
                    }
                }
            }
        }
    },
      :operation => "UPDATE"
}

response = client.call(:sync_m_objects, message: request)

puts response
```
