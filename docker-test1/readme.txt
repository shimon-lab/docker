# docker-compose.ymlからビルドする
docker-compose build 

# ymlに書かれてるコンテナを起動する　
docker-compose run
# backgroundで起動する場合、
# -dオプションをつける

# コンテナの確認
docker-compose ls

# コンテナの終了
docker-compose kill

#コンテナの削除
docker-compose rm