## JDK8 的JVM相關指令
### 檢查JVM預設參數
```
$java -XX:+PrintCommandLineFlags -version
```
### 檢查JVM的GC分配
```
$java -XX:+PrintGCDetails -version
```
### 列出jar包中的文件清单
```
$jar tf test-0.0.1-SNAPSHOT.jar
```
### 解析出jar包中的文件
```
$jar xf finance-1.0.0.jar BOOT-INF/classes/application.yml
```