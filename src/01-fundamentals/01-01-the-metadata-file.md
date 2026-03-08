# メタデータファイル

まず、`mods`フォルダ内に新しいフォルダを作成します。ここにMODのアセットとスクリプトを配置します。次に、新しいテキストファイルを作成し、名前を`_polymod_meta.json`に変更します。誤って`_polymod_meta.json.txt`と名付けないように注意してください！

このファイル内には、ゲームがあなたのMODを認識するために必要な情報を記述します。[Visual Studio Code](https://code.visualstudio.com/)のようなエディターでの作業をお勧めします。カンマの位置を誤った場合などに自動で修正してくれます。

```json
{
  "title": "Intro Mod",
  "description": "An introductory mod.",
  "contributors": [
    {
      "name": "EliteMasterEric"
    }
  ],
  "dependencies": {
    "modA": "1.0.0"
  },
  "optionalDependencies": {
    "modB": "1.3.2"
  },
  "api_version": "0.6.3",
  "mod_version": "1.0.0",
  "license": "Apache-2.0"
}
```

`_polymod_meta.json` には以下のフィールドがあります:

- `title`: MODの読みやすい名前。
- `description`: MODの読みやすい説明。
- `contributors`: クレジットオブジェクトのリスト。
- `homepage`: ユーザーがあなたのMODについて詳しく知ることができるURL。
- `dependencies`: 必須依存関係であるMOD IDとそのバージョン番号のマップ。
  - これらは、このMODをロードするために必ず一緒にロードされなければならないMODです。
  - 含まれていない場合、MODは失敗します。
  - 依存関係が先にロードされるようにMODリストは再順序付けされます。
- `optionalDependencies`: オプション依存関係となるMOD IDとバージョン番号のマップ。
  - これらのMODは本MODのロードに必須ではありませんが、依存関係MODが本MODより先にロードされるようMODリストの順序が強制的に変更されます。
- `api_version`: MODがあなたのFunkin『コピーと互換性があるかを判断するためのバージョン番号。サポートしたいFriday Night Funkin』のバージョン番号に変更してください（執筆時点では`0.6.3`が推奨）。
- `mod_version`: あなたのMOD専用のバージョン番号。任意のバージョンを選択するか、`1.0.0`のままにしておいてください。
- `license`: MODの配布に使用するライセンス。[こちらから選択](https://opensource.org/licenses) するか、`Apache-2.0` のままにしておいてください。

Contributor（クレジット）には以下のフィールドがあります：

- `name`: クレジットの名前。
- `role`: *(オプション)* クレジットの役割（例: 「Artist」や「Programmer」）。
- `email`: *(オプション)* 連絡先メールアドレス。
- `url`: *(オプション)* ホームページやX、YouTubeのURL。

これらのフィールドの多くは、今後実装予定のModメニューインターフェースで使用されることを想定しています。このインターフェースにより、ユーザーは自身のMODを整理できるようになります。