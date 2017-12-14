# Hexo Blog (tpwilovepanda.github.io)
## 安裝需求
安裝 Hexo 檢查下列條件
* [Node.js](http://nodejs.org/)
* [Git](http://git-scm.com/)
* [GitHub](https://github.com/)

## GitHub
Github create a new repository

## 設定 SSH
開啟 Git 工具「Git Bash」，如何開啟呢？只要在想要的資料夾按右鍵選擇「Git Bash here」的選項，點擊即可。
設置「使用者名稱」和「電子信箱」
```bash
$ git config —global user.name
$ git config —global user.email
```
生成「ssh密鑰」輸入命令，用戶文件夾下會有新的文件夾「`.ssh`」裡面有「`id_rsa`」和「`id_rsa.pub`」
```bash
$ ssh-keygen -t rsa -c
```
> 「`id_rsa`」是私鑰，要妥善保管，「`id_rsa.pub`」是公鑰

## Github 添加公鑰
1. Settings（設置）選項
1. 選擇「SSH and GPG keys」
1. 選擇「New SSH key」，將「id_rsa.pub」中的內容複製到 Key 文本框
1. 選擇「Add SSH key」

## 測試 SSH
開啟`「Git Bash」`，`$ ssh -t git@github.com`，接下來會出來下面的確認信息：
```bash
The authenticity of host 'github.com (207.97.227.239)' can't be established. 
RSA key fingerprint is 17:24:ac:a5:76:28:24:36:62:1b:36:4d:eb:df:a6:45.
Are you sure you want to continue connecting (yes/no)?
```
輸入 yes，然後顯示如下信息則 OK（其中的 tpwilovepanda 是用戶名）。
```bash
Hi tpwilovepanda! You've successfully authenticated, 
but GitHub does not provide shell access.
```

## 安裝 Hexo
1. 安裝「Hexo 套件」至全域環境
    * `$ npm install -g hexo-cli`
1. 「初使化」與「創建部落格資料夾」
    * `$ hexo init blog`
1. 進入部落格資料夾
    * `$ cd blog`
1. 安裝「Hexo 套件」所需要的套件，根據`package.json`安裝相關依賴（dependency）
    * `$ npm install`
    * `$ npm install hexo-deployer-git --save # 安裝 git 佈署套件`
1. 啟動 Hexo
    * `$ hexo server`
1. 啟動瀏覽器
    * http://localhost:4000

## 設定部署 Hexo
### 編輯配置文件連結遠端倉庫
用編輯器中打開 Hexo 配置文件`_config.yml`，找到下面內容：
```yaml
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
type:
```
添加 Github 倉庫信息：
```yaml
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
type: git
## Github 遠端倉庫位置
repo: git@github.com:tpwilovepanda/tpwilovepanda.github.io.git 
## Github 選擇佈署分支
branch: master
```
> type、repo、branch 的前面有兩個空格，後面的:後面有一個空格

## 小叮嚀: 記得安装 hexo 佈署到 git 的套件
要使用`hexo deploy`佈署到 GitHub 上面，需要安裝`hexo-deployer-git`，如果沒有安裝此佈署套件，可能在`hexo deploy`會有錯誤提示。  
hexo-deployer-git：套件功能是使`git`同步代碼到`git`倉庫的套件。
```bash
npm install hexo-deployer-git --save
```

## 安裝主題
預設主题是 **landscape**，如果不喜歡，LovePanda 推薦以下主題
* [Hueman](https://github.com/ppoffice/hexo-theme-hueman)
* [Material](https://github.com/viosey/hexo-theme-material)
* [NexT](https://github.com/iissnan/hexo-theme-next)

將主題源碼下載到 themes 文件夾中，修改主题配置文件 `_config.yml`，此配置文件在主題文件夾下面。  
例如：`theme: landscape`為`theme: hueman`，許多安裝主題都有自己的詳細文件，請參考詳細文件設定。

## 認識 Hexo 命令
### Hexo 常用命令
```bash
$ hexo new [layout] <title> # 新建文章
$ hexo generate # 創建 hexo blog 所需文件
$ hexo server # 模擬伺服器
$ hexo deploy # 佈署到 GitHub
$ hexo clean # 清除 hexo blog 所需文件
$ hexo version # hexo 版本
```

### Hexo 命令缩寫
* **`hexo g`**：`hexo generate`
* **`hexo s`**：`hexo server`
* **`hexo d`**：`hexo deploy`

> For Visual Studio Code 快捷鍵
> `hexo clean '&&' hexo g '&&' hexo s`
> `hexo clean '&&' hexo g '&&' hexo d`

## 配置文件說明
網站配置文件是在根目錄下的`_config.yml` 文件，是`yaml`格式的。所有的配置項後面的冒號（:）與值之間要有一個空格。[官方配置文件說明](https://hexo.io/zh-tw/docs/configuration.html)

## 撰寫文章
```bash
$ hexo new "new article" #新建文章
```
`source`文件 > `_post`文件 > `new-article.md`，會看到新建文章，可以使用`Markdown`開始撰寫文章。

## 佈署到 GitHub 上
```bash
$ hexo deploy # 佈署到 GitHub
```

## Hexo Blog 備份
實現不同電腦上 Hexo 部落格的同步，主要想法是利用 GitHub 的分支概念在`username.github.io`版本庫中額外增設分支（branch），GitHub 規定要顯示的網頁分支必須為`master`，因此考慮增設分支`hexo`用以存放部落格原始碼：

* master: 利用`hexo deploy`佈署 Hexo 產生的靜態頁面到 GitHub 的`master`分支上，存放部落格要顯示的網頁。
* hexo: 利用`git push origin hexo`推送到 GitHub 的`hexo`分支上，存放部落格原始碼。

```bash
$ git init # 重新初始化 Git
$ git remote add origin "https://github.com/your/name.github.io.git" # 連線 GitHub 遠程倉庫
$ git add . # 暫存全部檔案，注意！請先設定好 .gitignore
$ git commit -m "你想要紀錄的資訊" # Git 紀錄
$ git branch hexo # 建立 hexo 分支
$ git checkout hexo # 切換到 hexo 分支
$ git push origin hexo # 推送到 hexo 分支
```