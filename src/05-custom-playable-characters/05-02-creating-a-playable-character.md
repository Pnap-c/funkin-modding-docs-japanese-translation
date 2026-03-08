# プレイアブルキャラクターの作成

カスタムプレイアブルキャラクターを作成するには、`data/characters`フォルダ内に新しいJSONファイルを作成する必要があります。以下は、`assets/data/players/pico.json`[^picosource]にあるPicoのキャラクターデータファイルの例です。

```json
{
  "version": "1.0.0",
  "name": "Pico",
  "ownedChars": [
    "pico",
    "pico-playable",
    "pico-blazin",
    "pico-christmas",
    "pico-dark"
  ],
  "showUnownedChars": false,
  "unlocked": true,
  "freeplayStyle": "pico",
  "freeplayDJ": {
    "assetPath": "freeplay/freeplay-pico",
    "text1": "PICO",
    "text2": "GOD DAMN HE DOWN ON THE NUT",
    "text3": "ZEBOIM DAMN IMA NUT",
    "fistPump": {
      "introStartFrame": 0,
      "introEndFrame": 4,

      "loopStartFrame": 4,
      "loopEndFrame": -1,

      "introBadStartFrame": 0,
      "introBadEndFrame": 0,

      "loopBadStartFrame": 0,
      "loopBadEndFrame": -1
    },
    "charSelect": {
      "transitionDelay": 0.45
    },
    "animations": [
      {
        "name": "intro",
        "prefix": "pico dj intro",
        "offsets": [631.7, 362.6]
      },
      {
        "name": "idle",
        "prefix": "Pico DJ",
        "offsets": [625, 360]
      },
      {
        "name": "idleEasterEgg",
        "prefix": "Pico DJ afk",
        "offsets": [625, 360]
      },
      {
        "name": "confirm",
        "prefix": "Pico DJ confirm",
        "offsets": [625, 360]
      },
      {
        "name": "fistPump",
        "prefix": "pico cheer",
        "offsets": [975, 260]
      },
      {
        "name": "loss",
        "prefix": "Pico DJ loss",
        "offsets": [625, 360]
      },
      {
        "name": "charSelect",
        "prefix": "Pico DJ to CS",
        "offsets": [625, 360]
      }
    ]
  },
  "charSelect": {
    "position": 3,
    "gf": {
      "assetPath": "charSelect/neneChill",
      "animInfoPath": "charSelect/neneAnimInfo",
      "visualizer": true
    }
  },
  "results": {
    "music": {
      "PERFECT_GOLD": "resultsPERFECT-pico",
      "PERFECT": "resultsPERFECT-pico",
      "EXCELLENT": "resultsEXCELLENT-pico",
      "GREAT": "resultsNORMAL-pico",
      "GOOD": "resultsNORMAL-pico",
      "SHIT": "resultsSHIT-pico"
    },
    "perfectGold": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsPERFECT",
        "zIndex": 500,
        "scale": 0.88,
        "offsets": [385, 82],
        "loopFrame": 91
      }
    ],
    "perfect": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsPERFECT",
        "zIndex": 500,
        "scale": 0.88,
        "offsets": [385, 82],
        "loopFrame": 91
      }
    ],
    "excellent": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsGREAT",
        "zIndex": 500,
        "scale": 1.25,
        "offsets": [350, 25],
        "looped": true,
        "loopFrame": 32
      }
    ],
    "great": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsGREAT",
        "zIndex": 500,
        "scale": 1.25,
        "offsets": [350, 25],
        "looped": true,
        "loopFrame": 32
      }
    ],
    "good": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsGOOD",
        "zIndex": 500,
        "scale": 1.25,
        "offsets": [350, 25],
        "loopFrame": 41
      }
    ],
    "loss": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsSHIT",
        "zIndex": 500,
        "offsets": [-185, -125],
        "loopFrame": 0
      }
    ]
  }
}
```

利用可能なフィールドは以下の通りです：
- `version`: プレイアブルキャラクターデータファイル形式のバージョン番号。`1.0.0` のままにしておいてください。
- `name`: キャラクターの読みやすい名前（内部で使用）。
- `ownedCharacters`: このキャラクターが所有する[キャラクター](../03-custom-characters/03-00-custom-characters.md) のリスト。
    - フリープレイで表示する楽曲を決定する際、ゲームはこのリストにプレイヤーキャラクターが含まれる楽曲をチェックし、それらを表示します。プレイヤーキャラクターが別の配列に含まれる楽曲は表示されません。
- `showUnownedChars`: この値が `true` の場合、プレイヤーキャラクターがどの `ownedCharacters` リストにも含まれない楽曲がこのキャラクターに表示されます。
- `unlocked`: キャラクターがアンロックされているかどうか。
    - このプレイアブルキャラクター用にスクリプトクラスを作成し、`isUnlocked():Bool` をオーバーライドして条件付きにします。詳細は[スクリプト化されたプレイアブルキャラクター](21-scripted-classes\21-10-scripted-playable-characters.md)を参照してください。
- `freeplayStyle`: 表示するフリープレイスタイルのID。
    - デフォルトでボーイフレンドのフリープレイスタイルを使用するには`「bf」`を指定するか、`data/ui/freeplay/styles`フォルダに新規JSONファイルを作成（Pico用ファイルをコピーして編集）。
- `freeplayDJ`: フリープレイメニューでDJとしてキャラクターが表示される際のデータ。
- `charSelect`: キャラクター選択メニューでの表示データ。
- `results`: 結果画面での表示データ。

フリープレイDJデータは以下のように構成されています：
- `assetPath`: このキャラクターのアニメーションアトラスが配置されているフォルダ（`images/`フォルダからの相対パス）。
    - フリープレイアニメーションではスパーロウアトラスはサポートされていません。
- `animations`: キャラクターのアニメーションデータの一覧。
    - 有効なアニメーション名: `intro` `idle` `idleEasterEgg` `confirm` `fistPump` `loss` `charSelect` および `
- `charSelect`: 以下の構造化データオブジェクト:
    - `transitionDelay`: キャラクターがキャラクター選択画面へ遷移し始めてから、カメラがフェードアウトを開始するまでの時間（秒単位）。
- `fistPump`: 以下の構造化データオブジェクトを含む:
    - `introStartFrame` `fistPump` アニメーション内でイントロアニメーション（ランクが叩きつけられるまでループする）が開始されるフレーム番号。
    - `introEndFrame`: `fistPump` アニメーション内でイントロアニメーションが終了するフレーム番号。
    - `loopStartFrame`: `fistPump` アニメーション内でフォローアップアニメーションが開始するフレーム番号。
    - `loopEndFrame` `fistPump` アニメーション内でフォローアップアニメーションが終了するフレーム番号。
        - 指定したフレームラベルの最終フレームを使用するには `-1` を指定。
    - `introBadStartFrame` `loss` アニメーション内でイントロアニメーションが開始するフレーム番号。
    - `introBadEndFrame` イントロアニメーションが終了する`loss`アニメーション内のフレーム番号。
    - `loopBadStartFrame` フォローアップアニメーションが開始する`loss`アニメーション内のフレーム番号。
    - `loopBadEndFrame` フォローアップアニメーションが終了する`loss`アニメーション内のフレーム番号。

キャラクター選択データは以下のように構成されています：
- `position`: キャラクター選択グリッドにおけるキャラクターの優先配置位置。
    - `0`は左上、`3`は左中央、`8`は右下を表します。
    - キャラクターはアルファベット順に評価され、スロットが既に埋まっている場合、収まるまで横方向にシフトされます。
    - 執筆時点（v0.5.1）ではグリッドに合計9キャラクターまで配置可能。
- `gf`: (v0.5.1で新規追加) 以下の構造化データオブジェクトを含む:
    - `assetPath`: このキャラクターのAnimate Atlasが配置されているフォルダ（`images/`フォルダからの相対パス）。
        - Sparrowアトラスは非対応に注意。
    - `animInfoPath`: キャラクターのスライド動作を記述したFlash JSFLファイルへのパス。
    - `visualizer`: ビジュアライザー（例：NeneのABot）を表示するかどうか。
        - 実装方法についてはNeneキャラクター選択FLAを参照してください。

結果データは以下の構造です：
- `music`: 以下の構造を持つデータオブジェクト：
    - `PERFECT_GOLD`: `music/`フォルダ内の音楽トラックへのパス。全SICK達成時のPerfectランクアニメーション中に再生。
    - `PERFECT`: `music/`フォルダ内の音楽トラックへのパス。Perfectランクアニメーション中に再生。
    - `EXCELLENT`: `music/`フォルダ内の音楽トラックへのパス。Excellentランクのアニメーション中に再生されます。
    - `GREAT`: `music/`フォルダ内の音楽トラックへのパス。Greatランクのアニメーション中に再生されます。
    - `GOOD`: `music/`フォルダ内の音楽トラックへのパス。Goodランクのアニメーション中に再生されます。
    - `SHIT`: `music/`フォルダ内の音楽トラックへのパス。Lossランクアニメーション中に再生される。
    - 楽曲のBPMやループ方法をゲームに伝えるため、フォルダ内にメタデータファイルを必ず含めること。
    - メイン楽曲再生前に一度再生されるよう、`-intro.ogg`サフィックス付きの楽曲バリエーションを含めること。
- `perfect`: プレイヤーがPerfectランクを獲得した際に再生されるアニメーションを記述する、アニメーションデータ構造の配列。
    - データはアニメーションオブジェクトの配列形式。
    - Sparrowアニメーションまたは`animateatlas`スプライトを使用可能。`renderType`でどちらを使用するか指定。
    - `loopFrame` でループ開始フレームを指定するか、`looped` を `「false」` に設定してアニメーションを1回だけ再生します。
- `excellent`: プレイヤーがExcellentランクを獲得した際に再生されるアニメーションのデータ。
- `great`: プレイヤーがGreatランクを獲得した際に再生されるアニメーションのデータ。
- `good`: プレイヤーがGoodランクを獲得した際に再生されるアニメーションのデータ。
- `loss`: プレイヤーがLossランクを獲得した際に再生されるアニメーションのデータ。
- `perfectGold`: (v0.5.1で新規追加) プレイヤーが全SICKでPerfectランクを獲得した際に再生されるアニメーションのデータ。
    - 基本ゲームでは、これは単に`perfect`と同じデータですが、必要に応じて異なるデータにすることも可能です。

[^picosource]: <https://github.com/FunkinCrew/funkin.assets/blob/main/preload/data/players/pico.json>