# ファイルへの追加

データファイルの末尾に値を追加するのは比較的簡単ですが、追加対象のファイルタイプによって異なります。

追加対象ファイルのパスに一致するパスで、MODの`_append`フォルダ内に新規ファイルを作成します。例えば`assets/data/introText.txt`に追加する場合、ファイルは`mods/mymod/_append/data/introText.txt`に配置します。

### TXTファイルへの追加

追加ファイルの拡張子が`.txt`の場合、ファイルの内容は単純に対象ファイルの末尾に追加されます。

### CSV/TSVファイルへの追加

追加ファイルの拡張子が`.csv`または`.tsv`の場合、シート内の行が対象シートの末尾に追加されます。

### XMLファイルへの追加

TODO: 内容を記入してください。

### JSONファイルへの追加

追加対象ファイルの拡張子が `.json` の場合、値が解析され、単純にターゲットデータに追加されます。

例：ソースファイル `data/mydata.json` がある場合：

```json
{
  "test1": [1, 2, 3],
  "test2": {
    "foo": "bar"
  },
  "test3": "baz"
}
```

ファイル `mods/mymod/_append/data/mydata.json` を提供できます:

```json
{
  "test4": "hello",
  "test2": {
    "fizz": "buzz"
  }
}
```

そしてPolymodはこれを変化させて、この結果を得ます：

```jsonc
{
  // Unreferenced values are untouched.
  "test1": [1, 2, 3],
  // Included values are placed in directly, not merged!
  "test2": {
    "fizz": "buzz"
  },
  "test3": "baz",
  // New values are simply included.
  "test4": "hello"
}
```

より具体的な方法が必要な場合は、より強力で柔軟なアプローチとして[JSONファイルへのマージ](./10-02-merging-files.md#merging-into-json-files)を参照してください。
