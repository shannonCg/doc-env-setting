# 軟體開發環境設定
## 建立檔案搜尋列表的別名
1. 編輯zprofile檔案
    ```
    $ vi ~/.zprofile
    ```
2. 把以下內容貼到檔案裡
    ```
    alias ll='ls -alF'
    ```
3. 重新載入zprofile
    ```
    $ source ~/.zprofile
    ```

## 安裝homebrew
[homebrew管網](https://brew.sh/index_zh-tw)

安裝指令如下：
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
## 建立git專案的ssh連線
1. 產生private key
   ```
    $ssh-keygen -t rsa -b 4096 "github註冊信箱"
    > Enter a file in which to save the key (/Users/you/.ssh/id_rsa):  ~/.ssh/git_ssh
    > Enter passphrase (empty for no passphrase): github登入密碼
    ```
2. 建立config檔
   ```
   $vi ~/.ssh/config
   ```
   ```
   Host *
     UseKeychain yes
     AddKeysToAgent yes
   Host gitlab.com
     hostname gitlab.com
     IdentityFile ~/.ssh/git_ssh
   Host github.com
     hostname github.com
     IdentityFile ~/.ssh/git_ssh
   ```
3. 把private key加入到 keychain
   ```
   $ssh-add -K ~/.ssh/git_ssh
   ```
4. 把public key加入到github/gitlab帳號設定裡
   複製public key檔案的內容
   ```
   $pbcopy < ~/.ssh/git_ssh.pub
   ```
   把複製好的內容貼到帳號的ssh設定裡


## 安裝IDE: Visual Studio Code 
安裝Visual Studio Code

[Visual Studio Code下載點](https://code.visualstudio.com/docs/setup/setup-overview)

安裝常用套件
- Markdown
    ![Markdown All in One.png](install_dev_env/Markdown%20All%20in%20One.png)
    ![Markdown Preview Enhanced.png](install_dev_env/Markdown%20Preview%20Enhanced.png)

## 各程式語言開發環境設定
[springboot專案開發環境設定](install_springboot_dev_env.md)
[angular專案開發環境設定](install_angular_dev_env.md)