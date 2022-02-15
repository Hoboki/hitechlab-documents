# Dockerスタート

`cd Hitechlab`

`cd laradock`

`docker-compose up -d mysql phpmyadmin redis nginx`

20210102

# Dockerに移動する方法

Larevel系の操作コマンドは全てdocker側でしか使えない。従ってUbuntuのコマンドラインをdockerのroot userに移動する必要がある。

`docker-compose exec workspace bash`

20211118

# Docker for Windowsアンインストール

Windows PowerShell(Run as Administrator)で以下を実行
```powershell
$ErrorActionPreference = "SilentlyContinue"

kill -force -processname 'Docker for Windows', com.docker.db, vpnkit, com.docker.proxy, com.docker.9pdb, moby-diag-dl, dockerd

try {
    ./MobyLinux.ps1 -Destroy
} Catch {}
$service = Get-WmiObject -Class Win32_Service -Filter "Name='com.docker.service'"
if ($service) { $service.StopService() }
if ($service) { $service.Delete() }
Start-Sleep -s 5
Remove-Item -Recurse -Force "~/AppData/Local/Docker"
Remove-Item -Recurse -Force "~/AppData/Roaming/Docker"
if (Test-Path "C:\ProgramData\Docker") { takeown.exe /F "C:\ProgramData\Docker" /R /A /D Y }
if (Test-Path "C:\ProgramData\Docker") { icacls "C:\ProgramData\Docker\" /T /C /grant Administrators:F }
Remove-Item -Recurse -Force "C:\ProgramData\Docker"
Remove-Item -Recurse -Force "C:\Program Files\Docker"
Remove-Item -Recurse -Force "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Docker"
Remove-Item -Force "C:\Users\Public\Desktop\Docker for Windows.lnk"
Get-ChildItem HKLM:\software\microsoft\windows\currentversion\uninstall | % {Get-ItemProperty $_.PSPath}  | ? { $_.DisplayName -eq "Docker" } | Remove-Item -Recurse -Force
Get-ChildItem HKLM:\software\classes\installer\products | % {Get-ItemProperty $_.pspath} | ? { $_.ProductName -eq "Docker" } | Remove-Item -Recurse -Force
Get-Item 'HKLM:\software\Docker Inc.' | Remove-Item -Recurse -Force
Get-ItemProperty HKCU:\software\microsoft\windows\currentversion\Run -name "Docker for Windows" | Remove-Item -Recurse -Force
#Get-ItemProperty HKCU:\software\microsoft\windows\currentversion\UFH\SHC | ForEach-Object {Get-ItemProperty $_.PSPath} | Where-Object { $_.ToString().Contains("Docker for Windows.exe") } | Remove-Item -Recurse -Force $_.PSPath
#Get-ItemProperty HKCU:\software\microsoft\windows\currentversion\UFH\SHC | Where-Object { $(Get-ItemPropertyValue $_) -Contains "Docker" }
```
win+Rで`regedit`を入力し実行後、アドレスバーに`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall`を入力。その中のDocker Desktopディレクトリを削除

[Windows版Dockerの強制アンインストールと旧バージョンの再インストール方法 - Qiita](https://qiita.com/comefigo/items/957a5d555e9305add353)

[Dockerの再インストールプロンプト既存のインストールは最新のソリューションです](https://blog.csdn.net/qq_35445306/article/details/106242761)

20220211

# イメージ、ボリューム削除
```
docker rmi `docker images -q` && docker volume rm $(docker volume ls -qf dangling=true)
```

# PHPバージョン変更

## 例）8.0に変更

`update-alternatives --set php /usr/bin/php8.0`

20220214

# `docker.credentials.errors.InitializationError: docker-credential-desktop.exe not installed or not available in PATH`

解決法
```bash
echo 'export PATH="$PATH:/mnt/c/Program Files/Docker/Docker/resources/bin:/mnt/c/ProgramData/DockerDesktop/version-bin"' >> ~/.profile
source ~/.profile
```
Ubuntu再起動

それでもダメな場合 `rm ~/.docker/config.json`