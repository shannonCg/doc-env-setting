# 部署zookeeper 3.5.8
## 前置動作
[已安裝zookeeper](zookeeper_install.md)

## 部署方式
  - [Standalone模式](#standalone模式)
  - [Clustered模式](#clustered模式三台zookeeper)

## Standalone模式
1. 建立設定檔($ZOOKEEPER_HOME/conf/zoo.cfg)
```
$sudo vi $ZOOKEEPER_HOME/conf/zoo.cfg
```
設定檔內容為：
```
tickTime=2000
dataDir=/tmp/zookeeper
clientPort=2181
```
2. 建立log檔存放位置的資料夾
```
$sudo mkdir $ZOOKEEPER_HOME/logs
$sudo chmod -R a+w $ZOOKEEPER_HOME/logs
```
3. 啟動zookeeper server
```
$zkServer.sh start
```
4. 連上zookeeper server
```
$zkCli.sh -server 127.0.0.1:2181
```
5. 對zookeeper做節點操作
   - 查詢節點目錄
    ```
    ls /
    ```
   - 建立znode節點和存放資料到節點上
    ```
    create /zk_test data_str
    ```
   - 取得znode節點存放的資料
    ```
    get -s /zk_test 
    ```
   - 更新znode節點存放的資料
    ```
    set /zk_test data_str_new
    ```
   - 刪除znode節點
    ```
    delete /zk_test
    ```
   - 離開對zookeeper server的連線
    ```
    quit
    ```
6. 停止zookeeper server
```
$zkServer.sh stop
```

## Clustered模式（三台zookeeper）
1. 建立設定檔($ZOOKEEPER_HOME/conf/zoo.cfg)
```
$sudo cp $ZOOKEEPER_HOME/conf/zoo_sample.cfg $ZOOKEEPER_HOME/conf/zoo.cfg 
```
```
$sudo vi $ZOOKEEPER_HOME/conf/zoo.cfg 
```
```
dataDir=/opt/zookeeper/data

#最後增加以下內容：
server.1=10.211.55.14:2888:3888
server.2=10.211.55.15:2888:3888
server.3=10.211.55.16:2888:3888
```
2. 在zoo.cfg中dataDir設定的檔案位置增加myid檔案
```
$sudo mkdir -p /opt/zookeeper/data
$sudo chown -R shaice:shaice /opt/zookeeper/data
$vi /opt/zookeeper/data/myid
```
在10.211.55.14寫
```
1
```
在10.211.55.15寫
```
2
```
在10.211.55.16寫
```
3
```
3. 建立log檔存放位置的資料夾
```
$sudo mkdir $ZOOKEEPER_HOME/logs
$sudo chmod -R a+w $ZOOKEEPER_HOME/logs
```
4. 啟動zookeeper server
```
$zkServer.sh start
```
5. 停止zookeeper server
```
$zkServer.sh stop
```