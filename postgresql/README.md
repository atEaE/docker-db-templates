# Postgresql 
PostgreSQLを使ったアプリケーション開発に使えるコンテナセットです。

# Environment
## Windows
- Windows 10 pro(LocalUser)
- Docker CE

## Image
- [postgres](https://hub.docker.com/_/postgres)

## Usage
1. `docker-compose`および`Dockerfile`が存在するフォルダに移動する。
2. `docker-compose build`コマンドでイメージのBuildを行う。
3. イメージがビルドできたら、`docker-compose up -d`コマンドでコンテナを立ち上げる。

## Tips
- Windows環境における共有ディスクエラー  
  実行ファイルが存在するフォルダを、LOCALのフォルダと共有しようとするとコンテナ起動時に下記のエラーが発生する。
  ```sh
  [81] FATAL:  data directory "/var/lib/postgresql/data" has wrong ownership      
  [81] HINT:  The server must be started by the user that owns the data directory.
  ```
  Postgresの実行ファイルを共有ディスクしてしまうと権限が違うフォルダ状のファイルを実行しようとしている扱いになり、コンテナの起動に失敗してしまう。  
  [Windows 10 is always FATAL: data directory "/var/lib/postgresql/data" has wrong ownership #435](https://github.com/docker-library/postgres/issues/435)  
  対処方法としては、今のところ自分が確認したのは2通り。  

  1. 名前付きVolumeを使ってエラー回避  
   
        ```yaml
        version: "2.2"
            services:
            db:
                build: .
                ports:
                - "5432:5432"
                restart: on-failure
                environment: 
                - TZ=Asia/Tokyo
                - POSTGRES_USER=test
                - POSTGRES_PASSWORD=password
                - POSTGRES_DB=testdb
                - POSTGRES_INITDB_ARGS=--encoding=UTF-8
                volumes:
                - ini:/docker-entrypoint-initdb.d
                - database:/var/lib/postgresql/data
            volumes:
                ini:
                driver: local
                database:
                driver: local
        ```
  2. データフォルダの場所を規定位置から変更  
   
        ```yaml
        version: "2.2"
            services:
            db:
               build: .
               ports:
                - "5432:5432"
               restart: on-failure
               environment: 
                - TZ=Asia/Tokyo
                - POSTGRES_USER=test
                - POSTGRES_PASSWORD=password
                - POSTGRES_DB=testdb
                - PGDATA=/var/lib/postgresql/data/pgdata
                - POSTGRES_INITDB_ARGS=--encoding=UTF-8
               volumes:
                - ./ini:/docker-entrypoint-initdb.d
                - ./database:/var/lib/postgresql
        ```
