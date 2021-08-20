# Dockerスタート

`cd Hitechlab`

`cd laradock`

`docker-compose up -d mysql phpmyadmin redis nginx`

20210102

# dockerに移動する方法

Larevel系の操作コマンドは全てdocker側でしか使えない。従ってUbuntuのコマンドラインをdockerのroot userに移動する必要がある。

`docker-compose exec workspace bash`
