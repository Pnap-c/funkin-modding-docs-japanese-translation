# 既存のステッカーパックの修正

[JSONPatch](../10-appending-and-merging-files/10-02-merging-files.md) 機能を使用して、既存のステッカーパックからステッカーを追加または削除できます。

例えば、ボーイフレンドの標準ステッカーパックに追加するには、以下のJSON Patchファイルを使用できます（`mods/mymod/_merge/data/stickerpacks/standard-bf.json`に配置。別のステッカーパックをパッチする場合は異なるファイルパスを使用してください）：

```jsonc
[
    // Add an asset path to the end of the sticker list.
    { "op": "add", "path": "/stickers/-", "value": "path/to/custom/sticker" }
]
```
