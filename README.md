# mysql-sandbox-20241126

## コンテナ起動
```
docker compose up -d
```

## world DB の構築
```
# sql フォルダまで移動
cd .\sql\

# コンテナ内にsqlファイルをコピー
docker compose cp .\world.sql db:root

# コンテナ内に入る
docker compose exec -it db /bin/bash

# コンテナ内でmysqlに入る（rootに入る場合）
mysql -u root -p

# DBの作成（=script読み込み）はrootで行う
source world.sql

# ユーザー情報の確認
SELECT User, Host FROM mysql.user;

# その後に指定ユーザーに権限を付与する
GRANT ALL PRIVILEGES ON world.* TO 'testuser'@'%';
```
※ world DBは [Mysql公式][mysql_official_database_world]からダウンロードしたものです

[mysql_official_database_world]:https://dev.mysql.com/doc/index-other.html
