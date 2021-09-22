20210524
# ファイルの検索法(Windows)
Command Promptで検索したいディレクトリまで移動
`dir/s/b *.uf2`

20210918
# 自社商品開発会議
- 貯金箱
- キーボード
- Wi-Fiモジュールを使った「自分だけのウェブサイト」
- 教育本「なぜ光るのか」「電気ができる仕組み」
- 楽器　ドップラーモジュール　画面に楽器を配置して、画像処理でオーケストラ
- 楽器　手袋　握った強さに比例して音楽が流れる「」
- 生物の動きを模倣する機械
- 心臓病患者の適度な運動のため、トルクを制御して動かす運動器具

20210921

# windowsでファイルを重い順に表示
Get-ChildItem -Path "C:\" -Force -Recurse -ErrorAction SilentlyContinue | Where-Object {$_.Length -ge 1GB} | Select-Object Fullname, Length