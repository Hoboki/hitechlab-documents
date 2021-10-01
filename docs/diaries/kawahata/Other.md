20210524
# ファイルの検索法(Windows)
Command Promptで検索したいディレクトリまで移動
`dir/s/b *.uf2`

20210921

# windowsでファイルを重い順に表示
Get-ChildItem -Path "C:\" -Force -Recurse -ErrorAction SilentlyContinue | Where-Object {$_.Length -ge 1GB} | Select-Object Fullname, Length