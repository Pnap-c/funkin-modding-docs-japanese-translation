# カスタム曲の追加

[チャートの作成](02-01-creating-a-chart.md) の最後で、`.fnfc`ファイルは単なる`.zip`アーカイブであることを学びました。そのため、ファイル名を変更して解凍するだけで済みます。これらのファイルを入手したら、MODフォルダ内の適切な場所に配置するだけです！

- `manifest.json`ファイルは不要です。当MODでは使用しません。
- `metadata.json`と`chart.json`ファイルは`data/songs/<songid>`フォルダに配置します。`<songid>`は楽曲の内部IDに置き換えてください。
- OGGファイルは`songs/<songid>`フォルダに配置します。ここでも`<songid>`を楽曲の内部名に置き換えてください。

最終的には以下のような構成になります。

```
-mods
 |-myMod
   |-data
     |-songs
       |-mychart
         |-mychart-metadata.json
         |-mychart-chart.json
   |-songs
     |-mychart
       |-Inst.ogg
       |-Voices-bf.ogg
       |-Voices-pico.ogg
   |-_polymod_meta.json
```

ゲーム起動時、`data/songs`フォルダ内の`<songid>/<songid>-metadata.json`ファイルを検索して利用可能な楽曲リストを取得し、チャートファイルと必要な楽曲ファイルを特定します。素晴らしい仕組みですね！しかし現状、ゲームを起動しても何も動作しません。ログにはエラーなく記載されているものの、ストーリーモードやフリープレイで再生できません。なぜでしょうか？

```
source/funkin/play/song/Song.hx:579: Fetching song metadata for mychart
source/funkin/data/song/SongRegistry.hx:103:   Loaded entry data: Song(mychart)
```

修正は簡単です。すべての楽曲は、フリープレイに表示されるためにはストーリーモードのレベルの一部でなければなりません。