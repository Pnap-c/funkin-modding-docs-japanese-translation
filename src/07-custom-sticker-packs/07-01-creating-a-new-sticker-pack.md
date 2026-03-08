# 新しいステッカーパックの作成

## ステッカーパックのアセット

独自のステッカーパックを作成するには、使用するステッカーのグラフィックが必要です。基本ゲームに含まれるステッカーのサイズは、一般的に300x300ピクセル前後で、多少のばらつきがあります。

## ステッカーパックのデータ

カスタムステッカーパックを作成するには、`data/stickerpacks`フォルダ内に新しいJSONファイルを作成する必要があります。

以下は「デフォルト」ステッカーパックのJSONファイル `assets/data/stickerpacks/default.json`[^stickerpacksource] の例です。

```json
{
  "version": "1.0.0",
  "name": "Default",
  "artist": "PhantomArcade3K",
  "stickers": [
    "transitionSwag/stickers-set-1/bfSticker1",
    "transitionSwag/stickers-set-1/bfSticker2",
    "transitionSwag/stickers-set-1/bfSticker3"
  ]
}
```

すべてを分解してみましょう。
- `version`: ステッカーパックデータファイル形式のバージョン番号。`1.0.0` のままにしておいてください。
  - データファイル形式が変更された場合に増加し、下位互換性のために追加処理が必要かどうかをゲームに伝えます。
- `name`: ステッカーパックの読みやすい名前。チャートエディタなどで使用されます。
- `author`: ステッカーパックの作成者、つまりアセットを作成したアーティスト。
- `stickers`: 使用する全ステッカーのパスを文字列で列挙したリスト。
  - 現時点では、大きさ、位置、テクスチャスムージング、アニメーションなどの追加引数は指定できません。

[^stickerpacksource]: <https://github.com/FunkinCrew/funkin.assets/blob/main/preload/data/stickerpacks/default.json>