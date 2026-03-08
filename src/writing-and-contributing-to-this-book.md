# この本の執筆と貢献について
本書はMarkdown形式で記述され、[mdbook](https://rust-lang.github.io/mdBook/)を用いて生成されています。

本書の生成元となるソースファイルは[GitHub](https://github.com/FunkinCrew/funkin-modding-docs)で公開されています。

## 考慮すべき点

- ディレクトリパスの説明をどう扱うべきか？ソースコードでは一部の
アセットがライブラリ（`preload/`、`songs`、`shared`など）に分割されていますが、
モッディングを行うほとんどの人は、ソースコード版のアセットパスを
気にする必要はありません。
- 現在、[第10章: ファイルの追加とマージ](10-appending-and-merging-files/10-00-appending-and-merging-files.md) が「第5章」と表示される問題

### スタイルガイド

#### フォルダ/章の構造

[SUMMARY.md](SUMMARY.md) は、`mdbook` がすべてのマークダウンファイルから章や小見出しを生成するための基盤です。このファイルでは、書籍の内容がどのように構成されているかを確認できます。

フォルダ構造はコンテンツの順序とは完全に独立しているため、[SUMMARY.md](SUMMARY.md)が正しいファイルを指している限り、自由に整理できます。

フォルダ名は`{章番号}-{章タイトル}`とする必要があります。`章タイトル`が長くなる場合でも、基本的にこの形式に従ってください。
このガイドのソースから：
```shell
src/
    01-fundamentals/
    02-custom-songs-and-custom-levels/
    03-custom-characters/
    ... // and so on...
```

メインの章ページは、章のフォルダ内で `{chapter number}-00-{chapter title}.md` であるべきです。
このガイドのソースから：
```shell
src/
    01-fundamentals/
        01-00-fundamentals.md
        ...

    02-custom-songs-and-custom-levels/
        02-00-custom-songs-and-custom-levels.md
        ...
    ...
```

その後、各サブチャプターは `{chapter number}-{sub-chapter number}-{subchapter title}.md` の形式に従うべきです。
このガイドのソースから：
```shell
src/
    01-fundamentals/
        01-00-fundamentals.md
        01-01-the-metadata-file.md
        01-02-loading-the-mod-in-game.md
        ...

    02-custom-songs-and-custom-levels/
        02-00-custom-songs-and-custom-levels.md
        02-01-creating-a-chart.md
        02-02-adding-the-custom-song.md
        02-03-adding-a-custom-level.md
    03-custom-characters/
        03-00-custom-characters.md
        03-01-character-assets.md
        ...
    ...
```




