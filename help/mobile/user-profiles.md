---
title: ユーザプロファイル
feature: Mobile Marketing, Users and Roles
description: Marketo Mobile でのユーザプロファイルの使用
exl-id: 1b2cfb7f-d678-4022-8cd9-a56004a1ac46
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '83'
ht-degree: 100%

---

# ユーザプロファイル

ユーザプロファイルの作成方法

1. [iOS でのユーザプロファイルの作成](#ios_user_profiles)
1. [Android でのユーザプロファイルの作成](#android_user_profiles)

## iOS でのユーザプロファイルの作成 {#ios_user_profiles}

次に示すように、ユーザフィールドを送信することで、リッチプロファイルを作成できます。

```
MarketoLead *profile = [[MarketoLead alloc] init];

// Get user profile from network and populate
[profile setEmail:@"jd@makesomething.com"];
[profile setFirstName:@"John"];
[profile setLastName:@"Doe"];
[profile setAddress:@"1234KingFishSt"];
[profile setCity:@"SouthPadreIsland"];
[profile setState:@"CA"];
[profile setPostalCode:@"78596"];
[profile setCountry:@"USA"];
[profile setGender:@"male"];
[profile setLeadSource:@"_facebook_ads"];
[profile setBirthDay:@"01/01/1985"];
[profile setFacebookId:@"facebookid"];
[profile setFacebookProfileURL:@"facebook.com/profile"];
[profile setFacebookProfilePicURL:@"faceboook.com/profile/pic"];
[profile setLinkedInId:@"linkedinid"];
[profile setTwitterId:@"twitterid"];
```

```
let profile =  MarketoLead()

// Get user profile from network and populate
profile.setEmail("jd@makesomething.com")
profile.setFirstName("John")
profile.setLastName("Doe")
profile.setAddress("1234KingFishSt")
profile.setCity("SouthPadreIsland")
profile.setState("CA")
profile.setPostalCode("78596")
profile.setCountry("USA")
profile.setGender("male")
profile.setLeadSource("_facebook_ads")
profile.setBirthDay("01/01/1985")
profile.setFacebookId("facebookid")
profile.setFacebookProfileURL("facebook.com/profile")
profile.setFacebookProfilePicURL("faceboook.com/profile/pic")
profile.setLinkedInId("linkedinid")
profile.setTwitterId("twitterid")
```

その他の[標準フィールド](../rest-api/list-of-standard-fields.md)を追加します。

>[!BEGINTABS]

>[!TAB Objective C]

```
// Add other custom fields
[profile setFieldName:@"mobilePhone"withValue:@"123.456.7890"];
[profile setFieldName:@"numberOfEmployees"withValue:@"10"];
[profile setFieldName:@"phone"withValue:@"123.456.7890"];
```

>[!TAB Swift]

```
// Add other custom fields
profile.setFieldName("mobilePhone" , withValue :"123.456.7890");
profile.setFieldName("numberOfEmployees", withValue: "10");
profile.setFieldName("phone", withValue:"123.456.7890");
```

>[!ENDTABS]

ユーザプロファイルを報告します。

>[!BEGINTABS]

>[!TAB Objective C]

```
Marketo *sharedInstance = [Marketo sharedInstance];

// This method will update user profile
[sharedInstance associateLead:profile];
```

>[!TAB Swift]

```
let marketo = Marketo.sharedInstance()

// This method will update user profile
marketo.associateLead(profile)
```

>[!ENDTABS]

## Android でのユーザプロファイルの作成 {#android_user_profiles}

1. ユーザプロファイルを作成します。

   次に示すように、ユーザフィールドを送信することで、リッチプロファイルを作成できます。

   ```java
   MarketoLead profile = new MarketoLead();
   
   // Get user profile from network and populate
   try {
       profile.setEmail("htcone3@gmail.com");
       profile.setFirstName("Mike");
       profile.setLastName("Gray");
       profile.setFacebookId("facebookid");
       profile.setAddress("1234 King Fish Blvd");
   }
   catch (MktoException e) {
       e.printStackTrace();
   }
   ```

1. その他の[標準フィールド](../rest-api/list-of-standard-fields.md)を追加します。

   ```java
   // Add other custom fields
   profile.setCustomField("mobilePhone", "123.456.7890");
   profile.setCustomField("numberOfEmployees", "10");
   profile.setCustomField("phone", "123.456.7890");
   profile.setCustomField("rating", "R");
   profile.setCustomField("facebookDisplayName", "mini");
   profile.setCustomField("facebookReach", "10");
   profile.setCustomField("facebookReferredEnrollments", "100");
   profile.setCustomField("facebookReferredVisits", "9998");
   profile.setCustomField("lastReferredEnrollment", "03/01/2015");
   profile.setCustomField("lastReferredVisit", "03/01/2015");
   profile.setCustomField("linkedInDisplayName", "Android");
   ```

1. ユーザプロファイルを報告します。

   ```java
   MarketoLead profile = new MarketoLead();
   
   // This method will update user profile
   marketoSdk.associateLead(profile);
   ```
