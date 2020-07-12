# 安裝hadoop 3.0.0
## 下載
```
$wget https://archive.apache.org/dist/hadoop/common/hadoop-3.0.0/hadoop-3.0.0.tar.gz
```

## 解壓縮
```
$sudo mv hadoop-3.0.0.tar.gz /opt/
$sudo mkdir /opt/hadoop
$cd /opt
$sudo tar zxvf hadoop-3.0.0.tar.gz -C /opt/hadoop
```

## 設定HADOOP PATH
1. 編輯.bash_profile檔案
    ```
    $ vi ~/.bash_profile
    ```
2. 把以下內容貼到檔案裡
    ```
    #set hadoop path
    export HADOOP_HOME=/opt/hadoop/hadoop-3.0.0
    export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
    ```
3. 重新載入.bash_profile
    ```
    $source ~/.bash_profile
    ```
4. 驗證hadoop是否有安裝成功
    ```
    $hadoop version
    ```
    ![check_hadoop_is_available.png](hadoop-3.0.0_install/check_hadoop_is_available.png)