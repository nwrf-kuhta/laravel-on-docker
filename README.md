# laravel-on-docker

## About

A local development environment for applications using Laravel. <br>
A container exists with the following configuration.

Laravelを使ったアプリケーションのローカル開発環境です。<br>
以下の構成でコンテナが存在しています。

- web
- mysql
- redis

In addition, the version of each package is as follows.

また、それぞれのパッケージのバージョンは以下のようになっています。

| PackageName | Version |
| --- | --- |
| nginx | 1.16.1 |
| php | 7.4.9 |
| mysql | 5.7.31 |
| redis | 6.0.6 |

You can access MySQL and Redis from the web container.

WebコンテナからMySQLやRedisにアクセスすることができます。

## Usage

### Introduction

First, clone the repository.

まずはリポジトリをクローンします。

```
git clone https://github.com/nwrf-kuhta/laravel-on-docker
```

Then copy env-testing and create an env file. <br>
Change the application code path and database settings accordingly.

次に `.env-testing`をコピーして`.env`ファイルを作成します。 <br>
アプリケーションコードのパスや、データベースの設定を適宜変更します。

```
cp -rp .env-testing .env
```

### Container construction

To start the container, execute the following command on the terminal.

コンテナを起動するにはターミナル上で以下のコマンドを実行します。

```
docker-compose up -d --build
```

After building the container, you can start the armillar by executing the following command.

コンテナ構築後は以下のコマンドを実行することで、渾天を起動することができます。

```
docker-compose up -d
```

### Accessing other containers from the web container

First, access the web container.

まずはWebコンテナにアクセスします。

```
docker-compose exec web bash
```

You can access MySQL with the following command.

以下のコマンドでMySQLへアクセスできます。

```
mysql -hmysql -udeveloper -p
```

You can also access Redis with the following command.

また、以下のコマンドでRedisへアクセスすることができます。

```
redis-cli -h redis
```
