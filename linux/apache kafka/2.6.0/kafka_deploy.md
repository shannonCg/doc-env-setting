# 部署kafka 2.6.0
## 部署方式
1. 單機模式（可直接執行內建的zookeeper)
2. 集群模式（建議自行安裝zookeeper)

## 部署設定
#### 單機模式
1. 啟動zookeeper (運行在獨立的shell)
```
$/opt/kafka/kafka_2.13-2.6.0/bin/zookeeper-server-start.sh /opt/kafka/kafka_2.13-2.6.0/config/zookeeper.properties
```
2. 啟動kafka server(broker) (運行在獨立的shell)
```
$/opt/kafka/kafka_2.13-2.6.0/bin/kafka-server-start.sh /opt/kafka/kafka_2.13-2.6.0/config/server.properties
```
3. 建立topic
```
$/opt/kafka/kafka_2.13-2.6.0/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test
```
觀看此broker存在的topic，會發現出現剛建立的topic: test
```
$/opt/kafka/kafka_2.13-2.6.0/bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```
觀看此broker上的topic資訊
```
$/opt/kafka/kafka_2.13-2.6.0/bin/kafka-topics.sh --describe --bootstrap-server localhost:9092 --topic test
```
4. 測試傳送訊息到topic，並觀察consumer是否有接收到
建立producer並傳送訊息到topic: test
```
$/opt/kafka/kafka_2.13-2.6.0/bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic test
```
```
message a
```
```
message b
```

建立consumer並從topic: test接收訊息(運行在獨立的shell)
```
$/opt/kafka/kafka_2.13-2.6.0/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```
![consumer-accept-message.png](kafka_deploy/consumer-accept-message.png)

#### 集群模式（三台broker）
1. 設定兩台broker的server.properties
```
$cd /opt/kafka/kafka_2.13-2.6.0
$cp config/server.properties config/server-1.properties
$cp config/server.properties config/server-2.properties
```
更改server-1.properties和server-2.properties的broker.id設定
和listeners的port設定（若broker建立在不同機器上不用改）
和log.dirs檔案位置（若broker建立在不同機器上不用改）
```
config/server-1.properties:
    broker.id=1
    listeners=PLAINTEXT://:9093
    log.dirs=/tmp/kafka-logs-1

config/server-2.properties:
    broker.id=2
    listeners=PLAINTEXT://:9094
    log.dirs=/tmp/kafka-logs-2
```
2. 啟動zookeeper
```
$/opt/kafka/kafka_2.13-2.6.0/bin/zookeeper-server-start.sh /opt/kafka/kafka_2.13-2.6.0/config/zookeeper.properties > zookeeper.log &
```
3. 啟動kafka server(broker) 
```
$/opt/kafka/kafka_2.13-2.6.0/bin/kafka-server-start.sh -daemon /opt/kafka/kafka_2.13-2.6.0/config/server.properties 
$/opt/kafka/kafka_2.13-2.6.0/bin/kafka-server-start.sh -daemon /opt/kafka/kafka_2.13-2.6.0/config/server-1.properties
$/opt/kafka/kafka_2.13-2.6.0/bin/kafka-server-start.sh -daemon /opt/kafka/kafka_2.13-2.6.0/config/server-2.properties
```