---
title: React Native
feature: Mobile Marketing
description: React Native for Marketoのインストール
exl-id: 462fd32e-91f1-4582-93f2-9efe4d4761ff
source-git-commit: e7cb23c4d578d949553b2b7a6e127d6be54cdf23
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 1%

---

# React Native

この記事では、Marketo ネイティブ SDK をインストールおよび設定して、モバイルアプリをプラットフォームと統合する方法について説明します。

## 前提条件

[Marketo管理者でアプリケーションを追加します ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) （アプリケーションの秘密鍵と Munchkin ID を取得します）。

## SDK 統合

### Android SDK の統合

**Gradle を使用したセットアップ**

Marketo SDK の依存関係を、最新バージョンで追加します。アプリケーションレベルの `build.gradle` ファイルの dependencies セクションで、（Marketo SDK の適切なバージョンを含めて）を追加します

```
implementation 'com.marketo:MarketoSDK:0.x.x'
```

**Mavencentral リポジトリの追加**

Marketo SDK は、[maven central リポジトリー ](https://mvnrepository.com/) で入手できます。 これらのファイルを同期するには、リポジトリー `mavencentral` ルート `build.gradle` に追加します

```
build script {
  repositories {
    google()
    mavencentral()
  }
}
```

次に、プロジェクトを Gradle ファイルと同期します。

#### iOS SDK の統合

React Native プロジェクトのブリッジを作成する前に、Xcode プロジェクトで SDK を設定することが重要です。

**SDK 統合 – CocoaPods の使用**

iOS SDK をアプリで簡単に使用できます。 CocoaPods を使用してアプリの Xcode プロジェクトにプラットフォームをセットアップし、アプリとプラットフォームを統合するには、次の手順を実行します。

[CocoaPods](https://cocoapods.org/) をダウンロード - Ruby Gem として配布され、コード内でiOS SDK などのサードパーティライブラリを使用するプロセスを簡素化する、Objective-C および Swift の依存関係マネージャーです。

ダウンロードしてインストールするには、Macでコマンドラインターミナルを起動し、次のコマンドを実行します。

1. CocoaPods をインストールします。

`$ sudo gem install cocoapods`

1. Podfile を開きます。 （ReactNative プロジェクトのiOS フォルダー内）

`$ open -a Xcode Podfile`

1. Podfile に次の行を追加します。

`$ pod 'Marketo-iOS-SDK'`

1. Podfile を保存して閉じます。

1. Marketo iOS SDK をダウンロードしてインストールします。

`$ pod install`

1. Xcode でワークスペースを開きます。

`$ open App.xcworkspace`

## ネイティブモジュールのインストール手順

React Native アプリは、AppleまたはGoogle Pay にアクセスするためのネイティブ API など、JavaScriptでデフォルトでは使用できないネイティブ Platform API にアクセスする必要が生じる場合があります。 JavaScriptに再実装することなく、既存の Objective-C、Swift、Java、C++ライブラリを再利用したり、画像処理などの目的で高性能のマルチスレッドコードを記述したりする場合があります。

NativeModule システムは、Java/Objective-C/C++（ネイティブ）クラスのインスタンスを JS オブジェクトとしてJavaScript（JS）に公開します。これにより、JS 内から任意のネイティブコードを実行できます。 この機能が通常の開発プロセスに含まれるとは思いませんが、この機能が存在することは不可欠です。 React Nativeが JS アプリに必要なネイティブ API を書き出さない場合は、自分で書き出すことができます。

React Native ブリッジは、JSX とネイティブアプリレイヤー間の通信に使用されます。 この場合、ホストアプリは、Marketo SDK のメソッドを呼び出す JSX コードを記述できます。

### Android

このファイルには、指定されたパラメーターでMarketo SDK のメソッドを内部で呼び出すことができるラッパーメソッドが含まれています。

```
public class RNMarketoModule extends ReactContextBaseJavaModule {

   final Marketo marketoSdk;
   RNMarketoModule(ReactApplicationContext context) {
       super(context);
       marketoSdk = Marketo.getInstance(context);
   }

   @NonNull
   @Override
   public String getName() {
       return "RNMarketoModule";
   }

   @ReactMethod
   public void associateLead(ReadableMap leadData) {

       MarketoLead mLead = new MarketoLead();
       try {
           mLead.setCity(leadData.getString(MarketoLead.KEY_CITY));
           mLead.setFirstName(leadData.getString(MarketoLead.KEY_FIRST_NAME));
           mLead.setLastName(leadData.getString(MarketoLead.KEY_LAST_NAME));
           mLead.setAddress(leadData.getString(MarketoLead.KEY_ADDRESS));
           mLead.setEmail(leadData.getString(MarketoLead.KEY_EMAIL));
           mLead.setBirthDay(leadData.getString(MarketoLead.KEY_BIRTHDAY));
           mLead.setCountry(leadData.getString(MarketoLead.KEY_COUNTRY));
           mLead.setFacebookId(leadData.getString(MarketoLead.KEY_FACEBOOK));
           mLead.setGender(leadData.getString(MarketoLead.KEY_GENDER));
           mLead.setState(leadData.getString(MarketoLead.KEY_STATE));
           mLead.setPostalCode(leadData.getString(MarketoLead.KEY_POSTAL_CODE));
           mLead.setTwitterId(leadData.getString(MarketoLead.KEY_TWITTER));
           marketoSdk.associateLead(mLead);
       }
       catch (MktoException e){
       }
   }
   @ReactMethod
   public void setSecureSignature(ReadableMap readableMap) {
       MarketoConfig.SecureMode secureMode = new MarketoConfig.SecureMode();
       secureMode.setAccessKey(readableMap.getString("accessKey"));
       secureMode.setEmail(readableMap.getString("email"));
       secureMode.setSignature(readableMap.getString("signature"));
       secureMode.setTimestamp(readableMap.getInt("timeStamp"));
       marketoSdk.setSecureSignature(secureMode);
   }
   @ReactMethod
      public void initializeSDK(String frameworkType, String munchkinId, String appSecreteKey){
          marketoSdk.initializeSDK(munchkinId,appSecreteKey,frameworkType);
    }
   

   @ReactMethod
   public void initializeMarketoPush(String projectId){
       marketoSdk.initializeMarketoPush( projectId);
   }

   @ReactMethod
   public void initializeMarketoPush(String projectId, String channelName){
       marketoSdk.initializeMarketoPush( projectId, channelName);
   }

   @ReactMethod
   public void uninitializeMarketoPush(){
       marketoSdk.uninitializeMarketoPush();
   }

   @ReactMethod
   public void reportAction(String action){
       Marketo.reportAction(action, null);
   }

   @ReactMethod
   public void reportAction(String action, ReadableMap readableMap){
       MarketoActionMetaData marketoActionMetaData = new MarketoActionMetaData();
       marketoActionMetaData.setActionDetails(readableMap.getString("setMetric"));
       marketoActionMetaData.setActionMetric(readableMap.getString("setLength"));
       marketoActionMetaData.setActionLength(readableMap.getString("actionDetails"));
       marketoActionMetaData.setActionType(readableMap.getString("actionType"));
       Marketo.reportAction(action, marketoActionMetaData);
   }
}
```

**パッケージを登録**

React-native にMarketo パッケージについて知らせます。

```
public class MarketoPluginPackage implements ReactPackage {

   @NonNull
   @Override
   public List createNativeModules(@NonNull ReactApplicationContext reactContext) {
           List modules = new ArrayList<>();

           modules.add(new RNMarketoModule(reactContext));

           return modules;    
   }

   @NonNull
   @Override
   public List createViewManagers(@NonNull ReactApplicationContext reactContext) {
       return Collections.emptyList();
   }
}
```

パッケージの登録を完了するには、MarketoPluginPackage をアプリケーションクラスの React パッケージリストに追加します。

```
public class MainApplication extends Application implements ReactApplication {
 
  private final ReactNativeHost mReactNativeHost =
      new ReactNativeHost(this) {
        @Override
        public boolean getUseDeveloperSupport() {
          return BuildConfig.DEBUG;
        }
 
        @Override
        protected List getPackages() {
          @SuppressWarnings("UnnecessaryLocalVariable")
          List packages = new PackageList(this).getPackages();
          packages.add(new MarketoPluginPackage());     //Add the Marketo Package here.
          // Packages that cannot be autolinked yet can be added manually here, for example:
          return packages;
        }
}
```

### iOS

次のガイドでは、JavaScriptからMarketoの API にアクセスできるネイティブモジュール _RNMarketoModule_ を作成します。

開始するには、React Native アプリケーション内でiOS プロジェクトを Xcode で開きます。 iOS プロジェクトは、React Native アプリ内で見つけることができます。 Xcode を使用してネイティブコードを記述することをお勧めします。 Xcode はiOS開発用に構築されており、コード構文などの小さなエラーをすばやく解決するのに役立ちます。

メインのカスタムネイティブモジュールヘッダーと実装ファイルを作成します。 `MktoBridge.h` という名前の新しいファイルを作成し、次の内容を追加します。

```
//
//  MktoBridge.h
//
//  Created by Marketo, An Adobe company.
//

#import <Foundation/Foundation.h>
#import <React/RCTBridgeModule.h>

NS_ASSUME_NONNULL_BEGIN

@interface MktoBridge : NSObject 

@end

NS_ASSUME_NONNULL_END
```

対応する実装ファイル `MktoBridge.m` を同じフォルダーに作成し、次の内容を含めます。

```
//
//  MktoBridge.h
//  Created by Marketo, An Adobe company.
//

#import <Foundation/Foundation.h>
#import <React/RCTBridgeModule.h>

NS_ASSUME_NONNULL_BEGIN

@interface MktoBridge : NSObject <RCTBridgeModule>

@end

NS_ASSUME_NONNULL_END


//
//  MktoBridge.m
//  Created by Marketo, An Adobe company.
//

#import "MktoBridge.h"
#import <MarketoFramework/Marketo.h>
#import <React/RCTBridge.h>
#import "ConstantStringsHeader.h"

@implementation MktoBridge 

RCT_EXPORT_MODULE(RNMarketoModule);
 
+(BOOL)requiresMainQueueSetup{
  return NO;
}
 
RCT_EXPORT_METHOD(initializeSDK:(NSString *) munchkinId SecretKey: (NSString *) secretKey andFrameworkType: (NSString *) frameworkType){
  [[Marketo sharedInstance] initializeWithMunchkinID:munchkinId appSecret:secretKey mobileFrameworkType:frameworkType launchOptions:nil];
}
 
RCT_EXPORT_METHOD(reportAction:(NSString *)actionName withMetaData:(NSDictionary *)metaData){
  MarketoActionMetaData *meta = [[MarketoActionMetaData alloc] init];
  [meta setType:[metaData objectForKey:KEY_ACTION_TYPE]];
  [meta setDetails:[metaData objectForKey:KEY_ACTION_DETAILS]];
  [meta setLength:[metaData valueForKey:KEY_ACTION_LENGTH]];
  [meta setMetric:[metaData valueForKey:KEY_ACTION_METRIC]];
  [[Marketo sharedInstance] reportAction:actionName withMetaData:meta];
}
 
RCT_EXPORT_METHOD(associateLead:(NSDictionary *)leadDetails){
  MarketoLead *lead = [[MarketoLead alloc] init];
  if ([leadDetails objectForKey:KEY_EMAIL] != nil) {
    [lead setEmail:[leadDetails objectForKey:KEY_EMAIL]];
  }
  if ([leadDetails objectForKey:KEY_FIRST_NAME] != nil) {
    [lead setFirstName:[leadDetails objectForKey:KEY_FIRST_NAME]];
  }
  
  if ([leadDetails objectForKey:KEY_LAST_NAME] != nil) {
    [lead setLastName:[leadDetails objectForKey:KEY_LAST_NAME]];
  }
  
  if ([leadDetails objectForKey:KEY_CITY] != nil) {
    [lead setCity:[leadDetails objectForKey:KEY_CITY]];
  }
    [[Marketo sharedInstance] associateLead:lead];
}
 
RCT_EXPORT_METHOD(uninitializeMarketoPush){
  [[Marketo sharedInstance] unregisterPushDeviceToken];
}
 
RCT_EXPORT_METHOD(reportAll){
  [[Marketo sharedInstance] reportAll];
}
 
RCT_EXPORT_METHOD(setSecureSignature:(NSDictionary *)secureSignature){
  MKTSecuritySignature *secSignature = [[MKTSecuritySignature alloc]
                                        initWithAccessKey:[secureSignature objectForKey:KEY_ACCESSKEY]
                                        signature:[secureSignature objectForKey:KEY_SIGNATURE]
                                        timestamp: [secureSignature objectForKey:KEY_EMAIL]
                                        email:[secureSignature objectForKey:KEY_EMAIL]];
  
    [[Marketo sharedInstance] setSecureSignature:secSignature];
}

RCT_EXPORT_METHOD(requestPermission:(RCTPromiseResolveBlock)resolve rejecter:(RCTPromiseRejectBlock)reject) {
  UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
  [center requestAuthorizationWithOptions:(UNAuthorizationOptionAlert + UNAuthorizationOptionSound + UNAuthorizationOptionBadge)
                        completionHandler:^(BOOL granted, NSError * _Nullable error) {
    if (error) {
      reject(@"PERMISSION_ERROR", @"Permission request failed", error);
    } else {
      resolve(@(granted));
    }
  }];
}

RCT_EXPORT_METHOD(registerForRemoteNotifications) {
  dispatch_async(dispatch_get_main_queue(), ^{
    [[UIApplication sharedApplication] registerForRemoteNotifications];
  });
}


@end
```

#### Marketo SDK の初期化

ネイティブモジュールの createCalendarEvent （） メソッドの呼び出しを追加する場所を、アプリケーションで見つけます。 以下は、アプリに追加できる NewModuleButton コンポーネントの例です。 NewModuleButton の onPress （）関数内でネイティブモジュールを呼び出すことができます。

```
import React from 'react';
import { NativeModules, Button } from 'react-native';

const NewModuleButton = () => {
  const onPress = () => {
    console.log('We will invoke the native module here!');
  };

  return (
    
  );
  };

export default NewModuleButton;
```

このJavaScript ファイルは、ネイティブモジュールをJavaScript レイヤーに読み込みます。

```javascript
import React from 'react';
import {Node} from 'react';
import { NativeModules } from 'react-native';

const { RNMarketoModule } = NativeModules;
```

上記のファイルが正しく配置されたら、js モジュールを任意の js クラスにインポートし、そのメソッドを直接呼び出すことができます。 例：

React ネイティブアプリのフレームワークタイプとして「reactNative」を渡す必要があります。 

```
// Initialize marketo SDK with Munchkin & Seretkey you have from step 1.
RNMarketoModule.initializeSDK("MunchkinID","SecreteKEY","FrameworkType")

//You can create a Marketo Lead by calling the associateLead function.
RNMarketoModule.associateLead({ email: "", firstName: "", lastName:"", city:""})

//You can report any user performed action by calling the reportaction function.
RNMarketoModule.reportAction("Bought Shirt", {actionType:"Shopping", actionDetails: "Red Shirt", setLength : 20, setMetric : 30 })

//You can set Secure Signature by calling this method.
RNMarketoModule.setSecureSignature({accessKey: "Key102", email: "testleadrk@001.com", signature : "asdfghjkloiuytds", timeStamp: "12345678987654"})

//This function will Enable user notifications (Only Android)
RNMarketoModule.initializeMarketoPush("350312872033", "MKTO")

//The token can also be unregistered on logout.
RNMarketoModule.uninitializeMarketoPush()
```

#### プッシュ通知の設定

プロジェクト ID とチャネル名を使用してプッシュを初期化

```
RNMarketoModule.initializeMarketoPush("ProjectId", "Channel_name")
```

`AndroidManifest.xml` に次のサービスを追加します

```xml
<service android:exported="true" android:name=".MyFirebaseMessagingService" android:stopWithTask="true">
    <intent-filter>
        <action  android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
    </intent-filter/>
    <intent-filter> 
        <action android:name="com.google.firebase.MESSAGING_EVENT"/> 
    </intent-filter/>
</activity/>
```

`FirebaseMessagingService.java` という名前のクラスを作成し、次のコードを追加します

```java
import com.google.firebase.messaging.FirebaseMessagingService;
import com.google.firebase.messaging.RemoteMessage;
import com.marketo.Marketo;

public class MyFirebaseMessagingService extends FirebaseMessagingService {

   @Override
   public void onNewToken(String token) {
       super.onNewToken(token);
       Marketo marketoSdk = Marketo.getInstance(this.getApplicationContext());
       marketoSdk.setPushNotificationToken(token);
   }

   @Override
   public void onMessageReceived(RemoteMessage remoteMessage) {
       Marketo marketoSdk = Marketo.getInstance(this.getApplicationContext());
       marketoSdk.showPushNotification(remoteMessage);
   }
}
```

ユーザーのデバイスにプッシュ通知を送信するには、Xcode プロジェクトで権限が有効になっている必要があります。

プッシュ通知を送信するには、[ プッシュ通知を追加 ](push-notifications.md) します。

iOSのプッシュ通知を設定する。
pushNotifications.tsx ファイルを作成し、以下を追加します。

```
import { NativeModules } from 'react-native';
const { RNMarketoModule } = NativeModules;

const requestPermission = (): Promise<boolean> => {
return RNMarketoModule.requestPermission()
.then((granted: boolean) => {
console.log('Permission granted:', granted);
return granted;
})
.catch((error: any) => {
console.error('Permission error:', error);
throw error;
});
};

const registerForRemoteNotifications = (): void => {
RNMarketoModule.registerForRemoteNotifications();
};

export { requestPermission, registerForRemoteNotifications };
```


`App.tsx` を追加してプッシュ通知を許可する

```
import React, { useEffect } from 'react';

useEffect(() => {
requestPermission().then(granted => {
if (granted) {
registerForRemoteNotifications();
}
});
}, []);
```

APNS デリゲートメソッドで `AppDelegate.mm` を更新します。

```
#import "AppDelegate.h"
#import "MktoBridge.h"
#import <MarketoFramework/Marketo.h>
#import <React/RCTBundleURLProvider.h>

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  self.moduleName = @"MyNewApp";
  // You can add your custom initial props in the dictionary below.
  // They will be passed down to the ViewController used by React Native.
  self.initialProps = @{};

  return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

- (NSURL *)sourceURLForBridge:(RCTBridge *)bridge
{
  return [self bundleURL];
}

-(void)userNotificationCenter:(UNUserNotificationCenter *)center 
      willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler{
    completionHandler(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge);
}

- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response
         withCompletionHandler:(void(^)(void))completionHandler {
    [[Marketo sharedInstance] userNotificationCenter:center 
                      didReceiveNotificationResponse:response
                               withCompletionHandler:completionHandler];
}

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    // Register the push token with Marketo
    [[Marketo sharedInstance] registerPushDeviceToken:deviceToken];
}

- (void)applicationWillTerminate:(UIApplication *)application {
    [[Marketo sharedInstance] unregisterPushDeviceToken];
}

-(void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error{
  NSLog(@"Failed to register for remote notification - %@", [error userInfo]);
}

- (NSURL *)bundleURL
{
#if DEBUG
  return [[RCTBundleURLProvider sharedSettings] jsBundleURLForBundleRoot:@"index"];
#else
  return [[NSBundle mainBundle] URLForResource:@"main" withExtension:@"jsbundle"];
#endif
}

@end
```

### テスト デバイスの追加

**Android**

アプリケーションタグ内のファイルに「MarketoActivity」 `AndroidManifest.xml` 追加します。

```xml
<activity android:name="com.marketo.MarketoActivity" android:configChanges="orientation|screenSize" android:exported="true">
    <intent-filter android:label="MarketoActivity">
        <action  android:name="android.intent.action.VIEW"/>
        <category  android:name="android.intent.category.DEFAULT"/>
        <category  android:name="android.intent.category.BROWSABLE"/>
        <data android:host="add_test_device" android:scheme="mkto"/>
    </intent-filter/>
</activity/>
```

**iOS**

1. Project/Target/情報/URL タイプを選択します。

1. 識別子の追加：${PRODUCT_NAME}

1. URL スキームの設定：`mkto-<S_ecret Key_>`

1. `AppDelegate.m` ファイルに `application:openURL:sourceApplication:annotation:` を含める（Objective-C）

**iOS - AppDelegate でカスタム Url タイプ/ディープリンクを処理します** 

```
- (BOOL)application:(UIApplication *)app
            openURL:(NSURL *)url
            options:(NSDictionary *)options{
   
    return [[Marketo sharedInstance] application:app
                                         openURL:url
                                         options:options];    
}
```

これらの定数は、JavaScript から API を呼び出す際に使用されます。 定数ファイルを作成し、次の情報を追加する必要があります。

```
// Lead attributes.
static NSString *const KEY_FIRST_NAME = @"firstName";
static NSString *const KEY_LAST_NAME = @"lastName";
static NSString *const KEY_ADDRESS = @"address";
static NSString *const KEY_CITY = @"city";
static NSString *const KEY_STATE = @"state";
static NSString *const KEY_COUNTRY = @"country";
static NSString *const KEY_GENDER = @"gender";
static NSString *const KEY_EMAIL = @"email";
static NSString *const KEY_TWITTER = @"twitterId";
static NSString *const KEY_FACEBOOK = @"facebookId";
static NSString *const KEY_LINKEDIN = @"linkedinId";
static NSString *const KEY_LEAD_SOURCE = @"leadSource";
static NSString *const KEY_BIRTHDAY = @"dateOfBirth";
static NSString *const KEY_FACEBOOK_PROFILE_URL = @"facebookProfileURL";
static NSString *const KEY_FACEBOOK_PROFILE_PIC = @"facebookPhotoURL";

// Custom actions
static NSString *const KEY_ACTION_TYPE = @"actionType";
static NSString *const KEY_ACTION_DETAILS = @"actionDetails";
static NSString *const KEY_ACTION_LENGTH = @"setLength";
static NSString *const KEY_ACTION_METRIC = @"setMetric";

//Secure Signature
static NSString *const KEY_ACCESSKEY = @"accessKey";
static NSString *const KEY_SIGNATURE = @"signature";
static NSString *const KEY_TIMESTAMP = @"timeStamp";
```

使用例

```
//You can create a Marketo Lead by calling the associateLead function.
RNMarketoModule.associateLead({ email: "", firstName: "", lastName:"", city:""})
```
