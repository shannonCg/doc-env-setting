# ssh連線[要ssh連線方]
## 使用免密碼輸入ssh遠端連線
1. 產生private key
    ```
    $ssh-keygen -t rsa -b 4096 -C "shaice@ubuntu.com"
    > Enter a file in which to save the key (/Users/you/.ssh/id_rsa): ~/.ssh/ubuntu14_ssh
    ```
2. 在~/.ssh資料夾下建立config檔案
    ```
    $vi ~/.ssh/config
    ```
    內容如下：
    ```
    Host ubuntu14
        hostname 10.211.55.11
        user shaice
        IdentityFile ~/.ssh/ubuntu14_ssh
    ```
3. 把public key複製到遠端主機的.ssh/authorized_keys裡
    ```
    $ssh-copy-id -i ~/.ssh/ubuntu14_ssh ubuntu14
    ```
4. 遠端ssh連線測試（不需要輸入密碼）
    ```
    $ssh ubuntu14
    ```
   

