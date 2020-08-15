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

Laradockの`.env`を編集

```
APP_CODE_PATH_HOST=../melpit
```

xdebugも？
```
PHP_FPM_INSTALL_XDEBUG=true
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
APP_NAME=Melpit
DB_HOST=mysql
DB_PASSWORD=root
```

ロケールとタイムゾーンの変更
`config/app.php`

```
    'timezone' => 'Asia/Tokyo',
    'locale' => 'ja',
```

ストレージのリンクを貼る

```
php artisan storage:link
```

DBを作成する
```
http://localhost:8081/
```
サーバ mysql
ユーザ root
パスワード root

laravelでDB作成

Laravel動作確認

`http://localhost/`


# 認証機能

## 会員登録・ログイン・ログアウト

```
docker-compose exec workspace bash
composer require laravel/ui:2.1.0
php artisan ui --auth
npm install
npm run dev
php artisan migrate
```

Modelの移動
seederとfactory

```
php artisan make:seeder UserSeeder
php artisan make:factory UserFactory
```

（実装）

バリデーションを日本語化
https://github.com/caouecs/Laravel-lang/blob/master/src/ja/validation.php

```
mkdir resources/lang/ja
curl -o resources/lang/ja/auth.php https://raw.githubusercontent.com/caouecs/Laravel-lang/master/src/ja/auth.php
curl -o resources/lang/ja/pagination.php https://raw.githubusercontent.com/caouecs/Laravel-lang/master/src/ja/pagination.php
curl -o resources/lang/ja/passwords.php https://raw.githubusercontent.com/caouecs/Laravel-lang/master/src/ja/passwords.php
curl -o resources/lang/ja/validation-inline.php https://raw.githubusercontent.com/caouecs/Laravel-lang/master/src/ja/validation-inline.php
curl -o resources/lang/ja/validation.php https://raw.githubusercontent.com/caouecs/Laravel-lang/master/src/ja/validation.php
```


画面を開いて確認

```
http://localhost/register
```

## パスワードリセット

mailtrapのセットアップ

リセットメールの日本語化

```
php artisan vendor:publish --tag=laravel-notifications
```

## プロフィール編集

scss, jsのビルド方法
javascriptのデバッグ方法

```
php artisan make:request Mypage/Profile/EditRequest
```

intervention imageの使い方

```
composer require intervention/image:2.5.1
```

```
php artisan migrate:refresh --seed
```

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
