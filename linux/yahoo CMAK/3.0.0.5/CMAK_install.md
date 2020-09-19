# 安裝CMAK(Cluster Manager for Apache Kafka) 3.0.0.5
## 安裝依賴套件
- JDK v11 or higher(可參考[JDK11 安裝](../../java/openJDK/11/adoptOpenJDK11_install.md))

## 下載
```
$wget https://github.com/yahoo/CMAK/releases/download/3.0.0.5/cmak-3.0.0.5.zip
```

## 解壓縮
```
$sudo mv cmak-3.0.0.5.zip /opt/
$sudo mkdir -p /opt/kafka-manager
$cd /opt
$sudo unzip cmak-3.0.0.5.zip -d /opt/kafka-manager
```

## 設定Kafka-Manager Home PATH
1. 編輯.bash_profile檔案
    ```
    $vi ~/.bash_profile
    ```
2. 把以下內容貼到檔案裡
    ```
    #set kafka-manager home path
    export KAFKA_MANAGER_HOME=/opt/kafka-manager/cmak-3.0.0.5
    export PATH=$PATH:$KAFKA_MANAGER_HOME/bin
    ```
3. 重新載入.bash_profile
    ```
    $source ~/.bash_profile
    ```
