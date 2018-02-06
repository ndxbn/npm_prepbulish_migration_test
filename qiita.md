https://qiita.com/ndxbn/items/f0cd2b13a3268254f2aa.md

npm prepublish の現状と今後どう変わっていくかを、表にしてみた。
# 概要
## この記事 is なに
いい加減 Node.js v8 系使いたいので npm 5.x 系を使うことになるのだけれど、「[prepublish がまともな挙動をするように、なだらかに変更かけていくよ](https://github.com/npm/npm/issues/10074)、だから気をつけてね」って言われてるのもわかっていたのだけれど、その内容とか現状をちゃんと把握できていなかったので、調べました。

[作業して結果をまとめたリポジトリがある](https://github.com/ndxbn/npm_prepbulish_migration_test/)ので、それの日本語訳+アルファ を書きます。

## 作業したリポジトリ
https://github.com/ndxbn/npm_prepbulish_migration_test/

prepublish と prepare の（現状のパット見よくわからない状態になった）発端的なものは、 https://docs.npmjs.com/misc/scripts#prepublish-and-prepare とか  https://github.com/npm/npm/issues/10074 を見てください。

[.travis.yml](https://github.com/ndxbn/npm_prepbulish_migration_test/blob/master/.travis.yml) を見ればわかりますが、複数のバージョンで `npm isntall` と `npm install ./local_module/sub_project` と `npm publish` と `npm pack` を実行してます。
どの npm-script がどのような順番で実行されたか？を眺めて、なんとなく表にしてみました。

実行結果は、 https://travis-ci.org/ndxbn/npm_prepbulish_migration_test で見れます。
エラーになってるやつは、 `npm publish` を `private: true` で抑止してるからなので、意図通りです。

## "ステップ4" と "ステップ 5" とはなにか
https://github.com/npm/npm/issues/10074 で言ってるやつです。


ステップ 4 は、

> 4. In a year or so, make a semver-major bump to npm and make prepublish's behavior match prepublishOnly.
> 1年後くらいに、メジャーバージョンを上げて（=破壊的変更だと明示して）、 `prepublish` を `prepublishOnly` と同じ挙動になるに変更した状態にします。

ステップ5 は、

> 5. Either then or sometime after that, deprecate `prepublishOnly` and have just `prepare` and `prepublish`.
> 5. 適当に時間が経ち、よさげな雰囲気になった頃合いを見て、 `prepublishOnly` を非推奨（≒削除）して、（本来の） `prepare` と `prepublish` だけがある状態にします。

## 使用する package.json の概要
必要なところは、以下の通りです。

```json
{
  "name": "npm_prepbulish_migration_test",
  "private": true,
  "dependencies": {
    "npm_prepbulish_migration_test_sub": "file:local_module/sub_project"
  }
}
```

この後の表に出てくる、 "main" というのは `npm_prepbulish_migration_test` 、sub というのは `local_module/sub_project` のことです。

# やってみた結果
表の数字は、実行された順番です。

## `npm install` したときに実行される npm-scirpt の移り変わり


npm script stage ＼ version | 2.14.3 | 2.15.11 | 3.8.6 | 3.10.10 | 4.2.0 | 5.6.0 | step 4 | step 5
:-- | --- | --- | --- | --- | --- | --- | --- | ---
prepublish     main |  8  |  8  |  8  |  8  |  9  |  7  | No  | No  
prepublishOnly main | No  | No  | No  | No  | No  | No  | No  | No  
publis         main | No  | No  | No  | No  | No  | No  | No  | No  
postpublis     main | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     main |  1  |  1  |  5  |  2  |  3  |  1  |  1  |  1  
install        main |  6  |  6  |  6  |  6  |  7  |  5  |  5  |  5  
postinstall    main |  7  |  7  |  7  |  7  |  8  |  6  |  6  |  6  
prepack        main | No  | No  | No  | No  | No  | No  | No  | No  
pack           main | No  | No  | No  | No  | No  | No  | No  | No  
postpack       main | No  | No  | No  | No  | No  | No  | No  | No  
prepare        main | No  | No  | No  | No  | 10  |  8  |  7  |  7  
(is_private)   main | No  | No  | No  | No  | No  | No  | No  | No  
===                 | ==  | ==  | ==  | ==  | ==  | ==  | ==  | ==  
prepublish     sub  |  2  |  2  |  1  |  1  |  1  | No  | No  | No  
prepublishOnly sub  | No  | No  | No  | No  | No  | No  | No  | No  
publis         sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpublis     sub  | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     sub  |  3  |  3  |  2  |  3  |  4  |  2  |  2  |  2  
install        sub  |  4  |  4  |  3  |  4  |  5  |  3  |  3  |  3  
postinstall    sub  |  5  |  5  |  4  |  5  |  6  |  4  |  4  |  4  
prepack        sub  | No  | No  | No  | No  | No  | No  | No  | No  
pack           sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpack       sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepare        sub  | No  | No  | No  | No  |  2  | No  | No  | No  


見どころは、

* 4.2.0 で `prepare` が追加され
* 5.6.0 で サブモジュール側（インストールされた側）で `prepublish` されなくなり
* 5.6.0 で サブモジュール側で `prepare` も実行されくて
* （おそらく）step 4 で `npm install` した側でも `prepublish` が走らなくなる

あたりです。

`npm install` した時に サブモジュール側が `prepare` されないのは、 `npm publish` するときに `prepare` された結果のものだけを npm registry にアップロードするから、このタイミングで `prepare` する必要がないからだと思います。

## `npm install foo` したときに実行される npm-scirpt の移り変わり

npm script stage ＼ version | 2.14.3 | 2.15.11 | 3.8.6 | 3.10.10 | 4.2.0 | 5.6.0 | step 4 | step 5
:-- | --- | --- | --- | --- | --- | --- | --- | ---
prepublish     main | No  | No  | No  | No  | No  | No  | No  | No  
prepublishOnly main | No  | No  | No  | No  | No  | No  | No  | No  
publis         main | No  | No  | No  | No  | No  | No  | No  | No  
postpublis     main | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     main | No  | No  | No  | No  | No  | No  | No  | No  
install        main | No  | No  | No  | No  | No  | No  | No  | No  
postinstall    main | No  | No  | No  | No  | No  | No  | No  | No  
prepack        main | No  | No  | No  | No  | No  | No  | No  | No  
pack           main | No  | No  | No  | No  | No  | No  | No  | No  
postpack       main | No  | No  | No  | No  | No  | No  | No  | No  
prepare        main | No  | No  | No  | No  | No  | No  | No  | No  
(is_private)   main | No  | No  | No  | No  | No  | No  | No  | No  
===                 | ==  | ==  | ==  | ==  | ==  | ==  | ==  | ==  
prepublish     sub  |  1  |  1  |  1  |  1  |  1  | No  | No  | No  
prepublishOnly sub  | No  | No  | No  | No  | No  | No  | No  | No  
publis         sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpublis     sub  | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     sub  |  2  |  2  |  2  |  2  |  3  |  1  |  1  |  1  
install        sub  |  3  |  3  |  3  |  3  |  4  |  2  |  2  |  2  
postinstall    sub  |  4  |  4  |  4  |  4  |  5  |  3  |  3  |  3  
prepack        sub  | No  | No  | No  | No  | No  | No  | No  | No  
pack           sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpack       sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepare        sub  | No  | No  | No  | No  |  2  | No  | No  | No  

見どころは、

* 5.6.0 で prepublish されなくなり
* 5.6.0 で prepare もされなくなった

あたりです。

prepublish も prepare も、 `npm publish` するときに `prepare` された結果のものだけを npm registry にアップロードするから、このタイミングでやる必要がありません。

## `npm publish` したときに実行される npm-scirpt の移り変わり

npm script stage ＼ version | 2.14.3 | 2.15.11 | 3.8.6 | 3.10.10 | 4.2.0 | 5.6.0 | step 4 | step 5
:-- | --- | --- | --- | --- | --- | --- | --- | ---
prepublish     main |  1  |  1  |  1  |  1  |  1  |  1  |  3  |  2  
prepublishOnly main | No  | No  | No  | No  |  3  |  3  |  2  | No (deleted)  
publis         main | ??? | ??? | ??? | ??? | ??? | ??? | ??? | ???
postpublis     main | ??? | ??? | ??? | ??? | ??? | ??? | ??? | ???
preinstall     main | No  | No  | No  | No  | No  | No  | No  | No  
install        main | No  | No  | No  | No  | No  | No  | No  | No  
postinstall    main | No  | No  | No  | No  | No  | No  | No  | No  
prepack        main | ??? | ??? | ??? | ??? | No  |  4  |  4  |  3  
pack           main | ??? | ??? | ??? | ??? | No  | No! | ??? | ???  
postpack       main | ??? | ??? | ??? | ??? | No  |  5  |  5  |  4  
prepare        main | No  | No  | No  |  No |  2  |  2  |  1  |  1  
(is_private)   main |  2  |  2  |  2  |  2  |  4  |  6  |  6  |  5  
===                 | ==  | ==  | ==  | ==  | ==  | ==  | ==  | ==  
prepublish     sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepublishOnly sub  | No  | No  | No  | No  | No  | No  | No  | No  
publis         sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpublis     sub  | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     sub  | No  | No  | No  | No  | No  | No  | No  | No  
install        sub  | No  | No  | No  | No  | No  | No  | No  | No  
postinstall    sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepack        sub  | No  | No  | No  | No  | No  | No  | No  | No  
pack           sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpack       sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepare        sub  | No  | No  | No  | No  | No  | No  | No  | No  

"???" になっている部分は、実際に publish してないから実行されるはずだけど未確認なところです。

npm 4.2.0 以下では、 `prepack` と `postpack` は実装されていないはずですが、 3.10.10 以下は早い段階で private 判定をしてしまっていたので、一応 ??? にしてあります。

見どころは

* 5.0.0 から `prepack` と `postpack` が導入された（今回のはあまり関係ない）
* 5.6.0 から step 4 になるときに、 `prepublish` の実行タイミングが（おそらく）変更される
* step 5 で、 `prepublishOnly` が非推奨になる（予定）

あたりです。

「5.6.0 から step 4 になるときに、 `prepublish` の実行タイミングが（おそらく）変更される」のは、

> 4. In a year or so, make a semver-major bump to npm and make prepublish's behavior match prepublishOnly.
> 1年後くらいに、メジャーバージョンを上げて（=破壊的変更だと明示して）、 `prepublish` を `prepublishOnly` と同じ挙動になるに変更した状態にします。
> （再掲）

を根拠に言っています。
これを忠実にやるのであれば、

* `prepublish` は `prepare` の後に実行されるように変更される
* `prepublish` と `prepublishOnly` はお互いの実行に依存していないはずだし、入れ替えても問題ないよね

の2点から、「step 4 では、 `prepublish` が `prepublishOnly` の後に実行される」ように変更されるのではないかと予想しています。

ところで、本当は、dev バージョンあたりを上げたものを 実際に `publish` して動作確認したかったのですが、めんどくさいし、今回知りたいことはそこまでやらなくても知れたので、やってません。やる予定も今のところはありません。

## `npm pack` したときに実行される npm-scirpt の移り変わり

`npm pack` というコマンドは、もしかしたら馴染みのない人が多いかもしれません。
[ドキュメントはちゃんとあります](https://docs.npmjs.com/cli/pack)し、[ `prepublish` のほうにも「（registry に アップロードしないという意味の）"dry run" がしたかったら、 `npm pack` を使えばいいんじゃないかな」と下の方に](https://docs.npmjs.com/cli/publish)書いてあります。

そんなコマンドでも、 `prepublish` は実行されています。

npm script stage ＼ version | 2.14.3 | 2.15.11 | 3.8.6 | 3.10.10 | 4.2.0 | 5.6.0 | step 4 | step 5
:-- | --- | --- | --- | --- | --- | --- | --- | ---
prepublish     main |  1  |  1  |  1  |  1  |  1  |  1 | No  | No  
prepublishOnly main | No  | No  | No  | No  | No! | No | No  | No  
publis         main | No  | No  | No  | No  | No  | No | No  | No  
postpublis     main | No  | No  | No  | No  | No  | No | No  | No  
preinstall     main | No  | No  | No  | No  | No  | No | No  | No  
install        main | No  | No  | No  | No  | No  | No | No  | No  
postinstall    main | No  | No  | No  | No  | No  | No | No  | No  
prepack        main | No  | No  | No  | No  | No! |  3 |  2  |  2  
pack           main | No  | No  | No  | No  | No! | No!| ??? | ???  
postpack       main | No  | No  | No  | No  | No! |  4 |  3  |  3  
prepare        main | No  | No  | No  | No  |  2  |  2 |  1  |  1  
(is_private)   main | No  | No  | No  | No  | No  | No | No  | No  
===                 | ==  | ==  | ==  | ==  | ==  | ==  | ==  | ==  
prepublish     sub  | No  | No  | No  | No  | No  | No | No  | No  
prepublishOnly sub  | No  | No  | No  | No  | No  | No | No  | No  
publis         sub  | No  | No  | No  | No  | No  | No | No  | No  
postpublis     sub  | No  | No  | No  | No  | No  | No | No  | No  
preinstall     sub  | No  | No  | No  | No  | No  | No | No  | No  
install        sub  | No  | No  | No  | No  | No  | No | No  | No  
postinstall    sub  | No  | No  | No  | No  | No  | No | No  | No  
prepack        sub  | No  | No  | No  | No  | No  | No | No  | No  
pack           sub  | No  | No  | No  | No  | No  | No | No  | No  
postpack       sub  | No  | No  | No  | No  | No  | No | No  | No  
prepare        sub  | No  | No  | No  | No  | No  | No | No  | No  


[`prepack` と`postpack` は、 v5.0.0 で実装されたものです。](http://blog.npmjs.org/post/161081169345/v500)


見どころとしては、

* step 4 以降で、 `prepublish` は実行されない
* pack する前には `prepare` が実行される

あたりでしょうか。

これについては、[iarna 氏の以下のコメント](https://github.com/npm/npm/issues/15454#issuecomment-288606051)に説明されている意図通りになった、という感じです。

> "I want to do build steps that are neccessary to use my module." — use prepare
>  `prepare` は、「モジュールを実行できるようにするために、ビルドする」ステップであってほしい。
> "I want to do validation steps that stop me from publishing bad code." — use prepublishOnly
> （"本来の" `prepublish` という意味で）`prepublishOnly` は、「おかしなコードを publish しないように、バリデーションするステップ」であってほしい。

`npm pack` は、 「 `npm publish` から ファイルのアップロードをする部分を抜いただけのもの」**ではありません**。単に「 `npm publish` する時と同じ tar ball を作る」というだけなので、**`npm pack` では `prepublish` は実行されるべきではありません**。

# まとめ
現状は、まだ「移行作業を進めるための段階」です。 `prepare` はまだ"本来の挙動" ではないので、使用は控えるべきです。もともと `prepare` で行っていたタスクは、きちんと `prepublisOnly` と `prepare` のどちらか適切な方に振り分け、「 `prepare` ではなにもしていない状態」にして、次の step 4 に備えましょう。

step 4 が来て `prepublish` が本来の姿になったら 、速やかに `prepublishOnly` のものを `prepublish` へ戻して「 `prepublishOnly` を使用していない状態」にし、 step 5 へ備えましょう。


# おまけ

[prepublishOnly should run on `npm pack` という ISSUE](https://github.com/npm/npm/issues/15363) がありました。私も、最初はこの疑問を持ちましたが、やはり同じように疑問に思う人はいる（？）みたいですね。
