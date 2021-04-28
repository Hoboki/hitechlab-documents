# digitalocean のサーバーについて

[外部ページ](http://hitechlab.co.jp/)用のサーバー.  
Ruby on Rails で動いており, プロジェクトのルートパスは`/home/rails/hitechlab.jp/homepage`である.

### ログイン

[DigitalOcean](https://cloud.digitalocean.com/projects)にアクセスし、以下でログイン.

- ユーザー名: apple@hitechlab.co.jp
- パスワード: Nishikawalab2016

### ssh 接続

コマンド例: `ssh rails@138.68.51.107 -p 10022` など.

- ユーザー名: rails
- IP アドレス: 1138.68.51.107
- ポート番号: 10022
- パスワード: Nishikawalab2016

### 証明書の更新について

SSL 証明書には Let's Encrypt を用いている.
`/etc/letsencrypt`配下に設定ファイル等がある. HTTP サーバー側の設定は`/etc/nginx/sites-enabled/rails`に記述されている.
証明書の更新は自動的(crontab により)に行うようになっているはず...(動作不安定)
万が一更新されていない場合は, `sudo crontab -l`に記述されているコマンド等を手動で実行することで解決する.

### その他コマンド

- nginx の再起動 `sudo service nginx restart`
- rails(puma)の再起動 `bundle exec pumactl -F config/puma.rb restart`
