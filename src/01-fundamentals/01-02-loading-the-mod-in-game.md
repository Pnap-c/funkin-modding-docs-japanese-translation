# ゲーム内でのMODの読み込み

メタデータファイルが用意できたので、ゲームを起動しましょう！プロのコツとして、コマンドラインからゲームを実行すると、MODが読み込まれたことを示すメッセージなど、多くの有用なデバッグ情報が確認できます！

```shell
source/funkin/modding/PolymodHandler.hx:316: Found 5 mods when scanning.
source/funkin/modding/PolymodHandler.hx:118: Attempting to load 5 mods...
...
source/funkin/modding/PolymodErrorHandler.hx:79: [INFO-] LOADING MOD - Preparing to load mod ../../../../example_mods/introMod
source/funkin/modding/PolymodErrorHandler.hx:79: [INFO-] LOADING MOD - Done loading mod ../../../../example_mods/introMod
...
source/funkin/modding/PolymodHandler.hx:169: Mod loading complete. We loaded 5 / 5 mods.
```

いいね！でも今のところ、君のMODは何も機能してないよ。(次に進もう)
