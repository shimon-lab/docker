ubuntu install

docker インスコ:参考 https://qiita.com/mochizukikotaro/items/ae7ae1461ea4bf495bd0

1.docker-compose導入

　sudo apt-get install docker
　sudo apt install docker-compose

参考:https://qiita.com/ohhara_shiojiri/items/0ac80924a1a8292ce511

2.docker-compose.ymlの構築

　docker-compose up -d #実行時/dockerに入ること
　wordpressは再起動必須
　docker ps による動作確認(とくにport関連要注意)

3.mysqlの設定

DBコンテナ "docker-id" にdocker execします。
　docker exec -it ~docker-id~ /bin/bash

参考:https://www.adminweb.jp/wordpress/install/index1.html
　create user 'wordpressuser'@'db' identified by 'c1o2n3t4r5o6l';
　grant all on wordpress.* to 'wordpressuser'@'db';
　grant all on wordpress.* to 'wordpressuser'@'wordpress';

4.wordpressの導入

データベース選択において使用する場所
localhost ではなく DB:3306　のように打ち込むこと
ユーザー・パスワードはmysqlでの設定を使用すること
root rootで入る（くそいやだ

5.wordpressの復活術
容量制限がかかる場合
 php -r "echo phpinfo();" | grep "php.ini"

php.iniの中の編集

　post_max_size
　upload_max_filesize

wordpress直下の .htaccess に以下を追加

　php_value memory_limit 50M
　php_value post_max_size 40M
　php_value upload_max_filesize 30M


変更

～～参考文献～～
######

docker コマンド:参考 https://blog.kasei-san.com/entry/2018/03/12/060801

ビルド
  docker-compose build # Build or rebuild services
起動、停止
  docker-compose up      # Create and start containers
  docker-compose up -d   # デーモンとして起動

  docker-compose start   # サービスを開始
  docker-compose restart # サービスを再起動
  docker-compose stop    # サービスをstop
  docker-compose kill    # サービスを強制終了
コマンド実行
# 起動中のコンテナでコマンド実行
  docker-compose exec ${service_name} ${command}

# コンテナを作成してコマンド実行(実行後コンテナを削除
  docker-compose run --rm ${service_name} ${command}
削除
  # Stop and remove containers, networks
  docker-compose down

# imageも削除
  docker-compose down --rmi all

# 名前付きvolume も削除
  docker-compose rm  --volumes
一覧
  docker-compose images               # image の一覧
  docker-compose ps                   # 起動しているコンテナの一覧
  docker-compose top ${service_name}  # サービスで実行中のプロセスの一覧
  docker-compose logs ${service_name} # View output from containers


ポート開放 :参考 https://qiita.com/toujika/items/be21d361cf80d664859c
　sudo ufw status
　sudo ufw enable
　sudo ufw allow ~number~

mysql 関連

ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2 "No such file or directory")
エラーの出てるところにmysql.sock #だめでした

sudo mysql -u root -h 127.0.0.1 -ports wordpress -p
https://www.virment.com/setup-nextcloud-docker/
db選択はここで


これ駄目ーwordpress user設定
　create database wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
　CREATE USER wordpressuser IDENTIFIED BY 'c1o2n3t4r5o6l';

参考:https://www.adminweb.jp/wordpress/install/index1.html

######

よくわからんがnextcloudのcomposeを魔改造してうまく行った.
wordpress.ymlを読み込むこと
