## JDK8 的JVM相關指令
### 檢查JVM預設參數
```
$java -XX:+PrintCommandLineFlags -version
```
### 檢查JVM的GC分配
```
$java -XX:+PrintGCDetails -version
```