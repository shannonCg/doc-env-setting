# 安裝clickhouse 21.1.2.15
## 下載
```
export LATEST_VERSION=`curl https://api.github.com/repos/ClickHouse/ClickHouse/tags 2>/dev/null | grep -Eo '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+-stable' | grep -Eo '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' | head -n 1`
wget https://github.com/ClickHouse/ClickHouse/releases/download/v$LATEST_VERSION-stable/clickhouse-common-static-$LATEST_VERSION.tgz
wget https://github.com/ClickHouse/ClickHouse/releases/download/v$LATEST_VERSION-stable/clickhouse-common-static-dbg-$LATEST_VERSION.tgz
wget https://github.com/ClickHouse/ClickHouse/releases/download/v$LATEST_VERSION-stable/clickhouse-server-$LATEST_VERSION.tgz
wget https://github.com/ClickHouse/ClickHouse/releases/download/v$LATEST_VERSION-stable/clickhouse-client-$LATEST_VERSION.tgz
```

## 解壓縮
```
sudo mv clickhouse* /opt/
sudo mkdir -p /opt/clickhouse
cd /opt
sudo tar -xzvf clickhouse-common-static-$LATEST_VERSION.tgz -C /opt/clickhouse
sudo tar -xzvf clickhouse-common-static-dbg-$LATEST_VERSION.tgz -C /opt/clickhouse
sudo tar -xzvf clickhouse-server-$LATEST_VERSION.tgz -C /opt/clickhouse
sudo tar -xzvf clickhouse-client-$LATEST_VERSION.tgz -C /opt/clickhouse
```

## 安裝
```
sudo /opt/clickhouse/clickhouse-common-static-$LATEST_VERSION/install/doinst.sh
sudo /opt/clickhouse/clickhouse-common-static-dbg-$LATEST_VERSION/install/doinst.sh
sudo /opt/clickhouse/clickhouse-server-$LATEST_VERSION/install/doinst.sh
sudo /opt/clickhouse/clickhouse-client-$LATEST_VERSION/install/doinst.sh
```

## 建立clickhouse帳號(不可登入)
```
sudo useradd -r -s /bin/false clickhouse
sudo chown clickhouse:clickhouse -R /opt/clickhouse
```