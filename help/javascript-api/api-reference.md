---
title: Munchkin API リファレンス
description: Munchkin JavaScript API を使用して、Munchkin データをカスタマイズします。
feature: Munchkin Tracking Code, Javascript
exl-id: e9727691-5501-4223-bc98-2b4bacc33513
source-git-commit: 1ad2d793832d882bb32ebf7ef1ecd4148a6ef8d5
workflow-type: ht
source-wordcount: '414'
ht-degree: 100%

---

# Munchkin API リファレンス

Munchkin は、JavaScript を通じて手動で呼び出すことができるいくつかの関数を提供します。これにより、ビデオの再生やリンク以外のクリックなどのブラウザーイベントのカスタマイズされたトラッキングが可能になります。

## 関数

Munchkin API は、`init`、`createTrackingCookie`、`munchkinFunction` の各関数で構成されています。

<a name="munchkin_init"></a>

### Munchkin.init()

`Munchkin.init()` は、他の関数の前に呼び出す必要があります。現在のページで Munchkin を設定して、特定のインスタンスにアクティビティを送信し、現在のページの「Web ページを訪問」アクティビティを生成します。

| パラメーター名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| Munchkin ID | 必須 | 文字列 | Munchkin アカウント ID は、管理／統合／Munchkin メニューにあります。アクティビティの送信先のターゲットインスタンスを設定します。 |
| [設定](configuration.md) | オプション | オブジェクト | Munchkin の代替動作設定を有効にします。 |

```javascript
Munchkin.init('299-BYM-827');
```

### Munchkin.createTrackingCookie()

呼び出されると、ブラウザーに `_mkto_trk` cookie が存在するかどうかが確認され、存在しない場合は作成されます。これは、`cookieAnon` が false に設定されている場合、登録やアセットのダウンロードなどの特定のアクション中のユーザのトラッキングに役立ちます。

| パラメーター名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| forceCreate | 必須 | ブール値 | `cookieAnon` が false に設定されている場合でも、cookie を作成します。 |


```javascript
Munchkin.createTrackingCookie(true);
```

### Munchkin.munchkinFunction()

ビデオプレーヤーの再生と一時停止、ハッシュコードなどの標準以外のナビゲーションのページ訪問などのカスタムトラッキング動作を生成するのに使用されます。

| パラメーター名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| 関数のタイプ | 必須 | 文字列 | 記録するアクティビティを決定します。許容値：`visitWebPage`、`clickLink`、`associateLead` |
| データ | 必須 | オブジェクト | 記録するアクティビティのデータが含まれます。 |

#### visitWebPage

`visitWebPage` で `munchkinFunction()` を呼び出すと、現在のユーザの「訪問」アクティビティが Marketo に送信されます。2 番目の引数のデータオブジェクトと共に送信される URL と `querystring` をカスタマイズできます。

| データプロパティ名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| URL | 必須 | 文字列 | ページ訪問の記録に使用する URL ファイルパス。この値は、現在のドメイン名に追加され、完全なページ名が作成されます。例えば、URL が `/index.html` で、ドメイン名が `www.example.com` の場合、訪問したページは `www.example.com/index.html` として記録されます。 |
| params | オプション | 文字列 | 記録する目的のパラメーターのクエリ文字列。 |

例：`foo=bar&biz=baz`。

```javascript
Munchkin.munchkinFunction('visitWebPage', {
        'url': '/Football/Team/Seahawks',
        'params': 'defense=legion_of_boom&qb=wilson'
    }
);
```

#### clickLink

`clickLink` で `munchkinFunction()` を呼び出すと、現在のユーザのクリックアクティビティが Marketo に送信されます。データオブジェクトの `href` プロパティを使用してクリック URL をカスタマイズできます。

| データプロパティ名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| href | 必須 | 文字列 | リンククリックの記録に使用する URL ファイルパス。この値は、現在のドメイン名に追加され、完全なリンクが作成されます。 |

例えば、href が `/index.html` で、ドメイン名が `www.example.com` の場合、リンククリックは `www.example.com/index.html` として記録されます。

```javascript
Munchkin.munchkinFunction('clickLink', {
        'href': '/Football/Team/Seahawks'
    }
);
```

#### associateLead

このメソッドは非推奨（廃止予定）となり、使用できなくなりました。
