# Contents
- [Dockerとは](#dockerとは)
    - [コンテナとは](#コンテナとは)
    - hoge
-  [Docker Composeで実際にコンテナを作ってみよう](#docker-composeで実際にコンテナを作ってみよう)
    - [Docker Compsoseファイルを作成する](#docker-composeファイルを作成する)
- VSCode+Dockerで開発環境を構築
    - 拡張機能のインストール
    - VSCodeで実行するプログラム環境をコンテナにする
    - 
- [dockerコマンドチート表](#dockerコマンドチート表)
    - [Note](#note)

</br>

# Dockerとは
Dockerとは，[コンテナ](#コンテナとは)を作成・実行するためのソフトウェア．（は？）

## コンテナとは
コンテナとは，**「アプリ&ファイルシステムを隔離する特殊なプロセス」** のこと．
（**プロセス**とは，OS上で動作している１つ１つの処理（動作中の個々のプログラム）のこと．）

要するに，コンテナ技術を使うことで，**そのプロセスの中だけが別マシンで動いているような状態になる** ．

</br>

# Docker Composeで実際にコンテナを作ってみよう
このセクションでは実際にDocker ComposeでApacheコンテナを作成する．
（とりあえず作ってみることが目的なので，詳しいことは理解しなくてもOK．）

- 作成するApacheコンテナの情報
    | コンテナ作成に必要な項目 | 設定値 |
    | ----- | ----- |
    | 使用するイメージ | httpd（バージョンは2.4） |
    | ポート番号 | 8080.80 |

## Docker Composeファイルを作成する
Docker Composeでコンテナを作るには`compose.yaml`が必要．
デフォルトではカレントディレクトリにある`compose.yaml`が読み込まれ，
Docker Composeのプロジェクト名にはカレントディレクトリの名前が使用される．

- ディレクトリの構造
    <pre>
    .
    └── apache
        └── compose.yaml
    </pre>





</br>

# dockerコマンドチート表

dockerコマンドはすべて `docker 対象 操作` の順に入力する．

| 対象 | 操作 | オプション |
| --- | --- | --- |
| `image` | `build` | hgoe |
|         | `ls`    | hgoe |
|         | `pull`  | hgoe |
|         | `push`  | hgoe |
|         | `rm`    | hgoe |
| `container` | `run`   | hgoe |
|             | `start` | hgoe |
|             | `stop`  | hgoe |
|             | `rm`    | hgoe |
| `network` | `create` | hgoe |
|           | `ls`     | hgoe |
|           | `rm`     | hgoe |
| `volume` | `create` | hgoe |
|          | `ls`     | hgoe |
|          | `rm`     | hgoe |
| `compose` | `up`    | hgoe |
|           | `run`   | hgoe |
|           | `start` | hgoe |
|           | `stop`  | hgoe |
|           | `down`  | hgoe |

### Note
- dockerコマンドには**古い書き方（例えば`docker container run`ではなく`docker run`，`docker image pull`ではなく`docker pull`など）が存在**
- **Docker ComposeにもV1とV2が存在**
    - コマンドはV1では`docker-compose`，V2では`docker compose`
    - yamlファイルの名前はV1では`docker-compose.yaml`が使われていたが，V2では`compose.yaml`が推奨されている