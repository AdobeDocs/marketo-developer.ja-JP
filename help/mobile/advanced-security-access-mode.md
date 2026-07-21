---
title: 高度なセキュリティアクセスモード
feature: Mobile Marketing
description: HMAC署名の生成、サーバーエンドポイントの設定、デバイス IDの使用、iOSおよびAndroidの例を含む、Marketo Mobile SDKの高度なセキュリティアクセスモードについて説明します
exl-id: bd4730ff-708b-465e-b494-485a4dbf67ff
TQID: https://experienceleague.adobe.com/F6lH1aGbCakK-E6IU4wLwYw58BG2-CRE-Ras2bMHeO8
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 217
ht-degree: 7%

---

# 高度なセキュリティアクセスモード

高度なセキュリティアクセスモードでは、セキュリティ署名を取得して設定するためにMarketo SDKが必要です。 SDKには、署名を設定および削除する方法と、デバイス IDを取得するユーティリティ方法が用意されています。

ログイン時に、デバイス IDと電子メールアドレスを顧客サーバーに送信して、セキュリティ署名を計算します。 その後、SDKは顧客エンドポイントを呼び出して、署名オブジェクトのインスタンス化に必要なフィールドを取得します。 Marketo Mobile Adminでセキュリティアクセスモードが有効になっている場合は、SDKでこのシグネチャを設定する必要があります。

## セキュアアクセスモードの設定

Marketo管理者/ モバイルアプリとデバイス ページでセキュアアクセスモードを有効にする前に、この設定を実装します。

セキュアアクセスモードには、サーバーサイド署名アルゴリズムと顧客エンドポイントが必要です。 エンドポイントは次の値を返します。

- アクセスキー
- 予定署名
- 有効期限タイムスタンプ
- メールアドレス

このアルゴリズムは、ユーザーアクセスキー、アクセス秘密鍵、メールアドレス、タイムスタンプ、デバイス IDを使用します。 お客様は、エンドポイントを設定し、署名計算を実行して、有効期限タイムスタンプを最新の状態に保つ必要があります。

```python
import argparse
import datetime
import hashlib
import hmac


ACCESS_KEY = 'Your Access Key'
ACCESS_SECRET = 'Your access secret'

# Key should not be unicode
def get_signing_key(timestamp):
    return 'MKTO' + ACCESS_SECRET + str(timestamp)

def get_string_to_sign(email, uuid):
    return email + uuid

def get_hmac(key, string_to_sign):
    return hmac.new(key, string_to_sign.encode('utf-8'), hashlib.sha256).hexdigest()

def get_epoch_plus_day():
    epoch = datetime.datetime.utcfromtimestamp(0)
    valid_until_dt = datetime.datetime.utcnow() + datetime.timedelta(days=1)
    return long((valid_until_dt - epoch).total_seconds())

if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.add_argument("-e", "--email", required=True, help="email address")
    parser.add_argument("-u", "--uuid", required=True, help="Device install id")
    parser.add_argument("-t", "--timestamp", type=int, help="Valid until timestamp")
    args = parser.parse_args()
    string_to_sign = get_string_to_sign(args.email, args.uuid)
    if not args.timestamp:
        valid_until = get_epoch_plus_day()
    else:
        valid_until = args.timestamp
    signing_key = get_signing_key(valid_until)
    hmac_string = get_hmac(signing_key, string_to_sign)
    print 'HMAC is ', hmac_string
```

プラットフォーム固有の方法を使用して、セキュリティ署名を設定または削除し、デバイス IDを取得します。

### iOS

```objectivec
Marketo * sharedInstance =[Marketo sharedInstance];

// set secure signature
MKTSecuritySignature *signature =
[[MKTSecuritySignature alloc] initWithAccessKey:<ACCESS_KEY> signature:<SIGNATURE_TOKEN> timestamp:<EXPIRY_TIMESTAMP> email:<EMAIL>];
[sharedInstance setSecureSignature:signature];

// remove signature
[sharedInstance removeSecureSignature];

// get device id
[sharedInstance getDeviceId];
```

```swift
let sharedInstance = Marketo.sharedInstance()

 // set secure signature
let signature = MKTSecuritySignature(accessKey: <ACCESS_KEY>, signature: <SIGNATURE_TOKEN> , timestamp: <EXPIRY_TIMESTAMP>, email: <EMAIL>)
sharedInstance.setSecureSignature(signature)

// remove signature
[sharedInstance removeSecureSignature];

// get device id
sharedInstance.getDeviceId()
```

### Android

```java
Marketo sdk = Marketo.getInstance(getApplicationContext());

// set signature
MarketoConfig.SecureMode secureMode = new MarketoConfig.SecureMode();
secureMode.setAccessKey(<ACCESS_KEY>);
secureMode.setEmail(<EMAIL_ADDRESS>);
secureMode.setSignature(<SIGNATURE_TOKEN>);
secureMode.setTimestamp(<EXPIRY_DATE>);
if (secureMode.isValid()) {
  sdk.setSecureSignature(secureMode);
}

// remove signature
sdk.removeSecureSignature();

// get device id
sdk.getDeviceId();
```
