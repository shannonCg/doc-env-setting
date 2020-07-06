# MD5計算(或sha1, sha512...)
常用來對檔案進行hash code計算（md5, sha1, sha512...),以偵測檔案內容是否有被異動過
通常用在偵測網路傳輸的檔案內容是否有被異動、或檔案備份的資料內容是否完整
使用方式如下：
1. 建立測試檔案test.txt
   ```
   $vi ~/test.txt
   ```
   檔案內容如下
   ```
   aaa
   ```
2. 產生test.txt的hash code
   ```
   $md5sum test.txt > test.md5
   ```
3. 驗證檔案的hash code
   ```
   $md5sum -c test.md5
   ```
   會產生驗證成功的訊息
   ![md5_success_msg.png](ubuntu_command/md5_success_msg.png)
4. 若更改檔案內容再進行驗證，會出現驗證失敗的訊息
   ```
   $vi ~/test.txt
   ```
   檔案內容如下
   ```
   baa
   ```
   ```
   $md5sum -c test.md5
   ```
   會產生驗證失敗的訊息
   ![md5_fail_msg.png](ubuntu_command/md5_fail_msg.png)