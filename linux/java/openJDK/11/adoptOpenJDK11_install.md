# 安裝java11
## 從adoptOpenJDK下載
```
$wget https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk-11.0.8%2B10/OpenJDK11U-jdk_x64_linux_hotspot_11.0.8_10.tar.gz
```

## 解壓縮
```
$sudo mv OpenJDK11U-jdk_x64_linux_hotspot_11.0.8_10.tar.gz /opt/
$sudo mkdir -p /opt/jdk
$cd /opt
$sudo tar zxvf OpenJDK11U-jdk_x64_linux_hotspot_11.0.8_10.tar.gz -C /opt/jdk
$sudo mv jdk-11.0.8+10/ jdk-11.0.8
```

## 設定JAVA PATH
1. 編輯.bash_profile檔案
    ```
    $vi ~/.bash_profile
    ```
2. 把以下內容貼到檔案裡
    ```
    #set java path
    export JAVA_HOME=/opt/jdk/jdk-11.0.8
    export PATH=$PATH:$JAVA_HOME/bin
    ```
3. 重新載入.bash_profile
    ```
    $source ~/.bash_profile
    ```
4. 驗證java是否有安裝成功
    ```
    $java -version
    ```
    ![check_java_is_available.png](adoptOpenJDK11_install/check_java_is_available.png)