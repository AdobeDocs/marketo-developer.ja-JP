---
title: プッシュ通知
feature: Mobile Marketing
description: APNs証明書とXcodeの設定からMarketo SDKの統合、トークン登録、処理まで、MarketoでiOS プッシュ通知を有効にする方法をガイドします。
exl-id: 41d657d8-9eea-4314-ab24-fd4cb2be7f61
TQID: https://experienceleague.adobe.com/ghits-m4w3oid3cZuRTz-foAar8OaqtiQqWu2yRKTwE
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1162
ht-degree: 23%

---

# プッシュ通知

Marketo Mobile SDKを使用するiOSまたはAndroid アプリケーションのプッシュ通知を有効にします。

## iOS でのプッシュ通知の設定

プッシュ通知を有効にするには、次の 3 つの手順があります。

1. Apple Developer アカウントでプッシュ通知を設定します。
1. xCode でプッシュ通知を有効にします。
1. Marketo SDKを使用して、アプリでプッシュ通知を有効にします。

### Apple Developer アカウントでのプッシュ通知の設定

1. Apple Developer [ メンバーセンター](https://developer.apple.com/membercenter)にログインします。
1. 「証明書、識別子、プロファイル」を選択します。
1. 「iOS、tvOS、watchOS」の下にある「証明書 – >すべて」フォルダーを選択します。
1. 左上隅の証明書の横にある「+」を選択します。![](assets/certificates-plus.png)
1. 「Apple プッシュ通知サービス SSL （サンドボックスおよび実稼動）」を選択し、「続行」を選択します。
1. アプリの構築に使用するアプリケーション IDを選択します。![](assets/push-appid.png)
1. CSRを作成してアップロードし、プッシュ証明書を生成します。![](assets/push-ssl.png)
1. 証明書をダウンロードし、ダブルクリックしてインストールします。![](assets/certificate-download.png)
1. 「キーチェーンアクセス」を開き、証明書を右クリックして、両方の項目を`.p12` ファイルに書き出します。![key_chain](assets/key-chain.png)
1. 通知を設定するには、Marketo Admin Console を通じてこのファイルをアップロードします。
1. アプリのプロビジョニングプロファイルを更新します。

### xCode でのプッシュ通知の有効化

xCode プロジェクトでプッシュ通知機能を有効にします。![](assets/push-xcode.png)

### Marketo SDK を使用したアプリでのプッシュ通知の有効化

次のコードを`AppDelegate.m` ファイルに追加して、顧客デバイスにプッシュ通知を配信します。

**注** - [!DNL Adobe Launch]拡張機能を使用する場合は、クラス名として`ALMarketo`を使用します。

次のインポートを`AppDelegate.h`に追加します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
#import <UserNotifications/UserNotifications.h>
```

>[!TAB Swift]

```swift
import UserNotifications
```

>[!ENDTABS]

次に示すように、`AppDelegate` に `UNUserNotificationCenterDelegate` を追加します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
@interface AppDelegate : UIResponder <UIApplicationDelegate, UNUserNotificationCenterDelegate>
```

>[!TAB Swift]

```swift
class AppDelegate: UIResponder, UIApplicationDelegate , UNUserNotificationCenterDelegate
```

>[!ENDTABS]

プッシュ通知サービスを初期化するには、次のコードを追加します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
        center.delegate = self;
        [center requestAuthorizationWithOptions:(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge) completionHandler:^(BOOL granted, NSError * _Nullable error){
            if(!error){
                dispatch_async(dispatch_get_main_queue(), ^{
                    [[UIApplication sharedApplication] registerForRemoteNotifications];
                });
            }
        }];

    return YES;
}
```

>[!TAB Swift]

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

    UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .sound,    .badge]) { granted, error in
            if let error = error {
                print("\(error.localizedDescription)")
            } else {
                DispatchQueue.main.async {
                    application.registerForRemoteNotifications()
                }
            }
        }

        return true
}
```

>[!ENDTABS]

Apple プッシュサービスへの登録を開始するには、このメソッドを呼び出します。 登録が成功すると、アプリはApp デリゲート オブジェクトの`application:didRegisterForRemoteNotificationsWithDeviceToken:` メソッドを呼び出し、デバイストークンを渡します。

登録に失敗した場合、アプリは代わりにアプリデリゲートの `application:didFailToRegisterForRemoteNotificationsWithError:` メソッドを呼び出します。

Marketoにプッシュトークンを登録します。 Marketoからプッシュ通知を受信するには、デバイストークンを登録する必要があります。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    // Register the push token with Marketo
    [[Marketo sharedInstance] registerPushDeviceToken:deviceToken];
}
```

>[!TAB Swift]

```swift
func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    // Register the push token with Marketo
    Marketo.sharedInstance().registerPushDeviceToken(deviceToken)
}
```

>[!ENDTABS]

また、ユーザーがログアウトしたときにトークンを登録解除することもできます。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
[[Marketo sharedInstance] unregisterPushDeviceToken];
```

>[!TAB Swift]

```swift
Marketo.sharedInstance().unregisterPushDeviceToken
```

>[!ENDTABS]

プッシュトークンを再登録するには、手順3のコードをAppDelegate メソッドに抽出します。 ViewController ログインメソッドからそのメソッドを呼び出します。

デバイストークンをMarketoに登録した後、プッシュ通知を処理します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo
{
    [[Marketo sharedInstance] handlePushNotification:userInfo];
}
```

>[!TAB Swift]

```swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
    Marketo.sharedInstance().handlePushNotification(userInfo)
}
```

>[!ENDTABS]

AppDelegateに次のメソッドを追加します。

この方法を使用すると、アプリがフォアグラウンドにいる間にアラートを表示したり、サウンドを再生したり、バッジを上げたりできます。 このメソッドで適切なcompletionHandlerを呼び出します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
-(void)userNotificationCenter:(UNUserNotificationCenter *)center
    willPresentNotification:(UNNotification *)notification
        withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler{

    completionHandler(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge);
}
```

>[!TAB Swift]

```swift
func userNotificationCenter(_ center: UNUserNotificationCenter,
            willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (
    UNNotificationPresentationOptions) -> Void) {
    completionHandler([.alert, .sound,.badge])
}
```

>[!ENDTABS]

AppDelegateで新しく受信したプッシュ通知を処理します。

デリゲートは、ユーザーがアプリケーションを開いたり、通知を閉じたり、UNNotificationActionを選択したりして通知に応答する際に、このメソッドを呼び出します。 applicationDidFinishLaunching：からアプリケーションが返される前に、デリゲートを設定します。

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler {
    [[Marketo sharedInstance] userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
}
```

>[!TAB Swift]

```swift
func userNotificationCenter(_ center: UNUserNotificationCenter,
                                didReceive response: UNNotificationResponse,
                                withCompletionHandler
                                completionHandler: @escaping () -> Void) {
        Marketo.sharedInstance().userNotificationCenter(center, didReceive: response, withCompletionHandler: completionHandler)
}
```

>[!ENDTABS]

プッシュ通知の追跡：

アプリがバックグラウンドまたは非アクティブの場合、デバイスは次に示すようにプッシュ通知を受け取ります。 Marketoは、ユーザーが通知を選択したときにトラッキングします。

![mobile8](assets/mobile8.png)

デバイスがプッシュ通知を受信すると、アプリのデリゲートの`application:didReceiveRemoteNotification:` コールバックに通知が渡されます。

次のMarketo アクティビティログは、アプリイベントとプッシュ通知イベントを示しています。

![mobile9](assets/mobile9.png)

## Android でのプッシュ通知の設定

1. アプリケーションタグ内に次の権限を追加します。

   `AndroidManifest.xml`を開き、次の権限を追加します。 アプリでは、「INTERNET」および「ACCESS_NETWORK_STATE」権限をリクエストする必要があります。 アプリが既にリクエストしている場合は、この手順をスキップします。

   ```xml
   <uses‐permission android:name="android.permission.INTERNET"/>
   <uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
   
   <!‐‐Following permissions are required for push notification.‐‐>
   <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
   <!‐‐Keeps the processor from sleeping when a message is received.‐‐>
   <uses-permission android:name="android.permission.WAKE_LOCK"/>
   <permission android:name="<PACKAGE_NAME>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
   <uses-permission android:name="<PACKAGE_NAME>.permission.C2D_MESSAGE" />
   <!-- This app has permission to register and receive data message. -->
   <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   ```

1. HTTPv1でFCMを設定します。

   - Marketo feature managerでMME FCM HTTPv1を有効にします。![](assets/feature-manager.png)
   - アプリのサービスアカウント Json ファイルをMLMにアップロードします。
   - Firebase Consoleからサービスアカウント Json ファイルをダウンロードします。![](assets/fcm-console.png)
   - プッシュ通知を送信する前に、Marketoでサービスアカウント Json ファイルをアップロードしてから1時間待ちます。

## Android テストデバイス

アプリケーションタグ内のマニフェストファイルにMarketo アクティビティを追加します。

```xml
<activity android:name="com.marketo.MarketoActivity"  android:configChanges="orientation|screenSize">
    <intent-filter android:label="MarketoActivity">
        <action  android:name="android.intent.action.VIEW"/>
        <category  android:name="android.intent.category.DEFAULT"/>
        <category  android:name="android.intent.category.BROWSABLE"/>
        <data android:host="add_test_device" android:scheme="mkto"/>
    </intent-filter/>
</activity/>
```

## Marketo プッシュサービスの登録

1. 終了アプリケーション タグの前にFirebase メッセージング サービスを`AndroidManifest.xml`に追加します。

   ```xml
   <meta-data
       android:name="com.google.android.gms.version"
       android:value="@integer/google_play_services_version" />
   <service android:name=".MyFirebaseMessagingService">
   <intent-filter>
   <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
   <action android:name="com.google.firebase.MESSAGING_EVENT"/>
   </intent-filter>
   </service>
   ```

1. 次のように、`MyFirebaseMessagingService`にMarketo SDK メソッドを追加します。

   ```java
   import com.marketo.Marketo;
   
   public class MyFirebaseMessagingService extends FirebaseMessagingService {
   
       @Override
       public void onNewToken(String s) {
           super.onNewToken(s);
           Marketo marketoSdk = Marketo.getInstance(this.getApplicationContext());
           marketoSdk.setPushNotificaitonToken(s);
           // Add your code here...
       }
   
       @Override
       public void onMessageReceived(RemoteMessage remoteMessage) {
           Marketo marketoSdk = Marketo.getInstance(this.getApplicationContext());
           marketoSdk.showPushNotificaiton(remoteMessage);
           // Add your code here...
       }
   
   }
   ```

   **メモ** - Adobe拡張機能を使用する場合は、次のコードを追加します。

   ```java
   import com.marketo.Marketo;
   
   public class MyFirebaseMessagingService extends FirebaseMessagingService {
   
       @Override
       public void onNewToken(String token) {
           super.onNewToken(token);
           ALMarketo.setPushNotificationToken(token);
           // Add your code here...
       }
   
       @Override
       public void onMessageReceived(RemoteMessage remoteMessage) {
           ALMarketo.showPushNotification(remoteMessage);
           // Add your code here...
       }
   
   }
   ```

**メモ**: FCM SDKは、必要な権限と受信者の機能を自動的に追加します。 以前のSDK バージョンを使用していた場合は、メッセージの重複を引き起こす可能性のある、次の古い要素を削除します。

```xml
<receiver android:name="com.marketo.MarketoBroadcastReceiver" android:permission="com.google.android.c2dm.permission.SEND">
    <intent-filter>
        <!‐‐Receives the actual messages.‐‐>
        <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
        <!‐‐Register to enable push notification‐‐>
        <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
        <!‐‐‐Replace YOUR_PACKAGE_NAME with your own package name‐‐>
        <category android:name="YOUR_PACKAGE_NAME"/>
    </intent-filter>
</receiver>

<!‐‐Marketo service to handle push registration and notification‐‐>
<service android:name="com.marketo.MarketoIntentService"/>
```

1. Marketo プッシュを初期化します。 設定を保存したら、アプリケーションクラスを作成または開き、次のコードを追加します。 Firebase Consoleから送信者IDを取得します。

   ```java
   Marketo marketoSdk = Marketo.getInstance(getApplicationContext());
   
   // Enable push notification here. The push notification channel name can by any string
   marketoSdk.initializeMarketoPush(SENDER_ID,"ChannelName");
   ```

   [!DNL Adobe Launch]拡張機能を使用する場合は、次のコードを使用します。

   ```java
   // Enable push notification here. The push notification channel name can by any string
   ALMarketo.initializeMarketoPush(SENDER_ID,"ChannelName");
   ```

   [このチュートリアル](https://developers.google.com/cloud-messaging/)で詳しく説明されている手順を実行して、Google Cloud Messaging サービスを有効にします。

   また、ユーザーがログアウトしたときにトークンを登録解除することもできます。

   ```java
   marketoSdk.uninitializeMarketoPush();
   ```

   [!DNL Adobe Launch]拡張機能を使用する場合は、次のコードを使用します。

   ```java
   ALMarketo.uninitializeMarketoPush();
   ```

   注：プッシュトークンを再登録するには、手順3のコードをAppDelegate メソッドに抽出します。 ViewController ログインメソッドからそのメソッドを呼び出します。

1. オプション：通知アイコンを設定します。 次のメソッドを呼び出して、カスタム通知アイコンを設定します。

   ```java
   MarketoConfig.Notification config = new MarketoConfig.Notification();
   // Optional bitmap for honeycomb and above
   config.setNotificationLargeIcon(bitmap);
   
   // Required icon Resource ID
   config.setNotificationSmallIcon(R.drawable.notification_small_icon);
   
   // Set the configuration
   //Use the static methods on ALMarketo class when using Adobe Extension
   Marketo.getInstance(context).setNotificationConfig(config);
   
   // Get the configuration set
   Marketo.getInstance(context).getNotificationConfig();
   ```

## トラブルシューティング

モバイルプッシュメッセージが期待どおりに機能しない場合は、実装の詳細を調査する前に、一般的な設定の問題を確認してください。

### プッシュメッセージが表示されない

デバイスでプッシュメッセージが無効になっているかどうかを確認します。 モバイルユーザーは、アプリごとにメッセージを受信するかどうかを制御でき、開発者やマーケターは、開発中にメッセージを無効にする場合があります。

アプリが開いていてアクティブかどうかを確認します。 アプリがアクティブな場合、モバイルプッシュメッセージは画面に表示されません。 代わりに、アプリの「ローカル通知」エリアに表示されます。

### Marketo でのアクティビティログの表示

Marketo アクティビティログを使用して、メッセージが送信されたことを確認します。

メッセージを受信する必要があるユーザーのアクティビティレコードを確認します。 メッセージが送信された場合、アクティビティログにはレコードが含まれます。 レコードが存在しない場合は、MarketoでiOS証明書またはAndroid API キー設定を確認します。

### 証明書またはキーが無効

サンドボックスまたは実稼動用に正しい証明書が読み込まれていることを確認します。 必要に応じて、iOS証明書またはAndroid キーを再度書き出して、Marketoに再読み込みします。

### .p12 ファイルに証明書またはキーが欠落している（iOS）

証明書をエクスポートする場合は、キーと証明書の両方をエクスポートします。

### プロファイルのプロビジョニングが最新ではない（iOS）

デバイスを追加したら、プロビジョニングプロファイルを更新し、新しい証明書を生成します。 Xcode プロジェクトを正しいプロファイルと証明書に指定し、証明書をMarketoにインポートします。

### iOS 証明書をアップロードできない（iOS）

証明書の書き出しに使用するパスワードにスペースが含まれていないことを確認します。 例えば、次は使用しないでください。

`Hello World 123`

次を使用します。

`HelloWorld123`

### iOS 証明書のトラブルシューティング

サンドボックスアプリケーションの場合は、「開発者」または「ユニバーサル」証明書を使用します。 実稼動アプリケーションの場合は、有効な「配布」または「ユニバーサル」証明書をアップロードします。

### プッシュバウンス／無効なトークン

登録トークンは、次のシナリオで無効になる可能性があります。

- クライアントアプリが GCM を登録解除した場合。
- クライアントアプリが自動的に登録解除される場合。これは、ユーザがアプリケーションをアンインストールした場合に発生することがあります。 例えば、iOS では、APNS フィードバックサービスが APNS トークンを無効として報告した場合です。
- 登録トークンが期限切れになった場合。 例えば、Google が登録トークンを更新することを決定した場合や、iOS デバイスの APNS トークンが期限切れになった場合です。
- クライアントアプリが更新されたが、新しいバージョンがメッセージを受信するように設定されていない場合。
