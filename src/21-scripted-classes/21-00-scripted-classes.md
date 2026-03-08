# スクリプト化クラス

Funkin の HScript 実装では、スクリプトクラスシステムを採用しています。スクリプトクラスを作成するには、`mods/mymod/scripts/` フォルダ内に `.hxc` ファイルを作成し、Haxe 構文を用いて、スクリプト化するオブジェクトのタイプに対応する基底クラスを継承する新しいクラスを作成します。例えば以下のように記述します：

```haxe
// Remember to import each class you want to reference in your script!
import funkin.play.song.Song;

// Choose a name for your scripted class that will be unique
// Also specify the class you are extending, we choose Song here.
// This script's behaviors will extend the default behavior of the song.
class BallisticSong extends Song {
	public function new() {
        // You have to call the super constructor for the class you are extending, which may have different parameters.
        // Check the specific documentation for more info.
		super('ballistic');
	}
}
```

## スクリプト対応クラスのリスト

ゲーム内でスクリプト対応として設定済みのクラスは事前に定義されたリストが存在し、関連する場面で自動的に読み込まれ実行されます。今後さらに追加される予定です。

- `funkin.play.song.Song`：カスタム楽曲に独自の動作（カットシーン再生など）を提供するクラス。詳細は[スクリプト楽曲](21-scripted-classes/21-01-scripted-songs.md)を参照。
    - 関連項目：[動画カットシーン](21-scripted-classes/21-03-video-cutscenes.md)、 [ゲーム内カットシーン](21-scripted-classes/21-04-ingame-cutscenes.md)、および[会話カットシーン](21-scripted-classes/21-05-dialogue-cutscenes.md)
- `funkin.play.character.BaseCharacter`：カスタムキャラクターに固有の動作（特定の状況でのカスタムアニメーション再生など）を提供します。[Scripted Characters](21-scripted-classes/21-05-scripted-characters.md)を参照してください。
    - キャラクターのアニメーションタイプに合ったこのクラスの正しいサブクラスを選択する必要があることに注意してください！
	- `funkin.play.character.SparrowCharacter` は、Sparrow スプライトシートアニメーションを持つキャラクターに使用されます。
    - `funkin.play.character.MultiSparrowCharacter` は、複数の Sparrow スプライトシートアニメーションを組み合わせて1つのキャラクターを作成する場合に使用されます。
    - `funkin.play.character.PackerCharacter` は、Packer スプライトシートアニメーションを持つキャラクターに使用されます。
	- `funkin.play.character.AnimateAtlasCharacter` は、Adobe Animate テクスチャアトラスを持つキャラクターに使用します。
    - `funkin.play.character.BaseCharacter` は、すべてのレンダリングおよびアニメーションハンドラ用の空のスタブを持ち、キャラクターのアニメーションシステムを手作業で再実装したい場合にのみ有用です。
- `funkin.play.stage.Stage`：カスタムステージに独自の動作を提供します。カスタム移動プロップの作成や、プロップのアニメーションタイミング、ステージと同期した効果音の再生タイミングの定義などが可能です。詳細は[スクリプトステージ](21-scripted-classes/24-06-scripted-stages.md)を参照してください。
- `funkin.ui.story.Level`：ストーリーモードのレベルに独自の動作を提供します。詳細は[スクリプト化されたストーリーレベル](21-scripted-classes/25-07-scripted-story-levels.md)を参照してください。
- `funkin.play.notes.notekind.NoteKind`：特定の種類のノートに独自のビジュアルと動作を提供し、チャートエディタに配置できるようにします。詳細は[カスタムノート種類](21-scripted-classes/26-00-custom-note-kinds.md)を参照してください。
- `funkin.play.event.SongEvent`：カスタムソングイベントを作成します。チャートエディタに配置でき、到達時にゲームアクションを実行します。詳細は[カスタムソングイベント](21-scripted-classes/28-00-custom-note-kinds.md)を参照してください。
- `funkin.ui.freeplay.charselect.PlayableCharacter`：カスタムプレイアブルキャラクターに独自の動作を提供します。詳細は[スクリプト対応プレイアブルキャラクター](21-scripted-classes/25-10-scripted-playable-characters.md)を参照
- `funkin.ui.freeplay.FreeplayStyle`：特定のキャラクターが選択された際にフリープレイメニューで使用されるスプライトと色を定義します。詳細は[WIP](21-scripted-classes/25-10-freeplay-style.md)を参照
- `funkin.play.notes.notestyle.NoteStyle`：カスタムノートスタイルの動作を変更します。[WIP]を参照
- `funkin.play.cutscene.dialogue.Conversation`：カスタム対話シーンに独自の動作を提供します。[対話カットシーン](21-scripted-classes/21-05-dialogue-cutscenes.md)を参照
- `funkin.play.cutscene.dialogue.DialogueBox`：会話で使用されるカスタムダイアログボックスに独自の動作を提供します。[ダイアログカットシーン](21-scripted-classes/21-05-dialogue-cutscenes.md)を参照
- `funkin.play.cutscene.dialogue.Speaker`：会話で使用されるカスタムスピーカーに独自の動作を提供します。詳細は[ダイアログカットシーン](21-scripted-classes/21-05-dialogue-cutscenes.md)を参照
- `funkin.ui.freeplay.Album`：フリープレイアルバムのカスタム動作を定義します。詳細は[WIP](21-scripted-classes/21-05-freeplay.ui.album.WIP.md)を参照

カスタムスクリプトモジュール用の`funkin.modding.module.Module`も存在します。これは特定のコンテキスト内だけでなく、あらゆる場所でイベントを受信するスクリプトです。これらの動作の詳細については[スクリプトモジュール](30-scripted-modules/30-00-scripted-modules.md)を参照してください。

スクリプト化可能なクラスも用意されていますが、他のスクリプトからアクセスされる場合にのみ有用です。今後さらに追加される予定です。

- `funkin.graphics.FunkinSprite`：基本的な静的またはアニメーション付きスプライト用。
- `funkin.graphics.adobeanimate.FlxAtlasSprite`：Adobe Animateのテクスチャアトラスを使用する汎用スプライト用
- `flixel.group.FlxSpriteGroup`：ステート内に含まれ一括操作されるスプライト群用
- `funkin.ui.MusicBeatState`：特定のゲーム状態を表すスプライト群用。スクリプトイベント処理用の追加ユーティリティを含む
- `funkin.ui.MusicBeatSubState`：既存状態のサブ状態を表すスプライト群用
- `flixel.addons.display.FlxRuntimeShader`：カスタムGLSLシェーダー用
- `funkin.play.stage.Bopper`：ステージの一部として音楽のリズムに合わせてアイドルアニメーションを再生するスプライト用
- `flixel.FlxSprite`：基本的な静的またはアニメーション付きスプライト用。FunkinSpriteが使用できない場合のみ使用してください。
- `flixel.FlxState`：特定のゲーム状態を表す基本的なスプライトグループ用。MusicBeatStateが使用できない場合のみ使用してください。
- `flixel.FlxSubState`：既存の状態のサブ状態を表すスプライトグループ用
