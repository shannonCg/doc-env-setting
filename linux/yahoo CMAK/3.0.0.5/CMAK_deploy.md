# 部署CMAK(Cluster Manager for Apache Kafka) 3.0.0.5
## 前置動作
- 已啟動Kafka (可參考[kafka 2.6.0 安裝](../../apache%20kafka/2.6.0/kafka_install.md)和[kafka 2.6.0 部署](../../apache%20kafka/2.6.0/kafka_deploy.md))
- [已安裝cmak](CMAK_install.md)

## 部署方式
  - [Standalone模式](#standalone模式)

## Standalone模式
1. 設定設定檔（$KAFKA_MANAGER_HOME/conf/application.conf）
```
$sudo vi $KAFKA_MANAGER_HOME/conf/application.conf
```
```
cmak.zkhosts="10.211.55.14:2181,10.211.55.15:2181,10.211.55.16:2181"
```
2. 建立log檔存放位置的資料夾
```
$sudo mkdir $KAFKA_MANAGER_HOME/logs
$sudo chown -R shaice:shaice $KAFKA_MANAGER_HOME
```
3. 建立kafka manager啟動指令檔
```
$vi $KAFKA_MANAGER_HOME/bin/cmak_startup.sh
```
```
#!/usr/bin/env bash
nohup cmak -Dconfig.file=$KAFKA_MANAGER_HOME/conf/application.conf -Dhttp.port=8080 -Dapplication.home=$KAFKA_MANAGER_HOME > $KAFKA_MANAGER_HOME/logs/kafka-manager.log 2>&1 &
```
```
$chmod +x $KAFKA_MANAGER_HOME/bin/cmak_startup.sh
```
4. 建立kafka manager停止指令檔
```
$vi $KAFKA_MANAGER_HOME/bin/cmak_shutdown.sh
```
```
#!/usr/bin/env bash
PID_PATH=$KAFKA_MANAGER_HOME/RUNNING_PID
kill -9 $(cat $PID_PATH)
if [ -f $PID_PATH ]
then 
    echo -e "Delete CMAK RUNNING_PID !\n"
    rm $PID_PATH
fi
```
```
$chmod +x $KAFKA_MANAGER_HOME/bin/cmak_shutdown.sh
```
5. 啟動kafka manager
```
$cmak_startup.sh
$tail -f $KAFKA_MANAGER_HOME/logs/kafka-manager.log
```
6. 關閉kafka manager
```
$cmak_shutdown.sh
```