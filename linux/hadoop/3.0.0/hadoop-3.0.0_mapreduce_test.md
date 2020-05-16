# Hadoop技術手冊-Ch2 MapReduce練習
## 運行環境
- linux 14.04
- openJDK 1.8
- hadoop 3.0.0 單機模式(Standalone mode)

## 下載測試資料（每年的天氣資料）
1. 在網上的[github repository](https://gist.github.com/phstudy/1706f9635d088cc64327f50399bb7c87)下載ncdc.sh檔 
   ```
   下載完ncdc.sh並解壓縮完
   $mkdir -p ~/hadoop_practice/shell
   $chmod +x ncdc.sh
   $mv ncdc.sh ~/hadoop_practice/shell
   ``` 
1. 執行ncdc.sh來下載測試資料
   ```
   $cd ~/hadoop_practice/shell/ncdc.sh
   $./ncdc.sh
   $mv ./ncdc_data/ ~/hadoop_practice
   ```

## 建立可計算每年最高溫度的script檔
1. 建立max_temperature.sh
   ```
   $vi ~/hadoop_practice/shell/max_temperature.sh
   ```
   max_temperature.sh內容為：
   ```
    #!/usr/bin/env bash
    t1=`date +%s%N`
    for year in ../ncdc_data/*
    do
    echo -ne `basename $year .gz`"\t"
    gunzip -c $year | \
    awk '{ temp = substr($0, 88, 5) + 0;
           q = substr($0, 93, 1);
           if (temp != 9999 && q ~ /[01459]/ && temp > max) max = temp }
         END { print max }'
    done
    t2=`date +%s%N`
    total=$((t2-t1))
    echo "process time:"$(($total/1000000))"ms"
   ```
   ```
    $chmod +x max_temperature.sh
   ```

## 建立可計算每年最高溫度的mapreduce程式
1. 下載用java寫好的mapreduce程式
   ```
   $cd ~/git
   $git pull git@github.com:shannonCg/hadoop_practice.git
   ```
2. 編譯原始碼
   ```
   $cd git/hadoop_practice
   $javac -cp $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-client-core-3.0.0.jar:$HADOOP_HOME/share/hadoop/common/hadoop-common-3.0.0.jar -d ./class -sourcepath src src/mapreduce/MaxTemperature.java
   ```
3. 製作成jar檔
   ```
   $jar cvf hadoop-example.jar -C class/ .
   ```

## 比較執行script檔計算每年最高溫的結果和透過mapreduce計算的結果是否相同
1. 執行max_temperature.sh
   ```
   $cd ~/hadoop_practice/shell
   $./max_temperature.sh
   ```
   執行結果會列印在畫面上
2. 執行mapreduce任務
   若~/hadoop_practice/output資料夾已經存在，必須先刪除才可正常執行mapreduce任務
   ```
   $export HADOOP_CLASSPATH=~/git/hadoop_practice/hadoop-example.jar
   $hadoop mapreduce.MaxTemperature ~/hadoop_practice/ncdc_data/1901.gz ~/hadoop_practice/output
   ```
   查看執行結果
   ```
   $cat hadoop_practice/output/part-r-00000
   ```
3. 執行計算結果
   ```
   1901	317
   1902	244
   1903	289
   1904	256
   1905	283
   1906	294
   1907	283
   1908	289
   1909	278
   1910	294
   1911	306
   1912	322
   1913	300
   1914	333
   1915	294
   1916	278
   1917	317
   1918	322
   1919	378
   1920	294
   ```
   