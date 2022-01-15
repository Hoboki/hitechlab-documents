20201222

# Laravel 入門

**Laravel とは**

PHP のホームページ作成用のフレームワーク。名前は『ナルニア国物語』に登場するナルニア国の王都、ケア・パラベルにちなむ。YouTube による参考動画多数。

**composer とは**

パッケージ管理ツール。
必要なものを一括で入れてくれるもの。

**テンプレートエンジン（テンプレートファイル）とは**

HTML と PHP 処理を統合して HTML レスポンスを生成する仕組み。PHP コード、HTML コードそれぞれの可読性が向上する。さらに、HTML コードの再利用が可能になる。Laravel に同梱されているのは Blade。

welcome.blade.php

参考

> [Laravel - ウェブ職人のための PHP フレームワーク](http://laravel.jp/)

> [名前の意味を調べたら、PHP, Laravel への愛が高まってきた](https://qiita.com/yohei_tanaka/items/ed4b216906e82e92c55e)

> [Static method (静的メソッド) - MDN Web Docs 用語集: ウェブ ...](https://developer.mozilla.org/ja/docs/Glossary/Static_method)

> [今さら聞けない IT 用語：やたらと耳にするけど「API」って何 ...](https://data.wingarc.com/what-is-api-16084)

20210103

# Hitechlab サンプルサイトへのアクセス情報

http://192.168.0.8/

20210108

**URL の階層を指定する**

`Route::group('prefix', function(){ })`

**アイコンを挿入する**

`<i class="fas fa-plus-circle"></i>`

---

**Question**

リレーションの withPivot がよくわからない。

参考

> [Font Awesome](https://fontawesome.com/icons?d=gallery)

> [リレーション](https://readouble.com/laravel/6.x/ja/eloquent-relationships.html)

20210112

# ルーティング：Route::resource, Route::group(['middleware' => ['auth']], function () {});, Redis

## Route::resource

ルーティングに Route::resouce を指定することで、CRUD ルーティングを一度に行うことができる。公式のドキュメントの対応表参照。

## Route::group(['middleware' => ['auth']], function () {});

ログインしていないとそれ以降のルートにアクセスできなくする。

## Redis

結局ようわからん

![Route:resource](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F176572%2Fca4ad251-af3c-9195-4934-ad587fe184e8.png?ixlib=rb-1.2.2&auto=format&gif-q=60&q=75&s=7790398f657b1372b157e0230e8fe069)

参考

> [Laravel で Route::resource を使うときに気をつけること](https://qiita.com/sympe/items/9297f41d5f7a9d91aa11)

> [Laravel のルーティングで authenticate middleware を使って認証する 3 つの方法](https://qiita.com/yamotuki/items/b96978f8e379e285ecb6)

> [ルートグループ](https://readouble.com/laravel/5.2/ja/routing.html)

> [【入門】Redis - Qiita](https://qiita.com/wind-up-bird/items/f2d41d08e86789322c71)

20210115

# Role とは, Seeder

## Role とは

Role という言葉の使い方がわからん。
→User に与えられた権限

## Seeder

データベースの中身を生成するもの

## withPivot, withTrashed

中間テーブルのカラムを取得する

## 生基板 hasMany 基板

Company と Office の関係と同じ

20210117

# Tinker, config('app.name', 'Laravel'), mix('js/app.js')

## Tinker

<image src="images\Tinker.png" width="300" style="margin: 0 auto;">

20210121

# `<input id='name'>`

`<label for='name'>`
と対応している。

---

**Qustion**

参考

> [`<input>`: 入力欄 (フォーム入力) 要素 - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/input)

20210124

# Bootstrap/グリッドシステム

参考

> [Bootstrap のグリッドシステムについてまとめてみた - Qiita](https://qiita.com/akatsuki174/items/53b7367b04ed0b066bbf)

20210126

# base_path

プロジェクトルートの完全パスを生成する。
指定されたプロジェクトルートディレクトリからの相対パスから絶対パスを生成する。

参考

> [ヘルパ 5.5 Laravel](https://readouble.com/laravel/5.5/ja/helpers.html#method-base-path)

20211119

# Laradock 複数プロジェクト環境構築

[【Laravel】Laradock で複数プロジェクトを動かす手順 | ぺんすけブログ - ぺんすけブログ](https://pensuke.work/posts/laradock-multiproject/)

[「/etc/hosts」ファイルについて - Qiita](https://qiita.com/hirokik-0076/items/830f18ed733e65defa58)

[【Tips】Windows 10 の hosts ファイルを編集する方法 | ソフトアンテナ](https://softantenna.com/wp/tips/windows-edit-hosts/)

20211205

# Request::route()でなぜインスタンスが取得できるのかがわからん。

20211206

# $casts

データの型変換を要するカラムを指定する。Company モデルの urls は、データには配列としてではなく、以下の''内全てを文字列として JSON 形式で保存される。

'[http://a.com, http://b.com]'

# $appends とアクセサ

Company モデルには full_name のカラムがないので、インスタンス生成の際（会社データを取り出してくるとき）に一緒に作る。

getFullNameAttribute 関数は特別な関数名（get{cammelCase の Attribute 名}Attribute）だから、自動で$company->full_name で getFullNameAttribute()の返り値が返される。

# Problem

- 個人一覧から個人の詳細が見られない->取り急ぎ修正済み

- 会社の分類が morph なのは個人も分類が充てられるからか？

- order_listable テーブルの order_listable_type カラムがおかしい。type=Maker や Supplier は会社か個人のはずだが order_listable_type=App\Models\Order\UnregisteredList になってしまう。そのせいか購入依頼一覧->未発注リスト(会社)が反映されない。

20211210

# Problem

分類に未登録の会社や未登録部品の登録を許すと、小さい誤字が増えるかも。誤字があるごとに未登録情報が増えていくと後で修正が面倒になるかもしれない。

購入依頼って 1000 個以上買うことある？

違う会社で同じ型番のメーカーになることある？

基盤と部品で型番が被ることはある？

パーツの value カラムは何だ？略名とかいる？

20211211

シーダーの編集・削除でシードエラーが出たら、オートローダー（シーダーファイルを自動認識してくれるやつ）を再生成する必要なときがある。

```
composer dump-autoload
```

20211212

# Problem

分類はただのタグで、例えば仕入れ先の分類をつけておかないと仕入れ先に指定できないようにするという訳ではない？

20211229

# Problem

ジョブって何個ある？数えられるくらいならドロップダウンでいいかも

20220103

# UnregisteredModel

会社作成時に同一名の未登録会社を削除&supplier_id 付与

部品/基板作成時に同一名の未登録部品/基板を削除&model_number 付与(型番は必須なので多分このままでは無理)

会社変更時に同一名の未登録会社を削除&supplier_id 付与

部品/基板変更時に同一名の未登録部品/基板を削除&model_number 付与(型番は必須なので多分このままでは無理)

発注時に unregisered_modelable_id 変更&unregistered_modelable_type を App\Models\Order\UnorderedList から App\Models\Order\UndeliveredList に変更

20220108

袋単位が未だ適当

「ついでに」はできなくなる

あとは基板と部品をどのようにデータベースに置くか

20220109

入り数と袋数がどちらか分からない

purchasedLists.index が遅すぎる、、、軽いビッグデータ状態->pagenation で解決

注文書の相手方の電話番号いる？

ジョブに 01J002-05 みたいなのがある。どうする？->要らない。最初の6文字でよし。

20220114

部品分類？関連JOB？->要らない

20220116

現状、移植元の部品マスタのメーカーがnullなら移植してもnullにしてある。でも部品のメーカーは必須がいいよね。
