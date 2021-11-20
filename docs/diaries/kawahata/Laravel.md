20201222

# Laravel入門
__Laravelとは__

PHPのホームページ作成用のフレームワーク。名前は『ナルニア国物語』に登場するナルニア国の王都、ケア・パラベルにちなむ。YouTubeによる参考動画多数。

__composerとは__

パッケージ管理ツール。
必要なものを一括で入れてくれるもの。

__テンプレートエンジン（テンプレートファイル）とは__

HTMLとPHP処理を統合してHTMLレスポンスを生成する仕組み。PHPコード、HTMLコードそれぞれの可読性が向上する。さらに、HTMLコードの再利用が可能になる。Laravelに同梱されているのはBlade。

welcome.blade.php

参考
>[Laravel - ウェブ職人のためのPHPフレームワーク](http://laravel.jp/)

>[名前の意味を調べたら、PHP, Laravelへの愛が高まってきた](https://qiita.com/yohei_tanaka/items/ed4b216906e82e92c55e)

>[Static method (静的メソッド) - MDN Web Docs 用語集: ウェブ ...](https://developer.mozilla.org/ja/docs/Glossary/Static_method)

>[今さら聞けないIT用語：やたらと耳にするけど「API」って何 ...](https://data.wingarc.com/what-is-api-16084)

20210103

# Hitechlabサンプルサイトへのアクセス情報

http://192.168.0.8/

20210108

__URLの階層を指定する__


`Route::group('prefix', function(){
})`

__アイコンを挿入する__

`<i class="fas fa-plus-circle"></i>`

___

__Question__

リレーションのwithPivotがよくわからない。

参考
>[Font Awesome](https://fontawesome.com/icons?d=gallery)

>[リレーション](https://readouble.com/laravel/6.x/ja/eloquent-relationships.html)

20210112

# ルーティング：Route::resource, Route::group(['middleware' => ['auth']], function () {});, Redis

## Route::resource

ルーティングにRoute::resouceを指定することで、CRUDルーティングを一度に行うことができる。公式のドキュメントの対応表参照。

## Route::group(['middleware' => ['auth']], function () {});

ログインしていないとそれ以降のルートにアクセスできなくする。

## Redis

結局ようわからん

![Route:resource](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F176572%2Fca4ad251-af3c-9195-4934-ad587fe184e8.png?ixlib=rb-1.2.2&auto=format&gif-q=60&q=75&s=7790398f657b1372b157e0230e8fe069)

参考
>[LaravelでRoute::resourceを使うときに気をつけること](https://qiita.com/sympe/items/9297f41d5f7a9d91aa11)

>[Laravel のルーティングでauthenticate middlewareを使って認証する3つの方法](https://qiita.com/yamotuki/items/b96978f8e379e285ecb6)

>[ルートグループ](https://readouble.com/laravel/5.2/ja/routing.html)

>[【入門】Redis - Qiita](https://qiita.com/wind-up-bird/items/f2d41d08e86789322c71)

20210115

# Roleとは, Seeder

## Roleとは

Roleという言葉の使い方がわからん。
→Userに与えられた権限

## Seeder

データベースの中身を生成するもの

## withPivot, withTrashed

中間テーブルのカラムを取得する

## 生基板 hasMany 基板

CompanyとOfficeの関係と同じ

20210117

# Tinker, config('app.name', 'Laravel'), mix('js/app.js')

## Tinker

<image src="images\Tinker.png" width="300" style="margin: 0 auto;">

20210121

# `<input id='name'>`

`<label for='name'>`
と対応している。

___

__Qustion__

参考
>[`<input>`: 入力欄 (フォーム入力) 要素 - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element/input)

20210124

# Bootstrap/グリッドシステム

参考
>[Bootstrapのグリッドシステムについてまとめてみた - Qiita](https://qiita.com/akatsuki174/items/53b7367b04ed0b066bbf)

20210126

# base_path

プロジェクトルートの完全パスを生成する。
指定されたプロジェクトルートディレクトリからの相対パスから絶対パスを生成する。

参考
>[ヘルパ 5.5 Laravel](https://readouble.com/laravel/5.5/ja/helpers.html#method-base-path)

20211119

# Laradock複数プロジェクト環境構築

[【Laravel】Laradockで複数プロジェクトを動かす手順 | ぺんすけブログ - ぺんすけブログ](https://pensuke.work/posts/laradock-multiproject/)

[「/etc/hosts」ファイルについて - Qiita](https://qiita.com/hirokik-0076/items/830f18ed733e65defa58)

[【Tips】Windows 10のhostsファイルを編集する方法 | ソフトアンテナ](https://softantenna.com/wp/tips/windows-edit-hosts/)