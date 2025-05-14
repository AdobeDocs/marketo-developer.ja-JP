---
title: ストリーム位置
feature: SOAP
description: ストリーム位置の概要
exl-id: c3a3fc1e-086b-4822-b2c7-2a7959db557c
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: ht
source-wordcount: '138'
ht-degree: 100%

---

# ストリーム位置

ストリーム位置の要素には、時系列データの 1 つ以上の論理ストリームの位置参照が含まれます。位置参照は、タイムスタンプなどのおおよその外部仕様や、以前の API 呼び出しによって返された位置の不透明な内部仕様である場合があります。ストリーム位置は、複雑な複数要素タイプとして定義することも、文字列として指定することもできます。

ストリーム位置は、データをバッチで取得するのに使用され、呼び出し元が結果をページ分割できます。API リクエスト内で渡されるストリーム位置は、以前の応答で返されたストリーム位置の値です。以前の API 呼び出しから返されたストリーム位置を変更することはお勧めしません。変更すると、予期しない API の動作が発生する場合があります。

## ストリーム位置をサポートする API

- [getCustomObjects](getcustomobjects.md)
- [getLeadChanges](getleadchanges.md)
- [getLeadActivity](getleadactivity.md)
- [getMObjects](getmobjects.md)
- [getMultipleLeads](getmultipleleads.md)

## シンプルなストリーム位置

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
