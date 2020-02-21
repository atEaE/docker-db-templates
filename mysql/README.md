# Postgresql 
MySQLを使ったアプリケーション開発に使えるコンテナセットです。

# Environment
## Windows
- Windows 10 pro(LocalUser)
- Docker CE

## Image
- [mysql](https://hub.docker.com/_/mysql)

## Usage
1. `docker-compose`および`Dockerfile`が存在するフォルダに移動する。
2. `docker-compose build`コマンドでイメージのBuildを行う。
3. イメージがビルドできたら、`docker-compose up -d`コマンドでコンテナを立ち上げる。

