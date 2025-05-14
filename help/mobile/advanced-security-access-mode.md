---
title: 高度なセキュリティアクセスモード
feature: Mobile Marketing
description: 高度なセキュリティアクセスモードに関する詳細
exl-id: bd4730ff-708b-465e-b494-485a4dbf67ff
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '303'
ht-degree: 100%

---

# 高度なセキュリティアクセスモード

Marketo SDK では、セキュリティ署名を設定および削除するメソッドを公開しています。また、デバイス ID を取得するユーティリティメソッドもあります。デバイス ID は、セキュリティ署名の計算に使用するために、ログイン時にメールと共に顧客サーバーに渡す必要があります。SDK では、署名オブジェクトをインスタンス化する必要なフィールドを取得するために、上記のアルゴリズムを指す新しいエンドポイントをヒットする必要があります。Marketo Mobile Admin でセキュリティアクセスモードが有効になっている場合、SDK でのこの署名の設定は必要な手順です。

## セキュアアクセスモードの設定

この設定は、Marketo Admin／モバイルアプリとデバイスページでセキュアアクセスモードを有効にする前に実装する必要があります。次の手順では、セキュリティ検証プロセスを完了するために必要なプロセスについて説明します。

セキュアアクセスモードでは、アクセスキー、計算署名、有効期限タイムスタンプおよびメールを取得するためのエンドポイントを提供する署名アルゴリズムを顧客サーバーサイドに実装する必要があります。このアルゴリズムでは、計算を実行するために、ユーザアクセスキー、アクセス秘密鍵、メール、タイムスタンプおよびデバイス ID が必要です。エンドポイントの設定、署名計算を実行するアルゴリズムの実装、有効期限タイムスタンプの最新状態の維持は、お客様の責任となります。

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

Marketo SDK では、セキュリティ署名を設定および削除する新しいメソッドを公開しています。また、デバイス ID を取得するユーティリティメソッドもあります。デバイス ID は、セキュリティ署名の計算に使用するために、ログイン時にメールと共に顧客サーバーに渡す必要があります。SDK では、署名オブジェクトをインスタンス化する必要なフィールドを取得するために、上記のアルゴリズムを指す新しいエンドポイントをヒットする必要があります。Marketo Mobile Admin でセキュリティアクセスモードが有効になっている場合、SDK でのこの署名の設定は必要な手順です。

### iOS

```
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

```
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

```
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
