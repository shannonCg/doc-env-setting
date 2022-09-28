# 安裝clickhouse 22.3.2.2
## 下載
```
export LATEST_VERSION=22.3.2.2
wget https://github.com/ClickHouse/ClickHouse/releases/download/v$LATEST_VERSION-lts/clickhouse-common-static-$LATEST_VERSION.tgz
wget https://github.com/ClickHouse/ClickHouse/releases/download/v$LATEST_VERSION-lts/clickhouse-common-static-dbg-$LATEST_VERSION.tgz
wget https://github.com/ClickHouse/ClickHouse/releases/download/v$LATEST_VERSION-lts/clickhouse-server-$LATEST_VERSION.tgz
wget https://github.com/ClickHouse/ClickHouse/releases/download/v$LATEST_VERSION-lts/clickhouse-client-$LATEST_VERSION.tgz
```

## 解壓縮
```
sudo mkdir -p /opt/clickhouse22
sudo tar -xzvf clickhouse-common-static-$LATEST_VERSION.tgz -C /opt/clickhouse22
sudo tar -xzvf clickhouse-common-static-dbg-$LATEST_VERSION.tgz -C /opt/clickhouse22
sudo tar -xzvf clickhouse-server-$LATEST_VERSION.tgz -C /opt/clickhouse22
sudo tar -xzvf clickhouse-client-$LATEST_VERSION.tgz -C /opt/clickhouse22
```

## 安裝
```
sudo /opt/clickhouse22/clickhouse-common-static-$LATEST_VERSION/install/doinst.sh
sudo /opt/clickhouse22/clickhouse-common-static-dbg-$LATEST_VERSION/install/doinst.sh
sudo /opt/clickhouse22/clickhouse-server-$LATEST_VERSION/install/doinst.sh
sudo /opt/clickhouse22/clickhouse-client-$LATEST_VERSION/install/doinst.sh
```

## 建立clickhouse帳號(不可登入)
```
sudo useradd -r -s /bin/false clickhouse
sudo chown clickhouse:clickhouse -R /opt/clickhouse22
```