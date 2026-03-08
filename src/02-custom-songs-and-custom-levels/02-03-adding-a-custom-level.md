# カスタムレベルの追加

modsフォルダ内の`data/levels/`ディレクトリに、任意の内部名で新しいファイルを追加します。ファイル拡張子は`.json`にしてください。

*注意*: 内部名がベースゲームの週名や他のMODと重複すると、互いに干渉し予期せぬ結果を招く可能性がありますのでご注意ください！

最終的には以下のような構成になります。

```
-mods
 |-myMod
   |-data
     |-levels
       |-myweek.json
     |-songs
       |-mychart
         |-mychart-metadata.json
         |-mychart-chart.json
   |-songs
     |-mychart
       |-Inst.ogg
       |-Voices-bf.ogg
       |-Voices-pico.ogg
   |-images
     |-storymenu
       |-titles
         |-myweek.png
   |-_polymod_meta.json
```

カスタムウィークのJSONファイルは、以下のような形式になります：

```json
{
  "version": "1.0.0",
  "name": "MY CUSTOM WEEK",
  "titleAsset": "storymenu/titles/myweek",
  "background": "#F9CF51",
  "songs": ["mychart"],
  "visible": true,
  "props": [
    {
      "assetPath": "storymenu/props/dad",
      "scale": 1.0,
      "offsets": [100, 60],
      "animations": [
        {
          "name": "idle",
          "prefix": "idle0",
          "frameRate": 24
        }
      ]
    },
    {
      "assetPath": "storymenu/props/bf",
      "scale": 1.0,
      "offsets": [150, 80],
      "animations": [
        {
          "name": "idle",
          "prefix": "idle0",
          "frameRate": 24
        },
        {
          "name": "confirm",
          "prefix": "confirm0",
          "frameRate": 24
        }
      ]
    }
  ]
}
```

ここには多くの情報があります！一つずつ見ていきましょう：

- `version`: レベルデータファイル形式のバージョン番号。`1.0.0` のままにしておいてください。
- `name`: ストーリーメニューの右上に表示される、レベルの見やすい名前。
- `titleAsset`: レベル一覧でレベル名として使用するアセット。MODフォルダ内の `images` フォルダからの相対パスで指定します。
- `background`: レベルで使用する背景色。`#F9CF51`がクラシックな黄色ですが、このフィールドにはカラーコードか画像ファイルパス（MODフォルダ内の`images`フォルダからの相対パス）のいずれかを指定します。
- `songs`: 週に含める楽曲IDのリスト。
- `visible`: ストーリーメニューにこのストーリーレベルを表示するかどうか。
- `props`: レベル選択時にストーリーメニューに表示するプロップのデータ。例：第1週では「最愛のパパ」「彼氏」「彼女」が表示される。

ゲーム起動時、`data/levels`フォルダ内のJSONファイルを検索して利用可能なレベル一覧を取得し、ストーリーメニューとフリープレイメニューに反映します（アルファベット順以外の表示では、フリープレイの楽曲は収録されているレベル順に表示されます）。

カスタム楽曲をフリープレイ専用に表示させたい場合は、カスタム週を作成し`visible`プロパティをfalseに設定するだけで、楽曲がフリープレイに表示されます！
