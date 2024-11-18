# Contents
- [Dockerとは](#dockerとは)
    - [コンテナとは](#コンテナとは)
    - [Dockerの基本的な使用手順](#dockerの基本的な使用手順)
        - [なぜ毎回コンテナを削除するのか](#なぜ毎回コンテナを削除するのか)
        - [コンテナ内のデータの永続化](#コンテナ内のデータの永続化)
            - ボリューム
            - バインドマウント
- [Dockerfileでイメージを作ってみる](#Dockerfileでイメージを作ってみる)
    - [Dockerfileに記述できる主な命令](#Dockerfileに記述できる主な命令)
-  [Docker Composeでコンテナを作ってみる](#docker-composeでコンテナを作ってみる)
    - [Docker Compsoseファイルを作成する](#docker-composeファイルを作成する)
- VSCode+Dockerで開発環境を構築
    - 拡張機能のインストール
    - VSCodeで実行するプログラム環境をコンテナにする
    - hoge
- [dockerコマンドチート表](#dockerコマンドチート表)
    - [Note](#note)

</br>

# Dockerとは
Dockerとは，[コンテナ](#コンテナとは)を作成・実行するためのソフトウェア．（は？）

## コンテナとは
コンテナとは，**「アプリ&ファイルシステムを隔離する特殊なプロセス」** のこと．
（**プロセス**とは，OS上で動作している１つ１つの処理（動作中の個々のプログラム）のこと．）

要するに，コンテナ技術を使うことで，**そのプロセスの中だけが別マシンで動いているような状態になる** ．

## Dockerの基本的な使用手順
 Dockerの基本的な使用手順は以下の通り．
[Docker Desktop](https://www.docker.com/ja-jp/products/docker-desktop/)が起動していないと`docker`コマンドが認識されないため注意．

1. imageを作成（Dockerfileを使ってbuild，またはDockerHubからpull）
2. imageからcontainerを作成
3. containerを起動し仮想環境の中で作業
4. containerを停止・削除

- Docker基本コマンド  
    <img src='./figures/docker_summary01.png' width=500px>

### なぜ毎回コンテナを削除するのか
**「作っては削除」が基本**なのは，コンテナの作成・削除コストが非常に低いから．
この **「作っては削除」** が簡単に行えるのがコンテナの魅力でもある．
ただし，コンテナを削除するとコンテナ内のデータも削除されるため，必要なデータは，ファイルのバインドマウントなどで，[データを永続化](#コンテナ内のデータの永続化)する必要がある．

#### Note
- イメージやコンテナが増えてくるとストレージを圧迫するため，不要なものはその都度削除する（DockerHubやDockerfileから簡単に再現できる）
- ローカルでの開発用途の利用であれば停止したコンテナを再利用するケースはある

### コンテナ内のデータの永続化
永続化の方法には，
1. ボリューム
2. バインドマウント



</br>

# Dockerfileでイメージを作ってみる
Dockerfileとは．．．

## Dockerfileに記述できる主な命令
| 命令 | 意味 |
| --- | --- |
| `FROM`       | 元となるイメージを指定する |
| `RUN`        | イメージのビルド時に実行するコマンド |
| `CMD`        | コンテナの起動時に実行するコマンド |
| `EXPOSE`     | 公開するポート番号．ただし，あくまでどのポートを公開したいかという意図を示すためのものであり，実際に公開するには`docker container run`で`-p`を指定するか，Docker Composeファイルで`ports`を記述する必要がある． |
| `COPY`       | イメージにファイルやフォルダをコピーする |
| `ADD`        | イメージにファイルやフォルダをコピーする．tarの展開などが可能など，COPYより高機能だが，COPYがが推奨されている． |
| `ENTRYPOINT` | コンテナの起動時に実行するコマンド．基本的にコマンドの上書きはできない |
| `WORKDIR`    | 作業ディレクトリを指定する．ディレクトリが存在しない場合，ディレクトリを作成． |


</br>

# Docker Composeでコンテナを作ってみる
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