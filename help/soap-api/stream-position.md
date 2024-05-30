---
title: "ストリーム位置"
feature: SOAP
description: 「スチームポジション概要」
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# ストリーム位置

ストリーム位置要素は、時系列データの 1 つ以上の論理ストリームの位置参照を含む。 位置参照は、タイムスタンプなどのおおよその外部仕様や、以前の API 呼び出しによって返された位置の不透明な内部仕様である場合があります。 ストリーム位置は、複合型の複数要素型として定義することも、文字列とすることもできます。

ストリーム位置は、データをバッチで取得するために使用され、呼び出し元が結果をページ番号で区切ることができます。 API リクエスト内で渡されるストリーム位置は、以前の応答で返されたストリーム位置の値です。 以前の API 呼び出しから返されたストリームの位置を変更することはお勧めしません。変更すると、予期しない API の動作が発生する場合があります。

## ストリームの位置をサポートする API

- [getCustomObjects](getcustomobjects.md)
- [getLeadChanges](getleadchanges.md)
- [getLeadActivity](getleadactivity.md)
- [getMObjects](getmobjects.md)
- [getMultipleLeads](getmultipleleads.md)

## 単純なストリーム位置

```
<streamPosition>8UJZetaMb1V6uUZl+L7DcPP2jG+PMmtpF</streamPosition>
```

## 複雑なストリーム位置

```xml
<startPosition>
  <latestCreatedAt  />
  <oldestCreatedAt>2013-08-01T00:13:13+00:00</oldestCreatedAt>
  <activityCreatedAt  />
  <offset>ID:1086173</offset>
</startPosition>
```
