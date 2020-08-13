# 環境構築

docker, docker-compose
Laradockを使う  

https://laradock.io/  



```
mkdir melpit-workspace
cd melpit-workspace
git clone -b v11.0 https://github.com/Laradock/laradock.git
cd laradock
cp env-example .env
```

`.env`を編集

```
APP_CODE_PATH_HOST=../melpit
```

```
docker-compose up -d nginx mysql phpmyadmin
docker-compose exec workspace bash
```

```
composer create-project --prefer-dist laravel/laravel="7.25.*" .
exit
```

rootで作成される問題
```
sudo chown -R kuni:kuni melpit
```

アプリの`.env`を編集する

```
DB_HOST=mysql
```

表示されればOK

`http://localhost/`


## メモ

docker-composeでエラー
docker-composeのバージョンアップが必要だった
```
Traceback (most recent call last):
  File "bin/docker-compose", line 6, in <module>
  File "compose/cli/main.py", line 72, in main
  File "compose/cli/main.py", line 128, in perform_command
  File "compose/cli/main.py", line 491, in exec_command
  File "compose/cli/main.py", line 1469, in call_docker
  File "subprocess.py", line 339, in call
  File "subprocess.py", line 800, in __init__
  File "subprocess.py", line 1462, in _execute_child
  File "os.py", line 810, in fsencode
TypeError: expected str, bytes or os.PathLike object, not NoneType
[3261] Failed to execute script docker-compose
```