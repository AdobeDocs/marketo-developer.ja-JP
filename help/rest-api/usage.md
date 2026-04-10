---
title: 使用状況
feature: REST API
description: ユーザーごとのカウントやエラーコードの合計など、毎日および過去7日間の統計エンドポイントを使用して、Marketo REST APIの使用状況とエラーをモニタリングします。
exl-id: 935a00a4-1e1e-4b48-ae9c-72c5e578312a
source-git-commit: e2606d6cb12c572603ff069617de58417e43ca63
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 9%

---

# 使用方法

[使用状況エンドポイントの参照](https://developer.adobe.com/marketo-apis/api/mapi#tag/Usage)

使用状況APIは、サブスクリプションのREST APIの使用状況とエラーアクティビティの概要を提供します。 これらのエンドポイントは、統合のモニタリング、1日の通話量の追跡、時間の経過に伴うエラー傾向の特定に役立ちます。

使用状況データには、API呼び出しの合計数とユーザーごとの内訳が含まれます。 エラーデータには、エラーの合計数とエラーコードによる分類が含まれます。

使用状況APIは、他のMarketo REST APIと同じ認証方法を使用します。 `Authorization: Bearer {accessToken}` ヘッダーにアクセストークンを渡します。

## エンドポイント

| メソッド | パス | 説明 |
| --- | --- | --- |
| GET | `/rest/v1/stats/usage.json` | 現在の日のAPI使用状況を取得します。 |
| GET | `/rest/v1/stats/usage/last7days.json` | 過去7日間のAPI使用状況を取得します。 |
| GET | `/rest/v1/stats/errors.json` | 現在の日付のAPI エラーを取得します。 |
| GET | `/rest/v1/stats/errors/last7days.json` | 過去7日間のAPI エラーを取得します。 |

## 1日の利用状況

現在の日のAPI使用状況を取得します。

```http
GET /rest/v1/stats/usage.json
```

```json
{
   "requestId": "5f7f#17d7d8f2b6f",
   "success": true,
   "result": [
      {
         "date": "2015-10-17",
         "total": 1120,
         "users": [
            {
               "userId": "some.body@yahoo.com",
               "count": 200
            },
            {
               "userId": "some.body@marketo.com",
               "count": 200
            },
            {
               "userId": "some.body@gmail.com",
               "count": 720
            }
         ]
      }
   ]
}
```

`result`配列内の各オブジェクトには、1日の使用合計とユーザーごとの分類が含まれています。

## 過去7日間の使用履歴

過去7日間のAPI使用状況を取得します。 `result`配列内の各要素は1日を表します。

```http
GET /rest/v1/stats/usage/last7days.json
```

## 日別エラー

現在の日付のAPI エラーを取得します。

```http
GET /rest/v1/stats/errors.json
```

```json
{
   "requestId": "5f7f#17d7d8f2b6f",
   "success": true,
   "result": [
      {
         "date": "2015-10-17",
         "total": 73,
         "errors": [
            {
               "errorCode": "604",
               "count": 1
            },
            {
               "errorCode": "609",
               "count": 56
            },
            {
               "errorCode": "610",
               "count": 16
            }
         ]
      }
   ]
}
```

`result`配列内の各オブジェクトには、1日のエラー合計とエラーコードによる分類が含まれています。

## 過去7日間のエラー

過去7日間のAPI エラーを取得します。 `result`配列内の各要素は1日を表します。

```http
GET /rest/v1/stats/errors/last7days.json
```

## 応答メンバー

### 使用結果オブジェクト

| 名前 | データタイプ | 説明 |
| --- | --- | --- |
| `date` | 文字列 | `YYYY-MM-DD`形式の使用概要の日付。 |
| `total` | 整数 | その日のAPI呼び出しの合計数。 |
| `users` | 配列 | その日のユーザーごとの使用回数のリスト。 |

### 使用状況ユーザーオブジェクト

| 名前 | データタイプ | 説明 |
| --- | --- | --- |
| `userId` | 文字列 | API ユーザーID: |
| `count` | 整数 | そのユーザーが1日に実行したAPI呼び出しの数。 |

### エラー結果オブジェクト

| 名前 | データタイプ | 説明 |
| --- | --- | --- |
| `date` | 文字列 | エラーの概要の日付を`YYYY-MM-DD`形式で指定します。 |
| `total` | 整数 | その日のAPI エラーの合計数です。 |
| `errors` | 配列 | その日のエラーコード数のリスト。 |

### エラーオブジェクト

| 名前 | データタイプ | 説明 |
| --- | --- | --- |
| `errorCode` | 文字列 | Marketoのエラーコード |
| `count` | 整数 | その日にエラーが発生した回数。 |

## 注意

API ユーザーはそれぞれ、使用状況レスポンスで個別にレポートされます。 Apiのユーザーを個別に分割することで、割り当てを消費しているサービスやエラーが発生しているサービスを特定しやすくなります。
