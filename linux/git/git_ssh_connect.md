# 線上git服務的ssh連線設定
1. 建立.ssh資料夾
   ```
   $mkdir ~/.ssh
   ```
2. 取得ssh連線的private key&public key檔案後放在~/.ssh資料夾下
3. 在~/.ssh資料夾下建立config檔案
   ```
   $cd ~/.ssh
   $vi config
   ```
   內容如下：
   ```
   Host gitlab.com
      hostname gitlab.com
      IdentityFile ~/.ssh/git_ssh
   Host github.com
      hostname github.com
      IdentityFile ~/.ssh/git_ssh
   ```
4. 把private key加入到 keychain
   1. 下載keychain
   ```
   $sudo apt-get install keychain
   ```
   2. 在$HOME/.bashrc檔加入下列設定
   ```
   keychain git_ssh
   . ~/.keychain/`uname -n`-sh
   ```
   重載設定
   ```
   $source ~/.bashrc
   ```
5. 測試ssh連線是否不用輸入密碼
   - 測試github的ssh連線
      ```
      $ssh -T git@github.com
      ```
      ![test-github-ssh.png](git_ssh_connect/test-github-ssh.png)
      <br>
   - 測試gitlab的ssh連線
      ```
      $ssh -T git@gitlab.com
      ```
      ![test-gitlab-ssh.png](git_ssh_connect/test-gitlab-ssh.png)
