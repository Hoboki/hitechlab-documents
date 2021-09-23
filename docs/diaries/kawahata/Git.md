20201124

# Gitの理解・実践

VSCodeでuser.nameとuser.emailを求められたとき、

`git config --global user.email "you@example.com"`

`git config --global user.name "Your Name"`

を実行する。
それでも解決しない場合は、--globalオプションを無くして実行するとうまくいく。

__記号「`」：バッククォート__

__強制コミット__

`git commit --amend`

`git push --force origin HEAD`

参考
>[1.6 使い始める - 最初のGitの構成](https://git-scm.com/book/ja/v2/%E4%BD%BF%E3%81%84%E5%A7%8B%E3%82%81%E3%82%8B-%E6%9C%80%E5%88%9D%E3%81%AEGit%E3%81%AE%E6%A7%8B%E6%88%90)

>[Markdown記法 サンプル集](https://qiita.com/tbpgr/items/989c6badefff69377da7)

>[記号と読み](http://www.asahi-net.or.jp/~jh3m-fjym/kigou/kigou.html)

20210923
# ローカルのディレクトリをGithubへアップロードする方法

[ローカルのディレクトリをGithubへアップロードする方法｜Koushi Kagawa｜note](https://note.com/koushikagawa/n/nfccf06fa845b)

もうすでにgit addしてしまっているファイルは.gitignoreの記載に関係なく追跡されてしまうので、以下のコマンドが必要。

```cmd
ファイルのキャッシュを削除
git git rm --cached FILE_NAME

ディレクトリ内の全てのファイルのキャッシュを削除
git rm -r --cached DIR_NAME
```

[.gitignore の書き方。ファイル/ディレクトリの除外 | WWWクリエイターズ](https://www-creators.com/archives/1662)

# refusing to merge unrelated historiesを解決する

[[Git] fatal: refusing to merge unrelated historiesを解決する話 - Qiita](https://qiita.com/mei28/items/85bc881ac1f26332ac15)

# リポジトリを変更する
```git
git remote set-url origin NEW_URL
※NEW_URL：https://github.com/AccountName/RepositoryName.git

git push origin main
※旧バージョンはmaster
```
the remote end hung up unexpectedlyエラーが出る場合、コミットサイズが大きい可能性がある。したがって、以下のコマンドを追加。
```
git config http.postBuffer 52428000
```
それでもダメな場合
```
git config --global http.postBuffer 2M
```

[gitで「the remote end hung up unexpectedly」が出た時の対処法 | CODE CLUB965](https://codeclub965.com/?p=2073)