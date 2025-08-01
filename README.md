---
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 100%

---
# 記事の投稿

アドビでは、コミュニティに加え、ドキュメントチーム以外のアドビ従業員からの投稿も歓迎します。

## アドビオープンソース行動規範

このプロジェクトでは、[アドビオープンソース行動規範](code-of-conduct.md)または [.NET Foundation 行動規範](https://dotnetfoundation.org/code-of-conduct)を採用しています。詳しくは、[投稿](contributing.md)の記事を参照してください。

## アドビコンテンツへの投稿方法

**アドビスタッフでない場合**&#x200B;は、外部からのコミュニティ投稿を送信できます。コミュニティ投稿は社内システムに読み込まれ、編集されてパブリックリポジトリに結合されます。パブリックリポジトリは、その後、最新の変更内容と同期され、プライベートリポジトリに結合されます。

**アドビスタッフの場合**&#x200B;は、プライベート [Adobe GitHub リポジトリ](https://git.corp.adobe.com/AdobeDocs/)に直接投稿できます。詳しくは、アドビスタッフ向けの Adobe Experience League オーサリングガイドを参照してください。

## 外部コントリビューター

### 軽微な変更

マイナーな更新を投稿しようとしている場合：

1. 編集するトピックに移動します。
1. 「このコンテンツは役に立ちましたか？」バナー（ブラウザーウィンドウの下部に表示される）で、「**詳細フィードバックオプション**」をクリックします。
1. 「**編集を提案**」をクリックし、変更内容を記載したプルリクエスト（PR）を GitHub UI で送信します。

   詳しくは、一般的な[アドビドキュメントのコントリビューターガイド](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=ja)を参照してください。

このリポジトリのドキュメントおよびコード例について送信した軽微な修正または説明には、アドビの利用条件が適用されます。

### コミュニティからの大きな変更または新規トピック

アドビコミュニティのメンバーで、新しいトピックの作成や大きな変更の送信を行う場合は、該当する Git リポジトリの「**Issues**」タブを使用してイシューを送信し、ドキュメントチームとの会話を開始してください。計画が合意されたら、アドビライターと協力してリビジョンを公開します。

**メモ：**&#x200B;ドキュメントやコード例に対する大幅な変更を含んだプルリクエストを送信すると、オンライン投稿ライセンス契約（CLA）を送信するように求めるメッセージがプルリクエストに表示されます。アドビでプルリクエストをレビューできるように、まず、オンラインフォームに記入する必要があります。

### ツール

コミュニティの投稿者は、GitHub UI を使用して、基本的な編集をしたり、リポジトリをフォークしたりして、大きな貢献をすることができます。

詳しくは、[アドビドキュメントのコントリビューターガイド](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=ja)を参照してください。

## 内部コントリビューター

Adobe Experience Cloud ソリューションの製品チームのテクニカルライター、プログラムマネージャーまたは開発者で、技術的な記事に寄稿または作成する場合は、[プライベートリポジトリ](https://git.corp.adobe.com/AdobeDocs)を使用します。

## トピックの形式設定

このリポジトリの記事はすべて GitHub Flavored Markdown（GFM）を使用しています。マークダウンについて詳しくは、次を参照してください。

* [マークダウンの基本](https://help.github.com/ja/articles/getting-started-with-writing-and-formatting-on-github/)
* [印刷用マークダウンチートシート](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## ラベル

パブリックリポジトリでは、アドビがプル要求のワークフローを管理したり、プル要求の状況を投稿者が把握できるようにしたりするために、プル要求に自動ラベルが割り当てられます。

* **Change sent to author**：保留中のプル要求について作成者に通知されました。
* **ready-to-merge**：プル要求レビューチームによるレビューの準備ができました。
