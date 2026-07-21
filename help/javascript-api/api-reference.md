---
title: Munchkin API リファレンス
description: Munchkin Javascript APIを使用して、init メソッド、createTrackingCookie メソッド、munchkinFunction メソッドを使用して、ページ訪問、リンククリック、カスタムイベントを追跡します。
feature: Munchkin Tracking Code, Javascript
exl-id: e9727691-5501-4223-bc98-2b4bacc33513
TQID: https://experienceleague.adobe.com/s97x6wVZijnnxZwS7HMIkQAKlxXkcfPXuSZG4KjXGoc
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 414
ht-degree: 66%

---

# Munchkin API リファレンス

Munchkinには、ブラウザーイベントのトラッキングをカスタマイズするためのJavaScript機能が用意されています。 例えば、リンク以外の要素に対するビデオの再生またはクリックを追跡できます。

## 関数

Munchkin APIには、次の関数が含まれています。

- `init`
- `createTrackingCookie`
- `munchkinFunction`

<a name="munchkin_init"></a>

### Munchkin.init()

`Munchkin.init()` は、他の関数の前に呼び出す必要があります。 現在のページで Munchkin を設定して、特定のインスタンスにアクティビティを送信し、現在のページの「Web ページを訪問」アクティビティを生成します。

| パラメーター名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| Munchkin ID | 必須 | 文字列 | Munchkin アカウント ID は、管理／統合／Munchkin メニューにあります。 アクティビティの送信先のターゲットインスタンスを設定します。 |
| [設定](configuration.md) | オプション | オブジェクト | Munchkin の代替動作設定を有効にします。 |

```javascript
Munchkin.init('299-BYM-827');
```

### Munchkin.createTrackingCookie()

`Munchkin.createTrackingCookie()`は、`_mkto_trk` Cookieがブラウザーに存在するかどうかを確認します。 Cookieが存在しない場合、関数は1つを作成します。

`cookieAnon`がfalseに設定されている場合、この関数を使用して、アセットの登録やダウンロードなどの特定のアクション中にユーザーを追跡します。

| パラメーター名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| forceCreate | 必須 | ブール値 | `cookieAnon` が false に設定されている場合でも、cookie を作成します。 |

```javascript
Munchkin.createTrackingCookie(true);
```

### Munchkin.munchkinFunction()

`Munchkin.munchkinFunction()`を使用してカスタム トラッキング動作を作成します。 例えば、ハッシュ変更などの非標準ナビゲーションからビデオプレーヤーのアクティビティやページ訪問を追跡できます。

| パラメーター名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| 関数のタイプ | 必須 | 文字列 | 記録するアクティビティを決定します。 許容値：`visitWebPage`、`clickLink`、`associateLead` |
| データ | 必須 | オブジェクト | 記録するアクティビティのデータが含まれます。 |

#### visitWebPage

`visitWebPage` で `munchkinFunction()` を呼び出すと、現在のユーザの「訪問」アクティビティが Marketo に送信されます。 2番目の引数のデータオブジェクトを使用して、URLと`querystring`をカスタマイズします。

| データプロパティ名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| URL | 必須 | 文字列 | ページ訪問の記録に使用する URL ファイルパス。  この値は、現在のドメイン名に追加され、完全なページ名が作成されます。 例えば、URL が `/index.html` で、ドメイン名が `www.example.com` の場合、訪問したページは `www.example.com/index.html` として記録されます。 |
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

`clickLink` で `munchkinFunction()` を呼び出すと、現在のユーザのクリックアクティビティが Marketo に送信されます。 データオブジェクトの`href` プロパティを使用して、クリック URLをカスタマイズします。

| データプロパティ名 | オプション／必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| href | 必須 | 文字列 | リンククリックの記録に使用する URL ファイルパス。 この値は、現在のドメイン名に追加され、完全なリンクが作成されます。 |

例えば、href が `/index.html` で、ドメイン名が `www.example.com` の場合、リンククリックは `www.example.com/index.html` として記録されます。

```javascript
Munchkin.munchkinFunction('clickLink', {
        'href': '/Football/Team/Seahawks'
    }
);
```

#### associateLead

このメソッドは非推奨（廃止予定）となり、使用できなくなりました。
