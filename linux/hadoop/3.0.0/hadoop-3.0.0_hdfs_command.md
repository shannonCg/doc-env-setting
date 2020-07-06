# HDFS Command說明
## 查詢檔案區塊資訊
```
$hdfs fsck / -files -blocks
```
## 基本檔案操作
- 在HDFS檔案系統上建立一個資料夾
    建立單一資料夾
    ```
    $hdfs dfs -mkdir /user
    ```
    建立此路徑結構的資料夾(若上層目錄不存在也會一同建立)
    ```
    $hdfs dfs -mkdir -p /user/shaice
    ```
- 在HDFS檔案系統上顯示資料夾內檔案列表
    顯示"/"資料夾下的檔案列表
    ```
    $hdfs dfs -ls /
    ```
    顯示"/"資料夾下的檔案列表(包含子資料夾下所有的檔案列表)
    ```
    $hdfs dfs -ls -R /
    ```
    顯示"/user/操作的使用者"資料夾下的檔案列表
    ```
    $hdfs dfs -ls .
    ```
- 從本機檔案系統複製一個檔案到HDFS上
    會把本地的test.txt上傳到HDFS的"/tmp"的資料夾下
    ```
    $hdfs dfs -copyFromLocal ~/test.txt hdfs://localhost:9000/tmp/test.txt
    $hdfs dfs -copyFromLocal ~/test.txt /tmp/test2.txt
    ```
    會把本地的test.txt上傳到HDFS的"/user/操作的使用者"的資料夾下
    ```
    $hdfs dfs -copyFromLocal ~/test.txt test3.txt
    ```
- 從HDFS檔案系統複製一個檔案到本地
    ```
    $hdfs dfs -copyToLocal /tmp/test.txt ~/test.txt.bak
    ```
