# hadoop 3.0.0部署
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
