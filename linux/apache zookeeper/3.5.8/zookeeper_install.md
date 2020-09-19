# 安裝zookeeper 3.5.8
## 安裝依賴套件
- JDK v1.8 or higher(可參考[JDK8 安裝](../../java/openJDK/8/adoptOpenJDK8_install.md))

## 下載
```
$wget http://apache.stu.edu.tw/zookeeper/zookeeper-3.5.8/apache-zookeeper-3.5.8-bin.tar.gz
```

## 解壓縮
```
$sudo mv apache-zookeeper-3.5.8-bin.tar.gz /opt/
$sudo mkdir /opt/zookeeper
$cd /opt
$sudo tar zxvf apache-zookeeper-3.5.8-bin.tar.gz -C /opt/zookeeper
```

## 設定Zookeeper Home PATH
1. 編輯.bash_profile檔案
    ```
    $vi ~/.bash_profile
    ```
2. 把以下內容貼到檔案裡
    ```
    #set zookeeper home path
    export ZOOKEEPER_HOME=/opt/zookeeper/apache-zookeeper-3.5.8-bin
    export PATH=$PATH:$ZOOKEEPER_HOME/bin
    ```
3. 重新載入.bash_profile
    ```
    $source ~/.bash_profile
    ```
4. 確認版本
   ```
   $zkServer.sh --version
   ```