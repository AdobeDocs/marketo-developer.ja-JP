---
title: Munchkin API リファレンス
description: Munchkin JavaScript API を使用して、Munchkin データをカスタマイズします。
feature: Javascript
source-git-commit: c6c0a492ede415471e10efb6213eb3f590e63ebe
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 9%

---


# Munchkin API リファレンス

Munchkin は、JavaScript を使用して手動で呼び出すことができるいくつかの関数を提供しています。 これにより、ビデオ再生やリンク以外のクリックなど、ブラウザーイベントのトラッキングをカスタマイズできます。

## 関数

Munchkin API は、`init`、`createTrackingCookie`、`munchkinFunction` の関数で構成されています。

### Munchkin.init()

`Munchkin.init()` は、他の関数の前に呼び出す必要があります。 現在のページに Munchkin を設定して、特定のインスタンスにアクティビティを送信し、現在のページの「訪問 Web ページ」アクティビティを生成します。

| パラメータ名 | オプション/必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| Munchkin ID | 必須 | 文字列 | Munchkin アカウント ID は、管理者/統合/Munchkin メニューにあります。 アクティビティの送信先のターゲットインスタンスを設定します。 |
| [ 設定 ](configuration.md) | オプション | オブジェクト | Munchkin の代替動作設定を有効にします。 |

```javascript
Munchkin.init('299-BYM-827');
```

### Munchkin.createTrackingCookie()

呼び出されると、ブラウザーに `_mkto_trk` しい Cookie が存在するかが確認され、存在しない場合は作成されます。 `cookieAnon` が false に設定されている場合、登録やアセットのダウンロードなど、特定のアクション中にユーザーを追跡するのに役立ちます。

| パラメータ名 | オプション/必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| forceCreate | 必須 | ブール値 | `cookieAnon` が false に設定されている場合でも、cookie を作成します。 |


```javascript
Munchkin.createTrackingCookie(true);
```

### Munchkin.munchkinFunction()

ビデオプレーヤーの再生と一時停止などのカスタムトラッキング動作の生成や、非標準ナビゲーションのページ訪問（ハッシュコードなど）の生成に使用します。

| パラメータ名 | オプション/必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| 関数のタイプ | 必須 | 文字列 | 記録するアクティビティを決定します。 指定可能な値：`visitWebPage`、`clickLink`、`associateLead` |
| データ | 必須 | オブジェクト | 記録されるアクティビティのデータを含みます。 |

#### visitWebPage

`visitWebPage` で `munchkinFunction()` を呼び出すと、現在のユーザーの「訪問」アクティビティがMarketoに送信されます。 2 番目の引数でデータオブジェクトと共に送信される URL と `querystring` をカスタマイズできます。

| データプロパティ名 | オプション/必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| URL | 必須 | 文字列 | ページ訪問の記録に使用される URL ファイルパス。  この値が現在のドメイン名に追加され、完全なページ名が作成されます。 例えば、url が `/index.html` でドメイン名が `www.example.com` の場合、訪問したページは `www.example.com/index.html` として記録されます。 |
| params | オプション | 文字列 | 記録する必要のあるパラメーターのクエリ文字列。 |

例：`foo=bar&biz=baz`。

```javascript
Munchkin.munchkinFunction('visitWebPage', {
        'url': '/Football/Team/Seahawks',
        'params': 'defense=legion_of_boom&qb=wilson'
    }
);
```

#### clickLink

`clickLink` で `munchkinFunction()` を呼び出すと、現在のユーザーのクリックアクティビティがMarketoに送信されます。 クリック URL は、データオブジェクトの `href` プロパティでカスタマイズできます。

| データプロパティ名 | オプション/必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| href | 必須 | 文字列 | リンククリックを記録するために使用される URL ファイルパス。 この値は、フルリンクを作成するために現在のドメイン名に追加されます。 |

例えば、href が `/index.html` でドメイン名が `www.example.com` の場合、リンククリックが `www.example.com/index.html` として記録されます。

```javascript
Munchkin.munchkinFunction('clickLink', {
        'href': '/Football/Team/Seahawks'
    }
);
```

#### associateLead

このメソッドは非推奨となり、使用できなくなりました。
