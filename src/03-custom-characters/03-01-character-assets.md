# キャラクタースプライトシート形式

キャラクターのアニメーションを構成する個々のスプライトは、ゲームで使用するためにスプライトシートに結合する必要があります。Friday Night Funkin' は以下の形式のいずれかをサポートしています：

- `sparrow`: 画像を大きなシートに結合し、各フレームの座標を含む XML ファイルを同梱します。Adobe Animate または Flash CS6 の「スプライトシートを生成」オプションで直接エクスポート可能。あるいは [Free Texture Packer](http://free-tex-packer.com/) を使用して個々のフレームから作成可能（Free Texture Packer ではこの形式を Starling と呼称）。

- `packer`: 画像をシートに結合し、各フレームの座標を含むTXTファイルを提供します。

- `animateatlas`: Adobe Animate使用時のみ生成される形式。個々のシンボルを大型シートにエクスポートし、各シンボルを分割するデータを含むJSONファイルを提供。さらにそれらのシンボルをアニメーションに配置するための2つ目のJSONを提供します。パフォーマンス向上が期待でき、特に小さなパーツを再配置して作成されたキャラクターに有効です。この処理には[FlxAnimate](https://github.com/Dot-Stuff/flxanimate) Haxelibを使用しています。

- `multisparrow`: 異なるアニメーショングループを別々のSparrowスプライトシートにエクスポートし、それらを1つのキャラクターに統合することを可能にします。
