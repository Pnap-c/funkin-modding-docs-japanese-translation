# マージ

ファイルをデータファイルにマージすることは、より複雑な操作（ドキュメントの先頭以外へのデータ挿入、特定のデータを新しいデータで置き換え、あるいはドキュメントから特定のデータを削除するなど）を行うために必要です。

データファイル全体を置き換える代わりに`_merge`ファイルを使用することで、ベースゲームの変更や他のMODによる変更とも完全に互換性を保てます。マージファイルはMODのロード順序で適用されるため、複数のMODが同じファイルに変更を加えても競合は発生しません！

### TXTファイルへのマージ
**TODO**

### CSV/TSVファイルへのマージ

CSVおよびTSVファイルもマージ可能です。この場合、MODローダーはベースファイル内の行をスキャンし、マージファイルの行と最初のセルの値が一致する行を検出すると、それらをマージファイルの行で置き換えます。

### XMLファイルへのマージ

*注意: XMLファイルのマージ動作は近い将来大幅に変わる可能性があります。*

XMLの場合、挿入位置をPolymodに指示する追加情報と共に、必要な値を含むXMLドキュメントを作成する必要があります。

例えば、`data/stuff.xml`に多数のノードを含む複雑なXMLファイルがあるとします:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<data>
   <!--lots of complicated stuff-->
   <mode id="difficulty" values="easy"/>
   <!--even more complicated stuff-->
</data>
```

代わりにこう表示してほしい:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<data>
   <!--lots of complicated stuff-->
   <mode id="difficulty" values="super_hard"/>
   <!--even more complicated stuff-->
</data>
```

基本的に、このタグを次のものから変更したいのです：

```xml
<mode id="difficulty" values="easy"/>
```

→これを
```xml
<mode id="difficulty" values="super_hard"/>
```

これは`<modroot>/<mergeFolder>/data/stuff.xml`に配置するファイルです：
```xml
<?xml version="1.0" encoding="utf-8" ?>
<data>
    <mode id="difficulty" values="super_hard">
        <merge key="id" value="difficulty"/>
    </mode>
</data>
```

このファイルにはデータとマージ指示の両方が含まれています。`<merge>`の子タグはMODローダーに何をすべきかを指示するもので、最終データには含まれません。実際のペイロードは次の通りです：

```xml
<mode id="difficulty" values="super_hard">
```

`<merge>`タグは、MODローダーに以下の指示を与えます：

* 親タグ（この場合は`<mode>`）と同じ名前のタグを探す
* 該当タグ内で`key`属性（この場合は`「id」`という名前のもの）を探す
* キーの値が探している値（この場合は`「difficulty」`）と一致するか確認する

最初の一致が見つかり次第、検索を停止し、ペイロードを指定されたタグにマージします。属性はすべてベースタグに追加され（同名の既存属性は上書きされます。この例では値が「easy」から「super_hard」に変更されます）、これが目的です。さらに、ペイロードに子ノードがある場合、そのすべての子ノードもターゲットタグにマージされます。

### JSONファイルへのマージ

JSONファイルへのマージは[JSON Patch](https://jsonpatch.com/)ドキュメントを用いて行います（注：これはv0.4.1以前のバージョン向けに作成されたJSONパッチファイルとは大きく異なります。以前のシステムは正直言ってあまり良くありませんでした）。

以下のようなJSONデータファイル`data/songs/mysong-metadata.json`があるとします：

```json
{
  "version": "2.1.0",
  "playData": {
    "characters": {
      "player": "bf",
      "opponent": "dad"
    },
    "difficulties": [
      "easy", "normal", "hard"
    ],
    "garbageValue": 37,
    "stage": "mainStage"
  }
}
```

上記のデータは、ドキュメント `mods/mymod/_merge/data/songs/mysong-metadata.json` で変更できます：

```jsonc
[
  { "op": "replace", "path": "/playData/characters/opponent", "value": "monster" }, // Replace the value of opponent with monster.
  { "op": "add", "path": "/playData/characters/girlfriend", "value": "nene" }, // Add a new key girlfriend with the value Nene.
  { "op": "add", "path": "/playData/difficulties/1", "value": "funky" }, // Add a new value funky to the difficulty array, after easy
  { "op": "add", "path": "/playData/difficulties/-", "value": "expert" }, // Add a new value expert to the end of the difficulty array.
  { "op": "remove", "path": "/playData/garbageValue" }, // Remove the key garbageValue from the data entirely
  { "op": "test", "path": "/playData/garbageValue", "value": 37 } // Test that a given value is in the JSON. If this operation fails, the patches will be rejected.
]
```

サポートされている操作は、`add`、`remove`、`replace`、`move`、`copy`、および`test`です。JSON Patchドキュメント内のいずれかの操作が失敗した場合、そのファイル内のすべての変更は元に戻されます。

`add`、`replace`、`test`操作には`value`キー（配列やオブジェクトを含む任意のJSONデータ）が必要であり、`move`および`copy`操作には`from`キー（移動またはコピー元のパス値を示す）が必要です。

`path` は、スラッシュ (`/`) で始まり、スラッシュで区切られたプロパティ名または配列インデックス (0 から始まる) の文字列でなければなりません。例: `/playData/characters/opponent`。

`path`はJSONPath文字列としても指定可能で、フィルタリングロジックをサポートした堅牢なターゲットパス指定が可能です。詳細は以下を参照してください：https://goessner.net/articles/JsonPath/
