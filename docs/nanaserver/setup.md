# nanaserver セットアップ

nanserver セットアップに必要な項目のまとめ

### パソコンの準備(物理的に必要なもの)

- パソコン本体(64bit)
- モニター(セットアップ時のみ？)
- HDMI ケーブル
- キーボード
- マウス
- LAN ケーブル

### OS のインストール

OS(Operating System)は ubuntu 18.04 LTS で良さそう？使いやすさを考慮し、GUI 付きのもので。
手順は https://linuxfan.info/ubuntu-18-04-install-guide などを参考に

### 必要となるミドルウェア、ライブラリ、パッケージ

- PHP 7.3 & Composer(インストールは https://xn--o9j8h1c9hb5756dt0ua226amc1a.com/?p=3532 あたりを参照)その他、以下も実行(`sudo apt install php7.3-fpm php7.3-mbstring php7.3-mysqli unzip`)

- Node v13 以上(多分... https://www.trifields.jp/how-to-install-node-js-on-ubuntu1604-2680 等を参照)
- MySQL5.7(https://qiita.com/witchcraze/items/759201593e2b89fed632 等を参照)。root ユーザーに初期パスワードを設定する必要がある。`sudo mysql`で mysql にログインし、`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';`で'password'をパスワードに設定。`mysql -u root -p`でログインできるか確認。
- Nginx(`sudo apt install -y nginx`で良さそう)
- phpMyAdmin(`sudo apt install phpmymin`でインストール。)その後次のステップ。
  1. `sudo ln -s /usr/share/phpmyadmin /var/www/phpmyadmin`でシンボリックリンク作成。
  2. `sudo chmod 775 -R /usr/share/phpmyadmin/`と`sudo chown www-data:[ユーザー名] -R /usr/share/phpmyadmin/`で権限変更。
  3. /etc/nginx/sites-available/default を修正する。(nginx.sample.conf を参考)
  4. /phpmyadmin にアクセスし、root,password でログインできるか確認。php7.3 になっているのかも確認。

### laravel プロジェクトのインストール

/var/www 配下で`git clone https://github.com/sengun27/hitechlab.git`を実行。その後のステップは laravel のレポジトリを参照。
