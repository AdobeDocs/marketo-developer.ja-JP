---
title: 「高度なセキュリティアクセスモード」
feature: "Mobile Marketing"
description: 「高度なセキュリティアクセスモードの詳細」
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# 高度なセキュリティ アクセス モード

Marketo SDK が、セキュリティシグネチャを設定および削除するメソッドを公開します。 デバイス ID を取得するためのユーティリティメソッドもあります。 デバイス ID は、ログイン時に、セキュリティ署名の計算に使用するために、メールと共に顧客サーバーに渡す必要があります。 SDK は、上記のアルゴリズムを指すヒットの新しいエンドポイントを取得して、signature オブジェクトをインスタンス化するために必要なフィールドを取得する必要があります。 Marketo Mobile Admin でセキュリティアクセスモードが有効になっている場合、SDK でこのシグネチャを設定する必要があります。

## セキュア アクセス モードの設定

この設定は、Marketo管理者/ モバイルアプリとデバイス ページでセキュアアクセスモードが有効になる前に実装する必要があります。 次の手順では、セキュリティ検証プロセスを完了するために必要なプロセスについて説明します。

セキュアアクセスモードでは、アクセスキー、計算署名、有効期限タイムスタンプ、メールを取得するエンドポイントを提供する署名アルゴリズムを顧客サーバーサイドで実装する必要があります。 このアルゴリズムでは、計算を実行するために、ユーザーアクセスキー、アクセシークレット、メール、タイムスタンプ、デバイス ID が必要です。 顧客は、エンドポイントを設定し、署名計算を実行するアルゴリズムを実装し、有効期限タイムスタンプを最新の状態に保つ責任があります。

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

Marketo SDK は、セキュリティシグネチャを設定および削除する新しいメソッドを公開します。 デバイス ID を取得するためのユーティリティメソッドもあります。 デバイス ID は、ログイン時に、セキュリティ署名の計算に使用するために、メールと共に顧客サーバーに渡す必要があります。 SDK は、上記のアルゴリズムを指すヒットの新しいエンドポイントを取得して、signature オブジェクトをインスタンス化するために必要なフィールドを取得する必要があります。 Marketo Mobile Admin でセキュリティアクセスモードが有効になっている場合、SDK でこのシグネチャを設定する必要があります。

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
