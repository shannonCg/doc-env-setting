# 部署clickhouse 21.1.2.15
## 前置動作
- [已安裝clickhouse](./cliclhouse_install.md)

## 部署方式
  - [Standalone模式](#standalone模式)

## Standalone模式
1. 建立clickhouse-server執行的pid檔存放位置的資料夾
```
sudo mkdir /var/run/clickhouse-server
sudo chown clickhouse:clickhouse -R /var/run/clickhouse-server
```
2. 修改config.xml
```
sudo vi /etc/clickhouse-server/config.xml
```
修改成參數值
```
<log>/opt/clickhouse/log/clickhouse-server/clickhouse-server.log</log>
<errorlog>/opt/clickhouse/log/clickhouse-server/clickhouse-server.err.log</errorlog>

<listen_host>0.0.0.0</listen_host>

<path>/opt/clickhouse/</path>
<tmp_path>/opt/clickhouse/tmp/</tmp_path>
<user_files_path>/opt/clickhouse/user_files/</user_files_path>

<local_directory>
    <!-- Path to folder where users created by SQL commands are stored. -->
    <path>/opt/clickhouse/access/</path>
</local_directory>

<format_schema_path/opt/clickhouse/format_schemas/</format_schema_path>
```
3. 啟動clickhouse server
```
sudo -u clickhouse /usr/bin/clickhouse-server --config-file /etc/clickhouse-server/config.xml --pid-file /var/run/clickhouse-server/clickhouse-server.pid --daemon
```
4. 啟動clickhouse client測試
預設用使用者default連本地clickhouse server
```
clickhouse-client
```
或
```
clickhouse-client -h localhost -d default -u default
```
5. 停止clickhouse server
```
sudo kill -9 $(sudo -u clickhouse cat /run/clickhouse-server/clickhouse-server.pid)
```