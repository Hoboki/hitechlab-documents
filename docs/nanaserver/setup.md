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

- PHP 7.3 & Composer(インストールは https://xn--o9j8h1c9hb5756dt0ua226amc1a.com/?p=3532 あたりを参照)
- Node v13 以上(多分... https://www.trifields.jp/how-to-install-node-js-on-ubuntu1604-2680 等を参照)
- MySQL5.7(https://qiita.com/witchcraze/items/759201593e2b89fed632 等を参照)
- Nginx(`sudo apt install -y nginx`で良さそう)
