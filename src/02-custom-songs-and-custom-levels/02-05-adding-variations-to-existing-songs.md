# 既存楽曲へのバリエーション追加

改造を通じて、既存楽曲に新たなバリエーションを追加することが可能です。これは既存楽曲（他の改造MODの楽曲であっても）に新たな難易度やリミックスを追加するのに最適です。

## 必要ファイルの入手

最初のステップは、楽曲用の新たなリミックスを作曲することです。プレイアブルキャラクター向けリミックスを作成する場合、代替Instを使用するオプションを有効にしたいなら、作曲者が手動で元のボーカルと同期させる必要があります。

次に、このリミックスをチャート化します。完了すると、`Inst.ogg`ファイル、2つの`Voices` OGGファイル、`metadata.json`、`chart.json`が得られるはずです。

## ファイルの配置

次に、MODフォルダ内の適切な場所にアセットを配置します！各ファイル名に任意のバリエーションIDを末尾に追加してリネームしてください（例：erectリミックスを作成する場合、`Inst.ogg`を`Inst-erect.ogg`に変更）：

```
-mods
 |-myMod
   |-data
     |-songs
       |-mychart
         |-mychart-metadata-erect.json
         |-mychart-chart-erect.json
   |-songs
     |-mychart
       |-Inst-erect.ogg
       |-Voices-bf-erect.ogg
       |-Voices-pico-erect.ogg
   |-_polymod_meta.json
```

## JSONデータへのバリエーション登録

各チャートには`songVariations`配列が含まれており、これによりゲームは楽曲がどのバリエーションに対応しているかを認識し、それぞれのメタデータファイルを問い合わせることができます。ゲームにカスタムバリエーションを読み込ませるには、その楽曲のチャートの`metadata.json`ファイルを修正し、そのバリエーションが存在することをゲームに認識させる必要があります。

### 楽曲が自作MODの場合

リミックスを追加するベース楽曲が自作MODの場合、そのチャートの`metadata.json`にバリエーションを追加するだけで済みます。

`playData.songVariations`配列にバリエーションIDを追加します（キーが存在しない場合は作成してください）。

```json
{
    "playData": {
        "songVariations": ["erect"] // Add your new variation to this array.
        // ...
    }
    // ...
}
```

### 楽曲がベースゲームまたは別のMODからの場合

追加対象のベース楽曲が別のMODからのものである場合、変更される可能性のある基盤データを上書きすべきではありません。代わりに、ファイルにJSONパッチを適用する必要があります（Polymodはこの機能を提供します）。

MODフォルダ内に`_merge`フォルダを作成し、その中にパッチを適用したいファイルのパスに一致するディレクトリを作成します。例：

```
-mods
 |-myMod
   |-_merge
     |-data
       |-songs
         |-mychart
           |-mychart-metadata.json
```

次に、`playData.songVariations`配列に新しい値を追加する簡単なパッチを適用します。JSONファイルを編集し、以下の内容を追加してください：

```json
[
    { "op": "add", "path": "/playData/songVariations/-", "value": "erect" } // Add a new value erect to the end of the songVariations array.
]
```

パッチングシステムは非常に柔軟です。あらゆるJSONファイル（基本ゲームまたは他のMODが提供するファイル）に対応し、高度な動作をサポートしています。詳細は[ファイルの結合](../10-appending-and-merging-files/10-02-merging-files.md)を参照してください。

## まとめ

これでゲームを起動すると、追加したバリエーションがゲーム内で利用可能になっているはずです！

キャラクターリミックスを作成した場合、そのリミックス用プレイヤーキャラクターがカスタムプレイアブルキャラクターの`ownedCharacters`データに含まれていることを確認してください。詳細は[カスタムプレイアブルキャラクター](../05-custom-playable-characters/05-00-custom-playable-characters.md)を参照してください。
