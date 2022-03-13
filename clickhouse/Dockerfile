FROM ubuntu

RUN apt-get update && \
    apt-get install -y sudo apt-transport-https ca-certificates dirmngr && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv E0C56BD4 && \
    echo "deb https://repo.clickhouse.com/deb/stable/ main/" | sudo tee \
        /etc/apt/sources.list.d/clickhouse.list && \
    apt-get update && \
    apt-get install -y clickhouse-server clickhouse-client

CMD service clickhouse-server start