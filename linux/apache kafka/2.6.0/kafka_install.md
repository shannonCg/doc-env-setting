# 安裝kafka 2.6.0
## 安裝依賴套件
- JDK v1.8 or higher(可參考[JDK8 安裝](../../java/openJDK/8/adoptOpenJDK8_install.md))
  
## 下載
```
$wget http://ftp.twaren.net/Unix/Web/apache/kafka/2.6.0/kafka_2.13-2.6.0.tgz
```

## 解壓縮
```
$sudo mv kafka_2.13-2.6.0.tgz /opt/
$sudo mkdir -p /opt/kafka
$cd /opt
$sudo tar zxvf kafka_2.13-2.6.0.tgz -C /opt/kafka
```

## 設定Kafka Home PATH
1. 編輯.bash_profile檔案
    ```
    $vi ~/.bash_profile
    ```
2. 把以下內容貼到檔案裡
    ```
    #set kafka home path
    export KAFKA_HOME=/opt/kafka/kafka_2.13-2.6.0
    export PATH=$PATH:$KAFKA_HOME/bin
    ```
3. 重新載入.bash_profile
    ```
    $source ~/.bash_profile
    ```
4. 確認版本
   ```
   $kafka-server-start.sh --version
   ```
