# ノーツスタイルの作成

## ノーツスタイルのアセット

独自のノーツスタイルを作成するには、以下の要素のアセットが必要です：

- `note`: 曲の一般的なノーツ。チャートエディタとゲーム内で、プレイヤーが叩くべきノーツとして表示されます。
- `holdNote`: 押すのではなくキーを押し続ける必要があるホールドノーツのスプライト。
- `noteStrumline`: プレイヤーがキーを押した際に反応し、ノーツを叩くタイミングを視覚的に示す、ストラムライン上のノーツ。
- `noteSplash`: プレイヤーが`Sick!`評価を得た際の特殊効果。
- `holdNoteCover`: プレイヤーがホールドノーツを押さえている際の特殊効果。
- `countdown`: 曲開始前に表示されるカウントダウンのアセット（スプライトと音声の両方）。
- `judgementShit`: 判定表示用アセット。ノーツの正確なヒット度合いを表示します。
- `comboNumber0`: コンボカウンター用アセット。連続して一定数のノーツをヒットした際に表示されます。

これらのアセットは、modフォルダ内の整理された場所に配置してください。特定の場所である必要はありませんが、ノーツスタイルのJSONデータファイルから直接参照できる場所であることが重要です。

## ノーツスタイルのフォールバック

ノーツスタイルは再帰的なフォールバックシステムを採用しています。基本的に、ノーツスタイルに対して1つまたは複数のアセットを指定できます。フォールバックノーツスタイルが指定されている場合、親スタイルに含まれていないアセットが検索されます。親スタイルに該当するアセットがない場合、その親スタイルを参照し、以下同様です。これにより、基となるスタイルからわずかなバリエーションのみを加えたノーツスタイルを簡単に作成できます。

## ノーツスタイルデータ

カスタムノーツスタイルを作成するには、`data/notestyles`フォルダ内に新しいJSONファイルを作成する必要があります。

以下は「funkin」（別名デフォルト）ノーツスタイルのJSONファイル`assets/data/notestyles/funkin.json`[^notestylesource]です。

```json
{
  "version": "1.1.0",
  "name": "Funkin'",
  "author": "PhantomArcade",
  "fallback": null,
  "assets": {
    "note": {
      "assetPath": "shared:notes",
      "scale": 1.0,
      "data": {
        "left": { "prefix": "noteLeft" },
        "down": { "prefix": "noteDown" },
        "up": { "prefix": "noteUp" },
        "right": { "prefix": "noteRight" }
      }
    },
    "noteStrumline": {
      "assetPath": "shared:noteStrumline",
      "scale": 1.55,
      "offsets": [0, 0],
      "data": {
        "leftStatic": { "prefix": "staticLeft0" },
        "leftPress": { "prefix": "pressLeft0" },
        "leftConfirm": { "prefix": "confirmLeft0" },
        "leftConfirmHold": { "prefix": "confirmLeft0" },
        "downStatic": { "prefix": "staticDown0" },
        "downPress": { "prefix": "pressDown0" },
        "downConfirm": { "prefix": "confirmDown0" },
        "downConfirmHold": { "prefix": "confirmDown0" },
        "upStatic": { "prefix": "staticUp0" },
        "upPress": { "prefix": "pressUp0" },
        "upConfirm": { "prefix": "confirmUp0" },
        "upConfirmHold": { "prefix": "confirmUp0" },
        "rightStatic": { "prefix": "staticRight0" },
        "rightPress": { "prefix": "pressRight0" },
        "rightConfirm": { "prefix": "confirmRight0" },
        "rightConfirmHold": { "prefix": "confirmRight0" }
      }
    },
    "holdNote": {
      "assetPath": "NOTE_hold_assets",
      "data": {}
    },
    "noteSplash": {
      "assetPath": "",
      "data": {
        "enabled": true
      }
    },
    "holdNoteCover": {
      "assetPath": "",
      "data": {
        "enabled": true
      }
    },
    "countdownThree": {
      "data": {
        "audioPath": "shared:gameplay/countdown/funkin/introTHREE"
      },
      "assetPath": null
    },
    "countdownTwo": {
      "data": {
        "audioPath": "shared:gameplay/countdown/funkin/introTWO"
      },
      "assetPath": "shared:ui/countdown/funkin/ready",
      "scale": 1.0,
      "isPixel": false
    },
    "countdownOne": {
      "data": {
        "audioPath": "shared:gameplay/countdown/funkin/introONE"
      },
      "assetPath": "shared:ui/countdown/funkin/set",
      "scale": 1.0,
      "isPixel": false
    },
    "countdownGo": {
      "data": {
        "audioPath": "shared:gameplay/countdown/funkin/introGO"
      },
      "assetPath": "shared:ui/countdown/funkin/go",
      "scale": 1.0,
      "isPixel": false
    },
    "judgementSick": {
      "assetPath": "default:ui/popup/funkin/sick",
      "scale": 0.65,
      "isPixel": false
    },
    "judgementGood": {
      "assetPath": "default:ui/popup/funkin/good",
      "scale": 0.65,
      "isPixel": false
    },
    "judgementBad": {
      "assetPath": "default:ui/popup/funkin/bad",
      "scale": 0.65,
      "isPixel": false
    },
    "judgementShit": {
      "assetPath": "default:ui/popup/funkin/shit",
      "scale": 0.65,
      "isPixel": false
    },
    "comboNumber0": {
      "assetPath": "default:ui/popup/funkin/num0",
      "isPixel": false,
      "scale": 0.45
    },
    "comboNumber1": {
      "assetPath": "default:ui/popup/funkin/num1",
      "isPixel": false,
      "scale": 0.45
    },
    "comboNumber2": {
      "assetPath": "default:ui/popup/funkin/num2",
      "isPixel": false,
      "scale": 0.45
    },
    "comboNumber3": {
      "assetPath": "default:ui/popup/funkin/num3",
      "isPixel": false,
      "scale": 0.45
    },
    "comboNumber4": {
      "assetPath": "default:ui/popup/funkin/num4",
      "isPixel": false,
      "scale": 0.45
    },
    "comboNumber5": {
      "assetPath": "default:ui/popup/funkin/num5",
      "isPixel": false,
      "scale": 0.45
    },
    "comboNumber6": {
      "assetPath": "default:ui/popup/funkin/num6",
      "isPixel": false,
      "scale": 0.45
    },
    "comboNumber7": {
      "assetPath": "default:ui/popup/funkin/num7",
      "isPixel": false,
      "scale": 0.45
    },
    "comboNumber8": {
      "assetPath": "default:ui/popup/funkin/num8",
      "isPixel": false,
      "scale": 0.45
    },
    "comboNumber9": {
      "assetPath": "default:ui/popup/funkin/num9",
      "isPixel": false,
      "scale": 0.45
    }
  }
}

```

解きほぐすべき点はかなり多いので、全て分解していきましょう。
- `version`: ノーツスタイルデータファイル形式のバージョン番号。`1.0.0` のままにしておいてください。
- `name`: ノーツスタイルの読みやすい名前。チャートエディタなどで使用されます。
- `author`: ノーツスタイルの作成者、つまりアセットを作成したアーティスト。
- `fallback`: フォールバック用ノーツスタイルID。このスタイルに未設定のアセットは親スタイルのアセットを使用します。未指定要素には基本ゲームのアセットを適用するため、`「funkin」`を推奨デフォルト値とします。
- `assets`: ノーツスタイル用アセットデータのリスト。
    - 提供可能なデータの一覧は[アセット一覧](#note-style-assets)を参照してください。

アセットデータは以下の構造です：
- `assetPath`: このアセットに使用するメインアセットパス。
- `scale`: オリジナルサイズに対するアセットのサイズを指定します。例えば`2.0`はスプライトを2倍の大きさにする。指定しない場合、デフォルトは`1.0`。
- `offsets`: 一部のアニメーションでは、待機アニメーションに対する位置補正が必要になる場合があります。
  - 2つの小数値の配列を使用します。最初の値が水平位置、2番目の値が垂直位置です。
- `isPixel`: このアセットをピクセル表示するか（テクスチャスムージングを無効化）を指定します。オプションで、デフォルトは `false` です。
- `data`: 編集するアセットに応じて異なる、ノーツスタイルアセットデータオブジェクトの構造です。

ノーツスタイルアセットデータは以下のように構成されています：
- `note`の場合：`left`、`down`、`up`、`right`各方向のアニメーションデータリスト。
- `noteStrumline`の場合：各方向とそのバリエーション（例：`<direction>Static`、`<direction>Press`、`<direction>Confirm`、`<direction>ConfirmHold`）のアニメーションデータ一覧。`<direction>`は対応する各方向で置き換えます。
  - 提供された[例](#note-style-data)[^notestylesource]からもわかるように、`confirm`と`confirmHold`のアニメーションデータは一致していますが、独自のアニメーションを設定することも可能です。
- `holdNote`の場合：現在、設定可能なアニメーションデータのリストはありません。
- `noteSplash`の場合：現在、設定可能なアニメーションデータのリストはありません。将来追加される可能性があります。
  - `enabled`: アセットを表示するかどうかを指定します。オプションで、デフォルトは `true` です。
- `holdNoteCover` について: 現在設定可能なアニメーションデータのリストはありません。将来追加される可能性があります。
  - `enabled`: アセットを表示するかどうかを指定します。オプションで、デフォルトは `true` です。

アニメーションデータは以下のように構成されています：
- `prefix`: スプライトシートで指定されたアニメーション名。
  - SparrowまたはPackerの場合、データファイル内で各フレームセットの名前を確認し、末尾のフレーム番号を除いた名前をプレフィックスとして使用してください。
  - Animate Atlasesの場合、再生したいアニメーションのフレームラベルまたはシンボル名のいずれかを使用してください。
- `offsets`: 一部のアニメーションは、待機アニメーションに対する相対位置の補正が必要になる場合があります。
  - 2つの小数値の配列を使用します。最初の値が水平位置、2番目の値が垂直位置です。
- `looped`: ゲーム内でこのアニメーションをループ再生するかどうか。falseの場合、アニメーション終了時に一時停止し、ゲームがアセットに別の動作を指示するまで待機します。
- `flipX`: ゲーム内でこのアニメーションのスプライトを水平反転するかどうか。
- `flipY`: ゲーム内でこのアニメーションのスプライトを垂直反転するかどうか。
- `frameRate`: フレームレート値。デフォルトは `24`。
- `frameIndices`: オプションで、指定されたプレフィックスから使用するフレーム番号の配列（フレーム0から開始！）を指定します。
  - 例: `[0, 1, 2, 3]` を指定すると、このアニメーションは指定されたプレフィックスの最初の4フレームのみを使用します。

[^notestylesource]: <https://github.com/FunkinCrew/funkin.assets/blob/main/preload/data/notestyles/funkin.json>