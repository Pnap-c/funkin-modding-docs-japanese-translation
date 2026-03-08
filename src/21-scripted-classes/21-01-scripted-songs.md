# Friday Night Funkin' MODの作成 - スクリプト付き楽曲

この章では、楽曲にスクリプトを追加する手順を解説し、この機能で実装可能なカスタム動作の例を示します。

まず、スクリプト付きクラスファイルを `.hxc` 拡張子で作成します（整理したい場合は `mods/mymod/scripts/songs` 内に配置してください）。

```haxe
// Remember to import each class you want to reference in your script!
import funkin.play.song.Song;

// Choose a name for your scripted class that will be unique, and make sure to specifically extend the Song class.
// This class's functions will override the default behavior for the song.
class BallisticSong extends Song {
	public function new() {
        // The constructor gets called once, when the game loads.
        // The constructor takes one parameter, which is the song ID for the song you are applying the script to.
		super('ballistic');
	}

    // Add override functions here!
}
```

その後、カスタム動作を実行するためのオーバーライド関数を追加できます。
