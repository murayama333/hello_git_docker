# Dockerの基礎

## Agenda

* Docker
* コンテナ型仮想化
* MacにおけるDockerのサポート

---

## Docker

* 2013年に登場したえげつない技術
* パソコンの中で、別のパソコンを当たり前のように動かす技術（コンテナ型仮想化）
* Dockerによってアプリケーションの実行に必要なミドルウェア（Webサーバ、DBサーバ）を簡単に用意できる

<img src="img/66.png?" width="200px">

---

## コンテナ型仮想化

+ Dockerは「コンテナ」と呼ばれる小さな単位で実行環境を構築する
+ パソコンの中に複数のOSをインストールしておく必要がない
+ コンテナの作成に必要な"Dockerイメージ"はインターネット上からダウンロードできる


<img src="img/65.png?a" width="200px">

> コンテナの中にWebサーバやDBサーバといったソフトウェアが入っている、という具合です。

<img src="img/67.png?a" width="200px">

> インターネット上から必要なコンテナをダウンロードできる

---

## MacにおけるDockerのサポート

* MacでDockerを使うには Docker Desktop for Mac というアプリケーションが必要
* パソコンの中であらかじめ `Docker Desktop for Mac` を起動しておく必要がある
* 2021.12月現在、`Docker Desktop for Mac` を小規模組織であれば無料で利用できる

> 価格については以下のページを参考にしてください。 https://www.docker.com/pricing

### Docker for Desktop Macのメモリ設定について

<img src="img/68.png?a" width="600px">

> 稀にメモリが不足して起動できないというケースもあります。そのような場合は `Docker Desktop for Mac` の設定画面を確認します。

---

## Dockerコンテナの起動例1 - `hello-workd` イメージ

* ターミナルで以下のコマンドを入力する

```
% docker run hello-world
```

* コマンドを実行すると以下のように出力される

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
93288797bd35: Pull complete 
Digest: sha256:cc15c5b292d8525effc0f89cb299f1804f3a725c8d05e158653a563f15e4f685
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

> Hello from Docker! というメッセージが確認できればOKです。

---

## Dockerコンテナの起動例2 - `docker/getting-started` イメージ

* ターミナルで以下のコマンドを入力する

```
% docker run -d -p 80:80 docker/getting-started
```

* コマンドを実行すると以下のように出力される

```
Unable to find image 'docker/getting-started:latest' locally
latest: Pulling from docker/getting-started
be307f383ecc: Pull complete 
bcbca5debd8f: Pull complete 
b01ce6b852e5: Pull complete 
82b5e1c8a205: Pull complete 
a03caadc034c: Pull complete 
32ccf701d239: Pull complete 
ad05f374a3d4: Pull complete 
377fcc7dfb96: Pull complete 
Digest: sha256:86093b75a06bf74e3d2125edb77689c8eecf8ed0cb3946573a24a6f71e88cf80
Status: Downloaded newer image for docker/getting-started:latest
09d158a6cdcf264f6a5d4370863b34cc153595f0007c491a8047bb1a21f0e785
```

* ブラウザから http://localhost にアクセスすると以下のような画面が表示される

<img src="img/69.png?a" width="600px">

> Dockerコンテナ（Webサーバ）が起動しているのがわかります。

* Dockerコンテナを停止するためにコンテナIDを調べる

```
% docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED         STATUS         PORTS                NAMES
09d158a6cdcf   docker/getting-started   "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   0.0.0.0:80->80/tcp   awesome_bhabha
```

> この場合、コンテナIDは `09d158a6cdcf` となります。

* コンテナIDをを指定して、コンテナを停止する

```
% docker stop 09d15
09d15
```

> コンテナIDは先頭5文字程度でもよい（識別できればOK）

* ブラウザから http://localhost にアクセスすると以下のような画面が表示される

<img src="img/70.png?a" width="600px">

> コンテナが停止したのでアクセスできなくなります。