# 部署hadoop 3.0.0
## 設定檔介紹
1. hadoop的設定檔都是xml格式，而主要的設定檔都放在$HADOOP_HOME下的etc/hadoop中
2. 主要的設定檔有：
   - core-site.xml: common的屬性參數設定
   - hdfs-site.xml: HDFS的屬性參數設定
   - mapred-site.xml: MapReduce的屬性參數設定
   - yarn-site.xml: YARN的屬性參數設定


## 部署方式
1. 單機模式(Standalone mode): 適用於開發mapreduce程式時的測試環境
2. 偽分散模式(Pseudo-distributed mode): 單機運行，但可模擬小規模的叢集
3. 完全分散模式(Fully distributed mode): 叢集運行


## 部署設定
#### 單機模式(Standalone mode)
不需額外設定，設定檔的參數預設值就是單機模式，且不執行任何背景服務

#### 偽分散模式(Pseudo-distributed mode)
1. 複製*-site.xml的設定檔，分離原設定檔
   ```
   $mkdir hadoop_config
   $cp $HADOOP_HOME/etc/hadoop/*-site.xml hadoop_config/
   $cp hadoop-3.0.0/etc/hadoop/log4j.properties hadoop_config/
   $cp hadoop-3.0.0/etc/hadoop/hadoop-env.sh hadoop_config/
   $cp hadoop-3.0.0/etc/hadoop/workers hadoop_config/
   $cp hadoop-3.0.0/etc/hadoop/capacity-scheduler.xml hadoop_config/
   ```
2. 設定環境變數HADOOP_CONF_DIR給複製出來的設定檔位置
   ```
   $vi .bash_profile
   ```
   ```
   # set hadoop config directory
   export HADOOP_CONF_DIR=~/hadoop_config
   ```
   ```
   $source .bash_profile
   ```
3. 更改設定檔
   - 添加core-site.xml設定
        ```
        $vi $HADOOP_CONF_DIR/core-site.xml
        ```
        ```
            <configuration>
                <property>
                    <name>fs.defaultFS</name>
                    <value>hdfs://localhost:9000</value>
                </property>
            </configuration>
        ```
   - 添加hadoop-env.sh設定
        ```
        $vi $HADOOP_CONF_DIR/hadoop-env.sh
        ```
        ```
        export JAVA_HOME=/opt/jdk8u232-b09
        ```
   - 添加hdfs-site.xml設定
        ```
        $vi $HADOOP_CONF_DIR/hdfs-site.xml
        ```
        ```
            <configuration>
                <property>
                    <name>dfs.replication</name>
                    <value>1</value>
                </property>
                <property>
                    <name>dfs.namenode.secondary.http-address</name>
                    <value>localhost:9868</value>
                </property>
                <property>
                    <name>dfs.namenode.secondary.https-address</name>
                    <value>localhost:9869</value>
                </property>
            </configuration>
        ```
   - 添加yarn-site.xml設定
        ```
        $vi $HADOOP_CONF_DIR/yarn-site.xml
        ```
        ```
            <configuration>
                <property>
                    <name>yarn.nodemanager.aux-services</name>
                    <value>mapreduce_shuffle</value>
                </property>
            </configuration>
        ```
    - 添加mapred-site.xml設定
        ```
        $vi $HADOOP_CONF_DIR/mapred-site.xml
        ```
        ```
            <configuration>
                <property>
                    <name>mapreduce.framework.name</name>
                    <value>yarn</value>
                </property>
            </configuration>
        ```
4. 設定ssh
    - 安裝ssh
        ```
        $sudo apt-get install ssh
        ```
    - 啟動免密碼登入
        ```
        $ssh-keygen -t rsa -P '' -f ~/.ssh/hadoop_ssh
        $cat ~/.ssh/hadoop_ssh.pub >> ~/.ssh/authorized_keys
        $chmod 0600 ~/.ssh/authorized_keys
        ```
        ```
        $vi .ssh/config
        ```
        ```
        Host localhost
        hostname localhost
        IdentityFile ~/.ssh/hadoop_ssh
        ```
    - 測試是否可免密碼登入
        ```
        ＄ssh localhost
        ```
5. 格式化HDFS檔案系統
   ```
   $hdfs namenode -format
   ```
6. 啟動服務(依序啟動hdfs、yarn、mapreduce jobhistory)
   - 啟動hdfs
        ```
        $start-dfs.sh
        ```
        確認hdfs是否有正常啟動:
        1. 從機器上查看
            ```
            $jps
            ```
            會印出
            ```
            DataNode
            NameNode
            SecondaryNameNode
            ```
        2. 從瀏覽器上查看
            http://10.211.55.11:9870
   - 啟動yarn
        ```
        $start-yarn.sh
        ```
        確認hdfs是否有正常啟動:
        1. 從機器上查看
            ```
            $jps
            ```
            會印出
            ```
		    ResourceManager
		    NodeManager
            ```
        2. 從瀏覽器上查看
            http://10.211.55.11:8088
   - 啟動mapreduce jobhistory
        ```
        $mapred --daemon start historyserver
        ```
        確認hdfs是否有正常啟動:
        1. 從機器上查看
            ```
            $jps
            ```
            會印出
            ```
            JobHistoryServer
            ```
        2. 從瀏覽器上查看
            http://10.211.55.11:19888
7. 關閉服務(依序關閉mapreduce jobhistory、yarn、hdfs)
    ```
    $mapred --daemon stop historyserver
    $stop-yarn.sh
    $stop-dfs.sh
    ```